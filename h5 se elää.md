# H5 Se elää!
Kosti Kangasmaa 22/09/2025
## Ympäristö
- Windows 11 PC
- VMware Workstation Pro 17
- [Kali Linux VMware image](https://www.kali.org/get-kali/#kali-virtual-machines)
- Memory - 2 GB
- Processors - 4
- Hard Disk - 80 GB
- Network - NAT
## lab0
![lab0-1](/kuvat/h5/lab0-1.png)
![lab0-2](/kuvat/h5/lab0-2.png)
![lab0-3](/kuvat/h5/lab0-3.png)
![lab0-4](/kuvat/h5/lab0-4.png)

## lab1
![lab1-1](/kuvat/h5/lab1-1.png)
```bash
gdb ./gdb_example1
``` 
```bash
break main
```
```bash
info args
```
```bash
watch message
```
- Tämän jälkeen kuljin stepillä ohjelman toimintaa läpi kunnes ohjelma kaatui

![lab1-2](/kuvat/h5/lab1-2.png)
![lab1-3](/kuvat/h5/lab1-3.png)
![lab1-4](/kuvat/h5/lab1-4.png)
- Huomasin että ohjelma kaatui kun se yritti käsitellä messagen NULL arvoa stringinä
- Joten lisäsin ohjelmaan if-lauseen käsittelemään tilanteen
![lab1-5](/kuvat/h5/lab1-5.png)
![lab1-6](/kuvat/h5/lab1-6.png)
## lab2
```bash
gdb ./passtr
```
![lab2-1](/kuvat/h5/lab2-1.png)
![lab2-2](/kuvat/h5/lab2-2.png)
- Tämän jälkeen aika loppui kesken, koska tehtävänannot saapui moodleen vasta perjantai iltapäivällä vaikka olin niitä jo kysynyt tiistaina kasvotukse, sekä torstaina sähköpostitse. Opiskelen ma-pe klo 8-16 työaikoina. joten minulla oli noin 6 tuntia aikaa tehdä tehtävät, koin tämän melko kohtuuttomaksi.
