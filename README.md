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

            //Set the user
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

```cs
    UserIQSDK.SharedInstance.InitWithAPIKey("<YOUR_API_KEY>", "EMP124", "Alex", "alex@useriq.com",1,"Acme Corp", "2017-04-21",null);
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
