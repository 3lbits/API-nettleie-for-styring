# DIGIN Nettariff API <br> Spesifikasjon

## Dokumentversjoner
|     Dato    |     Versjon    |     Endring    |
|-------------|----------------|----------------|
|  27.10.21   |        0.8     |       Init     |
|             |                |                |
|             |                |                |


## 1. Bakgrunn
DIGINprosjektet 'Nettariff API' jobber med utvikling av en standard for deling av nettariffdata med brukere og tredjepartsakt�rer i kraftsystemet. Det er ikke innenfor prosjektets mandat � standardisere hvilke nettariffmodeller som skal benyttes.
<br/>
Hensikten med APIet er � st�tte styring ved hjelp av smarthusteknologi og dermed stimulere til �kt utnyttelse av fleksibilitet fra sluttbrukere. APIet er ikke ment � brukes til � f� et korrekt historsik datagrunnlag for sluttbrukeres nettariff.
<br/>
Dette betyr for eksempel at APIet leverer ut et GridTariff-objekt med kobling mellom en tariff og et m�lepunkt som er korrekt p� tidspunktet for funksjonskallet. Hvis tidsperioden i g�r lenger tilbake enn startdato for m�lepunktets kontrakt, s� gjenspeiles ikke dette i APIet.
<br/>
Alts� er prishistorikken i responsen koblet til tariffen, ikke m�lepunktet.
<br/>
Prosjektet leverer standardiserte skjema, med tilh�rende dokumentasjon, for utveksling av nettariffdata. Legg merke til at det er opp til det enkelte nettselskap hvordan APIet skal implementeres, s� prosjektet leverer ikke programvare for implementasjon.
<br/>
## 2. Hensikt med dette dokumentet
Dokunmentasjon av beslutninger tatt i DIGINs prosjektgruppe for � lage et standard API for utveksling av Nettariff data for styring/smarthus. 

## 3. Definisjoner
API - Application programing interface
<br/>
OpenAPI - Standard for API spesifikasjoner, se referanser.
<br/>
Konsument/Klient - En applikasjon som konsumerer data fra et API. I denne sammenheng, typisk en 3. partsleverand�r som skal hente nettariff data fra en eller flere nettselskap.
<br/>
Implementasjon/Service - En tjeneste hos et nettselskap som leverer nettariff data etter DIGIN Nettariff spesifikasjonen.
<br/>
LS - Lavspent nettilknytning
<br/>
HS - H�yspent nettilknytning
<br/>
DN - DistribusjonsNett
<br/>
RN - RegionalNett
<br/>

## 4. Versjoner
F�lgende versjoner finnes av DIGIN Nettariff API spesifikasjonen.

|      Versjon     |      Type           |      Beskrivelse                            |      Kommentar        |
|------------------|---------------------|---------------------------------------------|-----------------------|
|     1.0          |     Offisiell       |     Offisiell versjon som skal implementeres|  Ikke utgitt          |
|     0.9          |     Arbeid          |     Arbeids versjon etter innspill          |  Ikke utgitt          |
|     0.8          |     Arbeid          |     Versjon for innspill fra akt�rer        |  Publisert 27.10.2021 |
|     0.7          |     Arbeid          |     Arbeids versjon                         |  Skal ikke publiseres |

## 5. Hva best�r spesifikasjonen av.
Spesifikasjonen er opprettet ved bruk av standarden OpenAPI, https://www.openapis.org/
<br/>
Spesifikasjonen best�r av 2 json filer.
<br/>
<br/>
DiginGridTariffAPI.v0_8.json
<br/>
Dette er OpenAPI spesifikasjonsfilen. Denne inneholder metoder, skjema definisjoner.
<br/>
<br/>
gridtariffapi.v0_8.common.schema.json
<br/>
Inneholder definisjoner for input og output objekter brukt av metoder.
<br/>
<br/>
OpenApi json filer kan vises som SWAGGER dokumentasjon. En m�te � gj�re dette er � benytte Microsoft Visual Studio Code (gratis).
<br/>
Importer OpenApi utvidelsen. 
<br/>
�pne begge json filene i Visual Studio Code.
<br/>
Velge utvidelsen OpenAPI (R�d sirkel rundt) og trykke p� knappen "Show Preview using default render" (R�d sirkel rundt)
<br/>
Dette vill vise SWAGGER dokumentasjon som vist i bildet under.
<br/>
![image](https://user-images.githubusercontent.com/92018405/137330959-ff522cbb-87ee-41b1-9393-f683b0b21964.png)



## 6. Implementasjon
DIGIN leverer ikke en ferdig implementasjon av APIet. DIGIN leverer spesifikasjon for implementasjon.
<br/>
<br/>
Spesifikasjonsfilene kan benyttes til � generere klient og service.<br/>
OpenAPI, https://www.openapis.org/, nevner flere verkt�y som kan benyttes til dette.
<br/>
<br/>
Hvis en bruker Microsoft Visual Studio kan en generere en klient.
<br/>
Dette gj�res i Visual Studio ved � legge til en "Service Reference", velge s� OpenAPI og s� velge filen DiginGridTariffAPI.v0_8.json.
<br/>
Merk at filene DiginGridTariffAPI.v0_8.json og gridtariffapi.v0_8.common.schema.json m� v�re i samme mappe.
<br/>
<br/>
Det finnes open source implementasjoner av tidligere arbeids-versjon av denne spesifikasjonen, som f.eks. Elvias implementasjon:
<br/>
https://github.com/3lvia/grid-tariff-api
<br/>
<br/>
I f�rste versjon av APIet er det kun PULL som st�ttes, med anbefalt kallfrekvens p� �n gang per d�gn. PUSH vurderes st�ttet i fremtidige versjoner!
<br/>
[image](https://user-images.githubusercontent.com/67076443/138090808-99e1e13e-f54d-4166-a437-5872af67a621.png)

  
## 7. Sikkerhet
Implementasjon hos nettselskapene eller deres leverand�rer kan bli "hostet" flere steder og p� forskjellige m�ter.
<br/>
Det er 3 store sky l�sninger, Microsoft Azure, Google Cload, Amazon Web Services.
<br/>
Samt nettselskapene eller leverand�rene kan "hoste" implementasjonen p� lokale "on prem" web servere.
<br/>
Vi har derfor sett det vanskelig � spesifisere hvilken modell av sikkerhet som kan passe alle.
<br/>
DIGIN Grid Tariff API kommer med f�lgende anbefalinger:
<ul>
  <li>En hver implementasjon b�r sikres med autorisering og autentisering av innkommende foresp�rsler.
  <br/>
Hvordan dette gj�res er opp til hver nettselskap/leverand�r.</li>
  <li>Alle implementasjoner b�r benytte seg av https og bruke et gyldig sertifikat utgitt av godkjent leverand�r.
<br/>
Med dette menes sertifikatet b�r v�re godkjent av en "Certificate Authority, CA"</li>
  <li>Alle innkommende foresp�rsler og implementasjoner/installasjoner b�r valideres i henhold til OWASP TOP 10, 
  <a href="https://owasp.org/www-project-top-ten">https://owasp.org/www-project-top-ten</a> </li>
</ul>

## 8. Dato- og timeformat
Alle angivelser av dato og tid i sp�rringer og responser skal v�re i henhold til Elhubs Edielstandard.
<br/>
https://dok.elhub.no/ediel/datetime-elements-37751603.html

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
Fra og med 01.01.2022 endres kravene og i praksis gjelder f�lgende:
<br/>
<br/>
Fastledd:
<ul>
  <li>Fastleddet skal differensieres etter kundens ettersp�rsel etter kapasitet/effekt og vil dermed variere for kunder med �rsforbruk under 100.000 kWh</li>
  <br/>
  <li>I praksis vil de fleste tariffene baseres p� makstime(r) pr dag eller m�ned, eller v�re sikringsbasert.</li>
  <br/>
  <li>Sikringsbasert: niv�et p� fastleddet er basert p� st�rrelse p� hovedsikring.</li>
  <br/>
  <li>Makstimebasert: niv�et p� fastleddet er basert p� de(n) timen(e) i d�gnet, ogs� kalt "d�gnmaks", eller m�neden(e), ogs� kalt "m�nedsmaks", der forbruket m�lt i kW(eller kWh/h) er h�yest.</li>
</ul>
<br/>
<br/>
Effektledd:
<ul>
  <li>Effektledd er kun tillatt for bedriftskunder med �rsforbruk over 100.000 kWh</li>
</ul>
<br/>
<br/>
<br/>
Eksempler p� prising av forskjellige tariffer (pris i kr eks mva og forbrukseffekt/elavgift) og link til eksempelfiler:
<br/>
<br/>
1. M�nedsmaks ("monthlymax" med differensiert fastledd) (priser er inkludert mva og avgifter)
<br/>
Type: LS kunde < 100.000 kWh
<br/>
Nettniv�: LS DN
<br/>
Fastledd (kr/mnd): 
<br/>
    0-2 kW: 100,00
<br/>
    2-4 kW: 115,00
<br/>
    4-8 kW: 140,00
<br/>
    8-12 kW: 170,00
<br/>
    12-16 kW: 225,00
<br/>
    > 16 kW: 350,00
<br/>
Energiledd (�re/kWh):
<br/>
     Vinter dag: 50,58
<br/>
     Vinter natt: 30,58
<br/>
     Sommer dag: 27,85
<br/>
     Sommer natt: 25,85
<br/>
Link eksempel: https://github.com/DIGINenergi/API-nettleie-for-styring/blob/master/doc/DiginGridTariffAPI.v0_8_meteringpointsgridtariffs_json_output_monthlymax_example1.json
<br/>
<br/>
<br/>
2. D�gnmaks (med differensiert fastledd)  (priser er inkludert mva og avgifter)
<br/>
Type: LS kunde < 100.000 kWh
<br/>
Nettniv�: LS DN
<br/>
Fastledd (kr/mnd): 
<br/>
    0-2 kW: 100,00
<br/>
    2-4 kW: 115,00
<br/>
    4-8 kW: 140,00
<br/>
    8-12 kW: 170,00
<br/>
    12-16 kW: 225,00
<br/>
    > 16 kW: 350,00
<br/>
Energiledd (�re/kWh):
<br/>
     Vinter dag: 50,58
<br/>
     Vinter natt: 30,58
<br/>
     Sommer dag: 27,85
<br/>
     Sommer natt: 25,85
<br/>
Link eksempel: https://github.com/DIGINenergi/API-nettleie-for-styring/blob/master/doc/DiginGridTariffAPI.v0_8_meteringpointsgridtariffs_json_output_dailymax_example1.json
<br/>
<br/>
<br/>
3. Sikringsbasert (med differensiert fastledd) (priser er inkludert mva og avgifter)
<br/>
Type: LS kunde < 100.000 kWh
<br/>
Nettniv�: LS DN
<br/>
Fastledd (kr/mnd): 
<br/>
    10 A: 100,00
<br/>
    17 A: 115,00
<br/>
    25 A: 140,00
<br/>
    35 A: 170,00
<br/>
    50 A: 225,00
<br/>
    65 A: 350,00
<br/>
    80 A: 500,00
<br/>
    99 A: 700,00
<br/>
Energiledd (�re/kWh):
<br/>
     Vinter dag: 50,58
<br/>
     Vinter natt: 30,58
<br/>
     Sommer dag: 27,85
<br/>
     Sommer natt: 25,85
<br/>
Link eksempel: https://github.com/DIGINenergi/API-nettleie-for-styring/blob/master/doc/DiginGridTariffAPI.v0_8_meteringpointsgridtariffs_json_output_fusesize_example1.json
<br/>
<br/>
<br/>
4. Effekttariff LS DN (priser er oppgitt ekskludert mva og avgifter)
<br/>
Type: Tariff med effektledd. 
<br/>
Nettniv�: LS DN
<br/>
Fastledd (kr/mnd): 340.00
<br/>
Effektledd (kr/kW/mnd): 
<br/>
    Aktiv effekt vinter: 120,00
<br/>
    Aktiv effekt sommer: 22,00
<br/>
    Reaktiv effekt vinter: 65,61
<br/>
    Reaktiv effekt sommer: 10,61
<br/>
Energiledd (�re/kWh): 
<br/>
     Vinter: 7,87
<br/>
     Sommer: 3,90
<br/>
Link eksempel: https://github.com/DIGINenergi/API-nettleie-for-styring/blob/master/doc/DiginGridTariffAPI.v0_8_meteringpointsgridtariffs_json_output_LSDN_example1.json
<br/>
<br/>
<br/>
5. Effekttariff LS DN med differensiert effektledd (priser er oppgitt ekskludert mva og avgifter)
<br/>
Type: Tariff med effektledd. 
<br/>
Nettniv�: LS DN
<br/>
Fastledd (kr/mnd): 340,00
<br/>
Effektledd (kr/kW/mnd): 
<br/>
    Aktiv effekt vinter: 
<br/>
       0-100 kW : 111,0 
<br/>
       over 100 kW: 55,5
<br/>
    Reaktiv effekt vinter: 65,61
<br/>
    Aktiv effekt sommer: 
<br/>
       0-100 kW : 50,0 
<br/>
       over 100 kW: 25,00
<br/>
    Reaktiv effekt sommer: 10,61
<br/>
  Energiledd (�re/kWh): 
<br/>
     Vinter: 7,87
<br/>
     Sommer: 3,90
<br/>
Link eksempel: https://github.com/DIGINenergi/API-nettleie-for-styring/blob/master/doc/DiginGridTariffAPI.v0_8_meteringpointsgridtariffs_json_output_LSDN_example2.json
<br/>
<br/>
<br/>
<br/>
Eksempler input:
<br/>
Input with range parameter: https://github.com/DIGINenergi/API-nettleie-for-styring/blob/master/doc/DiginGridTariffAPI.v0_8_meteringpointsgridtariffs_json_input_example_range.json
<br/>
Input with startTime and endTime parameters: https://github.com/DIGINenergi/API-nettleie-for-styring/blob/master/doc/DiginGridTariffAPI.v0_8_meteringpointsgridtariffs_json_input_example_startTime_endTime.json
<br/>