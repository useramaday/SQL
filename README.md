# SQL
Voici le RENDU SQL de la formation de Jean-Frédéric Vincent

# TP 10 - Location ski
# Les données

# Partie 1
- Créer la base de données
```CREATE DATABASE location_ski; USE location_ski;```

# Partie 2
- Edit des tables

```CREATE TABLE clients (
    noCli INT NOT NULL PRIMARY KEY,
    nom VARCHAR(30) NOT NULL,
    prenom VARCHAR(30) NOT NULL,
    adresse VARCHAR(120) NOT NULL,
    cpo VARCHAR(5) NOT NULL,
    ville VARCHAR(80) NOT NULL
);

CREATE TABLE fiches (
    noFic INT NOT NULL PRIMARY KEY,
    noCli INT NOT NULL,
    dateCrea DATE NOT NULL,
    datePaiement DATE,
    etat ENUM('en cours', 'payée', 'annulée') NOT NULL
);

CREATE TABLE lignesFic (
    noLig INT NOT NULL,
    noFic INT NOT NULL,
    refArt CHAR(8) NOT NULL,
    depart DATE NOT NULL,
    retour DATE,
    PRIMARY KEY (noLig, noFic)
); 


CREATE TABLE articles (
    refArt CHAR(8) NOT NULL PRIMARY KEY,
    designation VARCHAR(80) NOT NULL,
    codeGam CHAR(5) NOT NULL,
    codeCate CHAR(5) NOT NULL
);

CREATE TABLE gammes (
    codeGam CHAR(5) NOT NULL PRIMARY KEY,
    libelle VARCHAR(45) NOT NULL
);

CREATE TABLE categories (
    codeCate CHAR(5) NOT NULL PRIMARY KEY,
    libelle VARCHAR(30) NOT NULL
);

CREATE TABLE grilleTarifs (
    codeGam CHAR(5) NOT NULL,
    codeCate CHAR(5) NOT NULL,
    codeTarif CHAR(5) NOT NULL,
    PRIMARY KEY (codeGam, codeCate)
);

CREATE TABLE tarifs (
    codeTarif CHAR(5) NOT NULL PRIMARY KEY,
    libelle VARCHAR(30) NOT NULL,
    prixJour DECIMAL(5, 2) NOT NULL
);

ALTER TABLE fiches ADD CONSTRAINT fk_fiches_clients FOREIGN KEY (noCli) REFERENCES clients(noCli);
ALTER TABLE lignesFic ADD CONSTRAINT fk_lignesFic_fiches FOREIGN KEY (noFic) REFERENCES fiches(noFic);
ALTER TABLE lignesFic ADD CONSTRAINT fk_lignesFic_articles FOREIGN KEY (refArt) REFERENCES articles(refArt);
ALTER TABLE articles ADD CONSTRAINT fk_articles_gammes FOREIGN KEY (codeGam) REFERENCES gammes(codeGam);
ALTER TABLE articles ADD CONSTRAINT fk_articles_categories FOREIGN KEY (codeCate) REFERENCES categories(codeCate);
ALTER TABLE grilleTarifs ADD CONSTRAINT fk_grilleTarifs_gammes FOREIGN KEY (codeGam) REFERENCES gammes(codeGam);
ALTER TABLE grilleTarifs ADD CONSTRAINT fk_grilleTarifs_categories FOREIGN KEY (codeCate) REFERENCES categories(codeCate);
ALTER TABLE grilleTarifs ADD CONSTRAINT fk_grilleTarifs_tarifs FOREIGN KEY (codeTarif) REFERENCES tarifs(codeTarif);```

# Partie 3
