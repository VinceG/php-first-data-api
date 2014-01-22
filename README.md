First Data Global Gateway PHP API Service
==================

<a href='https://twitter.com/gabrielva' target='_blank'>Follow @gabrielva</a>

This component provides a PHP Wrapper to post api calls to the First Data payment processor.

It requires curl and the php curl extension.

## Features:
* Supports all transaction types.
* Supports Transarmor Token for charging credit cards more than once without storing the actual card number. 

## Installation
This library is now installable using <a href='http://getcomposer.org'>Composer</a>

Add this to your project composer.json:

```
	"require": {
        "vinceg/firstdataapi": "dev-master"
	},
```

To use the component:

```php
<?php
use VinceG\FirstDataApi\FirstData;

//
// 3rd Parameter sets debug mode on.  
// In debug mode, the demo gateway is used.  
// You will need to create a demo gateway account with First Data
// 
$firstData = new FirstData(API_LOGIN, API_KEY, true);

```

## Documentation and Examples 
### First Data Documentation:
<a href='https://firstdata.zendesk.com/entries/407571-First-Data-Global-Gateway-e4-Web-Service-API-Reference-Guide'>Api Reference Guide</a>

In these examples:
* API_LOGIN is the Terminal Gateway ID of your commerce terminal.
* API_KEY is the password you generate in the terminal screen.


### Examples:

#### Pre Auth

```
// Pre Auth Transaction Type
$firstData = new FirstData(API_LOGIN, API_KEY, true);

// Charge
$firstData->setTransactionType(FirstData::TRAN_PREAUTH);
$firstData->setCreditCardType($data['type'])
		->setCreditCardNumber($data['number'])
		->setCreditCardName($data['name'])
		->setCreditCardExpiration($data['exp'])
		->setAmount($data['amount'])
		->setReferenceNumber($orderId);

if($data['zip']) {
	$firstData->setCreditCardZipCode($data['zip']);
}

if($data['cvv']) {
	$firstData->setCreditCardVerification($data['cvv']);
}

if($data['address']) {
	$firstData->setCreditCardAddress($data['address']);
}

$firstData->process();

// Check
if($firstData->isError()) {
	// there was an error
} else {
	// transaction passed
}
```

#### Purchase

```
// Purchase Transaction type
$firstData = new FirstData(API_LOGIN, API_KEY, true);

// Charge
$firstData->setTransactionType(FirstData::TRAN_PURCHASE);
$firstData->setCreditCardType($data['type'])
		->setCreditCardNumber($data['number'])
		->setCreditCardName($data['name'])
		->setCreditCardExpiration($data['exp'])
		->setAmount($data['amount'])
		->setReferenceNumber($orderId);

if($data['zip']) {
	$firstData->setCreditCardZipCode($data['zip']);
}

if($data['cvv']) {
	$firstData->setCreditCardVerification($data['cvv']);
}

if($data['address']) {
	$firstData->setCreditCardAddress($data['address']);
}

$firstData->process();

// Check
if($firstData->isError()) {
	// there was an error
} else {
	// transaction passed
}
```

#### Purchase with TransArmor Token

```
// Purchase Transaction type
$firstData = new FirstData(API_LOGIN, API_KEY, true);

// Charge
$firstData->setTransactionType(FirstData::TRAN_PURCHASE);
$firstData->setCreditCardType($data['number'])
		->setTransArmorToken($data['token'])
		->setCreditCardName($data['name'])
		->setCreditCardExpiration($data['exp'])
		->setAmount($data['amount'])
		->setReferenceNumber($orderId);

$firstData->process();

// Check
if($firstData->isError()) {
	// there was an error
} else {
	// transaction passed
}
```

#### Pre Auth Complete

```
// Purchase Transaction type
$firstData = new FirstData(API_LOGIN, API_KEY, true);

// Charge
$firstData->setTransactionType(FirstData::TRAN_PREAUTHCOMPLETE);
$firstData->setCreditCardType($data['number'])
		->setTransArmorToken($data['token'])
		->setCreditCardName($data['name'])
		->setCreditCardExpiration($data['exp'])
		->setAuthNumber($dat['auth_number'])
		->setAmount($data['amount'])
		->setReferenceNumber($orderId);

$firstData->process();

// Check
if($firstData->isError()) {
	// there was an error
} else {
	// transaction passed
}
```

#### Refund

```
// Purchase Transaction type
$firstData = new FirstData(API_LOGIN, API_KEY, true);

// Charge
$firstData->setTransactionType(FirstData::TRAN_REFUND);
$firstData->setCreditCardType($data['number'])
		->setTransArmorToken($data['token'])
		->setCreditCardName($data['name'])
		->setCreditCardExpiration($data['exp'])
		->setAmount($data['amount'])
		->setReferenceNumber($orderId);

$firstData->process();

// Check
if($firstData->isError()) {
	// there was an error
} else {
	// transaction passed
}
```

#### Void

```
// Purchase Transaction type
$firstData = new FirstData(API_LOGIN, API_KEY, true);

// Charge
$firstData->setTransactionType(FirstData::TRAN_VOID);
$firstData->setCreditCardType($data['number'])
		->setTransArmorToken($data['token'])
		->setCreditCardName($data['name'])
		->setCreditCardExpiration($data['exp'])
		->setAmount($data['amount'])
		->setReferenceNumber($orderId);

$firstData->process();

// Check
if($firstData->isError()) {
	// there was an error
} else {
	// transaction passed
}
```

<p>&copy; <a href='http://vadimg.com' target="_blank">Vadim Vincent Gabriel</a> <a href='https://twitter.com/gabrielva' target='_blank'>Follow @gabrielva</a> 2013</p>

License
===============
The MIT License (MIT)

Copyright (c) 2013 - Vincent Gabriel

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
