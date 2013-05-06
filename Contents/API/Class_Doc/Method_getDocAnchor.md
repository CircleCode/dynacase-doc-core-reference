# Doc::getDocAnchor() {#core-ref:55e9c46c-2a10-4911-8243-7c913416648f}

<div class="short-description">
Générer un fragment HTML contenant une ancre HTML vers un document.
</div>

## Description {#core-ref:8ca28abd-366b-47b8-bf17-9d9e2e952080}

    [php]
    string getDocAnchor ( int $id, [ string $target = "_self" [, bool $htmllink = true [, bool|string $title = false [, bool $js = true [, string $docrev = "latest" [, bool $viewIcon = false ]]]]]] )

Permet de générer un fragment HTML, qui pourra être inséré dans un document
HTML, et qui contiendra une ancre HTML (`<a href="…">…</a>`) vers un document
Dynacase.

### Avertissements {#core-ref:124fbf30-ae8c-4dd7-9023-76b80d7804bb}

N/A

## Liste des paramètres {#core-ref:de6252d4-d376-4c35-a85d-f2ff835aa224}

(int) `id`
:   L'identifiant du document pour lequel on souhaite générer le code
de l'ancre HTML.

(string) `target`
:   Le nom du format du lien HTML. Les valeurs supportés sont : <br/>
`_self` (par défaut), <br/>
`mail` (pour un fragment HTML inséré dans un mail),<br/>
`ext` (pour un fragment HTML inséré dans une interface ExtJS), <br/>
toute autre valeur sera prise en compte comme la propriété `target` de l'ancre
HTML générée.

(bool) `htmllink`
:   Si `false` alors seul le fragment HTML contenant le
titre, sans ancre, sera généré.

(bool|string) `title`
:   Si une chaîne est spécifiée, alors elle sera utilisée à
la place du titre du document.

(bool) `js`
:   Si `true` alors du code JavaScript est inclus pour ouvrir le
document dans une popup.

(string) `docrev`
:   Indique sur quelle révision du document pointera l'ancre
HTML. Valeurs possible : `latest` ou `fixed`.

(bool) `viewIcon`
:   Si `true` l'icône de la famille du document sera présentée
dans l'ancre HTML.

## Valeur de retour {#core-ref:c812a822-8874-49a4-8905-5cc88d2f6eda}

La méthode retourne une chaîne contenant un fragment HTML avec une ancre
vers le document.

## Erreurs / Exceptions {#core-ref:d21f852c-d233-408f-aaeb-ff3cca310d4b}

N/A

## Historique {#core-ref:3a513f2a-6956-4199-b716-7919790b3d47}

N/A

## Exemples {#core-ref:6167c555-8387-460e-bed6-121a67c2bdd8}

    [php]
    /* Générer une ancre HTML sans JS mais avec l'icône de la famille du document */
    $htmlAnchor = $this->getDocAnchor($docId, "_self", true, false, false, "latest", true);
    /* Insérer le fragment HTML dans le layout */
    $this->lay->set('LINK_TO_DOCUMENT', $htmlAnchor);

## Notes {#core-ref:a3c9ae9e-3ed8-4611-9b39-7f742e381d9a}

Si `$target` est positionné avec la valeur `mail`, alors l'URL de l'ancre est
composée à partir du paramètre interne [`CORE_MAILACTIONURL`](#core-ref:a3dacf94-b966-11e2-a8ac-001ff3d775e1).

Le paramètre
[`CORE_MAILACTIONURL`](#core-ref:a3dacf94-b966-11e2-a8ac-001ff3d775e1) est
composé à partir du paramètre applicatif
[`CORE_MAILACTION`](#core-ref:c3d9cb18-16d0-435a-b8c2-5fa6ac06c522), si
celui-ci est renseigné. Dans le cas contraire, il est composé à partir du
paramètre applicatif
[`CORE_URLINDEX`](#core-ref:c3d9cb18-16d0-435a-b8c2-5fa6ac06c522).

Pour toute autre valeur de `$target`, l'URL de l'ancre est générée relative à
l'action courante.

## Voir aussi {#core-ref:58c61a64-7a4e-4283-9cc1-237fa2b3911d}

N/A
