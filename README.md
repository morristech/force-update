ForceUpdate
============

This library is currently in __concept phase__ feel free to stare it but do not try to use it :-)

Force your users to update the app, or notify about non-critical updates.


Download
--------

Download the latest JAR:

[ ![Download](https://api.bintray.com/packages/skoumal/maven/force-update/images/download.svg) ](https://bintray.com/skoumal/maven/force-update/_latestVersion)

or via Gradle:

```groovy
compile 'net.skoumal.forceupdate:force-update:0.1.0'
```

Usage
-----

This library was designed with full customisability in mind. Whole library is based on three simple
terms:

* **VersionProvider** - provides version from some source, for example from your APK, Google Play,
your server, or any other third party service. You can choose one of existing VersionProviders, or
create your own.

* **UpdateView** - abstraction of the way how we notify user about new version available
(recommended update) or about necessary update (forced update). Predefined Activities and dialogs
available again.

* **CheckInterval** - how often should we ask _VersionProvider_ for new data. The under-the-hood
strategy is to ask with every _Activity.onResume()_ event if _MinInterval_ is already reached.

To init ForceUpdate library use this simple builder in your Application:

```java
    new ForceUpdate.Builder()

        // required - needs android.app.Application object
        .application(this)

        // defaults to NULL - no force update view will ever appear
        .minAllowedVersionProvider(new MyCustomVersionProvider())

        // defaults to 24 hours
        .minAllowedVersionCheckMinInterval(4 * 3600)

        // defaults to version from http://carreto.pt/tools/android-store-version/?package=<your package>
        .recommendedVersionProvider(new GooglePlayVersionProvider())

        // defaults to 24 hours
        .recommendedVersionCheckMinInterval(6 * 3600)

        // defaults to NULL - no force update view will ever appear
        .excludedVersionProvider(new MyExcludedVersionListProvider())

        // defaults to 24 hours
        .excludedVersionCheckMinInterval(8 * 3600)

        // defaults to current apk version
        .currentVersionProvider(new ApkVersionProvider())

        // defaults to predefined activity
        .forcedUpdateView(new ForcedVersionActivityView())

        // defaults to predefined dialog
        .recommendedUpdateView(new RecommendedVersionView())

        // alias for .build().init()
        .buildAndInit();
```

Extras
------

Library is able to detect crash during last version check and hangs main thread during next app
start to avoid any other code execution and allow successful version check. If there is new version
available it fires notification automatically.

Contact
=======

Feel free to [report any issues](https://github.com/skoumalcz/force-update/issues/new) or for the library on contribute few pieces of code!

Follow us on Twitter! [@skoumal_dev](https://twitter.com/skoumal_dev)

License
=======

    Copyright 2016 SKOUMAL, s.r.o.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
