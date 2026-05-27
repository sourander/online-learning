# 2B: FlowerModel

Vaihe 2B jatkaa vaihetta 2A siten, että teet sinun oman toteutuksesi opettajan mallin pohjalta. Käytettävä koneoppimismalli on kuitenkin suurempi ja toiminnaltaan hieman eri sorttia: käyttäjä ei piirrä mitään vaan lähettää kuvan. Tämä aiheuttaa muutoksia koko arkkitehtuuriin.

* Käyttöliittymä: kuinka käyttäjä lataa kuvan
* Blob Queue: mitä queueen tallennetaan? Koko kuva tuskin mahtuu.
* Backendiin: kuinka inferenssi ajetaan?

## Vinkkejä

### Debug-työkaluja

#### Docker (Desktop)

Voit avata konttien lokaalisti ajettavien serviceiden lokit joko Docker Compose -käskyillä CLI:stä tai Docker Desktopin graafisesta käyttöliittymästä. CLI:ssä se hoituu näin, olettaen että halutun servicen nimi on `foobar`:

```bash
docker compose logs foobar -f
```

Perässä oleva `-f` tarkoittaa, että lokit jatkuvat reaaliaikaisesti. Voit lopettaa lokien seuraamisen painamalla `Ctrl+C`.

#### Azure Storage Explorer

Voit varmistaa tällä työkalulla, että oikea malli löytyy Azure Blog Storagesta ja että jonoon menee tavaraa. Työkalu toimii niin Azuriten kuin oikean Azuren kanssa.

#### Print

Vanha kunnon printtaus pettää harvoin. 

* Kenties sinun frontend voi tulostaa tietoja käyttäjälle asti?
* Kenties backend voi tulostaa lähes kaiken mitä tekee?
 
Azuressa ajettavien konttien viestejä ei näy tietenkään Docker Compose -komentojen avulla, koska kontit pyörivät pilvessä. Olettaen että kontti ei kaadu aivan välittömästi vaan tulostaa kiltisti tavaraa, niin voit kuitenkin seurata myös tätä fiidiä! Voit varmistaa, että kontti ei kaadu käyttämällä `try-except` blokkeja Pythonissa. Lyhyimmillään pääset kiinnittymään `stdout` ja `stderr` striimeihin näin:

```bash
az container attach --resource-group myResourceGroup --name mycontainer
```

Tarkemmat ohjeet: [Retrieve container logs and events in Azure Container Instances](https://learn.microsoft.com/en-us/azure/container-instances/container-instances-get-logs)

### Työskentelyvinkkejä

* Muuta yhtä asiaa kerrallaan. 
* Tee `git commit` vain toimivissa väleissä mutta silti usein! 
* Kirjoita järkevät `git commit`-viestit, jotta voit tarpeen mukaan kelata taaksepäin.
* Kysy tekoälyltä vinkkejä. 
    * Älä syötä sille koko koodia vaan muotoile hyvä, rajattu kysymys.
    * Joskus huomaat, että kysymystä laatiessa ongelma ratkeaa itsestään, kun huomaat itse vian.
* Tee kehitystyö omalla koneellasi äläkä Azuressa. Tämä nopeuttaa.
 
!!! tip

    Koeponnista servicet Azuressa sitä mukaan kun olet varmentanut niiden toiminnan lokaalisti. Tämä auttaa välttämään mahdolliset ympäristön aiheuttamat ongelmat. Niitä on inha korjata, jos ongelmia on päässyt kasautumaan. [Fail fast!](https://medium.com/@denhox/the-benefits-of-fail-fast-systems-dc72a665cfb5)-metodologia käyttöön!


### Arkkitehtuurisia vinkkejä

* Voit tallentaa jonon kuvat Azure Blob Storageen ja lähettää jonoon vain blobin nimen ja labelin. Näin vältyt jonon asettamilta rajoituksilta messagen maksimikokoon liittyen.
* Flowerfinetune-kontti tuskin pärjää vakio 1G muistin kanssa. Kannattaa kokeilla nostaa sen muistin määrää.
* Jos debuggauksesta haluaa tehdä superhelppoa, niin kannattaa kylvää esim. `logging.debug()`-kutsua pitkin poikin koodia lokkaamaan aivan liiallisen määrän tietoa. Se, haluaako tätä nähdä vai ei, on togglettavissa päälle ja pois asettamalla `logging.basicConfig(level=logging.INFO)` tai  `...(...=logging.DEBUG)`

### Mallin tahallinen (tai tahaton) rikkominen

Mallin tahallinen (tai tahaton) rikkominen
Kurssin kohdan 2B mallilla voi testata, kuinka helppoa mallin toiminta on rikkoa tahallisesti tai tahattomasti. Tähän vaikuttaa mm. seuraavat seikat:

1. Fine tuning vaiheessa käytetty data 
    - On hyvä sisällyttää Fine tuning koulutukseen aina näytteitä alkuperäisestä datasta
    - On hyvä, että fine tuning data on käynyt läpi ihmisen tarkastuksen
2. Jos fine tuning opettaa vain osaa mallista (esim. luokittelijaa), malli ei yleensä juuri parane, mutta se on todella helppo rikkoa.   


Linkkejä:

* https://course.spacy.io/en/chapter4 -> Best practices for training spaCy models
* https://rekrytointi.talenom.fi/posts/ai-at-talenom-active-learning
