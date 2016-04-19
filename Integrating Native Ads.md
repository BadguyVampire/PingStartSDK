# Integrating Native Ads
Native ads let you easily monetize your app in a way that’s consistent with its existing design. The PingStart SDK gives you access to an ad’s individual assets so you can lay them out the way you want to; that way, the ad looks and feels like the rest of your app.

#### Prerequisites:
Before integrating native ads in your app, you’ll need to go through the steps in our [Getting Started Guide](http://baidu.com) to create an account on PingStart and integrate the SDK into your project.
#### Load native ads in your app:
Step1. Set up your native ad layout:

Start by defining an XML layout for how an ad should look inside your app’s feed. The native ads contain these informations like title, description, icon, cover, interactive action and so on, so you should define a suitable XML layout to show the native ads.

Step2. Declare an instance variable for native in your Activity code:

        PingStartNative native = new PingStartNative(this, YOUR_PUBLISH_ID, YOUR_SOLT_ID);
###### Note:
1. YOUR_PUBLISHER_ID is necessary and can't be null or an empty character, it's the unique identification of your app, you can get it when you create an account on PingStart;
2. YOUR_SLOT_ID is also necessary and can't be null or an empty character, it's the unique identification which ads integrated in your app, you can get it when you create an ad unit.

Step3. Using the listener interface:

`PingStartNative` provides a listener interface, `NativeListener`, which you can use to stay informed about ad lifecycle events. `NativeListener` includes the following methods:

        //Sent when the native has successfully retrived an ad.
        public void onAdLoaded(BaseNativeAd ad);
        
        // Sent when native has failed to retrieve an ad. You can use the ErrorCode value to diagnose the cause of failure.
        public void onAdError(String error);
        
        //Sent when the user has tapped on the native
        public void onAdClicked();
Step4. Place ads in your layout and register it:
    
        // In this method, you can place ads into your layout, and register which view response the click action
        public void onAdLoaded(BaseNativeAd ad){
            titile.setText(ad.getTitle());
            description.setText(ad.getDescription());
            button.setText(ad.getAdCallToAction());
            ..............
            // get PingStartNative at step2, you can replace the view with any view of your native layout
            native.registerNativeView(View view);
        }
Step5. Destroy native:
        
        In your `Activity`'s `onDestroy()` method, you should call the `PingStartNative`'s `destroy()` method to destroy native ad like this:
        
        @Override
        public void onDestroy(){
            if (native != null){
                native.destroy();
            }
            super.onDestroy();
        }

