Förbättring av rumsval


Problembeskrivning

När jag började test obligationen provade jag funktionerna på olika sätt för att kontrollera att de funkade. Till en början märkte jag inte något särskilt problem eftersom jag fokuserar på en funktion i taget och kontrollerade att programmen gav rätt resultat.

När jag sen sen testade hela flödet för att skapa en bokning upptäckte jag att vissa validering gjordes för sent.

Jag provade bland annat att skriva felaktiga datum och tider, då fick jag ett felmeddelande direkt och kunde försöka igen innan jag fortsatte.

Men när jag råkade skriva fel namn på rummet märkte jag inte misstaget. Programmet lät mig fortsätta fylla i datum tider och antal deltagare. Först efter den sista fältet fick jag ett meddelande om att rummet inte existerade.

Jag insåg då att användaren kunde lägga tid på att fylla uppgifter för en bokning som ändå skulle nekas.


Undersökning och orsak

Jag undersökte metoden CreateBooking() i BookingConsole.cs för att förstå varför programmet inte reagerade tidigare.

Jag upptäckte att användaren kunde fortsätta till nästa steg även om rumsnamnet var felaktigt eller kundnamnet var tomt.

Dessa uppgifter kontrollerades först när bokningen skickades vidare till BookingService.

Jag föredrog därför att lägga till validering direkt vid inmatningen, eftersom användaren då kan rätta ett misstag innan nästa steg. På så sätt slipper man fylla i flera fält för att sedan få veta att något var fel redan från början.


Lösning

Jag började med att ändra hur användaren väljer rum. I stället för att skriva rummets namn manuellt skapade jag en meny med tre alternativ: Aspen, Birken och Eken.

Jag använde switch-case för att koppla varje nummer till rätt rum och en while-loop för att upprepa frågan om användaren väljer ett ogiltigt alternativ.

Därefter förbättrade jag inmatningen av kundnamn genom att använda string.IsNullOrWhiteSpace() tillsammans med while. Nu kan användaren inte fortsätta om namnet är tomt eller bara innehåller mellanslag.

Jag lade även till Trim() för att ta bort onödiga mellanslag i början och slutet av kundnamn och sökningar.

Jag behöll valideringarna i BookingService eftersom de fortfarande behövs för att kontrollera bokningarna.

Test och resultat

Efter ändringarna testade jag rumsvalet med både giltiga och ogiltiga alternativ. Vid ett felaktigt val visades ett felmeddelande direkt och jag kunde försöka igen.

Jag kontrollerade även att ett tomt kundnamn inte tillät mig att fortsätta och att extra mellanslag kunde tas bort.


Slutsats

Jag lärde mig att det inte räcker att ett program upptäcker fel. Det är också viktigt när användaren får information om felet.

Genom att validera inmatningen direkt kunde jag göra bokningsprocessen smidigare, minska onödigt arbete och förbättra användarupplevelsen.

Jag insåg också hur viktigt det är att testa ett helt användarflöde, eftersom vissa problem inte märks när man bara testar funktionerna var för sig.


