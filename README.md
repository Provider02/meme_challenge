# meme_challenge

## Detekcia antisociálneho správania v multimodálnych vstupných dátach

Tento repozitár bol vytvorený ako súčasť bakalárskej práce na tému Detekcia antisociálneho správania v multimodálnych vstupných dátach (2024). Obsahom tohto repozitára je využívaný kód modelu ISSUES, ktorého zameraním je funkcia klasifikovania mémov ako nenávistných alebo neškodných podľa ich sémantického kontextu popisu a obrázka. Model ISSUES reprodukujeme a vizualizujeme pre porovnanie v plnení úlohy s online dostupnými LLMs. Model ISSUES bol nami len prevzatý, pričom vznikol vrámci práce [paper](https://openaccess.thecvf.com/content/ICCV2023W/CLVL/html/Burbi_Mapping_Memes_to_Words_for_Multimodal_Hateful_Meme_Classification_ICCVW_2023_paper.html) a je dostupný prostredníctvom príslušného repozitára (https://github.com/miccunifi/ISSUES).


### Abstrakt práce
Multimodálny obsah v podobe mémov sa stal behom posledných desaťročí jednou z dominantných a rýchlo rastúcich foriem dát dostupných online. Takýto obsah sa ale nemusí vždy zhodovať s politikami a pravidlami sociálnych sietí a iných stránok, na ktorých je zverejňovaný a musí tak byť moderovaný. V tejto práci sa zaoberáme automatickým posudzovaním nenávistného charakteru mémov, prostredníctvom na túto úlohu trénovaných modelov hlbokého učenia. Okrem podania teoretického pohľadu na problematiku a replikovania spomínaných modelov, posudzujeme aj možnosť využitia veľkých jazykových modelov pre túto úlohu.


<summary><h3>Príprava prostredia a kódu</h3></summary>
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




### Vizualizácia modelu




### Autor
* [**Jakub Paranič**](https://github.com/Provider02)


### Uznanie
Naša práca využíva model [**ISSUES**](https://github.com/miccunifi/ISSUES).
