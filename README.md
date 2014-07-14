# iso-639-2

This ISO 639-2 JavaScript library works in NodeJS and modern web browsers.  
It provides a function to get an array of all languages, sorted by alpha-3
code, alpha-2 code, native name, English name, or reading direction
(LTR or RTL).  It also provides a function to look up a language by the
alpha-3 or alpha-2 code.  

As of 14 July 2014, all 486 languages listed on the
[official Library of Congress web page](http://www.loc.gov/standards/iso639-2/php/code_list.php)
are supported.

## API

* **languages.getLanguages(sortBy, isAlpha2Code)**: *Returns an array of sorted
language objects. Default sortBy is "a3".  Default isAlpha2Code is false.*

* **languages.getLanguage(languageCode, isAlpha2Code)**: *Returns a language
object that matches the languageCode.  Default isAlpha2Code is false.*

* **languages.getLabel(propertyName)**: *Returns the label associated with the
propertyName.  Valid property names are a3, a3t, a2, name, eng, dir.*

* **languages.isValid(languageCode, isAlpha2Code)**: *Returns true if a
language object is found that matches the languageCode.  Default isAlpha2Code
is false.*

* **languages.isRtl(languageCode, isAlpha2Code)**: *Returns true if a
language object is found that matches the languageCode and has a dir property
value of rtl.*

## NodeJS Usage
```js
    var languages = require('iso-639-2');
    var langs = languages.getLanguages('eng');

    for (i=0, len=langs.length; i<len; i++) {
        lang = langs[i];
        console.log(lang.eng + ':');
        console.log('    ' + JSON.stringify(lang));
    }
    console.log('\n# of Languages: ' + i);
```

## Browser Usage

```html
<!doctype html>
<html>
<head>
    <title>ISO 639-2 Languages Module</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=0">
    <script src="iso-639-2.js"></script>
    <style>
        body {
            background-color: #fff;
        }
        th {
            vertical-align: bottom;
            text-align: left;
            padding: 4px;
        }
        table {
            border-collapse: collapse;
        }
        td {
            vertical-align: top;
            border: 1px solid black;
            padding: 4px;
        }
    </style>
</head>
<body>
    <h2>ISO 639-2 Languages Module Test</h2>
    <div id="test"></div>
    <script>
        var i, len, lang,
        text = '<table><tr><th>' + languages.getLabel('eng') +
            '</th><th>' + languages.getLabel('name') +
            '</th><th>' + languages.getLabel('a3') +
            '</th><th>' + languages.getLabel('a3t') +
            '</th><th>' + languages.getLabel('a2') +
            '</th><th>' + languages.getLabel('dir') +
            '</th></tr>';


        var langs = languages.getLanguages('eng');

        for (i=0, len=langs.length; i<len; i++) {
            lang = langs[i];
            text += '<tr><td>' + lang.eng +
                '</td><td>' + lang.name +
                '</td><td>' + lang.a3 +
                '</td><td>' + lang.a3t +
                '</td><td>' + lang.a2 +
                '</td><td>' + lang.dir +
                '</td></tr>';

        }
        text += '</table>';

        text = '<h3># of Languages: '+i+'</h3>'+text;

        document.getElementById('test').innerHTML = text;

    </script>
</body>
</html>
```
