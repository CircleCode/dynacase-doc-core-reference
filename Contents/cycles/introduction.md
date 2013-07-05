# Cycles de vie {#core-ref:55a53d99-0c24-48d8-8cb9-1caa171f2e9a}

Le *cycle de vie* (*workflow*) permet de gérer la vie d'un document en lui
imposant un ensemble d'*étapes* pour aller de sa création jusqu'à sa fin (moment
à partir duquel le document n'évolue plus).

Dans la suite de ce chapitre, l'exemple suivant de cycle de
vie sera utilisé :

<svg width="100%" height="470pt"
 viewBox="0.00 0.00 315.00 470.00" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <g id="graph1" class="graph" transform="scale(1 1) rotate(0) translate(4 466)">
        <title>Défaut</title>
        <!-- Rédaction -->
        <g id="node2" class="node">
            <title>Rédaction</title>
            <polygon fill="#ffe991" stroke="black" stroke-width="2" points="179,-462 95,-462 95,-426 179,-426 179,-462"/>
            <text text-anchor="middle" x="137" y="-440.3" font-family="sans" font-size="14.00">Rédaction</text>
        </g>
        <!-- Vérification -->
        <g id="node3" class="node">
            <title>Vérification</title>
            <polygon fill="#a8e5ff" stroke="black" points="212,-370 132,-370 132,-334 212,-334 212,-370"/>
            <text text-anchor="middle" x="172" y="-348.9" font-family="sans" font-size="12.00">Vérification</text>
        </g>
        <!-- Rédaction&#45;&gt;Vérification -->
        <g id="edge3" class="edge">
            <title>Rédaction&#45;&gt;Vérification</title>
            <path fill="none" stroke="#00008b" d="M112.595,-425.977C100.361,-415.269 89.7336,-401.054 98,-388 101.33,-382.742 111.043,-376.985 122.382,-371.686"/>
            <polygon fill="#00008b" stroke="#00008b" points="124.002,-374.796 131.734,-367.552 121.172,-368.394 124.002,-374.796"/>
            <text text-anchor="middle" x="126.5" y="-395.8" font-family="sans" font-size="9.00">Transmettre</text>
        </g>
        <!-- Abandonné -->
        <g id="node7" class="node">
            <title>Abandonné</title>
            <ellipse fill="#8870ff" stroke="black" cx="169" cy="-162" rx="43.0805" ry="43.2732"/>
            <text text-anchor="middle" x="169" y="-158.9" font-family="sans" font-size="12.00">Abandonné</text>
        </g>
        <!-- Rédaction&#45;&gt;Abandonné -->
        <g id="edge15" class="edge">
            <title>Rédaction&#45;&gt;Abandonné</title>
            <path fill="none" stroke="#00008b" d="M179.433,-436.276C196.355,-431.343 214.318,-422.798 225,-408 265.622,-351.727 253.039,-318.137 232,-252 226.339,-234.205 215.687,-216.91 204.731,-202.371"/>
            <polygon fill="#00008b" stroke="#00008b" points="207.206,-199.855 198.28,-194.147 201.698,-204.175 207.206,-199.855"/>
            <text text-anchor="middle" x="278" y="-308.8" font-family="sans" font-size="9.00">Abandonner</text>
        </g>
        <!-- Vérification&#45;&gt;Rédaction -->
        <g id="edge5" class="edge">
            <title>Vérification&#45;&gt;Rédaction</title>
            <path fill="none" stroke="#00008b" d="M167.544,-370.119C164.48,-381.112 160.059,-395.6 155,-408 153.825,-410.881 152.498,-413.844 151.111,-416.769"/>
            <polygon fill="#00008b" stroke="#00008b" points="147.92,-415.325 146.587,-425.836 154.183,-418.451 147.92,-415.325"/>
            <text text-anchor="middle" x="191" y="-400.8" font-family="sans" font-size="9.00">Renvoyer</text>
            <text text-anchor="middle" x="191" y="-390.8" font-family="sans" font-size="9.00">en rédaction</text>
        </g>
        <!-- Diffusion -->
        <g id="node4" class="node">
            <title>Diffusion</title>
            <polygon fill="#66ff7a" stroke="black" points="111,-288 39,-288 39,-252 111,-252 111,-288"/>
            <text text-anchor="middle" x="75" y="-266.9" font-family="sans" font-size="12.00">Diffusion</text>
        </g>
        <!-- Vérification&#45;&gt;Diffusion -->
        <g id="edge7" class="edge">
            <title>Vérification&#45;&gt;Diffusion</title>
            <path fill="none" stroke="#00008b" d="M138.844,-333.951C130.041,-328.739 120.817,-322.618 113,-316 106.044,-310.112 99.326,-302.869 93.5228,-295.929"/>
            <polygon fill="#00008b" stroke="#00008b" points="96.162,-293.626 87.1715,-288.02 90.704,-298.009 96.162,-293.626"/>
            <text text-anchor="middle" x="134" y="-308.8" font-family="sans" font-size="9.00">Accepter</text>
        </g>
        <!-- Vérification&#45;&gt;Abandonné -->
        <g id="edge17" class="edge">
            <title>Vérification&#45;&gt;Abandonné</title>
            <path fill="none" stroke="#00008b" d="M171.728,-333.985C171.307,-307.543 170.476,-255.499 169.842,-215.74"/>
            <polygon fill="#00008b" stroke="#00008b" points="173.34,-215.605 169.681,-205.662 166.341,-215.717 173.34,-215.605"/>
            <text text-anchor="middle" x="199" y="-267.8" font-family="sans" font-size="9.00">Abandonner</text>
        </g>
        <!-- Diffusion&#45;&gt;Rédaction -->
        <g id="edge9" class="edge">
            <title>Diffusion&#45;&gt;Rédaction</title>
            <path fill="none" stroke="#00008b" d="M68.5018,-288.257C61.9248,-308.367 53.9191,-342.368 63,-370 69.621,-390.147 85.7568,-407.18 101.277,-419.713"/>
            <polygon fill="#00008b" stroke="#00008b" points="99.2168,-422.544 109.283,-425.849 103.475,-416.988 99.2168,-422.544"/>
            <text text-anchor="middle" x="93" y="-354.8" font-family="sans" font-size="9.00">Renvoyer</text>
            <text text-anchor="middle" x="93" y="-344.8" font-family="sans" font-size="9.00">en rédaction</text>
        </g>
        <!-- Diffusé -->
        <g id="node5" class="node">
            <title>Diffusé</title>
            <ellipse fill="#66ff7a" stroke="black" cx="36" cy="-162" rx="36" ry="36"/>
            <text text-anchor="middle" x="36" y="-158.9" font-family="sans" font-size="12.00">Diffusé</text>
        </g>
        <!-- Diffusion&#45;&gt;Diffusé -->
        <g id="edge11" class="edge">
            <title>Diffusion&#45;&gt;Diffusé</title>
            <path fill="none" stroke="#00008b" d="M50.3577,-251.779C44.978,-246.719 40.0008,-240.715 37,-234 33.421,-225.991 31.7543,-216.95 31.2134,-208.068"/>
            <polygon fill="#00008b" stroke="#00008b" points="34.7085,-207.728 31.0484,-197.786 27.7094,-207.841 34.7085,-207.728"/>
            <text text-anchor="middle" x="55.5" y="-226.8" font-family="sans" font-size="9.00">Diffuser</text>
        </g>
        <!-- Diffusion&#45;&gt;Abandonné -->
        <g id="edge19" class="edge">
            <title>Diffusion&#45;&gt;Abandonné</title>
            <path fill="none" stroke="#00008b" d="M81.4171,-251.801C85.1823,-242.985 90.4842,-232.373 97,-224 105.339,-213.285 115.824,-203.115 126.192,-194.259"/>
            <polygon fill="#00008b" stroke="#00008b" points="128.582,-196.825 134.061,-187.756 124.123,-191.429 128.582,-196.825"/>
            <text text-anchor="middle" x="126" y="-226.8" font-family="sans" font-size="9.00">Abandonner</text>
        </g>
        <!-- Archivé -->
        <g id="node6" class="node">
            <title>Archivé</title>
            <ellipse fill="#ff527a" stroke="black" cx="36" cy="-36" rx="36" ry="36"/>
            <text text-anchor="middle" x="36" y="-32.9" font-family="sans" font-size="12.00">Archivé</text>
        </g>
        <!-- Diffusé&#45;&gt;Archivé -->
        <g id="edge13" class="edge">
            <title>Diffusé&#45;&gt;Archivé</title>
            <path fill="none" stroke="#00008b" d="M36,-125.798C36,-112.316 36,-96.7402 36,-82.4342"/>
            <polygon fill="#00008b" stroke="#00008b" points="39.5001,-82.2897 36,-72.2898 32.5001,-82.2898 39.5001,-82.2897"/>
            <text text-anchor="middle" x="55" y="-92.8" font-family="sans" font-size="9.00">Archiver</text>
        </g>
    </g>
</svg>

Le cycle présenté est un cycle standard de rédaction :

1.  Le document est rédigé par un rédacteur.
2.  Il est ensuite soumis à un contrôle.
3.  Suite à ce contrôle, le vérificateur peut :
    *   accepter le document,
    *   le renvoyer en rédaction
4.  Une fois le document vérifié, il peut être :
    *   diffusé
    *   renvoyé en rédaction
5.  Enfin, une fois diffusé, le document finira par être archivé.
6.  De plus, tant qu'il n'a pas été diffusé (et donc été publiquement
    accessible), le document peut être abandonné.

## Vocabulaire {#core-ref:32c41ece-b50e-49d9-a480-c5265dc10b36}

Les éléments de vocabulaires utilisés dans la définition d'un cycle de vie sont
les suivants :

L'`étape`
:   c'est un moment clef de la vie document.
    
    Elle peut être caractérisée par une *activité* ou un *état*.

L'`activité`
:   Elle désigne ce qui doit être fait sur un document pour une étape donnée.

L'`état`
:   Il désigne le statut du document.
    
    On parle d'état lorsque le document est inerte, soit parce que l'on consulte
    des anciennes révisions du document soit parce qu'on est sur un état
    final. Il est à noter qu'ici, *final* ne désigne pas forcément un état en
    bout de cycle, mais plutôt un état pour lequel il n'y a rien à faire. Dans
    notre exemple, *diffusé* est un état *final*, sans activité, car le document
    reste inerte, même s'il finira à terme par être *archivé*.

On peut résumer ces concepts comme suit :

>   Pour une **étape** donnée,  
>   l'**état** désigne **comment le document est arrivé à cette étape**  
>   l'**activité** désigne **ce qui doit être fait**.
