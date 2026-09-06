# Référentiel technique

Portail de documentation d'architecture et d'exploitation, organisé par technologie.

**Accès :** https://siradio.github.io/ressources/

## Contenu

| Technologie | Documents |
|---|---|
| Talend | Remote Engine · Talend Runtime ESB · Développement Routes & Services · Laboratoire de diagnostic · Audit de sécurité · Mémento des commandes |
| Organisation | Intégration Euromaster · Carnet d'intégration |
| Azure | Azure Service Bus |

Neuf documents, 116 chapitres. Chaque entrée du menu est une technologie, chaque
sous-entrée un document, et chaque document expose ses chapitres en troisième niveau.

## Accès protégé

Le contenu de `index.html` est **chiffré** :

- AES-256-GCM ;
- clé dérivée de l'identifiant et du mot de passe par PBKDF2-HMAC-SHA256, 310 000 itérations ;
- déchiffrement réalisé dans le navigateur via WebCrypto.

Le fichier publié ne contient donc aucun texte lisible : sans le mot de passe, il n'y a
rien à extraire du code source de la page.

**Les identifiants ne figurent pas dans ce dépôt.** Ils sont transmis séparément.

## Le carnet d'intégration

Un des documents est un bloc-notes : il enregistre la saisie au fil de la frappe dans le
**stockage local du navigateur** (`localStorage`), sous la clé `carnet-euromaster-v1`.

- Les notes ne quittent jamais la machine : elles ne sont ni transmises, ni publiées,
  ni incluses dans ce dépôt.
- Elles ne sont **pas chiffrées** : le mot de passe protège le contenu publié, pas la
  saisie. N'y consigner ni mot de passe, ni jeton, ni donnée personnelle.

Pour les retrouver depuis un autre navigateur ou une autre machine, le document permet
de **lier un fichier `.json`** choisi par l'utilisateur (File System Access API, donc
Chrome et Edge sur poste de travail) : le carnet y écrit à chaque modification et le
relit à l'ouverture. Placé dans un dossier synchronisé, ce fichier suit le poste.

La relecture **fusionne entrée par entrée** en gardant la plus récente, l'égalité
conservant la version locale : deux postes ayant travaillé en parallèle ne s'écrasent
pas. Aucun service tiers, aucun jeton, rien de tout cela n'est stocké dans ce dépôt.
Le handle du fichier est conservé dans l'IndexedDB `carnet-euromaster` du navigateur.

Dans les navigateurs sans cette interface, l'export `.json` et l'export Markdown
restent la voie universelle.

## Prérequis navigateur

WebCrypto exige un contexte sécurisé. La page fonctionne servie en **https**
(GitHub Pages) ou depuis `localhost`. Ouverte directement en `file://`, le
déchiffrement est indisponible et la page l'indique explicitement.

## Limites à connaître

- Ce dépôt est public : le fichier chiffré est téléchargeable par tous. La confidentialité
  repose entièrement sur la robustesse du mot de passe, une attaque hors ligne restant
  toujours possible. Pour une confidentialité forte, utiliser un dépôt privé.
- Toute personne disposant du mot de passe accède à l'intégralité du contenu et peut
  le rediffuser.
- Le mécanisme protège le contenu au repos, il ne constitue pas un contrôle d'accès
  par utilisateur : il n'y a ni comptes distincts, ni révocation individuelle, ni
  journal d'accès.

## Régénérer le document

Le générateur et les sources non chiffrées sont conservés hors de ce dépôt.
Changer le mot de passe consiste à relancer la génération puis à remplacer `index.html`.
