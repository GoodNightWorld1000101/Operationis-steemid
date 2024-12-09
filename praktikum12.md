## ülesanne 3
```#!/bin/sh echo "Sisesta nimi:" read nimi echo "Sisesta eriala:" read eriala echo "Sisesta nr:" read matriklinumberecho "nimi: $nimi eriala: $eriala NR: $matriklinumber" ```


## output 3 
![image](https://github.com/user-attachments/assets/b98dd360-5a59-4dd5-a543-86e97baec57b)

## ülesanne 4
```#!/bin/bash

"faili laiendi muutmine kaustas"
#!/bin/bash

# Kontrollime, et kasutaja sisestas kaks argumenti
if [ $# -ne 2 ]; then
    echo "Kasutamine: $0 <algne_laiend> <uus_laiend>"
    exit 1
fi

# Argumendid
algne_laiend=$1
uus_laiend=$2

# Käime kaustas olevad failid läbi
for fail in *.$algne_laiend; do
    # Kontrollime, kas fail eksisteerib
    if [ -f "$fail" ]; then
        # Uue faili nimi
        uus_fail=${fail%.$algne_laiend}.$uus_laiend
        # Nimetame faili ümber
        mv "$fail" "$uus_fail"
        echo "Nimetasin ümber: $fail -> $uus_fail"
    fi
done
 ```
## output 4
![image](https://github.com/user-attachments/assets/496bc843-a1f9-4e24-a4e3-b0ecaa45c35a)
