# Doc::postStore() {#core-ref:99520a31-0aef-4bc6-b20a-114737059d17}

<div class="short-description" markdown="1"> 
[Hameçon][hook] (ou hook) utilisé par la méthode [`Doc::Store()`][docstore].
Cette méthode est appelée après l'enregistrement en base de données.
</div>

## Description {#core-ref:6a794ff2-4c9c-4bb1-aed7-8c23e3b7ab2d}

    [php]
    string postStore ()

Cette méthode est aussi utilisable pour réaliser un post-traitement après une
modification. Elle ne peut pas annuler l'enregistrement. Le document possède un
identificateur et est déjà enregistré en base.

### Avertissements {#core-ref:a3f912a9-0ccf-4f38-97af-faeac7c423aa}

Il ne faut pas appeler la méthode [`Doc::Store()`][docstore] dans cette méthode
au risque d'avoir une boucle de récursion infinie.

Si des modifications d'attributs sont réalisées dans cette méthode, elles sont
enregistrées en base par la méthode [`Doc::Store()`][docstore].


## Liste des paramètres {#core-ref:0252e614-71e3-44f8-a4d8-6bc5ea238ce2}

Aucun paramètre.

## Valeur de retour {#core-ref:5ceded6d-ae21-4c1e-b554-537b532aed23}

La valeur de retour est un message d'information. Il est stocké dans le
paramètre de sortie `$info->postStore` de la méthode [`Doc::Store()`][docstore].

## Erreurs / Exceptions {#core-ref:e187697c-5e99-4083-ab9d-05d2a6056435}

Aucun.

## Historique {#core-ref:265bde3d-c9a9-4976-8a57-e9c4c980b73c}

Anciennement nommée `postModify()`.

## Exemples {#core-ref:47b6948d-d6a5-4b04-b96d-8657499dc5c2}

Calcul de la somme des attributs `my_numberone` et `my_numbertwo` et
enregistrement dans l'attribut `my_sum`.

Soit la famille suivante :

| BEGIN |                   | Ma famille        |                 |     | MYFAMILY |       |     |     |   |         |     |
| ----- | ----------------- | ----------------- | --------------- | --- | -------- | ----- | --- | --- | - | ------- | --- |
| CLASS | My\MyFamily       |                   |                 |     |          |       |     |     |   |         |     |
| //    | idattr            | idframe           | label           | T   | A        | type  | ord | vis | … | phpfunc |     |
| ATTR  | MY_IDENTIFICATION |                   | Identification  | N   | N        | frame | 10  | W   |   |         |     |
| ATTR  | MY_NUMBERONE      | MY_IDENTIFICATION | nombre 1        | Y   | N        | int   | 20  | W   |   |         |     |
| ATTR  | MY_NUMBERTWO      | MY_IDENTIFICATION | nombre 2        | N   | N        | int   | 30  | W   |   |         |     |
| ATTR  | MY_SUM            | MY_IDENTIFICATION | nombre 1&plus;2 | N   | N        | int   | 30  | R   |   |         |     |
| END   |                   |                   |                 |     |          |       |     |     |   |         |     |

Avec la classe :

    [php]
    namespace My;
    use \Dcp\AttributeIdentifiers\MyFamily as MyAttributes;
    
    class MyFamily extends \Dcp\Family\Document
    {
        public function mySum($x, $y)
        {
            return ($x + $y);
        }
        public function postStore()
        {
            $err=parent::postStore();
            if (empty($err)) {
                $n1 = $this->getAttributeValue(MyAttributes::my_numberone);
                $n2 = $this->getAttributeValue(MyAttributes::my_numbertwo);
                $this->setAttributeValue(MyAttributes::my_sum, $this->mySum($n1, $n2));
            }
            return $err;
        }

## Notes {#core-ref:339dfc65-e878-4451-9145-f7e70b729cf5}

En cas de famille héritée, il est nécessaire d'appeler l'hameçon du parent pour
disposer des mêmes fonctionnalités.

Cette méthode est appelée par [`Doc::store()`][docstore] en cas de création, de
révision et de modification tandis que l'hameçon
[`Doc::postCreated()`][docpostcreated] est appelé qu'en cas de création ou de
révision.


## Voir aussi {#core-ref:ade45758-e063-4c80-8694-6a49f0845270}

*   [`Doc::store()`][docstore],
*   [`Doc::preCreated()`][docprecreated],
*   [`Doc::preStore()`][docprestore],
*   [`Doc::postCreated()`][docpostcreated].

<!-- links -->
[docstore]:         #core-ref:b8540d13-ece6-4e9e-9b72-6a56bca9da12
[docpostcreated]:   #core-ref:b8f80e6b-a374-4bf4-bc76-47290cd69c45 "Hameçon Doc::postCreated()"
[docpoststore]:     #core-ref:99520a31-0aef-4bc6-b20a-114737059d17 "Hameçon Doc::postStore()"
[docprestore]:      #core-ref:3517da95-82fe-4adb-8bc4-ef49ca55edb0 "Hameçon Doc::preStore()"
[docprecreated]:    #core-ref:e85aa9d4-5e62-4a60-9d1c-f60433301747 "Hameçon Doc::preCreated()"
[docprerefresh]:    #core-ref:580d6be1-6b6a-439b-abd7-34b26cfaf2e5 "Hameçon Doc::preRefresh()"
[docpostrefresh]:   #core-ref:9352c534-3691-41e3-b293-599db8e9a4fd "Hameçon Doc::postRefresh()"
[docrevise]:        #core-ref:882e3730-0483-4dbc-9b9d-0d0b5cc31d38
[hook]:             https://fr.wikipedia.org/wiki/Hook_(informatique)
