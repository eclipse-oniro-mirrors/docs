# XML概述


XML（可扩展标记语言）是一种用于描述数据的标记语言，旨在提供一种通用的方式来传输和存储数据，特别是Web应用程序中经常使用的数据。XML并不预定义标记。因此，XML更加灵活，并且可以适用于广泛的应用领域。


XML文档由元素（element）、属性（attribute）和内容（content）组成。


- 元素指的是标记对，包含文本、属性或其他元素。

- 属性提供了有关元素的其他信息。

- 内容则是元素包含的数据或子元素。


XML可以通过使用XML Schema或DTD（文档类型定义）来定义文档结构。这些机制允许开发人员创建自定义规则以验证XML文档是否符合其预期的格式。


XML支持命名空间、实体引用、注释和处理指令等特性，使其能够灵活地适应各种数据需求。


语言基础类库提供了XML相关的基础能力，包括：[XML的生成](xml-generation.md)、[XML的解析](xml-parsing.md)和[XML的转换](xml-conversion.md)。

以下是一个简单的XML样例及对应说明，更多XML的接口和具体使用，请见[@ohos.xml](../reference/apis-arkts/js-apis-xml.md)。

```XML
<?xml version="1.0" encoding="utf-8"?> <!-- 声明 -->
<!-- 处理指令 -->
<?xml-stylesheet type="text/css" href="style.css"?>
<!-- 元素、属性及属性值 -->
<note importance="high">
    <title>Happy</title>
    <!-- 实体引用 -->
    <todo>&amp;</todo>
    <!-- 命名空间的声明及统一资源标识符 -->
    <h:table xmlns:h="http://www.w3.org/TR/html4/">
        <h:tr>
            <h:td>Apples</h:td>
            <h:td>Bananas</h:td>
        </h:tr>
    </h:table>
</note>
```