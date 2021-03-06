---
layout: post
title: "Android Lollipop Sends Multiple BroadcastReceivers for Telephone State Changes"
modified:
categories: blog
excerpt:
tags: [android]
image:
  feature:
date: 2014-11-14
---

I’ve been working on an Android app named [Urgent Call][urgentcall] that alerts people when they’ve received several calls from the same person in a short time. To do this, the app needs to be able to detect when calls come in and who they’re coming from. Android made a change to the way this works in the Lollipop release that broke the functionality of my app. In this post, I’ll explain what changed and how to work around it.

If you haven’t used a BroadcastReceiver to detect phone state changes before, you might want to check out [this tutorial][android-labs] from Android Labs first. If you’re newer to Android, haven’t used BroadcastReceivers at all, or want a more in-depth look at the topic, vogella provides a [more detailed tutorial][vogella] covering this as well.

## What Changed

Below is a simple BroadcastReceiver that detects changes to the phone state and logs them. The BroadcastReceiver is called anytime the phone state changes; namely, when the phone starts ringing, the call is dismissed, or the call is answered. The String grabbed from the intent is the state itself.

{% highlight java %}
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.telephony.TelephonyManager;
import android.util.Log;

public class PhoneStateBroadcastReceiver extends BroadcastReceiver {

  public static final String TAG = "PHONE STATE";
  private static String mLastState;
  
  @Override
  public void onReceive(Context context, Intent intent) {
    String state = intent.getStringExtra(TelephonyManager.EXTRA_STATE);
    Log.e(TAG, state);
    }
  }  
}
{% endhighlight %}

On API levels 19 and below, receiving and ending a phone call will produce log output like this:

|Time                 |Tag          |Message  |
|:-------------------:|:-----------:|--------:|
|11-13 21:59:39.678   |PHONE STATE  |RINGING  |
|11-13 21:59:43.624   |PHONE STATE  |IDLE     |


However, starting with API 21[^1], the log output looks like this:

|Time                 |Tag          |Message  |
|:-------------------:|:-----------:|--------:|
|11-13 22:01:02.876   |PHONE STATE  |RINGING  |
|11-13 22:01:03.620   |PHONE STATE  |RINGING  |
|11-13 22:01:13.349   |PHONE STATE  |IDLE     |
|11-13 22:01:13.616   |PHONE STATE  |IDLE     |

For whatever reason, when the phone state changes on Lollipop, two BroadcastReceivers are received. This can have some adverse implications if your code doesn’t take this possibility into account.

This caused some issues in the app that I'm working on. In my app, when a BroadcastReceiver is received for an incoming call and the app detects that the same person has called several times in a row, it starts up a background service that plays a special ringtone. When the call is answered or dismissed, the ringtone should stop playing and the service should stop. My app wasn't robust to the changes in Lollipop. On Lollipop, when the incoming call was answered or ignored, the ringtone would keep playing until the phone was restarted. The ringtone would also have an echo effect. My app was starting its background service twice, and only successfully stopping one of them.

## A Solution

An easy solution to this problem is to keep track of the phone state each time your BroadcastReceiver is called. If the state is the same as it was last time, then nothing’s changed and you should ignore it.

You can do this by declaring a static String that keeps track of the phone state. It needs to be static so that the variable is shared among all instances of your BroadcastReceiver.

{% highlight java %}
private static String mLastState;
{% endhighlight %}

You’ll want to update this state anytime the BroadcastReceiver is called.

{% highlight java %}
mLastState = state;
{% endhighlight %}

Within the BroadcastReceiver, make sure your logic is only executed if the phone state is different than it was before.

{% highlight java %}
if (!state.equals(mLastState)) {
  doMyStuff(); 
}
{% endhighlight %}

Make sure that you either update the mLastState variable within or after the if statement. If you update the previous state to the new state before checking their equality, you'll run into some issues.

That’s it! Below is the same code snippet from above, but modified to be robust to one, two, or as many sequential BroadcastReceivers that future versions of Android decide to send it.

{% highlight java %}
public class PhoneStateBroadcastReceiver extends BroadcastReceiver {

  public static final String TAG = "PHONE STATE";
  private static String mLastState;
  
  @Override
  public void onReceive(Context context, Intent intent) {
    String state = intent.getStringExtra(TelephonyManager.EXTRA_STATE); 

    if (!state.equals(mLastState)) {
      mLastState = state;
      Log.e(TAG, state);  
    }
  }  
}
{% endhighlight %}

The log output from a phone call will look like this:

|Time                 |Tag          |Message  |
|:-------------------:|:-----------:|--------:|
|11-13 22:06:36.298   |PHONE STATE  |RINGING  |
|11-13 22:06:39.207   |PHONE STATE  |IDLE     |

The app is now successfully ignoring the redundant BroadcastReceivers.

[^1]: On API 20, the Android L Preview, I'd see the state change twice to idle, but only once to ringing.

[urgentcall]:   http://play.google.com/store/apps/details?id=com.mmarvick.uc_lite
[android-labs]: http://androidlabs.org/short-experiments/broadcast-receivers/do-something-when-the-phone-rings/
[vogella]:      http://www.vogella.com/tutorials/AndroidBroadcastReceiver/article.html
