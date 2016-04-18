# Integrating Interstitial Ads
Interstitial Integration for Android Interstitial ads provode full-screen experiences, commonly inccorporating rich media to offer a higher level of interactivity compared to banner ads. Interstitial are typically shown during natural tranitions in your app, e.g.after completing a game level,or while waiting for a new view to load. You can use the 'PingStartInterstitial' object and it's associated listeners to fetch and display interstitial ads in your app.

### Prerequisites:
Before integrating interstitial ads in your app, you'll need to go through the steps in our [Getting Started](http://baidu.com) to create an account on PingStart and integrate the SDK into your project.

### Load interstitial ads in your app:
The PingStart SDK provides a custom class, `PingStartInterstitial`,that handles fetching and displaying fullscreen interstitial ads. To ensure a smooth experience, you should pre-fetch the content as soon as your `Activity` is created,then display it if the fetch was successful. IN the `Activity` in which you want to show the interstitial ad, declare a `PingStartInsterstitial` instance variable:

        private PingStartInterstitial mInterstitial;
`PingStartInterstitial` provides a listener interface, `InterstitialListener`, which you'll use to stay informed about ad lifecycle events. Make sure your `Activity` implements the `InterstitialListener` interface. In your `Activity`'s `onCreate()` method,instantiate the `PingStartInterstitial` using the context and the Publisher Id and Slot Id you created in the [Getting Started](http://baidu.com).     
    
        mInterstitial = new PingStartInterstitial(this,YOUR_PUBLISHER_ID,YOUR_SLOT_ID);
Next,register your activity as the InterstitialListener:
        
        //here "this" refers to the listener that you implements on this activity
        mInterstitial.setAdListener(this);
Now you're ready to display an ad. Displaying the ad takes four steps:
1. In your `onCreate()` method, call `loadAd()` to begin prefetching the ad. it's important to fetch interstitial ad content well before you plan to show it, since it often incorporates rich media and may take some time to load. We suggest prefetching when your `Activity` is first created, but you may also choose to do it based on events in your app, like beginning a game level.
2. When you're ready to display your ad, use `PingStartInterstitial.isReady()` to check whether the interstitial was successfully prefetched.
3. If `isReady()` returns ture, display the interstitial by calling the `show()` method. You can add logic to the other interstitial lifecycle methods to handle what should happen when your user interacts with the ad- e.g. resuming your game `onAdClosed()`.
4. Lastly, rememeber to call `destroy()` on the interstitial in your `Activity`'s `onDestroy()` method. Yourcompleted `Activity` code shuold look something like this:

        public class ExampleActivity extents Activity implements InterstitialListener{
            private PingStartInterstitial mInsterstitial;
        
            @Override
            protected void onCreate(Bundle saveInstanceState){
               super.onCreate(saveInstanceState);
               setContentView(R.layout.main);
               mInterstitial = new PingStartInterstitial(this,YOUR_PUBLISH_ID,YOUR_SLOT_ID);
               mInterstitial.setAdListener(this);
               mInterstitial.load();
           }
           
            @Override
            protected void onDestroy(){
               if (mInterstitial != null){
                  mInterstitial.destroy();
                  super.onDestroy();
              }
           }
           
            // InterstitialListener methods
            @Override
            public void onAdClosed(){}
        
            @Override
            public void onAdError(String error){}
        
            @Override
            public void onAdLoaded(){
                if (mInterstitial.isReady()){
                mInterstitial.show();
                } else {
                // other code
                }
            }
        
            @Override
            public void onAdClicked(){}
        }