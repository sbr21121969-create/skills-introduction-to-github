# Systeemplan Zuster in Huis: één systeem met vier onderdelen

*Opgesteld 10-11-2026. Gebaseerd op wat nu in Pipedrive, PandaDoc en Airtable staat.*

Geldt voor:
- **Zuster in Huis Nederland**: Global Care Capacity BV (GCC) en Smiling Faces BV
- **Zuster in Huis België**: Smiling Faces Private Services BV (SFPS)

---

## 1. Het idee in één zin

Elk onderdeel doet één ding, en elk gegeven wordt maar op één plek ingevoerd:

| Onderdeel | Taak | Is de bron voor |
|---|---|---|
| **Pipedrive** | Verkoop en werving | Aanvragen, klantcontact, contactpersonen, kandidaat-zorgverleners |
| **PandaDoc** | Documenten en handtekeningen | Offertes, zorgvoorstellen, overeenkomsten, arbeidsvoorwaarden |
| **Airtable** | Uitvoering van de zorg | Plaatsingen, planning, matching, cliëntendossier (ECD) |
| **Facturatie** (voorstel: Exact Online) | Geld | Verkoopfacturen, inkoopfacturen, debiteuren, boekhouding per BV |

## 2. De klantreis van begin tot eind

```
Nieuwe aanvraag ──► Pipedrive (deal in "Sales ZIHNL")
      │
      ▼
Intake gepland / gehad ──► PandaDoc: "Persoonlijk zorgvoorstel" + "Offerte en overeenkomst"
      │                    (gegevens komen automatisch uit de Pipedrive-deal)
      ▼
Klant tekent in PandaDoc ──► deal automatisch op "Gewonnen"
      │
      ▼
Gewonnen deal ──► Airtable: nieuw record in "Zorgklanten" (Planning ZIH-NL)
                  en in "Cliënten" (ECD), met link terug naar Pipedrive
      │
      ▼
Matching en plaatsing ──► Airtable: "Plaatsingen" (zorgverlener + data)
      │
      ▼
Einde maand ──► Airtable telt gewerkte dagen, extra dagen en gaten in de zorg
      │
      ▼
Facturatie ──► conceptfactuur per klant, in de juiste BV (GCC, SF of SFPS)
      │        jij keurt goed, daarna wordt de factuur verstuurd
      ▼
Betaling ──► status terug in Pipedrive/Airtable (betaald / herinnering)
```

Voor zorgverleners loopt het op dezelfde manier: werving in Pipedrive ("Zorgverleners ZIH-NL"),
arbeidsvoorwaarden tekenen in PandaDoc, daarna inzet in Airtable ("Zorgverleners").

## 3. Wat er al staat (en goed is)

**Pipedrive**: vier pijplijnen (Sales ZIHNL, Zorgverleners ZIH-NL, Het Zorgkabinet, Later ZIH)
en veel eigen velden (112 bij deals, 59 bij personen).

**PandaDoc**: de belangrijkste templates bestaan al:
- Offerte en overeenkomst ZiH (oktober 2026)
- Persoonlijk zorgvoorstel ZiH (september 2026)
- Overeenkomst levering zorg: uurtarief, vast tarief en privé maandtarief
- Offerte tariefwijziging, NulOfferte, Informatiepakket
- Aanvullende arbeidsvoorwaarden en gedragsregels

**Airtable**:
- *Planning ZIH-NL*: Zorgklanten, Zorgverleners, Plaatsingen, Zorgvraag (ADL), met matchingcriteria
- *ECD – Elektronisch Cliëntendossier GCC*: volledig dossier volgens het Normenkader zorg thuis 2026

## 4. Wat er nog ontbreekt

1. **Koppelingen.** Nu wordt veel dubbel ingevoerd. Bijvoorbeeld: de Pipedrive-link staat als
   losse URL in Airtable, en klantgegevens staan zowel in Pipedrive als in twee Airtable-bases.
2. **Facturatie uit de planning.** In "Plaatsingen" staan al "Aantal dagen plaatsing",
   "Extra gewerkte dagen", "Totaal dagen geen zorg" en "Aantekeningen mbt Facturatie",
   maar daar komt nog geen factuur uit.
3. **Welke BV factureert?** Elke klant moet een vast veld "Contracterende BV" krijgen
   (GCC / Smiling Faces / SFPS), zodat de factuur in de juiste administratie komt.
4. **Opruimen.** In Airtable staan velden die weg mogen ("ZZ dubbel 1 t/m 5",
   "ZZ – foutief veld") en de tabel "Klantenoverzicht (excel)" heeft kolommen met
   namen als telefoonnummers en datums. Die tabel kan na controle worden gearchiveerd.

## 5. Facturatie: voorstel

Pipedrive, PandaDoc en Airtable maken geen echte facturen met btw en boekhouding.
Daarvoor is een apart pakket nodig.

**Voorstel: Exact Online** (je gebruikt het al voor inkoopfacturen):
- Eén administratie per BV: GCC, Smiling Faces en SFPS (België, Belgische btw-regels)
- Verkoopfacturen worden aangemaakt vanuit Airtable (maandtelling per plaatsing)
- Inkoopfacturen blijven via de bestaande e-mailroute naar Exact gaan
- Betaalstatus gaat terug naar Pipedrive, zodat je ziet wie nog moet betalen

Alternatieven als je van Exact af wilt: Moneybird of e-Boekhouden (eenvoudiger, goedkoper,
maar minder sterk voor een Belgische BV erbij).

## 6. Hoe de koppelingen werken

| Van → naar | Wanneer | Hoe |
|---|---|---|
| Pipedrive → PandaDoc | Offerte maken vanuit een deal | Officiële PandaDoc-app in Pipedrive |
| PandaDoc → Pipedrive | Document getekend | PandaDoc-app: deal naar "Gewonnen", PDF bij de deal |
| Pipedrive → Airtable | Deal gewonnen | Zapier of Make (of Airtable-automatisering met webhook) |
| Airtable → Exact | Einde maand, na jouw akkoord | Zapier/Make of een klein script |
| Exact → Pipedrive | Factuur betaald / te laat | Zapier/Make |

## 7. Stappenplan

| Fase | Wat | Wie |
|---|---|---|
| **1. Opruimen** (week 1) | Dubbele velden weg, één klantnummer leidend, veld "Contracterende BV" toevoegen | Claude, met jouw akkoord |
| **2. Pipedrive ↔ PandaDoc** (week 1–2) | Templates koppelen aan deal-velden, ondertekening zet deal op gewonnen | Jij installeert de app, Claude zet velden klaar |
| **3. Pipedrive → Airtable** (week 2–3) | Gewonnen deal maakt automatisch klant aan in Planning en ECD | Claude bouwt de automatisering |
| **4. Facturatie** (week 3–5) | Maandtelling per plaatsing → conceptfactuur per BV in Exact | Samen met boekhouder |
| **5. Oude software uitzetten** (week 6) | Pas opzeggen als een volle maand foutloos is gefactureerd | Jij |

## 8. Belangrijk: privacy en zorgregels

Het ECD bevat medische gegevens. Daarvoor gelden de AVG en de NEN 7510-eisen voor zorgdossiers.
Airtable bewaart gegevens standaard in de VS. Controleer daarom:
- of er een verwerkersovereenkomst (DPA) met Airtable is afgesloten;
- of EU-dataopslag mogelijk is in je abonnement;
- dat medische gegevens **niet** naar Pipedrive, PandaDoc of Exact worden gekopieerd.
  Daar staan alleen naam, contact, contract en bedragen.

## 9. Open vragen

1. Welke software wil je precies opzeggen? (bijv. een ander CRM, planningspakket, ECD-pakket,
   facturatieprogramma, Excel-lijsten, SharePoint?)
2. Blijft Exact Online je boekhoudpakket, of wil je ook daarvan af?
3. Factureert Zuster in Huis België (SFPS) op dezelfde manier (per dag/maand) als Nederland?
4. Heb je Zapier of Make al, of mag dat erbij komen (ca. € 20–50 per maand)?
