# Execution d'une application Java

## 1. Squelette d’une application

Une application Java est un programme autonome qui peut être exécuté sur n’importe quelle plate-forme disposant d’une **machine virtuelle** Java.
Tout type d’application peut être développé en Java : interface graphique, accès aux bases de données, applications client/serveur, multithreading...
Une application est composée au minimum d’un fichier **.class** qui doit lui-même contenir au *minimum* le point d’entrée de l’application, la méthode **main()**.

Exemple de la structure minimum d’une application

```java
public class MonApplication { 

	public static void main(String[] arguments) { 
		/* corps de la méthode principale */ 
	}

}
```

Si l’application est importante, il est possible de créer autant de classes que nécessaire. 

Les classes qui ne contiennent pas la méthode main() sont nommées **classes auxiliaires**.

La méthode main() est le premier élément appelé par la machine virtuelle Java au lancement de l’application.

Le corps de cette méthode doit contenir les instructions nécessaires pour le lancement de l’application, c’est-à-dire la création d’instances de classe, l’initialisation de variables et l’appel de méthodes.

Idéalement, la méthode main() peut ne contenir qu’une seule instruction.

La déclaration de la méthode main() se fait toujours suivant la syntaxe suivante :

```java
public static void main(String[] <identificateur>) {...}
```

### public

Modificateur d’accès utilisé pour rendre la méthode accessible à l’ensemble des autres classes et objets de l’application, et également pour que l’interpréteur Java puisse y accéder de l’extérieur au lancement de l’application.

### static

Modificateur d’accès utilisé pour définir la méthode main() comme étant une méthode de classe. La machine virtuelle Java peut donc appeler cette méthode sans avoir à créer une instance de la classe dans laquelle elle est définie.

### void

Mot clé utilisé pour indiquer que la méthode est une procédure qui ne retourne pas de valeur.

### main

Nom de la méthode principale. C'est un mot réservé.

### Identificateur de la méthode.

```java
String <identificateur>[ ] :
```

Paramètre de la méthode, c’est un tableau de chaînes de caractères. Ce paramètre est utilisé pour passer des arguments en ligne de commande au lancement de l’application. 

Dans la plupart des programmes, le nom utilisé pour `<identificateur>` est argument ou args, pour indiquer que la variable contient des arguments pour l’application.

## 2. Arguments en ligne de commande

### a. Principes et utilisation

Une application Java étant un programme autonome, il peut être intéressant de lui fournir des paramètres ou des options qui vont déterminer le comportement ou la configuration du programme au lancement de celui-ci.

Les arguments en ligne de commande sont stockés dans un tableau de chaînes de caractères. Si vous voulez utiliser ces arguments sous un autre format, vous devez faire une conversion de type, du type String vers le type désiré lors de l’utilisation de l’argument.

    Dans quels cas faut-il utiliser les arguments en ligne de commande ?

Les arguments en ligne de commande sont à utiliser au lancement d’une application dès qu’une ou des données utilisées à l’initialisation de votre programme peuvent prendre des valeurs variables en fonction de l’environnement.

Par exemple :

    • nom du port de communication utilisé dans le cas d’une communication avec un matériel périphérique.
    • adresse IP d’une machine sur le réseau dans le cas d’une application client/serveur.
    • nom d’utilisateur et mot de passe dans le cas d’une connexion à une base de données avec gestion des permissions d’accès.

Dans le cas d’une application qui accède à une base de données, il faut en général fournir un nom d’utilisateur et un mot de passe pour ouvrir une session d’accès à la base. Des utilisateurs différents peuvent accéder à la base de données, mais avec des permissions différentes. Il peut donc exister plusieurs sessions différentes. Il n’est pas envisageable de créer une version de l’application pour chaque utilisateur.

De plus, ces informations sont susceptibles d’être modifiées. Il n’est donc pas judicieux de les intégrer dans votre code, car tout changement vous obligerait à modifier votre code source et à le recompiler et à détenir une version pour chaque utilisateur.

    La solution à ce problème réside dans les arguments en ligne de commande.

Il suffit dans votre code d’utiliser le tableau d’arguments de la méthode main qui contient les variables (nom et mot de passe) de votre application.

Ensuite, selon l’utilisateur du programme, il faut au lancement de l’application par l’instruction java, faire suivre le nom de la classe principale par la valeur des arguments de ligne de commande de l’application.

### b. Passage d’arguments à une application Java au moment de l’exécution

Le passage d’arguments à une application Java se fait au lancement de l’application par l’intermédiaire de la ligne de commande. L’exemple de programme suivant montre comment utiliser le passage d’arguments en ligne de commande dans une application Java.

```java
/* Déclaration de la classe principale de l’application */  
public class MaClasse { 

    /* Déclaration de la méthode point d’entrée de l’application*/ 
    public static void main(String[] args) {     
        /* Affichage des arguments de la ligne de commande */   
        for (int i = 0 ; i < args.length; i++){    
            System.out.println("Argument " +i + " = " + args[i]); 
        } 
    
        /* Conversion de deux arguments de la ligne de commande de 
        String vers int, puis addition des valeurs entières, et 
        affichage du résultat */ 
        int somme = Integer.parseInt(args[3]) + Integer.parseInt(args[4]); 
        System.out.println("Argument 3 + Argument 4 = " + somme); 
        } 
}
``` 
|
Après compilation, le programme s’exécute avec la **ligne de commande** suivante :

    >>>java MaClasse société NEEDEMAND "société NEEDEMAND" 2 5

L’exécution du programme affiche les informations suivantes :

    Argument    0    =    société
    Argument    1    =    NEEDEMAND 
    Argument    2    =    société NEEDEMAND 
    Argument    3    =    2 
    Argument    4    =    5 
    Argument    3    +    Argument 4 = 7
