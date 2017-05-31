# ISO8859-1ToUTF8
Convert strings encoded with charset ISO-8859-1 to UTF-8 with pure JavaScript, mainly for CJK (Chinese/Jpanese/Korean) languages.

## Background
Sometimes we call WebService in JavaScript with Jquery/AJAX, but the WebService charset is set to ISO-8859-1, but we can't get the Chinese words correctly, the words will be shown as garbled characters.

To solve this issue, I write a charset mapping/convertion tool.

It works in Windows 7 with Chrome browser.

## Usage:
First step, we need make HTTP POST method getting data with charset ISO-8859-1, because JS call WS with charse UTF-8 by default if it is not set in WS. We need overide MIME type of request.

* If you are using Jquery SOAP plugin, please add property 'mimeType' in jquery.soap.js. 
```
return $.ajax({
type:"POST",
url:options.url,
......
contentType:contentType+";charset=UTF-8",
mimeType:"text/xml;charset=iso-8859-1",
```

* If you are using XMLHTTP, call `overrideMimeType` method of XMLHttpRequest object.
```
xmlobj.overrideMimeType("text/xml;charset=iso-8859-1");
```

* If you are using AngularJS, there is no property provided by AngularJS, but we can modify angular.js by call `overrideMimeType` method of XMLHttpRequest object after create it.
```
var xhr = createXhr();
//add this line after createXhr()
xhr.overrideMimeType("text/xml;charset=iso-8859-1");
```

Second step, convert strings encoded with charset ISO-8859-1 to UTF-8. We need reference the ISO88591toUTF.js in your project.
```
var out = convertToUTF8(responseText);
```

