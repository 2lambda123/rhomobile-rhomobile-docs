#AudioCapture


## Overview
Audio capture API allows you to capture audio from the device's built in microphone or input source.
## Enabling the API
In order to use this API you must include reference to the following JavaScript file that is included with the Enterprise Browser installation:

* ebapi-modules.js - this file contains all available Enterprise Browser APIs

If you wish to minimize the amount of JavaScript being included, you can choose to only include the individual API that your application is using:

ex:

* ebapi.js - core APIs needed 
* eb.audiocapture.js - just the AudioCapture API
* other individual JavaScript files included with the Enterprise Browser installation
        


##Methods



### cancel()
Cancel audio recording. During recording if 'cancel' method is called, the status of recording will be 'cancel' in the callback returning parameter of 'start' method. No file is saved. In android, it will delete the file if it exists.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.cancel()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.cancel()</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.getAllProperties()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.getAllProperties()</code> </li></ul></li></ul>

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
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.AudioCapture.getDefault()</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.getProperties(<span class="text-info">ARRAY</span> arrayofNames)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.getProperties(<span class="text-info">ARRAY</span> arrayofNames)</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.getProperty(<span class="text-info">STRING</span> propertyName)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.getProperty(<span class="text-info">STRING</span> propertyName)</code> </li></ul></li></ul>

### setDefault(<span class="text-info">SELF_INSTANCE: EB.AudioCapture</span> defaultInstance)
This method allows you to set the attributes of the default object instance by passing in an object of the same class.

####Parameters
<ul><li>defaultInstance : <span class='text-info'>SELF_INSTANCE: EB.AudioCapture</span><p>
An instance object that is of the same class. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>EB.AudioCapture.setDefault(<span class="text-info">SELF_INSTANCE: EB.AudioCapture</span> defaultInstance)</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.setProperties(<span class="text-info">HASH</span> propertyMap)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.setProperties(<span class="text-info">HASH</span> propertyMap)</code> </li></ul></li></ul>

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
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)</code> </li></ul></li></ul>

### start(<span class="text-info">HASH</span> props)
Starts capturing audio until either 'stop' is received, or 'maxDuration' is reached. The successful recording will set 'ok' as the status. An unsuccessful recording will set 'cancel' or 'error' as the status in the callback returning parameters. If 'cancel' method is called during recording, 'cancel' status will be set in the callback returning parameters. In order to restart the audio capture, if the audio capturing is already in process, it is mandatory to call 'stop' or 'cancel' method before calling 'start' method again.

####Parameters
<ul><li>props : <span class='text-info'>HASH</span><p>
Map of Audio Capture properties to be set. Valid `properties` for this parameter are the properties avaliable to this API module. <a href='#Properties'>Check the property section</a> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li>status : <span class='text-info'>STRING</span><p>
Whether or not the audio recording was successfully captured, status will be 'ok' or 'cancel' or 'error'. </p></li><li>message : <span class='text-info'>STRING</span><p>
If 'status' == 'error', then message contains error message. In all other cases, it will remain empty. </p></li><li>fileName : <span class='text-info'>STRING</span><p>
If 'status' == 'ok', then contain full file path with the file name of recorded audiofile. In all other cases, it will remain empty. </p></li></ul></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.start(<span class="text-info">HASH</span> props)</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.start(<span class="text-info">HASH</span> props)</code> </li></ul></li></ul>

### stop()
Stop audio recording. During recording if 'stop' method is called, the status of recording will be 'ok' in the callback returning parameter of 'start' method. The file is saved in user provided location.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Android
* Windows Mobile/CE

####Method Access:
<ul><li><i class="icon-file"></i>Instance Method: This method can be accessed via an instance object of this class: <ul><li><code>myObject.stop()</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This method can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.stop()</code> </li></ul></li></ul>

##Properties



###encoder

####Type
<span class='text-info'>STRING</span> 
####Description

Encoder to compress recorded audio. In Android devices, the supported encoder type is dependent upon device hardware and vendor.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: EB.AudioCapture.ENCODER_AAC 
	* String: AAC
	* 
AAC low complexity. This is the default value. If wrong or no value is specified this value will be accounted.
* Constant: EB.AudioCapture.ENCODER_AMR_NB 
	* String: AMR_NB
	* 
AMR narrow-band.
* Constant: EB.AudioCapture.ENCODER_AMR_WB 
	* String: AMR_WB
	* 
AMR wide-band.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.encoder</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.encoder</code> </li></ul></li></ul>


####Platforms

* Android

###fileName

####Type
<span class='text-info'>STRING</span> 
####Description

(Required) This parameter is used to specify the file name. The file name should be set at least once before calling 'start' method, otherwise the 'start' method will update the callback 'status' as 'error'.
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.fileName</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.fileName</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

###maxDuration

####Type
<span class='text-info'>INTEGER</span> 
####Description

Specifies the number of milliseconds of audio to capture, defining the size of the capture buffer. This is also the maximum number of milliseconds of audio to capture when the 'start' method is called if not interrupted with the 'stop' method. The duration cannot be set to less than 1000 milliseconds, if a value of less than 1000 milliseconds is specified, the interval will be defaulted to 20000 milliseconds. The default value is 20,000 milliseconds.
####Params
<p><strong>Default:</strong> 20000</p>
####Access
<ul><li><i class="icon-file"></i>Instance: This property can be accessed via an instance object of this class: <ul><li><code>myObject.maxDuration</code></li></ul></li><li><i class="icon-file"></i>Default Instance: This property can be accessed via the default instance object of this class. <ul><li><code>EB.AudioCapture.maxDuration</code> </li></ul></li></ul>


####Platforms

* Android
* Windows Mobile/CE

##Remarks



###File Name

                    
In Windows, to store the file in a particular location, specify the path with the file name. Mentioning the extension name with the file name is optional. Only *.wav files are supported. If the path is not specified with the file name, the captured file is stored in the root directory of the device. In Windows and Android, if the folder is not present, it should be created manually for storing the file in that location. In Android, the file extension depends on encoder value. If it is AAC, the extension should be '.mp4'. In all other cases, it is of '.3gpp'. If only filename is specified, it will be saved in the root directory of external storage.
                     
                

###Audio Capture

			
In Windows & Android, Audio capture will not be started, if the file name is set to null. File will not be saved for invaild file name. It will return error in the callback returning parameters with the valid reason.
			
			

###Restarting of Audio Capture

                    
Audio recording will not be restarted, if the audio recording is already in process. In order to restart the audio capture, stop or cancel method need to be invoked before invoking start method.
                    
                

###Page Refresh

                    
If the page is to be refreshed, the audio recording should be canceled. In Android, the state will be persisted.
                    
                

###Page Navigation

                    
Upon page navigation, the audio recording should be canceled.
                    
                

###Duration And File Name Settings

                    
The default values will be applied for duration if no values are provided by the user. If values are provided then it will apply the user provided values. Later if values are not provided then it will apply the last provided values for the same. The settings for duration and file name will not be applied if the audio capture is already started and in progress. In android, there might be slight omit of recording data initially.
                    
                

###Get Property Or Get Properties

                    
In Windows, 'getProperty' or 'getProperties' for fileName will return the complete path along with the extension name. For example: If file name was set to '\\Application\\AudioCapture', then 'getProperty' or 'getProperties' will return '\Application\AudioCapture.wav'. If file name was set to 'AudioCapture', then 'getProperty' or 'getProperties' will return '\AudioCapture.wav'. In Android, the fileName will return whatever is set with or without extension.
                    
                

###General

                    
On Quitting of the Application, Android will save the data in the file and gracefully exit. In Android, during suspend/resume or screen timeout the audio will keep on recording.
                    
                