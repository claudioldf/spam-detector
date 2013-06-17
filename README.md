Spam Filter
---------------------

Spam Filter is a simple library for detecting spam messages. It follows the open closed principle by introducing
Spam Detectors which are just separate classes used to extend the spam filter detecting capabilities.

## Installation

Spam Filter library can be loaded into your projects using [Composer](http://getcomposer.org) or by loading
the inbuilt autoloader.

##### Composer Installation

You can define the spam filter as a dependency in your project. Below is a minimal setup required

	{
		"require" : {
			"linko/spam" : "dev-master"
		}
	}

##### Using autoload.php

If you are not using composer for your dependency (which you should) there is a simple autoloader packaged with
this library which you can just 'include()' into your project files

	<?php

	require_once '/path/to/linko/spam/autoload.php';

## Usage

	```php
	<?php

	use Linko\Spam\SpamFilter;

	// Create a black list spam detector
	$blackListDetector = new BlackList();

	// add some text string to the black list detector
	$blackListDetector->add('example.com');
	$blackListDetector->add('127.0.0.1');

	// Create the spam filter
	$spam = new SpamFilter();

	// Register a spam detector (Like the black list we added above)
	$spam->registerDetector($blackListDetector);

	// Run the check
	$spamCheck = $spam->check("
		Hello, this is some text containing example.com
		and should fail as it has a word that is black listed
	");

	if($spamCheck->passed())
	{
		// Do stuff
	}

Each time you call the ``check()`` method on a string, it returns a ``SpamResult``
Object which holds the ... hmm ... spam check result.

## Currently Supported Spam Detector

###### 1. BlackList Detector:

The black list detector is a spam detector that flags a string as a spam  if it contains
any of one or more words that has been added to the black list.
Strings could be a regular expression or a character sequence.