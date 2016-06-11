# node-gettext-json

**node-gettext-json** is a Node.JS module to use .json files.

Fork of andris9 [node-gettext](https://github.com/andris9/node-gettext). But only supports json to be able to use it with React Native.

## Features

  * Load *json* files
  * Supports contexts and plurals

## Installation

    npm install node-gettext-json

## Usage

### Create a new Gettext object

    var Gettext = require("node-gettext-json");

    var gt = new Gettext();

### Add a language

*addTextdomain(domain, file)*

Language data needs to be in the Buffer format - it can be either contents of a *json* file.

*addTextdomain(domain[, fileContents])*

Load from a *json* file

    var gt = new Gettext();
    var jsonFile = JSON.parse(fs.readFileSync(__dirname + '/fixtures/latin13.json'));

    gt.addTextdomain('et-EE', jsonFile);

Plural rules are automatically detected from the language code

    gt.addTextdomain("et");
    gt.setTranslation("et", false, "hello!", "tere!");

### Check or change default language

*textdomain(domain)*

    gt.textdomain("et");

The function also returns the current texdomain value

    var curlang = gt.textdomain();

## Translation methods

### Load a string from default language file

*gettext(msgid)*

    var greeting = gt.gettext("Hello!");

### Load a string from a specific language file

*dgettext(domain, msgid)*

    var greeting = gt.dgettext("et", "Hello!");

### Load a plural string from default language file

*ngettext(msgid, msgid_plural, count)*

    gt.ngettext("%d Comment", "%d Comments", 10);

### Load a plural string from a specific language file

*dngettext(domain, msgid, msgid_plural, count)*

    gt.dngettext("et", "%d Comment", "%d Comments", 10)

### Load a string of a specific context

*pgettext(msgctxt, msgid)*

    gt.pgettext("menu items", "File");

### Load a string of a specific context from specific language file

*dpgettext(domain, msgctxt, msgid)*

    gt.dpgettext("et", "menu items", "File");

### Load a plural string of a specific context

*npgettext(msgctxt, msgid, msgid_plural, count)*

    gt.npgettext("menu items", "%d Recent File", "%d Recent Files", 3);

### Load a plural string of a specific context from specific language file

*dnpgettext(domain, msgctxt, msgid, msgid_plural, count)*

    gt.dnpgettext("et", "menu items", "%d Recent File", "%d Recent Files", 3);

### Get comments for a translation (if loaded from PO)

*getComment(domain, msgctxt, msgid)*

    gt.getComment("et", "menu items", "%d Recent File");

Returns an object in the form of `{translator: "", extracted: "", reference: "", flag: "", previous: ""}`

## Advanced handling

If you need the translation object for a domain, for example `et_EE`, you can access it from `gt.domains.et_EE`.

## License

MIT
