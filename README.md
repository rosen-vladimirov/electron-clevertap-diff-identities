# electron-quick-start

**Demonstrates an issue with merging identities**

This project demonstrates an issue with identities in CleverTap.



### Issue description
The desired workflow is to have an application with sign in and sign out operations.
When application starts for the first time, Sign In screen is shown. User can doe different actions there, like using Google Login or creating account. All of them have tracking in CleverTap. As user is not identified yet, they are still anonymous.

Once Signed in, the email of the user is pushed in CleverTap. All consecutive actions are tracked in the profile, where the email is set.

At some point the user signs out and gets back to the Sign In screen. At this point we want to start tracking in new anonymous profile. After user signs in (probably with different email), the Email of this profile will be set in CleverTap. If there's an existing profile with this email, we want to merge them.

However, no matter what we do, after Sign Out is clicked, the events are still tracked in the previously used profile (the one which was signed in).
We have tried:
- calling onUserLogin without params
- calling onUserLogin with Identity - this introduces issue as we want later to merge the accounts, so it is not an option
- removing the WZRK_G key from localStorage as suggested by support
- removing all WZRK keys from localStorage
### Setup
1. Clone the repo:
```
git clone https://github.com/rosen-vladimirov/electron-clevertap-diff-identities.git
```
2. In the cloned dir, find the index.html file and set your Clevertap ID in the placeholder `<ID HERE>`.
3. In the root directory run `npm install`
4. Now you can run the app with `npm run start`

To reproduce the issue, execute the following actions:
1. Click on the TRACK EVENT button. At the bottom of the page you will see log what happened. In this case an event should be tracked in an anonymous profile in CleverTap. You can check it by searching for the event name (take it from the logs). Each click will generate a new event with incremented number at the end.
2. Click on Sign In button. This will push a random email for the current profile.
3. Click on TRACK EVENT button. The new events should go to the previously generated profile, however it is not anonymous anymore.
4. Click on Sign Out button. From now on, all events MUST go to a new anonymous profile.
5. Click on TRACK EVENT button. The new event should go to the anonymous profile. However, they are tracked in the previously generated one.
6. Click on Sign In button again. This will add new email to the CleverTap profile.
After all those action, we should have two profiles with different actions. Actually we have a single one with two emails.