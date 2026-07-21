# Guide: SAP Integration Suite API Management

## 1. API Management aktivieren

Öffnen Sie in der SAP Integration Suite die Startseite:

```text
Home
```

Öffnen Sie die Kachel:

```text
Manage Capabilities
```

Klicken Sie auf:

```text
Add Capability
```

Wählen Sie folgende Capabilities aus:

✅ Manage APIs

✅ Developer Hub

Klicken Sie anschließend auf:

```text
Activate
```

> Hinweis:
> Die Aktivierung dauert in der Regel einige Minuten.

### Ergebnis

API Management und Developer Hub wurden erfolgreich aktiviert.

---

## 2. Rechte vergeben

Wechseln Sie in das SAP BTP Cockpit.

Navigieren Sie zu:

```text
Security
→ Users
```

Öffnen Sie Ihren Benutzer.

Scrollen Sie nach unten zum Abschnitt:

```text
Role Collections
```

Klicken Sie auf:

```text
Assign Role Collection
```

Suchen Sie nach folgenden Präfixen:

```text
APIPortal
```

und

```text
AuthGroup
```

Wählen Sie alle verfügbaren Rollensammlungen mit diesen Präfixen aus.

Klicken Sie auf:

```text
Assign Role Collection
```

### Ergebnis

Die erforderlichen Berechtigungen für API Management und Developer Hub wurden vergeben.

> Hinweis:
> Schließen Sie anschließend den Browser oder leeren Sie den Browser-Cache, damit die neuen Berechtigungen übernommen werden.

---

## 3. Developer Hub aktivieren

Wechseln Sie zurück zur SAP Integration Suite.

Navigieren Sie zu:

```text
Settings
→ Runtimes
```

Klicken Sie auf:

```text
Activate
```

> Hinweis:
> Die Aktivierung dauert in der Regel etwa zwei Minuten.

Nach Abschluss der Aktivierung werden Sie automatisch abgemeldet.

Melden Sie sich erneut an.

Öffnen Sie anschließend über das Kachel-Symbol:

```text
Developer Hub
```

> Falls der Developer Hub nicht angezeigt wird:
>
> - Browser schließen
> - Cache leeren
> - Erneut anmelden

### Ergebnis

Der Developer Hub ist aktiviert und einsatzbereit.

---

## 4. API Provider anlegen

Navigieren Sie zu:

```text
Configure
→ APIs
```

Wechseln Sie in den Reiter:

```text
API Providers
```

Klicken Sie auf:

```text
Create
```

### API Provider

| Eigenschaft | Wert |
|------------|------|
| Name | Northwind_ODATAV4 |

### Connection

| Einstellung | Wert |
|------------|------|
| Type | Internet |
| Host | services.odata.org |
| Port | 443 |
| Use SSL | ✅ |

### Catalog Service Settings

| Einstellung | Wert |
|------------|------|
| Path Prefix | /V4/Northwind/Northwind.svc |
| Service Collection URL | / |
| Authentication Type | None |

Klicken Sie auf:

```text
Save
```

### Ergebnis

Der API Provider wurde erfolgreich angelegt.

---

## 5. API Proxy anlegen

Navigieren Sie zu:

```text
Configure
→ APIs
```

Wechseln Sie in den Reiter:

```text
API Proxies
```

Klicken Sie auf:

```text
Create
```

### API Proxy

| Eigenschaft | Wert |
|------------|------|
| API Provider | Northwind_ODATAV4 |
| URL | /V4/Northwind/Northwind.svc/ |
| Name | Northwind |
| Title | Northwind |
| API Base Path | /northwind |

Klicken Sie auf:

```text
Save
```

Anschließend:

```text
Deploy
```

### Testen

Der API Proxy kann getestet werden über:

```text
Test
→ APIs
```

### Ergebnis

Die Northwind API wird über API Management bereitgestellt.

---

## 6. API Produkt anlegen

Navigieren Sie zu:

```text
Engage
```

Klicken Sie auf:

```text
Create
```

### Produkt

| Eigenschaft | Wert |
|------------|------|
| Name | Northwind |
| Title | Northwind APIs |

Wechseln Sie anschließend in den Reiter:

```text
APIs
```

Klicken Sie auf:

```text
Add
```

Wählen Sie aus:

```text
Northwind
```

Bestätigen Sie mit:

```text
Add
```

Veröffentlichen Sie das Produkt:

```text
Publish
```

### Ergebnis

Das API Produkt wurde erfolgreich veröffentlicht.

---

## 7. Produkt im Developer Hub testen

Wechseln Sie in den:

```text
Developer Hub
```

Öffnen Sie das Produkt:

```text
Northwind APIs
```

Wechseln Sie in den Reiter:

```text
APIs
```

Klicken Sie auf:

```text
Northwind
```

Öffnen Sie anschließend:

```text
API Reference
```

### Ergebnis

Die API-Dokumentation ist verfügbar und die API kann direkt über den Developer Hub getestet werden.

---

## Entwicklerzugriff vergeben

Damit ein Entwickler den Developer Hub nutzen kann, muss dieser als Benutzer im SAP BTP Cockpit angelegt werden.

Navigieren Sie zu:

```text
Security
→ Users
```

Öffnen Sie den entsprechenden Benutzer und weisen Sie folgende Role Collection zu:

```text
AuthGroup.API.ApplicationDeveloper
```

### Ergebnis

Der Benutzer kann auf den Developer Hub zugreifen und veröffentlichte APIs testen.

---

# 🎯 Lernziele

Nach Abschluss dieser Übung können Sie:

- [ ] API Management aktivieren
- [ ] Developer Hub bereitstellen
- [ ] Benötigte Berechtigungen vergeben
- [ ] API Provider konfigurieren
- [ ] API Proxies erstellen und deployen
- [ ] API Produkte veröffentlichen
- [ ] APIs über den Developer Hub testen
- [ ] Entwickler für den Developer Hub berechtigen

Herzlichen Glückwunsch! Sie haben den vollständigen Lebenszyklus einer API in SAP Integration Suite API Management umgesetzt.
