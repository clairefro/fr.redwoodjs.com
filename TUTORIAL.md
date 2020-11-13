# Bienvenue chez Redwood

Bienvenue chez Redwood! Si vous ne l’avez pas encore fait, prenez le temps de lire [Redwood README](https://github.com/redwoodjs/redwood/blob/main/README.md) pour en savoir un peu plus sur les origines de Redwood et les problèmes qu'il entend résoudre. Redwood assemble plusieurs technologies de façon inédite et qui correspond à ce que nous pensons être le futur des applications web avec base de données.  

Dans ce didacticiel, nous allons construire un moteur de blog. En réalité, un blog n’est probablement pas le candidat idéal pour une application construite avec Redwood: les articles peuvent être enregistrés dans un CMS et générées statiquement sous la forme de fichiers HTML servis par un CDN. Ceci étant, la plupart des développeurs comprennent intuitivement ce que recouvre ce type d’application, et un blog présente toutes les caractéristiques que nous souhaitons mettre en lumière. Nous avons donc décidé d'en construire un malgré tout.

Peut-être souhaitez-vous voir ce didacticiel en vidéo? C’est ici :

<div class="relative pb-9/16">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/tiF9SdM1i7M?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

<div class="relative pb-9/16 mt-4">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/SP5vbsWf5Yg?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

<div class="relative pb-9/16 mt-4">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/eT7iIy0F8Tk?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

<div class="relative pb-9/16 mt-4">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/UpD3HyuZkvY?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

## Prérequis

Ce didacticiel suppose que vous soyez déjà familier avec quelques concepts fondamentaux :

- [React](https://reactjs.org/)
- [GraphQL](https://graphql.org/)
- [The Jamstack](https://jamstack.org/)

Vous pouvez tout à fait compléter ce didacticiel sans savoir quoique ce soit sur ces technologies, mais il est possible que vous soyez un peu perdu par certains termes que nous utiliserons sans forcément les expliquer au préalable. D'une façon générale, il est toujours utile de savoir où se situe les frontières et pouvoir distinguer par exemple ce qui provient de React de ce qui est ajouté par Redwood. 

### Node.js et Yarn

Pendant l’installation, RedwoodJS commence par verifier si votre système possède les versions requises de Node et Yarn :

- node: ">=12"
- yarn: ">=1.15"

👉 **Important:** Si votre système ne repond pas à ces prérequis, _l’installation se soldera par une ERREUR._ Vérifiez en exécutant les commandes suivantes dans un terminal:

```
node --version
yarn --version
```
Procédez aux mises à jour le cas échéant, puis relancez l’installation de RedwoodJS lorsque vous êtes prêt !


> **Installer Node et Yarn**
>
> Il y a différentes façons d’installer Node.js et Yarn. Si vous procédez à leur installation pour la première fois, nous vous recommandons de suivre les points suivants :
>
> **Yarn**
>
> - Nous recommandons de suivre les instructions fournies sur [Yarnpkg.com](https://classic.yarnpkg.com/en/docs/install/).
>
> **Node.js**
>
> - Pour les utilisateurs de **Linux** et **Mac**, `nvm` est un excellent outil pour gérer plusieurs versions de Node sur un même système. Il demande un petit effort à mettre en place. Dans les deux cas, utiliser la version la plus récente de [Nodejs.org](https://nodejs.org/en/) fonctionne très bien.
>   - Pour les utilisateurs de **Mac**, si vous avez dejà installé Homebrew, vous pouvez l’utiliser pour [installer `nvm`](https://formulae.brew.sh/formula/nvm). Dans le cas contraire, suivez les [instructions d'installation pour `nvm`](https://github.com/nvm-sh/nvm#installing-and-updating).
>   - Pour les utilisateurs de **Linux**, vous pouvez suivre les [instructions d'installation pour `nvm`](https://github.com/nvm-sh/nvm#installing-and-updating).
> - Nous recommandons aux utilisateurs de **Windows** de visiter [Nodejs.org](https://nodejs.org/en/) pour savoir comment procéder.
>
> Si vous êtes un peu perdu au moment de choisir quelle version de Node utiliser, nous vous recommandons la plus récente LTS avec un numéro de version pair, actuellement il s'agit de la v12.

## Installation & Démarrage du développement

Nous utiliserons yarn ([yarn](https://yarnpkg.com/en/docs/install) est un pré-requis) pour créer la structure de base pour notre application :

    yarn create redwood-app ./redwoodblog

Vous obtenez ainsi un nouveau répertoire `redwoodblog` contenant plusieurs sous-répertoires et fichiers. Déplacez-vous dans ce répertoire, puis lancez le serveur de développement :

    cd redwoodblog
    yarn redwood dev

Votre navigateur web devrait se lancer automatiquement et ouvrir `http://localhost:8910` laissant apparaître la page d’accueil de Redwood. 

![Redwood Welcome Page](https://user-images.githubusercontent.com/300/73012647-97a43d00-3dcb-11ea-8554-42df29c36e4a.png)

> Mémoriser le numéro de port est très simple, comptez simplement: 8-9-10!

### Premier Commit

Maintenant que nous avons le squelette de notre application Redwood, c'est le bon moment pour enregistrer notre travail avec un premier commit... au cas où.

    git init
    git add .
    git commit -m 'Premier commit'

## Structure d'une application Redwood

Examinons maintenant les fichiers et répertoires qui ont été créés pour nous (laissons de côté les fichiers de configuration sur lesquels nous reviendrons plus tard)

```terminal
├── api
│   ├── prisma
│   │   ├── schema.prisma
│   │   └── seeds.js
│   └── src
│       ├── functions
│       │   └── graphql.js
│       ├── graphql
│       ├── lib
│       │   └── db.js
│       └── services
└── web
    ├── public
    │   ├── README.md
    │   ├── favicon.png
    │   └── robots.txt
    └── src
        ├── Routes.js
        ├── components
        ├── index.css
        ├── index.html
        ├── index.js
        ├── layouts
        └── pages
            ├── FatalErrorPage
            │   └── FatalErrorPage.js
            └── NotFoundPage
                └── NotFoundPage.js
```
Au premier niveau nous avons deux répertoires, `api` et `web`. Redwood sépare le backend (`api`) et le frontend (`web`) au sein du projet. ([Yarn qualifie cette séparation de "workspaces"](https://yarnpkg.com/lang/en/docs/workspaces/). Avec Redwood, on fait plutôt référence aux "côtés" web et api de l'application). Ainsi, lorsque plus tard vous serez amené à ajouter des packages, il vous faudra préciser dans quel côté ils doivent aller. Par exemple, (inutile d'exécuter ces commandes):

    yarn workspace web add marked
    yarn workspace api add better-fs

### Le Répertoire /api

A l'intérieur du répertoire `api` se trouve deux sous-répertoires :

- `prisma` contient du code d'infratructure relatif à la base de donnée

  - `schema.prisma` contient le schéma de la base de données (ses tables et ses colonnes)
  - `seeds.js` est utilisé pour initialiser la base de données avec les données de base nécessaire à votre application (utilisateur admin, configuration diverses..).

  Lorsque nous aurons créé notre première table dans la base de données, nous trouverons également à cet endroit une base de données SQLite sous la forme d’un fichier `dev.db`, ainsi qu’un répertoire `migrations` contenant des captures successives du schéma au fil de son évolution.

- `src` contient l'ensemble du code côté backend. `api/src` contient quatre répertoires supplémentaires :
  - `functions` contiendra toutes les [fonctions lambda](https://docs.netlify.com/functions/overview/) utilisées par votre application en plus du fichier `graphql.js` généré automatiquement par Redwood. Ce dernier fichier est requis pour utiliser une API GraphQL.
  - `graphql` contient votre schéma GraphQL écrit au format SDL (Schema Definition Language). Les fichiers SDL se terminent par `.sdl.js`.
  - `lib` contient un seul fichier, `db.js`, qui instancie le client Prisma utilisé pour dialoguer avec la base de données. Vous pouvez parfaitement personnaliser ce fichier en ajoutant des options supplémentaires. Vous pouvez utiliser ce répertoire pour tout code relatif au côté API de votre application qui ne trouverai pas sa place dans `functions` ou `services`.
  - `services` contient la logique métier de votre application. Lorsque vous effectuez une requête ou une mutation de données via GraphQL, ce code se trouve ici dans un format réutilisable depuis d’autres endroits de votre application.

Et nous en avons terminé avec la partie backend.

### Le répertoire /web

- `src` contient plusieurs sous-répertoires :
  - `components` contient vos composants React traditionnels ainsi que les _Cells_ introduites par Redwood (nous y reviendrons bientôt en détail).
  - `layouts` contient du code HTML sous forme de composants qui viennent entourer le contenu de votre application et sont partagés par les différentes _Pages_.
  - `pages` contient des composants souvent insérés dans les _Layouts_ et qui constituent les points d'entrées de votre application pour une URL donnée (une URL comme `/articles/hello-world` correspondra ainsi à une page tandis que `/contact-us` correspondra à une autre page). Chaque nouvelle application comprend deux pages par défaut :
    - `NotFoundPage.js` qui est utilisée lorsqu’aucune route n’est trouvée par le routeur (voir `Routes.js` plus bas).
    - `FatalErrorPage.js` qui est utilisée lorsqu’une erreur survient, qu’elle n’a pas été gérée, et qu’il n’est pas possible de poursuivre plus avant sans faire exploser l’application (en général il s’agit d’une page blanche).
- `public` contient des ressources non utilisées par vos composants React (En bout de chaîne, ces ressources seront copiées sans être modifiées dans le répertoire racine de l’application finale):
  - `favicon.png` est l’icône utilisée par les onglets des navigateurs lorsqu’une page est ouverte (par défaut il s’agit du logo RedwoodJS).
  - `robots.txt` est utilisé pour controller ce que les moteurs de recherche sont [autorisé à indexer](https://www.robotstxt.org/robotstxt.html).
  - `README.md` explique comment, et quand, utiliser le répertoire `public` pour vos ressources statiques. Il mentionne également les bonnes méthodes pour importer des ressources à l'intérieur des composants via Webpack. Vous pouvez également lire à ce sujet ce [fichier README.md sur GitHub](https://github.com/redwoodjs/create-redwood-app/tree/main/web/public).
- `index.css` est l'endroit par défaut où placer vos règles CSS. Il existe cependant d’autres possibilités avancées.
- `index.html` est le point d’entrée React standard de votre application.
- `index.js` contient le code de démarrage pour une application Redwood.
- `Routes.js` contient les définitions des routes de l’application afin de faire correspondre chaque URL à une _Page_.

## Notre Première Page

Donnons à nos utilisateurs quelque chose de plus à contempler que la page d'accueil de Redwood. Utilisons la commande `redwood` pour créer une première page :

    yarn redwood generate page home /

Cette commande fait les choses suivantes :

- Création de `web/src/pages/HomePage/HomePage.js`. Redwood prend le nom spécifié comme premier argument, le met en majuscules et le suffixe avec "Page" pour construire votre nouveau composant de type Page.
- Création d’un fichier de test du composant `web/src/pages/HomePage/HomePage.test.js` avec un simple test d’exemple à l’intérieur. Vous écrivez _toujours_ les tests de vos composants, _n’est-ce pas ??_
- Création d’un fichier Storybook `web/src/pages/HomePage/HomePage.stories.js`. Storybook est un outil formidable pour développer efficacement et organiser vos composants. Si vous souhaitez en savoir plus jetez un oeuil à ce [sujet sur le forum Redwood](https://community.redwoodjs.com/t/how-to-use-the-new-storybook-integration-in-v0-13-0/873) pour apprendre comment l’utiliser.
- Ajout d’une `<Route>` dans `web/src/Routes.js` qui fait correspondre le chemin `/` à la nouvelle page _HomePage_.

> **Import automatique des pages dans le fichier Routes**
>
> Si vous regardez dans Routes, vous constaterez mention d'un composant, `HomePage`, qui n'est présent nulle part ailleurs. Redwood importe automatiquement toutes les pages dans le fichier Routes puisque nous aurons besoin de toutes les référencer de toute façon. Cela permet de s'épargner un `import` massif qui viendrait encombrer le fichier Routes.

En réalité, cette page est déjà active (et votre navigateur l’a rechargée pour vous) :

![Default HomePage render](https://user-images.githubusercontent.com/300/76237559-b760ba80-61eb-11ea-9a77-b5006b03031f.png)

D’accord, ça ne flatte pas encore la rétine mais c’est un début! Ouvrez cette page dans votre éditeur, modifiez un peu le texte et sauvegardez. Votre navigateur devrait recharger la page avec vos modifications.

### Routing

Ouvrez `web/src/Routes.js` et observez la route qui vient d’être créée :

```html
<Route path="/" page={HomePage} name="home" />
```

Essayez de modifier cette route de la façon suivante:

```html
<Route path="/hello" page={HomePage} name="home" />
```

Dès que vous ajoutez votre première route, la page d'accueil par défaut de Redwood disparaît. Désormais, lorsqu'aucune route ne peut être trouvée pour l'URL demandée, Redwood va retourner la page `NotFoundPage`. Modifiez l'URL de votre navigateur pour ouvrir `http://localhost:8910/hello`, vous devriez voir de nouveau le contenu de `HomePage.js`.

Modifiez à nouveau la route pour revenir à son état initial `/` avant de continuer. 

## Une Seconde Page et un Lien

Ajoutons donc une page "About" à notre blog de manière à ce que personne n'ignore qui se trouve derrière cette application exceptionnelle. Nous allons créer une nouvelle page en utilisant `redwood`:

    yarn redwood generate page about

Remarquez que nous n'avons pas spécifié de chemin cette fois-ci, uniquement le nom de la page. En effet, si vous ne le précisez pas, la commande `redwood generate page` créera une `Route` en lui donnant pour chemin le nom de la page préfixé par un slash `/`. Dans le cas présent, ce sera donc `/about`. 

> **Fragmenter le code pour chaque page**
>
> Au fur et à mesure que vous ajoutez des pages à votre application, vous pouvez légitimement vous inquiéter du fait que le navigateur va devoir télécharger un volume initial de données toujours croissant. Soyez rassuré! Redwood va automatiquement fragmenter le code pour chaque page de telle façon que le chargement soit toujours extrêmement véloce. Vous pouvez donc créer autant de pages que vous le souhaitez sans vous inquiéter outre mesure de la taille finale du bundle webpack. Si, dans le cas contraire, vous souhaitez que certaines pages soient spécifiquement intégrées dans le bundle principal, il vous est possible de personaliser cette fonctionalité.

`http://localhost:8910/about` devrait maintenant pointer sur votre nouvelle page. Bien entendu, absolument personne ne va trouver cette page de votre blog en modifiant manuellement l'URL! Ajoutons donc un lien depuis la page d'accueil vers la page About, et vice-versa. Nous commencerons par créer un simple header et une barre de navigation dans `HomePage.js`:

```javascript{3,7-19}
// web/src/pages/HomePage/HomePage.js

import { Link, routes } from '@redwoodjs/router'

const HomePage = () => {
  return (
    <>
      <header>
        <h1>Redwood Blog</h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>A Propos</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>Home</main>
    </>
  )
}

export default HomePage
```

Remarquons ici plusieurs points :

- Redwood adore les "[Function Components](https://www.robinwieruch.de/react-function-component)". Nous ferons un usage fréquent des "[React Hooks](https://reactjs.org/docs/hooks-intro.html)" au fil de l'élaboration de notre blog, et ces derniers ne sont actifs que dans les "function components". Vous êtes libres d'utiliser des "class components", mais nous vous recommandons de les éviter sauf cas particulier.
- Les balises Redwood `<Link>`, dans leur usage le plus simple, prennent un seul attribut `to`. Cet attribut `to` appelle une "_named route function_" de façon à générer l'URL correcte. Cette fonction possède le même nom que l'attribut `name` présent sur la `<Route>`:

  `<Route path="/about" page={AboutPage} name="about" />`

  Si vous n'aimez pas le nom que la commande `redwood generate` utilise pour votre route, vous pouvez parfaitement le changer dans le fichier `Routes.js`! Les routes nommées sont extrêmement utiles car, si vous désirez modifiez le chemin associé avec une route, il vous suffit de le modifier dans le fichier `Routes.js` et immédiatement tous les liens qui utilisent cette route pointerons au bon endroit. Vous pouvez également passer directement une chaîne de caractères à l'attribut `to`, mais alors vous ne bénéficiez plus de ce mécanisme bien utile. 

### Retour à la maison

Une fois sur la page "About", nous n'avons aucun moyen de revenir en arrière. Pour y remédier, ajoutons également un lien à cet endroit:

```javascript{3,7-25}
// web/src/pages/AboutPage/AboutPage.js

import { Link, routes } from '@redwoodjs/router'

const AboutPage = () => {
  return (
    <>
      <header>
        <h1>Redwood Blog</h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>About</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>
        <p>
          Ce site est créé avec pour seule intention de démontrer la puissance créative de Redwood! Oui, c'est très 
          impressionant :D
        </p>
        <Link to={routes.home()}>Retour à la page d'accueil</Link>
      </main>
    </>
  )
}

export default AboutPage
```

Bien! Affichons cette page dans le navigateur and vérifions que nous pouvons aller et venir entre les différentes pages.

En tant que développeur de classe cosmique, vous avez probablement repéré ce copier-coller un peu lourd du `<header>`. Nous aussi. C'est la raison pour laquelle Redwood dispose d'un petite chose bien pratique appelé "_Layout_"."

## Layouts

Une façon de résoudre la duplication du `<header>` aurait pu être de créer un composant `<Header>` et l'inclure à la fois dans `HomePage` et `AboutPage`. C'est valide! Mais il y a beaucoup mieux... Dans l'idéal, votre code ne devrait comporter qu'une seule et unique balise `<header>`.

Lorsque vous regardez à ces deux pages, quelle est leur raison d'être principale? Toutes deux ont un peu de contenu à afficher. Toutes deux ne devraient pas avoir à connaître ce qui vient avant ce contenu (comme un `<header>`), ou après ce même contenu (comme un `<footer>`). C'est exactement ce que font les "Layouts": ils entourent une page dans un composant qui va ensuite afficher à l'intérieur le contenu de la page:

<img src="https://user-images.githubusercontent.com/300/70486228-dc874500-1aa5-11ea-81d2-eab69eb96ec0.png" alt="Diagramme de structure des Layouts" width="300">

Utilisons Redwood pour générer un layout contenant ce `<header>` :

    yarn redwood g layout blog

> **raccourci `generate`**
>
> Désormais nous utiliserons le raccourci `g` à la place de `generate`

Ce faisant, nous avons créé le fichier `web/src/layouts/BlogLayout/BlogLayout.js` et un son fichier de test associé. Nous appellerons ce dernier le "blog" layout car nous aurons certainement d'autres layout plus tard (un layout "admin" par exemple).

Supprimez ce `<header>` de `HomePage` et `AboutPage` et copier son contenu à l'intérieur du layout. Supprimons également le doublon de la balise `<main>` par la même occasion.

```javascript{3,7-19}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'

const BlogLayout = ({ children }) => {
  return (
    <>
      <header>
        <h1>Redwood Blog</h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>About</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>{children}</main>
    </>
  )
}

export default BlogLayout
```

`children` est l'endroit où la magie opère! Toute page passée en argument à un layout s'affiche là. Pour en revenir à `HomePage` et `AboutPage`, en les entourant simplement au sein du `<BlogLayout>`, nos deux pages ne font désormais que ce qu'elles sont supposées faire: afficher leur contenu. Nous pouvons maintenant supprimer les imports de `Link`et `Route` puisqu'ils figurent également dans le Layout.

```javascript{3,6}
// web/src/pages/HomePage/HomePage.js

import BlogLayout from 'src/layouts/BlogLayout'

const HomePage = () => {
  return <BlogLayout>Home</BlogLayout>
}

export default HomePage
```

```javascript{4,8-14}
// web/src/pages/AboutPage/AboutPage.js

import { Link, routes } from '@redwoodjs/router'
import BlogLayout from 'src/layouts/BlogLayout'

const AboutPage = () => {
  return (
    <BlogLayout>
        <p>
          Ce site est créé avec pour seule intention de démontrer la puissance créative de Redwood! Oui, c'est très 
          impressionant :D
        </p>
      <Link to={routes.home()}>Return home</Link>
    </BlogLayout>
  )
}

export default AboutPage
```

> **L'alias `src`**
>
> Remarquez que l'import utilise `src/layouts/BlogLayout` et non `../src/layouts/BlogLayout` ou `./src/layouts/BlogLayout`. Pouvoir se contenter d'ajouter uniquement `src` est un petit apport bien pratique de Redwood: `src` est un alias pour le chemin du répertoire `src` du workspace courant. En d'autres termes, lorsque vous travaillez dans `web`, `src` pointe vers `web/src`. Et lorsque vous travaillez dans `api` il pointe vers `api/src`. 

Revenez donc dans votre navigateur, et vous devriez alors voir...... rien de nouveau. Et c'est très bien! Votre layout fonctionne parfaitement.

> **Pourquoi certaines choses sont nommées d'une certaine façon?**
>
> Il est possible que vous ayez remarqué quelques répetitions dans le nom des fichiers utilisés par Redwood. Ainsi les pages se trouvent dans un répertoire appelé `/pages`, et contiennent de nouveau `Page` dans leur nom. Idem pour les Layouts. Pourquoi de choix?
>
> Lorsque vous avez des dizaines de fichiers ouverts dans votre éditeur de code, il est facile de se perdre. C'est d'autant plus le cas lorsque vous avez des fichiers aux noms similaires dans des répertoires différents. A l'usage, il nous est apparut que cette petite répetition dans les noms était au final bien pratique lorsqu'il s'agit de repérer un fichier précis parmi tous les onglets ouverts..
>
> Le plugin [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) peut également vous aider à distinguer les fichiers entre eux.
>
> <img src="https://user-images.githubusercontent.com/300/73025189-f970a100-3de3-11ea-9285-15c1116eb59a.png" width="400">

### Retour à la Maison, encore une fois

Ajoutons encore un autre `<Link>` de façon à ce que le titre et le logo pointent vers la page d'accueil:

```javascript{9-11}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'

const BlogLayout = ({ children }) => {
  return (
    <>
      <header>
        <h1>
          <Link to={routes.home()}>Redwood Blog</Link>
        </h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>About</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>{children}</main>
    </>
  )
}

export default BlogLayout
```

Enfin nous pouvons éliminer de la page About le lien "Retour à la page d'accueil" devenu superflu (ainsi que les imports `Link` et `routes` associés).

```javascript
// web/src/pages/AboutPage/AboutPage.js

import BlogLayout from 'src/layouts/BlogLayout'

const AboutPage = () => {
  return (
    <BlogLayout>
      <p>
        Ce site est créé avec pour seule intention de démontrer la puissance créative de Redwood! Oui, c'est très 
        impressionant :D
      </p>
    </BlogLayout>
  )
}

export default AboutPage
```

## Devenir Dynamique

La seconde partie du didacticiel est disponible en video ici:

<div class="relative pb-9/16">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/SP5vbsWf5Yg?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

Ces deux pages sont plutôt sympas, mais un blog sans article c'est tout de même un peu léger! Travaillons sur ce point à présent.

Pour les besoins de ce didacticiel, nous allons récupérer nos articles depuis la base de données. Puisque les bases de données relationelles sont encore aujourd'hui au coeur de beaucoup d'applications complexes (ou moins complexes d'ailleurs), nous avons fait en sorte de réserver un traitement de première classe aux accès SQL. Dans une application Redwood, tout part du schéma. 

### Créer le schéma de la base de données

Nous devons identifier quelles données seront nécessaires pour un article. Plus tard nous ajouterons d'autres éléments, mais pour commencer nous avons besoin de ceci:

- `ìd` l'identifiant unique pour un article (chaque table de notre base de données aura également un identifiant tel que celui-ci)
- `title` le titre de l'article
- `body` le contenu de l'article
- `createdAt` un 'timestamp' correspondant au moment où l'article est enregistré dans la base de données

Nous utilisons [Prisma Client JS](https://github.com/prisma/prisma-client-js) pour parler vac la base de données. Prisma possède aun autre librairie, appellée [Migrate](https://github.com/prisma/migrate), qui nous permet de mettre à jour le schéma de la base de données en capturant chaque changement successif. Chacun de ces changement est appelé _migration_, et cette librairie Migrate en créé un nouveau à chaque modification du schéma.  

Tout d'abord, définissons la structure d'un article de notre blog dans la base de données. Ouvrez `api/prisma/schema.prisma` et ajoutez la définition de la table `Post` (supprimez au passage tous les modèles présents par défaut dans ce fichier). Une fois terminé, le fichier se présente ainsi: 

```plaintext{13-18}
// api/prisma/schema.prisma

datasource DS {
  provider = "sqlite"
  url      = env("DATABASE_URL")
}

generator client {
  provider      = "prisma-client-js"
  binaryTargets = "native"
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  body      String
  createdAt DateTime @default(now())
}
```

Cette série d'instructions signifie que nous voulons créer une table `Post` avec les éléments suivants:

- Un champ `id` de type `Int`, nous précisions à Prisma que cette colonne constitue un identifiant `@id` (de façon à pouvoir créer des relations avec d'autres tables) et que la valeur par `@default` correspond à la fonction Prisma `autoincrement()` impliquant que la base de données insèrera une nouvelle valeur automatiquement lorsqu'un enregistrement est créé.
- Un champ `title` de type `String`
- Un champ `body` également de type `String`
- Un champ `createdAt` de type `DateTime` avec une valeur par `@default` égale à `now()` pour chaque nouvel enregistrement (ainsi nous n'avons pas à nous en charger dans l'application, la base de données le fera pour nous)

> **Identifiant de type Integer vs. identifiant de type String**
>
> Pour le didacticiel, nous resterons simple et utiliserons un identifiant de type Integer. Ceci étant, une application plus évoluée pourra utiliser un identifiant de type CUID ou UUID. Tous deux sont pris en charge par Prisma. Dans ce cas, vous utiliseriez un champ de type `String` au lieu de `Int`, et `cuid()` ou `uuid()` au lieu de `autoincrement()`:
>
> `id String @id @default(cuid())`
>
> Notez que l'utilisation d'un identifiant de type Integer permet d'obtenir des url plus simples comme https://redwoodblog.com/posts/123 instead of https://redwoodblog.com/posts/eebb026c-b661-42fe-93bf-f1a373421a13. 
>
> Allez voir la [documentation officielle de Prisma](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-schema/data-model#defining-an-id-field) pour plus de détails sur les champs identifiants.

### Migrations

Bon, la création du schéma : c'est fait! Maintenant ce que nous vonlons c'est capturer son état pour en faire une _migration_:

    yarn redwood db save create posts

Ce faisant, vous venez de nommer votre première migration "create posts". Redwood ne tient pas compte de ce nom, mais il est recommandé de choisir un nom significatif pour les autres développeurs de votre équipe.

Une fois la commande exécutée, vous pourrez constater la création d'un nouveau sous-répertoire dans `api/prisma/migrations` avec un _timestamp_ et le nom que vous avez donné votre migration. Ce sous-répertoire contient quelques fichiers: une capture du schéma de la base dans `schema.prisma`, ainsi que la suite de directives que Prima utilise pour effectuer les modifications dans `steps.json`).

Nous allons maintenant appliquer cette migration avec cette commande:

    yarn rw db up

> **Raccourçi `redwood`**
>
> Désormais, nous utiliserons dans nos commandes la forme courte `rw` à la place de `redwood`.

L'exécution de cette commande permet à Prisma d'appliquer les changements sur la base de données, en l'espèce la création d'une nouvelle table `Post` avec les champs définis plus haut.

### Créer une Interface d'Édition d'un Article

Nous n'avons pas encore décidé du look de notre site, mais ne serait-il pas extra si nous pouvions commencer à manipuler nos articles de blog, commencer à créer quelques pages rapidement le temps que l'équipe chargée du design rende sa copie? Heureusement pour nous, "Incroyable" est le petit nom de Redwood :)

Générons tout ce sont nous avons besoin pour réaliser un CRUD (Create, Retrieve, Update, Delete) (Créer, Récupérer, Mettre à jour, Supprimer) sur nos articles. Redwood a justement un generateur spécialement fait pour ça :

    yarn rw g scaffold post

Ouvrons la page `http://localhost:8910/posts` et constatons le résultat:

<img src="https://user-images.githubusercontent.com/300/73027952-53c03080-3de9-11ea-8f5b-d62a3676bbef.png" />

Humm.. ça n'est pas beaucoup plus que ce que nous avions obtenu losque nous avions créé notre première page. Que se passe-t-il lorsque nous cliquons sur le bouton "New Post" (Nouvel Article) ?

<img src="https://user-images.githubusercontent.com/300/73028004-72262c00-3de9-11ea-8924-66d1cc1fceb6.png" />

Ah, maintenant on commence à parler sérieusement! Remplissez donc les champs _title_ (titre) et _body_ (contenu), puis cliquez sur "Save" pour enregistrer.

<img src="https://user-images.githubusercontent.com/300/73028757-08a71d00-3deb-11ea-8813-046c8479b439.png" />

Venons-nous bien de créer un nouvel article? Exactement! Essayez-donc d'en créer d'autres.

<img src="https://user-images.githubusercontent.com/300/73028839-312f1700-3deb-11ea-8e83-0012a3cf689d.png" />

Et maintenant, que se passe-t-il lorsqu'on clique sur "Edit" (éditer) pour l'un de ces articles?

<img src="https://user-images.githubusercontent.com/300/73031307-9802ff00-3df0-11ea-9dc1-ea9af8f21890.png" />

D'accord, et en cliquant sur le bouton "Delete" (supprimer)?

<img src="https://user-images.githubusercontent.com/300/73031339-aea95600-3df0-11ea-9d58-475d9ef43988.png" />

Oui c'est bien ça, en une seule commande, Redwood à créé l'ensemble des pages, composants et services nécessaires aux opérations usuelles de manipulation des articles. Pas même besoin d'ouvrir le gestionnaire de base de données. Redwood appelle ceci des _scaffolds_. Pas mal, non?

Voici dans le détail ce qui arrive lorsqu'on execute la commande `yarn rw g scaffold post` : 

- Ajout d'un fichier _SDL_ pour définir quelques requêtes et mutations GraphQL dans `api/src/graphql/posts.sdl.js` 
- Ajout d'un fichier _service_ `api/src/services/posts/posts.js` qui permet au client Javascript Prisma de manipuler la base de données
- Ajout de quelques _pages_ dans `web/src/pages`:  
  - `EditPostPage` pour éditer un article
  - `NewPostPage` pour créer un nouvel article
  - `PostPage` pour montrer les détails d'un article
  - `PostsPage` pour lister tous les articles
- Ajout de _routes_ pour ces nouvelles pages dans `web/src/Routes.js`
- Ajout de trois _cells_ dans `web/src/components`:
  - `EditPostCell` cellule permettant de récupérer un article pour l'éditer
  - `PostCell` cellule permettant de récupérer un article pour l'afficher
  - `PostsCell` cellule permettant de récupérer tous les articles
- Ajout de quatre _composants_ également dans `web/src/components`:
  - `NewPost` affiche le formulaire permettant la création d'un nouvel article
  - `Post` affiche un article en particulier
  - `PostForm` le formulaire utilisé à la fois par les composants de création et d'édition d'un aricle 
  - `Posts` affiche la table avec l'ensemble des articles

> **Générateurs et conventions de nommage**
>
> Vous remarquerez que certains fichiers générés ont un nom au pluriel, et d'autres au singulier. Cette convention est empruntée au framework Ruby on Rails. Lorsque vous avez à traiter d'un multiple de quelque chose (comme par exemple une liste d'articles), on utilisera le pluriel. Dans le cas contraire (par exemple la création d'un nouvel article), on utilisera le singulier. C'est aussi plus naturel lorsque l'on parle: "montre moi une liste d'articles" vs. "je vais créer un nouvel article".
>
> Pour ce qui concerne les générateurs:
>
> - Les fichiers de Services sont toujours au pluriel.
> - Les méthodes dans les Services sont au singulier ou au pluriel selon qu'ils retournent plusieurs articles ou un seul article (`posts` vs. `createPost`).
> - les fichiers SDL sont toujours au pluriel.
> - Les pages générées par une commande de scaffold sont au pluriel ou au singulier selon que la page manipule plusieurs ou un seul article. Notez que lorsque vous utilisez vous-même un commande `page` en dehors d'un scaffold, le nom utilisé sera simplement celui que vous donnerez.
> - Les Layouts utilisent le nom que vous leur donnez
> - Les composants et les cellules sont au pluriel ou au singulier selon le contexte lorsqu'ils sont générés par scaffolding. Dans le cas contraire, ils utilisent simplement le nom que vous leur donnez.
>
> Remarquez également que seul le nom de la table en base de données et au singulier ou au pluriel, et pas le mot complet. Ainsi on a `PostsCell`, et non `PostCells`. 
>
> Vous n'avez pas à suivre cette convention de façon obligatoire lorsque vous créez vos propres composants, pages, etc... Ceci étant nous vous le recommandons chaudement. Au bout du compte, la communauté Ruby on Rails a fini par s'attacher à cette convention, et ce même si au départ de nombreuses personnes s'y étaient opposées. "[Give it five minutes](https://signalvnoise.com/posts/3124-give-it-five-minutes)" comme disent les anglo-saxons.

### Créer la page d'accueil

Nous pouvons commencer à remplacer ces pages les unes après les autres au fur et à mesure que l'équipe chargée du design nous donne des éléments, ou bien nous pouvons simplement les déplacer dnas la partie "administration" de notre site, et commencer à créer nos propres pages. Ceci étant, la partie publique du site ne va certainement pas autoriser les utilisateurs à créer, éditer ou supprimer les articles. Que peuvent donc faire les utilisateurs?

1. Voir la liste des articles (sans liens pour éditer ou supprimer)
2. Voir le détail d'un article

Puisque nous voudront probablement conserver un moyen de créer et éditer des articles plus tard, conservons les pages générées par scaffolding et créons-en de nouvelles pour ces deux cas de figure.

Nous avons déjà la `HomePage`, pas besoin de créer celle-ci donc. Nous souhaitons afficher une liste d'articles à l'utilisateur donc nous allons devoir ajouter ça. Nous avons besoin de récupérer le contenu depuis la base de données, et nous ne voulons pas que l'utilisateur soit face à une page blanche le temps du chargement (conditions réseau dégradées, serveur géographiquement distant, etc...), donc nous voudrons montrer une sorte de message de chargement et/ou une animation. D'autre part, si une erreur se produit, nous devrons faire en sorte de la prendre en charge. Enfin, nous devrons également prendre en compte le cas où le blog ne contient encore aucun article. 

Wow... notre première page et il semble que nous ayons déjà à nous inquiéter de tant de choses... mais est-ce véritablement le cas ? 

## Cells

Ce que nous cherchons à faire ici constituent en réalité des objectifs partagés par la plupart des applications web. Nous voulions voir s'il était possible de faciliter la vie aux développeurs. Nous pensons être arrivé à réaliser quelque chose d'utile. Nous appelons ça les _Cells_ (ou _cellules_ en français). Les Cells proposent une approche simple et déclarative pour récupérer des données au sein de vos composants. (Vous pouvez lire la documentation complète à propos des Cells. You can read the full documentation about Cells [ici](https://redwoodjs.com/docs/cells).

Lorsque vous créez une nouvelle Cell, vous exportez quelques constantes, toujours nommées de façon identique, et Redwood s'appuie dessus pour mettre en place la mécanique. Une Cell ressemble typiquement à ceci:

```javascript
export const QUERY = gql`
  query {
    posts {
      id
      title
      body
      createdAt
    }
  }
`

export const Loading = () => <div>Chargement...</div>

export const Empty = () => <div>Aucun article disponible!</div>

export const Failure = ({ error }) => (
  <div>Erreur lors du chargement des articles: {error.message}</div>
)

export const Success = ({ posts }) => {
  return posts.map((post) => (
    <article>
      <h2>{post.title}</h2>
      <div>{post.body}</div>
    </article>
  ))
}
```

Lorsque React affiche ce composant, Redwood va:

- Exécuter la requête `QUERY` et afficher le composant `Loading` jusqu'à ce qu'une réponse soit reçue
- Lorsque la requête retourne une réponse, il va afficher un des trois états suivants:
  - S'il y a eu une erreur, le composant `Failure`
  - Si aucune donnée n'est retournée (c'est à dire `null` ou un tableau vide), le composant `Empty`
  - Dans le cas contraire (ni erreur, ni vide), le composant `Success`

Il existe également quelques outils supplémentaire pour générer le cycle de vie du composant comme `beforeQuery` (pour manipuler les propriétés passées à `QUERY`) et `afterQuery` (pour manipuler les données retournées par GraphQL avant qu'elles ne soient transmises au composant `Success`)

Le minimum dont vous avez besoin pour une Cell sont les exports `QUERY` et `Success`. Si vous n'exportez pas `Empty`, `Success` recevra les données vides. Si vous n'exportez pas `Failure`, les éventuelles erreurs seront envoyées à la console.

Pour déterminer dans quels cas utiliser les Cells, gardez en tête qu'elles sont utiles lorsque vos composants ont besoin de récupérer des données depuis la base, ou depuis tout autre service qui pourrait avoir un délai de réponse. Laissez Redwood se charger de jongler avec les états, de manière à pouvoir porter votre attention sur le comportement attendu de vos composants correctement affichés avec leur données.

### Notre Première Cell

La page d'accueil affichant une liste d'articles est un candidat parfait pour réaliser notre première cellule. Naturellement, nous avons prévu un générateur pour ça:

    yarn rw g cell BlogPosts

L'exécution de cette commande provoque la création d'un nouveau fichier `/web/src/components/BlogPostsCell/BlogPostsCell.js` (et son fichier de test associé) avec un peu de code par défaut pour vous faciliter la tâche:

```javascript
// web/src/components/BlogPostsCell/BlogPostsCell.js

export const QUERY = gql`
  query BlogPostsQuery {
    blogPosts {
      id
    }
  }
`

export const Loading = () => <div>Loading...</div>

export const Empty = () => <div>Empty</div>

export const Failure = ({ error }) => <div>Error: {error.message}</div>

export const Success = ({ blogPosts }) => {
  return JSON.stringify(blogPosts)
}
```
> Lorsque vous utilisez le générateur, vous pouvez employer le type de casse qui vous plaît. Redwood fera en sorte de s'adapter pour créer une cellule avec un nom de fichier correct. Ainsi toutes les commandes ci-dessous aboutissent à créer un fichier avec le même nom:
>
>     yarn rw g cell blog_posts
>     yarn rw g cell blog-posts
>     yarn rw g cell blogPosts
>     yarn rw g cell BlogPosts
>
> Vous devez juste pensez à indiquer d'une façon ou d'une autre que vous utilisez plusieurs mots. Appeler `yarn redwood g cell blogposts` sans utiliser aucune casse pour séparer "blog" et "posts" va générer un fichier `web/src/components/BlogpostsCell/BlogpostsCell.js`.  

Pour vous aider à être efficace, le générateur suppose que vous utiliserez une requête racine GraphQL nommées de la même façon que votre Cell et écrit pour vous une requête minimale pour récupérer des données depuis la base. Dans le cas présent, la requête a donc été nommée `blogPosts`. Cependant, ce nom de requête n'est pas valide par rapport à ce qui a déjà été créé dans nos fichiers SDL et Service. Nous devons donc renommer `blogPosts` en `posts` à la fois dans le nom de la requête GraphQL et dans la propriété passée à `Success`: 

```javascript{5,17,18}
// web/src/components/BlogPostsCell/BlogPostsCell.js

export const QUERY = gql`
  query BlogPostsQuery {
    posts {
      id
    }
  }
`

export const Loading = () => <div>Loading...</div>

export const Empty = () => <div>Empty</div>

export const Failure = ({ error }) => <div>Error: {error.message}</div>

export const Success = ({ posts }) => {
  return JSON.stringify(posts)
}
```

Insérons cette Cell dans notre `HomePage` et voyons ce qui se passe:

```javascript{4,9}
// web/src/pages/HomePage/HomePage.js

import BlogLayout from 'src/layouts/BlogLayout'
import BlogPostsCell from 'src/components/BlogPostsCell'

const HomePage = () => {
  return (
    <BlogLayout>
      <BlogPostsCell />
    </BlogLayout>
  )
}

export default HomePage
```

Le navigateur devrait en principe montrer un tableau avec un peu de contenu (en supposant que vous ayez créé un article à l'étape du [scaffolding](/tutorial/getting-dynamic#creating-a-post-editor) un peu plus tôt). Impeccable!

<img src="https://user-images.githubusercontent.com/300/73210519-5380a780-40ff-11ea-8639-968507a79b1f.png" />

> **Dans le composant `Success`, d'où vient donc `posts`?**
>
> Remarquez que dans le composant `QUERY`, nous avons nommée notre requête `posts`. Quelque soit le nom de la requête, ce sera le nom de la propriété qui sera transmise au composant `Success` et qui  contiendra vos données. Vous pouvez toutefois créer un alias de la façon suivante:  
>
> ```javascript
> export const QUERY = gql`
>   query BlogPostsQuery {
>     postIds: posts {
>       id
>     }
>   }
> `
> ```
>
> De cette manière la propriété `postIds` sera transmise à `Success` au lieu de `posts`

En plus de l'identifiant `id` qui a été ajouté dans `QUERY` par le générateur, récupérons également le titre, le contenu et la date de création de l'article:

```javascript{7-9}
// web/src/components/BlogPostsCell/BlogPostsCell.js

export const QUERY = gql`
  query BlogPostsQuery {
    posts {
      id
      title
      body
      createdAt
    }
  }
`
```

La page devrait désormais afficher un dump de l'ensemble des données pour tous les articles enregistrés:

<img src="https://user-images.githubusercontent.com/300/73210715-abb7a980-40ff-11ea-82d6-61e6bdcd5739.png" />

`Success` est ni plus ni moins qu'un bon vieux composant React, vous pouvez donc le modifier simplement pour afficher chaque article dans un format un peu plus sympa et lisible:

```javascript{4-12}
// web/src/components/BlogPostsCell/BlogPostsCell.js

export const Success = ({ posts }) => {
  return posts.map((post) => (
    <article key={post.id}>
      <header>
        <h2>{post.title}</h2>
      </header>
      <p>{post.body}</p>
      <div>Créé le: {post.createdAt}</div>
    </article>
  ))
}
```

Et ce faisant, nous avons maintenant notre blog! Ok, à ce stade c'est encore le plus basique et hideux blog jamais vu sur Internet.. mais c'est déjà quelque chose! (Pas d'inquiétude, nous avons encore un tas de fonctionnalités à ajouter)

<img src="https://user-images.githubusercontent.com/300/73210997-3dbfb200-4100-11ea-847a-602cbf59cb2a.png" />

### Résumé

Pour résumer, qu'avons nous réalisé jusqu'ici ?

1. Génération de la page d'accueil
2. Génération du Layout pour notre blog
3. Définition du schéma de la base de données
4. Application d'une migrations pour mettre à jour la base de données et créer une table
5. Réalisation d'un Scaffold pour créer une interface CRUD sur la table
6. Création d'une Cell pour charger les donner et gérer les états "loading", "empty", "failure" et enfin "success". 
7. Ajout de la Cell à notre page d'accueil

En réalité, cette différentes étapes sont ni plus ni moins ce qui deviendra votre façon habituelle d'ajouter de nouvelles fonctionnalités dans une application Redwood.

Jusqu'ici, hormis un peu de code HTML, nous n'avons pas écrit grand chose à la main. En particulier, nous n'avons pratiquement pas eu à écrire de code pour récupérer les données depuis la base. Le développement web s'en trouve facilité et devient même agréable, qu'en pensez-vous?

## Quête secondaire: Fonctionnement de Redwood avec les Données

Redwood apprécie GraphQL. Nous pensons qu'il s'agit de l'API pour l'avenir. Notre implémentation de GraphQL is construite avec [Apollo](https://www.apollographql.com/). Voici comment une requête GraphQL classique fonctionne dans votre application: 

![Redwood Data Flow](https://user-images.githubusercontent.com/300/75402679-50bdd180-58ba-11ea-92c9-bb5a5f4da659.png)

La partie frontend de l'application s'appuie sur [Apollo Client](https://www.apollographql.com/docs/react/) pour créer une requête GraphQL. Celle-ci est ensuite envoyée à [Apollo Server](https://www.apollographql.com/docs/apollo-server/) qui s'exécute dans une fonction lambda AWS serverless.  

Les fichiers `*.sdl.js` qui se trouvent dans le répertoire `api/src/graphql` définissent les types GraphQL [Object](https://www.apollographql.com/docs/tutorial/schema/#object-types), [Query](https://www.apollographql.com/docs/tutorial/schema/#the-query-type) et [Mutation](https://www.apollographql.com/docs/tutorial/schema/#the-mutation-type) et donc l'interface de votre API.

En principe, vous devriez écrire une "[resolver map](https://www.apollographql.com/docs/tutorial/resolvers/#what-is-a-resolver)" qui contiendrait l'ensemble de vos "resolvers" de façon à ce qu'Apollo sache comment les brancher à vos fichiers SDL. Cependant, inscrire votre logique métier directement dans votre "resolver map" aurait pour conséquence la création d'un énorme fichier ne favorisant pas la réutilisation. Vous pourriez également extraire toute cette logique dans une librairie de fonctions que vous importeriez et appelleriez depuis votre "resolver map", en ayant toutefois à vous rappeller de passer tous les arguments nécessaires. Humm.. c'est beaucoup d'efforts pour au final une masse de code de toute façon peu réutilisable.

Redwood s'y prend autrement! Voos rappellez-vous le répertoire `api/src/services`? Redwood va automatiquement importer et brancher vos "resolvers" depuis les **services** vers vos fichiers SDL. Dans le même temps, Redwood vous permet d'écrire vos "resolvers" de façon à ce qu'ils soient facilement appellés comme de simples fonctions depuis d'autres "resolvers" ou d'autres services. Cela fait pas mal de choses étonnantes à intégrer, il est temps de passer à un exemple.

Observez donc le morceau de code SDL javascript suivant :

```javascript
// api/src/graphql/posts.sdl.js

export const schema = gql`
  type Post {
    id: Int!
    title: String!
    body: String!
    createdAt: DateTime!
  }

  type Query {
    posts: [Post!]!
    post(id: Int!): Post!
  }

  input CreatePostInput {
    title: String!
    body: String!
  }

  input UpdatePostInput {
    title: String
    body: String
  }

  type Mutation {
    createPost(input: CreatePostInput!): Post!
    updatePost(id: Int!, input: UpdatePostInput!): Post!
    deletePost(id: Int!): Post!
  }
`
```

A partir de ce fichier SDL, Redwood va aller chercher les cinq "resolvers" suivants dans `api/src/services/posts/posts.js` :

- `posts()`
- `post({id})`
- `createPost({input})`
- `updatePost({id, input})`
- `deletePost({id})`

Pour implémenter ces cinq "resolvers", il vous suffit de les exporter depuis vos fichiers services. Vos resolvers vont habituellement récupérer les données depuis une base de données, mais en réalité ils peuvent faire ce que vous souhaitez du moment qu'ils retournent le type de données qu'Apollo s'attend à recevoir comme défini dans `posts.sdl.js`. 

```javascript
// api/src/services/posts/posts.js
import { db } from 'src/lib/db'

export const posts = () => {
  return db.post.findMany()
}

export const post = ({ id }) => {
  return db.post.findOne({
    where: { id },
  })
}

export const createPost = ({ input }) => {
  return db.post.create({
    data: input,
  })
}

export const updatePost = ({ id, input }) => {
  return db.post.update({
    data: input,
    where: { id },
  })
}

export const deletePost = ({ id }) => {
  return db.post.delete({
    where: { id },
  })
}
```

> Apollo suppose que ces fonctions retournent des "promises", ce que `db` fait parfaitement. `db` est une instance de `PrismaClient`. Apollo attend sagement que ces promises s'achèvent avant de répondre avec le résultat de vos requêtes. De cette manière, vous n'avez pas à gérer vous-même les `async`/`await`, ou autres callbacks. 

Vous êtes parfaitement fondé à vous interroger sur la raison pour laquelle nous appelons ces fichiers des "services". Bien que le blog que nous construisons ensemble ne soit pas assez complexe pour le montrer, les services sont conçus pour être une abstraction qui couvre **plus** qu'une simple table de la base de données. Une application plus avancée pourrait par exemple avoir un service nommé "facturation" qui reposerait à fois sur les tables `transactions` et `souscriptions`. Certaines des fonctionnalités de ce service pourraient être exposées via GraphQL, mais pas forcément toutes. 

Vous n'avez pas besoin d'exposer chaque fonction de votre service via GraphQL. Si vous ne les déclarez pas dans dans vos types `Query` ou `Mutation`, ils n'existerons tout simplement pas pour GraphQL. Mais vous pourrez toujours les utiliser vous-même. Les services ne sont ni plus ni moins que des fonctions javascript que vous pouvez utiliser où bon vous semble :

- Depuis un autre service
- Dans une autre fonction lambda créée par vous-même
- Depuis une autre API, complètement séparée

En organisant votre application autour de services bien définis, et en proposant une API pour chacun de ces services (à la fois pour un usage interne, **et** pour GraphQL), vous contribuerez naturellement à respecter la règle dite de ["separation of concerns"](https://fr.wikipedia.org/wiki/S%C3%A9paration_des_pr%C3%A9occupations) (SoC). Selon toute probabilité, cela vous permettra de favoriser la maintenance de votre code dans le temps.

Revenons-en à notre flux de données: Apollo a créé un "resolver" qui, dans notre cas, récupère les données depuis une base de données. Apollo reconstruit l'objet en ne retournant que les couples clé/valeur demandés dans la requête GraphQL. Enfin, Apollo emballe la réponse au format GraphQL et la retourne au navigateur.

Si vous utilisez une **Cell** Redwood, vos données seront dès lors disponible dans votre compsant `Success`, prêtes à être affichées comme avec n'importe quel composant React.

## Paramètres de Routes

Maintenant que notre page d'accueil liste l'ensemble des articles de notre blog, il est temps de créer une page présentant le détail d'un article. Commençons par générer une page et sa route associée:

    yarn rw g page BlogPost

> Remarquez que nous ne pouvons pas nommer cette page `Post` car une autre page homonyme a déjà été crée lors de notre précédente démonstration du scaffolding.

Pour chaque article listé sur la page d'accueil, ajoutons un lien qui pointe vers notre nouvelle page (sans oublier au passage les imports pour `Link` et `routes`):

```javascript{3,12}
// web/src/components/BlogPostsCell/BlogPostsCell.js

import { Link, routes } from '@redwoodjs/router'

// QUERY, Loading, Empty and Failure definitions...

export const Success = ({ posts }) => {
  return posts.map((post) => (
    <article key={post.id}>
      <header>
        <h2>
          <Link to={routes.blogPost()}>{post.title}</Link>
        </h2>
      </header>
      <p>{post.body}</p>
      <div>Créé le: {post.createdAt}</div>
    </article>
  ))
}
```

Si vous cliquez sur le lien, vous deviez voir s'afficher un peu de texte issu de `BlogPostPage`. Mais ce dont nous avons vraiment besoin, c'est de pouvoir préciser _quel_ article nous souhaitons afficher. Ce que nous cherchons a obtenir en définitive, c'est une URL du type `/blog-post/1`. Pour cela, nous allons dire au routeur que notre url comporte une partie variable supplémentaire:

```html
// web/src/Routes.js

<Route path="/blog-post/{id}" page={BlogPostPage} name="blogPost" />
```

Notez l'ajout de `{id}` dans notre route. Redwood nomme ceci un _paramètre de route_. Ces paramètres de route signifie la chose suivante: "quelque soit la valeur à cette position, elle sera référencée par le nom utilisé entre les accolades".

Cool, cool, cool. Maintenant, nous devons donc construire un lien qui possède cet identifiant:

```html
// web/src/components/BlogPostsCell/BlogPostsCell.js

<Link to={routes.blogPost({ id: post.id })}>{post.title}</Link>
```

Pour les routes avec paramètres, un objet est attendu pour chaque paramètre. Si vous cliquez sur le lien d'un article, vous constaterez qu'en effet il pointe désormais vers `/blog-post/1` (ou `/blog-post/2`, etc... selon l'article).

### Utilisation des Paramètres

OK, donc l'identifiant se trouve bien dans l'URL. Et maintenant que fait-t-on pour afficher le bon article? On dirait bien que nous allons devoir récupérer les données depuis la base. Vous l'aurez compris, c'est le bon moment pour utiliser une Cell:

    yarn rw g cell BlogPost

Nous allons ensuite utiliser cette Cell dans notre page `BlogPostPage` (et pendant que nous y sommes, nous insèrerons notre page dans notre Layout `BlogLayout`):

```javascript
// web/src/pages/BlogPostPage/BlogPostPage.js

import BlogLayout from 'src/layouts/BlogLayout'
import BlogPostCell from 'src/components/BlogPostCell'

const BlogPostPage = () => {
  return (
    <BlogLayout>
      <BlogPostCell />
    </BlogLayout>
  )
}

export default BlogPostPage
```

Maintenant, à l'intérieur de notre Cell, nous avons besoin d'accéder à ce paramètre de route `{id}` qui contient l'identifiant de notre article en base de données. Pour ce faire, mettons à jour la requête de façon à ce qu'elle accepte une variable en entrée. Modifions également le nom de la requête `blogPost` en `post`.

```javascript{4,5,7-9,20,21}
// web/src/components/BlogPostCell/BlogPostCell.js

export const QUERY = gql`
  query BlogPostQuery($id: Int!) {
    post(id: $id) {
      id
      title
      body
      createdAt
    }
  }
`

export const Loading = () => <div>Loading...</div>

export const Empty = () => <div>Empty</div>

export const Failure = ({ error }) => <div>Error: {error.message}</div>

export const Success = ({ post }) => {
  return JSON.stringify(post)
}
```

Okay, on approche du but! Ceci étant, d'où vient donc ce `$id`? Redwood a plus d'un tour dans son sac. Chaque fois que vous ajoutez un paramètre de route, ce paramètre est automatiquement accessible dans la page qui correspond. Ce qui signifie que vous pouvez modifier la page `BlogPostPage` de la façon suivante:

```javascript{3,6}
// web/src/pages/BlogPostPage/BlogPostPage.js

const BlogPostPage = ({ id }) => {
  return (
    <BlogLayout>
      <BlogPostCell id={id} />
    </BlogLayout>
  )
}
```

`id` existe déjà sans effort supplémentaire puisque nous avons nommé notre paramètre de route `{id}`. Merci qui? Merci Redwood! Mais comment se fait-il que cet `id` finisse par devenir un paramètre GraphQL `$id`? Redwood s'en charge également pour vous! Par défaut, chaque propriété que vous donnez à une Cell devient automatiquement un variable disponible pour une requête GraphQL. Incroyablement simple, et pourtant vrai :)

D'ailleurs on peut le prouver! Essayez maintenant d'aller voir un article and — ... uh oh. Hmm:

![image](https://user-images.githubusercontent.com/300/75820346-096b9100-5d51-11ea-8f6e-53fda78d1ed5.png)

> Au passage le code d'erreur que vous voyez s'afficher provient de la section `Failure` de votre Cell!

Si vous examinez la console de votre navigateur, vous constaterez la présence d'une erreur GraphQL:

    [GraphQL error]: Message: Variable "$id" got invalid value "1";
      Expected type Int. Int cannot represent non-integer value: "1",
      Location: [object Object], Path: undefined

Il s'avère que les paramètres de route sont extraits des URL sous la forme de chaînes de caractères, et dans le cas présent GraphQL s'attend à recevoir un identifiant sous la forme d'un entier. Nous pourrions simplement utiliser la fonction javascript `parseInt()` afin de convertir notre paramètre de route vers un entier avant de le passer à `BlogPostCell`. Mais honnêtement, on peut faire bien mieux que ça! 

### Paramètres de Route Typés

Et si vous aviez la possibilité de demander cette conversion directement dans le chemin de la route? Et bien devinez-quoi, vous pouvez! Redwood appelle ça les **paramètres de route typés** ("route param types" en anglais). Et c'est aussi simple que d'ajouter `:Int` à notre paramètre de route:
What if you could request the conversion right in the route's path? Well, guess what: you can! Introducing **route param types**. It's as easy as adding `:Int` to our existing route param:

```html
// web/src/Routes.js

<Route path="/blog-post/{id:Int}" page={BlogPostPage} name="blogPost" />
```

Voilà! Non seulement vous allez convertir sans effort le paramètre `id` en un entier avant de la passer à votre Page, mais en bonus vous faîtes en sorte que la route n'applique que si `id` représente effectivement un entier, c'est à dire une suite de chiffres. Dans le cas contraire, le routeur essaiera d'autres routes. S'il ne s'en trouve aucune à s'appliquer, le routeur affichera la page `NotFoundPage`.

> **Que se passe-t-il si je veux passer d'autres propriétés à ma Cell dont je n'ai pas besoin dans la requête, mais qui me sont utile dans les composants Success/Loader/etc... ?**
>
> Toutes les propriétés que vous donnez à votre Cell seront automatiquement disponibles pour ses composants internes. Seuls ceux qui se se trouvent dans la liste des variables GraphQL seront transmises à la requête. Vous avez ainsi le meilleur des deux mondes! Dans l'affichage de notre article ci-dessus, si vous désirez montrer par exemple un nombre au hasard (pour des raisons evidentes liées à ce didacticiel :D), il vous suffit de passer cette propriété à votre Cell:
>
> ```javascript
> <BlogPostCell id={id} rand={Math.random()} />
> ```
> 
> Et ensuite vous la récupérez avec le résulat de la requête ans le composant (et même avec l'identifiant de l'article si vous le souhaitez):
> And get it, along with the query result (and even the original `id` if you want) in the component:
>
> ```javascript
> export const Success = ({ post, id, rand }) => {
>   //...
> }
> ```
>
> Merci Redwood!

### Displaying a Blog Post

Maintenant, affichons un véritable article au lieu d'un simple dump du résultat de la requête. Il semble que ce soit l'endroit parfait pour utiliser un bon vieux composant puisque nous affichons les articles de façon identique (pour l'instant) à la fois sur la page d'accueil et sur la page de détail.

    yarn rw g component BlogPost

L'exécution de cette commande créé le composant `BlogPost` dans le fichier `web/src/components/BlogPost/BlogPost.js`, accompagné de son fichier de test: 

```javascript
// web/src/components/BlogPost/BlogPost.js

const BlogPost = () => {
  return (
    <div>
      <h2>{'BlogPost'}</h2>
      <p>{'Find me in ./web/src/components/BlogPost/BlogPost.js'}</p>
    </div>
  )
}

export default BlogPost
```

> Vous remarquerez peut-être que nous n'avons ici aucun `import` relatif à la librairie `React`. Il s'agit pourtant bien d'un classique composant React. En réalité, nous (la "Redwood dev team") sommes un peu fatigués d'avoir à importer constamment les mêmes fichiers de la même manière... alors nous avons fait en sorte que Redwood le fasse pour nous, et donc pour vous!

Supprimons la partie de code qui affiche l'article dans `BlogPostCell`, et mettons la plutôt ici. Ce faisant, passons à notre nouveau composant la propriété `post`:

```javascript{3,5,7-14}
// web/src/components/BlogPost/BlogPost.js

import { Link, routes } from '@redwoodjs/router'

const BlogPost = ({ post }) => {
  return (
    <article>
      <header>
        <h2>
          <Link to={routes.blogPost({ id: post.id })}>{post.title}</Link>
        </h2>
      </header>
      <div>{post.body}</div>
    </article>
  )
}

export default BlogPost
```

Mettons à jour `BlogPostsCell` et `BlogPostCell` pour utiliser notre composant d'affichage commun:

```javascript{3,8}
// web/src/components/BlogPostsCell/BlogPostsCell.js

import BlogPost from 'src/components/BlogPost'

// Loading, Empty, Failure...

export const Success = ({ posts }) => {
  return posts.map((post) => <BlogPost key={post.id} post={post} />)
}
```

```javascript{3,8}
// web/src/components/BlogPostCell/BlogPostCell.js

import BlogPost from 'src/components/BlogPost'

// Loading, Empty, Failure...

export const Success = ({ post }) => {
  return <BlogPost post={post} />
}
```

Et nous y sommes! Nous devrions maintenant pouvoir aller et venir à notre guise entre la page d'accueil et les articles.

> Si vous appréciez ce que vous venez de voir sur le routeur, vous pouvez en apprendre plus dans le [guide](/docs/redwood-router) qui lui est consacré. 

### Résumé

Un petit état des lieux de ce que nous avons réalisé:

1. Création d'une nouvelle page pour afficher un article
2. Ajout d'une route prenant en char l'identifiant `id` d'un article sous la forme d'un paramètre de route
3. Création d'une Cell permettant de récupérer et afficher un article
4. Constat de la capacité de Redwood à vous mettre de bonne humeur en vous donnant accès à `id` là où vous en avez besoin tout en le convertissant au format numérique à la volée
6. Transformation de l'affichage d'un article en un composant React classique pouvant être partagé à plusieurs endroits dans l'interface (en l'espèce dans la page d'accueil et la page de détail)

## Votre partie préférée: Les Formulaires

Attendez! Ne partez pas! Vous deviez bien vous douter que ça allait venir, non? Rassurez-vous, pour les formulaires aussi, Redwood a trouvé une façon de faire qui les rend moins pénible que d'habitude. En fait, Redwood pourrait même vous faire _aimer_ les formulaires. Bon, aimer est peut-être un peu fort. Disons _apprécier_ travailler avec les formulaires, ou à tout le moins les _tolérer_?   

La troisième partie du didacticiel en video commence ici:

<div class="relative pb-9/16">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/eT7iIy0F8Tk?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

Nous avons déjà un formulaire ou deux dans notre application; vous rappellez-vous notre _scaffolding_ avec les articles? Ils fonctionnaient plus bien, non? Alors, a quel point est-ce difficile de reproduire ces formulaires? (Si vous n'avez pas encore eu la curiosité d'aller voir le code généré, ce qui va suivre va vous surprendre)

Construisons donc le formulaire le plus élémentaire qui soit pour notre blog, et utile de surcroît, celui qui permettra à vos lecteurs de vous contacter. 

### La Page

    yarn rw g page contact

Après avoir exécuté cette commande, nous pouvons ajouter un lien vers Contact dans notre Layout:

```javascript{17-19}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'

const BlogLayout = ({ children }) => {
  return (
    <>
      <header>
        <h1>
          <Link to={routes.home()}>Redwood Blog</Link>
        </h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>About</Link>
            </li>
            <li>
              <Link to={routes.contact()}>Contact</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>{children}</main>
    </>
  )
}

export default BlogLayout
```

And then use the `BlogLayout` in the `ContactPage`:

```javascript{3,6}
// web/src/pages/ContactPage/ContactPage.js

import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  return <BlogLayout></BlogLayout>
}

export default ContactPage
```

Vérifiez que tout fonctionne correctement, puis passons aux réjouïssances.

### Présentation des Form Helpers

Les formulaires avec React sont surtout connus pour être particulièrement agaçants à construire. Il existes les [Controlled Components](https://reactjs.org/docs/forms.html#controlled-components), les [Uncontrolled Components](https://reactjs.org/docs/uncontrolled-components.html), diverses [librairies tierces](https://jaredpalmer.com/formik/) et enfin pas mal d'astuces diverses pour essayer de les rendre aussi simples qu'ils sont sensés être selon les spécifications HTML: un champ `<input>` avec un attribut `name` qui sera envoyé quelque part lorsque l'utilisateur clique sur un bouton.  

Nous pensons que Redwood fait quelques pas dans la bonne direction, non seulement en vous libérant d'avoir à écrire un tans de code relatif aux composants controllés (controlled components), mais aussi en s'occupant de gérer automatiquement les validations et éventuelles erreurs. Regardons ensemble comment tout celà fonctionne.

Avant de commencer, ajoutons quelques classes CSS pour que les formulaires par défaut s'affichent correctement sans que nous ayons à alourdir notre code avec des attributs `style` un peu partout. Pour le moment nous écrirons ces règles dans le fichier `index.css` situé dans le répertoire `web/src`:

```css
/* web/src/index.css */

button, input, label, textarea {
  display: block;
  outline: none;
}

label {
  margin-top: 1rem;
}

.error {
  color: red;
}

input.error, textarea.error {
  border: 1px solid red;
}
```

Pour l'instant nous n'allons pas faire dialoguer notre formulaire de contact avec la base de données, raison pour laquelle nous ne générons pas une Cell. Nous allons simplement ajouter le formulaire à notre page. Dans Redwood, la création d'un formulaire débute par... attention à la surprise...une balise `<Form>`:

```javascript{3,9}
// web/src/pages/ContactPage/ContactPage.js

import { Form } from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  return (
    <BlogLayout>
      <Form></Form>
    </BlogLayout>
  )
}

export default ContactPage
```

Humm, OK... pour le moment rien d'incroyable. Ajoutons un premier champ que l'on puisse au moins afficher quelque chose. Redwood propose une variété de type de champs parmi lesquels se trouve `<TextField>`. Ce dernier correspond à un champ text tout ce qu'il y a de plus basique. Il possède un attribut `name` de telle façon que lorsqu'un formulaire contient de multiples champs, il soit possible de savoir lequel contient telle ou telle donnée.

```javascript{3,10}
// web/src/pages/ContactPage/ContactPage.js

import { Form, TextField } from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  return (
    <BlogLayout>
      <Form>
        <TextField name="input" />
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

<img src="https://user-images.githubusercontent.com/300/80258121-4f4d2300-8637-11ea-83f5-c667e05aaf74.png" />

Enfin quelque chose s'affiche! Pas encore très intéressant toutefois. Ajoutons un bouton "envoyer".

```javascript{3,11}
// web/src/pages/ContactPage/ContactPage.js

import { Form, TextField, Submit } from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  return (
    <BlogLayout>
      <Form>
        <TextField name="input" />
        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

<img src="https://user-images.githubusercontent.com/300/80258188-7572c300-8637-11ea-9583-1b7636f93be0.png" />

Nous obtenons ce qu'on peut considérer comme un véritable et authentique formulaire! Essayez de saisir quelque chose et cliquez sur le bouton. Rien n'explose, mais nous n'avons aucune indication que le formulaire à bien été envoyé (et vous aurez noté l'apparition d'une erreur dans la console). Voyons à présent comment récupérer les données depuis nos champs de formulaire.

### onSubmit

De façon similaire à un formulaire HTML, une balise `<Form>` possède un "_handler_" `onSubmit`. Ce handler sera appelé avec un seul argument: un unique objet contenant l'ensemble des champs du formulaire.

```javascript{4-6,10}
// web/src/pages/ContactPage/ContactPage.js

const ContactPage = () => {
  const onSubmit = (data) => {
    console.log(data)
  }

  return (
    <BlogLayout>
      <Form onSubmit={onSubmit}>
        <TextField name="input" />
        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}
```

Essayons maintenant de saisir quelques mots puis soumettre ce formulaire:

<img src="https://user-images.githubusercontent.com/300/80258293-c08cd600-8637-11ea-92fb-93d3ca1db3cf.png" />

Extra! Rendons le formulaire un peu plus utile en ajoutant quelques champs supplémentaires. Nous renommons ainsi notre premier champ en `name` puis ajoutons les champs `email` et `message`:

```javascript{3,15,16}
// web/src/pages/ContactPage/ContactPage.js

import { Form, TextField, TextAreaField, Submit } from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  const onSubmit = (data) => {
    console.log(data)
  }

  return (
    <BlogLayout>
      <Form onSubmit={onSubmit}>
        <TextField name="name" />
        <TextField name="email" />
        <TextAreaField name="message" />
        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

Remarquez le nouveau composant `<TextAreaField>` qui génère une balise HTML `<textarea>` contenant quelques spécificités utiles propres à Redwood:

<img src="https://user-images.githubusercontent.com/300/80258346-e4e8b280-8637-11ea-908b-06a1160b932b.png" />

Ajoutons également quelques étiquettes en face des champs:

```javascript{6,9,12}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField name="name" />

      <label htmlFor="email">Email</label>
      <TextField name="email" />

      <label htmlFor="message">Message</label>
      <TextAreaField name="message" />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

<img src="https://user-images.githubusercontent.com/300/80258431-15c8e780-8638-11ea-8eca-0bd222b51d8a.png" />

Essayez donc de soumettre à nouveau le formulaire, vous devriez obtenir dans la console un message avec le contenu des trois champs.

### Validation

"Humm... cher auteur de ce didacticiel, qui a-t-il d'incroyable jusqu'ici?". C'est sans doute votre état d'esprit à ce stade. En effet, il existe déjà un nombre conséquent de librairies permettant d'obtenir un résultat similaire.. Vous avez raison! N'importe qui peut remblir un formulaire _correctement_, mais que se passe-t-il lorsqu'un utilisateur fait une erreur, oubli un champ, voire tente de jouer les hackers? Qui va vous aider à gérer cette situation? Redwood va le faire. 

Tout d'abord, ce trois champs devraient être obligatoirement remplis pour pouvoir soumettre le formulaire. Rendons cette règle obligatoire en utilisant l'attribut HTML standard `required`:

```javascript{7,10,13}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField name="name" required />

      <label htmlFor="email">Email</label>
      <TextField name="email" required />

      <label htmlFor="message">Message</label>
      <TextAreaField name="message" required />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

<img src="https://user-images.githubusercontent.com/300/80258542-5163b180-8638-11ea-8450-8a727de177ad.png" />

Désormais, lorsque vous essayez de soumettre le formulaire, un message s'affiche dans votre navigateur. C'est mieux que rien, mais l'apparence de ce message ne peut être modifiée. Peut-on faire mieux?

Oui! Remplaçons cet attribut `required` par un object que nous passons à un attribut nommé `validation`, spécifique à Redwood:

```javascript{7,10,13}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField name="name" validation={{ required: true }} />

      <label htmlFor="email">Email</label>
      <TextField name="email" validation={{ required: true }} />

      <label htmlFor="message">Message</label>
      <TextAreaField name="message" validation={{ required: true }} />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

Maintenant lorsqu'un champ reste vide, le formulaire n'est pas envoyé et le champ en question prend le focus de telle manière que l'utilisateur puisse saisir une valeur. Pas encore stupéfiant, mais c'est une première étape. Redwood a d'autres fonctions sympatiques pour les formulaires, dont la possibilité d'afficher les erreurs à côté des champs.  


### `<FieldError>`

Pour celà, voici le composant `<FieldError>` (n'oubliez pas d'inclure l'`import` associé en haut du fichier):

```javascript{8,22,26,30}
// web/src/pages/ContactPage/ContactPage.js

import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
} from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  const onSubmit = (data) => {
    console.log(data)
  }

  return (
    <BlogLayout>
      <Form onSubmit={onSubmit}>
        <label htmlFor="name">Name</label>
        <TextField name="name" validation={{ required: true }} />
        <FieldError name="name" />

        <label htmlFor="email">Email</label>
        <TextField name="email" validation={{ required: true }} />
        <FieldError name="email" />

        <label htmlFor="message">Message</label>
        <TextAreaField name="message" validation={{ required: true }} />
        <FieldError name="message" />

        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

Observez que l'attribut `name` correspond à celui du champ au dessus. De cette manière, Redwood sait où afficher le message d'erreur d'un champ.

<img src="https://user-images.githubusercontent.com/300/80258694-ac95a400-8638-11ea-904c-dc034f07b12a.png" />

Mais c'est juste le début. Maintenant faisons en sorte que nos utilisateurs sachent qu'il s'agisse bien d'un message d'erreur. Vous rappellez-vous la classe CSS `.error` que nous avions définie dans `index.css`? Indiquons-la à l'attribut `className` de nos composants `<FieldError>`:

```javascript{8,12,16}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField name="name" validation={{ required: true }} />
      <FieldError name="name" className="error" />

      <label htmlFor="email">Email</label>
      <TextField name="email" validation={{ required: true }} />
      <FieldError name="email" className="error" />

      <label htmlFor="message">Message</label>
      <TextAreaField name="message" validation={{ required: true }} />
      <FieldError name="message" className="error" />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

<img src="https://user-images.githubusercontent.com/300/73306040-3cf65100-41d0-11ea-99a9-9468bba82da7.png" />

Vous savez ce qui serez bien? Que le champ lui-même indique qu'il y a eu une erreur. Remarquez ici l'utilisation de l'attribut `errorClassName`:

```javascript{10,18,26}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField
        name="name"
        validation={{ required: true }}
        errorClassName="error"
      />
      <FieldError name="name" className="error" />

      <label htmlFor="email">Email</label>
      <TextField
        name="email"
        validation={{ required: true }}
        errorClassName="error"
      />
      <FieldError name="email" className="error" />

      <label htmlFor="message">Message</label>
      <TextAreaField
        name="message"
        validation={{ required: true }}
        errorClassName="error"
      />
      <FieldError name="message" className="error" />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

<img src="https://user-images.githubusercontent.com/300/80258907-39d8f880-8639-11ea-8816-03a11c69e8ac.png" />

Bravo! Et maintenant, appliquons ce principe à l'étiquette elle-même. Pour celà utilisons le composant `<Label>` fourni par Redwood. Notez comme l'attribut `for` correspond à la valeur de l'attribut `name` du composant associé. N'oubliez pas également d'importer le composant:

```javascript{9,21-23,31-33,41-43}
// web/src/pages/ContactPage/ContactPage.js

import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
  Label,
} from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  const onSubmit = (data) => {
    console.log(data)
  }

  return (
    <BlogLayout>
      <Form onSubmit={onSubmit}>
        <Label name="name" errorClassName="error">
          Name
        </Label>
        <TextField
          name="name"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="name" className="error" />

        <Label name="email" errorClassName="error">
          Email
        </Label>
        <TextField
          name="email"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="email" className="error" />

        <Label name="message" errorClassName="error">
          Message
        </Label>
        <TextAreaField
          name="message"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="message" className="error" />

        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

<img src="https://user-images.githubusercontent.com/300/80259003-70af0e80-8639-11ea-97cf-b6b816118fbf.png" />

> En plus de `className` et `errorClassName` vous pouvez également utiliser `style` et `errorStyle`

### Validation du Format des Champs

Nous devrions nous assurer que le champ email contient bien... un email!

```html{7-9}
// web/src/pages/ContactPage/ContactPage.js

<TextField
  name="email"
  validation={{
    required: true,
    pattern: {
      value: /[^@]+@[^.]+\..+/,
    },
  }}
  errorClassName="error"
/>
```

OK, ça n'est pas la validation ultime pour un champ email, mais pour le moment faisons comme si. Modifions également le message affiché en cas d'échec de la validation:

```html{9}
// web/src/pages/ContactPage/ContactPage.js

<TextField
  name="email"
  validation={{
    required: true,
    pattern: {
      value: /[^@]+@[^.]+\..+/,
      message: 'Please enter a valid email address',
    },
  }}
  errorClassName="error"
/>
```

<img src="https://user-images.githubusercontent.com/300/80259139-bd92e500-8639-11ea-99d5-be278dc67afc.png" />

Vous avez peut-être remarqué qu'essayer d'envoyer le formulaire alors que sont présentes des erreurs de validation n'affiche rien dans la console. C'est en réalité une bonne chose car celà vous indique que le formulaire n'a pas été envoyé. Corrigez la valeur des champs concernés, et tout fonctionne correctement.

> Lorsqu'un message lié à une erreur lors de la validation d'un champ s'affiche, il disparaît dès que la valeur est corrigée. Ainsi l'utilisateur n'a pas à devoir envoyer de nouveau le formulaire pour vérifier la validité de la saisie.

Finalement, savez-vous ce qui serait _vraiment_ sympa? Ce serait de faire en sorte que les champs soient validés dès que l'utilisateur quitte un champ. De cette manière l'utilisateur n'a pas besoin de remplir l'ensemble des champs et envoyer le formulaire pour voir toutes les erreurs s'afficher. Voyons comment faire:

```html
// web/src/pages/ContactPage/ContactPage.js

<Form onSubmit={onSubmit} validation={{ mode: 'onBlur' }}>
```

Alors, qu'en pensez-vous? Quelques composants, un ou deux attributs, et vous avez devant vous un formulaire qui gère les erreurs, valide les champs et vous envoie le contenu sous la forme d'un bel objet javascript. Merci Redwood!

> Les formulaires de Redwood sont construits à partir de la librairie [React Hook Form](https://react-hook-form.com/). Celle-ci contient d'autres fonctionalités très utiles que nous n'avons pas documenté ici.  

Redwood a encore plus d'un tour dans son sac pour ce qui concerne les formulaires, mais nous allons garder ça pour une étape ultérieure.

Avoir un formulaire de contact, c'est bien. Mais conserver les message qu'on vous envoie, c'est mieux! Procédons maintenant à la création de la table en base de données pour y enregistrer ces informations. Ce faisant nous allons créer notre première mutation GraphQL!

## Enregistrer les Données

Ajoutons une nouvelle table à notre base de données. Ouvrez `api/prisma/schema.prisma` et ajoutez un nouveau modèle "Contact" à la suite du premier modèle "Post": 

```javascript
// api/prisma/schema.prisma

model Contact {
  id        Int @id @default(autoincrement())
  name      String
  email     String
  message   String
  createdAt DateTime @default(now())
}
```

> Pour définir une colonne comme optionnelle (c'est à dire permettre que sa valeur soit `NULL`), il suffit de suffixer le type de la donnée avec un point d'interrogation: `name String?` 

Nous créons ensuite notre nouvelle migration:

    yarn rw db save create contact

Enfin, nous executons la migration de façon à mettre à jour le schéma de la base de données:

    yarn rw db up

Maintenant nous créeons l'interface GraphQL permettant d'accéder à cette nouvelle table. C'est la première fois que nous utilisons cette commande `generate` nous même. (la commande `scaffold` repose également dessus):

    yarn rw g sdl contact

De la même manière qu'avec la commande `scaffold`, ceci va créer deux nouveaux fichiers dans le répertoire `api`:

1. `api/src/graphql/contacts.sdl.js`: qui définit le schéma GraphQL
2. `api/src/services/contacts/contacts.js`: qui contient votre code métier

Ouvrez `api/src/graphql/contacts.sdl.js` et vous verrez les types `Contact`, `CreateContactInput` et `UpdateContactInput` déjà définis pour vous. La commande `generate sdl` a analysé le schéma et créé un type `Contact` contenant chaque champ de la table, ainsi qu'un type `Query` avec une requête `contacts` qui retourne un tableau de types `Contact`.

```javascript
// api/src/graphql/contacts.sdl.js

export const schema = gql`
  type Contact {
    id: Int!
    name: String!
    email: String!
    message: String!
    createdAt: DateTime!
  }

  type Query {
    contacts: [Contact!]!
  }

  input CreateContactInput {
    name: String!
    email: String!
    message: String!
  }

  input UpdateContactInput {
    name: String
    email: String
    message: String
  }
`
```

Que sont les "input" `CreateContactInput` et `UpdateContactInput`? Redwood suit la recommandation de GraphQL d'utiliser les [Input Types](https://graphql.org/graphql-js/mutations-and-input-types/) dans les mutations plutôt que de lister tous les champs qui peuvent être définis. Tous les champs requis dans `schema.prisma` sont également requis dans `CreateContactInput` (vous ne pouvez pas créer un enregistrement valide sans eux) mais rien n'est explicitement requis dans `UpdateContactInput`. En effet, vous pouvez souhaiter mettre à jour un seul champ, deux champs ou tous les champs. L'alternative serait de créer des types d'entrée séparés pour chaque permutation de champs que vous souhaitez mettre à jour. Nous avons estimé que le fait de n'avoir qu'une seule entrée de mise à jour, bien que ce ne soit peut-être pas la manière absolument correcte de créer une API GraphQL, était un bon compromis pour faciliter le développement.

> Redwood suppose que votre code n'essaiera pas de définir une valeur sur un champ nommé `id` ou `createdAt` donc il les a laissés en dehors des types d'entrée, mais si votre base de données autorise l'un ou l'autre de ceux à définir manuellement, vous pouvez mettre à jour` CreateContactInput `ou `UpdateContactInput` et les ajouter.

Puisque toutes les colonnes de la table étaient définies comme requises dans `schema.prisma`, elles sont également définies comme requises ici (notez le suffixe `!` sur les types de données)

> **important:** la syntaxe de `schema.prisma` requiert l'ajout d'un caractère `?` lorsqu'un champ _n'est pas_ requis, tandis que la syntaxe GraphQL requiert l'ajout d'un caractère `!` lorsqu'un champ _est_ requis.

Comme décrit dans [Quête secondaire: Fonctionnement de Redwood avec les Données](qu-te-secondaire-fonctionnement-de-redwood-avec-les-donn-es), il n'y a pas de "resolver" définit explicitement dans le fichier SDL. Redwood suit une convention de nommage simple: chaque champ listé dans les types `Query` et `Mutation` correspondent à une fonction avec un nom identique dans les fichiers `service` et `sdl` associés (`api/src/graphql/contacts.sdl.js -> api/src/services/contacts/contacts.js`) 

Dans le cas présent, nous créeons une unique `Mutation` que nous appelons `createContact`. Nous l'ajoutons à la fin de notre fichier SDL (avant le caractère 'backtick'): 

```javascript
// api/src/graphql/contacts.sdl.js

type Mutation {
  createContact(input: CreateContactInput!): Contact
}
```

La mutation `createContact` accepte une variable unique, `input`, qui est un objet conforme à ce qu'on attend pour un `CreateContactInput`, c'est à dire `{ name, email, message }`.

C'est terminé pour le fichier SDL, définissons maintenant le service qui va réellement enregistrer les données en base. Le service inclut une fonction `contacts` permettant de récupérer l'ensemble des contacts depuis la base. Ajoutons-y une mutation pour pouvoir créer un nouveau contact:

```javascript{9-11}
// api/src/services/contacts/contacts.js

import { db } from 'src/lib/db'

export const contacts = () => {
  return db.contact.findMany()
}

export const createContact = ({ input }) => {
  return db.contact.create({ data: input })
}
```

Grâce au client Prisma, il faut peu de code pour enregistrer nos données en base! Il s'agit d'un appel asynchrone, mais nous n'avons pas à nous soucier de manipuler un objet Promise ou s'arranger avec `async/await`. La librairie Apollo le fait pour nous!

Avant d'insérer tout ceci dans notre interface utilisateur, prennons un peu de temps pour utiliser un outil bien pratique en exécutant la commande `yarn redwood dev`.

### Le Bac à Sable GraphQL

Souvent, il est utile d'expérimenter notre API dans une forme un peu "brute" avant de poursuivre plus avant le développement de l'interface et s'apercevoir que l'on a oublié quelque chose.

Lorsque vous avez exécuté la commande `yarn redwood dev` au début de ce didacticiel, vous avez en réalité démarré un second processus en arrière-plan. Ouvrez donc une nouvelle page de votre navigateur à cette adresse: http://localhost:8911/graphql . Il s'agit du [Bac à Sable GraphQL](https://github.com/prisma-labs/graphql-playground) fournit par la librairie Prisma, une application web permettant d'interagir avec une API GraphQL: 

<img src="https://user-images.githubusercontent.com/300/70950852-9b97af00-2016-11ea-9550-b6983ce664e2.png" />

Observez en particulier l'onglet "Doc" situé sur la partie droite de l'écran:

<img src="https://user-images.githubusercontent.com/300/73311311-fce89b80-41da-11ea-9a7f-2ef6b8191052.png" />

Vous y trouverez le schema complet tel que définit dans vos fichiers SDL! L'application analyse ces définitions et vous propose ces éléments pour vous permettre de construire vos requêtes. Essayez par exemple de récupérer les ID de tous les articles en écrivant votre requête dans la partie gauche puis en cliquant sur le bouton "Play":

<img src="https://user-images.githubusercontent.com/300/70951466-52e0f580-2018-11ea-91d6-5a5712858781.png" />

Le bac à sable GraphQL est une excellente manière d'expérimenter avec votre API, et comprendre pourquoi une requête ne fonctionne pas comme prévue.

### Créer un Contact

Notre mutation GraphQL est prête pour la partie backend, tout ce qu'il reste à faire c'est l'invoquer depuis la partie frontend. Tout ce qui à trait à notre formulaire se trouve dans `ContactPage`, c'est donc l'endroit logique pour y mettre l'appel à notre nouvelle mutation. D'abord nous définissons cette mutation comme une constante que nous appellerons plus tard (ceci peut être défini en dehors du composant lui-même, juste après les lignes d'imports):

```javascript
// web/src/pages/ContactPage/ContactPage.js

const CREATE_CONTACT = gql`
  mutation CreateContactMutation($input: CreateContactInput!) {
    createContact(input: $input) {
      id
    }
  }
`
```

Nous référençons ainsi la mutation `createContact` définie auparavant dans le fichier SDL des contacts, tout en lui passant en argument un objet `input` contenant la valeur des champs `name`, `email` et `message`.

Après quoi, nous appelons le 'hook' `useMutation` fourni par Appolo, ce qui nous permet d'exécuter la mutation lorsque le moment est venu (n'oubliez pas les imports comme à chaque fois):

```javascript{11,15}
// web/src/pages/ContactPage/ContactPage.js

import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
  Label,
} from '@redwoodjs/forms'
import { useMutation } from '@redwoodjs/web'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  const [create] = useMutation(CREATE_CONTACT)

  const onSubmit = (data) => {
    console.log(data)
  }

  return (...)
}
```
`create` est une fonction qui invoque la mutation et prend en paramètre un objet contenant un clef `variables`. Cette dernière contient à son tour une clef `input`. Par exemple, nous pourrions l'appeler également de cette manière:

```javascript
create({
  variables: {
    input: {
      name: 'Rob',
      email: 'rob@redwoodjs.com',
      message: 'I love Redwood!',
    },
  },
})
```

Si votre méémoire est bonne, vous vous souvenez sans doute que la balise `<Form>` nous donne accès à l'ensemble des champs du formulaire avec un objet bien pratique dans lequel chaque clef se trouve être le nom du champ. Celà signifie donc que l'objet `data`que nous recevons dans `onSubmit` est déjà dans le format adapté pour `input`!  

Maintenant nous pouvons mettre à jour la fonction `onSubmit` pour invoquer la mutation avec les données qu'elle reçoit:

```javascript{7}
// web/src/pages/ContactPage/ContactPage.js

const ContactPage = () => {
  const [create] = useMutation(CREATE_CONTACT)

  const onSubmit = (data) => {
    create({ variables: { input: data }})
    console.log(data)
  }

  return (...)
}
```

Essayez-donc de remplir le formulaire et de l'envoyer. Vous devriez obtenir un nouveau contact en base de données! Vous pouvez vérifier ceci avec l'outil bac à sable de GraphQL:

![image](https://user-images.githubusercontent.com/300/76250632-ed5d6900-6202-11ea-94ce-bd88e3a11ade.png)

### Améliorer le formulaire de contact

Notre formulaire de contact fonctionne, mais il subsiste quelques problèmes:

- Cliquer sur le bouton d'enregistrement plusieurs fois à pour conséquence d'envoyer le formulaire également plusieurs fois
- L'utilisateur ne sait pas si l'envoi a bien été pris en compte
- Si une erreur devait se produire côté serveur, nous n'avons aucun moyen d'en informer l'utilisateur

Essayons d'y apporter une solution.

Le 'hook' `useMutation` retourne quelques autres éléments en plus de la fonction permettant de l'invoquer. Nous pouvons déstructurer ceux-ci (`loading` et `error`) de la façon suivante:

```javascript{4}
// web/src/pages/ContactPage/ContactPage.js

const ContactPage = () => {
  const [create, { loading, error }] = useMutation(CREATE_CONTACT)

  const onSubmit = (data) => {
    create({ variables: { input: data } })
    console.log(data)
  }

  return (...)
}
```

Ce faisant, nous savons si un appel à la base est toujours en cours en utilisant la valeur de `loading`. Une façon simple de résoudre le problème des soumissions multiples du même formulaire est de rendre inactif le bouton d'envoi tant que la réponse n'a pas été reçue. Nous pouvons faire celà en liant l'attribut `disabled` du bouton "save" à la valeur contanue dans `loading`:

```javascript{5}
// web/src/pages/ContactPage/ContactPage.js

return (
  // ...
  <Submit disabled={loading}>Save</Submit>
  // ...
)
```

Il peut être difficile de voir une différence en phase de développement car l'envoi est très rapide. Mais vous pouvez néanmoins activer un outil bien pratique dans le navigateur Chrome afin de simuler une connection lente:

<img src="https://user-images.githubusercontent.com/300/71037869-6dc56f80-20d5-11ea-8b26-3dadb8a1ed86.png" />

Vous verrez alors que le bouton "Save" devient inactif pendant une seconde ou deux en attendant la réponse.

Maintenant, utilisons le système dit de `Flash` proposé par Redwood afin d'informer l'utilisateur que son envoi à bien été traité. `useMutation` accepte un second paramètre optionnel contenant des options. Une de ces options est une fonction callback appelée `onCompleted` qui sera invoquée lorsque la mutation sera achevée avec succès. Nous allons donc utiliser cette fonction pour ajouter un message qui sera affiché par un composant `Flash`. Ajoutez donc le composant `Flash` a votre page et utilisez sa propriété `timeout` pour définir le temps d'affichage. (Vous pouvez lire la documentation à propos du système de Flash proposé par Redwood [ici](https://redwoodjs.com/docs/flash-messaging-bus))

```javascript{4,10,13-17,24}
// web/src/pages/ContactPage/ContactPage.js

// ...
import { Flash, useFlash, useMutation } from '@redwoodjs/web'
import BlogLayout from 'src/layouts/BlogLayout'

// ...

const ContactPage = () => {
  const { addMessage } = useFlash()

  const [create, { loading, error }] = useMutation(CREATE_CONTACT, {
    onCompleted: () => {
      addMessage('Thank you for your submission!', {
        style: { backgroundColor: 'green', color: 'white', padding: '1rem' }
      })
    },
  })

  // ...

  return (
    <BlogLayout>
      <Flash timeout={2000} />
      // ...
```

### Afficher les erreurs serveur

Nous allons maintenant informer l'utilisateur des éventuelles erreurs côté serveur. Jusqu'ici nous n'avons notifié les utilisateurs quie des erreurs _côté client_ lorsqu'un champ était manquant ou formaté incorrectement. Mais si nous avons également des contraintes côté serveur que le composant `<Form>` ignore, nous devons tout de même pouvoir en informer l'utilisateur.

Ainsi, nous avons une validateur de l'email côté client, mais tout bon développeur web sait qu'il ne faut [_jamais faire confiance au client_](https://www.codebyamir.com/blog/never-trust-data-from-the-browser). Ajoutons une validation de l'email côté serveur de façon à être certain qu'aucune donnée erronée ne soit ajoutée dans la base, et ce même si un utilisateur parvenait à contourner le fonctionnement de l'application côté client.

> Pourquoi n'avons-nous pas besoin de validation côté serveur pour s'assurer que les champs name, email et message sont bien remplis? Car la base de données le fait pour nous. Vous rappellez-vous `String!` dans notre fichier SDL? Celà ajoute une contrainte en base de données de telle façon que ce champ ne puisse être `null`. Une valeur `null` serait rejetée par la base et GraphQL renverrait une erreur à la partie client. 
>
> Cependant, il n'existe pas de type `Email!`, raison pour laquelle nous devons assurer la validation nous même 

Nous avons déjà parlé de code métier et du fait que ce type de code a vocation à se trouver dans nos fichiers services. Ceci en est un exemple parfait. Ajoutons une fonction `validate` à notre service `contacts`:

```javascript{3,7-15,22}
// api/src/services/contacts/contacts.js

import { UserInputError } from '@redwoodjs/api'

import { db } from 'src/lib/db'

const validate = (input) => {
  if (input.email && !input.email.match(/[^@]+@[^.]+\..+/)) {
    throw new UserInputError("Can't create new contact", {
      messages: {
        email: ['is not formatted like an email address'],
      },
    })
  }
}

export const contacts = () => {
  return db.contact.findMany()
}

export const createContact = ({ input }) => {
  validate(input)
  return db.contact.create({ data: input })
}
```

Ainsi, lorsque `createContact` est invoquée, la fonction commence par valider le contenu des champs du formulaire. Puis, et seulement s'il n'y a aucune erreur, l'enregistrement sera créé en base de données.

Nous capturons déjà toutes les erreurs dans la constante `error` que nous obtenons grâce au 'hook' `useMutation`. C'est pourquoi nous avons la possibilité d'afficher ces erreurs sur la page, par exemple au dessus du formulaire:

```html{4-9}
// web/src/pages/ContactPage/ContactPage.js

<Form onSubmit={onSubmit} validation={{ mode: 'onBlur' }}>
  {error && (
    <div style={{ color: 'red' }}>
      {"We couldn't send your message: "}
      {error.message}
    </div>
  )}
  // ...
```

> Si vous avez besoin de manipuler l'objet contenant les erreurs, vous pouvez procéder ainsi:
>
> ```javascript{3-8}
> // web/src/pages/ContactPage/ContactPage.js
> const onSubmit = async (data) => {
>   try {
>     await create({ variables: { input: data } })
>     console.log(data)
>   } catch (error) {
>     console.log(error)
>   }
> }
> ```

Afin de tester ceci, provoquons une erreur en retirant temporairement la validation côté client de l'adresse email:

```html
// web/src/pages/ContactPage/ContactPage.js

<TextField
  name="email"
  validation={{
    required: true,
  }}
  errorClassName="error"
/>
```

Maintenant, essayons de remplir le formulaire avec un adresse invalide:

<img src="https://user-images.githubusercontent.com/300/80259406-5aee1900-863a-11ea-9b82-def3a4f3e162.png" />

Celà fonctionne, même si l'affichage reste à améliorer. Voir apparaître une erreur GraphQL n'est pas idéal. Il serait plus sympa de faire en sorte que ce soit le champ concerné qui soit marqué d'une erreur...

Vous rapellez-vous lorsque nous avons dit que `<Form>` avait plus d'un tour dans son sac? Voyons donc ça!

Supprimez l'affichage de l'erreur tel que nous venons de l'ajouter (`{ error && ...}`) , et remplacez-le avec `<FormError>` tout en passant en argument la constante `error` que nous récupérons depuis `useMutation`. Ajoutez également quelques ééléments de style à `wrapperStyle`, sans oublier les `import` associés.

```javascript{10,18-22}
// web/src/pages/ContactPage/ContactPage.js

import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
  Label,
  FormError,
} from '@redwoodjs/forms'
import { Flash, useFlash, useMutation } from '@redwoodjs/web'
// ...

return (
  <BlogLayout>
    <Flash timeout={1000}>
    <Form onSubmit={onSubmit} validation={{ mode: 'onBlur' }} error={error}>
      <FormError
        error={error}
        wrapperStyle={{ color: 'red', backgroundColor: 'lavenderblush' }}
      />

      //...
)
```

Désormais, l'envoi du formulaire avec une adresse invalide donne ceci:

<img src="https://user-images.githubusercontent.com/300/80259553-c46e2780-863a-11ea-9441-54a9112b9ce5.png" />

Nous obtenons un message d'erreur en haut du formulaire _et_ les champs concernés sont mis en avant! Le message en haut du formulaire peut apparaître un peu lourd pour un si petit formulaire, mais vous contaterez son utilité lorsque vous construirez des formulaires de plusieurs pages; de cette façon l'utilisateur peut voir imméédiatement ce qui ne fonctionne pas sans avoir à parcourir l'ensemble du formulaire. Si vous ne souhaitez pas utiliser cet affichage, il vous suffit de supprimer `<FormError>`, les champs seront toujours mis en avant.

> `<FormError>` a plusieurs options pour adapter le style d'affichage
>
> - `wrapperStyle` / `wrapperClassName`: le conteneur pour l'ensemble du message
> - `titleStyle` / `titleClassName`: le titre "Can't create new contact"
> - `listStyle` / `listClassName`: le `<ul>` qui contient la liste des erreurs
> - `listItemStyle` / `listItemClassName`: chaque `<li>` contenant chaque erreur

### One more thing...

Puisque nous ne redirigeons pas l'utilisateur une fois le formulaire envoyé, nous devrions au moins remettre le formulaire à zéro. Pour celà nous devons utiliser la fonction `reset()` proposée par `react-hook-form`, mais nous n'y avons pas accès compte tenu de la manière dont nous utilisons `<Form>`.

`react-hook-form` possède un 'hook' appelé `useForm()` qui est en principe invoquéé pour nous à l'intérieur de `<Form>`. De façon à réinitialiser le formulaire nous devons invoquer ce 'hook' manuellement. Voici comment faire:

Commençons par importer `useForm`:

```javascript
// web/src/pages/ContactPage/ContactPage.js

import { useForm } from 'react-hook-form'
```

Puis invoquons ce 'hook' dans notre composant:

```javascript{4}
// web/src/pages/ContactPage/ContactPage.js

const ContactPage = () => {
  const formMethods = useForm()
  //...
```

Enfin, donnons pour instruction explicite à `<Form>` d'utiliser `formMethods`, au lieu de le laisser le faire lui-même:

```javascript{10}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Flash timeout={1000}>
    <Form
      onSubmit={onSubmit}
      validation={{ mode: 'onBlur' }}
      error={error}
      formMethods={formMethods}
    >
    // ...
```

Maintenant nous pouvons invoquer manuellement `reset()` depuis `formMethods()` juste après que le message de confirmation soit affiché:

```javascript
// web/src/pages/ContactPage/ContactPage.js

const [create, { loading, error }] = useMutation(CREATE_CONTACT, {
  onCompleted: () => {
    // addMessage...
    formMethods.reset()
  },
})
```

<img alt="Capture écran du formulaire de Contact avec message de confirmation Flash" src="https://user-images.githubusercontent.com/44448047/93649232-1be9a700-f9d1-11ea-821c-7a69c626f50c.png">

> Vous pouvez maintenant réactiver la validation email côté client sur le `<TextField>`, tout en conservant la validation côté serveur.

Voici le contenu final de la page `ContactPage.js`: 

```javascript
import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
  Label,
  FormError,
} from '@redwoodjs/forms'
import { Flash, useFlash, useMutation } from '@redwoodjs/web'
import { useForm } from 'react-hook-form'
import BlogLayout from 'src/layouts/BlogLayout'

const CREATE_CONTACT = gql`
  mutation CreateContactMutation($input: CreateContactInput!) {
    createContact(input: $input) {
      id
    }
  }
`

const ContactPage = () => {
  const formMethods = useForm()
  const { addMessage } = useFlash()

  const [create, { loading, error }] = useMutation(CREATE_CONTACT, {
    onCompleted: () => {
      addMessage('Thank you for your submission!', {
        style: { backgroundColor: 'green', color: 'white', padding: '1rem' }
      })
      formMethods.reset()
    },
  })

  const onSubmit = (data) => {
    create({ variables: { input: data } })
    console.log(data)
  }

  return (
    <BlogLayout>
      <Flash timeout={1000} />
      <Form
        onSubmit={onSubmit}
        validation={{ mode: 'onBlur' }}
        error={error}
        formMethods={formMethods}
      >
        <FormError
          error={error}
          wrapperStyle={{ color: 'red', backgroundColor: 'lavenderblush' }}
        />
        <Label name="name" errorClassName="error">
          Name
        </Label>
        <TextField
          name="name"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="name" className="error" />

        <Label name="name" errorClassName="error">
          Email
        </Label>
        <TextField
          name="email"
          validation={{
            required: true,
          }}
          errorClassName="error"
        />
        <FieldError name="email" className="error" />

        <Label name="name" errorClassName="error">
          Message
        </Label>
        <TextAreaField
          name="message"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="message" className="error" />

        <Submit disabled={loading}>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

C'est terminé! [React Hook Form](https://react-hook-form.com/) propose pas mal de fonctionalités que `<Form>` n'expose pas. Lorsque vous souhaitez les utiliser, appelez juste le 'hook' `useForm()` vous-même, en vous assurant de bien passer en argument l'objet retourné (`formMethods`) comme propriété de `<Form>` de façon à ce que la validation et les autres fonctionalités puissent continuer à fonctionner. 

> Vous avez peut-être remarqué que la validation onBlur a cessé de fonctionner lorsque vous avez commencé à appeler `userForm()` par vous-même. Ceci s'explique car Redwood invoque `userForm()` et lui passe automatiquement en argument ce que vous avez passé à `<Form>`. Puisque Redwood n'appelle plus automatiquement `useForm()` à votre place, vous devez de faire manuellement:
>
> ```javascript
> const formMethods = useForm({ mode: 'onBlur' })
> ```

La partie publique du site a bon aspect. Que faire maintenant de la partie administration qui nous permet de créer et éditer les articles? Nous devrions la déplacer dans une partie réservée et la placer derrière un login, de façon à ce des utilisateurs mal intentionnés ne puissent pas créer en chaîne, par exemple, des publicités pour l'achat de médicaments en ligne...

## Administration

Having the admin screens at `/admin` is a reasonable thing to do. Let's update the routes to make that happen by updating the four routes starting with `/posts` to start with `/admin/posts` instead:

```html
// web/src/Routes.js

<Route path="/admin/posts/new" page={NewPostPage} name="newPost" />
<Route path="/admin/posts/{id:Int}/edit" page={EditPostPage} name="editPost" />
<Route path="/admin/posts/{id:Int}" page={PostPage} name="post" />
<Route path="/admin/posts" page={PostsPage} name="posts" />
```

Head to http://localhost:8910/admin/posts and our generated scaffold page should come up. Thanks to named routes we don't have to update any of the `<Link>`s that were generated by the scaffolds since the `name`s of the pages didn't change!

> On the last page we said we were going to set up an admin section **and** put it
> behind a login. So far, all we've done is updated the routes. Don't worry, we
> haven't forgotten! We will be setting up authentication in a [future step](/tutorial/authentication).

How about getting this thing out into the real world?

## Deployment

Part 4 of the video tutorial picks up here:

<div class="relative pb-9/16">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/UpD3HyuZkvY?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

The whole reason we started building Redwood was to make full-stack web apps easier to build and deploy on the Jamstack. You've seen what building a Redwood app is like, how about we try deploying one?

We've only got one change to make to the codebase to get it ready for deployment and we've got a generator to do it for us:

```terminal
yarn rw g deploy netlify
```

This creates a file at `/netlify.toml` which contains the commands and file paths that Netlify needs to know about to build a Redwood app.

Before we continue, make sure your app is fully committed and pushed to GitHub, GitLab, or Bitbucket. We're going to link Netlify directly to our git repo so that a simple push to `main` will re-deploy our site. If you haven't worked on the Jamstack yet you're in for a pleasant surprise!

> **NOTE:** Git initializes with `master`. Don't know how to rename `master` to `main`? If you're pushing to GitHub, you can follow these steps:
>
> ```plaintext{4,6}
> git init
> git add .
> git commit -m 'First commit'
> git branch -m main
> git remote add origin ...
> git push -u origin main
> ```

### Vercel (alternative deploy target)

Redwood officially supports multiple hosting providers (with even more on the way). Although this Tutorial continues with a focus on Netlify deployment and authentication with Netlify Identity, you can deploy to [Vercel](https://vercel.com/redwoodjs-core) instead. To do this, first complete "The Database" section below, but then use this [Vercel deploy walkthrough](https://redwoodjs.com/docs/deploy#redwood-deploy-configuration) in place of the following "Netlify" instructions. **Note**: Netlify Identity, used in upcoming "Authentication" section, won’t work on the Vercel platform.

### The Database

We'll need a database somewhere on the internet to store our data. We've been using SQLite locally, but that's a file-based store meant for single-user. SQLite isn't really suited for the kind of connection and concurrency requirements a production website will require. For this part of this tutorial, we will use Postgres. (Prisma currently supports SQLite, Postgres and MySQL.) Don't worry if you aren't familiar with Postgres, Prisma will do all the heavy lifting. We just need to get a database available to the outside world so it can be accessed by our app.

First we'll let Prisma know that we intend to use Postgres in addition to SQLite so it will build client libraries for both. Update the `provider` entry in `schema.prisma`:

```javascript
provider = ["sqlite", "postgresql"]
```

If you'd like to develop locally with Postgres, see the
[Local Postgres Setup](/docs/local-postgres-setup) guide.

> For now, you need to set up your own database, but we are working with various infrastructure providers to make this process simpler and more Jamstacky. Stay tuned for improvements in that regard!

There are several hosting providers where you can quickly start up a Postgres instance:

- [Heroku](https://www.heroku.com/postgres)
- [Digital Ocean](https://www.digitalocean.com/products/managed-databases)
- [AWS](https://aws.amazon.com/rds/postgresql/)

We're going to go with Heroku for now because it's a) free and b) easier to get started from scratch than AWS.

Head over to [Heroku](https://signup.heroku.com/) and create an account or log in. Then click that **Create a new app** button:

<img alt="Screen Shot 2020-02-03 at 3 22 36 PM" src="https://user-images.githubusercontent.com/300/73703866-438c3900-46a6-11ea-9a90-bdab2fed8bff.png">

Give it a name like "redwoodblog" if it's available. Go to the **Resources** tab and then click **Find more add-ons** in the **Add-ons** section:

<img alt="Screen Shot 2020-02-03 at 3 23 25 PM" src="https://user-images.githubusercontent.com/300/73703877-4e46ce00-46a6-11ea-87c0-079346f4d9b3.png">

And scroll down to **Heroku Postgres**:

<img alt="Screen Shot 2020-02-03 at 3 23 48 PM" src="https://user-images.githubusercontent.com/300/73703883-556ddc00-46a6-11ea-8777-ee27d2202e0e.png">

Click that and then on the detail page that comes up click the **Install Heroku Postgres** button that top right. On the next screen tell it you want to connect it to the app you just created, then click **Provision add-on**:

<img alt="Screen Shot 2020-02-03 at 3 24 15 PM" src="https://user-images.githubusercontent.com/300/73703930-64548e80-46a6-11ea-9f1b-e06a183834f4.png">

You'll be returned to your app's detail page. You should be on the **Resources** tab and see the Heroku Postgres add-on ready to go:

<img alt="Screen Shot 2020-02-03 at 3 24 43 PM" src="https://user-images.githubusercontent.com/300/73703951-6ae30600-46a6-11ea-8d9b-a900b7af2ac5.png">

Click the **Heroku Postgres** link to get to the detail page, then the **Settings** tab and finally the **View Credentials...** button. We did all the steps above so that we could copy the URI listed at the bottom:

<img alt="Screen Shot 2020-02-03 at 3 25 31 PM" src="https://user-images.githubusercontent.com/300/73703956-70405080-46a6-11ea-81f2-bed99ca4c4cc.png">

It will be really long and scroll off the right side of the page so make sure you copy the whole thing!

### Netlify

Now we're going to [create a Netlify account](https://app.netlify.com/signup) if you don't have one already. Once you've signed up and verified your email done just click the **New site from Git** button at the upper right:

<img src="https://user-images.githubusercontent.com/300/73697486-85f84a80-4693-11ea-922f-0f134a3e9031.png" />

Now just authorize Netlify to connect to your git hosting provider and find your repo. When the deploy settings come up you can leave everything as the defaults and click **Deploy site**.

Netlify will start building your app (click the **Deploying your site** link to watch the logs) and it will say "Site is live", but nothing will work. Why? We haven't told it where to find our database yet.

Go back to the main site page and then to **Settings** at the top, and then **Build & Deploy** > **Environment**. Click **Edit Variables** and this is where we'll paste the database connection URI we got from Heroku (note the **Key** is "DATABASE_URL"). After pasting the value, append `?connection_limit=1` to the end. The URI will have the following format: `postgres://<user>:<pass>@<url>/<db>?connection_limit=1`.

![Adding ENV var](https://user-images.githubusercontent.com/300/83188236-3e834780-a0e4-11ea-8cfa-790c2e335a92.png)

> When configuring a database, you'll want to append `?connection_limit=1` to the URI. This is [recommended by Prisma](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-client/deployment#recommended-connection-limit) when working with relational databases in a Serverless context.

Make sure to click the **Save** button. Now go over to the **Deploys** tab in the top nav and open the **Trigger deploy** dropdown on the right, then finally choose **Deploy site**:

![Trigger deploy](https://user-images.githubusercontent.com/300/83187760-835aae80-a0e3-11ea-9733-ff54969bba1f.png)

With a little luck (and SCIENCE) it will complete successfully! You can click the **Preview** button at the top of the deploy log page, or go back and click the URL of your Netlify site towards the top:

![Netlify URL](https://user-images.githubusercontent.com/300/83187909-bef57880-a0e3-11ea-97dc-e557248acd3a.png)

Did it work? If you see "Empty" under the About and Contact links then it did! Yay! You're seeing "Empty" because you don't have any posts in your brand new production database so head to `/admin/posts` and create a couple, then go back to the homepage to see them.

> If you view a deploy via the **Preview** button notice that the URL contains a hash of the latest commit. Netlify will create one of these for every push to `main` but will only ever show this exact commit, so if you deploy again and refresh you won't see any changes. The real URL for your site (the one you get from your site's homepage in Netlify) will show the latest deploy. See [branch deploys](#branch-deploys) below for more info.

If the deploy failed, check the log output in Netlify and see if you can make sense of the error. If the deploy was successful but the site doesn't come up, try opening the web inspector and look for errors. Are you sure you pasted the entire Postgres connection string correctly? If you're really, really stuck head over to the [Redwood Community](https://community.redwoodjs.com) and ask for help.

### Branch Deploys

Another neat feature of Netlify is _Branch Deploys_. When you create a branch and push it up to your repo, Netlify will build that branch at a unique URL so that you can test your changes, leaving the main site alone. Once your branch is merged to `main` then a deploy at your main site will run and your changes will show to the world. To enable Branch Deploys go to **Settings** > **Continuous Deployment** and under the **Deploy contexts** section click **Edit settings** and change **Branch deploys** to "All". You can also enable _Deploy previews_ which will create them for any pull requests against your repo.

![Netlify settings screenshot](https://user-images.githubusercontent.com/30793/90886476-c1016780-e3b2-11ea-851a-3014257484fd.png)

> You also have the ability to "lock" the `main` branch so that deploys do not automatically occur on every push—you need to manually tell Netlify to deploy the latest, either by going to the site or using the [Netlify CLI](https://cli.netlify.com/).

### A Note About DB Connections

In this tutorial, your lambda functions will be connecting directly to the Postgres database. Because Postgres has a limited number of concurrent connections it will accept, this does not scale very well. The proper solution is to put a connection pooling service in front of Postgres and connect to that from your lambda functions. To learn how to do that, see the [Connection Pooling](/docs/connection-pooling) guide.

We are working on making this process much easier, but keep it in mind before you deploy a Redwood app to production and announce it to the world.

## Authentication

"Authentication" is a blanket term for all of the stuff that goes into making sure that a user, often identified with an email address and password, is allowed to access something. Authentication can be [famously fickle](https://www.rdegges.com/2017/authentication-still-sucks/) to do right both from a technical standpoint and developer happiness standpoint.

But you know Redwood has your back! Login isn't something we have to write from scratch—it's a solved problem and is one less thing we should have to worry about. Today Redwood includes integrations to:

- [Auth0](https://auth0.com/)
- [Netlify Identity](https://docs.netlify.com/visitor-access/identity/)

We're going to demo a Netlify Identity integration in this tutorial since we're already deployed there and it's very easy to add to a Netlify site.

> There are two terms which contain a lot of letters, starting with an "A" and ending in "ation" (which means you could rhyme them if you wanted to) that become involved in most discussions about login:
>
> * Authentication
> * Authorization
>
> Here is how Redwood uses these terms:
>
> * **Authentication** deals with determining whether someone is who they say they are, generally by "logging in" with an email and password, or a third party OAuth provider like Google.
> * **Authorization** is whether a user (who has usually already been authenticated) is allowed to do something they want to do. This generally involves some combination of roles and permission checking before allowing access to a URL or feature of your site.
>
> This section of the tutorial focuses on **Authentication** only. We're currently working on integrating a simple and flexible role-based authorization system and once we release it we'll update the tutorial to include a walkthrough!

### Netlify Identity Setup

Assuming you've been following along, you already have a Netlify account and a site set up. If you'd be so kind, head to the **Identity** tab and click the **Enable Identity** button:

![Netlify Identity screenshot](https://user-images.githubusercontent.com/300/82271191-f5850380-992b-11ea-8061-cb5f601fa50f.png)

When the screen refreshes click the **Invite users** button and enter a real email address (they're going to send a confirmation link to it):

![Netlify invite user screenshot](https://user-images.githubusercontent.com/300/82271302-439a0700-992c-11ea-9d6d-004adef3a385.png)

We'll need to get that email confirmation link soon, but for now let's set up our app for authentication.

### Authentication Generation

There are a couple of places we need to add some code for authentication and lucky for us Redwood can do it automatically with a generator:

```terminal
yarn rw g auth netlify
```

The generator adds one file and modifies a couple others.

> Don't see any changes?
>
> For this to work you must be on version `0.7.0` or greater of Redwood. If you
> don't see any file changes, try
> [upgrading](/reference/command-line-interface#upgrade) your Redwood packages
> with `yarn rw upgrade`.

Take a look at the newly created `api/src/lib/auth.js` (usage comments omitted):

```javascript
// api/src/lib/auth.js

import { AuthenticationError } from '@redwoodjs/api'

export const getCurrentUser = async (decoded, { token, type }) => {
  return decoded
}

export const requireAuth = () => {
  if (!context.currentUser) {
    throw new AuthenticationError("You don't have permission to do that.")
  }
}
```

By default the authentication system will return only the data that the third-party auth handler knows about (that's what's inside the `jwt` object above). For Netlify Identity that's an email address, an optional name and optional array of roles. Usually you'll have your own concept of a user in your local database. You can modify `getCurrentUser` to return that user, rather than the details that the auth system stores. The comments at the top of the file give one example of how you could look up a user based on their email address. We also provide a simple implementation for requiring that a user be authenticated when trying to access a service: `requireAuth()`. It will throw an error that GraphQL knows what to do with if a non-authenticated person tries to get to something they shouldn't.

The files that were modified by the generator are:

* `web/src/index.js`—wraps the router in `<AuthProvider>` which makes the routes themselves authentication aware, and gives us access to a `useAuth()` hook that returns several functions for logging users in and out, checking their current logged-inness, and more.
* `api/src/functions/graphql.js`—makes `currentUser` available to the api side so that you can check whether a user is allowed to do something on the backend. If you add an implementation to `getCurrentUser()` in `api/src/lib/auth.js` then that is what will be returned by `currentUser`, otherwise it will return just the details the auth system has for the user. If they're not logged in at all then `currentUser` will be `null`.

We'll hook up both the web and api sides below to make sure a user is only doing things they're allowed to do.

### API Authentication

First let's lock down the API so we can be sure that only authorized users can create, update and delete a Post. Open up the Post service and let's add a check:

```javascript{4,17,24,32}
// api/src/services/posts/posts.js

import { db } from 'src/lib/db'
import { requireAuth } from 'src/lib/auth'

export const posts = () => {
  return db.post.findMany()
}

export const post = ({ id }) => {
  return db.post.findOne({
    where: { id },
  })
}

export const createPost = ({ input }) => {
  requireAuth()
  return db.post.create({
    data: input,
  })
}

export const updatePost = ({ id, input }) => {
  requireAuth()
  return db.post.update({
    data: input,
    where: { id },
  })
}

export const deletePost = ({ id }) => {
  requireAuth()
  return db.post.delete({
    where: { id },
  })
}

export const Post = {
  user: (_obj, { root }) => db.post.findOne({ where: { id: root.id } }).user(),
}
```

Now try creating, editing or deleting a post from our admin pages. Nothing happens! Should we show some kind of friendly error message? In this case, probably not—we're going to lockdown the admin pages altogether so they won't be accessible by a browser. The only way someone would be able to trigger these errors in the API is if they tried to access the GraphQL endpoint directly, without going through our UI. The API is already returning an error message (open the Web Inspector in your browser and try that create/edit/delete again) so we are covered.

> Note that we're putting the authentication checks in the service and not checking in the GraphQL interface (in the SDL files).
>
> Redwood created the concept of **services** as containers for your business logic which can be used by other parts of your application besides the GraphQL API. By putting authentication checks here you can be sure that any other code that tries to create/update/delete a post will fall under the same authentication checks. In fact, Apollo (the GraphQL library Redwood uses) [agrees with us](https://www.apollographql.com/docs/apollo-server/security/authentication/#authorization-in-data-models)!

### Web Authentication

Now we'll restrict access to the admin pages completely unless you're logged in. The first step will be to denote which routes will require that you be logged in. Enter the `<Private>` tag:

```javascript{3,12,16}
// web/src/Routes.js

import { Router, Route, Private } from '@redwoodjs/router'

const Routes = () => {
  return (
    <Router>
      <Route path="/contact" page={ContactPage} name="contact" />
      <Route path="/about" page={AboutPage} name="about" />
      <Route path="/" page={HomePage} name="home" />
      <Route path="/blog-post/{id:Int}" page={BlogPostPage} name="blogPost" />
      <Private unauthenticated="home">
        <Route path="/admin/posts/new" page={NewPostPage} name="newPost" />
        <Route path="/admin/posts/{id:Int}/edit" page={EditPostPage} name="editPost" />
        <Route path="/admin/posts/{id:Int}" page={PostPage} name="post" />
        <Route path="/admin/posts" page={PostsPage} name="posts" />
      </Private>
      <Route notfound page={NotFoundPage} />
    </Router>
  )
}

export default Routes
```

Surround the routes you want to be behind authentication and optionally add the `unauthenticated` attribute that lists the name of another route to redirect to if the user is not logged in. In this case we'll go back to the homepage.

Try that in your browser. If you hit http://localhost:8910/admin/posts you should immediately go back to the homepage.

Now all that's left to do is let the user actually log in! If you've built authentication before then you know this part is usually a drag, but Redwood makes it a walk in the park. Most of the plumbing was handled by the auth generator, so we get to focus on the parts the user actually sees. First, let's add a **Login** link that will trigger a modal from the [Netlify Identity widget](https://github.com/netlify/netlify-identity-widget). Let's assume we want this on all of the public pages, so we'll put it in the `BlogLayout`:

```javascript{4,7,22-26}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'
import { useAuth } from '@redwoodjs/auth'

const BlogLayout = ({ children }) => {
  const { logIn } = useAuth()

  return (
    <div>
      <h1>
        <Link to={routes.home()}>Redwood Blog</Link>
      </h1>
      <nav>
        <ul>
          <li>
            <Link to={routes.about()}>About</Link>
          </li>
          <li>
            <Link to={routes.contact()}>Contact</Link>
          </li>
          <li>
            <a href="#" onClick={logIn}>
              Log In
            </a>
          </li>
        </ul>
      </nav>
      <main>{children}</main>
    </div>
  )
}

export default BlogLayout
```

Try clicking the login link:

![Netlify Identity Widget modal](https://user-images.githubusercontent.com/300/82387730-aa7ef500-99ec-11ea-9a40-b52b383f99f0.png)

We need to let the widget know the URL of our site so it knows where to go to get user data and confirm they're able to log in. Back over to Netlify, you can get that from the Identity tab:

![Netlify site URL](https://user-images.githubusercontent.com/300/82387937-28430080-99ed-11ea-91b7-a4e10f14aa83.png)

You need the protocol and domain, not the rest of the path. Paste that into the modal and click that **Set site's URL** button. The modal should reload and now show a real login box:

![Netlify identity widget login](https://user-images.githubusercontent.com/300/82388116-97205980-99ed-11ea-8fb4-13436ee8e746.png)

Before we can log in, remember that confirmation email from Netlify? Go find that and click the **Accept the invite** link. That will bring you to your site live in production, where nothing will happen. But if you look at the URL it will end in something like `#invite_token=6gFSXhugtHCXO5Whlc5V`. Copy that (including the `#`) and appened it to your localhost URL: http://localhost:8910/#invite_token=6gFSXhugtHCXO5Whlc5Vg Hit Enter, then go back into the URL and hit Enter again to get it to actually reload the page. Now the modal will show **Complete your signup** and give you the ability to set your password:

![Netlify identity set password](https://user-images.githubusercontent.com/300/82388369-54ab4c80-99ee-11ea-920e-9df10ee0cac2.png)

Once you do that the modal should update and say that you're logged in! It worked! Click the X in the upper right to close the modal.

> We know that invite acceptance flow is less than ideal. The good news is that once you deploy your site again with authentication, future invites will work automatically—the link will go to production which will now have the code needed to launch the modal and let you accept the invite.

We've got no indication on our actual site that we're logged in, however. How about changing the **Log In** button to be **Log Out** when you're authenticated:

```javascript{7,23-24}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'
import { useAuth } from '@redwoodjs/auth'

const BlogLayout = ({ children }) => {
  const { logIn, logOut, isAuthenticated } = useAuth()

  return (
    <div>
      <h1>
        <Link to={routes.home()}>Redwood Blog</Link>
      </h1>
      <nav>
        <ul>
          <li>
            <Link to={routes.about()}>About</Link>
          </li>
          <li>
            <Link to={routes.contact()}>Contact</Link>
          </li>
          <li>
            <a href="#" onClick={isAuthenticated ? logOut : logIn}>
              {isAuthenticated ? 'Log Out' : 'Log In'}
            </a>
          </li>
        </ul>
      </nav>
      <main>{children}</main>
    </div>
  )
}

export default BlogLayout
```

`useAuth()` provides a couple more helpers for us, in this case `isAuthenticated` which will return `true` or `false` based on your login status, and `logOut()` which will log the user out. Now clicking **Log Out** should log you out and change the link to **Log In** which you can click to open the modal and log back in again.

When you *are* logged in, you should be able to access the admin pages again: http://localhost:8910/admin/posts

> If you start working on another Redwood app that uses Netlify Identity you'll need to manually clear out your Local Storage which is where the site URL is stored that you entered the first time you saw the modal. Local Storage is tied to your domain and port, which by default will be the same for any Redwood app when developing locally. You can clear your Local Storage in Chrome by going to the Web Inspector, the **Application** tab, and then on the left open up **Local Storage** and click on http://localhost:8910. You'll see the keys stored on the right and can delete them all.

One more touch: let's show the email address of the user that's logged in. We can get the `currentUser` from `useAuth()` and it will contain the data that our third party authentication library is storing about the currently logged in user:

```javascript{7,27}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'
import { useAuth } from '@redwoodjs/auth'

const BlogLayout = ({ children }) => {
  const { logIn, logOut, isAuthenticated, currentUser } = useAuth()

  return (
    <div>
      <h1>
        <Link to={routes.home()}>Redwood Blog</Link>
      </h1>
      <nav>
        <ul>
          <li>
            <Link to={routes.about()}>About</Link>
          </li>
          <li>
            <Link to={routes.contact()}>Contact</Link>
          </li>
          <li>
            <a href="#" onClick={isAuthenticated ? logOut : logIn}>
              {isAuthenticated ? 'Log Out' : 'Log In'}
            </a>
          </li>
          {isAuthenticated && <li>{currentUser.email}</li>}
        </ul>
      </nav>
      <main>{children}</main>
    </div>
  )
}

export default BlogLayout
```

![Logged in email](https://user-images.githubusercontent.com/300/82389433-05b2e680-99f1-11ea-9d01-456cad508c80.png)

> Check out the settings for Identity over at Netlify for more options, including allowing users to create accounts rather than having to be invited, add third party login buttons for Bitbucket, GitHub, GitLab and Google, receive webhooks when someone logs in, and more!

Believe it or not, that's it! Authentication with Redwood is a breeze and we're just getting started. Expect more magic soon!

> If you inspect the contents of `currentUser` you'll see it contains an array called `roles`. On the Netlify Identity dashboard you can give your user a collection of roles, which are just strings like "admin" or "guest". Using this array of roles you *could* create a very rudimentary role-based authentication system. Unless you are in dire need of this simple role checking, we recommend waiting for the Redwood solution, coming soon!

## Wrapping Up

You made it! If you really went through the whole tutorial: congratulations! If you just skipped ahead to this page to try and get a free congratulations: tsk, tsk!

That was potentially a lot of new concepts to absorb all at once so don't feed bad if all of it didn't fully sink in. React, GraphQL, Prisma, serverless functions...so many things! Even those of us working on the framework are heading over to Google multiple times per day to figure out how to get these things to work together.

As an anonymous Twitter user once mused: "If you enjoy feeling like both the smartest person on earth and the dumbest person in history within a span of 24 hours, programming may be the career for you!"

### What's Next?

Want to add some more features to your app? Check out some of our Cookbook recipies like [calling to a third party API](/cookbook/using-a-third-party-api) and [deploying an app without an API at all](/cookbook/disable-api-database). Have you grown out of SQLite and want to [install Postgres locally](/docs/local-postgres-setup)? We've also got lots of [guides](/docs/introduction) for more info on Redwood's internals.

### Roadmap

Check out our [Roadmap](https://redwoodjs.com/roadmap) to see where we're headed and how we're going to get there.
If you're interested in helping with anything you see, just let us know over on the [RedwoodJS Forum](https://community.redwoodjs.com/) and we'll be happy to get you set up.
We want to hit `1.0` by the end of the year. And with your help, we think we can do it!

### Help Us!

What did you think of Redwood? Is it the Next Step for JS frameworks? What can it do better? We've got a lot more planned. Want to help us build these upcoming features?

- [Open a PR](https://github.com/redwoodjs/redwood/pulls)
- [Write some docs](/docs/introduction)
- [Join the community](https://community.redwoodjs.com)

Thanks for following along. Now go out and build something amazing!
