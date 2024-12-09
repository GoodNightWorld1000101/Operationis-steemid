# Praktikum 12
See praktikum võttis mul umbes 4 tundi aega. Selles praktikumis õppisin .sh skriptimis syntaxit.

## ülesanne 3
```
#!/bin/sh
echo "Sisesta nimi:"
read nimi
echo "Sisesta eriala:"
read eriala
echo "Sisesta nr:"
read matriklinumber
echo "nimi: $nimi
eriala: $eriala
NR: $matriklinumber"
```


### ekraanipilt 3 
![image](https://github.com/user-attachments/assets/b98dd360-5a59-4dd5-a543-86e97baec57b)

## ülesanne 4
```
#!/bin/bash

#skripti eesmark:faili laiendi muutmine kaustas

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
### ekraanipilt 4
![image](https://github.com/user-attachments/assets/d77d7c7c-2b8c-4530-8955-6edc58685cdd)


## ülesanne 5
```
#!/bin/bash

# Protsessi nimi argumendist
protsess_nimi=$1

# IFS reavahetuseks (et saaks ridade kaupa läbi vaadata)
IFS=$'\n'

#otsi protsessi listist
for rida in $(ps -A); do
    # Lisa rea algusesse tühik, eemalda korduvad tühikud, ja lõika PID ja protsessi nimi välja
    pid=$(echo " $rida" | tr -s ' ' | cut -d ' ' -f2)
    nimi=$(echo " $rida" | tr -s ' ' | cut -d ' ' -f5)

    # Kontrolli, kas protsessi nimi vastab otsitavale
    if [[ "$nimi" == *"$protsess_nimi"* ]]; then
        echo "Protsess: $nimi, PID: $pid"
    fi
done
 ```
### ekraanipilt 5
![image](https://github.com/user-attachments/assets/82cc23af-f736-4f31-b02d-f20416ffbaf5)

## ülesanne 6
```
#!/bin/bash
#Astme funktsioon
aste () {
  #Argumendid
  i=1
  alus=$1
  vastus=1

  #Võrdleb i-d, mis on astme loendur soovitud astmega
  while [ $i -le $2 ];
  do
    #Korrutab eelneva vastuse alusega ja salvestab selle vastusesse ja astme loendurit suurendatakse 1 võrra
    vastus=$(( vastus * alus ))
    i=$(( i + 1 ))

  done
    echo $vastus
}

a=$(aste 5 9)

echo $a

```
### ekraanipilt 6
![image](https://github.com/user-attachments/assets/f4094da0-bfbe-4644-8c01-3d3243b958c7)

## ülesanne 7
```
#!/bin/bash

# Function to calculate x to the power of y
power() {
  local x=$1
  local y=$2
  local result=1
  local i=0

  while [ $i -lt $y ]; do
    result=$((result * x))
    i=$((i + 1))
  done

  echo $result
}

# Example usage
x=2
y=3
echo "$(power $x $y)"
```
### ekraanipilt 7
![image](https://github.com/user-attachments/assets/6c66d4c5-3e65-4226-bcc8-3f47f58daaf7)
![image](https://github.com/user-attachments/assets/ca7968d0-ce98-400b-9b2d-f5df7b048d1e)


