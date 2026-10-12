# Ü2 Wiederholung PHP

| Kategorie | Wert |
| ---- | ---- |
| Klasse | 5AHITS |
| Verfasser | Xu Matthias Chen, Jonas Franz Wolfbauer |
| Datum | 12.10.2026 |
| Fach | ITSE (Übungen) |
| Link | [https://www.franzmatejka.at/htl/doc/ITSI/lab/ransom_ryuk/01_ryuk.html](https://www.franzmatejka.at/htl/doc/ITSI_5/itsi5-lab/02_php.html) |

>**AUFGABENSTELLUNG**
>HINZUFÜGEN!!!

# KI Verwendung
Im Laufe dieses Berichts wurde KI vereinzelt verwendet.  
Verwendetete Tools:

- Google Suche (AI Overview)
- Claude Fehlersuche vom PHP Code
- 
Es wurde **kein** Code mit generativer KI verwendet.

## Beispielhafter Anwedungsfall
Google Suche:
```
> input decimal values html 

Um Dezimalzahlen (Kommazahlen) in einem HTML-Eingabefeld zu erlauben, müssen Sie das step-Attribut des <input type="number">-Elements verwenden.
Standardmäßig akzeptiert das HTML5-Zahlenfeld nur ganze Zahlen (step="1").
...
```
Claude:
```
> input das ganze index.php
Suche mir die Fehler in diesem PHP Programm und sag mir was ich verbessern sollte.
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
- (Pixelpilot PHP Formulare)[https://pixelpilot.github.io/webdev/php_mysql/20_formulare.html]

### Passwort-Generator

**Quellen**
- [Generating a random password in php](https://stackoverflow.com/questions/6101956/generating-a-random-password-in-php)

#### Version 1
```
<h1>Passwortgenerator</h1>

<?php

// Source - https://stackoverflow.com/q/6101956
// Posted by nunos, modified by community. See post 'Timeline' for change history
// Retrieved 2026-10-12, License - CC BY-SA 3.0

function randomPassword($laenge) 
{
    $alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_-=+;:,.?";
    for ($i = 0; $i < $laenge; $i++) 
    {
        $n = rand(0, strlen($alphabet)-1);
        $pass[$i] = $alphabet[$n];
    }
    // implode() joins array elements with a string -> macht aus einem Array einen String
    return implode("", $pass); 
}

$anzahl = 0;
$passwort = "";
if (isset($_GET["laenge"]))
{
    $anzahl = $_GET["laenge"];
    $passwort = randomPassword($anzahl);
}
?>



<form action="<?php echo $_SERVER["PHP_SELF"]?>" method="get">
    <input type="number" name="laenge" placeholder="Länge" value ="<?php echo $laenge?>">
    <input type="submit"value="Sei freundlich zu mir!">
</form>

<?php

echo "<h2>Dein Passwort: </h2>";
if (isset($_GET["laenge"]))
{
    echo "$passwort";
}
?>
```
#### Version 2
```
<h1>Passwortgenerator</h1>

<?php

// Source - https://stackoverflow.com/q/6101956
// Posted by nunos, modified by community. See post 'Timeline' for change history
// Retrieved 2026-10-12, License - CC BY-SA 3.0

function randomPassword($laenge) 
{
    $alphabet = "abcdefghijklmnopqrstuvwxyz";

    // schaut ob die Checkbox angehackt ist unf fügt die Option hinzu
    if (isset($_GET["Großbuchstaben"]) && $_GET["Großbuchstaben"] == 1)
    {
        $alphabet .= "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    }
    if (isset($_GET["zahl"]) && $_GET["zahl"] == 1)
    {
        $alphabet .= "0123456789";
    }
    if (isset($_GET["sonderzeichen"]) && $_GET["sonderzeichen"] == 1)
    {
        $alphabet .= "!@#$%^&*()_-=+;:,.?";
    }
    
    for ($i = 0; $i < $laenge; $i++) 
    {
        $n = rand(0, strlen($alphabet)-1);
        $pass[$i] = $alphabet[$n];
    }
    // implode() joins array elements with a string -> macht aus einem Array einen String
    return implode("", $pass); 
}

$anzahl = 0;
$passwort = "";
if (isset($_GET["laenge"]))
{
    $anzahl = $_GET["laenge"];
    $passwort = randomPassword($anzahl);
}
?>



<form action="<?php echo $_SERVER["PHP_SELF"]?>" method="get">
    <input type="number" name="laenge" placeholder="Länge" value ="<?php echo $laenge?>"> <br>
    <input type="checkbox" name="Großbuchstaben" value="1"> Großbuchstaben <input type="checkbox" name="zahl" value="1"> Zahlen <input type="checkbox" name="sonderzeichen" value="1"> Sonderzeichen<br>
    <input type="submit"value="Sei freundlich zu mir!">
</form>

<?php

echo "<h2>Dein Passwort: </h2>";
if (isset($_GET["laenge"]))
{
    echo "$passwort";
}

?>
```


### Zahlenratespiel

**Quellen**
