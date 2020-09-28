# Proefopgaven DEA Toets 2020
*Versie: 0.1*
*Datum: 28 september 2020*
*Auteur: Bart van der Wal*

In deze serie opgaven maak je zelf een nieuwe Java applicatie, met wat functionaliteit en tests en refactort deze.
NB Deze repo bevat dus GEEN werkend project. Normaal maak jezelf een `README.md` aan in een nieuw project. Maar zet nu gewoon dit bestand in je project na het aanmaken van je project bij opgave 1.

NB2 Verder staat in dit markdown bestand alle code en ook klasse- en methodenamen zoals `Greeter` en `greet("Marie")` tussen zogenaamde backticks. Deze moet je NIET meekopieren bij copy-paste acties. Wel evt. dubbele quotes e.d.. Beste is de 'reader view' van je IDE/editor te gebruiken i.p.v. 'source view'.

Succes!

## Opgave 1 - Maven - 10 punten

### 1A Maak een nieuw Java project aan met Maven
Gebruik als 'groupid' `nl.han.dea`, versie `1.0` en de artifactId is je eigen volledige naam in kebab case met de prefix `proeftoets-2020-`. Dus bijvoorbeeld: `proeftoets-2020-jan-van-steen`.

Zet het gebruikte Maven commando om het project te genereren hieronder in de console expressies in deze `README.md`.

```console
```

Open voordat je naar 1b gaat het zojuist aangemaakte Maven project uit 1a in IntelliJ en:
- Verwijder eventueel aangemaakt standaardcode (zoals unit tests, en evt. een `App.java` of gebruik deze )
- Upgrade in je `pom.xml` naar een hogere Java versie die ook de `var`-syntax ondersteunt (en die je lokaal hebt staan)
- Voeg in de properties van je pom ook dit toe om UTF-8 te gebruiken:
`<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>`
- Update je IntelliJ project voor de bijgewerkte `pom.xml`.

### 1B Hello World code

Zorg dat er een `Main` klasse toe in de root van de aangemaakte package structuur staat en dat deze klasse de standaard public static `main` methode zit.

Voeg onderstaande methoden `greet` toe in deze klasse en laat je `main` methode deze op de goede manier aanroepen. Geef hierbij voor de `name` parameter je eigen voornaam als hardcoded string mee (bijvoorbeeld `"Jan"` :) ). Eindig je `main` methode met het weergeven van het resultaat van de `helloWorld` in de console via een `println`.
NB Hierbij mag je van de `helloWorld` methode NIET een static methode maken.

```java
    public final String greet(String name) {
        return String.format("Hello, World in general and '%s' specifically!", name);
    }

```
NB, 

### 1D. Start met Maven
Geef tenslotte het Maven commando om deze `main` methode vanaf de command line te starten.
Vul deze hieronder in.

```console

```

### Sla de gemaakte code tot nu toe op in een zip `opgave1.zip` (of doe een commit van werk tot nu toe in github.com, maar dat is minder specifieke oefening)


## Opgave 2 - JUnit en refactoring - 10 punten

### Opgave 2A Refactoren en uitbreiden naar meertalige groeter
We gaan nu de simpele applicatie van opgave 1 uitbreiden principe om meertalig te kunnen groeten.
En hem hierbij ook testbaar maken via wat refactoring acties in IntelliJ.

Dit doen we in een serie van refactorings:

A. Gebruik `Extract Superclass` om de `greet` methode naar zijn eigen klasse `Greeter` te verplaatsen.
B. Introduceer een variabele/constante GREETING voor de tekst `"Hello, World in general and... `.
C. Hernoem de bestaande `Greeter` klasse naar `EnglishGreeter`
C. Gebruik een `Extract...` refactoring om nu een abstracte klasse of interface `Greeter` te maken die de `greet(name)` methode bevat.
D Vervang compile time type van `EnglishGreeter` variabelen in `Main` door `Greeter`.
E. Maak een tweede implementatie van de nieuwe `Greeter` genaamd `SpanishGreeter` die de volgende tekst teruggeeft aanroep van `greet()`:
`"¡Hola, mundo en general y '%s' específicamente!"`

NB Het omgekeerde uitroepteken aan het begin van de spaanse groet is dus GEEN `i` :). Maar als copy-pasten niet werkt, mag je dit ook gebruiken ;).
De `%s` in de string zorgt ervoor dat de String.format methode deze kan vervangen door de tweede meegegeven parameter. Hier staan dus weer quotes omheen in de string om hem eruit te laten springen, net als in de Engelse versie.

### Opgave 2B Refactoring, vs code smells vs design patterns
Zorg hierbij dat de bij A aangemaakte `GREETING` op de meest logische plek staat nu we tweetalig zijn, en splits deze in twee 'variabelen' `SPANISH_GREETING` en `ENGLISH_GREETING`.

Hierbij is de term 'magic string' relevant. Wat is dit?
A. De naam van een code smell
B. De naam van een refactor actie
C. Beiden
D. Geen van beiden, magic string is een design pattern

### Opgave 2C Runnen, ¡Hola!
Bij Refactoring B ben je gevraagd om `Extract superclass` te doen, maar het is logischer dat je Main klasse een `Greeter` *heeft* in plaats van dat dit een Greeter *is*. Dit hoort bij het OO principe: 'Favor composition over inheritance'.

Verwijder dus gebruik van de superklasse en geef de `Main` een property met type `IGreeter`. Maak in de `main` hiervan nu een instantie aan van de `SpanishGreeter`, en test of dit werkt (mag runnen in IntelliJ of Maven).


## Opgave 3 Unit tests & Dependency management

### Opgave 3A JUnit 5 dependency
Verander je Maven project zodat je JUnit 5.7.0 tests kunt runnen.

NB/Tip: Denk eraan evt. standaard gegenereerde JUnit 4 tests/testcode uit opgave 1 te verwijderen en je (IntelliJ) project te reloaden.

### Opgave 3B 2 units
Schrijf 2 unit tests voor de `Greeter.helloWorld` methode uit opgave B die zowel de Engelse als Spaanse greeter testen (als Spaanse greeter niet lukte, test dan alleen Engelse).

Geef als `name` de string `"Don Quixote"` mee en gebruik onderstaande `expected` waarden. Zet deze code regels in het correcte blokje volgens het AAA pattern. Zorg voor 100% line coverage ('line code coverage').

```java
    var expected = "Hello, World in general and 'Don Quixote' specifically!";
    ...
    var expected = "¡Hola, mundo en general y 'Don Quixote' específicamente!";
```

### Opgave 3C Before
Refactor nu je geschreven test code nog om meer DRY te zijn. Zie hierbij `"Don Quichote"` ook als magic string. En gebruik hierbij ook initialisatie van testwaarden en sut met de standaard JUnit methode.

## Opgave 4 Exceptions

### Opgave 4A
Voeg in de greeter code nu onderstaande `askName` methode toe in `Main` klasse.

Vervang de aanroep van `greet` met een hardcoded string in de `Main` nu door een zelf (door de gebruiker ingegeven string) - analoog aan opgave 1 - door deze uit te vragen:
```java
    var name = askName()
```

```java
    /**
     * Read an 'entered' string from the keyboard (e.g. 'standard in') (uses a Scanner).
     * @return The string that was read from the keyboard.
     * Source: https://www.techiedelight.com/read-string-standard-input-java/
     */
    public String askName() {
        System.out.println("Welcome! \nPlease type your name, followed by the Enter key (⏎)");
        Scanner scanner = new Scanner(System.in);
        String tokens[] = scanner.nextLine().split("\n");
        scanner.close();
        return tokens[0];
    }
```

### Opgave 4B NoNameSuppliedException
De `greet` methode print een lege naam als de gebruiker direct enter drukt in plaats van een naam invoert. Zorg ervoor dat de methode je eigen custom `NoNameSuppliedException`. Maak hier een non-checked exception van...

### Opgave 4C Catch
Pas je code zo aan dat als de exceptie gegooid wordt de main methode om een naam blijft vragen tot de gebruiker wel een string invoert.

# TODO
Onderstaande is nog niet klaar, maak hiervoor de `PrimeTester` opgave (https://github.com/HANICA-DEA/exercise-maven-threading).

## Opgave 5 Lambda expressies - 5 punten
### TODO Work in progress


Voeg een klasse `StudentResult` toe in je project.
Herschrijf onderstaande imperatieve code in de average functie naar functionele variant die met Streams werkt. Je hoeft niet per se naar de huidige werking te kijken. Maar de 'average' functie berekent het gemiddeld cijfer als float tussen 0.0 en 10.0, maar 'streept' hierbij het laagste behaalde cijfer nog weg.

```java
public class StudentResult {

    private List<Grade> grades = 

    private Student student;

    public StudentResult(Student student, List<Grade> grades) {
        this.student = student;
        this.grades = grades;
    }

    public int average()
        let sum = 0.0;
        let minimum = 0.0;
        for (var grade: this.grades) {
            let gradeValue = grade.getValue();
            sum = sum + gradeValue
            if minimum>gradeValue {
                minimum=gradeValue;
            }
        }
        // Lowest grade can be skipped.
        sum = sum-minimum;

        // Determine the average of the rest of the grades.
        var average = (sum/grades.size()-1);
        return average;
    }

    public boolean isSufficient() {
        return average()>=5.5
    }
}

class Student {
    private int studentId;
    private String name;

    public Student(int studentId, String name) {
        this.name = name;
        this.studentId = studentId;
    }

    @Override
    public equals(Object student) {
        if (!student instanceof Student) {
            return false;
        }
        return studentId==student.studentID;
    }
}

class Grade() {
    public Grade(float value) {
        if (value>10.0 || value <0.0) {
            throw InvalidArgumentException("Grade should be between 0.0 and 10.0 (inclusive these borders)");
        }
        this.value = value;
    }
    getValue() {
        return value;
    }
    // TODO (later): Connect course info per grade....
}
```

Schrijf een functionele interface genaamd 'Averageable` met een methode `average` die een lijst van cijfers verwacht

Zorg dat de `StudentResult` klasse deze functionele interface implementeert.

Zorg dat de methode `average` als deze een cijferlijst (grades) met minder dan drie cijfers erin krijgt een custom exception `NotEnoughGradesException` gooit. De methode . Moet je hier dan een checked exception van maken of een unchecked exception?
Hoe doe je dit? Zet deze exception in een subpackage 

## Opgave 6 - Multithreading - 10 punten

### TODO Work in progress
Het is einde van het blok, de gemiddeldes moeten uitgerekend worden van duizenden studenten. We 
gaan nu het uitrekenen van gemiddeldes uit de vorige opgave parallel laten uitvoeren, door meerdere threads te starten.

### 6A Bepaal welke klasse Runnable moet worden

### 6B Synchroniseer op de student iterator

### 6C 

