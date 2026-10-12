# API-Funktion: Benutzer abrufen

## Beschreibung und Nutzen

Die Funktion ruft die Informationen eines Benutzers anhand seiner eindeutigen ID ab. Sie ermöglicht es dem Client, Benutzerdaten abzurufen und beispielsweise in einer Detailansicht darzustellen.

## Endpoint

- **Methode:** `GET`
- **Endpoint:** `/api/v1/users/{userId}`
- **Authentifizierung:** Erfordert ein gültiges Access Token.

## Request-Payload

Es wird kein Request-Body benötigt. Die Benutzer-ID wird als URL-Pfadparameter übergeben.

| Parameter | Typ | Pflicht | Beschreibung |
|---|---|---|---|
| `userId` | String | Ja | Eindeutige ID des Benutzers |

**Beispielaufruf:**

```http
GET /api/v1/users/12345
Authorization: Bearer <access_token>
```

## Response bei Erfolg

**HTTP-Status:** `200 OK`

```json
{
  "id": "12345",
  "name": "Max Mustermann",
  "email": "max@example.com"
}
```

**Verarbeitung im Client:**

- Die Response validieren und die Benutzerdaten auslesen.
- Die Daten in der Benutzeroberfläche darstellen oder weiterverarbeiten.

## Response bei Misserfolg

| HTTP-Status | Bedeutung | Verhalten im Client |
|---|---|---|
| `400 Bad Request` | Ungültige Anfrage | Eingabe prüfen und korrigieren |
| `401 Unauthorized` | Authentifizierung fehlt oder ist ungültig | Anmeldung erneuern oder Benutzer zur Anmeldung auffordern |
| `404 Not Found` | Benutzer nicht gefunden | Hinweis anzeigen und gegebenenfalls zur Übersicht zurückkehren |
| `429 Too Many Requests` | Zu viele Anfragen | Anfrage verzögert erneut versuchen |
| `500 Internal Server Error` | Interner Serverfehler | Fehler anzeigen und erneuten Versuch ermöglichen |

**Beispiel einer Fehler-Response:**

```json
{
  "error": {
    "code": "USER_NOT_FOUND",
    "message": "Der angeforderte Benutzer wurde nicht gefunden."
  }
}
```

## Hinweise zur Fehlerbehandlung

Der Client muss den HTTP-Statuscode prüfen und zwischen fachlichen Fehlern, Authentifizierungsproblemen und technischen Fehlern unterscheiden. Fehlermeldungen dürfen nicht ungeprüft als technische Details an Endnutzer weitergegeben werden. Automatische Wiederholungen sollten nur bei geeigneten Fehlern und mit angemessener Verzögerung erfolgen.

---

> **Hinweis:** Dies ist ein fiktives API-Beispiel. Die tatsächlichen Endpoints, Payloads und Fehlercodes müssen der Implementierung deiner API entsprechen.
