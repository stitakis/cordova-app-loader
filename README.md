cordova-app-loader
==========

This is branch version of [cordova-app-loader](https://github.com/markmarijnissen/cordova-app-loader).

It contains the changes that I did so far to get it working with the android emulator.

It worked out-of-the-box in chrome (used live-server) but not when I ran in the android emulator. 

Additionally I've added the whitelist plugin.

Let us take a look at the changes...


### Changes in the file www\index.html

##### Added the `cordova-app-loader-complete.js` to the `www\index.html` and copied it from the folder `dist` to `www`

```
<script type="text/javascript" src="cordova-app-loader-complete.js"></script>
```


##### Added the `server` attribute in the `bootstrap.js` import script tag.

This was necessary to indicate to the app where to pickup the original manifest. 

Note that when running a cordova app in the emulator the localhost is not anymore your workstation. It is the emulated system itself.

Therefore the url to get access to workstation from the cordova app is `10.0.2.2`

```
<script src="bootstrap.js" timeout="5100" manifest="manifest.json" server="http://10.0.2.2:8080/"></script>
```

### Changes in file www\app.js

I've changed the server host url in the file `app.js`
```
var SERVER = 'http://10.0.2.2:8080/';
```


### Added the whitelist plugin and configure it

[cordova whitelist plugin](https://github.com/apache/cordova-plugin-whitelist) provides a whitelist policy for navigating the application webview. 

To add it you'll need to run:

```
cordova plugin add cordova-plugin-whitelist
```


##### I've added the allow naviation tag to the `config.xml` 

This controls which URLs the WebView itself can be navigated to.

```
    <allow-navigation href="*://*/*"/>
```


##### I've added the meta tag `http-equiv="Content-Security-Policy"` in the file `www\index.html`

```
<!-- This policy allow everything: use it only in development -->
<meta http-equiv="Content-Security-Policy" content="default-src *">
```



