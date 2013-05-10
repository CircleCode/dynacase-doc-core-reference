# Action::getParam {#core-ref:a3dacf94-b966-11e2-a8ac-001ff3d775e1}
 
<div class=”short-description”>
Cette méthode donne la valeur d'un paramètre applicatif.

</div>

<div class=”applicabilite”>
Applicable
</div>


## Description


    [php]
    mixed getParam(string $name [, mixed $def = ""])

Cette méthode permet de récupérer la valeur d'un des paramètres de l'application dont est issu l'action. Les paramètres de l'application "*CORE*" et les paramètres globaux sont aussi disponibles. De plus cette méthode permet aussi de récupérer les valeurs des paramètres volatiles.

Si le paramètre choisi est un paramètre *utilisateur*, c'est la valeur choisie par l'utilisateur qui sera retournée. Si l'utilisateur n'a pas encore choisi de valeur pour ce paramètre c'est la valeur définie par le paramètre applicatif qui sera retourné.

Les paramètres volatiles généraux sont :
`CORE_EXTERNURL`
: Url d'accès au serveur. Elle est composée à partir du paramètre application "*CORE_URLINDEX*". Si ce paramètre n'est pas renseigné, elle est composée en fonction de l'url d'accès à l'action.

`CORE_MAILACTIONURL`
: Url d'accès au serveur pour les mails envoyés par Dynacase. Elle est composée à partir du paramètre application "[*CORE_MAILACTION*](#core-ref:c3d9cb18-16d0-435a-b8c2-5fa6ac06c522)". Si ce paramètre n'est pas renseigné, elle est composée en fonction du paramètre "*CORE_EXTERNURL*".

`ISIE`
: Égale à *true*, si l'url d'accès à l'action provient d'un navigateur Internet Explorer (toutes version confondues). Est égale à *false* en mode console (*wsh*).

`ISIE6`
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 6. Est égale à *false* en mode console (*wsh*).

`ISIE7`
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 7. Est égale à *false* en mode console (*wsh*).

`ISIE8`
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 8. Est égale à *false* en mode console (*wsh*).

`ISIE9`
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 9. Est égale à *false* en mode console (*wsh*).

`ISIE10`
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Internet Explorer version 10. Est égale à *false* en mode console (*wsh*).

`ISSAFARI`
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Safari (Windows ou MacOs X). Est égale à *false* en mode console (*wsh*).

`ISCHROME`
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Google Chrome (Windows , MacOs X ou Linux). Est égale à *false* en mode console (*wsh*).

`ISAPPLEWEBKIT`
: Égale à true, si l'url d'accès à l'action provient d'un navigateur Google Chrome ou Safari utilsant AppleWebKit. Est égale à *false* en mode console (*wsh*).



### Avertissements

N/A

## Liste des paramètres

(string) `name`
: Nom du paramètre

(mixed) `def`
: Valeur retournée si la paramètre n'existe pas ou si la valeur du paramètre est strictement égal à *null*.
   valeur par défaut : chaîne vide.

## Valeur de retour

Le retour est la valeur du paramètre. Si le paramètre n'existe pas ou est *null* c'est la valeur *def* qui est retournée.

## Erreurs / Exceptions

N/A

## Historique

N/A

## Exemples

    [php]
    // myaction.php - MY_PARAM est déclaré dans le fichier MYAPP_init.php
    function myAction(Action &$action) {

       if ($action->getParam("ISIE") {
         // Internet Explorer détecté
       }
       $myParam = $action->getParam("MY_PARAM");
    }

## Notes

Bien que cette méthode soit définie sur la classe Action, elle est un raccourci pour accéder à la méthode Application::getParam de l'application dont est issue l'action.

Cette méthode ne peut fonctionner que si l'action est initialisé (`::isAffected()`) . Si ce n'est pas le cas, la valeur *def* est toujours retournée.

Les paramètres applicatifs sont déclarés dans le fichier &lt;APPLICATION_NAME&gt;_init.php.

Les valeurs des paramètres sont visibles et modifiables avec l'application *APPMNG*.

## Voir aussi

*  Voir Action::setVolatileParam()
*  Voir la classe *ParameterManager*
