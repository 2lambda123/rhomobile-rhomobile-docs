# Application Configuration

## Build time configuration

### Application Permissions and Capabilities

To enable specific device capabilities, edit application's build.yml as below:

	:::yaml
	capabilities:
	  - camera
	  - gps
	android:
	  capabilities:
	    - network_state

Rhodes support common plus platform-specific capabilities. They are merged into a single list at build time.

** NOTE: Right now only Android recognizes these platform specific configuration options. However, we are planning to enable these options across all platforms. **

List of supported capabilities:

* audio: allow using of audio hardware (record audio, modify audio settings)
* camera: allow use of hardware camera
* gps: allow use of geo location service
* network_state: allow read device network state (connected/disconnected)
* phone: allow make calls/read phone state
* pim: allow read/modify personal information and contacts
* push: allow to use PUSH on device
* record_audio: allow recording audio ('audio' implies it)
* vibrate: allow to use hardware vibration mechanism
* bluetooth: allow to use bluetooth hardware
* sdcard: allow writing to SD card on Android devices

### RhoGallery Security Token

To restrict access to the application it could be built with a security token. Specify security token in the build.yml and build application. Application built with security token can be started in normal mode only if you provide this token as a parameter.
If you do not specify correct security token in start params, application will close on start by default. If you want do something instead of exit (for example show special message or run application in limited mode etc.) you can define another start_path for your application in "rhoconfig.txt":

	invalid_security_token_start_path = '/app/InvalidSecurityTokenStartPage'

Specify security token in build.yml:

	security_token: 123

Run application with special parameter:
	:::ruby
	System::run_app( 'app_name', "security_token=123" )

### JavaScript and CSS Obfuscation

To enable JavaScript and/or CSS code obfuscation at `public` folder of Rhodes application just add the following lines to the build.yml:

	obfuscate:
	  js: yes
	  css: yes
	  exclude_dirs: ["jqmobile", "jqtouch", "jquery"]

If JavaScript or CSS code obfuscation is not required, then just omit `js` or `css` line accordingly.

**NOTE: The `jqmobile`, `jqtouch`, and `jquery` folders <b>must</b> be excluded when obfuscation is enabled, because the obfuscated versions of these libraries are there already.

## Run time configuration
Each Rhodes application contains a configuration file called "rhoconfig.txt".  A typical rhoconfig.txt will look like the following when an app is generated:

Startup page for your application

	start_path = '/app'

NOTE: If you set your start path to a location not ending in .erb, then the ruby code in application.rb will not execute (ex. if you are trying to change the default menu, etc.).

Path to the options page (in this case handled by JavaScript)

	options_path = '/app/Settings'

Location of bundle url (i.e. from rhohub.com); used by desktop win32 simulator

	rhobundle_zip_url = ''

Optional password to access bundle (usually not required); used by desktop win32 simulator

	rhobundle_zip_pwd = nil

Log level: 0-trace, 1-info(app level), 3-warnings, 4-errors. It is recommended for production set it to 3 to minimize log and increase speed lost due to log output

	MinSeverity  = 1

Enable copy log messages to standard output, useful for debugging

	LogToOutput = 1

Log categories: '*' means all categories, otherwise list them : Cat1, Cat2

	LogCategories = *

What log categories to exclude

	ExcludeLogCategories =

Max log file size in Bytes, set 0 to unlimited size; when limit is reached, log wraps to beginning of file

	MaxLogFileSize=50000

Custom log file path. On Android devices "sdcard" capability must be enabled to allow writing to SD card.

	LogFilePath = '/mnt/sdcard/myapp.log'

Enables the logging of memory usage in the system; specifies the time interval in milliseconds at which memory logs will be generated periodically

	LogMemPeriod=5000

Turn on local http server traces, off by default

	net_trace = 0

Skip http package body from log(for security reasons), off by default

	log_skip_post = 1

Define exclude parameters log filter(for security reasons) - parameter names separated by comma, empty by default.

	log_exclude_filter = 'login, password'

Timeout of network requests in seconds (30 by default)

	net_timeout = 60

Log server address where log will be posted by using RhoConf.send_log or from the log view. Log server source code is open and available at <http://github.com/rhomobile/rhologs>, so you can deploy your own logserver

	logserver = 'http://rhologs.heroku.com'

Log file prefix - contain human-readable text

	logname='helloworld'

Sync server url, typically this will look like 'http://<hostname>:<port>/application'. For example:

	syncserver = 'http://localhost:9292/application'

Set this option to 1 in order to open Rhodes app in full screen mode. Default is 1 for Android up to Rhodes 2.2.5. On all other platforms and on Android from Rhodes > 2.2.5 default is 0

	full_screen = 1

Set this option to 1 in order to enable WebView zoom (Android only). Default is 0

	enable_screen_zoom = 1

Set application window width and hieght (Win32 only). Default is 400 x 600.

	screen_width = 800
	screen_height = 600

Port of the local (embedded) HTTP server. This parameter is mainly for debug purposes. If not specified, application will use dynamically selected one.
**NOTE WARNING!!! Remove this parameter before put application to production. **

	local_server_port = 8080

Show status bar on windows mobile. Default is 1 (show)

	wm_show_statusbar = 1

**NOTE: This parameter works only with Internet Explorer Browser. When you use Zebra WebKit browser, statusbar is not available **

Disable screen rotation. By default set to 0 (enabled). This option available on ANDROID and iPhone ONLY

	disable_screen_rotation = 1

Disable closing app when pressing back on home screen on blackberry

	bb_disable_closebyback = 0

Load images in background, this improve reaction speed on user actions, 0 by default

	bb_loadimages_async = 0

Set to 0 to reset the bulksync_state and trigger a bulk sync the next time rhodes synchronizes

	bulksync_state = 1

Hides forward button and animates back button transition

	jqtouch_mode=1

Splash screen image display options. See more details [here](ui#loading-screen).

	splash_screen='zoom'

Turn on Full Browser mode for Blackberry 4.6.0 and higher

	use_bb_full_browser = 1

Turn on Persistent Storage usage mode for Blackberry

	use_persistent_storage = 1

To use only models from bulk database. If true, application will not create models and will use models from bulk sync database

	use_bulk_model = true

Disable WebView to check SSL certificate (Android). Used to allow proceed with self signed certificates. Use at your own risk. This configuration option works well for any Android version except 2.3.3/2.3.4 (due to Android WebView behavior).

	no_ssl_verify_peer = 1

Allows finish sync if sync is active at the time when application is put to background. This parameter will take effect only on iOS devices.

	finish_sync_in_background = 1

Enable web plugins (Flash etc.) on Android devices.

	enable_web_plugins = 1

### Last Visited Page
To save/restore last visited page use WebView.current_location in on_ui_created/on_ui_destroyed of [AppApplication class](application#appapplication-class).

### Application Database Version
If you want the next version of your application to start from a clean database, set app_db_version in rhoconfig.txt.
When a Rhodes app starts, it compares the current db version with app_db_version cleans the db if they do not match.

### RhoConfig API Examples

Each of the configuration options shown above are available through the [RhoConfig Ruby API](../rhodesapi/rhoconfig-api).

 * [configuration property methods](../rhodesapi/rhoconfig-api#configuration-property-methods) - The properties in the rhoconfig.txt file for a Rhodes application are available through the RhoConfig API. To access the property, use the name of the property as the method name.
 * [exists?](../rhodesapi/rhoconfig-api#exists) - Checks to see if a configuration property exists for this Rhodes application.

To access configuration properties from application code use the Rho::RhoConfig class.<a id="rhoconfig-api-ex"></a>

	:::ruby
	Rho::RhoConfig.full_screen
	Rho::RhoConfig.app_property='some value'
	if Rho::RhoConfig.exists?('some_property')
	  #do something
	end

For example:

To get start_path:
	:::ruby
	Rho::RhoConfig.start_path
	#=> will return current value of start_path

To set start_path
	:::ruby
	Rho::RhoConfig.start_path = '/app/MyObject'
	#=> start_path will be saved to rhoconfig.txt as '/app/MyObject'

You may store any arbitrary options in the rhoconfig.txt file using the Ruby API. Keep in mind that they will may be lost the next time the user installs a new version of the application.

# TBD add link to update of rhoconfig.txt

### SyncEngine Configuration
In the previous section, there is a "syncserver" option available.  This option can be changed through the Rho::RhoConfig API as you would expect. However, since changing the syncserver option requires updating the SyncEngine at runtime, another Ruby call is available:

	:::ruby
	SyncEngine.set_syncserver(
		'http://examplesyncserver.com/apps/MyApp/sources/')

Calling the function above will do the following:

* Update the in-memory syncserver for the SyncEngine (all subsequent synchronization will use the new syncserver)
* Perform a logout to make sure the session for the old syncserver is removed
* Write the new syncserver property to rhoconfig.txt

To enable auto sync you can call (enabled by default with 5 minutes interval )

	:::ruby
	SyncEngine.set_pollinterval(timeout_in_seconds)

OR set in rhoconfig.txt:

	sync_poll_interval=timeout_in_seconds

To disable auto sync you can call

	:::ruby
	SyncEngine.set_pollinterval(0)

OR set in rhoconfig.txt:

	sync_poll_interval=0

### Logging
To show the application log on the device with log and log-related menu items, like clear, send and log options:

	:::ruby
	Rho::RhoConf.show_log

To send the log to the log server url, defined in rhoconfig.txt:

	:::ruby
	Rho::RhoConf.send_log = "http://example.com/client_log?client_id=123&device_pin=345&log_name=mylog"

Url format: \<logserver\>/client_log?client_id=\<client_id\>&device_pin=\<device_pin\>&log_name=\<logname\>

### Persistent Storage (Blackberry only)
To enable use of the RIM persistent storage API in rhodes, just add following line to your rhoconfig.txt:

	use_persistent_storage = 1

It will enable RIM's persistent storage API (instead of files) to store the DB version, the DB journal and the database itself. The main goal of persistent storage is that all objects stored by an application will be automatically removed when the application is uninstalled.
