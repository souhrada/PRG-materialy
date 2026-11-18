# Rozdíly mezi Pythonem a Javascriptem

## Odsazování

V Pythonu je nezbytné správně odsazovat. Kdežto v Javascriptu je odsazování dobrovolné a jeho hlavní důvod je čitelnost a zachování dobrého mentálního stavu vašeho učitele, **v Pythonu je odsazování povinné (!)** - Python totiž nepoužívá složené závorky pro označení, kde začíná a končí kód. Místo toho používá právě odsazení.

## snake_case vs camelCase

V Pythonu je standard používat tzv. snake_case po pojmenovávání víceslovných proměnných.

Javascript

```js
let krestniJmeno = "Kvído"
```

Python

```python
krestni_jmeno = "Kvído"
```

## Komentáře

Komentáře v Pythonu začínáme pomocí "hashtagu" `#`

## Obecné

Místo `console.log()` používáme v Pythonu `print()`

Příkaz `input()` přijímá uživatelův input v příkazovém řádku. Input přijímá vždy `string`, který na `int` můžeme změnit pomocí funkce `int()`

Javascript

```js
console.log("Ahoj")
```

Python

```python
# Vypíše ahoj
print("Ahoj")

# Přijme input z příkazového řádku
uziv_input = input()

# Vypíše uživatelův input
print(uziv_input)

```

## Vytváření proměnných

Python nepoužívá žádné klíčové slovo jako `var`, `let` nebo `const`, pokud chci vytvořit proměnnou, stačí napsat její jméno a =

Javascript

```js
let text =
    "What  is the answer to the ultimate question of life, the universe, and everything"
let cislo = "42"
```

Python

```python
text = "What  is the answer to the ultimate question of life, the universe, and everything"
cislo = 42
```

Pozor, v Pythonu nefunguje syntax známý z Javascriptu `cislo++` zvýšení hodnoty proměnné o 1. Musíme používat `cislo += 1`

## Array vs List

Místo názvue `array` používáme v Pythonu slovo `list`. Jinak se chovájí téměř totožně. Aneb array = list.

## Podmínky

Logika naprosto stejná jako v Javascriptu. V Pythonu ale nepoužíváme ani kulaté, ani složené závorky, místo toho používáme dvojtečku. Také zkracujeme `else if` na `elif`.

Javascript

```js
let skore = window.prompt("Jaké je tvé skóre?")

if (skore === 90) {
    znamka = "Výborně"
} else if (skore === 80) {
    znamka = "Chvalitebně"
} else {
    znamka = "Nedostatečně"
}
```

Python

```python
skore = int(input("Jaké je tvé skóre?"))

if skore == 90:
  znamka = "Výborně"
elif skore == 80:
  znamka = "Chvalitebně"
else:
  znamka = "Nedostatečně"
```

## Cyklus while

Obdobně jako v podmínkách, také tady nepoužíváme závorky. Jinak je logika naprosto stejná.

Javascript

```js
skore = parseInt(window.prompt("Jaké je tvé skóre?"))
while (skore < 60) {
    console.log("Snaž se víc")
    skore = parseInt(window.prompt("Jaké je tvé skóre?")}
}
```

Python

```python
skore2 = int(input("Jaké je tvé skóre?"))
while skore2 < 60:
  print("Snaž se víc")
  skore2 = int(input("Jaké je tvé skóre?"))
```

U nekonečného cyklu pozor, boolean `True` je v Pythonu s velkým písmenkem, tzn. `while True:`

V Pythonu neexistuje `do while`

## Cyklus for

U cyklu for nalezneme největší rozdíl. V Pythonu zapisujeme cyklus for následujícím způsobem `for promenna in nejaky_seznam`

Javascript

```js
// Vypsání čísel od 0-10
for (let i = 0; i < 11; i++) {
    console.log(i)
}

const seznam = ["Kulík", "Dulík", "Bubík"]

// Vypsání seznamu
for (let i = 0; i < seznam.length; i++) {
    console.log(seznam[i])
}
```

Python

```python
# Vypsání čísel od 0-10
for x in range(0, 11):
  print(x)

seznam = ["Kulík", "Dulík", "Bubík"]

# Vypsání seznamu
for jmeno in seznam:
    print(jmeno)
```

## Funkce

V Pythonu používáme klíčové slovo `def` místo `function` známého z Javascriptu

Javascript

```js
function pozdrav() {
    console.log("Ahoj!")
}
```

Python

```python
def pozdrav():
  print("Ahoj!")

```
