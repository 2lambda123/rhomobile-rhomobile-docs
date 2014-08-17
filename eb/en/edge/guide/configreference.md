# Config.XML Reference
Runtime configuration of the Motorola Enterprise Browser is managed through an XML file called Config.xml. This file is *mandatory* for proper MEB execution: not every setting has a default and if the configuration file cannot be found, the MEB will *not* start. An example configuration file is provided as part of the installation and contains sensible defaults, this page explains the meanings of each of the settings and their possible values. The example `Config.xml` file is bundled your installation or the MEB on your device.

## Configuration File Location
The location of the configuration file loaded by the MEB is dependent on a number of factors:

* When running on the Enterprise Tablet the configuration file is read from `/Android/data/com.motorolasolutions.enterprisebrowser/Config.xml`.
* When running on all other devices the MEB will attempt to launch the configuration file `Config.xml` located in the folder `Config` off the installation root.
* You can change which configuration file is loaded using the /C: configuration option

For persistent installations, on cold boot the `Config.xml` file is copied from `\Application\Enterprise Browser\Config\Config.xml` to `\Program Files\Enterprise Browser\Config\Config.xml`; bear this in mind if you want your configuration to persist across cold boot. <!-- This behavior may be modified by changing `\Application\RhoElements.cpy`. --> <!-- Need to verify this -->

## Substitution Variables
The following substitution variables are available in the configuration file
<table class="re-table">
<tr>
<th>Substitution Variable</th>
<th>Expanded Value</th>
</tr>
<tr>
<td>%INSTALLDIR%</td>
<td>The directory into which the Enterprise Browser has been installed.</td>
</tr>
</table>

## Config.xml File Format
The following is an example of a typical configuration file

	:::xml
	<?xml version="1.0"?>
	<!-- Motorola Enterprise Browser Configuration file -->
	<Configuration>
		<DebugButtons>
			<DebugButtonsEnabled value="0"/>
		</DebugButtons>

		<Logger>
			<LogProtocol value="FILE"/>
			<LogPort value="80"/>
			<LogURI value="file://%INSTALLDIR%/log.txt"/>
			<LogError value="1"/>
			<LogWarning value="0"/>
			<LogInfo value="0"/>
			<LogUser value="1"/>
			<LogMemory value="0"/>
			<LogMemPeriod value="5000"/>
			<LogMaxSize value="10"/>
		</Logger>

		<FileLocations>
			<RegEXFile value="file://%INSTALLDIR%/RegEx.xml"/>
		</FileLocations>

		<Screen>
			<FullScreen value="1"/>
		</Screen>

		<WebServer>
			<Enabled VALUE="0"/>
			<Port VALUE="8080"/>
			<WebFolder VALUE="\www"/>
			<Public VALUE="0"/>
		</WebServer>

		<DeviceKeys>
			<EnableFunctionKey_F1 value="0"/>
			<EnableFunctionKey_F2 value="0"/>
			<EnableFunctionKey_F3 value="0"/>
		</DeviceKeys>

		<Navigation>
			<NavTimeout value="45000"/>
		</Navigation>

		<Geolocation>
			<GeolocationEnabled value="1"/>
		</Geolocation>

		<Applications>
			<Application>
				<General>
					<Name value="Menu"/>
					<StartPage value="file://%INSTALLDIR%/menu.html" name="Menu"/>
				</General>

				<HTTP_Proxy value=""/>
				<HTTPS_Proxy value=""/>

				<WebDB>
					<WebStorageDBPath value="file://%INSTALLDIR%"/>
					<WebSQLDBQuota value="5000000"/>
					<WebSQLDBPath value="file://%INSTALLDIR%"/>
				</WebDB>

				<ApplicationCache>
					<ApplicationCachePath value="file://%INSTALLDIR%"/>
					<ApplicationCacheQuota value="5000000"/>
				</ApplicationCache>

				<NPAPI>
					<Preloads>
						<PreloadLegacyGeneric value="1"/>
						<PreloadLegacyODAX value="1"/>
						<PreloadLegacyNoSIP value="1"/>
						<PreloadLegacyAirBeam value="1"/>
						<PreloadLegacyAPD value="1"/>
						<PreloadJSObjects value="1"/>
					</Preloads>
				</NPAPI>

				<HTMLStyles>
					<TextSelectionEnabled value="0"/>
					<FontFamily value="Droid Sans Fallback"/>
				</HTMLStyles>

				<GUI>
					<SignalRefresh value="5000"/>
					<HourglassEnabled value="1"/>
					<HourglassLeft value=""/>
					<HourglassTop value=""/>
				</GUI>

				<Navigation>
					<BadLinkURI value="file://%INSTALLDIR%/badlink.html"/>
					<UserAgent value="Mozilla/5.0 (%p) AppleWebKit/%w (KHTML, like Gecko) MotorolaWebKit/%e Safari/%w"/>
					<NetworkCookieDatabase value="file://%INSTALLDIR%/cookies.db"/>
					<ViewportEnabled value="1"/>
					<Cache value="5MB"/>
				</Navigation>
			</Application>
		</Applications>
	</Configuration>

## General
### StartPage
Defines the start page of the Enterprise Browser application, the first page to be displayed when Enterprise Browser is launched.  This should be a local file to avoid connectivity issues on start up.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

**Possible Values**

* Fully qualified path to start page.

### Name
The name of the application

**Possible Values**

* ASCII text

### UseRegularExpressions
In order to be backwardly compatible with PocketBrowser syntax for controlling device capabilities Enterprise Browser uses a Regular Expression engine to apply a series of transformations to each meta tag or JavaScript call being processed, as defined in RegEx.xml. If you are developing applications without the need to be backwardly compatible with PocketBrowser syntax you can disable regular expressions, this can result in an improvement in application performance, depending on how the application is structured. This setting is only applicable to RhoMobile Suite version 2.2 and above on Windows devices.

**Possible Values**

* 0 - Do Not Use Regular Expressions
* 1 - Use Regular Expressions

## HTTP_Proxy
Specifies the HTTP Proxy settings to use in the format URL:port.  Note that this setting only applies to the Motorola WebKit engine, proxy settings for the Internet Explorer engine are picked up from the Windows connection manager.  Leave this field blank to not use a proxy.

**Possible Values**

* URL:PortNo

## HTTPS_Proxy
Specifies the HTTPS Proxy settings to use in the format URL:port.  Note that this setting only applies to the Motorola WebKit engine, proxy settings for the Internet Explorer engine are picked up from the Windows connection manager.  Leave this field blank to not use a proxy. Not supported on Windows Mobile/Windows CE, use HTTP_Proxy instead.

**Possible Values**

* URL:PortNo

## No_Proxy
Sets the sites that should be accessed directly. This should be a comma-separated list of host names, domain names (starting with a dot), IP addresses, or CIDR format IP network addresses eg. myhost, .mydomain.com, 192.168.1.1,192.168.0.0/24. Note this configuration setting is usable with the Motorola Webkit browser only.

**Possible Values**

* Comma separated list of direct access addresses.

## DebugButtons

### DebugButtonsEnabled
When enabled, a set of controls useful for development and debugging purposes will be present in the interface.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

## Logger

### LogProtocol
Sets the protocol over which the logging data will be sent

**Possible Values**

* File or 
* HTTP

### LogPort
The port over which the logging data will be sent (ignored for File protocol)

**Possible Values**

* Any valid HTTP port

### LogURI
The URL or File name & path to which logged data should be sent

**Possible Values**

* Any valid URL or fully qualified file name

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

### LogError
Enables or Disables the logging of ERROR messages generated by Enterprise Browser. If we set this to 1, it enables the Error level only.

**Possible Values**

0 - Disabled
1 - Enabled

### LogWarning
Enables or Disables the logging of WARNING messages generated by Enterprise Browser. If we set this to 1, it enables the following levels i.e. Warning & Error, even if Error level is not set to 1.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### LogInfo
Enables or Disables the logging of INFORMATION messages generated by Enterprise Browser. If we set this to 1, it enables the following levels i.e. Info, Warning & Error, even if Warning or Error levels is not set to 1.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### LogUser
Enables or Disables the logging of messages from the user application. If we set this to 1, it enables the following levels i.e. User, Info, Warning & Error, even if Info or Warning or Error levels is not set to 1. Data can be logged using the Log API

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### LogMemory
Enables or Disables the logging of memory usage in the system. Not applicable to the Enterprise Tablet.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### LogMemPeriod
Specifies the time interval at which memory logs will be generated periodically. Not applicable to the Enterprise Tablet.

**Possible Values**

* Time in milliseconds

### LogMaxSize
The maximum size the log file should be allowed to reach, once the maximum size is reached no more logs will be saved.

**Possible Values**

* File size in kilobytes

## FileLocations

### RegExFile
In order to enable backward compatibility with pages written in EMML 1.0 regular expressions are used to convert to EMML1.1 meta tags. This setting defines the location of the XML file which contains the conversions to be used. This setting is only applicable to Windows

**Possible Values**

* Fully qualified path to file defining the regular expressions.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

### PluginFile
Not applicable to the Enterprise Tablet:
Enterprise Browser has a plugin based architecture so functionality can be tailored to the individual application, lessening the memory footprint on the device. It is necessary for Enterprise Browser to have a mapping between modules, plugins and the physical location of the Plugin DLL on the device; this mapping is stored in the Plug-in file and the location of that file is defined by this setting.

**Possible Values**

* Fully qualified path to file defining the regular expressions.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

## Screen

### FullScreen
Sets Enterprise Browser to fullscreen mode, locking out the OS to the user unless specifically minimized using the Application API. Some Windows Mobile devices feature a customized Motorola user interface; in this case access is provided to the status bar at the top of the screen.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### PageZoom
Sets the zoom factor of the page. Default zoom is 1.0. In Android, negative values and 0.0 is not supported. In Windows, zoom value less than 1.0 is defaulted to 1.0 because below 1.0 zoom value, the page doesn't look in readable format.* (see remark)

>Note: Sometimes, while navigating from any page to any other page, the actual page zoom setting reflects after few milli seconds delay. This doesn't happens everytime.

Setting page zoom property on page load event doesnot reflect the set value for the Application start page for the first time. Users are advised to set the page zoom property with a minimum of 1 second delay on page load.

Setting page zoom property on page load will reflect only for that page.

**Possible Values**

* Zoom factor of the page.

## VoidConnection

### TrackConnection
This value should be 0 or 1. By default it's value is 0. It implies whether the application is going to use this feature or not. When its value is 0 it is NOT going to use the feature else otherwise. The feature is to try to connect to a particular URL mentioned in the "HostURL" element. Whenever connectivity is lost, it will display a pop up message. Whenever Connectivity is established the pop up meaage will be disappered. If connection is not established during timeout value, it will navigate to badlink page. On windows, if this feature is enabled, it will display a non modal dialog whenever connectivity goes, whereas in case of Android it will display a modal dialog and user will be blocked from performing any UI actions. On windows as it is a non modal dialog, user still can continue work on the parent screen until the timeout occurs. However it is not recommended to access the back ground application when the  connection checking window is being shown.

**Possible Values**

* Connection Tracking

### HostURL
This is the URL to which the application will try to connect to. The default port is 80. It can take both dotted ip and host name. Mentioning of port no is also optional. The port no should be appeneded to i after appending  colon to the ip.

**Possible Values**

* Connection Tracking

### Message
Message is the customized Message to be shown in the pop up window.

**Possible Values**

* Customized Message

### Timeout
This value indicates for how many milliseconds the application should try to connect to the URL before navigating to badlink page. The minimum value is 30000. If specified less than 30000, it will take 30000. The value of this parameter should be at least 3 times bigger than PollInterval,else both will take default  values. 

**Possible Values**

* Timeout

### PollInterval
This value indicates for how many miliseconds the application should pause from trying to connect to the URL between consecutive checking. This value should be small enough and  Timeout value should be some multiple of this value. The minimum value is 5000. If specified less than 5000, it will take 5000. It is a non-testable parameter.

**Possible Values**

* PollInterval

## WebServer
### Enabled
Enables or Disables an internal web server to run locally on the device.  If running multiple applications with internal web servers consideration should be made over whether a single server should be used or multiple servers running on different ports.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### Port
By default should be left at 8080, This specifies the IP port the Web Server is running on.
**Possible Values**

* 8080

### WebFolder
Specifies a folder on the device where the web application is stored, Index.html is the default page if no other page is requested.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

**Possible Values**

* Fully qualified path to folder containing web application.

### Public
Enables or Disables access to the local WebServer from an external device, it is recommended that the setting is only used for debugging purposes. ***Enabling this feature in a production deployment is a potential security risk. Make sure to check this value before deployment.***

**Possible Values**

* 0 - Disabled
* 1 - Enabled

## DeviceKeys
>Note: On Windows Mobile and Windows CE devices full control is given to the developer over how their application handles function keys.  Because of the limitations of the operating system <b>any settings applied will persist until the device is next warm booted</b>.  Which function keys have default operating system behavior will vary from device to device, e.g. on the MC75a F3 and F4 represent the red and green phone keys and on many devices the volume keys are also mapped as Function keys.  Not all function keys will have default operating system behavior.

Unblocking function keys may expose the underlying operating system, particularly the red and green phone keys will give access to the start menu and programs.

The list below shows the behavior of Enterprise Browser when Function Keys are pressed given the possible configuration settings:

* **ENABLE FUNCTION KEY = TRUE & FUNCTION KEYS CAPTURABLE = TRUE**
	* All Function Keys can be captured by the Key Capture Module
	* Function Key will not have its default Operating system behavior
* **ENABLE FUNCTION KEY = TRUE & FUNCTION KEYS CAPTURABLE = FALSE**
	* Function Keys with default OS behavior can not be captured by the Key Capture Module
	* Function Keys without default OS behavior can be captured by the Key Capture Module
	* Function Key will have its default Operating system behavior (if any)
* **ENABLE FUNCTION KEY = FALSE & FUNCTION KEYS CAPTURABLE = TRUE**
	* All Function Keys can be captured by the Key Capture Module
	* Function Key will not have its default Operating system behavior
* **ENABLE FUNCTION KEY = FALSE & FUNCTION KEYS CAPTURABLE = FALSE**
	* All Function Keys can not be captured by the Key Capture Module
	* Function Key will not have its default Operating system behavior (if any)

### FunctionKeysCapturable
This parameter is specific to Windows Mobile and Windows CE:<P>When disabled (default) this parameter will allow enabled Function keys to have their default Windows system behavior (e.g. F6/F7 controls the volume on some devices whilst F3/F4 represent the Red / Green phone keys).  When enabled, function keys will be capturable by the Key Capture module.

The interaction between FunctionKeysCapturable and EnableFunctionKey_X is shown below.  This setting is not specific to the current application and will be applied globally on the device.

**Possible Values**

* 0 - F keys not capturable
* 1 - F keys capturable

### EnableFunctionKey_X
By default all function keys are disabled (e.g. F1, F2) but this setting is used to specify which function keys should be enabled.  For each key you wish to enable define a EnableFunctionKey_X tag but replace 'X' with the key being enabled, so for example to enable F1 specify EnableFunctionKey_F1.  The maximum function key you can enable is F24.  In order to use this configuration setting you must preload the KeyCapture module

On the Enterprise tablet, this tag can be used to enable the 'P' keys. For compatibility with other devices the 'P' keys are referred to as 'F' keys in the config file. Therefore in order to enable P2 key on the enterprise tablet, the tag EnableFunctionKey_F2 should be set to 1.  For Windows Mobile / CE this setting is not specific to the current application and will be applied globally on the device, ***only being unset when a device warm boot is performed.**

>Note: MC40, F1 is mapped to the Volume Down button, F2 to the Volume UP button and F3 to the Search button.

The interaction between FunctionKeysCapturable and EnableFunctionKey_X is shown at below.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### EnableApplicationKey_X
This parameter is specific to Windows Mobile and Windows CE:

Some devices have keys to access specific applications on the device, e.g. Calendar, Outlook etc, all of which are disabled by default.  This setting is used to specify which application keys should be enabled, numbered A1 to A16.  For each key you wish to enable define a EnableApplicationKey_X tag but replace 'X' with the key being enabled, e.g. EnableApplicationKey_A1.  Note that the mapping of keys to applications is device specific so A1 may have two functions on two different devices.  In order to use this configuration setting you must preload the KeyCapture module<P>This setting is not specific to the current application and will be applied globally on the device. **Once set, this will persist across multiple Enterprise Browser executions and can only be unset by performing a device warm boot.**

**Possible Values**

* 0 - Disabled
* 1 - Enabled

## Navigation
### NavTimeout
Number of milliseconds before the browser times out and navigates to the page specified in the badlink setting.  If it is determined that the destination is unreachable regardless of wait time, the 'badlink' page may be loaded before NAVTIMEOUT.  This is the time taken to establish communication with the server, not the time taken to fully load the page.

>Note: The navigation timeout will not be invoked when navigating to the start page, best practice is to store your first page locally to avoid connectivity issues at start up, you can then redirect to an on-line page if desired.

**Possible Values**

* Timeout in Milliseconds, maximum value is 45000

## ScreenOrientation
### AutoRotate
When disabled the orientation of the screen will not change as the device is rotated and vice versa.  This is a screen rotation lock.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

## UserData
Used to persist data when using Read/WriteUserSetting.

**Possible Values**

* Any valid user setting.

## WebDB
### WebStorageDBPath
Path to an existing directory to store Web Storage databases.

**Possible Values**

* Fully qualified local path.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

### WebSQLDBQuota
Web SQL database maximum quota per database.

**Possible Values**

* Size in bytes

### WebSQLDBPath
Path to an existing directory to store Web SQL databases.

**Possible Values**

* Fully qualified local path.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

## ApplicationCache
### ApplicationCacheQuota
Application Cache data maximum quota per application.

**Possible Values**

* Size in bytes
### ApplicationCachePath
Path to an existing directory to store Application Cache data.

**Possible Values**

* Fully qualified local path.

## NPAPI
### NPAPIDirectory
Not applicable to the Enterprise Tablet:<br>

Path to an existing directory where the NPAPI Plugins are stored.

**Possible Values**

* Fully qualified local path.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

### Preloads \\ PreloadLegacyActiveX
Whether or not to preload the ActiveX object in WebKit. You'll need to use this if you want backwards compatibility with code written in PocketBrowser that used the ActiveXObject. This setting is supported on Windows Mobile / CE with the Motorola Webkit only.

**Possible Values**

* 0 - Do Not Preload
* 1 - Preload

### Preloads \\ PreloadLegacyGeneric
Whether or not to preload the NPAPI plugin to mimic the Generic ActiveX object in WebKit. On the Enterprise Tablet this plugin is automatically loaded when the JSObjects plugin is preloaded.

**Possible Values**

* 0 - Do Not Preload
* 1 - Preload

### Preloads \\ PreloadLegacyODAX
Not applicable to the Enterprise Tablet:

Whether or not to preload the NPAPI plugin to mimic the ODAX ActiveX object in WebKit.

**Possible Values**

* 0 - Do Not Preload
* 1 - Preload

### Preloads \\ PreloadLegacyNoSIP
Whether or not to preload the NPAPI plugin to mimic the NoSIP ActiveX object in WebKit.

**Possible Values**

* 0 - Do Not Preload
* 1 - Preload

### Preloads \\ PreloadLegacyAirBeam
Not applicable to the Enterprise Tablet:

Whether or not to preload the NPAPI plugin to mimic the AirBeam ActiveX object in WebKit

**Possible Values**

* 0 - Do Not Preload
* 1 - Preload

### Preloads \\ PreloadLegacyAPD
Whether or not to preload the NPAPI plugin to mimic the APD ActiveX object in WebKit.

**Possible Values**

* 0 - Do Not Preload
* 1 - Preload

### Preloads \\ 2PreloadJSObjects
Whether or not to preload the NPAPI plugin to provide native JavaScript objects for each of the modules.

**Possible Values**

* 0 - Do Not Preload
* 1 - Preload

## Preloads
### Preload
By default plug-ins will be loaded into memory when needed, e.g. when `Barcode.enable` is called, the `Barcode` plugin DLL will be loaded into memory. This loading operation takes takes a certain amount of time when it is performed for the first time; to prevent the user from noticing any lag when using their application, modules can be loaded in the background when Enterprise Browser starts.  Specify a Preload tag for each module you wish to load at Enterprise Browser startup; note that multiple modules may be defined in the same DLL but you still need to list all modules to preload here to see maximum benefit.

>Note: On low memory devices, it is recommended to preload all your required modules to avoid your program running out of memory during execution.

Preloads are not applicable to the enterprise tablet, as plugins are integral to Enterprise Browser on this platform.

**Possible Values**

* Module name

## Scrolling
### ScrollTechnique
Specifies the technique used to scroll the viewport:

**Possible Values**

* FingerScroll : You can scroll around the page using finger swiping.
* Scrollbars : When the size of the page is too large to fit into the viewport, scrollbars will be presented which can be used to scroll the page (Not available on Android)
* None : No scrollbars will be displayed and the page will not respond to finger swipes.

## Authentication
### Username
Specifies the username to be provided automatically when Enterprise Browser is instructed to navigate to any page which requires basic or digest HTTP authentication.<P/>If this setting is absent from the configuration file a popup dialog will be displayed prompting the user to enter their own credentials.  Leaving the value blank will provide a username of "".  Enterprise Browser will only permit the user to enter incorrect credentials twice before presenting the HTTP 401 Unauthorized page, the application should be designed to handle this scenario.

**Possible Values**

* ASCII text

### Password
Specifies the password to be provided automatically when Enterprise Browser is instructed to navigate to any page which requires basic or digest HTTP authentication.<P/>If this setting is absent from the configuration file a popup dialog will be displayed prompting the user to enter their own credentials.  Leaving the value blank will provide a password of "".  Enterprise Browser will only permit the user to enter incorrect credentials twice before presenting the HTTP 401 Unauthorized page, the application should be designed to handle this scenario.

**Possible Values**

* ASCII text

## HTMLStyles
### CaretWidth
This setting is a number which specifies the width of the textbox / text area caret, in pixels. The default value if you don't specify anything is '1'.  Prior to this release the width was fixed at '1' and you could not change it. This setting only applies to the Webkit on Windows Mobile or Windows CE.

**Possible Values**

* Integer values for caret width in pixels

### FontFamily
Specifies the default font to use when rendering text in web pages.  The specified font should be a TrueType font present on the device. On Windows, the default font has been set to 'Tahoma' as this is present on all Motorola WM / CE devices. Note that Tahoma has no italic or oblique variants. On the Enterprise Tablet the default is Droid Sans Fallback. The specified font must be stored in `\Windows` for Windows WM / CE devices, or `/system/fonts for Enterprise Tablet`.

**Possible Values**

* Font name

### FontDirectory
Specifies the font directory where true type fonts can be found.  On Windows the default font directory is `\Windows` on all Motorola WM / CE devices.  Not applicable to the Enterprise Tablet.

**Possible Values**

* `\Windows`

### UseNativeFonts
When set to 0 (default) the FreeType library is used, this is the same as behavior on RMS 2.x. When set to 1 the native font engine on the device is used to render fonts and the 'FontFamily' setting will have no effect. By default, on localized devices from 4.1 onwards the native font engine will be used as the FreeType library can not render localized characters (e.g. Italian accented characters, Korean characters, Chinese characters etc). Some early BSPs of CE7 do not support the native font render unfortunately. The log file will show the font engine in use on launch if there is doubt. This setting is specific to Windows Mobile / Windows CE. NOTE: This config item is not currently available on the latest BSPs for MC92, VC70 or WT41N0.

**Possible Values**

* 0 - Use FontFamily Setting
* 1 - Use FreeType font library

## SIP
### ResizeOnSIP
When enabled the browser window will resize to accommodate the SIP (Soft Input Panel, the on-screen virtual keyboard) when displayed.  If the SIP has been moved to the top half of the screen the browser window will reduce in size from the top.  In order to use this configuration setting you must preload the SIP module.  (Windows Mobile Only.  This option is not compatible with CE or Finger Scrolling, the SIP will always appear at the bottom of the screen)

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### EnableSIP
Disables or Enables the SIP (Soft Input Panel, the on-screen virtual keyboard).  (Android Only, on Windows the Left & Top parameters of the SIP module can be used to position the SIP off the screen.)

**Possible Values**

* 0 - Disabled
* 1 - Enabled

## System
### LowBatteryScan
Windows Mobile and CE only.  Set to 0 to disable scanning when the battery is low or set to 1 to enable it.  Once disabled the scanner can be enabled again by calling `Barcode.enable`.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

## Scanner
### DisableScannerDuringNavigation
By default if you have enabled the Scanner on a page, through either meta tags, JavaScript or Ruby and navigate to a new page the Scanner will automatically disable.  To override this behavior you can set this option to '0' and once enabled the Scanner will remain so in the foreground application until you disable it.  This setting is only applicable to RhoMobile Suite version 2.2 and above.

**Possible Values**

* 0 - The Scanner will remain enabled during page navigation
* 1 - The Scanner will disable during a page navigation

## Sound
### DecodeVolume
The volume of the device beeper when a barcode is scanned.

**Possible Values**

* 0 to 5 with 5 being the loudest

### DecodeFrequency
The frequency of the device beeper when a barcode is successfully decoded.  This should be within the range of the beeper.

**Possible Values**

* 0 to 0xFFFF

### InvalidDecodeFrequency<
The frequency of the device beeper when a barcode is scanned but not successfully decoded.  This should be within the range of the beeper. Not applicable to the Enterprise Tablet.

**Possible Values**

* 0 to 0xFFFF

### DecodeDuration
The duration of the device beeper when a barcode is scanned.

**Possible Values**

* Milliseconds

### ScanDecodeWav
Wave file to be played when the scanner successfully decodes a barcode.  This setting overrides the scanner beeper.

**Possible Values**

* File name and path stored locally on the device.

### ScanInvalidWav
.Wav file to be played when a barcode is scanned but not successfully decoded.  This setting overrides the scanner beeper. Not applicable to the Enterprise Tablet.

**Possible Values**

* File name and path stored locally on the device.

### ImagerCaptureWav
.Wav file to be played when the Imager captures an image

**Possible Values**

* File name and path stored locally on the device.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

## GUI
### SignalRefresh
Specifies the refresh rate of the signal display, see the Signal API for more information.

**Possible Values**

* Refresh rate in milliseconds

### BatteryRefresh
Specifies the refresh rate of the battery display, see the Battery API for more information. Not applicable to the Enterprise Tablet

>Note: On the Enterprise Tablet the battery notification is asynchronous. For this reason, BatteryRefresh is not supported on the Enterprise Tablet. The effect of this is that a batteryEvent is fired only when the battery level changes. This has been done to save battery power compared to polling.

**Possible Values**

* Refresh rate in milliseconds

### HourglassEnabled
By default an Hourglass will be displayed whilst navigating between pages, this setting can be used to disable that behavior.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### HourglassLeft
By default an Hourglass will be displayed whilst navigating between pages, this setting can be used to adjust its horizontal position.  If not specified the hourglass will appear at the center of the screen.

**Possible Values**

* Pixels

### HourglassTop
By default an Hourglass will be displayed whilst navigating between pages, this setting can be used to adjust its vertical position.  If not specified the hourglass will appear in the center of the screen.

**Possible Values**

* Pixels

## Navigation

### BadLinkURI
Navigates to the specified badlink uri when one of the following occurs:

* There is an error attempting to navigate to the page, e.g. the device has no network connection.
* The timeout occurs when navigating to the page.  You can adjust the value of the timeout using the NavTimeout setting.
* The user presses the stop button.

The browser will automatically append the querystring value "badlink" containing the url of the page which could not be reached and "stop=true" if the page was loaded because the user pressed the stop button.  The page specified in the badlink setting should be an offline file using the `file://` protocol, this way the browser can always access the file.

**Possible Values**

* File name and path stored locally on the device.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

### UserAgent
When visiting a web server the WebKit browser will report its User-Agent header as the specified value.  Use the following substitution variables:

* %p - platform name ("Windows CE " + version number)
* %w - WebKit version number
* %e - MotorolaWebKit version number.

Use the UserAgent setting to spoof your device to the server, e.g. to view content designed for the desktop on your mobile screen.

From Enterprise Browser 2.1 onwards the default value was changed to work out of the box with a greater number of server configurations, prior to Enterprise Browser 2.1 the default user agent was: "Mozilla/5.0 (%p) AppleWebKit/%w (KHTML, like Gecko) MotorolaWebKit/%e Safari/%w"

**Possible Values**

* String

### ViewportEnabled
Whether to enable or disable viewport meta tag processing (default is enabled)

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### ViewportWidth
Default viewport width to use for pages that do not have a viewport meta tag (uses 1:1 scaling if not specified)

**Possible Values**

* Number

### CaFile
A file of CA certificates in PEM format.  See <a href="http://www.openssl.org/docs/ssl/SSL_CTX_load_verify_locations.html" target="_blank">openssl</a>.  This setting is supported on Windows Mobile / CE and Android.

**Possible Values**

* Local File name on the device.

### CaPath
A directory containing CA certificates in PEM format (one certificate per file).  The OpenSSL `c_rehash` utility must be used to generate appropriately named links to the certificate files. See <a href="http://www.openssl.org/docs/ssl/SSL_CTX_load_verify_locations.html" target="_blank">openssl</a> for more information. This setting is supported on Windows Mobile / CE and Android.

**Possible Values**

* Local File path on the device.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

### VerifyPeerCertificate
Verify the server certificate against the internal certificates.  It is strongly recommended not to set this to 0 in deployment situations, but it can be useful during development.  A value of 0 is equivalent to automatically clicking 'OK' on a web browser's dialog querying an untrusted certificate.

**Possible Values**

* Boolean

### NetworkCookieDatabase
If you want your cookies to persist across device boots then specify a file name here for the database used to hold the cookies.  If the specified file does not already exist then one will be created.  The cookies will be loaded in from this file and saved back to it when Enterprise Browser exits, unless the file is read only in which case it will not be overwritten.  If not specified cookies will not persist.

**Possible Values**

* Fully qualified local path.

>Note: The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

### Cache
The browser cache size, in whole MBs.

**Possible Values**

* Whole MBs, eg. 5MB

## DeviceKeys
### EnableCtrlKey_X
This setting is used to specify which CTRL+Key combinations should be enabled.  For each combination you wish to enable define a EnableCtrlKey_X tag but replace 'X' with the key being enabled, so for example to enable text copying specify EnableCtrlKey_C as enabled or to enable text pasting specify EnableCtrlKey_V as enabled.
>Note CE Only:
By default all CTRL+Key combinations are disabled (e.g. CTRL+C to copy text; CTRL+V to paste text).


**Possible Values**

* 0 - Disabled
* 1 - Enabled

### EnableVolumeSlider
Specific to the MC2100:<BR>Allows or prevents the key combination Orange+F1 from bringing up a slider to adjust the volume.  This setting is not application specific and will be applied globally on the device.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

### EnableBacklightSlider
Specific to the MC2100:<BR>Allows or prevents the key combination Orange+F2 from bringing up a slider to adjust the backlight.  This setting is not application specific and will be applied globally on the device.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

## DefaultMetaTags
### MetaTag
All Enterprise Browser Meta Tags can be set by default in the configuration, meaning if a common tag is required by the application it need not be present on every HTML page. Set a default tag in by specifying the tag's module, followed by a tilda character and then the properties of the module you wish to set, specified in EMML 1.1.  If the meta tag is present in both the configuration and a loaded page then the page will take priority. Logically only persistent tags can be set in the configuration, a tag's persistence being stated in the 'additional information' section in the help file.

**Possible Values**

* [Module]~[Contents expressed in EMML1.1]

## Geolocation
### GeolocationEnabled
Enables/disables HTML5 Geolocation. When enabled on a device supporting geolocation and under GPS/network coverage, the geolocation data is returned to the defined JavaScript callback. When disabled the defined JavaScript error callback is called notifying that the permission to using Geolocation is disabled.

**Possible Values**

* 0 - Disabled
* 1 - Enabled

## TabInstance
### NewTabPhysicalMemLimit
This setting controls whether a new Tab will be created using the NativeTabbar.create API when a physical memory usage percentage is hit. Ex: if it is set to 80 - then the tab instance will not be created if the physical memory usage on the device is>=80%. If the tab is unable to be created due to this limit being reached the NativeTabbar.create API callback will contain a `tabEvent` = `onTabNewError`.

**Possible Values**

* 0-100 (100=no limit)

### NewTabVirtualMemLimit
This setting controls whether a new Tab will be created using the NativeTabbar.create API when a virtual memory usage percentage is hit. Ex: if it is set to 80 - then the tab instance will not be created if the physical memory usage on the device is>=80%.If the tab is unable to be created due to this limit being reached the NativeTabbar.create API callback will contain a `tabEvent` = `onTabNewError`

**Possible Values**

* 0-100 (100=no limit)

## Remarks
### <a name="_caseSensitivity"></a>Case Sensitivity
The operating systems of some devices have case sensitive file systems. Therefore it is good practice to always keep URL values in the Config.xml file case identical to the names of the actual files.

### <a name="_batteryRefresh"></a>Battery Polling on the Enterprise Tablet
On the Enterprise Tablet the battery notification is asynchronous. For this reason, BatteryRefresh is not supported on the Enterprise Tablet. The effect of this is that a batteryEvent is fired only when the battery level changes. This has been done to save battery power compared to polling.

### <a name="_fnbehavior"></a>Interaction between FunctionKeysCapturable and EnableFunctionKey configuration settings
On Windows Mobile and Windows CE devices full control is given to the developer over how their application handles function keys.  Because of the limitations of the operating system <b>any settings applied will persist until the device is next warm booted</b>.  Which function keys have default operating system behavior will vary from device to device, e.g. on the MC75a F3 and F4 represent the red and green phone keys and on many devices the volume keys are also mapped as Function keys.  Not all function keys will have default operating system behavior.

<b><i>Unblocking function keys may expose the underlying operating system, particularly the red and green phone keys will give access to the start menu and programs.</i></b>

The table below shows the behavior of the MEB when Function Keys are pressed given the possible configuration settings:

<table border=1 width="100%" class="re-table">
	<tr>
		<th></th>
		<th>Function Keys Capturable = TRUE</th>
		<th>Function Keys Capturable = FALSE</th>
	</tr>
	
	<tr>
		<th>Enable Function Key = TRUE</th>
		<td valign="top">
			<ul>
				<li>All Function Keys <b>can</b> be captured by the <a href="../rhoelements/keycapture">Key Capture Module</a>
				<li>Function Key will <b>not</b> have its default Operating system behavior
			</ul>
		</td>
		<td valign="top">
			<ul>
				<li>Function Keys with default OS behavior <b>can not</b> be captured by the <a href="../rhoelements/keycapture">Key Capture Module</a>
				<li>Function Keys without default OS behavior <b>can</b> be captured by the <a href="../rhoelements/keycapture">Key Capture Module</a>
				<li>Function Key <b>will</b> have its default Operating system behavior (if any)
			</ul>
		</td>
	</tr>
	
	<tr>
		<th>Enable Function Key = FALSE</th>
		<td valign="top">
			<ul>
				<li>All Function Keys <b>can</b> be captured by the <a href="../rhoelements/keycapture">Key Capture Module</a>
				<li>Function Key will <b>not</b> have its default Operating system behavior
			</ul>
		</td>
		<td valign="top">
			<ul>
				<li>All Function Keys <b>can not</b> be captured by the <a href="../rhoelements/keycapture">Key Capture Module</a>
				<li>Function Key will <b>not</b> have its default Operating system behavior (if any)</li>
			</ul>
		</td>
	</tr>
</table>