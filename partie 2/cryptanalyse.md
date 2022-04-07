# Ils étaient 8

La piste du suicide est écartée, et le coupable serait donc l'un des employés de la compagnie.
Il vous faut recueillir leurs procès-verbaux.
Prenez la clef ci-joint qui vous permettra d'ouvrir la porte de Silverlake et y avoir accès.
Cependant, la route ne sera pas si simple !

## Objectif 

Forcer l'entrée de la compagnie en obtenant un code, vous aurez accès aux témoignages.
Mais il semblerait qu'ils soient eux-mêmes protéger à leur tour.

--- 

## Résolution 

Un document est mis à votre disposition : id_rsa

Il faut donc récupérer la passphrase que contient ce fichier à l'aide de John the ripper.
La création d'une wordlist est alors nécessaire.

### Wordlist

À partir du site web qui a été préalablement donné, changé l'URL et mettez silverlake.html, vous obtiendrez le site web de l'entreprise et aurez accès à la liste des employés.

À partir de toutes les informations mises entre vos mains, vous pouvez créer votre propre wordlist.

Le mot à ne surtout pas oublier est **PinewoodDrive**, l'adresse de l'entreprise.

---

### Traduction de la clé RSA

L'aide de Kali vous sera précieuse, il faudra intégrer un script python pour permettre de transformer une clef RSA dans un format utilisable par John the Ripper (commande python, le fichier .py contient un script en python qui fera la transformation) (https://github.com/openwall/john/blob/bleeding-jumbo/run/ssh2john.py) 

Une fois que vous avez le fichier en main, utilisez la commande suivante : **python3 ssh2john.py [nom_fichier_clé_rsa] > [nom_fichier].txt**

---

### Obtenir la passphrase

La clé traduite, il faut indiquer à john de retrouver la passphrase à partir de la wordlist créé. Si la wordlist créée ne contient pas la passphrase qui correspond, ça ne fonctionnera pas !

Voici la commande à utiliser : **sudo john –wordlist=[nom_wordlist].txt [nom_fichier].txt** 

---

### Connexion à la machine

Il vous faudra utiliser la commande suivante qui vous permettra l'accès aux témoignages des employés : **ssh -i [nom_fichier_clé_rsa] silverlake@[adresseIp]**

La passphrase donné par John The Ripper vous sera ensuite demandé.

Si tout ce passe comme prévu, Bienvenu à Silverlake & Co !

---

### Les témoignages

Vous remarquerez très vite que le fichier zip contenant les témoignages est protégé par un mot de passe. Mais où peut-il bien être ?
Ce dernier n'est pas très loin, mais se cache un peu, à l'abri des regards indiscrets ! 

Pour le faire apparaître, rien de plus simple : **ls -a** 
Et le voici de retour !

Le mot de passe : **temoignageSL**

Il vous faudra utiliser la commande **unzip** pour lire le contenu du dossier zip.

---

## Flag

Le flag est répartie dans les 8 fichiers contenant les témoignages. Il vous faudra être attentif aux moindres lettres qu'ils contiennent.

**25042002** ***(date de création de l'entreprise)***
