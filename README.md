# [Angular 2 Seed Advanced](https://github.com/NathanWalker/angular2-seed-advanced)

This is an **advanced** seed project for Angular 2 apps based on [Minko Gechev's](https://github.com/mgechev) [angular2-seed](https://github.com/mgechev/angular2-seed) that expands on all of its great features to include core support for:

#### Integration with:
- [ngrx/store](https://github.com/ngrx/store) RxJS powered state management, inspired by **Redux**
- [ng2-translate](https://github.com/ocombe/ng2-translate) for i18n 
  - Usage is optional but on by default
  - Up to you and your team how you want to utilize it. It can be easily removed if not needed. 
- [angulartics2](https://github.com/angulartics/angulartics2) Vendor-agnostic analytics for Angular2 applications.
  - Out of box support for [Segment](https://segment.com/)
    - When using the seed, be sure to change your `write_key` [here](https://github.com/NathanWalker/angular2-seed-advanced/blob/master/src/client/index.html#L24)
  - Can be changed to any vendor, [learn more here](https://github.com/angulartics/angulartics2#supported-providers)
- [lodash](https://lodash.com/) Helps reduce blocks of code down to single lines and enhances readability
- [NativeScript](https://www.nativescript.org/) cross platform mobile (w/ native UI) apps. [Setup instructions here](#nativescript-app).
- [Electron](http://electron.atom.io/) cross platform desktop apps (Mac, Windows and Linux). [Setup instructions here](#electron-app).

# Table of Contents

- [Enhanced development workflow](#enhanced-development-workflow)
- [Enhanced testing support options](#enhanced-testing-support-options)
- [Prerequisites](#prerequisites)
- [Usage](#usage)
- [NativeScript App](#nativescript-app)
- [Electron App](#electron-app)
- [Testing](#testing)
- [Framework How-Tos](#framework-how-tos)
- [Web Configuration Options](#web-configuration-options)
- [Change Detection OnPush Note](#change-detection-onpush-note)
- [General Best Practice Guide to Sharing Code](#general-best-practice-guide-to-sharing-code)
- [Feature Branches](#feature-branches)
- [Integration Guides](https://github.com/NathanWalker/angular2-seed-advanced/wiki)
- [How best to use for your project](#how-best-to-use-for-your-project)
- [Contributing](#contributing)
- [License](#license)

#### Enhanced development workflow
- Decorators for components which reduce boilerplate for common component setups
- Shared code can be found in `frameworks`:
  - `app`: your shared application architecture code
  - `core`: foundation layer (decorators and low-level services)
  - `analytics`: analytics provided by [Segment](https://segment.com/)
    - Only reports data in **production** build
  - `i18n`: internationalization features
  - `electron`: [Electron](http://electron.atom.io/) specific code
  - `test`: test specific code providing conveniences to make testing your code easier and faster 

#### Enhanced testing support options
- mocks for various services
- configurable provider blocks for easy test setup of common application providers
  - tired of setting up similar providers over and over again for different tests?
  - configure a reusable test provider which can be configured on a case-by-base basis
  - see [example here](https://github.com/NathanWalker/angular2-seed-advanced/blob/master/src/client/app/frameworks/core/testing/providers/core.ts)
- helpers for end-to-end (e2e, integration) tests
- convenient shorthand to reduce test setup boilerplate and enhance speed of writing tests
  - are your test cases buried by multiple import lines requiring you to scroll just to get to the substance of the test?
  - removes noise allowing you to better focus on the substance of the test
  - provides full intellisense support
  - allows your team to add unique shorthands for various testing scenarios specific to your application needs
  - plays nice with `tslint` options like `"no-unused-variable": true` as the api hangs off a plain `Object` instead of globals 
    - what's the value of that you ask? have you ever isolated a test with `iit` or `ddescribe` but didn't import those or vice versa, used `iit` leaving an unused `it` now in your tests? yeah, `tslint` will be all over you :/
    - avoids `unused` variable warnings altogether in tests since you are always using a valid key from the shorthand `Object`
  - see [example here](https://github.com/NathanWalker/angular2-seed-advanced/blob/master/src/client/app/frameworks/test/shorthand/ng2-jasmine.ts)
  
**Advice**: If your project is intended to target a single platform (i.e, web only), then [angular2-seed](https://github.com/mgechev/angular2-seed) is likely more than suitable for your needs. However if your project goals are to target multiple platforms (web, native mobile and native desktop), with powerful out of the box library support and highly configurable/flexible testing options, then you might want to keep reading.

### Prerequisites

* node v5.x.x or higher and npm 3 or higher.

* To run the NativeScript app:

```
npm install -g nativescript
npm install -g typescript
```

## Usage


```bash
git clone --depth 1 https://github.com/NathanWalker/angular2-seed-advanced.git
cd angular2-seed-advanced

# install the project's dependencies
npm install
# watches your files and uses livereload by default
npm start
# api document for the app
npm run serve.docs

# dev build
npm run build.dev
# prod build
npm run build.prod
# prod build with AoT compilation
npm run build.prod.exp
```

## NativeScript App

#### Setup

```
npm install -g nativescript 
```

#### Dev Workflow

You can make changes to files in `src/client` or `nativescript` folders. A symbolic link exists between the web `src/client` and the `nativescript` folder so changes in either location are mirrored because they are the same directory inside.

Create `.tns.html` and `.tns.css` NativeScript view files for every web component view file you have. You will see an example of the `app.component.html` as a [NativeScript view file here](https://github.com/NathanWalker/angular2-seed-advanced/blob/master/src/client/app/components/app/app.component.tns.html).

#### Run

```
iOS:                      npm run start.ios
iOS (livesync emulator):  npm run start.livesync.ios
iOS (livesync device):    npm run start.livesync.ios.device

// or...

Android:                      npm run start.android
Android (livesync emulator):  npm run start.livesync.android
Android (livesync device):    npm run start.livesync.android.device
```

* Requires an image setup via AVD Manager. [Learn more here](http://developer.android.com/intl/zh-tw/tools/devices/managing-avds.html) and [here](https://github.com/NativeScript/nativescript-cli#the-commands).

OR...

* [GenyMotion Android Emulator](https://www.genymotion.com/)

## Electron App

#### Develop

```
Mac:      npm run start.desktop
Windows:  npm run start.desktop.windows
```

#### Develop with livesync
```
Mac:      npm run start.livesync.desktop
Windows:  npm run start.livesync.desktop.windows
```

#### Release: Package Electron App for Mac, Windows or Linux

```
Mac:      npm run build.desktop.mac
Windows:  npm run build.desktop.windows
Linux:    npm run build.desktop.linux
```

## Testing

```bash
npm test

# Development. Your app will be watched by karma
# on each change all your specs will be executed.
npm run test.watch
# NB: The command above might fail with a "EMFILE: too many open files" error.
# Some OS have a small limit of opened file descriptors (256) by default
# and will result in the EMFILE error.
# You can raise the maximum of file descriptors by running the command below:
ulimit -n 10480


# code coverage (istanbul)
# auto-generated at the end of `npm test`
# view coverage report:
npm run serve.coverage

# e2e (aka. end-to-end, integration) - In three different shell windows
# Make sure you don't have a global instance of Protractor

# npm install webdriver-manager <- Install this first for e2e testing
# npm run webdriver-update <- You will need to run this the first time
npm run webdriver-start
npm run serve.e2e
npm run e2e

# e2e live mode - Protractor interactive mode
# Instead of last command above, you can use:
npm run e2e.live
```
You can learn more about [Protractor Interactive Mode here](https://github.com/angular/protractor/blob/master/docs/debugging.md#testing-out-protractor-interactively)

## Web Configuration Options

Default application server configuration

```javascript
var PORT             = 5555;
var LIVE_RELOAD_PORT = 4002;
var DOCS_PORT        = 4003;
var APP_BASE         = '/';
```

Configure at runtime

```bash
npm start -- --port 8080 --reload-port 4000 --base /my-app/
```

## Framework How-Tos

### i18n

* how to add a language?
  - `src/client/assets/i18n/`
    - add `[language code].json` (copy existing one and adapt the translation strings)
  - `src/client/app/frameworks/sample/services/app-config.spec.ts`
    - fix test
  - `src/client/app/frameworks/sample/services/app-config.ts`
    - add language to `SUPPORTED_LANGUAGES`
  - `src/client/app/frameworks/i18n/components/lang-switcher.component.spec.ts`
    - fix test

## Change Detection OnPush Note

*Please Note:* The seed uses Angular's `ChangeDetectionStrategy.OnPush` by default which requires some understanding of immutability and one-way data flows. Please check out the following resources to learn more:

* http://blog.thoughtram.io/angular/2016/02/22/angular-2-change-detection-explained.html
* http://victorsavkin.com/post/110170125256/change-detection-in-angular-2
* http://www.syntaxsuccess.com/viewarticle/change-detection-in-angular-2.0
* http://ngcourse.rangle.io/handout/change-detection/change_detection_strategy_onpush.html

If you experience issues with changes not occuring in your views, you can disable this by commenting out [these lines](https://github.com/NathanWalker/angular2-seed-advanced/blob/master/src/client/app/frameworks/core/decorators/utils.ts#L43-L48). The seed uses `OnPush` by default because it  provides optimal performance and if you decide to turn it off while developing your application, you can always turn it back on when you're ready to refactor your data services to utilize `OnPush` properly.

## General Best Practice Guide to Sharing Code 

There’s actually only a few things to keep in mind when sharing code between web/mobile. The seed does take care of quite a few of those things but here’s a brief list:

* Don’t import {N} modules into your components/services. {N} modules can only be used inside the {N} app therefore cannot be shared. To get around this, use `OpaqueTokens` which is a fancy name for something quite simple. [Learn more here](http://blog.thoughtram.io/angular/2016/05/23/opaque-tokens-in-angular-2.html). A great example of how to integrate 2 different plugins (1 for web, 1 for {N}) and share all the code exists in [this wiki article: How to integrate Firebase across all platforms](https://github.com/NathanWalker/angular2-seed-advanced/wiki/How-to-integrate-Firebase-across-all-platforms-(web-nativescript-desktop)) written by the awesome [Scott Lowe](https://twitter.com/scott_d_lowe).
* Use the conditional hooks provided by the seed in shared methods where you may need to handle something differently in {N} than you do on the web. For example, see [here](https://github.com/NathanWalker/angular2-seed-advanced/blob/master/src/client/app/frameworks/i18n/components/lang-switcher.component.ts#L35-L41).
* Don’t use window global. Inject the `WindowService` provided by the seed instead. This includes usage of `alert`, `confirm`, etc. For example:

If you were thinking about doing: `alert('Something happened!');`, *Don't*.
Instead inject `WindowService`:
```
constructor(private win: WindowService) {}

public userAction() {
  if (success) {
    // do stuff
  } else {
    this.win.alert('Something happened!');
  }
}
```

This ensures that when the same code is run in the {N} app, the native `dialogs` module will be used.

* Lastly, understand this video: http://www.nativescriptsnacks.com/videos/2016/06/13/zoned-callbacks.html … As far as dealing with {N} and 3rd party plugins, you want to understand that.

The advice I like to give is:

> Code with web mentality first. Then provide the native capability using Angular’s `{provide: SomeWebService, useClass: SomeNativeService }` during bootstrap.

There are some cases where you may want to use `useValue` vs. `useClass`, and other times may need to use `useFactory`. Read [the Angular docs here to learn more about which you may need for your use case](https://angular.io/docs/ts/latest/cookbook/dependency-injection.html#!#provide).

## Feature Branches

Several branches exist with certain features integrated:

* [ui-router-ng2](https://github.com/NathanWalker/angular2-seed-advanced/tree/ui-router)

## How best to use for your project

#### Setup

*NOTE*: This should be done first before you start making any changes and building out your project. Not doing so will likely result in dificulty when trying to merge in upstream changes later.

1. Download a zip of the seed. (**Do not fork**)
2. `npm run git.setup` - This will initialize `git` as well as setup `upstream` properly.
3. `git remote add origin ...your private repo...`
4. `npm run git.prepare` - This will prepare git to handle the merge
5. `npm run git.merge` - This will fetch upstream and run the first merge (*Important)
  * IMPORTANT: You will see a wall of Conflicts after doing above (a Conflict for every single file). This is normal. There actually will not be any problematic conflicts as it's just reporting every single file which both sides (`upstream` and your first commit) added.
  * IMPORTANT: If you see `unknown option --allow-unrelated-histories` either upgrade git to 2.9+ or use `npm run git.merge.legacy`
6. `git add .; git commit -m'ready'`. **Yes**, you will be committing all those conflicts, which actually are not a problem in this 1 time case.
7. Now you have `git` setup and ready to develop your application as well as merge in upstream changes in the future.
8. `npm install` (and all other usage docs in this `README` apply)
9. Create a new `framework` for your application in `src/client/app/frameworks` to build your codebase out. Say your app is called `AwesomeApp`, then create `awesomeapp` and start building out all your components and services in there. Create other frameworks as you see fit to organize.
10. If you don't want an integration that comes out of box with this seed; for example. let's say you don't want to use i18n. Then just delete the `i18n`, remove `ng2-translate` as dependency root `package.json` and `nativescript/package.json`. Then remove any references to `i18n` throughout.

#### Merging latest upstream changes

1. `npm run git.merge.preview` - This will fetch `upstream` and show you how the merge would look
  * If you see `unknown option --allow-unrelated-histories` either upgrade git to 2.9+ or use `npm run git.merge.legacy.preview`
2. `npm run git.merge` - This will actually do the merge
  * If you see `unknown option --allow-unrelated-histories` either upgrade git to 2.9+ or use `npm run git.merge.legacy`
3. Handle any conflicts to get latest upstream into your application.
4. Continue building your app.

You can read more about [syncing a fork here](https://help.github.com/articles/syncing-a-fork/).

If you have any suggestions to this workflow, please post [here](https://github.com/NathanWalker/angular2-seed-advanced/issues).

## License

MIT
