#NativeToolbar


## Overview
<p>The NativeToolbar method let you create and remove a toolbar at runtime.</p>
<p> Only a Toolbar or a Tabbar can present in application &ndash; both can not be used at the same time.</p>

<h2>Enabling the API</h2>

<p>This API is part of the <code>coreapi</code> extension that is included automatically.</p>

<pre><code>:::ruby
extensions: ["coreapi"]
</code></pre>

<h2>JavaScript Usage</h2>

<p>Be sure to review the <a href="/guide/api_js">JavaScript API Usage</a> guide for important information about using this API in JavaScript.</p>

<h2>Ruby Usage</h2>

<p>Be sure to review the <a href="/guide/api_ruby">Ruby API Usage</a> guide for important information about using this API in Ruby.</p>



##Methods



### create(<span class="text-info">ARRAY</span> toolbarElements, <span class="text-info">HASH</span> toolBarProperties)
Removes the current toolbar / tabbar and replaces it with this one.

####Parameters
<ul><li>toolbarElements : <span class='text-info'>ARRAY</span><p>
Array of Toolbar elements. Do not create more than five elements for maximum portability.Toolbar elements are not scrollable, so if some buttons will not fit into the screen dimensions, they will be invisible. </p></li><ul><li>toolbarElement : <span class='text-info'>HASH</span><p>
Properties of Toolbar elements. Either :icon or :label must be specified. If both are specified, :icon is drawn and :label is discarded. </p></li><ul><li>label : <span class='text-info'>STRING</span><p>
Visible label to display instead of an icon.For predefined actions, icon will be displayed.Android,iOS note: for predefined actions no label will be displayed. </p></li><li>action : <span class='text-info'>STRING</span><p>
URL to call when button is pressed or special value.It may be path to Ruby controller action; i.e. '/app/Account' would load the Account index action. For ruby callback use 'callback:/app/Account' Or javascript method to call: 'javascript: methodOnButton();'. </p><p><strong>Possible Values</strong> :</p> <dl  ><dt>separator</dt><dd>
Add a separator to the toolbar. If only one separator is specified, then elements after separator will be right-aligned. If more then one separator is added: on WM/CE, platform dependent separator will be displayed, on Android/iOS center-aligned groups will be created. Platforms: 
WM, Win32, iOS, Android</dd><dt>exit</dt><dd>
Exit the application.</dd><dt>close</dt><dd>
Exit the application.</dd><dt>options</dt><dd>
Navigate to Settings page, defined in configuration file.</dd><dt>home</dt><dd>
Navigate to Home page, defined in configuration file.</dd><dt>refresh</dt><dd>
Refresh current page.</dd><dt>back</dt><dd>
Perform back action or execute browser back.</dd><dt>log</dt><dd>
Display Log View window. Platforms: 
WM, Win32, iOS, Android</dd><dt>fullscreen</dt><dd>
Expand application window to full screen. Platforms: 
WM, Win32, Android, WP8</dd><dt>sync</dt><dd>
Run full sync command.</dd><dt>minimize</dt><dd>
Minimize application window. Platforms: 
WM, Win32</dd><dt>SIP</dt><dd>
Display software keyboard window.Set Rho.System.keyboardState to Rho.System.KEYBOARD_AUTOMATIC to use this element. Platforms: 
WM</dd></dl></li><li>icon : <span class='text-info'>STRING</span><p>
Relative path to toolbar item icon in your rhodes app (typically located in '/public/images/'). Icon is ignored for predefined actions, icon will be displayed even if no icon specified. iPhone and Android: Icons must be no more than 30x30 pixels and must be in .png format. Windows Mobile: Icons can be any size, but all icons should have same size (default - 48x48). .png and .bmp formats are supported. </p></li><li>coloredIcon : <span class='text-info'>BOOLEAN</span><span class='label '> Default: false</span><p>
Use colored icon in toolbar on iPhone instead of standard monochrome white icon (prepared from image alpha). Platforms:iOS </p></li><li>width : <span class='text-info'>INTEGER</span><p>
Button width in pixel. Used to define separator width when more than one separator specified. Platforms:WM </p></li></ul></ul><li>toolBarProperties : <span class='text-info'>HASH</span><p>
Properties of TabBar. </p></li><ul><li>backgroundColor : <span class='text-info'>INTEGER</span><p>
Background color of the toolbar. </p></li><li>maskColor : <span class='text-info'>INTEGER</span><span class='label '> Default: 0xFFFFFF</span><p>
Image mask color(transparent color). Platforms:WM, Win32 </p></li><li>viewHeight : <span class='text-info'>INTEGER</span><p>
Toolbar height in pixels. Platforms:WM, Win32 </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.NativeToolbar.create(<span class="text-info">ARRAY</span> toolbarElements, <span class="text-info">HASH</span> toolBarProperties)</code> </li></ul></li></ul>

### remove()
Removes the current toolbar. Does nothing if there is no active toolbar.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.NativeToolbar.remove()</code> </li></ul></li></ul>

##Examples



###Create native toolbar

Create a native Toolbar.
<pre><code>:::javascript
           
Rho.NativeToolbar.create([{
        label: "Home",
        action: Rho.Application.startURI
    }, {
        label: "example.com",
        action: "http://www.example.org"
    }], {})
                   
                 
</code></pre>

###Remove the toolbar

Remove the toolbar.
<pre><code>:::javascript
           
Rho.NativeToolbar.remove();
                   
                 
</code></pre>