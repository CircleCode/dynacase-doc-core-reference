# `[ACTION FDL:FDL_METHOD]` {#core-ref:ba244eb7-c38a-4393-9024-a982ce495f42}

## Description  {#core-ref:63babdf0-3b7e-4d9c-86be-1f38214c6e01}

Cette action permet d'exécuter une méthode de la classe associée au document.
Une fois la méthode exécutée un [header location][header_location] contenant le
le [referer][referer] est renvoyé, ce qui dans la majorité des cas équivaut à un 
refresh de la page en cours. Si le referer n'est pas présent alors le header 
location contient l'url d'accès en consultation du document référencé par l'id.  
Si la méthode exécutée retourne une chaîne de caractère un [`AddWarningMsg`][warningMessage] avec
cette chaîne est ajouté.

**Attention** : La méthode doit avoir le tag `@apiExpose` pour pouvoir être 
exécutée.

## Paramètres {#core-ref:0f2875df-ba84-43fd-be13-927f50f52fa5}

id
:    L'[id][id_document] du document source.

method
:   `string` : Nom de la méthode à exécuter. Cette méthode doit avoir le tag 
    `@apiExpose` pour pouvoir être exécutée.

redirect
:   `n` : Si l'argument est à n alors le [header location][header_location] est
    remplacé par un texte indiquant le statut de l'exécution.

zone
:   `texte` : Si une zone est présente et que le `redirect` n'est pas à `n` alors
    le redirect ne renvoi pas vers le `referer` mais vers le document en 
    consultation avec la zone.


## Limites {#core-ref:7d2e2732-20f5-434b-9260-b1cbc21f53d1}

N/A

<!-- link -->

[id_document]:          #core-ref:9aa8edfa-2f2a-11e2-aaec-838a12b40353 "Propriété ID"
[header_location]:      https://en.wikipedia.org/wiki/HTTP_location "Wikipedia : Header location"
[referer]:              https://en.wikipedia.org/wiki/Referer "Wikipedia : Referer"
[warningMessage]:       https://docs.anakeen.com/dynacase/3.2/dynacase-core-api-reference/_lib_8_common_8php.html#ab39caef8851ccc293383615211dee0c3 "AddWarningMessage"