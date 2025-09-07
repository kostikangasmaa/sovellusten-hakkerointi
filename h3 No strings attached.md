# H3 No strings attached
Kosti Kangasmaa 07/09/2025
## Ympäristö
- Windows 11 PC
- VMware Workstation Pro 17
- [Kali Linux VMware image](https://www.kali.org/get-kali/#kali-virtual-machines)
- Memory - 2 GB
- Processors - 4
- Hard Disk - 80 GB
- Network - NAT
## A) Strings
### Tehtävän alustus
```bash
curl -O https://terokarvinen.com/loota/yctjx7/ezbin-challenges.zip
```
```bash
unzip ezbin-challenges.zip
cd challenges/passtr
```
### Ratkaisu
- Ajoin ohjelman ja kokeilin sitä
```bash
./passtr
```
![passtr1](/kuvat/passtr-2.png)
 - Seuraavaksi lähdin tutkimaan ohjelmaa strings ohjelman avulla
```bash
strings passtr
```
![passtr2](/kuvat/passtr-1.png)
 - stringssin avulla paljastui kaikki stringit mitä ohjelma tulostaa.
- Ajoin ohjelman uudestaan ja kokeilin eri stringejä.
```bash
./passtr
```
![passtr3](/kuvat/passtr-3.png)
## B) passtr.c korjaus
- Jotta sain piilotettua stringit päädyin käyttämään menetelmää missä stringit kootaan ohjelman ollessa käynnissä
- Obfuskoin stringit kirjainten ASCII koodien avulla luomalla jokaista tulostetta varten arrayn, joka sisälsi koodit. Tähän käytin github copilottia avuksi
- Käytin [strcmp](https://www.geeksforgeeks.org/c/strcmp-in-c/) funktiota if-lauseessa; toimintatapa ei ollut minulle entuudestaan tuttu.

![fpasstr1](/kuvat/f-passtr-1.png)
## C) packd
## Lähteet:
https://www.geeksforgeeks.org/c/strcmp-in-c/
