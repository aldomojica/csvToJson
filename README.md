# CSVtoJSON 
[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/iuccio/csvToJson/Node%20CI?label=Build)](https://github.com/iuccio/csvToJson/actions?query=workflow%3A%22Node+CI%22)
[![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/iuccio/csvToJson/CodeQL/master?label=CodeQL)](https://github.com/iuccio/csvToJson/actions?query=workflow%3ACodeQL)
[![Code Climate](https://codeclimate.com/github/iuccio/csvToJson/badges/gpa.svg)](https://codeclimate.com/github/iuccio/csvToJson)
[![NPM Version](https://img.shields.io/npm/v/convert-csv-to-json.svg)](https://npmjs.org/package/convert-csv-to-json)
[![Downloads](https://img.shields.io/npm/dm/convert-csv-to-json.svg)](https://npmjs.org/package/convert-csv-to-json)

**This project is not dependent on others packages or libraries.**

## Table of Contents
1. [Description](#description)
1. [Prerequisites](#prerequisites)
1. [Install npm *convert-csv-to-json package*](#install-npm-convert-csv-to-json-package)
1. [Usage](#usage)
    * [Generate JSON file](#generate-json-file)
    * [Generate Array of Object in JSON format](#generate-array-of-object-in-json-format)
    * [Generate Object with sub array](#generate-object-with-sub-array)
    * [Define field delimiter](#define-field-delimiter)
    * [Format property value by type](#format-property-value-by-type)
        * [Number](#number)
        * [Boolean](#boolean)
    * [Encoding](#encoding)
1. [Development](#development)
1. [License](#license)
1. [Buy me a Coffee](#buy-me-a-coffee)


## Description
Converts *csv* files to *JSON* files with Node.js. 

Give an input file like:

|first_name|last_name|email|gender|age|zip|registered|
|:----------:|:-------:|:---:|:----:|:---:|:---:|:---:|
|Constantin|Langsdon|clangsdon0@hc360.com|Male|96|123|true|
|Norah|Raison|nraison1@wired.com|Female|32| |false|

e.g. :
~~~
first_name;last_name;email;gender;age;zip;registered
Constantin;Langsdon;clangsdon0@hc360.com;Male;96;123;true
Norah;Raison;nraison1@wired.com;Female;32;;false
~~~

will generate:


```json
[
 {
  "first_name": "Constantin",
  "last_name": "Langsdon",
  "email": "clangsdon0@hc360.com",
  "gender": "Male",
  "age": "96",
  "zip": "123",
  "registered": "true"
 },
 {
  "first_name": "Norah",
  "last_name": "Raison",
  "email": "nraison1@wired.com",
  "gender": "Female",
  "age": "32",
  "zip": "",
  "registered": "false"
 }
]
```

## Prerequisites
**NPM** (see [Installing Npm](https://docs.npmjs.com/getting-started/installing-node)).

## Install npm *convert-csv-to-json package*
Go to NPM package [convert-csv-to-json](https://www.npmjs.com/package/convert-csv-to-json).

### Install
Install package in your *package.json*
```bash
$ npm install convert-csv-to-json --save
```
Install package on your machine
```bash
$ npm install -g convert-csv-to-json
```

### Usage
#### Generate JSON file
```js
let csvToJson = require('convert-csv-to-json');

let fileInputName = 'myInputFile.csv'; 
let fileOutputName = 'myOutputFile.json';

csvToJson.generateJsonFileFromCsv(fileInputName,fileOutputName);
```
#### Generate Array of Object in JSON format
```js
let csvToJson = require('convert-csv-to-json');

let json = csvToJson.getJsonFromCsv("myInputFile.csv");
for(let i=0; i<json.length;i++){
    console.log(json[i]);
}
```

#### Generate Object with sub array 
```
firstName;lastName;email;gender;age;birth;sons
Constantin;Langsdon;clangsdon0@hc360.com;Male;96;10.02.1965;*diego,marek,dries*
```
Given the above CSV example, to generate a JSON Object with properties that contains sub Array, like the property **sons** 
with the values <b>*diego,marek,dries*</b> you have to call the function ```parseSubArray(delimiter, separator)``` .
To generate the JSON Object with sub array from the above CSV example:
```js
    csvToJson.parseSubArray('*',',').getJsonFromCsv('myInputFile.csv');
``` 
The result will be:
```json
[
  {
      "firstName": "Constantin",
      "lastName": "Langsdon",
      "email": "clangsdon0@hc360.com",
      "gender": "Male",
      "age": "96",
      "birth": "10.02.1965",
      "sons": ["diego","marek","dries"]
    }
]
``` 

#### Define field delimiter
As default the filed delimiter is the **semicolon** (**;**). You can define another field delimiter 
by call the function ```fieldDelimiter(myDelimiter)```.
If you want that the field delimiter is a **~**:

```js
 csvToJson.fieldDelimiter('~').getJsonFromCsv(fileInputName);
```

#### Format property value by type
If you want that a number will be printed as a Number type, and values *true* or *false* is printed as a Boolean Type, use:
```js
 csvToJson.formatValueByType().getJsonFromCsv(fileInputName);
```
For example: 

```json
[
 {
  "first_name": "Constantin",
  "last_name": "Langsdon",
  "email": "clangsdon0@hc360.com",
  "gender": "Male",
  "age": 96,
  "zip": 123,
  "registered": true
 },
 {
  "first_name": "Norah",
  "last_name": "Raison",
  "email": "nraison1@wired.com",
  "gender": "Female",
  "age": 32,
  "zip": "",
  "registered": false
 }
]
```
##### Number
The property **age** is printed as 
```json
 "age": 32
```
instead of
```json
  "age": "32"
 ```
##### Boolean
The property **registered** is printed as 
```json
 "registered": true
```
instead of
```json
  "registered": "true"
 ```

#### Encoding
You can read and decode files with the following encoding:
 * utf8: 
    ```js
     csvToJson.utf8Encoding().getJsonFromCsv(fileInputName);
    ```
 * ucs2:
    ```js
      csvToJson.ucs2Encoding().getJsonFromCsv(fileInputName);
     ```
 * utf16le:
     ```js
       csvToJson.utf16leEncoding().getJsonFromCsv(fileInputName);
      ```
 * latin1:
     ```js
       csvToJson.latin1Encoding().getJsonFromCsv(fileInputName);
      ```
 * ascii:
     ```js
       csvToJson.asciiEncoding().getJsonFromCsv(fileInputName);
      ```
 * base64:
     ```js
       csvToJson.base64Encoding().getJsonFromCsv(fileInputName);
      ```
 * hex:
     ```js
       csvToJson.hexEncoding().getJsonFromCsv(fileInputName);
      ```

## Development
* Download all csvToJson dependencies:
    ~~~
    npm install
    ~~~
* Run Tests
    ~~~
    npm test
    ~~~
* Watch Tests
    ~~~
    npm run test-watch
    ~~~

## License
CSVtoJSON is licensed under the GNU General Public License v3.0 [License](LICENSE).

## Buy me a Coffee	
Just if you want to support this repository:	
   * **BTC** tip address: 3KCCK292a61AHrKuVCFZ8Agr3j31Zw8Mzg
