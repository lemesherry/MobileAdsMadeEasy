# Documentation for implementing "Ads Package"

### Prerequisites: <br>

> **1.** Install latest versions of Google AdMob unity package (or at-least version 8.x.x), you can find all versions here: [Google Mobile Ads](https://github.com/googleads/googleads-mobile-unity/releases). <br>
> **2.** Install the Google Native ads unity package from here: [Google Native Ads Guide](https://developers.google.com/admob/unity/native) or directly from here: [Google Native ads unity package](https://dl.google.com/googleadmobadssdk/GoogleMobileAds-native.unitypackage). <br>
> **3.** Try to resolve dependencies by going to the External dependency manager settings. In your unity project click on _Assets/External Dependency Manager/Android Resolver/Resolve_ (external dependency manager is always automatically installed with google mobile ads package). <br>
> **4.** Add your google ads app ID in google ads package by going to menu _Assets/Google Mobile Ads/Settings_. <br>

###### Note3: A known issue: If in-case you are building project for Android then sometimes when you import google ads packge, the external dependency manager might throw an error saying "Assets/ExternalDependencyManager/Editor/1.2.176/Google.IOSResolver.dll' will not be loaded due to errors" since you are not building project for iOS, A simple solution for that would be to disable iOS resolver validate references by going to directory Assets/ExternalDependencyManager/versionNumber/Google.IOSResolver and then uncheck the box "Validate References" and hit apply, then it should be resolved.

* Add "**Ads Manager**" script to any GameObject in
  unity scene, so that the script can initialize all the Ads when game loads up. "_Note: you can add this script only by clicking on add component and typing AdsManager on any gameObject_" <br>
  or Create A new script and paste these functions in them to initialize ads before showing them.
```csharp
      /// Note: You can set all Ads ID in the window menu inside Assets/MobileAdsMadeEasy/settings/>
      
      private bool _isAdLoaded;
      
      public void Awake() {

         // ★彡[ When true all events raised by GoogleMobileAds will be raised on the Unity main thread. The default value is false. ]彡★
         MobileAds.RaiseAdEventsOnUnityMainThread = true;

         _isAdLoaded = false;
         
         // ★彡[ Initializing the Google Mobile Ads SDK. ]彡★
         MobileAds.Initialize( initStatus => {
            // ★彡[ This callback is called once the MobileAds SDK is initialized. ]彡★

            if( initStatus != null ) {

               _isAdLoaded = true;
               BannerAd.LoadAd( AdPosition.Top );
               BannerAd.LoadAdMedium( AdPosition.Bottom );
               // ★彡[ Initializing 5 ads at the beginning so that we always have at-least a single ad when there are too many rewarded ad requests back to back ]彡★
               RewardedAd.InitializeAds( 5 );
               InterstitialAd.LoadAd();
            }
         } );

         InitializeNativeAd();
      }

      /// <summary>
      /// An asynchronous function to make sure that we await for the mobileAds SDK to initialize so that we can load native ads without any issues.
      /// </summary>
      private async void InitializeNativeAd() {

         if( _isAdLoaded ) {
            
            NativeAds.InitializeAds();
            return;
         }

         await Task.Delay( 500 );
         InitializeNativeAd();
      }
```

* Call the Ads function like the examples below:

```csharp
      // ★彡[ Calling examples ]彡★
      
      /// <summary>
      /// Example for calling interstitial Ad.
      /// </summary>
      public static void ShowInterstitialAd() {

         InterstitialAd.ShowAd();
      }
      
      /// <summary>
      /// Example for calling banner Ad.
      /// </summary>
      public static void ShowBannerAd() {

         BannerAd.ShowBannerAd( true );
         // ★彡[ similarly pass the false value in above method to hide the banner ]彡★
      }
      
      /// <summary>
      /// Example for calling medium banner Ad/Rect Ad.
      /// </summary>
      public static void ShowBannerAdMedium() {

         BannerAd.ShowBannerAdMedium( true );
         // ★彡[ similarly pass the false value in above method to hide the banner ]彡★
      }
      

      /// <summary>
      /// Example for calling rewarded Ad.
      /// </summary>
      public static void ShowRewardedAd() {

         RewardedAd.ShowAd( hasRewarded => {

            if( hasRewarded ) {

               // ★彡[ Give reward ]彡★
            }

            Debugger.Log( hasRewarded? "Rewarded" : "Not Rewarded", LogSeverity.Ads );
         } );
      }

      /// <summary>
      /// Example for calling native Ad.
      /// </summary>
      public static void ShowNativeAd() {

         // ★彡[ Example for calling a native ad object as a UI element (with desired size and position) ]彡★
         var adPosition2D = new Vector2( 0, -200 ); // x & y position in rect
         var adSize2D = new Vector2( 300, 100 ); // width & height
         
         NativeAds.ShowAd( adPosition2D, adSize2D );
         
         // ★彡[ Example for calling a native ad object as a gameObject (with desired size and position) ]彡★
         var adPosition = new Vector3( 0, 5, 1 );
         var adSize = new Vector3( 2, 2, 2 );
         
         NativeAds.ShowAd( adPosition, adSize );
      }

```

<br>
<br>
Note: You can set all Ads ID in the window menu inside Assets/MobileAdsMadeEasy/settings.
