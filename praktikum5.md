# Praktikum 5 failioigused

## punkt 5-1 
### a) Kaustal peab olema käivitamisõigus ja failil peab olema lugemisõigus.
### b) Kaustale on vaja kirjutamis ja käivitamisõigusi, failile ei ole vaja mitte mingeid õigusi.

## punkt 5-2
### chmod a=x skriptifail ei ole piisav õigus shelli skriptifaili käivitamiseks, sest shellil on vaja ka skriptifaili sisu lugeda, et seda tõlgendada.

## punkt 5-3
### Igal kasutajal on omanimeline grupp, sest siis saab kasutaja luua faile ja kaustu grupi õigustega muretsemata, et teistele kasutajatele antakse automaatselt juurdepääs. Sama on ka faile ja kaustu lihtsam jagada lisades teised kasutaja gruppi selle asemel, et iga faili ja kasuta õigusi muutma hakkata. 

## punkt 5-4
###  minimaalsed õigused, mis on vajalikud tavakasutajal faili uusfail.txt sisu lugemiseks on grupile käivitamis õigus kaustale majasiseseks-kasutamiseks ja grupile faili lugemisõigus.
![image](https://github.com/user-attachments/assets/1a8e8a8c-9b20-4af3-91f2-6cdf7da47f09)

## punkt 5-5
### Setuid õigust on vaja, et programm saaks töötada opetaja õigustega kui jukuisa käivitab selle.
### ![image](https://github.com/user-attachments/assets/3475233d-8076-45c4-962e-4a198821484e)

## punkt 5-6
### Jah kui programm sisaldab turvaauke võib ründaja saada ligipääsu tundlikele failidele või süsteemi konfiguratsioonidele.

## punkt 5-7 
### Kasutajad, kes saavad peetri loodud faile yhiskaustast kustudad on peeter,opetaja ja root.

## punkt 5-8
### # file: hinded.txt
### # owner: opetaja
### # group: opetaja
### user::rw-
### group::---
### group:direktor:rw-
### mask::rw-
### other::---

## punkt 5-9
### Mitte keegi isegi mitte root kasutaja ei saa faili sisu modifitseerida kuni seal on immutability parameeter aktiivne.
### Faili kustutamiseks peab jooksutama käsku "sudo chattr -i testfail-2" ja siis "rm testfail-2".
