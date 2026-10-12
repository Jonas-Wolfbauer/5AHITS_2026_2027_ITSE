# Ü2 Wiederholung PHP

| Kategorie | Wert |
| ---- | ---- |
| Klasse | 5AHITS |
| Verfasser | Xu Matthias Chen, Jonas Franz Wolfbauer |
| Datum | 12.10.2026 |
| Fach | ITSE (Übungen) |
| Link | [https://www.franzmatejka.at/htl/doc/ITSI/lab/ransom_ryuk/01_ryuk.html](https://www.franzmatejka.at/htl/doc/ITSI_5/itsi5-lab/02_php.html) |

# KI Verwendung
Im Laufe dieses Berichts wurde KI vereinzelt verwendet.  
Verwendetete Tools:

- Google Suche (AI Overview)

Es wurde **kein** Code mit generativer KI verwendet.

## Beispielhafter Anwedungsfall
Google Suche:
```
> input decimal values html 

Um Dezimalzahlen (Kommazahlen) in einem HTML-Eingabefeld zu erlauben, müssen Sie das step-Attribut des <input type="number">-Elements verwenden.
Standardmäßig akzeptiert das HTML5-Zahlenfeld nur ganze Zahlen (step="1").
...
```

# Übungen

## Übung  2.1 (PHP)
PHP ist in der Lage Quelltext zur Laufzeit zu generieren.


**PHP Blöcke und Kommentare**
PHP Kann nur in PHP Blöcken ausgeführt werden, welche willkürlich zwischen HTML Code platziert werden können.
```PHP
<?php
// This is a single line comment.
/*
  This
  is
  a
  multiline
  comment.
*/
?>
```

| Befehl / Keyword / Funktionen   | Beschreibung |
| ------------------  | ------------ |
| ``echo``            | Gibt Output in Dokument aus (z.B. kann HTML Code so generiert werden). Kann mehrere Argumente übernehmen. |
| ``print``           | Gibt Output in Dokument aus - ähnlich zu ``echo``, nimmt jedoch nur einen Parameter und returned 1. ||
| ``$variableName``       | Variablen werden immer mit ``$`` deklariert. Variablentypen müssen **nicht** spezifiziert werden. |
| ``if`` / ``else`` / ``elseif`` | Werden bei bool'schen Bedingungen aufgerufen. |
| Schleife | Es gibt ``for``, ``while`` oder auch ``foreach`` Schleifen. |
| ``var_dump()`` | Nimmt beliebige Objekte als Übergabeparameter und liefert dessen Typ zurück. |
| ``function()`` | Funktionen werden mit dem ``function`` Keyword deklariert. |
| ``(<Datatype>)`` | Typecasts sind möglich und werden vor dem Wert bzw. der Variable geschrieben. |
| Stringfunktionen | ``strlen()`` (Stringlänge), ``str_word_count()`` (Anzahl der Wörter in einem String) , ... |
| Mathematische Funktionen | ``pi()`` (liefert Pi), ``min()``/``max()`` (liefert größten/kleinsten Wert), ... |

**Quellen**
- (w3schools PHP)[https://www.w3schools.com/php/]

## Übung 2.2 (PHP Aufgaben)

### Notenverwaltung

**Quellen**
- [Generating a random password in php](https://stackoverflow.com/questions/6101956/generating-a-random-password-in-php)

### Passwort-Generator

**Quellen**

### Zahlenratespiel

**Quellen**
