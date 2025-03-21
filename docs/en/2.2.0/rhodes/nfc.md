# NFC Developer Guide

The Near Field Communications (NFC) API allows you to use NFC functionality in your Rhodes application. With the NFC API, you can check to see if the mobile device supports NFC, and if so, have it listen for an NFC tag and register a callback if it finds one. You can also have your device push out an NFC tag. 

**NOTE: As of Rhodes version 3.3.3, the NFC API is removed from Rhodes. This feature is only supported in Zebra RhoMobile Suite. If you wish to use this feature, you will need to [upgrade to RhoMobile Suite](../rhomobile-install). Your application's build.yml will also need to be modified to [indicate the application type is 'Rhoelements'](../rhoelements/rhoelements2-native#enabling-motorola-device-capabilities). Additionally, a [RhoElements license](../rhoelements/licensing) is required.**

Example Code
-----------
Example code for NFC is located here.

 * [Rhodes Webinar Sample: NFC](https://github.com/rhomobile/webinar-samples/tree/master/nfc-rhodes)
 * [Rhodes System API Samples: NFC](https://github.com/rhomobile/rhodes-system-api-samples/tree/master/app/Nfc)

## Generating a Container Model for NFC

To create a Rhodes NFC application, you generate a Rhodes application, then you generate an NFC model in that application. Note that the model attributes are stubs in this case; you might not use the model attribute code that is generated.

	:::term
	$ rhodes app nfc
	
	$ (the command line now shows the app being generated)
	
	$ cd nfc
	$ rhodes model stub1 stub2

## Setting up build.yml

NFC is supported only on Android devices with Android 2.3.3 or later. You must edit the Android section in your build.yml file for NFC: 'nfc' extension must be in the extension list.

	:::text
	android:
	  extensions:
	  - nfc

## Enabling NFC on the Mobile Device

Before you can send or receive NFC tags on your NFC-capable mobile device, you must enable NFC on the device with the method NFCManager.enable. Also, when your application is in the background, you should enable it to receive NFC tag messages with the method NFCManager.perform_open_application_event.

Rhodes has a hook called on_activate_app that is called every time an application using this hook launches, and when that application comes in from the background. You can call this hook in app/application.rb.

	:::ruby
	def on_activate_app
	  # enable NFC on your NFC-capable mobile device
	  Rho::NFCManager.enable
	  
	  # Set the method to call for nfc callback
	  Rho::NFCManager.set_nfc_callback("/app/Nfc/nfc_callback")
	  
	  # Enable listening for events when the application is in the background
	  Rho::NFCManager.perform_open_application_event
	end

You can use the method NFCManager.is_supported to see if NFC is supported on your mobile device, and the method NFCManager.is_enabled to see if NFC has been enabled. The method NFCManager.disable disables NFC on your mobile device.

## Setting NFC Callback Methods

If your method is going to read or write NFC tags, it also needs to set the callback methods that process the NFC tag. The NFCManager.set_nfc_tech_callback is for reading and writing NFC tags (when the Android ACTION_TECH_DISCOVERED event is processed). NFCManager.set_nfc_callback is for peer-to-peer communication (when the Android ACTION_NDEF_DISCOVERED or ACTION_TAG_DISCOVERED events are processed).

For NFCManager.set_nfc_tech_callback (the Android ACTION_TECH_DISCOVERED event), set up your list of techs in a resource file : [Rhodes ROOT]/lib/extensions/nfc/ext/nfc/platform/android/additional_files/res/xml/filter_nfc.xml. Refer to the Android documentation - [Android ACTION_TECH_DISCOVERED description](http://developer.android.com/reference/android/nfc/NfcAdapter.html#ACTION_TECH_DISCOVERED). Here is an example.

	:::xml
	<?xml version="1.0" encoding="utf-8"?>
	<resources xmlns:xliff="urn:oasis:names:tc:xliff:document:1.2">
	  <!-- capture all MIFARE Classics with NDEF payloads -->
	  <tech-list>
	    <tech>android.nfc.tech.MifareClassic</tech>
	    <tech>android.nfc.tech.Ndef</tech>
	  </tech-list>
	</resources>

You will write the callback methods in your NFC controller method to process your NFC tags: the example below points to the callback methods nfc_callback and nfc_tech_callback in the app/Nfc/nfc_controller.rb file. You can set the NFC callback methods in on_activate_app.

	:::ruby
	def on_activate_app
	  # enable NFC on your NFC-capable mobile device
	  Rho::NFCManager.enable
	  
	  # Set the method to call upon an nfc callback
	  Rho::NFCManager.set_nfc_callback("/app/Nfc/nfc_callback")
	  
	  # Set the method to call upon an nfc tech callback
	  Rho::NFCManager.set_nfc_tech_callback("/app/Nfc/nfc_tech_callback")
	  
	  # Enable listening for events when the application is in the background
	  Rho::NFCManager.perform_open_application_event
	end

Callbacks can be simple. You could just have the callback method say that it received a tag:

	:::ruby
	def nfc_callback
	  @log = "TAG received: #{Time.now.strftime('%H:%M:%S')}"
      add_to_log(@log)
	end

But to read or write NFC message and records from the NFC tag, you first get the current tag, determine the type of tag, and connect to the tag.

## Getting, Determining Type of, and Connecting to a Tag

Before you read from or write to a tag, get the tag with the method NFCManager method get_current_Tag. Find out what tech the tag uses with the method NFCTag.get_tech; the tag techs are listed in the NFCTagTechnology class. In this example, the tag is Ndef tech. Connect to the tag with the method NFCTagTechnology.connect.

	:::ruby
	tag = Rho::NFCManager.get_current_Tag
	ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
	  if ndef != nil
	    ndef.connect
	    # read or write the NFC tag
	  end

You can now read from or write to the NFC tag.

## Reading an NFC Tag

After you get a tag, determine its type, and connect to the tag, you can read from the tag.

### Read the Tag Message and Get Its Records

In this example, it is an Ndef tag, so use the NTagTechnology_Ndef.read_NdefMessage method (subclass of NFCTechnology) to read the message. Then get the records from that message: since this is an Ndef tag, use the NTagTechnology_Ndef.get_records method.

	:::ruby
	# read the ndef tag message and get the records from it.
	msg = ndef.read_NdefMessage
    records = msg.get_records

### Iterate Through the Records and Hash Them

Iterate through the records in the message (in the following example, the message has only one record). And since this is an Ndef record, use the NdefRecord method make_hash to make a hash of the record.

	:::ruby
    # iterate through the array of records and hash the record
    # this example has only one tag, so the array has only one element
    r_a = []
    records.each do |record|
      r_a << record.make_hash
    end

### Grab the Payload from the Hash

In the case of the Ndef record, grab the payload from the hash with the payload_as_string part of the hash.

	:::ruby
    # assign to a variable and print it out
    msg_hash = { 'records' => r_a }
    puts "records after processing: #{msg_hash.inspect}"
    # Assign the string payload from the hash to the result
    result = "Tag Result: " + msg_hash['records'][0]['payload_as_string'] if msg_hash['records'].size > 0

## Writing an NFC tag

After you get a tag, determine its type, and connect to the tag, you can write to the tag.

To write to an NFC tag, you fill the tag with a message that you create and load with payloads.

### Creating a Message for the NFC tag

For an Ndef record, you make payloads for the records in the message. You have several methods you can use to make the payload; the example here uses the NFCManager.make_payload_with_well_known_uri method. The NFC tag will contain the URL for Rhomobile.

	:::ruby
	payload = Rho::NFCManager.make_payload_with_well_known_uri(0, 'http://www.rhomobile.com')

### Putting the Payload Into The Record

For a Ndef record, make a hash and put the payload into it.

	:::ruby
    hash = { 'id' => [0], 'type' => Rho::NdefRecord::RTD_URI, 'tnf' => Rho::NdefRecord::TNF_WELL_KNOWN, 'payload' => payload}

### Making the Records, Put Records into an Array, Make a Message

Then make a record from the hash with the NFCManager method make_NdefRecord_from_hash, put the record(s) into an array, and make a message from the array with the NFCManager method make_NdefMessage_from_array_of_NdefRecord(records).

	:::ruby
    record = Rho::NFCManager.make_NdefRecord_from_hash(hash)       
    records = [record]        
    msg = Rho::NFCManager.make_NdefMessage_from_array_of_NdefRecord(records)

### Writing the NFC Message

Once an Ndef message is created, you can write it with the NFCTagTechnology_Ndef method write.

	:::ruby
	ndef.write_NdefMessage(msg)
    puts ' finish write NdefMessage'

## Closing the Connection to the Tag

When you are done reading or writing to the NFC tag, close the connection to it with the NFCTagTechnology method close.

	:::ruby
    ndef.close

For example, you can have the following code in your NFC controller method to process NFC tech callbacks. 

	:::ruby
	def nfc_tech_callback	
	  # Get the current tag 
	  tag = Rho::NFCManager.get_current_Tag
	  # get the tag technology to find out how to process it; it is an ndef tag
	  ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
	  if ndef != nil
	    # connect to the ndef tag
	    ndef.connect
	    #... read from or write to the NFC tag
	    ndef.close
	  end
	  #...
	end

## Pushing a Peer-to-Peer NFC Tag

You can push an NFC tag to another NFC-enabled device with the NFCManager. p2p_enable_foreground_nde_push(msg) method.

First, you need to make the payload for the message.

	:::ruby
	def start_nfc_push
      puts "Sending #{@params['push'].inspect}..."
      payload = Rho::NFCManager.make_payload_with_well_known_text("en", @params['push'])
      #... more processing
    end

Then put the payload into the record. This is an Ndef example, so we make a hash, then use the NFCManager.make_NdefRecord_from_hash method to create the record.

	:::ruby
    hash = { 
      'id' => [0], 
      'type' => Rho::NdefRecord:: RTD_TEXT, 
      'tnf' => Rho::NdefRecord::TNF_WELL_KNOWN, 
      'payload' => payload
    }
    record = Rho::NFCManager.make_NdefRecord_from_hash(hash)

Make the record array, then use the NFCManager. make_NdefMessage_from_array_of_NdefRecord(records) method to make the message from the record array.

	:::ruby
    records = [record]
    msg = Rho::NFCManager.make_NdefMessage_from_array_of_NdefRecord(records)

Now you can push the message with the NFCManager. p2p_enable_foreground_nde_push(msg) method.

	:::ruby
      # start push message
	  Rho::NFCManager.p2p_enable_foreground_nde_push(msg)
      @notice = "Started push."
      render :action => :index
	end

And when you want to stop pushing the message, use the NFCManager. p2p_disable_foreground_nde_push method.

	:::ruby
	def stop_nfc_push
      Rho::NFCManager.p2p_disable_foreground_nde_push
      @notice = "Stopped push."
      render :action => :index
	end

## NdefRecord Class API

The NdefRecord class contains methods for getting data from NFC Ndef tag records.

An Ndef record consists of a hash:

	:::ruby
	ID = 'id'
	TNF = 'tnf'
	TYPE = 'type'
	PAYLOAD = 'payload'

The Type Name Format (TNF part of the hash) is a 3-bit field that indicates how you interprete the type field (TYPE). Here is a list of the TNF values.

	:::ruby
	TNF_ABSOLUTE_URI = 3
	TNF_EMPTY = 0
	TNF_EXTERNAL_TYPE = 4
	TNF_MIME_MEDIA = 2
	TNF_UNCHANGED = 6
	TNF_UNKNOWN = 5
	TNF_WELL_KNOWN = 1

The RTD text type (TYPE part of the hash) is used with the TNF_WELL_KNOWN value.

	:::ruby
	RTD_TEXT = [0x54]   # "T"
	RTD_URI = [0x55] # "U"
	RTD_SMART_POSTER = [0x53, 0x70] # "Sp"
	RTD_ALTERNATIVE_CARRIER = [0x61, 0x63]   # "ac"
	RTD_HANDOVER_CARRIER = [0x48, 0x63] # "Hc"
	RTD_HANDOVER_REQUEST = [0x48, 0x72] # "Hr"
	RTD_HANDOVER_SELECT = [0x48, 0x73] # "Hs"

Here is some code that creates a hash for an NdefRecord, which will be part of an NFCMessage to be pushed to an NFC-capable mobile device.

	:::ruby
	hash = { 'id' => [0], 'type' => Rho::NdefRecord::RTD_URI, 'tnf' => Rho::NdefRecord::TNF_WELL_KNOWN, 'payload' => payload}

### NdefRecord get methods

You can extract data from an Ndef record with the following methods:

	:::ruby
	get_id                   # returns byte[] 
	get_tnf                  # return int
	get_type                 # returns byte[]
	get_payload              # returns byte[]
	get_payload_as_string    # returns string
	get_byte_array           # returns byte[]

Example:

	:::ruby
    ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
    if ndef != nil
      ndef.connect
	  type = ndef.get_type
	  #...
	end

### NdefRecord.make_hash

The make_hash method returns a hash from an Ndef record, from which you can then extract data with the NdefRecord get methods.

#### Returns

A hash of the following format:

 * 'id' - byte[]
 * 'tnf' - int
 * 'type' - byte[]
 * 'payload' - byte[]
 * 'payload_as_string' - string

#### Parameters

None.

#### Example

This example steps through a records array, makes a hash of each record, and puts the hash into an array.

	:::ruby
	r_a = []
    i = 0
	while i < records.size do
      r_a << records[i].make_hash 
      i = i+1
    end

### NdefRecord.convert_Tnf_to_string(int)

Converts the int value of tnf from an Ndef record hash to a string.

#### Returns

A string. Text description of the Type Name Format (TNF).

#### Parameters

int: The tnf from a NdefRecord hash.

#### Example

	:::ruby
	puts 'tnf = '+Rho::NdefRecord.convert_Tnf_to_string(record['tnf'])

### NdefRecord.convert_RTD_to_string(byte[])

Converts the byte[] value of rtd from an Ndef record hash to a string.

#### Returns

A string. Text description of the rtd (type part of the NdefRecord hash).

#### Parameters

byte[]: The rtd (type) from an NdefRecord hash.

#### Example

	:::ruby
	puts 'type = '+Rho::NdefRecord.convert_RTD_to_string(record['type'])

## NdefMessage Class API

Use the NdefMesage class to convert an NdefMessage into a format from which you can extract data.

### NdefMessage.get_byte_array

Converts an NdefMessage into a raw byte array.

#### Returns

byte[] - byte array containing the Ndef message.

#### Parameters

None.

### NdefMessage.get_records

Converts an NdefMessage into an NdefRecord array containing the records in the Ndef Message.

#### Returns

NdefRecord[] - NdefRecord array containing the records in an NdefMessage.

#### Parameters

None.

#### Example

	:::ruby
	ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
    if ndef != nil
      ndef.connect
      msg = ndef.read_NdefMessage
      records = msg.get_records
      #...
    end

## NFCTagTechnology Class API

Use the NFCTagTechnology to connect to NFC tags and to determine their type.

### NFCTagTechnology Properties

The NFCTagTechnology class has several properties to determine the type of the NFC tag.

 * ISODEP = 'IsoDep'
 * MIFARE_CLASSIC = 'MifareClassic'
 * MIFARE_ULTRALIGHT = 'MifareUltralight'
 * NDEF = 'Ndef'
 * NDEF_FORMATABLE = 'NdefFormatable'
 * NFCA = 'NfcA'
 * NFCB = 'NfcB'
 * NFCF = 'NfcF'
 * NFCV = 'NfcV'

### NFCTagTechnology.get_name

This method gets the name of an NFC tag.

#### Returns

String - the name of the NFC tag.

#### Parameters

None.

### NFCTagTechnology.connect

This method connects to an NFC tag.

#### Returns

None.

#### Parameters

None.

#### Example

	:::ruby
	tag = Rho::NFCManager.get_current_Tag
	if tag != nil
	  ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
	  if ndef != nil
	    puts '  Ndef is supported !'
	    ndef.connect
	    connected = ndef.is_connected
	    puts '  Ndef.isConnected() = '+connected.to_s
	    #...
	  end
	  #...
	end

### NFCTagTechnology.close

Closes a connection with an NFC tag.

#### Returns

None.

#### Parameters

None.

#### Example

	:::ruby
	ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
    if ndef != nil
      ndef.connect
      msg = ndef.read_NdefMessage
      records = msg.get_records
      r_a = []
      records.each do |record|
        r_a << record.make_hash
      end
      msg_hash = { 'records' => r_a }
      result = "Tag Result: " + msg_hash['records'][0]['payload_as_string'] if msg_hash['records'].size > 0
      
      ndef.close

### NFCTagTechnology.is_connected

This method returns true if the application is connected with an NFC tag, false otherwise. 

#### Returns

True or false.

#### Parameters

None.

#### Example

	:::ruby
	tag = Rho::NFCManager.get_current_Tag
    if tag != nil   
      ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
      if ndef != nil
        ndef.connect
        connected = ndef.is_connected
        puts '  Ndef.isConnected() = '+connected.to_s	

## NFCTagTechnology_NfcA Class API
	    
Subset of NFCTagTechnology class.

### NFCTagTechnology_NfcA.get_Atqa

Gets a byte array containing Atqa.

#### Returns

byte[] - Atqa.

#### Parameters

None.

### NFCTagTechnology_NfcA.get_Sak

Gets a int containing Sak.

#### Returns

int - Sak.

#### Parameters

None.

### NFCTagTechnology_NfcA.transceive(data)

Sends data (a byte array) to a tag and receives result in a byte array.

#### Returns

byte[] - data received from the tag.

#### Parameters

data - byte[] sent to the tag.

## NFCTagTechnology_Ndef Class API

Subset of NFCTagTechnology class.
	        
MIFARE_CLASSIC = 'com.nxp.ndef.mifareclassic'
NFC_FORUM_TYPE_1 = 'org.nfcforum.ndef.type1'
NFC_FORUM_TYPE_2 = 'org.nfcforum.ndef.type2'
NFC_FORUM_TYPE_3 = 'org.nfcforum.ndef.type3'
NFC_FORUM_TYPE_4 = 'org.nfcforum.ndef.type4'

### NFCTagTechnology_Ndef.get_max_size

Gets the maximum size of the Ndef tag.

#### Returns

int - Maximum size of the Ndef tag.

#### Parameters

None.

#### Example

	:::ruby
	tag = Rho::NFCManager.get_current_Tag
	if tag != nil
      ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
      if ndef != nil
        puts '  Ndef is supported !'
        ndef.connect
	    puts '       max_size = '+ndef.get_max_size.to_s
	    #...
	  end
	  #...
	end

### NFCTagTechnology_Ndef.is_writable

Returns true if the Ndef tag is writeable, false otherwise.

#### Returns

bool - True if the tag is writeable, false otherwise.

#### Parameters

None.

#### Example

	:::ruby
	tag = Rho::NFCManager.get_current_Tag
	if tag != nil
      ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
      if ndef != nil
        puts '  Ndef is supported !'
        ndef.connect
	    puts '       is_writable = '+ndef.is_writable.to_s
	    #...
	  end
	  #...
	end

### NFCTagTechnology_Ndef.can_make_read_only

Returns true if the Ndef tag can be made read only, false otherwise.

#### Returns

bool - True if the tag can be made read only, false otherwise.

#### Parameters

None.

#### Example

	:::ruby
	tag = Rho::NFCManager.get_current_Tag
	if tag != nil
      ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
      if ndef != nil
        puts '  Ndef is supported !'
        ndef.connect
	    puts '       can_make_read_only = '+ndef.can_make_read_only.to_s
	    #...
	  end
	  #...
	end

### NFCTagTechnology_Ndef.make_read_only

Returns true if the Ndef tag is made read only, false otherwise.

#### Returns

bool - True if the tag is made read only, false otherwise.

#### Parameters

None.
	    
### NFCTagTechnology_Ndef.get_type

Returns a string containing the type of the Ndef tag.

#### Returns

string - The type of the Ndef tag.

#### Parameters

None.

#### Example

	:::ruby
	tag = Rho::NFCManager.get_current_Tag
	if tag != nil
      ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
      if ndef != nil
        puts '  Ndef is supported !'
        ndef.connect
	    type = ndef.get_type
        puts '       type = '+type
	    #...
	  end
	  #...
	end
	    
### NFCTagTechnology_Ndef.read_NdefMessage

Returns an NdefMessage read from an Ndef tag.

#### Returns

NdefMessage - The message contained in the Ndef tag.

#### Parameters

None.

#### Example

	:::ruby
	ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
    if ndef != nil
      ndef.connect
      msg = ndef.read_NdefMessage
      #... process the message
    end

### NFCTagTechnology_Ndef.write_NdefMessage(msg)

Returns an NdefMessage read from an Ndef tag.

#### Returns

None.

#### Parameters

msg - an NdefMessage written to an Ndef tag.

#### Example

	:::ruby
	ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
    if ndef != nil
      ndef.connect
      #... create the message to write
      ndef.write_NdefMessage(msg)
    end

## NFCTagTechnology_MifareClassic Class API

Subset of NFCTagTechnology.

### Constants

	:::term
	KEY_DEFAULT = [0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF]
	KEY_MIFARE_APPLICATION_DIRECTORY = [0xA0, 0xA1, 0xA2, 0xA3, 0xA4, 0xA5]
	KEY_NFC_FORUM =[0xD3, 0xF7, 0xD3, 0xF7, 0xD3, 0xF7]    
	
### Types

	:::term
	TYPE_CLASSIC = 0
	TYPE_PLUS = 1
	TYPE_PRO = 2
	TYPE_UNKNOWN = -1

### NFCTagTechnology_MifareClassic.get_type

Returns the type of a MifareClassic tag.

#### Returns

int - the tag type.

#### Parameters

None.

### NFCTagTechnology_MifareClassic.convert_type_to_string(type)

Returns the named type of a MifareClassic tag.

#### Returns

type - A string containing the tag type.

#### Parameters

None.

### NFCTagTechnology_MifareClassic.write_block(index, block)

Writes a block to a MifareClassic tag.

#### Returns

None.

#### Parameters

index - integer, the index to where in the tag sector the block will be written.
block - a 16 byte array written to the tag.

### NFCTagTechnology_MifareClassic.read_block(index)

Reads a block from a MifareClassic tag.

#### Returns

A 16 byte array.

#### Parameters

index - integer, the index to where in the tag sector the block is read from.

### NFCTagTechnology_MifareClassic.get_size

Return the size in bytes of a MifareClassic tag.

#### Returns

The size in bytes of a MifareClassic tag.

#### Parameters

None.

### NFCTagTechnology_MifareClassic.get_block_count

Return the number of blocks in a MifareClassic tag.

#### Returns

The number of blocks in a MifareClassic tag.

#### Parameters

None.

### NFCTagTechnology_MifareClassic.get_sector_count

Return the sector count in a MifareClassic tag.

#### Returns

The sector count in a MifareClassic tag.

#### Parameters

None.

### NFCTagTechnology_MifareClassic.get_blocks_in_sector_count(index)

Returns the number of blocks in a sector in a MifareClassic tag.

#### Returns

The number of blocks in the sector.

#### Parameters

index - the index to a sector.

### NFCTagTechnology_MifareClassic.sector_to_block(index)

Returns the index of the first block in a sector in a MifareClassic tag.

#### Returns

The index of the first block in a sector.

#### Parameters

index - the index to the current sector.
	
### NFCTagTechnology_MifareClassic.authenticate_sector_with_key_A(index, key)

Authenticates a sector with a key. Returns true if the authenticate was passed.

#### Returns

True if the authenticate was passed.

#### Parameters

index - the index to the current sector.
key - a 6 byte array containing the key.

### NFCTagTechnology_MifareClassic.authenticate_sector_with_key_B(index, key)

Authenticates a sector with a key. Returns true if the authenticate was passed.

#### Returns

True if the authenticate was passed.

#### Parameters

index - the index to the current sector.
key - a 6 byte array containing the key.

### NFCTagTechnology_MifareClassic.transceive(data)

Sends data (a byte array) to a tag and receives result in a byte array.

#### Returns

byte[] - data received from the tag.

#### Parameters

data - byte[] sent to the tag.

## NFCTagTechnology_MifareUltralight Class API

Subclass of NFCTagTechnology.
	
	   TYPE_ULTRALIGHT = 1
	   TYPE_ULTRALIGHT_C = 2
	   TYPE_UNKNOWN = -1

### NFCTagTechnology_MifareUltralight.get_type

Returns the type of a MifareUltralight tag.

#### Returns

int - the tag type.

#### Parameters

None.

### NFCTagTechnology_MifareUltralight.write_page(index, block)

Write a page to a MifareUltralight tag.

#### Returns

None.

#### Parameters

index - integer
block - 4 byte array

### NFCTagTechnology_MifareUltralight.read_page(index)

Reads a page from a MifareUltralight tag.

#### Returns

16 byte array.

#### Parameters

index - integer

### NFCTagTechnology_MifareUltralight.transceive(data)

Sends data (a byte array) to a tag and receives result in a byte array.

#### Returns

byte[] - data received from the tag.

#### Parameters

data - byte[] sent to the tag.

## NFCTagTechnology_IsoDep Class API

Subclass of NFCTagTechnology.

### NFCTagTechnology_IsoDep.get_hi_layer_responce

Returns the hi layer response.

#### Returns

byte[] - hi layer response.

#### Parameters

None.

### NFCTagTechnology_IsoDep.get_historical_bytes

Returns the historical bytes.

#### Returns

byte[] - historical bytes.

#### Parameters

None.

### NFCTagTechnology_IsoDep.set_timeout(timeout)

Sets a timeout.

#### Returns

None.

#### Parameters

int - the timeout.

### NFCTagTechnology_IsoDep.transceive(data)

Sends data (a byte array) to a tag and receives result in a byte array.

#### Returns

byte[] - data received from the tag.

#### Parameters

data - byte[] sent to the tag.

## NFCTagTechnology_NdefFormatable Class API

Subclass of NFCTagTechnology.

### NFCTagTechnology_NdefFormatable.format(msg)

Formats a NdefMessage to NdefFormatable format.
QUESTION: Needs a correct definition.

#### Returns

None.

#### Parameters

msg - NdefMessage.

### NFCTagTechnology_NdefFormatable.format_read_only(msg)

Formats a NdefMessage to NdefFormatable read-only format.
QUESTION: Needs a correct definition.

#### Returns

None.

#### Parameters

msg - NdefMessage.	
	
## NFCTagTechnology_NfcB Class API

Subclass of NFCTagTechnology.

### NFCTagTechnology_NfcB.get_application_data

Gets application data from an NfcB tag.

#### Returns

byte[] - the application data.

#### Parameters

None.

### NFCTagTechnology_NfcB.get_protocol_info

Gets protocol information from an NfcB tag.

#### Returns

byte[] - the protocol information.

#### Parameters

None.

### NFCTagTechnology_NfcB.transceive(data)

Sends data (a byte array) to a tag and receives result in a byte array.

#### Returns

byte[] - data received from the tag.

#### Parameters

data - byte[] sent to the tag.

## NFCTagTechnology_NfcF Class API

Subset of NFCTagTechnology.

### NFCTagTechnology_NfcF.get_manufacturer

#### Returns

byte[] - the manufacturer.

#### Parameters

None.

### NFCTagTechnology_NfcF.get_system_code

#### Returns

byte[] - the system code.

#### Parameters

None.

### NFCTagTechnology_NfcF.transceive(data)

Sends data (a byte array) to a tag and receives result in a byte array.

#### Returns

byte[] - data received from the tag.

#### Parameters

data - byte[] sent to the tag.

## NFCTagTechnology_NfcV Class API

Subset of NFCTagTechnology.

### NFCTagTechnology_NfcV.get_dsf_id

#### Returns

int - the dsf ID.

#### Parameters

None.

### NFCTagTechnology_NfcV.get_responce_flags

#### Returns

int - the response flags.

#### Parameters

None.

### NFCTagTechnology_NfcV.transceive(data)

Sends data (a byte array) to a tag and receives result in a byte array.

#### Returns

byte[] - data received from the tag.

#### Parameters

data - byte[] sent to the tag.

## NFCTag Class API

Use the NFCTag class to get the NFC tag in certain formats, such as Ndef.

### NFCTag.get_tech(tech_name)

This method returns an object with the implementation of the requested NFC tech based on the NFCTagTechnology class. 

#### Returns

An object with the implementation of the requested NFC tech based on the NFCTagTechnology class. Refer to the NFCTagTechnology class for the types of NFC tech you can request.

#### Parameters

tech_name - Tech name based on the NFCTagTechnology class.

#### Example

	:::ruby
	tag = Rho::NFCManager.get_current_Tag
	if tag != nil
	  ndef = tag.get_tech(Rho::NFCTagTechnology::NDEF)
	  if ndef != nil
	    puts '  Ndef is supported !'
	    ndef.connect
	    connected = ndef.is_connected
	    puts '  Ndef.isConnected() = '+connected.to_s
	    #... read from or write to the tag
	  end

### NFCTag.get_tech_list

This method returns a string array containing the NFC tag. 

#### Returns

A string array containing the NFC tag.

#### Parameters

None.

### NFCTag.get_ID

This method returns a byte array containing the NFC tag ID. 

#### Returns

byte[] - A byte array containing the NFC tag ID.

#### Parameters

None.

## NFCManager Class API

Use NFCManager to manage NFC messages and records that your NFC application sends and receives.

Methods:

 * is_supported
 * enable
 * is_enabled
 * disable
 * set_nfc_callback(url)
 * set_nfc_tech_callback(url)
 * get_current_Tag
 * perform_open_application_event
 * p2p_enable_foreground_nde_push
 * p2p_disable_foreground_nde_push
 * make_NdefRecord_from_byte_array(array)
 * make_NdefRecord_from_hash(hash)
 * make_NdefMessage_from_array_of_NdefRecord(array)
 * make_string_from_payload(payload, tnf, type)
 * make_payload_with_absolute_uri(uri_string)
 * make_payload_with_well_known_uri(prefix_code, uri_string)
 * make_payload_with_well_known_text(language, text)

### Callback Tag Message Storage

The NFC callback stores the NFC tag messages in a hash array: 

@params['messages'] - array of NFC tag messages. Each message is a hash.

The messages can be picked up in 'raw_message', an array of bytes containing the raw message. The messages can also be picked up in 'records', an array of records where each record is a hash. The records use the NFC Data Exchange Format. Each record has the following hash items.

 * 'raw_record' - Array of bytes. The raw record.
 * 'id' - Array of bytes. The tag ID.
 * 'payload' - Array of bytes.
 * 'tnf' - Int. The Type Name Format. 
 * 'type' - array of bytes
 * 'payload_as_string' - String. The message payload in a string (support special formats for URI, TEXT). 
 * 'subrecords' - message hash (only for SMART_POSTER type)

### NFCManager.is_supported

This method returns true if the mobile device supports NFC, false otherwise. 

#### Returns

True or false.

#### Parameters

None.

#### Example

	:::ruby
	def index
	  $status = Rho::NFCManager.is_enabled.to_s
	  # See if NFC supported and save that info in a string
	  $supported = Rho::NFCManager.is_supported.to_s
	  $log = ''
	  Rho::NFCManager.set_nfc_callback(url_for(:action => :nfc_callback))
	  Rho::NFCManager.set_nfc_tech_callback(url_for(:action => :nfc_tech_callback))
	
	  puts 'NfcController.index'
	  render
	end

### NFCManager.enable

The enable method enables NFC event processing on your mobile device. Your nfc and nfc_tech callback methods are executed only if Rhodes NFC is enabled. On Android, when Rhodes NFC is enabled and the application activity is in the foreground, the activity gets high priority for NFC events. Android will not show additional UI for the select Activity for Tag processing; the Rhodes application will process the tag.

#### Returns

None.

#### Parameters

None.

#### Example

	:::ruby
	# Enable NFC functionality and set up callbacks.
	def on_activate_app
	  Rho::NFCManager.enable
	  Rho::NFCManager.set_nfc_callback("/app/Nfc/nfc_callback")
	  Rho::NFCManager.set_nfc_tech_callback("/app/Nfc/nfc_tech_callback")
	  Rho::NFCManager.perform_open_application_event
	end

### NFCManager.disable

This method disables your application from receiving NFC events. Your application will not be able to receive NFC tags.

#### Returns

None.

#### Parameters

None.

#### Example

	:::ruby
	# Disable the NFC functionality and set a status string accordingly
	def do_disable
	  Rho::NFCManager.disable
	  $status = Rho::NFCManager.is_disabled.to_s
	  set_status($status)    
	end

### NFCManager.is_enabled

This method returns true if the mobile device has been enabled for NFC, false otherwise.

#### Returns

True or false.

#### Parameters

None.

#### Example

	:::ruby
	def do_enable
	  Rho::NFCManager.enable
	  $status = Rho::NFCManager.is_enabled.to_s
	  set_status($status)    
	end

### NFCManager.set_nfc_callback(string), NFCManager.set_nfc_tech_callback(string)

The set_nfc_callback method tells your application what callback to perform when it receives an NFC tag and your application is in the foreground. set_nfc_callback executes when the Android events ACTION_NDEF_DISCOVERED or ACTION_TAG_DISCOVERED are processed.

The set_nfc_tech_callback method tells your application what callback to perform when it receives an NFC tag and your application is in the background. The set_nfc_tech_callback method executes when the Android event ACTION_TECH_DISCOVERED is processed.

#### Returns

None.

### Parameters

string - url. The path to the method in the NFC controller that is executed on NFC callback.

### Example:

	:::ruby
	def on_activate_app
      Rho::NFCManager.enable
      
      # Perform the nfc_callback or nfc_tech_callback method in 
      #   nfc_controller.rb on nfc callback
      Rho::NFCManager.set_nfc_callback("/app/Nfc/nfc_callback")
      Rho::NFCManager.set_nfc_tech_callback("/app/Nfc/nfc_tech_callback")
    
      Rho::NFCManager.perform_open_application_event
	end

### NFCManager.get_current_Tag

This method returns the current NFCTag that the mobile device has just read, or returns nil if no tag has been discovered. 

#### Returns

NFCTag. An NFC tag.

#### Parameters

None.

#### Example

	:::ruby
	def nfc_tech_callback
	  @msg = 'Tech received! Reading tag...'
	  add_to_log(@msg)
	  tag = Rho::NFCManager.get_current_Tag
	  if tag != nil
	    @msg = test_ndef_read(tag)
	  else
	    @msg = "Tag is nil!"
	  end
	  add_to_log(@msg)
	end

### NFCManager.perform_open_application_event

Call the perform_open_application_event method to have your application listen for NFC tags when it is in the background.  When your application is in the background or it has not started, then the NFC event was saved, and the application open/start process is executed. To process that NFC event, your application needs to call perform_open_application_event.

#### Returns

None.

#### Parameters

None. 

#### Example:

	:::ruby
	def on_activate_app
      Rho::NFCManager.enable
      
      # Perform the nfc_callback or nfc_tech_callback method in 
      #   nfc_controller.rb on nfc callback
      Rho::NFCManager.set_nfc_callback("/app/Nfc/nfc_callback")
      Rho::NFCManager.set_nfc_tech_callback("/app/Nfc/nfc_tech_callback")
    
      Rho::NFCManager.perform_open_application_event
	end

### NFCManager.p2p_enable_foreground_nde_push(NDefMessage)

The p2p_enable_foreground_nde_push method causes your mobile device to push an NFC message (NdefMessage) for any NFC-enabled device to receive.

#### Returns

None.

#### Parameters

NdefMessage - The NFC message that is pushed.

#### Example

	:::ruby
	def do_p2p_enable
	  # prepare NdefMessage for send to another device
	  payload = Rho::NFCManager.make_payload_with_well_known_uri(0, 'http://www.rhomobile.com')
	  hash = { 'id' => [0], 'type' => Rho::NdefRecord::RTD_URI, 'tnf' => Rho::NdefRecord::TNF_WELL_KNOWN, 'payload' => payload}
	  record = Rho::NFCManager.make_NdefRecord_from_hash(hash)
	  records = [record]
	  msg = Rho::NFCManager.make_NdefMessage_from_array_of_NdefRecord(records)
	  # start push message
	  Rho::NFCManager.p2p_enable_foreground_nde_push(msg)
	  add_to_log('Enable PUSH P2P')
	  set_log($log)
	end

### NFCManager.p2p_disable_foreground_nde_push

The p2p_disable_foreground_nde_push method causes your mobile device to stop pushing NFC messages to any other NFC-enabled devices that can receive them.

#### Returns

None.

#### Parameters

 None.

#### Example

	:::ruby
	def do_p2p_disable
	  # stop push message
	  Rho::NFCManager.p2p_disable_foreground_nde_push
	  add_to_log('Disable PUSH P2P')
	  set_log($log)
	end

### NFCManager.make_NdefRecord_from_byte_array(array)

The make_NdefRecord_from_byte_array method creates a record for an NFC tag message (NdefRecord) from a byte array.

#### Returns

NdefRecord - An Ndef record.

#### Parameters

array - a byte array containing a raw NFC record.

### NFCManager.make_NdefRecord_from_hash(hash)

The make_NdefRecord_from_hash method creates a record for an NFC tag message (NdefRecord) from a hash.

#### Returns

NdefRecord - An Ndef record.

#### Parameters

@params['Tag_event'] - 'discovered'

@params['messages'] - array of messages. Each message is a hash.
 * 'id' - Array of bytes. The tag ID.
 * 'tnf' - Int. The Type Name Format.
 * 'type' - Array of bytes. The payload type.
 * 'payload' - Array of bytes. The message payload.

#### Example

	:::ruby
	def do_p2p_enable
	  # prepare an NdefMessage for sending to another device
	  payload = Rho::NFCManager.make_payload_with_well_known_uri(0, 'http://www.rhomobile.com')
	  
	  # Create a hash -- id, tnf, type, payload -- for an NFC record
	  hash = { 'id' => [0], 'type' => Rho::NdefRecord::RTD_URI, 'tnf' => Rho::NdefRecord::TNF_WELL_KNOWN, 'payload' => payload}
	  
	  # Create the NFC record with that hash
	  record = Rho::NFCManager.make_NdefRecord_from_hash(hash)
	  records = [record]
	  
	  msg = Rho::NFCManager.make_NdefMessage_from_array_of_NdefRecord(records)
	  
	  # start push message
	  Rho::NFCManager.p2p_enable_foreground_nde_push(msg)
	end


### NFCManager.make_NdefMessage_from_byte_array(array)

The make_NdefMessage_from_byte_array method creates an NFC tag message (NdefMessage) from a byte array.

#### Returns

A NFC message (NdefMessage).

#### Parameters

array - a byte array containing a raw NFC message.

### NFCManager.make_NdefMessage_from_array_of_NdefRecord(array)

The make_NdefMessage_from_byte_array method creates an NFC tag message (NdefMessage) from an array of records (NdefRecord, such as what you get from make_NdefRecord_from_hash).

#### Returns

An NFC message (NdefMessage).

#### Parameters

array - an array of records (NdefRecord).

#### Example

	:::ruby
	def do_p2p_enable
	  # prepare an NdefMessage for sending to another device
	  payload = Rho::NFCManager.make_payload_with_well_known_uri(0, 'http://www.rhomobile.com')
	  # Create a hash -- id, tnf, type, payload -- for an NFC record
	  hash = { 'id' => [0], 'type' => Rho::NdefRecord::RTD_URI, 'tnf' => Rho::NdefRecord::TNF_WELL_KNOWN, 'payload' => payload}
	  # Create the NFC record with that hash
	  record = Rho::NFCManager.make_NdefRecord_from_hash(hash)
	  records = [record]
	  # Create the NdefMessage from the NdefRecord (just one record in array)
	  msg = Rho::NFCManager.make_NdefMessage_from_array_of_NdefRecord(records)
	  # start push message
	  Rho::NFCManager.p2p_enable_foreground_nde_push(msg)
	  add_to_log('Enable PUSH P2P')
	  set_log($log)
	end

### NFCManager.make_string_from_payload(payload, tnf, type)

The make_string_from_payload method creates a string from the payload of an NFC tag message record (NdefRecord).

#### Returns

A string containing the payload of an NFC tag message record.

#### Parameters

 * payload - a byte array containing the payload.
 * tnf - int. The Type Name Format. From NdefRecord.
 * type - Array of bytes. The payload type.	From NdefRecord.

### NFCManager.make_payload_with_absolute_uri(uri_string)

The make_payload_with_absolute_uri method prepares a byte array for an NFC record payload from a string with an absolute URI.

#### Returns

A byte array for an NFC record payload.

#### Parameters

uri_string - a string containing an absolute URI.

#### Example

	:::ruby
	payload = Rho::NFCManager.make_payload_with_absolute_uri('http://www.rhomobile.com')

### NFCManager.make_payload_with_well_known_uri(prefix_code, uri_string)

The make_payload_with_absolute_uri method prepares a byte array for an NFC record payload from a string with an absolute URI.

#### Returns

A byte array for an NFC record payload.

#### Parameters

 * prefix_code - an int containing a prefix code.
 * uri_string - a string containing an absolute URI.

#### Example

	:::ruby
	def do_p2p_enable
	  # prepare an NdefMessage for sending to another device
	  payload = Rho::NFCManager.make_payload_with_well_known_uri(0, 'http://www.rhomobile.com')
	  # Create a hash -- id, tnf, type, payload -- for an NFC record
	  hash = { 'id' => [0], 'type' => Rho::NdefRecord::RTD_URI, 'tnf' => Rho::NdefRecord::TNF_WELL_KNOWN, 'payload' => payload}
	  # Create the NFC record with that hash
	  record = Rho::NFCManager.make_NdefRecord_from_hash(hash)
	  records = [record]
	  # Create the NdefMessage from the NdefRecord (just one record in array)
	  msg = Rho::NFCManager.make_NdefMessage_from_array_of_NdefRecord(records)
	  # start push message
	  Rho::NFCManager.p2p_enable_foreground_nde_push(msg)
	  add_to_log('Enable PUSH P2P')
	  set_log($log)
	end

### NFCManager.make_payload_with_well_known_text(language, text)

The make_payload_with_well_known_text method prepares a byte array for an NFC record payload from a string language code and a string text.

#### Returns

A byte array for an NFC record payload.

#### Parameters

 * language - a string containing a language code.
 * text - a string containing an absolute URI.