---
name: company-research
description: >-
  Bruk når du skal finne, følge med på eller analysere informasjon om
  børsnoterte selskaper eller fond (børsmeldinger, kvartals- og årsrapporter,
  nøkkeltall, ratinger, utbytte, generalforsamlinger), f.eks. for en
  porteføljegjennomgang eller en løpende overvåkingsrutine.
---
# Selskapsanalyse – kilder og framgangsmåte

Generisk oppskrift for å hente inn og analysere selskaps- og fondsinformasjon fra åpne, etterprøvbare kilder. Hvilke selskaper/fond som sjekkes, hører hjemme i rutinen eller oppgaven som bruker skillen – ikke her.

## Grunnregler
- Bruk primærkilder først (selskapets egen melding/rapport, børsens meldingssystem, tilsynsregister). Mediesaker og aggregatorer brukes bare som supplement og merkes som det.
- Aldri finn på tall, datoer, ratinger eller sitater. Finner du ikke noe: skriv «ikke funnet» og hvilken kilde som ble prøvd.
- Oppgi kilde (lenke) for hvert vesentlig tall, og datoen tallet gjelder for («per 31.10.»).
- Skill mellom rapportert og justert/underliggende resultat, og mellom selskapets egne forventninger og analytikerkonsensus (konsensus varierer mellom kilder – si det).
- Informasjonsformål, ikke investeringsråd.

## 1. Identifiser instrumentet
- Fastslå navn, ticker, børs/handelsplass, ISIN og evt. ADR/dobbeltnotering. Notér rapporteringsvaluta.
- For fond: fondsnavn, andelsklasse, ISIN, forvalter, Morningstar-kategori.

## 2. Kilder
### Børsmeldinger og offisielle innleveringer
- Oslo Børs / Euronext Oslo: Newsweb (newsweb.oslobors.no) – søk på utsteder; filtrer på kategori (finansiell rapportering, utbytte, innsidehandel, generalforsamling). Euronext Live for kurs og finanskalender.
- Andre nordiske børser: Nasdaq Nordic (company news), Spotlight m.fl.
- USA: SEC EDGAR (sec.gov/edgar) – 10-K (år), 10-Q (kvartal), 8-K (vesentlige hendelser), 6-K/20-F (utenlandske utstedere, ADR), DEF 14A (generalforsamling), Form 4 (innsidehandel), 13D/13G (store eierposter). EDGAR full-text search og JSON-API (data.sec.gov/submissions/CIK##########.json) krever en User-Agent-header.
- Øvrige: nasjonale OAM-registre, LSE RNS, Deutsche Börse osv. etter børs.

### Selskapets egne kilder
- Investor Relations-siden: kvartals- og årsrapporter (PDF), presentasjoner, webcast, finanskalender, utbyttehistorikk, generalforsamlingsdokumenter.
- Pressemeldinger via GlobeNewswire, Cision, Business Wire, PR Newswire, Modular Finance.

### Regnskap og selskapsdata (Norge)
- Brønnøysundregistrene / Enhetsregisteret (data.brreg.no API) for org.nr., roller og vedtekter; Regnskapsregisteret for årsregnskap for ikke-noterte selskaper.
- Proff.no, Purehelp o.l. som sekundærkilde for nøkkeltall.

### Fond og ratinger
- Morningstar (stjerner oppdateres månedlig og krever 36 mnd. historikk; Medalist Rating; Sustainability Rating/globuser). Kryss-sjekk mot Nordnet, Kron, FT Markets eller forvalterens faktaark når Morningstar ikke er tilgjengelig.
- Forvalterens egne sider: faktaark, månedsrapport, kvartalsvis/halvårlig fullstendig beholdningsliste, prospekt/KID, SFDR-klassifisering (artikkel 6/8/9 – ikke det samme som Morningstars bærekraftsrating).

### Marked og nyheter (supplement)
- E24, DN, Finansavisen, Reuters, Bloomberg, Seeking Alpha (konsensus og beat/miss), Investtech/Infront for kurs.

## 3. Framgangsmåte – løpende overvåking
1. Les forrige sjekkpunkt (tidsstempel) fra lagret state, så du bare vurderer nye meldinger.
2. For hvert instrument: hent nye meldinger fra børsens meldingssystem/EDGAR siden sjekkpunktet, deretter IR-side/pressemeldinger.
3. Klassifiser hver melding:
   - Vesentlig: kvartals-/årsresultat, resultatvarsel/guiding, utbytte (beløp, ex-dato, betalingsdato), oppkjøp/salg, emisjon eller nytt tilbakekjøpsprogram, store eierskifter, ledelses-/styreendringer av betydning, ratingendringer, søksmål/regulatoriske hendelser, innkalling med uvanlige forslag.
   - Rutine: små innsidehandler, ukentlig status på tilbakekjøp, vanlige obligasjonsutstedelser, rutinemessige skjemaer.
4. Ved feil eller utilgjengelig kilde: logg det, ikke flytt sjekkpunktet forbi perioden som ikke ble dekket, og si fra om at dekningen ikke er uttømmende.
5. Oppdater sjekkpunktet først når kjøringen er fullført.
6. Rapporter bare når noe vesentlig har skjedd: kort, med lenke per punkt, og nevn kommende datoer (rapporter, ex-dato, generalforsamling).

## 4. Framgangsmåte – analyse av et selskap
1. Hent siste årsrapport og de siste 2–4 kvartalsrapportene.
2. Nøkkeltall (med periode og valuta): omsetning, EBITDA/EBIT og margin, resultat etter skatt, EPS, kontantstrøm fra drift, fri kontantstrøm, netto rentebærende gjeld, egenkapitalandel. For banker: rentenetto, kostnadsgrad, tap, ROE, CET1. For forsikring: combined ratio.
3. Utvikling: endring mot samme periode i fjor og mot forrige kvartal; organisk vekst hvis oppgitt.
4. Verdsettelse (oppgi kurs og dato): P/E, EV/EBITDA, P/B, direkteavkastning.
5. Utbytte- og kapitalpolitikk, tilbakekjøp, gjeldsforfall.
6. Selskapets guiding og vesentlige risikoer (fra rapportens risikoavsnitt).
7. Kommende hendelser fra finanskalenderen.

## 5. Framgangsmåte – fond og gjennomlysning (look-through)
1. Hent faktaark/månedsrapport: topp-10, sektor- og landfordeling, løpende kostnader, referanseindeks.
2. Indirekte eksponering: beholdningens andel av fondet × verdien av fondsandelene = anslått beløp. Oppgi dato for beholdningslisten og hvor stor del av fondet som er dekket (f.eks. topp-10 = x %).
3. Slå sammen på tvers av fond og direkte aksjer for å finne overlapp og konsentrasjon.
4. Notér rating (stjerner, Medalist, bærekraft) med as-of-dato; sammenlign mot forrige registrering og flagg endringer.

## 6. Leveranse
- Det viktigste først i én–to setninger, deretter punkter med tall og lenke.
- Rund av fornuftig, og ta alltid med valuta og periode.
- Lengre analyser med tabeller egner seg som side/rapport; løpende varsler holdes korte.
