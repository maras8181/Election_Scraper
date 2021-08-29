Engeto: Project 3
===
Třetí project na online python akademii od Engeta. Tento kód je psaný po skončení kurzu. Psaní kódu trvalo 50 hodin.

Popis zadání
---
Tento projekt slouží k extrahování výsledků parlamentních voleb v roce 2017. Odkaz k prohlédnutí najdete [zde](https://volby.cz/pls/ps2017nss/ps3?xjazyk=CZ).

Instalace knihoven
---
Knihovny, které jsou použity v kódu, jsou uložené v souboru ```requirements.txt```. Pro instalaci doporučuji použít nové virtuální prostředí a s nainstalovaným manažerem spustit následovně.

```python
$ pip3 --version			# overim verzi manageru
$ pip3 install -r requirements.txt	# nainstalujeme knihovny
```

Spuštění projektu
---
Spuštění souboru ```election-scraper.py``` v rámci příkazového řádku požaduje 2 povinné argumenty.

```python
python election_scraper <odkaz-uzemniho-celku> <vysledny-soubor>
```

Následně se vám stáhnou výsledky jako soubor s příponou ```.csv```.

Ukázka projektu
---
Výsledky hlasování pro okres Prostějov:

1. argument: ```https://volby.cz/pls/ps2017nss/ps32?xjazyk=CZ&xkraj=12&xnumnuts=7103```
2. argument: ```vysledky_prostejov.csv```

Spuštění programu:

```python
python election-scraper.py "https://volby.cz/pls/ps2017nss/ps32?xjazyk=CZ&xkraj=12&xnumnuts=7103" "vysledky_prostejov.csv"
```

Průběh stahování:
```
STAHUJI DATA Z VYBRANEHO URL: https://volby.cz/pls/ps2017nss/ps32?xjazyk=CZ&xkraj=12&xnumnuts=7103
UKLADAM DO SOUBORU: vysledky_prostejov.csv
UKONCUJI election-scraper
```

Částečný výstup:

```
Code,City,Registered,Envelopes,...
506761,Alojzov,205,145,144,29,0,0,9,0,5,17,4,1,1,0,0,18,0,5,32,0,0,6,0,0,1,1,15,0
589268,Bedihošť,834,527,524,51,0,0,28,1,13,123,2,2,14,1,0,34,0,6,140,0,0,26,0,0,0,0,82,1
589276,Bílovice-Lutotín,279,279,275,13,0,0,32,0,8,40,1,0,4,0,0,30,0,3,83,0,0,22,0,0,0,1,38,0
```

Popis programu
---

Na začátku programu je potřeba naimportovat knihovny, se kterými budeme v programu pracovat.

ř. (line) 6 - ř. (line) 18 - Přiřazování elementů.
Do proměnných přiřazujeme elementy tříd, odkud budeme brát jak výstupní data, tak i data, která budeme potřebovat v našem programu.

ř. (line) 185 - Kontrolujeme pořadi argumentů.
V případě, že uživatel zadal nesprávný počet argumentů, nebo argumenty v nesprávném pořadí, pak jej program upozorní a končí.

ř. (line) 195 - Žádání o HTML kód.
V opačném případě požádáme ze zadané webové stránky uživatelem o HTML kód. O tohle se nám postará funkce ```get_html(arg)```.

ř. (line) 196 - Stahujeme města, kódy měst a odkazy.
Jakmile jsme úspěšně získali strukturu HTML naší webové stránky, můžeme ji začít prohledávat ```for``` cyklem. Našim cílem bude najít všechny názvy měst, kódy jednotlivých měst, ale i odkazy, které jsou ukryty pod znakem X. Všechna tato data nalezneme pomocí právě námi nadeklarovaných proměnných od řádku 6 po řádek 18. Pod těmito elementy jsou tato data ukryta. Po nalezení zmíněných dat je uložíme do listů s názvy ```codes```, ```cities``` a ```links```. První dva listy můžeme na chvilku nechat být, ale ```links``` budeme za chvilku potřebovat. Tuto část kódu obsahuje funkce ```get_first_columns```.

ř. (line) 197 - Stahujeme ostatní data. Voláme funkci ```get_second_data(arg)```.
Nyní začneme stahovat ostatní data. Ta najdeme právě pod ukrytými odkazy, které jsme si stáhli před chvilkou. Námi nalezené odkazy jsou však neúplné, protože každému chybí hlavní část. Na ř. (line) 6 jsme si mohli všimnout proměnné ```MAIN_URL```, ve které je právě uložena hlavní čast odkazu. Po spojení této proměnné s každou částí odkazu, která se nacházi v listu ```links``` se dostaneme na stránku, odkud budeme brát ostatní data.
Naše odkazy v listu ```links``` jsou rozděleny do 2 skupin, a to proto, že některé obce jsou rozděleny do několika menších okrsků. To znamená, že u některých odkazů se neproklikneme na stránku, ze které chceme brát požadovaná data, ale na stránku, kde je obec rozdělena do těchto menších okrsků. Pro nás to znamená, že musíme udělat mezikrok.
Tento mezikrok se nachází na ř. (line 157 - ř. (line) 160. Napřed požádáme o HTML strukturu kódu této "mezistránky". Poté najdeme všechny odkazy, pod kterými jsou ukryta naše požadovaná data. Následně sečteme všechna tato data jednotlivých menších okrsků do jednoho objektu. Sčítaní hodnot je rozděleno na horní a dolní data, starají se o to funkce ```sum_header_data``` a ```sum_party_numbers```. Všechna tato data jsou uložena v listech, které budeme při ukládání do souboru ```.csv``` potřebovat.
Posledními daty, které nám chybí, jsou kandidující strany. Získání těchto stran nám zajistí funkce ```get_cand_parties(arg)```.

ř. (line) 21 - Ukládáme do ```.csv``` souboru.
Nyní už máme všechna data stažená a můžeme začit zvesela ukládat do ```.csv```. První řádek bude obsahovat hlavičku (ř. (line) 18) a kandidující strany. Další řádky budeme postupně vyplňovat za pomocí ```for``` cyklu a metody ```writerow``` od ř. line 26 - ř (line) 31.
