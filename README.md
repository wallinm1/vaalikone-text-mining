# vaalikone-text-mining
Tästä Github-repositorysta löytyy Jupyter notebook jossa tutkitaan Ylen vaalikoneen avoimien kysymyksien vastauksia ja tehdään tilastollista analyysiä sen pohjalta. Samalla tarkoituksena on kokeilla Pythonin text mining-ominaisuuksia suomen kielen analysoinnissa. Lisäksi päästään kokeilemaan Githubin uutta Jupyter-notebook-renderingiä.

## Data
Analyysin lähdedatana käytetään Ylen avoimeksi tekemää [Vaalikone-dataa](http://yle.fi/uutiset/yle_julkaisee_vaalikoneen_vastaukset_avoimena_datana/7869597).  Tästä datasta olen käyttänyt versiota joka löytyy [avoindata.fi-sivuilta](https://www.avoindata.fi/data/fi/dataset/eduskuntavaalien-2015-ylen-vaalikoneen-vastaukset-ja-ehdokkaiden-taustatiedot).

Avoindata.fi:n hostaamaan aineistoon on eksynyt yksi enkoodausvirhe joka pitää korjata käsin jotta .csv-tiedoston pystyy onnistuneesti lukemaan utf-8-enkoodauksella. SDP:n Raimo Piiraisen vastauksesta (vastausid 4798, rivi 1358) pitää poistaa merkki 伋 joka löytyy aika loppupuolelta Piiraisen vastauksia (tekstinpätkän `vaan ilmastonmuutoksen hyväksi on työskenneltävä pitkällä aikavälillä` jälkeen ja ennen pätkää `Nykyisille periaateluvan saanneille ydinvoimaloille`). Kun tämä virhe on korjattu, sijoita .csv-tiedosto nimellä `vaalikone_data_fix.csv` data-kansioon.

## Kirjastot ja muut vaatimukset
Notebookissa kutsutaan R:n `ggplot2`-kirjastoa ipythonista käsin joten R:n ja `ggplot2`-kirjaston pitää olla asennettuna.

Notebookissa käytetään muutamia kirjastoa jotka eivät kuulu Pythonin standardikirjastoihin: `pandas`, `scikit-learn`, `numpy`, `langdetect`, `nltk`, `seaborn`, `matplotlib` ja `rpy2`. Lisäksi Jupyter-notebookin ajamiseen tarvitaan `ipython`-kirjasto. Ehkä helpoin tapa asentaa tarvittavat python-kirjastot on [Anaconda-distron](http://continuum.io/downloads) kautta. Tuo distro sisältää itsessään jo `pandas`-, `scikit-learn`-, `numpy`-, `nltk`-, `matplotlib`- ja `ipython`-kirjastot. Kirjastot `langdetect` ja `seaborn` voi asentaa komennoilla `pip install langdetect` ja `pip install seaborn`. Linuxilla myös `rpy2`-kirjaston voi asentaa helposti komennolla `pip install rpy2`. Windowsilla `rpy2`-kirjaston asentaminen on jokseenkin hankalaa. Vinkkejä tuohon löytää mm. [täältä](http://stackoverflow.com/questions/11165123/install-rpy2-on-windows7-64bit-for-python-2-7), [täältä](http://stackoverflow.com/questions/14882477/rpy2-install-on-windows-7) ja [täältä](http://eurekastatistics.com/installing-rpy2).

Kun kaikki kirjastot on asennettu, pitää vielä ladata nltk:ssa suomen ja ruotsin kielen "stopwords"-listat. Nämä voi esimerkiksi ladata ajamalla python-interpreterissä `nltk.download()`-komento ja sitten valitsemalla `all corpora` nltk:n lataus-GUIssa.


