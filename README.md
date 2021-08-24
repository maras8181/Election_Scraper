Engeto: Project 3
===
Třetí project na online python akademii od Engeta.

Popis programu
---

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
