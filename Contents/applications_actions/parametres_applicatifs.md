# Les paramètres applicatifs {#core-ref:c3d9cb18-16d0-435a-b8c2-5fa6ac06c522}
 
## CORE - Noyau

`CORE_URLINDEX`
:   Url d'accès à l'index de dynacase.
    
    Type : `G`
    
    Défaut : &lt;vide&gt;
    
    Exemple : `http://www.example.net/dynacase/`

`CORE_MAILACTION`
:   Url d'accès à dynacase pour les liens des mails envoyés par dynacase.
    
    Type : `G`
    
    Défaut : &lt;vide&gt;
    
    Exemple : `http://www.example.net/dynacase/?app=MY_APP&action=MY_ACTION`

`MEMORY_LIMIT`
:   Limite mémoire par processus.
    
    Type : `G`
    
    Défaut : `32M`

`CORE_DBCONNECT`
:   Mode de connexion à la base de données (persistent vs. non-persistent).
    
    Type : `G`
    
    Défaut : `unpersistent`
    
    Mettre en persistent peut permettre une accélération des requêtes.
    
    Ce mode peut nécessiter un paramétrage spécifique de Postgresql comme le
nombre de connexion max : `max_connection`. Le nombre de connexions doit être
approximativement 3 fois le nombre max de requêtes en parallèles.
    
    La prise en compte de ce paramètre n'est effectif qu'après avoir lancé le
script `./wstart`.
    
    La modification en persistent ne doit être fait que si nécessaire après des
tests de performances.
    
`USE_FREEDOM_USER`
:   Utilise dynacase comme interface de modification des utilisateurs.
    
    Type : `G`
    
    Défaut : `yes`

`STYLE`
:   Style par défaut.
    
    Type : `G`
    
    Défaut : `default`

`FONTSIZE`
:   Taille par défaut des fontes.
    
    Type : `G`
    
    Défaut : `normal`

`CORE_CLIENT`
:   Nom du client.
    
    Type : `G`
    
    Défaut : &lt;vide&gt;

`CORE_LOGOCLIENT`
:   Logo du client.
    
    Type : `G`
    
    Défaut : &lt;vide&gt;

`CORE_LANG`
:   Langue par défaut.
    
    Type : `GU`
    
    Défaut : `fr_FR`

`CORE_DB`
:   Coordonnées d'accès à la base de données.
    
    Type : `G`
    
    Défaut : `service=<pgServiceName>`

`CORE_PUBDIR`
:   Chemin d'accès absolu du contexte.
    
    Type : `G`
    
    Défaut : `</path/to/context>`

## FDL - Blibliothèque dynacase

L'application FDL définit un ensemble de fonctions pour la manipulation des
documents. Ces paramètres sont tous globaux et sont utilisés par les autres
applications : FREEDOM, GENERIC et ONEFAM.

`FREEDOM_DB`
:   Coordonnées d'accès à la base de données.
    
    Type : `G`
    
    Défaut : `service=<pgServiceName>`
    
    Ce paramètre doit avoir la même valeur que le paramètre `CORE_DB`.

`ENUM_TITLE_SIZE`
:   Taille maximum des chaines de caractères pour les choix.
    
    Type : `GU`
    
    Défaut : `40`

`FDL_BCC`
:   Copie envoi de mail.
    
    Type : `GU`
    
    Défaut : `No`
    
    Mettre `yes` si vous voulez recevoir une copie des mails que vous envoyez
via le serveur. Dans ce cas, vous êtes mis en destinataire caché (Blind Carbon
Copy).

`FDL_MAX_FGEXPORTDOC`
:   Nombre maximum de document pouvant être importé directement, c'est à dire
pas en tâche de fond.
    
    Type : `G`
    
    Défaut : `20`
    
    Ce paramètre est à ajuster en fonction du temps d'exécution maximal fixé
par PHP (paramètre PHP ini `max_execution_time`). Si le temps d'import est
supérieur au `max_execution_time`, alors seuls les documents traités dans le
temps d'exécution imparti seront importés.

`SMTP_HOST`
:   Nom DNS, ou adresse IP, du serveur SMTP.
    
    Type : `G`
    
    Défaut : `localhost`

`SMTP_PORT`
:   Numéro du port du serveur SMTP.
    
    Type : `G`
    
    Défaut : `25`

`TE_HOST`
:   Nom DNS ou adresse IP, du serveur de transformation.
    
    Type : `G`
    
    Défaut : `localhost`

`TE_PORT`
:   Numéro du port du serveur de transformation.
    
    Type : `G`
    
    Défaut : `51968`

### GENERIC - Manipulation d'une famille

L'application GENERIC n'est pas utilisée directement. Ses paramètres sont
transmis aux applications héritant de GENERIC. Il n'est pas nécessaire de
modifier ces paramètres.

`DEFAULT_FAMILY`
:   Famille de document par défaut.
    
    Type : `A`
    
    Défaut : &lt;vide&gt;

`DEFAULT_FLD`
:   Identifiant dossier par défaut.
    
    Type : `A`
    
    Défaut : &lt;vide&gt;

`CARD_SLICE_LIST`
:   Nombre de cartes par page.
    
    Type : `AU`
    
    Défaut : `8`

### FREEDOM - Gestion des documents

`ROOT_FLD`
:   Identifiant du dossier racine. Ceci permet de définir le dossier racine du
plan de classement commun.
    
    Type : `A`
    
    Défaut : `9`

