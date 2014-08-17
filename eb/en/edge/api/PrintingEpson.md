#PrintingEpson


## Overview
Example extension api
## Enabling the API
In order to use this API you must include the following extension in your `build.yml`.
    :::ruby
    extensions: ["printing_epson"]

The `printing_epson` extension is also included automatically if you specify the following in your `build.yml`.
    :::ruby
    app_type: "rhoelements"

NOTE: If you are building a Windows Mobile or Windows CE app with this API, you must set your app_type as "rhoelements" in your build.yml as shown [here](../guide/build_config#other-build-time-settings).
        
## Enabling the API
There are two methods of enabling the PrintingEpson API: 

* Include all ebapi modules or 
* Include only the API modules you need 

For either of these methods, you'll need to include files from the `/Enterprise Browser/JavaScript Files/Enterprise Browser` directory on the computer that you installed the Motorola Enterprise Browser.

### Include all JS API modules
To include all JS APIs, you must copy the ebapi-modules.js file to a location accessible by your app's files and include the JavaScript file in your app. For instance, to include the modules file in your index.html, with the file in the same directory as your index.html, you would add the following line to the <head> section of your index.html:

    :::html
    <script type="text/javascript" charset="utf-8" src="ebapi-modules.js"></script>

> Note: that the pathing for this file is relative to the current page.

This will define the EB class within the page. Any page you need to use the modules will need to have the .js file included in this fashion.

### Include only the modules you need
To include single APIs, you must first include the `ebapi.js` in your HTML as well as the API file you want to use. For instance, to use the PrintingEpson API, I would add the following code to my HTML file(s), assuming the API files have been copied to the same directory as the HTML.

    :::html
    <script type="text/javascript" charset="utf-8" src="ebapi.js"></script>
    <script type="text/javascript" charset="utf-8" src="eb.printer.js"></script>
    <script type="text/javascript" charset="utf-8" src="eb.printerepson.js"></script>

The ebapi.js file is necessary for all single API inclusions.
        


##Methods



### calcSumm(<span class="text-info">INTEGER</span> a, <span class="text-info">INTEGER</span> b)
Return sum of two params: a+b.

####Parameters
<ul><li>a : <span class='text-info'>INTEGER</span><p> </p></li><li>b : <span class='text-info'>INTEGER</span><p> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>INTEGER</span></p><ul></ul>

####Returns
Synchronous Return:

* INTEGER

####Method Access:

* Instance Method: This method can be accessed via an instance object of this class: 
	* <code>myObject.calcSumm(<span class="text-info">INTEGER</span> a, <span class="text-info">INTEGER</span> b)</code>
* Default Instance: This method can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.calcSumm(<span class="text-info">INTEGER</span> a, <span class="text-info">INTEGER</span> b)</code> 


### enumerate()


####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>ARRAY</span></p><ul><ul><li><i>Object</i> : <span class='text-info'>SELF_INSTANCE: EB.PrintingEpson</span><p> </p></li></ul></ul>

####Returns
Synchronous Return:

* ARRAY : Array of PrintingEpson objects.<ul><li><i>Object</i> : <span class='text-info'>SELF_INSTANCE: EB.PrintingEpson</span><p> </p></li></ul>

####Method Access:

* Class Method: This method can only be accessed via the API class object. 
	* <code>EB.PrintingEpson.enumerate()</code> 


### getAllProperties()
This method will return all of object/value pairs for the propertyNames of the API class.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li> : <span class='text-info'>STRING</span><p> </p></li></ul></ul>

####Returns
Synchronous Return:

* HASH : Map of all available properties<ul><li> : <span class='text-info'>STRING</span><p> </p></li></ul>

####Method Access:

* Instance Method: This method can be accessed via an instance object of this class: 
	* <code>myObject.getAllProperties()</code>
* Default Instance: This method can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.getAllProperties()</code> 


### getDefault()
This method will return an object that represents the default instance of the API Class. For example Camera.getDefault will return a Camera object that represents the default camera.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>SELF_INSTANCE</span></p><ul></ul>

####Returns
Synchronous Return:

* SELF_INSTANCE : Default object of Module.

####Method Access:

* Class Method: This method can only be accessed via the API class object. 
	* <code>EB.PrintingEpson.getDefault()</code> 


### getPlatformName()
Return string with platform.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:

* STRING

####Method Access:

* Instance Method: This method can be accessed via an instance object of this class: 
	* <code>myObject.getPlatformName()</code>
* Default Instance: This method can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.getPlatformName()</code> 


### getProperties(<span class="text-info">ARRAY</span> arrayofNames)
This method will return a set of object/value pairs for the list of the propertyName that is passed in. The propertyNames must be a valid property of the API class.

####Parameters
<ul><li>arrayofNames : <span class='text-info'>ARRAY</span><p>List of properties I want to know about </p></li><ul><li><i>Object</i> : <span class='text-info'>STRING</span><p> </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>HASH</span></p><ul><ul><li> : <span class='text-info'>STRING</span><p> </p></li></ul></ul>

####Returns
Synchronous Return:

* HASH : Map of properties I want to know about<ul><li> : <span class='text-info'>STRING</span><p> </p></li></ul>

####Method Access:

* Instance Method: This method can be accessed via an instance object of this class: 
	* <code>myObject.getProperties(<span class="text-info">ARRAY</span> arrayofNames)</code>
* Default Instance: This method can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.getProperties(<span class="text-info">ARRAY</span> arrayofNames)</code> 


### getProperty(<span class="text-info">STRING</span> propertyName)
This method will return the value of the propertyName that is passed in. The propertyName must be a valid property of the API class.

####Parameters
<ul><li>propertyName : <span class='text-info'>STRING</span><p>The property to return info about. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:

* STRING : The property to return info about.

####Method Access:

* Instance Method: This method can be accessed via an instance object of this class: 
	* <code>myObject.getProperty(<span class="text-info">STRING</span> propertyName)</code>
* Default Instance: This method can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.getProperty(<span class="text-info">STRING</span> propertyName)</code> 


### joinStrings(<span class="text-info">STRING</span> a, <span class="text-info">STRING</span> b)
Return join of two strings: a+b.

####Parameters
<ul><li>a : <span class='text-info'>STRING</span><p> </p></li><li>b : <span class='text-info'>STRING</span><p> </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:

* STRING

####Method Access:

* Instance Method: This method can be accessed via an instance object of this class: 
	* <code>myObject.joinStrings(<span class="text-info">STRING</span> a, <span class="text-info">STRING</span> b)</code>
* Default Instance: This method can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.joinStrings(<span class="text-info">STRING</span> a, <span class="text-info">STRING</span> b)</code> 


### setDefault(<span class="text-info">SELF_INSTANCE: EB.PrintingEpson</span> defaultInstance)
This method allows you to set the attributes of the default object instance by passing in an object of the same class.

####Parameters
<ul><li>defaultInstance : <span class='text-info'>SELF_INSTANCE: EB.PrintingEpson</span><p>An instance object that is of the same class. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:

* Void

####Method Access:

* Class Method: This method can only be accessed via the API class object. 
	* <code>EB.PrintingEpson.setDefault(<span class="text-info">SELF_INSTANCE: EB.PrintingEpson</span> defaultInstance)</code> 


### setProperties(<span class="text-info">HASH</span> propertyMap)
This method will set the values of a list of properties for the API class. The propertyName must be a valid property for the class and must also not be read only.

####Parameters
<ul><li>propertyMap : <span class='text-info'>HASH</span><p>Map of properties I want to set </p></li><ul><li><i>Object</i> : <span class='text-info'>STRING</span><p> </p></li></ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:

* Void

####Method Access:

* Instance Method: This method can be accessed via an instance object of this class: 
	* <code>myObject.setProperties(<span class="text-info">HASH</span> propertyMap)</code>
* Default Instance: This method can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.setProperties(<span class="text-info">HASH</span> propertyMap)</code> 


### setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)
This method will set the value of a property for the API class. The propertyName must be a valid property for the class and must also not be read only.

####Parameters
<ul><li>propertyName : <span class='text-info'>STRING</span><p>The one property name that I want to set </p></li><li>propertyValue : <span class='text-info'>STRING</span><p>The one property value that I want to set </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:

* Void

####Method Access:

* Instance Method: This method can be accessed via an instance object of this class: 
	* <code>myObject.setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)</code>
* Default Instance: This method can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.setProperty(<span class="text-info">STRING</span> propertyName, <span class="text-info">STRING</span> propertyValue)</code> 


##Properties



###simpleStringProperty

####Type
<span class='text-info'>STRING</span> 
####Description
Simple string property.
####Access


* Instance: This property can be accessed via an instance object of this class: <code>myObject.simpleStringProperty</code>
* Default Instance: This property can be accessed via the default instance object of this class. 
	* <code>EB.PrintingEpson.simpleStringProperty</code> 