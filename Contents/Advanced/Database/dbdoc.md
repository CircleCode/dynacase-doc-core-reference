# Description des tables de documents {#core-ref:b3ef653f-e8ca-4385-b551-2ead886133e6}

## La table _Doc_ {#core-ref:d4b8d8ce-6f7a-4c1c-a5c4-f1adfcb74864}

Toutes les informations des documents sont enregistrées dans les tables héritées
de la table `doc`.

La table `doc` définie les [propriétés des documents][docprop] ; c'est à dire
tout ce qui est commun à tout type de document.


|   Colonne    |             Type            |                                            Définition                                            |
| ------------ | --------------------------- | ------------------------------------------------------------------------------------------------ |
| adate        | timestamp without time zone | Date de dernier accès au document.                                                               |
| allocated    | integer                     | Identifiant système de l'utilisateur auquel le document est affecté.                             |
| archiveid    | integer                     | Id de l'archive dans laquelle est contenue ce document.                                          |
| atags        | text                        | Balises applicatives                                                                             |
| attrids      | text                        | Liste de l'ensemble des attributs ayant une valeur non nulle (calculé par trigger)               |
| cdate        | timestamp without time zone | Date de création de la révision.                                                                 |
| classname    | character varying(64)       | Nom de la classe PHP associée au document (utilisé dans la table `docfam` uniquement)            |
| comment      | text                        | *Obsolète*                                                                                       |
| confidential | integer                     | Indique si le document est confidentiel (>0)                                                     |
| cvid         | integer                     | Identifiant du document [contrôle de vue][CVDoc] associé à ce document                           |
| doctype      | character(1)                | Type de document.                                                                                |
| domainid     | text                        | *pour application offline*                                                                       |
| dprofid      | integer                     | Identifiant du [profil dynamique][docprofdyn] associé à ce document                              |
| forumid      | integer                     | *Obsolète*                                                                                       |
| fromid       | integer                     | Id de la famille d'appartenance.                                                                 |
| fulltext     | tsvector                    | Ensemble des valeurs du document y compris les textes des fichiers indexés                       |
| id           | integer                     | Identifiant unique du document (issue de la séquence `seq_id_doc`)                               |
| icon         | character varying(256)      | Référence au fichier d'icone du document                                                         |
| initid       | integer                     | Id du premier document de la lignée documentaire                                                 |
| ldapdn       | text                        | *Obsolète*                                                                                       |
| lmodify      | character(1)                | Tag de modification                                                                              |
| lockdomainid | integer                     | *Pour application offline*                                                                       |
| locked       | integer                     | Indique l'identifiant système de l'utilisateur qui a verrouillé le document                      |
| name         | text                        | Nom logique du document.                                                                         |
| owner        | integer                     | Identifiant système de l'utilisateur ayant créé le document                                      |
| postitid     | text                        | Identifiant du document post-it associé                                                          |
| prelid       | integer                     | Identifiant du document (dossier) de relation primaire                                           |
| profid       | integer                     | Identifiant du [profil de document][docprof]                                                     |
| revdate      | integer                     | Date de révision.                                                                                |
| revision     | integer                     | Numéro d'ordre du document dans sa lignée documentaire                                           |
| state        | character varying(64)       | Étape du document                                                                                |
| svalues      | text                        | Liste des valeurs d'[attributs recherchables][attropt] y compris les textes des fichiers indexés |
| title        | character varying(256)      | Titre du document.                                                                               |
| usefor       | text                        | Type d'utilisation du document                                                                   |
| values       | text                        | Liste de l'ensemble des valeurs non nulles en corrélation avec _attrids_                         |
| version      | text                        | Libellé de la version : il est vide par défaut                                                   |
| views        | integer[]                   | Liste des [identifiants de compte][dbuser] qui ont accès au document                             |
| wid          | integer                     | Identifiant du [document *cycle de vie*][WF_document] associé à ce document.                     |


## Les tables des documents {#core-ref:0c6cc474-d5e9-4ee0-aeed-1aa00100d7df}

Pour chacune des familles enregistrées, une table associée est créée. Cette
table  est nommée `doc<famid>` où `<famid>` est l'identifiant numérique de la
famille. Une même famille peut avoir un nom de table différent sur différente
installation suivant l'identifiant qui lui a été attribué au moment de la
création. De même si la famille est [détruite][destroyfam], une nouvelle table
avec un nom différent lui est attribué.

Exemple :
![ Héritage des tables de documents ](advanced/dbinherit.png)

Les tables de documents sont créées avec le schéma _public_. Pour chacune des
familles une vue créée avec le nom logique de la famille est crée en même temps
que la table réelle. Toutes les vues de documents sont créées sous le schéma
_family_.

    [sql]
    select * from public.doc1098;
    -- equivalent à
    select * from family.myfamily;

**Important** : Ces vues ne sont utilisables qu'en lecture seule. À partir de 
postgresql 9.3, ces vues sont utilisables en mise à jour.

Note : Les noms des tables en postgresql ne sont pas sensibles à la casse.

La table `doc` propre ne comprend aucune données.

    [sql]
    db# select count(id) from only doc ;-- aucun document
     count 
    -------
         0
         
    db=# select count(id) from doc ; -- tout les documents
     count 
    -------
     15008

Chacune des tables de documents contient en plus des propriétés héritées de la
table `doc`, une colonne par attributs pouvant contenir une valeur. Cela exclu
les attributs de type _tab_, _frame_, _array_, et _menu_. Le nom de ces colonnes
sont les identifiants des attributs. Le type de ces colonnes est fonction du
[type d'attribut][docattr]. Le type correspondant en base est indiqué dans
chacun des chapitres décrivant les attributs.



## Table de recherche générale {#core-ref:378a7ed5-2703-4167-a980-c84bc29f8c56}

La table `docread` a les mêmes colonnes que la table `doc` mais elle n'en hérite
pas. Cette table contient une réplications de l'ensemble des documents qui sont
disséminés dans l'ensemble des tables `doc<famid>`.

Cette table répliquée a ces propres index globaux qui permets dans le cas d'une
recherche globale, c'est à dire non liée à une famille particulière, d'être plus
optimisée pour donner une réponse rapide.

    [sql]
    db=# select id, title from doc where id=1098;
      id  |           title           
    ------+---------------------------
     1098 | lecteur de Premier espace
    (1 ligne)
    Temps : 24,690 ms
    
    db=# select id, title from docread where id=1098;
      id  |           title           
    ------+---------------------------
     1098 | lecteur de Premier espace
    (1 ligne)
    Temps : 1,037 ms


Cette table doit être utilisée en lecture seule. Seules les tables `doc<famid>`
peuvent être utilisée pour la modification.

## Indexation des fichiers {#core-ref:354273d6-7fab-4096-8f22-6dc3e540ee65}

Si le [moteur de transformation][te] est opérationnel, les contenus des fichiers
peuvent être indexés. Un attribut fichier produit trois colonnes dans la table
associées à sa famille.

1.  colonne `<attrid>`
:   Contient la référence au fichier : `<vaultId>|<mimeType>|<fileName>`.
    
    1. vaultId : Identifiant dans le coffre (table `vaultdiskstorage`, colonne `id_file`),
    1. mimeType : type mime du fichier,
    1. fileName : nom du fichier (basename).
    
1.  colonne `<attrid>_txt`
:   Contient le contenu textuel (type `text`) du fichier qui a été retourné par 
    le moteur de transformation.
    
1.  colonne `<attrid>_vec`
:   Contient le contenu vectorisé (type `tsvector`) de la colonne `<attrid>_txt`.

## Colonne de recherche générale. {#core-ref:d5fc4bc8-067d-4dd8-b617-9641e3b11707}

La colonne `svalues` contient l'ensemble des valeurs recherchables ainsi que les
contenus des colonnes `_txt` des attributs fichiers. Cette colonne est utilisée
pour les [recherches générales][globsearch] utilisant des expressions (partie de
mot).


La colonne `fulltext` contient la version vectorisée de `svalues`.
Cette colonne est utilisée pour les recherches globales de mot entier.

Ces deux colonnes sont calculées par trigger. Toutes modifications
d'enregistrement sur les tables documentaires déclenchent le recalcul de ces
colonnes.

<!-- links -->
[docprop]:          #core-ref:9aa8edfa-2f2a-11e2-aaec-838a12b40353 "Propriétés de la classe Doc" 
[docrevise]:        #core-ref:882e3730-0483-4dbc-9b9d-0d0b5cc31d38
[docgetprop]:       #core-ref:80e3ca49-26ea-4090-9fcd-7b92bf9d5c6d
[CVDoc]:            #core-ref:017f061a-7c12-42f8-aa9b-276cf706e7e0
[profil_dynamique]: #core-ref:bc24834a-b380-4681-ae94-08b93076a7e8
[wsh_cleanContext]: #core-ref:100b123b-da1a-45b4-848b-0622f3e09a40
[WF_document]:      #core-ref:b541e22f-5ece-4d19-8460-0cb0c5f3ec7a
[docprof]:          #core-ref:f1575705-10e8-4bf2-83b3-4c0b5bfb77cf
[docprofdyn]:       #core-ref:bc24834a-b380-4681-ae94-08b93076a7e8
[attropt]:          #core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496 "option searchcriteria"
[destroyfam]:       #core-ref:534bf934-5a2f-4160-8912-567d8f933ddb "wsh destroyFamily"
[docattr]:          #core-ref:4e167170-33ed-11e2-8134-a7f43955d6f3 "Description des types d'attribut"
[te]:               https://docs.anakeen.com/dynacase/3.2/dynacase-doc-tengine-installation-operating/website/book/index.html "Manuel d'installation"
[globsearch]:       #core-ref:19b9f4b4-c960-46eb-b4e0-805ed76be3a6
[dbuser]:           #core-ref:6d5684f4-73e8-431c-8b2b-6224a9e6b074 "table users"