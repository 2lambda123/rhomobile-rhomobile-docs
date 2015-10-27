#Barcode API Tutorial

This tutorial covers the use of the Enterprise Browser Barcode API.

##Prerequisites

The following are required to complete this tutorial:
* A background in HTML, CSS and JavaScript coding
* Enterprise Browser installed on a development PC 
* A Zebra mobile device and USB cable
* Enterprise Browser installed on the Zebra device 

##Coding for the Barcode API

Enterprise Browser includes an API for scanning barcodes. The steps shown below are typical for code that uses this API. The following tutorial will walk through creating a working barcode example application using these steps. 

![Barcode API tutorial image 1](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Barcode_API_tutorial_01.png?raw=true)

The resulting example application looks like this:

![Barcode API tutorial image 2](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Barcode_API_tutorial_02.png?raw=true)

##Creating the App

The following HTML template will be used as a starting point for this tutorial. It includes the following features:
* Home button that returns the user to an Enterprise Browser index page 
* Quit button that exits Enterprise Browser
* Styling to size components in an appropriate manner for use on a device

HTML Starter Template:

	:::html
	<HTML>
	<HEAD>
	<style>
	h1{font-size:2.5em;background-color:lightgray;margin:5px;padding:5px;}
	button{font-size:.5em;}
	input{font-size:1.3em;}
	#scanData{width:90%;margin:10px;}
	</style>
	</HEAD>
	<BODY>
	<h1>Barcode<br/>
	<button onclick="window.location.href='./index.html'">Home</button>
	<button onclick="EB.Application.quit();">Quit</button>
	</h1>
	<div id=content>
	</div>
	</BODY>
	<SCRIPT>
	</SCRIPT>
	</HTML>

###Create the application file:
1. Create a directory on your development machine for application files
2. Create a file named barcode.html in your application directory and open it in a text editor
3. Copy the contents of the starter template above into the file and save it

###Add input field and control buttons:
4. Open barcode.html in a text editor
5. Add an input field with the following definition to the content div

HTML:
		:::html
		<input id="scanData" type=text ><br/>

6. After the input field add two input buttons. The first button will be used to enable scanning, and the second to disable scanning. 

	:::html
	<input type=button value="Enable Scan">
	<input type=button value="Disable Scan">        

###Include the API JavaScript file:

7. The Barcode API requires the Enterprise Browser API JavaScript file. Copy the ebapi-modules.js file from `C:\EnterpriseBrowser\JavaScriptFiles\EnterpriseBrowser` to your application directory. 
 
8. Open barcode.html for editing and add the following as the first line in the HEAD section. 

	:::html
	<script type="text/javascript" charset="utf-8" src="./ebapi-modules.js"></script>

###Configure scanner settings and enable scanner
9. Add a method called fnScanEnable() to the script section that appears between the end body tag and the end html tag 

	:::JavaScript
	function fnScanEnable() { 
 	 	EB.Barcode.enable({allDecoders:true},fnBarcodeScanned); 
  		document.getElementById('scanData').value 
  	 = "enabled: press HW trigger to capture.";   
	}
        
In this method, two parameters are being passed to the enable() method. The first parameter is a hash including settings for the scanner. The second is a callback function that will be executed when data has been successfully captured. The second line of code displays a message notifying the user that the device is ready to scan. 

###Trigger a scan
1. In our demo application, scans will be triggered by the user pressing the device's hardware trigger button. It's also possible to trigger scans from an on-screen button if desired by setting up the button to call the EB,Barcode.start() method. 

>NOTE: For more information on using this method, see the Enterprise Browser Barcode API documentation on LaunchPad.

###Process the results
1. Add a method called fnBarcodeScanned() at the end of the script section to process scan results:

	:::JavaScript
	function fnBarcodeScanned(jsonObject) {
 	 console.log("Barcode Scanned:{" + JSON.stringify(jsonObject) + "}");
 	 document.getElementById('scanData').value = "barcode: " + jsonObject.data;
	}

`fnBarcodeScanned()` is the callback function we passed to enable()in the previous method. The JSON object passed to the function contains data captured during the scan. A console.log() statement is used to show the JSON object's contents for testing purposes. The last line takes the data attribute from the object and displays it in a text input field.

###Disable the scanner
1. Add the method fnScanDisable() to the script section:

:::JavaScript
	function fnScanDisable() { 
  	EB.Barcode.disable(); 
  	document.getElementById('scanData').value = "disabled: press 'enable' to scan.";  
	}

The EB.Barcode.disable() method on the first line is shuts down the scanner and prevents additional data captures. The second line displays a message for the user. 

1. Make sure to save the file periodically as you edit. 

###Hook up JavaScript method to buttons
Now that the JavaScript functions have been created we can hook them up to the control buttons.  

1. Open barcode.html and add onClick handlers to the input button tags as shown here:

	:::HTML
	<input type=button value="Enable Scan" onClick="fnScanEnable();">
	<input type=button value="Disable Scan" onClick="fnScanDisable();">         

###Copy Files to the Device

To test the application, you need to copy the application files to the device and set the StartPage setting in the Enterprise Browser config.xml file. Android- and Windows-based devices use different methods for transferring files. Please see the documentation for your device for specific instructions on copying files. 

In general, here's what is required:

1. Create a directory on your device for the Barcode application. Make sure the directory is in an unrestricted location to avoid any permissions issues when Enterprise Browser tries to open the files. 
2. Copy the barcode.html and any JavaScript API files you have included to the directory you created on the device. 
3. Copy the config.xml file from the Enterprise Browser install directory on the device to a suitable location on the development machine and open it in a text editor. 
4. Update the StartPage setting in config.xml to point to the location on the device where you placed barcode.html and then save the changes. 
5. Copy the config.xml file back to its original location on the device.  

##Testing the App
1. Tap the Enterprise Browser icon on the device. If the device is not yet licensed for Enterprise Browser, you will see the following screen:

![Barcode API tutorial image 3](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Barcode_API_tutorial_03.png?raw=true)

2. Click on the cancel button in the upper right hand corner of the screen to dismiss the message and open the Barcode app. If you turn the device sideways it should look like this:

![Barcode API tutorial image 4](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Barcode_API_tutorial_04.png?raw=true)

3. Click on the Enable Scan button.

![Barcode API tutorial image 5](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Barcode_API_tutorial_05.png?raw=true)

4. Press on the device's hardware trigger button, point the device at a barcode and wait until you hear a beep signaling that the code has been captured. You should see the barcode number displayed in the input field. 

![Barcode API tutorial image 6](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Barcode_API_tutorial_06.png?raw=true)

5. Click the Disable Scan button. Then try pressing the device's hardware trigger again. This time the device should not scan. 

![Barcode API tutorial image 7](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Barcode_API_tutorial_07.png?raw=true)

Conclusion
This completes the Enterprise Browser Barcode API tutorial. For more information on the Barcode API see the Enterprise Browser API documentation on LaunchPad.