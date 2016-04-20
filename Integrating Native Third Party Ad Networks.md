#  Integrating Native Third Party Ad Networks
The PingStart SDK can mediate any native ad network SDK through our custom events capabilities. As a developer, this allows you to serve ads from multipe networks through our NativeResponse class. In order to mediate third party native ads, you must have already integrated [PingStart native ads](http://baidu.com).

We offer 'plug-and-play' native ad integrations for the following networks:
* [Facebook Audience Network](https://developers.facebook.com/docs/audience-network/)

## Supported Native Third-Party Integration Guide
##### 1. Add the custom event files to your project
* We pre-built adaptors for what we supported mediations, it's in the form of Jar,download the jar which ads you want to include into your app,you can get them [here]().
* Integrating the SDK that we supported with their integrating guide, and set up the corresponding network campaigns and target the proper ad units at the corresponding dashboard.
 
##### 2. Display native ads as usual
No changes are required to any of the other code! Be sure to setup corresponding network campaigns and target the proper ad units in your PingStart account.

## Unsupported Native Third-Party Integration Guide
### Writing Custom Events for Unsupported Ad Networks(Native)
Custom events allow you to support native ad networks not bundled with the PingStart SDK.

#### Quick Start for Native Ads
1. Create a subclass of CustomEventNative in your application.
2. Override the `loadNative(Context,Map, CustomEventNativeListener)` method and implement code that request a native ad.
3. Override the `registerNativeView(View)` method and implement code that response an ad click. 
4. Override the `unregisterNativeView()` method and implement code that clean ad click event.
5. Override the `reLoad()` method and implement code that when ads need to reload.
6. Override the `destroy()` method if your custom event requires any sort of cleanup.
7. When your ad loads successfully, you must notify PingStart of the event and display your ad by calling the `onNativeAdLoaded(BaseNativeAd)` method on the `CustomEventNativeListener` object (passed in loadAd).
8. Similarly, you must notify the `CustomEventNativeListener` object when your ad fails to load by calling the `onNativeAdFailed(String)` method on the listener object.
9. (Optional) Notify the listener object of other ad lifecycle event via the corresponding methods on `CustomEventNativeListener`.

        public void onNativeClicked();
        
10. After loading the native ad from the network, initialize a *`BaseNativeAd`* object, and using the folling setter methods:
* `setTitle` for a title string
* `setDescription` for a description string
* `setIconUrl` for an icon-size image
* `setCoverImageUrl` for a large image
* `setCallToAction` for a call to action string
* `setNetworkName` for a network name string

11. In your `Activity`'s XML layout, create a suitable layout for your native ads.

Once you've completed these steps, the PingStart SDK will be able to cause your *`CustomEventNative`* subclass to be instantiated at the proper time while your application is running. You do not need to instantiate any of these subclassed in your application code. *Note:* the PingStart SDK will cause a new *`CUstomEventNative`* object ti be instantiated on every ad call, so you can safely make changes to the custom event object's internal state between calls.