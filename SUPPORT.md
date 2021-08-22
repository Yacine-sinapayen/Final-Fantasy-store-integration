# Support de projet

## BEM : block element modifier

Prenons l'exemple de nos articles.

 <article class="product product--out--of-stock">
            <img 
            class="product__image"
            src="/images/aerith.png" 
            alt="Cloud Strife" 
            />
            <div class="product__content">
                <h4 class="product__category"> Final Fantasy Crisis Core</h4>
                <h3 class="product__name">Aerith Gainsborough</h3>
                <p class="product__description">Figurine de 7 pouces - livrée avec son packaging</p>
                <a href="" class="product__buy">
                    <span class="product__buy-text">Ajouter au panier</span> 
                    <ins class="product__promo">74,90 €</ins> 
                </a> 
            </div> 
        </article> 

- Block c'est un ensemble d'élément, un regroupement qui représente littéralement un bloc visuel
Il s'écrit avec une classe qui comporte des lettre, des chiffres ou des traits d'unions. On peut avoir des blocs dans des blocs, mais ça reste de nouveau blocs, on ne va pas les concatainer. Exemple : `class ="product"`

- Element : `class ="product__buy"` or `class="product__buy-text"` or `class="product__promo"` for example.
One element can be inside than an other element. But it keeps a specific writing. NameBlock + NameElement Not NameBlock + NameElement-Element.
Element, ils composent le bloc, ils se trouvent obligatoirement dans un bloc, et si on a un élément dans un élément on ne concataine pas non plus, chaque élément restera un élément à pars entière du bloc.
Il suffixe la classe du bloc avec un double underscore ex: .bloc__element. Il peut être composé de lettre, de chiffres, d'underscore et de traits d'unions

- Modifier, il vient modifier le visuel d'un bloc ou d'un élément. Il ne sert pas à définir une structure, seulement à la modifier. Par exemple on a un article normal, on veut qu'il s'affiche comme étant hors stock, alors on va appliquer le modifier au block.
Il s'écrit en suffixant le bloc ou l'élément avec un double trait d'union puis le nom du modifier ex: .block_element--modifier ou alors .block--modifier exemple `product--out--of-stock`

Modifier targets element who wants changement inside style.css :

.product--out--of-stock .product__buy{
    background-color: #666 ;
}

.product--out--of-stock .product__name{
    color: red ;
}

Une fois que le modifier est créer il n'y a plus qu'a l'appliquer à un block comme pour l'article d'aerith :

Like this, only elements `product__name` and `product__buy` are modifier.

## Flex 

- `align-content`, définit la façon dont l'espace est réparti entre et autour des éléments quand ils sont sur plusieurs lignes. Il ne fonctionnera pas si il n'y a qu'une seule ligne, dans ce cas là il va plutot falloir utiliser le `align-items`.

- `flex-wrap`, par défaut, le `display: flex` affiche ses enfants en une seule ligne, et essaye de se débrouiller pour TOUS les afficher sur cette même ligne, il va donc complétement ignorer la `width` de ses enfants. Avec le `flex-wrap` la `width` compte, et du coups on peut ne pas pouvoir tout avoir sur la même ligne. Dans ce cas la `flex-wrap: wrap` va permettre de mettre les éléments à la ligne.

- `flex-grow`, définit le facteur **d'expansion** d'un élément flexible dans un conteneur avec un `display: flex`.  
On peut voir ça comme un poids, une place qu'il occupe. Si jamais j'ai 3 élément qui ont la même valeur `flex-grow` ( par exemple `1`), alors ces éléments occuperont tous la même place.  
Si jamais un de ces 3 éléments a comme valeur le double des deux autres ( par exemple `2` ) alors il viendra occuper `2` fois plus de place.
![Flex Grow](https://css-tricks.com/wp-content/uploads/2018/10/flex-grow.svg)

## Positionnement

Un élément positionné est un élément dont la propriété de position calculée est relative, absolute, fixed ou sticky.  

- `static`, c'est le comportement par défaut. L'élément est alors visible dans le flux avec sa position. Les propriétés top, right, bottom, left et z-index ne s'appliquent pas. On dit en fait qu'il N'EST PAS positionné.
- `relative`, L'élément est positionné dans le flux normal du document puis décalé, par rapport à lui-même, selon les valeurs fournies par `top`, `right`, `bottom` et `left`. Le décalage n'a pas d'impact sur la position des éléments. Aussi, l'espace fourni à l'élément sur la page est le même que celui fourni avec static.
- `absolute`, L'élément est retiré du flux normal et aucun espace n'est créé pour l'élément sur la page, c'est comme si il n'était pas là. Il est ensuite positionné par rapport à son ancêtre le plus proche qui est lui-même positionné ( c'est à dire le parent le plus proche ayant une valeur de position soit `relative`, `absolute`, `fixed` ou `sticky`),  s'il y en a un ou par rapport au bloc englobant initial sinon, la position finale de l'élément est déterminée par les valeurs de top, right, bottom et left.
Exemple avec `produc__badge` il est en `position:absolute` et nous voulons qui soit positionné à l'intérieur de son parent `.product`, pour cela nous avons ajouté un `position:relative` à .product avfin qu'il se positionne par rapport à celui-ci. 
- `fixed`, L'élément est retiré du flux normal ( c'est comme si il n'existait plus dans le DOM ) et **aucun espace** n'est laissé pour l'élément. L'élément est positionné relativement par rapport à la fenêtre. Si on scroll dans cette fenetre, alors l'élément ne bouge pas;
- `sticky` Sa position est comme un relative, sauf qu'il faut le positionner quand même pour que ça fonctionne. Il va se position normalement, et quand on va scroll dans son parent, lui va garder sa position à l'écran. Si jamais on dépasse son parent sur la page, lui ne quittera pas son parent.

## Situation ou l'on a deux élément dans la nav et que l'on veut que seulement le première élément soit en `position : fixed`

1- Mettre l'éléménet 1 en position fixed et ensuiote je lui donne l'endroit de ma fenêtre ou je veux qu'il soit :  
    `top: 0;`
    `left: 0;`
    `right: 0;`

Sur l'élément2 je mets un margin-top de l'équivalent de l'épaisseur de l'élément 1. par exemple `magin-top : 4rem;`

Enfin, vu que le html et une superposition de feuille de calque, il faut que je ramène en position 1 du front mon élément 1. POur cela je vais utiliser la propriété `z-index :  1;`.
Exemple :
.element__1{
    background-color: red;
    padding: 1rem;
    color: white;
    font-size: 2rem;
    font-weight: bold;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1;
}
.element__2{
    padding: 1rem;
    background-color:#666;
    text-align: center;
    color: white;
    margin-top: 4rem;
}


## Suuport html part a revoir

Modifier le contenu deplusieurs balises identiques dans un doc html. 
je selectione l'occurence , je fais un "cmd d" pour toutes les sélectionner. ensuite je mantiens cmd et pour modifier au bonne endroit. 

Récupérer une police Google font

- se rendre sur google font

- taper dans la barre de recherche la police

- cliquer sur la police

- sélectionner les type et version de police que l’on veut importer 

Par exemple : light 300 / medium 500 / bold 700 (possible d’importer en italique en super gras etc)

- Une sélectionné, cliquer sur import et copier le lien tout en haut de notre feuille de styles.css 
Exemple : @import url('https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,300;0,500;0,700;1,300&display=swap');

- Ensuite copier le cas rules et le coller dans la balise body 
Exemple :
body{
    font-family: 'Raleway', sans-serif; 
}


Flexbox (tags;display flex): Comment centrer un élément à l’horizontal et à la verticale ? 

Sur le parent de l’élément : « Flex-direction row » + « justify-content: center » permet d’aligner horizontalement un text et « align-items : center » va permettre d’aligner verticalement ce même élément. 

Exemple : 
.main-content{
    display: flex;
    flex-direction: row;
    align-items: center; (verticalemment)
    justify-content: center;(horizontalement)
}

BEM : block__element-modifier

Balise del :
L’élèment HTML <del> représente une portion de texte ayant été supprimée d’un document. Cet élément est souvent (mais pas nécessairement) affiché rayé. 
L’élèment <ins> est quant à lui utilisé pour représenter des portions de texte ajoutées.

Exemple d’utilisation pour une promotion de prix : 
   <a href="" class="product__buy">
       <span class="product__buy-text">Ajouter au panier</span> 
       <del class="product__price">98,90 €</del> 
       <ins class="product__promo">59 €</ins>
   </a> 


Display block /inline:
Display block respecte les dimensions de son conteneur et pousse les éléments autour de lui. 
À contrario quand l’élément est en display inline se fou de son contenu et va prendre tout l’espace dont il peu disponible dans et en dehors de son conteneur. 

Créer un menu centré avec les flexbox (cf vidéo grafikart flexbox): 
Example :
.menu{
	display : flex;
	align-items: center;
	align-content: center; 
	justify-content: space-around;
	flex-wrap: wrap
}

En responsicve je veux que mes éléments s’empiles en 1 seule colonne :

@media (max-width: 500px) {
	.menu{
		flex-direction: colum;
		height: auto;
}

Créer une Sidecar (cf vidéo grafikart flexbox 19 min).

Centrer une image dans son conteneur (cf vidéo grafikart flexbox 29,20min):  

.sur-l’lélément-parent {
	display: flex;
	Justify-content:center;
	Align-items:center;
}

Box-sizing: border-box : contrairement à « box-sizing: content-box » , border-box permet de prendre en compte le pudding et le marin d’un élément dans son contenue et de faire en sorte que celui-ci ne dépasse pas. 
Du coup dans le calcul de répartition de l’espace de plusieurs éléments c’est très utile car nous obtenons des calcules justes.

Width calc : comment diviser notre espace en trois colonnes égales ?

.product{
    border: 1px solid #ccc;
    width: calc((100%/3) - (2*1rem));ici dans notre calcule on a divisé la largeur par 3 tout en retirant le margin à gauche et à droite de nos produits afin de ne pas fausser le calcule. Ne oublier l’espace avant et après le trait d’union. 
    margin: 1rem;  
    padding: 0.5rem;
    box-sizing: border-box; permet de prendre en compte son contenu, son padding et son border mais pas le margin car le marin reste toujours en dehors de l’élément.
}



