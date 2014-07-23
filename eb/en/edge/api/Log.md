#Log


## Overview
<p> Use this API to control the behavior of the RhoMobile Log API as well as access it.</p>
<p>This API gives access to Rhodes Logging functionality. There are five functions to add messages to the log with different severity (from lowest to highest) : trace, info, warning, error and fatal. Each of those functions gets two parameters: message and category. Category is an user defined group that helps with used  searching and filtering.</p>

<p>Accessing Log File:
sendLogFile: will sent all the log to server
showLog: brings up popup with log,
readLogFile: returns the full log file,
cleanLogFile: removes all logged messages</p>

<p>Filtering:</p>

<ul>
<li><p>Using level property: It limits minimal severity of messages that will be added to log. For example: setting log level to 2 (warning) will filter out messages generated by trace and info.</p></li>
<li><p>Categories: user defined groups that are used to select messages from different modules for ease of use. There are two main filters: includeCategories and excludeCategories. They are both active at the same time. includeCategories allows to select groups/categories that should be in the log (setting this property to empty will turn disable logging). excludeCategories is used for filtering out some of categories.</p></li>
<li><p>excludeFilter, this filter is used to remove all sensitive information like passwords, security tokens from log.</p></li>
</ul>


<p>Log destinations (any combinations of them):</p>

<ul>
<li>debug console (stdio),</li>
<li>device filesystem (file)</li>
<li>remote sever (url)</li>
</ul>


<h2>Enabling the API</h2>

<p>This API is part of the <code>coreapi</code> extension that is included automatically.</p>

<pre><code>:::ruby
extensions: ["coreapi"]
</code></pre>

<h2>JavaScript Usage</h2>

<p>Be sure to review the <a href="/guide/api_js">JavaScript API Usage</a> guide for important information about using this API in JavaScript</p>

<h2>Ruby Usage</h2>

<p>Be sure to review the <a href="/guide/api_ruby">Ruby API Usage</a> guide for important information about using this API in Ruby</p>



##Methods



### cleanLogFile()
Clean log file, all logged messages will be removed. 

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.cleanLogFile()</code> </li></ul></li></ul>

### error(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)
Log message at the Error level.

####Parameters
<ul><li>message : <span class='text-info'>STRING</span><p>
Log message. </p></li><li>category : <span class='text-info'>STRING</span><span class='label '> Default: APP</span><p>
Log category. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.error(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)</code> </li></ul></li></ul>

### fatalError(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)
Log message at the FatalError level. Application will be terminated (on all platforms except iOS).

####Parameters
<ul><li>message : <span class='text-info'>STRING</span><p>
Log message. </p></li><li>category : <span class='text-info'>STRING</span><span class='label '> Default: APP</span><p>
Log category. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.fatalError(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)</code> </li></ul></li></ul>

### info(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)
Log message at the Info level.

####Parameters
<ul><li>message : <span class='text-info'>STRING</span><p>
Log message. </p></li><li>category : <span class='text-info'>STRING</span><span class='label '> Default: APP</span><p>
Log category. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.info(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)</code> </li></ul></li></ul>

### readLogFile(<span class="text-info">INTEGER</span> limit)
Read log file. Returns string from the log file containing specified number of symbols.

####Parameters
<ul><li>limit : <span class='text-info'>INTEGER</span><p>
Maximum size of the resulting string in symbols. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Callback
Async Callback Returning Parameters: <span class='text-info'>STRING</span></p><ul></ul>

####Returns
Synchronous Return:<ul><li>STRING</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.readLogFile(<span class="text-info">INTEGER</span> limit)</code> </li></ul></li></ul>

### sendLogFile()
Send log file to destinationURI property. Please note that this procedure is blocking and will stop any logging while log file is being send.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.sendLogFile()</code> </li></ul></li></ul>

### showLog()
Display Log view window.

####Parameters
<ul><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.showLog()</code> </li></ul></li></ul>

### trace(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)
Log message at the Trace level. By default trace messages are not shown in log (if level equals to 1).

####Parameters
<ul><li>message : <span class='text-info'>STRING</span><p>
Log message. </p></li><li>category : <span class='text-info'>STRING</span><span class='label '> Default: APP</span><p>
Log category. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.trace(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)</code> </li></ul></li></ul>

### warning(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)
Log message at the Warning level.

####Parameters
<ul><li>message : <span class='text-info'>STRING</span><p>
Log message. </p></li><li>category : <span class='text-info'>STRING</span><span class='label '> Default: APP</span><p>
Log category. </p></li><li>callback : <span class='text-info'>CallBackHandler</span></li></ul>

####Returns
Synchronous Return:<ul><li>Void</li></ul>

####Platforms

* Javascript
* Ruby
* Android
* iOS
* Windows Embedded
* Windows Phone 8
* Windows Desktop

####Method Access:
<ul><li><i class="icon-book"></i>Class Method: This method can only be accessed via the API class object. <ul><li><code>Rho.Log.warning(<span class="text-info">STRING</span> message, <span class="text-info">STRING</span> category)</code> </li></ul></li></ul>

##Properties



###destination

####Type
<span class='text-info'>ARRAY</span> 
####Description

List of log destinations that are being used. Destination could be set to empty (disable all logging), "file" - log just into file specified in (filePath), "stdio" - log into debug debug console, "uri" - send log to the server. Logging to several destinations could be set by setting destination to comma separated list in any order (for example "stdio,file"). By default logging to console can be enabled from rhoconfig.txt (LogToOutput = 1). After Rhodes initialization logging to file is enabled automatically.
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: Rho.Log.DEST_FILE 
	* String: file
	* 
Log is written to a local file on the device (typically rholog.txt)
* Constant: Rho.Log.DEST_OUTPUT 
	* String: stdio
	* 
Log is written to the standard output (ex: Android ADB)
* Constant: Rho.Log.DEST_URI 
	* String: uri
	* 
Log is written to a remote logger.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.destination</code> </li></ul></li></ul>

###destinationURI

####Type
<span class='text-info'>STRING</span> 
####Description

Log server URI where log will be posted by using Rho::Log.sendLogFile or from the log view. Log server source code is open and available at http://github.com/rhomobile/rhologs, so you can deploy your own logserver. URI format: 'http://host:port[/path][?log_name=appName]'. Default value is set in rhoconfig.txt (logserver)
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.destinationURI</code> </li></ul></li></ul>

###excludeCategories

####Type
<span class='text-info'>STRING</span> 
####Description

Comma-separated list of excluded log categories. Set to '' (empty) to allow all messages to be logged. Set to concrete value to filter out log from those categories. Default value is '' (empty), it is set in rhoconfig.txt (ExcludeLogCategories)
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.excludeCategories</code> </li></ul></li></ul>

###excludeFilter

####Type
<span class='text-info'>STRING</span> 
####Description

Define exclude parameters log filter(for security reasons) - parameter names separated by comma. It works when user tries to put in log string containing json / urls. Default value is "" (empty). For example, if user set excludeFilter="password", then tries to put in log this string: "{"user":"alex","password":"abcdef","sessionid":123456}", "abcdef" will not appear in log.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.excludeFilter</code> </li></ul></li></ul>

###filePath

####Type
<span class='text-info'>STRING</span> 
####Description

Path to the log file including file name. The path is relative to the platform specific application root or start if from '/' if you wish to store elsewhere ('/mnt/sdcard/myapp.log').  Default file path is "rholog.txt"
####Params
<p><strong>Default:</strong> rholog.txt</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.filePath</code> </li></ul></li></ul>

###fileSize

####Type
<span class='text-info'>INTEGER</span> 
####Description

Maximum log file size in bytes, set 0 to unlimited size; when limit is reached, log wraps to beginning of file. Default value is 50000, it is set in rhoconfig.txt (MaxLogFileSize)
####Params
<p><strong>Default:</strong> 50000</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.fileSize</code> </li></ul></li></ul>

###includeCategories

####Type
<span class='text-info'>STRING</span> 
####Description

Comma-separated list of included log categories. Set to '*' to log all categories. Set to '' (empty) to filter out all messages. Default value is '*', it is set in rhoconfig.txt (LogCategories).
####Params
<p><strong>Default:</strong> *</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.includeCategories</code> </li></ul></li></ul>

###level

####Type
<span class='text-info'>INTEGER</span> 
####Description

The current logging level. Minimal severity level of messages that will appear in log. When level is set to 0 any messages will be logged. When level is set to 4 only fatal error messages will be logged. Default value is defined in rhoconfig.txt (MinSeverity) 
####Values

<strong>Possible Values</strong> (<span class='text-info'>STRING</span>):
 
* Constant: Rho.Log.LEVEL_TRACE 
	* String: 0
	* 
Everything will be logged. Also see settings for controlling log size.
* Constant: Rho.Log.LEVEL_INFO 
	* String: 1
	* 
Information level logs and above will be shown.
* Constant: Rho.Log.LEVEL_WARNING 
	* String: 2
	* 
Warnings and above will only be shown.
* Constant: Rho.Log.LEVEL_ERROR 
	* String: 3
	* 
Error level log messages and above will be shown.
* Constant: Rho.Log.LEVEL_FATAL 
	* String: 4
	* 
Fatal level log messages and above will be shown.
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.level</code> </li></ul></li></ul>

###memoryPeriod

####Type
<span class='text-info'>INTEGER</span> 
####Description

Enables the logging of memory usage in the system; specifies the time interval in milliseconds at which memory logs will be generated periodically. Setting it to 0 will disable logging memory information.
####Params
<p><strong>Default:</strong> 0</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.memoryPeriod</code> </li></ul></li></ul>

###netTrace

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Turn on local http server traces. Traces contain information about connection process, sent and received headers and data. Please note that this parameter will not take an effect in case of remote server app (and / or shared runtime). Default value can be overridden by the setting in rhoconfig.txt (net_trace) 
####Params
<p><strong>Default:</strong> false</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.netTrace</code> </li></ul></li></ul>

###skipPost

####Type
<span class='text-info'>BOOLEAN</span> 
####Description

Skip http package body from log(for security reasons). Please note that this parameter will not take an effect in case of remote server app (and / or shared runtime), no log will appear in this case. 
####Params
<p><strong>Default:</strong> false</p>
####Access
<ul><li><i class="icon-book"></i>Class: This property can only be accessed via the API class object. <ul><li><code>Rho.Log.skipPost</code> </li></ul></li></ul>

##Examples



###Show log file

Show the contents of the log file in a window with controls to refresh, clear and send. Useful for debugging and when asking users to report error messages.
<pre><code>:::javascript
           
Rho.Log.showLog();
                
</code></pre>

###Read log file content

Retrieve the contents of the log file as a string.
<pre><code>:::javascript
           
//Read at most 16384 symbols
logFileContent = Rho.Log.readLogFile(16384);
                
</code></pre>

###Clean log file

Clear the contents of the log file. In this example, logFileContentBefore will contain the log up until that point, while logFileContentAfter will be empty.
<pre><code>:::javascript
           
// Read log file
logFileContentBefore = Rho.Log.readLogFile(16384);

// Clear log file
Rho.Log.cleanLogFile();

// Read log file again - this time it will be empty
logFileContentAfter = Rho.Log.readLogFile(16384);
                
</code></pre>

###Logging categories

Categories help you organize your logging messages and find related statements using tools like grep or a text editor's "search" function.
<pre><code>:::javascript
           
Rho.Log.info("Consectetuer adipiscing elit", "Lorem Ipsum");
Rho.Log.info("Foo acquired value Bar in method Baz", "Miscellaneous");

//The above code will result in logging statements like these
Lorem Ipsum| Consectetuer adipiscing elit
Miscellaneous Foo acquired value Bar in method Baz

                
</code></pre>

###Memory Usage

You can ask the system to automatically log memory usage information on a set interval. This can be used to debug potential memory leaks in operations where a high number of objects are touched in memory. 
<pre><code>:::javascript
           
Rho.Log.memoryPeriod = 1000;
// Perform memory-intensive operations here. Examining the log will tell us if we have a memory leak
// Once our task finishes, disable automatic memory logging
Rho.Log.memoryPeriod = 0;
               
</code></pre>