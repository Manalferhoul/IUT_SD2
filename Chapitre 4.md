# Chapitre 4 : Initiation au R Markdown

- [Chapitre 4 : Initiation au R Markdown](#chapitre-4--initiation-au-r-markdown)
  - [Objectifs](#objectifs)
  - [Pratique](#pratique)
  - [Liens utiles](#liens-utiles)


## Objectifs

Voici les objectifs de ce module :
- [x] Créer un Rmarkdown
- [x] Utiliser les options des Chunks
- [x] Afficher des tableaux
- [x] Utiliser des variables
- [x] Utiliser des paramètres

## Pratique

1. En-tête de métadonnées (YAML)

```yaml
---
title: "Mon Cours RMarkdown"
author: "Nom de l'auteur"
output: word_document
---
```

2. Syntaxe de base pour les chunks de code R

````markdown
```{r}
# Ceci est un chunk de code R
summary(iris)
```
````

3. Ajouter des titres
   
```
# Titre 1
## Sous-titre 2
```

4. Texte en gras ou en italique

```
*Texte en italique*
**Texte en gras**
```

5. Options principales des chunks de code

- **`echo`** : Affiche ou non le code.
- **`eval`** : Exécute ou non le code.
- **`warning`** : Affiche ou non les warnings.
- **`message`** : Affiche ou non les messages.

````markdown
```{r, eval=FALSE}
install.packages("knitr")
```
````

6. Option par défaut des chunks
````markdown
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
````

7. Créer des tableaux élégants avec `kable`

````markdown
```{r, echo=FALSE}
library(knitr)
kable(head(iris), caption = "Tableau des premières lignes du jeu de données iris")
```
````

8. Utilisation de variables R dans les chunks

````markdown
```{r}
mean_petal_length <- mean(iris$Petal.Length)
```
````

La longueur moyenne des pétales est : \`r mean_petal_length\`.

9. Paramètres en en-tête de métadonnées (YAML)

```yaml
---
title: "Mon Cours RMarkdown"
author: "Nom de l'auteur"
date: "`r Sys.Date()`"
output: word_document
params:
  mon_parametre: "Sepal.Width"
---
```

:bulb: La fonction `get(params)` permet d'accéder dynamiquement à la colonne du jeu de données iris correspondant au paramètre passé.

````markdown
```{r warning = FALSE, echo  = FALSE}
# Chargement du jeu de données iris et de ggplot2
library(ggplot2)

# Récupérer le paramètre passé dans le YAML
param <- params$mon_parametre

# Créer un boxplot en croisant la variable Species et le paramètre
ggplot(iris, aes(x = Species, y = get(param))) + 
  geom_boxplot() +
  labs(y = param, title = paste("Boxplot de", param, "par Species"))
```
````

10. Utiliser la valeur d'un paramètre dans du texte
    
La colonne sélectionnée est \`\`r params$mon_parametre\`\`

<details>
<summary>Vous avez terminé ?</summary>

<img src="./img/congratulation.gif" alt="" style="height: 300px;">

</details>

## Liens utiles

Voici quelques liens utiles :

- [Initiation au R Markdown](https://rmarkdown.rstudio.com/lesson-1.html)
- [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)
