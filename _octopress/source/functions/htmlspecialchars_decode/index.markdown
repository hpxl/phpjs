---
layout: page
title: "JavaScript htmlspecialchars_decode function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/htmlspecialchars_decode:427
- /functions/view/htmlspecialchars_decode
- /functions/view/427
- /functions/htmlspecialchars_decode:427
- /functions/427
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's htmlspecialchars_decode

{% codeblock strings/htmlspecialchars_decode.js lang:js https://raw.github.com/kvz/phpjs/master/functions/strings/htmlspecialchars_decode.js raw on github %}
function htmlspecialchars_decode (string, quote_style) {
  // http://kevin.vanzonneveld.net
  // +   original by: Mirek Slugen
  // +   improved by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
  // +   bugfixed by: Mateusz "loonquawl" Zalega
  // +      input by: ReverseSyntax
  // +      input by: Slawomir Kaniecki
  // +      input by: Scott Cariss
  // +      input by: Francois
  // +   bugfixed by: Onno Marsman
  // +    revised by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
  // +   bugfixed by: Brett Zamir (http://brett-zamir.me)
  // +      input by: Ratheous
  // +      input by: Mailfaker (http://www.weedem.fr/)
  // +      reimplemented by: Brett Zamir (http://brett-zamir.me)
  // +    bugfixed by: Brett Zamir (http://brett-zamir.me)
  // *     example 1: htmlspecialchars_decode("<p>this -&gt; &quot;</p>", 'ENT_NOQUOTES');
  // *     returns 1: '<p>this -> &quot;</p>'
  // *     example 2: htmlspecialchars_decode("&amp;quot;");
  // *     returns 2: '&quot;'
  var optTemp = 0,
    i = 0,
    noquotes = false;
  if (typeof quote_style === 'undefined') {
    quote_style = 2;
  }
  string = string.toString().replace(/&lt;/g, '<').replace(/&gt;/g, '>');
  var OPTS = {
    'ENT_NOQUOTES': 0,
    'ENT_HTML_QUOTE_SINGLE': 1,
    'ENT_HTML_QUOTE_DOUBLE': 2,
    'ENT_COMPAT': 2,
    'ENT_QUOTES': 3,
    'ENT_IGNORE': 4
  };
  if (quote_style === 0) {
    noquotes = true;
  }
  if (typeof quote_style !== 'number') { // Allow for a single string or an array of string flags
    quote_style = [].concat(quote_style);
    for (i = 0; i < quote_style.length; i++) {
      // Resolve string input to bitwise e.g. 'PATHINFO_EXTENSION' becomes 4
      if (OPTS[quote_style[i]] === 0) {
        noquotes = true;
      } else if (OPTS[quote_style[i]]) {
        optTemp = optTemp | OPTS[quote_style[i]];
      }
    }
    quote_style = optTemp;
  }
  if (quote_style & OPTS.ENT_HTML_QUOTE_SINGLE) {
    string = string.replace(/&#0*39;/g, "'"); // PHP doesn't currently escape if more than one 0, but it should
    // string = string.replace(/&apos;|&#x0*27;/g, "'"); // This would also be useful here, but not a part of PHP
  }
  if (!noquotes) {
    string = string.replace(/&quot;/g, '"');
  }
  // Put this in last place to avoid escape being double-decoded
  string = string.replace(/&amp;/g, '&');

  return string;
}
{% endcodeblock %}

 - [view on github](https://github.com/kvz/phpjs/blob/master/functions/strings/htmlspecialchars_decode.js)
 - [edit on github](https://github.com/kvz/phpjs/edit/master/functions/strings/htmlspecialchars_decode.js)

### Example 1
This code
{% codeblock lang:js example %}
htmlspecialchars_decode("<p>this -&gt; &quot;</p>", 'ENT_NOQUOTES');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
'<p>this -> &quot;</p>'
{% endcodeblock %}

### Example 2
This code
{% codeblock lang:js example %}
htmlspecialchars_decode("&amp;quot;");
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
'&quot;'
{% endcodeblock %}


### Other PHP functions in the strings extension
{% render_partial _includes/custom/strings.html %}
