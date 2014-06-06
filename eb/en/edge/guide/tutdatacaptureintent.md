<!-- Launchpad Link id: tutdatacaptureintent
    usage <a data-link="profilebarcode">blah blah</a>
    replace id
-->
<div class="tableofcontents"> </div>
## Overview
DataWedge on Android has the ability to output captured data via Intents. This article describes how to use the DataWedge Intent output plug-in and the Data Capture API to receive captured data in your native Android application.

Knowledge of Android programming and familiarity with the Android intent mechanism are assumed. Also assumed is some familiarity with DataWedge and that you have read the DataWedge section in the Integrator Guide for your device.
 
## APPLICATION LAYOUT
For this article we created an Android application with a blank activity using Eclipse, to which we added the following layout.

<pre class="jive_text_macro jive_macro_code" jivemacro="code" ___default_attr="xml" _jivemacro_uid="_1398870592774641">
<p>&lt;?xml version="1.0" encoding="utf-8"?&gt;</p>
<p>&lt;LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"</p>
<p>    android:layout_width="fill_parent"</p>
<p>    android:layout_height="fill_parent"</p>
<p>    android:orientation="vertical" &gt;</p>
<p>    &lt;LinearLayout</p>
<p>        android:layout_width="fill_parent"</p>
<p>        android:layout_height="wrap_content"</p>
<p>        android:orientation="horizontal" &gt;</p>
<p>        &lt;ImageView</p>
<p>            android:id="@+id/logo"</p>
<p>            style="@style/logo"</p>
<p>            android:contentDescription="@string/title" /&gt;</p>
<p>        &lt;LinearLayout</p>
<p>            android:layout_width="fill_parent"</p>
<p>            android:layout_height="wrap_content"</p>
<p>            android:orientation="vertical" &gt;</p>
<p>            &lt;TextView style="@style/title" /&gt;</p>
<p>            &lt;TextView style="@style/copyright" /&gt;</p>
<p>        &lt;/LinearLayout&gt;</p>
<p>    &lt;/LinearLayout&gt;</p>
<p>    &lt;View style="@style/hr" /&gt;</p>
<p>    &lt;TextView style="@style/intro" /&gt;</p>
<p>    &lt;EditText</p>
<p>        android:id="@+id/editbox"</p>
<p>        style="@style/editbox"</p>
<p>        android:inputType="textMultiLine"</p>
<p>        /&gt;</p>
<p> &lt;/LinearLayout&gt;</p>
</pre>

The things to note in the above layout are the ImageView and the EditText widgets.  The ImageView widget will effectively act as a button which can be used to toggle the scanner instead of pressing the trigger button on the device. The EditText widget will be used to display the data that we receive in the intent.
 
## INTENT STRINGS
The intent we will receive from DataWedge will contain a bundle of data which we will be retrieving using the Intent.getStringtExtra() and Intent.getSerializableExtra() methods.  

### Data Items
The following is a list of the data item names that the bundle could contain.

* String SOURCE_TAG = "com.motorolasolutions.emdk.datawedge.source";
* String contains the source of the data i.e. scanner or MSR
* String DATA_STRING_TAG = "com.motorolasolutions.emdk.datawedge.data_string";
    * String contains the output data as a String. In the case of concatenated bar codes, the decode data is concatenated and sent out as a single string. In the case of MSR output, the data from the MSR tracks is concatenated and sent out as a single string.
* String LABEL_TYPE_TAG = "com.motorolasolutions.emdk.datawedge.label_type";
* String contains the label type of the bar code.
* String DECODE_DATA_TAG = "com.motorolasolutions.emdk.datawedge.decode_data";
    * Decode data returned as a list of byte arrays. In most cases there will be one byte array per decode. For bar-code symbologies that support concatenation e.g. Codabar, Code128, MicroPDF, etc., the decoded data is stored in multiple byte arrays (one byte array per bar code). Clients can get data in each byte array by passing an index.

### MSR Intent Names
Let’s list the MSR intent names (in case we want to use these in the future).
The MSR related data added to the intent’s bundle can be retrieved using the Intent.getStringtExtra() and Intent.getSerializableExtra() calls, using the following String tags…

* String MSR_DATA_TAG = "com.motorolasolutions.emdk.datawedge.msr_data";
    * The data from the MSR tracks is concatenated and sent out as a byte array.
* String MSR_TRACK1_TAG = "com.motorolasolutions.emdk.datawedge.msr_track1";
    * MSR track 1 data is returned as a byte array.
* String MSR_TRACK2_TAG = "com.motorolasolutions.emdk.datawedge.msr_track2";
    * MSR track 2 data is returned as a byte array.
* String MSR_TRACK3_TAG = "com.motorolasolutions.emdk.datawedge.msr_track3";
    * MSR track 3 data is returned as a byte array.
* String MSR_TRACK1_STATUS_TAG = "com.motorolasolutions.emdk.datawedge.msr_track1_status";
    * MSR track 1 decode status as an Integer where 0 indicates a successful decode.
* String MSR_TRACK2_STATUS_TAG = "com.motorolasolutions.emdk.datawedge.msr_track2_status";
    * MSR track 2 decode status as an Integer where 0 indicates a successful decode.
* String MSR_TRACK3_STATUS_TAG = "com.motorolasolutions.emdk.datawedge.msr_track3_status";
    * MSR track 3 decode status as an Integer where 0 indicates a successful decode.
* String MSR_TRACK1_ENCRYPTED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track1_encrypted";
    * MSR track 1 encrypted data is returned as a byte array.
* String MSR_TRACK2_ENCRYPTED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track2_encrypted";
    * MSR track 2 encrypted data is returned as a byte array.
* String MSR_TRACK3_ENCRYPTED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track3_encrypted";
    * MSR track 3 encrypted data is returned as a byte array.
* String MSR_TRACK1_HASHED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track1_hashed";
    * MSR track 1 hashed data is returned as a byte array.
* String MSR_TRACK2_HASHED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track2_hashed";
    * MSR track 2 hashed data is returned as a byte array.
* String MSR_TRACK3_HASHED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track3_hashed";
    * MSR track 3 hashed data is returned as a byte array.

### Soft Scan Trigger Intent Names
Here are the API intent names for the soft scan trigger…

* String ACTION_SOFTSCANTRIGGER = "com.motorolasolutions.emdk.datawedge.api.ACTION_SOFTSCANTRIGGER";
    * This is the intent action for the soft scan trigger.
* String EXTRA_PARAM = "com.motorolasolutions.emdk.datawedge.api.EXTRA_PARAMETER";
    * Parameter passed in the intent to specify the action the soft scan trigger should perform.  The following actions are recognized…
* String DWAPI_START_SCANNING = "START_SCANNING";
    * Start scanning.
* String DWAPI_STOP_SCANNING = "STOP_SCANNING";
    * Stop scanning.
* String DWAPI_TOGGLE_SCANNING = "TOGGLE_SCANNING";
    * Toggle scanning.

>In the code that follows we will just be using the SOURCE_TAG, DATA_STRING_TAG and LABEL_TYPE_TAG intent data to display the intent data in the EditText widget.
 
## HANDLING INTENTS
Incoming intents can be handled by overriding the onNewIntent method.

<pre class="jive_text_macro jive_macro_code" jivemacro="code" ___default_attr="java" _jivemacro_uid="_1398870592774641">
<p>@Override </p>
<p>public void onNewIntent(Intent i) {</p>
<p>    handleDecodeData(i);</p>
<p>}</p>
</pre>

Our *handleDecodeData()* method will responsible for getting the data from the intent, formatting it and adding it to the end of the edit box; something like this:

<pre class="jive_text_macro jive_macro_code" jivemacro="code" ___default_attr="java" _jivemacro_uid="_1398870592774641">
<p>private void handleDecodeData(Intent i) {</p>
<p>    // check the intent action is for us</p>
<p>    if ( i.getAction().contentEquals(com.motorolasolutions.emdk.sample.dwdemosample.RECVR) ) {        </p>
<p>        // define a string that will hold our output</p>
<p></p>
<p></p>
<p>        String out = "";</p>
<p>        // get the source of the data</p>
<p>        String source = i.getStringExtra(SOURCE_TAG);</p>
<p>        // save it to use later</p>
<p>        if (source == null) source = "scanner";</p>
<p>        // get the data from the intent</p>
<p>        String data = i.getStringExtra(DATA_STRING_TAG);</p>
<p>        // let's define a variable for the data length</p>
<p>        Integer data_len = 0;</p>
<p>        // and set it to the length of the data</p>
<p>        if (data != null) data_len = data.length();</p>
<p>        // check if the data has come from the barcode scanner</p>
<p>        if (source.equalsIgnoreCase("scanner")) {</p>
<p>            // check if there is anything in the data</p>
<p>            if (data != null &amp;&amp; data.length() &gt; 0) { </p>
<p>              // we have some data, so let's get it's symbology</p>
<p>                String sLabelType = i.getStringExtra(LABEL_TYPE_TAG);</p>
<p>                // check if the string is empty</p>
<p>                if (sLabelType != null &amp;&amp; sLabelType.length() &gt; 0) {</p>
<p>                    // format of the label type string is LABEL-TYPE-SYMBOLOGY </p>
<p>                    // so let's skip the LABEL-TYPE- portion to get just the symbology</p>
<p>                    sLabelType = sLabelType.substring(11);</p>
<p>                 }</p>
<p>                else { </p>
<p>                  // the string was empty so let's set it to "Unknown"</p>
<p>                    sLabelType = "Unknown";</p>
<p>                } </p>
<p>              // let's construct the beginning of our output string</p>
<p>                out = "Source: Scanner, " + "Symbology: " + sLabelType + ", Length: " + data_len.toString() + ", Data: ...\r\n";</p>
<p>            }</p>
<p>        } </p>
<p>        // check if the data has come from the MSR</p>
<p>        if (source.equalsIgnoreCase("msr")) {</p>
<p>            // construct the beginning of our output string </p>
<p>          out = "Source: MSR, Length: " + data_len.toString() + ", Data: ...\r\n";</p>
<p>        }</p>
<p></p>
<p></p>
<p>        // let's get our edit box view</p>
<p>        EditText et = (EditText)findViewById(R.id.editbox);</p>
<p>        // and get it's text into an editable string </p>
<p>        Editable txt = et.getText();</p>
<p>        // now because we want format our output </p>
<p>      // we need to put the edit box text into a spannable string builder</p>
<p>        SpannableStringBuilder stringbuilder = new SpannableStringBuilder(txt);</p>
<p>        // add the output string we constructed earlier</p>
<p>        stringbuilder.append(out);</p>
<p>        // now let's highlight our output string in bold type </p>
<p>      stringbuilder.setSpan(new StyleSpan(Typeface.BOLD), txt.length(), stringbuilder.length(), SpannableString.SPAN_EXCLUSIVE_EXCLUSIVE); </p>
<p></p>
<p></p>
<p>      // then add the barcode or msr data, plus a new line, and add it to the string builder </p>
<p>      stringbuilder.append(data + "\r\n"); </p>
<p>      // now let's update the text in the edit box </p>
<p>      et.setText(stringbuilder); </p>
<p>        // we want the text cursor to be at the end of the edit box</p>
<p>        // so let's get the edit box text again</p>
<p>        txt = et.getText();</p>
<p>        // and set the cursor position at the end of the text</p>
<p>        et.setSelection(txt.length());</p>
<p>        // and we are done! </p>
<p>  } </p>
<p>}</p>
</pre>


## TOGGLING THE SCAN TRIGGER
Our activity layout has an ImageView which we will use as a button to toggle the scan trigger.  This is done by using the Data Capture API.  The following code toggles the scan trigger each time the image is tapped.

<pre class="jive_text_macro jive_macro_code" jivemacro="code" ___default_attr="java" _jivemacro_uid="_1398870592774641">
<p>ImageView img = (ImageView) findViewById(R.id.dwdemo_logo);</p>
<p>img.setOnClickListener(new OnClickListener() {</p>
<p>    @Override</p>
<p>    public void onClick(View v) {</p>
<p>        Intent i = new Intent();</p>
<p>        i.setAction(ACTION_SOFTSCANTRIGGER);</p>
<p>        i.putExtra(EXTRA_PARAM, DWAPI_TOGGLE_SCANNING);</p>
<p>        DWDemoActivity.this.sendBroadcast(i);</p>
<p>        Toast.makeText(v.getContext(), "Soft scan trigger toggled.", Toast.LENGTH_SHORT).show();</p>
<p>    }</p>
<p>});</p>
</pre>


## PUTTING ALL THE CODE TOGETHER
Let’s put all that code together so that we can see what our final activity class should look like.

<pre class="jive_text_macro jive_macro_code" jivemacro="code" ___default_attr="java" _jivemacro_uid="_1398870592774641">
<p>package com.motorolasolutions.emdk.sample.dwdemosample;</p>
<p>import android.os.Bundle;</p>
<p>import android.app.Activity;</p>
<p>import android.content.Intent;</p>
<p>import android.graphics.Typeface;</p>
<p>import android.view.View;</p>
<p>import android.view.View.OnClickListener;</p>
<p>import android.widget.EditText;</p>
<p>import android.widget.ImageView;</p>
<p>import android.widget.Toast;</p>
<p>import android.text.Editable;</p>
<p>import android.text.SpannableString;</p>
<p>import android.text.SpannableStringBuilder;</p>
<p>import android.text.style.StyleSpan;</p>
<p>public class MainActivity extends Activity {</p>
<p>    // Tag used for logging errors</p>
<p>    private static final String TAG = MainActivity.class.getSimpleName();</p>
<p>    // Let's define some intent strings</p>
<p>    // This intent string contains the source of the data as a string</p>
<p>    private static final String SOURCE_TAG = "com.motorolasolutions.emdk.datawedge.source";</p>
<p>    // This intent string contains the barcode symbology as a string</p>
<p>    private static final String LABEL_TYPE_TAG = "com.motorolasolutions.emdk.datawedge.label_type";</p>
<p>    // This intent string contains the barcode data as a byte array list</p>
<p>    private static final String DECODE_DATA_TAG = "com.motorolasolutions.emdk.datawedge.decode_data";</p>
<p>    // This intent string contains the captured data as a string</p>
<p>    // (in the case of MSR this data string contains a concatenation of the track data)</p>
<p>    private static final String DATA_STRING_TAG = "com.motorolasolutions.emdk.datawedge.data_string";</p>
<p>    // Let's define the MSR intent strings (in case we want to use these in the future)</p>
<p>    private static final String MSR_DATA_TAG = "com.motorolasolutions.emdk.datawedge.msr_data";</p>
<p>    private static final String MSR_TRACK1_TAG = "com.motorolasolutions.emdk.datawedge.msr_track1";</p>
<p>    private static final String MSR_TRACK2_TAG = "com.motorolasolutions.emdk.datawedge.msr_track2";</p>
<p>    private static final String MSR_TRACK3_TAG = "com.motorolasolutions.emdk.datawedge.msr_track3";</p>
<p>    private static final String MSR_TRACK1_STATUS_TAG = "com.motorolasolutions.emdk.datawedge.msr_track1_status";</p>
<p>    private static final String MSR_TRACK2_STATUS_TAG = "com.motorolasolutions.emdk.datawedge.msr_track2_status";</p>
<p>    private static final String MSR_TRACK3_STATUS_TAG = "com.motorolasolutions.emdk.datawedge.msr_track3_status";</p>
<p>    private static final String MSR_TRACK1_ENCRYPTED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track1_encrypted";</p>
<p>    private static final String MSR_TRACK2_ENCRYPTED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track2_encrypted";</p>
<p>    private static final String MSR_TRACK3_ENCRYPTED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track3_encrypted";</p>
<p>    private static final String MSR_TRACK1_HASHED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track1_hashed";</p>
<p>    private static final String MSR_TRACK2_HASHED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track2_hashed";</p>
<p>    private static final String MSR_TRACK3_HASHED_TAG = "com.motorolasolutions.emdk.datawedge.msr_track3_hashed";</p>
<p>    // Let's define the API intent strings for the soft scan trigger    private static final String ACTION_SOFTSCANTRIGGER = "com.motorolasolutions.emdk.datawedge.api.ACTION_SOFTSCANTRIGGER";</p>
<p>    private static final String EXTRA_PARAM = "com.motorolasolutions.emdk.datawedge.api.EXTRA_PARAMETER";</p>
<p>    private static final String DWAPI_START_SCANNING = "START_SCANNING";</p>
<p>    private static final String DWAPI_STOP_SCANNING = "STOP_SCANNING";</p>
<p>    private static final String DWAPI_TOGGLE_SCANNING = "TOGGLE_SCANNING";</p>
<p>    private static String ourIntentAction = "com.motorolasolutions.emdk.sample.dwdemosample.RECVR";</p>
<p></p>
<p></p>
<p>    @Override</p>
<p>    public void onCreate(Bundle savedInstanceState) {</p>
<p>        super.onCreate(savedInstanceState);</p>
<p>        setContentView(R.layout.activity_main);</p>
<p>        // Let's set the cursor at the end of any text in the editable text field        EditText et = (EditText)findViewById(R.id.editbox);</p>
<p>        Editable txt = et.getText();</p>
<p>        et.setSelection(txt.length());</p>
<p></p>
<p></p>
<p>        // Since we will be using the image as a soft scan trigger toggle button        // let's handle the image on onClick event</p>
<p>        ImageView img = (ImageView) findViewById(R.id.logo);</p>
<p>        img.setOnClickListener(new OnClickListener() {</p>
<p>            @Override</p>
<p>            public void onClick(View v) {</p>
<p>                // the image has been tapped so shoot off the intent to DataWedge                // to toggle the soft scan trigger</p>
<p>                // Create a new intent</p>
<p>                Intent i = new Intent();</p>
<p>                // set the intent action using soft scan trigger action string declared earlier</p>
<p>                i.setAction(ACTION_SOFTSCANTRIGGER);</p>
<p>                // add a string parameter to tell DW that we want to toggle the soft scan trigger</p>
<p>                i.putExtra(EXTRA_PARAM, DWAPI_TOGGLE_SCANNING);</p>
<p>                // now broadcast the intent</p>
<p>                MainActivity.this.sendBroadcast(i);</p>
<p>                // provide some feedback to the user that we did something                Toast.makeText(v.getContext(), "Soft scan trigger toggled.", Toast.LENGTH_SHORT).show();</p>
<p>            }</p>
<p>        });</p>
<p></p>
<p></p>
<p>        // in case we have been launched by the DataWedge intent plug-in</p>
<p>        // using the StartActivity method let's handle the intent</p>
<p>        Intent i = getIntent();</p>
<p>        handleDecodeData(i);</p>
<p>    }</p>
<p></p>
<p></p>
<p>    // We need to handle any incoming intents, so let override the onNewIntent method</p>
<p>    @Override</p>
<p>    public void onNewIntent(Intent i) {</p>
<p>        handleDecodeData(i);</p>
<p>    }</p>
<p></p>
<p></p>
<p>    // This method is responsible for getting the data from the intent</p>
<p>    // formatting it and adding it to the end of the edit box</p>
<p>    private void handleDecodeData(Intent i) {</p>
<p>        // check the intent action is for us</p>
<p>        if ( i.getAction().contentEquals(ourIntentAction) ) {</p>
<p>            // define a string that will hold our output</p>
<p>            String out = "";</p>
<p>            // get the source of the data</p>
<p>            String source = i.getStringExtra(SOURCE_TAG);</p>
<p>            // save it to use later</p>
<p>            if (source == null) source = "scanner";</p>
<p>            // get the data from the intent</p>
<p>            String data = i.getStringExtra(DATA_STRING_TAG);</p>
<p>            // let's define a variable for the data length</p>
<p></p>
<p></p>
<p>            Integer data_len = 0;</p>
<p>            // and set it to the length of the data</p>
<p>            if (data != null) data_len = data.length();</p>
<p>            // check if the data has come from the barcode scanner</p>
<p>            if (source.equalsIgnoreCase("scanner")) {</p>
<p>                // check if there is anything in the data</p>
<p>                if (data != null &amp;&amp; data.length() &gt; 0) {</p>
<p>                    // we have some data, so let's get it's symbology </p>
<p>                    String sLabelType = i.getStringExtra(LABEL_TYPE_TAG);</p>
<p>                    // check if the string is empty</p>
<p>                    if (sLabelType != null &amp;&amp; sLabelType.length() &gt; 0) {                        // format of the label type string is LABEL-TYPE-SYMBOLOGY</p>
<p>                        // so let's skip the LABEL-TYPE- portion to get just the symbology</p>
<p>                        sLabelType = sLabelType.substring(11);</p>
<p>                    }</p>
<p>                    else {</p>
<p>                        // the string was empty so let's set it to "Unknown"</p>
<p>                        sLabelType = "Unknown";</p>
<p>                    }</p>
<p></p>
<p></p>
<p>                    // let's construct the beginning of our output string</p>
<p>                    out = "Source: Scanner, " + "Symbology: " + sLabelType + ", Length: " + data_len.toString() + ", Data: ...\r\n";</p>
<p>                }</p>
<p>            }</p>
<p>            // check if the data has come from the MSR</p>
<p>            if (source.equalsIgnoreCase("msr")) {</p>
<p>                // construct the beginning of our output string</p>
<p>                out = "Source: MSR, Length: " + data_len.toString() + ", Data: ...\r\n";</p>
<p>            }</p>
<p></p>
<p></p>
<p>            // let's get our edit box view</p>
<p>            EditText et = (EditText)findViewById(R.id.editbox);</p>
<p>            // and get it's text into an editable string</p>
<p>            Editable txt = et.getText();</p>
<p>            // now because we want format our output</p>
<p></p>
<p></p>
<p>            // we need to put the edit box text into a spannable string builder</p>
<p>            SpannableStringBuilder stringbuilder = new SpannableStringBuilder(txt);</p>
<p>            // add the output string we constructed earlier</p>
<p>            stringbuilder.append(out);</p>
<p>            // now let's highlight our output string in bold type</p>
<p>            stringbuilder.setSpan(new StyleSpan(Typeface.BOLD), txt.length(), stringbuilder.length(), SpannableString.SPAN_EXCLUSIVE_EXCLUSIVE);</p>
<p>            // then add the barcode or msr data, plus a new line, and add it to the string builder</p>
<p>            stringbuilder.append(data + "\r\n");</p>
<p>            // now let's update the text in the edit box</p>
<p>            et.setText(stringbuilder);</p>
<p>            // we want the text cursor to be at the end of the edit box</p>
<p>            // so let's get the edit box text again</p>
<p>            txt = et.getText();</p>
<p>            // and set the cursor position at the end of the text</p>
<p>            et.setSelection(txt.length());</p>
<p>            // and we are done!</p>
<p>        }</p>
<p>    }</p>
<p> }</p>
</pre>

## DEFINING INTENT FILTERS
Having dealt with the coding of our activity, we now need to inform the system which implicit intents our application can handle.  For that we need to define an intent-filter as follows.

<pre class="jive_text_macro jive_macro_code" jivemacro="code" ___default_attr="xml" _jivemacro_uid="_1398870592774641">
<p>&lt;intent-filter&gt;</p>
<p>    &lt;action android:name="com.motorolasolutions.emdk.sample.dwdemosample.RECVR"/&gt;</p>
<p>    &lt;category android:name="android.intent.category.DEFAULT"/&gt;</p>
<p>&lt;/intent-filter&gt;</p>
</pre>

We will be using the com.motorolasolutions.emdk.sample.dwdemosample.RECVR action and the android.intent.category.DEFAULT category we have just defined above later on when we come to configure our DataWedge profile.

In this article DataWedge is configured to use the startActivity() method to send the intent. The startActivity() method causes a new activity to be launched. However since we do not want another instance of our activity launched each time we receive an intent, we need to specify the launch mode of our activity as single task.
android:launchMode="singleTask"

After adding the above, our AndroidManifest.xml should look something like this…
<pre class="jive_text_macro jive_macro_code" jivemacro="code" ___default_attr="java" _jivemacro_uid="_1398870592774641">
<p>&lt;manifest xmlns:android="http://schemas.android.com/apk/res/android"</p>
<p>    package="com.motorolasolutions.emdk.sample.dwdemosample"</p>
<p>    android:versionCode="1"</p>
<p>    android:versionName="1.0.0" &gt;</p>
<p>    &lt;uses-sdk</p>
<p>        android:minSdkVersion="10"</p>
<p>        android:targetSdkVersion="10" /&gt;</p>
<p>    &lt;application</p>
<p>        android:icon="@drawable/ic_launcher"</p>
<p>        android:label="@string/app_name"</p>
<p>        android:theme="@style/AppTheme" &gt;</p>
<p>        &lt;activity</p>
<p>            android:name=".MainActivity"</p>
<p>            android:label="@string/app_name"</p>
<p>            android:launchMode="singleTask" &gt;</p>
<p>            &lt;intent-filter&gt;</p>
<p>                &lt;action android:name="android.intent.action.MAIN" /&gt;</p>
<p>                &lt;category android:name="android.intent.category.LAUNCHER" /&gt;</p>
<p>            &lt;/intent-filter&gt;</p>
<p>            &lt;intent-filter&gt;</p>
<p>                &lt;action android:name="com.motorolasolutions.emdk.sample.dwdemosample.RECVR"/&gt;</p>
<p>                &lt;category android:name="android.intent.category.DEFAULT"/&gt;</p>
<p>            &lt;/intent-filter&gt;</p>
<p>            &lt;/activity&gt;</p>
<p>    &lt;/application&gt;</p>
<p>&lt;/manifest&gt;</p>
</pre>

## CONFIGURING DATAWEDGE
Now we need to configure DataWedge to send the desired intent to our application.

The following steps will help you get started…

* Launch DataWedge
* Create a new profile and give it a name such as "dwdemosample"
* Edit the profile
* Go into Associated apps, tap the menu button, and add a new app/activity
* For the application select com.motorolasolutions.emdk.sample.dwdemosample
* For the activity select com.motorolasolutions.emdk.sample.dwdemosample.MainActivty
* Go back and disable the keystroke output plug-in
* Enable the intent output plug-in
* For the intent action enter com.motorolasolutions.emdk.sample.dwdemosample.RECVR
* For the intent category enter android.intent.category.DEFAULT
 
## SUMMARY
That’s it.  You should now be able to scan a bar-code and see it appear in the sample application.
In this article, we covered:

* DataWedge intent strings
* Handling intents from Data Capture
* Receiving barcode/MSR data
* Sending intents to Data Capture
* Toggling of the soft scan trigger
* Defining intent filters
* Configuring DataWedge to send intents to our application

## SAMPLE CODE
Download the source for this project in the <a data-link="sampledatacaptureintent">associated sample</a>