# TP3-Traitement-du-signal

# Rapport TP3: - La corrélation croisée Mesure de similarité entre deux signaux

## réalisé par Wafae Hamdaoui et Oumayma EL Bakkali

## Objectifs du TP:

• Comprendre la notion de la corrélation croisée et évaluer sa capacité dans la 
mesure de dépendance deux signaux.

• Evaluer l’efficacité de cette mesure en présence du bruit.

## Mesure de similarité entre deux signaux:

En traitement du signal, la corrélation croisée (aussi appelée covariance croisée) est 
la mesure de la similitude entre deux signaux. Afin de mieux appréhender cette notion, 
on procédera à l’estimation de la corrélation croisée entre un signal sonore 
échantillonné et un fragment de ce signal, en utilisant les outils appropriés fournis par 
MATLAB. Le signal sonore qui fera l’objet de cet exercice est celui d’un anneau 
tournant sur une table. 

Q1: On Charge dans l’espace de travail l’enregistrement correspondant en tapant la commande load('Ring.mat').
```Matlab

clear all
 close all
 clc
load('Ring.mat');

```
Q2: le signal en fonction du temps:
```Matlab

Fs=44100;
Ts =1/Fs;
t =0:Ts:(length(y)-1)*Ts ;
 plot(t,y);
 
```
> Si on veut  écoutez-le on peux utiliser la commande `sound(y,Fs)` .

Q3:  En utilisant deux droites en pointillés rouges, repérons le morceau du signal entre 
t=7s et t=8s (Commande : xline).

```Matlab
 xline(7,'--r');
 xline(8,'--r');
```
output:

![image](https://user-images.githubusercontent.com/75392302/152984418-a6114ecf-32a9-481e-8399-15df1065aed2.png)

Q4: On récupére ce morceau dans une variable nommée « Fragment », , puis on le trace en fonction du temps:

```Matlab
 fragment=y(7*Fs:8*Fs);
 figure(2)
 plot(fragment)
```
output:

![image](https://user-images.githubusercontent.com/75392302/152985187-f4fd981a-1451-4e74-a868-28b1515b5b86.png)

> Si on veut  écoutez-le on peux utiliser la commande `sound(fragment,Fs)` .

Q5: Calculons et tracons la corrélation croisée du signal complet et du fragment:

```Matlab
  correlation=xcorr(y,fragment);
  figure(3)
  plot(correlation);
```
output:

![image](https://user-images.githubusercontent.com/75392302/152985683-811931c8-0c8a-43a6-aade-ce8eb118898f.png)

> là ou il ya une correspondance entre le signal y et  fragment il se produit un pic et Le plus grand pic se produit à la valeur de décalage lorsque les éléments de y et fragment correspondent exactement.

Q6: Déduisons la valeur du décalage pour lequel la corrélation entre les deux signaux est 
maximal et utilisons ce décalage pour faire apparaitre le fragment dans le signal. 

```Matlab
[m,d]=max(correlation);      
 del=d-max(length(y),length(fragment));  
 plot(y)                                    
 hold on,plot([del+1:length(fragment)+del],fragment,'r');  
```

output:

![image](https://user-images.githubusercontent.com/75392302/152986815-e7d270bf-dbd2-4a6a-a360-d624f5542f92.png)

## Part 2:Mesure de similarité entre deux signaux en présence du bruit

Dans cette partie, nous chercherons à évaluer le degré de dépendance de deux 
signaux en présence du bruit, en utilisant toujours cette notion de corrélation croisée.

Q1: Ajoutons un bruit blanc gaussien au signal de départ et aussi au fragment, puis 
traçons-les en fonction du temps. 

```Matlab
 ynoise = awgn(y,30)+y;
 fnoise=awgn(fragment,30)+fragment;
 %le signal
 plot(t,[y ynoise]);
 xline(7,'--r');
 xline(8,'--r')
 %fragment
 plot(fnoise);
```
output:

![image](https://user-images.githubusercontent.com/75392302/152987719-4741fd1e-0638-4c42-a827-9f5d6edc1beb.png)![image](https://user-images.githubusercontent.com/75392302/152987784-f02d9f08-f730-4c5d-b2c1-2ec4670175b7.png)

Q2 Q3: Appliquons la fonction xcorr afin de calculer la corrélation croisée entre les deux 
signaux bruités, puis évaluons la capacité de cette mesure de détecter le fragment dans 
le signal en présence du bruit. Retracons la partie du signal détecté.

```Matlab
  correlation1=xcorr(ynoise,fnoise);
  plot(correlation1);
  %Le plus grand pic se produit à la valeur de décalage lorsque les éléments de x et y correspondent exactement

  [m,d]=max(correlation1);      
  del1=d-max(length(ynoise),length(fnoise));  
  plot(ynoise);
  hold on,plot([del1+1:length(fnoise)+del1],fnoise,'r');
```
output:

![image](https://user-images.githubusercontent.com/75392302/152988524-3a08519d-13a7-4d14-8ed3-67eeb4f1b3f4.png)
![image](https://user-images.githubusercontent.com/75392302/152988572-234dfdfa-7bb0-4147-aba3-02e62d47ad71.png)
















