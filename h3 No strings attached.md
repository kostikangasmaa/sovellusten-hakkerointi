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
- Obfuskoin stringit kirjainten ASCII koodien avulla luomalla jokaista tulostetta varten arrayn, joka sisälsi koodit. Tähän käytin github [copilottia](https://github.com/copilot) avuksi
- Käytin [strcmp](https://www.geeksforgeeks.org/c/strcmp-in-c/) funktiota if-lauseessa; toimintatapa ei ollut minulle entuudestaan tuttu.

![fpasstr1](/kuvat/f-passtr-1.png)
- Seuraavaksi käänsin koodin README:n ohjeiden mukaisesti 
```bash
make 
```
- Tämän jälkeen testasin stringien piilottamisen stringssin avulla

![fpasstr2](/kuvat/f-passtr-2.png)

- Sekä ohjelman toiminan

![fpasstr3](/kuvat/f-passtr-3.png)
## C) packd
### Tehtävän alustus
```bash
cd challenges/packd
```
### Tehtävän ratkaisu
 - Aloitin tutkimisen strings ohjelman avulla
 ```bash
 strings packd
 ```

![packd1](/kuvat/packd-1.png)

- Katselmoinnista huomasin että myös tällä kertaa salasana oli näkyvissä, testasin sen toiminan.
- Salasana ei ollut oikea, joten palasin stringsin avulla ohjelman katselmointiin, jonka jälkeen huomasin rivin jossa, luki "$Info: This file is packed with the UPX executable packer".
- Myös ensimmäisellä rivillä luki wUPX!
- kokeilin...
```bash
upx
```
![packd2](/kuvat/packd-2.png)
- Komennolla -d pystyi purkamaan upx:llä pakatun tiedoston.
```bash
upx -d packd
```
- Katselmoin ohjelmaa uudestaan purun jälkeen

```bash
strings packd
```
![packd3](/kuvat/packd-3.png)
- stringsin tulosteet olivat muuttuneet
- Testasin vielä "salasanan" toiminan
```bash
./packd
```
![packd4](/kuvat/packd-4.png)

## Lähteet
1. GeeksforGeeks. strcmp in C. Luettavissa: https://www.geeksforgeeks.org/c/strcmp-in-c/
2. GitHub Copilot. Luettavissa: https://github.com/copilot
3. Kali Linux VMware image. Luettavissa: https://www.kali.org/get-kali/#kali-virtual-machine
4. Tero Karvinen. Sovellusten hakkerointi. Luettavissa: https://terokarvinen.com/sovellusten-hakkerointi/
