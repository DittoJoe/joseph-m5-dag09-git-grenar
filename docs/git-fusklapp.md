# Git-fusklapp

## Se läget
| Kommando | Gör |
|---|---|
| `git status` | Vad har ändrats, vad är stageat |
| `git branch` | Lista lokala grenar (`*` = den du står på) |
| `git branch -a` | Lista även grenar på GitHub |
| `git log --oneline --graph --all` | Historiken som en graf över alla grenar |
| `git diff` | Ändringar som inte är stageade |
| `git diff main..grenen` | Skillnader mellan två grenar |

## Grenar
| Kommando | Gör |
|---|---|
| `git switch -c namn` | Skapa en ny gren och flytta dit |
| `git switch main` | Byt till en befintlig gren |
| `git merge namn` | Slå ihop grenen `namn` in i grenen du står på |
| `git merge --abort` | Avbryt en merge som blivit konflikt |
| `git branch -d namn` | Ta bort en gren (säkert: nekar om den inte är mergad) |

## Spara och dela
| Kommando | Gör |
|---|---|
| `git add fil` | Lägg en fil i nästa commit |
| `git commit -m "text"` | Spara en commit |
| `git push -u origin namn` | Skicka grenen till GitHub (första gången) |
| `git push` | Skicka nya commits |
| `git pull` | Hämta och slå ihop det som finns på GitHub |

## Ångra
| Kommando | Gör | Säkert? |
|---|---|---|
| `git restore fil` | Kasta ändringar i en fil som inte är committad | Ja, men ändringen försvinner för gott |
| `git revert hash` | Ny commit som tar bort effekten av en gammal | Ja, historiken bevaras |
| `git reset --hard hash` | Flyttar grenen bakåt och raderar ändringar | NEJ. Kan radera arbete |
| `git push --force` | Skriver över historiken på GitHub | NEJ. Aldrig på gemensamma grenar |

## Konfliktmarkörer
```
<<<<<<< HEAD
din version (grenen du står på)
=======
den andras version (grenen du slår ihop)
>>>>>>> grenens-namn
```
Välj, blanda eller skriv om. Ta bort ALLA tre markörrader. `git add filen`, sedan `git commit`.
