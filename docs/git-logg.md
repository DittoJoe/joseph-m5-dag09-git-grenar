# Git-logg

Klistra in utskrifter och svara på frågorna. Det här är din dokumentation av dagens arbete.

## 1. Utgångsläget
Skriv ut `git log --oneline --graph --all` direkt efter att du klonat. Klistra in här:

* 5a5841d (HEAD -> main, upstream/main, origin/main, ori>
* 3804533 Add files via upload
* f7a13a4 Add files via upload
* c9a0075 Initial commit

## 2. Merge utan konflikt
Klistra in `git log --oneline --graph --all` efter merge:

*   5d5f1b4 (HEAD -> main) merge without conflict
|\
| * 2efc908 (meny-nyheter) Lägg till Vaniljbulle på menyn
* | 1bd25c5 Lägg till telefonnummer
|/
* 5a5841d (upstream/main, origin/main, origin/HEAD) Modu>
* 3804533 Add files via upload
* f7a13a4 Add files via upload
* c9a0075 Initial commit

Fråga: Vad är skillnaden mellan en *fast-forward*-merge och en merge som skapar en egen merge-commit? Svara med egna ord:

En fast-forward händer när den finns ingen konflikt

## 3. Konflikten
Klistra in filen med konfliktmarkörerna, precis som den såg ut innan du löste den:

# Öppettider

Vardagar: 07–18
<<<<<<< HEAD
Helger: 10–17
=======
Helger: 09–18
>>>>>>> oppettider-sommar
Röda dagar: stängt


Fråga: Vad betyder `<<<<<<< HEAD`, `=======` och `>>>>>>> grennamn`?
HEAD visar ändringen som finns där du är nu, medans grennamn visar ändringen från en annan gren

Hur löste du den, och varför blev det så?
Jag valde de längre öppettider för att kunna vara mer precis sen

## 4. Ångra
Vad är skillnaden mellan `git restore`, `git revert` och `git reset`? Vilken är säkrast när ändringen redan är pushad?
git revert, då går vi tillbaka till en version som har redan granskats

## 5. Pull request
Länk till din pull request (på ditt eget repo):
https://github.com/DittoJoe/joseph-m5-dag09-git-grenar/pull/1

## 6. Reflektion
Vad är det värsta som kan hända om man kör `git push --force` på en gren som andra använder?
Allt deras jobb försvinner och de måste starta om utan att kunna se historiken

