## Werkcollege week 3

Vanaf deze week zullen de studenten ook beoordeelt worden op het design en de style van hun code. Dit werkcollege staat daarom in het teken van design en style. We bespreken de beoordeling, styleguide, en leggen uit over de "globals checker", waarna we een code review gaan doen.

Je hebt vorige week **feedback** gegeven, daarover zul je wel wat vragen krijgen. Als studenten hun eigen specifieke feedback willen bespreken kan dit het best even buiten de groep om! ("Kunnen we dat na de werkgroep even bespreken?").

### Terugblik (15 minuten)

Laat iedereen even vertellen hoe het ging, waar het knelde en of het gelukt is. Zeg ook gewoon tegen je studenten dat **klagen** OK is, en zeg dat je goed zult luisteren en noteren (beloof niet dat je er iets mee gaat doen! Het gaat vooral om luisteren, bespreekbaar maken en het totaalbeeld). Hier kan je ook de open vragen van Machine Learning extra bespreken.

⚠️ Jij als mentor moet het gesprek leiden, zorg dat iedereen aan de beurt komt!

- Nog opvallende dingen over specifieke studenten? Noteer ze op Basecamp!
- Nog dingen die mis lijken te gaan voor meerdere studenten? Noteer ze en deel ze na de werkgroep meteen met het team via Basecamp.

### Style (10 minuten)

Doel: Studenten nogmaals wijzen op de styleguide, en uitleggen waarom style zo belangrijk is.

In de eerste week hebben de studenten kennis gemaakt met de styleguide. Deze kan je vinden op de website, links onderaan _iedere_ pagina. Vanaf de derde module zullen de studenten ook daadwerkelijk beoordeeld worden op style en design. (Hiervoor was het alleen nodig om werkende code in te leveren).

Open [de syllabus op de PDP website](https://pdp.mprog.nl/syllabus#passing-the-course) en wijs de studenten aan waar ze op beoordeelt gaan worden vanaf module 3. Als het goed is zijn de studenten vanaf deze week aardig bekend met de basisconcepten van het programmeren, en hebben ze voor hun volgende deadline al twee keer feedback gehad. Beantwoord eventuele vragen die studenten hebben.

Doorloop daarna samen met de studenten [de styleguide op de PDP website](https://pdp.mprog.nl/python/en/style) (hier staan stiekem ook wat design-aspecten in). Het is hierbij belangrijk dat je niet alleen focust op _wat_ er staat, maar ook probeert uit te leggen _waarom_ we het op deze manier aanpakken.

Als er specifieke dingen zijn die je opgevallen zijn tijdens het nakijken van de eerste module, kan je die hier ook nog noemen. Neem ook de tijd om de studenten te vragen om toevoegingen/suggesties.

### Notebook checker (20 minuten)

Doel: De studenten begrijpen wat de `notebook_checker` doet, en waar deze voor waarschuwt.

Mogelijk hebben de studenten het al gezien; in de notebooks vanaf module 2 wordt in de eerste cells een package geïmporteerd dat `notebook_checker` heet:

```python
from notebook_checker import start_checks

# Start automatic globals checks
%start_checks
```

Dit is een door ons (specifiek; Tim Doolan) geschreven package dat bepaalde fouten bij studenten voorkomt die erg lastig te vinden zijn. Wanneer de code hierboven uitgevoerd wordt in een notebook voorkomt dit onder andere dat er in functies variabelen gebruikt worden die niet meegegeven worden. Een concreet voorbeeld:

```python
tekst = "kaas"

def functie_die_wat_print(meegegeven_variabele):
  print(tekst)

functie_die_wat_print("ham")
```

De code hierboven print `"kaas"`, terwijl we volgens de naam van de functie zouden verwachten dat `"ham"` geprint zou worden. Nu is het in dit voorbeeld duidelijk dat er wat mis gaat, maar het wordt een stuk minder duidelijk als er in de code van de student (die verspreid is over een groot aantal cellen) variabelen zijn als hoofdletters: `X`, en `x`. Ook kan er in een functie per ongeluk een globale variabele aangepast worden zoals in het voorbeeld hieronder:

```python
result = []

def simulate(iterations):
    n = 0
    while n < iterations:
        n = n + 1
        result.append(n)

    return result

print(simulate(10))
print(simulate(10))
```

In dit geval wordt `result` globaal aangepast door de functie `simulate()`. De functie werkt één keer zoals verwacht. Wanneer de functie in een andere situatie nog een keer aangeroepen wordt bevat result al elementen. Dit soort aanpassingen aan globale variabelen kan onverwachte bijeffecten veroorzaken die erg lastig te debuggen zijn. Zie hierover ook het stukje ["pure functions" in de styleguide](https://pdp.mprog.nl/python/en/style#pure-functions). We willen "pure" functions; doen maar één ding, gebruiken geen variabelen die ze niet meekrijgen, en hebben geen onverwachte effecten.

Wanneer bovenstaande stukken code in een notebook worden uitgevoerd na het inladen van de notebook checker worden er warnings weergeven. De code wordt verder wel zoals gewoon uitgevoerd.

Download het [voorbeeld notebook](notebook-design/voorbeelden-design.ipynb) voor dit werkcollege.

🧑‍🏫 Uitleg aan studenten

- Leg het bovenstaande over de notebook checker aan de studenten uit m.b.v. het voorbeeld notebook
- Leg uit: In Python zijn er een aantal variabelen die "gereserveerd" zijn, doordat ze al gebruikt worden door functionaliteit die onderdeel is van Python. Dit zijn bijvoorbeeld `sum`, `list`, `id`, etc. In notebooks kan je deze herkennen aan dat ze een (groene) kleur krijgen. Deze wil je zoals in het voorbeeld notebook wordt laten zien niet overschrijven, dan werken ze namelijk niet meer. In Atom krijgen deze built-ins geen kleur.
- Leg uit dat i/o interacties zoals printen en plotten langzaam zijn. Een voorbeeld: het liefst wil je `plt.plot()` zo weinig mogelijk aanroepen. Dit kan je doen door in plaats van iedere keer dat je een punt genereerd deze direct te plotten de punten te verzamelen in lijsten. Zodra je alle punten hebt verzameld plot je de lijst alsof het punten zijn. Ook dit staat in het voorbeeld notebook.
- In Atom kan je de package "MagicPython" installeren, en de package "language-python" uitzetten, dan krijgen in Python ingebouwde functies ook een kleur. Doorloop met de studenten dit proces.

### Code review (30 minuten)

Doel: Studenten zien andere aanpakken dan die van hunzelf. Ze leren te discussiëren over code en zich uit te drukken in aspecten die relateren aan programmeren.

Zoals hierboven al besproken is de komende module de eerste waarop de studenten ook beoordeelt zullen worden op style en design. Nu de studenten bekend zijn met een aantal verschillende aspecten uit style en design is er genoeg kennis om een code review te doen.

> Een code review is een methodische toetsing van code die ervoor bedoeld is om potentiële bugs te vinden, de codekwaliteit te verbeteren, maar ook om kennis en aanpak van verschillende programmeurs uit te wisselen.

🧑‍🏫 Eerste keer code review! Hoe werkt het?

- We doen code reviews in tweetallen. Is er een oneven aantal studenten? Dan mag er één drietal zijn.
- Studenten werken samen, hardop denkend, achter één computer met de code die op dat moment gereviewd wordt. Als dit klaar is, wisselen ze naar de volgende computer voor het stuk code van de ander.
- (5-10 minuten) We beginnen met een klassikaal deel over de opgave waarover de code review gaat:
  - Wat moest er ook alweer gebeuren in de opgave?
  - Wat was er moeilijk?
  - Zijn er dingen die de assistent tijdens het nakijken zijn opgevallen, en waar specifiek op gelet kan worden?
- (15-20 minuten) Iedereen voert de code review uit, mentor loopt langs en bemoeit zich er soms mee, maar is vooral bezig met kritisch luisteren.
- (5 minuten) Vraag een aantal tweetallen of er specifieke dingen zijn geweest die hun opgevallen zijn. Probeer deze te relateren aan de opgaves die de studenten deze week in moeten leveren.

Leg het reviewen zo goed mogelijk uit en zorg dat je studenten corrigeert als ze het verkeerd aanpakken. Laat de studenten zichzelf vragen stellen als: Wat ontbreekt er? Hoe kan de code (nog) beter? Druk de studenten op het hart om hardop na te denken, en de code en de werking daarvan écht te bespreken.

⚠️ Hou het positief. Zorg dat studenten concrete suggesties doen over hoe het beter kan, en niet alleen benoemen wat "fout" is. Noemt iemand een "fout", leg dan zorgvuldig uit waarom het inderdaad niet goed is (leesbaarheid, begrijpelijkheid, consistentie) en vraag de kritiek-gever om een concrete suggestie voor verbetering.

Leg uit dat de studenten code reviews altijd kunnen/mogen gebruiken om elkaars code te beoordelen, waarna het verbeterd kan worden voor de deadline. Het is hierbij wel belangrijk dat (het onderdeel van) de opgave wat gereviewd wordt door **beide** studenten volledig is afgerond.

**We reviewen in deze codereview module 2 van PDP.**

## Administratie

Direct na afloop van de werkgroep:

- Als je weet dat je studenten mist en je hebt geen contact, maak een TODO op Basecamp aan voor de vakcoördinator. Deze zal achter de student aan gaan.
- Als je vermoed dat een student het moeilijk heeft, er een gesprek met gevoerd moet worden, of op een andere manier extra aandacht nodig is, maak dan ook een TODO aan voor de coördinator. Een van je taken is om zo vroeg mogelijk te signaleren dat er mogelijk iets mis gaat.
- Er kunnen vragen zijn opgekomen tijdens de werkgroep. Check voor alle vragen of je antwoorden kunt vinden in de handleiding, of in een post (Message) op Basecamp. Wees niet spaarzaam met je vragen! Liever teveel dan te weinig. De coördinator denkt dan mee en maakt eventueel ook een mededeling voor de andere mentoren.
