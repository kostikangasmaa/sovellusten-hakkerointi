# SFS-EN ISO/IEC 27000:2020:en standardissa käytetyt termit

**Effectiveness 3.2**  
Tällä kuvataan dokumentissa suunniteltujen toimenpiteiden realisointia ja suunniteltujen vaatimusten täyttymystä.

**Information security incident 3.31**  
On yksittäinen tai sarja epätoivottuja tai odottamattomia tietoturvatapahtumia, joilla on korkea todennäköisyys aiheuttaa vakavaa liiketoiminnallista tai tietoturvahaittaa.

**Requirement 3.56**  
Vaatimus, joka on tarve tai odotus, joka tulee täyttää osapuolten toimesta.

**Review 3.58**  
Arvio, joka on toimi, missä määritetään kohteen soveltuvuus, sopivuus ja tehokkuus saavuttaakseen tahdotun toimen.

**Vulnerability 3.77**  
Haavoittuvuus, eli omaisuuden tai riskiä kasvattavan toimen heikkous, jota on mahdollista hyväksikäyttää.

---

# ISO 27034-1 – 5 Standard: Information technology — Security techniques ― Application security

Standardin tarkoituksena on opastaa organisaatioita integroimaan tietoturvallisuutta saumattomasti läpi sovellusten elinkaaren tarjoamalla tietoturvaa edistäviä toimintatapoja, prosesseja ja periaatteita. Standardi koostuu 5 osasta:

1. **Overview and concepts**
2. **Organization normative framework**
3. **Application security management process**
4. **Application security validation**
5. **Protocols and application security control data structure**

---

# Laatulöpinät 30: Tietoturvallisuus ohjelmistokehityksessä – Väittämät

1. **Mikään ohjelmisto ei ole täysin tietoturvallinen.**  
   - Samaa mieltä puhujien kanssa. Ohjelmiston kehitysprosessissa on aina ihmisiä mukana, mikä tuo mukanaan riskejä.

2. **Hallinnollinen tietoturva on teknisen tietoturvan onnistumisen edellytys.**  
   - Hallinnollinen tietoturva on olennainen osa todellista tietoturvaa.

3. **Automaatiotestaus on ohjelmiston tietoturvan kannalta erittäin tärkeää.**  
   - Vahvasti samaa mieltä. Automaatiotestaus vie resursseja, ja kehittäjien tulee ymmärtää sen sisältö ja ylläpidon tärkeys.

4. **Ohjelmistoa suunniteltaessa voidaan tehdä paljonkin auttamaan käyttäjää toimimaan tietoturvallisesti. Usein nämä toimenpiteet kuitenkin vaikuttavat negatiivisesti käytettävyyteen.**  
   - Mielestäni user storyjen kautta tapahtuva tietoturvallisuuden suunnittelu on paras toimintatapa.

5. **Ohjelmiston tietoturvallisuuden suunnitteluun vaikuttaa paljolti se, kuinka arkaluonteisia tietoja ohjelmistolla on tarkoitus käsitellä.**  
   - Väittämä ei kata yhteiskunnallisesti kriittisten toimintojen, kuten sähköntuotannon, turvaamista.

6. **Ohjelmistokehittäjät näkevät omat ohjelmistonsa aina merkittävästi riskialttiimpina kuin muiden tekemät ohjelmistot.**  
   - Väittämä resonoi tällä hetkellä, koska oma osaaminen tietoturvasta on vielä kehittymässä.

---

# Riskienhallintasuunnitelma

## Ympäristön kuvaus

Ympäristö koostuu host Windows-tietokoneestani, jossa ajetaan VMware Workstation Pro -virtualisointiohjelmistoa. Kali Linux asennetaan virtuaalikoneeseen.

## Ympäristöön tunkeutumisen hallinta

- Varmistetaan, että Kali Linux -image on virallinen distro, jolloin käyttöjärjestelmän mukana ei tule haittaohjelmia jo ennen asennusta.
- Ulkopuolisten tunkeutumista estetään asentamalla palomuuri virtuaalikoneeseen ja eristämällä verkkoyhteyksiä virtualisointiohjelmistosta.

## Haittaohjelmien eristys ympäristössä

- Riskiä hallitaan eristämällä ympäristö tutkimisen ajaksi ottamalla snapshot virtuaalikoneesta ennen toimien aloittamista.
- Varmistetaan, ettei virtuaalikoneella ja host-koneella ole jaettua verkkoa, kansioita tai laitteita.
- Tutkimisen jälkeen palautetaan virtuaalikone snapshotin avulla tiedetysti turvalliseen tilaan.

---

# Lähteet

1. [Kali Linuxin viralliset image-tiedostot](https://www.kali.org/docs/introduction/download-official-kali-linux-images/)
2. [Arter Podcast – Laatulöpinät: Tietoturvallisuus ohjelmistokehityksessä](https://www.arter.fi/podcast/laatulopinat-podcast-tietoturvallisuus-ohjelmistokehityksessa-tarkastele-kokonaisuutta-ja-hyodynna-viitekehykset/)
