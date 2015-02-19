SniffAdBlock (v0.0.0)
===========

Allows you to detect those nasty ad blockers.
Online example: http://sitexw.fr/fuckadblock/


Valid on :
---------------------
- Google Chrome
- Mozilla Firefox
- Internet Explorer (8+)
- Safari
- Opera

Code example
---------------------
```javascript
// Function called if AdBlock is not detected
function adBlockNotDetected() {
	alert('AdBlock is not enabled');
}
// Function called if AdBlock is detected
function adBlockDetected() {
	alert('AdBlock is enabled');
}

// Recommended audit if AdBlock locks the file 'sniffadblock.js' 
// If the file is not called, the variable does not exist 'sniffAdBlock'
// This means that AdBlock is present
if(typeof sniffAdBlock === 'undefined') {
	adBlockDetected();
} else {
	sniffAdBlock.onDetected(adBlockDetected);
	sniffAdBlock.onNotDetected(adBlockNotDetected);
	// and|or
	sniffAdBlock.on(true, adBlockDetected);
	sniffAdBlock.on(false, adBlockNotDetected);
	// and|or
	sniffAdBlock.on(true, adBlockDetected).onNotDetected(adBlockNotDetected);
}

// Change the options
sniffAdBlock.setOptions('checkOnLoad', false);
// and|or
sniffAdBlock.setOptions({
	checkOnLoad: false,
	resetOnEnd: false
});
```

Default options
---------------------
```javascript
// At launch, check if AdBlock is enabled
// Uses the method sniffAdBlock.check()
checkOnLoad: true

// At the end of the check, is that it removes all events added ?
resetOnEnd: true

// The number of milliseconds between each check
loopCheckTime: 50

// The number of negative checks after which there is considered that AdBlock is not enabled
// Time (ms) = 50*(5-1) = 200ms (per default)
loopMaxNumber: 5

// CSS class used by the bait caught AdBlock
baitClass: 'pub_300x250 pub_300x250m pub_728x90 text-ad textAd text_ad text_ads text-ads text-ad-links'

// CSS style used to hide the bait of the users
baitStyle: 'width: 1px !important; height: 1px !important; position: absolute !important; left: -10000px !important; top: -1000px !important;'
```

Method available
---------------------
```javascript
// Allows to set options
// #options: string|object
// #value:   string
sniffAdBlock.setOption(options, value);

// Allows to check if AdBlock is enabled
// The parameter 'loop' allows checking without loop several times according to the value of 'loopMaxNumber'
// Example: loop=true  => time~=200ms (time varies depending on the configuration)
//          loop=false => time~=1ms
// #loop: boolean (default: true)
sniffAdBlock.check(loop);

// Allows to manually simulate the presence of AdBlock or not
// #detected: boolean (AdBlock is detected ?)
sniffAdBlock.emitEvent(detected);

// Allows to clear all events added via methods 'on', 'onDetected' and 'onNotDetected'
sniffAdBlock.clearEvent();

// Allows to add an event if AdBlock is detected
// #detected: boolean (true: detected, false: not detected)
// #fn:       function
sniffAdBlock.on(detected, fn);

// Similar to sniffAdBlock.on(true|false, fn)
sniffAdBlock.onDetected(fn);
sniffAdBlock.onNotDetected(fn);
```
