---
layout: post
title: "developing-on-blackberry"
date: 2014-09-05 21:58:07 +0800
comments: true
categories: dev
---

# Create BlackBerry ID token
here: 
** https://www.blackberry.com/SignedKeys/ **

If you will develop an app on BlackBerry OS 10 or some new plateform, choose the first checkbox, and you will be requested your BlackBerry ID username and password, other choices I haven't tried. Then fill a storepass for the key, you can download a file like `bbidtoken.csk`, save this file to `~/Library/Research In Motion`, if you are on Windows or Linux, save this file to where website mentioned.

# Create developer certificate file

developer certificate file is a file named author.p12

I have installed a WebWorks SDK, so I can access blackberry tools on `/Applications/BB10 WebWorks SDK 2.1.0.13/cordova-blackberry/bin/dependencies/bb-tools/bin`, you should change this path as your SDK type, the target file is `blackberry-keytool`.

`blackberry-keytool -genkeypair -storepass <keystore_pw> -author <YOUR_NAME>`

This will create the author.p12 file on the same directory described below:`~/Library/Research In Mothion`

# Create debug token

`blackberry-debugtokenrequest -storepass <KeystorePassword> -devicepin <YOUR_DEVICE_PIN> ~/Library/Research In Motion/debug_token.bar`

This will create debug token bar file on `~/Library/Research In Motion`, caution: debug token file must be a *.bar file.

# Install debug token on your device

Enable your development mode on your device first (Settings > Security and Privacy > Development Mode)

`blackberry-deploy -installDebugToken <path to debug token> -device <DEVICE_IP_ADDRESS> -password <DEVICE_PIN>`

Your should get output like these:

{% codeblock %}
Info: Sending request: INSTALL_DEBUG_TOKEN
Info: Action: Install Debug Token
Info: File size: 2607
result::success
{% endcodeblock %}
Then your device development info has changed, "Debug Token Installed"

# deploy an hello world to your device

I use WebWorks SDK, so I launched this app on Mac, and fill some info about project on `localhost:3123`, a web management for development. After created the app, choose "Build" on left hand, fill your device password and keystore password, choose BUILD & INSTALL, you may get output like these:

{% codeblock %}
[INFO]    Target Q10-2b1e42dc selected
[INFO]    Generating debug token
[INFO]    Debug token created.
[INFO]    Deploying debug token to target "Q10-2b1e42dc"
[INFO]    Sending request: INSTALL_DEBUG_TOKEN
[INFO]    Action: Install Debug Token
[INFO]    File size: 2605
[INFO]    result::success
[INFO]    Populating application source
[INFO]    Parsing config.xml
[INFO]    Generating output files
[INFO]    Package created: /Users/dawncold/WebWorks Projects/Project1/platforms/blackberry10/build/simulator/bb10app.bar
[INFO]    Package created: /Users/dawncold/WebWorks Projects/Project1/platforms/blackberry10/build/device/bb10app.bar
[INFO]    BAR packaging complete
[INFO]    Sending request: INSTALL_AND_LAUNCH
[INFO]    Action: Install and Launch
[INFO]    File size: 69497
[INFO]    Installing Project1.testDev_Project1___c8537c58...
[INFO]    Processing 69497 bytes
[INFO]    Progress 100%...
[INFO]    Progress 100%...
[INFO]    actual_dname::Project1.testDev_Project1___c8537c58actual_id::testDev_Project1___c8537c58
[INFO]    actual_version::0.0.1.1result::successLaunching Project1.testDev_Project1___c8537c58...
[INFO]    result::19132657
[INFO]    done
{% endcodeblock %}
Meanwhile, your app will be opened on your device!
![webworks launch screen](http://pic.yupoo.com/dawncold0/E2fQtBuX/small.jpg)