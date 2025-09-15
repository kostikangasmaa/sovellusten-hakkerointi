# H4 Kääntöpaikka
Kosti Kangasmaa 15/09/2025
## Ympäristö
- Windows 11 PC
- VMware Workstation Pro 17
- [Kali Linux VMware image](https://www.kali.org/get-kali/#kali-virtual-machines)
- Memory - 2 GB
- Processors - 4
- Hard Disk - 80 GB
- Network - NAT
## x)
 Hammond kävi videossa ["Ghidra for reverce engineering (PicoCTF) 2022 #42 bbbloat"](https://www.youtube.com/watch?v=oTD_ki86c9I) läpi yksinkertaisesti ghidran asentamisen ja sen käyttöä
## a) Ghidran asennus
- Asensin ghidran apt-getin avulla
```bash
sudo apt-get update
sudo apt-get install ghidra
```
## b) Rever-C

### Tehtävän Ratkaisu
- käynnistin ghidran
```bash
ghidra
```
- Loin uuden projektin ghidrassa

![ghidra1](/kuvat/h4/ghidra1.png)

- Seuraavaksi Importtasin tehtävään tarvittavan packd ohjelman

![ghidra3](/kuvat/h4/ghidra3.png)

![ghidra2](/kuvat/h4/ghidra4.png)

- tämän jälkeen avasin packd tehtävän ghidran codebrowserilla

![ghidra4](/kuvat/h4/ghidra2.png)

 - Avattua packd ghidra kysyi analysoidaanko packd 
 - Valitsin kaikki perusvalinnat
 - Jonka jälkeen avasin Pseudo-C decompilerin 

 ```
 Ctrl+E
 ```

![reverC-1](/kuvat/h4/rever-c1.png)

 - Löydettyäni main Function nimesin muuttujat selventämään ohjelmaa
 - Käynnistyessä ohjelma printtaa (puts) "Whats's the password?"
 - Tämän jälkeen ohjelma jää odottamaan syötettä käyttäjältä terminaaliin
 - Kun ohjelma saa inputin se määrittää password int muuttujan arvon vertailemalla inputin stringiä "piilos-AnAnAs" stringiin
 - Tämän jälkeen ohjelma toimii if-lauseen ehdoin ja tulostaa salasanan jos password muuttujan arvo on 0
## c) Jos väärinpäin
### Tehtävän Alustus
- Importtasin passtr ohjelman ghidra projektiin
- Avasin ghidran codebrowserilla ohjelman
### Tehtävän Ratkaisu
- Etsin binääristä main funktion
- Avasin Pseudo-C decompilerin
```bash
Ctrl+E
```
- Tämän jälkeen ajattelin, että kääntämällä if-lauseen toiminnan saan ratkaistua tehtävän
- Maalaamalla decompileristä highlighttaantuu binäärin ohjeistus binäärin katselmointi-ikkunassa
- Lähdin googlaamaan JNZ ohjeistusta ja löysin wikipedian artikkelin [branch (computer science)](https://en.wikipedia.org/wiki/Branch_(computer_science)), jossa käydään läpi branch, jump ja transfer toimintoja
- Artikkelista opin että JNZ (Jump if not zero) vastakohta on JZ(jump if zero)
- Tämän jälkeen lähdin selvittämään miten ohjeistuksia voidaan muuttaa ghidrassa.
- Toimin artikkelin [Ghidra 101: Binary patching](https://www.tripwire.com/state-of-security/ghidra-101-binary-patching)

![passtr1](/kuvat/h4/passtr3.png)

- Oikealla clikillä etsin Patch Instruction toiminnon

![passtr2](/kuvat/h4/passtr4.png)

 - Tämän jälkeen muutin ohjeistuksen JZ jonka jälkeen näin Decompilerissä miten if-lauseen tulosteet ovat vaihtaneet paikkaa

![passtr3](/kuvat/h4/passtr5.png)

- Tämän jälkeen yritin exportata ohjelmaa binäärinä ja c kielellä, mutta valitettavasti en saanut ohjelmaa toimimaan ilman kaatumista

### Latefix
- Opin Jälkikäteen kanssaopiskelijan [läksyistä](https://github.com/snorhh/hack_public/blob/main/julk_viikko4_teht.md) miten exportataan oikein.
- Eli ohjelma tuli exportata original file muodossa
- Kävin vielä kokeilemassa, saisinko ohjelman toimimaan oikein
![passtr666](/kuvat/h4/passtr666.png)

- Jee :)
## d) Crackme tehtävien lataus ja alustus
- Avasin  Tindall 2023: NoraCodes / crackmes [tehtävärepositorion](https://github.com/NoraCodes/crackmes) selaimessa ja luin README.md:n
- Latasin repon sisällön zippinä ja purin tiedostot unzip komennolla
## e) crackme01
### Tehtävän alustus
- Navigoin tehtävien kansioon ja alustin tehtävän makella
```bash
cd crackmes-master
make crackme01
```
### Tehtävän ratkaisu 
- Aloitin binäärin katselmoinnin ihan stringssin avulla ja sieltähän ratkaisu löytyi
```bash
strings crackme01.64
```
![crack1](/kuvat/h4/crack1-1.png)
![crack1](/kuvat/h4/crack1-2.png)
## f) crackme01e
### Tehtävän alustus
- Alustin tehtävän
```bash
make crackme01e
```
### Tehtävän ratkaisu
Vastaus löytyi samalla tavalla kuin edellisessä
```bash
strings crackme01e.64
```
![crack1e](/kuvat/h4/crack1e-1.png)
![crack1e](/kuvat/h4/crack1e-2.png)
## g) crackme02
### Tehtävän alustus
- Alustin tehtävän
```bash
make crackme02
```
### Tehtävän ratkaisu
 - Aloitin tehtävän ratkaisun katselmoimalla koodia ja määrittämällä argc(argument count) jonka määrän ohjelma tarkastaa
 ```bash
 ./crackme02.64 kosti
 ```
 - **argc** = 2
 - Sekä nimeämällä argv (argument value) tässä tapauksessa main funktio käyttää vain argv[1] koska se tarkastaa ettei argumentteja ole muuta määrää kuin 2
 - Päättelin ensimmäiseksi indeksimuuttujan ohjelmasta ja nimesin sen uudestaan

![crackme2](/kuvat/h4/crackme2-1.png)

 - Tämän jälkeen kiinnitin huomiota riville kaksikymmentä huomasin että stringiä "password1" käsiteltiin listana [indeksimuutuja+1] avulla ja täten päättelin että char muuttuja oli tarkistuskirjain[i]
 - Jonka jälkeen pystyin heti päättelemään viimeisen muuttuja jonka oli oltava argv[1]:n syötteenkirjain[i]

![crackme2](/kuvat/h4/crackme2-2.png)
### Ohjelman toiminnan läpikäynti riveittäin
- 2  Main funktion importit (argc ja argv(annettu syöte eli salasana))
- 5  Määritetään muuttuja tarkistuskirjain[i]
- 6  Ohjelman main fuktion return muuttuja
- 7  Määritetään Indeksimuuttuja
- 8  Määritetään muuttuja syötteenkirjain[i]
- 10 If-lause missä varmistetaan että ohjelma vastaanottaa tasan 2 syötettä käynnistettäessä eli käynnistyskehotteen ja yhden syötteen
- 11 Ohelma alustaa tarkistuskirjain muuttujan stringilä "p"
- 12 indeksimuuttuja määritetään nollaksi
- 13 while loopin alustus
- 14 Ohjelma asettaa syötteenkirjain[i] muuttujaan argv
- 15 Rivillä tarkistetään onko syötteenkirjain "tyhjä" jos niin looppi katkeaa
- 16 if-lause jossa tarkistetaan vastaako syötteenkirjain sen hetkistä tarkistuskirjainta josta on miinustettu 1
- 17 Tulostus jos if-lause toteutuu
- 20 Ohjelma asettaa tarkistuskirjain[i] muuttujan arvoksi seuraavan kirjaimen "password1"
- 21 indeksimuuttujaan lisätään 1
- 22 kun tarkistuskirjain on saavuttanut loopissa tyhjän arvon 
- 23 ohjelma tulostaa oikean vastauksen
- 24 return arvoksi asetetaan 0 
- 26 else joka on sidottu riviin 10 tämä toteutuu kun syötteitä on enemmän tai vähemmän kuin 2
- 30 ohjelma palauttaa return muuttujan arvon  

### Ohjelman toiminnan päättely ja lopullinen ratkaisu
- rivillä 16 ohjelma miinustaa 1 numeraalisesti yhden kirjaimen stringistä eli konekielen ASCII arvosta
- Eli ohjelma toimii koko while loopin aikana näin 
- 'p' → 'o'
- 'a' → '`'
- 's' → 'r'
- 's' → 'r'
- 'w' → 'v'
- 'o' → 'n'
- 'r' → 'q'
- 'd' → 'c'
- '1' → '0'

Täten todellinen stringi mitä tarkistetaan on:
```bash
o`rrvnqc0
```
- Koitin syötettä

![crackme2](/kuvat/h4/crackme2-3.png)

- Lisätään backquote että saadaan lähettyä stringi oikein.

```bash
o\`rrvnqc0
```

![crackme2](/kuvat/h4/crackme2-4.png)

## Lähteet
1. Hammond. "Ghidra for reverce engineering (PicoCTF) 2022 #42 bbbloat". Katsottavissa: https://www.youtube.com/watch?v=oTD_ki86c9I
2. Kali Linux VMware image. Luettavissa: https://www.kali.org/get-kali/#kali-virtual-machines
3. NoraCodes / crackmes. Luettavissa: https://github.com/NoraCodes/crackmes
4. branch (computer science). Luettavissa: https://en.wikipedia.org/wiki/Branch_(computer_science)
5. Tripwire. Ghidra 101: Binary patching. Luettavissa: https://www.tripwire.com/state-of-security/ghidra-101-binary-patching