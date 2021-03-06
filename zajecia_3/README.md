Kolejność programw wg wykładu:

* wyjatek_lapanie.py
* wyjatek_lapanie_as.py
* wyjatek_wlasny.py
* wyjatek_lapanie_Exception.py
* wyjatek_lapanie_reraise.py
* my_iter.py
* my_range.py
* infinite_fib.py
* read_file.py
* read_file_line_by_line.py
* read_file_with.py
* write_file.py
* writelines.py

Praca domowa:
# zadanie 1
Stworzyć własny wyjątek `SizeError` dziedziczący po ValueError.
W klasie Vector (praca domowa z II zajęć) próba porównania dodania dwóch
wektorów o różnym wymiarze powinna rzucać wyjątek SizeError z komunikatem

- dla porównania: `Cannot compare vectors with different sizes`
- dla dodawania: `Cannot add vectors with different sizes`

przykładowy kod porównania:
```
    v1 = Vector(1, 2)
    v2 = Vector(1, 2, 3)
    v1 == v2
```
Spodziewany efekt:
```
Traceback (most recent call last):
  File ".../kursy/MINI_3/wyklad_3/praca_domowa/zad_1.py", line 68, in <module>
    v1 == v2
  File ".../kursy/MINI_3/wyklad_3/praca_domowa/zad_1.py", line 16, in __eq__
    raise SizeError('Cannot compare vectors with different sizes')
SizeError: Cannot compare vectors with different sizes
```
Przykładowy kod dodawania:
```
v1 = Vector(1, 2)
v2 = Vector(1, 2, 3)
v1 + v2
```
Spodziewany efekt:
```
Traceback (most recent call last):
  File ".../kursy/MINI_3/wyklad_3/praca_domowa/zad_1.py", line 68, in <module>
    v1 + v2
  File ".../kursy/MINI_3/wyklad_3/praca_domowa/zad_1.py", line 21, in __add__
    raise SizeError('Cannot add vectors with different sizes')
SizeError: Cannot add vectors with different sizes
```

# Zadanie 2
Na wykładzie był prezentowany iterator naśladujący działanie range.
Iterator był popsuty (pomijał pierwszą liczbę).
Należy go naprawić, zmienić jego działanie i sposób wywołania tak aby spełniał
 następujące wywołania:

```
assert [x for x in MyIter(0, 10)] == list(range(0, 10))
assert [x for x in MyIter(4)] == list(range(4))
assert [x for x in MyIter(2, 30, 5)] == list(range(2, 30, 5))
assert [x for x in MyIter(-50, -1, 7)] == list(range(-50, -1, 7))
```
Bonus:
```
assert [x for x in MyIter(-1, -50, -7)] == list(range(-1, -50, -7))
```

Podanie step == 0 powino spowodować rzucenie wyjątku:
`ValueError: MyIter() arg 3 must not be zero`

range nie obsługuje keyword arguments, nasz iterator też nie powinien. Dokumentacja do range: https://docs.python.org/3/library/stdtypes.html#range

Kod z wykładu:
```
class MyIter():
    '''symuluje range'''
    def __init__(self, start=0, stop=0, step=1):
        print('__init__ called')
        self.start = start
        self.stop = stop
        self.step = step
        self.curr = self.start

    def __iter__(self):
        print('__iter__ called')
        self.curr = self.start
        return self

    def __next__(self):
        print('__next__ called')
        self.curr += self.step
        if self.curr < self.stop:
            return self.curr
        else:
            raise StopIteration
```

# zadanie 3
Napisać generator sekwencji Collatza `collatz_gen`.
Dla danej liczby startowej x
zwróci x
przy następnym wywołaniu (`next()`)
```
jeśli x == 1:
    zakończy działanie
jeśli x jest parzyste:
    nowy_x = x/2
    zwróci nowy_x
jeśli x jest nieparzyste:
    nowy_x = 3 * x + 1
    zwróci nowy_x
```
kolejne wywołania będą podstawiały nowy_x w miejsce x tak długo, aż zostanie zwrócone 1 i generator zakończy działanie.

Spodziewany efekt:
```
assert list(collatz_gen(1)) == [1]
assert list(collatz_gen(2)) == [2, 1]
assert list(collatz_gen(3)) == [3, 10, 5, 16, 8, 4, 2, 1]
assert list(collatz_gen(12)) == [12, 6, 3, 10, 5, 16, 8, 4, 2, 1]
assert list(collatz_gen(19)) == [19, 58, 29, 88, 44, 22, 11, 34, 17, 52, 26, 13, 40, 20, 10, 5, 16, 8, 4, 2, 1]
```

artykuł z wikipedii:
https://pl.wikipedia.org/wiki/Problem_Collatza

# zadanie 4
url: https://dumps.wikimedia.org/other/static_html_dumps/current/pl/html.lst
napisać funkcję `get_words(in_file_name, out_file_name)`

Funkcja ma zapisać do pliku out_file_name wszystkie unikalne słowa występujące w
nazwach artykułów z wikipedii w pliku in_file_name. 
Słowa w out_file_name mają być posortowane w kolejności alfabetycznej. 
Jedno słowo na jedną linię w out_file_name.
Za słowo uznajemy maksymalny ciąg znaków dla, którego funkcja isalpha() zwraca True.
Ciągi które bierzemy pod uwagę występują między ostatnim / a pierwszą . (kropką)
przykład: 
w tej linii:
`pl/articles/k/a/r/Grafika~Karl_Fourth_Bohemia_Anna_Schweidnitz.jpeg_b996.html`
występują słowa:
'Anna', 'Bohemia', 'Fourth', 'Grafika', 'Karl', 'Schweidnitz'

czyli w pliku wynikowym powinny pojawić się w kolejności:
```
Anna
Bohemia
Fourth
Grafika
Karl
Schweidnitz
```

Rozwiązaniem zadania jest kod przetwarzający in_file_name na out_file_name.
Proszę nie przysyłać plików out_file_name.
Dodatkowo liczba słów jest duża.
Zalecam na potrzeby testów działać na fragmencie pliku html.lst
