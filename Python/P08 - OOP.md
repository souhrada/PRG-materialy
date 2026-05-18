# Objektově orientované programování (OOP), aneb classy

OOP je styl programování, který umožňuje vytvářet si **vlastní datové typy** – tzv. **objekty**. Objekty slouží k uspořádání a organizování kódu, podobně jako funkce (objekty jsou však trochu komplexnější). V Pythonu vytváříme objekty pomocí klíčového slova `class`.



### Kdy používat OOP?

- když chceme spojit data a funkce dohromady
- když se snažíme modelovat skutečné objekty (postavy, předměty, účty…)
- když chceme kód, který má jasnou strukturu a je snadné jej rozšířit
- když nechceme stále opakovat stejný kód



## `class`

Class (třída) je v Pythonu synonymum pro objekty. Názvy class píšeme s velkým prvním písmenkem

```python
class Pokemon:
    def __init__(self, jmeno, element):
        self.jmeno = jmeno
        self.element = element

    def zavolani(self):
        print(f"{self.jmeno}, volím si tebe!")
```

### Konstruktor, atributy, metody a self

*	`__init__` je tzv. **konstruktor** – spouští se při vytvoření objektu - konstruktor musí mít parametr self, ostatní parametry, v našem případě *jmeno* a *element* jsou dobrovolné, podobně jako u klasických funkcí
* `self.jmeno` a `self.element` jsou vlastnosti objektu (tzv. **atributy**)
* objekt může mít také svou vlastní funkci, např `zavolani(self)` - říkáme jim **metody**, ale je to pouze technický pojem, chovají se prakticky stejně jako funkce, které známe
* **`self`** značí aktuální objekt (něco jako „já“ nebo "tohle / tohoto")


Proměnné se `self` jsou něco jako vnitřní proměnné pro naše objekty (classy). Díky nim můžeme uložit nějaký údaj a k němu přistupovat v rámci celé classy - každá metoda (funkce) v classe bude mít přístup k této proměnné se self. Proměnná, která je bez self žije jen uvnitř jedné metody a po jejím skončení zmizí

### Instance

Classa je však pouze blueprint, plánek na vytvoření objektu. Abychom s objektem mohli pracovat v kódu, musíme jej vytvořit (čemuž říkáme vytvořit jeho instanci) a uložit jej pod proměnnou

```python
bulbasaur = Pokemon("Charmander", "oheň")
moje_auto.zavolani()  # "Charmander, volím si tebe!".
```


### Přepisování

Podobně jako můžeme vypsat attribut classy, tak jej můžeme i přepsat

```python
pikachu = Pokemon("Pikachu", "elektrický")

pikachu.jmeno = "Raichu"
```

## Inheritance (dědičnost)

Pomocí **inheritance** můžeme vytvořit novou classu, která **přebírá vlastnosti a metody** z jiné classy. Té původní se říká parent class, nové pak child class

To nám umožňuje *znovupoužívat kód* bez nutnosti kopírování



Příklad: class `Zvire` a její potomci

```python
class Zvire:
    def __init__(self, jmeno):
        self.jmeno = jmeno

    def pozdrav(self):
        print(f"Ahoj, jsem {self.jmeno}.")

class Pes(Zvire):
    def stekej(self):
        print("Haf!")

class Kocka(Zvire):
    def mnoukni(self):
        print("Mňau!")



pluto = Pes("Pluto")
pluto.pozdrav()   # Ahoj, jsem Pluto. --> dědí pozdrav() ze Zvire
pluto.stejej()    # Haf --> vlastní metoda

hello_kitty = Kocka("Hello Kitty")
hello_kitty.pozdrav()
hello_kitty.mnoukni()

```

### `super()`

Pokud chceme, aby classa zdělila část předchozí metody a dále ji upravit, můžeme použít `super()`

```python
class Pes(Zvire):
    def pozdrav(self):
        super().pozdrav() # funkce zděděná ze Zvire
        print("Nashledanou") # po pozdravu ze Zvire se dopíše ještě tento nový řádek
```

`super()` platí také pro `__init__`, kde se používá nejčastěji a umožní nám rozšířit počet parametrů konstruktoru 
*Pozor super() nemá self*

```python
class Kocka(Zvire):
    def __init__(self, jmeno)
        super().__init__(jmeno, barva):
        self.barva = barva

# nyní bude naše classa přijímat další vlastnost, barvu        
hello_kitty = Kocka("Hello Kitty", "růžová") 
```









