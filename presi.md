class: center, middle
background-image: url(background-intro.png)

# Arbeiten mit git-flow

---
class: middle, center
background-image: url(background.png)

## Was ist git-flow?

---
background-image: url(img/git-flow-command.png)

.right-column-more-space[
## git-flow Befehlsstruktur

* *git-flow* ist eine Zusammenfassung von Standard *git*-Befehlen

* Vereinfacht einen gemeinsamen Workflow

* Orientiert sich an einem zentralisierten Entwicklungsansatz

* Vereinfacht die Qualitätssicherung (Peer-Reviews)
]

---
background-image: url(img/s0_start.png)

.right-column[
## Ausgangssituation

1. **Entwickler**
   * Entwickelt Anforderung
   * Zuständig für Feature-Branches (start/publish/finish)
   * Setzt Hotfixes um

2. **Reviewer**
   * Prüft nach Abschluss der Entwicklung
   * Zeigt Verbesserungsvorschläge auf
   * Erteilt Freigabe
   * Wissenstransfer
]

---
background-image: url(img/s1_git_init.png)

.right-column[
## Ausgangssituation

```bash
  » git flow init .
```
]

---

background-image: url(img/s1-1_branch_names.png)

.right-column[
## Ausgangssituation

* **master** - Letzte Releases
* **release** - Releases
* **develop** - Integration 'neuer Releases'
* **feature** - Umsetzung neuer Features
* **hotfix** - Lösung akuter Probleme
* **(support)** - Unterstützende Funktion
]

---
class:
background-image: url(img/s2_feature_start.png)

.right-column[
## Entwickler beginnt die Arbeit

** *feature*-Branch erzeugen**

```bash
  » git flow feature start [featurename]
```

** *feature*-Branch auf dem Server veröffentlichen**

```bash
  » git flow feature publish [featurename]
```
]

---
class:
background-image: url(img/s2_1_feature_commit.png)

.right-column[
## Entwickler arbeitet am Feature

Änderungen der anderen Entwickler vom Server laden

```bash
  » git flow feature pull origin [featurename]
```

Änderungen durchführen und auf dem Server veröffentlichen

```bash
  » git add <Files>
  » git commit -m "done..."
  » git push
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
]

---
class: center, middle
background-image: url(background.png)

# Arbeit abgeschlossen --> Review!

---
class:
background-image: url(background.png)

.right-column[
## Aufgaben des Reviewer

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

**Feature abschließen. Es wird damit automatisch mit dem *develop*-Branch gemerged und der *feature*-Branch wird gelöscht**

```bash
  » git flow feature finish -F [featurename]
  » # -F lässt zuerst einen Fetch durchführen
```

Das geschieht zunächst nur **LOKAL**.
]

---
class:
background-image: url(img/s4_feature_publish.png)

.right-column[
## Reviewer

**Änderungen auf dem Server veröffentlichen**
```bash
  » git push
```

Jetzt sind sowohl auf dem Repository als auch lokal der *feature*-Branch gelöscht
]

---
class: center, middle
background-image: url(img/bg1.png)

# Neue Softwareversion --> **Release** ;-)


---
class:
background-image: url(img/s6_release_start.png)

.right-column[
## *release*-Branch erstellen

**Release starten**
```bash
  » git flow release start v<MAJOR>.<MINOR>.<PATCH>
```

**Release veröffentlichen**

```bash
  » git flow release publish v<MAJOR>.<MINOR>.<PATCH>

  » git push
```

[1] Analog zu SemVer.org

]

---
class:
background-image: url(img/s7_release_finish.png)

.right-column[
## Release finalisieren

```bash
  » git flow release finish -Fp v<MAJOR>.<MINOR>.<PATCH>
```
]

---
class: center, middle
background-image: url(background.png)

# Bug --> **Hotfix** ;-(

---
class:
background-image: url(img/s8_hotfix_start.png)

.right-column[
## Hotfix im *hotfix*-Branch starten

** *master*-Branch auschecken**

```bash
  git checkout master
```

**Hotfix starten**
```bash
  » git flow hotfix start v<Ma>.<Mi>.<Pa>_<YYYYMMDD>_<#>
```

Wieder SemVer verwenden.

]

---
class:
background-image: url(img/s9_hotfix_finish.png)

.right-column[
## Bug fixen und testen
]

---
class:
background-image: url(img/s9_hotfix_finish.png)

.right-column[
## Hotfix finalisieren

```bash
  » git commit ...

  » git flow hotfix finish -Fp v<MAJOR>.<MINOR>.<PATCH>_<YYYYMMDD>_<#>

  » git push
```
]

---
class:
background-image: url(img/s9_hotfix_finish.png)

.right-column[
## Release erzeugen

Analog zu "Neue Softwareversion"

]

---
class:
background-image: url(img/s10_done.png)

.right-column[
##Das war es bereits
]

---
class: center, middle
background-image: url(background.png)

# Tips und Tricks

---
class:
background-image: url(background.png)

.right-column[
## Feature/Release/Hotfix verwerfen

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
## Remote Tracking Branches anzeigen

```bash
  » git remote show origin
```
]

---
class:
background-image: url(background.png)

.right-column[
## Lokale Änderungen verwerfen

```bash
  » git reset HEAD --hard
```

Unwiderruflich!
]


---
class:
background-image: url(background.png)

.right-column[
## **develop** Branch als Tracking-Branch auschecken

```bash
  » git checkout -t origin/develop
```
]
---
class:
background-image: url(background.png)

.right-column[
## Rebase beim feature finish



```bash
  » git rebase <...>
```
]
