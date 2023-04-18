# STUDI-Eval-03

- Ouvrez votre terminal (ou le terminal depuis votre IDE) et rendez-vous dans le répertoire où vous souhaitez importer le projet :
```cd /chemin/de/votre/projet```

- Connexion à mysql
```mysql -u root -p```

- Création de la BDD
```CREATE DATABASE brault_studi_cine;```

- Connexion à la BBD
```USE brault_studi_cine;```

- Création des tables
```CREATE TABLE Cinema (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50) NOT NULL,
    adresse VARCHAR(255) NOT NULL
);

CREATE TABLE Salle (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50) NOT NULL,
    capacite INT NOT NULL,
    id_cinema INT NOT NULL,
    FOREIGN KEY (id_cinema) REFERENCES Cinema(id) ON DELETE CASCADE
);

CREATE TABLE User (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50) NOT NULL,
    prenom VARCHAR(50) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    mot_de_passe VARCHAR(255) NOT NULL
);

CREATE TABLE Film (
    id INT PRIMARY KEY AUTO_INCREMENT,
    titre VARCHAR(100) NOT NULL,
    duree TIME NOT NULL,
    description TEXT NOT NULL,
    categorie INT NOT NULL
);

CREATE TABLE Seance (
    id INT PRIMARY KEY AUTO_INCREMENT,
    date_seance DATE NOT NULL,
    horaire TIME NOT NULL,
    id_film INT NOT NULL,
    id_salle INT NOT NULL,
    FOREIGN KEY (id_film) REFERENCES Film(id) ON DELETE CASCADE,
    FOREIGN KEY (id_salle) REFERENCES Salle(id) ON DELETE CASCADE
);

CREATE TABLE Ticket (
    id INT PRIMARY KEY AUTO_INCREMENT,
    prix FLOAT NOT NULL,
    type ENUM('plein_tarif', 'etudiant', 'moins_de_14_ans') NOT NULL,
    id_seance INT NOT NULL,
    id_user INT NOT NULL,
    FOREIGN KEY (id_seance) REFERENCES Seance(id) ON DELETE CASCADE,
    FOREIGN KEY (id_user) REFERENCES User(id) ON DELETE CASCADE
); 
```

- Insertion de données dans la BDD
```INSERT INTO cinema (id, nom, adresse)
VALUES (1, 'cinema A', '1 Rue des Cinémas, 75001 Paris'),
       (2, 'cinema B', '15 Rue du Cinéma, 75002 Paris'),
       (3, 'cinema C', '28 Rue des Arts, 75003 Paris');
```

- Sauvegarde de la BDD dans un fichier .sql
```mysqldump -u root -p brault_studi_cine > C:\Users\brault\Desktop\brault_studi_cine.sql```

- Restaurer la BDD
```mysql -u root -p brault_studi_cine < C:\Users\brault\Desktop\brault_studi_cine.sql```

- Si la BDD a été completement effacée
```mysql -u root -p
CREATE DATABASE brault_studi_cine;
USE brault_studi_cine;
SOURCE C:\Users\brault\Desktop\brault_studi_cine.sql
```
