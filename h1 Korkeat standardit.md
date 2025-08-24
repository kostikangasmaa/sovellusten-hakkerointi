SFS-EN ISO/IEC 27000:2020:en standardissa käytetyt termit.
Effectiveness 3.2
Tällä kuvataan dokumentissa suunniteltujen toimenpiteiden realisointia ja suunniteltujen vaatimusten täyttymystä.
Information security incident 3.31
On yksittäinen tai sarja epähaluttuja tai odottomattomia tietoturva tapahtumia, joilla on korkea todennäköisyys aiheuttaa vakvaa liiketoiminnalista tai tietoturva haittaa.  
Requirement  3.56
Vaatimus, joka on tarve tai odotus joka tulee täyttää osapuolien toimesta.
 Review 3.58
Arvio, joka on toimi missä määritetään kohteen soveltuvuus, sopivuus ja tehokkuus saavuttakseen tahdottu toimi.
 Vulnerability 3.77
Haavoittuvuus, eli omaisuuden tai riskiä kasvattavan toimen heikkous jota on mahdollista hyväksikäytää.

ISO 27034-1 – 5 Standard: Information technology — Security techniques ― Application security
Standardin tarkoituksena on opastaa organisaatioita integroimaan tietoturvallisuutta saumattomasti läpi sovellusten elinkaaren tarjoamalla tietoturvaa edistäviä toimintatapoja, prosseja ja periaatteita. Standardi koostuu 5 osasta.
•	Overview and concepts
•	Organization normative Framework
•	Application security management process
•	Application security validation
•	Protocols and application security control data structure


Laatulöpinät 30: Tietoturvallisuus ohjelmistokehityksessä väittämät
1.	Mikään ohjelmisto ei ole täysin tietoturvallinen.
•	Samaa mieltä pitkälti puhujien kanssa + ohjelmiston kehittämisprosessissa on ollut aina ihmisiä mukana ja ihmiset ovat aina myös osana riskiä.
2.	Hallinnollinen tietoturva on teknisen tietoturvan onnistumisen edellytys.
•	Hallinnollinen tietoturva on mielestäni juurikin osana todellista tietoturvaa laajemmin.
3.	Automaatiotestaus on ohjelmiston tietoturvan kannalta erittäin tärkeää.
•	Vahvasti samaa mieltä puhujien kanssa, varsinkin siitä miten automaatiotestaus vie paljon resursseja ja se miten kehittäjen pitää ymmärtää automaatiotestauksen sisältö ja ylläpidon tärkeys.
4.	Ohjelmistoa suunniteltaessa voidaan tehdä paljonkin auttamaan käyttäjää toimimaan tietoturvallisesti. Usein nämä toimenpiteet kuitenkin vaikuttavat negatiivisesti käytettävyyteen.
•	Mielestäni nosto siitä miten tietoturvallisuutta edistävä suunnittelu userstoryen kautta on paras toimintatapa oli hyvä näkemys.
5.	Ohjelmiston tietoturvallisuuden suunnitteluun vaikuttaa paljolti se, kuinka arkaluonteisia tietoja ohjelmistolla on tarkoitus käsitellä.
•	Väittämä ei myöskään kata yhteiskunnallisesti kriittisten toimintojen turvaamista kuten esimerkiksi sähköntuotanto.
6.	Ohjelmistokehittäjät näkevät omat ohjelmistonsa aina merkittävästi riskialttiimpina, kuin muiden tekemät ohjelmistot.
•	Väittämä resonoi vahvasti tällähetkellä varsinkin, koska oma osaaminen tietoturvan saralla on vielä vajaavainen.
(https://www.arter.fi/podcast/laatulopinat-podcast-tietoturvallisuus-ohjelmistokehityksessa-tarkastele-kokonaisuutta-ja-hyodynna-viitekehykset/)


Riskienhallintasuunnitelma
Ympäristön kuvaus
Ympäristö koostuu host windows tietokoneestani, jossa ajetaan Vmware workstation pro virtualisointiohjelmistoa, johon Kali linux asennetaan virtuaalikoneeseen.
Ympäritöön tunkeutumisen hallinta.
Varmentamalla kali linux image viralliseksi distroksi täten varmennutaan siitä ettei itse käyttöjärjestelmän mukana tule haittaohjelmia jo ennen virtuaalikoneen asentamista ympäristöön (https://www.kali.org/docs/introduction/download-official-kali-linux-images/). Ulkopuolisten tunkeutumista estetään asentamalla palomuuri virtuaalikoneeseen ja toteuttamalla verkkoyhteyksien eristystä virtualisointiohjelmistosta.
Haittaohjelmien eristys ympäristössä
Riskiä hallitaan eristämällä ympäristö tutkimisen ajaksi ottamalla snapshot virtuaalikoneesta ennen toimien aloittamista ja varmistamalla ettei, virtuaalikoneella ja host koneella ole jaettua verkkoa , kansioita tai laitteita. Tutkimisen jälkeen palautetaan virtuaalikone snapshotin avulla tiedetysti turvalliseen tilaan.

 
