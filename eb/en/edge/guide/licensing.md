#Licensing the Runtime

## Obtaining a License
To license your device you will need to log in to the Motorola web based [licensing system](http://pocketbrowserlicense.motorola.com). Please ensure you use Microsoft Internet Explorer to access the licensing system.

When you purchased your licenses, you will have been sent an email with a username and password to access the licensing system, log in using these details.

Once logged in, there are options to view your orders, where you can monitor how many licenses remain unassigned, and also to your licenses.

Click on the licensing tab followed by "Assign a License" section.  You will see a list of products for which you have available licenses.  

> TBD Insert Screen shot

Ensuring you select the correct version for the EnterpriseBrowser runtime you have installed, click on the "Assign License" link to the right.

> TBD Insert Screen Shot

You will now be presented with the licensing form; this corresponds with the licensing wizard which appears after you have started the EnterpriseBrowser runtime.  Key in the details from the device into the form provided.

> Note: The Group By field is free text and can be used to sort licenses on the website.

> TBD ScreenShot
 		
Once you have completed the form, hit submit and you will be presented with two barcodes which should be scanned into your device.  If you have a laser barcode scanner, you will need to print the license out and scan the license code in from that, alternatively, with an imager scanner you can scan the codes directly from the screen.

Please refer to following sections to learn how to apply the Runtime license.

##Device Licensing
A device license allows you to run multiple EnterpriseBrowser applications on the same device and places no limits on the number of applications allowed.

A device license consists of:

* The company name.
* A hexadecimal key.

There are two types of device license, both of which are applied in the same way.

* **Device specific licenses** are tied to the specific device and only apply to that device, trying to apply a device specific license to another device will fail.
* **Deployment licenses** are not tied to a specific device, a single deployment license will work across an entire deployment and is most useful when including the license file in your device deployment or licensing non-Motorola Solutions devices.

Once your device is licensed, a splash screen will be displayed briefly each time the application is run saying who EnterpriseBrowser has been licensed to.

> TBD ScreenShot

## Applying a Device License via the Wizard
Devices running Windows Mobile and Windows CE as well as Motorola Solutions Android devices present the user with a licensing Wizard to guide the user through licensing.

The first page of the licensing wizard has a "Cancel" button. Clicking it allows you to evaluate the software. While you are evaluating the software, the functionality is not restricted.

> TBD ScreenShot

The licensing wizard assumes you have already obtained a license via the Motorola Solutions software licensing website. The wizard will guide you through applying your license. There are two options available.

* **Internet Licensing**. This only requires you to know the order number associated with your EnterpriseBrowser licenses order. Provided your device has an internet connection not obstructed by a proxy and can contact the licensing server your device will be licensed automatically.
* **Manual Licensing**. You can also print off the license from the licensing website and manually key in your company name and license number. If you are using a Motorola Solutions device you will be able to scan the information rather than keying it in manually.

More verbose instructions on licensing your device and how to interact with the licensing server are available within the Motorola Solutions software licensing website.

## Applying a Device License via a File
There are two ways to apply a device license via a file.

* **Via a Registry key**: From the Motorola Solutions Software licensing site, after you have applied for your license you are able to download a registry key file (.reg) containing the company name and license key. On Windows Mobile and Windows CE devices, you can license the device via this registry key.
* **Via a file** on Android devices when developing hybrid applications: Create the file /mnt/sdcard/keys/rhoelements. On its first line, enter your company name associated with the license. On its second line, enter the hexadecimal license key. The easiest way to do this is to manually license one device and then the use the file /mnt/sdcard/keys/rhoelements that was created.

You can also define your device license and company name in your config.xml file as follows:

	:::xml
	<Applications>
	<Application> 
	   <LicenseKeyCompany value="Deployment License Company name"/>
	   <LicenseKey value="Deployment License Number"/>
	   ...
	</Application> 
	</Applications>

## Deployment License
If you have purchased more than 50 licenses, you can request a deployment license from the web based licensing system.  Once you have received a deployment license, you can use the same license on each of you devices; however it is important to note that you are bound by contract to install the software on devices up to the number specified in the contract.  If you wish to use the software on more devices, you will need to purchase more licenses and then update your deployment license through the same portal.
