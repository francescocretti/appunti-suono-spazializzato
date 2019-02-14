# Appunti sul suono spazializzato

##### A partire dagli spunti della *Masterclass su suono immersivo*, View Conference, Torino, 23 ottobre 2018
##### Relatori
* [Gianni Ricciardi](mailto:gianni.ricciardi@wantmusik.com) - [WANTmusik](http://www.wantmusik.com/)
* [Matteo Milani](mailto:matteo@unidentifiedsoundobject.com) - [Unidentified Sound Object](http://www.unidentifiedsoundobject.com/)


## Introduzione

Principale differenza fra le esperienze VR -> **gradi di libertà (DOF)**

**3 DOF** -> solo roll, pitch and yaw. Rappresenta l'esperienza ottenuta con
normali video 360°. I visori di questo tipo sono equipaggiati con piattaforma inerziale e monitor (Oculus Go) o sfruttano lo smartphone (Samsung Gear VR).

**6 DOF** -> consente la localizzazione dell'utente nello spazio. Rappresenta l'esperienza di realtà virtuale completa. E' quindi necessario un sistema in grado di tracciare i movimenti traslatori dell'utente. Esistono due tecniche:
* [outside-in tracking](https://xinreality.com/wiki/Outside-in_tracking): tracciamento attraverso sensoristica esterna, come Oculus Rift e HTC Vive;
* [inside-out tracking](https://xinreality.com/wiki/Inside-out_tracking): tracciamento attraverso sensori interni al dispositivo (camere infrarossi, ecc), come Oculus Quest e Razer OSVR.

<img src="https://www.qualcomm.com/sites/ember/files/styles/optimize/public/blog/managed-images/image_1_sized.jpg?itok=8lp5NbB7" height="200">


## Suono spazializzato
La relatà virtuale comporta l'immersività anche dal punto di vista del suono: l'orecchio umano ha una risoluzione di pochi *cm* in termini di [localizzazione di un suono](https://en.wikipedia.org/wiki/Sound_localization) nello spazio.

I primi esperimenti sul suono spazializzato risalgono agli anni 70. Ad esempio:
* Sviluppo di [microfoni binaurali](https://it.wikipedia.org/wiki/Registrazione_binaurale) come il celebre [Neumann KU100](https://en-de.neumann.com/ku-100);
* Registrazioni [olofoniche](https://it.wikipedia.org/wiki/Olofonia) pubblicate da [Hugo Zuccarelli](http://www.rivistaunaspecie.com/cult-olofonia-lesperienza-del-suono-tridimensionale/) negli anni 80;
* Esperimenti di sintesi binaurale e studi sull'[HRTF](https://en.wikipedia.org/wiki/Head-related_transfer_function).

Per una precisa percezione del suono spazializzato è necessario l'ascolto in cuffia, per evitare cross-talking fra orecchio sx e dx e le interferenze fra i due segnali acustici.

Un problema comune in questo tipo di contenuto audio è la difficoltà nel distinguere fra un suono frontale ed uno posteriore. Nel caso di suoni reali l'ambiguità è risolta quando l'ascoltatore effettua leggeri movimenti della testa. Nel caso di una registrazione olofonica la posizione del suono è solidale a quella della testa: il suono registrato sarà sempre localizzato nello stesso punto da chi ascolta, indipendentemente dalla posizione della sua testa.

Nella realtà virtuale è necessario invece che il suono rimanga sempre fisso nella stessa posizione dello spazio, e di conseguenza venga localizzato in punti diversi a seconda della posizione della testa. Oltre un sistema di **_head tracking_** è quindi necessario un insieme di tecniche di registrazione e riproduzione che consentono di ottenere questo tipo di contenuto audio.

## Ambisonics
Il primo step è quello di registrare un suono ricreando completamente la sfera acustica 360. Il formato [Ambisonics](https://en.wikipedia.org/wiki/Ambisonics) nasce esattamente con questo scopo intorno alla metà degli anni 70.

**Ambisonics** è un contenitore, *open-source*, che comprende un insieme di metodi per *registrare, mixare e riprodurre* una sfera di suono a 360°, proveniente da diverse direzioni attorno ad un punto centrale (sweet spot) in cui si trova l'ascoltatore.

Ambisonics rappresenta una *bolla di suono*, liscia, stabile e continua, completa di elevazione.
È *speaker-agnostic*: può essere decodificato per qualsiasi sistema di speaker.

<br>
<br>

| PROS | CONS |
| :--: | :--: |
| flessibile, evocativo, future-proof | Ascolto solo in un punto preciso, richiede decodifica, file pesanti |

###### Campi di applicazione
Film/video - Mix/post-produzione - VR - Installazioni sonore - Ricerca scientifica - Composizione musicale

###### Hardware ambisonic
Un microfono in grado di registrare audio Ambisonics è chiamato anche *[Soundfield microphone](https://en.wikipedia.org/wiki/Soundfield_microphone)*, ed è stato brevettato da Michael Gerzon e Peter Craven nel '75.
Attualmente la [SoundField](https://www.soundfield.com/#/home) è un'azienda che produce HW e SW per l'audio ambisonics.

La maggior parte dei microfoni Ambisonics sono equipaggiati con 4 capsule a condensatore (solitamente cardiodi) che puntano nelle direizioni Left-Front, Left-Back, Right-Front e Right-Back e registrano in A-Format, ovvero l'output raw delle 4 capsule.

<img src="https://dannywellens.files.wordpress.com/2014/11/sps200-software-controlled-microphone-2.jpg" height=250 style="display:block;margin:0 auto;">

Alcuni microfoni codificano anche un metadata contentene la direzione di puntamento (upright, endfire, upside-down).

Alcuni mic Ambisonics:
* [Soundfield SPS200](https://www.soundfield.com/#/products/sps200)
* [Sennheiser Ambeo](https://en-us.sennheiser.com/microphone-3d-audio-ambeo-vr-mic)
* [Rode/Soundfield NT-SF1](https://www.rode.com/ntsf1)
* [Zoom H3-VR](https://www.zoom-na.com/products/field-video-recording/field-recording/zoom-h3-vr-handy-recorder)

Il segnale raw trasdotto da un microfono ambisonics è chiamato A-Format.
I microfoni ambisonici possono essere differenti per diversi parametri (numero e diagramma polare di capsule, configurazione, ecc), di conseguenza l'A-Format non può essere considerato uno standard.

##### First-order vs Higher-order Ambisonics

A partire da una registrazione raw in A-Format, il segnale viene normalmente trasformato in un altro formato, detto B-Format.

Il B-Format è il formato standard per la rappresentazione dell'audio Ambisonics. Il segnale sferico viene codificato in una serie di segnali che rappresentano ognuno una porzione del volume sferico.

Il formato di base è chiamato First Order Ambisonics (FOA), è composto da quattro canali e la detiene la risoluzione spaziale minima per un segnale audio 360.
I quattro canali si dividono in:
* W - diagramma polare omnidirezionale - *sound pressure*
* X - diagramma polare a 8 (bidirezionale) - *front-minus-back*
* Y - diagramma polare a 8 (bidirezionale) - *left-minus-right*
* Z - diagramma polare a 8 (bidirezionale) - *up-minus-down*

La scarsa risoluzione del FOA ha portato allo sviluppo di formati di ordine maggiore, che mediante l'utilizzo di un numero maggiore di canali è in grado di rappresentare l'informazione di un numero maggiore di porzioni del volume (*spherical harmonics*).

| Ordine Ambisonic | Numero di canali |
| :--: | :--:|
| FOA | 4 |
| 2OA | 9 |
| 3OA | 16 |
| 4OA | 25 |
| 5OA | 36 |
| 6OA | 49 |

Nello schema sottostante una rappresentazione visuale degli *spherical harmonics* del segnale Ambisonics dal primo al terzo ordine.

<img src="http://w2.mat.ucsb.edu/240/D/notes/spherical_harmonics.preview.jpg" height=250 style="display:block;margin:0 auto;">

Lo standard B-Format ha due varianti, che differiscono per l'ordine dei canali:
* ACN Order (AmbiX)
* Furse-Malham Ordering (FuMa) (lo standard *de facto* per gli ordini <= 3)

> NOTA: lettura consigliata - [Towards usability of
Higher Order Ambisonics in Digital Audio Workstations](http://www.matthiaskronlachner.com/wp-content/uploads/2013/01/ambisonics-daw-presentation.pdf), Matthias Kronlachner, 2012

## Plugins

Per la codifica/decodifica e gestione del suono spazializzato sono necessari plugin, disponibili per le più usate DAW in commercio:

* [Sennheiser Ambeo Suite](https://en-us.sennheiser.com/ambeo-blueprints-downloads) - suite
* [ambiX by Mathias Kronlachner](http://www.matthiaskronlachner.com/?p=2015) - suite di produzione audio spazializzato
* [Soundfield by Rode](https://it.rode.com/soundfieldplugin) - ambisonics recordings post-processor
* [SoundField SurroundZone2](https://www.soundfield.com/products/surroundzone2) - ambisonics recordings post-processor
* [Plugins by Noisemakers](https://www.noisemakers.fr/) - diversi plugins
* [HARPEX](https://harpex.net/) - spatial audio formats cross-coding algorithm
* [Blue Ripple Sound O3A](http://www.blueripplesound.com/) - suite (con effetti spazializzati)
* [Waves 360° Ambisonics Tools](https://www.waves.com/hardware/360-ambisonics-tools)
* [Suite open source dell'IEM (Gratz)](https://plugins.iem.at/)
* [Sparta, open-source VST plug-in](http://research.spa.aalto.fi/projects/sparta_vsts/)

## FB360 Spatial Audio Workstation
[Facebook360 Spatial Audio Workstation](https://facebook360.fb.com/spatial-workstation/) (*FB260 SAW*) è una suite di strumenti completa e gratuita per il design e la codifica di contenuti audio spazializzati per il VR.

**Spatial Audio Workstation 8-channel**: formato inventato da FB360, 8 canali perché sta a metà fra FOA e 2OA, ha più risoluzione sul piano orizzontale - *NON STANDARD*

Il formato di uscita è chiamato Two Big Eears (.tbe).

> NOTA: lettura consigliata - [Conversion from Ambisonics to TBE format](http://pcfarina.eng.unipr.it/TBE-conversion.htm) dal blog di Angelo Farina, 2017

FB360 mette anche a disposizione un SDK che supporta l'integrazione del formato .tbe in diversi ambienti (Android, Unity...).

A questo [link](https://www.facebook.com/groups/audio360support/) si trova il gruppo di discussione su FB riguardo l'utilizzo della *FB360 SAW*.


## Recap: formati e standard
* **A-Format**: raw ambisonics. Contiene i dati audio *raw* provenienti dalle capsule di un mic - *NON STANDARD*
* **B-Format**: formato standard di rappresentazione dell'audio ambisonics. Il numero di canali dipende dall'ordine dell'ambisonics (vedi paragrafo precedente). Si divide in FuMa e AmbiX a seconda dell'ordine in cui sono codificati i canali (FuMa: WXYZ, AmbiX: WYZX) - *STANDARD*
* **Two Big Ears (.tbe)**: formato di uscita dell'audio processato con FB360 SAW. Può contenere 8 canali (solo spazializzato) o 10 canali (spazializzato + una traccia stereo fissa) - *NON STANDARD*


## Altri progetti e riferimenti

#### Carne y Arena
[Installazione di realtà virtuale](http://www.fondazioneprada.org/project/carne-y-arena/) che comprende anche l'utilizzo di "mixed audio reality": suono in cuffia spazializzato + infrasuoni riprodotti da subwoofer [Meyer Sound](https://meyersound.com/news/inarritus-virtual-reality/).
Regia di Alejandro Inarritu, Sound Design di Randy Thom e Martin Hernandez.

<br>

#### FMOD Audio Engine
[FMOD](https://www.fmod.com/) è un sound engine proprietario usato soprattutto per lo sviluppo di audio per video games e applicazioni interattive.

#### Link vari

###### Teoria
* [Ambisonics Explained: A Guide for Sound Engineer](https://www.waves.com/ambisonics-explained-guide-for-sound-engineers) - Waves Audio
* [Differences between A Format and B Format](https://postperspective.com/vr-audio-differences-format-b-format/) - postperspective.com
* [An Introduction to Ambisonics](https://www.creativefieldrecording.com/2017/03/01/explorers-of-ambisonics-introduction/) - creativefieldrecording.com
* [Binaural and ambisonic sound
](http://www.garethfry.co.uk/binaural-sound/) - Gareth Fry

###### Pratica
* [FB360 Spatial Workstation Workflow](https://facebookincubator.github.io/facebook-360-spatial-workstation/KB/SpatialWorkstationWorkflow.html) - Facebook
* [Resonance Audio Project](https://developers.google.com/resonance-audio/) - Google
* [A beginner’s guide to spatial audio in 360-degree video](https://training.npr.org/visual/a-beginners-guide-to-spatial-audio-in-360-degree-video/) - NPR
* [Your Detailed Guide to Spatial Audio for 360 Video](https://nofilmschool.com/2016/10/detailed-guide-to-spatial-audio-for-360-video-using-mostly-free-tools) - nofilmschool.com
* [First-order ambisonics in REAPER](https://support.google.com/jump/answer/6399978) - Google
* [Samsung VR Best Practices](https://samsungvr.com/portal/content/content_specs) - Samsung
* [Ambisonic Audio with 360 Video in Premiere Pro CC 2017](https://www.youtube.com/watch?v=MqBDQLV7xZI) - Jason Levine
* [Add Spatial Audio To Oculus Video (Gear VR)](https://fb360spatialworkstation.zendesk.com/hc/en-us/articles/207888609-Add-Spatial-Audio-To-Oculus-Video-Gear-VR-) - Facebook
* [How to Create 360⁰ Mixes from Stereo Mix Stems](https://www.waves.com/how-to-create-360-mixes-from-stereo-mix-stems) - Waves Audio
