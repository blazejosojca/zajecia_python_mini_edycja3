fundusze.py <- program z zajęć

Praca domowa:
Zadanie 1

Stworzyć skrypt, który dla danej daty pobierze wyniki losowania Lotto (dawny Duży Lotek).
Wyniki mają być zapisane do posortowanej listy liczb całkowitych i wyprintowane.
Data, dla której zostaną pobrane wyniki może być zapisana w skrypcie.

Przykład:
```
data            --->        lista wyników
wyniki losowania nr: 5715
2015-11-28      --->        [12, 14, 18, 25, 36, 45]
tego dnia nie było losowania
2015-11-27      --->        []
```

Do pobrania wyników zapewne będą potrzebne dwa zapytania:
1. GET - do otrzymania "ukrytej" wrtości formularza
2. POST - do wysłania zapytania o interesujące nas wyniki.

Materiały pomocnicze:
http://docs.python-requests.org/en/master/user/quickstart/
https://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigating-the-tree
http://www.lotto.pl/lotto/wyniki-i-wygrane
