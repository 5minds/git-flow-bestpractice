class: center, middle
background-image: url(background-intro.png)

# Arbeiten mit git-flow

---
class: middle, center
background-image: url(background.png)

## Was ist git-flow?

---
background-image: url(img/s1_git_init.png)

.right-column[
## Ausgangssituation

* **master** - Produktive Releases
* **develop** - Integration 'neuer Releases'
* **feature** - Unterstützende Branches
* **hotfix** - Wenns mal schnell gehen muss...
]

---
background-image: url(img/s1_git_init.png)

.right-column[
## Ausgangssituation

1. **Entwickler**
   * Entwickelt Anforderung
   * Zustöndig für Feature-Branches (start/pubslish/finish)

2. **Reviewer**
   * Die Person, die die Entwicklung prüft und Verbesserungsvorschläge aufzeigt
   * Nach Abschluss der Entwicklung prüft der Reviewer die Arbeit und erteilt Freigabe
]

---
class: 
background-image: url(img/s2_feature_start.png)

.right-column[
## Entwickler beginnt die Arbeit

**Feature-Branch erzeugen**

```bash
  » git flow feature start [featurename]
```

**Feature-Branch auf dem Server veröffentlichen**

```bash
  » git flow feature publish [featurename]
```
]

---
class: 
background-image: url(img/s3_feature_finish.png)

.right-column[
## Entwickler arbeitet am Feature

Änderungen der anderen Entwickler vom Server laden

```bash
  » git flow feature pull origin [featurename]
```

Änderungen durchführen und auf dem Server veröffentlichen

```bash
  » git commit
  » git push  #eventuell git push origin feature/[featurename]
```
]

---
class: 
background-image: url(img/s5_feature_pull.png)

.right-column[
## Entwickler holt sich das Feature vom Server

```bash
  » git flow feature track [featurename]
```
optional:
```bash
  » git flow feature rebase -i [featurename]
```
]

---
class: center, middle
background-image: url(background.png)

# Arbeit abgeschlossen --> Review!

---
class:
background-image: url(background.png)

.right-column[
## Reviewer

**Aufgaben**

1 Reviews durchführen

2 Tests durchführen

3 Features abschließen
]

---
class: 
background-image: url(img/s5_feature_pull.png)

.right-column[
## Reviewer

**Holen des aktuellen Stands vom Server**

```bash
  » git flow feature track [featurename]
```

oder

```bash
  » git flow feature pull origin [featurename]
```
]

---
class: 
background-image: url(img/s3_feature_finish.png)

.right-column[
## Reviewer

**Feature-Branch abschließen. Es wird damit automatisch mit dem *Development*-Branch gemerged und gelöscht**

**NUR LOKAL**

```bash
  » git flow feature finish -F [featurename]   # -F führt zuerst ein Fetch aus ;-)
```
]

---
class: 
background-image: url(background.png)

.right-column[
# Reviewer

## Änderungen auf dem Server schieben
```bash
  » git push
```

## Feature Branch löschen
```bash
  » git push origin :feature/[featurename]
```
]

---
class: center, 
background-image: url(background.png)

.right-column[
## Neue Softwareversion --> **Release** ;-)
]

---
class: 
background-image: url(background.png)

.right-column[
## Release-Branch erstellen

**Release starten**
```bash
  » git flow release start v<MAJOR>.<MINOR>.<PATCH>
```

**Release veröffentlichen**
```bash
  » git flow release publish v<MAJOR>.<MINOR>.<PATCH>

  » git push
```
]

---
class: 
background-image: url(background.png)

.right-column[
# Release finalisieren

```bash
  » git flow release finish -Fp v<MAJOR>.<MINOR>.<PATCH>
```
]

---
class: center, 
background-image: url(background.png)

.right-column[
# Bug --> **Hotfix** ;-(
]

---
class: 
background-image: url(background.png)

.right-column[
# Hotfix-Branch erstellen

## Hotfix starten
```bash
  » git flow hotfix start v<MAJOR>.<MINOR>.<PATCH>_<YYYYMMDD>_<#>
```
]

---
class: center, 
background-image: url(background.png)

.right-column[
# Hotfix fixen und testen
]

---
class: 
background-image: url(background.png)

# Hotfix finalisieren

```bash
  » git commit ...

  » git flow hotfix finish -Fp v<MAJOR>.<MINOR>.<PATCH>_<YYYYMMDD>_<#>

  » git push
```
]

---
class: center, 
background-image: url(background.png)

.right-column[
# Tips und Tricks
]

---
class: 
background-image: url(background.png)

.right-column[
# Feature/Release/Hotfix verwerfen

```bash
  » git flow feature|release|hotfix finish [...name]
```
oder
```bash
  » git branch -D [branchname] # (Präfix nicht vergessen :feature/...)
```
]

---
class: 
background-image: url(background.png)

.right-column[
# Remote Tracking Branches anzeigen

```bash
  » git remote show origin
```
]

---
class: 
background-image: url(background.png)

.right-column[
# Lokale Änderungen rückgängig machen

```bash
  » git reset HEAD --hard
```
]

---
class: 
background-image: url(background.png)

.right-column[
# Development Branch als Tracking-Branch auschecken

```bash
  » git checkout -t origin/development
```
]
