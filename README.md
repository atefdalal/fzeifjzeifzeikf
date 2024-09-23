# testttt
USE m07_drone;

CREATE TABLE utilisateur (
    idutilisateur INT(11) PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(45),
    prenom VARCHAR(45),
    email VARCHAR(45),
    naissance,
    pseudo VARCHAR(45) 
);

CREATE TABLE drone (
    iddrone INT(11) PRIMARY KEY AUTO_INCREMENT,
    marque VARCHAR(45),
    modele VARCHAR(45),
    refDrone VARCHAR(45),
    dateAchat TIMESTAMP 
);

CREATE TABLE vol (
    idvol INT PRIMARY KEY AUTO_INCREMENT,
    idutilisateurs INT,
    iddrone INT NOT NULL,
    dateVol TIMESTAMP NOT NULL,
    FOREIGN KEY (idutilisateurs) REFERENCES utilisateur(idutilisateur) ON DELETE CASCADE,
    FOREIGN KEY (iddrone) REFERENCES drone(iddrone) ON DELETE CASCADE
);

CREATE TABLE listeCommandes (
    idlisteCommandes INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(45)
);

CREATE TABLE commandes (
    idcommandes INT(11) PRIMARY KEY AUTO_INCREMENT,
    idvol INT(11),
    idlisteCommandes INT(11),
    valeur INT(11),
    time_ms INT(11),
    FOREIGN KEY (idvol) REFERENCES vol(idvol) ON DELETE CASCADE,
    FOREIGN KEY (idlisteCommandes) REFERENCES listeCommandes(idlisteCommandes) ON DELETE CASCADE
);

CREATE TABLE etats (
    idetats INT PRIMARY KEY AUTO_INCREMENT,
    idvol INT,
    pitch FLOAT,
    roll FLOAT,
    yaw FLOAT,
    vgx FLOAT,
    vgy FLOAT,
    vgz FLOAT,
    templ INT,
    temph INT,
    tof INT,
    h INT,
    bat INT,
    baro FLOAT,
    time INT,
    agx FLOAT,
    agy FLOAT,
    agz FLOAT,
    FOREIGN KEY (idvol) REFERENCES vol(idvol) ON DELETE CASCADE
);






-----
-
-
-
-
--
------


1. Vérifier si tu as déjà une clé SSH
Avant de générer une nouvelle clé SSH, il est important de vérifier si tu en as déjà une sur ton ordinateur. Pour cela, ouvre Git Bash et tape la commande suivante :

ls -al ~/.ssh
Cela listera les fichiers dans le dossier .ssh de ton utilisateur. Si tu vois des fichiers comme id_rsa et id_rsa.pub, cela signifie que tu as déjà une paire de clés SSH. Tu peux les utiliser directement, mais si tu veux en créer une nouvelle, passe à l'étape suivante.

2. Générer une nouvelle clé SSH
Si tu n'as pas encore de clé SSH ou si tu veux en créer une nouvelle, suis ces étapes :

Dans Git Bash, entre la commande suivante pour générer une nouvelle clé SSH :
ssh-keygen -t rsa -b 4096 -C "atef.dalal2005@gmail.com"
L'option -t rsa spécifie que tu utilises l'algorithme RSA (c'est standard).
L'option -b 4096 spécifie la taille de la clé (4096 bits est une bonne sécurité).
Remplace "ton_email@example.com" par ton adresse email GitHub.

Tu devrais voir une sortie comme celle-ci :
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/YourName/.ssh/id_rsa): [Appuie sur Entrée]
Appuie simplement sur Entrée pour accepter l'emplacement par défaut. Tu peux aussi définir un mot de passe pour protéger ta clé si tu le souhaites.

3. Ajouter ta clé SSH à l'agent SSH
Maintenant que tu as généré une clé SSH, tu dois l'ajouter à l'agent SSH (un programme qui gère les clés SSH) pour qu'il puisse l'utiliser automatiquement lors des connexions. Tape cette commande dans Git Bash pour démarrer l'agent SSH :
eval "$(ssh-agent -s)"
Ensuite, ajoute ta clé SSH à l'agent avec cette commande :
ssh-add ~/.ssh/id_rsa
Cette commande suppose que tu as utilisé le nom de fichier par défaut pour la clé (id_rsa). Si tu as choisi un autre nom, remplace id_rsa par le bon nom.

4. Ajouter ta clé SSH à GitHub
Maintenant, tu dois ajouter ta clé publique sur ton compte GitHub pour permettre l'authentification. La clé publique est stockée dans le fichier id_rsa.pub. Pour afficher le contenu de cette clé publique, tape :

bash
Copier le code
cat ~/.ssh/id_rsa.pub
Cela va afficher quelque chose comme :

css
Copier le code
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEArI9J9V... nom@machine
Copie tout le contenu affiché (commençant par ssh-rsa) dans ton presse-papiers.

Ensuite, va sur GitHub :

Ouvre la page des clés SSH sur GitHub.
Clique sur New SSH key.
Colle ta clé publique dans le champ "Key" et donne-lui un titre (par exemple, "Clé SSH lycée").
Clique sur Add SSH key.
5. Changer l'URL de ton dépôt GitHub pour utiliser SSH
Si ton dépôt GitHub utilise actuellement l'URL HTTPS, tu dois la remplacer par l'URL SSH.

Dans le répertoire de ton projet (où se trouve ton dépôt Git local), exécute cette commande pour changer l'URL :

bash
Copier le code
git remote set-url origin git@github.com:username/nom-du-depot.git
Remplace username par ton nom d'utilisateur GitHub, et nom-du-depot par le nom du dépôt sur GitHub.

Tu peux vérifier si l'URL a bien été modifiée avec cette commande :

bash
Copier le code
git remote -v
Tu devrais voir quelque chose comme :

scss
Copier le code
origin  git@github.com:username/nom-du-depot.git (fetch)
origin  git@github.com:username/nom-du-depot.git (push)
6. Vérifier la connexion SSH avec GitHub
Avant de faire un push, tu peux vérifier que la connexion SSH fonctionne correctement. Pour cela, utilise cette commande :

bash
Copier le code
ssh -T git@github.com
La première fois que tu fais cela, tu verras un message te demandant si tu veux ajouter GitHub à la liste des hôtes connus. Tape yes et appuie sur Entrée. Si tout fonctionne bien, tu verras un message comme celui-ci :

vbnet
Copier le code
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
Cela signifie que tu es connecté à GitHub via SSH.

7. Pusher ton code avec Git
Maintenant que tout est configuré, tu peux essayer de pusher tes changements sur GitHub :

bash
Copier le code
git add .
git commit -m "Ton message de commit"
git push origin main
Si tout est correctement configuré, le push devrait se faire sans que Git Bash te demande des identifiants ou des permissions.

Résumé des étapes :
Vérifier si tu as déjà une clé SSH (ls -al ~/.ssh).
Générer une clé SSH si besoin (ssh-keygen -t rsa -b 4096 -C "email").
Ajouter la clé à l'agent SSH (ssh-add ~/.ssh/id_rsa).
Ajouter la clé publique sur GitHub.
Changer l'URL du dépôt pour utiliser SSH (git remote set-url origin git@github.com:username/repo.git).
Vérifier la connexion SSH avec GitHub (ssh -T git@github.com).
Faire un push sur ton dépôt GitHub.
Dis-moi si tu as des questions ou si tu rencontres un problème dans l'une des étapes.
