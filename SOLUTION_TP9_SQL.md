## TP9
### CRÉATION DE LA BASE DE DONNÉES (question 1,2,3)
```sql
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
```
### 4) Afficher la commande de Brad PITT
```sql
SELECT client.nom,client.prenom,commande.date_achat,article.nom,article.prix,commande.nb_article,commande.total FROM commande
INNER JOIN client ON commande.id_client=client.id
INNER JOIN article ON commande.id_article=article.id;

SELECT SUM(commande.total) ,SUM(commande.total)*0.20,SUM(commande.total)*0.20+SUM(commande.total)  FROM commande
INNER JOIN client ON commande.id_client=client.id
INNER JOIN article ON commande.id_article=article.id

```
|prenom|nom|date_achat|nom|prix|nb|total|
|---|---|---|---|---|---|---|
|PITT|Brad|2024-09-08 10:15:00|X box|350|1|350|
|PITT|Brad|2024-09-08 10:15:00|Machine à café|300|1|300|
|PITT|Brad|2024-09-08 10:15:00|PlayStation 3|100|2|200|

|total_ht|total_tva|total_ttc|
|---|---|---|
|850|170|1020|