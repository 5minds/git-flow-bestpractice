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
### git-flow Befehlsstruktur

* *git-flow* ist eine Zusammenfassung von Standard *git*-Befehlen

* Vereinfacht einen gemeinsamen Workflow

* Orientiert sich an einem zentralisierten Entwicklungsansatz

* Vereinfacht die Qualitätssicherung (Peer-Reviews)
]

---
background-image: url(img/s0_start.png)

.right-column[
### Ausgangssituation

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
### Ausgangssituation

```bash
  git-dojo 𝚿 git flow init
```
]

---
class:
background-image: url(img/s1_git_init.png)

.right-column[
### Ausgangssituation

```bash
  git-dojo 𝚿 git flow init

  Which branch should be used for bringing forth production releases?
    - develop
    - master
  Branch name for production releases: [master]

  Which branch should be used for integration of the "next release"?
    - develop
  Branch name for "next release" development: [develop]

  How to name your supporting branch prefixes?
  Feature branches? [feature/]
  Release branches? [release/]
  Hotfix branches? [hotfix/]
  Support branches? [support/]
  Version tag prefix? []
```
]

---

background-image: url(img/s1-1_branch_names.png)

.right-column[
### Ausgangssituation

* **master** - Letzte Releases
* **release** - Integration von Releases
* **develop** - Integration von Fetures
* **feature** - Umsetzung neuer Features
* **hotfix** - Lösung von Bugs von Releases
* **(support)** - Unterstützende Funktion
]

---
class:
background-image: url(img/s2_feature_start.png)

.right-column[
### Entwickler A beginnt die Arbeit

** *feature*-Branch erzeugen **

```bash
  git-dojo 𝚿 git flow feature start fancy_feature              (b:develop)
  Switched to a new branch 'feature/fancy_feature'

  Summary of actions:
  - A new branch 'feature/fancy_feature' was created, based on 'develop'
  - You are now on branch 'feature/fancy_feature'

  Now, start committing on your feature. When done, use:

      git flow feature finish fancy_feature
```
]

---
class:
background-image: url(img/s2_feature_start.png)

.right-column[
### Entwickler A beginnt die Arbeit
** *feature*-Branch auf dem Server veröffentlichen **

```bash
  git-dojo 𝚿 git flow feature publish fancy_feature        (b:feature/...)
```
]

---
class:
background-image: url(img/s2_feature_start.png)

.right-column[
### Entwickler A beginnt die Arbeit
** *feature*-Branch auf dem Server veröffentlichen **

```bash
  git-dojo 𝚿 git flow feature publish fancy_feature        (b:feature/...)
  Total 0 (delta 0), reused 0 (delta 0)
  To git@github.com:cmg-dev/git-dojo
  * [new branch]      feature/fancy_feature -> feature/fancy_feature
  Already on 'feature/fancy_feature'
  Your branch is up-to-date with 'origin/feature/fancy_feature'.

  Summary of actions:
  - A new remote branch 'feature/fancy_feature' was created
  - The local branch 'feature/fancy_feature' was configured to track
  - You are now on branch 'feature/fancy_feature'
```
]

---
class:
background-image: url(img/s2_1_feature_commit.png)

.right-column[
### Entwickler A arbeitet am Feature

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
### Entwickler B holt sich das Feature vom Server

** Möglichkeit 1: **

```bash
  » git flow feature track [featurename]
```

Beispiel:

```bash
  git-dojo2 𝚿 git flow feature track fancy_feature             (b:develop)

  Branch feature/fancy_feature set up to track remote
  branch feature/fancy_feature from origin.
  Switched to a new branch 'feature/fancy_feature'

  Summary of actions:
  - A new remote tracking branch 'feature/fancy_feature' was created
  - You are now on branch 'feature/fancy_feature'
```
]

---
class:
background-image: url(img/s5_feature_pull.png)

.right-column[
### Entwickler B holt sich das Feature vom Server

** Möglichkeit 2: **

```bash
  » git flow feature pull origin [featurename]
```

Beispiel:

```bash
  git-dojo2 𝚿 git flow feature pull origin fancy2              (b:develop)
  Created local branch feature/fancy2 based on origin's feature/fancy2
```
]

---
class:
background-image: url(img/s5_feature_pull.png)

.right-column[
### Entwickler B holt sich das Feature vom Server

** Sicherheitsfunktionen **

```bash
  git-dojo2 𝚿 git flow feature pull origin fancy2 (b:feature/fancy_fea...)

  Trying to pull from 'feature/fancy2' while currently on
  branch 'feature/fancy_feature'.
  To avoid unintended merges, git-flow aborted.
```
]

---
class: center, middle
background-image: url(background.png)

## Arbeit abgeschlossen --> Review!

---
class:
background-image: url(background.png)

.right-column[
### Aufgaben des Reviewer

1 Reviews durchführen

2 Tests durchführen

3 Features abschließen
]

---
class:
background-image: url(img/s5_feature_pull.png)

.right-column[
### Reviewer

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
### Reviewer

**Feature abschließen. Es wird damit automatisch mit dem *develop*-Branch gemerged und der *feature*-Branch wird gelöscht**

```bash
  » git flow feature finish -F [featurename]
  » # -F lässt zuerst einen Fetch durchführen
```
]

---
class:
background-image: url(img/s3_feature_finish.png)

.right-column[
### Reviewer

** Beispiel **
```bash
git-dojo 𝚿 git flow feature finish -F fancy_feature   (b:feature/fancy...)
Switched to branch 'develop'
Merge made by the 'recursive' strategy.
 TestA.txt | 2 +-
 TestB.txt | 2 ++
 2 files changed, 3 insertions(+), 1 deletion(-)

To git@github.com:cmg-dev/git-dojo
 - [deleted]         feature/fancy_feature
Deleted branch feature/fancy_feature (was 48131dd).

Summary of actions:
- The feature branch 'feature/fancy_feature' was merged into 'develop'
- Feature branch 'feature/fancy_feature' has been removed
- You are now on branch 'develop'
```
]

---
class:
background-image: url(img/s4_feature_publish.png)

.right-column[
### Reviewer

**Änderungen auf dem Server veröffentlichen**

** Optional **
```bash
  » git push
```

Jetzt sind sowohl auf dem Repository als auch lokal der *feature*-Branch gelöscht
]

---
class: center, middle
background-image: url(img/bg1.png)

## Neue Softwareversion --> **Release** ;-)


---
class:
background-image: url(img/s6_release_start.png)

.right-column[
### *release*-Branch erstellen

**Release starten**

```bash
  » git flow release start v<MAJOR>.<MINOR>.<PATCH>
```

```bash
  git-dojo 𝚿 git flow release start v0.1                       (b:develop)
  Switched to a new branch 'release/v0.1'

  Summary of actions:
  - A new branch 'release/v0.1' was created, based on 'develop'
  - You are now on branch 'release/v0.1'

  Follow-up actions:
  - Bump the version number now!
  - Start committing last-minute fixes in preparing your release
  - When done, run:

      git flow release finish 'v0.1'
```
]

---
class:
background-image: url(img/s6_release_start.png)

.right-column[
### *release*-Branch veröffentlichen

**Release veröffentlichen**

```bash
  » git flow release publish v<MAJOR>.<MINOR>.<PATCH>

  » git push
```

[1] Analog zu [SemVer.org](SemVer.org)

]

---
class:
background-image: url(img/s6_release_start.png)

.right-column[
### *release*-Branch veröffentlichen

** Beispiel **

```bash
  git-dojo 𝚿 git flow release publish v0.1                (b:release/v0.1)
  Counting objects: 3, done.
  Delta compression using up to 8 threads.
  Compressing objects: 100% (2/2), done.
  Writing objects: 100% (3/3), 278 bytes | 0 bytes/s, done.
  Total 3 (delta 1), reused 0 (delta 0)
  To git@github.com:cmg-dev/git-dojo
  * [new branch]      release/v0.1 -> release/v0.1
  Already on 'release/v0.1'
  Your branch is up-to-date with 'origin/release/v0.1'.

  Summary of actions:
  - A new remote branch 'release/v0.1' was created
  - The local branch 'release/v0.1' was configured to track the
    remote branch
  - You are now on branch 'release/v0.1'
```
]

---
class:
background-image: url(img/s7_release_finish.png)

.right-column[
### Release finalisieren

Nach der Integration der Features wird der Release finalisiert:

```bash
  » git flow release finish -Fp v<MAJOR>.<MINOR>.<PATCH>
```

Am Ende wird eine stabile Version veröffentlicht und mit einem Tag versehen.

Danach müssen bei der Verwendung von GitHub auch noch die Tags auf dem Server
gespeichert werden:

```bash
  » git push --tags 
```
]

---
class:
background-image: url(img/s7_release_finish.png)

.right-column[
### Release finalisieren
```bash
  git-dojo 𝚿 git flow release finish v0.1                 (b:release/v0.1)

  Switched to branch 'master'
  Your branch is behind 'origin/master' by 1 commit,
  and can be fast-forwarded.
    (use "git pull" to update your local branch)
  Merge made by the 'recursive' strategy.
  New.txt   | 1 +
  TestA.txt | 2 +-
  TestB.txt | 2 ++
  3 files changed, 4 insertions(+), 1 deletion(-)
  create mode 100644 New.txt
  fatal: no tag message?
  Tagging failed. Please run finish again to retry.

```
]

---
class:
background-image: url(img/s7_release_finish.png)

.right-column[
### Release finalisieren
```bash
  git-dojo 𝚿 git flow release finish v0.1                       (b:master)
  #
  # Es folgt Dialog zur Eingabe einer Nachricht für den Tag
  #
  Deleted branch release/v0.1 (was 6ef67a8).

  Summary of actions:
  - Latest objects have been fetched from 'origin'
  - Release branch has been merged into 'master'
  - The release was tagged 'v0.1'
  - Release branch has been back-merged into 'develop'
  - Release branch 'release/v0.1' has been deleted
```
]

---
class: center, middle
background-image: url(background.png)

## Bug --> **Hotfix** ;-(

---
class:
background-image: url(img/s8_hotfix_start.png)

.right-column[
### Hotfix im *hotfix*-Branch starten

** *master*-Branch auschecken**

```bash
  git checkout master
```

**Hotfix starten**
```bash
  » git flow hotfix start v<Ma>.<Mi>.<Pa>_<YYYYMMDD>_<#>
```

SemVer verwenden.
]

---
class:
background-image: url(img/s8_hotfix_start.png)

.right-column[
### Hotfix im *hotfix*-Branch starten

** Beispiel **

```bash
git-dojo 𝚿 git flow hotfix start v0.1.1                         (b:master)

Switched to a new branch 'hotfix/v0.1.1'

Summary of actions:
- A new branch 'hotfix/v0.1.1' was created, based on 'master'
- You are now on branch 'hotfix/v0.1.1'

Follow-up actions:
- Bump the version number now!
- Start committing your hot fixes
- When done, run:

     git flow hotfix finish 'v0.1.1'
```
]

---
class:
background-image: url(img/s9_hotfix_finish.png)

.right-column[
### Bug fixen und testen

*bugfix*-Branches sollten nicht veröffentlicht werden

*git-flow* stellt keine Boardmittel zur Verfügung das zu tun

Nach der Lösung des Bugs wird dieser integriert

]

---
class:
background-image: url(img/s9_hotfix_finish.png)

.right-column[
### Hotfix finalisieren

```bash
  » git commit ...

  » git flow hotfix finish -Fp v<MAJOR>.<MINOR>.<PATCH>_<YYYYMMDD>_<#>
```
]

---
class:
background-image: url(img/s9_hotfix_finish.png)

.right-column[
### Hotfix finalisieren

```bash
  git-dojo 𝚿 git flow hotfix finish v0.1.1               (b:hotfix/v0.1.1)

  Switched to branch 'master'
  Your branch and 'origin/master' have diverged,
  and have 7 and 1 different commit each, respectively.
    (use "git pull" to merge the remote branch into yours)
  Merge made by the 'recursive' strategy.
  bug.txt | 1 +
  1 file changed, 1 insertion(+)
  create mode 100644 bug.txt
  Switched to branch 'develop'
  Your branch is ahead of 'origin/develop' by 1 commit.
    (use "git push" to publish your local commits)
  Merge made by the 'recursive' strategy.
  bug.txt | 1 +
  1 file changed, 1 insertion(+)
  create mode 100644 bug.txt
  Deleted branch hotfix/v0.1.1 (was a996930).
```
]

---
class:
background-image: url(img/s9_hotfix_finish.png)

.right-column[

### Hotfix finalisieren

** Ausgabe von git-flow **

```bash
  Summary of actions:
  - Latest objects have been fetched from 'origin'
  - Hotfix branch has been merged into 'master'
  - The hotfix was tagged 'v0.1.1'
  - Hotfix branch has been back-merged into 'develop'
  - Hotfix branch 'hotfix/v0.1.1' has been deleted
```
]

---
class:
background-image: url(img/s9_hotfix_finish.png)

.right-column[
### Release erzeugen

Ein Release wurde ** automatisch ** bei diesem Vorgang analog zu den vorher gezeigten Release-Vorgang erstellt.
]

---
class: middle, center
background-image: url(img/s10_done.png)

### Das war es... 

---
class: center, middle
background-image: url(background.png)

## Tipps und Tricks

---
class:
background-image: url(background.png)

.right-column[
### Feature/Release/Hotfix verwerfen

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
### Remote Tracking Branches anzeigen

```bash
  » git remote show origin
```
]

---
class:
background-image: url(background.png)

.right-column[
### Lokale Änderungen verwerfen

```bash
  » git reset HEAD --hard
```

Unwiderruflich!
]


---
class:
background-image: url(background.png)

.right-column[
### **develop** Branch als Tracking-Branch auschecken

```bash
  » git checkout -t origin/develop
```
]
