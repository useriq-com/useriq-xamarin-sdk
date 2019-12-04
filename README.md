# Getting Started

You're 4 steps away from adding great in-app support to your Xamarin App.

**Content**

- Download UserIQSDK
- Add UserIQSDK to your Xamarin project
- Initializing UserIQSDK in your app
- Start using UserIQSDK

## Step 1: Download UserIQSDK

Download the corresponding dll files

- Android - [UserIQSDK.dll](./Android/UserIQSDK.dll)
- iOS - [UserIQ.iOS.Xamarin.dll](./iOS/UserIQ.iOS.Xamarin.dll)

## Step 2: Add UserIQSDK to your Xamarin project

#### Android

Add the UserIQSDK.dll to the References in your Android specific project.

#### iOS

Add the UserIQ.iOS.Xamarin.dll in the iOS specific project under the `References` folder as a new reference.

## Step 3: Initializing UserIQSDK in your app

#### Android

```cs
using Com.Useriq.Sdk;

namespace UserIQXamarinSampleApp {

    public class MainActivity : Activity {

        protected override void OnCreate(Bundle savedInstanceState) {

            // Initialize the UserIQSDK
            UserIQSDK.Init(Application, "API_KEY");

            // Set user. Can be called from any other activity AFTER user login. 
            // NOTE: SDK will be initalized only after the user has been set 
            UserIQSDK.User user = new UserIQSDK.UserBuilder()
                .SetId("EMP124")
                .SetAccountId("1")
                .SetAccountName("Acme Corp")
                .SetName("Alex")
                .SetEmail("alex@useriq.com")
                .AddParams("location", "Atlanta")
                .Build();
            UserIQSDK.SetUser(user);
        }
    }
}
```

#### iOS

Set the api key of the SDK in  `FinishedLaunching` method of `AppDelegate.cs`.

```cs
    // Set API Key
    UserIQSDK.SharedInstance.InitWithAPIKey("<your-api-key>");
```

Set the user once you have the user info.
>  NOTE: SDK will be initalized only after the user has been set

```cs
    // Set user
    UserIQSDK.SharedInstance.SetUserId("EMP124", "Alex", "alex@useriq.com", "1", "Acme Corp", "2017-04-01", null);
```

## Step 4: Start using UserIQ

### Disable Fab

Floating Action Button (FAB) can be permanently disabled by calling the `DisableFAB()` from the sdk.

```cs
UserIQSDK.DisableFAB();
```

This can be called anytime before or after initializing the SDK. Once invoked, it will hide the FAB & also overrides the enableFAB sent from the dashboard. (ie) if this method is called on the SDK, this will take precendence over configuration from dashboard!

### Show Helpcenter

Helpcenter can be programatically invoked by calling `UserIQSDK.ShowHelpCenter()`

```cs
bool isHelpCentreShown = UserIQSDK.ShowHelpCentre();
```

When Modal window or popup is active, helpcenter can't be shown. In those cases, above API will return `false`

### Show Contextual help

Contextual help can be shown by calling `UserIQSDK.ShowCtxHelp()`

```cs
bool isContextualHelpShown = UserIQSDK.ShowCtxHelp();
```

Contextual help will only be shown when the current screen is tagged. If the current screen is not tagged then the above API will return `false`

## Step 5 : Logout

If a user logs out, the user can be reset to anonymous user just by calling the `logout` API. Make sure this method is called when the user logs out, so that login screen tracking and other information not related to the user does not get linked to the user.

- iOS
    ```cs
        UserIQSDK.SharedInstance.Logout();
    ```

- Android
    ```cs
        UserIQSDK.LogOut();
    ```

## ⚠ Important  

It is recommended that `AutomationId` is added to the view in `.xaml` files for views which needs tracking. This can be used in the dashboard for identifying features and screens

```xml
<Button Text="Checkout" AutomationId="checkoutBtn" />
```

## Android Only

In case of android apps, make sure that views that needs click tracking has click tracker attached to it or `clickable` is set to `true`. 

For view with `clickable` set as `false`,UserIQSDK won't be able to track the clicks due to limitation of Android SDK.

# API & USAGE

For more details on API & usage, please refer to [wiki page](https://github.com/useriq-com/useriq-xamarin-sdk/wiki)

# ChangeLog

[Android Changelog](https://github.com/useriq-com/android-sdk/blob/master/CHANGELOG.md)

[iOS Changelog](https://github.com/useriq-com/ios-sdk/blob/master/CHANGELOG.md)


