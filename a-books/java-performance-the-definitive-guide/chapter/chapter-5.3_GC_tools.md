# 垃圾回收工具

## GC 日志


## jconsole


## jstat
```md
$ jstat -gcutil [pid] 1000
  S0     S1     E      O      M     CCS    YGC     YGCT    FGC    FGCT     GCT
  0.00   0.00  51.13   1.80  97.55  93.80   1578   93.217     9    3.658   96.875
  0.00   0.00  51.13   1.80  97.55  93.80   1578   93.217     9    3.658   96.875
  0.00   0.00  51.13   1.80  97.55  93.80   1578   93.217     9    3.658   96.875
  ... ...
```
```md
jstat 接受一个时间可选参数，制定每个多少ms重复执行这个命令。

*  YGC YGCT
  新生代垃圾回收 次数 和 花费的秒数。
* FGC FGCT
  Gull GC 次数 和 花费的秒数。
* S0     S1     E  O M
  两个 Survivor 空间 和 Eden 空间，老年代，方法区，已占用百分比。
```

