# Angular Ace Wrapper

<a href="https://badge.fury.io/js/ngx-ace-wrapper"><img src="https://badge.fury.io/js/ngx-ace-wrapper.svg" align="right" alt="npm version" height="18"></a>

This is an Angular wrapper library for the [Ace](http://ace.c9.io/).

To use this library you should get familiar with the [Ace documentation](http://ace.c9.io/#nav-api) as well, this documentation only explains details specific to this wrapper.

See a live example application <a href="https://zefoy.github.io/ngx-ace-wrapper/">here</a>.

### Building the library

```bash
npm install
npm start
```

### Running the example

```bash
cd example
npm install
npm start
```

### Library development

```bash
npm link
cd example
npm link ngx-ace-wrapper
```

### Installing and usage

```bash
npm install brace --save
npm install ngx-ace-wrapper --save
```

##### Load the module for your app (with global configuration):

```javascript
import { AceModule } from 'ngx-ace-wrapper';
import { ACE_CONFIG } from 'ngx-ace-wrapper';
import { AceConfigInterface } from 'ngx-ace-wrapper';

const DEFAULT_ACE_CONFIG: AceConfigInterface = {
};

@NgModule({
  ...
  imports: [
    ...
    AceModule
  ],
  providers: [
    {
      provide: ACE_CONFIG,
      useValue: DEFAULT_ACE_CONFIG
    }
  ]
})
```

##### Use it in your HTML template (with custom configuration):

This library provides two ways to create a Ace element, component for simple use cases and directive for more custom use cases.

**COMPONENT USAGE**

Simply replace the element that would ordinarily be passed to `Ace` with the ace component.

**NOTE:** Component provides default toolbar element which you can enable by setting the appropriate configuration to 'true' or by providing custom toolbar config. If you want to use a custom toolbar then you might want to use the directive instead.

```html
<ace [config]="config" [(value)]="value"></ace>
```

```javascript
[config]                     // Custom config to override the global defaults.

[mode]                       // Mode for the editor (import mode manually!).
[theme]                      // Theme for the editor (import theme manually!).

[value]                      // Input value of the ace editor content (text).

[disabled]                   // Disables all functionality (focus & editing).

[useAceClass]                // Use ace class (use provided default styles).

(valueChange)                // Event handler for the input value change event.
```

**DIRECTIVE USAGE**

When using only the directive you need to import the used mode(s) and theme(s):

```javascript
@import 'brace/mode/text';
@import 'brace/theme/github';
```

Ace directive can be used in correctly structured div element with optional custom configuration:

```html
<div class="ace" [ace]="config" [(text)]="text"></div>
```

```javascript
[ace]                        // Custom config to override the global defaults.

[disabled]                   // Disables all functionality (focus & editing).
```

##### Available configuration options (custom / global configuration):

```javascript
mode                         // Mode for the editor (import mode manually!).
theme                        // Theme for the editor (import theme manually!).

wrap                         // Sets text wrapping to be enabled or disabled.
tabSize                      // Size in spaces of the soft tabs (Default: 4).

showPrintMargin              // Sets showing of the print margin (Default: false).
```

For more detailed documentation with all the supported config options see [Ace documentation](http://ace.c9.io/#nav-api).

##### Available control / helper functions (provided by the directive):

```javascript
ace()                        // Returns the Ace instance reference for full API access.

clear()                      // Clears the editor document and resets text selection.

setValue(value, cursorPos?)  // Text value for the editor document (clears selection).
```

Above functions can be accessed through the directive reference (available as directiveRef in the component).