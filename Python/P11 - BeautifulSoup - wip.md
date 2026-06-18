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


## Kód

```python

from bs4 import BeautifulSoup # Nejprve je potřeba importovat knihovnu
import requests # knihovna requests nám umožní připojit se na webovou stránku


def main():
    
    url = "https://www.trebesin.cz" # adresu stránky, ze které budeme sbírat informace uložíme pod proměnnou

    response = requests.get(url) # pomocí knihovny request se připojíme na webovous stránku

    soup = BeautifulSoup(response.content, "html.parser") # obsah z webové stránky zpracujeme pomocí tzv. parseru a zpracovaná data uložíme pod proměnnou soup

    # pokud chceme konkrétní prvky z webové stránky, máme dvě možnosti
    # soup.find(id="id_nadpisu") - zde je potřeba zachovat syntax
    # pomocí soup.find_all("p") můžeme získat data ze všech prvků určitého elementu/classy
    # 
    # možná snažší je však používat funkce
    # soup.select_one(".classa") a soup.select("p"), ve kterých můžeme používat CSS selectory, které již známe (.class, #id, p, h1, apod.)
    # 
    # pokud poté chceme pouze text z daného prvku, musíme aplikovat funkci .text, například:
    all_p = soup.find_all("p")

    # for p in all_p:
    #     print(p.text)

    # gym = soup.find(id="favimagehover-title4")
    # print(gym)

    # .select používá CSS selectory ., #, atd.
    # select vrací všechny prvky v listu
    gym2 = soup.select("#favimagehover-title4")
    print(gym2[0].text)

    # alternativně
    # gym2 = soup.select_one("#favimagehover-title4")
    # print(gym2.text)

    # select_one a select jsou alternativy k find a find_all

if __name__ == "__main__":
    main()
```
