# [NetLab Warmup](https://ctf.viblo.asia/puzzles/netlab-warmup-vg104c0hpc7)
[The challenge file](https://ctf.viblo.asia/api/download?file=hIuLADLjpimd5sxHAP0DOD0CrOQ4bq6XtLHZWZzt.zip&name=netlab0.zip&puzzle_hash_id=Vg104C0hPc7) is contains a pcap file. To start, i inspected the file using [wireshark](https://www.wireshark.org/) and surfed it.  
After reading the information of some packets, i noticed there is a packet which hold a flag text.  
It looks like encoded by [Rot-13](https://en.wikipedia.org/wiki/ROT13) which is a special case of caesar cipher and my mission is decoded it.   
```linux
user@LAPTOP-TL39B5OL:~$ echo 'Synt{ArgYno0_SGC_1f_a0g_f3pHe3333}' | tr 'A-Za-z' 'N-ZA-Mn-za-m'
Flag{NetLab0_FTP_1s_n0t_s3cUr3333}
```
## Flag: **```Flag{NetLab0_FTP_1s_n0t_s3cUr3333}```**
