## TP11
### BASE DE DONNÉES
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


INSERT INTO clients VALUES(20, 'Dubosc', 'Frank', '12 avenue des flots bleus', '76140', 'Petit-Quevilly');
INSERT INTO clients VALUES(21, 'Boon', 'Dany', '22 rue des Ch''tis', '59280', 'Armentières');
INSERT INTO clients VALUES(22, 'Elmaleh', 'Gad', '45 rue du sentier', '75001', 'Paris');
INSERT INTO clients VALUES(23, 'Dujardin', 'Jean', 'rue Brice', '92500', 'Rueil-Malmaison');
INSERT INTO clients VALUES(24, 'Marceau', 'Sophie', 'Boulevard de la Boom', '75010', 'Paris');
INSERT INTO clients VALUES(25, 'Merad', 'Kad', 'Rue du petit nicolas', '91130', 'Ris-Orangis');
INSERT INTO clients VALUES(26, 'Seigner', 'Mathilde', '357 rue du Camping', '75012', 'Paris');
INSERT INTO clients VALUES(27, 'Reno', 'Jean', '78 Boulevard de Léon', '51200', 'Montmirail');
INSERT INTO clients VALUES(28, 'Lanvin', 'Gérard', '84 avenue de l''aile ou la cuisse', '92100', 'Boulogne-Billancourt');
INSERT INTO clients VALUES(29, 'Tautou', 'Audrey', 'rue de Montmartre', '63110', 'Beaumont');
INSERT INTO clients VALUES(30, 'Cotillard', 'Marion', '45 rue de la Même', '13001', 'Marseille');
INSERT INTO clients VALUES(31, 'Duris', 'Romain', '76 rue de l''arnaqueur', '06000', 'Nice');
INSERT INTO clients VALUES(32, 'Depardieu', 'Gérard', '57 rue du conte de Monté-Cristo', '36000', 'Chateauroux');
INSERT INTO clients VALUES(33, 'Youn', 'Michaël', 'rue de la beuze', '92150', 'Suresnes');
INSERT INTO clients VALUES(34, 'Poelvoorde', 'Benoït', '22 rue du Boulet', '22500', 'Paimpol');
INSERT INTO clients VALUES(35, 'Paradis', 'Vanessa', '12 rue des arnaqueurs', '94100', 'Saint-Maur-des-Fosses');
INSERT INTO clients VALUES(36, 'Wilson', 'Lambert', '100 rue de Dieu', '92200', 'Neuilly-sur-Seine');
INSERT INTO clients VALUES(37, 'Garcia', 'José', '65 rue de la vérité', '75001', 'Paris');
INSERT INTO clients VALUES(38, 'Luchini', 'Fabrice', '73 rue de Beaumarchais', '75016', 'Paris');
INSERT INTO clients VALUES(39, 'Baye', 'Nathalie', '33 rue de Vénus', '27150', 'Mainneville');
INSERT INTO clients VALUES(40, 'Magimel', 'Benoït', '47 rue des petits mouchoirs', '33950', 'Lège-Cap-Ferret');
INSERT INTO clients VALUES(41, 'Cluzet', 'François', '7 rue des apprentis', '75018', 'Paris');
INSERT INTO clients VALUES(42, 'Frot', 'Catherine', 'rue Odette', '69110', 'Sainte Foy-les-Lyon');
INSERT INTO clients VALUES(43, 'Dupontel', 'Albert', '11 impasse de Bernie', '78100', 'Saintermain-en-Laye');
INSERT INTO clients VALUES(44, 'Huppert', 'Isabelle', '8 rue des femmes', '75002', 'Paris');
INSERT INTO clients VALUES(45, 'Deneuve', 'Catherine', '12 rue de Rochefort', '50100', 'Cherbourg-Octeville');
INSERT INTO clients VALUES(46, 'de France', 'Cécile', '17 rue de l''auberge espagnole', '08000', 'Charlesville-Mézières');
```

### 1) Liste des clients (nom, prénom, adresse, code postal, ville) ayant au moins une fiche de location en cours
```sql
SELECT clients.nom,clients.prenom,clients.adresse,clients.cpo,clients.ville FROM clients
INNER JOIN fiches ON clients.noCli=fiches.noCli
INNER JOIN lignesFic ON fiches.noFic=lignesFic.noFic
where lignesFic.retour IS NULL
GROUP BY clients.nom
```
|nom|prenom|adresse|cpo|ville|
|---|---|---|---|---|
|Desmoulin|Daniel|Rue descendantes|21000|Dijon|
|Ferdinand|Francois|Rue de la convention|44100|Nantes|
|Dupond|Camille|Rue Crébillon|44000|Nantes|
|Albert|Anatole|Rue des accacias|61000|Amiens|
|Bernard|Barnabé|Rue du bar |1000|Bourg en presse|

### 2) Détail de la fiche de location de M. Dupond Jean de Paris (avec la désignation des articles loués, la date de départ et de retour)
```sql
SELECT articles.designation,lignesFic.depart,lignesFic.retour FROM clients
INNER JOIN fiches ON clients.noCli=fiches.noCli
INNER JOIN lignesFic ON fiches.noFic=lignesFic.noFic
INNER JOIN articles ON lignesFic.refart=articles.refart
where clients.nom="Dupond" AND clients.prenom="Jean" AND clients.ville="Paris"
GROUP BY articles.designation;
```
|designation|depart|retour|
|---|---|---|
|Décathlon Apparition|2025-03-25 11:59:38|2025-03-26 11:59:38|

### 3) Liste de tous les articles (référence, désignation et libellé de la catégorie) dont le libellé de la catégorie contient ski
```sql
SELECT articles.refart,articles.designation,categories.libelle FROM articles
INNER JOIN categories On categories.codeCate=articles.codeCate
WHERE  categories.libelle LIKE "%Ski%"
Group BY  articles.refart
```
