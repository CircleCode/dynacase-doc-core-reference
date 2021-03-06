# Options communes à tous les types d'attributs {#core-ref:16e19c90-3233-11e2-a58f-6b135c3a2496}

searchcriteria
:   Indique quelle sera l'utilisation de l'attribut dans les recherches.
    
    Les valeurs possibles sont :
    
    *   **`visible` (comportement par défaut)** : Dans ce cas
        
        *   l'attribut *est indexé* pour la recherche plein texte
        *   l'attribut *est présenté* dans les critères des recherches détaillées et des rapports
    
    *   `restricted` : Dans ce cas
        
        *   l'attribut *est indexé* pour la recherche plein texte
        *   l'attribut *n'est pas présenté* dans les critères des recherches détaillées et des rapports
    
    *   `hidden` : Dans ce cas
        
        *   l'attribut *n'est pas indexé* pour la recherche plein texte
        *   l'attribut *n'est pas présenté* dans les critères des recherches détaillées et des rapports

showempty
:   Indique que l'attribut doit être présenté en consultation, même si sa valeur est vide.
    
    Cela modifie le comportement par défaut, qui consiste à n'afficher en consultation que les attributs valués.
    
    Les valeurs possibles sont :
    
    *   `` (une chaîne vide) : Dans ce cas, le libellé sera présenté, et aucune valeur ne sera affichée
    *   toute chaîne de caractères : Dans ce cas, le libellé est affiché, et la valeur est remplacée par le texte donné.
    
    Remarque : Pour le type [image][attrimage], la valeur doit indiquer le chemin 
    relatif à un fichier 'image'. L'image sera alors affichée si la valeur est vide.

sortable
:   Indique les modalités de tri de l'attribut.
    
    Par défaut, les attributs sont considérés comme non triable.
    
    Les valeurs possibles sont :
    
    *   `asc` : Dans ce cas
        *   l'attribut sera présenté dans le menu de tri de *ONEFAM* et dans les rapports
        *   l'ordre de tri par défaut sera ascendant
    *   `desc` : Dans ce cas
        *   l'attribut sera présenté dans le menu de tri de *ONEFAM* et dans les rapports
        *   l'ordre de tri par défaut sera descendant

version
:   Indique que l'attribut est utilisé pour la composition de la *version*.
    Se reporter aux [propriétés de la classe Doc](#core-ref:9aa8edfa-2f2a-11e2-aaec-838a12b40353) pour plus de détails.
    
    Les valeurs possibles sont :
    
    *   `yes`
    *   **`no` (comportement par défaut)**

vlabel
:   Indique la position du libellé de l'attribut.
    
    Les valeurs possibles sont :
    
    *   pour les attributs de type _frame_ et _onglet_ :
        
        *   **`up` (comportement par défaut)**
        *   `none`
    
    *   pour les attributs de type _array_ :
        
        *   **`left` (valeur par défaut *en consultation*)**
        *   **`up` (valeur par défaut *en modification*)**
        *   `none`
    
    *   pour les autres attributs :
        
        *   **`left` (comportement par défaut)**
        *   `up`
        *   `none`

<a class="chapter-reference" name="commonELabel"/>
elabel 
:   Texte du tooltip du label de l'attribut pour le document en mode modification.
    
    Ne s'applique pas aux attributs de structure (tab, frame, array).
    
    Les valeurs possibles sont :
    
    *   Toute chaîne de caractères. Attention, la plupart des navigateurs n'acceptent pas de retour chariot.



ititle
:   Texte du tooltip du bouton '...' de l'[aide à la saisie][aide_saisie]. 
    Par défaut : « choisissez une valeur »

ltitle
:   Texte affichable en tooltip sur l'hyperlien lorsque la souris passe
    dessus

ltarget
:   Nom de la fenêtre destinataire de l'hyperlien. Par défaut `_self`.
    Si `ltarget=fhidden` alors la requête ira dans une fenêtre cachée.

lconfirm
:   Indique si on veut un message de confirmation avant l'activation du
    lien. Mettre `lconfirm=yes` pour activer la confirmation.

tconfirm
: Texte de la confirmation

autosuggest
:   En édition, sur une aide à la saisie, indique que la recherche est
    lancée à chaque modification du texte saisi. (par défaut `yes`).
    Mettre à `no` pour désactiver l'auto-suggestion

eltitle
:   Options pour pour les extra liens (*elink*).
    Texte affichable surgissant sur le bouton généré par l'[extra lien][elink].

elsymbol
:   Caractère affiché sur le bouton généré par l'[extra lien][elink].
    Par défaut c'est le caractère `+` qui est affiché.

eltarget
:   Nom de la fenêtre destinataire sur le bouton généré par l'[extra lien][elink].

viewtemplate
:   Référence de la [vue d'attribut][viewtemplate] à utiliser lors de la
    consultation du document

edittemplate
:   Référence de la [vue d'attribut][edittemplate] à utiliser lors de la
    modification du document

<!-- links -->
[aide_saisie]: #core-ref:0b2d4cd0-4eed-41d8-ac57-37525a444194
[elink]: #core-ref:edf84026-7980-442f-bc86-88739e49e3b5
[viewtemplate]: #core-ref:9cb7b313-7294-424d-bd86-a63155025902 "vue de consultation"
[edittemplate]: #core-ref:4faa4b17-56fc-4e42-a091-f1a97b7591b8 "vue de modification"
[attrimage]: #core-ref:4fca7712-59e0-4186-bfd0-6214104a0f60