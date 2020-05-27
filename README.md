# Meteor PWA Explained
Demonstrate the use of PWA and service workers in Meteor 1.8+ Project

<a href="https://www.repostatus.org/#active"><img src="https://www.repostatus.org/badges/latest/active.svg" alt="Project Status: Active – The project has reached a stable, usable state and is being actively developed." /></a>

**This is running in production with https://www.activitree.com**

<img alt="Activitree" src="https://assets.activitree.com/images/ad_banner.jpg" width="100%">


* **This is not a Meteor project/app.** The folder structure represents where each and every file should exist in your project. 

* sw.js contains the necessary service worker installation, activation and newtork strategies for caching and delivery of the Meteor bundle files and other assets. This also handles the offline experience (show an offline HTML page).

* firebase-messaging-sw.js contains the above (sw.js) plus an example of configuration and listeners for Web Push Notifications which has been tested with activitree:push.

You can refer to https://www.activitree.com where these are implemented as presented in this documentation. This will help you understand debugging and what exactly you can expect from your own implementation.

* How it works. There are multiple scenarios (strategies) and similarly you can change to your needs:
    * The PWA manifest is being precached. This means that it will load the first time any page is being rendered. At the time of first load only files in pre-cacheing are being loaded. After the first load, since now we have a manifest and the PWA knows what to do, on consequent loads of pages the Workbox worker will load assets and pages as per the strategies defined.
    * The two main Meteor bundle files (JS and CSS) are being cached locally whenever a new file is detected (detection is done by filename which is unique for every production bundle release (if either JS or CSS have been modified). Once the two files are cached, they will always be served from the workbox storage (in Chrome - Cache Storage) or from the browser cache whatever the browser prefers to do.
    * Every other page (route) is cached if refreshed / opened. Since most Meteor Webapps behave like SPAs, unless you refresh a page, just routing to it will not produce a caching of that page. This is the present behavior of this example but you are free to hook the Workbox into your router and listen to page changes and cache them all. The strategy here is "network first". The route comes from network when online. When offline, this route + the two Meteor bundle files (CSS and JS) should be enough to do a minimum rendering of the respective page (depending on what has been cached.)
    * You can add as many strategies you want. For example, images that you know will not change for a long time can be cached with a "Cache First" strategy (as if they were served from the usual browser cache).
    * When set properly, not only you get a nice user experience with screens loading instantly but you save on your tech cost by have a lot of assets, bundles, pages already distributed (cached with users).
    * Please do read the Workbox documentation in order to understand the lifecycle and lifespan of caches.

* You can get Workbox by adding it as an NPM to you project bundle or the way is presented in this repo (by importing the script from CDN). I didn’t want to load this in the JS bundle so I prefer to use import script.

* There are very many options to catch any kind of files, with expiration dates etc. Please read the Workbox 5 documentation (https://developers.google.com/web/tools/workbox)

* We have this in production with the 'under-construction' project in case you want to give it a try/check. (https://www.activitree.com)
