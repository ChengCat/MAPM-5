# MAPM-5
Mike's Arbitrary Precision Math Library Version 5.0  

Tried many attempts to contact *Michael C. Ring* for MAPM long overdued updates (20 years?)  
His official website was retired: http://www.tc.umn.edu/~ringx004/mapm-main.html  
  
I revised his calc.exe demo program into a more useful rpn.exe  
  
Example: decimal -> IEEE double -> decimal  
```
> rpn 0.1 g17       // (double) 0.1 17 sig. digits (half-way round-to-even)  
0.10000000000000001  
> rpn 0.1 g ?? k    // (double) 0.1, print exact value, then clear stack
0.1000000000000000055511151231257827021181583404541015625  
``` 
Example: data stats
```
> seq 0 .1 100 > data     // different ways to sum data
> rpn 0 [ + ] < data      // pipe in data  
50050  
> rpn 0 [ + ]data         // read file directly  
50050  
> rpn [1 + ]data          // skip first line, so first '+' have 2 arguments  
50050  
  
> perl stat.pl data       // Welford's method for accurate std-dev  
Average = 49.999999999999289 = 50049.999999999287 / 1001  
Std Dev = 28.910811126635725  

> perl stat.pl -x data    // exact mode -> wrapper for rpn.exe  
Average = 50 = 50050 / 1001  
Std Dev = 28.910811126635657  

> lua stat.lua < data     // 2-passes for accurate std-dev
Items   1001              // note: my patched lua default to print  
Average 50                // shortest digits that still round-trip
Std Dev 28.910811126635657  
-------  
Min     0  
Q1      25  
Med     50  
Q3      75  
Max     100  
```
