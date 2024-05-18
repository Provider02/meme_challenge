# Meme klasifikácia modelom ISSUES

## Detekcia antisociálneho správania v multimodálnych vstupných dátach

Tento repozitár bol vytvorený ako súčasť bakalárskej práce na tému Detekcia antisociálneho správania v multimodálnych vstupných dátach (2024). Obsahom tohto repozitára je využívaný kód modelu ISSUES, ktorého zameraním je funkcia klasifikovania mémov ako nenávistných alebo neškodných podľa ich sémantického kontextu popisu a obrázka. Model ISSUES reprodukujeme a vizualizujeme pre porovnanie v plnení úlohy s online dostupnými LLMs. Model ISSUES bol nami len prevzatý, pričom vznikol vrámci práce [paper](https://openaccess.thecvf.com/content/ICCV2023W/CLVL/html/Burbi_Mapping_Memes_to_Words_for_Multimodal_Hateful_Meme_Classification_ICCVW_2023_paper.html) a je dostupný prostredníctvom príslušného repozitára (https://github.com/miccunifi/ISSUES).


### Abstrakt práce
Multimodálny obsah v podobe mémov sa stal behom posledných desaťročí jednou z dominantných a rýchlo rastúcich foriem dát dostupných online. Takýto obsah sa ale nemusí vždy zhodovať s politikami a pravidlami sociálnych sietí a iných stránok, na ktorých je zverejňovaný a musí tak byť moderovaný. V tejto práci sa zaoberáme automatickým posudzovaním nenávistného charakteru mémov, prostredníctvom na túto úlohu trénovaných modelov hlbokého učenia. Okrem podania teoretického pohľadu na problematiku a replikovania spomínaných modelov, posudzujeme aj možnosť využitia veľkých jazykových modelov pre túto úlohu.


### Príprava prostredia a kódu
Kód obsiahnutý v tomto repozitári bol použitý a je vhodný na použitie prostredníctvom platformy Google Colab & Google Drive.

1. Prevzatie / Stiahnutie
   Obsah repozitára stiahnite a nahrajte na Google Drive alebo použite kód pre prevzatie:
   ```sh
   https://github.com/Provider02/model_issues.git
   ```

2. Stiahnutie zdrojov

   'resources' pre tento kód sú dostupné na stiahnutie vo vydaní pôvodného autora [release](https://github.com/miccunifi/ISSUES/releases/tag/latest).

   Obsah:
   * Pred-trénované modely na datasetoch HMC a HarMeme
   * Pred-trénované váhy
   * Súbory datasetov HMC a HarMeme (vrátane rozdelenia príkladov a ich správnych označení | vynímaj samotné príklady)
  
3. Stiahnutie datasetov

   * Dataset HMC je dostupný na stiahnutie na ofcialnej stánke súťaže [**Hateful Memes Challenge**](https://hatefulmemeschallenge.com/#download)
   * Dataset HarMeme je dostupný na stiahnutie v tomto GitHub projekte [**HarMeme**](https://github.com/di-dimitrov/mmf/tree/master/data/datasets/memes/defaults/images)
  
4. Štruktúra projektu

   Upravte súbory do nasledujúcej štruktúry:

   <pre>
   project_base_path
   └─── resources
     └─── datasets
       └─── harmeme
           | clip_embds
           | img
           | labels
       └─── hmc
           | clip_embds
           | img
           | labels
  
     └─── <b>pretrained_models
         | hmc_text-inv-comb_best.ckpt
         | harmeme_text-inv-comb_best.ckpt
      
     └─── pretrained_weights
         | hmc
         | harmeme
         | phi
         </b>
  
   └─── src
     | combiner.py
     | datasets.py
     | engine.py
     ...

   └─── run_harmeme_text-inv-comb.sh
  
   └─── run_hmc_text-inv-comb.sh

   └─── requirements

   └─── visualization
   </pre>

   Obsah priečinkov 'img' nahraďte príkladmi datasetov pre obe HMC a HarMeme

5. Upravte src .py súbory

   U súborov datasets.py, engine.py a main.py, je potrebná úprava označená komentármi:
   <pre>
   !!! ACTION REQUIRED !!! - update path
   </pre>
   V týchto častiach kódu je potrebné upraviť cestu k súborom podľa usporiadania priečinkou používateľa na Google Dirve, teda nahraďit časť 'YOUR_PATH' správnou cestou.
  
6. Upravte súbor visualization.ipynb

   Nastavte svoju cestu koreňového priečinka, a to na mieste označenom komentárom:
   <pre>
   !!! ACTION REQUIRED !!! - update path to your root folder
   </pre>

   Potrebné aj je dosadenie API KEY účtu Wandb pre jeho využitie, a to na mieste označenom komentárom:
   <pre>
   !!! ACTION REQUIRED !!! - update API KEY
   </pre>

7. Spustenie bloku 'Enviroment setup'

   Blok ' Enviroment setup' obsahuje 5 cells, ktoré pripoja Google Drive, nastavia cestu koreňového priečinka a nainštalujú potrebné požiadavky.
   
8. Spustenie bloku 'Weights & Biases setup'

   Blok ' Weights & Biases setup' obsahuje 1 cell, ktorý prepojí používateľov Wandb účet.


### Použitie modelu

Model je možné použiť na oboch datasetoch HMC aj HarMeme, prostrednítvom spustenia kódu v časti 'Usage of model on HMC and HarMeme datasets' vo 'visualization.ipynb'.

Pre zopakovanie výsledkov trénovania podľa [**pôvodným autorom**](https://github.com/LorenzoAgnolucci) poskytnutého checkpointu, nie je nutné vykonanie žiadnej zmeny.
* tag " --reproduce t "
* tag " --pretrained_proj_weights t "
* --pretrained_model 'hmc_text-inv-comb_best.ckpt' / --pretrained_model 'harmeme_text-inv-comb_best.ckpt'

Pre trénovanie modelu je potrebné vykonať tieto zmeny:
* tag " --reproduce f "
* tag " --pretrained_proj_weights f "
*  --pretrained_model ' '


### Popis arguemtov

#### Hlavné
- ```dataset``` - názov datasetu: [hmc / harmeme]
- ```num_mapping_layers``` -  počet projekčných vrstiev na mapovanie CLIP funkcií v úlohovo orientovanom latentnom priestore
- ```num_pre_output_layers``` - počet MLP skrytých vrstiev na vykonanie konečnej klasifikácie
- ```max_epochs``` - maximálny počet epoch
- ```lr``` - miera učenia
- ```batch_size``` - veľkosť dávky
- ```fast_process``` - označenie, či sa majú ako vstup modelu používať predpočítané funkcie CLIP namiesto ich výpočtu počas procesu trénovania
- ```name``` - názov modelu
- ```pretrained_model``` - názov kontrolného bodu predtrénovaného modelu v priečinku 'pretrained_models'
- ```reproduce``` - označenie, či sa má vykonať proces trénovania nasledovaný fázou hodnotenia (f) alebo priamo hodnotiť predtrénovaný model na testovacích údajoch (t)

#### Všeobecné
- ```map_dim``` - výstupná dimenzia projektovaných funkčných vektorov
- ```fusion``` - fúzna metóda medzi textovými a vizuálnymi modalitami: [concat / align]
- ```pretrained_proj_weights``` - označenie, či sa majú používať predtrénované projekčné váhy
- ```freeze_proj_layers``` - označenie, či sa majú zmraziť predtrénované váhy

#### Combiner Architektúra
- ```comb_proj``` - označenie, či sa majú projektovať vstupné funkcie
- ```comb_fusion``` - fúzna metóda na kombinovanie vstupných funkcií
- ```convex_tensor``` - označenie, či sa má ako výstup konvexnej kombinácie vypočítať tenzor alebo skalár

#### Architektúra textovej inverzie
- ```text_inv_proj``` - označenie, či sa má použiť projekcia textového enkodéra CLIP
- ```phi_inv_proj``` - označenie, či sa má projektovať výstup phi siete
- ```post_inv_proj``` - označenie, či sa majú projektovať výstupné funkcie textového enkodéra CLIP
- ```enh_text``` - označenie, či sa má použiť prompt iba s pseudo-slovom alebo pripojiť text meme
- ```phi_freeze``` - označenie, či sa má zmraziť predtrénovaná phi sieť 


### Vizualizácia modelu

Vizualizácia modelu, v podobe akú sme ju vytvorili, predstavuje zobrazenie náhodného mému zo sady testovacíh príkladov spolu s jeho predikovaným a skutočným zaradením. Takáto vizualizácia bola vytvorená pre obe datasety HMC a HarMeme, pričom využíva už predtrénovaný model, trénovaný na danom dataste, ako aj u reprodukcie výsledkov modelu. Vizualizácia je takisto dostupná v súbore 'visualization.ipynb' v bloku označenom ako 'Visualization'. Po prejdení do potrebného priečinka je možné spustiť kód pre vizualizáciu, rozdelený do troch častí, osobitne pre oba datasety HMC a HarMeme.


### Autor
* [**Jakub Paranič**](https://github.com/Provider02)


### Uznanie
Naša práca využíva nami len prevzatý, nie vyvíjaný, model [**ISSUES**](https://github.com/miccunifi/ISSUES).
