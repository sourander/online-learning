# 1B: ONNX Runtime Web

Vaiheessa 1B muokkaamme edellisen vaiheen (lesson_01 - Static Webpage) sitten, että saamme Blob Storagen staattisessa webbisivussa pyörimään **Syväoppiminen 2** -kurssin FlowerModel-harjoituksessa tehdyn verkkosivun, sisältäen javascript tiedoston (ONNX) ja koulutetut painot. Kyseessä on neuroverkko, joka tunnistaa 5 eri kukkalajia (`['daisy', 'dandelion', 'roses', 'sunflowers', 'tulips']`).

Koodin, jolla mallin saa koulutettua, löydät repositoriosta: [flower-model-demo](https://gitlab.dclabra.fi/jani-public/flower-model-demo).

## Ohjeet (TODO!)

1. Kopioi harjoituksen `www/`-hakemiston koodit ja malli siihen hakemistoon, missä työstät tätä `1B`-harjoitusta.
2. Muokkaa Terraform-koodia siten, että siinä kopioidaan kaikki tarvittavat tiedostot Azure Blob storageen.
3. Varmista, että nettisivu avautuu oikein ja että kukkien tunnistus toimii.

