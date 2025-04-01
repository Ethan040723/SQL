
## TP10
### BASE DE DONNÉE
```sql

DROP DATABASE IF EXISTS location_ski;
CREATE DATABASE location_ski CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE location_ski;


DROP TABLE IF EXISTS clients;
DROP TABLE IF EXISTS fiches;
DROP TABLE IF EXISTS tarifs;
DROP TABLE IF EXISTS gammes;
DROP TABLE IF EXISTS categories;
DROP TABLE IF EXISTS grilleTarifs;
DROP TABLE IF EXISTS artilces;
DROP TABLE IF EXISTS lignesFic;

CREATE TABLE clients (
    noCli INT PRIMARY KEY,
    nom VARCHAR(100),
    prenom VARCHAR(100),
    adresse VARCHAR(255),
    cpo VARCHAR(10),
    ville VARCHAR(100)
);

CREATE TABLE fiches (
    noFic INT PRIMARY KEY,
    noCli INT,
    dateCrea DATETIME,
    datePaiement DATETIME,
    etat VARCHAR(2),
    FOREIGN KEY (noCli) REFERENCES clients(noCli)
);

CREATE TABLE tarifs (
    codeTarif VARCHAR(3) PRIMARY KEY,
    libelle VARCHAR(50),
    prixJour DECIMAL(10, 2)
);

CREATE TABLE gammes (
    codeGam VARCHAR(2) PRIMARY KEY,
    libelle VARCHAR(50)
);

CREATE TABLE categories (
    codeCate VARCHAR(4) PRIMARY KEY,
    libelle VARCHAR(50)
);

CREATE TABLE grilleTarifs (
    codeGam VARCHAR(2),
    codeCate VARCHAR(4),
    codeTarif VARCHAR(3),
    PRIMARY KEY (codeGam, codeCate),
    FOREIGN KEY (codeGam) REFERENCES gammes(codeGam),
    FOREIGN KEY (codeCate) REFERENCES categories(codeCate),
    FOREIGN KEY (codeTarif) REFERENCES tarifs(codeTarif)
);

CREATE TABLE articles (
    refart VARCHAR(4) PRIMARY KEY,
    designation VARCHAR(255),
    codeGam VARCHAR(2),
    codeCate VARCHAR(4),
    FOREIGN KEY (codeGam) REFERENCES gammes(codeGam),
    FOREIGN KEY (codeCate) REFERENCES categories(codeCate)
);

CREATE TABLE lignesFic (
    noFic INT,
    noLig INT,
    refart VARCHAR(4),
    depart DATETIME,
    retour DATETIME,
    PRIMARY KEY (noFic, noLig),
    FOREIGN KEY (noFic) REFERENCES fiches(noFic),
    FOREIGN KEY (refart) REFERENCES articles(refart)
);



INSERT INTO clients (noCli, nom, prenom, adresse, cpo, ville) VALUES 
    (1, 'Albert', 'Anatole', 'Rue des accacias', '61000', 'Amiens'),
    (2, 'Bernard', 'Barnabé', 'Rue du bar', '1000', 'Bourg en Bresse'),
    (3, 'Dupond', 'Camille', 'Rue Crébillon', '44000', 'Nantes'),
    (4, 'Desmoulin', 'Daniel', 'Rue descendante', '21000', 'Dijon'),
     (5, 'Ernest', 'Etienne', 'Rue de l’échaffaud', '42000', 'Saint Étienne'),
    (6, 'Ferdinand', 'François', 'Rue de la convention', '44100', 'Nantes'),
    (9, 'Dupond', 'Jean', 'Rue des mimosas', '75018', 'Paris'),
    (14, 'Boutaud', 'Sabine', 'Rue des platanes', '75002', 'Paris');

INSERT INTO fiches (noFic, noCli, dateCrea, datePaiement, etat) VALUES 
    (1001, 14,  DATE_SUB(NOW(),INTERVAL  15 DAY), DATE_SUB(NOW(),INTERVAL  13 DAY),'SO' ),
    (1002, 4,  DATE_SUB(NOW(),INTERVAL  13 DAY), NULL, 'EC'),
    (1003, 1,  DATE_SUB(NOW(),INTERVAL  12 DAY), DATE_SUB(NOW(),INTERVAL  10 DAY),'SO'),
    (1004, 6,  DATE_SUB(NOW(),INTERVAL  11 DAY), NULL, 'EC'),
    (1005, 3,  DATE_SUB(NOW(),INTERVAL  10 DAY), NULL, 'EC'),
    (1006, 9,  DATE_SUB(NOW(),INTERVAL  10 DAY),NULL ,'RE'),
    (1007, 1,  DATE_SUB(NOW(),INTERVAL  3 DAY), NULL, 'EC'),
    (1008, 2,  DATE_SUB(NOW(),INTERVAL  0 DAY), NULL, 'EC');

INSERT INTO tarifs (codeTarif, libelle, prixJour) VALUES
    ('T1', 'Base', 10),
    ('T2', 'Chocolat', 15),
    ('T3', 'Bronze', 20),
    ('T4', 'Argent', 30),
    ('T5', 'Or', 50),
    ('T6', 'Platine', 90);

INSERT INTO gammes (codeGam, libelle) VALUES
    ('PR', 'Matériel Professionnel'),
    ('HG', 'Haut de gamme'),
    ('MG', 'Moyenne gamme'),
    ('EG', 'Entrée de gamme');

INSERT INTO categories (codeCate, libelle) VALUES
    ('MONO', 'Monoski'),
    ('SURF', 'Surf'),
    ('PA', 'Patinette'),
    ('FOA', 'Ski de fond alternatif'),
    ('FOP', 'Ski de fond patineur'),
    ('SA', 'Ski alpin');

INSERT INTO grilleTarifs (codeGam, codeCate, codeTarif) VALUES
    ('EG', 'MONO', 'T1'),
    ('MG', 'MONO', 'T2'),
    ('EG', 'SURF', 'T1'),
    ('MG', 'SURF', 'T2'),
    ('HG', 'SURF', 'T3'),
    ('PR', 'SURF', 'T5'),
    ('EG', 'PA', 'T1'),
    ('MG', 'PA', 'T2'),
    ('EG', 'FOA', 'T1'),
    ('MG', 'FOA', 'T2'),
    ('HG', 'FOA', 'T4'),
    ('PR', 'FOA', 'T6'),
    ('EG', 'FOP', 'T2'),
    ('MG', 'FOP', 'T3'),
    ('HG', 'FOP', 'T4'),
    ('PR', 'FOP', 'T6'),
    ('EG', 'SA', 'T1'),
    ('MG', 'SA', 'T2'),
    ('HG', 'SA', 'T4'),
    ('PR', 'SA', 'T6');

INSERT INTO articles (refart, designation, codeGam, codeCate) VALUES 
    ('F01', 'Fischer Cruiser', 'EG', 'FOA'),
    ('F02', 'Fischer Cruiser', 'EG', 'FOA'),
    ('F03', 'Fischer Cruiser', 'EG', 'FOA'),
    ('F04', 'Fischer Cruiser', 'EG', 'FOA'),
    ('F05', 'Fischer Cruiser', 'EG', 'FOA'),
    ('F10', 'Fischer Sporty Crown', 'MG', 'FOA'),
    ('F20', 'Fischer RCS Classic GOLD', 'PR', 'FOA'),
    ('F21', 'Fischer RCS Classic GOLD', 'PR', 'FOA'),
    ('F22', 'Fischer RCS Classic GOLD', 'PR', 'FOA'),
    ('F23', 'Fischer RCS Classic GOLD', 'PR', 'FOA'),
    ('F50', 'Fischer SOSSkating VASA', 'HG', 'FOP'),
    ('F60', 'Fischer RCS CARBOLITE Skating', 'PR', 'FOP'),
    ('F61', 'Fischer RCS CARBOLITE Skating', 'PR', 'FOP'),
    ('F62', 'Fischer RCS CARBOLITE Skating', 'PR', 'FOP'),
    ('F63', 'Fischer RCS CARBOLITE Skating', 'PR', 'FOP'),
    ('F64', 'Fischer RCS CARBOLITE Skating', 'PR', 'FOP'),
    ('P01', 'Décathlon Allegre junior 150', 'EG', 'PA'),
    ('P10', 'Fischer mini ski patinette', 'MG', 'PA'),
    ('P11', 'Fischer mini ski patinette', 'MG', 'PA'),
    ('S01', 'Décathlon Apparition', 'EG', 'SURF'),
    ('S02', 'Décathlon Apparition', 'EG', 'SURF'),
    ('S03', 'Décathlon Apparition', 'EG', 'SURF'),
    ('A01', 'Salomon 24X+Z12', 'EG', 'SA'),
    ('A02', 'Salomon 24X+Z12', 'EG', 'SA'),
    ('A03', 'Salomon 24X+Z12', 'EG', 'SA'),
    ('A04', 'Salomon 24X+Z12', 'EG', 'SA'),
    ('A05', 'Salomon 24X+Z12', 'EG', 'SA'),
    ('A10', 'Salomon Pro Link Equipe 4S', 'PR', 'SA'),
    ('A11', 'Salomon Pro Link Equipe 4S', 'PR', 'SA'),
    ('A21', 'Salomon 3V RACE JR+L10', 'PR', 'SA');

INSERT INTO lignesFic (noFic, noLig,  refart, depart, retour) VALUES 
    (1001, 1, 'F05', DATE_SUB(NOW(),INTERVAL  15 DAY), DATE_SUB(NOW(),INTERVAL  13 DAY)),
    (1001, 2, 'F50', DATE_SUB(NOW(),INTERVAL  15 DAY), DATE_SUB(NOW(),INTERVAL  14 DAY)),
    (1001, 3, 'F60', DATE_SUB(NOW(),INTERVAL  13 DAY), DATE_SUB(NOW(),INTERVAL  13 DAY)),
    (1002, 1, 'A03', DATE_SUB(NOW(),INTERVAL  13 DAY), DATE_SUB(NOW(),INTERVAL  9 DAY)),
    (1002, 2, 'A04', DATE_SUB(NOW(),INTERVAL  12 DAY), DATE_SUB(NOW(),INTERVAL  7 DAY)),
    (1002, 3, 'S03', DATE_SUB(NOW(),INTERVAL  8 DAY), NULL),
    (1003, 1, 'F50', DATE_SUB(NOW(),INTERVAL  12 DAY), DATE_SUB(NOW(),INTERVAL  10 DAY)),
    (1003, 2, 'F05', DATE_SUB(NOW(),INTERVAL  12 DAY), DATE_SUB(NOW(),INTERVAL  10 DAY)),
    (1004, 1, 'P01', DATE_SUB(NOW(),INTERVAL  6 DAY), NULL),
    (1005, 1, 'F05', DATE_SUB(NOW(),INTERVAL  9 DAY), DATE_SUB(NOW(),INTERVAL  5 DAY)),
    (1005, 2, 'F10', DATE_SUB(NOW(),INTERVAL  4 DAY), NULL),
    (1006, 1, 'S01', DATE_SUB(NOW(),INTERVAL  10 DAY), DATE_SUB(NOW(),INTERVAL  9 DAY)),
    (1006, 2, 'S02', DATE_SUB(NOW(),INTERVAL  10 DAY), DATE_SUB(NOW(),INTERVAL  9 DAY)),
    (1006, 3, 'S03', DATE_SUB(NOW(),INTERVAL  10 DAY), DATE_SUB(NOW(),INTERVAL  9 DAY)),
    (1007, 1, 'F50', DATE_SUB(NOW(),INTERVAL  3 DAY), DATE_SUB(NOW(),INTERVAL  2 DAY)),
    (1007, 3, 'F60', DATE_SUB(NOW(),INTERVAL  1 DAY), NULL),
    (1007, 2, 'F05', DATE_SUB(NOW(),INTERVAL  3 DAY), NULL),
    (1007, 4, 'S02', DATE_SUB(NOW(),INTERVAL  0 DAY), NULL),
    (1008, 1, 'S01', DATE_SUB(NOW(),INTERVAL  0 DAY), NULL);

```

### 1) Liste des clients (toutes les informations) dont le nom commence par un D ?
```sql
Select * FROM clients WHERE nom LIKE "D%" ;
```
|noCli|nom|prenom|adresse|cpo|ville|
|---|---|---|---|---|---|
|3|Dupond|Camille|Rue Crébillon|44000|Nantes|
|4|Desmoulin|Daniel|Rue descendante|21000|Dijon|
|9|Dupond|Jean|Rue des mimosas|75018 |Paris| 


### 2) Nom et prénom de tous les clients ?
```sql
Select nom,prenom FROM clients ;
```
|prenom|nom|
|---|---|
|Albert|Anatole|
|Bernard|Barnab|
|Dupond|Camille|
|Desmoulin|Daniel|
|Ferdinand|François|
|Albert|Anatole|
|Dupond|Jean|
|Boutaud|Sabine|

### 3) Liste des fiches (n°, état) pour les clients (nom, prénom) qui habitent en Loire Atlantique (44) ?
```sql
SELECT fiches.noFic,fiches.etat,clients.nom,clients.prenom FROM clients
INNER JOIN fiches ON fiches.noCLI=clients.noCLI
WHERE cpo like "44%"
```
|noFic|etat|nom|prenom|
|---|---|---|---|
|1004|EC|Ferdinand|François|
|1005|EC|Dupond|Camille|

### 4) Détail de la fiche n°1002 ?

```sql
SELECT fiches.noFic,clients.nom,clients.prenom,lignesFic.refart,articles.designation,lignesFic.depart,lignesFic.retour,tarifs.prixjour,DATEDIFF(IFNULL(lignesFic.retour, NOW()), lignesFic.depart) * tarifs.prixJour+tarifs.prixJour 
FROM fiches
JOIN clients ON clients.noCLI=fiches.noCLI
JOIN lignesFic ON lignesFic.noFic=fiches.noFic
JOIN articles ON articles.refart=lignesFic.refart
JOIN gammes ON gammes.codeGam=articles.codeGam
JOIN grilleTarifs ON grilleTarifs.codeGam=gammes.codeGam
JOIN tarifs ON tarifs.codeTarif=grilleTarifs.codeTarif
WHERE fiches.noFic=1002 
GROUP BY lignesFic.refart

```
|noFic|nom|prenom|refart|designation|depart|retour|prixJour|montant|
|---|---|---|---|---|---|---|---|---|
|1002|Desmoulin|Daniel|A03|Salomon 24X+Z12|2024-11-18|2024-11-22|10|50|
|1002|Desmoulin|Daniel|A04|Salomon 24X+Z12|2024-11-19|2024-11-24|10|60|
|1002|Desmoulin|Daniel|S03|Décathlon Apparition|2024-11-23|NULL|10|90|

### 5)  Prix journalier moyen de location par gamme ?
```sql
SELECT gammes.libelle,AVG(tarifs.prixJour)
FROM fiches
JOIN clients ON clients.noCLI=fiches.noCLI
JOIN lignesFic ON lignesFic.noFic=fiches.noFic
JOIN articles ON articles.refart=lignesFic.refart
JOIN gammes ON gammes.codeGam=articles.codeGam
JOIN grilleTarifs ON grilleTarifs.codeGam=gammes.codeGam
JOIN tarifs ON tarifs.codeTarif=grilleTarifs.codeTarif 
GROUP BY gammes.libelle
```
|Gamme|tarif journalier moyen|
|---|---|
|Entrée de gamme|10.833333|
|Haut de gamme|27.500000|
|Moyenne gamme|15.833333|
|Matériel Professionnel|80.000000|

### 6) Détail de la fiche n°1002 avec le total ?

```sql

SELECT fiches.noFic,clients.nom,clients.prenom,lignesFic.refart,articles.designation,lignesFic.depart,lignesFic.retour,tarifs.prixjour,DATEDIFF(IFNULL(lignesFic.retour, NOW()), lignesFic.depart) * tarifs.prixJour+tarifs.prixJour,SUM(DATEDIFF(IFNULL(lignesFic.retour, NOW()), lignesFic.depart) * tarifs.prixJour+tarifs.prixJour) OVER (PARTITION BY fiches.noFic)
FROM fiches
JOIN clients ON clients.noCLI=fiches.noCLI
JOIN lignesFic ON lignesFic.noFic=fiches.noFic
JOIN articles ON articles.refart=lignesFic.refart
JOIN gammes ON gammes.codeGam=articles.codeGam
JOIN grilleTarifs ON grilleTarifs.codeGam=gammes.codeGam
JOIN tarifs ON tarifs.codeTarif=grilleTarifs.codeTarif
WHERE fiches.noFic=1002 
GROUP BY lignesFic.refart
```
|noFic|nom|prenom|refart|designation|depart|retour|prixJour|Montant|Total|
|---|---|---|---|---|---|---|---|---|---|
|1002|Desmoulin|Daniel|A03|"Salomon 24X+Z12"|2024-11-18|2024-11-22|10|50|200|
|1002|Desmoulin|Daniel|A04|"Salomon 24X+Z12"|2024-11-19|2024-11-24|10|60|200|
|1002|Desmoulin|Daniel|S03|"Décathlon Apparition"|2024-11-23|NULL|10|90|200|

### 7) Grille des tarifs ?

```sql
SELECT categories.libelle,tarifs.libelle,gammes.libelle,tarifs.prixjour FROM tarifs 
JOIN grilleTarifs ON grilleTarifs.codeTarif=tarifs.codeTarif
JOIN gammes ON gammes.codeGam=grilleTarifs.codeGam
JOIN categories ON categories.codeCate=grilletarifs.codeCate
```
|libelle|libelle|libelle|prixJour|  
|---|---|---|---|
|Ski de fond alternatif|Entrée de gamme|Base|10|
|Ski de fond patineur|Entrée de gamme|Chocolat|15|
|Monoski|Entrée de gamme|Base|10|
|Patinette|Entrée de gamme|Base|10|
|Ski alpin|Entrée de gamme|Base|10|
|Surf|Entrée de gamme|Base|10|
|Ski de fond alternatif|Haut de gamme|Argent|30|
|Ski de fond patineur|Haut de gamme|Argent|30|
|Ski alpin|Haut de gamme|Argent|30|
|Surf|Haut de gamme|Bronze|20|
|Ski de fond alternatif|Moyenne gamme|Chocolat|15|
|Ski de fond patineur|Moyenne gamme|Bronze|20|
|Monoski|Moyenne gamme|Chocolat|15|
|Patinette|Moyenne gamme|Chocolat|15|
|Ski alpin|Moyenne gamme|Chocolat|15|
|Surf|Moyenne gamme|Chocolat|15|
|Ski de fond alternatif|Matériel Professionnel|Platine|90|
|Ski de fond patineur|Matériel Professionnel|Platine|90|
|Ski alpin|Matériel Professionnel|Platine|90|
|Surf|Matériel Professionnel|Or|50|

### 8) Liste des locations de la catégorie SURF ?

```sql
SELECT articles.refart,articles.designation,COUNT(lignesFic.noFic)
FROM articles
JOIN lignesFic ON lignesFic.refart=articles.refart
JOIN categories ON categories.codeCate=articles.codeCate
where categories.libelle="surf"
GROUP BY articles.refart
```
|refart|designation|nbLocation|
|---|---|---|
|S01|"Décathlon Apparition"|2|
|S02|"Décathlon Apparition"|2|
|S03|"Décathlon Apparition"|2|

### 9) Calcul du nombre moyen d’articles loués par fiche de location ?
) AS sous_requete;

```sql
SELECT 
    AVG(nb_articles)
FROM (
    SELECT noFic,COUNT(refart) AS nb_articles
    FROM lignesFic
    GROUP BY noFic
);
```
|nb_lignes_moyen_par_fiche|
|---|
|2.375000|

### 10) Calcul du nombre de fiches de location établies pour les catégories de location Ski alpin, Surf et Patinette ?

```sql
SELECT categories.libelle,COUNT(lignesFic.noFic)
FROM categories
JOIN articles ON categories.codeCate=articles.codeCate
JOIN lignesFic ON lignesFic.refart=articles.refart
where categories.libelle IN ("ski alpin","surf","Patinette")
GROUP BY categories.libelle
```

|catégorie|nombre de location|
|---|---|
|Ski alpin|2|
|Patinette|1|
|Surf|6|


