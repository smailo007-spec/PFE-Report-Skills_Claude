---
name: pfe-content-improver
description: "Use this skill when the user wants to correct, improve, rewrite, or enhance the academic content of a PFE report. Triggers include: 'corriger mon rapport', 'améliorer mon texte', 'reformuler', 'vérifier la cohérence', 'améliorer la qualité académique', 'corriger les fautes', 'rendre mon texte plus professionnel', 'améliorer mon introduction/conclusion/chapitre'. Use for any request to refine written content in a PFE report (Word or text). Do NOT use for formatting/styling tasks — use pfe-docx-formatter instead."
---

# PFE Content Improver — Amélioration du contenu académique

## Objectif
Corriger et améliorer le contenu rédigé d'un rapport PFE pour atteindre un niveau académique professionnel.

---

## Workflow d'amélioration en 5 étapes

### Étape 1 — Extraction du contenu
```bash
# Extraire le texte du DOCX
extract-text rapport_pfe.docx > contenu_brut.txt

# Ou via pandoc pour garder la structure
pandoc rapport_pfe.docx -o contenu.md
```

### Étape 2 — Analyse de la structure
Vérifier la présence et la cohérence de :
- [ ] Introduction générale (contexte, problématique, objectifs, plan)
- [ ] Chapitres (introduction de chapitre, corps, conclusion de chapitre)
- [ ] Conclusion générale (synthèse, apports, perspectives)
- [ ] Transitions entre sections

### Étape 3 — Corrections à appliquer
### Étape 4 — Réinjection dans le DOCX
### Étape 5 — Validation finale

---

## Règles d'écriture académique PFE

### Style
| ❌ À éviter | ✅ Remplacer par |
|------------|----------------|
| "j'ai fait" | "nous avons réalisé" / "il a été procédé à" |
| "c'est bien" | "cela présente l'avantage de" |
| "beaucoup de" | "un nombre important de" / "plusieurs" |
| "très important" | "particulièrement significatif" |
| "on voit que" | "il ressort de cette analyse que" |
| phrases trop courtes | phrases structurées avec connecteurs logiques |

### Connecteurs logiques à utiliser
- **Cause** : en effet, car, étant donné que, puisque
- **Conséquence** : ainsi, par conséquent, c'est pourquoi, de ce fait
- **Opposition** : cependant, néanmoins, toutefois, en revanche
- **Addition** : de plus, par ailleurs, également, en outre
- **Illustration** : par exemple, notamment, à titre d'illustration
- **Conclusion** : en conclusion, en définitive, pour résumer

---

## Templates de sections clés

### Introduction générale
```
[Contexte général du domaine]
Dans un contexte de [domaine/secteur], [problème général observé].
Cette réalité soulève des défis majeurs, notamment [défis spécifiques].

[Problématique]
Face à ces enjeux, la question centrale de ce travail est :
« [Question de recherche principale ?] »

[Objectifs]
Ce projet vise à atteindre les objectifs suivants :
- Objectif 1 : [...]
- Objectif 2 : [...]
- Objectif 3 : [...]

[Plan du rapport]
Pour répondre à cette problématique, ce rapport est structuré en [N] chapitres :
- Le premier chapitre présente [...]
- Le deuxième chapitre aborde [...]
- Le troisième chapitre détaille [...]
- Enfin, une conclusion générale synthétise [...]
```

### Introduction de chapitre
```
Ce chapitre est consacré à [sujet du chapitre].
Dans un premier temps, nous présenterons [section 1].
Ensuite, nous analyserons [section 2].
Enfin, nous conclurons par [section 3].
```

### Conclusion de chapitre
```
En résumé, ce chapitre nous a permis de [synthèse des points clés].
Nous avons notamment mis en évidence que [point important 1] et que [point important 2].
Ces éléments constituent le socle nécessaire pour aborder le chapitre suivant,
qui traitera de [sujet du prochain chapitre].
```

### Conclusion générale
```
[Rappel de la problématique]
Ce travail avait pour objectif principal de [rappel de l'objectif].

[Synthèse des résultats]
Au terme de cette étude, les principaux résultats obtenus sont :
- [Résultat 1]
- [Résultat 2]
- [Résultat 3]

[Apports du travail]
Ce projet contribue à [domaine] en proposant [apport principal].

[Limites]
Néanmoins, ce travail présente certaines limites, notamment [limite principale].

[Perspectives]
En perspective, il serait intéressant d'envisager [piste future 1]
et d'explorer [piste future 2] afin d'approfondir les résultats obtenus.
```

---

## Code Python — Amélioration automatique avec suivi des modifications

```python
import subprocess
import shutil
import os

def extract_content(docx_path):
    """Extrait le texte du DOCX en markdown."""
    result = subprocess.run(
        ["pandoc", docx_path, "-o", "contenu.md"],
        capture_output=True, text=True
    )
    with open("contenu.md", "r", encoding="utf-8") as f:
        return f.read()

def apply_style_corrections(text):
    """Applique des corrections de style académique basiques."""
    corrections = {
        "j'ai ": "nous avons ",
        "j'ai fait": "nous avons réalisé",
        "on a ": "nous avons ",
        "on voit": "il ressort",
        "beaucoup de": "un nombre important de",
        "très important": "particulièrement significatif",
        "c'est bien": "cela présente l'avantage",
        "facile": "aisé",
        "difficile à": "complexe à",
    }
    for wrong, correct in corrections.items():
        text = text.replace(wrong, correct)
    return text

def check_structure(text):
    """Vérifie la présence des sections obligatoires."""
    required_sections = [
        "Introduction générale",
        "Conclusion générale",
        "Bibliographie"
    ]
    missing = []
    for section in required_sections:
        if section.lower() not in text.lower():
            missing.append(section)
    return missing

def improve_document(docx_path):
    """Workflow complet d'amélioration."""
    print(f"📄 Traitement de : {docx_path}")

    # 1. Extraire
    content = extract_content(docx_path)
    print("✅ Contenu extrait")

    # 2. Vérifier la structure
    missing = check_structure(content)
    if missing:
        print(f"⚠️  Sections manquantes : {', '.join(missing)}")
    else:
        print("✅ Structure complète")

    # 3. Appliquer les corrections
    improved = apply_style_corrections(content)
    print("✅ Corrections de style appliquées")

    # 4. Sauvegarder le markdown corrigé
    with open("contenu_ameliore.md", "w", encoding="utf-8") as f:
        f.write(improved)

    # 5. Reconvertir en DOCX
    subprocess.run([
        "pandoc", "contenu_ameliore.md",
        "-o", "rapport_ameliore.docx",
        "--reference-doc", docx_path  # Garde les styles du doc original
    ])
    print("✅ rapport_ameliore.docx généré")

    return missing

if __name__ == "__main__":
    missing = improve_document("rapport_pfe.docx")
    if missing:
        print(f"\n📋 À ajouter manuellement : {missing}")
```

---

## Checklist de relecture finale

### Fond
- [ ] La problématique est clairement posée dans l'introduction
- [ ] Chaque chapitre commence par une introduction et se termine par une conclusion
- [ ] Les transitions entre chapitres sont présentes
- [ ] Les figures et tableaux sont légendés et référencés dans le texte
- [ ] La bibliographie correspond aux sources citées dans le texte

### Forme
- [ ] Pas de "je" — utiliser "nous" ou la forme passive
- [ ] Phrases complètes (sujet + verbe + complément)
- [ ] Pas d'abréviations non définies au préalable
- [ ] Cohérence des temps verbaux (présent de vérité générale)
- [ ] Ponctuation correcte (espace avant ":" et ";" en français)

### Technique
- [ ] Toutes les figures sont numérotées (Figure 1, Figure 2...)
- [ ] Toutes les références bibliographiques sont au format IEEE ou APA
- [ ] Les acronymes sont définis à leur première apparition
