# Analytiikkanäyttö Älykotiin - Mikrobitti 2/2020

Oheisesta repositoriosta löytyy vinkkejä helmikuun 2020 Mikrobitin 'Analytiikkanäyttö älykotiin' taikapeilinrakennusosioon. Tee-se-itse kotiautomaatiota -artikkelisarjan 3. osa.


## MagicMirror -taikapeilin rakennusvaiheet

Kuvitetut ohjeet itse taikapeilin kasaamiseen löydät Mikrobitistä 2/2020. Tällä sivulla tarkemmin vinkkejä peilin ohjelmistopuolen käyttöönottoon sekä hieman vinkkejä peilin kustomoimiseksi.


### Käyttöjärjestelmän asentaminen Raspberry Pi:lle

Mikäli kaivoit tuoreen Raspberry Pi:n suoraan naftaliinista, on siihen ensin asennettava käypä käyttöjärjestelmä. Tässä artikkelissa käytämme suosittua Raspbian -käyttöjärjestelmää. Oheisilla ohjeilla saat Raspin kehräämään! Alla olevat ohjeet mukailevat [tätä sivua](https://www.raspberrypi.org/documentation/installation/installing-images/).

1. Lataa `Raspbian Buster with desktop` -kuva osoitteesta [(https://www.raspberrypi.org/downloads/raspbian/](https://www.raspberrypi.org/downloads/raspbian/)

2. Lataa ja asenna balenaEtcher -ohjelma käyttöjärjestelmän muistikortille kirjoittamista varten osoitteesta [https://www.balena.io/etcher/](https://www.balena.io/etcher/)

3. Liitä micro-SD- muittikortti tietokoneeseen kiinni ja avaa balenaEtcher. Valitse .img -päätteinen Raspbian Buster -kuva latauskansiostasi (`Select image`) ja juuri kytkemäsi muistikortti (`Select drive`). Paina `Flash!` -nappia.

4. Siinäpä se! Laita muistikortti kiinni Raspberry Pihin. Kytke myös virtalähde, näyttö, näppäimistö ja hiiri, niin pääset alkuun!

5. Konfiguroi käyttöjärjestelmän asetukset mieluiseksesi Raspbianin käyttöönottovelhon (Setup Wizard) avulla. Sen pitäisi käynnistyä automaattisesti ensimmäisellä käynnistyskerralla.

Mikäli et ole aiemmin tutustunut Raspberry Pi:hin, suosittelen lämpimästi tutustumaan Raspberry Pi:n omaan, lempeään aloitussivuun: [Getting Started with Raspberry Pi](https://projects.raspberrypi.org/en/pathways/getting-started-with-raspberry-pi), ja selailemaan etenkin `Using your Raspberry Pi > Using the terminal` -osion läpi.

Varmistathan ennen MagicMirror2 -ohjelmiston asentamista, että internetyhteys toimii. Kytke siis joko verkkokaapeli Raspberry Pi:hin tai kliksuttele langattoman verkon asetukset kuntoon työpöydän oikeasta yläkulmasta.


### Näytön asetusten konfigurionti

Taikapeilinäytöstä voi olla enemmän hyötyä pystyasennossa. Näytön orientaation saa muutettua `/boot/config.txt` -tiedostosta. Avaa siis tiedosto rohkeasti tekstieditorissa kirjoittamalla komentoriville `sudo nano /boot/config.txt`. Kirjoita (tai muuta riviä) `display_rotate=1`. Tämä kiertää kuvaa 90 astetta. Vaihtoehtoisesti `display_rotate=3` voi toimia paremmin, mikäli kaikki näyttäisi olevan tyystin väärinpäin.

Tallenna asetustiedosto näppäinyhdistelmällä `Ctrl+x`. Käynnistä Raspberry Pi uudelleen komennolla `sudo reboot`.


### MagicMirror2 -ohjelmiston asentaminen Raspberry Pi:lle

MagicMirror -ohjelmisto kehittyy jatkuvasti, joten varmasti tuoreimmat asennus- ja konfigurointiohjeet löydät [docs.magicmirror.builders](https://docs.magicmirror.builders) -sivustolta.

---

**Vaihtoehto 1. asennusskripti**
Helpoimmalla pääset ajamalla sdteweil:in komentoriviasennusskriptin [täältä](https://github.com/sdetweil/MagicMirror_scripts).

Asennusskripti kysyy seuraavan kysymyksen asennuksen aikana: `Do you want use pm2 for auto starting of your MagicMirror (y/N)?`. YES.

Kirjoita vielä `pm2 save` tallentaaksesi asennusskriptin luomat MagicMirror -asetukset. Tätä en löytänyt tuoreimmasta skriptistä.
Käynnistä / sammuta ohjelmisto PM2:n kautta komentoriviltä komennoilla `pm2 start/restart/stop MagicMirror`.

**Vaihtoehto 2. manuaaliasennus**
Mikäli em. tapa aiheuttaa harmaita karvoja, kannattaa asennus suorittaa manuaalisesti magicmirror.buildersin [ohjeilla](https://docs.magicmirror.builders/getting-started/installation.html#manual-installation). Manuaaliasennus ei kuitenkaan ota kantaa automaattikäynnistykseen. Ohjeet sen käyttöönottoon [täällä](https://github.com/MichMich/MagicMirror/wiki/Auto-Starting-MagicMirror)

Käynnistä / sammuta ohjelmisto suoraan asennuskansiosta (`cd ~/MagicMirror`) komennolla `npm start`.
Mikäli seurasit automaattikäynnistyksen ohjeita, voit käyttää käynnistykseen suoraan työkalua PM2: `pm2 start/restart/stop MagicMirror`.

---

Lisäksi kannattaa seurata [näitä](https://github.com/MichMich/MagicMirror/wiki/Configuring-the-Raspberry-Pi) hyviksi havaittuja Raspberry Pi -spesifejä konfiguraatio-ohjeita ja niksejä muun muassa suoritinkäytön vähentämiseksi, näytön konfiguroimiseksi ja hiirenosoittimen piilottamiseksi.


### MagicMirror2 -ohjelmiston konfigurointi ja lisäosien asentaminen

MagicMirror2 -ohjelmisto on Node.js -pohjainen Electron -käyttöliittymäkehystä käyttävä web-ohjelma. Sen konfigurointi tapahtuu muokkaamalla `config.js` -tiedostoa, joka löytyy ohjelman asennuskansiosta (oletuksena `cd ~/MagicMirror/config/config.js`).

Listan asetuksista löydät [täältä](https://docs.magicmirror.builders/getting-started/configuration.html#general).


### Ulkoisten lisämoduulien asentaminen

MagicMirror2 -ohjelmisto on laajennettavissa lukuisin liitännäisin, eli moduulein. Jokainen taikapeilillä näkyvä kokonaisuus on todennäköisesti oma moduulinsa. Kaikki MagicMirro2 -ohjelmiston moduulita ovat erillisiä node.js -moduuleja, jotka asennetaan omaan kansioonsa `~/MagicMirror/modules/<moduuli>`. Moduulit otetaan käyttöön ja konfiguroidaan lisäämällä moduulikohtainen konfiguraatio-objekti `config.js`:n `modules` -listaan.

Kattavat ohjeet moduulien käyttämisestä löydät (docs.magicmirror.builders/modules)[https://docs.magicmirror.builders/modules/introduction.html] -sivuilta.


**Uusien moduulien käyttöönotto tapahtuu tyypillisesti kutakuinkin näin:**

1. Asenna moduuli, mikäli se on kolmannen osapuolen koodaama. Tarkemmat asennusohjeet tähän löytyy yleensä moduulin github-sivuilta, mutta useimmat noudattavat samaa kaavaa.
2. Navigoi moduulikansioon `cd ~/MagicMirror/modules`
3. Kloonaa moduulin koodi githubista `git clone git clone https://github.com/mymoduleauthor/MMM-mymodule.git`
4. Navigoin moduulin kansioon `cd MMM-mymodule`
5. Asenna riippuvuudet `npm install`
6. Konfiugroi ja ota moduuli käyttöön lisäämällä juuri asentamasi moduulin konfiguraatio-objekti `config.js`:n `modules` -listaan. Esimerkiksi Gedit-editorin avulla `gedit ~/MagicMirror/config/config.js`.

MagicMirror-tarjoaa helpohkon rajapinnan omien näyttömoduulien rakentamiseen, ja alan harrastajat ovatkin rakentaneet omiin peileihinsä aimo liudan erilaisia moduuleja ja integraatioita.

Muutaman manuaaliasennuksen jälkeen saatat haluta kokeilla [MagicMirror Package Manageria](https://github.com/Bee-Mar/mmpm) moduulien hallintaan.



