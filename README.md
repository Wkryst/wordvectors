# Polskie modele Word2Vec

Repozytorium zawiera narzedzia służace do wygenerowania polskich korpusów językowych oraz modeli reprezentacji werktorowej słów word2vec.
Do pracy wykorzystano następujące korpusy:
* polskie napisy do filmów OpenSubtitles
* polska Wikipedia
* polskie Wikibooks
* polskie Wictionary

Szczególnej uwadze polecam korpus OpenSubtitles gdyż jako jedyny zawiera prawie wyłącznie dialogi. Tego typu korpus może mieć zastosowanie np. przy budowie interfejsów słownych czy głosowych typu człowiek-maszyna. 

# Generowanie modeli
Proces generowania modeli składa się z dwóch kroków. Pierwszym jest przygotoeanie pliku z korpusem tekstowym na podstawie danych źródłowych. Drugi to uczenie modelu word2vec na podstawie przygotowanego uprzednio korpusu.

## Przygotowanie korpusu
Do utworzenia korpusów opartych o Wikipedię służy notatnik [Build Corpus.ipynb](Build%20Corpus.ipynb), dla korpusu OpenSubtitles jest to [Build OpenSubtitles Corpus.ipynb](Build%20OpenSubtitles%20Corpus.ipynb). W wyniu ich działania do katalogu `data` zostaną pobrane dane wejściowe w postaci archiwów a następnie zostaną one rozpakowane i wyekstraktowane z nich korpusy do plików z rozszerzeniem `.txt`.
Pliki te mają wiele gigabajtów dla tego niezbędna jest odpwiednia ilość miejsca na dysku. Dla korpusu OpenSubtitles jest to ok 20GB, dla korpusów Wikipedii ok. 15GB. Pliki wynikowe zawierają jedno zdanie w każdej linii. Szczegółowy opis działania znajduje się w notatniku.

## Tworzenie reprezentacji wektorowej
Do tworzenia reprezentacji wektorowej słów, czyli modelu word2vec służy notatnik [Make WordVectors.ipynb](Make%20WordVectors.ipynb).
Jego centralną częścią jest wywołanie funkcji `make_wordvectors()`. Parametry zostały dobrane tak aby wygenerować następujące modele:
1. OpenSubtitles - Słownik milion słów, algorytm skip-gram, wektory w przestzeni 300 wymiarowej, okno 5, negatywny sampling 5
1. Wikipedia - Słownik 50000 słów, algorytm skip-gram, wektory 300D, okno 5, neg. samppling 5
1. Wikibooks - Słownik 50000 słów, algorytm skip-gram, wektory 300D, okno 5, neg. samppling 5
1. Wiktionary - Słownik 50000 słów, algorytm skip-gram, wektory 300D, okno 5, neg. samppling 5

Modele wynikowe zapisane są w postaci plików o nazwach w formacie:

`w2v-773752559-1000000-300-5-5-OpenSubtitles2016.bin` - gdzie poszczególne elementy oznaczają:
* `w2v` - skrót word2vector
* `773752559` - ilość słów korpusie (w korpusie OpenSubtitles jako słowa traktowane są też niektóre znaki interpunkcyjne kończące zdanie, takie jak kropka, wykrzyknik, znak zapytania)
* `1000000` - ilość unikalnych słów w korpusie
* `300` - wymiarowość przestrzeni
* `5` - wielkość okna
* `5` - nwgatywny sampling
* `OpenSubtitles2016` - nazwa korpusu źródłowego

### Źródło
Oryginalnie projekt powstał ze sklonowania repoztorium: https://github.com/Kyubyong/wordvectors
Aktualnie zawiera jednak znaczą część zupełnie nowego kodu oraz optymalizacje powastałe na potrzeby obróbki polskich korpusów, w szczególnośći korpusu OpenSubtitles.
