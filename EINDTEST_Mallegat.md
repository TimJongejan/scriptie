# Eindtest — reproductie Mallegat-vergelijking (v19)

Doel: aantonen dat de rekentool de Mallegat-vergelijking consistent en navolgbaar
reproduceert. De tool rekent **per m² verdiepingsvloer**, fasen **A1–A5**, op
**categorie 3** (generieke NMD-kaarten), inclusief de ontbrekende bouwplaatsfactoren
en faalkosten. De reden dat de absolute getallen afwijken van de GPR-uitdraai staat
onderaan.

## Invoer (gelijke uitgangspunten)

| | Systeem A | Systeem B |
|---|---|---|
| Type | In-situ tunnelgietbouw | Prefab breedplaat (schil + druklaag) |
| Maatvoering | vloerdikte 280 mm, warme gietbouw | schil 70 mm + druklaag 190 mm |
| Betonklasse | C30/37 | schil C45/55 · druklaag C30/37 (CEM II/A) |
| Belasting (kaartschaal) | 2,50 kN/m² | n.v.t. (schaalt op dikte) |
| Faalkosten | 8 % | 8 % |

## Uitkomst (engine v19, kg CO₂/m² vloer)

| Systeem | A1–A3 | A4 | A5 | **Totaal** | cat.3-kaart | ontbrekend | faalkosten |
|---|--:|--:|--:|--:|--:|--:|--:|
| A — tunnelgietbouw | 47,80 | 23,12 | 10,46 | **81,38** | 120,48 | −45,13 | 6,03 |
| B — breedplaat | 151,13 | 20,02 | 9,55 | **180,70** | 164,18 | 3,13 | 13,39 |

**Richting gelijk aan Mallegat:** systeem A (tunnel) scoort lager dan systeem B
(breedplaat) — net als de GPR-uitdraai (A = 61, B = 92 kg CO₂/m² BVO).

## Navolgbaarheid (steekproef, reproduceert de basisgegevens)

- Beton C30/37 CEM I = **297,82** kg CO₂/m³ (§5.1.1); CEM III/B = **97,05** (§6.7).
- Warme-gietbouw cementcorrectie = (97,05 − 297,82) × 0,28 m = **−56,2** kg CO₂/m² bij 280 mm
  (bij 250 mm: −50,2, conform §6.7); zichtbaar als de negatieve post in "ontbrekend".
- cat.3 tunnel = in-situ-kaart bij 2,50 kN/m² (107,57) × 280/250 = **120,48** kg CO₂/m².
- Materieel/personeel reproduceren §4.8 exact (bv. breedplaat 21 mandagen → 0,655;
  kraan 80T 7 u → 0,686 inzet / 1,467 transport).
- In de tool zelf staat dit per systeem onder **Resultaat → Verschaling & afleiding**
  (schaalpunten, interpolatie, driver → projecttotaal → ÷ referentie → per m²) en onder
  **Navolgbaarheid** (per post de berekening + bron).

## Waarom de absolute getallen afwijken van de GPR-score (61 / 92)

| | Mallegat (GPR) | Deze rekentool |
|---|---|---|
| Eenheid | per m² **BVO** (incl. wanden, kern, dak) | per m² **vloer** |
| Datacategorie | gemengd cat. 1/2 (productkaarten) + cat. 3 wapening | cat. 3 (generiek), homogeen |
| Scope | A1–A5 **materiaalgebonden**, geen bouwplaats | A1–A5 **incl.** bekisting, materieel, uitvoering, faalkosten |

De rekentool levert daarmee precies wat het referentieonderzoek als tekortkoming
benoemt: een **eerlijke, complete en navolgbare** vergelijking op gelijke
uitgangspunten, in plaats van een onvolledige materiaalgebonden GPR-score.

> Reproduceerbaar in de tool: maak een nieuwe vergelijking, kies tunnelgietbouw en
> breedplaat, en vul bovenstaande maatvoering in (modus "Exact").
