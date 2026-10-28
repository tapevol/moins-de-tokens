# Moins de tokens

**4 habitudes qui vident ta limite Claude, et quoi faire à la place.**
Le repo de la vidéo [@tapevol_ia](https://www.instagram.com/tapevol_ia/). Version courte, à copier en un geste : **[tapevol.vercel.app/tokens](https://tapevol.vercel.app/tokens)**

## Le prompt à coller dans Claude

Dans claude.ai : **Paramètres → Profil → Préférences personnelles**, colle ce bloc et enregistre.
(Ou, pour un seul projet : ouvre le Projet → **Instructions** → colle-le.)

```text
Réponds court et direct : pas de politesse, pas de reformulation, pas de résumé final. Style télégraphique, listes plutôt que paragraphes. Développe seulement si j'écris « détaille ».
Pour du code : seulement les lignes qui changent.
N'utilise la recherche web que si je la demande.
Si je change de sujet ou si la conversation devient longue, dis-le en une ligne et propose un résumé de 5 lignes à coller dans une nouvelle conversation.
```

Tu utilises **Claude Code** ? Mets plutôt [`CLAUDE.md`](./CLAUDE.md) à la racine de ton projet (ou dans `~/.claude/CLAUDE.md` pour tous tes projets).

---

## 1. Les PDF

Chaque page de PDF coûte **entre 1 500 et 3 000 tokens** rien qu'en texte (selon la doc d'Anthropic), et Claude reçoit souvent aussi chaque page en image. Un rapport de 40 pages peut vider une bonne partie de ta limite en un message.

**À la place :** convertis-le en texte avec [MarkItDown](https://github.com/microsoft/markitdown), l'outil gratuit de Microsoft, puis envoie le `.md`.

```bash
pip install 'markitdown[all]'
markitdown rapport.pdf -o rapport.md
```

(Python 3.10 ou plus. Ça marche aussi pour Word, Excel et PowerPoint.)
Garde le PDF seulement quand Claude doit *voir* la page : graphiques, schémas, mise en page.

## 2. La recherche web et les connecteurs

Chaque résultat de recherche, chaque page lue par un connecteur (Drive, Gmail, etc.) **reste dans la conversation** et est relu à chaque message suivant.

**À la place :** dans la conversation, ouvre le menu des outils (sous la zone de texte) et **désactive la recherche web et les connecteurs** dont tu n'as pas besoin. Rallume-les seulement pour la question qui en a besoin.

## 3. Les réponses trop longues

Les formules de politesse, les reformulations et les récapitulatifs coûtent des tokens à chaque réponse.

**À la place :** le prompt plus haut demande des réponses courtes. Et si tu codes avec Claude Code, essaie [caveman](https://github.com/JuliusBrussee/caveman) (plus de 100 000 étoiles), qui fait parler Claude en style télégraphique. D'après ses tests, ça retire **65 % des tokens** de ses réponses.

```bash
npx @caveman-ai/cli@latest
```

(Node.js 22.13 ou plus. Le README de caveman donne les autres façons de l'installer, dont l'app Claude.)

## 4. La conversation ouverte depuis ce matin

La plus coûteuse : à chaque message, **Claude relit toute la conversation**. Une conversation de 3 heures fait payer tout son historique, même pour une question d'une ligne.

**À la place :** un sujet = une conversation. Quand tu changes de sujet, ouvre-en une nouvelle. Si tu as besoin du contexte, demande d'abord à Claude un résumé en 5 lignes et colle-le dans la nouvelle (le prompt plus haut le propose tout seul).
Dans Claude Code : `/clear` entre deux tâches, `/compact` pour alléger sans repartir de zéro.

---

Ça t'a fait gagner des messages ? Dis-le-moi en commentaire sur [@tapevol_ia](https://www.instagram.com/tapevol_ia/) 👀
