# NFCTagTechnology_MifareClassic API

Subset of NFCTagTechnology. For code examples, see [Rhodes System API Samples: NFC](https://github.com/rhomobile/rhodes-system-api-samples/blob/master/app/Nfc/controller.rb).

**NOTE: As of Rhodes version 3.3.3, the [Barcode](barcode-api), [NFC](../rhodes/device-caps#nfc), and [Signature Capture](../rhodes/device-caps#signature-capture) APIs, as well as [Rhom data encryption](../rhodes/rhom#database-encryption) are removed from Rhodes. These features are only supported in Zebra RhoMobile Suite. If you wish to use these features, you will need to [upgrade to RhoMobile Suite](../rhomobile-install). Your application's build.yml will also need to be modified to [indicate the application type is 'Rhoelements'](../rhoelements/rhoelements2-native#enabling-motorola-device-capabilities). Additionally, a [RhoElements license](../rhoelements/licensing) is required.**

## Enabling NFC

To use the NFC methods, you need to enable NFC on the Android device and ensure that the version is 2.3.3 or later. Do this by adding that capability to the build.yml file:

	:::yaml
	android: 
	  version 2.3.3
	  extensions:
	  - nfc

## Constants

	:::term
	KEY_DEFAULT = [0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF]
	KEY_MIFARE_APPLICATION_DIRECTORY = [0xA0, 0xA1, 0xA2, 0xA3, 0xA4, 0xA5]
	KEY_NFC_FORUM =[0xD3, 0xF7, 0xD3, 0xF7, 0xD3, 0xF7]    
	
## Types

	:::term
	TYPE_CLASSIC = 0
	TYPE_PLUS = 1
	TYPE_PRO = 2
	TYPE_UNKNOWN = -1

## get_type

Returns an int: the type of a MifareClassic tag.

### NFCTagTechnology_MifareClassic.convert_type_to_string(type)

Returns a string: the named type of a MifareClassic tag.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.convert_type_to_string(type)

<table border="1">
<tr>
	<td><code>type</code></td>
	<td>int: the type of a MifareClassic tag.</td>
</tr>
</table>

## write_block(index, block)

Writes a block to a MifareClassic tag.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.write_block(index, block)

<table border="1">
<tr>
	<td><code>index</code></td>
	<td>integer: the index to where in the tag sector the block will be written.</td>
</tr>
<tr>
	<td><code>block</code></td>
	<td>a 16 byte array written to the tag.</td>
</tr>
</table>

## read_block(index)

Returns a block: a 16 byte array of data read from a MifareClassic tag.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.read_block(index)

<table border="1">
<tr>
	<td><code>index</code></td>
	<td>integer: the index to where in the tag sector the block is read from.</td>
</tr>
</table>

## get_size

Return the size in bytes of a MifareClassic tag.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.get_size

## get_block_count

Return the number of blocks in a MifareClassic tag.

## get_sector_count

Returns the sector count in a MifareClassic tag.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.get_block_count

### get_blocks_in_sector_count

Returns the number of blocks in a sector of a MifareClassic tag.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.get_blocks_in_sector_count(index)

<table border="1">
<tr>
	<td><code>index</code></td>
	<td>integer: the index to the tag sector.</td>
</tr>
</table>

## sector_to_block

Returns the index of the first block in a sector in a MifareClassic tag. Does not cause any RF activity.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.sector_to_block(index)

<table border="1">
<tr>
	<td><code>index</code></td>
	<td>integer: the index to the tag sector.</td>
</tr>
</table>
	
## authenticate_sector_with_key_A

Authenticates a sector with a key. Returns true if the authenticate was passed.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.authenticate_sector_with_key_A(index, key)

<table border="1">
<tr>
	<td><code>index</code></td>
	<td>integer: the index to the tag sector.</td>
</tr>
<tr>
	<td><code>key</code></td>
	<td>a 6 byte array containing the key.</td>
</tr>
</table>

## authenticate_sector_with_key_B

Authenticates a sector with a key. Returns true if the authenticate was passed.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.authenticate_sector_with_key_B(index, key)

<table border="1">
<tr>
	<td><code>index</code></td>
	<td>integer: the index to the tag sector.</td>
</tr>
<tr>
	<td><code>key</code></td>
	<td>a 6 byte array containing the key.</td>
</tr>
</table>

## transceive

Sends data in a byte array to a tag and returns the result from the tag in a byte array.

	:::ruby
	Rho::NFCTagTechnology_MifareClassic.transceive(data)

<table border="1">
<tr>
	<td><code>data</code></td>
	<td>byte[] sent to the tag.</td>
</tr>
</table>
