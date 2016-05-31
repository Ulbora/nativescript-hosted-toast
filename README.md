# Nativescript Hosted Toast Plugin
This a Nativescript Plugin that lets you make toast from a hosted Angular 2 application.

## Installation

```
tns plugin add nativescript-hosted-toast

```

## Usage

Create a wrapper application with the following code and a Navivescript WebView.
See the following project as an example:
https://github.com/Ulbora/NSWrapper

```
var application = require("application");
var context = application.android.context;
function pageLoaded(args) {
    var page = args.object;   
    var web = page.getViewById("webView"); 
    var androidSettings = web.android.getSettings();
    androidSettings.setJavaScriptEnabled(true);    
    var hostedToast = new com.ulbora.hosted.toast.HostedToast(context);    
    web.android.addJavascriptInterface(hostedToast, 'HostedToast');
    web.url = "http://someURLWhereAngular2AppIsHosted";
}
exports.pageLoaded = pageLoaded;

```

Inside the Angular 2 hosted application, write the code where you want to access device information.
See the following project as an example:
https://github.com/KenWilliamson/Angular2HostedMobileApp

Component code:
```
deviceReady: boolean;

 ngOnInit() {        
        try {
            if (HostedToast) {
                this.deviceReady = true;
            }
        } catch (err) {
        }
    }


 showToast() {
        try {
            HostedToast.showToast("Toast is working in a hosted world.");            
        } catch (err) {
        }
    }

```

Template Code:
```
<div *ngIf="deviceReady">
    <div> <b>Your Toast</b>: <span (click)="showToast()" class="glyphicon glyphicon-phone"></span></div>        
</div>

```

## Available Methods
#### HostedToast.showToast("some message")
Sends a toast message to the device


