|变量名|缩写|含义|
|:--------|:-----|:-----|
|(no)autoindent|ai    |自动缩进，即为新行自动添加与当前行同等的缩进。|
|(no)cindent|ci    |类似C语言程序的缩进|
|(no)smartindent|si    |基于autoindent的一些改进|
|tabstop=X|ts    |编辑时一个TAB字符占多少个空格的位置。|
|shiftwidth=X|sw    |使用每层缩进的空格数。|
|(no)expandtab|(no)et|是否将输入的TAB自动展开成空格。开启后要输入TAB，需要Ctrl-V

&lt;TAB&gt;

|
|softtabstop=X|sts   |方便在开启了et后使用退格（backspace）键，每次退格将删除X个空格|
|(no)smarttab|(no)sta|开启时，在行首按TAB将加入sw个空格，否则加入ts个空格。|