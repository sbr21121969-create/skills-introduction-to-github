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
| **Exact Online** | Facturatie en boekhouding | Verkoopfacturen, inkoopfacturen, debiteuren, boekhouding per BV |
| **Nmbrs** | Salaris | Loonstroken, loonheffing, verlof en salaris van zorgverleners in loondienst |

Exact en Nmbrs blijven. Een factuur of loonstrook mag niet uit Airtable of Pipedrive komen:
daarvoor gelden btw-, loonheffings- en bewaarregels die alleen een boekhoud- en salarispakket goed regelt.
Wel komen de gegevens (gewerkte dagen, tarieven, personeelsnummer) automatisch uit Airtable,
zodat er niets dubbel wordt ingevoerd.

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

En tegelijk voor de zorgverleners:

```
Einde maand ──► Airtable: gewerkte dagen per zorgverlener (per Personeelsnummer)
      │
      ▼
Nmbrs ──► variabele dagen/uren worden ingelezen, jij controleert, salaris wordt gedraaid
      │
      ▼
Exact Online ──► Nmbrs boekt de loonjournaalpost automatisch in de juiste BV
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

## 5. Facturatie en salaris

**Exact Online**
- Eén administratie per BV: GCC, Smiling Faces en SFPS (België, Belgische btw-regels)
- Verkoopfacturen worden aangemaakt vanuit Airtable (maandtelling per plaatsing)
- Inkoopfacturen (o.a. van agents) blijven via de bestaande e-mailroute naar Exact gaan
- Betaalstatus gaat terug naar Pipedrive, zodat je ziet wie nog moet betalen

**Nmbrs**
- Het veld "Personeelsnummer" in Airtable (Zorgverleners) moet gelijk zijn aan het
  werknemersnummer in Nmbrs. Dat is de sleutel van de koppeling.
- Maandelijks gaan de gewerkte dagen/uren uit "Plaatsingen" naar Nmbrs
  (eerst als importbestand, later via de Nmbrs-API).
- Nmbrs heeft een standaardkoppeling met Exact Online voor de loonjournaalpost; die zetten we aan
  per BV.
- Nieuwe zorgverlener in dienst (arbeidsvoorwaarden getekend in PandaDoc) → gegevens klaarzetten
  voor Nmbrs, zodat je ze niet overtypt.
- Zorgverleners via een agent of als zzp zitten niet in Nmbrs; die lopen via inkoopfacturen in Exact.

## 6. Hoe de koppelingen werken

| Van → naar | Wanneer | Hoe |
|---|---|---|
| Pipedrive → PandaDoc | Offerte maken vanuit een deal | Officiële PandaDoc-app in Pipedrive |
| PandaDoc → Pipedrive | Document getekend | PandaDoc-app: deal naar "Gewonnen", PDF bij de deal |
| Pipedrive → Airtable | Deal gewonnen | Zapier of Make (of Airtable-automatisering met webhook) |
| Airtable → Exact | Einde maand, na jouw akkoord | Zapier/Make of een klein script |
| Exact → Pipedrive | Factuur betaald / te laat | Zapier/Make |
| Airtable → Nmbrs | Einde maand, na jouw akkoord | Importbestand (start), later Nmbrs-API |
| Nmbrs → Exact | Na elke salarisrun | Standaardkoppeling Nmbrs–Exact Online |
| PandaDoc → Nmbrs | Arbeidsvoorwaarden getekend | Gegevens klaarzetten voor nieuwe werknemer |

## 7. Stappenplan

| Fase | Wat | Wie |
|---|---|---|
| **1. Opruimen** (week 1) | Dubbele velden weg, één klantnummer leidend, veld "Contracterende BV" toevoegen | Claude, met jouw akkoord |
| **2. Pipedrive ↔ PandaDoc** (week 1–2) | Templates koppelen aan deal-velden, ondertekening zet deal op gewonnen | Jij installeert de app, Claude zet velden klaar |
| **3. Pipedrive → Airtable** (week 2–3) | Gewonnen deal maakt automatisch klant aan in Planning en ECD | Claude bouwt de automatisering |
| **4. Facturatie** (week 3–5) | Maandtelling per plaatsing → conceptfactuur per BV in Exact | Samen met boekhouder |
| **5. Salaris** (week 4–6) | Personeelsnummers gelijk trekken met Nmbrs, maandexport gewerkte dagen, Nmbrs–Exact-koppeling aan | Samen met salarisadministrateur |
| **6. Oude software en Excel-lijsten uitzetten** (week 7) | Pas als een volle maand foutloos is gefactureerd én verloond | Jij |

## 8. Belangrijk: privacy en zorgregels

Het ECD bevat medische gegevens. Daarvoor gelden de AVG en de NEN 7510-eisen voor zorgdossiers.
Airtable bewaart gegevens standaard in de VS. Controleer daarom:
- of er een verwerkersovereenkomst (DPA) met Airtable is afgesloten;
- of EU-dataopslag mogelijk is in je abonnement;
- dat medische gegevens **niet** naar Pipedrive, PandaDoc of Exact worden gekopieerd.
  Daar staan alleen naam, contact, contract en bedragen.

## 9. Open vragen

Beantwoord: Exact Online (facturatie/boekhouding) en Nmbrs (salaris) blijven.

1. Factureert Zuster in Huis België (SFPS) op dezelfde manier (per dag/maand) als Nederland?
   En loopt het Belgische salaris ook via Nmbrs, of via een Belgisch sociaal secretariaat?
2. Worden zorgverleners per dag of per uur verloond in Nmbrs?
3. Heb je Zapier of Make al, of mag dat erbij komen (ca. € 20–50 per maand)?
4. Zijn er nog andere pakketten of Excel-lijsten die weg moeten?
