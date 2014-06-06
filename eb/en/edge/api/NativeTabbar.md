#NativeTabbar


## Overview
<p>The NativeTabbar methods let you use multiple instances of the RhoMobile webview in separate tabs. On Android, iOS and WIndows Phone 8 the tabs are true Native Tabbar controls to give your application a native look and feel.</p>
<p>No more than 4 tabs can be created in the Windows Phone 8 tabbar. A tabbar separator doesn&rsquo;t exist in Windows Phone 8. On Windows Mobile/CE there are no visible tabs. At one time only Toolbar or Tabbar can present in application &ndash; Toolbar and Tabbar can not be used both in one time.</p>

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



### create(<span class="text-info">ARRAY</span> tabElements, <span class="text-info">HASH</span> tabBarProperties)
Removes the current tabbar / toolbar and replaces it with this one. Callback will be called when tab is switched.

####Parameters
<ul><li>tabElements : <span class='text-info'>ARRAY</span><p>
Array of Tab elements. </p></li><ul><li>tabElement : <span class='text-info'>HASH</span><p>
Properties of Tab elements. </p></li><ul><li>label : <span class='text-info'>STRING</span><p>
Visible label to display on the tabbar. </p></li><li>action : <span class='text-info'>STRING</span><p>
URL to page which will be loaded into tab. Predefined actions are not supported. It may be path to Ruby controller action; i.e. '/app/Account' would load the Account index action. For ruby callback use 'callback:/app/Account' Or javascript method to call: 'javascript: methodOnTab();'. Or path to html page to load. </p></li><li>icon : <span class='text-info'>STRING</span><p>
Relative path to tabbar item icon in your rhodes app; typically located in /public/images/. Platforms:Win32, Android, iOS, WP8 </p></li><li>reload : <span class='text-info'>BOOLEAN</span><span class='label '> Default: false</span><p>
When tab is activated  - page in tab will be reloaded. </p></li><li>selectedColor : <span class='text-info'>INTEGER</span><p>
Change the selected color of this tab. On Android this works only if you setup selectedColor for all tabs and also setup backgroundColor for the whole Tabbar. Platforms:Win32, Android, iOS, WP8 </p></li><li>disabled : <span class='text-info'>BOOLEAN</span><span class='label '> Default: false</span><p>
Tab will be displayed as disabled. Platforms:Win32, Android, iOS, WP8 </p></li><li>backgroundColor : <span class='text-info'>INTEGER</span><p>
 Background color for tab. Use when your application background color is not white for removing blink during switch tabs. Platforms:Win32, Android, iOS, WP8 </p></li><li>useCurrentViewForTab : <span class='text-info'>BOOLEAN</span><span class='label '> Default: false</span><p>
Gives a smooth transfer to a newly opened tab from the current view into this Tab and make this Tab active. Only one Tab can have this parameter. Platforms:WM, Win32, Android, iOS </p></li><li>perishable : <span class='text-info'>BOOLEAN</span><span class='label '> Default: false</span><p>
Sets whether this tab is allowed to be destroyed when a memory limit is reached (Windows Mobile) Platforms:WM </p></li><li>createOnInit : <span class='text-info'>BOOLEAN</span><span class='label '> Default: false</span><p>
Create tab immediately when TabBar is created. Action also will be executed. If false, the tab will be created when it is switched to. Platforms:WM </p></li></ul></ul><li>tabBarProperties : <span class='text-info'>HASH</span><p>
Properties of TabBar. </p></li><ul><li>verticalOrientation : <span class='text-info'>BOOLEAN</span><span class='label '> Default: false</span><p>
Creates a vertical tabbar on the iPad. Platforms:iOS </p></li><li>backgroundColor : <span class='text-info'>INTEGER</span><p>
Background color of the tabbar. Platforms:Win32, Android, iOS, WP8 </p></li><li>hiddenTabs : <span class='text-info'>BOOLEAN</span><span class='label '> Default: true</span><p>
Do not display Tabs with labels.Only hiddenTab=true is currently supported. Platforms:WM </p></li><li>createOnInit : <span class='text-info'>BOOLEAN</span><span class='label '> Default: false</span><p>
Create tabs immediately when TabBar is created. Action also will be executed. If false, then each tab will be created when first switch to the tab is executed. Platforms:WM </p></li><li>placeTabsBottom : <span class='text-info'>BOOLEAN</span><p>
Place TabBar to bottom instead of default top - only for Android. Platforms:Android </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li>tab_index : <span class='text-info'>INTEGER</span><p>
New tab index. </p></li><li>newTabIndex : <span class='text-info'>INTEGER</span><p>
New tab index. Platforms:WM </p></li><li>oldTabIndex : <span class='text-info'>INTEGER</span><p>
New tab index. If you switched to first activated tab, when oldTabIndex will be -1, which means that there was no old tab index exists. Platforms:WM </p></li><li>tabEvent : <span class='text-info'>STRING</span><p>
{} Platforms:WM </p><p><strong>Possible Values</strong> :</p> <dl  ><dt>onTabFocus</dt><dd>
Fires when a tab gains focus.</dd><dt>onTabNewError</dt><dd>
Fires when a new tab cannot be created.</dd></dl></li></ul></ul>

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
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.NativeTabbar.create(<span class="text-info">ARRAY</span> tabElements, <span class="text-info">HASH</span> tabBarProperties)</code> </li></ul></li></ul>

### currentTabIndex()
Returns the current tab 0-based index.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>INTEGER</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>INTEGER</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.NativeTabbar.currentTabIndex()</code> </li></ul></li></ul>

### remove()
Removes the current tabbar. Does nothing if there is no active tabbar.

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
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.NativeTabbar.remove()</code> </li></ul></li></ul>

### removeTab(<span class="text-info">INTEGER</span> tabIndex)
Removes the Tab by index. Method will remove the WebView for the specific tab, it will not remove the tab from the tab array, so all indexes will remain the same.You cannot delete the tab with useCurrentViewForTab flag.If you switch to previously removed tab, tab will be recreated.

####Parameters
<ul><li>tabIndex : <span class='text-info'>INTEGER</span><p>
The index for tab (index numbered from 0) to delete. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Windows Embedded

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.NativeTabbar.removeTab(<span class="text-info">INTEGER</span> tabIndex)</code> </li></ul></li></ul>

### setTabBadge(<span class="text-info">INTEGER</span> tabIndex, <span class="text-info">STRING</span> badge)
Set the iPhone badge to tab.

####Parameters
<ul><li>tabIndex : <span class='text-info'>INTEGER</span><p>
The index for this tab (index numbered from 0). You can also set -1 to select current tab for set badge. </p></li><li>badge : <span class='text-info'>STRING</span><p>
String for iPhone badge, such as '12'. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* iOS

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.NativeTabbar.setTabBadge(<span class="text-info">INTEGER</span> tabIndex, <span class="text-info">STRING</span> badge)</code> </li></ul></li></ul>

### switchTab(<span class="text-info">INTEGER</span> tabIndex)
Switch active tab.

####Parameters
<ul><li>tabIndex : <span class='text-info'>INTEGER</span><p>
The index for this tab (index numbered from 0). </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

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
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.NativeTabbar.switchTab(<span class="text-info">INTEGER</span> tabIndex)</code> </li></ul></li></ul>

##Examples



###Create native tabbar

Create a platform-native tabbar. Tabs can link to internal application links (such as those built with "url_for") as well as external URLs.
<pre><code>

           
function create_tabbar() {
    Rho.NativeTabbar.create([{
            label: "Home",
            action: "/app"
        }, {
            label: "example.com"
            action: "http://www.example.com"
        }], {}, tabbar_callback
    );
}

function tabbar_callback(params) {
    alert("Switching to tab "+params["tab_index"]);
}
                   
                 
</code></pre>

###Switch tab

Switch the active tab.
<pre><code>

           
// Make the third tab active
Rho.NativeTabbar.switchTab(2);
                   
                 
</code></pre>

###Remove tabbar

Remove the tabbar.
<pre><code>

           
Rho.NativeTabbar.remove();
                   
                 
</code></pre>