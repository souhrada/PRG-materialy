# Lambda - anonymní funkce

**Lambda funkce** jsou anonymní (tj. bezejmenné) funkce, které vytvoříme **na jednom řádku**. Používáme je, když potřebujeme krátkou funkci **rychle a jednorázově** – například jako argument jiné funkce.

Lambda funkci lze uložit pod proměnnou nebo ji použít přímo v rámci jiné funkce.

Lambda funkce jsou alternativou ke klasickým funkcím vytvořeným pomocí `def`. Jejich hlavní výhodou je stručnost a možnost použití přímo v místě, kde je potřebujeme, bez nutnosti je předem definovat.

Lambda automaticky **return**uje (vrací) výsledek operace.

## Kdy se lambda hodí?

-   když nepotřebujeme pojmenovat funkci
-   když funkci používáme jen jednou
-   jako argument funkcí `map()`, `filter()`, `sorted()` a dalších
-   v situacích, kde chceme kód stručnější a přehlednější

## Základní syntaxe

```python
lambda parametry: výraz
```

Lambda funkce se skládá z:

-   klíčového slova `lambda`
-   parametrů (může jich být 0 nebo více)
-   dvojtečky `:`
-   výrazu, který se vyhodnotí a automaticky vrátí (jako by tam bylo `return`, které ale není třeba psát)

**Příklad:**

```python
pozdrav = lambda jmeno: f"Ahoj, {jmeno}!"
print(pozdrav("Jarmil"))  # Ahoj, Jarmil!
```

Je totéž jako klasická funkce:

```python
def pozdrav(jmeno):
    return f"Ahoj, {jmeno}!"

print(pozdrav("Jarmil"))  # Ahoj, Jarmil!
```

**Lambda bez parametru**

Lambda funkce nemusí mít žádný parametr

```python
pozdrav = lambda: "Dobrý den!"
print(pozdrav())  # Dobrý den!
```

**Více parametrů**

Lambda může přijímat i více parametrů, v tom případě je oddělujeme čárkou

```python
scitani = lambda a, b: a + b
print(scitani(3, 5))  # 8

obsah_obdelnik = lambda delka, sirka: delka * sirka
print(obsah_obdelnik(5, 3))  # 15
```

## Příklady použití

### Lambda jako mini-výpočet

```python
xp_za_level = lambda level: level * 100
print(xp_za_level(5))  # 500
print(xp_za_level(42))  # 4200
```

### Herní logika – je postava naživu?

Lambda funkce může vracet i `bool` hodnotu

```python
je_nazivu = lambda hp: hp > 0

print(je_nazivu(75))   # True
print(je_nazivu(0))    # False
print(je_nazivu(-10))  # False
```

### Kontrola hesla

```python
je_silne_heslo = lambda heslo: len(heslo) >= 8

print(je_silne_heslo("123"))        # False
print(je_silne_heslo("Admin123"))   # True
```

## Lambda vs `def` – kdy použít kterou variantu

| Vlastnost      | `lambda`                  | `def`                     |
| -------------- | ------------------------- | ------------------------- |
| Délka          | krátké, 1 řádek           | libovolně dlouhé          |
| Název          | nemusí mít (anonymní)     | musí mít                  |
| Výrazy/příkazy | jen jeden výraz           | může mít více příkazů     |
| `return`       | automaticky               | musíme napsat `return`    |
| Použití        | rychlé jednoduché funkce  | plnohodnotné funkce       |
| Čitelnost      | horší u složitějšího kódu | lepší u složitějšího kódu |

## Časté chyby

-   **Příliš složité lambda funkce** – pokud lambda má více než jednoduchou logiku, lepší je použít `def`
-   **Pokus o víc než jeden příkaz** – lambda může obsahovat jen jeden výraz, nikoliv více příkazů
-   **Zapomenuté `list(...)` kolem `map()` nebo `filter()`** – v Pythonu 3 vrací iterátor, nikoliv přímo seznam
-   **Nečitelný kód** – pokud není na první pohled jasné, co lambda dělá, raději použij pojmenovanou funkci s `def`

**Příklad špatného použití:**

```python
# Příliš složité, lepší použít def
vypocet = lambda x: x * 2 if x > 10 else x * 3 if x > 5 else x * 4
```

**Lepší řešení:**

```python
def vypocet(x):
    if x > 10:
        return x * 2
    elif x > 5:
        return x * 3
    else:
        return x * 4
```

## Funkce `sort()`, `filter()`, `map()`

Lambda funkce se často používají společně s funkcemi pro práci se listy a dictionary (seznamy, slovníky). `sort()` umožňuje seřadit data podle vlastního pravidla, `filter()` vybere jen prvky splňující podmínku a `map()` provede stejný výpočet nad každým prvkem listu/dictionary. Díky lambdám je možné tyto operace zapsat krátce a přehledně bez vytváření klasických funkcí pomocí def

### Lambda se `sort()` – seřazení podle vlastního pravidla

Funkce `sort()` umožňuje seřadit seznam. Pomocí parametru `key` můžeme určit, podle čeho se má řadit. Zde se lambda hodí perfektně.

**Seřazení studentů podle známky**

```python
studenti = [
    {"jmeno": "Jarmil", "znamka": 2},
    {"jmeno": "Anděla", "znamka": 1},
    {"jmeno": "Hvězďon", "znamka": 3}
]

studenti.sort(key=lambda student: student["znamka"])
print(studenti)
# [{'jmeno': 'Anděla', 'znamka': 1}, {'jmeno': 'Jarmil', 'znamka': 2}, {'jmeno': 'Hvězďon', 'znamka': 3}]
```

**Seřazení písniček podle délky názvu**

```python
songy = ["Bohemian Rhapsody", "Smells Like Teen Spirit", "Crawling", "Zombie"]
songy.sort(key=lambda song: len(song))
print(songy)  # ['Zombie', 'Crawling', 'Bohemian Rhapsody', 'Smells Like Teen Spirit']
```

### Lambda s `map()` – aplikace funkce na každý prvek

Funkce `map()` aplikuje funkci na každý prvek seznamu. Vrací iterátor, který musíme převést na list pomocí `list()`

**Přidání emoji k jménům**

```python
jmena = ["Jarmil", "Anděla", "Kvído"]
s_emoji = list(map(lambda jmeno: f"{jmeno} 🎮", jmena))
print(s_emoji)  # ['Jarmil 🎮', 'Anděla 🎮', 'Kvído 🎮']
```

**Přepočet teplot z Celsia na Fahrenheita**

```python
teploty_c = [0, 15, 25, 30]
teploty_f = list(map(lambda c: c * 9/5 + 32, teploty_c))
print(teploty_f)  # [32.0, 59.0, 77.0, 86.0]
```

### Lambda s `filter()` – filtrování seznamu

Funkce `filter()` vrací pouze ty prvky, pro které lambda vrátí `True`. Opět vrací iterátor, který převedeme na list.

**Filtrování hráčů s dostatečným levelem**

```python
levely = [1, 5, 10, 15, 20, 3, 12]
high_level = list(filter(lambda level: level >= 10, levely))
print(high_level)  # [10, 15, 20, 12]
```

**Zprávy obsahující spam**

```python
zpravy = ["Ahoj jak se máš?", "KLIKNI ZDE!!!", "Díky za včera", "VYHRÁL JSI!!!"]
spam = list(filter(lambda zprava: zprava.isupper(), zpravy))
print(spam)  # ['KLIKNI ZDE!!!', 'VYHRÁL JSI!!!']
```

## Návaznost na další kapitoly

Lambda funkce navazují na kapitolu [P05 - Funkce](P05%20-%20Funkce.md)

Funkce `map()` a `filter()` se často používají při práci se seznamy, více o seznamech najdeš v kapitole [P06 - List a tuple](P06%20-%20List%20a%20tuple.md).
