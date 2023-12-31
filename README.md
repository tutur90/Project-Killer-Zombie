# Project Killer Zombie


![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Banniere.png)


L'objectif principal de notre projet était de concevoir un dispositif ingénieux pour piéger les zombies lors d'une invasion. Après une session intense de brainstorming, nous avons pris en compte notre spécialisation en électronique et ses applications au sein de notre école d'ingénieurs. C'est ainsi que nous avons opté pour l'idée fascinante d'un système de détection des zombies, suivi d'une élimination par des éclairs produits grâce à une bobine Tesla. 

![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Projet%20Killer%20Zombie.jpg)

Pour atteindre cet objectif, nous avons choisi de recycler un projet antérieur réalisé par des deuxièmes années de notre école : une bobine Tesla. Nous avons entrepris des améliorations significatives de ce système, en l'adaptant pour qu'il fonctionne en conjonction avec un capteur capable de détecter la présence de zombies. 


![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Shema%20initial.png)


Dans notre première illustration, nous avions envisagé d'incorporer une bobine Tesla contrôlée par un capteur de pression (qui sera ensuite remplacé par un capteur ultrasonore). Nous avions également prévu d'inclure un écran LCD ou des LED pour indiquer l'état de fonctionnement de notre système, ainsi qu'un bouton d'arrêt d'urgence pour le désactiver en cas de besoin (comme pour ramasser les cadavres des zombies). 

Pour controler tout ceci, nous avons chaoisit d'utiliser un microcontrolleur (Nucleo STM 32) avec un relai pour activer la bobine tesla.

## La bobine Tesla

Une bobine Tesla est un dispositif électronique qui utilise des principes de résonance électromagnétique pour produire des arcs électriques spectaculaires et des décharges électriques à haute tension. Elle a été inventée par l'ingénieur et physicien Nikola Tesla à la fin du XIXe siècle. 


Voici les principaux éléments et le fonctionnement d'une bobine Tesla :  

![alt text](https://upload.wikimedia.org/wikipedia/commons/2/2d/Teslacirc2.png)


1. Transformateur d'alimentation : La bobine Tesla nécessite une source d'alimentation électrique pour fonctionner. Un transformateur d'alimentation est utilisé pour augmenter la tension électrique provenant d'une source d'énergie ordinaire (par exemple, le courant alternatif domestique) à une tension beaucoup plus élevée. Le transformateur élève la tension à des milliers, voire des millions de volts, ce qui est essentiel pour générer les arcs électriques. 

2. Bobine primaire : La bobine primaire est composée d'un enroulement de fil de cuivre épais et est connectée au transformateur d'alimentation. Lorsque le courant électrique circule dans la bobine primaire, cela crée un champ magnétique alternatif. 

3. Condensateur : Un condensateur est utilisé pour stocker l'énergie électrique et la libérer de manière contrôlée. Il est connecté en parallèle avec la bobine primaire. Le condensateur est chargé avec une tension élevée provenant de l'alimentation électrique et, lorsqu'il est déchargé, libère cette énergie sous forme d'impulsions électriques rapides. 

![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Condensateur.jpg)

4. Bobine secondaire : La bobine secondaire est composée d'un grand nombre de tours de fil de cuivre fin et est placée à proximité de la bobine primaire. Lorsque les impulsions électriques du condensateur atteignent la bobine secondaire, cela crée un champ magnétique intense qui induit une tension élevée dans la bobine secondaire. Cette tension induite est plusieurs fois supérieure à la tension d'entrée et génère des arcs électriques à haute fréquence au sommet de la bobine. 


5. Éclateurs : Les éclateurs sont des dispositifs de commutation utilisés pour réguler le flux d'électricité entre la bobine primaire et la bobine secondaire. Ils permettent de contrôler le moment de décharge du condensateur dans la bobine primaire, ce qui crée des oscillations et une résonance électromagnétique dans le système. 

6. Arcs électriques : Lorsque le champ magnétique généré par la bobine secondaire atteint une tension suffisamment élevée, cela crée des arcs électriques à haute fréquence qui se forment à partir du sommet de la bobine. Ces arcs peuvent atteindre plusieurs mètres de longueur et sont accompagnés de crépitements caractéristiques. Ils peuvent sauter dans l'air ou se diriger vers des objets conducteurs à proximité. 

Le fonctionnement global de la bobine Tesla repose sur la résonance électromagnétique, où l'énergie électrique est transférée entre les circuits primaire et secondaire grâce aux propriétés résonantes de l'inductance et de la capacité du système. Cela permet d'amplifier la tension et de générer des arcs électriques impressionnants. 

 ## Le microcontroleur
 
![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Boitier%20STM.jpg)

### Capteur de distance et déclenchement de la Tesla :
Les tâches Trigger et écho sont deux tâches qui s’exécutent en parallèle, elles sont toutes deux en lien avec le capteur de distance HC SR04. En effet comme nous avons pu le voir dans la datasheet du composant, il suffit de l’alimenter ainsi que de générer une courte impulsion sur le pin trigger du composant afin qu’il génère un signal d’écho comme réponse.
 Le signal d’écho reste à l’état haut jusqu’à ce que le capteur reçoive l’onde sonore qui a été réfléchie par un obstacle, cette durée est donc proportionnelle à la distance parcourue par l’onde sonore. Le calcul de la distance est alors D = V*T avec V la vitesse du son dans l’air soit 340 m/s.
Une fois que nous avons calculé la distance, on peut alors définir un seuil en dessous duquel nous déclenchons la bobine, nous l’avons défini à 70cm lors de la démonstration de notre projet. 
Le déclenchement de la bobine Tesla se fait par la mise en tension d’une PIN de sortie du STM32, cette PIN est reliée à un circuit électronique simple que nous verrons dans la suite de ce document.

### Bouton d’arrêt :
Nous avons aussi programmé un bouton d’arrêt, il s’agit du bouton bleu du STM32. Un algorigramme n’est pas nécessaire ici puisqu’il s’agit simplement de détecter l’appui du bouton et remettre à zéro la PIN de sortie qui avait été activée lors d’une détection de présence et ce pendant dix secondes nous laissant le temps de couper l’alimentation sans risque.

### Algorigrames

![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Algorigrame%201.png)
![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Algorigrame%202.png)

## Le realai

![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Relai.jpg)

![alt text](https://github.com/tutur90/Project-Killer-Zombie/blob/main/Photos/Shema%20electrique%20relai.jpg)

