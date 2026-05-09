---
name: pfe-docx-formatter
description: "Use this skill when the user wants to format, style, or structure a PFE (Projet de Fin d'Études) report in DOCX format. Triggers include: 'mettre en forme mon rapport', 'formatter mon PFE', 'appliquer les styles', 'mise en page rapport', 'titres et marges PFE', 'page de garde', 'table des matières', 'numérotation des pages'. Also use when the user asks to apply academic formatting standards to a Word document, fix heading hierarchy, set margins/fonts, or produce a polished university report. Do NOT use for PDF creation or content writing."
---

# PFE DOCX Formatter — Mise en forme académique de rapports

## Objectif
Appliquer une mise en forme professionnelle et académique à un rapport PFE (Projet de Fin d'Études) au format DOCX.

---

## Stack technique
- **Langage** : JavaScript (Node.js)
- **Librairie** : `docx` → `npm install -g docx`
- **Validation** : `python scripts/office/validate.py`
- **Conversion** : LibreOffice via `scripts/office/soffice.py`

---

## Standards de mise en forme PFE

### Police & Taille
| Élément | Police | Taille | Style |
|--------|--------|--------|-------|
| Corps du texte | Times New Roman | 12pt (24 half-pts) | Normal |
| Titre niveau 1 | Times New Roman | 16pt (32 half-pts) | Gras |
| Titre niveau 2 | Times New Roman | 14pt (28 half-pts) | Gras |
| Titre niveau 3 | Times New Roman | 12pt (24 half-pts) | Gras Italique |
| Légende figure/tableau | Times New Roman | 10pt (20 half-pts) | Italique |

### Marges (en DXA, 1440 DXA = 1 pouce = 2.54 cm)
| Côté | Valeur recommandée |
|------|-------------------|
| Haut | 2520 (4.45 cm) |
| Bas | 2520 (4.45 cm) |
| Gauche | 3600 (6.35 cm) |
| Droite | 2520 (4.45 cm) |

### Interligne & Espacement
- Corps : interligne 1.5 (360 twips)
- Avant titre H1 : 480 twips
- Après titre H1 : 240 twips
- Avant titre H2 : 360 twips
- Après titre H2 : 180 twips

---

## Structure complète d'un rapport PFE

```
1. Page de garde
2. Dédicaces (optionnel)
3. Remerciements
4. Résumé (Français + Anglais)
5. Table des matières
6. Liste des figures
7. Liste des tableaux
8. Liste des abréviations
9. Introduction générale
10. Chapitres (I, II, III...)
11. Conclusion générale
12. Bibliographie / Webographie
13. Annexes
```

---

## Code JavaScript — Template complet

```javascript
const {
  Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell,
  Header, Footer, AlignmentType, HeadingLevel, LevelFormat,
  PageNumber, PageBreak, TableOfContents, BorderStyle,
  WidthType, ShadingType, VerticalAlign, NumberFormat
} = require('docx');
const fs = require('fs');

// ── STYLES GLOBAUX ──────────────────────────────────────────────────
const docStyles = {
  default: {
    document: {
      run: { font: "Times New Roman", size: 24 } // 12pt
    }
  },
  paragraphStyles: [
    {
      id: "Heading1",
      name: "Heading 1",
      basedOn: "Normal",
      next: "Normal",
      quickFormat: true,
      run: { size: 32, bold: true, font: "Times New Roman", color: "1F3864" },
      paragraph: {
        spacing: { before: 480, after: 240 },
        outlineLevel: 0,
        pageBreakBefore: true
      }
    },
    {
      id: "Heading2",
      name: "Heading 2",
      basedOn: "Normal",
      next: "Normal",
      quickFormat: true,
      run: { size: 28, bold: true, font: "Times New Roman", color: "2E74B5" },
      paragraph: {
        spacing: { before: 360, after: 180 },
        outlineLevel: 1
      }
    },
    {
      id: "Heading3",
      name: "Heading 3",
      basedOn: "Normal",
      next: "Normal",
      quickFormat: true,
      run: { size: 24, bold: true, italics: true, font: "Times New Roman" },
      paragraph: {
        spacing: { before: 240, after: 120 },
        outlineLevel: 2
      }
    },
    {
      id: "Caption",
      name: "Caption",
      basedOn: "Normal",
      run: { size: 20, italics: true, font: "Times New Roman" },
      paragraph: { alignment: AlignmentType.CENTER, spacing: { before: 60, after: 120 } }
    }
  ]
};

// ── PAGE DE GARDE ────────────────────────────────────────────────────
function createCoverPage(info) {
  // info = { universite, faculte, departement, titre, etudiant, encadrant, annee }
  return [
    new Paragraph({
      alignment: AlignmentType.CENTER,
      spacing: { before: 0, after: 120 },
      children: [new TextRun({ text: info.universite, bold: true, size: 28, font: "Times New Roman" })]
    }),
    new Paragraph({
      alignment: AlignmentType.CENTER,
      spacing: { before: 0, after: 240 },
      children: [new TextRun({ text: info.faculte, size: 24, font: "Times New Roman" })]
    }),
    new Paragraph({
      alignment: AlignmentType.CENTER,
      spacing: { before: 720, after: 120 },
      children: [new TextRun({ text: "Rapport de Projet de Fin d'Études", bold: true, size: 32, font: "Times New Roman", color: "1F3864" })]
    }),
    new Paragraph({
      alignment: AlignmentType.CENTER,
      spacing: { before: 0, after: 720 },
      children: [new TextRun({ text: "Pour l'obtention du diplôme de Master", size: 24, font: "Times New Roman" })]
    }),
    new Paragraph({
      alignment: AlignmentType.CENTER,
      spacing: { before: 480, after: 480 },
      children: [new TextRun({ text: info.titre, bold: true, size: 36, font: "Times New Roman", color: "2E74B5" })]
    }),
    new Paragraph({
      alignment: AlignmentType.CENTER,
      spacing: { before: 480, after: 120 },
      children: [new TextRun({ text: `Réalisé par : ${info.etudiant}`, size: 24, font: "Times New Roman" })]
    }),
    new Paragraph({
      alignment: AlignmentType.CENTER,
      spacing: { before: 0, after: 120 },
      children: [new TextRun({ text: `Encadré par : ${info.encadrant}`, size: 24, font: "Times New Roman" })]
    }),
    new Paragraph({
      alignment: AlignmentType.CENTER,
      spacing: { before: 480, after: 0 },
      children: [new TextRun({ text: `Année universitaire : ${info.annee}`, size: 22, font: "Times New Roman" })]
    }),
    new Paragraph({ children: [new PageBreak()] })
  ];
}

// ── PARAGRAPHE CORPS DE TEXTE ────────────────────────────────────────
function bodyParagraph(text) {
  return new Paragraph({
    children: [new TextRun({ text, font: "Times New Roman", size: 24 })],
    spacing: { line: 360, before: 0, after: 200 }, // Interligne 1.5
    alignment: AlignmentType.JUSTIFIED,
    indent: { firstLine: 720 } // Indentation première ligne : 1.27 cm (720 twips)
  });
}

// ── DOCUMENT PRINCIPAL ───────────────────────────────────────────────
const doc = new Document({
  styles: docStyles,
  sections: [{
    properties: {
      page: {
        size: { width: 11906, height: 16838 }, // A4
        margin: { top: 2520, right: 2520, bottom: 2520, left: 3600 }
      }
    },
    headers: {
      default: new Header({
        children: [
          new Paragraph({
            border: { bottom: { style: BorderStyle.SINGLE, size: 6, color: "2E74B5", space: 1 } },
            alignment: AlignmentType.RIGHT,
            children: [new TextRun({ text: "Rapport PFE — [Titre du projet]", size: 18, italics: true, font: "Times New Roman", color: "666666" })]
          })
        ]
      })
    },
    footers: {
      default: new Footer({
        children: [
          new Paragraph({
            border: { top: { style: BorderStyle.SINGLE, size: 6, color: "2E74B5", space: 1 } },
            alignment: AlignmentType.CENTER,
            children: [
              new TextRun({ text: "Page ", size: 18, font: "Times New Roman" }),
              new TextRun({ children: [PageNumber.CURRENT], size: 18, font: "Times New Roman" }),
              new TextRun({ text: " / ", size: 18, font: "Times New Roman" }),
              new TextRun({ children: [PageNumber.TOTAL_PAGES], size: 18, font: "Times New Roman" })
            ]
          })
        ]
      })
    },
    children: [
      // ── Page de garde ──
      ...createCoverPage({
        universite: "Université [Nom]",
        faculte: "Faculté [Nom] — Département [Nom]",
        titre: "[Titre de votre PFE]",
        etudiant: "[Prénom Nom]",
        encadrant: "Pr. [Prénom Nom]",
        annee: "2024-2025"
      }),

      // ── Table des matières ──
      new Paragraph({ heading: HeadingLevel.HEADING_1, children: [new TextRun("Table des matières")] }),
      new TableOfContents("Table des matières", {
        hyperlink: true,
        headingStyleRange: "1-3"
      }),
      new Paragraph({ children: [new PageBreak()] }),

      // ── Introduction générale ──
      new Paragraph({ heading: HeadingLevel.HEADING_1, children: [new TextRun("Introduction générale")] }),
      bodyParagraph("Rédigez ici votre introduction générale..."),

      // ── Chapitre I ──
      new Paragraph({ heading: HeadingLevel.HEADING_1, children: [new TextRun("Chapitre I : [Titre du chapitre]")] }),
      new Paragraph({ heading: HeadingLevel.HEADING_2, children: [new TextRun("1.1 [Titre de la section]")] }),
      bodyParagraph("Contenu de la section..."),

      // ── Conclusion générale ──
      new Paragraph({ heading: HeadingLevel.HEADING_1, children: [new TextRun("Conclusion générale")] }),
      bodyParagraph("Rédigez ici votre conclusion générale..."),

      // ── Bibliographie ──
      new Paragraph({ heading: HeadingLevel.HEADING_1, children: [new TextRun("Bibliographie")] }),
      bodyParagraph("[1] Auteur, Titre, Éditeur, Année."),
    ]
  }]
});

// ── EXPORT ──────────────────────────────────────────────────────────
Packer.toBuffer(doc).then(buffer => {
  fs.writeFileSync("rapport_pfe_formate.docx", buffer);
  console.log("✅ rapport_pfe_formate.docx généré avec succès !");
});
```

---

## Utilisation

```bash
# 1. Installer la dépendance
npm install -g docx

# 2. Adapter les informations dans le code (université, titre, étudiant...)

# 3. Exécuter
node pfe_formatter.js

# 4. Valider
python scripts/office/validate.py rapport_pfe_formate.docx

# 5. (Optionnel) Convertir en PDF
python scripts/office/soffice.py --headless --convert-to pdf rapport_pfe_formate.docx
```

---

## Points critiques
- Toujours utiliser `WidthType.DXA` pour les tableaux, jamais PERCENTAGE
- Ne jamais utiliser `\n` dans les TextRun — créer des Paragraph séparés
- La Table des matières nécessite `outlineLevel` dans les styles de titres
- Utiliser `ShadingType.CLEAR` pour les cellules colorées
- La page de garde ne doit pas avoir d'en-tête/pied de page → gérer via section séparée si nécessaire
- **Indentation de première ligne** : utiliser `indent: { firstLine: 720 }` (720 twips = 1.27 cm) sur chaque paragraphe de corps de texte — NE PAS appliquer aux titres, légendes, page de garde ni au premier paragraphe après un titre
