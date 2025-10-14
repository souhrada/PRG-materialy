# Exceptions v Pythonu - řešení potenciálních chyb

Během běhu programu může nastat - samozřejmě velmi výjimečně - **chyba**, která způsobí, že se program zastaví. Například se tak může stát, když:

- dělíme nulou
- snažíme se pracovat k neexistujícímu indexem
- převádíme písmenka na čísla
- načítáme neexistující soubor

Python v takovém případě **vyhodí výjimku** (exception) a program se zastaví.

---

Tzn. pokud nastane chyba a Python **vyhodí** (*raise*) výjímku (exception), program spadne. Proto se snažíme výjimkám předejít v podobě, nejčastěji tak, že do konzole vypíšeme hlášku, ale umožníme programu pokračovat dále.

---

## `try` / `except` - předcházení výjimkám

Když očekáváme, že může nastat chyba, použijeme klíčové slovo `try` v kombinaci s řešením dané situace `except`

```python
try:
    cislo = int(input("Zadej číslo: "))
    vysledek = 10 / cislo
    print("Výsledek je", vysledek)

except ZeroDivisionError: # chybová hláška pro dělení 0
    print("Nemůžeš dělit nulou!")

except ValueError: # chybová hláška pro chybu s hodnotou - např. očekáváme int ale přijde string
    print("To není platné číslo.")

```

Vysvětlení kódu výše ↑

- zkus provést kód v bloku `try`:

- pokud dojde k chybě, program skočí do `except`:, v závislosti na tom, k jaké chybě dojde

- pokud vše proběhne bez chyby, `except` se ignoruje

*Výsledek je, že program v případě chyby vypíše hlášku do konzole, ale pokračuje v práci dále. Bez try / except by se program přerušil.*

### `else` a `finally`

try / except lze rozšířit i o klíčová slova `else` a `finally`

- `else` se spustí, pokud nenastala žádná chyba

- `finally` se spustí vždy, ať chyba byla nebo ne – používá se např. na zavírání souborů


```python
try:
    x = int(input("Zadej číslo: "))
except ValueError:
    print("Chyba.")
else:
    print("Zadáno číslo:", x)
finally:
    print("Program končí.")
```


## Časté exceptions (výjimky)

| Typ chyby           | Kdy nastane                             |
| ------------------- | --------------------------------------- |
| `ZeroDivisionError` | dělení nulou                            |
| `ValueError`        | špatná hodnota (např. `int("abc")`)     |
| `IndexError`        | index mimo rozsah seznamu               |
| `KeyError`          | klíč neexistuje ve slovníku             |
| `TypeError`         | nekompatibilní typy (`"text" + 1`)      |
| `FileNotFoundError` | pokus o otevření neexistujícího souboru |

## `raise` - vlastní výjimka

Pomocí klíčového slova `raise` můžeme vyvolat exception (výjimku) i v případech, kdy by ji Python nevyvolal sám

```python
vek = int(input("Zadej věk: "))
if vek < 0:
    raise ValueError("Věk nemůže být záporný.")
```

alternativně si můžete vymyslet vlastní exeception

```python
vek = int(input("Zadej věk: "))
if vek < 0:
    raise TohleNedelej("Věk nemůže být záporný.")
```

V takovém případě ale musíme nejprve vytvořit `classu` pro tuto exception

```python
class TohleNedelej(Exception):
    """Tohle vyskočí, když někdo dělá něco co by neměl"""
    pass
```