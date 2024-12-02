# [Netlab1_sharing](https://ctf.viblo.asia/puzzles/netlab1-sharing-7ftcbkfnovy)
This challenge contains a pcap file and the hints mentions about protocol. First, i opened the file using ```Wireshark``` and analyzed a protocol column.  
I noticed that in the ```SMB2 protocol```, there is a zip file named ```netlab1.7z```, a password text file so i decided to export it.
```linux
File ⟶ Export Objects ⟶ SMB...
```
After extracting the zip file, i obtained a file named ```netlab1.db``` which is in SQLite format so i use [SQLite Viewer](https://inloop.github.io/sqlite-viewer/) to read it.  
![image](https://github.com/user-attachments/assets/bd9455f6-01f6-4b4d-ab15-1e8367485ff1)  
![image](https://github.com/user-attachments/assets/60abfbe4-c996-4b84-a040-243e43f36d71)  
## FLAG: **```Flag{NetLab1_N0w_y0u_kn0w_SMB??}```**
