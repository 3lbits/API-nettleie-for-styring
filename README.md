# DIGIN Nettariff API <br> Spesifikasjon

## Dokumentversjoner
|     Dato    |     Versjon    |     Endring       |
|-------------|----------------|-------------------|
|  27.10.21   |        0.8     |       Init        |
|  17.11.21   |        0.9     | Soft release      |
|  01.12.21   |        1.0     | Offisiell versjon |

## 1. Bakgrunn
DIGINprosjektet 'Nettariff API' jobber med utvikling av en standard for deling av nettariffdata med brukere og tredjepartsaktører i kraftsystemet. Det er ikke innenfor prosjektets mandat å standardisere hvilke nettariffmodeller som skal benyttes.
<br/>
Hensikten med APIet er å støtte styring ved hjelp av smarthusteknologi og dermed stimulere til økt utnyttelse av fleksibilitet fra sluttbrukere. APIet er ikke ment å brukes til å få et korrekt historisk datagrunnlag for sluttbrukeres nettariff.
<br/>
Dette betyr for eksempel at APIet leverer ut et GridTariff-objekt med kobling mellom en tariff og et målepunkt som er korrekt på tidspunktet for funksjonskallet. Hvis tidsperioden går lenger tilbake enn startdato for målepunktets kontrakt, så gjenspeiles ikke dette i APIet.
<br/>
Altså er prishistorikken i responsen koblet til tariffen, ikke målepunktet.
<br/>
Prosjektet leverer standardiserte skjema, med tilhørende dokumentasjon, for utveksling av nettariffdata. Legg merke til at det er opp til det enkelte nettselskap hvordan APIet skal implementeres, så prosjektet leverer ikke programvare for implementasjon.
<br/>
Denne versjonen av standard for 'Nettariff API' tar ikke hensyn til kunder med redusert elavgift. Disse kundene må selv sørge for å trekke fra sin reduksjon av elavgift for å få korrekte priser.
<br/>

## 2. Hensikt med dette dokumentet
Dokumentasjon av beslutninger tatt i DIGINs prosjektgruppe for å lage et standard API for utveksling av Nettariff data for styring/smarthus. 

## 3. Definisjoner
API - Application programming interface
<br/>
DN - DistribusjonsNett
<br/>
HS - Høyspent nettilknytning
<br/>
Implementasjon/Service - En tjeneste hos et nettselskap som leverer nettariff data etter DIGIN Nettariff spesifikasjonen.
<br/>
Konsument/Klient - En applikasjon som konsumerer data fra et API. I denne sammenheng, typisk en 3. partsleverandør som skal hente nettariff data fra en eller flere nettselskap.
<br/>
LS - Lavspent nettilknytning
<br/>
MPID - Målepunkt-Id som finnes på faktura fra Nettselskapet eller på Min side (et logisk nummer som ikke er det samme som målernummer)
<br/>
OpenAPI - Standard for API-spesifikasjoner, se referanser.
<br/>
RN - RegionalNett (NB. DEKKES IKKE AV APIet)
<br/>
Unique id - En unik id som er garantert unik innenfor responsen fra ett nettselskap. Dette kan være for eksempel en GUID (Global Unique IDentifier) eller et løpenummer som unikt identifiserer elementet i responsen. Denne er ikke garantert unik på tvers av flere nettselskaper.
<br/>


## 4. Versjoner
Følgende versjoner finnes av DIGIN Nettariff API spesifikasjonen.

|      Versjon     |      Type           |      Beskrivelse                            |      Kommentar        |
|------------------|---------------------|---------------------------------------------|-----------------------|
|     1.0          |     Offisiell       |     Offisiell versjon som skal implementeres|  Publisert 01.12.2021 |
|     0.9          |     Arbeid          |     Arbeidsversjon etter innspill           |  Ikke utgitt          |
|     0.8          |     Arbeid          |     Versjon for innspill fra aktører        |  Publisert 27.10.2021 |
|     0.7          |     Arbeid          |     Arbeidsversjon                          |  Skal ikke publiseres |

## 5. Hva består spesifikasjonen av
Spesifikasjonen er opprettet ved bruk av standarden OpenAPI, https://www.openapis.org/.
<br/>
Spesifikasjonen består av 2 json filer.
<br/>
<br/>
DiginGridTariffAPI.v1_0.json
<br/>
Dette er OpenAPI spesifikasjonsfilen. Denne inneholder metoder og skjemadefinisjoner.
<br/>
<br/>
gridtariffapi.v1_0.common.schema.json
<br/>
Inneholder definisjoner for input- og outputobjekter brukt av metoder.
<br/>
<br/>
OpenApi json filer kan vises som SWAGGER dokumentasjon. En måte å gjøre dette er å benytte Microsoft Visual Studio Code (gratis).
<br/>
Importer OpenApi utvidelsen. 
<br/>
Åpne begge json filene i Visual Studio Code.
<br/>
Velg utvidelsen OpenAPI (Rød sirkel rundt) og trykk på knappen "Show Preview using default render" (Rød sirkel rundt)
<br/>
Dette vil vise SWAGGER-dokumentasjon som vist i bildet under.
<br/>
![image](https://user-images.githubusercontent.com/92018405/137330959-ff522cbb-87ee-41b1-9393-f683b0b21964.png)



## 6. Implementasjon
DIGIN leverer ikke en ferdig implementasjon av APIet. DIGIN leverer spesifikasjon for implementasjon.
<br/>
<br/>
DiginGridTariffAPI.gridcompany-mapping.json
<br/>
Nettselskap som implementerer Nettariff API melder inn sine MPID-serier, navn på nettselskap, organisasjonsnummer, url til api og url til brukerdokumentasjon eller epost-adresse til DIGIN på epost-adresse digin@energinorge.no.
<br/>
Filen inneholder mapping av MPID (fra - til), nettselskapsnavn, nettselskapets organisasjonsnummer, url til api og url til brukerdokumentasjon eller epost-adresse.
<br/>
https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.gridcompany-mapping.json
<br/>
<br/>
GridTariffAPI-3part-registration-and-use-of-api_v1_0.jpg
<br/>
Sekvensdiagram som beskriver rutine for 3.-parts registerering av bruker og utstedelse av api-key.
<br/>
https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/GridTariffAPI-3part-registration-and-use-of-api_v1_0.jpg
<br/>
<br/>
Spesifikasjonsfilene kan benyttes til å generere klient og service.<br/>
OpenAPI, https://www.openapis.org/, nevner flere verktøy som kan benyttes til dette.
<br/>
<br/>
Hvis en bruker Microsoft Visual Studio kan en generere en klient.
<br/>
Dette gjøres i Visual Studio ved å legge til en "Service Reference", velge OpenAPI og så velge filen DiginGridTariffAPI.v1_0.json.
<br/>
Merk at filene DiginGridTariffAPI.v1_0.json og gridtariffapi.v1_0.common.schema.json må være i samme mappe.
<br/>
<br/>
Det finnes open source implementasjoner av tidligere arbeids-versjon av denne spesifikasjonen, som f.eks. Elvias implementasjon:
<br/>
https://github.com/3lvia/grid-tariff-api
<br/>
<br/>
I første versjon av APIet er det kun PULL som støttes, med anbefalt kallfrekvens på én gang per døgn. PUSH vurderes støttet i fremtidige versjoner!
<br/>
<br/>
  
## 7. Sikkerhet
Implementasjon hos nettselskapene eller deres leverandører kan bli "hostet" flere steder og på forskjellige måter.
<br/>
Det er 3 store skyløsninger: Microsoft Azure, Google Cloud, Amazon Web Services.
<br/>
Samt nettselskapene eller leverandørene kan "hoste" implementasjonen på lokale "on prem" web servere.
<br/>
Vi har derfor sett det vanskelig å spesifisere hvilken modell av sikkerhet som kan passe alle.
<br/><br/>
DIGIN kommer med følgende anbefalinger for implementering av GridTariffAPI:
<ul>
  <li>Enhver implementasjon bør sikres med autorisering og autentisering av innkommende forespørsler.
  <br/>
  Hvordan dette gjøres er opp til hver nettselskap/leverandør, men det anbefales fra DIGIN at det anvendes:
  </br>
  <ul>
    <li>HTTPS</li>
    <li>Gyldig sertifikat utgitt av godkjent leverandør
    </br>Med dette menes sertifikatet bør være godkjent av en "Certificate Authority, CA"</li>
    <li>API key (name: X-API-Key) som request header
    </br>
    Mer om bruk av API key her: <a href="https://swagger.io/docs/specification/authentication/api-keys/">https://swagger.io/docs/specification/authentication/api-keys/ </a>
    </br>
    og her: <a href="https://cloud.google.com/endpoints/docs/openapi/when-why-api-key">https://cloud.google.com/endpoints/docs/openapi/when-why-api-key</a> </li> </li> 
    <li>API key utstedes per klient(for eksempel en smarthusleverandør eller en privat bruker) med registrert epost 
    </br>
    API key bør ha en gyldighet på flere år (for eksempel 5 år)
    </br>
    Registrert epost brukes til å varsle klient ved invalidering av API key eller i god tid før automatisk utløp av API key</li></ul>
<br/>

  <li>Alle innkommende forespørsler og implementasjoner/installasjoner bør valideres i henhold til OWASP TOP 10, 
  <a href="https://owasp.org/www-project-top-ten">https://owasp.org/www-project-top-ten</a> </li>
</ul>

## 8. Dato- og timeformat
Alle angivelser av dato og tid i spørringer og responser skal være i henhold til Elhubs Edielstandard.
<br/>
https://dok.elhub.no/ediel/datetime-elements-37751603.html
<br/>
I en tidsperiode, feks angitt av startDate og endDate, så er startDate inkludert og endDate ikke inkludert. Dvs endDate betyr at prisen gjelder inntil denne datoen.
<br/>
Eksempel for en tidsperiode som gjelder hele januar, så angis dette av:
<br/>
startDate = 2022-01-01
<br/>
endDate = 2022-02-01
<br/>
Dette gjelder alle tidsperioder med mindre annet er spesifisert.
<br/>

## 9. Referanser
Intitative, OPEN API. 2021. OPEN API. October. https://www.openapis.org/.
<br/>
2021. SWAGGER. October. https://swagger.io/.
<br/>
Visual Studio Code https://code.visualstudio.com/
<br/>
OWASP https://owasp.org
<br/>
Elhub Edielstandard. https://dok.elhub.no/ediel/edielstandard-37751483.html

## 10. Forklaring av tariffstruktur og eksempler
Nettselskapene velger selv hvordan nettariffene bygges opp, innenfor visse rammer.
<br/>
Fra og med 01.01.2022 endres kravene og i praksis gjelder følgende:
<br/>
<br/>
Fastledd:
<ul>
  <li>Fastleddet skal differensieres etter kundens etterspørsel etter kapasitet/effekt og vil dermed variere for kunder med årsforbruk under 100.000 kWh.</li>
  <br/>
  <li>I praksis vil de fleste tariffene baseres på makstime(r) pr dag eller måned, eller være sikringsbasert.</li>
  <br/>
  <li>Sikringsbasert: nivået på fastleddet er basert på størrelse på hovedsikring.</li>
  <br/>
  <li>Makstimebasert: nivået på fastleddet er basert på de(n) timen(e) i døgnet, også kalt "døgnmaks", eller måneden(e), også kalt "månedsmaks", der forbruket målt i kW(eller kWh/h) er høyest.</li>
</ul>
<br/>
Effektledd:
<ul>
  <li>Effektledd er kun tillatt for bedriftskunder med årsforbruk over 100.000 kWh.</li>
</ul>
<br/>
<br/>
Eksempler på prising av forskjellige tariffer og link til eksempelfiler:
<br/>
<br/>
1. Månedsmaks ("monthlymax" med differensiert fastledd)
<br/>
Type: LS kunde < 100.000 kWh
<br/>
Nettnivå: LS DN
<br/>
Link eksempel: https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.v1_0_meteringpointsgridtariffs_json_output_monthlymax_example1.json
<br/>
<br/>
<br/>
2. Døgnmaks (med differensiert fastledd)  (priser er inkludert mva og avgifter)
<br/>
Type: LS kunde < 100.000 kWh
<br/>
Nettnivå: LS DN
<br/>
Link eksempel: https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.v1_0_meteringpointsgridtariffs_json_output_dailymax_example1.json
<br/>
<br/>
<br/>
3. Sikringsbasert (med differensiert fastledd)
<br/>
Type: LS kunde < 100.000 kWh
<br/>
Nettnivå: LS DN
<br/>
Link eksempel: https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.v1_0_meteringpointsgridtariffs_json_output_fusesize_example1.json
<br/>
<br/>
<br/>
4. Effekttariff LS DN
<br/>
Type: Tariff med effektledd. 
<br/>
Nettnivå: LS DN
<br/>
Link eksempel: https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.v1_0_meteringpointsgridtariffs_json_output_LSDN_example1.json
<br/>
<br/>
<br/>
5. Effekttariff LS DN med differensiert effektledd
<br/>
Type: Tariff med effektledd. 
<br/>
Nettnivå: LS DN
<br/>
Link eksempel: https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.v1_0_meteringpointsgridtariffs_json_output_LSDN_example2.json
<br/>
<br/>
<br/>
6. Effekttariff HS DN med effektledd
<br/>
Type: Tariff med effektledd. 
<br/>
Nettnivå: HS DN
<br/>
Link eksempel: https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.v1_0_meteringpointsgridtariffs_json_output_HSDN_example1.json
<br/>
<br/>
<br/>
Eksempler input:
<br/>
Input with range parameter: https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.v1_0_meteringpointsgridtariffs_json_input_example_range.json
<br/>
Input with startTime and endTime parameters: https://github.com/digin-energi/API-nettleie-for-styring/blob/main/doc/DiginGridTariffAPI.v1_0_meteringpointsgridtariffs_json_input_example_startTime_endTime.json
<br/>

## 11. Endringslogg:
22.12.2021 Versjon 1.0.1: DiginGridTariffAPI.v1_0: Lagt til input parameter Product(for internt bruk for nettselskap) som er Exclusive OR med TariffKey. TariffKey ikke lenger definert required.
<br/>