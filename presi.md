class: center, middle
background-image: url(background-intro.png)

# Working with git and git-flow

---
class: middle
background-image: url(background.png)

# Ausgangssituation

- Es gibt 2 Rollen:
  - Entwickler: Die Person, die eine Anforderung entwickelt.
  - Reviewer: Die Person, die die Entwicklung prüft und Verbesserungsvorschläge aufzeigt.
- 1. Entwickler legt den Feature-Branch an, veröffentlicht ihn auf dem Server und arbeitet darauf
- 2. Entwickler arbeitet auch an dem Feature.
- Nach Abschluss der Entwicklung prüft der Revier die Arbeit und schließt diese ab.

---
class: middle
background-image: url(background.png)

# 1. Entwickler beginnt die Arbeit

### Feature-Branch erzeugen

```
git flow feature start [featurename]
```

### Feature-Branch auf dem Server veröffentlichen

```
git flow feature publish [featurename]
```

---
class: middle
background-image: url(background.png)

# 1. Entwickler entwickelt an dem Feature

### Änderungen der anderen Entwickler vom Server laden

```
git flow feature pull origin [featurename]
```

### Änderungen durchführen und auf dem Server veröffentlichen

```
git commit
git push  # eventuell git push origin feature/[featurename]
```

---
class: middle
background-image: url(background.png)

# 2. Entwickler holt sich das Feature vom Server

```
git flow feature track [featurename]
```
optional:
```
git flow feature rebase -i [featurename]
```

---
class: middle
background-image: url(background.png)

# 1. Entwickler entwickelt an dem Feature

### Änderungen der anderen Entwickler vom Server laden

```
git flow feature pull origin [featurename]
```

### Änderungen durchführen und auf dem Server veröffentlichen

```
git commit
git push  # eventuell git push origin feature/[featurename]
```

---
class: center, middle
background-image: url(background.png)

# Arbeit abgeschlossen --> Review!

---
class: middle
background-image: url(background.png)

# Reviewer

### Holen des aktuellen Stand vom Server
```
git flow feature track [featurename]
```
oder
```
git flow feature pull origin [featurename]
```

---
class: center, middle
background-image: url(background.png)

# Reviewer

### Review und Tests durchführen


---
class: middle
background-image: url(background.png)

# Reviewer

### Feature-Branch abschließen. Es wird damit automatisch mit dem **Development**-Branch gemerged und gelöscht
**NUR LOKAL**

```
git flow feature finish -F [featurename]   # -F führt zuerst ein Fetch aus ;-)
```

---
class: middle
background-image: url(background.png)

# Reviewer

### Änderungen auf dem Server schieben
```
git push
```

### Feature Branch löschen
```
git push origin :feature/[featurename]
```

---
class: center, middle
background-image: url(background.png)

# Neue Softwareversion --> **Release** ;-)

---
class: middle
background-image: url(background.png)

# Release-Branch erstellen

### Release starten
```
git flow release start v<MAJOR>.<MINOR>.<PATCH>
```

### Release veröffentlichen
```
git flow release publish v<MAJOR>.<MINOR>.<PATCH>

git push
```

---
class: middle
background-image: url(background.png)

# Release finalisieren

```
git flow release finish -Fp v<MAJOR>.<MINOR>.<PATCH>
```

---
class: center, middle
background-image: url(background.png)

# Bug --> **Hotfix** ;-(

---
class: middle
background-image: url(background.png)

# Hotfix-Branch erstellen

### Hotfix starten
```
git flow hotfix start v<MAJOR>.<MINOR>.<PATCH>_<YYYYMMDD>_<#>
```

---
class: center, middle
background-image: url(background.png)

# Hotfix fixen und testen

---
class: middle
background-image: url(background.png)

# Hotfix finalisieren

```
git commit ...

git flow hotfix finish -Fp v<MAJOR>.<MINOR>.<PATCH>_<YYYYMMDD>_<#>

git push
```

---
class: center, middle
background-image: url(background.png)

# Tips und Tricks

---
class: middle
background-image: url(background.png)

# Feature/Release/Hotfix verwerfen

```
git flow feature|release|hotfix finish [...name]
```
oder
```
git branch -D [branchname] # (Präfix nicht vergessen :feature/...)
```

---
class: middle
background-image: url(background.png)

# Remote Tracking Branches anzeigen

```
git remote show origin
```

---
class: middle
background-image: url(background.png)

# Lokale Änderungen rückgängig machen

```
git reset HEAD --hard
```

---
class: middle
background-image: url(background.png)

# Development Branch als Tracking-Branch auschecken

```
git checkout -t origin/development
```
