# Git-logg

Klistra in utskrifter och svara på frågorna. Det här är din dokumentation av dagens arbete.

## 1. Utgångsläget

Skriv ut `git log --oneline --graph --all` direkt efter att du klonat. Klistra in här:

```
$ git log --oneline --graph --all
* 5a5841d (HEAD -> main, origin/main, origin/HEAD) Modul 5 i TypeScript med Vite
* 3804533 Add files via upload
* f7a13a4 Add files via upload
* c9a0075 Initial commit

$ git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main

$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   docs/git-logg.md

no changes added to commit (use "git add" and/or "git commit -a")


```

## 2. Merge utan konflikt

Klistra in `git log --oneline --graph --all` efter merge:

```
$ git log --oneline --graph --all
*   ab22224 (HEAD -> main) Merge branch 'meny-nyheter'
|\
| * 7764b4e (meny-nyheter) Lägger till kanelbulle på menyn
* | a666952 Lägger till telefonummer
|/
* 01ede46 (origin/main, origin/HEAD) Steg 1 - Lägga till logoutput
* 5a5841d Modul 5 i TypeScript med Vite
* 3804533 Add files via upload
* f7a13a4 Add files via upload
* c9a0075 Initial commit
```

Fråga: Vad är skillnaden mellan en _fast-forward_-merge och en merge som skapar en egen merge-commit? Svara med egna ord:

## 3. Konflikten

Klistra in filen med konfliktmarkörerna, precis som den såg ut innan du löste den:

```
<<<<<<< HEAD
Helger: 10–16
=======
Helger: 09–17
>>>>>>> oppentider-sommar-daniel
Röda dagar: stängt
```

Fråga: Vad betyder `<<<<<<< HEAD`, `=======` och `>>>>>>> grennamn`?
Raderna mellan `<<<<<<< HEAD`, `=======` tillhör första branchen
Raderna mellan `=======` och `>>>>>>> grennamn`? tillhör branchen oppentider-sommar-daniel
och dessa 2 rader är i konflict. Git vet inte vilken den ska ta, så programmeraren för avgöra
vad som är "rätt"

Hur löste du den, och varför blev det så?
Raderade raderna (Observera raderna) från <<<<<Head och >>>>>>>
och lade en komprimiss öppentider, där vi båda är nöjda

## 4. Ångra

Vad är skillnaden mellan `git restore`, `git revert` och `git reset`? Vilken är säkrast när ändringen redan är pushad?

- git revert är den säkraste. Den skapar en NY commit med samma state som den föregående commit hade. Historiken bevaras, fast med +1 commit fram i tiden. Dina kollegor får den "rätta" commiten efter en git pull
- git restore, hmmm parametrara gör stor skillnad och jag kan inte alla. Men generellt så skrivs innehållet i filen som finns i working/ area över, från staging/index eller från en commit som finns i repository. När du sedan gör en ny commit så
- git reset skriver om historien. Oftast använder man den på lokala branches. Skriver om historien. Man brukar gå bakåt med reset, dvs branch pekar på en "äldre" commit. Problemet blir när du pushar nästa gång eftersom en vanlig git push får bara flytta serverns branch framåt

- P.S det är så mkt som kan gå fel om man börjar experimentera, bättre göra rätt i början och hålla sig till vissa riktlinjet. Git kan bli hur komplicerat som helst, en parameter kan ändra funktionaliteten väldigt mkt. Git commandon som ändrar historik är problematisk eftersom dina kollegor kan ha pullat ner din historik innan du ändrade din egen.

AI fick genera ett scenario som visar på problematiken
Steg GitHub main Din main Annas main

1. Alla i synk A B C A B C A B C
2. Anna pushar D A B C D A B C A B C D
3. Du kör reset HEAD~1 A B C D A B A B C D <- Här problem börjar
4. Du committar E A B C D A B E A B C D <- med din main
5. Du kör push --force A B E A B E A B C D <- Allt galet

## 5. Pull request

Länk till din pull request (på ditt eget repo):
https://github.com/ripper079/daniel_oikarainen-m5-dag09-git-grenar/pull/1

## 6. Reflektion

Vad är det värsta som kan hända om man kör `git push --force` på en gren som andra använder?
