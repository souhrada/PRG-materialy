# Beautiful Soup

Beautiful Soup 4 (dále jen BS4) je knihovna, která se používá ke sbírání dat z webových stránek, tzv. web scraping.
Pomocí programu můžeme získat informace z webu a dále je použít v našem kódu.
Příkladem může být sbírání dat o aktuálním počasí, sportovních výsledků nebo jiných novinek z webových stránek.

**Web scraping je morálně šedá zóna a neměli bychom stahovat data z webů, které to nepřejí.**

## Instalace

BS4 nainstalujeme, když do konzole napíšeme příkaz 
```python
pip install beautifulsoup4
```

## Dokumentace

Dokumentaci k BS4 naeznete [zde](https://beautiful-soup-4.readthedocs.io/en/latest/)


## Příklad kódu

```python

from bs4 import BeautifulSoup
import requests


def main():
    
    url = "https://www.trebesin.cz"

    response = requests.get(url)

    soup = BeautifulSoup(response.content, "html.parser")

    
    all_paragraphs = soup.select("p")
    print(all_paragraphs[0].text)

    gymnazium = soup.select_one("#favimagehover-title4")
    print(gymnazium.text)

if __name__ == "__main__":
    main()
```

## Vysvětlení kódu

### importy
Nejprve je potřeba importovat knihovnu BS4.

Dále importujeme knihovnu request, která nám umožní připojit se na webovou stránku
```python
from bs4 import BeautifulSoup 
import requests
```

### připojení na stránku
Adresu stránky, ze které budeme sbírat informace uložíme pod proměnnou, abychom měli čitelnější kód

Requests.get nám zajistí připojení na webovou stránku a uloží odpověď serveru pod proměnnou response
```python
url = "https://www.trebesin.cz" # adresu stránky, ze které budeme sbírat informace uložíme pod proměnnou
response = requests.get(url) # pomocí knihovny request se připojíme na webovous stránku
```

### zpracování pomocí BS4
V následujícím kódu vezmeme obsah z webové stránky, který jsme získali pomocí knihovny requests a prožene jej parserem. Tzv, nám zpracuje data, vezme hrubá HTML data umožní našemu kódu s nimi lépe pracovat.
```python
soup = BeautifulSoup(response.content, "html.parser") # obsah z webové stránky zpracujeme pomocí tzv. parseru a zpracovaná data uložíme pod proměnnou soup
```

### práce s obsahem stránky
Vytvoříme proměnnou a na soup, kterou jsme vytvořili výše, zavoláme funkci `select()`. Select zvolí všechny prvky. Jaké prvky chceme, zvolíme pomocí CSS selectorů.

Můžete použít všechny prvky (p, h1, img), classy (.class), id (#id) a další CSS selektory, které znáte.

`select()` volí všechny prvky, `select_one()` zvolí první prvek

```python
all_paragraphs = soup.select("p")
gymnazium = soup.select_one("#favimagehover-title4")
```

### text z prvku

`select()`a `select_one()` označí prvek a uloží jej pod proměnnou. Uloží však celý prvek, který nám bude vracet html kód, např. `soup.select_one("#favimagehover-title4")` vrátí:

```bash
<h4 id="favimagehover-title4" style="color: #FFFFFF; background-color: #D96327; font-family: Open Sans; font-weight: 400; font-style: normal; padding: 10px 20px; font-size: 15px; line-height: 1.4em; text-align: center; margin-bottom: 0;"><i class="f" style="color: #FFFFFF; font-size: 15px; vertical-align: baseline"></i>
            GYMNÁZIUM
</h4>
```

Častěji však chcete pouze obsah prvku, tedy text **GYMNÁZIUM**. V tom případě můžeme použít ```.text```

```python
gymnazium.text
```
a můžeme přímo vypsat do konzole 
```python
print(gymnazium.text)
```

což nám vrátí

```bash
GYMNÁZIUM
```

Nezapomeňte, že `select()` označí všechny prvky a vrátí je jako list, v takže k jednotlivým prvkům můžeme přistupovat pomocí indexu

```python
all_paragraphs = soup.select("p")
print(all_paragraphs[0].text)
```

popřípadě vypsat všechny pomocí cyklu `for`

```python
all_paragraphs = soup.select("p")

for paragraph in all_paragraphs:
    print(paragraph.text)
```

### alternativa

V návodech na internetu/od AI, častokrát naleznete alternativu k select() a select_one() v podobě `find_all()` a `find()`.

find_all() funguje totožně jako select() ---> vybere všechny prvky
find() pak stejně jako select_one() ----> vybere první prvek

find() a find_all() používají však jiný syntax pro výběr prvků.

```python
all_paragraphs = soup.find_all("p")
gymnazium = soup.find(id="favimagehover-title4")
```

Osobně doporučuji používat select() a select_one(), CSS selektory znáte a není potřeba učit se nový syntax.


### celý kód s komentáři

```python

from bs4 import BeautifulSoup # nejprve je potřeba importovat knihovnu
import requests # knihovna requests nám umožní připojit se na webovou stránku


def main():
    
    url = "https://www.trebesin.cz" # adresu stránky, ze které budeme sbírat informace uložíme pod proměnnou

    response = requests.get(url) # pomocí knihovny request se připojíme na webovous stránku

    soup = BeautifulSoup(response.content, "html.parser") # obsah z webové stránky zpracujeme pomocí tzv. parseru a zpracovaná data uložíme pod proměnnou soup

    
    all_paragraphs = soup.select("p") # najde všechny p
    print(all_paragraphs[0].text) # vypíše text z prvního p

    # alternativně lze zvolit pouze jeden prvek
    gymnazium = soup.select_one("#favimagehover-title4") # najde prvek s id favimagehover-title4
    print(gymnazium.text) # vypíše text ze zvoleného prvku

if __name__ == "__main__":
    main()
```
