# Getting Started

You're 4 steps away from adding great in-app support to your Xamarin App.

**Content**
- Download UserIQSDK
- Add UserIQSDK to your Xamarin project
- Initializing UserIQSDK in your app
- Start using UserIQSDK

# Step 1: Download UserIQSDK

Download [UserIQSDK.dll](./Android/UserIQSDK.dll)

# Step 2: Add UserIQSDK to your Xamarin project
- Add the UserIQSDK.dll to the References in your Android specific project. 

# Step 3: Initializing UserIQSDK in your app

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

# Step 4: Start using UserIQ

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

```java
boolean isContextualHelpShown = UserIQSDK.ShowCtxHelp();
```

Contextual help will only be shown when the current screen is tagged. If the current screen is not tagged then the above API will return `false`
