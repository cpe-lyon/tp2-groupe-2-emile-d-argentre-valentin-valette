# Exercice 1

### Questions :
1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?

2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans
votre répertoire personnel ?

3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.

4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.

5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.

6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.

7. Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace. Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.
8. Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS.

9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande
unset ?

10. Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre
dossier personnel d’après bash)

### Réponses :
1. Pour trouver le dossier bash qui trouve les commandes tappées par l'utilisateur il faut réaliser la commande `echo $PATH` ou `printenv PATH`. 
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
Vous enregistrerez vos scripts dans un dossier script que vous créerez dans votre répertoire personnel. 
Tous les scripts sont bien entendu à tester.
Ajoutez le chemin vers script à votre PATH de manière permanente.

### Réponses : 
Pour créer le dossier `script` on réalise la commande `mkdir script`, puis on créer une variable d'environnement "SCRIPT" qui contient le chemin du dossier créer précédemment en réalisant la commande ` export SCRIPT='/home/val/script/'.`

# Excercice 2
### Question : 
Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non aucontenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi parl’utilisateur ne doit pas s’afficher.

### Réponse :
Pour créer le fichier il faut réaliser la commande `touch testpwd.sh`, puis pour autoriser l'exécution du fichier il faut réaliser la commande `chmod u+x testpwd.sh`. 
Enfin il suffit de d'ouvrir le fichier avec la commmande `nano testpwd.sh` et d'y ajouter le scripts suivant : 
```bash
#!/bin/bash 
password="123456789" 
read -s -p 'Entrez le mot de passe :' pass 
echo ' ' 
if [ $pass = $password ]; then 
        echo 'Bon mot de passe' 
else
        echo 'Mauvais mot de passe' 
fi  
```

Pour enregistrer le fichier il faut utiliser la raccourcis `CTRL + X`.

# Excercice 3

### Question : 
Ecrivez un script qui prend un paramètre et utilise la fonction suivante pour vérifier que ce paramètre est un nombre réel :
```bash
function is_number() 
{ 
re='^[+-]?[0-9]+([.][0-9]+)?$' 
if ! [[ $1 =~ $re ]] ; then 
return 1 
else 
return 0 
fi 
} 
```  
Il affichera un message d’erreur dans le cas contraire.

### Réponse :

Le script suivant nous permet de vérifier si le nombre est un nombre réel ou non : 
```bash
#!/bin/bash 
function is_number() 
{	
re='^[+-]?[0-9]+([.][0-9]+)?$'	
if ! [[ $1 =~ $re ]] ; then	
        return 1	
else	
       return 0	
fi	
}	

read -p "Saisir un nombre réel: " nombre	
echo ' '	
if is_number $nombre ; then	
        echo 'Le nombre est bien un nombre réel'	
else	
        echo 'Le nombre n est pas un nombre réel'	
fi	
``` 

# Excercice 4

### Question : 
Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”, où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre script, le message doit changer automatiquement)

### Réponse : 

Le script suivant nous permet de tester si un utilisateur existe en le passant en paramètre du script.
```bash
#!/bin/bash 

if [[ "$1" == "" ]]; then 
        echo "Utilisation : $0 nom_utilisateur" 
        exit 
fi 
users=`cut -d : -f1 /etc/passwd | grep ^$1$ | wc -l` 

if [[ $users -eq 0 ]]; then 
        echo "L'utilisateur $1 n'existe pas !!" 
else 
        echo "L'utilisateur $1 existe !!" 
fi 

``` 

# Exercice 5

### Question :
Écrivez un programme qui calcule le factorielle d’un entier naturel passé en paramètre (on supposera que l’utilisateur saisit toujours un entier naturel).

### Réponse :

Le script ci dessous permet de calculer le factorielle d'un entier : 
```bash
#!/bin/bash 

i=1; 
resultat=1 
for i in $(seq 1 $1); do 
        resultat=$((resultat*i)) 
done 
echo $resultat 

``` 

# Exercice 6 

### Question: 
Écrivez un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner. Le programme écrira ”C’est plus !”, ”C’est moins !” ou ”Gagné !” selon les cas (vous utiliserez $RANDOM).

### Réponse :
A l'aide du script suivant on pour réaliser le jeu du juste prix :
```bash

#!/bin/bash 

nb=$((RANDOM%1000)) 
echo "$nb" 
read -p "Essayez de deviner le nombre choisit aléatoirement par la machine. Saissisez votre proposition" nb_joueur 
while [[ $nb_joueur != $nb ]]; do 
if [[ $nb_joueur < $nb ]]; then 
        read -p "Ce n'est pas le bon chiffre, c'est plus ! " nb_joueur 
else 
        read -p "Ce n'est pas le bon chiffre, c'est moins ! " nb_joueur 
fi 
done 
echo "Bravo ! Le nombre $nb_joueur est le nombre qu'il fallait trouver" 

``` 

# Exercice 7

### Questions:
1. Écrivez un script qui prend en paramètres trois entiers (entre -100 et +100) et affiche le min, le max
et la moyenne. Vous pouvez réutiliser la fonction de l’exercice 3 pour vous assurer que les paramètres
sont bien des entiers.
2. Généralisez le programme à un nombre quelconque de paramètres (pensez à SHIFT)
3. Modifiez votre programme pour que les notes ne soient plus données en paramètres, mais saisies et
stockées au fur et à mesure dans un tableau.

### Réponses : 
1. Le scripts suivant permet de prendre en paramètre trois nombre et de renvoyer le minimum, le maximum et la moyenne :
```bash
#!/bin/bash 

#--------MOY---------------- 

moy=$((($1+$2+$3)/3)) 

#---------MAX--------------- 

if (("$1" < "$2")) ; then 
min=$1 
else 
min=$2 
fi 

if (("$min" < "$3")) ; then 
min=$min 
else 
min=$3 
fi 

#------------MAX------------- 

if (("$1" > "$2")) ; then 
max=$1 
else 
max=$2 
fi 

if (("$max" > "$3")) ; then 
max=$max 
else 
max=$3 
fi 

echo "La moyenne est $moy, le minimum est $min et le maximum est $max" 
``` 

2. Le script suivant nous permet d'obtenir la moyenne, le minimum et le maximum d'un nombre non défini d'argument:

```bash
#!/bin/bash 

min=100  
max=-100 

for arg in $@ 
do 
nb_arg=$((nb_arg + 1)) 
tot=$((tot + arg)) 
if (("$min" < "$arg")) ; then 
min=$min 
else 
min=$arg 
fi 
if (("$max" > "$arg")) ; then 
max=$max 
else 
max=$arg 
fi 

done 

moy=$(($tot / $nb_arg)) 
echo "La moyenne est $moy, le minimum est $min et le maximum est $max" 

``` 

3. Le script suivant nous permet de remplir un tableau de nombre entier de calculer le minimum, le maximum et la moyenne de cette série de nombre :
```bash

#!/bin/bash 

nb_arg=0 
tot=0 

declare -a NB='()' 

while [[ $saisie != "STOP" ]]; do 

read -p "Entrer un nombre ou STOP pour terminé la série" saisie 

if [[ $saisie != "STOP" ]]; then 
NB[${#NB[@]}]=$saisie 
fi 
done 
min=${NB[0]} 
max=${NB[0]} 

for nb in "${NB[@]}";do 

nb_arg=$((nb_arg + 1)) 
tot=$((tot + nb)) 
if (("$min" < "$nb")) ; then 
min=$min 
else 
min=$nb 
fi 
if (("$max" > "$nb")) ; then 
max=$max 
else 
max=$nb 
fi 
done 

moy=$(($tot / $nb_arg)) 

echo "La moyenne est $moy, le minimum est $min et le maximum est $max" 

``` 



