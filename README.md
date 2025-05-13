# IS-218-oppgave2-gruppe10

- [Problemstilling](#problemstilling)
- [Målsetning](#målsetning)
- [Teknologivalg](#teknologivalg)
- [Datasettene](#datasettene)
- [Metode og implementering](#metode_og_implementering)
- [Mulig videre arbeid og utvidelser](#Mulig_videre_arbeid_og_utvidelser)
- [Kildekode og brukerveiledning](#Kildekode_og_brukerveiledning)
- [Konklusjon](#konklusjon)
- [Kilder](#kilder)



# 📌 Problemstilling
I en krisesituasjon er tilgang til trygge tilfluktsrom avgjørende for befolkningens sikkerhet. I Agder fylke bor det 319 644 personer[Lenke til kilde](https://kartkatalog.geonorge.no/metadata/befolkning-paa-grunnkretsniv/7eb907de-fdaa-4442-a8eb-e4bd06da9ca8?search=befolkning) , men kapasiteten i offentlige tilfluktsrom er kun 16 773 plasser [Lenke til kilde](https://kartkatalog.geonorge.no/metadata/tilfluktsrom-offentlige/dbae9aae-10e7-4b75-8d67-7f0e8828f3d8?search=tilfluktsrom) . Dette betyr at det i gjennomsnitt er 1 plass per 19 innbyggere, noe som indikerer en alvorlig mangel på tilgjengelige tilfluktsrom.

Denne applikasjonen undersøker følgende spørsmål:

Er det nok tilfluktsrom i Agder til å dekke behovet i en krisesituasjon?
Hvilke områder har størst kapasitetsutfordringer?
Kan alternativer, som enkle "basic huts" fra OpenStreetMap (OSM), bidra til å gi inbyggere tilfluktssteder?

# 🎯 Målsetning
Prosjektets formål er å utvikle en nettbasert applikasjon som:
✅ Lar brukeren finne nærmeste tilfluktsrom basert på sin posisjon.
✅ Visualiserer overbelastning av tilfluktsrom ved å sammenligne befolkningstall med kapasitet.
✅ Utforsker alternative tilfluktsmuligheter, som for eksempel turistforeningens hytter (basic_hut fra OSM).

# 🗺️ Teknologivalg

Prosjektet er bygget med følgende teknologier:
- **Express.js**: Brukt som back-end rammeverk for å håndtere server-side logikk og API-forespørsler
- **Leaflet.js**: Åpen kildekode JavaScript bibliotek for interaktive kart
- **Supabase**: Database og API-tjenester for å lagre og hente geografiske data
- **PostgreSQL med PostGIS**: Kraftig database med geografisk funksjonalitet
- **Proj4js**: Bibliotek for geografiske koordinattransformasjoner
- **Leaflet Draw**: Tilleggspakke for Leaflet som muliggjør tegning av figurer på kartet

Prosjektet bruker moderne GIS-teknologier for å visualisere og analysere romlige data. Leaflet gir oss et lettvindt kart-grensesnitt, mens PostGIS i Supabase gir oss kraftige romlige analysemuligheter. Proj4js muliggjør konvertering mellom ulike koordinatsystemer, noe som er særlig viktig for norske kartdata som ofte bruker UTM Sone 32N (EPSG:25832).

# 📊 Datasettene
Prosjektet benytter tre primære datasett:

Befolkningsdata: Antall innbyggere i Agder.[Lenke til kilde -geonorge.no](https://kartkatalog.geonorge.no/metadata/befolkning-paa-grunnkretsniv/7eb907de-fdaa-4442-a8eb-e4bd06da9ca8?search=befolkning) 
Tilfluktsrom: Offisielle tilfluktsrom med informasjon om kapasitet.[Lenke til kilde - geonorge.no](https://kartkatalog.geonorge.no/metadata/tilfluktsrom-offentlige/dbae9aae-10e7-4b75-8d67-7f0e8828f3d8?search=tilfluktsrom) 
Basic_hut-shelters: Filtrert datasett som viser enkle hytter i mindre sentrale strøk i Agder [Lenket til kilde - OpenStreetMap.org](https://www.openstreetmap.org).

# 🔍 Metode og implementering

Prosjektet følger en klient-server arkitektur med Express.js på serversiden og Leaflet.js på klientsiden.

1️⃣ **Datainnsamling og lagring**
- Geodata for tilfluktsrom og befolkning er hentet fra offentlige API-er (Geonorge)
- Data er lagret i Supabase med PostGIS-utvidelser for effektiv geografisk spørringshåndtering
- Koordinater er normalisert til samme koordinatsystem (WGS84) for korrekt visning på kart

2️⃣ **Kartvisualisering**
- Kartgrunnlag fra OpenStreetMap er brukt som bakgrunnskart
- Tilfluktsrom vises med egne ikoner og popups med detaljert informasjon
- Befolkningsdata vises som fargede polygoner der farge indikerer befolkningstetthet
- Brukerens posisjon kan spores og vises via geolocation API

3️⃣ **Interaktive analyseverktøy**
- Tegne- og analyseverktøy er implementert ved hjelp av Leaflet Draw
- Brukere kan tegne sirkler, rektangler eller polygoner på kartet
- Systemet beregner automatisk total befolkning og tilfluktsromskapasitet innenfor det markerte området
- Dekningsgrad beregnes som prosentandel av befolkning som kan få plass i tilfluktsrom

4️⃣ **Serverside prosessering**
- Express.js håndterer API-forespørsler til Supabase
- Data transformeres til klientvennlig format før sending til frontend
- Systemet optimaliserer datamengden som sendes til klienten for å sikre god ytelse

# 📢 Mulig videre arbeid og utvidelser

Prosjektet har flere muligheter for utvidelse og forbedring:

✅ **Utvidede datakilder**
- Inkludere private tilfluktsrom i analysen
- Legge til flere attributter for tilfluktsrom, som tilstand, tilgjengelighet, og fasilitetsoversikt
- Inkorporere høydedata for å analysere terrengets innvirkning på tilgjengelighet

✅ **Avansert analyse**
- Implementere "isochrone" analyse for å vise områder som er innen 5, 10, og 15 minutters gange fra tilfluktsrom
- Analyse av befolkningsbevegelser på ulike tider av døgnet (dag vs. natt)
- Simuleringsmodeller for evakueringsscenarier med ulike tidsrammer

✅ **Tekniske forbedringer**
- Implementere caching-strategier for bedre ytelse ved håndtering av store datasett
- Optimaliser mobilvisning og støtte for ulike enheter
- Legge til offline-funksjonalitet for krisesituasjoner med ustabil internettilkobling

✅ **Brukergrensesnitt og funksjonalitet**
- Utbedre rapporteringsfunksjonalitet med eksport til PDF eller Excel
- Implementere brukerveiledninger og hjelp integrert i applikasjonen
- Støtte for flere språk, spesielt viktig for kriseinformasjon

# 📂 Kildekode og brukerveiledning

🔗 **GitHub Repository**: [https://github.com/Ivark1/IS-218-oppgave2-gruppe10](https://github.com/Ivark1/IS-218-oppgave2-gruppe10)

## Hvordan kjøre prosjektet:

1. Klone repoet: `git clone https://github.com/Ivark1/IS-218-oppgave2-gruppe10.git`
2. Naviger til prosjektmappen: `cd IS-218-oppgave2-gruppe10`
3. Installer avhengigheter: `npm install`
4. Legg til Supabase URL og KEY til .env filen.
5. Start serveren: `npm start`
6. Åpne nettleseren på: `http://localhost:3002`

## Avhengigheter:
- Node.js (v14 eller nyere)
- NPM eller Yarn pakkebehandler
- Moderne nettleser med JavaScript aktivert
- Supabase-konto (for database-tilgang)

## Bruk av applikasjonen:
1. **Navigere kartet**: Bruk zoom og pan-kontroller for å utforske kartet
2. **Finn posisjon**: Trykk på "Finn min posisjon" for å bruke din nåværende lokasjon
3. **Vis/skjul lag**: Bruk avkrysningsboksene øverst for å vise eller skjule ulike datalag
4. **Analyser område**: Bruk tegneverkøyet til å markere et område for analyse
5. **Se resultater**: Analyseresultater vises automatisk under kartet
6. **Fjern analyse**: Trykk på "Fjern analyse" for å starte på nytt


# 📜 Konklusjon

https://private-user-images.githubusercontent.com/142518867/418985078-06bd7032-e6eb-424a-8afc-09c1c6b8860b.gif?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDcxNDczODgsIm5iZiI6MTc0NzE0NzA4OCwicGF0aCI6Ii8xNDI1MTg4NjcvNDE4OTg1MDc4LTA2YmQ3MDMyLWU2ZWItNDI0YS04YWZjLTA5YzFjNmI4ODYwYi5naWY_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTEzJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUxM1QxNDM4MDhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05YjdiNzc2YWZkZGQ5YTY5M2IzOTJlNDFiMGVlZjJlNDBiMzM5MjkwMmM0YWQxN2FkMGI3MjA1M2JlMzQ0NTBlJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Sw6Lt3Gtyiwfzr6lTVqoNdJyoKQlo2Ihpo3ZdGL1BsQ

Denne applikasjonen demonstrerer hvordan geografisk IT-utvikling kan brukes til å analysere og forbedre samfunnsberedskap. Ved å kombinere befolkningsdata, tilfluktsromsinformasjon og alternative tilfluktsmuligheter, avdekkes kritiske mangler i nødberedskap som kan ha stor betydning for sikkerhet i krisesituasjoner.

Gjennom prosjektet har vi oppnådd følgende:

1. **Kartlagt dekningsgraden** for tilfluktsrom i forhold til befolkning i Agder
2. **Identifisert geografiske områder** med kapasitetsutfordringer
3. **Utviklet verktøy** for romlig analyse av beredskapsinfrastruktur
4. **Demonstrert verdien** av åpne datasett for samfunnssikkerhet

Resultatene indikerer at det er store variasjoner i tilfluktsromsdekning på tvers av regionen. Mange områder med høy befolkningstetthet har utilstrekkelig kapasitet, hvilket understreker behovet for ytterligere planlegging og ressursallokering.

Denne type geografiske analyseverktøy kan være verdifulle for kommuner, fylker og nasjonale myndigheter i deres arbeid med beredskapsplanlegging og risikohåndtering. Det demonstrerer også viktigheten av å vedlikeholde oppdaterte og nøyaktige datasett for kritisk infrastruktur.

# 📚 Kilder
Kartverket / GeoNorge: https://kartkatalog.geonorge.no
OpenStreetMap: https://www.openstreetmap.org
PostGIS Dokumentasjon: https://postgis.net/documentation/
Supabase API: https://supabase.com/docs/
