# Exercice 1

### Questions :
1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?
2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans
votre répertoire personnel ?
3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.
4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.
5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin
de cette question, tapez la commande exit pour revenir dans votre session initiale.
6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.
7. Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace.
Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.
8. Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2
sont vos deux noms) en utilisant la variable NOMS.
9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande
unset ?
10. Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre
dossier personnel d’après bash)

### Réponses :
1. Pour trouver le dossier bash qui trouve les commandes tappées par l'utilisateur il faut réaliser la commande `echo $PATH` ou `printenv PATH`. <br/>
On otient le résultat suivant : > /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
2. La variable d'environnement `~` permet à la commande cd d'accéder directement à notre répertoire personnel.
3. Pour chaque variable il faut réaliser la commande `ècho $nom_variable` pour connaître le rôles de ses variables.
* LANG : permet d'afficher la langue et le type d'encodage. On obtient ces informations : `fr_FR.UTF-8`. Ici on est donc en français et en encodage UTF-8.
* PWD : permet d'afficher le chemin courant. On obtient ces informations : `/home/val`. Ici on est donc dans le répertoire personnel de l'utilisateur "val".
* OLDPWD : permet d'afficher le chemin où l'on se trouvait précédemment.
* SHELL : permet d'accéder au fichier de notre bash. On obtient `/bin/bash`.
4. Pour créer une variable "MY_VAR", on réalise la commande `MY_VAR='valeur_variable'`. Puis on l'affiche avec la commande `echo MY_VAR`.
5. La commande `bash` permet d'ouvrir une nouvelle cession utilisateur. Si on essaye d'afficher à nouveau la variable "MY_VAR" on obtient rien car on avait créé la variable en tant que variable locale. Pour quitter la cession bash il faut réaliser la commande `exit`.
6. Pour transformer la variable "MY_VAR" en variable d'environnement il faut réaliser la commande `export MY_VAR`. Une fois cela réalisé, on peut rouvrir une cession bash et cette fois ci la variable "MY_VAR" est visible.
7. On réalise la commande `echo NOMS='EMILE VALENTIN'` pour créer une variable d'environnement contenant les deux noms de notre binôme.
8. Il faut réaliser la commande ` echo Bonjour à vous deux, $NOMS!` pour afficher "Bonjour à vous deux, EMILE VALENTIN!".
9. Si on donne une valeur vide à la variable d'environnement, celle-ci existe toujours mais elle est vide. Alors que la commande `unset` permet de la supprimer totalement de la liste des variables.
10. Il faut réaliser la commmande `echo \$HOME = $HOME` pour afficher `$HOME = /home/val`.

# Programation BASH

### Questions : 
Vous enregistrerez vos scripts dans un dossier script que vous créerez dans votre répertoire personnel. <br/>
Tous les scripts sont bien entendu à tester.<br/>
Ajoutez le chemin vers script à votre PATH de manière permanente.

### Réponses : 
Pour créer le dossier `script` on réalise la commande `mkdir script`, puis on créer une variable d'environnement "SCRIPT" qui contient le chemin du dossier créer précédemment en réalisant la commande ` export SCRIPT='/home/val/script/'.`

# Excercice 2
### Question : 
Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non aucontenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi parl’utilisateur ne doit pas s’afficher.

### Réponse :
Pour créer le fichier il faut réaliser la commande `touch testpwd.sh`, puis pour autoriser l'exécution du fichier il faut réaliser la commande `chmod u+x testpwd.sh`. <br/>
Enfin il suffit de d'ouvrir le fichier avec la commmande `nano testpwd.sh` et d'y ajouter le scripts suivant : <br/>
```bash
#!/bin/bash <br/>
password="123456789" <br/>
read -s -p 'Entrez le mot de passe :' pass <br/>
echo ' ' <br/>
if [ $pass = $password ]; then <br/>
        echo 'Bon mot de passe' <br/>
else
        echo 'Mauvais mot de passe' <br/>
fi <br/> 
```

Pour enregistrer le fichier il faut utiliser la raccourcis `CTRL + X`.

# Excercice 3

### Question : 
Ecrivez un script qui prend un paramètre et utilise la fonction suivante pour vérifier que ce paramètre est un nombre réel :
```bash
function is_number() <br/>
{ <br/>
re='^[+-]?[0-9]+([.][0-9]+)?$' <br/>
if ! [[ $1 =~ $re ]] ; then <br/>
return 1 <br/>
else <br/>
return 0 <br/>
fi <br/>
} 
``` <br/> 
Il affichera un message d’erreur dans le cas contraire.

### Réponse :

Le script suivant nous permet de vérifier si le nombre est un nombre réel ou non : 
```bash
#!/bin/bash <br/>
function is_number() <br/>
{	<br/>
re='^[+-]?[0-9]+([.][0-9]+)?$'	<br/>
if ! [[ $1 =~ $re ]] ; then	<br/>
        return 1	<br/>
else	<br/>
       return 0	<br/>
fi	<br/>
}	<br/>

read -p "Saisir un nombre réel: " nombre	<br/>
echo ' '	<br/>
if is_number $nombre ; then	<br/>
        echo 'Le nombre est bien un nombre réel'	<br/>
else	<br/>
        echo 'Le nombre n est pas un nombre réel'	<br/>
fi	
``` <br/>
# Excercice 4

### Question : 
Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”, où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre script, le message doit changer automatiquement)

### Réponse : 

