# Dag 9 · Git: grenar, merge och konflikter

*Modul 5, UI/UX & Frontendutveckling (JavaScript), Lexicon IT-Proffs*

## Vad du ska göra idag

Du lär dig använda Git på riktigt: **grenar** för att arbeta utan att störa `main`, **merge** för att slå ihop, att **lösa en konflikt** när två ändringar krockar, att **ångra** säkert och att öppna en **pull request** på ditt eget repo. Du dokumenterar allt i `docs/git-logg.md`.

## Bakgrund

Hittills har du jobbat på en enda gren och bara gått framåt. I verkligheten jobbar flera personer samtidigt, och du själv vill kunna prova något utan att riskera det som fungerar. Därför finns grenar. En merge-konflikt är inget fel, det är Git som säger: "ni har ändrat samma rad, du måste avgöra vilken som ska gälla". Idag skapar vi konflikten med flit, så att den inte är skrämmande när den dyker upp på riktigt. Du arbetar helt själv, på din egen fork.

## Så arbetar du (samma som alltid)

1. **Forka** dagens repo på GitHub (*Fork → Create fork*).
2. **Klona din fork:** *Code → HTTPS → kopiera adressen*. I terminalen (Ctrl+ö i VS Code): `git clone <adressen>`. Öppna den nya mappen i VS Code och starta *Live Server*.
3. **Gör uppgiften.** Spara och kontrollera i webbläsaren och Console (F12) efter varje steg. Gör en commit efter varje avslutat steg: `git add .` och `git commit -m "Beskriv vad du gjorde"`.
4. **Skicka upp** när du är klar: `git push`.
5. **Fortsätt i `mitt-projekt`** med dagens projektsteg (längre ned).
6. **Lämna in i Microsoft Forms.**

Den här dagen jobbar du med grenar. Du pushar fler grenar än `main`, och du öppnar en pull request. Stegen nedan visar exakt hur.

Fastnar du: skriv ner exakt var och vad du försökt (och vilket felmeddelande du fick), och ta det först i nästa handledda pass.

## Uppgiften steg för steg

### Steg 1. Klona och titta runt

Forka repot, kör `git clone`, öppna mappen i VS Code. Kör `git log --oneline --graph --all`, `git branch -a` och `git status`. Klistra in loggen i `docs/git-logg.md` (avsnitt 1). Läs igenom `docs/git-fusklapp.md`.

### Steg 2. En gren för en ny funktion

Skapa en gren: `git switch -c meny-nyheter`. Lägg till en rad sist i `kafe-info/meny.md`, till exempel `- Kanelbulle, 33 kr`. Gör `git add .` och `git commit -m "Lägg till kanelbulle på menyn"`. Kör `git branch` och se att du står på grenen. Titta i `kafe-info/meny.md` på `main`: byt med `git switch main` och se att raden inte finns där. Byt tillbaka och se att den finns.

### Steg 3. Merge utan konflikt

Stå på `main`: `git switch main`. Ändra `kafe-info/kontakt.md` (lägg till en rad med ett telefonnummer), `git add .` och `git commit -m "Lägg till telefonnummer"`. Slå ihop: `git merge meny-nyheter`. Editorn öppnas för merge-meddelandet: spara och stäng. Kör `git log --oneline --graph --all` och klistra in grafen i `docs/git-logg.md` (avsnitt 2). Besvara frågan om fast-forward.

### Steg 4. Skapa en konflikt med flit

Skapa två grenar från `main` som ändrar SAMMA rad. Gren 1: `git switch -c oppettider-helg`, ändra `Helger: 09–16` till `Helger: 10–17` i `kafe-info/oppettider.md`, commit. Tillbaka: `git switch main`. Gren 2: `git switch -c oppettider-sommar`, ändra samma rad till `Helger: 09–18`, commit. Tillbaka: `git switch main`. Kör `git merge oppettider-helg` (går bra, en så kallad *fast-forward*). Kör sedan `git merge oppettider-sommar`. Nu får du CONFLICT.

### Steg 5. Lös konflikten

Öppna `kafe-info/oppettider.md` i VS Code. Klistra in filen med markörerna i `docs/git-logg.md` (avsnitt 3) innan du ändrar något. Välj en av raderna, eller skriv en ny (till exempel `Helger: 10–18`), och ta bort ALLA tre markörrader (`<<<<<<<`, `=======`, `>>>>>>>`). Spara. `git add kafe-info/oppettider.md`, sedan `git commit` (spara standardmeddelandet). Kontrollera: `git status` ska vara rent och `git grep "<<<<<<<"` ska inte ge någon träff. Förklara i loggen vad markörerna betyder och hur du valde.

### Steg 6. Avbryt en merge

Skapa en ny konflikt på samma sätt (två nya grenar som ändrar `Röda dagar: stängt` på varsitt sätt). Kör `git merge` så att du får konflikt, och avbryt sedan med `git merge --abort`. Kör `git status`: allt är som förut. Att kunna backa är det som gör konflikter ofarliga.

### Steg 7. Ångra säkert

Ändra något i `kafe-info/meny.md` utan att committa och kör `git restore kafe-info/meny.md` (ändringen försvinner). Gör en commit med en onödig ändring, hitta hashen med `git log --oneline` och kör `git revert <hash>`: Git skapar en ny commit som tar bort effekten, och historiken bevaras. Läs om `git reset --hard` och `git push --force` i fusklappen. Skriv i loggen (avsnitt 4) vilken som är säkrast när något redan är pushat.

### Steg 8. Ignorera filer med .gitignore

Skapa filerna `.env`, `debug.log` och `node_modules/x.txt` (mappen får du skapa själv). Kör `git status`: de syns. Skapa `.gitignore` med raderna `.env`, `*.log` och `node_modules/`. Kör `git status` igen: nu syns bara `.gitignore`. Commit. Förklara varför man aldrig ska committa en `.env`.

### Steg 9. Pull request på ditt eget repo

Skapa en gren `info-uppdatering`, ändra något i `kafe-info/`, committa och kör `git push -u origin info-uppdatering`. På GitHub: *Compare & pull request*. VIKTIGT: ändra *base repository* till ditt EGET repo (som standard föreslår GitHub Lexicon-RC, och det vill du inte). Skriv en beskrivning, klicka *Create pull request* och sedan *Merge pull request*. Lokalt: `git switch main`, `git pull`, `git branch -d info-uppdatering`. Klistra in länken i loggen (avsnitt 5).

### Steg 10. Fördjupning (frivillig): stash och cherry-pick

Läs om `git stash` (lägg undan ändringar tillfälligt) och `git cherry-pick` (plocka en enskild commit till en annan gren). Prova båda i en testgren och förklara när du skulle behöva dem.

## AI-spåret (nivå 2: Specificera och jämför)

**Konflikten, först själv** (cirka 20 minuter, efter att du gjort din egen lösning)

Du beskriver exakt vad koden ska göra och skriver testerna. AI föreslår kod, du kör testerna, jämför och förstår. Git-kommandon som AI föreslår kan radera arbete. Du ska förstå dem innan du kör dem.

Regler: egen lösning först, du ska kunna förklara varje rad, och du loggar i `docs/ai-logg.md` i `mitt-projekt` under rubriken *Modul 5*. Reglerna står i `AI-REGLER-MODUL5.md`.

1. Skapa en konflikt och lös den själv i VS Code enligt övningen.
2. Skapa en ny konflikt. Be AI förklara vad konfliktmarkörerna betyder.
3. Be AI föreslå en lösning och jämför med din.
4. Kör aldrig ett git-kommando du inte kan förklara. Fråga AI vad det gör först.
5. Kontrollera resultatet med git log --graph --oneline.

Prompt att utgå från:

```
Jag har en git-merge-konflikt i den här filen:
[klistra in filen med <<<<<<< markörer]
Förklara vad varje del betyder. Föreslå en lösning
men kör inget. Förklara också vilka kommandon
jag skulle köra efteråt och vad de gör.
```

**Kontrollera med:**

- git status och git log --graph --oneline.
- Öppna filen och leta efter kvarglömda markörer.
- Kan du förklara varje kommando AI nämnde?

**I ditt projekt:** Arbeta i en feature-branch i mitt-projekt, öppna en pull request till din egen main och lös en konflikt. Dokumentera i docs/git-logg.md.

## Kontrollista: så vet du att du är klar

- [ ] `docs/git-logg.md` är ifylld med graf-utskrifter, konfliktfilen, förklaringar med egna ord och PR-länk.
- [ ] Historiken innehåller minst en merge-commit och en löst konflikt.
- [ ] Inga konfliktmarkörer finns kvar i någon fil (`git grep "<<<<<<<"` ger inga träffar).
- [ ] Du har avbrutit en merge med `git merge --abort`.
- [ ] Du har en `.gitignore` som döljer `.env`, `*.log` och `node_modules/`.
- [ ] Din pull request är öppnad och mergad på ditt eget repo (inte på Lexicon-RC).
- [ ] Du kan förklara skillnaden mellan `restore`, `revert` och `reset`.
- [ ] Du har gjort AI-uppgiften och skrivit en post i `docs/ai-logg.md` i `mitt-projekt`.

## Tips om du fastnar

- Osäker på var du står? `git status` och `git branch` svarar alltid.
- Konflikt och panik? `git merge --abort` tar dig tillbaka till innan merge.
- Editorn som öppnades fastnar? Skriv ett meddelande, spara och stäng fliken (i VS Code), eller `:wq` i vim.
- Glömde du `git add` efter att ha löst konflikten? `git status` visar "Unmerged paths". Gör `git add filen` och `git commit`.
- Kör aldrig `git reset --hard` eller `git push --force` utan att veta exakt vad de gör. De kan radera arbete.
- Windows-fråga: får du "LF will be replaced by CRLF"? Det är en varning, inte ett fel. Ignorera den.
- Du pushade till fel gren? Kör `git branch` och `git log --oneline --graph --all` och kolla innan du gör något drastiskt.

## Ditt projekt: Arbeta i en gren i ditt projekt och lös en konflikt

Efter övningen jobbar du vidare i `mitt-projekt`, samma repo som i modul 4. Övningen här är träningsbanan, projektet är det som växer. Dagens steg står också i `PROJEKTSTEG-MODUL5.md` (som du kopierar till ditt projekt dag 1), under **Dag 9**.

1. Se till att `main` i ditt projekt fungerar och är pushad. `git status` ska vara rent.
2. Skapa en gren `feature/ny-funktion` (välj ett eget namn som beskriver vad den gör). Gör minst två commits där.
3. Skapa en medveten, ofarlig konflikt i `docs/git-logg.md` i projektet: ändra samma rad på `main` och på grenen. Slå ihop och lös den.
4. Pusha grenen och öppna en pull request till `main` på ditt eget repo (kontrollera *base repository*). Mergea den.
5. Lägg till `.gitignore` om du saknar en (`.env`, `*.log`, `node_modules/`).
6. Dokumentera i `docs/git-logg.md` i projektet: grafen, konflikten och hur du löste den.
7. Commit och push.

**Klart när:** Projektet har en mergad pull request, en löst konflikt, en `.gitignore` och en ifylld `docs/git-logg.md`.

## Inlämning

**Deadline: imorgon klockan 09.00.** Allt lämnas in i Microsoft Forms. Du behöver inte redovisa något muntligt.

I formuläret fyller du i:

1. Länk till din fork av det här repot.
2. Länk till ditt `mitt-projekt`.
3. Reflektion: Vad är en merge-konflikt, varför uppstår den, och varför är det okej att den uppstår? Beskriv hur du löste din egen konflikt, steg för steg.

## Vill du mer? (frivilligt)

- Skapa en tredje gren som ändrar samma rad och slå ihop alla tre. Hur ser filen ut mitt i konflikten?
- Läs om `git rebase` och beskriv skillnaden mot `git merge` med egna ord. Kör inte rebase på delade grenar.
- Ställ in grenskydd på `main` i ditt repo på GitHub (Settings, Branches, Add rule) så att man måste använda pull request. Förklara varför team gör så.
