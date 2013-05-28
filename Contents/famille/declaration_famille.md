# Déclaration de familles {#core-ref:cfc7f53b-7982-431e-a04b-7b54eddf4a75}

## Introduction {#core-ref:4b4cb93e-e717-4a42-888d-c2376deab4bb}

Pour ajouter des familles de document à Dynacase, on va utiliser divers formats
de fichier :

*   Les familles seront définies dans des fichiers csv ;
*   Le code php sera à déployer dans des fichiers php, à intégrer à la plate-forme ;
*   Les documents systèmes seront importés au moyen de fichiers csv ou xml.

## Définition de familles {#core-ref:17500007-32d8-4aee-bc3f-7e569e1cd5a6}

Les familles sont définies dans un fichier csv respectant le format suivant :

*   Encodage : UTF-8,
*   Délimiteur de texte : ` ` (vide),
*   séparateur de colonnes : `;`.

Exemple de définition d'une famille :

    BEGIN;;Animal;;;ZOO_ANIMAL;;;;;;;;;;;
    //;properties;;;;;;;;;;;;;;;
    //propid;value;;;;;;;;;;;;;;;
    ICON;zoo_animal.png;;;;
    METHOD;Method.zoo_animal.php;;;;
    DFLDID;FLD_ZOO_ANIMAL;;;;
    ;;;;;;;;;;;;;;;;
    //;attributes;;;;;;;;;;;;;;;
    //;idattr;idframe;label;T;A;type;ord;vis;need;link;phpfile;phpfunc;elink;constraint;option;Commentaires
    ;;;;;;;;;;;;;;;;
    ATTR;AN_IDENTIFICATION;;Identification;N;N;frame;100;W;;;;;;;;
    ATTR;AN_NOM;AN_IDENTIFICATION;nom;Y;N;text;110;W;Y;;;;;;edittemplate=ZOO:ANIMALNAME:U|viewtemplate=ZOO:ANIMALNAME;
    ATTR;AN_TATOUAGE;AN_IDENTIFICATION;tatouage;N;N;int;120;W;;;;;;;edittemplate=ZOO:ANIMALTATOO:S|viewtemplate=ZOO:ANIMALTATOO:S;
    ATTR;AN_ESPECE;AN_IDENTIFICATION;espèce;N;N;docid('ZOO_ESPECE');130;W;Y;;;;;;creation={es_nom:CT}|doctitle=an_espece_title;
    ATTR;AN_ESPECE_TITLE;AN_IDENTIFICATION;espèce (titre);Y;N;text;140;H;;;;::getTitle(an_espece);;;;
    ATTR;AN_ORDRE;AN_IDENTIFICATION;ordre;N;N;text;150;R;;;;::getdocvalue(an_espece,es_ordre);;;;
    ATTR;AN_CLASSE;AN_IDENTIFICATION;classe;N;N;docid("ZOO_CLASSE");160;R;;;;::getdocvalue( an_espece , es_classe);;;doctitle=auto;
    ATTR;AN_SEXE;AN_IDENTIFICATION;sexe;N;N;enum;170;W;;;;M|Masculin,F|Féminin,H|Hermaphrodite;;;;
    ATTR;AN_PHOTO;AN_IDENTIFICATION;photo;N;N;image;180;W;;;;;;;;
    ATTR;AN_NAISSANCE;AN_IDENTIFICATION;date naissance;N;N;date;190;W;;;;;;::validatePastDate(AN_NAISSANCE);;
    ATTR;AN_ENTREE;AN_IDENTIFICATION;date entree;N;N;date;200;W;;;;;;::validatePastDate(AN_ENTREE);;
    ATTR;AN_ENFANT_T;AN_IDENTIFICATION;liste enfant;N;N;array;210;W;;;;;;;;
    ATTR;AN_ENFANT;AN_ENFANT_T;enfant;N;N;docid("ZOO_ANIMAL");220;W;;;;;;;creation={an_nom:CT,an_espece:an_espece};
    ATTR;AN_CARNETSANTE;AN_IDENTIFICATION;Carnet Santé;N;N;menu;230;W;;%S%app=GENERIC&action=GENERIC_ISEARCH&id=%I%&famid=ZOO_CARNETSANTE&viewone=Y;;;;;;
    ATTR;AN_ENCLOS;AN_IDENTIFICATION;Enclos;N;N;menu;240;W;;%S%app=GENERIC&action=GENERIC_ISEARCH&id=%I%&famid=ZOO_ENCLOS&viewone=Y;;;;;;
    ATTR;AN_PARENT;AN_IDENTIFICATION;Parents;N;N;menu;250;W;;%S%app=GENERIC&action=GENERIC_ISEARCH&generic=Y&id=%I%&famid=ZOO_ANIMAL;;;;;;
    ATTR;AN_PERE;AN_IDENTIFICATION;pere;N;Y;docid('ZOO_ANIMAL');260;R;;;;::getAscendant(M);;;doctitle=auto
    ATTR;AN_MERE;AN_IDENTIFICATION;mere;N;Y;docid('ZOO_ANIMAL');270;R;;;;::getAscendant(F);;;doctitle=auto
    ATTR;AN_FOLDER;;Dossier;N;N;menu;10;W;;%S%app=ZOO&action=ZOO_ANIMALFOLDER&id=%I%;;;;;
    ;;;;;;;;;;;;;;;;
    END;;;;;;;;;;;;;;;;

**Note** : Le format `ODS` (openDocument Spread Sheet) peut aussi être utilisé
comme format de fichier d'importation de famille ou de document.

Ce qui donne, vu dans un tableau :

|          |                       |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| -        |                       |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| BEGIN    |                       | Animal            |                |   | ZOO_ANIMAL |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| //       | properties            |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| //propid | value                 |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| ICON     | zoo_animal.png        |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| METHOD   | Method.zoo_animal.php |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| DFLDID   | FLD_ZOO_ANIMAL        |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
|          |                       |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| //       | attributes            |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| //       | idattr                | idframe           | label          | T | A          | type                | ord | vis | need | link                                                                         | phpfile | phpfunc                               | elink      | constraint                       | option                                   | Commentaires                   |  |  |
|          |                       |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| ATTR     | AN_IDENTIFICATION     |                   | Identification | N | N          | frame               | 100 | W   |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| ATTR     | AN_NOM                | AN_IDENTIFICATION | nom            | Y | N          | text                | 110 | W   | Y    |                                                                              |         |                                       |            |                                  | edittemplate=ZOO:ANIMALNAME:U            | viewtemplate=ZOO:ANIMALNAME    |  |  |
| ATTR     | AN_TATOUAGE           | AN_IDENTIFICATION | tatouage       | N | N          | int                 | 120 | W   |      |                                                                              |         |                                       |            |                                  | edittemplate=ZOO:ANIMALTATOO:S           | viewtemplate=ZOO:ANIMALTATOO:S |  |  |
| ATTR     | AN_ESPECE             | AN_IDENTIFICATION | espèce         | N | N          | docid('ZOO_ESPECE') | 130 | W   | Y    |                                                                              |         |                                       |            |                                  | creation={es_nom:CT}                     | doctitle=an_espece_title       |  |  |
| ATTR     | AN_ESPECE_TITLE       | AN_IDENTIFICATION | espèce (titre) | Y | N          | text                | 140 | H   |      |                                                                              |         | ::getTitle(an_espece)                 |            |                                  |                                          |                                |  |  |
| ATTR     | AN_ORDRE              | AN_IDENTIFICATION | ordre          | N | N          | text                | 150 | R   |      |                                                                              |         | ::getdocvalue(an_espece,es_ordre)     |            |                                  |                                          |                                |  |  |
| ATTR     | AN_CLASSE             | AN_IDENTIFICATION | classe         | N | N          | docid("ZOO_CLASSE") | 160 | R   |      |                                                                              |         | ::getdocvalue( an_espece , es_classe) |            |                                  | doctitle=auto                            |                                |  |  |
| ATTR     | AN_SEXE               | AN_IDENTIFICATION | sexe           | N | N          | enum                | 170 | W   |      |                                                                              |         | M                                     | Masculin,F | Féminin,H                        | Hermaphrodite                            |                                |  |  |
| ATTR     | AN_PHOTO              | AN_IDENTIFICATION | photo          | N | N          | image               | 180 | W   |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| ATTR     | AN_NAISSANCE          | AN_IDENTIFICATION | date naissance | N | N          | date                | 190 | W   |      |                                                                              |         |                                       |            | ::validatePastDate(AN_NAISSANCE) |                                          |                                |  |  |
| ATTR     | AN_ENTREE             | AN_IDENTIFICATION | date entree    | N | N          | date                | 200 | W   |      |                                                                              |         |                                       |            | ::validatePastDate(AN_ENTREE)    |                                          |                                |  |  |
| ATTR     | AN_ENFANT_T           | AN_IDENTIFICATION | liste enfant   | N | N          | array               | 210 | W   |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| ATTR     | AN_ENFANT             | AN_ENFANT_T       | enfant         | N | N          | docid("ZOO_ANIMAL") | 220 | W   |      |                                                                              |         |                                       |            |                                  | creation={an_nom:CT,an_espece:an_espece} |                                |  |  |
| ATTR     | AN_CARNETSANTE        | AN_IDENTIFICATION | Carnet Santé   | N | N          | menu                | 230 | W   |      | %S%app=GENERIC&action=GENERIC_ISEARCH&id=%I%&famid=ZOO_CARNETSANTE&viewone=Y |         |                                       |            |                                  |                                          |                                |  |  |
| ATTR     | AN_ENCLOS             | AN_IDENTIFICATION | Enclos         | N | N          | menu                | 240 | W   |      | %S%app=GENERIC&action=GENERIC_ISEARCH&id=%I%&famid=ZOO_ENCLOS&viewone=Y      |         |                                       |            |                                  |                                          |                                |  |  |
| ATTR     | AN_PARENT             | AN_IDENTIFICATION | Parents        | N | N          | menu                | 250 | W   |      | %S%app=GENERIC&action=GENERIC_ISEARCH&generic=Y&id=%I%&famid=ZOO_ANIMAL      |         |                                       |            |                                  |                                          |                                |  |  |
| ATTR     | AN_PERE               | AN_IDENTIFICATION | pere           | N | Y          | docid('ZOO_ANIMAL') | 260 | R   |      |                                                                              |         | ::getAscendant(M)                     |            |                                  | doctitle=auto                            |                                |  |  |
| ATTR     | AN_MERE               | AN_IDENTIFICATION | mere           | N | Y          | docid('ZOO_ANIMAL') | 270 | R   |      |                                                                              |         | ::getAscendant(F)                     |            |                                  | doctitle=auto                            |                                |  |  |
| ATTR     | AN_FOLDER             |                   | Dossier        | N | N          | menu                | 10  | W   |      | %S%app=ZOO&action=ZOO_ANIMALFOLDER&id=%I%                                    |         |                                       |            |                                  |                                          |                                |  |  |
|          |                       |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |
| END      |                       |                   |                |   |            |                     |     |     |      |                                                                              |         |                                       |            |                                  |                                          |                                |  |  |


La définition d'une famille commence toujours par une ligne de la forme :

    BEGIN;[fromid];[title];[id];[className];[logicalName]

et se termine toujours par une ligne de la forme :

    END;

avec les correspondances suivantes:

BEGIN
:   Obligatoire, signale le début d'une définition de famille.

[fromid]
:   Identifiant logique (nom logique ou identifiant interne numérique) de la
 famille de laquelle cette famille hérite.
    
    Laisser vide s'il n'y a pas d'héritage.
    
    L'utilisation d'un identifiant interne numérique à la place d'un nom
    logique est à réserver aux familles de core.

[title]
:   Titre de la famille.
    
    Ce titre est utilisé sur les IHM pour désigner la famille.
    
    Il est automatiquement ajouté au catalogue de traduction, et peut ainsi 
    être traduit.

[id]
:   Identifiant numérique de la famille.
    
    Laisser vide pour utiliser un identifiant logique
    (Dans ce cas, Dynacase affectera automatiquement un identifiant interne
     unique à la famille).
    
    S'il est renseigné, il faut que cet identifiant ne soit pas déjà pris par
     un autre document.
    
    Les valeurs entre 900 et 999 peuvent être utilisée pour vos besoins
    spécifiques, bien que l'usage de valeurs numériques fixes soit fortement
    déconseillée.

[className]
:   Nom de la classe PHP de cette famille.
    
    Cette classe doit être présente sur le serveur dans un fichier appelé
    `/FDL/Class.[CLASSNAME].php`.
    
    Le laisser à vide pour que Dynacase génère la classe automatiquement.
    
    Permet un héritage autre que celui prévu par défaut par les classes
    documentaire.

[logicalName]
:   Nom logique de la famille.
    
    Doit commencer par une lettre.
    Il ne peut ensuite contenir que des caractères alphanumériques ainsi
    que les caractères _ et - (pas d'espace, ni de ponctuation).

END
:   Obligatoire, signale la fin d'une définition de famille.

Entre ces 2 lignes, chacune des lignes correspond à :

*   un [paramètre de propriété](#core-ref:40d229c4-33c4-11e2-9147-a3eaf356c37c),
*   une [propriété de famille](#core-ref:6f013eb8-33c7-11e2-be43-373b9514dea3),
*   un [attribut](#core-ref:bc3fad86-33cc-11e2-9a69-1bbd9c32b0f2),
*   un [paramètre de famille](#core-ref:c28824e2-3486-11e2-be3b-337d2321d8ee),
*   une [valeur par défaut](#core-ref:94fa51e2-3488-11e2-9e34-1f7c912168cf),
*   une [valeur initiale de paramètre](#core-ref:da804e2e-3573-11e2-8974-4ba96567fbf9),
*   une [modification d'attribut père](#core-ref:13dcd96d-561f-463c-a88f-4b9db58e4fbd),
*   une [instruction de réinitialisation](#core-ref:5c661733-772d-42b8-8b3e-b70453ddfd33),
*   un commentaire.
    
    Une ligne qui ne sera pas traitée lors du traitement de la définition de famille.
    
    Un commentaire commence toujours par `//`. Par exemple : `// Ceci est un commentaire;;;;;;;;;;;;;;;;`

### Définition de paramètres de propriété {#core-ref:40d229c4-33c4-11e2-9147-a3eaf356c37c}

Des paramètres permettent de modifier le comportement des propriétés du document.

Leur syntaxe est toujours de la forme `PROP;[propid];[param]`,
avec les correspondances suivantes :

[propid]
:   Nom de la propriété.

[param]
:   Définition du paramètre, sous la forme `[parameterName]=[parameterValue]`.

Par exemple :

    PROP;title;sort=asc

Les paramètres de propriété disponibles sont :

sort
:   Permet de spécifier si la propriété est disponible dans les recherches
    et les rapports, et quel est son ordre de tri par défaut.
    
    Les valeurs possibles sont :
    
    *   `no` : la propriété n'apparaîtra pas dans les recherches et rapports ;
    *   `asc` : la propriété est disponible dans les recherches et les rapports ;
        et est trié par défaut par ordre ascendant ;
    *   `desc` : la propriété est disponible dans les recherches et les rapports ;
        et est trié par défaut par ordre descendant.
    
    Les propriétés suivantes ont un paramètre *sort* par défaut :
    
    *   initid : sort=desc,
    *   revdate : sort=desc,
    *   state : sort=asc,
    *   title : sort=asc
    
    Les autres propriétés sont par défaut à *sort=no*.

### Définition de propriétés de famille {#core-ref:6f013eb8-33c7-11e2-be43-373b9514dea3}

Les propriétés de famille permettent, selon les cas,
de définir un comportement particulier pour la famille,
ou de définir les valeurs par défaut des propriétés
des nouveaux documents de cette famille.

Leur syntaxe est toujours de la forme `[propid];[value]`, avec les
correspondances suivantes :

[propid]
:   Identifiant de la propriété.

[value]
:   Valeur de la propriété.

Les différents identifiants de propriété sont les suivants :

CPROFID
:   Indique le *profil* utilisé pour les documents créé avec cette famille.
    Affecte la valeur de la propriété `profid` pour les nouveaux documents de
    cette famille.  
    Contient l'identifiant d'un document profil.
    
    Lors de l'importation, les vérifications suivantes sont effectuées :
    
    *   Si la famille hérite de dossier,
        le profil référencé doit être de la famille profil de dossier ;
    *   Si la famille hérite de recherche,
        le profil référencé doit être de la famille profil de recherche, ;
    *   Sinon le profil référencé doit être de la famille profil de document.
    
    Si la valeur est vide le profil de document par défaut est enlevé.

    **Note** : Cette propriété ne modifie pas les profils des documents de cette
    famille qui sont déjà créés au moment de la mise à jour de la famille.

CVID
:   Indique le *contrôle de vue* qui sera associé aux documents crééx avec cette
    famille. Affecte la valeur de la propriété `cvid` pour les nouveaux
    documents de cette famille.  
    Contient l'identifiant d'un document *contrôle de vue*. 
    
    Lors de l'importation, les vérifications suivantes sont effectuées :
    
    *   Ce document doit être de la famille *contrôle de vue*.
    *   Ce contrôle de vue doit être applicable à la famille en cours.
    
    Si la valeur est vide le contrôle de vue par défaut est enlevé.

    **Note** : Cette propriété ne modifie pas les contrôles de vue des 
    documents de cette famille qui sont déjà créés au moment de 
    la mise à jour de la famille.  

DFLDID
:   Identifiant du dossier principal permettant de constituer une arborescence
    spécifique à la famille .
    
    Ce dossier est nécessaire pour manipuler les documents d'une famille 
    depuis l'application "ONEFAM".
    Il peut être égal à `auto`, ce qui a pour effet de créer un dossier
    principal automatiquement. 
    Ce dossier aura les restrictions indiquant que seuls des documents de 
    cette famille et des dossiers pourront être insérés dans ce dossier 
    principal.
    
    Si cette propriété est déjà renseignée, deux cas de figure se présentent :
    
    *   La nouvelle valeur est 'auto' : Dans ce cas, l'ancienne valeur est
        conservée
    *   La nouvelle valeur n'est pas 'auto' : la nouvelle valeur est utilisée.
    
    Si la valeur est vide le dossier principal par défaut est enlevé.

ICON
:   Nom du fichier image définissant l'icône de la famille.
    
    Cette icône doit être une image carré. 
    La taille conseillée varie de 48 à 128 pixels. 
    Le format d'image conseillé est `png`. 
    Les formats d'images supportés sont `png` et `gif`.
    
    Si cette propriété est déjà renseignée, la nouvelle valeur ne sera pas
    prise en compte.
    
    Si la famille n'a pas encore d'icône, alors la nouvelle valeur est prise en
    compte.

METHOD
:   Indique le nom du fichier PHP contenant les méthodes supplémentaires de la
    famille.
    
    Le fichier référencé doit être disponible dans le répertoire *FDL*. 

    **Note** : Le nom du fichier doit être unique parmi tous les fichiers
    présents dans le répertoire `FDL`. Il est fortement conseillé d'indiquer
    l'identifiant de la famille dans le nom de fichier
    (par exemple : `Method.MyFamily.php` où `MYFAMILY` est l'identifiant de la
    famille).
    
    Cette propriété peut être utilisé plusieurs fois, avec la sémantique
    suivante :
    
    *   Lorsque le nom est préfixé par `+`,
        son contenu est concaténé directement dans la classe générée ;
    *   Lorsque le nom est préfixé par `*`,
        le fichier n'est pas intégré directement dans la famille ,
        mais une classe intermédiaire est générée.
        Cela permet notamment une surcharge plus fine des méthodes.
    
    Si la valeur est vide, *toutes* les méthodes associées seront enlevées (y
    compris celles déclarées avec `*` ou `+`).

PROFID
:   Identifiant (nom logique ou identifiant interne) du document profil de
 famille pour cette  famille.
    
    Lors de l'importation, les vérifications suivantes sont effectuées :
    
    *   Ce document doit être de la famille 'profil de famille'.
    
    Si la valeur est vide le profil de famille est enlevé.

SCHAR
:   Indique les modalités de révision des documents de cette famille :
    
    *   *R* : Révision automatique à chaque modification,
    *   *S* : document non révisable
    
    Si la valeur est vide la caractéristique spéciale par défaut est enlevée.

TAG
:   Initialise les valeurs de la propriété *atags*.
    
    Chaque utilisation de la balise TAG ajoutera une valeur à la propriété
    *atags*.
    
    **Note** : Les tags applicatifs ne peuvent être supprimés par cette
    directive.
    
    Certains tags sont déjà prédéfinis par Dynacase :
    
    MAILRECIPIENT
    :   Déclare la famille comme *destinataire de mail*.
        Cela permet aux documents de cette famille d'être présentés dans la
        liste de destinataires lors des envois de mail.
        
        La famille doit alors implémenter l'interface `IMailRecipient`.
        <span class="fixme" data-assignedto="nobody">ajout d'un lien vers l'interface</span>

TYPE
:   Valeur par défaut de la propriété *type*.
    
    Si la valeur est vide, le type inféré est *C*.

USEFOR
:   Caractère désignant une utilisation spéciale. Seulement pour les documents
    systèmes :
    
    *   *W* : pour les cycles de vie
    *   *G* : pour les intercalaires de chemise
    *   *P* : pour les profils
    
    Si la valeur est vide l'utilisation spéciale par défaut est enlevée.

WID
:   Indique le cycle de vie qui sera associé pour les documents créé avec 
cette famille. 
Affecte la valeur de la propriété `wid` pour les nouveaux documents de cette 
 famille. Contient l'identifiant d'un document *cycle de vie*. 
    
    Lors de l'importation, les vérifications suivantes sont effectuées :
    
    *   Ce document doit être un document [cycle de vie][workflow] ;
    *   Le cycle de vie doit être applicable à la famille en cours.
    
    Si la valeur est vide le cycle par défaut est enlevé.

### Définition d'attributs {#core-ref:bc3fad86-33cc-11e2-9a69-1bbd9c32b0f2}

Un attribut est défini par la syntaxe suivante :

    ATTR;[id_attribut];[id_conteneur];[label];[in_title];[in_abstract];[type];[ordre];[visibility];[required];[link];[phpfile];[phpfunc];[elink];[constraint];[options]

avec les correspondances suivantes :

ATTR
:   **Obligatoire**  
    Signale que la ligne est une définition d'attribut.

[id_attribut]
:   **Obligatoire**  
    Identifiant système de l'attribut.
    
    Il sera automatiquement converti en minuscules.
    
    Cet item n'est plus modifiable une fois créé car il peut être utilisé dans
    les parties spécifiques de la famille.
    
    Cet identificateur doit être unique dans la famille.
    
    Il est conseillé d'adopter des règles de nommage des attributs, permettant
    de simplifier leur manipulation.
    Par exemple : `[FAM]_[TYPE]_[NAME]` avec :
    
    *   [FAM] : un préfixe indiquant la famille,
    *   [TYPE] : une lettre indiquant le type de l'attribut,
    *   [NAME] : le nom de l'attribut.

[id_conteneur]
:   **Obligatoire** (sauf pour les attributs de type *frame* ou *tab*)  
    Identifiant système de l'attribut structurant ou tableau contenant cet
    attribut.
    
    Le type *tab* ne peut pas avoir d'attribut conteneur.
    
    Le type *frame* peut être contenu dans un *tab*, ou ne pas avoir d'attribut
    conteneur.
    
    Le type *array* doit être contenu dans un *frame*.
    
    Tous les autres type d'attributs doivent être contenus dans 
    un *array* ou un  *frame*.

[label]
:   **facultatif**  
    Libellé de l'attribut.
    
    Ce libellé sera automatiquement traduit s'il est présent dans le catalogue
    de traduction (la clé correspondante est de la forme `[FAMNAME]#[attrid]`,
    avec [FAMNAME] le nom logique de la famille et
    [attrid] l'identifiant de l'attribut, en minuscule).

[in_title]
:   **Obligatoire** (sauf pour les attributs de type *array*, *frame* ou *tab*)  
    Indique que l'attribut sera utilisé dans la composition du titre du document.
    
    Le titre du document est alors composé en concaténant tous les attributs
    définis comme tels, par ordre croissant de leur *ordre* et en les séparant
    par des espaces.
    
    Cette caractéristique est ignorée sur les attributs de type 
    *array*, *frame* ou *tab*.
    
    Si aucun attribut n'est marqué comme composant le titre, ou si tous ces
    attributs sont vides, le titre sera *Document sans titre* suivi de 
    l'identifiant interne du document.
    
    Les valeurs possibles sont :
    
    *   `Y` pour *yes*
    *   `N` pour *no*

[in_abstract]
:   **Obligatoire** (sauf pour les attributs de type 
    *array*, *frame* ou *tab*)  
    Indique que l'attribut sera utilisé dans le résumé du document.
    
    Le résumé du document est utilisé pour construire la fiche résumé dans
    l'application ONEFAM.
    
    Les valeurs possibles sont :
    
    *   `Y` pour *yes*
    *   `N` pour *no*

[type]
:   **Obligatoire** (sauf pour les attributs de type *array*, *frame* ou *tab*)  
    Indique le type de l'attribut.
    Les types d'attributs supportés sont définis au chapitre [Type de l'attribut][type_attribut].
    
    Cette colonne permet également de définir le formatage de l'attribut :
    
    *   attributs de type *text*
        
        Le formatage est effectué avec la [syntaxe sprintf][PHP_sprintf].
        
        Par exemple, `text("%s environ")` ajoute *environ* après la valeur ;
        tandis que `text("<b>%s</b>")` affichera la valeur en gras.
    
    *   attributs de type *int* ou *double*
        
        Le formatage est effectué avec la [syntaxe sprintf][PHP_sprintf].
        
        Par exemple, `double("%.02f")` affiche le nombre avec 2 décimales ;
        tandis que `integer("%d m³")` : la valeur suivie de *m³* ;
        et que `double("%.02f %%")` : affiche *%* après le nombre.
    
    *   attributs de type *date*, *time* et *timestamp*
        
        Le formatage est effectué avec la syntaxe [strftime][PHP_strftime].
        
        Par exemple, `time("%H:%M:%S")`, ou `timestamp("%A %d %B %Y %X")`.


[ordre]
:   **Obligatoire** (sauf pour les attributs de type *frame* ou *tab*)  
    Définit l'ordre de présentation des attributs dans le document.
     L'ordre est un nombre entier.
    
    **Note**: Les tableaux (type `array`) doivent toujours avoir un ordre
    inférieur aux attributs qui le composent.
    
    Cette caractéristique est ignorée sur les attributs de type *frame* ou *tab*.

[visibility]
:   **Obligatoire**  
    Définit la visibilité par défaut de l'attribut dans les interfaces web de
    consultation et de modification du document.
    
    Les valeurs possibles sont :
    
    *   `H` (*Hidden*) : attribut caché.
        Généralement utilisé pour des attributs servant soit au calcul, soit à
        la génération des liens.
    *   `I` (*Invisible*) : attribut invisible :
        l’attribut n’est présent ni en consultation ni en modification dans le
        document.  
        Un attribut de visibilité I n'est pas modifiable et pour en modifier la
        valeur, il est nécessaire de modifier sa visibilité.
    *   `O` :
        attribut modifiable en modification mais non visible en lecture.
    *   `R` (*Read-only*) : attribut visible en lecture seulement.
        Généralement utilisé pour les attributs calculés.
    *   `S` (*Statique*) : attribut visible en lecture et en modification, mais
        non modifiable en modification.
    *   `W` (*Writable*) : attribut visible en lecture et modifiable en
        modification.
    
    Le type `array` dispose en plus de la visibilité
    
    *   `U` : Interdit l'ajout et la suppression de lignes dans le tableau.

    Cette caractéristique peut être modifiée par les [masques][masque] 
    des [contrôle de vues][control_de_vue].

[required]
:   **facultatif**  
    Indique si l'attribut est obligatoire pour la sauvegarde du document 
    depuis l'interface web de modification du document. 
    Cette caractéristique n'est pas prise en compte lors des sauvegardes faite
     par le code (méthode `Doc::store()`) ni lors de l'importation de document.
    Par contre, cette caractéristique est prise en compte lors d'un passage de
     transition (document lié par un cycle de vie -_workflow_-).  
    Cette caractéristique peut être modifiée par les [masques][masque] 
    des [contrôle de vues][control_de_vue].
    
    Les valeurs possibles sont :
    
    *   `Y` pour *yes*
    *   **`N` (valeur par défaut)** pour *no*

[link]
:   **facultatif** (Non applicable pour les types "frame", "tab", "array")  
    Ajoute un hyperlien sur l'attribut sur les interfaces web de consultation des documents.
    
    Par défaut, le texte de l'hyperlien est la valeur de l'attribut. L'option
    `ltarget` permet de changer ce texte.
    
    L'hyperlien peut être :
    
    *   une URL statique ("http://www.dynacase.org"),
    *   une URL paramétrée par
        *   des attributs du document,
        *   des propriétés du document,
        *   des paramètres applicatifs,
       *   des méthodes du document.
    
    *   Utilisation d'attribut du document
        
        Les références aux attributs du document sont écrites entre les
        caractères `%`, en indiquant l'identifiant de l'attribut, en majuscules
        ou en minuscules.
        
        Le caractère `%` est obtenu en le doublant : `TEST%%25` sera converti en
        *TEST%25*.
        
        Par exemple, soit l'attribut US_MAIL définissant le mail d'une personne.
        Pour déclencher l'édition d'un mail vers une personne,
        il suffit de mettre l'hyperlien suivant : `mailto:%US_MAIL%`.
        
        Autre exemple, soit l'attribut SI_TOWN indiquant la ville de la famille
        société.  Pour avoir la météo de la ville 
        il suffit de mettre l'hyperlien suivant :
        `http://www.location.org/&strLocation=%SI_TOWN%&strCountry=EUR`.
        
        Si la valeur est vide pour un des attributs de l'URL,
        l'hyperlien ne sera pas affiché (on ne pourra pas cliquer sur
        l'attribut).
        
        Il est possible de désigner des attributs optionnels en utilisant la
        notation suivante : `%?[ATTRID]%`.
        Le point d'interrogation placé après le pourcentage indique que la
        valeur de l'attribut peut être vide.
        
        Les valeurs insérées dans le lien sont encodés selon la
        [RFC 3986][RFC_3986] pour être utilisable comme valeur de paramètre web.
    
    *   Utilisation de propriétés du document
        
        Les références aux propriétés du document sont écrites entre les
        caractères `%`, en indiquant l'identifiant de l'attribut, en majuscules
        ou en minuscules.
        
        Le caractère `%` est obtenu en le doublant : `TEST%%25` sera converti en
        *TEST%25*.
        
        Les mots-clefs spéciaux suivants peuvent être utilisés pour la
        composition de l'URL :
        
        *   `%S%` : est remplacé par l'URL relative vers dynacase,
        *   `%I%` : est remplacé par l'identifiant (équivalent à %ID%),
        *   `%T%` : est remplacé par le titre (équivalent à %TITLE%).
        
        Les valeurs insérées dans le lien sont encodés selon la
        [RFC 3986][RFC_3986] pour être utilisable comme valeur de paramètre web.
    
    *   Utilisation de paramètres applicatifs
        
        Les références aux paramètres applicatifs sont écrites entre accolades,
        en indiquant l'identifiant de l'attribut, en majuscules ou en
        minuscules.
        
        Par exemple : `%S%app=TEST&action=TESTONE&arg={CORE_CLIENT}` :
        ici {CORE_CLIENT} sera remplacé par la valeur du paramètre CORE_CLIENT.
        
        Seuls les paramètres de *CORE* et les *paramètres globaux* sont
        accessibles pour la composition de l'URL.
    
    *   Utilisation de méthodes du document
        
        Les références aux méthodes du document sont écrites entre caractères `%`,
        en notant la méthode comme pour les attributs calculés.
        
        Les parties variables peuvent aussi faire référence à une méthode du
        document.
        Cette méthode doit retourner une chaîne de caractère encodée selon la
        [RFC 3986][RFC_3986] qui sera insérée dans la variable.
        
        Par exemple : `%::myTitleLink()%&x=3`
        
            [php]
            public function myTitleLink(){
                return sprintf('http://www.test.net/?b=%s',
                    rawurlencode($this->getTitle())
                );
            }

[phpfile]
:   **Facultatif** (Non applicable pour les types "frame", "tab", "array")  
    Nom du fichier php pour l'[aide à la saisie][aide_saisie].
    Ce fichier doit être présent dans le répertoire `EXTERNALS`.

[phpfunc]
:   **Facultatif** (Non applicable pour les types "frame", "tab", "array") 
    Cette caractéristique est utilisée pour trois usages différents : 

    1. Nom et attributs de la fonction pour l'[aide à la saisie][aide_saisie]. 
    Cela nécessite que `phpfile` soit défini.
    1. Nom et attributs de la méthode de calcul s'il s'agit d'un 
    [attribut calculé][attribut_calcule]. 
    Dans ce cas `phpfile` doit être vide.
    1. Définition des clés-valeurs dans le cas d'un attribut de type énuméré.
    Le type de l'attribut est `enum`. Les aides à la saisie ne sont pas 
    autorisé pour les attributs de type `enum`.

[elink]
:   **facultatif** (Non applicable pour les types "frame", "tab", "array")  
    Extra lien supplémentaire.
    
    Cet extra lien sera présenté dans les interfaces web de modification de
    document, sous la forme d'un bouton supplémentaire.
    
    La syntaxe de l'extra lien est la même que celle de la colonne *link*.

[constraint]
:   **facultatif** (Non applicable pour les types "frame", "tab", "array")  
    Nom et attributs de la méthode de [contrainte][contrainte].

[options]
:   **facultatif**  
    Liste des options à appliquer à l'attribut. Les options dépendent du [type d'attribut][type_attribut].
    
    Les options se présentent sous la forme de couples `clé=valeur` séparés par des `|`.
    
    Par exemple: `esize=3|elabel=saisissez votre prénom`

### Définition de paramètres de famille {#core-ref:c28824e2-3486-11e2-be3b-337d2321d8ee}

Un [paramètre de famille][family_param] est défini par la syntaxe suivante :

    PARAM;[id_attribut];[id_conteneur];[label];[in_title];[in_abstract];[type];[ordre];[visibility];[required];[link];[phpfile];[phpfunc];[elink];[constraint];[options]

avec les mêmes correspondances que pour [les attributs][attributs],
aux exceptions suivantes :

*   Pour les paramètres calculés, le calcul est fait lors de l'accès au
    paramètre.
*   Les méthodes de calcul et de contrainte doivent être statiques (elles sont
    spécifiées par la syntaxe `class::method`).

### Définition de valeurs par défaut {#core-ref:94fa51e2-3488-11e2-9e34-1f7c912168cf}

Les valeurs par défaut s'appliquent aux attributs comme aux paramètres.

Appliquées aux attributs, elles déterminent la valeur de l'attribut lors de la
création d'un nouveau document, alors qu'appliquées aux paramètres,
elles déterminent la valeur du paramètre lorsque l'utilisateur n'a saisi aucune
valeur.

Une valeur par défaut est définie par la syntaxe suivante :

    DEFAULT;[attrid|paramid];[value];force=yes

avec les correspondances suivantes :

DEFAULT
:   **Obligatoire**  
    Signale que la ligne est une définition de valeur par défaut.

[attrid|paramid]
:   **Obligatoire**  
    Identifiant de l'attribut ou du paramètre auquel s'applique la valeur par
    défaut.

[value]
:   La valeur par défaut, statique, ou la méthode de calcul.
    
    Dans le cas d'une méthode de calcul, sa syntaxe est identique à celle d'un
    [attribut calculé][attribut_calcule].
    
    Par exemple, `DEFAULT;SGATE_RED;::getTitle(SGATE_IDRED)`
    pré-remplit l'attribut  avec le titre de l'attribut *SGATE_IDRED*,
    alors que `DEFAULT;SGATE_ACTION;GATE_WEATHER`
    pré-remplit l'attribut SGATE_RED avec la chaîne *GATE_WEATHER*.
    
    Cas particulier des *array*:
    
    *   Pour définir quelles lignes seront présentes par défaut dans le tableau,
        on spécifie la valeur par défaut de l'attribut *array*.
        
        Cette valeur par défaut est une structure JSON sous la forme d'un
        tableau d'objets.
        
        Par exemple,
        `DEFAULT;ATTR_ARRAY;[{"c1":"1.1", "c2":"1.2"},{"c1":"2.1", "c2":"2.2"}]`
        indique que le tableau *ATTR_ARRAY* sera pré-rempli avec 2 lignes.
        
        *   La première ligne aura comme valeurs
            *   *1.1* dans la colonne correspondant à l'attribut *c1*
            *   *1.2* dans la colonne correspondant à l'attribut *c2*
        *   La seconde ligne aura comme valeurs
            *   *2.1* dans la colonne correspondant à l'attribut *c1*
            *   *2.2* dans la colonne correspondant à l'attribut *c2*
        
        Si l'on souhaite utiliser une méthode de calcul pour cette valeur par
        défaut, la méthode doit retourner le tableau à 2 dimensions qui, une
        fois json_encodé, donne la structure précédente.
        
        Par exemple, la méthode correspondant à la valeur par défaut précédente
        sera `DEFAULT;ATTR_ARRAY;::defaultArrayValue()`.
        
            [php]
            public function defaultArrayValue(){
                return array(
                    array(
                        "c1" => "1.1",
                        "c2" => "1.2"
                    ),
                    array(
                        "c1" => "2.1",
                        "c2" => "2.2"
                    )
                );
            }
    
    *   Pour définir les valeurs par défaut de chaque cellule lors de
        l'ajout d'une nouvelle ligne, on spécifie la valeur par défaut de 
        l'attribut correspondant à cette colonne.  
        De fait, la valeur par défaut d'un attribut contenu dans un *array* doit
        être simple.

[force=yes]
:   **facultatif** Indique, lors de la surcharge de valeur par défaut, que la
    nouvelle valeur par défaut écrase l'ancienne.
    
    Dans le cas contraire, la nouvelle valeur par défaut n'est pas prise en
    compte lors des mises à jours.

    Les valeurs par défaut peuvent être réinitialisées avec la clef
     [`RESET default`][reset].

### Définition de valeur initiale de paramètre {#core-ref:da804e2e-3573-11e2-8974-4ba96567fbf9}

Les paramètres de familles peuvent avoir des valeurs par défaut,
utilisées lorsque ces paramètres n'ont pas de valeur explicite ;
mais il est parfois nécessaire de définir la valeur initiale du paramètre en
plus de sa valeur par défaut.

Une valeur initiale de paramètre est définie par la syntaxe suivante :

    INITIAL;[paramid];[value];force=yes

avec les correspondances suivantes :

INITIAL
:   **Obligatoire**  
    Signale que la ligne est une définition de valeur initiale de paramètre.

[paramid]
:   **Obligatoire**  
    identifiant du paramètre auquel s'applique la valeur initiale.

[value]
:   la valeur initiale, statique, ou la méthode de calcul.
    
    Dans le cas d'une méthode de calcul, sa syntaxe est identique à celle d'un
    [attribut calculé][attribut_calcule].

[force=yes]
:   Indique, lors de la surcharge de valeur initiale, que la nouvelle valeur
    initiale écrase l'ancienne.
    
    Dans le cas contraire, la nouvelle valeur initiale n'est pas prise en compte.
    Les valeurs initiales peuvent être réinitialisées avec la clef
     [`RESET parameters`][reset].

### Modification d'attribut père {#core-ref:13dcd96d-561f-463c-a88f-4b9db58e4fbd}

Lorsqu'une famille étend une autre famille, il peut être nécessaire de changer
la définition d'un attribut. Cela se fait au moyen d'une ligne de la forme :

    MODATTR;[id_attribut];[id_conteneur];[label];[in_title];[in_abstract];[type];[ordre];[visibility];[required];[link];[phpfile];[phpfunc];[elink];[constraint];[options]

avec les même correspondances que pour la
[définition d'un attribut][definition_attribut], à quelques différences près :

MODATTR
:   **Obligatoire**  
    Signale que la ligne est une modification d'attribut.

[id_attribut]
:   **Obligatoire**  
    Identifiant système de l'attribut à surcharger.
    Il sera automatiquement converti en minuscules.
    
    L'attribut référencé doit obligatoirement exister dans la famille étendue.

[id_conteneur]
:   Identifiant système de l'attribut structurant ou tableau contenant cet
    attribut.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.

[label]
:   Libellé de l'attribut.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.

[in_title]
:   Indique que l'attribut sera utilisé dans la composition du titre du document.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.

[in_abstract]
:   Indique que l'attribut sera utilisé dans le résumé du document.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.

[type]
:   [type de l'attribut][type_attribut]
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.
    
    Le nouveau type d'attribut doit être compatible avec l'ancien
    (son stockage en base de données doit être de même type).

[ordre]
:   Définit l'ordre de présentation des attributs dans le document.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.

[visibility]
:   Définit la visibilité par défaut de l'attribut.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.


[required]
:   Indique si l'attribut est obligatoire pour la sauvegarde du document.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.

[link]
:   Ajoute un hyperlien sur l'attribut (en consultation uniquement).
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.
    
    Pour supprimer l'hyperlien, il faut mettre la valeur `-`.

[phpfile]
:   Nom du fichier php pour l'[aide à la saisie][aide_saisie].
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.
    
    Pour supprimer l'hyperlien, il faut mettre la valeur `-`.

[phpfunc]
:   Nom et attributs de la fonction pour l'aide à la saisie,
    ou nom et attributs de la méthode de calcul s'il s'agit d'un attribut
    calculé, ou définition des clés-valeurs dans le cas d'un attribut de type
    énuméré.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.
    
    Pour supprimer l'hyperlien, il faut mettre la valeur `-`.

[elink]
:   Extra lien supplémentaire.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.
    
    Pour supprimer l'hyperlien, il faut mettre la valeur `-`.

[constraint]
:   Nom et attributs de la méthode de [contrainte][contrainte].
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.
    
    Pour supprimer l'hyperlien, il faut mettre la valeur `-`.

[options]
:   Liste des options à appliquer à l'attribut.
    
    Si la valeur est vide, l'attribut conservera sa valeur héritée.
    
    Pour supprimer l'hyperlien, il faut mettre la valeur `-`.
    
    Afin de modifier la valeur d'une seule option, il est nécessaire de toutes
    les reporter, car la valeur `-` va effacer entièrement le contenu de la
    colonne *options*.

### Instructions de réinitialisation {#core-ref:5c661733-772d-42b8-8b3e-b70453ddfd33}

Lors de la [surcharge de famille](#core-ref:686b17c3-220e-4450-a0d0-feb5db002cbc),
il est possible de réinitialiser certaines parties de la famille.

La syntaxe est la suivante :

    RESET;[keyword]

avec les correspondantes suivantes :

RESET
:   **Obligatoire**  
    Signale que la ligne est une réinitialisation.

[keyword]
:   **Obligatoire**  
    Indique quels éléments doivent être réinitialisés.
    
    Les valeurs possibles sont :
    
    `attributes`
    :   Réinitialise les attributs.
        
        La définition de tous les attributs sera effacée
        (les valeurs ne sont pas supprimées des documents existants).
        
        **Attention** : la définition des paramètres de la famille est également
        effacée (bien que les valeurs soient également conservées).
    
    `default`
    :   Réinitialise les valeurs par défaut.
        
        Toutes les valeurs par défaut sont effacées.
    
    `properties`
    :   Réinitialise les valeurs des paramètres des propriétés.
        
        Tous les paramètres de propriétés seront remis à leur valeur par défaut.
    
    `parameters`
    :   Réinitialise les valeurs des paramètres de famille
        
        Toutes les valeurs des paramètres de famille sont effacées. Ces 
        paramètres utiliseront les valeurs par défaut si elles sont définies.


Ces instructions de réinitialisation doivent être placées avant la nouvelle
définition des éléments réinitialisés.

Chaque instruction doit être sur sa propre ligne.

## Surcharge de définition de famille {#core-ref:686b17c3-220e-4450-a0d0-feb5db002cbc}

La définition d'une famille peut être surchargée, permettant ainsi une
importation plus modulaire.
Il est bien question ici de la notion de *surcharge* qui change la définition
d'une famille, et à ne pas confondre avec le mécanisme d'héritage, qui crée une
nouvelle famille.

Pour surcharger une définition de famille, il suffit d'utiliser le même nom
logique (sur la ligne *BEGIN*).

Lors de la surcharge, le comportement est le suivant :

*   pour les [paramètres de propriété](#core-ref:40d229c4-33c4-11e2-9147-a3eaf356c37c)
    
    La nouvelle valeur écrase la valeur précédemment définie.

*   pour les [propriétés de famille](#core-ref:6f013eb8-33c7-11e2-be43-373b9514dea3)
    
    La nouvelle valeur écrase la valeur précédemment définie.

*   pour les [attributs](#core-ref:bc3fad86-33cc-11e2-9a69-1bbd9c32b0f2)
    
    La nouvelle valeur écrase la valeur précédemment définie.

*   pour les [paramètres de famille](#core-ref:c28824e2-3486-11e2-be3b-337d2321d8ee)
    
    La nouvelle valeur écrase la valeur précédemment définie.

*   pour les [valeurs par défaut](#core-ref:94fa51e2-3488-11e2-9e34-1f7c912168cf)
    
    La nouvelle valeur écrase la valeur précédemment définie si *force=yes*
     est utilisé.

*   pour les [valeurs initiale de paramètre](#core-ref:da804e2e-3573-11e2-8974-4ba96567fbf9)
    
    La nouvelle valeur écrase la valeur précédemment définie si *force=yes* 
    est utilisé.

Ce comportement peut être altéré par l'utilisation des
[Instructions de réinitialisation][reset].

## Prise en compte d'une définition de famille dans Dynacase {#core-ref:a2a64666-660f-43ca-8edf-943d0037f0df}

Une fois votre définition de famille créée, vous pouvez l'importer dans Dynacase.

Cette importation permettra à Dynacase de créer les tables nécessaires aux
documents de cette famille, et de rendre la dite famille disponible dans les
différentes IHM de Dynacase.

L'importation se fait en ligne de commande, avec la commande suivante :

    ./wsh.php --api=importDocuments --file=[chemin vers le fichier de définition]

<span class="fixme" data-assignedto="nobody">Pour plus de détails sur l'API `importDocuments`, se référer à la documentation correspondante</span>

<!-- links -->
[PHP_sprintf]: http://php.net/manual/fr/function.sprintf.php "Documentation de la fonction sprintf sur php.net"
[PHP_strftime]: http://php.net/manual/fr/function.strftime.php "Documentation de la fonction strftime sur php.net"
[RFC_3986]: http://www.ietf.org/rfc/rfc3986.txt
[attributs]: #core-ref:bc3fad86-33cc-11e2-9a69-1bbd9c32b0f2
[type_attribut]: #core-ref:4e167170-33ed-11e2-8134-a7f43955d6f3
[attribut_calcule]: #core-ref:4565cab9-73c8-4eee-bfa7-218ffbd4b687
[aide_saisie]: #core-ref:0b2d4cd0-4eed-41d8-ac57-37525a444194
[contrainte]: #core-ref:7b41906b-f199-41a4-94df-33b9ad34153b
[definition_attribut]: #core-ref:bc3fad86-33cc-11e2-9a69-1bbd9c32b0f2
[workflow]: #core-ref:55a53d99-0c24-48d8-8cb9-1caa171f2e9a
[family_param]: #core-ref:4595c8e7-5002-4dbc-b6bb-882b4123efd8
[masque]: #core-ref:327ad491-06df-4e5b-b49a-695c75439fe1
[control_de_vue]: #core-ref:017f061a-7c12-42f8-aa9b-276cf706e7e0
[reset]: #core-ref:5c661733-772d-42b8-8b3e-b70453ddfd33