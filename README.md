# electron-quick-start

**Demonstrates an issue with session length when using Clevertap in Electron app**

This project demonstrates an issue with session length when using Clevertap analytics in Electron application.

**Setup**
1. Clone the repo:
```
git clone git@github.com:rosen-vladimirov/electron-quick-start.git
```
2. In the cloned dir, find the index.html file and set your Clevertap ID in the placeholder `<ID HERE>`.
3. In the root directory run `npm install`
4. You can test if everything works as expected by running `npm run start` - this will open a simple Electron app, that will try to send four events to Clevertap. You'll also see the DevTools are opened and in session storage the WZRK_D variable is set.
4. Now you have to build the application:
```
npm run dist
```
5. The above command will produce a `dist` folder, which will contain several files. Double-click the `electron-quick-start-1.0.0.dmg` file. This will start the installation of the app.
6. Once finished, open your Applications directory and locate the `electron-quick-start` application. Right-click it and select Open. First time it will not allow you to run the app, as the app is not notarized, but use right-click-> open again and the app will start.
7. The application writes all of the DevTools logs in the electronDevToolsLogs.log file in the user's home directory: `~/electronDevToolsLogs.log`.
8. Close the app and check the logs.
9. Now start the app again - as there are no 20 mins between the sessions, it is expected to have the same session, but instead a new session is started (you can verify this both in the DevTools and the mentioned log file).