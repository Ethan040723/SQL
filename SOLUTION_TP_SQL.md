## TP1 et TP2 
'''
DROP DATABASE IF EXISTS zoo;
CREATE DATABASE zoo CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE zoo
USE zoo;
DROP TABLE IF EXISTS chat;
CREATE TABLE IF NOT EXISTS chat (
id int NOT NULL auto_increment,
nom VARCHAR(50)NOT NULL,
yeaux VARCHAR(50) NOT NULL,
age int,
CONSTRAINT pk_chat PRIMARY KEY (id)
) ENGINE=InnoDB;

INSERT INTO chat (nom,yeaux,age) 
VALUES
(  "MUSSOLINI", "VERT" , 10 ),
("ADOLFO", "BLEU", 9),
("STALINE", "MARRON",5);


USE invitation;
DROP TABLE IF EXISTS personne; 
CREATE TABLE IF NOT EXISTS personne(
pers_id INT NOT NULL AUTO_INCREMENT,
pers_prenom VARCHAR(50),
pers_nom VARCHAR(50),
pers_age INT,
pers_date DATE NOT NULL,
pers_etat BOOL,
pers_status ENUM("membre","non membre"),
pers_CV TEXT ,
pers_salaire INT,
CONSTRAINT pk_id PRIMARY KEY (pers_id)
)ENGINE=InnoDB;

INSERT INTO personne (pers_prenom,pers_nom,pers_age,pers_date,pers_etat,pers_status,pers_CV,pers_salaire) VALUES
("COUCOU","SALUT",32,20/10/2025,true,"membre","negioepogjepj",350000);
SELECT * FROM personne
'''
## TP3
'''
DROP DATABASE IF EXISTS zoo;
CREATE DATABASE zoo CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE zoo;
DROP TABLE IF EXISTS chat;
CREATE TABLE IF NOT EXISTS chat (
id int NOT NULL auto_increment,
nom VARCHAR(50)NOT NULL,
yeaux VARCHAR(50) NOT NULL,
age int,
CONSTRAINT pk_chat PRIMARY KEY (id)
) ENGINE=InnoDB;

INSERT INTO chat (nom,yeaux,age) 
VALUES
(  "Maine coon","marron",20 ),
("Siamois","bleu",15),
("Scottish Fold","marron",10),
("Bengal","marron",18);

SELECT * FROM chat WHERE id=2; 
SELECT * FROM chat ORDER BY nom  DESC;
SELECT * FROM chat WHERE age BETWEEN 11 AND 19;
USE zoo;
DROP TABLE IF EXISTS chat;
CREATE TABLE IF NOT EXISTS chat (
id int NOT NULL auto_increment,
nom VARCHAR(50)NOT NULL,
yeaux VARCHAR(50) NOT NULL,
age int,
CONSTRAINT pk_chat PRIMARY KEY (id)
) ENGINE=InnoDB;

INSERT INTO chat (nom,yeaux,age) 
VALUES
(  "Maine coon","marron",20 ),
("Siamois","bleu",15),
("Scottish Fold","marron",10),
("Bengal","marron",18);

SELECT * FROM chat WHERE id=2;
SELECT * FROM chat ORDER BY nom  DESC;
SELECT * FROM chat WHERE age BETWEEN 11 AND 19;
USE zoo;
DROP TABLE IF EXISTS chat;
CREATE TABLE IF NOT EXISTS chat (
id int NOT NULL auto_increment,
nom VARCHAR(50)NOT NULL,
yeaux VARCHAR(50) NOT NULL,
age int,
CONSTRAINT pk_chat PRIMARY KEY (id)
) ENGINE=InnoDB;

INSERT INTO chat (nom,yeaux,age) 
VALUES
(  "Maine coon","marron",20 ),
("Siamois","bleu",15),
("Scottish Fold","marron",10),
("Bengal","marron",18);

SELECT * FROM chat WHERE id=2;
SELECT * FROM chat ORDER BY nom  DESC;
SELECT * FROM chat WHERE age BETWEEN 11 AND 19;
SELECT * FROM chat WHERE nom LIKE "%sia%"
SELECT * FROM chat WHERE nom LIKE "%a%"
SELECT AVG(age) FROM  chat ;
SELECT COUNT(id) FROM chat
SELECT COUNT(id) FROM chat WHERE yeaux = "marron";
SELECT * FROM chat ORDER BY age ASC LIMIT 1;
SELECT * FROM chat ORDER BY age DESC LIMIT 1;
SELECT COUNT(id) FROM chat GROUP BY yeaux
LOAD DATA INFILE '/Utilisateurs/Ethan/Vidéos/chats.csv'
INTO TABLE chat
FIELDS TERMINATED BY ';'        -- Délimiteur de champ (virgule dans un fichier CSV)
ENCLOSED BY '"'                 -- Valeurs entre guillemets (si applicable)
LINES TERMINATED BY '\n'        -- Délimiteur de ligne (nouvelle ligne)
IGNORE 1 LINES;                 -- Ignore la première ligne (en-tête du fichier CSV)

POUR UPDATE ET DELETE :
UPDATE chat SET age=21 WHERE id =1 ;
DELETE FROM chat WHERE id = 3;
'''
## TP4
'''
DROP DATABASE IF EXISTS invitations;
CREATE DATABASE invitations CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE invitations;
DROP TABLE IF EXISTS personne; 
CREATE TABLE IF NOT EXISTS personne(
pers_id INT NOT NULL AUTO_INCREMENT,
pers_prenom VARCHAR(50),
pers_nom VARCHAR(50),
pers_age INT,
pers_date DATE NOT NULL,
pers_etat BOOL,
pers_status ENUM("membre","non membre"),
pers_CV TEXT ,
pers_salaire INT,
CONSTRAINT pk_id PRIMARY KEY (pers_id)
)ENGINE=InnoDB;

INSERT INTO personne (pers_prenom,pers_nom,pers_age,pers_date,pers_etat,pers_status,pers_CV,pers_salaire) VALUES
("Brad","PITT",60,01/01/1970,True,"non membre","lorem ipsum",2000000),
("George","CLONEY",62,01/01/1999,True,"membre","juste beau",4000000),
("Jean","DUJARDIN",51,01/01/1994,False,"membre","brice de nice",100000);

SELECT MAX(pers_salaire) FROM personne;
SELECT MIN(pers_salaire) FROM personne;
SELECT pers_nom,pers_prenom,pers_salaire FROM personne ORDER BY pers_salaire ASC limit 1 ;
SELECT pers_nom,pers_prenom,pers_salaire FROM personne ORDER BY pers_salaire DESC limit 1 ;
SELECT AVG(pers_salaire) FROM personne;
SELECT COUNT(pers_id) FROM personne;
SELECT *  FROM personne WHERE pers_salaire BETWEEN 1000000 AND 4000000;
SELECT pers_id,pers_nom,pers_prenom,UPPER(pers_prenom)  FROM personne;
SELECT pers_id,pers_nom,pers_prenom,LOWER(pers_nom) FROM personne;
SELECT * FROM personne WHERE pers_prenom LIKE "%bra%";
SELECT * FROM personne ORDER BY pers_age DESC;
SELECT COUNT(pers_status) FROM personne WHERE pers_status = "membre" ;
Select pers_status,COUNT(pers_id) FROM personne WHERE pers_status GROUP BY pers_status;
'''
## TP5
'''
DROP DATABASE IF EXISTS salade_de_fruits;
CREATE DATABASE salade_de_fruits CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE salade_de_fruits;
DROP TABLE IF EXISTS chats;
DROP TABLE IF EXISTS couleurs;
CREATE TABLE IF NOT EXISTS couleurs(
id INT NOT NULL AUTO_INCREMENT, 
nom VARCHAR(50),
CONSTRAINT pk_id PRIMARY KEY(id)
)ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS chats (
id int NOT NULL AUTO_INCREMENT,
nom VARCHAR(50) ,
age int ,
couleurs_id int NULL,
CONSTRAINT pk_id PRIMARY KEY(id),
CONSTRAINT fk_couleur FOREIGN KEY (couleurs_id) REFERENCES couleurs(id)
)ENGINE=InnoDB;


INSERT INTO couleurs (nom)
VALUES
("marron"),
("bleu"),
("vert");

INSERT INTO chats (nom,age,couleurs_id) 
VALUES
(  "Maine coon",20 ,1 ),
("Siamois",15,2),
("Scottish Fold",10,1),
("Bengal",18,1),
("DOMESTIQUE",21,null);

Select * FROM chats 
INNER JOIN couleurs ON chats.couleurs_id=couleurs.id

Select * FROM chats 
LEFT JOIN couleurs ON chats.couleurs_id=couleurs.id

Select * FROM chats 
LEFT JOIN couleurs ON chats.couleurs_id=couleurs.id
WHERE couleurs_id=null


Select couleurs.nom,COUNT(chats.id) FROM chats 
INNER JOIN couleurs ON chats.couleurs_id=couleurs.id
GROUP BY couleurs.nom

Select couleurs.nom,COUNT(chats.id) FROM chats 
RIGHT JOIN couleurs ON chats.couleurs_id=couleurs.id
GROUP BY couleurs.nom

SELECT AVG(Faste) FROM(
Select COUNT(chats.id) AS Faste FROM chats 
INNER JOIN couleurs ON chats.couleurs_id=couleurs.id
GROUP BY couleurs.id)
'''
## TP6
'''
DROP DATABASE IF EXISTS Netflix;
CREATE DATABASE Netflix CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE Netflix;

DROP TABLE IF EXISTS categ;
DROP TABLE IF EXISTS film;

CREATE TABLE IF NOT EXISTS categ (
id int AUTO_INCREMENT,
nom VARCHAR(200),
CONSTRAINT pk_id PRIMARY KEY (id)
);

CREATE TABLE IF NOT EXISTS film (
id INT AUTO_INCREMENT,
nom VARCHAR(50),
sortie DATE,
categ_id INT,
CONSTRAINT pk_film PRIMARY KEY (id),
CONSTRAINT fk_film FOREIGN KEY (categ_id) REFERENCES categ(id)
);

INSERT INTO categ (nom) VALUES
("Science Fiction"),
("Thriller");

INSERT INTO film (nom,sortie,categ_id) VALUES
("STAR WARS","1977-05-25",1),
("THE MATRIX","1999-06-23",1),
("PULP FICTION","1994-10-26",2);


SELECT film.nom,sortie,categ.nom FROM film 
INNER JOIN categ ON film.categ_id=categ.id
'''
## TP7
'''
DROP DATABASE IF EXISTS clients;
CREATE DATABASE clients CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE clients;



DROP TABLE IF EXISTS facture;
DROP TABLE IF EXISTS devis;
DROP TABLE IF EXISTS projet;
DROP TABLE IF EXISTS client;

CREATE TABLE IF NOT EXISTS client(
id INT AUTO_INCREMENT,
nom VARCHAR(200),
CONSTRAINT pk_client PRIMARY KEY (id)
)ENGINE= InnoDB;

CREATE TABLE IF NOT EXISTS projet( 
id INT AUTO_INCREMENT,
nom VARCHAR(200),
id_client INT,
CONSTRAINT pk_projet PRIMARY KEY (id),
CONSTRAINT fk_projets FOREIGN KEY (id_client) REFERENCES client(id)
)ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS devis(
id INT AUTO_INCREMENT,
nom VARCHAR(200),
version INT ,
info VARCHAR(200),
prix INT,
id_projet INT,
CONSTRAINT pk_devis PRIMARY KEY (id),
CONSTRAINT fk_projet FOREIGN KEY (id_projet) REFERENCES projet(id)
)ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS facture(
id INT AUTO_INCREMENT,
nom VARCHAR(200),
dates DATE,
paiment DATE,
total INT,
id_devis INT,
CONSTRAINT pk_facture PRIMARY KEY (id),
CONSTRAINT fk_facture FOREIGN KEY (id_devis) REFERENCES devis(id)
)ENGINE=InnoDB;

INSERT INTO client (nom) VALUES
('Mairie de Rennes'),
('Neo Soft'),
('Sopra'),
('Accenture'),
('Amazon');

INSERT INTO projet ( nom, id_client) VALUES
('Creation de site internet', 1),
('Logiciel CRM', 2),
('Logiciel de devis', 3),
('Site internet ecommerce', 4),
('logiciel ERP', 2),
('logiciel Gestion de Stock', 5);


INSERT INTO devis ( nom, version, info, prix, id_projet) VALUES
( 'DEV2100A', 1, 'Site internet', 3000, 1),
( 'DEV2100B', 2, 'Site internet', 5000, 1),
( 'DEV2100C', 1, 'Logiciel CRM', 5000, 2),
( 'DEV2100D', 1, 'Logiciel devis', 3000, 3),
( 'DEV2100E', 1, 'Site internet ecommerce', 5000, 4),
( 'DEV2100F', 1, 'logiciel ERP', 2000, 5),
( 'DEV2100G', 1, 'logiciel Gestion de Stock', 1000, 6);

-- Insérer les factures
INSERT INTO facture ( nom, dates, paiment,total, id_devis) VALUES
( 'FA001', '2023-09-01', '2023-10-01',1500, 1),
( 'FA002', '2023-09-20', NULL,1500, 1),
( 'FA003', '2024-02-01', NULL,5000, 3),
( 'FA004', '2024-03-03', '2024-04-03',3000, 4),
( 'FA005', '2023-03-01', NULL,5000, 5),
( 'FA006', '2023-03-01', NULL,2000, 6);

SELECT facture.nom,client.nom,devis.info,facture.total,facture.dates,facture.paiment FROM facture 
INNER JOIN devis ON facture.id_devis=devis.id
INNER JOIN projet ON devis.id_projet=projet.id
INNER JOIN client ON projet.id_client=client.id

SELECT client.nom,COUNT(facture.id) FROM facture 
RIGHT JOIN devis ON facture.id_devis=devis.id
RIGHT JOIN projet ON devis.id_projet=projet.id
RIGHT JOIN client ON projet.id_client=client.id
GROUP BY client.nom


SELECT client.nom,SUM(facture.total) FROM facture 
RIGHT JOIN devis ON facture.id_devis=devis.id
RIGHT JOIN projet ON devis.id_projet=projet.id
RIGHT JOIN client ON projet.id_client=client.id
GROUP BY client.nom

SELECT SUM(facture.total) FROM facture 
RIGHT JOIN devis ON facture.id_devis=devis.id
RIGHT JOIN projet ON devis.id_projet=projet.id
RIGHT JOIN client ON projet.id_client=client.id

SELECT facture.nom,DATEDIFF(NOW(),facture.dates) FROM facture 
RIGHT JOIN devis ON facture.id_devis=devis.id
RIGHT JOIN projet ON devis.id_projet=projet.id
RIGHT JOIN client ON projet.id_client=client.id
WHERE facture.paiment IS NULL AND DATEDIFF(NOW(),facture.dates)>30
GROUP BY facture.nom;

SELECT client.nom,facture.nom,DATEDIFF(NOW(),facture.dates) FROM facture 
RIGHT JOIN devis ON facture.id_devis=devis.id
RIGHT JOIN projet ON devis.id_projet=projet.id
RIGHT JOIN client ON projet.id_client=client.id
WHERE facture.paiment IS NULL AND DATEDIFF(NOW(),facture.dates)>30
GROUP BY facture.nom;
'''
## TP8
'''
DROP DATABASE IF EXISTS prime_vdo;
CREATE DATABASE prime_vdo CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE prime_vdo;

CREATE TABLE film (
  id INT  NOT NULL AUTO_INCREMENT,
  nom VARCHAR(100) NOT NULL,
  CONSTRAINT pk_film PRIMARY KEY(id)
)ENGINE=INNODB;

CREATE TABLE acteur (
  id INT NOT NULL AUTO_INCREMENT,
  prenom VARCHAR(100) NOT NULL,
  nom VARCHAR(100) NOT NULL,
   CONSTRAINT pk_acteur PRIMARY KEY(id)
)ENGINE=INNODB;

CREATE TABLE film_has_acteur (
  film_id INT NOT NULL,
  acteur_id INT NOT NULL,
  CONSTRAINT pk_film_has_acteur PRIMARY KEY (film_id, acteur_id)
)ENGINE=INNODB;

ALTER TABLE film_has_acteur ADD CONSTRAINT fk_acteur FOREIGN KEY (acteur_id) REFERENCES acteur (id);
ALTER TABLE film_has_acteur ADD CONSTRAINT fk_film FOREIGN KEY (film_id) REFERENCES film (id);



INSERT INTO acteur (id, prenom, nom) VALUES
(1, 'Brad', 'PITT'),
(2, 'Léonardo', 'Dicaprio');

INSERT INTO film (id, nom) VALUES
(1, 'Fight Club'),
(2, 'Once Upon a time in Hollywood');

INSERT INTO film_has_acteur 
(film_id, acteur_id) 
VALUES 
('1', '1'), 
('2', '1'), 
('2', '2');

select film.nom,acteur.nom,acteur.prenom FROM film_has_acteur
RIGHT JOIN acteur ON film_has_acteur.acteur_id=acteur.id
RIGHT JOIN film ON film_has_acteur.film_id=film.id
WHERE acteur.nom = "PITT" AND acteur.prenom = "Brad";

SELECT acteur.prenom,acteur.nom,COUNT(film.id) FROM film_has_acteur
RIGHT JOIN film ON film_has_acteur.film_id=film.id
RIGHT JOIN acteur ON film_has_acteur.acteur_id=acteur.id
GROUP BY acteur.prenom

INSERT INTO film (id,nom) VALUES
(3,"TITANIC");

SELECT film.nom FROM film

INSERT INTO film_has_acteur VALUES
(3,2);

SELECT film.nom,acteur.nom,acteur.prenom FROM film_has_acteur
JOIN film ON film_has_acteur.film_id=film.id
JOIN acteur ON film_has_acteur.acteur_id=acteur.id

INSERT INTO acteur (id,prenom,nom) VALUES
(3,"Tom","CRUISE");

SELECT acteur.nom,acteur.prenom,COUNT(film.id) FROM film_has_acteur
RIGHT JOIN film ON film_has_acteur.film_id=film.id
RIGHT JOIN acteur ON film_has_acteur.acteur_id=acteur.id
GROUP BY acteur.nom

SELECT acteur.nom,acteur.prenom,COUNT(film.id) FROM film_has_acteur
RIGHT JOIN film ON film_has_acteur.film_id=film.id
RIGHT JOIN acteur ON film_has_acteur.acteur_id=acteur.id
GROUP BY acteur.nom
HAVING COUNT(film.id)=2
'''

## TP9
'''
DROP DATABASE IF EXISTS ecommerce;
CREATE DATABASE ecommerce CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE ecommerce;


DROP TABLE IF EXISTS client;
DROP TABLE IF EXISTS article;
DROP TABLE IF EXISTS commande;

CREATE TABLE IF NOT EXISTS client (
id INT AUTO_INCREMENT,
nom VARCHAR(200),
prenom VARCHAR(200),
CONSTRAINT pk_client PRIMARY KEY (id)
)ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS article(
id INT AUTO_INCREMENT,
nom VARCHAR(200),
prix DECIMAL(7.2),
CONSTRAINT pk_article PRIMARY KEY (id)
)ENGINE=InnoDB;

CREATE TABLE IF NOT EXISTS commande(
id INT AUTO_INCREMENT,
nb_article INT,
date_achat DATETIME,
total DECIMAL(8.2),
id_client INT,
id_article INT,
CONSTRAINT pk_commande PRIMARY KEY (id),
CONSTRAINT fk_commande FOREIGN KEY (id_client) REFERENCES client(id),
CONSTRAINT fk_commande2 FOREIGN KEY (id_article) REFERENCES article(id)
)ENGINE=InnoDB;

INSERT INTO client (nom,prenom) VALUES
("PITT","Brad"),
("CLONEY","George"),
("DUJARDIN","Jean");

INSERT INTO article (nom,prix) VALUES
("Playstation 5",400.00),
("Xbox x",350.00),
("Machine à café",300.00),
("Playstation 3", 100.00);


INSERT INTO commande (nb_article,date_achat,total,id_client,id_article) VALUES
(1,"2024-09-08 10:15:00",350.00,1,2),
(1,"2024-09-08 10:15:00",300.00,1,3),
(2,"2024-09-08 10:15:00",200.00,1,4);

SELECT client.nom,client.prenom,commande.date_achat,article.nom,article.prix,commande.nb_article,commande.total FROM commande
INNER JOIN client ON commande.id_client=client.id
INNER JOIN article ON commande.id_article=article.id;

SELECT SUM(commande.total) ,SUM(commande.total)*0.20,SUM(commande.total)*0.20+SUM(commande.total)  FROM commande
INNER JOIN client ON commande.id_client=client.id
INNER JOIN article ON commande.id_article=article.id
'''
## TP10
'''
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


Select * FROM clients WHERE nom LIKE "D%" ;
Select nom,prenom FROM clients ;

SELECT fiches.noFic,fiches.etat,clients.nom,clients.prenom FROM clients
INNER JOIN fiches ON fiches.noCLI=clients.noCLI
WHERE cpo like "44%"

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


SELECT gammes.libelle,AVG(tarifs.prixJour)
FROM fiches
JOIN clients ON clients.noCLI=fiches.noCLI
JOIN lignesFic ON lignesFic.noFic=fiches.noFic
JOIN articles ON articles.refart=lignesFic.refart
JOIN gammes ON gammes.codeGam=articles.codeGam
JOIN grilleTarifs ON grilleTarifs.codeGam=gammes.codeGam
JOIN tarifs ON tarifs.codeTarif=grilleTarifs.codeTarif 
GROUP BY gammes.libelle


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
'''