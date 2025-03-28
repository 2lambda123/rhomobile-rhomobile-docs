# NFCManager API

Manage near field communications messages and records that your NFC application sends and receives. For code examples, see [Rhodes Webinar Sample: NFC](https://github.com/rhomobile/webinar-samples/blob/master/nfc-rhodes/app/Nfc/nfc_controller.rb) and [Rhodes System API Samples: NFC](https://github.com/rhomobile/rhodes-system-api-samples/blob/master/app/Nfc/controller.rb).

**NOTE: As of Rhodes version 3.3.3, the [Barcode](barcode-api), [NFC](../rhodes/device-caps#nfc), and [Signature Capture](../rhodes/device-caps#signature-capture) APIs, as well as [Rhom data encryption](../rhodes/rhom#database-encryption) are removed from Rhodes. These features are only supported in Zebra RhoMobile Suite. If you wish to use these features, you will need to [upgrade to RhoMobile Suite](../rhomobile-install). Your application's build.yml will also need to be modified to [indicate the application type is 'Rhoelements'](../rhoelements/rhoelements2-native#enabling-motorola-device-capabilities). Additionally, a [RhoElements license](../rhoelements/licensing) is required.**

## Enabling NFC

To use the NFC methods, you need to enable NFC on the Android device and ensure that the version is 2.3.3 or later. Do this by adding that capability to the build.yml file:

	:::yaml
	android: 
	  version 2.3.3
	  extensions:
	  - nfc

## Callback Tag Message Storage

The NFC callback stores the NFC tag messages in a hash array: 

@params['messages'] - array of NFC tag messages. Each message is a hash.

The messages can be picked up in `raw_message`, an array of bytes containing the raw message. The messages can also be picked up in `records`, an array of records where each record is a hash. The records use the NFC Data Exchange Format. Each record has the following hash items.

<table border="1">
<tr>
	<td><code>raw_record</code></td>
	<td>Array of bytes. The raw record.</td>
</tr>
<tr>
	<td><code>id</code></td>
	<td>Array of bytes. The tag ID.</td>
</tr>
<tr>
	<td><code>payload</code></td>
	<td>Array of bytes. The tag payload.</td>
</tr>
<tr>
	<td><code>tnf</code></td>
	<td>int. The Type Name Format.</td>
</tr>
<tr>
	<td><code>type</code></td>
	<td>array of bytes</td>
</tr>
<tr>
	<td><code>payload_as_string</code></td>
	<td>String. The message payload in a string (support special formats for URI, TEXT).</td>
</tr>
<tr>
	<td><code>subrecords</code></td>
	<td>message hash (only for SMART_POSTER type)</td>
</tr>
</table>

## is_supported

Returns true if the mobile device supports NFC, false otherwise.

	:::ruby
	Rho::NFCManager.is_supported

## enable

The enable method enables NFC event processing on your mobile device. Your nfc and nfc_tech callback methods are executed only if Rhodes NFC is enabled. On Android, when Rhodes NFC is enabled and the application activity is in the foreground, the activity gets high priority for NFC events. Android will not show additional UI for the select Activity for Tag processing; the Rhodes application will process the tag.

	:::ruby
	Rho::NFCManager.enable

## disable

Disables your application from receiving NFC events. Your application will not be able to receive NFC tags.

	:::ruby
	Rho::NFCManager.disable

## is_enabled

Returns true if the mobile device has been enabled for NFC, false otherwise.

## set_nfc_callback(callback_url)

Tells your application what callback to perform when it receives an NFC tag and your application is in the foreground. set_nfc_callback executes when the Android events ACTION_NDEF_DISCOVERED or ACTION_TAG_DISCOVERED are processed. [Click here for an example in the Rhodes Developer Guide under NFC.](../rhodes/nfc#setting-nfc-callback-methods)

	:::ruby
	Rho::NFCManager.set_nfc_callback(callback_url)

<table border="1">
<tr>
	<td><code>callback_url</code></td>
	<td>String. The path to the method in the NFC controller that is executed on NFC callback.</td>
</tr>
</table>

## set_nfc_tech_callback(callback_url)

Tells your application what callback to perform when it receives an NFC tag and your application is in the background. The set_nfc_tech_callback method executes when the Android event ACTION_TECH_DISCOVERED is processed. [Click here for an example in the Rhodes Developer Guide under NFC.](../rhodes/nfc#setting-nfc-callback-methods)

	:::ruby
	Rho::NFCManager.set_nfc_tech_callback(callback_url)

<table border="1">
<tr>
	<td><code>callback_url</code></td>
	<td>String. The path to the method in the NFC controller that is executed on NFC callback.</td>
</tr>
</table>

## get_current_Tag

Returns the current NFCTag that the mobile device has just read, or returns nil if no tag has been discovered. [Click here for an example in the Rhodes Developer Guide under NFC.](../rhodes/nfc#getting-determining-type-of-and-connecting-to-a-tag)

	:::ruby
	Rho::NFCManager.get_current_Tag

## perform_open_application_event

Call this method to have your application listen for NFC tags when it is in the background.  When your application is in the background or it has not started, then the NFC event was saved, and the application open/start process is executed. To process that NFC event, your application needs to call perform_open_application_event, most likely from on_activate_app.

	:::ruby
	Rho::NFCManager.perform_open_application_event

## p2p_enable_foreground_nde_push

The p2p_enable_foreground_nde_push method causes your mobile device to push an NFC message (NdefMessage) for any NFC-enabled device to receive. [Click here for an example in the Rhodes Developer Guide under NFC.](../rhodes/nfc#pushing-a-peer-to-peer-nfc-tag)

	:::ruby
	Rho::NFCManager.p2p_enable_foreground_nde_push(NDefMessage)

<table border="1">
<tr>
	<td><code>NdefMessage</code></td>
	<td>The NFC message that is pushed.</td>
</tr>
</table>

## p2p_disable_foreground_nde_push

Causes your mobile device to stop pushing NFC messages to any other NFC-enabled devices that can receive them. [Click here for an example in the Rhodes Developer Guide under NFC.](../rhodes/nfc#pushing-a-peer-to-peer-nfc-tag)

	:::ruby
	Rho::NFCManager.p2p_disable_foreground_nde_push

## make_NdefRecord_from_byte_array

Returns an NdefRecord for an NFC tag message.

	:::ruby
	Rho::NFCManager.make_NdefRecord_from_byte_array(array)

<table border="1">
<tr>
	<td><code>array</code></td>
	<td>a byte array containing a raw NFC record.</td>
</tr>
</table>

## make_NdefRecord_from_hash

Returns an NdefRecord for an NFC tag message.

The make_NdefRecord_from_hash method creates a record for an NFC tag message (NdefRecord) from a hash.

	:::ruby
	Rho::NFCManager.make_NdefRecord_from_hash(hash)

#### Parameters

`hash` is either a tag event, as in @params['Tag_event'] - 'discovered', or an array of hashes, each of the following form:

<table border="1">
<tr>
	<td><code>id</code></td>
	<td>Array of bytes. The tag ID.</td>
</tr>
<tr>
	<td><code>tnf</code></td>
	<td>Int. The Type Name Format.</td>
</tr>
<tr>
	<td><code>type</code></td>
	<td>Array of bytes. The payload type.</td>
</tr>
<tr>
	<td><code>payload</code></td>
	<td>Array of bytes. The message payload.</td>
</tr>
</table>

Example call:

	:::ruby
	hash = { 'id' => [0], 'type' => Rho::NdefRecord::RTD_URI, 'tnf' => Rho::NdefRecord::TNF_WELL_KNOWN, 'payload' => payload}
	record = Rho::NFCManager.make_NdefRecord_from_hash(hash)

## make_NdefMessage_from_byte_array

Returns an NFC tag message (NdefMessage) created from a byte array.

	:::ruby
	make_NdefMessage_from_byte_array(array)

<table border="1">
<tr>
	<td><code>array</code></td>
	<td>a byte array containing a raw NFC message.</td>
</tr>
</table>

## make_NdefMessage_from_array_of_NdefRecord

Returns an NFC tag message (NdefMessage) created from an array of records (NdefRecord, such as what you get from make_NdefRecord_from_hash). [Click here for an example in the Rhodes Developer Guide under NFC.](../rhodes/nfc#writing-an-nfc-tag)

	:::ruby
	Rho::NFCManager.make_NdefMessage_from_array_of_NdefRecord(array)

<table border="1">
<tr>
	<td><code>array</code></td>
	<td>an array of records (NdefRecord).</td>
</tr>
</table>

## make_string_from_payload

Returns a string from the payload of an NFC tag message record (NdefRecord).

	:::ruby
	Rho::NFCManager.make_string_from_payload(payload, tnf, type)

<table border="1">
<tr>
	<td><code>payload</code></td>
	<td>a byte array containing the payload.</td>
</tr>
<tr>
	<td><code>tnf</code></td>
	<td>int. The Type Name Format. From NdefRecord.</td>
</tr>
<tr>
	<td><code>type</code></td>
	<td>Array of bytes. The payload type. From NdefRecord.</td>
</tr>
</table>

## make_payload_with_absolute_uri

Returns a byte array for an NFC record payload created from a string with an absolute URI.

	:::ruby
	Rho::NFCManager.make_payload_with_absolute_uri(uri_string)

<table border="1">
<tr>
	<td><code>uri_string</code></td>
	<td>a string containing an absolute URI, such as 'http://www.rhomobile.com'.</td>
</tr>
</table>

## make_payload_with_well_known_uri

Returns a byte array for an NFC record payload from a string with an absolute URI. [Click here for an example in the Rhodes Developer Guide under NFC.](../rhodes/nfc#writing-an-nfc-tag)

	:::ruby
	Rho::NFCManager.make_payload_with_well_known_uri(prefix_code, uri_string)

<table border="1">
<tr>
	<td><code>prefix_code</code></td>
	<td>an int containing a prefix code.</td>
</tr>
<tr>
	<td><code>uri_string</code></td>
	<td>a string containing an absolute URI, such as 'http://www.rhomobile.com'.</td>
</tr>
</table>

## make_payload_with_well_known_text

Returns a byte array for an NFC record payload from a string language code and a string text.

	:::ruby
	Rho::NFCManager.make_payload_with_well_known_text(language, uri_string)

<table border="1">
<tr>
	<td><code>language</code></td>
	<td>a string containing a language code.</td>
</tr>
<tr>
	<td><code>uri_string</code></td>
	<td>a string containing an absolute URI, such as 'http://www.rhomobile.com'.</td>
</tr>
</table>