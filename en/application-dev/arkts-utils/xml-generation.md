# XML Generation


XML can be used as a data exchange format, which is supported by a wealth of systems and applications. For example, web services can transfer structured data in XML format.


XML can also be used as a message passing format for communication between nodes in a distributed system.


## Precautions

- XML tags must appear in pairs: one start tag and one end tag.

- XML tags are case sensitive. The start tag and end tag must use the same case.


## How to Develop

The **xml** module provides the **XmlSerializer** class to generate XML files. The input is an object of the ArrayBuffer or DataView type with a fixed length, which is used to store the output XML data.

You can call different to write different types of content. For example, call **startElement(name: string)** to write the start tag and **setText(text: string)** to write a tag value. 

For details about the APIs of the **XML** module, see [@ohos.xml (XML Parsing and Generation)](../reference/apis/js-apis-xml.md).

The following steps walk you through on how to generate an XML file.

1. Import the modules.
   
   ```js
   import xml from '@ohos.xml'; 
   import util from '@ohos.util';
   ```

2. Create a buffer and create an **XmlSerializer** object, either based on an object of the ArrayBuffer or DataView type.
   
   ```js
   // 1. Create an XmlSerializer object based on an object of the ArrayBuffer type.
   let arrayBuffer = new ArrayBuffer(2048); // Create a 2048-byte object of the ArrayBuffer type.
   let thatSer = new xml.XmlSerializer (arrayBuffer); // Create an XmlSerializer object based on the object of the ArrayBuffer type.
   
   // 2. Create an XmlSerializer object based on an object of the DataView type.
   let arrayBuffer = new ArrayBuffer(2048); // Create a 2048-byte object of the ArrayBuffer type.
   let dataView = new DataView(arrayBuffer); // Use an object of the DataView type to operate the object of the ArrayBuffer type.
   let thatSer = new xml.XmlSerializer (dataView); // Create an XmlSerializer object based on the object of the DataView type.
   ```

3. Call the functions to generate an XML file.
   
   ```js
   thatSer.setDeclaration(); // Write the XML file declaration.
   thatSer.startElement('bookstore'); // Write the start flag.
   thatSer.startElement('book'); // Write the start tag of a nested element.
   thatSer.setAttributes('category', 'COOKING'); // Write the attributes and attribute values.
   thatSer.startElement('title');
   thatSer.setAttributes('lang', 'en');
   thatSer.setText('Everyday'); // Write the tag value.
   thatSer.endElement(); // Write the end flag.
   thatSer.startElement('author');
   thatSer.setText('Giada');
   thatSer.endElement();
   thatSer.startElement('year');
   thatSer.setText('2005');
   thatSer.endElement();
   thatSer.endElement();
   thatSer.endElement();
   ```

4. Use **Uint8Array** to operate the object of the ArrayBuffer type, and use **TextDecoder** to decode the Uint8Array.
   
   ```js
   let view = new Uint8Array(arrayBuffer); // Use Uint8Array to read data from the object of the ArrayBuffer type.
   let textDecoder = util.TextDecoder.create(); // Call the TextDecoder class of the util module.
   let res = textDecoder.decodeWithStream (view); // Decode the view.
   console.info(res);
   ```

   The output is as follows:

   
   ```js
   <?xml version=\"1.0\" encoding=\"utf-8\"?><bookstore>\r\n  <book category=\"COOKING\">\r\n    <title lang=\"en\">Everyday</title>\r\n    <author>Giada</author>\r\n    <year>2005</year>\r\n  </book>\r\n</bookstore>
   ```
