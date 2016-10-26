# Hadoop_harkkatyo

# 2.4.	Ensimmäinen harjoitus Apache Hadoop –järjestelmällä: wordcount
Ensimmäisenä harjoituksena tehdään Hadoop:lla sanojenlaskentaohjelma; ohje siihen löytyy alle linkatusta paikasta ja sitä noudatetaan soveltaen kun emme vielä käytä Hadoop:in hajautettua tietojenkäsittelymallia. Poikkeamat linkin ohjeista löydät linkin jälkeen kirjoitetussa tekstissä.
https://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html#Example:_WordCount_v1.0
Ohjelmaa ajetaan Hadoop:in local-standalone –moodissa. Tarkemmat ohjeet tähän ovat seuraavat:
1.	Huolehdi siitä, että pseudo distributed mode:n kaikki Apache Hadoop:iin liittyvät taustaprosessit ovat pois ajosta. Tilanteen pitäisi olla alkuvaiheessa tällainen. Saat prosessit pois ajosta komennoilla:
stop-dfs.sh
ja
stop-yarn.sh
Aja nämä komennot tarvittaessa hadoop-tunnuksella (jonka teit edellä).
2.	Huolehdi siitä, että kansiossa /usr/local/hadoop/etc/hadoop tiedostojen mapred-site.xml, hdfs-site.xml, core-site.xml ja yarn-site.xml sisällöt ovat ne, mitkä löydät tabulasta kohdan standalone settings alta. Sisällöt estävät Hadoop:in hajautetun moodin käytön koska haluamme käyttää paikallista tiedostojärjestelmää (yksinkertaisin mahdollinen Hadoop-kokoonpano).
3.	Tee hadoop:in kotihakemistoon hakemisto input sekä kopioi sinne tabulassa tämän dokumentin alle julkaistut tekstitiedostot LICENSE.txt,  NOTICE.txt  ja README.txt.
4.	Pidä huoli, että samassa kotihakemistossa ei ole hakemistoa output. Poista se jos on (jos ko. hakemistossa on arvokasta dataa ota hakemistosta ensin varmistus).
5.	Aja komento:
hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar  wordcount input output
hadoop-käyttäjän kotihakemistossa. Komento “kaivaa” .jar-tiedostosta valmiiksi käännetyn wordcount-ohjelman, joka lukee input-hakemistosta sinne viemäsi tiedostot ja tekee niille analyysin output-hakemistoon.
Tässä vaiheessa seisahdu hetkeksi ja tutki seuraavia asioita. Kirjoita tutkimustesi tulokset työstä vaadittavaan raporttiin.
•	Mikäli linkissä kerrotussa työohjeessa tai yllä kerrotuissa ohjeissa on sinulle ennestään tuntemattomia komentoja selvitä Internet:in eri lähteitä käyttämällä mitä ne tekevät ja mikä on niiden pääidea. Kirjoita nämä tiedot raporttiin.
•	Miten wordcount-ohjelma on ohjelmoitu? Löydät lähdekoodin hadoop-2.7.2.tar.gz -tiedoston sisältä alihakemistosta hadoop/share/hadoop/mapreduce/sources paikasta hadoop-mapreduce-examples-2.7.2-sources.jar. jar-komennolla voit purkaa lähdekoodin kyseisen tiedoston sisältä (käyttöohje: lue man jar Linux:in shell-istunnossa). Tee ohjelmakoodin rakenteesta lyhyt kuvaus tästä työstä tehtävään raporttiin. Selitä karkealla tasolla koodin toiminta.
•	Miten ohjelma käsittelee syötteensä?
•	Mikä on ohjelman ajon tulos ? Miten ohjelma toteuttaa toiminnassaan MapReduce-paradigmaa ?
•	Voisiko tuloksia millään lailla parantaa informaation häviämättä ?
•	Mikä on ohjelman työnjako siinä mielessä että mitä asioita käsitellään oman koodisi puolella ja mitä asioita käsitellään kehyksessä (Hadoop-järjestelmässä) ?
•	Esimerkkiä ajetaan paikallisessa tiedostojärjestelmässä. Miten Hadoop organisoi datan sijoittelun ja prosessien ajon jos ohjelmaa ajettaisiin aidosti hajautetussa moodissa ? Esimerkiksi lähde http://www.ibm.com/developerworks/library/l-hadoop-2/ käsittelee tätä asiaa. Samoin lähde http://bradhedlund.s3.amazonaws.com/2011/hadoop-network-intro/Understanding_Hadoop_Clusters_and_the_Network-slides_and_text_bradhedlund_com.pdf .
•	Palauta myös kaikki tekemäsi lähdekoodit sekä erillisinä tiedostoina (siten että niistä saa testauksessa helposti kasaan toimivan ohjelman) että kirjoitetun raportin liitteinä. Raporttiin pitää myös oheistaa todisteet siitä, että annetuilla syötteilla ohjelma tuottaa oikean tuloksen (sisällytä raporttiisi vaikka ohjelman tulosteet näytönkuvina).

# 2.5.	Toinen harjoitus Apache Hadoop –järjestelmällä: sähkön kulutus
Tehdään seuraavaksi sivustolla http://www.tutorialspoint.com/hadoop/hadoop_mapreduce.htm esitelty sähkönkulutuksen laskentaohjelma jälleen local-moodissa. Tällä harjoituksella lähestymme lopullista tavoitetta eli kykyä tehdä alusta asti itse MapReduce-arkkitehtuuria noudattava ohjelma ennalta speksatun tiedon käsittelemiseksi.
Huom: ohje on kirjoitettu ohjelman ajamiseen pseudo distributed –moodissa. Meille riittää tässä vielä local-moodin käyttö eli sovella ohjeita (= toimi edellisen wordcount-harjoituksen tavalla). Alla huomioita tekemisestä:
•	Syötetiedoston sisältö kannattaa kopioida sivustolta http://www.tutorialspoint.com/hadoop/hadoop_mapreduce.htm kuitenkin niin, että vaihdat editorilla kaikki välilyöntejä sisältävät pätkät yhdeksi tabulaattorimerkiksi. Ohjelmakoodi edellyttää tämän. Vaihtoehtona on tietenkin sallia ohjelmakoodissa että tiedoston rivin kenttäerottimina toimivat sekä tabulaattorimerkit että välilyöntimerkit ja tämäkin on helposti tehtävissä.
•	Lataa kirjasto hadoop-core-1.2.1.jar hadoop käyttäjän kotihakemistoon ohjeen http://www.tutorialspoint.com/hadoop/hadoop_mapreduce.htm ”Step 2”:n mukaisesti.
•	Editoi tiedostoon ProcessUnits.java sisällöksi sivuston http://www.tutorialspoint.com/hadoop/hadoop_mapreduce.htm kohdassa Example Program oleva lähdekoodi. Tämä tiedosto tulee sijoittaa hadoop-käyttäjän kotihakemistoon.
•	Ohjelmakoodisi ajon voit tehdä tämän jälkeen seuraavasti:
cd ~hadoop
mkdir units
javac -classpath hadoop-core-1.2.1.jar -d units ProcessUnits.java
jar -cvf units.jar -C units/ .
rm -rf output
hadoop jar units.jar hadoop.ProcessUnits input output

Vinkki: edellisistä komennoista kannattaa tehdä pieni shell-skripti tai make-työkalun välityksellä ajettava toiminto koska on todennäköistä että virheiden sattuessa joudut suorittamaan sitä uudestaan ja uudestaan. Tällöin ei ole mielekästä kirjoittaa uudestaan kuuden komennon sarjaa. 
Kirjaa jälleen tästä harjoituksesta tekemäsi havainnot ja oppimisesi raporttiin. Kirjaa esim. seuraavat asiat:
•	Mikä on ohjelmassa käytetty avain syöttötiedoille ? Entä tulostiedoille ?
•	Mitkä vastaavasti ovat arvoja syöttötiedoille ja tulostiedoille ?
•	Miten map()-metodissa hoidetaan tiedon tiivistäminen ja sen eteenpäin lähettäminen ?
•	Mikä näyttäisi olevan reduce() –metodin päätehtävä ?
•	Kuvaa tehdyn pääohjelman keskeiset tehtävät.
•	Tehdyt lähdekoodit palautetaan samalla tavoin kuin edellisessä tehtävässä tehtiin.

# 2.6.	Kolmas harjoitus Apache Hadoop –järjestelmällä: ulkolämpötila
Tässä harjoituksessa on tarkoitus tehdä itse alusta loppuun Big Dataa käsittelevä ohjelma Apache Hadoop –järjestelmää käyttäen. Mallia tekemiseen kannattaa kuitenkin ottaa kahdesta edellisestä harjoituksesta jotta kaikkia asioita ei tarvitse selvittää uudestaan nollapisteestä lähtien. Tässä harjoituksessa tehtävää ohjelmaa on tarkoitus ajaa Pseudo Distributed –moodissa jotta pääsemme tutustumaan Hadoop:in taustaprosessien ajamiseen ja käyttäytymiseen.
2.6.1	Kolmannessa tehtävässä tehtävän ohjelman speksi
Tee ohjelma, joka käsittelee alla kerrotussa formaatissa olevan ulkolämpötila-aineiston ja tuottaa siitä vuorokauden keskilämpötiladatan.
Syöttötiedoston muoto on seuraava (sisältö on vain esimerkki):
25022016 00:00:00 -10.3
25022016 00:01:00 -10.3
25022016 00:02:00 -10.3
25022016 00:03:00 -10.3
25022016 00:04:00 -10.3 
…
Tuloksen muoto on seuraava (datasisältö vain esimerkki):
25022016	-9.78
# 2.6.2	Tarkemmat ohjeet kolmannen tehtävät tekoon
Tarkemmat ohjeet tehtävän tekemiseen ovat alla:
1.	Konfiguroi Hadoop:in pseudo distributed –moodi päälle sivuston http://www.tutorialspoint.com/hadoop/hadoop_mapreduce.htm ohjeen Compilation and Execution of Process Units Program sekä sivuston http://www.tutorialspoint.com/hadoop/hadoop_enviornment_setup.htm ohjeen Installing Hadoop in Pseudo Distributed Mode mukaisesti. Huomioi kuitenkin alla kerrotut poikkeukset.
Ohjeessa kerrotussa core-site.xml –tiedostossa on painovirhe, sen tulee sisältää rivi:
<value>hdfs://localhost:9000</value>
ohjeessa kerrotun rivin sijaan. Ohjeen rivillä on yksi välilyönti liikaa 9000:n perässä.
Ohjeessa kerrotussa hdfs-site.xml –tiedostossa hadoop-käyttäjän kotihakemisto pitää antaa muodossa /user/hadoop /home/hadoop:in sijaan.
Komento hdfs namenode –format kysyy tietyssä vaiheessa (Y or N) –kysymyksen; vastaa tähän Y (iso Y).
Komento start-dfs.sh saattaa kysyä toistamiseen hadoop-käyttäjän salasanaa. Anna silloin tämä. Voit tutkia nettilähteistä saisiko tämän ominaisuuden kierrettyä (salasanaa ei kysytä).
Kun kyseessä on avoimen lähdekoodin tuote siinä on ohjelmointivirheitä. Eräs ohjeen noudattamisen seurauksena syntyvä virhe on seuraava:
Tiedostossa ~/hadoopinfra/hdfs/datanode/current/VERSION tiedon clusterID sisältö on väärä. Siihen tulee kopioida sisältö tiedostosta ~/hadoopinfra/hdfs/namenode/current/VERSION samasta tiedosta. Ko. tietosisällön rikkoo komento hadoop namenode –format. Tämän virheen korjauksen seurauksena komento start-dfs.sh pystyy käynnistämään datanoden joka ei onnistu virhetilanteessa ennen edellistä päivitystä (datanodea tarvitaan hajautetussa tiedostokäsittelyssä!). Voit varmistaa että start-dfs.sh käynnistää oikeat taustaprosessit komennolla jps; tulostuksen pitäisi olla kutakuinkin seuraava (prosessi-Id:t luonnollisesti vaihtelevat):
hadoop@myMachine:~$ jps
11840 Jps
11533 DataNode
11726 SecondaryNameNode
11375 NameNode

2.	Sovella sivustolta http://www.tutorialspoint.com/hadoop/hadoop_mapreduce.htm kohdasta Compilation and Execution of Process Units Program eteenpäin löytyviä ohjeita oman ohjelmasi kääntämiseksi ja ajamiseksi. Huom: tavoitteena on tehdä tässä oma ohjelma mutta sovellamme sähkönkulutusohjelman käännös- ja ajo-ohjeita kun vaiheet tehdään oman ohjelman osalta samalla tavoin.
Kun olet käynnistänyt hadoop:in taustaprosessit komentojen start-dfs.sh ja start-yarn.sh avulla pitäisi ajossa olla seuraavat prosessit (pid:it luonnollisesti vaihtelevat):
hadoop@erkki-VirtualBox:~$ jps
29523 NodeManager
28707 NameNode
29208 ResourceManager
3689 Jps
29917 DataNode
29054 SecondaryNameNode

Tässä kohdassa ohjeista joutuu poikkeamaan seuraavissa kohdin:
$HADOOP_HOME/bin/hadoop fs -mkdir input_dir
pitääkin antaa muodossa
$HADOOP_HOME/bin/hadoop fs -mkdir /input_dir
Lisäksi ohjeista joutuu poikkeamaan seuraavassa kohdin:
$HADOOP_HOME/bin/hadoop fs -cat output_dir/part-00000/bin/hadoop dfs get output_dir /home/hadoop 
korvaa tämä komennolla:
hdfs dfs -get output_dir /user/hadoop 

Kirjoita tästä tehtävästä raporttiin kuvaus tehdystä työstä. Siitä pitää ilmetä vastaukset esitettyihin kysymyksiin ja kuvaus työn etenemisestä. Raportin liitteeksi pitää oheistaa tehty lähdekoodi. Kaikki tehty lähdekoodi pitää palauttaa myös erillisinä tiedostoina sekä ohjeet siitä, miten lähdekoodeista alkaen saadaan aikaiseksi toimiva testijärjestely (opettaja voi testata tehdyn ohjelman). Raporttiin pitää oheistaa myös ajotulokset todisteena siitä että ohjelma toimii. Voit esimerkiksi ottaa kuvankaappauksia Terminal-ohjelman sisällöistä joista näkyy annetut syötteet ja saadut tulokset.
Vastaa myös raportissasi seuraaviin erillisiin kysymyksiin:
•	Mikä on ohjelmasi suunnitteluratkaisu ?
•	Miten ohjelman ajaminen Pseudo Distributed –moodissa eroaa sen ajamisesta Local Standalone –moodissa ?
•	Mitä dataa map()-metodille annetaan avainarvoina (mitä ovat key-arvot) ?
•	Mitä ovat key-arvot reduce()-metodissa ?
•	Miten periaatetasolla tekemääsi ohjelmaa voitaisiin ajaa aidosti hajautettuna: mikä on klusterien rooli, missä tieto sijaitsee, missä prosessit, kuka/miten hoitaa edellisten hallinnoinnin jne. ? Eli miten tämä homma hoidettaisiin jos datan koko olisi todella ”Big” ja suorituskyvylle olisi asetettu vaatimuksia ?


# 3	VAADITUT TULOKSET
Tee työskentelystä raportti, jossa vastaat edellä esitetyssä työohjeessa kerrottuihin kysymyksiin ja kerrot edellä vaadittuja asioita. Tavoite on, että kirjoittaessasi asiat valaistuvat sinulle lisää tai ne herättävät uusia kysymyksiä joiden selvittämiseen saat kipinän (tai ainakin polun alkuun; jatkat sitten polulla jos aikaa ja motivaatiota löytyy).
Raportin muotoilun pitää noudattaa TAMKin kirjallisten töiden raportointiohjeen ohjeistusta. Jäsentely on vapaa mutta on suotavaa, että asioita käsitellään siinä kronologisessa järjestyksessä missä työskentelyä tuli tehtyä. Samoin jäsentelyssä tulee noudattaa aihepiireihin liittyvää kriteeriä; esim. käsittelet yhdessä kohdin (mahdollisesti alilukujen kera) WordCount-ohjelmointiprojektisi kaikki asiat.
Tee raporttiisi johdanto, jossa kerrot tavoitteet, sekä yhteenveto, jossa kokoat opitut asiat lyhyeen ja koostavaan muotoon. Nämä kannattaa tehdä raporttiin viimeiseksi. Yhteenvedossa tulee käsitellä seuraavia asioita: mitä opittiin, mitä voisi vielä oppia, mitä hyvää työssä oli, mitä siinä voisi kehittää, yleisvaikutelma työstä. Kirjoita vielä yhteenvetoon arvio työn tekemiseen kuluneesta ajasta.
Raportin liitteeksi tulee liittää kaikki tehty ohjelmakoodi kronologisessa ja projektikohtaisessa järjestyksessä.
Kun kerrot raportissasi asioiden ymmärtämistä ehdotan asioiden kertomista hyvien kuvien avulla. Sanonta hyvä kuva kertoo enemmän kuin tuhat sanaa pätee tässä. Toki kuvaa tulee käsitellä myös tekstissä ettei se jää irralliseksi liitetyksi kuvaksi. Kuvana voidaan ajatella myös graafit, tilastokäyrät ja ylipäätään kaikki kaksi-/kolmiulotteinen visuaalinen materiaali (emme sisällytä raporttiin videoita ainakaan toistaiseksi; en näe niillä olevan riittävästi lisäarvoa).
