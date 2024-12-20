# Device Capabilities

## Introduction

Rhodes provide access to device specific capabilities such as GPS, PIM, camera, SMS, video player, accelerometer, proximity detector and [native UI elements](ui).  Check the [API Compatibility Matrix](../rhoelements/apicompatibility) for complete details on which APIs are supported on the variety of operating systems.


**NOTE: As of Rhodes version 3.3.3, the [Barcode](#barcode), [NFC](#nfc), and [Inline Signature Capture](#signature-capture) APIs, as well as [Rhom data encryption](rhom#database-encryption) are removed from Rhodes. These features are only supported in Zebra RhoMobile Suite. If you wish to use these features, you will need to [upgrade to RhoMobile Suite](../rhomobile-install). Your application's build.yml will also need to be modified to [indicate the application type is 'Rhoelements'](../rhoelements/rhoelements2-native#enabling-motorola-device-capabilities). Additionally, a [RhoElements license](../rhoelements/licensing) is required.**

## System Class

The System Ruby class provides access to the system specific information.

 * [get_property](../rhodesapi/system-api#getproperty) - Get the value of a system property. [The get_property API documentation](../rhodesapi/system-api#getproperty) has a complete list of properties.
 * [app_install](../rhodesapi/system-api#appinstall) - Install an application.
 * [app_installed?](../rhodesapi/system-api#appinstalled) - Returns true if the specified application is installed on the device.
 * [app_uninstall](../rhodesapi/system-api#appuninstall) - Uninstall an application.
 * [exit](../rhodesapi/system-api#exit) - Exit the application.
 * [get_start_params](../rhodesapi/system-api#getstartparams) - Return the command line parameters as a string (iPhone only).
 * [open_url](../rhodesapi/system-api#openurl) - Open the application associated with the URL. Used to prepare for printing.
 * [run_app](../rhodesapi/system-api#runapp) - Run an application.
 * [set_application_icon_badge](../rhodesapi/system-api#setapplicationiconbadge) - Set application icon badge to a number. iPhone only.
 * [set_locale](../rhodesapi/system-api#setlocale) - Switch application locale at runtime.
 * [set_http_proxy_url](../rhodesapi/system-api#sethttpproxyurl) - To use client with the HTTP proxy, you can set its URL with this method.
 * [unset_http_proxy](../rhodesapi/system-api#unsethttpproxy) - Stop using HTTP proxy that was set by `set_http_proxy_url`.
 * [set_network_status_notify](../rhodesapi/system-api#setnetworkstatusnotify) - Set a network status notification for a callback which receives notifications when the network goes up or down.
 * [clear_network_status_notify](../rhodesapi/system-api#clearnetworkstatusnotify) - Clear network status callback from `set_network_status_notify` so notifications will not be fired.
 * [set_screen_rotation_notification](../rhodesapi/system-api#setscreenrotationnotification) - Notify (call a callback method) when the screen rotates.
 * [set_sleeping](../rhodesapi/system-api#setsleeping) - Enable/disable phone sleeping.
 * [set_push_notification](../rhodesapi/system-api#setpushnotification) - Register push callback, the method to call upon receiving a push message.
 * [set_window_frame](../rhodesapi/system-api#setwindowframe) - Change application window position and size. Implemented only for Windows desktop.
 * [set_window_position](../rhodesapi/system-api#setwindowposition) - Change application window position. Implemented only for Windows desktop.
 * [set_window_size](../rhodesapi/system-api#setwindowsize) - Change application window size. Implemented only for Windows desktop.
 * [lock_window_size](../rhodesapi/system-api#lockwindowsize) - Lock/unlock the window size change by the user. Implemented only for Windows desktop.
 * [unzip_file](../rhodesapi/system-api#unzipfile) - Unzip a file.
 * [zip_file](../rhodesapi/system-api#zipfile) - Zip one file to a specified zip.
 * [zip_files](../rhodesapi/system-api#zipfiles) - Zip several files to a specified zip.

### Sample
See layout.erb of [System API Sample application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/layout.erb)  for some of the examples of how to use System class. There is also [system test](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/SystemTest/controller.rb) which demonstrate System class usage.

## Localization 

See [Rhodes System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/Localization/index.erb) as an example.

Rhodes use localization_simplified library to support non-English languages.

Add to build.yml:

	extensions: ["rholang"]

In case of several extensions, insert space after extension name and comma:

	extensions: ["rholang", "net-http"]

Create utf-8 encoded file in app `<app_folder>/app/lang/lang_<lang_id>_<country_id>.rb` or `<app_folder>/app/lang/lang_<lang_id>.rb`. This file will be automatically loaded by rhodes based on current locale.

For Example create lang_en.rb:
	:::ruby
	module Localization
		Views = {
			:greeting => "This is test"
		}
	end

And use this string in the view:
	:::html
	<ul id="home">
		<li><%= Localization::Views[:greeting] %></li>
	</ul> 

To switch locale at runtime use:
	:::ruby
    System::set_locale('es') #set current locale to Spanish

### Details:

All non-ascii symbols should be utf-8 encoded.

To get current locale on the phone use System.get_locale method. It returns 'en', 'de', etc. locale id's.

To show localized Date and Time:
	:::ruby
	Time.now.to_formatted_s(:long)
	Time.now.strftime("%B %d, %Y %H:%M") # all names will be localized
	Date.today.to_formatted_s(:long)
	Date.today.strftime("%B %e, %Y") # all names will be localized

To show currency (see rails analog for details):
	:::ruby
	Rho::NumberHelper.number_to_currency

## Geolocation

Geolocation information is available in two ways: as an asynchronous service through Ajax calls to a predefined local URL, or in a controller using Ruby calls to the GeoLocation class.

You need to enable the GPS capability to use GeoLocation. This is done by adding the following line to build.yml:

	:::yaml
	capabilities:
	  - gps

See the [Configuration](configuration#build-time-configuration) section for more details.

The GPS receiver consumes a significant amount of energy, and should be switched off most of the time in order to preserve the device's battery life.
Any call to GeoLocation method or notification call back will power up the GPS receiver.
The GPS receiver will be switched off automatically after some time (see [Configuration](configuration#run-time-configuration) for parameters) or explicitly by GeoLocation.turnoff.
Also note that it usually takes a while to acquire the device's current position; in some cases, it may take several minutes and may not work at all indoors.

Note that in old rhodes versions (up to 2.3.1) this feature uses only GPS location provider. In more recent rhodes, it also uses network based location determination. Network based location
is not as precise as GPS, but in most cases it consumes less power and returns results faster than GPS.
Rhodes will update location using network data until the GPS signal has been received; then only GPS will be used for more precise data.

There are two ways to use GeoLocation.

 * Synchronous call to GeoLocation module for particular value.
 * Set GeoLocation notification (geoLocation.set_notification) and track location by the notification callback. In this case all location values are passed to notification as parameters in a @param variable.

Note that GeoLocation is switched off automatically when the application goes into the background, and is switched on as the application goes back to foreground.
However it is possible to switch on location services as usual while the application is in background.

See the [Rhodes-System-Api-Samples example](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/Geolocation) application for GeoLocation usage example.

### Asynchronous Ajax calls

The Rhodes framework provides a simple HTML tag for accessing Geolocation information. To use it, include the appropriate JavaScript library on your page:

* For iPhone, Android: `/public/jquery/jquery-1.6.2.min.js` and `/public/js/rhogeolocation.js`
* For Windows Mobile: `/public/js/rhogeolocation-wm.js`
* For BlackBerry: Unsupported. The BlackBerry webview control doesn't support Ajax. 

Then add one of the following tags in the appropriate location in your HTML: `<geolocation/>`, `<geolatitude/>` or `<geolongitude/>`. The included JavaScript will query a predefined URL and fill these tags with location information.

`<geolocation/>` - returns a string in the form `[formatted position];[latitude];[longitude]`. 

For example: 37.3317° North, 122.0307° West;37.331689;-122.030731

`<geolatitude/>` - returns just the latitude <br/>
`<geolongitude/>` - returns just the longitude

### GeoLocation API

Refer to the [GeoLocation API](../rhodesapi/geolocation-api) for the methods to access geolocation information from your device.

 * [latitude](../rhodesapi/geolocation-api#latitude) - Returns current latitude in degrees.
 * [longitude](../rhodesapi/geolocation-api#longitude) - Returns current longitude in degrees.
 * [known_position?, is_known_position](../rhodesapi/geolocation-api#knownposition-isknownposition) - Returns true if the location system is up and running, false otherwise, null if this feature is not supported on the device platform.
 * [set_notification](../rhodesapi/geolocation-api#setnotification) - Set callback to track location changes.
 * [haversine_distance](../rhodesapi/geolocation-api#haversinedistance) - Returns the distance between two points in miles.
 * [turnoff](../rhodesapi/geolocation-api#turnoff) - Turn off GeoLocation.

GeoCoding: You can use any free web service for direct and reverse geocoding. See our complete example of using Google geocoding web service in [Rhodes-System-Api-Samples example](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/GeoCoding).

**NOTE: On iOS and Android, real GPS starts working after the first access to the GeoLocation module. Real GPS hardware is switched off after a call to GeoLocation.turnoff. But keep in mind - any call to GeoLocation, such as getting latitude, starts the hardware GPS again!**

### Testing GeoLocation

While developing your application on Windows Mobile emulator, you may find the [FakeGPS](http://msdn.microsoft.com/en-us/library/bb158722.aspx) utility useful.

Before testing on BB simulator, select menu Simulate/GPS Location and set your position.

To provide Mock Location Data on Android, see [here](http://developer.android.com/guide/topics/location/index.html)

### Samples

Here are some examples of GeoLocation Ruby code.<a id="geolocation-setnotification-ex" />

#### Tracking location all the time
You may decide to keep track of your position right after application starts. To do that, add following to your application.rb:

	:::ruby
    class AppApplication < Rho::RhoApplication
      def on_activate_app
        #start geolocation
        GeoLocation.set_notification("/app/Settings/geo_callback", "", 3)
      end
    end

Callback points to the `geo_callback` in the Settings controller.rb:
    
	:::ruby
    class SettingsController < Rho::RhoController
      def geo_callback
        puts "geo_callback : #{@params}"
		# do something on position changes
		#...
      end
    end

#### Requiring location only on a specific view

	:::ruby
    def show_location
	  # check if we know our position	
      if !GeoLocation.known_position?
		# wait till GPS receiver acquire position
        GeoLocation.set_notification( url_for(:action => :geo_callback), "")
        redirect url_for(:action => :wait)
      else
		# show position
        render
      end
    end
    
    def geo_callback
      # navigate to `show_location` page if GPS receiver acquire position  
	  if @params['known_position'].to_i != 0 && @params['status'] =='ok'
	  
	  	GeoLocation.set_notification '', '', 2
	  	WebView.navigate url_for(:action => :map_all)
	  end
    end

#### Turning off GeoLocation as soon as the app goes off the device front page

In this code sample, /GeoLocation/ has to be replaced with an appropriate regular expression to detect the controller. This code is called from geo_callback. This decision allows you to switch off GeoLocation from a single code point in case geo_callback is set.

	:::ruby
	def geo_callback
	  puts "geo_callback : #{@params}"

	  if WebView.current_location !~ /GeoLocation/
	    puts "Stopping geo location since we are away of geo page: " + WebView.current_location
	    GeoLocation.turnoff
	    return
	  end
	end

If the app does not need location updates, and GeoLocation should still remain active, you can send an empty notification.

	:::ruby
	GeoLocation.set_notification "", "", 30

### Code Sample

See controller and view in the /app/GeoLocation folder of the [System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/GeoLocation/controller.rb) for more information.

## PIM Contacts

Rhodes provides access to the device's local phone book and stored contacts via the Ruby class RhoContact.

To allow read/modify personal information and contacts enable the pim capability. This is done by adding the following lines to build.yml:

	:::yaml
	capabilities:
	  - pim

### PIM Contacts API

Refer to the [PIM Contacts API](../rhodesapi/rhocontact-api) methods to perform the following functionality.

 * [find](../rhodesapi/rhocontact-api#find) - Returns the contacts in the device phone book.
 * [create!](../rhodesapi/rhocontact-api#create) - Create a new contact in the phonebook.
 * [destroy](../rhodesapi/rhocontact-api#destroy) - Delete this contact from the phonebook.
 * [update_attributes](../rhodesapi/rhocontact-api#updateattributes) - Find a contact in the phonebook and update its properties.

The [Contact Properties](../rhodesapi/rhocontact-api#contact-properties) lists the contact properties that are supported for all platforms, and additional contact properties supported on Android and iOS.

Example of returning a hash of hashes of all the contacts stored in the phonebook (index):

	:::ruby
	Rho::RhoContact.find(:all)

Example for Android and iOS of finding the number of contacts in the phonebook:

	:::ruby
	Rho::RhoContact.find(:first)

**NOTE: It is allowed to pass additional params hash at all platforms. Platforms that has no extended functionality will just skip these**

Example of returning a hash of all properties of the contact identified by the provided id (show):

	:::ruby
	Rho::RhoContact.find(@params['id'])

Example of finding with conditions:

	:::ruby
	@count = Rho::RhoContact.find(:count, :conditions => {:phone => 'not_nil'})
	if @params['offset']
		@offset = @params['offset'].to_i
	else
		@offset = 0;
	end
	@contacts = Rho::RhoContact.find(:all, :per_page => 10, :offset => @offset, :select => ["id", "display_name", "mobile_number"], :conditions => {:phone => 'not_nil'})    
	@contacts = {} unless @contacts
	@contacts = @contacts.sort do |x,y| 
		res = 1 if x[1]['display_name'].nil? 
		res = -1 if y[1]['display_name'].nil?
		res = x[1]['display_name'] <=> y[1]['display_name'] unless res
		res
	end

### Sample
For examples on how to use the API provided by this class, see the view and controller in the /app/Contacts folder in the [System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/Contacts/controller.rb).

## PIM Calendar/Events
Rhodes provides access to the device's local calendar and stored events via the [Ruby class RhoEvent](../rhodesapi/rhoevent-api). Click the links below for detailed information about the methods.

 * [find](../rhodesapi/rhoevent-api#find) - Returns the events in the device calendar.
 * [create!](../rhodesapi/rhoevent-api#create) - Creates a new event in the calendar. Returns a hash of the properties in the event.
 * [update_attributes](../rhodesapi/rhoevent-api#updateattributes) - Update the properties for this event and save the event in the calendar.
 * [destroy](../rhodesapi/rhoevent-api#destroy) - Remove this event from the calendar.
 * [Event hash properties](../rhodesapi/rhoevent-api#event-hash-properties) - A listing of the propeties storied in a calendar event hash, which is returned by the find method.

To allow read/modify calendar information enable the calendar capability. This is done by adding the following lines to build.yml:

	:::yaml
	capabilities:
	  - calendar

Check if the device has a calendar:
	:::ruby
	System::get_property('has_calendar')

Example of returning a hash of hashes of all the events stored in the calendar (index):
	:::ruby
	Rho::RhoEvent.find(:all) 

Example of returning a hash of all the properties of the event identified by the provided id (show):
	:::ruby
	Rho::RhoEvent.find(@params['id'])

Example of returning a hash of all properties of the events found by specified parameters (index):
	:::ruby
	start = Time.utc(2010, 'jan', 1, 0, 0, 0)
    finish = Time.utc(2012, 'dec', 31, 23, 59, 59)
    @@events = Rho::RhoEvent.find(:all, :start_date => start, 
    	:end_date => finish, :find_type => 'starting', 
        :include_repeating => true)
 
Create new event in the calendar:
	:::ruby
	created_event = Rho::RhoEvent.create!(@params['event'])

Update event in the calendar:
	:::ruby
	Rho::RhoEvent.update_attributes(@params['event'])

Delete event from the calendar:
	Rho::RhoEvent.destroy(@params['id']))

### Sample
For examples on how to use the API provided by this class, see the view and controller in the /app/Calendar folder in the [System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/Calendar/controller.rb).

## Camera

You need to enable the Camera capability. This is done by adding the following lines to build.yml:

	:::yaml
	capabilities:
	  - camera

Check if the device has a camera:
	:::ruby
	System::get_property('has_camera')

### Camera API

Refer to the [Camera API](../rhodesapi/camera-api) methods to perform the following functionality.

 * [get_camera_info](../rhodesapi/camera-api#getcamerainfo) - Get camera information.
 * [choose_picture](../rhodesapi/camera-api#choosepicture) - Choose a picture from an album.
 * [take_picture](../rhodesapi/camera-api#takepicture) - Take a picture.

You can set [extended options for take_picture on iOS and Android, for choose_picture on iPhone](../rhodesapi/camera-api#optionshashforiosandandroiddevices), and for [RhoElements Zebra devices](../rhodesapi/camera-api#optionshashforrhoelementsmotoroladevices).

### Sample

See controller and view in the /app/Image folder of the [ System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/Image/controller.rb) for more information.

Here is an example call from the System API Samples application.

	:::ruby
	settings = { :camera_type => @params['camera_type'], 
	  :color_model => @params['color_model'], :enable_editing => en_ed, 
	  :desired_width => width, :desired_height => height, :flash_mode => 'auto' }
    Camera::take_picture(url_for(:action => :camera_callback), settings)

## Barcode

**NOTE: As of Rhodes version 3.3.3, the [Barcode](#barcode) API is removed from Rhodes. This feature is only supported in Zebra RhoMobile Suite. If you wish to use this feature, you will need to [upgrade to RhoMobile Suite](../rhomobile-install). Your application's build.yml will also need to be modified to [indicate the application type is 'Rhoelements'](../rhoelements/rhoelements2-native#enabling-motorola-device-capabilities). Additionally, a [RhoElements license](../rhoelements/licensing) is required.**

You can use the [Barcode API](../rhodesapi/barcode-api) methods to recognize barcodes.

 * [barcode_recognize](../rhodesapi/barcode-api#barcoderecognize) - Recognizes a barcode on an image.
 * [take_barcode](../rhodesapi/barcode-api#takebarcode) - iPhone and Android only. Open a user interface for real-time barcode recognition from the device camera.
 * [enumerate](../rhodesapi/barcode-api#enumerate) - Get a list of scanners present on the device.
 * [enable](../rhodesapi/barcode-api#enable) - Enables the scanner.
 * [disable](../rhodesapi/barcode-api#disable)- Disables the currently enabled scanner.
 * [start](../rhodesapi/barcode-api#start) - Performs a soft trigger start.
 * [stop](../rhodesapi/barcode-api#stop) - Performs a soft trigger stop.

Barcode recognition functionality is realized as Rhode Native extension. You should add "Barcode" to extension list in build.yml, which is located in your application folder. `Barcode.barcode_recognize(image_file_full_path)` returns a string with recognized code, or an empty string if there are no recognized barcodes on the image. You can combine Camera for get picture with Barcode recognition for process barcode data - see sample below.

For barcode recognition we use Zbar library (iPhone, and Windows Mobile platforms) and ZXing library (Android and BlackBerry platforms). In this case we support next barcode types :

* WM platform: UPC-A, UPC-E, EAN-8, EAN-13, Code 39, Code 128 .
* iPhone platform: UPC-A, UPC-E, EAN-8, EAN-13, Code 39, Code 128, QR Code .
* Android and BlackBerry platforms: UPC-A, UPC-E, EAN-8, EAN-13, Code 39, Code 128, Code 93, QR Code, ITF, Codabar

**NOTE: We are very sorry, but we are removed ZBar source code from our project by ZBar license requirements. For build Barcode extension for WM, you should download ZBar sources from http://zbar.sourceforge.net/ and copy to [rhodes root]/lib/extensions/barcode/ext/barcode/shared/zbar/zbar/ folder "include" and "zbar" folders from ZBar sources. Also you should fix ZBar sources for building by Microsoft Visual Studio (move define of inner function variables to begin of functions, etc.). See detailed instructions in your Rhodes installation at /lib/extensions/barcode/ext/barcode/shared/zbar/zbar/README.TXT**

### Sample
See controller and view in the /app/BarcodeRecognizer folder of the [System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/BarcodeRecognizer/controller.rb) for more information.

## Signature Capture

The [Signature Capture API](../rhodesapi/signaturecapture-api) allows your device to take a signature and save it as an image.

Click [here for information about the SignatureCapture.take method](../rhodesapi/signaturecapture-api#take). This method opens a window for hand writing, where the user draws his signature. Signature is saved to an image file.

Example:
	:::ruby
	Rho::SignatureCapture.take(url_for( :action => :signature_callback), { :imageFormat => "jpg", :penColor => 0xff0000, :penWidth=>3, :bgColor => 0x00ff00 })

**NOTE: To take signature on Blackberry devices, press the Menu button, then select 'Capture'.**

### Inline Signature Capture
**NOTE: As of Rhodes version 3.3.3, the Inline Signature API is removed from Rhodes. This feature is only supported in Zebra RhoMobile Suite. If you wish to use this feature, you will need to [upgrade to RhoMobile Suite](../rhomobile-install). Your application's build.yml will also need to be modified to [indicate the application type is 'Rhoelements'](../rhoelements/rhoelements2-native#enabling-motorola-device-capabilities). Additionally, a [RhoElements license](../rhoelements/licensing) is required.**

Windows Mobile and Windows CE devices support signature capture started in window, which you can show over the current page (scrolling is not supported in this case). 

Refer to the [Inline Signature API](../rhodesapi/signaturecapture-api#inline-signature-api) for the inline signature capture methods.

* [visible](../rhodesapi/signaturecapture-api#visible) - Display a window for hand writing, where the user draws his signature.
* [capture](../rhodesapi/signaturecapture-api#capture) - Save the signature to an image file and call a callback.
* [clear](../rhodesapi/signaturecapture-api#clear) - Clear the signature in the window.

Example of visible method:<a id="inline-signature-ex" />

	:::ruby
	Rho::SignatureCapture.visible(true, { :imageFormat => "jpg", :penColor => 0xff0000, :penWidth=>3, :bgColor => 0x00ff00 })

To save Signature to an image file and call callback:
	:::ruby
	Rho::SignatureCapture.capture(callback_url)

Example of capture method:

	:::ruby
	Rho::SignatureCapture.capture(url_for( :action => :signature_callback))

Example of clear method:

	:::ruby
	Rho::SignatureCapture.clear()

### Sample
See controller and view in the /app/SignatureUtil folder of the [System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/SignatureUtil/controller.rb) for more information.

## Bluetooth

Bluetooth API provide access to Bluetooth serial port connection between phone and another phone, phone and PC, phone and external Bluetooth device (for example external Bluetooth GPS device).

To allow Bluetooth enable the bluetooth capability. This is done by adding the following lines to build.yml:

	:::yaml
	capabilities:
	  - bluetooth

Currently Bluetooth support has the following limitations:

* On Apple device (iPhone, iPad etc.), you can connect only to another Apple device.
* On Blackberry, if you want to make client connection to any device, you should pair devices only when on another device is running server service, because it needs to add paired device to list of devices with support serial port profile - only the devices you can see in the list of devices to connect.
* On any platform, except iPhone, you should pair your devices before making connection.
* You can change local device name for display on another device only on iOS and Android platform - for WM and BB use system settings for change local device name.
* You can not see another device name when you are using server connection on BlackBerry.
* Only one connection session can be created and used on any device. You should close your current session before making another session.
* One-to-few peers connection scheme is unsupported.

There are two steps to make connection and start using of Bluetooth :

* Make connection session: execute `Rho::BluetoothManager.create_session` and setup callback where you receive result of connection. That callback will get events related to making connection(connect ok, canceled by user, error). Connection provided by platform specific UI.
* For make connection without UI, you should execute `Rho::BluetoothManager.create_server_and_wait_for_connection` on server and `Rho::BluetoothManager.create_client_connection_to_device` on client. On client you should specify server name(display name - not Bluetooth ID!) for connect. Specify callback - callback have the same parameters with `Rho::BluetoothManager.create_session`.  You can cancel connection process by `Rho::BluetoothManager.stop_current_connection_process`
* After receiving successful result and name of connected device in create_session_callback you should setup session_callback by `Rho::BluetoothSession.set_callback` to process incoming session events from connected device (data received) or event related to this session connection(disconnect, errors).

**NOTE: Connection without UI worked only on iOS and Android platforms!**

### Bluetooth API

You can use the [BluetoothManager API](../rhodesapi/bluetoothmanager-api) to make a connection between your Bluetooth-equipped device and another Bluetooth-equipped device.

 * [is_bluetooth_available](../rhodesapi/bluetoothmanager-api#isbluetoothavailable) - Returns true if Bluetooth is available on the device, false otherwise.
 * [off_bluetooth](../rhodesapi/bluetoothmanager-api#offbluetooth) - Turn Bluetooth off.
 * [set_device_name](../rhodesapi/bluetoothmanager-api#setdevicename) - Change the local device name.
 * [get_device_name](../rhodesapi/bluetoothmanager-api#getdevicename) - Get local device name for current device.
 * [get_last_error](../rhodesapi/bluetoothmanager-api#getlasterror) - Returns the last error: OK or ERROR or CANCEL.
 * [create_session](../rhodesapi/bluetoothmanager-api#createsession) - Creates a Bluetooth session.
 * [create_server_and_wait_for_connection](../rhodesapi/bluetoothmanager-api#createserverandwaitforconnection) - Connect without a user interface. Makes the current device discoverable for another device, and waits for the client connection from the other device.
 * [create_client_connection_to_device](../rhodesapi/bluetoothmanager-api#createclientconnectiontodevice) - Connect without user interface. Make the client connection to another device.
 * [stop_current_connection_process](../rhodesapi/bluetoothmanager-api#stopcurrentconnectionprocess) - When connecting without user interface (`create_server_and_wait_for_connection`), cancel the current connection.

You can use the [BluetoothSession API](../rhodesapi/bluetoothsession-api) to manage a connection session between your Bluetooth-equipped device and another Bluetooth-equipped device.

 * [set_callback](../rhodesapi/bluetoothsession-api#setcallback) - Set the Bluetooth session callback.
 * [disconnect](../rhodesapi/bluetoothsession-api#disconnect) - Disconnect from the device.
 * [get_status](../rhodesapi/bluetoothsession-api#getstatus) - Get the session status.
 * [read](../rhodesapi/bluetoothsession-api#read) - Read data from the connected device.
 * [write](../rhodesapi/bluetoothsession-api#write) - Write data to the connected device.
 * [read_string](../rhodesapi/bluetoothsession-api#readstring) - Read string from the connected device.
 * [write_string](../rhodesapi/bluetoothsession-api#writestring) - Write string to the connected device.

### Example of Controller with using Bluetooth API

This is not a complete example (for a link to a complete example, see the link below this example). This code just shows how you can make a connection and send/receive strings.<a id="bluetooth-ex" />

	:::ruby
	require 'rho/rhocontroller'
	require 'rho/rhobluetooth'

	class BluetoothController < Rho::RhoController
	  @layout = :simplelayout
	  $connected_device = nil
  
	  def index
	    render
	  end

	  def start_bluetooth
	    if Rho::BluetoothManager.is_bluetooth_available()
	      Rho::BluetoothManager.create_session(Rho::BluetoothManager::ROLE_CLIENT, url_for( :action => :connection_callback))
	    end
	  end

	  def send_string(str)
	    Rho::BluetoothSession.write_string($connected_device, str)
	  end

	  def connection_callback 
	    if @params['status'] == Rho::BluetoothManager::OK
	       $connected_device = @params['connected_device_name']
	       Rho::BluetoothSession.set_callback($connected_device, url_for( :action => :session_callback))
	       send_string('Hello friend !')
	    end
	  end 

	  def session_callback
	     if @params['event_type'] == Rho::BluetoothSession::SESSION_INPUT_DATA_RECEIVED
	        while Rho::BluetoothSession.get_status($connected_device) > 0
	          str = Rho::BluetoothSession.read_string($connected_device)
        
	          # use received string
           
	        end
	     end
	  end

	  def close_all
	    Rho::BluetoothSession.disconnect($connected_device)
	    Rho::BluetoothManager.off_bluetooth()
	  end
      
	end

### Example of chat application using Bluetooth connection

You can find a complete example of using Bluetooth API in [Rhodes-System-Api-Samples](http://github.com/rhomobile/rhodes-system-api-samples). See Bluetooth Chat Demo page - [BluetoothChat](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/BluetoothChat/). In this example you can see how to exchange text messages between two different devices. You also can use this example for connect to external Bluetooth device (external GPS device for example) or PC or Mac (use terminal to see and send messages).


## NFC

NFC (Near Field Communication). NFC API provide access to NFC functionality. You can check NFC availability on current device and register callback for listen event when NFC tag near of device. Currently NFC supported only on Android. And also Android version must be 2.3.3 or later.
NFC API implemented in native extension. You should add "nfc" to extension list in your build.yml before start using NFC in your application. Please see detailed doc: [Rhodes NFC extension](nfc).

**NOTE: As of Rhodes version 3.3.3, the [NFC](nfc) API is removed from Rhodes. This feature is only supported in Zebra RhoMobile Suite. If you wish to use this feature, you will need to [upgrade to RhoMobile Suite](../rhomobile-install). Your application's build.yml will also need to be modified to [indicate the application type is 'Rhoelements'](../rhoelements/rhoelements2-native#enabling-motorola-device-capabilities). Additionally, a [RhoElements license](../rhoelements/licensing) is required.**

## Ringtone manager

The [Ringtone manager API](../rhodesapi/ringtonemanager-api) provides access to view/play the user's installed ringtones.

 * [get_all_ringtones](../rhodesapi/ringtonemanager-api#getallringtones) - Get all available ringtones.
 * [play](../rhodesapi/ringtonemanager-api#play) - Play a given ringtone.
 * [stop](../rhodesapi/ringtonemanager-api#stop) - Halt playing of a ringtone.

**NOTE: Currently implemented for Android, Blackberry and Windows mobile. On Blackberry, only the user installed ringtones are accessible. System preinstalled ringtones are not accessible due to Blackberry limitations.**

### Sample
See controller and view in the /app/Ringtones folder of the [System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/Ringtones/controller.rb) for more information.

## Printing

### Printing on iOS
iOS include printing support. You should prepare File for printing and open it by standart platform - use:
	:::ruby
	System.open_url(file_full_path)

We recommend prepare PDF. You can use PDF-Writer pure Ruby library for it - we include it into rhodes - just include "pdf-writer" and "thread" extensions to your application extension list in build.yml :
	:::yaml
	extensions: ["pdf-writer", "thread"] 

See example in our [System API Samples application Generate PDF example](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/GeneratePDF/controller.rb) application.


### Printing on Android
Android do not support printing. You can use any third-party application for printing, for example Google Cloud Print application for print by using of Google Cloud Print web service.
You should prepare file for printing and open it by standart platform - use:
	:::ruby
	System.open_url(file_full_path)
Android platform opens that file in application registered for file extension or show select dialog for manually choose application if there are more than one application registered for this extension.

We recommend prepare PDF. You can use PDF-Writer pure Ruby library for it - we include it into rhodes - just include "pdf-writer" and "thread" extensions to your application extension list in build.yml.
	:::yaml
	extensions: ["pdf-writer", "thread"] 

See example in our [System API Samples application Generate PDF example](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/GeneratePDF/controller.rb) application.


## PUSH Notifications
Push notification support is currently available for Android, BlackBerry, iOS, and RoConnect Push Service on Android and Windows Mobile. Please refer to [RhoConnect Device Push](../rhoconnect/push) for information on setting up RhoConnect Push on the RhoConnect server and the Rhodes client.

## Alerts

In your controller, you may call on the [Alert API](../rhodesapi/alert-api) to show popup, vibrate, or play audio file.

The methods you can use are:

 * [show_popup](../rhodesapi/alert-api#showpopup) - Bring the application up fromt and show a message.
 * [hide_popup](../rhodesapi/alert-api#hidepopup) - Close the current opened popup window.
 * [vibrate](../rhodesapi/alert-api#vibrate) - Vibrate the device.
 * [play_file](../rhodesapi/alert-api#playfile) - Play specified media type.
 * [show_status](../rhodesapi/alert-api#showstatus) - Show a status message.

You can customize the popup window's title, icon, buttons and specify callback to be called on button click:

	:::ruby
	Alert.show_popup( {
		:message => 'Some message', 
		:title => 'Custom title', 
		:icon => '/public/images/icon.png',
	    :buttons => ["Yes", "No", 
			{:id => 'cancel', :title => 'Cancel all'}],
	    :callback => url_for(:action => :on_dismiss_popup) } )

Callback Example:
	:::ruby
	def on_dismiss_popup
	  id = @params['button_id']
	  title = @params['button_title']
	  index = @params['button_index']
	  if id == 'Yes'
	    # Handle 'Yes' button
	  elsif id == 'No'
	    # Handle 'No' button
	  elsif id == 'cancel'
	    # Handle 'Cancel all' button
	  end
	end

You can use Alert.show_status in a sync notification callback:
	:::ruby
	def sync_notify
	  status = @params['status'] ? @params['status'] : ""
	  Alert.show_status( 
		"Status", 
		"#{@params['source_name']} : #{status}", 
		Rho::RhoMessages.get_message('hide'))
	end

## Timer

In your controller, you may start timer using the [Rho::Timer API](../rhodesapi/timer-api).

 * [start](../rhodesapi/timer-api#start) - Start the timer and call a callback after the timer completes.
 * [stop](../rhodesapi/timer-api#stop) - Stop the timer by callback.

For example:

    :::ruby
	Rho::Timer.start(5000, (url_for :action => :timer_callback), "test")
		
## Screen rotation
When user rotate device, Rhodes update view corresponding to new orientation. To get notification about rotation use callback:
	:::ruby
	System.set_screen_rotation_notification(callback, params) 

Callback will be called when screen has rotated (available since Rhodes 2.0).
Callback parameters are:
- width - new screen width
- height - new screen height
- degrees - screen rotation relative to portrait position

NOTE: On tablet devices with default landscape form factor degrees value in normal position will be 90

### Sample
See controller and view in the /app/ScreenRotation folder of the [System API Samples application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/ScreenRotation/controller.rb) for more information.

## Run external application
Use System.open_url : you can provide any url with any schema(http, file etc), depending of platform will be run associated application to handle this url 
	:::ruby
	System.open_url('http://www.rhomobile.com')

Use rho_open_target=_blank in html link. Note that jQuery Mobile or other JavaScript library may disable this attribute.
	:::html
	<a href="http://www.google.com/?rho_open_target=_blank">Open Google in external browser</a>

### Sample
See CustomUri of [system API sample application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/CustomUri/controller.rb) for example.

## Run rhodes application from browser

### Android
On Android it is possible to start rhodes app from browser by http link or redirect response. It is also possible to register custom URI scheme for the app.
At Android the URI must strictly follow standard URI rules. Additionally Android Chrome browser makes additional restriction: the host part of the URI must be resolvable.
By default the http://rhomobile.com/com.vendor.appname URI format is used by Rhodes. You can add additional path and query parameters to the URI and handle it by application code.
It is possible to customize the URI with build.yml settings. Default Rhodes URI contains four parts:
- scheme
- host name
- path prefix
- optional path and query
You can customize scheme and host name parts with following build.yml parameters:
    :::ruby
    android:
        URIScheme: myapp
        URIHost: www.myhost.com
In case if URIHost is specified no path prefix will be used. If no custom URIHost then default one is used (rhomobile.com) and path prefix must contain java package name of your application.
Optional path and query just passed to your application for further processing.

**NOTE: Google recommends to always use common scheme such as 'http', 'https', 'ftp', etc.**

http scheme example:
    :::html
    <a href="http://rhomobile.com/com.rhomobile.rhodessystemapisamples">Open System API Samples</a>

Custom scheme examples:
    :::ruby
    android:
        URIScheme: rho

    :::html
    <a href="rho://rhomobile.com/com.rhomobile.rhodessystemapisamples">Open System API Samples</a>


    :::ruby
    android:
        URIScheme: rho-sas
        URIHost: rhomobile.com

    :::html
    <a href="rho-sas://rhomobile.com">Open System API Samples</a>

### iPhone
On iOS devices it is possible to start rhodes app by link with special registered URI scheme from browser. You should register custom URI scheme for the app.
Custom URI scheme is set up in build.yml then this scheme is used followed by any string.

Custom scheme example:
    :::ruby
    iphone:
        BundleURLScheme: myapp

    :::html
    <a href="myapp:string_with_params">Open MyApp application</a>

In application you can get start params by 
    :::ruby
    System.get_start_params()

For previous example start params will be "string_with_params".

For execute you rhodes based application from another rhodes based application use next code:
	:::ruby
	System.open_url('myapp:string_with_params')

## MapView

The MapView class provides an embeddable map interface, similar to the one provided by the Maps application. Click the links below for detailed information about the [MapView API methods](../rhodesapi/mapview-api).

 * [create](../rhodesapi/mapview-api#create) - Create a map on your device.
 * [set_file_caching_enable](../rhodesapi/mapview-api#setfilecachingenable) - Enable file caching for map tiles. The file cache can be used for offline map browsing.
 * [preload_map_tiles](../rhodesapi/mapview-api#preloadmaptiles) - Preload a map tiles for a region defined by a zoom level range.

### MapView Settings

The supported providers are 'Google', 'ESRI', "RhoGoogle" and "OSM".<a id="mapview-settings"></a>

To use ESRI maps in your projects on iPhone:

* Install [ESRI iOS SDK](http://resources.arcgis.com/content/arcgis-iphone/api) - use default folders during installations !
* Add "esri" to your applications extensions list in build.yml file.

To use native Google map view on Android:

* Install Google Add-on API
* Get [Google Maps API key](http://code.google.com/android/maps-api-signup.html)
* Add 'mapping' and 'apikey' parameters to your build.yml
    
        android:
            mapping: yes
            apikey: <YOUR-API-KEY>

* Add 'network_state' to capabilities list in your build.yml.

        capabilities:
            - network_state

Map settings in rhoconfig.txt :

* ESRI_map_url_roadmap - URL of ESRI roadmap tile map server (example:  'http://server.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/')
* ESRI_map_url_satellite - URL of ESRI satellite tile map server (example:  'http://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/')
* OSM_map_url_roadmap - URL of OSM tile map server (example:  'http://tile.openstreetmap.org/')

### MapView Examples

The following code in your controller has the map appear on a whole page.<a id="mapview-example-create"></a>

Ruby example:

	:::ruby
	map_params = {
	     :provider => 'Google',
	     :settings => {:map_type => "hybrid",:region => [@params['latitude'], @params['longitude'], 0.2, 0.2],
	                   :zoom_enabled => true,:scroll_enabled => true,:shows_user_location => false,
	                   :api_key => 'Google Maps API Key'},
	     :annotations => [{:latitude => @params['latitude'], :longitude => @params['longitude'], :title => "Current location", :subtitle => ""},
	                      {:street_address => "Cupertino, CA 95014", :title => "Cupertino", :subtitle => "zip: 95014", 
	                       :url => "/app/GeoLocation/show?city=Cupertino"},
	                      {:street_address => "Santa Clara, CA 95051", :title => "Santa Clara", :subtitle => "zip: 95051", 
	                       :url => "/app/GeoLocation/show?city=Santa%20Clara", :pass_location => true}]
	}
	MapView.create map_params

JavaScript example:

	var map_params = {
	  provider: 'Google',
	  settings: {
	    map_type: 'hybrid',
	    region: [@params['latitude'], @params['longitude'], 0.2, 0.2],
	    zoom_enabled: true,
	    scroll_enabled: true,
	    shows_user_location: false,
	    api_key: 'Google Maps API Key'
	    }, 
	  annotations: [
	    {latitude: @params['latitude'], longitude: @params['longitude'], title: "Current location", subtitle: ""},
	    {street_address: "Cupertino, CA 95014", title: "Cupertino", subtitle: "zip: 95014", url: "/app/GeoLocation/show?city=Cupertino"},
	    {street_address: "Santa Clara, CA 95051", title: "Santa Clara", subtitle: "zip: 95051", url: "/app/GeoLocation/show?city=Santa%20Clara"}
	    ]
	  };
	Rho.MapView.create(map_params);

You can enable file caching for map tiles - file cache can use for offline map browsing.<a id="mapview-example-preload"></a>

	:::ruby
	MapView.set_file_caching_enable(1)

Preload map tiles for region (0<=zoom<=18):
	:::ruby
	  def preload_callback
	       puts '@@@@@@@@@      Preload Callback       STATUS['+@params['status']+']   PROGRESS['+@params['progress']+']'
	  end
	
	  def preload_map
	      options = { :engine => 'OSM',
	          :map_type => 'roadmap',
	          :top_latitude => 60.1,
	          :left_longitude => 30.0,
	          :bottom_latitude => 59.7,
	          :right_longitude => 30.6,
	          :min_zoom => 9,
	          :max_zoom => 11
	        }
	      total_tiles_for_preload_count = MapView.preload_map_tiles(options, url_for(:action => :preload_callback))    
	      redirect :action => :index
	  end

### Sample
See GeoLocation/controller.rb of [system API sample application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/GeoLocation/controller.rb) for some of the examples of how to use MapView class.

## File system access

You can use the RhoApplication API to access your Rhodes application. Click the links below for detailed information about the [RhoApplication API methods](../rhodesapi/rhoapplication-api).

 * [get_base_app_path](../rhodesapi/rhoapplication-api#getbaseapppath) - Returns a string that contains the absolute path to the application.
 * [get_app_path](../rhodesapi/rhoapplication-api#getapppath) - Returns a string that contains the absolute path path to the given relative path in the application.
 * [get_model_path](../rhodesapi/rhoapplication-api#getmodelpath) - Returns a string that contains the absolute path to a model folder in the application.
 * [get_blob_path](../rhodesapi/rhoapplication-api#getblobpath) - Returns the real path to a blob (such as a digital photo). You need to use this method to have the correct path to a blob attribute.
 * [get_blob_folder](../rhodesapi/rhoapplication-api#getblobfolder) - Returns the absolute path to the folder where blobs, such as digital photos, are created in this application.
 * [get_user_path](../rhodesapi/rhoapplication-api#getuserpath) - Returns the path to the user folder. iOS only.

You can use the Rhodes subset of the Ruby File API to access the Rhodes file structure. [Click here for those File API methods in both Ruby and JavaScript](../rhodesapi/file-api).

### Rhodes client file system structure
	<rhodes root>  #system-dependent path
	  apps         #Rho::RhoApplication::get_base_app_path
	    app        #Rho::RhoApplication::get_app_path('app') - contain models
	      model1   #Rho::RhoApplication::get_model_path('app','model1')
	    public     #contains files from application public folder
	    db         #contains schema and data files
	      db-files #contains files stored in database(blobs)
	               # for file paths from camera callback etc: Rho::RhoApplication::get_blob_path(relative_file_path); 
	               # to create file path for blob: Rho::RhoApplication::get_blob_folder()
	    lib        #contains rho framework library files. Blackberry does not has this folder, library files are stored in jar
	    RhoLog.txt #application log

### Read\write file example
	:::ruby	
	fileName = File.join(Rho::RhoApplication::get_base_app_path(), 'myfile.txt')
	File.open(fileName).each do |line|
	end

	fileNameW = File.join(Rho::RhoApplication::get_base_app_path(), 'tempfile.txt')
	f = File.new(fileNameW)
	f.write('test')
	f.close

	#binary file read\write
	#to read file from blob attribute use Rho::RhoApplication::get_blob_path(image.image_uri) method

	file_testname = File.join(Rho::RhoApplication::get_model_path('app','Data'), 'test.png')
	test_content = File.binread(file_testname)

	file_name = File.join(Rho::RhoApplication::get_base_app_path(), 'temp.png')
	f = File.new(file_name, "wb")
	f.write(test_content)
	f.close        

### Platform notes

#### Blackberry
Only read from files are supported.

Simulator files folder (4.6 and bigger) - `<sdk root>/components/simulator/sdcard/rho/<appname>`

Device files folder can be found using Media/Explore. 

#### iPhone
Simulator files folder - run search for RhoLog.txt from the drive root. Files are placed inside simulator folder.

Application can creates folders and files under apps and db roots.

### Rhodes client file system structure on iOS platform
	<rhodes root>  # /Library/Caches/Private Documents/
	  apps         #Rho::RhoApplication::get_base_app_path
	    app        #Rho::RhoApplication::get_app_path('app') - contain models
	      model1   #Rho::RhoApplication::get_model_path('app','model1')
	    public       #contains files from application public folder
	  lib          #contains rho framework library files. Blackberry does not has this folder, library files are stored in jar
	  db           #contains schema files
	  RhoLog.txt   #application log
	<rhodes user root>  # /Documents/
                        apps     # user path   Rho::RhoApplication::get_user_path
	  db           #contains data files
	    db-files   #contains files stored in database(blobs)
	               # for file paths from camera callback etc: Rho::RhoApplication::get_blob_path(relative_file_path); 
	               # to create file path for blob: Rho::RhoApplication::get_blob_folder()

On iOS platform only files stored in /Documents/ backup in iCloud etc.
Before Rhodes 3.3.2 all files stored in /Documents/ but Apple require do not placing files in Documents folder except user produced files. 
Now all files except databases stored in /Library/Caches/Private Documents/ - files in this folder do not bakup.
If you want make any files should be bakup - use "user folder" for it - Rho::RhoApplication::get_user_path. All you files created in old version in Rho::RhoApplication::get_base_app_path now should be open in Rho::RhoApplication::get_user_path.

Also there are few additional parameters in build.yml (use it only if you want tune iOS specific folder scheme for some reason).

 * iphone_db_in_approot - if 1 then place databases files into <rhodes root>
 * iphone_set_approot - set <rhodes root> to one of the three folders (property value - folder): "Documents" - /Documents/, "Library_Caches" - /Library/Caches/Private Documents/, "Library_Private_Documents" - /Library/Private Documents/
 * iphone_userpath_in_approot  - is 1 then <rhodes user root> will be in the same place with <rhodes root>

### change low level parameters in build.yml example
	iphone_db_in_approot: 1
	iphone_set_approot: library_Private_Documents
	iphone_userpath_in_approot: 1

### write file in user folder example
	:::ruby
	fileNameW = File.join(Rho::RhoApplication::get_user_path(), 'tempfile.txt')	
	f = File.new(fileNameW, 'w+')
	f.write('my own file !')
	f.close  

Also you can set special iOS attribute "do not bakup" to any files or folders related to database :
### setup "do not bakup" attribute for files related database Model 'Product'
	:::ruby
	require_model 'Product'
	db = Rho::RHO::get_src_db('Product')
	db.set_do_not_bakup_attribute(1)


#### Windows Mobile
Device/simulator files folder root - Program Files/&lt;app name>/rho

## Shutdown hook
Like any application written in Ruby, rhodes can register a shutdown hook. Shutdown hook is routine registered for execution when the program exits. It useful for cleanup on exit, saving program states, etc. To create you own shutdown hook you should add at_exit block to the file application.rb. 
For example:
	:::ruby
	at_exit do
	  #delete all temporary files
	  ...
	  ...
	end

## Media Support
Rhodes can play video/audio files in native Internet Browser. So application developer can just add link to online or local audio/video file:
	:::html
	<a href="http://videos3.netprofesseur.com/1/videos/130/BRICOLAGE_Changer_un_joints.mp4">Play mp4 online video</a>

Application can download file to file system using [AsyncHttp.download_file](call-web-services) and than put link [to this file](#file-system-access) to view.

### Sample
See app\Media of [System API Sample application](http://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/Media/controller.rb) as an example.

## Using Hyperlinks for Email, Phone Dialing, SMS and others

You can allow your users to send email messages, call phone numbers and send SMS messages using the hyperlink (`<a href="...">`) syntax. Please note not all of these examples could work on simulators! Use real devices for test. Examples are shown below. 

To make phone calls enable the phone capability. This is done by adding the following lines to build.yml:

	:::yaml
	capabilities:
	  - phone

**mailto**
	:::html
	<a href="mailto:test@host.com?subject=testing123">Mailto</a>
Note, even for an empty address, you must add the @ symbol: <a href="mailto:@?subject=testing123">Mailto</a>

Blackberry: if you need cc, bcc fields, use rhomailto scheme:
	:::html
    <a href="rhomailto:test@host.com?cc=geny@mail.ru&bcc=vasy@gmail.com&body=testMessage&subject=sub1">Send e-mail to test@host.com</a>
    
**tel**
	:::html
	<a href="tel:1-555-531-3255!8335033#!#!9582#">Tel</a>
	<a href="wtai://wp/mc;5195551212" title="Call">Work Tel</a>
	<a href="wtai://wp/mc;5195551213" title="Call">Home Tel</a>
Note, the WML tel description can be found [ here](http://na.blackberry.com/eng/devjournals/resources/journals/oct_2004/wml_101.jsp).

**sms:**
	:::html
	<a href="sms:+3581234567">Send SMS to us </a>

Open link in external application (browser for http:// links):
	:::html
	<a href="http://www.google.com/?rho_open_target=_blank">Open Google in external browser</a>

Open appstore on iphone: [http://wiki.akosma.com/IPhone_URL_Schemes#App_Store](http://wiki.akosma.com/IPhone_URL_Schemes#App_Store)

### jQuery/jQuery Mobile
When using jQuery and/or jQuery Mobile in application code, you cannot use usual html links for hyperlinks. You need to call controller action and call WebView.navigate from there:

    #Ajax call of controller method:
    $.get("/app/TestController/send_mail",function(data) {});
    
    #TestController method:
    def send_mail
        WebView.navigate( 'mailto:test@host.com' )        
        #to open url in external application you can use System.open_url
    end

### Blackberry
On Blackberry 5.0 and later you can use JavaScript [blackberry.launch object](http://docs.blackberry.com/en/developers/deliverables/18446/blackberry_launch_971534_11.jsp#blackberry_launch_newMap_971532_11)
to create SMS, make Phone call etc.

## BlackBerry network connection
Rhodes may use any Blackberry network connection available on the device. What particular network connection will be selected depends on the url suffix used to connect. Here is the algorithm:

1. Rhodes enumerate device Service Books at application start to identify Wifi, BES (has priority over BIS-B) and BIS-B transport:

	* if WIFI exist we set wifi_postfix = ";interface=wifi"
	* if BES exist we set url_postfix = ""
	* If BIS-B exist and NO BES: url_postfix = ";deviceside=false;ConnectionType=mds-public"
	* If no BES or BES exist or in simulator mode : url_postfix = ";deviceside=true"

2. When application make network call, Rhodes create network connection:

	* if wifi_postfix is not empty and WIFI network available: add wifi_postfix to url
	* add url_postfix
	* make network connection

3. If connection creation failed, Rhodes try to connect without wifi_postfix(if exists) and then without url_postfix (if exists)

4. There are several [rhoconfig.txt](configuration#run-time-configuration) parameters which can modify this process (mostly for the testing purposes):

Do not use `;deviceside=true` suffix:

	no_deviceside_postfix = 0 

Set `url_postfix` to specific value, without enumerating Service Books records

	bb_connection_postfix = ''

## BlackBerry Browser Support

Capabilities of BlackBerry WebView control differ quite significantly form other OS-es as well as from one version of BB OS to another. And even with the single BB OS you may have different capabilities depending on what WebView do you use (see full browser capability described below).

Check out the [BlackBerry Browser Version 4.2 Content Developer Guide](http://docs.blackberry.com/eng/deliverables//1143/browser_devguide.pdf) to see what HTML, CSS and JavaScript supported on BlackBerry.

One of the limitation is that simple submit element in the form does not work (this issue was fixed in Rhodes > 2.2.4):

	:::html
	<form id="user_edit_form" 
	   method="POST" 
	   action="<%=url_for(:action => 'do_login')%>" selected="true">  
	<input type="submit" value="Login"/>
	</form>

Solution:

	:::html
	<form id="user_edit_form" 
	   method="POST" 
	   action="<%=url_for(:action => 'do_login')%>" selected="true">  
	</form>
	<a href="#" onclick="document.forms[0].submit(); return false;">
		<img src="/public/images/button_next.png" />
	</a>

### Blackberry Touch screen (4.7, 5.x )

There are some issues Rhodes developers encountered developing for Blackberry Touch screen 4.7 and 5.x.
 
Links with aligned images are not clickable:
	:::html
	<a href="/app/WelcomeScreen/do_info">
		<img src="/public/images/bb_info_btn.png" align="left" />
	</a>
Solution: remove alignment or add text to link

Links with div inside issue:
	:::html
	<a href="/app/Login"><div style="height:10px"></div>Login</a>
Solution: move dive out of `<a>`:
	:::html
	<div style="height:10px"></div><a href="/app/Login">Login</a>

Links with style display:block:
	:::html
	<a href="/app/Login" 
		style="display:block;background: url('test.png') no-repeat 97% 50%;">
		Login
	</a>
	<a href="/app/Login" 
		style="display:block;border-Top: 1px solid #bbb;">
		Login
	</a>
Solution: remove display:block from a element

### Blackberry 5.0 and above full browser

Blackberry 5.0 and above has new BrowserField class, which support JavaScript, ajax and extended css. To use it set in [rhoconfig.txt](configuration#run-time-configuration):

	# use full browser only on BB 5.0 and above
	use_bb_full_browser=5 

	# use full browser only on touch devices including 5.0
	use_bb_full_browser=touch 

WebView.execute_js is also supported in this mode.

NOTE: on Blackberry 6.0 and above it is recommended to use full browser mode, because otherwise some UI elements like combobox are not selectable by trackball:

	# use full browser only on BB 6.0 and above
	use_bb_full_browser=6


### Blackberry full browser

Available for Blackberry 4.6 and above

Support AJAX and better support of CSS

On non-touch screen looks like usual browser app, so not very useful because it uses pointer cursor. On Touch screen devices no visual difference between full browser and browser field (default mode). 

To enable on all devices - add to [rhoconfig.txt](configuration#run-time-configuration):

	use_bb_full_browser=1

To enable on Touch screen devices - add to [rhoconfig.txt](configuration#run-time-configuration):

	use_bb_full_browser='touch'

Submit form issue:
	:::html
	<head>
	<script type="text/javascript">
	function submitform()
	{
	    document.forms["login"].submit();
	}
	</script>
	</head>
	<form id="user_edit_form" 
	   method="POST" 
	   action="<%=url_for(:action => 'do_login')%>" selected="true">  
	<a href="javascript: submitform()">Login</a>
	</form>

Solution:
	:::html
	<form id="user_edit_form" 
	   method="POST" 
	   action="<%=url_for(:action => 'do_login')%>" selected="true">  
		<a href="#" onclick="document.forms[0].submit(); return false;">
			<img src="/public/images/bb_logon_btn1.png" />
		</a>
	</form>

## Android Hardware Accelerated Activity

Support android:hardwareAccelerated attribute at AndroidManifest.xml for main Rhodes activity.

To set android:hardwareAccelerated='true' at Androidmanifest.xml for RhodesActivity enable the hardware_acceleration capability. This is done by adding the following lines to build.yml:

	:::yaml
	android:
	  capabilities:
	    - hardware_acceleration
