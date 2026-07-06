---
document: book-04-evolution/01-evolution-engine.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: Chief AI Officer)
technical_owner: Claude Code (rol: Architecture Guardian)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: tweewekelijks
laatste_review: 2026-07-03
---

# Evolution Engine

Hoe Ziraat zichzelf structureel verbetert in plaats van incidenteel te repareren.

## De verbeterlus

```
Signaal → Memory (feedback/…) → Voorstel → Decision Record → Implementatie → Change-log → Review op effect
```

**Signalen** zijn: gebruikersfeedback, ontdekte fouten (bijv. Methode A-defect), pipeline-incidenten ("0 pdfs"-les), tokenlekken, en terugkerende data-gaten in IC-runs.

## Voorstelformat (verplicht, Meta §5)

Elk verbeteringsvoorstel bevat: huidige situatie, gewenste situatie, verwachte winst, verwachte risico's, tokenimpact, technische impact, businessimpact, implementatiecomplexiteit, rollback-plan. Zonder deze negen velden wordt een voorstel niet in behandeling genomen.

## Cadans

- **Tweewekelijks:** evolutieronde — nieuwe feedback-memories doornemen, kandidaat-verbeteringen opstellen, prompt-evolutie-items afhandelen.
- **Maandelijks:** samenvallen met de agent- en tokenreview (Book III); structurele bevindingen promoveren naar voorstellen.
- **Continu:** elke gebruikerscorrectie wordt dezelfde sessie als feedback-memory vastgelegd — dat is de brandstof van deze engine.

## Reeds door de lus gegane verbeteringen (precedenten)

1. Methode A-verbod na target1<trigger-fout → DR-003.
2. Pipeline-les: "0 pdfs" kan gefaalde download zijn; hash-check op evergreen links → knowledge-architecture kennisvallen.
3. Draft-onbetrouwbaarheid Master-Stratejist → Constitution (investeringsprincipes: draft ≠ besluit) + review-checklist A.6.

## Grenzen

De engine verbetert het systeem, niet de beleggingsthese: rendementsdoelen en risicoprincipes (Constitution) zijn geen evolutie-onderwerp zonder expliciete gebruikersbeslissing.
