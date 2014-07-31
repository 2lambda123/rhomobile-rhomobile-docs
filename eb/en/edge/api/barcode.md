#Barcode


## Overview
The Barcode Module provides access to control the functionality of the device's scanner. Because RhoMobile Suite is designed to run on both Consumer devices and Motorola Solutions' enterprise devices support for the Barcode API will vary for each method and properties depending on which platform you are running on. Please note that a lot these APIs are optimized for the extended functionality that Motorola Solutions devices provide. Check the platform indicators in each property or method section. In general if you are developing for a consumer device the number of symbologies available to you will be limited to just the most common ones, eg EAN13, UPCA etc and your scanning will be via the device camera. If your application is running on Motorola Solutions' hardware you will have much finer control over a more fully featured Scanner, often with a choice of scanner hardware on the device. In general if you wish to capture a single barcode in a 'one shot' use case, eg your App just wants to capture a single barcode to be submitted to a price comparison website then use Barcode.take(callback); if your application is expecting a number of barcodes to be received, common in enterprise scenarios for example a user in a warehouse then use Barcode.enable(callback). The Barcode API will not run on non-Motorola Windows Mobile / CE devices.Only the foreground application is given access to the scanning hardware, when an application is sent to the background its state will be saved and it will automatically relinquish control of the scanner. When brought back to the foreground, an application previously using the barcode API will have its previous configuration reapplied automatically.In VC70 scanner will work only if connected in SSI Mode.
## Enabling the API
In order to use this API you must TBD INSERT Eb specific instructions here

        


##Methods



### barcode_recognize(<span class="text-info">STRING</span> imageFilePath)
Recognizes a barcode on an image. Returns a string with recognized code, or empty string if the barcode is not recognized.

####Parameters
<ul><li>imageFilePath : <span class='text-info'>STRING</span><p>
Path to the image that contains the barcode to be recognized. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING : 
String with recognized code, or empty string if the barcode is not recognized.</li></ul>

####Platforms

* Android

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.barcode_recognize(<span class="text-info">STRING</span> imageFilePath)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.barcode_recognize(<span class="text-info">STRING</span> imageFilePath)</code> </li></ul></li></ul>

### commandRemoteScanner(<span class="text-info">STRING</span> command)
Instruct the connected RS507 scanner to perform some action.

####Parameters
<ul><li>command : <span class='text-info'>STRING</span><p>
The action the RS507 scanner should perform, can be 'Disconnect' which disconnects the bluetooth RS507; 'unpair' which unpairs the RS507 from the device for association with another device; 'StartPaging' or 'StopPaging' which will cause the RS507 scanner to start or stop emitting a beep, to allow it to be located. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.commandRemoteScanner(<span class="text-info">STRING</span> command)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.commandRemoteScanner(<span class="text-info">STRING</span> command)</code> </li></ul></li></ul>

### disable()
Disables the barcode scanner. This reverts the scanner to its default state and flushes any current decoder settings.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.disable()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.disable()</code> </li></ul></li></ul>

### enable(<span class="text-info">HASH</span> propertyMap)
Enabling the scanner puts it in a state where it will respond to the trigger (on devices with a hardware trigger) or will accept a command to initiate a soft scan (start method). Scanned barcodes will be available to the application through the callback provided to this method. Only one scanner on the device can be enabled at any one time, to switch between the imager and camera scanners (for example) then first disable the currently enabled scanner. If you do not specify a callback to this method you will received the scanned data as keystrokes. Note that it is necessary to enable the scanner on WM/CE devices prior to being able to retrieve the state of properties.

####Parameters
<ul><li>propertyMap : <span class='text-info'>HASH</span> <span class='label label-info'>Optional</span><p>
Provide a set of properties to configure the scanner, for example enable specific symbologies or check digits. Valid `properties` for this parameter are the properties avaliable to this API module. <a href='#Properties'>Check the property section</a> 
Not providing properties to this function will use the scanner's default properties, or those previously set on the Scanner instance.</p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li>data : <span class='text-info'>STRING</span><p>
The data decoded by the scanner or imaging device. </p></li><li>source : <span class='text-info'>STRING</span><p>
The source device and human readable decoder type of the decoded barcode or symbol. </p></li><li>type : <span class='text-info'>STRING</span><p>
Hex value representing the decoder type. </p></li><li>time : <span class='text-info'>STRING</span><p>
The time at which the decode occurred (hh:mm:ss) </p></li><li>length : <span class='text-info'>STRING</span><p>
The length of the decoded barcode or symbol. </p></li><li>direction : <span class='text-info'>STRING</span><p>
The direction the barcode was scanned, either forward, reverse or unavailable. </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.enable(<span class="text-info">HASH</span> propertyMap)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.enable(<span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

### enumerate()
Used to gain access to all scanner objects present on the device. For consumer devices you will most likely only have a single scanner, your device's camera but Enterprise grade hardware may have two or more scanners attached.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>ARRAY</span></p><ul><ul><li><i>Object</i> : <span class='text-info'>SELF_INSTANCE: EB.Barcode</span><p> </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Barcode.enumerate()</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.getAllProperties()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.getAllProperties()</code> </li></ul></li></ul>

### getDefault()
This method will return an object that represents the default instance of the API Class. For example Camera.getDefault will return a Camera object that represents the default camera.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>SELF_INSTANCE</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>SELF_INSTANCE : 
Default object of Module.</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Barcode.getDefault()</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.getProperties(<span class="text-info">ARRAY</span> arrayofNames)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.getProperties(<span class="text-info">ARRAY</span> arrayofNames)</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.getProperty(<span class="text-info">STRING</span> propertyName)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.getProperty(<span class="text-info">STRING</span> propertyName)</code> </li></ul></li></ul>

### getSupportedProperties()
Return array of properties supported by this scanner.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>ARRAY</span></p><ul><ul><li><i>Object</i> : <span class='text-info'>STRING</span><p> </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>ARRAY : 
Array of property names supported by this scanner.<ul><li><i>Object</i> : <span class='text-info'>STRING</span><p> </p></li></ul></li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.getSupportedProperties()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.getSupportedProperties()</code> </li></ul></li></ul>

### registerBluetoothStatus()
If you are using an RS507 barcode scanner you can register to receive connected or disconnected events through this method.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li>status : <span class='text-info'>STRING</span><p>
The message describing the bluetooth connection: BluetoothConnected, BluetoothDisconnected or BTScanAssociationBarcode. See below for further descriptions. </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.registerBluetoothStatus()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.registerBluetoothStatus()</code> </li></ul></li></ul>

### setDefault(<span class="text-info">SELF_INSTANCE: EB.Barcode</span> defaultInstance)
This method allows you to set the attributes of the default object instance by passing in an object of the same class.

####Parameters
<ul><li>defaultInstance : <span class='text-info'>SELF_INSTANCE: EB.Barcode</span><p>
An instance object that is of the same class. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.Barcode.setDefault(<span class="text-info">SELF_INSTANCE: EB.Barcode</span> defaultInstance)</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.setProperties(<span class="text-info">HASH</span> propertyMap)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.setProperties(<span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)</code> </li></ul></li></ul>

### start()
Performs a soft trigger start, initiating a scan without pressing the hardware trigger. If the scan does not result in a decode it is necessary to perform a soft stop before another soft start.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.start()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.start()</code> </li></ul></li></ul>

### stop()
Performs a soft trigger stop.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.stop()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.stop()</code> </li></ul></li></ul>

### take(<span class="text-info">HASH</span> propertyMap)
Enable the scanner and start capturing the barcode automatically. On Motorola Solutions' devices the amount of time to scan the barcode is defined by the scanTimeout property. On iPhone and Android if a barcode is found, the user can confirm barcode recognition, or continue to try to recognize the barcode. When the user confirms or cancels, the callback is called. Once the callback has been called the barcode hardware is disabled.This method will work only on scanners which support soft scan.

####Parameters
<ul><li>propertyMap : <span class='text-info'>HASH</span> <span class='label label-info'>Optional</span><p>
Provide a set of properties to configure the scanner, for example enable specific symbologies or check digits. Valid `properties` for this parameter are the properties avaliable to this API module. <a href='#Properties'>Check the property section</a> 
Not providing properties to this function will use the scanner's default properties, or those previously set on the Scanner instance.</p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li>barcode : <span class='text-info'>STRING</span><p>
The data decoded by the scanner or imaging device. </p></li><li>status : <span class='text-info'>STRING</span><p>
Whether or not the barcode was successfully scanned, status will be 'ok' or 'cancel' </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.take(<span class="text-info">HASH</span> propertyMap)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.take(<span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

### take_barcode(<span class="text-info">STRING</span> rubyCallbackURL, <span class="text-info">HASH</span> propertyMap)
deprecated old method for taking barcode.

####Parameters
<ul><li>rubyCallbackURL : <span class='text-info'>STRING</span><p>
Ruby callback URL. </p></li><li>propertyMap : <span class='text-info'>HASH</span> <span class='label label-info'>Optional</span><p>
Provide a set of properties to configure the scanner, for example enable specific symbologies or check digits. Valid `properties` for this parameter are the properties avaliable to this API module. <a href='#Properties'>Check the property section</a> 
Not providing properties to this function will use the scanner's default properties, or those previously set on the Scanner instance.</p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.take_barcode(<span class="text-info">STRING</span> rubyCallbackURL, <span class="text-info">HASH</span> propertyMap)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.take_barcode(<span class="text-info">STRING</span> rubyCallbackURL, <span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

##Properties



###adaptiveScanning

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables adaptive scanning. When set to true, the scan engine will automatically toggle between 2 scan angles, wide and narrow, allowing the scan engine to decode barcodes both in close proximity and far away (~100 inches). Adaptive scanning is only supported in high performance, long working range scan engines such as SE960.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.adaptiveScanning</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.adaptiveScanning</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Laser Scanners on Motorola Solutions' devices)

###aimMode

####Type
<span class='text-info'>STRING</span> 
####Description

Defines the aiming mode to use.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.AIMMODE_NONE 
	* String: none
	* 
No Aiming (Can be overridden by picklistMode).
* Constant: EB.Barcode.AIMMODE_DOT 
	* String: dot
	* 
Laser barcode readers will show a dot for aiming.
* Constant: EB.Barcode.AIMMODE_SLAB 
	* String: slab
	* 
Laser barcode readers will show a slab for aiming.
* Constant: EB.Barcode.AIMMODE_RETICLE 
	* String: reticle
	* 
Imager barcode readers will show a reticle for aiming.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.aimMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.aimMode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###aimType

####Type
<span class='text-info'>STRING</span> 
####Description

Describes the type of aiming to use.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.AIMTYPE_TRIGGER 
	* String: trigger
	* 
Standard trigger mode. Holding the trigger will start a decoding session.
* Constant: EB.Barcode.AIMTYPE_TIMED_HOLD 
	* String: timedHold
	* 
Aiming lasts for the time specified by 'timedAimDuration' before decoding. The opportunity to scan will last until the barcode is decoded or scanTimeout occurs.
* Constant: EB.Barcode.AIMTYPE_TIMED_RELEASE 
	* String: timedRelease
	* 
Aiming lasts until trigger is released. If the timedAimDuration has expired when the trigger is released then a decode session is started until a barcode is decoded or for the remaining time equal to the scanTimeout value.
* Constant: EB.Barcode.AIMTYPE_PRESENTATION 
	* String: presentation
	* 
Provided to support Kiosk devices. The scanner illuminates when movement is detected in the range of the scanner window. In order to use this mode the scanner must be initiated with a softscan using the Rho.Barcode.start() method and again after each decode. The device must be equipped with a sensor to detect movement to use presentation mode. MK31XX devices come with presentation modes preenabled in scanner driver. Aimtype should not be set to presentation for MK31xx devices as it may produce undesirable results.
* Constant: EB.Barcode.AIMTYPE_PRESS_AND_RELEASE 
	* String: pressAndRelease
	* 
Scan will continue after the trigger is released until scanTimeout occurs.
* Constant: EB.Barcode.AIMTYPE_CONTINUOUS_READ 
	* String: continuousRead
	* 
Once the trigger is pulled barcodes will continue to be scanned as long as the trigger is held, enabling rapid scanning, to be used in conjunction with sameSymbolTimeout and differentSymbolTimeout. This value is ignored if viewfinderMode is set to 'dynamicReticle'
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.aimType</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.aimType</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###allDecoders

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When set to true, the barcode scanner will read all barcode types that the scanner is capable of reading. When set to false, the barcode scanner will not be able to decode any symbologies, this is most useful if you want to set the scanner to a default state before only enabling your required symbologies. The fewer symbologies that are enabled the faster the decoding performance of the scanning engine will be. This property will return true only if all supported symbologies by the scanner are enabled, if only a subset of supported symbologies are enabled then false will be returned. Note that some decoders will not be enabled as some symbologies use the same systems to encode data, making it impossible to differentiate between them. For example: "canpostal" and "auspostal" both use a 4-state system, so devices will only enable either "canpostal" OR "auspostal" when "alldecoders" is enabled. Note that other symbologies also share the 4-state system.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.allDecoders</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.allDecoders</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE(Scanners on Motorola Solutions' devices)

###ausPostal

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Australian Postal barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.ausPostal</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.ausPostal</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###autoEnter

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, automatically appends the character code for 'enter' to the end of any barcodes scanned. This is useful if you want to submit forms following a scan without further interaction. This property will only take effect if you have not specified a callback to the enable method. AutoEnter and AutoTab are mutually exclusive properties.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.autoEnter</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.autoEnter</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###autoTab

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, automatically appends the tab character to the end of any barcodes scanned. This is useful if you are populating a form and want to jump to the next field in the form without further interaction. This property will only take effect if you have not specified a callback to the enable method. AutoTab and AutoEnter are mutually exclusive properties.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.autoTab</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.autoTab</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###aztec

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Aztec barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.aztec</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.aztec</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###barcodeDataFormat

####Type
<span class='text-info'>STRING</span> 
####Description

Specifies the format in which the barcode data is returned, binary data is returned in Data URI format with the appropriate mime type. This parameter is designed to be used primarily with image based symbologies (eg. Signature). Binary data will not be output as keystrokes, you must set a decode callback in order to receive scanned data.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.FORMAT_BINARY 
	* String: binary
	* 
Scanned data will be returned in Data URI format.
* Constant: EB.Barcode.FORMAT_TEXT 
	* String: text
	* 
Scanned data will be returned in Text format.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.barcodeDataFormat</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.barcodeDataFormat</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Camera / Imager Scanners on Motorola Solutions' devices)

###beamWidth

####Type
<span class='text-info'>STRING</span> 
####Description

Specifies the width of the laser beam. All devices will support normal beam widths but other widths may not be supported on your device.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.BEAM_NORMAL 
	* String: normal
	* 
Laser beam width is normal.
* Constant: EB.Barcode.BEAM_WIDE 
	* String: wide
	* 
Laser beam width is wide.
* Constant: EB.Barcode.BEAM_NARROW 
	* String: narrow
	* 
Laser beam width is narrow.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.beamWidth</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.beamWidth</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Laser Scanners on Motorola Solutions' devices)

###bidirectionalRedundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables bidirectional redundancy.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.bidirectionalRedundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.bidirectionalRedundancy</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Laser Scanners on Motorola Solutions' devices)

###canPostal

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Canadian Postal barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.canPostal</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.canPostal</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###chinese2of5

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Chinese 2of5 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.chinese2of5</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.chinese2of5</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###codabar

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Codabar barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.codabar</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.codabar</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###codabarClsiEditing

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables Codabar CLSi formatting when set to true.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.codabarClsiEditing</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.codabarClsiEditing</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###codabarMaxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a Codabar barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.codabarMaxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.codabarMaxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###codabarMinLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a Codabar barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.codabarMinLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.codabarMinLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###codabarNotisEditing

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables Codabar NotisEditing formatting when set to true.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.codabarNotisEditing</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.codabarNotisEditing</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###codabarRedundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the Codabar Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.codabarRedundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.codabarRedundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code11

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Code11 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code11</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code11</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code11checkDigitCount

####Type
<span class='text-info'>STRING</span> 
####Description

Specifies whether to verify 0, 1 or 2 check digits.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.CODE11_CHECKDIGIT_NONE 
	* String: none
	* 
Scanning engine will verify no Code 11 check digits.
* Constant: EB.Barcode.CODE11_CHECKDIGIT_ONE 
	* String: one
	* 
Scanning engine will verify one Code 11 check digit.
* Constant: EB.Barcode.CODE11_CHECKDIGIT_TWO 
	* String: two
	* 
Scanning engine will verify two Code 11 check digits.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code11checkDigitCount</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code11checkDigitCount</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code11maxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a Code 11 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code11maxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code11maxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code11minLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a Code 11 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code11minLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code11minLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code11redundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the Code 11 Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code11redundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code11redundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code11reportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned Code 11 barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code11reportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code11reportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Code128 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128checkIsBtTable

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, decodes concatenated Code128 output only if the pair belongs to one of the commonly concatenated pairs as defined by the standard.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128checkIsBtTable</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128checkIsBtTable</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128ean128

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, barcodes with the EAN128 subtype property set will be read.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128ean128</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128ean128</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128isbt128

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, barcodes with the isbt128 subtype property set will be read.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128isbt128</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128isbt128</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128isbt128ConcatMode

####Type
<span class='text-info'>STRING</span> 
####Description

Sets the Code128 ISBT concatenation mode property. This feature allows a pair of barcodes which meet certain criteria defined in the ISBT128 spec to be reported as a single barcode. This parameter describes the different concatenation modes available for ISBT128.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.CODE128ISBT_NEVER 
	* String: never
	* 
Will ignore the barcode pair and only output decode data for one of the barcodes.
* Constant: EB.Barcode.CODE128ISBT_ALWAYS 
	* String: always
	* 
Will not decode if both barcodes are not present or if one of them can not be decoded.
* Constant: EB.Barcode.CODE128ISBT_AUTO 
	* String: auto
	* 
Auto-Discriminate.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128isbt128ConcatMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128isbt128ConcatMode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128maxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a Code 128 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128maxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128maxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128minLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a Code 128 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128minLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128minLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128other128

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the other 128 property which enables the non EAN and non ISBT 128 subtype.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128other128</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128other128</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128redundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the Code 128 Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128redundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128redundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code128securityLevel

####Type
<span class='text-info'>INTEGER</span> 
####Description

Sets the Code 128 security level and accepts a value between 0 and 3 inclusive. 0: Allows the scanner to operate in its most aggressive state, while providing sufficient security in decoding most 'in-spec' barcodes. 1: Eliminates most mis-decodes. 2: Select this option if security level 1 fails to eliminate mis-decodes. 3: Select this option if security level 1 and 2 fail to eliminate mis-decodes. Be advised that selecting level 3 is an extreme measure against mis-decoding and will significantly impair the decoding ability of the scanner.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code128securityLevel</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code128securityLevel</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Code 39 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39code32Prefix

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables reporting of the Code32 prefix when a Code39 barcode is converted.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39code32Prefix</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39code32Prefix</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39convertToCode32

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables conversion from Code39 to Code 32 barcodes, when set the decoded barcode is converted to Code 32.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39convertToCode32</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39convertToCode32</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39fullAscii

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables full ASCII conversion of Code 39 barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39fullAscii</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39fullAscii</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39maxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a Code 39 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39maxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39maxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39minLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a Code 39 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39minLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39minLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39redundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the Code 39 Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39redundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39redundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39reportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables reporting of the Code 39 check digit when a Code 39 barcode is scanned.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39reportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39reportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39securityLevel

####Type
<span class='text-info'>INTEGER</span> 
####Description

Sets the Code 128 security level and accepts a value between 0 and 3 inclusive. 0: This setting allows the scanner to operate in its most aggressive state, while providing sufficient security in decoding most 'in-spec' barcodes. 1: This setting eliminates most mis-decodes. 2: Select this option if security level 1 fails to eliminate mis-decodes. 3: Select this option if security level 1 and 2 fail to eliminate mis-decodes. Be advised that selecting level 3 is an extreme measure against mis-decoding and will significantly impair the decoding ability of the scanner.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39securityLevel</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39securityLevel</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code39verifyCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Turns on verification of the Code 39 check digit.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code39verifyCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code39verifyCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code93

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Code 93 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code93</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code93</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code93maxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a Code 93 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code93maxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code93maxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code93minLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a Code 93 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code93minLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code93minLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###code93redundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the Code 93 Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.code93redundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.code93redundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###compositeAb

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Composite AB barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.compositeAb</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.compositeAb</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###compositeAbUccLinkMode

####Type
<span class='text-info'>STRING</span> 
####Description

Describes whether UCC link mode is enabled.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.UCC_NEVER 
	* String: never
	* 
Link flag is ignored.
* Constant: EB.Barcode.UCC_ALWAYS 
	* String: always
	* 
Composite AB barcodes are always linked.
* Constant: EB.Barcode.UCC_AUTO 
	* String: auto
	* 
Auto-discriminate whether Composite AB barcodes are linked.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.compositeAbUccLinkMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.compositeAbUccLinkMode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###compositeAbUseUpcPreambleCheckDigitRules

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

This setting causes the UPC rules specified in the UPC EAN parameters to be used when reporting composite decode data.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.compositeAbUseUpcPreambleCheckDigitRules</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.compositeAbUseUpcPreambleCheckDigitRules</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###compositeC

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Composite C barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.compositeC</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.compositeC</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###connectionIdleTimeout

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the time, in seconds, that an external scanner will be allowed to remain idle before the connection is terminated to conserve power.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.connectionIdleTimeout</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.connectionIdleTimeout</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Bluetooth Scanners on Motorola Solutions' devices)

###d2of5

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for D2of5 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.d2of5</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.d2of5</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###d2of5maxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a D2of5 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.d2of5maxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.d2of5maxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###d2of5minLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a D2of5 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.d2of5minLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.d2of5minLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###d2of5redundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the D2of5 Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.d2of5redundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.d2of5redundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###dataBufferSize

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the number of bytes allocated to receive the scanned barcode. This parameter is designed to be used primarily with image based symbologies and should not be modified unless absolutely necessary (eg. Signature).
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.dataBufferSize</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.dataBufferSize</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###datamatrix

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Datamatrix barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.datamatrix</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.datamatrix</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###dbpMode

####Type
<span class='text-info'>STRING</span> 
####Description

Describes the type of Digital Bar Pulse (DBP) being produced by the scan engine.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.DBP_NORMAL 
	* String: normal
	* 
Tells the scan engine to produce normal DBP.
* Constant: EB.Barcode.DBP_COMPOSITE 
	* String: composite
	* 
Tells the scan engine to produce composite DBP, which is 2 different sets of DBP data multiplexed together for better decode performance. In order to enable this mode it must be supported by the scanner.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.dbpMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.dbpMode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Laser Scanners on Motorola Solutions' devices)

###decodeDuration

####Type
<span class='text-info'>INTEGER</span> 
####Description

The duration of the device beeper when a barcode is scanned, in milliseconds.
####Params
<p><strong>Default:</strong> 250</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.decodeDuration</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.decodeDuration</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###decodeFrequency

####Type
<span class='text-info'>INTEGER</span> 
####Description

The frequency of the device beeper when a barcode is successfully decoded. This should be within the range of the beeper but the API will accept values in the range 0 to 65535.
####Params
<p><strong>Default:</strong> 3000</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.decodeFrequency</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.decodeFrequency</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###decodeSound

####Type
<span class='text-info'>STRING</span> 
####Description

Path to a local wave file to be played when the scanner successfully decodes a barcode. This setting overrides the scanner beeper.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.decodeSound</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.decodeSound</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###decodeVolume

####Type
<span class='text-info'>INTEGER</span> 
####Description

The volume of the device beeper when a barcode is scanned. 0 to 5 with 5 being the loudest.  The value of 0 is device dependent, some Windows Mobile / CE devices interpret this as the quietest volume; if you wish to completely disable the beeper on scan please set decodeSound to an empty or invalid sound file.
####Params
<p><strong>Default:</strong> 5</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.decodeVolume</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.decodeVolume</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###differentSymbolTimeout

####Type
<span class='text-info'>INTEGER</span> 
####Description

When the aimType:continuousRead property is applied this value defines the interval between which different barcodes can be scanned. The value is specified in milliseconds, use 0 to indicate no interval between successive reads. Use this setting to allow time for the operator to reaim the device between successive scans.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.differentSymbolTimeout</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.differentSymbolTimeout</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###disconnectBtOnDisable

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Forces the scanner to disconnect from the terminal when it is 'disabled'. Since the scanner is disabled when you navigate to a new page, set this value to false if you want to maintain the bluetooth connection to your remote scanner.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.disconnectBtOnDisable</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.disconnectBtOnDisable</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Bluetooth Scanners on Motorola Solutions' devices)

###displayBtAddressBarcodeOnEnable

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If set to true the bluetooth address will be displayed as a barcode on the screen during the pairing process, initiated by calling 'enable' on a bluetooth scanner. Not all devices support this functionality. Note you must specify this parameter before or within the call to 'enable'.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.displayBtAddressBarcodeOnEnable</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.displayBtAddressBarcodeOnEnable</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Bluetooth Scanners on Motorola Solutions' devices)

###dpmMode

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Allows Direct Part Marking (DPM) barcodes to be read When true, but may adversely affect overall decoding performance. DPM is a way of stamping barcodes directly on physical objects and is only available on DPM terminals.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.dpmMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.dpmMode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Imager / Camera Scanners on Motorola Solutions' devices. The scanning engine must support DPM barcodes.)

###dutchPostal

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Dutch Postal barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.dutchPostal</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.dutchPostal</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###ean13

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for EAN 13 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.ean13</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.ean13</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###ean8

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for EAN 8 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.ean8</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.ean8</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###ean8convertToEan13

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, EAN 8 barcodes will be converted to EAN 13 and EAN 13 parameters used.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.ean8convertToEan13</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.ean8convertToEan13</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###enableTimeout

####Type
<span class='text-info'>INTEGER</span> 
####Description

Configures the time (in seconds) allowed to pair with the external bluetooth scanner after calling the 'enable()' method. You must specify this parameter before calling 'enable' to change the default.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.enableTimeout</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.enableTimeout</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Bluetooth Scanners on Motorola Solutions' devices)

###focusMode

####Type
<span class='text-info'>STRING</span> 
####Description

Sets the focus mode in use.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.FOCUS_FIXED 
	* String: fixed
	* 
Use fixed focus.
* Constant: EB.Barcode.FOCUS_AUTO 
	* String: auto
	* 
Use auto focus.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.focusMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.focusMode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Imager / Camera Scanners on Motorola Solutions' devices)

###friendlyName

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Returns the friendly name associated with the scanner.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.friendlyName</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.friendlyName</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###gs1dataBar

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for GS1 DataBar barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance. This symbology was previously known as rss.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.gs1dataBar</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.gs1dataBar</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###gs1dataBarExpanded

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for GS1 Databar Expanded barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance. This symbology was previously known as rssExp.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.gs1dataBarExpanded</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.gs1dataBarExpanded</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###gs1dataBarLimited

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for GS1 Databar Limited barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance. This symbology was previously known as rssLim.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.gs1dataBarLimited</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.gs1dataBarLimited</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###hapticFeedback

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Controls the haptic feedback on decode. This means that if this is set to true, then the device will vibrate when a decode occurs.
####Params
<p><strong>Default:</strong> true</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.hapticFeedback</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.hapticFeedback</code> </li></ul></li></ul>


####Platforms

* Android
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###i2of5

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for I2of5 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.i2of5</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.i2of5</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###i2of5convertToEan13

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, EAN 8 barcodes will be converted to EAN 13 and EAN 13 parameters used.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.i2of5convertToEan13</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.i2of5convertToEan13</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###i2of5maxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a I2of5 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.i2of5maxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.i2of5maxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###i2of5minLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a I2of5 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.i2of5minLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.i2of5minLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###i2of5redundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the I2of5 Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.i2of5redundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.i2of5redundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###i2of5reportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned I2of5 barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.i2of5reportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.i2of5reportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###i2of5verifyCheckDigit

####Type
<span class='text-info'>STRING</span> 
####Description

Enables the verification of the I2of5 check digit.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.I2OF5_VERIFY_NONE 
	* String: none
	* 
Disables verification of the check digit.
* Constant: EB.Barcode.I2OF5_VERIFY_USS 
	* String: uss
	* 
Enables the USS format for the check digit.
* Constant: EB.Barcode.I2OF5_VERIFY_OPCC 
	* String: opcc
	* 
Enables the OPCC format for the check digit.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.i2of5verifyCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.i2of5verifyCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###illuminationMode

####Type
<span class='text-info'>STRING</span> 
####Description

Selects the illumination mode to use.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.ILLUMINATION_AUTO 
	* String: auto
	* 
Auto-exposure algorithms will decide whether illumination is required or not. Not available on Android.
* Constant: EB.Barcode.ILLUMINATION_ALWAYS_ON 
	* String: alwaysOn
	* 
External illumination is always on.
* Constant: EB.Barcode.ILLUMINATION_ALWAYS_OFF 
	* String: alwaysOff
	* 
External illumination is always off.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.illuminationMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.illuminationMode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Imager / Camera Scanners on Motorola Solutions' devices)

###invalidDecodeFrequency

####Type
<span class='text-info'>INTEGER</span> 
####Description

The frequency of the device beeper when a barcode is scanned but not successfully decoded. This should be within the range of the beeper but the API will accept values in the range 0 to 65535.
####Params
<p><strong>Default:</strong> 2500</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.invalidDecodeFrequency</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.invalidDecodeFrequency</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###invalidDecodeSound

####Type
<span class='text-info'>STRING</span> 
####Description

Path to a local wave file to be played when a barcode is scanned but not successfully decoded. This setting overrides the scanner beeper.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.invalidDecodeSound</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.invalidDecodeSound</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###inverse1dMode

####Type
<span class='text-info'>STRING</span> 
####Description

Allows the user to select inverse 1D barcodes for decoding.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.INVERSE_ENABLED 
	* String: enabled
	* 
Inverse 1D symbology decoding is enabled.
* Constant: EB.Barcode.INVERSE_DISABLED 
	* String: disabled
	* 
Inverse 1D symbology decoding is disabled.
* Constant: EB.Barcode.INVERSE_AUTO 
	* String: auto
	* 
Allows decoding of both positive and inverse 1D symbologies.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.inverse1dMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.inverse1dMode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices. The scanning engine must support inverse barcodes)

###japPostal

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Japanese Postal barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.japPostal</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.japPostal</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###klasseEins

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the Klasse Eins laser on time function.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.klasseEins</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.klasseEins</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Laser Scanners on Motorola Solutions' devices)

###korean3of5

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Korean 3of5 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.korean3of5</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.korean3of5</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###korean3of5maxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a Korean 3of5 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.korean3of5maxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.korean3of5maxLength</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###korean3of5minLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a Korean 3of5 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.korean3of5minLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.korean3of5minLength</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###korean3of5redundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets Korean 3of5 Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.korean3of5redundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.korean3of5redundancy</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###lcdMode

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Controls whether LCD Mode is enabled on the scanner. LCD Mode makes it easier to scan barcodes off of LCD screens (like mobile device screens)
####Params
<p><strong>Default:</strong> false</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.lcdMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.lcdMode</code> </li></ul></li></ul>


####Platforms

* Android
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###linearSecurityLevel

####Type
<span class='text-info'>STRING</span> 
####Description

Describes the linear security level used during decoding. This determines the number of times a barcode must be read before it is decoded. If the successive reads of the barcode do not match, it will not be decoded.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.REDUNDANCY_AND_LENGTH 
	* String: redundancyAndLength
	* 
Double redundancy based on redundancy flags and code length. Only applicable to laser scanners, not BlockBuster imager scanners.
* Constant: EB.Barcode.SHORT_OR_CODABAR 
	* String: shortOrCodabar
	* 
Double redundancy if short barcode or Codabar.
* Constant: EB.Barcode.LONG_AND_SHORT 
	* String: longAndShort
	* 
Double redundancy for long barcodes, triple for short barcodes.
* Constant: EB.Barcode.ALL_TWICE 
	* String: allTwice
	* 
Double redundancy for all barcodes.
* Constant: EB.Barcode.ALL_THRICE 
	* String: allThrice
	* 
Triple redundancy for all barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.linearSecurityLevel</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.linearSecurityLevel</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###lowBatteryScan

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Set to false to disable scanning when the battery is low/critical or set to true to enable it.
####Params
<p><strong>Default:</strong> false</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.lowBatteryScan</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.lowBatteryScan</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###macroMicroPdf

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for MacroMicroPDF barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroMicroPdf</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroMicroPdf</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###macroMicroPdfBufferLabels

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, the scanner driver will return the barcode data only after the complete macroMicroPdf sequence has been read. If false, the scanner driver will return each barcode in the macroMicroPdf sequence as it is read.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroMicroPdfBufferLabels</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroMicroPdfBufferLabels</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###macroMicroPdfConvertToMicroPdf

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, MacroMicroPDF barcodes will be converted to MicroPDF codes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroMicroPdfConvertToMicroPdf</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroMicroPdfConvertToMicroPdf</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###macroMicroPdfExclusive

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, the scanner driver will not complete read requests while in the middle of a macroMicroPdf sequence. Once a macroMicroPdf sequence has been started it must be completed or canceled before the scan driver will complete other read requests.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroMicroPdfExclusive</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroMicroPdfExclusive</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###macroMicroPdfReportAppendInfo

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, the appended info is concatenated to the decoded data before being returned.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroMicroPdfReportAppendInfo</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroMicroPdfReportAppendInfo</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###macroPdf

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Macro PDF barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroPdf</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroPdf</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###macroPdfBufferLabels

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the scanner driver will return  he barcode data only after the complete macroPdf sequence has been read. If false, the scan driver will return each barcode in the macroPdf sequence as it is read.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroPdfBufferLabels</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroPdfBufferLabels</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###macroPdfConvertToPdf417

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, MacroPDF barcodes will be converted to PDF417 codes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroPdfConvertToPdf417</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroPdfConvertToPdf417</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###macroPdfExclusive

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, the scanner driver will not complete read requests while in the middle of a macroPdf sequence. Once a macroPdf sequence has been started it must be completed or canceled before the scan driver will complete other read requests.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.macroPdfExclusive</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.macroPdfExclusive</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###matrix2of5

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Matrix 2of5 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.matrix2of5</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.matrix2of5</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###matrix2of5maxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a Matrix 2of5 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.matrix2of5maxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.matrix2of5maxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###matrix2of5minLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a Matrix 2of5 barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.matrix2of5minLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.matrix2of5minLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###matrix2of5reportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned Matrix 2of5 barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.matrix2of5reportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.matrix2of5reportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###matrix2of5verifyCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables verification of the Matrix 2of5 symbology check digit.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.matrix2of5verifyCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.matrix2of5verifyCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###maxiCode

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Maxicode barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.maxiCode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.maxiCode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###microPdf

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Micro PDF barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.microPdf</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.microPdf</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###microQr

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Micro QR barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.microQr</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.microQr</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###msi

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for MSI barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.msi</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.msi</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###msiCheckDigitScheme

####Type
<span class='text-info'>STRING</span> 
####Description

Specifies the check digit scheme used to verify MSI barcodes.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.MSI_CHECKDIGITS_MOD11 
	* String: mod11
	* 
The first check digit is MOD 11, the second is MOD 10.
* Constant: EB.Barcode.MSI_CHECKDIGITS_MOD10 
	* String: mod10
	* 
Both check digits are MOD 10.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.msiCheckDigitScheme</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.msiCheckDigitScheme</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###msiCheckDigits

####Type
<span class='text-info'>STRING</span> 
####Description

Sets the number of MSI check digits to use.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.MSI_CHECKDIGITS_ONE 
	* String: one
	* 
Use one check digit for MSI barcodes.
* Constant: EB.Barcode.MSI_CHECKDIGITS_TWO 
	* String: two
	* 
Use two check digits for MSI barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.msiCheckDigits</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.msiCheckDigits</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###msiMaxLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the maximum number of allowable characters in a MSI barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.msiMaxLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.msiMaxLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###msiMinLength

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the minimum number of allowable characters in a MSI barcode. If your application only expects barcode lengths in a certain range, reducing the allowed range can improve scanning performance. Allowed values are 0 to 55.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.msiMinLength</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.msiMinLength</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###msiRedundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the MSI Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.msiRedundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.msiRedundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###msiReportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned MSI barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.msiReportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.msiReportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###pdf417

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for PDF 417 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.pdf417</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.pdf417</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###picklistMode

####Type
<span class='text-info'>STRING</span> 
####Description

Allows the imager to decode only the barcode that is directly under the cross-hair / center of the reticle. This feature is most useful in applications where multiple barcodes may appear in the field of view during a decode session and only one of them is targeted for decode. When enabled picklistMode will override aimMode or, if no aiming is chosen, and use aimMode:reticle. This mode will also interact with viewfinderMode, see the EMDK for C help file for more information. Enabling picklist mode may adversely affect overall decoding performance.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.PICKLIST_DISABLED 
	* String: disabled
	* 
Disables picklist mode so any barcode within the field of view can be decoded.
* Constant: EB.Barcode.PICKLIST_HARDWARE_RETICLE 
	* String: hardwareReticle
	* 
Enables picklist mode so that only the barcode under the projected reticle can be decoded. On Windows, if the imager does not support a projected reticle then the behavior is the same as softwareReticle. On Android, this is only supported for Imager (non-viewfinder) based scanners.
* Constant: EB.Barcode.PICKLIST_SOFTWARE_RETICLE 
	* String: softwareReticle
	* 
Enables picklist mode so that only the barcode in the center of the image is decoded. This is most useful when used in conjunction with static and dynamic reticle viewfinder modes. On Android, this is only supported for Camera (viewfinder) based scanners.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.picklistMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.picklistMode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Imager / Camera Scanners on Motorola Solutions' devices)

###poorQuality1dMode

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Allows poor quality 1D barcodes to be read When true, but this will adversely affect the overall decoding performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.poorQuality1dMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.poorQuality1dMode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Imager / Camera Scanners on Motorola Solutions' devices)

###qrCode

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for QR Code barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.qrCode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.qrCode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###rasterHeight

####Type
<span class='text-info'>INTEGER</span> 
####Description

Vertical rastering height to use, as a percentage, when rasterMode:openAlways is applied. This value must be between 0 and 100.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rasterHeight</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rasterHeight</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Laser Scanners on Motorola Solutions' devices)

###rasterMode

####Type
<span class='text-info'>STRING</span> 
####Description

Describes the type of vertical rastering to use.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.RASTER_NONE 
	* String: none
	* 
No vertical rastering.
* Constant: EB.Barcode.RASTER_OPEN_ALWAYS 
	* String: openAlways
	* 
Vertical rastering is always full open. To adjust the rastering height use the rasterHeight property.
* Constant: EB.Barcode.RASTER_SMART 
	* String: smart
	* 
Vertical rastering mode is 'Smart'.
* Constant: EB.Barcode.RASTER_CYCLONE 
	* String: cyclone
	* 
Vertical rastering mode is 'Cyclone'.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rasterMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rasterMode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###rsmBatteryCapacity

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

The remaining capacity of the battery, in the range 0 to 100. 'unknown' will be returned if the capacity could not be determined, for example if the scanner had no battery.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBatteryCapacity</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBatteryCapacity</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBatteryId

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

One of 'simple', 'double', 'disabled' or 'unknown'
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBatteryId</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBatteryId</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBatteryStatus

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Indicates the status of the remote scanner's battery, will be one of 'unknown', 'full', 'medium', 'empty', 'chargingFullRate', 'chargingHalfRate', 'chargingTrickle' or 'discharging'
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBatteryStatus</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBatteryStatus</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothAddress

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Bluetooth address as FF:FF:FF:FF:FF:FF where FF is a hex number.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothAddress</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothAddress</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothAuthentication

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

True if authentication is required.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothAuthentication</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothAuthentication</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothAutoReconnect

####Type
<span class='text-info'>STRING</span> 
####Description

Bluetooth reconnection scheme.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.RSM_AUTORECONNECT_NONE 
	* String: none
	* 
No scheme.
* Constant: EB.Barcode.RSM_AUTORECONNECT_ON_POWER 
	* String: onPower
	* 
When powered on.
* Constant: EB.Barcode.RSM_AUTORECONNECT_ON_OUT_OF_RANGE 
	* String: onOutOfRange
	* 
When device goes out of range.
* Constant: EB.Barcode.RSM_AUTORECONNECT_ON_POWER_OUT_OF_RANGE 
	* String: onPowerOutOfRange
	* 
When powered on or when the device goes out of range.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothAutoReconnect</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothAutoReconnect</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothBeepOnReconnectAttempt

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, scanner will emit 5 beeps every 5 seconds whilst re-connection in progress.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothBeepOnReconnectAttempt</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothBeepOnReconnectAttempt</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothEncryption

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

True if encryption is required.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothEncryption</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothEncryption</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothFriendlyName

####Type
<span class='text-info'>STRING</span> 
####Description

Friendly Bluetooth name, e.g. 'MyBTScanner'
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothFriendlyName</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothFriendlyName</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothHidAutoReconnect

####Type
<span class='text-info'>STRING</span> 
####Description

'neverReconnect', 'reconnectOnData' or 'reconnectImmediately'
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothHidAutoReconnect</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothHidAutoReconnect</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothInquiryMode

####Type
<span class='text-info'>STRING</span> 
####Description

To use a general inquiry mode, 'general' else, 'limited'
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothInquiryMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothInquiryMode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothPinCode

####Type
<span class='text-info'>STRING</span> 
####Description

Up to 5 character PIN code used for Bluetooth authentication.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothPinCode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothPinCode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothPinCodeType

####Type
<span class='text-info'>STRING</span> 
####Description

'UseStored' will use the PIN code stored in the memory of the ring scanner, by default '12345'. 'PromptUser' indicates that the ring scanner should be used to scan 5 alpha numeric barcodes to define the PIN, eg. "1", "2", "3", "4", "5" (for PIN 12345). This parameter is not saved permanently on the ring scanner.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothPinCodeType</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothPinCodeType</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmBluetoothReconnectionAttempts

####Type
<span class='text-info'>INTEGER</span> 
####Description

How long the scanner tries to re-establish connection if it goes out of range, in seconds. This value must be a multiple of 5 and in the range 30 to 60 seconds.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmBluetoothReconnectionAttempts</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmBluetoothReconnectionAttempts</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmDateOfManufacture

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Ring scanner date of manufacture as DDMMYY.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmDateOfManufacture</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmDateOfManufacture</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmDateOfService

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Ring scanner date of service as DDMMYY.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmDateOfService</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmDateOfService</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmDecodeFeedback

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, the remote scanner beeps and illuminates its green LED on a successful decode.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmDecodeFeedback</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmDecodeFeedback</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmDeviceClass

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

The device class of the ring scanner.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmDeviceClass</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmDeviceClass</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmFirmwareVersion

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Scanner's operating system version.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmFirmwareVersion</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmFirmwareVersion</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmForceSavePairingBarcode

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Force saving the barcode assigned to the device to which the scanner has been paired.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmForceSavePairingBarcode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmForceSavePairingBarcode</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmGoodScansDelay

####Type
<span class='text-info'>INTEGER</span> 
####Description

Delay between good scans in proximity continuous mode, measured in milliseconds. Range 0 to 15000. This value must be a multiple of 100.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmGoodScansDelay</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmGoodScansDelay</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmIgnoreCode128Usps

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Feature for ignoring Code 128 barcodes beginning with 420 and 421.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmIgnoreCode128Usps</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmIgnoreCode128Usps</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmLowBatteryIndication

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Whether or not the ring scanner should give a low battery indication.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmLowBatteryIndication</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmLowBatteryIndication</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmLowBatteryIndicationCycle

####Type
<span class='text-info'>INTEGER</span> 
####Description

Low battery indication cycle time, in seconds. Must be one of 15, 30, 60, 90 or 120.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmLowBatteryIndicationCycle</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmLowBatteryIndicationCycle</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmMems

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If you press the trigger on an RSM scanner, proximity enabled will be turned off, even though it still reports its self as being turned on if you query the property. In order to use ProximityEnable you need to also have Mems enabled, this is the motion sensor and if you disable Mems the scanner will not function.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmMems</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmMems</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmModelNumber

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Ring scanner model number.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmModelNumber</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmModelNumber</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmPagingBeepSequence

####Type
<span class='text-info'>INTEGER</span> 
####Description

Range 0 to 15 to specify the pattern for the paging beep sequence.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmPagingBeepSequence</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmPagingBeepSequence</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmPagingEnable

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Specify whether paging the device is enabled.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmPagingEnable</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmPagingEnable</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmProximityContinuous

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Proximity continuous mode.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmProximityContinuous</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmProximityContinuous</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmProximityDistance

####Type
<span class='text-info'>STRING</span> 
####Description

Specify the distance for the proximity feature as 'short', 'medium' or 'long' 
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmProximityDistance</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmProximityDistance</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmProximityEnable

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If you press the trigger on an RSM scanner, proximity enabled will be turned off, even though it still reports its self as being turned on if you query the property. In order to use ProximityEnable you need to also have Mems enabled, this is the motion sensor and if you disable Mems the scanner will not function.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmProximityEnable</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmProximityEnable</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmScanLineWidth

####Type
<span class='text-info'>STRING</span> 
####Description

The laser scan line width, 'wide' or 'narrow'.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmScanLineWidth</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmScanLineWidth</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmScanTriggerWakeup

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Scanner trigger will wakeup the device from a low power state.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmScanTriggerWakeup</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmScanTriggerWakeup</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###rsmSerialNumber

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

Ring scanner serial number.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.rsmSerialNumber</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.rsmSerialNumber</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Motorola Solutions' Bluetooth barcode scanners, model RS507)

###sameSymbolTimeout

####Type
<span class='text-info'>INTEGER</span> 
####Description

When the aimType:continuousRead property is applied this value defines the interval between which the same barcode can be decoded twice. The value is specified in milliseconds, use 0 to indicate no interval between successive reads. Use this value to prevent accidental duplicate scans.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.sameSymbolTimeout</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.sameSymbolTimeout</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###scanTimeout

####Type
<span class='text-info'>INTEGER</span> 
####Description

Maximum time in milliseconds that laser scanners will emit a beam or imager scanners will enable the imager. A value of 0 indicates an infinite timeout. This parameter is compatible with aimType:trigger, aimType:timedHold, aimType:timedRelease and aimType:pressAndRelease. Note that for regulatory reasons scanTimeout is not configurable on all laser/imager scanners.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.scanTimeout</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.scanTimeout</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###scannerType

####Type
<span class='text-info'>STRING</span> <span class='label'>Read Only</span>
####Description

The type of scanner in use, will be one of 'Camera', 'Imager' or 'Laser'. Camera scanners capture and process an image taken via the devices camera. Imager scanners rely on capturing and processing an image of the barcode via dedicated scanning hardware. Both camera and imager scanners are capable of decoding 1D and 2D barcodes. Laser scanners are only capable of decoding 1D barcodes and rely on a sweeping laser.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.scannerType</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.scannerType</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE(All Scanners)

###signature

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Signature barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance. Signature barcodes return their data in Data URI format, it is recommended you adjust the dataBufferSize and barcodeDataFormat properties when scanning Signature barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.signature</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.signature</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###signatureImageHeight

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the output height of the captured signature barcode. Signature barcodes return their data in Data URI format, it is recommended you adjust the dataBufferSize and barcodeDataFormat properties when scanning Signature barcodes. Provide a number greater than or equal to 20.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.signatureImageHeight</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.signatureImageHeight</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###signatureImageQuality

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the output quality of the captured signature barcode. Signature barcodes return their data in Data URI format, it is recommended you adjust the dataBufferSize and barcodeDataFormat properties when scanning Signature barcodes. Provide a value between 10 and 100 inclusive.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.signatureImageQuality</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.signatureImageQuality</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###signatureImageWidth

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the output width of the captured signature barcode. Signature barcodes return their data in Data URI format, it is recommended you adjust the dataBufferSize and barcodeDataFormat properties when scanning Signature barcodes. Provide a number greater than or equal to 20.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.signatureImageWidth</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.signatureImageWidth</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###timedAimDuration

####Type
<span class='text-info'>INTEGER</span> 
####Description

Duration in milliseconds for aimType:timedHold and aimType:timedRelease.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.timedAimDuration</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.timedAimDuration</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###tlc39

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for TLC 39 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.tlc39</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.tlc39</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###triggerConnected

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Only applies to an enabled laser or imaging scanner. Disconnecting the trigger will prevent the scan beam from being emitted, this can temporarily prevent a user from scanning without having to disable the scanner, which can take longer. By default the trigger will be connected when the scanner is first enabled, you do not have to connect it separately. Please note that disconnecting the trigger will also prevent the start method from emitting a laser. This property will only affect the scanner and will have no effect on the 'captureTrigger' API.
####Params
<p><strong>Default:</strong> true</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.triggerConnected</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.triggerConnected</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Scanners on Motorola Solutions' devices)

###trioptic39

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Trioptic 39 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.trioptic39</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.trioptic39</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###trioptic39Redundancy

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the Trioptic 39 Redundancy property, if set the barcode must be decoded twice before being accepted. This will slow scanning but improve reliability.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.trioptic39Redundancy</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.trioptic39Redundancy</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###ukPostal

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for UK Postal barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.ukPostal</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.ukPostal</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###ukPostalReportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned UK Postal barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.ukPostalReportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.ukPostalReportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanBookland

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables decoding of UPC EAN Bookland barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanBookland</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanBookland</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanBooklandFormat

####Type
<span class='text-info'>STRING</span> 
####Description

Specifies the bookland format to use when decoding UPC EAN Bookland barcodes.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.BOOKLAND_ISBN10 
	* String: isbn10
	* 
Causes 978 bookland barcodes to be reported in 10 digit mode.
* Constant: EB.Barcode.BOOKLAND_ISBN13 
	* String: isbn13
	* 
Causes 978/979 bookland barcodes to be transmitted as EAN13 as per 2007 ISBN-13 protocol.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanBooklandFormat</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanBooklandFormat</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanConvertGs1dataBarToUpcEan

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, RSS barcodes will be converted to UPC/EAN format. For this setting to work UPC/EAN symbologies must be enabled.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanConvertGs1dataBarToUpcEan</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanConvertGs1dataBarToUpcEan</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanCoupon

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables decoding of UPC EAN Coupon barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanCoupon</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanCoupon</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanLinearDecode

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Sets the linear decode property.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanLinearDecode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanLinearDecode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanRandomWeightCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, enables random weight check digit verification.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanRandomWeightCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanRandomWeightCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanRetryCount

####Type
<span class='text-info'>INTEGER</span> 
####Description

Sets the retry count for auto-discriminating for supplementals. The value must be between 2 - 20 inclusive.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanRetryCount</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanRetryCount</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanSecurityLevel

####Type
<span class='text-info'>INTEGER</span> 
####Description

Sets the Security level for decoding UPC EAN barcodes and accepts a value between 0 and 3 inclusive. 0: This setting allows the scanner to operate in its most aggressive state, while providing sufficient security in decoding most 'in-spec' barcodes. 1: This setting eliminates most mis-decodes. 2: Select this option if security level 1 fails to eliminate mis-decodes. 3: Select this option if security level 1 and 2 fail to eliminate mis-decodes. Be advised that selecting level 3 is an extreme measure against mis-decoding and will significantly impair the decoding ability of the scanner.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanSecurityLevel</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanSecurityLevel</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanSupplemental2

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, enables the supplemental barcode decoding. Note you must have upcEanSupplementalMode:always set for this parameter to take effect.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanSupplemental2</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanSupplemental2</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanSupplemental5

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, enables the supplemental barcode decoding. Note you must have upcEanSupplementalMode:always set for this parameter to take effect.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanSupplemental5</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanSupplemental5</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcEanSupplementalMode

####Type
<span class='text-info'>STRING</span> 
####Description

Describes the UPC EAN Supplemental mode.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.UPCEAN_NONE 
	* String: none
	* 
Supplementals are ignored.
* Constant: EB.Barcode.UPCEAN_AUTO 
	* String: auto
	* 
Auto-discriminates supplementals.
* Constant: EB.Barcode.UPCEAN_ALWAYS 
	* String: always
	* 
Will not decode upc/ean without supplementals.
* Constant: EB.Barcode.UPCEAN_SMART 
	* String: smart
	* 
The decoder will return the decoded value of the main block right away if it does not belong to any of the supplemental types. If the barcode starts with one of the prefixes it will search the image more aggressively for a supplemental. The scanner will try to scan the supplemental if it is present but if that fails, the main barcode will be returned.
* Constant: EB.Barcode.UPCEAN_379 
	* String: 378or379
	* 
Auto-discriminates supplemental for upc/ean codes starting with 378 or 379. Will disable reading of supplementals for any other upc/ean barcodes not starting with these values. The supplemental will be scanned if present but if scanning fails then the main barcode will be returned.
* Constant: EB.Barcode.UPCEAN_979 
	* String: 978or979
	* 
Auto-discriminates supplemental for upc/ean codes starting with 978 or 979. Will disable reading of supplementals for any other upc/ean barcodes not starting with these values. The supplemental will be scanned if present but if scanning fails then the main barcode will be returned.
* Constant: EB.Barcode.UPCEAN_439 
	* String: 414or419or434or439
	* 
Auto-discriminates supplemental for upc/ean codes starting with 414 or 419 or 434 or 439. Will disable reading of supplementals for any other upc/ean barcodes not starting with these values. The supplemental will be scanned if present but if scanning fails then the main barcode will be returned.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcEanSupplementalMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcEanSupplementalMode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upca

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for UPCA barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upca</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upca</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcaPreamble

####Type
<span class='text-info'>STRING</span> 
####Description

Controls the preamble applied to the UPCA barcode.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.UPCA_PREAMBLE_NONE 
	* String: none
	* 
Applies no preamble to the bar code.
* Constant: EB.Barcode.UPCA_PREAMBLE_SYSTEMCHAR 
	* String: systemChar
	* 
Applies system character preamble to the bar code.
* Constant: EB.Barcode.UPCA_PREAMBLE_COUNTRY 
	* String: countryAndSystemChars
	* 
Applies both system and country code preamble to the bar code.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcaPreamble</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcaPreamble</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upcaReportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned UPCA barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upcaReportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upcaReportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upce0

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for UPCE0 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upce0</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upce0</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upce0convertToUpca

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, scanned UPCE0 barcodes will be converted to UPCA and UPCA parameters used.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upce0convertToUpca</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upce0convertToUpca</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upce0preamble

####Type
<span class='text-info'>STRING</span> 
####Description

Controls the preamble applied to the UPCE0 barcode.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.UPCE0_PREAMBLE_NONE 
	* String: none
	* 
Applies no preamble to the bar code.
* Constant: EB.Barcode.UPCE0_PREAMBLE_SYSTEMCHAR 
	* String: systemChar
	* 
Applies system character preamble to the bar code.
* Constant: EB.Barcode.UPCE0_PREAMBLE_COUNTRY 
	* String: countryAndSystemChars
	* 
Applies both system and country code preamble to the bar code.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upce0preamble</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upce0preamble</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upce0reportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned UPCE0 barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upce0reportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upce0reportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upce1

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for UPCE1 barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upce1</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upce1</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upce1convertToUpca

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, scanned UPCE1 barcodes will be converted to UPCA and UPCA parameters used.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upce1convertToUpca</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upce1convertToUpca</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upce1preamble

####Type
<span class='text-info'>STRING</span> 
####Description

Controls the preamble applied to the UPCE1 barcode.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.UPCE1_PREAMBLE_NONE 
	* String: none
	* 
Applies no preamble to the bar code.
* Constant: EB.Barcode.UPCE1_PREAMBLE_SYSTEMCHAR 
	* String: systemChar
	* 
Applies system character preamble to the bar code.
* Constant: EB.Barcode.UPCE1_PREAMBLE_COUNTRY 
	* String: countryAndSystemChars
	* 
Applies both system and country code preamble to the bar code.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upce1preamble</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upce1preamble</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###upce1reportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned UPCE1 barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.upce1reportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.upce1reportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###us4state

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for US 4-State barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.us4state</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.us4state</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###us4stateFics

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for US 4-State FICS barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.us4stateFics</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.us4stateFics</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###usPlanet

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for US Planet barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.usPlanet</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.usPlanet</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###usPlanetReportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned US Planet barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.usPlanetReportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.usPlanetReportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###usPostNet

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for US Post Net barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.usPostNet</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.usPostNet</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###usPostNetReportCheckDigit

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

When true, the barcode check digit(s) will be reported for scanned US Post Net barcodes.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.usPostNetReportCheckDigit</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.usPostNetReportCheckDigit</code> </li></ul></li></ul>


####Platforms

* Android
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###viewfinderFeedback

####Type
<span class='text-info'>STRING</span> 
####Description

Configures the feedback given after a successful scan. This value is ignored if aimType is set to continuousRead and no feedback will be given.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.VF_FEEDBACK_ENABLED 
	* String: enabled
	* 
The last image that was successfully decoded is displayed. The time for which the image is displayed can be configured by the viewfinderFeedbackTime parameter.
* Constant: EB.Barcode.VF_FEEDBACK_DISABLED 
	* String: disabled
	* 
No feedback is given in the viewfinder after a successful decode.
* Constant: EB.Barcode.VF_FEEDBACK_RETICLE 
	* String: reticle
	* 
The last image that was successfully decoded is displayed along with a red reticle in the center of the image. The time for which the image is displayed can be configured by the viewfinderFeedbackTime parameter.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.viewfinderFeedback</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.viewfinderFeedback</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Camera Scanners on Motorola Solutions' devices)

###viewfinderFeedbackTime

####Type
<span class='text-info'>INTEGER</span> 
####Description

If the viewfinderFeedback:enabled or viewfinderFeedback:reticle are applied then the decoded barcode will remain on the screen for this duration. Specified in milliseconds.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.viewfinderFeedbackTime</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.viewfinderFeedbackTime</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Camera Scanners on Motorola Solutions' devices)

###viewfinderHeight

####Type
<span class='text-info'>INTEGER</span> 
####Description

When scanning a barcode using a Camera scanner the viewfinder preview window will be this number of pixels in height. The images displayed in the viewfinder will be scaled as appropriate.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.viewfinderHeight</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.viewfinderHeight</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Camera Scanners on Motorola Solutions' devices)

###viewfinderMode

####Type
<span class='text-info'>STRING</span> 
####Description

Configures the mode of the scanner viewfinder window. This attribute is not supported on all Scanners and will interact with the picklistMode parameter, see the EMDK for C help file for more information.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.Barcode.VIEWFINDER_ENABLED 
	* String: enabled
	* 
Only the viewfinder is enabled (not the reticle). Displays a viewfinder on the screen showing the image being captured by the camera.
* Constant: EB.Barcode.VIEWFINDER_DISABLED 
	* String: disabled
	* 
The viewfinder will not be displayed during aiming or scanning.
* Constant: EB.Barcode.VIEWFINDER_STATIC_RETICLE 
	* String: staticReticle
	* 
Displays the viewfinder as well as draws a red reticle in the center of the image which helps with tracking the barcode.
* Constant: EB.Barcode.VIEWFINDER_DYNAMIC_RETICLE 
	* String: dynamicReticle
	* 
Displays the viewfinder as well as draws a red reticle in the center of the image. If the barcode in the image is 'decodable' the reticle turns green to indicate this. This mode requires a second trigger press to decode the barcode after the reticle turns green. Not supported on Android.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.viewfinderMode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.viewfinderMode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Camera Scanners on Motorola Solutions' devices)

###viewfinderWidth

####Type
<span class='text-info'>INTEGER</span> 
####Description

When scanning a barcode using a Camera scanner the viewfinder preview window will be this number of pixels wide. The images displayed in the viewfinder will be scaled as appropriate.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.viewfinderWidth</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.viewfinderWidth</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Camera Scanners on Motorola Solutions' devices)

###viewfinderX

####Type
<span class='text-info'>INTEGER</span> 
####Description

When scanning a barcode using a Camera scanner the viewfinder preview window will appear this number of pixels from the left hand side of the screen. The images displayed in the viewfinder will be scaled as appropriate.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.viewfinderX</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.viewfinderX</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Camera Scanners on Motorola Solutions' devices)

###viewfinderY

####Type
<span class='text-info'>INTEGER</span> 
####Description

When scanning a barcode using a Camera scanner the viewfinder preview window will appear this number of pixels from the top of the screen. The images displayed in the viewfinder will be scaled as appropriate.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.viewfinderY</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.viewfinderY</code> </li></ul></li></ul>


####Platforms

* Windows Mobile/CE
* Motorola Solutions Devices Only(Camera Scanners on Motorola Solutions' devices)

###webcode

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Enables or disables the symbology for Webcode barcodes. If your application does not expect to scan this symbology you should disable it to improve scanning performance. Deprecated in Android 4.1 (Jelly Bean).
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.webcode</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.webcode</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

###webcodeDecodeGtSubtype

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

If true, the GT Webcode subtype will be decoded. Deprecated in Android 4.1 (Jelly Bean).
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.webcodeDecodeGtSubtype</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.Barcode.webcodeDecodeGtSubtype</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE
* Motorola Solutions Devices Only(Not all scanning engines support all symbologies or all symbology properties)

##Remarks



###Bluetooth Scanner Overview

                    
Once associated with the Device a Bluetooth Scanner will remain associated even after losing the BT connection. In order to associate a different Bluetooth scanner with the device it is necessary to scan the 'unpairing' barcode and then invoke the 'disabled' method followed by the 'enabled' method, this will allow you to scan the BT association barcode with a different scanner. You can override this default behavior using the disconnectBtOnDisable property.

The following messages will be received from the Bluetooth Scanner in the bluetoothStatus event:

**'BTScanAssociationBarcode'** 
Means the device is ready to be associated with a BT scanner. You must scan the 
association barcode. It is only necessary to scan the association 
barcode when you first associate a scanner with the device, this pairing will be remembered until
you scan the unpairing barcode.

** 'BluetoothConnected'**
The remote scanner has successfully connected to the device.
    
** 'BluetoothDisconnected'**
The remote scanner has become disconnected from the device, this may be due to loss of battery, being out
of range or scanning the 'unpairing' barcode. The scanner will attempt to reconnect automatically for
a period of time once it regains power or goes out of range, if it fails to reconnect after the specified
timeout the reconnect button on the device should be pushed. Once the unpairing barcode is scanned
it is necessary to disable the scanner and then re-enable it before another scanner can be associated.
                
                

###Viewfinder Position Parameters

                    
On Motorola Solutions' scanners the scanner viewfinder window is not infinitely resizable, when setting ViewFinderX, ViewFinderY, ViewFinderWidth and ViewFinderHeight ensure you do not exceed the size of the screen and it is recommended to use the same aspect ratio as your device. For applications designed to handle screen rotation it is recommended to use a scan window whose longest side will fit within both the screen width and screen height. If your viewfinder position fails to be applied it is recommended you query your log file to see which parameter is causing trouble, or reposition the window away from the edges of the screen.
                    
                

###Scanning and Camera Interaction

                    
In some device configurations the scanner and camera share the same hardware. Where two modules share the same physical hardware they cannot be enabled simultaneously, in this circumstance once the scanner is enabled it must be disabled before the camera can be used, and vice versa. 
                    
                

###Get Scanner Properties

                    
On WM/CE, it is first necessary to enable the scanner before most of the properties can be retrieved. The case of scanner properties will differ across platforms. In WM/CE, some of the scanner properties are not exposed to set but can be retrieved. In Android, only supported scanner properties can be retrieved in "getAllProperties" method.
                    
                

###DataWedge Interaction With Native Apps

                    
In order to use the scanner with RhoElements Native Apps you will need to either disable DataWedge or create a DataWedge profile for your app.

**Disabling Datawedge**

1. Start the DataWedge app
2. Click the menu button > "Settings" and untick "DataWedge enabled". 

**RhoElements Datawedge Profile**

1. Install your RhoElements native app,
2. Start the DataWedge app
3. Click the menu button > "New Profile" and enter a name,
4. Click on the link to the new profile in the profile list,
5. Click on "Associated apps" in the "Applications" section,
6. Click the menu button > "New app/activity",
7. Select the package name for your app,
8. Select "*",
9. Click the "Back" capacitive button,
10. Make sure the "Profile enabled" checkbox is ticked.
11. Uncheck all three "Enabled" checkboxes under the sections of:
    "Barcode input", "Keystroke output" and "Intent output".
                    
                