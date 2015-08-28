﻿#Imager API Tutorial

This tutorial covers the use of the Enterprise Browser Imager API for capturing images using a device's camera hardware.

##Prerequisites
The following are required to complete this tutorial:
* A background in HTML, CSS and JavaScript coding
* Enterprise Browser installed on a development PC 
* A Zebra mobile device and USB cable
* Enterprise Browser installed on the Zebra device

##Coding for the Imager API

Enterprise Browser includes an API for capturing images using a device's on board camera hardware. The steps shown below are typical for code that uses this API. 

The following tutorial will walk through creating a working example application using these steps. 

![Imager API tutorial image 1](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Imager_API_tutorial_01.png?raw=true)


The resulting example application will look like this:

![Imager API tutorial image 2](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Imager_API_tutorial_02.png?raw=true)

##Creating the App

The following HTML template will be used as a starting point for this tutorial. It includes the following features:

* Home button that returns the user to the Enterprise Browser start page 
* Quit button that exits Enterprise Browser
* Styling to size components in an appropriate manner for use on a device

HTML Starter Template:

  :::HTML
  <HTML>
  <HEAD>

  <script type="text/javascript" charset="utf-8" src="./ebapi-modules.js"></script>
  <style>
  h1{font-size:2.5em;background-color:lightgray;margin:5px;padding:5px;}
  button{font-size:.5em;}
  input{font-size:1.3em;}
  #content{width:250px;border:black 1px solid}
  #imgdata{margin:10px;top:150px;width:230px;height:150px;}
  </style>
  </HEAD>
  <BODY>
  <h1>Image Capture
  <button onclick="window.location.href='./index.html'">Home</button>
  <button onclick="EB.Application.quit();">Quit</button>
  </h1>
  <div id=controls >
  </div> 
  <div id=content >
  </div>
  </BODY>
  <SCRIPT>
  </SCRIPT>
  </HTML>

###Create the application file:
1. Create a directory on your development machine for application files. 
2. The Quit button relies on code in the ebapi-modules.js JavaScript file. Copy this file from C:\EnterpriseBrowser\JavaScriptFiles\EnterpriseBrowser to your application directory. 
3. Create a file named imgcap.html in your application directory and open it in a text editor.
4. Copy the contents of the starter template above into the file and save it.

###Add image display area and control buttons:
5. Open imgcap.html in a text editor.
6. Add four input buttons to the controls div. The first button will be used to activate the image capture area the others will be used to cancel the capture, capture an image and clear a currently displayed image.

  :::HTML
  <input type=button value="Open Capture Area">
  <input type=button value="Capture">
  <input type=button value="Cancel">
  <input type=button value="Clear">


7. Add an img element to the content div that can be used to display captured images. 

  :::HTML
  <img src="" id="imgdata" />
       
###Include the API JavaScript file:
8. The Imager API requires the elements.js JavaScript file. Copy elements.js file from C:\EnterpriseBrowser\JavaScriptFiles\BackwardCompatibility to your application directory. 
 
9. Open imgcap.html for editing and add the following as the first line in the HEAD section. 

  :::HTML
  <script type="text/javascript" charset="utf-8" src="./elements.js"></script>

###Initialize capture settings and display capture area: 
10. In the script section between the end body tag and the end html tag add the method fnImgCaptureEnable(). 

  :::JavaScript
  1. function fnImgCaptureEnable(){
  2.   imager.top = 155;
  3.   imager.left = 25;
  4.   imager.width = 350;
  5.   imager.height = 240;
  6.   imager.imagerCaptureEvent = 'onImageCapture(%json)';
  7.   keyCapture.triggerEvent = 'fnImgCapture()';       
  8.   imager.enable(); 
  9. }

The code in lines 2-5 sets the location on screen where the image capture area will be displayed. Line 6 sets a callback function that will be called after an image capture is triggered. Line 7 maps the hardware trigger on the device to a function we will be using to execute the image capture. And finally in line 8 we call the enable() function which displays the image capture area.    

Capture the image:
11. Add the method fnImgCapture() at the end of the script section:

  :::JavaScript
  function fnImgCapture() { 
      imager.capture(); 
      console.log("imager.capture() has been called");
  }

This method will be called when the user clicks on the Capture button or uses the device's hardware trigger button.  The capture() method will trigger the API to save the current image and use that data to execute the previously set callback function.  

Hide the capture screen:
12. Add a method called fnImgCaptureDisable() at the end of the script section:

  :::JavaScrtpt
  function fnImgCaptureDisable() { 
    imager.disable();
    keyCapture.triggerEvent = ''; 
  }

There may be situations where after displaying the image capture area the user decides not to take a picture. The fnImgCaptureDisable() is used to cancel the image capture and un-map the hardware trigger button.

Display the image:
13. Add a method called fnImgCaptureDisable() at the end of the script section:


function onImageCapture(capData){
    console.log(capData);
    document.getElementById("imgdata").src = capData.imageData;
    fnImgCaptureDisable();
}

This method takes the image that has been passed as data in the capData JSON object and assigns it to the src attribute of the img display element which displays the image on-screen. 


Add a method to clear the displayed image:
14. For convenience we will add a method to clear the displayed image:

function fnClearImage() { 
    document.getElementById("content").innerHTML = "<img src='' id=imgdata />";
    console.log("image cleared");
}

Hook up JavaScript method to buttons:
15. Now that the JavaScript functions have been created we can hook them up to the control buttons.  Open imgcap.html and add onClick handlers to the input button tags as shown here:

  :::JavaScript
  <input type=button value="Open Capture Area" onClick="fnImgCaptureEnable();">
  <input type=button value="Capture" onClick="fnImgCapture()" >
  <input type=button value="Cancel" onClick="fnImgCaptureDisable()" >
  <input type=button value="Clear"   onClick="fnClearImage()" >

##Copy Files to the Device

In order to test the application you need to copy the application files to the device and set the StartPage setting in the Enterprise Browser config.xml file. Android- and Windows-based devices use different methods for transferring files. Please see the documentation for your device for specific instructions on copying files. 

In general, here's what is required:

1. Create a directory on your device for the Imager application. Make sure the directory is in an unrestricted location to avoid any permissions issues when Enterprise Browser tries to open the files. 
2. Copy the imgcap.html and any JavaScript API files you have included to the directory you created on the device. 
3. Copy the config.xml file from the Enterprise Browser install directory on the device to a suitable location on the development machine and open it in a text editor. 
4. Update the StartPage setting in config.xml to point to the location on the device where you placed imgcap.html and then save the changes. 
5. Copy the config.xml file back to its original location on the device.

##Testing the App
1. Tap the Enterprise Browser icon on the device. If the device is not yet licensed for Enterprise Browser you will see the following screen:

![Imager API tutorial image 3](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Imager_API_tutorial_03.png?raw=true)

2. Click on the cancel button in the upper right hand corner of the screen to dismiss the message and open the Image Capture app. If you turn the device sideways it should look like this:

![Imager API tutorial image 4](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Imager_API_tutorial_04.png?raw=true)

3. Click on the Open Capture Area button to open the capture area. As you move the device around you will see the image change to whatever the device is pointing at. After focusing on the image you want to take click on the Capture button. The image is now fixed and will not change as you move the device around. 
    
![Imager API tutorial image 5](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Imager_API_tutorial_05.png?raw=true)

4. Click the Clear button and then use the Open Capture Area button again to open the capture area. Once you see that the area is active click on the Cancel button to cancel the capture. The image on the screen will be removed and the image display area will be empty again.

![Imager API tutorial image 6](https://github.com/rhomobile/rhomobile-docs/blob/master/public/images/EB_tutorials/Imager_API_tutorial_06.png?raw=true)

Conclusion
This completes the Enterprise Browser Imager API tutorial. For more information on the Imager API see the Enterprise Browser API documentation on LaunchPad.