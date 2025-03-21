# NFCTag API

Use the NFCTag class to get the NFC tag in certain formats, such as Ndef. For code examples, see [Rhodes Webinar Sample: NFC](https://github.com/rhomobile/webinar-samples/blob/master/nfc-rhodes/app/Nfc/nfc_controller.rb) and [Rhodes System API Samples: NFC](https://github.com/rhomobile/rhodes-system-api-samples/blob/master/app/Nfc/controller.rb).

**NOTE: As of Rhodes version 3.3.3, the [Barcode](barcode-api), [NFC](../rhodes/device-caps#nfc), and [Signature Capture](../rhodes/device-caps#signature-capture) APIs, as well as [Rhom data encryption](../rhodes/rhom#database-encryption) are removed from Rhodes. These features are only supported in Zebra RhoMobile Suite. If you wish to use these features, you will need to [upgrade to RhoMobile Suite](../rhomobile-install). Your application's build.yml will also need to be modified to [indicate the application type is 'Rhoelements'](../rhoelements/rhoelements2-native#enabling-motorola-device-capabilities). Additionally, a [RhoElements license](../rhoelements/licensing) is required.**

## Enabling NFC

To use the NFC methods, you need to enable NFC on the Android device and ensure that the version is 2.3.3 or later. Do this by adding that capability to the build.yml file:

	:::yaml
	android: 
	  version 2.3.3
	  extensions:
	  - nfc

## get_tech(tech_name)

Returns an object with the implementation of the requested NFC tech based on the NFCTagTechnology class. Refer to the NFCTagTechnology class for the types of NFC tech you can request.

	:::ruby
	Rho::NFCTag.get_tech(tech_name)

<table border="1">
<tr>
	<td><code>tech_name</code></td>
	<td>Tech name based on the NFCTagTechnology class.</td>
</tr>
</table>

## get_tech_list

Returns a string array containing the NFC tag.

	:::ruby
	Rho::NFCTag.get_tech_list

## get_ID

Returns a byte array containing the NFC tag ID.

	:::ruby
	Rho::NFCTag.get_ID
