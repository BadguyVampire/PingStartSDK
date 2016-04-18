
# Integrating Banner Ads
Banner ads usually appear at the top or bottom of your app's screen. Adding one to your app takes just a few lines of code.
##### Prerequisites:
Before integrating banner ads in your app, you'll need to go through the steps in our [Getting Start Guide](http://baidu.com) to create an account on PingStart and integrate the SDK into your project.
##### Load banner ads in your app:
Step1. Declare an instance variable for banner in your code like this:

        PingStartBanner banner = new PingStartBanner(Context context,String YOUR_PUBLISHER_ID,String YOUR_SLOT_ID);
###### Note:
1. YOUR_PUBLISHER_ID is necessary and can't be null or a empty character, it's the  unique identification of your app, you can get it when you create an account on PingStart.
2. YOUR_SLOT_ID is also necessary and can't be null or a empty character, it's the unique identification which ads integrated in your app, you can get it when you create an ad unit. 

Step2. Using the listener interface:

'PingStartBanner' provides a listener interface, 'BannerListener', which you can use to stay informed about ad lifecycle events. 'BannerAdListener' includes the following methods:
        
        //Sent when the banner has successfullyretrieved an ad.
        public void onAdLoaded(View view);
        
        //Sent when the banner has failed to retrieve an ad. You can use the ErrorCode value to diagnose the cause of failure.
        public void onAdError(String error);
        
        //Sent when the user has tapped on the banner.
        public void onAdClicked();
To listen for events, you'll need to use the method 'setAdListener(BannerListener listener)' in PingStartBanner as it's being created(see Step 1);

        banner.setAdListener(BannerListener listener);
        
After all above steps, you can show a banner ad in your app successfully.




