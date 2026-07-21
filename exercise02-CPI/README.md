# Guide: SAP Integration Suite Hands-on

## 1. Use Case & Postman

### Ziel

Ein HTTP-Request wird aus Postman an einen SAP Integration Suite iFlow gesendet und anschließend an einen Beeceptor Mock Server weitergeleitet.

<img width="1568" height="519" alt="image" src="https://github.com/user-attachments/assets/d3ff209e-a539-47b7-928f-97824d779052" />


### Postman Login

Melden Sie sich bei Postman an:

[Postman Login](https://identity.getpostman.com/login)

---

## 2. Package und iFlow anlegen

Navigieren Sie in der SAP Integration Suite zu:

```text
Design
→ Integrations and APIs
```

Klicken Sie auf:

```text
Create
```

### Package anlegen

| Eigenschaft | Wert |
|------------|------|
| Name | PM_to_Beeceptor |
| Short Description | Postman to Beeceptor Integrations |

Wechseln Sie anschließend auf den Reiter:

```text
Artifacts
```

Erstellen Sie einen neuen Integration Flow:

```text
Add
→ Integration Flow
```

### Integration Flow

| Eigenschaft | Wert |
|------------|------|
| Name | PM_to_Beeceptor_Employees |

---

## 3. Receiver konfigurieren

Öffnen Sie die [Beeceptor Website](https://beeceptor.com/) und erstellen Sie einen neuen Mock Server.

### Beeceptor Servername

```text
test-gfu-#
```

Kopieren Sie den erzeugten Beeceptor-Link.

Öffnen Sie den iFlow und klicken Sie auf:

```text
Edit
```

Ziehen Sie vom **Message End** eine Verbindung zu einem neuen **Receiver**.

<img width="1023" height="471" alt="image" src="https://github.com/user-attachments/assets/827529c8-4e59-4f10-954f-b1588c439100" />


### Receiver Adapter

| Einstellung | Wert |
|------------|------|
| Adapter Type | HTTP |

### Connection

| Einstellung | Wert |
|------------|------|
| Address | Beeceptor-Link |
| Proxy Type | Internet |
| Method | POST |
| Authentication | None |

Speichern Sie die Einstellungen.

---

## 4. Sender konfigurieren

Ziehen Sie vom **Sender** eine Verbindung zum **Message Start Event**.

<img width="1023" height="360" alt="image" src="https://github.com/user-attachments/assets/1f81f5e4-6c73-4fb8-94f2-c0fa53b22c42" />



### Sender Adapter

| Einstellung | Wert |
|------------|------|
| Adapter Type | HTTPS |

### Connection

| Einstellung | Wert |
|------------|------|
| Address | /send-employees |
| Authorization | User Role |
| User Role | ESBMessaging.send |

Deaktivieren Sie für diese Übung:

```text
CSRF Protection
```

> Hinweis:
> In produktiven Systemen sollte die CSRF Protection aktiviert bleiben.

Speichern Sie den iFlow und führen Sie anschließend ein Deployment durch.

```text
Save
→ Deploy
```

---

## 5. Sender Credentials anlegen

Navigieren Sie im SAP BTP Cockpit zu:

```text
Services
→ Instances and Subscriptions
```

Erstellen Sie eine neue Service Instanz: 
<img width="830" height="714" alt="image" src="https://github.com/user-attachments/assets/0772fc72-031c-477d-bd33-f7cb3ed4e55e" />


Öffnen Sie die Instanz und wechseln Sie zu:

```text
Service Keys
```

Klicken Sie auf:

```text
Create
```
Erstellen Sie den Service Key wie folgt: 

<img width="627" height="665" alt="image" src="https://github.com/user-attachments/assets/afad1ca7-0a35-4f13-8c2c-ebdef92af820" />


Laden Sie anschließend den erzeugten Service Key herunter oder kopieren Sie sich die Werte aus dem Service Key JSON.
Die folgenden Werte werden später in Postman verwendet:

- Client ID
- Client Secret
- Token URL

---

## 6. Postman konfigurieren

Navigieren Sie in der Integration Suite zu:

```text
Monitor
→ Integrations and APIs
→ Manage Integration Content
→ Started
```

Wählen Sie Ihren iFlow aus und kopieren Sie den **Endpoint** (Struktur: https://<<your-environment>>.hana.ondemand.com/http/send-employees)

### Environment und Collection anlegen

Importieren Sie die Collection und das Environment aus dem Ordner [Samples](samples): 

[Postman Collection](samples/Trial_Integration_Suite.postman_collection.json)

[Postman Environment](samples/Trial_Integration_Suite.postman_environment.json)

<img width="1276" height="401" alt="image" src="https://github.com/user-attachments/assets/9c19738b-14ae-48ff-8b4b-215d04422513" />



Pflegen Sie folgende Variablen im Environment "Trial Integration Suite":

| Variable | Wert |
|----------|------|
| Host | Endpoint bis /http |
| Endpoint | Endpoint ab /http |
| ClientId | aus Service Key |
| ClientSecret | aus Service Key |
| Tokenurl | aus Service Key |

Speichern Sie das Environment:

```text
STRG + S
```

---

## 7. Technischen Durchstich testen

Öffnen Sie in Postman:

```text
Collections
→ Deep Dive BTP
→ Send Employees
```

Wählen Sie das Environment:

```text
Integration Suite
```

### OAuth Token beziehen

Navigieren Sie zu:

```text
Authorization
→ Get New Access Token
```

Anschließend:

```text
Proceed
```

und anschließend:

```text
Use Token
```

### Test ausführen

Klicken Sie auf:

```text
Send
```

### Ergebnis

Prüfen Sie im Beeceptor Tab, ob die Nachricht erfolgreich angekommen ist.

✅ Technischer End-to-End Durchstich erfolgreich

---

# Optionale Erweiterungen

## 8. JSON zu XML Converter hinzufügen

Fügen Sie im iFlow folgenden Schritt hinzu:

```text
Transformation
→ Converter
→ JSON to XML Converter
```

Platzieren Sie den Converter möglichst nahe am Start Event.

Anschließend:

```text
Save
→ Deploy
```

Senden Sie die Nachricht erneut aus Postman.

### Optional

Fügen Sie zusätzlich einen Converter hinzu:

```text
XML to CSV Converter
```

Platzieren Sie diesen möglichst nahe am End Event.

---

## 9. Message Mapping

Fügen Sie im iFlow hinzu:

```text
Mapping
→ Message Mapping
```

> Wichtig:
> Das Message Mapping muss hinter dem JSON-to-XML Converter platziert werden.

### Mapping erstellen

| Eigenschaft | Wert |
|------------|------|
| Name | pm_to_bc_employee |

### Source Message

```text
Pm_employee.xsd
```

### Target Message

```text
Bc_employee.xsd
```

Verbinden Sie die Felder per Drag & Drop.

### FullName erzeugen

Der Zielwert **FullName** soll aus folgenden Feldern zusammengesetzt werden:

```text
EmployeeFirstname
+
Leerzeichen
+
EmployeeLastname
```

Anschließend:

```text
Save
→ Deploy
```

Testen Sie den Flow erneut mit Postman.

---

## 10. Groovy Script hinzufügen

Fügen Sie einen Groovy Script Schritt in den iFlow ein.

Positionieren Sie das Script nach den Convertern.

Klicken Sie auf:

```text
Create
```

Verwenden Sie folgendes Script:

```groovy
import com.sap.gateway.ip.core.customdev.util.Message;

def Message processData(Message message) {    
    
    def body = message.getBody(String)
    def lines = body.split("\\r?\\n")
    def newBody = lines.collect { line ->
        line + ";ACTIVE"
    }.join("\n")

    message.setBody(newBody)

    message.setHeader("TrainingHeader", "SAP Integration Suite Demo")
    message.setHeader("Content-Type", "text/csv; charset=UTF-8")

    return message
}
```

Anschließend:

```text
Apply
→ Close
→ Save
→ Deploy
```

---

## 11. Data Store verwenden

Fügen Sie im iFlow folgende Komponente hinzu:

```text
Persistence
→ Data Store Operations
→ Write
```

Platzieren Sie diese direkt nach dem Start Event.

### Konfiguration

| Einstellung | Wert |
|------------|------|
| Data Store Name | New_Data_Store |
| Validity | Integration Flow |
| Entry ID | EmployeeList |

Anschließend:

```text
Save
→ Deploy
```

### Ergebnis

Bei jedem erfolgreichen Aufruf des iFlows wird ein Eintrag im Data Store angelegt.

---

# 🎯 Lernziele

Nach Abschluss dieser Übung können Sie:

- [ ] HTTP-Endpunkte in einem iFlow bereitstellen
- [ ] Postman mit OAuth authentifizieren
- [ ] Nachrichten an externe Systeme senden
- [ ] JSON in XML konvertieren
- [ ] Message Mappings erstellen
- [ ] Groovy Scripts einsetzen
- [ ] Daten im Data Store persistieren
- [ ] Nachrichtenflüsse überwachen und testen

Herzlichen Glückwunsch! Sie haben einen vollständigen End-to-End Integrationsprozess mit der SAP Integration Suite umgesetzt.
