# FHIR Workshop 2021

## Start Hapi-fhir-server
Start hapi-fhir-server docker container ved å kjør følgende i en terminal: 
```
docker run -d -p 8080:8080 --name my-fhir-server -e hapi.fhir.default_encoding=json hapiproject/hapi:latest
```
Mer info finnes her: https://hub.docker.com/r/hapiproject/hapi.
Test ved å gå til http://localhost:8080/fhir/Patient i en nettleser, du skal få en tom Bundle av type searchset, det kan ta ca 1 minutt før tjenesten er tilgjengelig.

## Legg inn ressurser
Publiser alle fhir-ressursene i /resources/eksempler utenom QuestionaireResponse i hapi-serveren. Dette gjøres ved å gjøre HTTP POST med hver ressurs til sine respektive fhir-endepunkt. F.eks skal CodeSystem POSTes til http://localhost:8080/fhir/CodeSystem.

Dette kan gjøres vha. cURL-kommandoer i terminalen, men det er lettere med et verktøy, f.eks [Insomnia](https://insomnia.rest/) eller [Postman](https://www.postman.com/). HAPI har også et veldig enkelt web-gui ved å gå til http://localhost:8080/.

Eksprimenter med å gjør endringer på ressursene vha. PUT, sletting vha. DELETE og søk vha. GET.
Hvis du ønsker en clean-state kan du begynne pånytt ved å slette docker containeren: 
```
docker rm --force my-fhir-server
```

## Validering
FHIR ressurser kan valideres ved å bruke et valideringsendepunkt. F.eks kan questionnaire-response ressursen POSTes til /fhir/QuestionnaireResponse/$validate. Prøv å valider de forskjellige ressursene, eksprimenter også med å gjøre endringer som fremprovoserer valideringsfeil.

## Oppgaver
Følgende er noen oppgaver for å bli litt kjent med FHIR og det å navigere i [FHIR spesifikasjonen](http://hl7.org/fhir/).

### 1. Søk
Lag query-strenger for Patient-ressurser med følgende filter (tips: se på sidene for Patient og Search). Opprett gjerne flere Patient ressurser slik at dere har noe å filtrere.
1. Kvinner.
2. Menn født i 1982.
3. Født før 1982.
4. Har 28038203977 som fødselsnummer.
5. Har et fødselsnummer.
6. Heter ikke Jens.
7. Bare hent fødselsdato til Patients (istedenfor hele ressursen).

### 2. History
Gjør en endring på en fhir ressurs og oppdater den vha. PUT. Hent deretter ut den gamle versionen.

### 3. Optimistic-locking
For å unngå at 2 klienter går i beina på hverandre når de oppdaterer samme ressurs kan de benytte optimistic-locking. Les avsnittet [Managing Resource Contention](http://hl7.org/fhir/http.html#concurrency) og oppdater en ressurs.

### 4. Referanser
questionnaireresponse-workshop-skjema skal ha en referanse (subject) til en av Patient ressursene.
1. Opprett QuestionnaireResponse-ressursen i fhir-serveren, gjør nødvendige endringer på referansen.
2. Gjør et søk som henter QuestionnaireResponsen inkludert den refererte Patient ressursen i 1 operasjon. (se _include i spek.).

### 5. Lag en Questionnaire ressurs
Lag ditt eget spørreskjema, finn på tema\spørsmål selv. Skjemaet skal inneholde minst 5 spørsmål av forskjellige typer, prøv å eksprimenter med f.eks required, repeats, enableWhen og CodeSystem og\eller ValueSet. Skjemaet må kunne valideres og besvares.

CodeSystem/ValueSet kan dere lage selv, eller velge blant [de som er definert av HL7](https://www.hl7.org/fhir/terminologies-v3.html) og allerede tilgjengelige i HAPI sin validator.

Ved å åpne dette repoet i Visual Studio Code kan dere få hjelp av IntelliSense når dere jobber med ressursene.

### 6. Lag QuestionnaireResponse ressurs(er)
Del Questionnaire og nødvendige terminology-ressurser (CodeSystem og ValueSet) med hverandre og lag matchende QuestionnaireResponse som lar seg validere.