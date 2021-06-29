# FHIR Workshop 2021

## Start Hapi-fhir-server
Start hapi-fhir-server docker container ved å kjør følgende i en terminal: `docker run -d -p 8080:8080 --name my-fhir-server hapiproject/hapi:latest`
Mer info finnes her: https://hub.docker.com/r/hapiproject/hapi
Test ved å gå til http://localhost:8080/fhir/Patient?_format=json i en nettleser, du skal få en tom Bundle av type searchset.

## Legg inn ressurser
Publiser alle fhir-ressursene i /resources utenom QuestionaireResponse i hapi-serveren. Dette gjøres ved å gjøre HTTP POST med hver ressurs til sine respektive fhir-endepunkt. F.eks skal CodeSystem POSTes til http://localhost:8080/fhir/CodeSystem.
Eksprimenter med å gjør endringer på ressursene vha. PUT, sletting vha. DELETE og søk vha. GET.
Hvis du ønsker en clean-state kan du begynne pånytt ved å slette docker containeren: `docker rm --force my-fhir-server`