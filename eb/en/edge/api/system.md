#System


## Overview
The System API is used to control and modify core aspects of the device such as the screen, OS and device capabilities.
## Enabling the API
In order to use this API you must TBD INSERT Eb specific instructions here

        


##Methods



### applicationInstall(<span class="text-info">STRING</span> applicationUrl)
Install an application.

####Parameters
<ul><li>applicationUrl : <span class='text-info'>STRING</span><p>
The url of an application to install on the device. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.applicationInstall(<span class="text-info">STRING</span> applicationUrl)</code> </li></ul></li></ul>

### applicationUninstall(<span class="text-info">STRING</span> applicationName)
Uninstall the application. Not Supported on Windows CE devices.

####Parameters
<ul><li>applicationName : <span class='text-info'>STRING</span><p>
The name of the application. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.applicationUninstall(<span class="text-info">STRING</span> applicationName)</code> </li></ul></li></ul>

### bringToFront()
Bring application window to the top of the screen.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.bringToFront()</code> </li></ul></li></ul>

### clearNetworkStatusNotify()
Use Network.clearStatusNotify: Clear network status callback.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.clearNetworkStatusNotify()</code> </li></ul></li></ul>

### deleteFolder(<span class="text-info">STRING</span> pathToFolder)
Delete folder.

####Parameters
<ul><li>pathToFolder : <span class='text-info'>STRING</span><p>
Path to folder. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.deleteFolder(<span class="text-info">STRING</span> pathToFolder)</code> </li></ul></li></ul>

### deleteRegistrySetting(<span class="text-info">HASH</span> propertyMap)
Deletes the specified value from the device registry. Only applicable on Windows Mobile / Embedded Handheld and CE devices. When running on RhoSimulator, this method is supported only for Windows OS.

####Parameters
<ul><li>propertyMap : <span class='text-info'>HASH</span><p>
Map of properties associated with the registry key being set. </p></li><ul><li>hive : <span class='text-info'>STRING</span><p>
The hive name, setRegistrySetting. </p></li><li>key : <span class='text-info'>STRING</span><p>
Full path of the key, including '\' separators as required. Remember to use '\\' in JavaScript to specify backslash. </p></li><li>setting : <span class='text-info'>STRING</span><p>
The name of the setting to be deleted. </p></li><li>persistent : <span class='text-info'>BOOLEAN</span><p>
If the registry value was set to be persistent, ie a corresponding .reg file was created in the \Application folder then setting true here will delete that .reg file. </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>BOOLEAN</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>BOOLEAN : 
Whether or not the registry key was successfully deleted.</li></ul>

####Platforms

* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.deleteRegistrySetting(<span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

### exit()
Use Application.quit: exit application.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.exit()</code> </li></ul></li></ul>

### getAllProperties()
This method will return all of object/value pairs for the propertyNames of the API class.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li> : <span class='text-info'>STRING</span><p> </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>HASH : 
Map of all available properties<ul><li> : <span class='text-info'>STRING</span><p> </p></li></ul></li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.getAllProperties()</code> </li></ul></li></ul>

### getProperties(<span class="text-info">ARRAY</span> arrayofNames)
This method will return a set of object/value pairs for the list of the propertyName that is passed in. The propertyNames must be a valid property of the API class.

####Parameters
<ul><li>arrayofNames : <span class='text-info'>ARRAY</span><p>
List of properties I want to know about </p></li><ul><li><i>Object</i> : <span class='text-info'>STRING</span><p> </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li> : <span class='text-info'>STRING</span><p> </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>HASH : 
Map of properties I want to know about<ul><li> : <span class='text-info'>STRING</span><p> </p></li></ul></li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.getProperties(<span class="text-info">ARRAY</span> arrayofNames)</code> </li></ul></li></ul>

### getProperty(<span class="text-info">STRING</span> propertyName)
This method will return the value of the propertyName that is passed in. The propertyName must be a valid property of the API class.

####Parameters
<ul><li>propertyName : <span class='text-info'>STRING</span><p>
The property to return info about. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING : 
The property to return info about.</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.getProperty(<span class="text-info">STRING</span> propertyName)</code> </li></ul></li></ul>

### getRegistrySetting(<span class="text-info">HASH</span> propertyMap)
Retrieve a value from the device registry. Only applicable on Windows Mobile / Embedded Handheld and CE devices. When running on RhoSimulator, this method is supported only for Windows OS.

####Parameters
<ul><li>propertyMap : <span class='text-info'>HASH</span><p>
Map of properties associated with the registry key being set. </p></li><ul><li>hive : <span class='text-info'>STRING</span><p>
The hive name, see setRegistrySetting. </p></li><li>key : <span class='text-info'>STRING</span><p>
Full path of the key, including '\' separators as required. Remember to use '\\' in JavaScript to specify backslash. </p></li><li>setting : <span class='text-info'>STRING</span><p>
The name of the setting to be retrieved. </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING : 
Registry value of the key.</li></ul>

####Platforms

* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.getRegistrySetting(<span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

### getStartParams()
Return the command line parameters. At Android start parameters are returned as URL query string starting with '?', name-value delimiter '=' and name value pairs delimiter '&'.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.getStartParams()</code> </li></ul></li></ul>

### get_locale()
Use System.locale property: Current device locale.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.get_locale()</code> </li></ul></li></ul>

### isApplicationInstalled(<span class="text-info">STRING</span> applicationName)
Checks if the specified applicationName is installed on the device.

####Parameters
<ul><li>applicationName : <span class='text-info'>STRING</span><p>
The name of the application. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>BOOLEAN</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>BOOLEAN</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.isApplicationInstalled(<span class="text-info">STRING</span> applicationName)</code> </li></ul></li></ul>

### isBlobAttr(<span class="text-info">STRING</span> partition, <span class="text-info">INTEGER</span> sourceID, <span class="text-info">STRING</span> attrName)
Use Database.SQLite3.isBlobAttr: is model attribute is blob.

####Parameters
<ul><li>partition : <span class='text-info'>STRING</span><p> </p></li><li>sourceID : <span class='text-info'>INTEGER</span><p> </p></li><li>attrName : <span class='text-info'>STRING</span><p> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>BOOLEAN</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>BOOLEAN</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.isBlobAttr(<span class="text-info">STRING</span> partition, <span class="text-info">INTEGER</span> sourceID, <span class="text-info">STRING</span> attrName)</code> </li></ul></li></ul>

### openUrl(<span class="text-info">STRING</span> url)
Open the application associated with the URL. Behavior may be different on different platforms and depend on installed software. For example, open URL with http:// prefix will execute the Web Browser installed on system and open URL in executed browser. Note: For opening pdf files on android devices it is necessary to add option "no_compression: [ pdf ]" to android section in build.yml
                

####Parameters
<ul><li>url : <span class='text-info'>STRING</span><p>
URL as string. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.openUrl(<span class="text-info">STRING</span> url)</code> </li></ul></li></ul>

### runApplication(<span class="text-info">STRING</span> appName, <span class="text-info">STRING</span> params, <span class="text-info">BOOLEAN</span> blockingCall)
Run an application.

####Parameters
<ul><li>appName : <span class='text-info'>STRING</span><p>
The name of the application on the device to run. It depends from platform. On iOS it is BundleURLScheme of executed application. </p></li><li>params : <span class='text-info'>STRING</span> <span class='label label-info'>Optional</span><p>
Start parameters string. Executed Application can receive this string by getStartParams method. Parameter could be just value, or key-value pair separated by '=' sign. Please note that for each platform there are distinct ways to write several params at once. On Android parameters should be separated by "&", on other platforms by ',' or ' '. </p></li><li>blockingCall : <span class='text-info'>BOOLEAN</span> <span class='label label-info'>Optional</span><p>
Not Implemented. 
False by default.</p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.runApplication(<span class="text-info">STRING</span> appName, <span class="text-info">STRING</span> params, <span class="text-info">BOOLEAN</span> blockingCall)</code> </li></ul></li></ul>

### setDoNotBackupAttribute(<span class="text-info">STRING</span> pathToFile, <span class="text-info">BOOLEAN</span> doNotBackup)
Set do not backup attribute for file.

####Parameters
<ul><li>pathToFile : <span class='text-info'>STRING</span><p>
Path to file. </p></li><li>doNotBackup : <span class='text-info'>BOOLEAN</span><p>
True set doNotBackup attribute to file (exclude this file from backup), false for remove doNotBackup attribute from file. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setDoNotBackupAttribute(<span class="text-info">STRING</span> pathToFile, <span class="text-info">BOOLEAN</span> doNotBackup)</code> </li></ul></li></ul>

### setNetworkStatusNotify(<span class="text-info">STRING</span> url, <span class="text-info">INTEGER</span> poll_interval)
Use Network.setStatusNotify: set network notification callback.

####Parameters
<ul><li>url : <span class='text-info'>STRING</span><p>
The url to the user-defined callback method. </p></li><li>poll_interval : <span class='text-info'>INTEGER</span><p>
IOS. The network status polling period for systems that can not notify network status change immediately. Default value is 20 seconds. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setNetworkStatusNotify(<span class="text-info">STRING</span> url, <span class="text-info">INTEGER</span> poll_interval)</code> </li></ul></li></ul>

### setProperties(<span class="text-info">HASH</span> propertyMap)
This method will set the values of a list of properties for the API class. The propertyName must be a valid property for the class and must also not be read only.

####Parameters
<ul><li>propertyMap : <span class='text-info'>HASH</span><p>
Map of properties I want to set </p></li><ul><li><i>Object</i> : <span class='text-info'>STRING</span><p> </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setProperties(<span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

### setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)
This method will set the value of a property for the API class. The propertyName must be a valid property for the class and must also not be read only.

####Parameters
<ul><li>propertyName : <span class='text-info'>STRING</span><p>
The one property name that I want to set </p></li><li>propertyValue : <span class='text-info'>STRING</span><p>
The one property value that I want to set </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)</code> </li></ul></li></ul>

### setPushNotification(<span class="text-info">STRING</span> url, <span class="text-info">STRING</span> url_params, <span class="text-info">STRING</span> push_client)
Use Push.setPushNotification: Register push callback, the method to call upon receiving a push message.

####Parameters
<ul><li>url : <span class='text-info'>STRING</span><p>
URL of the callback method. If empty, unregisters rhoconnect-push. </p></li><li>url_params : <span class='text-info'>STRING</span> <span class='label label-info'>Optional</span><p>
Parameters which will be added to callback URL. </p></li><li>push_client : <span class='text-info'>STRING</span> <span class='label label-info'>Optional</span><p>
Name of a push service client. Current values can be 'rhoconnect_push' or 'gcm' or 'legacy' or empty. 
The call will be applied to every push client.</p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setPushNotification(<span class="text-info">STRING</span> url, <span class="text-info">STRING</span> url_params, <span class="text-info">STRING</span> push_client)</code> </li></ul></li></ul>

### setRegistrySetting(<span class="text-info">HASH</span> propertyMap)
Set a value in the device registry. Only applicable on Windows Mobile / Embedded Handheld and CE devices. When running on RhoSimulator, this method is supported only for Windows OS.

####Parameters
<ul><li>propertyMap : <span class='text-info'>HASH</span><p>
Map of properties associated with the registry key being set. </p></li><ul><li>hive : <span class='text-info'>STRING</span><p>
The hive name. </p><p><strong>Possible Values</strong> :</p> <dl  ><dt>Constant: EB.System.REGKEY_CLASSES_ROOT <br/> String:HKCR</dt><dd>
Set the property in the HKEY_CLASSES_ROOT hive.</dd><dt>Constant: EB.System.REGKEY_CURRENT_USER <br/> String:HKCU</dt><dd>
Set the property in the HKEY_CURRENT_USER hive.</dd><dt>Constant: EB.System.REGKEY_LOCAL_MACHINE <br/> String:HKLM</dt><dd>
Set the property in the HKEY_LOCAL_MACHINE hive.</dd><dt>Constant: EB.System.REGKEY_USERS <br/> String:HKU</dt><dd>
Set the property in the HKEY_USERS hive.</dd></dl></li><li>type : <span class='text-info'>STRING</span><p>
The type. </p><p><strong>Possible Values</strong> :</p> <dl  ><dt>Constant: EB.System.REGTYPE_SZ <br/> String:String</dt><dd>
The type of the value being set is a string.</dd><dt>Constant: EB.System.REGTYPE_BINARY <br/> String:Binary</dt><dd>
The type of the value being set is a binary number.</dd><dt>Constant: EB.System.REGTYPE_DWORD <br/> String:DWORD</dt><dd>
The type of the value being set is a natural number (DWORD)</dd><dt>Constant: EB.System.REGTYPE_MULTI_SZ <br/> String:MultiSZ</dt><dd>
The type of the value being set is a multi line string. Separate your lines with \n (\\n in JavaScript)</dd></dl></li><li>key : <span class='text-info'>STRING</span><p>
Full path of the key, including '\' separators as required. Remember to use '\\' in JavaScript to specify backslash. </p></li><li>setting : <span class='text-info'>STRING</span><p>
The name of the registry setting to be set. </p></li><li>value : <span class='text-info'>STRING</span><p>
The registry value to be set. </p></li><li>persistent : <span class='text-info'>BOOLEAN</span><p>
Whether or not to create a corresponding merge file, setting to true will cause your value to persist across a device clean boot. A .reg file is written to the \Application folder on the device to persist the setting. </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>BOOLEAN</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>BOOLEAN : 
Whether or not the registry key was successfully set.</li></ul>

####Platforms

* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setRegistrySetting(<span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

### setScreenRotationNotification(<span class="text-info">STRING</span> url, <span class="text-info">STRING</span> url_params)
Use ScreenOrientation.setScreenOrientationEvent: Notify (call a callback method) when the screen rotates.

####Parameters
<ul><li>url : <span class='text-info'>STRING</span><p>
URL of the callback method. If empty, unregisters notification callback. </p></li><li>url_params : <span class='text-info'>STRING</span> <span class='label label-info'>Optional</span><p>
Parameters which will be added to callback URL. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setScreenRotationNotification(<span class="text-info">STRING</span> url, <span class="text-info">STRING</span> url_params)</code> </li></ul></li></ul>

### setWindowFrame(<span class="text-info">INTEGER</span> x, <span class="text-info">INTEGER</span> y, <span class="text-info">INTEGER</span> width, <span class="text-info">INTEGER</span> height)
Change application window position and size.

####Parameters
<ul><li>x : <span class='text-info'>INTEGER</span><p>
Left corner of window. </p></li><li>y : <span class='text-info'>INTEGER</span><p>
Top corner of window. </p></li><li>width : <span class='text-info'>INTEGER</span><p>
Width of window. </p></li><li>height : <span class='text-info'>INTEGER</span><p>
Height of window. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setWindowFrame(<span class="text-info">INTEGER</span> x, <span class="text-info">INTEGER</span> y, <span class="text-info">INTEGER</span> width, <span class="text-info">INTEGER</span> height)</code> </li></ul></li></ul>

### setWindowPosition(<span class="text-info">INTEGER</span> x, <span class="text-info">INTEGER</span> y)
Change application window position.

####Parameters
<ul><li>x : <span class='text-info'>INTEGER</span><p>
Left corner of window. </p></li><li>y : <span class='text-info'>INTEGER</span><p>
Top corner of window. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setWindowPosition(<span class="text-info">INTEGER</span> x, <span class="text-info">INTEGER</span> y)</code> </li></ul></li></ul>

### setWindowSize(<span class="text-info">INTEGER</span> width, <span class="text-info">INTEGER</span> height)
Change application window size.

####Parameters
<ul><li>width : <span class='text-info'>INTEGER</span><p>
Width of the window. </p></li><li>height : <span class='text-info'>INTEGER</span><p>
Width of the of window. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.setWindowSize(<span class="text-info">INTEGER</span> width, <span class="text-info">INTEGER</span> height)</code> </li></ul></li></ul>

### set_application_icon_badge(<span class="text-info">INTEGER</span> badgeNumber)
Use System.applicationIconBadge: Set the application icon to have this badge number. Set to 0 (zero) to remove badge.iOS only.

####Parameters
<ul><li>badgeNumber : <span class='text-info'>INTEGER</span><p> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.set_application_icon_badge(<span class="text-info">INTEGER</span> badgeNumber)</code> </li></ul></li></ul>

### set_http_proxy_url(<span class="text-info">STRING</span> proxyURI)
Use System.httpProxyURI property: To use client with the HTTP proxy.

####Parameters
<ul><li>proxyURI : <span class='text-info'>STRING</span><p> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.set_http_proxy_url(<span class="text-info">STRING</span> proxyURI)</code> </li></ul></li></ul>

### set_locale(<span class="text-info">STRING</span> locale_code, <span class="text-info">STRING</span> country_code)
Use Application.setLocale method: set application specific locale.

####Parameters
<ul><li>locale_code : <span class='text-info'>STRING</span><p> </p></li><li>country_code : <span class='text-info'>STRING</span><p> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.set_locale(<span class="text-info">STRING</span> locale_code, <span class="text-info">STRING</span> country_code)</code> </li></ul></li></ul>

### set_sleeping(<span class="text-info">BOOLEAN</span> enable)
Use System.screenSleeping property: enable / disable phone sleeping.

####Parameters
<ul><li>enable : <span class='text-info'>BOOLEAN</span><p> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.set_sleeping(<span class="text-info">BOOLEAN</span> enable)</code> </li></ul></li></ul>

### startTimer(<span class="text-info">INTEGER</span> interval, <span class="text-info">STRING</span> url, <span class="text-info">STRING</span> url_params)
Use Timer.start: start timer.

####Parameters
<ul><li>interval : <span class='text-info'>INTEGER</span><p>
Timer interval. </p></li><li>url : <span class='text-info'>STRING</span><p>
URL of the callback method. </p></li><li>url_params : <span class='text-info'>STRING</span> <span class='label label-info'>Optional</span><p>
Parameters which will be added to callback URL. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.startTimer(<span class="text-info">INTEGER</span> interval, <span class="text-info">STRING</span> url, <span class="text-info">STRING</span> url_params)</code> </li></ul></li></ul>

### stopTimer(<span class="text-info">STRING</span> url)
Use Timer.stop: stop timer.

####Parameters
<ul><li>url : <span class='text-info'>STRING</span><p>
URL of the callback method which identify the timer to stop. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.stopTimer(<span class="text-info">STRING</span> url)</code> </li></ul></li></ul>

### unset_http_proxy()
Use System.httpProxyURI property: Stop using HTTP proxy that was set by the command line, rhoconfig.txt or set_http_proxy_url.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.unset_http_proxy()</code> </li></ul></li></ul>

### unzipFile(<span class="text-info">STRING</span> localPathToZip, <span class="text-info">STRING</span> password)
Unzip file.

####Parameters
<ul><li>localPathToZip : <span class='text-info'>STRING</span><p>
The path to the file to be unzipped. Application should have write permissions to this folder. </p></li><li>password : <span class='text-info'>STRING</span> <span class='label label-info'>Optional</span><p>
Password for the zip. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.unzipFile(<span class="text-info">STRING</span> localPathToZip, <span class="text-info">STRING</span> password)</code> </li></ul></li></ul>

### updateBlobAttribs(<span class="text-info">STRING</span> partition, <span class="text-info">INTEGER</span> sourceID)
Use Database.updateBlobAttribs: update model blob attributes list.

####Parameters
<ul><li>partition : <span class='text-info'>STRING</span><p> </p></li><li>sourceID : <span class='text-info'>INTEGER</span><p> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.updateBlobAttribs(<span class="text-info">STRING</span> partition, <span class="text-info">INTEGER</span> sourceID)</code> </li></ul></li></ul>

### zipFile(<span class="text-info">STRING</span> localPathToZip, <span class="text-info">STRING</span> localPathToFile, <span class="text-info">STRING</span> password)
Zip one file. Zip archive must placed to the folder where application can write files. 

####Parameters
<ul><li>localPathToZip : <span class='text-info'>STRING</span><p>
The path to the specified zip. Application should have write permissions to this folder. </p></li><li>localPathToFile : <span class='text-info'>STRING</span><p>
The path to the file to be zipped. </p></li><li>password : <span class='text-info'>STRING</span> <span class='label label-info'>Optional</span><p>
Password for the zip. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.zipFile(<span class="text-info">STRING</span> localPathToZip, <span class="text-info">STRING</span> localPathToFile, <span class="text-info">STRING</span> password)</code> </li></ul></li></ul>

### zipFiles(<span class="text-info">STRING</span> localPathToZip, <span class="text-info">STRING</span> basePath, <span class="text-info">ARRAY</span> filePathsToZip, <span class="text-info">STRING</span> password)
Zip list of files.

####Parameters
<ul><li>localPathToZip : <span class='text-info'>STRING</span><p>
The path to the specified zip. </p></li><li>basePath : <span class='text-info'>STRING</span><p>
Base path to the files to be zipped. </p></li><li>filePathsToZip : <span class='text-info'>ARRAY</span><p>
List of file paths to be zipped. </p></li><li>password : <span class='text-info'>STRING</span> <span class='label label-info'>Optional</span><p>
Password for the zip. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.System.zipFiles(<span class="text-info">STRING</span> localPathToZip, <span class="text-info">STRING</span> basePath, <span class="text-info">ARRAY</span> filePathsToZip, <span class="text-info">STRING</span> password)</code> </li></ul></li></ul>

##Properties



###applicationIconBadge

####Type
<span class='text-info'>INTEGER</span> 
####Description

Set the application icon to have this badge number. Set to 0 (zero) to remove badge.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.applicationIconBadge</code> </li></ul></li></ul>

###country

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Current device country code.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.country</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###deviceName

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Name of device application running on. Examples: '9000' (BB), 'iPhone', 'dream' (Android).
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.deviceName</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###deviceOwnerEmail

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Primary email of phone owner. To access this property 'pim' capability must be enabled in your build.yml.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.deviceOwnerEmail</code> </li></ul></li></ul>


####Platforms

* Android

###deviceOwnerName

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Name(account name) of phone owner. To access this property 'pim' capability must be enabled in your build.yml.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.deviceOwnerName</code> </li></ul></li></ul>


####Platforms

* Android

###<span class="text-info">devicePushId</span>

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description
<span class='label label-info'>Replaces:deviceId</span> 
Push notifications device ID which may be used to receive push messages.To get this ID , Push service should be configured on the device. Please refer to Push documentation.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.devicePushId</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###freeServerPort

####Type
<span class='text-info'>INTEGER</span> <span class='label'>Read Only</span>
####Description

Get free local server port, available for binding.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.freeServerPort</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###hasCalendar

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description

Returns true if calendar support is available.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.hasCalendar</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###hasCamera

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description

Returns true if there is a camera available on the device.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.hasCamera</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###<span class="text-error">hasCellNetwork</span>

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description
<span class='label label-important'>Deprecated</span> 
Use Network.hasCellNetwork to tell if device is connected to the cell network.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.hasCellNetwork</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###<span class="text-error">hasNetwork</span>

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description
<span class='label label-important'>Deprecated</span> 
Use Network.hasNetwork to tell if the device is connected to the network.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.hasNetwork</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###<span class="text-error">hasSqlite</span>

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description
<span class='label label-important'>Deprecated</span> 
Returns true if the device has sqlite capabilities (previously only BlackBerry did not support this).
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.hasSqlite</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###hasTouchscreen

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description

Returns true if the device has touch screen capabilities.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.hasTouchscreen</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###<span class="text-error">hasWifiNetwork</span>

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description
<span class='label label-important'>Deprecated</span> 
Use Network.hasWifiNetwork to tell if the device is connected to the wifi network.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.hasWifiNetwork</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###<span class="text-info">httpProxyURI</span>

####Type
<span class='text-info'>STRING</span> 
####Description
<span class='label label-info'>Replaces:http_proxy_url</span> 
Set HTTP proxy parameters for using by Network module. Example: user:password@url:port . Support only basic authentication. Setting the property overrides http_proxy_uri (or http_proxy_host, http_proxy_port, http_proxy_user, http_proxy_password). To set proxy for Motorola WebKit for Windows Mobile/CE use config.xml settings.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.httpProxyURI</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###isEmulator

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description

Returns true if the application is running on a platform emulator.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.isEmulator</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###isMotorolaDevice

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description

Returns true if the device supports Motorola device capabilities. APIs will indicate if the property or method is available on MSI devices only. You can use this property to help your application decide when to take advantage of advanced MSI capabilities.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.isMotorolaDevice</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###isRhoSimulator

####Type
<span class='text-info'>BOOLEAN</span> <span class='label'>Read Only</span>
####Description

Returns true if the application is running on RhoSimulator.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.isRhoSimulator</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###keyboardState

####Type
<span class='text-info'>STRING</span> 
####Description

For Windows Mobile and Windows CE the keyboard can be manually shown or hidden as required. All other platforms only support 'automatic'. The default state for Windows Mobile and Windows CE is manual, for all other platforms it is automatic.
####Params
<p><strong>Default:</strong> See Description</p>
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.System.KEYBOARD_SHOWN 
	* String: shown
	* 
Shows the on screen keyboard, after setting the keyboard to shown or hidden it will no longer appear / disappear automatically until you set this property to automatic.
* Constant: EB.System.KEYBOARD_HIDDEN 
	* String: hidden
	* 
Hides the on screen keyboard, after setting the keyboard to shown or hidden it will no longer appear / disappear automatically until you set this property to automatic. This is most useful if your device has a hardware keyboard or you are scanning / capturing data to an input field.
* Constant: EB.System.KEYBOARD_AUTOMATIC 
	* String: automatic
	* 
Automatically shows or hides the keyboard as needed by the application.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.keyboardState</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only

###localServerPort

####Type
<span class='text-info'>INTEGER</span> <span class='label'>Read Only</span>
####Description

Port of the local (embedded) HTTP server. This parameter is mainly for debug purposes. If not specified, the platform will detect a free port on the device and use that one.
####Params
<p><strong>Default:</strong> 8080</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.localServerPort</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###locale

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Current device locale Like 'en', 'ru' etc.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.locale</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###lockWindowSize

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Lock / unlock the window size change by the user. When running on RhoSimulator, this method is supported only for Windows OS.
####Params
<p><strong>Default:</strong> false</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.lockWindowSize</code> </li></ul></li></ul>

###oemInfo

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

The OEM Information string for the terminal.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.oemInfo</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only

###osVersion

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Version OS of device. Examples: '4.6.0.192' (BB), '3.0' (iPhone), '1.6' (Android).
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.osVersion</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###phoneId

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Hardware based ID. It depends on capabilities configured for an application and has to remain same even across application uninstall/install.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.phoneId</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###platform

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Platform where application is running.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.System.PLATFORM_WM_CE 
	* String: WINDOWS
	* 
* Constant: EB.System.PLATFORM_ANDROID 
	* String: ANDROID
	* 
* Constant: EB.System.PLATFORM_IOS 
	* String: APPLE
	* 
* Constant: EB.System.PLATFORM_WP8 
	* String: WP8
	* 
* Constant: EB.System.PLATFORM_WINDOWS_DESKTOP 
	* String: WINDOWS_DESKTOP
	* 
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.platform</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###ppiX

####Type
<span class='text-info'>INTEGER</span> <span class='label'>Read Only</span>
####Description

Horizontal PPI (Pixels Per Inch).
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.ppiX</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###ppiY

####Type
<span class='text-info'>INTEGER</span> <span class='label'>Read Only</span>
####Description

Vertical PPI (Pixels Per Inch).
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.ppiY</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###realScreenHeight

####Type
<span class='text-info'>INTEGER</span> <span class='label'>Read Only</span>
####Description

Screen height in real pixels.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.realScreenHeight</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###realScreenWidth

####Type
<span class='text-info'>INTEGER</span> <span class='label'>Read Only</span>
####Description

Screen width in real pixels.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.realScreenWidth</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###screenAutoRotate

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Screen auto rotate.
####Params
<p><strong>Default:</strong> true</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.screenAutoRotate</code> </li></ul></li></ul>


####Platforms

* Android

###screenHeight

####Type
<span class='text-info'>INTEGER</span> <span class='label'>Read Only</span>
####Description

Screen height in logical pixels (used for set coordinates).
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.screenHeight</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###screenOrientation

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Current screen orientation.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.System.SCREEN_PORTRAIT 
	* String: portrait
	* 
The return value if the screen is in portrait mode.
* Constant: EB.System.SCREEN_LANDSCAPE 
	* String: landscape
	* 
The return value if the screen is in landscape mode.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.screenOrientation</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###screenSleeping

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, then screen will go to sleep by system inactivity timeout. If false then screen never go to sleep while application is in foreground.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.screenSleeping</code> </li></ul></li></ul>


####Platforms

* Android

###screenWidth

####Type
<span class='text-info'>INTEGER</span> <span class='label'>Read Only</span>
####Description

Screen width in logical pixels (used for set coordinates).
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.screenWidth</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###uuid

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

The Unique Unit IDentifier for the terminal.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.uuid</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only

###webviewFramework

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Browser framework identity string.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>EB.System.webviewFramework</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE