## MyISAM ##

MyISAM无法处理事务，适用于：

  1. 选择密集的表。MyISAM在大量数据在中筛选非常迅速，甚至在高流量环境中也也是如此。
  1. 插入密集的表。MyISAM的并发插入特性允许同时选择和插入数据。例如，MyISAM和很适合管理邮件或Web的日志数据。

MyISAM的三种格式：

  1. MyISAM静态：所有表列的大小都是静态的（即不使用xBLOB, xTEXT或VCHAR数据类型）。
  1. MyISAM动态
  1. MyISAM压缩