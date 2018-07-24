# Kravspek for wiki

## Overview

Dette dokumentet skal fungere som en kravspek og implementasjonsplan for wikien som senere erstatter dette git-repoet in github.

## Prosjektbeskrivelse

Infected-wikien skal fungere som et crew-wide system for samling av informasjon vedrørende infected, samt relevante prosjekter. Det stilles tre krav til det:

 * Det skal være enkelt å lage/redigere artikler
   - Et sec-medlem skal ikke føle at å skrive artikler er vanskelig eller noe som må settes inn i. 
 * Det skal være lett tilgjelgelig, men med mulighet for å restriktere tilgang
   - Det skal være mulig å begrense avgang på dokumenter ved å gi dokumenter permission-krav for å kunne bli nådd.
   - Det skal være mulig å begrense avgang på dokumenter avhengig av crewmedlemskap og stilling
   - Det skal være mulig å gi ut tilgang på dokumenter til enkeltbrukere, uavhengig av reglene over.
   - _Dette er en nødvendighet for å kunne notere mer konfidensiell informasjon om infected på wikien_

Wiki-siden skal ligge som en underdel på crewsiden, i som en overordnet kategori i sidebaren. Dette skal implementeres fra v3 av crewsiden og utover(div. wiki-siden kommer tidligst når v3 kommer)

## Sidebaren

Wiki-siden fungerer som en funksjon i crewsiden, og har derfor et entry i sidebaren. Det er her wiki-siden lever. Strukturen på sidebar-innholdet er slik:

 * Wiki
   - Artikler
     * [_liste over artikler brukeren har tilgang til_]
   - Lag artikkel

_Artikler_ skal inneholde en liste over alle artikler brukeren har tilgang til, separert etter crew artiklen tilhører. _Lag artikkel_ skal intuitivt nok lage artikler.

Grunnen til at alle artikler blir listet i sidebaren, er først og fremst praktikalitet for resten av crewet. Veldig få i crewet vil få tilgang til såpass mange artikler at det er et problem(typ. Bare folk med `*`). For resten av crewet vil denne listen føre til et mindre klikk, og artiklene vil virke som "mer integrert" i siden.

## Egenskaper ved en artikkel

En artikkel:

 * Har tilhørlighet til et crew
 * Har en revisjonslogg som er lagret
 * Har permissions, som kan endres av ledere for lag og oppover, gitt at du selv har permissions til artikkelen.
 * Kan legge ved bilder som er lastet opp
 * Er skrevet i markdown

Det skal være mulig å se redigeringshistorikken til en artikkel, ved at revisjonene lagres i en egen tabell, og er tilknyttet en artikkel via id. Den seneste revisjonen vil til enhver tid bli brukt.

Å slette en artikkel vil markere den som slettet, men ikke fjerne innholdet fra databasen. Dette er for å unngå tapt informasjon - en artikkel burde ikke ta så mye plass at dette blir et problem.

Artikkelen rendres fra markdown til html ved visning av den. 

## Filopplasting

Bilder må kunne lastes opp i forbindelse med artiklene. Opplasting og håndtering av bilder reserveres til ledere for lag og oppover. Det må verifiseres at opplastingen er et bilde for sikkerhets skyld. Dette kan gjøres ved å prøve å lese bildet med php's innebygde bilde-bibiliotek, og si nei til bildet om det ikke er leselig.

En maksgrense på bildet er ikke nødvendig å implementere, for infected.no har allerede en maksgrense på opplastinger som kan følges på lik linje.

Filer som er lastet opp til wikien får tilhørlighet til en artikkel, må holdes styr på i en egen database, og burde bli slettet/flyttet til en søppelkasse dersom artikkelen de er knyttet til blir slettet. For fremtidens skyld generaliserer vi dette til "filer", men påtvinger at det er et bilde som blir lastet opp i første omgang.

## Ekstra informasjon

### Rangstige i wiki-sammenheng

 * `wiki.admin`
 * Crew-chiefs
 * Lagledere
 * Resten