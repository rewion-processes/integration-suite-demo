# SAP Integration Suite Training

## 🚀 Übersicht

Willkommen zum Rewion SAP Integration Suite Training.

In diesem praxisorientierten Training lernen Sie die wichtigsten Komponenten der SAP Integration Suite kennen und erstellen Ihre ersten Integrationsszenarien auf der SAP Business Technology Platform (SAP BTP).

Nach Abschluss dieses Trainings verfügen Sie über:

- Einen persönlichen SAP BTP Trial Account
- Zugriff auf die SAP Integration Suite
- Ihren ersten Integration Flow (iFlow)
- Erste Erfahrungen mit Monitoring und Fehlersuche
- Grundlagen für API Management und Event Mesh

---

# Schritt 1: SAP BTP Trial Account erstellen

Die SAP Integration Suite läuft auf der SAP Business Technology Platform (SAP BTP).

Falls Sie noch keinen SAP BTP Trial Account besitzen, erstellen Sie diesen zunächst.

## Trial Account anlegen

1. Öffnen Sie die SAP BTP Trial Registrierungsseite.
2. Registrieren Sie sich mit Ihrer E-Mail-Adresse.
3. Bestätigen Sie Ihre E-Mail-Adresse.
4. Melden Sie sich im SAP BTP Cockpit an.

### Ergebnis

Sie haben nun Zugriff auf:

- Global Account
- Trial Subaccount
- Cloud Foundry Umgebung

---

# Schritt 2: Trial Subaccount prüfen

Nach der Anmeldung:

1. Öffnen Sie Ihren Trial Subaccount.
2. Navigieren Sie zu **Entitlements**.
3. Stellen Sie sicher, dass die Cloud Foundry Runtime verfügbar ist.

# Schritt 3: SAP Integration Suite abonnieren

Navigieren Sie zu:

```text
Services
→ Service Marketplace
```


Suchen Sie nach:

```text
Integration Suite
```

Öffnen Sie den Service und wählen Sie:

```text
Create
```
<img width="574" height="494" alt="image" src="https://github.com/user-attachments/assets/7d360450-b418-406a-860d-b0c97b763032" />


Warten Sie, bis die Subscription erfolgreich angelegt wurde.

---

# Schritt 4: Rolle Integration_Provisioner zuweisen

Bevor die SAP Integration Suite verwendet werden kann, muss Ihrem Benutzer die erforderliche Role Collection zugewiesen werden.

Navigieren Sie im SAP BTP Cockpit zu:

```text
Security
→ Users
```

Suchen Sie Ihren Benutzer und wählen Sie diesen durch Klick auf die entsprechende Zeile aus.

Im rechten Bereich:

1. Scrollen Sie nach unten bis zum Abschnitt **Role Collections**
2. Klicken Sie auf **Assign Role Collection**
   - Falls die Schaltfläche nicht sichtbar ist, klicken Sie auf **...**
3. Suchen Sie nach:

```text
Integration
```

4. Wählen Sie folgende Role Collection aus:

```text
Integration_Provisioner
```

5. Klicken Sie auf:

```text
Assign Role Collection
```

> Hinweis:
> Es kann einige Minuten dauern, bis die neue Berechtigung wirksam wird.

---

# Schritt 5: SAP Integration Suite öffnen

Navigieren Sie zu:

```text
Instances and Subscriptions
```

Öffnen Sie:

```text
Integration Suite
```

Klicken Sie auf:

```text
Go to Application
```

---

# Schritt 6: Funktionen aktivieren

Klicken sie auf der Startseite auf das Feld:

```text
Manage Capabilities
```
<img width="939" height="406" alt="image" src="https://github.com/user-attachments/assets/8e4abff9-6cc5-4fca-a046-f4bbd82185ec" />

Aktivieren Sie:

✅ Cloud Integration

✅ API Management

Klicken Sie anschließend auf **Activate**.


---

Nach Abschluss dieses Setups verfügen Sie über:

- Eine vollständig eingerichtete SAP BTP Trial Umgebung
- Zugriff auf die SAP Integration Suite
- Einen lauffähigen Cloud Integration Tenant
- Die Grundlage für alle weiteren Übungen im Rewion SAP Integration Suite Training

Sie sind nun bereit für die nächsten Hands-on-Übungen!
