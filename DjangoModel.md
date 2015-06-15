**AutoField**

指一个能够根据可用ID自增的IntegerField。通常不用直接使用它，如果没有指定主键，系统会自动再模型中加入这样的主键。

**BooleanField**

一个真/假(true/false)字段。

**CharField**

一个字符串字段，适合于中小长度的字符串。对于长段的文字，请使用TextField。

CharField有一个额外的必需参数：max\_length，它是字段的最大长度（字符数）。