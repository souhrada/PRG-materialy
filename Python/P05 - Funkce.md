# Funkce

Funkce jsou způsob jak zabalit a pojmenovat určitý blok kódu, který budeme chtít použít opakovaně. Díky pojmenování můžeme tento úsek kód později zavolat v případě potřeby. A třeba několikrát. Je to také možnost uspořádání a organizace našeho kódu - díky funkcím je kód jednodušší, přehlednější a méně se opakujeme

## Vytvoření v Pythonu

Pro vytvoření funkce používáme klíčové slovo `def`, za ním název funkce a závorky `()`

```python
def pozdrav():
    print("Ahoj!")

```

## Zavolání funkce

Funkce vytvořena výše je zabalený kód, který sám o sobě nic nedělá. Musíme jej nejprve zavolat, což provedeme tak, že napíšeme název funkce a závorky `()`

```python
pozdrav()

# Ahoj!

```

## Parametry a argumenty

Funkci můžeme vylepšit tak, že do závorek přidáme tzv. **parametry**. Parametr je taková proměnná pro naší funkci, kterou funkce přijímá a nějakým způsobem ji zpracuje. Při zavolání funkce poté dosadíme reálné hodnoty, tzv. **argumenty**. Lze si to představit jako možnost, jak do funkce dosadit input, se kterým bude poté funkce pracovat.

Pojem parametr tedy používáme při vytváření funkce, argument při jejím zavolání

Do funkce můžeme dosazovat i více parametrů/argumentů

```python
def pozdrav(jmeno):
    print(f"Ahoj {jmeno}!")

pozdrav("Anděla") # Ahoj Anděla!
pozdrav("Jarmil") # Ahoj Jarmil!
```

Kód výše s komentáři

```python
def pozdrav(jmeno): # <- parametr, který se chová jako proměnná
    print(f"Ahoj {jmeno}!") # <- náš parametr dosazený do printu, při zavolání funkce se nahradí reálnou hodnotou

pozdrav("Anděla") # <- argumen/input, tedy skutečná hodnota, který nám říká, že jmeno="Anděla" -> všude, kde je ve funkci parametr/proměnná jmeno bude dosazena hodnota "Anděla"
pozdrav("Jarmil") # <- funkci můžeme znovu použít, ale s jiným argumentem
```

### Defaultní hodnota

Při vytváření funkce mohu zvolit defaultní hodnotu parametru. Pokud pak později zavoláme funkci a nedosadíme žádný input (argument), fukce použije naši defaultní hodnotu místo toho

```python
def pozdrav(jmeno="Želmíra"):
    print(f"Ahoj {jmeno}!")

pozdrav("Vesna") # Ahoj Vesna!
pozdrav() # Ahoj Želmíra!
```

## `return`

Častokrát po funkci požadujeme, aby zpracovala kód a vrátila nám nějakou hodnotu zpět, kterou budeme moci dále použít nebo uložit pod proměnnou. Pro vrácení kódu používáme `return`.

`return` zároveň ukončí funkci, cokoliv se nachází pod return se neprovede

```python
def scitani(a, b):
    c = a + b
    return c

vysledek = secti(5, 9) # funkce vrátí výsledek součtu a my jej uložíme pod proměnnou
print(vysledek) # 14
```

Funkci výše lze zkrátit

```python
def scitani(a, b):
    return a + b
```

## Funkce `main()`

V Pythonu bývá standardem zabalit hlavní logiku kód do funkce `main()`, tak, aby kód neležel jen tak v našem souboru. Funkci `main()` poté voláme speciální konstrukcí

```python

def main():
    print("Toto je ukázka")

if __name__ == "__main__":
    main()
```

Podmínka `if __name__ == "__main__"` znamená, že kód se spustí pouze tehdy, když je soubor spuštěn přímo. V Pythonu můžeme náš soubor totiž spustit nejen přímo, ale také jej můžeme snadno importovat do jiného souboru (viz kapitola [P20 - Moduly](P20%20-%20Moduly.md))

Při každém spuštění kódu je Pythonem automaticky vytvořena proměnná `__name__`, za kterou je dosazena hodnota `__main__` pokud je kód spuštěn přímo a nebo název souboru, pokud je kód importován.

Příklad: mám soubor **ukazka.py**. Pokud jej spustím v konzoli přímo pomocí `python ukazka.py`, pod proměnnou `__name__` se dosadí `__main__`. Pokud ale soubor importuji do jiného souboru, např. **hokus.py** a spustím tento soubor, tak pod proměnnou `__name__` v **ukazka.py** bude uložena hodnota `ukazka`

Je zvykem používat `if __name__ == "__main__"` i v případě, že neplánujeme náš kód nikam importovat. Předcházíme tím potenciálním bugům

## Scope - viditelnost proměnných

Tzv. **scope** nám udává, kde platí naše proměnná. Máme local scope a global scope.

Pokud vytvořím proměnnou uvnitř funkce, tato proměnná existuje pouze v dané funkci a ostatní kód mimo naši funkci o ní nemá ponětí a proměnná pro něj neexistuje. Taková proměnná je **lokální (local scope)**

```python
def ahoj():
    jmeno = "Kvído"
    print(jmeno)

ahoj()
print(jmeno)  # Chyba! jmeno není definováno mimo funkci
```

Proměnná vytvořená mimo funkci existuje v celém programu. Je to tedy **globální proměnná (global scope)**

```python
jmeno = "Kvído"

def ahoj():
    print(jmeno)

ahoj() # Kvído, print funguje
print(jmeno) # Kvído, i tento print funguje
```

Pokud chci globální proměnnou přepsat uvnitř funkce, musíme ji nejdřív označit klíčovým slovem `global`. Pokud bychom ji neoznačili jako global, Python by uvnitř funkce vytvořil novou lokální proměnnou se stejným jménem a ignoroval by naši globální proměnnou

```python
jmeno = "Kvído"

def zmen_jmeno():
    global jmeno
    jmeno = "Kazimír

zmen_jmeno()
print(jmeno) # Kazimír
```

Obecně ale platí, že se chceme vyhnout častému využívání globálních proměnných. Pokud jich používáme mnoho, v dlouhém kódu o nich ztrácíme přehled a zvyšujeme tím pravděpodobnost vytvoření bugů

## Anonymní funkce - `lambda`

V Pythonu můžeme vytvářet také anonymní funkce. Ty vytváříme klíčovým slovem `lambda`. Celý syntax je `lambda argumenty: kód`. Lambda funkci poté můžeme uložit pod proměnnou nebo použít přímo uvnitř další funkce

```python
# lambda funkce s argumentem
pozdrav = lambda jmeno: f"Ahoj, {jmeno}!"
print(pozdrav("Jarmil"))  # Ahoj, Jarmil!

# lambda funkce bez argumentu

pozdrav = lambda: "Ahoj!"
print(pozdrav())  # Ahoj!

# lambda funkce spuštěna uvnitř další funkce, v našem případě print()

print((lambda jmeno: f"Ahoj, {jmeno}!")("Anděla"))
```

Více o `lambda` funkcích v kapitole [P10 - Lambda](P10%20-%20Lambda%20-%20anonymní%20funkce.md)
