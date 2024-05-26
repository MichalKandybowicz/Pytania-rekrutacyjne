# Lista Pytań z Odnośnikami do Odpowiedzi

## Spis Treści

1. [Jakie są różnice między list comprehension a generator expressions pod względem wydajności?](#pytanie-1)
2. [Jak działa mechanizm zarządzania pamięcią w Pythonie. Jak działa garbage collection (GC) i kiedy może być wywołana ręcznie?](#pytanie-2)
3. [Jak implementowane są dekoratory w Pythonie i w jakich przypadkach są szczególnie użyteczne?](#pytanie-3)
4. [Jakie techniki stosujemy do profilowania kodu Pythona w celu zidentyfikowania wąskich gardeł?](#pytanie-4)
5. [Opisz, jak działa __getitem__, __setitem__ i __delitem__ w kontekście tworzenia niestandardowych typów kontenerów.](#pytanie-5)
6. [Jak działają wyrażenia regularne w Pythonie? Jakie są najczęściej używane funkcje w module re?](#pytanie-6)
7. [Opisz różnice między podejściem proceduralnym, obiektowym i funkcyjnym w programowaniu w Pythonie.](#pytanie-7)
8. [Jakie są różnice między @property a bezpośrednim dostępem do atrybutów klasy? Jakie są zalety używania @property?](#pytanie-8)
9. [Jak działają itertools i jakie są najczęściej używane funkcje tego modułu?](#pytanie-9)
10. [Jakie są różnice między funkcjami map(), filter(), a reduce()? Jakie są ich typowe zastosowania?](#pytanie-10)
11. [Czym jest i jak implementujesz memoizację w Pythonie?](#pytanie-11)
12. [Opisz zastosowanie i działanie funkcji super() w Pythonie.](#pytanie-12)
13. [Jakie są główne różnice między __init__ a __new__ w Pythonie?](#pytanie-13)
14. [Jakie są różnice między deepcopy a shallowcopy? Jakie problemy mogą się pojawić przy używaniu każdego z nich?](#pytanie-14)
15. [Jak działają sloty (__slots__) w Pythonie i jakie są ich zalety i wady?](#pytanie-15)
16. [Jak działają moduły abc (Abstract Base Classes) i do czego są używane?](#pytanie-16)
17. [Jakie są różnice między hash() a __hash__()? Jakie są zasady tworzenia hashable obiektów w Pythonie?](#pytanie-17)
18. [Jak zaimplementować wielowątkowość w Pythonie przy użyciu modułu threading? Jakie są pułapki i jak je unikasz?](#pytanie-18)
19. [Jakie są różnice między metodami __eq__() a __cmp__() w kontekście porównywania obiektów?](#pytanie-19)
20. [Jak zaimplementować własny kontekst menedżera (context manager) za pomocą klasy i dekoratora contextlib.contextmanager?](#pytanie-20)
21. [Jakie są różnice między yield a return w funkcjach Pythona?](#pytanie-21)
22. [Jakie są różnice między global a nonlocal? Jakie są ich zastosowania?](#pytanie-22)
23. [Jak działa moduł inspect w Pythonie i jakie są jego zastosowania?](#pytanie-23)
24. [Jakie są różnice między deepcopy a shallowcopy? Jakie problemy mogą się pojawić przy używaniu każdego z nich?](#pytanie-24)
25. [Jak działają funkcje wyższego rzędu w Pythonie? Podaj przykłady ich zastosowania.](#pytanie-25)
26. [Jakie są różnice między standardowym modułem logging a innymi popularnymi bibliotekami do logowania?](#pytanie-26)
27. [Jak działają mechanizmy serializacji w Pythonie (np. pickle, json)?](#pytanie-27)
28. [Jakie są różnice między set a frozenset w Pythonie? Jakie są ich typowe zastosowania?](#pytanie-28)
29. [Jakie są różnice między metodami __eq__ a __cmp__?](#pytanie-29)


---

## Pytania i Odpowiedzi

### Pytanie 1
#### Jakie są różnice między list comprehension a generator expressions?
[Powrót do spisu treści](#spis-treści)

List comprehensions i generator expressions to dwie konstrukcje w Pythonie do tworzenia sekwencji danych. 
Chociaż mają bardzo podobną składnię, różnią się pod względem wydajności, szybkości i zachowania. 

**Tworzenie Obiektów:**

List Comprehensions: Tworzą pełną listę w pamięci. Oznacza to, że wszystkie elementy są generowane od razu i przechowywane w pamięci.

Generator Expressions: Tworzą generator, który produkuje elementy na bieżąco, jeden po drugim, gdy są potrzebne. Nie tworzy pełnej listy w pamięci.

**Zarządzanie Pamięcią:**

List Comprehensions: Może być mniej wydajne, jeśli lista jest duża, ponieważ cała lista jest przechowywana w pamięci.

Generator Expressions: Bardziej efektywne pamięciowo, ponieważ elementy są generowane "leniwie" (lazy evaluation) i nie są przechowywane wszystkie naraz w pamięci.

**Czas Wykonania:**

List Comprehensions: Mają tendencję do bycia szybszymi, jeśli potrzebujesz przetworzyć wszystkie elementy, ponieważ cała lista jest dostępna od razu.

Generator Expressions: Mogą być wolniejsze w przetwarzaniu wszystkich elementów, ponieważ elementy są generowane na żądanie, co dodaje narzut czasowy dla każdej operacji "next".

**Kiedy wykorzystywać:**

List Comprehensions: Są idealne, gdy potrzebujesz dostępu do wszystkich elementów naraz lub gdy wynikowa lista ma być użyta wielokrotnie.

Generator Expressions: Są lepsze, gdy pracujesz z dużymi zbiorami danych lub strumieniami danych, których nie można załadować w całości do pamięci lub gdy chcesz przetworzyć elementy tylko raz.
```python
# PRZYKŁADY
# List comprehension
list_comp = [x * 2 for x in range(10)]
print(list_comp)
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# Iterating over List comprehension 
for x in list_comp:
    print(x)
# 0, 2, 4, 6, 8, 10, 12, 14, 16, 18 (one by one)

# Generator expression
gen_exp = (x * 2 for x in range(10))
print(gen_exp)
# <generator object <genexpr> at 0x...>

# Iterating over generator 
for x in gen_exp:
    print(x)
# 0, 2, 4, 6, 8, 10, 12, 14, 16, 18 (one by one)

```

### Pytanie 2
#### Jak działa mechanizm zarządzania pamięcią w Pythonie. Jak działa garbage collection (GC) i kiedy może być wywołana ręcznie?
[Powrót do spisu treści](#spis-treści)

Mechanizm zarządzania pamięcią w Pythonie odpowiada za przydzielanie i zwalnianie pamięci w aplikacjach napisanych w tym języku. Oto, jak działa w prostych słowach:


**Przydzielanie pamięci:** Kiedy tworzysz nowy obiekt (np. liczbę, listę, słownik), Python automatycznie przydziela dla niego pamięć. Nie musisz się martwić o zarządzanie tą pamięcią ręcznie.

**Zwalnianie pamięci:** Gdy obiekt nie jest już potrzebny (czyli nie ma żadnej zmiennej, która by się do niego odwoływała), pamięć, którą zajmował, powinna być zwolniona, aby mogła być użyta przez inne obiekty.

**Garbage Collection (GC) - Zbieranie Śmieci**
Garbage collection to mechanizm, który automatycznie zwalnia pamięć zajmowaną przez obiekty, które nie są już używane. W Pythonie działa to na dwa główne sposoby:

**Zliczanie referencji:** Każdy obiekt ma licznik, który mówi, ile zmiennych (referencji) się do niego odwołuje. Kiedy licznik spada do zera, obiekt jest usuwany, a pamięć zwalniana.

**Cykliczne zależności:** Python ma mechanizm wykrywania i usuwania cyklicznych zależności (np. dwa obiekty, które odwołują się do siebie nawzajem, ale nie są używane w kodzie). Do tego używa tzw. generacyjnego garbage collectora, który okresowo sprawdza obiekty w poszukiwaniu cykli.

Ręczne wywołanie garbage collection
Choć Python automatycznie zarządza pamięcią, możliwe jest wywołanie go ręcznie, można to zrobić, używając modułu `gc`:

```python
# PRZYKŁAD
import gc

# Funkcja do stworzenia cyklu odniesień
def create_cycle():
    list_a = []
    list_b = [list_a]
    list_a.append(list_b)
    # Po zakończeniu funkcji list_a i list_b nadal istnieją w pamięci jako cykl odniesień

create_cycle()

# Przed uruchomieniem GC
print(f"Objects in memory: {len(gc.get_objects())}")
# Uruchomienie GC ręcznie
gc.collect()

# Po uruchomieniu GC
print(f"Objects in memory: {len(gc.get_objects())}")
```


### Pytanie 3
#### Jak implementowane są dekoratory w Pythonie i w jakich przypadkach są szczególnie użyteczne?
[Powrót do spisu treści](#spis-treści)

Dekoratory w Pythonie są specjalnymi funkcjami, które modyfikują zachowanie innych funkcji lub metod. 
Pozwalają one na "opakowanie" jednej funkcji przez inną, co daje możliwość dodania dodatkowej funkcjonalności przed 
lub po wykonaniu oryginalnej funkcji, bez zmiany jej kodu źródłowego. 

Dekoratory są szczególnie użyteczne w następujących przypadkach:

1. Logowanie i monitorowanie: Umożliwiają śledzenie wywołań funkcji, co jest przydatne przy debugowaniu i monitorowaniu działania aplikacji.
```python
# PRZYKŁAD
def simple_decorator(func):
    def wrapper():
        print("Przed wywołaniem funkcji")
        func()
        print("Po wywołaniu funkcji")
    return wrapper

@simple_decorator
def say_hello():
    print("Hello!")

say_hello()
```
2. Autoryzacja i uwierzytelnianie: Mogą sprawdzić, czy użytkownik ma odpowiednie uprawnienia przed wykonaniem określonej funkcji.
```python
def requires_auth(funkcja):
    def wrapper(user, *args, **kwargs):
        if not user.get('is_authenticated'):
            raise PermissionError("User is not authenticated")
        return funkcja(user, *args, **kwargs)
    return wrapper

@requires_auth
def access_secure_data(user):
    return "Secure Data"

user = {'is_authenticated': True}
print(access_secure_data(user))

user = {'is_authenticated': False}
try:
    print(access_secure_data(user))
except PermissionError as e:
    print(e)

```
3. Modyfikacja wejścia/wyjścia: Pozwalają na modyfikowanie argumentów przekazywanych do funkcji oraz wyników zwracanych przez funkcję.
```python
def uppercase_output(funkcja):
    def wrapper(*args, **kwargs):
        result = funkcja(*args, **kwargs)
        return result.upper()
    return wrapper

@uppercase_output
def greet(name):
    return f"Hello, {name}"

print(greet("world"))

```
4. Cachowanie wyników: Przyspieszają działanie funkcji przez zapamiętywanie wyników dla już obliczonych argumentów.
```python
def cache(funkcja):
    przechowalnia = {}
    def wrapper(*args):
        if args in przechowalnia:
            return przechowalnia[args]
        wynik = funkcja(*args)
        przechowalnia[args] = wynik
        return wynik
    return wrapper

@cache
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(10))

```
5. Kontrola dostępu: Mogą ograniczać dostęp do funkcji, np. ze względu na czas (limity wywołań).
```python
import time

def rate_limit(funkcja):
    last_called = [0]  # Używamy listy do przechowania zmiennej w zamknięciu

    def wrapper(*args, **kwargs):
        now = time.time()
        if now - last_called[0] < 1:  # Limituje wywołania do 1 na sekundę
            raise RuntimeError("Function called too frequently")
        last_called[0] = now
        return funkcja(*args, **kwargs)
    return wrapper

@rate_limit
def do_something():
    print("Function executed")

try:
    do_something()
    time.sleep(0.5)
    do_something()
except RuntimeError as e:
    print(e)

time.sleep(1)
do_something()

```

### Pytanie 4
#### Jakie techniki stosujemy do profilowania kodu Pythona w celu zidentyfikowania wąskich gardeł?
[Powrót do spisu treści](#spis-treści)

Profilowanie kodu Pythona jest kluczowe do identyfikowania wąskich gardeł wydajnościowych i optymalizacji aplikacji. 
Na rynku dostępnych jest wiele rozwiazań, najprostzrym sposobem jest wykonanie "stopera" dzięki `timeit`, nadaje się on doskonale do mikrobenchmarków, czyli do mierzenia czasu wykonywania małych fragmentów kodu.


```python
# PRZYKŁAD
import timeit

def funkcja_do_testowania():
    suma = 0
    for i in range(10000):
        suma += i
    return suma

czas = timeit.timeit('funkcja_do_testowania()', globals=globals(), number=1000)
print(f"Czas wykonania: {czas:.5f} sekund")
```

`cProfile` to wbudowane narzędzie w Pythonie do profilowania. Można go użyć do mierzenia czasu wykonywania funkcji i identyfikowania najbardziej kosztownych fragmentów kodu.

```python
import cProfile
import pstats

def funkcja_do_profilowania():
    # Przykładowa funkcja do profilowania
    suma = 0
    for i in range(10000):
        suma += i
    return suma

cProfile.run('funkcja_do_profilowania()', 'profil_output')

# Wyświetlenie wyników w czytelnej formie
p = pstats.Stats('profil_output')
p.sort_stats('cumulative').print_stats(10)
```

Poza tym można skożystać z bardziej zaawansowanych narzędzi: 
`line_profiler` - jest narzędziem do profilowania kodu linia po linii. Jest to szczególnie przydatne 
narzędzie do dokładnej analizy czasu wykonania poszczególnych linii kodu. Dzięki niemu możesz zidentyfikować 
konkretne linie kodu, które są najbardziej kosztowne pod względem czasu wykonania.
`memory_profiler` - można dokładnie monitorować zużycie pamięci w trakcie wykonywania programu, co jest niezbędne do 
identyfikacji problemów związanych z zarządzaniem pamięcią i optymalizacją wydajności.
`Py-Spy` - umożliwia monitorowanie zużycia procesora przez aplikację oraz identyfikowanie gorących punktów, czyli 
fragmentów kodu, które zużywają najwięcej zasobów procesora. Jest to przydatne narzędzie do diagnostyki wydajnościowej 
i identyfikacji wąskich gardeł w aplikacji.




### Pytanie 5
#### Opisz, jak działa __getitem__, __setitem__ i __delitem__ w kontekście tworzenia niestandardowych typów kontenerów.
[Powrót do spisu treści](#spis-treści)

`__getitem__,` `__setitem__` i `__delitem__` to specjalne metody w Pythonie, które pozwalają na dostęp, ustawienie i 
usunięcie elementów z niestandardowych typów kontenerów, takich jak klasy, które zachowują się jak listy, słowniki 
lub inne kontenery.

1. `__getitem__(self, key)`
Metoda ta jest wywoływana, gdy próbujemy uzyskać dostęp do elementu kontenera za pomocą operatora 
indeksowania []. Akceptuje ona jeden argument, którym jest klucz lub indeks, za pomocą którego chcemy uzyskać 
dostęp do elementu.
```python
# PRZYKŁAD
class MojaLista:
    def __init__(self, dane):
        self.dane = dane

    def __getitem__(self, indeks):
        return self.dane[indeks]

moja_lista = MojaLista([1, 2, 3, 4, 5])
print(moja_lista[2])  # Wyświetli: 3

```

2. `__setitem__(self, key, value)`
Metoda ta jest wywoływana, gdy próbujemy przypisać wartość do elementu kontenera za pomocą operatora indeksowania []. 
Akceptuje dwa argumenty: klucz lub indeks oraz wartość, którą chcemy przypisać.
```python
# PRZYKŁAD
class MojaLista:
    def __init__(self, dane):
        self.dane = dane

    def __setitem__(self, indeks, wartosc):
        self.dane[indeks] = wartosc

moja_lista = MojaLista([1, 2, 3, 4, 5])
moja_lista[2] = 10
print(moja_lista.dane)  # Wyświetli: [1, 2, 10, 4, 5]

```
3. `__delitem__(self, key)`

Metoda ta jest wywoływana, gdy próbujemy usunąć element z kontenera za pomocą operatora del i indeksowania []. 
Akceptuje tylko jeden argument: klucz lub indeks elementu, który chcemy usunąć.

```python
class MojaLista:
    def __init__(self, dane):
        self.dane = dane

    def __delitem__(self, indeks):
        del self.dane[indeks]

moja_lista = MojaLista([1, 2, 3, 4, 5])
del moja_lista[2]
print(moja_lista.dane)  # Wyświetli: [1, 2, 4, 5]
```

Dzięki tym specjalnym metodom możliwe jest tworzenie niestandardowych typów kontenerów w Pythonie, które mogą 
zachowywać się jak wbudowane typy, takie jak listy czy słowniki. Pozwalają one na dostosowanie zachowania kontenera 
do indywidualnych potrzeb, na przykład poprzez niestandardowe operacje podczas uzyskiwania, ustawiania lub usuwania 
elementów.


### Pytanie 6
#### Jak działają wyrażenia regularne w Pythonie? Jakie są najczęściej używane funkcje w module re?
[Powrót do spisu treści](#spis-treści)

Wyrażenia regularne w Pythonie są narzędziem do manipulowania i przetwarzania tekstów za pomocą wzorców. Moduł `re` w 
Pythonie dostarcza funkcji i obiektów do obsługi wyrażeń regularnych.

Jak działają wyrażenia regularne?
Wyrażenia regularne opisują wzorce znaków, które są używane do wyszukiwania i manipulowania tekstami. Mogą zawierać specjalne znaki oraz zwykłe znaki, które definiują, jakie wzorce są dopasowywane w tekście.

Przykładowe specjalne znaki:

`.`  Dopasowuje dowolny pojedynczy znak (oprócz nowej linii).

`^`  Dopasowuje początek linii.

`$`  Dopasowuje koniec linii.

`*`  Dopasowuje zero lub więcej wystąpień poprzedniego znaku.

`+`  Dopasowuje jeden lub więcej wystąpień poprzedniego znaku.

`?`  Dopasowuje zero lub jedno wystąpienie poprzedniego znaku (opcjonalny).

`\ `  Oznacza specjalne sekwencje lub kontroluje znaki (np. \d - cyfra, \s - biały znak, \w - znak alfanumeryczny).

`[]`  Dopasowuje pojedynczy znak z zakresu lub zestawu znaków.

Najczęściej używane funkcje w module re:
re.search(pattern, string, flags=0): Szuka pierwszego dopasowania wzorca w całym tekście.
```python
import re
result = re.search(r'is', 'This is a test string.')
print(result)
# <re.Match object; span=(2, 4), match='is'>

```
re.match(pattern, string, flags=0): Sprawdza, czy wzorzec pasuje do początku tekstu.

```python
import re
result = re.match(r'This', 'This is a test string.')
print(result)
# <re.Match object; span=(0, 4), match='This'>

```
re.findall(pattern, string, flags=0): Znajduje wszystkie dopasowania wzorca w tekście i zwraca listę wyników.

```python
import re
result = re.findall(r'\d+', 'There are 10 apples and 20 oranges.')
print(result)
# ['10', '20']

```
re.sub(pattern, repl, string, count=0, flags=0): Zastępuje wszystkie wystąpienia wzorca w tekście danym łańcuchem.

```python
import re
result = re.sub(r'\s+', '_', 'This is a test string.')
print(result)
# This_is_a_test_string.

```
re.split(pattern, string, maxsplit=0, flags=0): Dzieli tekst na części, korzystając z wzorca jako separatora.

```python
import re
result = re.split(r'\s+', 'This is a test string.')
print(result)
# ['This', 'is', 'a', 'test', 'string.']

```
re.compile(pattern, flags=0): Kompiluje wyrażenie regularne do obiektu wzorca, który może być później używany do dopasowywania tekstu.

```python
import re
pattern = re.compile(r'\d+')
result = pattern.findall('There are 10 apples and 20 oranges.')
print(result)
# ['10', '20']
```
Te funkcje są podstawowymi narzędziami w pracy z wyrażeniami regularnymi w Pythonie. Pozwalają one na przeszukiwanie, 
dopasowywanie, podział i zamianę tekstu zgodnie z określonymi wzorcami.


### Pytanie 7
#### Opisz różnice między podejściem proceduralnym, obiektowym i funkcyjnym w programowaniu w Pythonie.
[Powrót do spisu treści](#spis-treści)

1.Podejście proceduralne:

W podejściu proceduralnym program jest strukturalnie zorganizowany wokół procedur (funkcji), które wykonują konkretne zadania na danych. Kod jest sekwencyjny i wykonywany od góry do dołu. Główne cechy podejścia proceduralnego to:

**Procedury**: Podstawowymi elementami są procedury (funkcje), które wykonują konkretne zadania na danych.

**Zmienne** globalne: Dane są zwykle przechowywane jako zmienne globalne, do których procedury mają dostęp.

**Proste struktury danych**: Używane są proste struktury danych, takie jak listy, krotki, słowniki itp.

**Prostota**: Jest to proste podejście, które jest łatwe do zrozumienia i stosowania w małych projektach.
```python
def oblicz_sume(a, b):
    return a + b

a = 10
b = 20
suma = oblicz_sume(a, b)
print(suma)
```
2.Podejście obiektowe:

W podejściu obiektowym program jest zorganizowany wokół obiektów, które są instancjami klas. Obiekty te przechowują dane (atrybuty) i metody (funkcje), które mogą operować na tych danych. Główne cechy podejścia obiektowego to:

**Klasy i obiekty**: Kod jest zorganizowany wokół klas, które definiują strukturę i zachowanie obiektów.
**Hermetyzacja**: Klasy mogą ukrywać swoje wewnętrzne implementacje, a dostęp do danych może być kontrolowany przez metody dostępowe (getter i setter).
**Dziedziczenie**: Klasy mogą dziedziczyć cechy i metody po innych klasach.
**Polimorfizm**: Obiekty różnych klas mogą być traktowane jednolicie, co umożliwia wykonywanie tych samych operacji na różnych typach danych.
```python
class Kalkulator:
    def __init__(self, a, b):
        self.a = a
        self.b = b
    
    def oblicz_sume(self):
        return self.a + self.b

kalkulator = Kalkulator(10, 20)
suma = kalkulator.oblicz_sume()
print(suma)
```
3.**Podejście funkcyjne**:
W podejściu funkcyjnym program jest zorganizowany wokół funkcji, które są traktowane jako pierwszorzędne obiekty. Funkcje te mogą być przekazywane jako argumenty do innych funkcji, zwracane jako wartości z funkcji i przechowywane jako zmienne. Główne cechy podejścia funkcyjnego to:

Funkcje pierwszego rzędu: Funkcje mogą być przypisywane do zmiennych, przekazywane jako argumenty i zwracane jako wartości.
Bezstanowość: Funkcje nie mają stanu wewnętrznego i operują tylko na swoich argumentach.
Unikanie efektów ubocznych: Stara się unikać efektów ubocznych, co oznacza, że funkcje nie powinny modyfikować danych poza swoim zakresem.
Rekurencja: Często używa rekurencji do iteracji i przetwarzania danych.
```python
def oblicz_sume(a, b):
    return a + b

a = 10
b = 20
suma = oblicz_sume(a, b)
print(suma)
```
W Pythonie można łączyć te trzy podejścia w jednym programie w zależności od potrzeb i preferencji projektowych.
Jednak zwykle Python zachęca do używania podejścia obiektowego ze względu na jego elastyczność i możliwość ponownego użycia kodu.

### Pytanie 8
#### Jakie są różnice między @property a bezpośrednim dostępem do atrybutów klasy? Jakie są zalety używania @property?

[Powrót do spisu treści](#spis-treści)


`@property` jest dekoratorem w Pythonie, który umożliwia definiowanie metod dostępowych do atrybutów klasy. 
Pozwala to na kontrolę dostępu do atrybutów oraz na wykonywanie dodatkowych działań podczas odczytu lub 
zapisu wartości atrybutu. Oto różnice między użyciem @property a bezpośrednim dostępem do atrybutów klasy:
1. Bezpośredni dostęp do atrybutów klasy:
```python
# Bezpośredni dostęp: Atrybut _atrybut jest dostępny publicznie,
# może być odczytywany i zapisywany bezpośrednio przez użytkownika klasy.
class Klasa:
    def __init__(self):
        self._atrybut = None

obiekt = Klasa()
obiekt._atrybut = "wartość"
print(obiekt._atrybut)
```
2. Użycie `@property:`

```python
# Używanie @property: Metoda atrybut jest teraz udekorowana dekoratorem @property, 
# co sprawia, że wygląda jak atrybut, ale jest to metoda. 
# Nie można jej przypisać wartości bezpośrednio, ale można ją wywoływać jak atrybut.
class Klasa:
    def __init__(self):
        self._atrybut = None
    
    @property
    def atrybut(self):
        return self._atrybut

obiekt = Klasa()
obiekt.atrybut = "wartość"  # Wywoła błąd AttributeError
print(obiekt.atrybut)
```

### Zalety używania @property:

**Kontrola dostępu**: Pozwala na kontrolowanie dostępu do atrybutów klasy, umożliwiając definiowanie niestandardowych działań podczas odczytu i zapisu wartości atrybutu.

**Enkapsulacja**: Pomaga w enkapsulacji danych, co oznacza, że można ukryć wewnętrzną implementację atrybutów i zapewnić bezpieczny dostęp do nich.

**Dostosowanie interfejsu**: Umożliwia definiowanie interfejsu klasy w sposób bardziej zrozumiały i przyjazny dla użytkownika.

**Łatwa do zrozumienia i utrzymania**: Pomaga w tworzeniu bardziej zrozumiałego i elastycznego kodu, który jest łatwiejszy do utrzymania i rozszerzania w przyszłości.



### Pytanie 9
#### Jak działają itertools i jakie są najczęściej używane funkcje tego modułu?
[Powrót do spisu treści](#spis-treści)

itertools jest modułem w Pythonie, który zawiera zestaw narzędzi do tworzenia efektywnych iteratorów. Iteratory są 
obiektami, które umożliwiają przeglądanie sekwencji danych, jednocześnie zajmując minimalną ilość pamięci. itertools 
oferuje wiele przydatnych funkcji do manipulowania iteratorami i generowania iterowalnych sekwencji danych.

Oto kilka najczęściej używanych funkcji z modułu itertools:

1. itertools.chain(*iterables)
Funkcja chain łączy wiele iterowalnych obiektów w jeden długi iterator.

```python
import itertools

lista1 = [1, 2, 3]
lista2 = ['a', 'b', 'c']
łańcuch = itertools.chain(lista1, lista2)

for element in łańcuch:
    print(element)
```
2. itertools.cycle(iterable)
Funkcja cycle tworzy nieskończony iterator, który cyklicznie powtarza elementy z danego iterowalnego obiektu.

```python
import itertools

cykl = itertools.cycle([1, 2, 3])

for _ in range(5):
    print(next(cykl))
```
3. itertools.count(start=0, step=1)
Funkcja count tworzy nieskończony iterator, który generuje liczby zaczynając od wartości start z określonym krokiem step.

```python
import itertools

licznik = itertools.count(start=1, step=2)

for _ in range(5):
    print(next(licznik))
```
4. itertools.product(*iterables, repeat=1)
Funkcja product tworzy iterator zawierający iloczyny kartezjańskie elementów z podanych iterowalnych obiektów.

```python
import itertools

produkty = itertools.product('AB', repeat=2)

for produkt in produkty:
    print(produkt)
```
5. itertools.permutations(iterable, r=None)
Funkcja permutations generuje wszystkie możliwe permutacje elementów z danego iterowalnego obiektu.

```python
import itertools

permutacje = itertools.permutations([1, 2, 3], 2)

for permutacja in permutacje:
    print(permutacja)
```
6. itertools.combinations(iterable, r)
Funkcja combinations generuje wszystkie możliwe kombinacje bez powtórzeń r elementów z danego iterowalnego obiektu.

```python
import itertools

kombinacje = itertools.combinations([1, 2, 3], 2)

for kombinacja in kombinacje:
    print(kombinacja)
```
7. itertools.groupby(iterable, key=None)
Funkcja groupby grupuje elementy z danego iterowalnego obiektu na podstawie klucza, który jest funkcją określającą klucz grupowania.

```python
import itertools

dane = [('a', 1), ('b', 2), ('a', 3), ('b', 4)]
grupy = itertools.groupby(dane, key=lambda x: x[0])

for klucz, grupa in grupy:
    print(klucz, list(grupa))
```

Te funkcje są tylko kilkoma z wielu dostępnych w module itertools. Pozwalają one na generowanie, łączenie, 
przekształcanie i analizowanie iteratorów w sposób efektywny i wydajny. Dzięki nim można wykonywać zaawansowane operacje
na danych w sposób bardziej zwięzły i elegancki.

### Pytanie 10
#### Jakie są różnice między funkcjami map(), filter(), a reduce()? Jakie są ich typowe zastosowania?
[Powrót do spisu treści](#spis-treści)

1. `map(function, iterable)`

Funkcja map() przyjmuje funkcję i iterowalny obiekt jako argumenty. Przechodzi przez każdy element 
iterowalny i stosuje funkcję do każdego z nich, zwracając iterator z wynikami.

Zastosowanie: Jest stosowana, gdy chcemy zastosować pewną operację do każdego elementu w kolekcji i uzyskać wyniki jako iterator.

```python
liczby = [1, 2, 3, 4, 5]
podwojone = map(lambda x: x * 2, liczby)
```

2. `filter(function, iterable)`

Różnica: Funkcja filter() również przyjmuje funkcję i iterowalny obiekt jako argumenty. Przechodzi przez każdy element iterowalny i zwraca tylko te elementy, dla których funkcja zwraca True.

Zastosowanie: Jest stosowana, gdy chcemy przefiltrować elementy w kolekcji na podstawie określonego warunku.

```python
liczby = [1, 2, 3, 4, 5]
parzyste = filter(lambda x: x % 2 == 0, liczby)
```
3. `reduce(function, iterable[, initializer])`

Różnica: Funkcja reduce() redukuje iterowalny obiekt do pojedynczej wartości, stosując funkcję do pary elementów sekwencji i akumulatora. Wynik tej operacji jest następnie używany jako nowy akumulator dla kolejnych elementów.

Zastosowanie: Jest stosowana, gdy chcemy zredukować kolekcję do pojedynczej wartości, łącząc wszystkie elementy za pomocą określonej operacji.

```python
from functools import reduce

liczby = [1, 2, 3, 4, 5]
suma = reduce(lambda x, y: x + y, liczby)
```
**Typowe zastosowania:**
1. **map()**: Jest używana, gdy chcemy zastosować pewną operację do każdego elementu w kolekcji i uzyskać wyniki 
jako iterator. Przykłady obejmują mnożenie elementów przez stałą wartość, konwersję typów danych itp.

2. **filter()**: Jest stosowana, gdy chcemy przefiltrować elementy w kolekcji na podstawie określonego warunku. 
Przykłady obejmują filtrowanie liczb parzystych, usuwanie pustych ciągów znaków itp.

3. **reduce()**: Jest stosowana, gdy chcemy zredukować kolekcję do pojedynczej wartości, łącząc wszystkie elementy za 
pomocą określonej operacji. Przykłady obejmują sumowanie wszystkich elementów, ł3. ączenie ciągów znaków, 
znajdowanie maksimum lub minimum itp.



### Pytanie 11
#### Czym jest i jak implementujesz memoizację w Pythonie?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 12
#### Opisz zastosowanie i działanie funkcji super() w Pythonie.
[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 13
#### Jakie są główne różnice między __init__ a __new__ w Pythonie?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 14
#### Jakie są różnice między deepcopy a shallowcopy? Jakie problemy mogą się pojawić przy używaniu każdego z nich?
[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 15
#### Jak działają sloty (__slots__) w Pythonie i jakie są ich zalety i wady?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 16
#### Jak działają moduły abc (Abstract Base Classes) i do czego są używane?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 17
#### Jakie są różnice między hash() a __hash__()? Jakie są zasady tworzenia hashable obiektów w Pythonie?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 18
#### Jak zaimplementować wielowątkowość w Pythonie przy użyciu modułu threading? Jakie są pułapki i jak je unikasz?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 19
#### Jakie są różnice między metodami __eq__() a __cmp__() w kontekście porównywania obiektów?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

### Pytanie 20
#### Jak zaimplementować własny kontekst menedżera (context manager) za pomocą klasy i dekoratora contextlib.contextmanager?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 21
#### Jakie są różnice między yield a return w funkcjach Pythona?
[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 22
#### Jakie są różnice między global a nonlocal? Jakie są ich zastosowania?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 23
#### Jak działa moduł inspect w Pythonie i jakie są jego zastosowania?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 24
#### Jakie są różnice między deepcopy a shallowcopy? Jakie problemy mogą się pojawić przy używaniu każdego z nich?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 25
#### Jak działają funkcje wyższego rzędu w Pythonie? Podaj przykłady ich zastosowania.

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 26
#### Jakie są różnice między standardowym modułem logging a innymi popularnymi bibliotekami do logowania?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 27
#### Jak działają mechanizmy serializacji w Pythonie (np. pickle, json)?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 28
#### Jakie są różnice między set a frozenset w Pythonie? Jakie są ich typowe zastosowania?

[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```


### Pytanie 29
#### Jakie są różnice między metodami __eq__ a __cmp__?



[Powrót do spisu treści](#spis-treści)

```python
# PRZYKŁAD

```

