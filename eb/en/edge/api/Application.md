#Application


## Overview
The Application class is used for accessing or setting application level configuration settings.
## Enabling the API
In order to use this API you must include reference to the following JavaScript file that is included with the Enterprise Browser installation:

* ebapi-modules.js - this file contains all available Enterprise Browser APIs

If you wish to minimize the amount of JavaScript being included, you can choose to only include the individual API that your application is using:

ex:

* ebapi.js - core APIs needed 
* eb.application.js - just the Application API
* other individual JavaScript files included with the Enterprise Browser installation

        


##Methods



### databaseFilePath(<span class="text-info">STRING</span> partitionName)
Path to the ORM database file by partition name. Please note that this function does not create a database file. This function only generates the file path based on the application path and partition name.

####Parameters
<ul><li>partitionName : <span class='text-info'>STRING</span><p>
Partition name. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING : 
Full path to the database file for given partition.</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Application.databaseFilePath(<span class="text-info">STRING</span> partitionName)</code> </li></ul></li></ul>

### expandDatabaseBlobFilePath(<span class="text-info">STRING</span> relativePath)
Generates the absolute path to database blob file. Please note that this function does not the create database file. This function only generates the file path based on application path and partition name.

####Parameters
<ul><li>relativePath : <span class='text-info'>STRING</span><p>
Relative path to the blob file, as it is stored in the database. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING : 
Full path to the database blob.</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Application.expandDatabaseBlobFilePath(<span class="text-info">STRING</span> relativePath)</code> </li></ul></li></ul>

### minimize()
Minimize or move the application to background. 

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Application.minimize()</code> </li></ul></li></ul>

### modelFolderPath(<span class="text-info">STRING</span> name)
Folder of the model by name.

####Parameters
<ul><li>name : <span class='text-info'>STRING</span><p>
Model name. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Application.modelFolderPath(<span class="text-info">STRING</span> name)</code> </li></ul></li></ul>

### quit()
Quit the application.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Application.quit()</code> </li></ul></li></ul>

### relativeDatabaseBlobFilePath(<span class="text-info">STRING</span> absolutePath)
Generates the relative path to database blob file. Please note that this function does not create a database file. This function only generates the file path based on the application path and partition name.

####Parameters
<ul><li>absolutePath : <span class='text-info'>STRING</span><p>
Absolute path to database blob file. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Application.relativeDatabaseBlobFilePath(<span class="text-info">STRING</span> absolutePath)</code> </li></ul></li></ul>

### restore()
Restores the application to be in the foreground.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Application.restore()</code> </li></ul></li></ul>

### setApplicationNotify()
This method allows your application to register for application specific events like application activation/deactivation, UI creation/destruction as well as others. Check the Callback section for details.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li>applicationEvent : <span class='text-info'>STRING</span><p>
{} </p><p><strong>Possible Values</strong> :</p> <dl  ><dt>Constant: EB.Application.APP_EVENT_ACTIVATED <br/> String:Activated</dt><dd>
The application has been activated.</dd><dt>Constant: EB.Application.APP_EVENT_DEACTIVATED <br/> String:Deactivated</dt><dd>
The application has been deactivated.</dd><dt>Constant: EB.Application.APP_EVENT_UIDESTROYED <br/> String:UIDestroyed</dt><dd>
This event is triggered when the application is closing and the UI has been cleared.</dd><dt>Constant: EB.Application.APP_EVENT_SCREEN_OFF <br/> String:ScreenOff</dt><dd>
Device screen was turned off when power button was pressed or due to idle timeout. On Android the application is not deactivated.Not supported on Windows CE. Platforms: 
Android, iOS, WM</dd><dt>Constant: EB.Application.APP_EVENT_SCREEN_ON <br/> String:ScreenOn</dt><dd>
Device screen was turned on and unlocked.Not supported on Windows CE. Platforms: 
Android, iOS, WM</dd></dl></li><li>eventData : <span class='text-info'>HASH</span><p>
This will only contain values for the `APP_EVENT_CONFIGCONFLICT` event. This event may be triggered after an application was upgraded. If your rhoconfig.txt file contains custom properties that are different then what is being provided in the application upgrade package. By default local values are kept in place but you may overwrite configuration with new values and any other steps required for your application upgrade. `eventData` will be a hash. It will look like {"conflicting key" : ["new value","old value"].. } </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Application.setApplicationNotify()</code> </li></ul></li></ul>

##Properties



###appName

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Application name.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.appName</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###badLinkURI

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Bad link URI to navigate in browser. This is defined in config.xml: Navigation\\BadLinkURI.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.badLinkURI</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE(Motorola Solutions' WebKit)

###bundleFolder

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Path to the Enterprise Browser folder on the device.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.bundleFolder</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###configPath

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Path to the configuration file.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.configPath</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###databaseBlobFolder

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Path to folder where the database blob files are stored. Blobs are usually images or binary files. In the ORM Model you would specify that the attribute is of type blob Ex. When capturing an image, the actual file is saved in the databaseBlobFolder.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.databaseBlobFolder</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###defaultNativeMenu

####Type
<span class='text-info'>ARRAY</span> <span class='label'>Read Only</span>
####Description

Native Menu items.
####Params
<li><i>Object</i> : <span class='text-info'>HASH</span><p>
Same values as nativeMenu. </p></li>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.defaultNativeMenu</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###invalidSecurityTokenStartPath

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Page to navigate to in case of check of SecurityToken failed. Can be set in rhoconfig.txt: invalid_security_token_start_path; This file is located in the installation folder of the EnetrpriseBrowser application installed on the device.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.invalidSecurityTokenStartPath</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###modelsManifestPath

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Path to file with the model list.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.modelsManifestPath</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###nativeMenu

####Type
<span class='text-info'>ARRAY</span> 
####Description

Native Menu items.
####Params
<li><i>Object</i> : <span class='text-info'>HASH</span><p> </p></li><ul><li>label : <span class='text-info'>STRING</span><p>
Visible label. </p></li><li>action : <span class='text-info'>STRING</span><p>
URL to page which will be loaded. Or it can be a JavaScript method to call: 'javascript: methodOnTab();'. Or path to html page to load. </p></li></ul>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.nativeMenu</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###publicFolder

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Path to the application's public folder.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.publicFolder</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###securityTokenNotPassed

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description

Indicates if the security token check was failed. Security token can be passed as command line parameter '-security_token=token_value' to the application. If security token check failed : if this page exist then application navigate to it, otherwise application will exit.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.securityTokenNotPassed</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###settingsPageURI

####Type
<span class='text-info'>STRING</span> 
####Description

Settings page URI. Will be used when Options menu or toolbar item is chosen by user.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.settingsPageURI</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###splash

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Splash screen image display options. This a string with several parameters divided by ';': delay=5;center;hcenter;vcenter;vzoom;hzoom;zoom.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.splash</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###startURI

####Type
<span class='text-info'>STRING</span> 
####Description

Startup page for your application.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.startURI</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###title

####Type
<span class='text-info'>STRING</span> 
####Description

Define Window caption text. If missed - caption from page used. Not supported on Windows CE devices.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.title</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE

###userFolder

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Path to folder where the application can write files and create subfolders.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.userFolder</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###version

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Version of Enterprise Browser.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.Application.version</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE