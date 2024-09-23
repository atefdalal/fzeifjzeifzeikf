# testttt
CREATE DATABASE drone_management;
USE drone_management;

-- Table utilisateur
CREATE TABLE utilisateur (
    idutilisateur INT(11) PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(45) NOT NULL,
    prenom VARCHAR(45) NOT NULL,
    email VARCHAR(45) NOT NULL,
    naissance DATE NOT NULL,
    pseudo VARCHAR(45) NOT NULL
);

-- Table drone
CREATE TABLE drone (
    iddrone INT(11) PRIMARY KEY AUTO_INCREMENT,
    marque VARCHAR(45) NOT NULL,
    modele VARCHAR(45) NOT NULL,
    refDrone VARCHAR(45) NOT NULL,
    dateAchat TIMESTAMP NOT NULL
);

-- Table vol
CREATE TABLE vol (
    idvol INT(11) PRIMARY KEY AUTO_INCREMENT,
    idutilisateurs INT(11) NOT NULL,
    iddrone INT(11) NOT NULL,
    dateVol TIMESTAMP NOT NULL,
    FOREIGN KEY (idutilisateurs) REFERENCES utilisateur(idutilisateur) ON DELETE CASCADE,
    FOREIGN KEY (iddrone) REFERENCES drone(iddrone) ON DELETE CASCADE
);

-- Table listeCommandes
CREATE TABLE listeCommandes (
    idlisteCommandes INT(11) PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(45) NOT NULL
);

-- Table commandes
CREATE TABLE commandes (
    idcommandes INT(11) PRIMARY KEY AUTO_INCREMENT,
    idvol INT(11) NOT NULL,
    idlisteCommandes INT(11) NOT NULL,
    valeur INT(11) NOT NULL,
    time_ms INT(11) NOT NULL,
    FOREIGN KEY (idvol) REFERENCES vol(idvol) ON DELETE CASCADE,
    FOREIGN KEY (idlisteCommandes) REFERENCES listeCommandes(idlisteCommandes) ON DELETE CASCADE
);

-- Table etats
CREATE TABLE etats (
    idetats INT(11) PRIMARY KEY AUTO_INCREMENT,
    idvol INT(11) NOT NULL,
    pitch FLOAT NOT NULL,
    roll FLOAT NOT NULL,
    yaw FLOAT NOT NULL,
    vgx FLOAT NOT NULL,
    vgy FLOAT NOT NULL,
    vgz FLOAT NOT NULL,
    templ INT(11) NOT NULL,
    temph INT(11) NOT NULL,
    tof INT(11) NOT NULL,
    h INT(11) NOT NULL,
    bat INT(11) NOT NULL,
    baro FLOAT NOT NULL,
    time INT(11) NOT NULL,
    agx FLOAT NOT NULL,
    agy FLOAT NOT NULL,
    agz FLOAT NOT NULL,
    FOREIGN KEY (idvol) REFERENCES vol(idvol) ON DELETE CASCADE
);
