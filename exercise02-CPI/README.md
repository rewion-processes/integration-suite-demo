# Guide: SAP Integration Suite Hands-on

## 1. Use Case & Postman

### Ziel

Ein HTTP-Request wird aus Postman an einen SAP Integration Suite iFlow gesendet und anschließend an einen Beeceptor Mock Server weitergeleitet.

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

Öffnen Sie die Beeceptor Website und erstellen Sie einen neuen Mock Server.

### Beeceptor Servername

```text
test-gfu-#
```

Kopieren Sie den erzeugten Beeceptor-Link.

Öffnen Sie den iFlow und klicken Sie auf:
