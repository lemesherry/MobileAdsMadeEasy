# Mobile Ads Made Easy - Package By LemeSherry

This package is used to integrate Admob ads (Ads type: Rewarded, Interstitial, Banner & Native) for Android & iOS.

## Instructions on how to add this package in unity.

### Prerequisites: <br>

> **1.** Install latest versions of Google AdMob unity package (or at-least version 8.x.x), you can find all versions here: [Google Mobile Ads](https://github.com/googleads/googleads-mobile-unity/releases). <br>
> **2.** Install the Google Native ads unity package from here: [Google Native Ads Guide](https://developers.google.com/admob/unity/native) or directly from here: [Google Native ads unity package](https://dl.google.com/googleadmobadssdk/GoogleMobileAds-native.unitypackage). <br>
> **3.** Try to resolve dependencies by going to the External dependency manager settings. In your unity project click on _Assets/External Dependency Manager/Android Resolver/Resolve_ (external dependency manager is always automatically installed with google mobile ads package). <br>
> **4.** Add your google ads app ID in google ads package by going to menu _Assets/Google Mobile Ads/Settings_. <br>

### Getting started: <br>


> **1.** Open the
> add ![iconAdd](https://github.com/lemesherry/MobileAdsMadeEasy/assets/84338798/0e27ddc6-4e08-43cc-be1d-bcadf849695a)
> menu in the Package Manager’s toolbar. <br>
> **2.** The options for adding packages appear. <br>
> ![upm-ui-giturl](https://github.com/lemesherry/MobileAdsMadeEasy/assets/84338798/77b5323f-c7af-471b-88a3-0fd168b3b50c)
>
> **3.** Select Add package from git URL from the add menu. A text box and an Add button appear. <br>
> **4.** Enter a valid Git URL in the text box (in this case its: https://github.com/lemesherry/AdsPackageForUnity.git)
> and click Add. <br>
> ![image](https://github.com/lemesherry/AdsPackageForUnity/assets/84338798/38e6f25b-a5c5-4c65-8607-aa1efe26ecf1) <br>
> **5.** After the package is imported, add each and every Ad Id by going into the menu Assets/MobileAdsMadeEasy/Settings.

###### Note: have a look into [documentation](https://github.com/lemesherry/MobileAdsMadeEasy/blob/main/Documentation/Documentation.md) to get to know how to use ads calling in your unity project.

###### Note2: This package uses newtonsoft-json library as a dependency for some json serialization, so if you have imported this package manually in your project you should not forget to also add newtonsoft-json library at-least v3.x.x.

###### Note3: A known issue: If in-case you are building project for Android then sometimes when you import google ads packge, the external dependency manager might throw an error saying "Assets/ExternalDependencyManager/Editor/1.2.176/Google.IOSResolver.dll' will not be loaded due to errors" since you are not building project for iOS, A simple solution for that would be to disable iOS resolver validate references by going to directory Assets/ExternalDependencyManager/versionNumber/Google.IOSResolver and then uncheck the box "Validate References" and hit apply, then it should be resolved. 

###### And that's it, unity will now automatically install dependencies and associated packages with it, and you can find the package contents inside "packages" folder in unity project root directory.

