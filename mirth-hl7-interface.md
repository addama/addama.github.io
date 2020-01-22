---
title: Mirth HL7 Interface
author: Addama
excerpt: Specification for installing and using the Schema 1.04+ Mirth HL7 channels to transfer HL7 data to an EMR
permalink: /mirth-hl7-interface/
---

# Mirth HL7 Interface

*The primary source for this information is the [Mirth repository](https://github.com/XtractSolutions/Mirth)*

## Brief HL7 Introduction

HL7 ("Health Level 7", don't ask) is a text formatting protocol used by medical applications to transfer structured patient and clinical data between applications, locations, and organizations. HL7 is divided into segments and subsegments. Segments are `\r\n` delimited, while subsegments are `|` delimited, though this is configurable. Each segment is a specific type of information that needs to be sent (e.g. _PV1_, data about the patient's visit to the clinic; _PID_, data about the patient themselves). It is common to refer to the subsegments by 'SEGMENT.SUBSEGMENT_POSITION', so you might hear about _OBX.4_, referring to the fourth subsegment in the _OBX_ segment. 

In our case, the HL7 is generally used as a vehicle for a text-based report that is encoded into the _OBX_ section of the message. Our clients read in the HL7, extract this text report, and display it elsewhere.

The point of this project is to abstract the creation of the HL7 message away from every day maintenance of the Mirth channels. If I've done my job correctly, you shouldn't have to know about HL7 message formatting until/unless a client specifically asks for something new and weird. All you should be concerned with is configuring the data and formatting of the text-based report.

HL7 version 2.8.2

**HL7 Sample**

```text
MSH|^~\&#|SUMMIT|XTRACT|EPIC|UUH|201909180000||ORU^R01|UUID|P|2.8.2|||||USA||ENG||||||
PID|1||85568546^^^^ALLEGRA||XTRACT^XANDER|WILLIS^^^|19700413|M||C|987 S WILLARD AVE^^SALT LAKE CITY^UT^84121^USA^^^SALT LAKE|Salt Lake|(801)445-7997^^PH^^^801^4457997||ENG|S||66062337|000-00-0000|||W||||||||N||
PV1|1|O-102|ALLDTN^^^^^^UNIDN^^^^DEP|3|||13648^VIERA-HUTCHINS^LOIDA^^^^^^^^^^ALG^^^^^^^^MD|13648^VIERA-HUTCHINS^LOIDA^^^^^^^^^^ALG||PBO||||2|||13648^VIERA-HUTCHINS^LOIDA^^^^^^^^^^ALG^^^^^^^^MD||534172667|COMM||||||||||||||||||||||||20180412104704||||||||||
ORC|RE||omr_85568546_201909180000|||||201909180000|201909180000|||||8012132900
OBR|1||omr_85568546_201909180000|ALLERGYINJECTIONS|||201909180000|||||||||13648^VIERA-HUTCHINS^LOIDA^^^^^^^^^^ALG^^^^^^^^MD|8012132900|||||201909180000||MDOC|F
OBX|1|TX|MIX RECEIPT||MIX RECEIPT||||||F|201909180000
OBX|2|TX|MIX RECEIPT||||||||F|201909180000
OBX|3|TX|MIX RECEIPT||Name: ZZ_TEST_XTRACT, XANDER NMI||||||F|201909180000
OBX|4|TX|MIX RECEIPT||MRN: 85568546||||||F|201909180000
OBX|5|TX|MIX RECEIPT||DOB: 1970-04-13||||||F|201909180000
OBX|6|TX|MIX RECEIPT||Note: ||||||F|201909180000
OBX|7|TX|MIX RECEIPT||||||||F|201909180000
OBX|8|TX|MIX RECEIPT||Prescription: Mix (A)||||||F|201909180000
OBX|9|TX|MIX RECEIPT||Prescription Number: 900332||||||F|201909180000
OBX|10|TX|MIX RECEIPT||Note: ||||||F|201909180000
OBX|11|TX|MIX RECEIPT||||||||F|201909180000
OBX|12|TX|MIX RECEIPT||DILUTION SET VIALS||||||F|201909180000
OBX|13|TX|MIX RECEIPT||--------------------------------------------------------------------------------------||||||F|201909180000
OBX|14|TX|MIX RECEIPT||  VIAL NUMBER   DILUTION   COLOR   BARCODE   TIMESTAMP             SIZE   OUT DATE    ||||||F|201909180000
OBX|15|TX|MIX RECEIPT||--------------------------------------------------------------------------------------||||||F|201909180000
OBX|16|TX|MIX RECEIPT||  1             1:1        RED     100988    2018-08-07 00:27:27   5 mL   2001-01-01  ||||||F|201909180000
OBX|17|TX|MIX RECEIPT||  2             1:10       YLW     100989    2018-08-07 00:27:27   5 mL   2001-01-01  ||||||F|201909180000
OBX|18|TX|MIX RECEIPT||  3             1:100      BLUE    100990    2018-08-07 00:27:27   5 mL   2001-01-01  ||||||F|201909180000
OBX|19|TX|MIX RECEIPT||  4             1:1000     GRN     100991    2018-08-07 00:27:27   5 mL   2001-01-01  ||||||F|201909180000
OBX|20|TX|MIX RECEIPT||  5             1:10000    SLVR    100992    2018-08-07 00:27:27   5 mL   2001-01-01  ||||||F|201909180000
OBX|21|TX|MIX RECEIPT||--------------------------------------------------------------------------------------||||||F|201909180000
OBX|22|TX|MIX RECEIPT||||||||F|201909180000
OBX|23|TX|MIX RECEIPT||CONCENTRATE (1:1) VIAL CONSTITUENTS||||||F|201909180000
OBX|24|TX|MIX RECEIPT||--------------------------------------------------------------------------------------------------------------------------||||||F|201909180000
OBX|25|TX|MIX RECEIPT||  EXTRACT                  TYPE   MANUFACTURER   DILUTION   DOSE       UNITS   GLYCERIN %   HSA %   PHENOL %   OUT DATE    ||||||F|201909180000
OBX|26|TX|MIX RECEIPT||--------------------------------------------------------------------------------------------------------------------------||||||F|201909180000
OBX|27|TX|MIX RECEIPT||  Normal Saline with HSA   DIL    TBD            1:20       4.250 mL   W/V     0.00%        0.03%   0.40%      2001-01-01  ||||||F|201909180000
OBX|28|TX|MIX RECEIPT||  Acacia (1:40)            TRS    TBD            1:40       0.500 mL   W/V     50.00%       0.00%   0.00%      2001-01-01  ||||||F|201909180000
OBX|29|TX|MIX RECEIPT||  Alder, White (1:10)      TRS    TBD            1:10       0.250 mL   W/V     50.00%       0.00%   0.00%      2001-01-01  ||||||F|201909180000
OBX|30|TX|MIX RECEIPT||--------------------------------------------------------------------------------------------------------------------------||||||F|201909180000
```

## How to install channels

- Open Mirth
- Create a group to house the HL7 Interface channels (recommended)
  - In the Channel Tasks section of the sidebar, click New Group
  - Give your group a name, e.g. "HL7 Interface" and a description if you would like
  - Click your newly created group in the Channels list to select it
- In the Channel Tasks section of the sidebar, click Import Channel
- Navigate to the repo and select the channel you wish to import
- Once imported, update/verify the following channel properties:
  - In the Source tab: Database URL/username/password
  - In the Destinations tab:
    - In the `Read JSON From DB (CHANGE CONFIG HERE)` destination: Make changes to the `config` and `format` variables as necessary based on client needs. This is where you'll spend most of your time making changes.
    - Enable/disable the `Send to Write File channel` destination, and change the directory the files will write to if enabled
    - Enable/disable the `Send over TCP (CHANGE THIS)` destination, and change the URI destination if enabled
  - If no channels use the `Send to Write File channel` destination, disable the `Write to File` channel
  
## Testing the channels outside of Mirth

Included in the [Mirth repository](https://github.com/XtractSolutions/Mirth) is the `/test` folder, which contains plain javascript versions of the HL7 Builder object and the `config`/`format` variables, as well as some dummy data stolen from the database. You can drop this into your `htdocs` folder to test channel output without having to deal with Mirth.

The `index.htm` file contains entries for the channels. Only one of these should be uncommented at a time. The test data lives in the `data_*.js` files. The `config` and `format` variables live in the `config_*.js` files. And finally, `builder.js` contains the actual HL7 builder. 

Be mindful that if you make changes in the javascript files, there are lines that need to be uncommented/commented in order to prepare it for use in Mirth. For example, in Mirth we use `channelMap.put('data', data);` to transfer data between destinations, but in the test environment, this isn't possible/needed.

All output is to the console.

## OBX Document Formatting

In the `Read JSON from the DB (CHANGE CONFIG HERE)` destination of each channel are two important variables:
- `config`
- `format`

These are the variables you will need to mess with in order to affect changes to the text report embedded inside the OBX segments of the HL7 message. As you might guess, `config` contains configuration variables like the document title, the name of the receiving organization, etc. The `format` variable is where you structure the text report, specifying what data you want, where in the report it goes, and what you want to do with the data before it's used.

The `format` variable is just an array (`[]`) of objects (`{}`), separated by commas. The text report will be built from top to bottom using the data in the objects in the order you give them. That means that if you want a table, then a spacer, then another table, you need to explicitly create those objects, in that order, inside `format`.

Everything is case sensitive!

Here is an example `format` object:

```
{
  name: 'patientHeader',
  type: 'text',
  source: 'Patient',
  values: {
    'Name': 'fullName',
    'Medical Record Number': 'chart',
    'DOB': 'dob',
    'Note': 'patient_notes'
  },
  preprocessor: function(item) {
    item.fullName = item.lastname + ', ' + item.firstname + ' ' + (item.mi ? item.mi : 'NMI');
    item.patient_notes = item.patient_notes.replace(/(\r\n|\n|\r)/gm, ' ');
    return item;
  }
},
```

The `format` object consists of the following parameters:
- _`name`_: (*OPTIONAL, MOSTLY*) This is a nice name you can use to know which element is which. If the element _`type`_ is `table`, this will be used as the title for the table
- _`type`_: (*REQUIRED*) This is the format you want the data to be presented in. `type` can only be the following values:
  - `text`
  - `table`
  - `hybridTable`
  - `contaner`
  - `spacer`
  - `title`
- _`source`_: (*REQUIRED*) The key inside of `report.json` (or inside the container data set if _`type`_ is `container`) where the data for this element exists. If the data source is not a subset of the data, and is instead just... the data... this should be `null`.
- _`values`_: (*REQUIRED*) This is an object containing key/value pairs, where the _key_ is the display name/title, and the _value_ is the key inside of _`source`_ where the data can be found. This key can be created in the _`preprocessor`_ function if it doesn't exist. If _`type`_ is `title`, this should instead be _`value`_ and contain a single value. If the _`type`_ is `container`, this should be an array of object similar to the `format` variable itself.
- _`preprocessor`_: (*OPTIONAL*) This is a function that takes one argument, the data object being used to create the element or table row, and must return that argument at the end with any changes you need. In this function, you can make new data using anything at your disposal, and use that new data in _`values`_. 

## Element Types

### text

A text element is a simple listing of key/value pairs separated by a colon. 

Example `text` object:
```
  {
    name: 'patientHeader',
    type: 'text',
    source: 'Patient',
    values: {
      'Name': 'fullName',
      'Medical Record Number': 'chart',
      'DOB': 'dob',
      'Note': 'patient_notes'
    },
    preprocessor: function(item) {
      item.fullName = item.lastname + ', ' + item.firstname + ' ' + (item.mi ? item.mi : 'NMI');
      item.patient_notes = item.patient_notes.replace(/(\r\n|\n|\r)/gm, ' ');
      return item;
    }
  },
```
Output
```text
Name: Barratt, Luke NMI
Medical Record Number: 9999
DOB: 01-01-1900
Note: Hey this guy's pretty cool
```


### table

A `table` element takes an array or objects from the data source, such as all the vials used in a daily injection, and uses the keys in _`values`_ as column headers to create a graphical table. If you want a table-like format, but don't have an entire array of objects to loop over, try a `hybridTable` instead.

The vertical and horizontal characters used to create the table borders are located in the `config` object.

If the `format` object contains a _`name`_ parameter, that value will be used as the table's title, which is placed just above the table.

Example `table` object:

```
{
  name: 'DILUTION SET VIALS',
  type: 'table',
  source: 'vials',
  values: {
    'VIAL NUMBER': 'vial_number', 
    'DILUTION': 'dilution', 
    'COLOR': 'color', 
    'BARCODE': 'barcode', 
    'TIMESTAMP': 'mix_date', 
    'SIZE': 'size', 
    'OUT DATE': 'out_date'
  },
  preprocessor: function(item) {
    item.dilution = '1:' + item.dilution;
    return item;
  }
},
```
Output
```text
DILUTION SET VIALS
--------------------------------------------------------------------------------------
  VIAL NUMBER   DILUTION   COLOR   BARCODE   TIMESTAMP             SIZE   OUT DATE    
--------------------------------------------------------------------------------------
  1             1:1        RED     100065    2018-04-25 19:04:31   5 mL   2001-01-01  
  2             1:10       YLW     100066    2018-04-25 19:04:31   5 mL   2001-01-01  
--------------------------------------------------------------------------------------
```


### hybridTable

A `hybridTable` element is essentially the same as a `text` element, but presented like a `table` element, in that its data is arranged in columns that are spaced out for readability, and a border is added around the outside.

If you need to present an array of data (where normally a `table` would be more appropriate) as a `hybridTable`, you will need to wrap the `hybridTable` object in a `container` object to deliver the array data appropriately to the element.

Example `hybridTable` object:

```
{
  name: 'INJECTION',
  type: 'hybridTable',
  source: null,
  values: {
    'Vial Name': 'vial_name', 
    'Timestamp': 'datetime_administered', 
    'Reaction': 'local_reaction', 
    'SysReaction': 'systemic_reaction', 
    'Dilution': 'dilution', 
    'Color': 'color', 
    'Dose': 'dose', 
    'Location': 'site', 
    'Provider': 'provider', // Non-native
    'Given By': 'givenBy', // Non-native
    'Note': 'notes_patient'
  },
  preprocessor: function(item) {
    item.color = item.vial.color;
    item.site = item.site || item.vial.prescription.injection_site;
    item.notes_patient = item.notes_patient.replace(/(\r\n|\n|\r)/gm, ' ');
    item.givenBy = item.vial.user.displayname; // New entry
    item.provider = item.vial.prescription.provider.displayname; // New Entry
    return item;
  }
}
```
Output
```text
-------------------------------------------------------------------
  Vial Name     MTS\DST                                             
  Timestamp     2019-09-18 11:55:49                                 
  Reaction      None                                                
  SysReaction   N                                                   
  Dilution      1:10                                              
  Color         BLUE                                                
  Dose          0.150 mL mL                                         
  Location      midL                                                
  Provider      James W. Baker, MD                                  
  Given By      Lynn Miller                                         
  Note
-------------------------------------------------------------------  
```


### container

The `container` type is the only one that might be a little complicated. A `container` is used when you need to iterate over a subset of the data, passing that smaller data subset on to a new set of child elements. For example, you could create a set of elements for a prescription to display that prescription's vials and constituents as tables; however, if you have multiple prescriptions, and each one needs its own set of vials/constituents tables, that's what a `container` is for. You would simply wrap the elements you want to repeat per each item inside the _`values`_ array of the `container` object, and use the _`source`_ parameter to specify where the data to be iterated over comes from.

Example `container` object:

```
{
		name: 'prescriptionContainer',
		type: 'container',
		source: 'PurchaseOrder.treatment_sets',
		values: [
			{ type: 'spacer' },
			{
				name: 'prescriptionHeader',
				type: 'text',
				source: null,
				values: {
					'Prescription': 'name',
					'Prescription Number': 'prescription_number',
					'Note': 'note'
				},
				preprocessor: function(item) {
					item.prescription_number = item.prescription.prescription_number;
					return item;
				}
			},
			{ type: 'spacer' },
			{
				name: 'DILUTION SET VIALS',
				type: 'table',
				source: 'vials',
				values: { 
					'VIAL NUMBER': 'vial_number', 
					'DILUTION': 'dilution', 
					'COLOR': 'color', 
					'BARCODE': 'barcode', 
					'TIMESTAMP': 'mix_date', 
					'SIZE': 'size', 
					'OUT DATE': 'out_date'
				},
				preprocessor: function(item) {
					item.dilution = '1:' + item.dilution;
					return item;
				}
			},
			{ type: 'spacer' },
			{
				name: 'CONCENTRATE (1:1) VIAL CONSTITUENTS',
				type: 'table',
				source: 'constituents',
				values: { 
					'EXTRACT': 'name',
					'TYPE': 'type',
					'MANUFACTURER': 'manufacturer',
					'DILUTION': 'dilution', 
					'DOSE': 'dose', 
					'UNITS': 'units',
					'GLYCERIN %': 'glycerin', 
					'HSA %': 'hsa',
					'PHENOL %': 'phenol',
					'OUT DATE': 'out_date'
				},
				preprocessor: function(item) {
					item.name = item.inventory.extract.name;
					item.type = item.inventory.extract.abbreviation;
					item.manufacturer = item.inventory.extract.manufacturer;
					item.dilution = item.inventory.extract.dilution;
					item.dose = item.dosing.dose + ' ' + config.doseUnit;
					item.glycerin = item.inventory.extract.percent_glycerin + '%';
					item.hsa = item.inventory.extract.percent_hsa + '%';
					item.phenol = item.inventory.extract.percent_phenol + '%';
					item.out_date = item.inventory.out_date;
					item.units = item.inventory.extract.dilution_units.name;
					return item;
				}
			}
		]
	},
```

### title

A `title` element is simply a singular string sitting solidly solo.

Example `title` object:
```
{
  type: 'title',
  value: 'ADDAMA\'S REALLY COOL README'
}
```
Output
```text
ADDAMA'S REALLY COOL README
```

### spacer

A `spacer` element is a vertical space, equivalent to `<br />` or `\r\n\n` or `\r\n\r\n` if you're nasty.

Example `spacer` object:
```
{
  type: 'title',
  value: 'ADDAMA'S REALLY COOL README'
},
{
  type: 'spacer'
},
{
  type: 'spacer'
},
{
  type: 'spacer'
},
{
  type: 'title',
  value: 'HEY Y'ALL'
}
```
Output
```text
ADDAMA'S REALLY COOL README



HEY Y'ALL
```

## Changing the actual HL7 subsegments

If you for some reason need to change something in the HL7 that isn't already available to you, you will find the things you need to change in the `Convert JSON to HL7` destination. Namely, these are:
- The `msh`, `orc`, and `obr` variables
- The `builder.add()` function, which constructs the _OBX_ segments
- The `hl7` variable at the bottom, which combines all segments into a single message, and is the first and only time we touch the _PID_ and _PV1_ segments, which come directly from the JSON rather than being constructed

Keep in mind that HL7 is a structured specification - you can't just change the order of things or get rid of things you/the client don't like. 
