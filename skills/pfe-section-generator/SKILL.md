---
name: pfe-section-generator
description: "Use this skill when the user wants to automatically generate missing sections of a PFE report, or generate a full structured plan for their report. Triggers include: 'générer mon résumé', 'écrire mon abstract', 'générer les remerciements', 'créer l'introduction', 'rédiger la conclusion', 'faire le plan de mon PFE', 'générer la bibliographie', 'écrire les annexes', 'générer une section manquante'. Use when the user provides a topic/theme and wants Claude to produce ready-to-use content for specific PFE sections. Do NOT use for formatting tasks — use pfe-docx-formatter instead."
---

# PFE Section Generator — Génération automatique de sections

## Objectif
Générer automatiquement les sections manquantes ou complètes d'un rapport PFE, prêtes à être insérées dans le document DOCX.

---

## Informations à collecter avant génération

Demander à l'utilisateur :
1. **Thème/Titre du PFE** : ex. "Développement d'une application web de gestion RH"
2. **Technologies utilisées** : ex. "React, Node.js, MongoDB"
3. **Domaine** : ex. "Génie logiciel / Systèmes d'information"
4. **Université & Filière** : ex. "FSTF — Master ISRS"
5. **Résultats principaux** : ex. "Application déployée, gain de 40% en efficacité"
6. **Section à générer** : résumé, abstract, remerciements, introduction, conclusion, bibliographie...

---

## Templates de génération par section

### 🔷 Résumé (Français)
```
Ce rapport présente le travail réalisé dans le cadre du Projet de Fin d'Études
intitulé « [TITRE] », effectué au sein de [ENTREPRISE/LABORATOIRE].

Dans un contexte de [DOMAINE], ce projet répond à la problématique suivante :
[PROBLÉMATIQUE].

Pour y répondre, nous avons [APPROCHE MÉTHODOLOGIQUE].
Les principales étapes de ce travail comprennent [ÉTAPE 1], [ÉTAPE 2] et [ÉTAPE 3].

Les résultats obtenus montrent que [RÉSULTATS PRINCIPAUX].
Ce projet contribue à [APPORT PRINCIPAL] et ouvre des perspectives vers [PISTE FUTURE].

Mots-clés : [MOT-CLÉ 1], [MOT-CLÉ 2], [MOT-CLÉ 3], [MOT-CLÉ 4]
```

### 🔷 Abstract (English)
```
This report presents the work carried out as part of the Final Year Project
entitled "[TITRE EN ANGLAIS]", conducted at [ENTREPRISE/LABORATOIRE].

In the context of [DOMAIN], this project addresses the following research question:
[PROBLÉMATIQUE EN ANGLAIS].

To address this challenge, we [APPROCHE EN ANGLAIS].
The main stages of this work include [ÉTAPE 1], [ÉTAPE 2], and [ÉTAPE 3].

The results demonstrate that [RÉSULTATS EN ANGLAIS].
This project contributes to [APPORT] and opens perspectives towards [PISTE FUTURE].

Keywords: [KEYWORD 1], [KEYWORD 2], [KEYWORD 3], [KEYWORD 4]
```

### 🔷 Remerciements
```
Au terme de ce travail, nous tenons à exprimer notre profonde gratitude
à toutes les personnes qui ont contribué, de près ou de loin,
à la réalisation de ce projet.

Nous adressons nos sincères remerciements à notre encadrant(e),
[PRÉNOM NOM], [TITRE], pour ses précieux conseils, sa disponibilité
et son suivi tout au long de ce projet.

Nos remerciements vont également à l'ensemble du corps professoral
de [DÉPARTEMENT/FILIÈRE] pour la qualité de la formation dispensée.

Nous remercions aussi [PERSONNE/ÉQUIPE EN ENTREPRISE] pour
leur accueil chaleureux et leur accompagnement lors de notre stage.

Enfin, nous exprimons toute notre reconnaissance à notre famille et
à nos proches pour leur soutien indéfectible tout au long de notre parcours.
```

### 🔷 Introduction générale
```
[PARAGRAPHE 1 — Contexte général]
Le domaine de [DOMAINE] connaît aujourd'hui des transformations profondes,
portées par [FACTEUR DÉCLENCHEUR : digitalisation, IA, mondialisation...].
Dans ce contexte, [PROBLÈME GÉNÉRAL OBSERVÉ].

[PARAGRAPHE 2 — Problématique]
Face à ces enjeux, [ORGANISME/SECTEUR] est confronté à [PROBLÈME SPÉCIFIQUE].
Cela soulève une question centrale : [QUESTION DE RECHERCHE ?]

[PARAGRAPHE 3 — Objectifs]
Pour répondre à cette problématique, ce projet se fixe les objectifs suivants :
- Analyser [OBJECTIF 1]
- Concevoir [OBJECTIF 2]
- Implémenter et valider [OBJECTIF 3]

[PARAGRAPHE 4 — Plan du rapport]
Ce rapport est organisé en [N] chapitres :
— Le Chapitre I intitulé « [TITRE CH.1] » présente [CONTENU CH.1].
— Le Chapitre II intitulé « [TITRE CH.2] » aborde [CONTENU CH.2].
— Le Chapitre III intitulé « [TITRE CH.3] » détaille [CONTENU CH.3].
— Une conclusion générale synthétise les apports du travail et
  trace les perspectives d'évolution.
```

### 🔷 Conclusion générale
```
[PARAGRAPHE 1 — Rappel de la problématique]
Ce travail avait pour objectif principal de [RAPPEL OBJECTIF PRINCIPAL],
en réponse à la problématique : [RAPPEL PROBLÉMATIQUE].

[PARAGRAPHE 2 — Synthèse des travaux]
Pour y parvenir, nous avons suivi une démarche structurée en [N] étapes.
Dans un premier temps, nous avons [ÉTAPE 1].
Ensuite, [ÉTAPE 2].
Enfin, [ÉTAPE 3].

[PARAGRAPHE 3 — Résultats et apports]
Les résultats obtenus sont encourageants : [RÉSULTAT PRINCIPAL].
Ce projet apporte une contribution concrète à [DOMAINE] en proposant [APPORT].

[PARAGRAPHE 4 — Limites]
Toutefois, ce travail présente certaines limites qu'il convient de mentionner :
[LIMITE 1] et [LIMITE 2].

[PARAGRAPHE 5 — Perspectives]
À court terme, il serait pertinent de [PISTE 1].
À plus long terme, l'intégration de [TECHNOLOGIE/APPROCHE] pourrait permettre
d'améliorer [ASPECT À AMÉLIORER].
```

### 🔷 Bibliographie (Format IEEE)
```
[1]  Auteur1, Auteur2, "Titre de l'article," Nom du Journal/Conférence, vol. X, no. Y, pp. Z-Z, Année.
[2]  Auteur, Titre du livre, Édition. Ville : Éditeur, Année.
[3]  Auteur, "Titre de la page web," [En ligne]. Disponible sur : URL. [Consulté le : JJ/MM/AAAA].

-- Exemples selon le thème --
[Pour le développement web]
[1]  T. Powell, HTML & CSS: The Complete Reference. New York : McGraw-Hill, 2010.
[2]  A. Banks, E. Porcello, Learning React. Sebastopol : O'Reilly Media, 2020.

[Pour l'IA / Machine Learning]
[1]  I. Goodfellow, Y. Bengio, A. Courville, Deep Learning. Cambridge : MIT Press, 2016.
[2]  A. Géron, Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow. O'Reilly, 2022.

[Pour les systèmes d'information]
[1]  R. Kimball, M. Ross, The Data Warehouse Toolkit. Indianapolis : Wiley, 2013.
```

---

## Script Python — Génération automatique de sections

```python
def generate_section(section_type, info):
    """
    Génère une section PFE à partir d'un template.
    
    section_type : 'resume', 'abstract', 'remerciements',
                   'introduction', 'conclusion', 'bibliographie'
    info : dict avec les informations du PFE
    """
    
    templates = {
        "resume": """Ce rapport présente le travail réalisé dans le cadre du Projet de Fin d'Études
intitulé « {titre} », effectué au sein de {lieu}.

Dans un contexte de {domaine}, ce projet répond à la problématique :
{problematique}

Les résultats obtenus montrent que {resultats}.

Mots-clés : {mots_cles}""",

        "remerciements": """Au terme de ce travail, nous tenons à exprimer notre profonde gratitude
à toutes les personnes qui ont contribué à la réalisation de ce projet.

Nous adressons nos sincères remerciements à notre encadrant(e),
{encadrant}, pour ses précieux conseils et son suivi constant.

Nos remerciements vont également à l'ensemble du corps professoral
de {departement} pour la qualité de la formation dispensée.

Enfin, nous exprimons toute notre reconnaissance à notre famille et
à nos proches pour leur soutien indéfectible.""",

        "conclusion": """Ce travail avait pour objectif principal de {objectif_principal}.

Les résultats obtenus sont encourageants : {resultats}.
Ce projet apporte une contribution concrète à {domaine}
en proposant {apport}.

Toutefois, ce travail présente certaines limites : {limites}.

En perspective, il serait pertinent d'explorer {perspectives}."""
    }
    
    if section_type not in templates:
        return f"⚠️ Section '{section_type}' non reconnue."
    
    return templates[section_type].format(**info)


# ── EXEMPLE D'UTILISATION ──────────────────────────────────────────
if __name__ == "__main__":
    info_pfe = {
        "titre": "Développement d'une plateforme web de gestion des ressources humaines",
        "lieu": "Entreprise XYZ, Casablanca",
        "domaine": "génie logiciel et systèmes d'information",
        "problematique": "Comment optimiser la gestion RH via une solution numérique intégrée ?",
        "resultats": "la plateforme développée réduit le temps de traitement RH de 40%",
        "mots_cles": "Gestion RH, Application web, React, Node.js, Base de données",
        "encadrant": "Pr. Mohammed Alami",
        "departement": "Département Informatique",
        "objectif_principal": "développer une plateforme web de gestion RH",
        "apport": "une solution digitale intégrée, accessible et évolutive",
        "limites": "l'absence de module de reporting avancé",
        "perspectives": "l'intégration de l'IA pour l'analyse prédictive des données RH"
    }
    
    sections_a_generer = ["resume", "remerciements", "conclusion"]
    
    for section in sections_a_generer:
        print(f"\n{'='*60}")
        print(f"  SECTION : {section.upper()}")
        print('='*60)
        print(generate_section(section, info_pfe))
    
    print("\n✅ Sections générées avec succès !")
```

---

## Intégration dans le DOCX

Une fois les sections générées, les injecter dans le document :

```bash
# 1. Extraire le contenu existant
pandoc rapport_pfe.docx -o rapport.md

# 2. Ajouter les sections générées au bon endroit dans rapport.md

# 3. Reconvertir en DOCX en conservant les styles
pandoc rapport.md -o rapport_complet.docx --reference-doc rapport_pfe.docx
```

---

## Plan type recommandé pour un PFE

```
Chapitre I   — État de l'art / Étude bibliographique
  1.1 Contexte et domaine
  1.2 Solutions existantes
  1.3 Analyse comparative
  1.4 Positionnement du projet

Chapitre II  — Analyse et conception
  2.1 Spécifications fonctionnelles
  2.2 Architecture générale
  2.3 Modélisation (UML / Merise...)
  2.4 Choix technologiques

Chapitre III — Réalisation et tests
  3.1 Environnement de développement
  3.2 Implémentation
  3.3 Tests et validation
  3.4 Résultats et évaluation
```
