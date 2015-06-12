SwiftyExpat
===========

Simple wrapper for the Expat XML parser.

###Targets

Updated to use Swift v2.0p1 (aka Xcode 7b).

The project includes two targets:
- SwiftyExpat
- SwiftyExpatTests

I suggest you start by looking at the SwiftyExpatTests.

####SwiftyExpat

This is a tiny framework containing the modified Expat parser. Plus a small
Swift class to make the API nicer, though this is not really necessary - the
block based Expat is reasonably easy to use from Swift.

```Swift
let p = Expat()
  .onStartElement   { name, attrs in println("<\(name) \(attrs)")       }
  .onEndElement     { name        in println(">\(name)")                }
  .onStartNamespace { prefix, uri in println("+NS[\(prefix)] = \(uri)") }
  .onEndNamespace   { prefix      in println("-NS[\(prefix)]")          }
  .onError          { error       in println("ERROR: \(error)")         }
p.write("<hello>world</hello>")
p.close()
```

The raw Expat API works like this:
```Swift
var p = XML_ParserCreate("UTF-8")
XML_SetStartElementHandler(p) { _, name, attrs in println("start tag \(name)") }
XML_SetEndElementHandler  (p) { _, name        in println("end tag \(name)") }

XML_Parse(parser, "<hello/>", 8, 0)
XML_Parse(parser, "", 0, 1)

XML_ParserFree(p); p = nil
```
You get the idea ...

Note: With the function based Expat API, the closures in the raw API cannot
      capture references. You need to use the 'user data' field (which the
      wrapper does).

####SwiftyExpatTests

Just a tiny demo on how to invoke the parser.

###Contact

[@helje5](http://twitter.com/helje5) | helge@alwaysrightinstitute.com
