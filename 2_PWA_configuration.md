Installing and uninstalling PWA with a Chrome browser: https://www.guidingtech.com/install-uninstall-pwas-chrome/

Android offers to save a PWA on the local device if this feature is detected in a website.

IOS requires a manual strategy, the developer needs to offer this in the UI. Read this about state of PWA on IOS: https://love2dev.com/pwa/ios/


**Requirements:**
* Have a manifest file available at https://yourdomain.com/manifest.json. This will be placed in your Meteor public folder: https://github.com/activitree/Meteor-PWA-Explained/blob/master/app/public/manifest-pwa.json

* Have a configuration specific for your PWA in your main html file of your Meteor webapp. This example shows the minimum meta tags for a PWA, do not copy-paste / overwrite your main.html file. Instead, add these tags to your existing head tag in your html file. https://github.com/activitree/Meteor-PWA-Explained/blob/master/app/client/main.html

* You need to register a service worker. This is a good time to read this article: https://dev.to/jankapunkt/transform-any-meteor-app-into-a-pwa-4k44


Move here: https://github.com/activitree/Meteor-PWA-Explained/blob/master/3_Service_workers.md


TODO

- [ ] Add to homescreen for IOS
- [ ] SimpleDDP - with PWA shell

