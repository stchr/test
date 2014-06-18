# API-Design und -Standards

## Einleitung

Um eine nachhaltige und erweiterbare Schnittstelle zu bekommen, sollen folgende Regeln eingehalten werden.

### RESTful

- Eine URL identifiziert eine Ressource
- URLs sollten Nomen enthalten, keine Verben
- Ressourcen werden im Plural verwendet
- HTTP-Verben benutzen, um Operationen mit Sammlungen und Elementen von Ressourcen durchzuführen:
-- **GET**: lesen
-- **POST**: erstellen
-- **PUT**: bearbeiten
-- **DELETE**: löschen
- Es sollte nicht tiefer als **resources/id/resources** gegangen werden
- Lässt es sich nicht vermeiden, Operationen in die URL mit aufzunehmen, weil passende HTTP-Verben fehlen, sind diese unter dem Slug **actions** zu sammeln
- Immer eine Versionsnummer beifügen

### Stateless

Jede Anfrage steht für sich alleine, es gibt keine Sessions.
Deshalb muss jede Anfrage Auth etc. erneut machen.

### Versionierung

Die API ist versioniert und innerhalb einer Version auch bei nachträglichen Änderungen komplett rückwärtskompatibel.
Die Version ist eine Ganzzahl mit vorangestelltem v: v1, v2 etc.

### Service-URL

http://rfr.example.com/api/v1/

### Datenformat/Codierung

- UTF8
- JSON-only

### Authentifizeirung/Identifizierung/Lizensierung

Um ein einfaches, aber gleichzeitig sicheres SSO zu realisieren, funktioniert die Authentifizierung folgendermaßen:

- Für jeden Client existiert eine eindeutige ID, welche in der Lizenz-Datei mit einer maximalen Anzahl angegeben wird
- Jeder Client muss den RFR-Nutzer anhand des Nutzernamens als HTTP-Basic-Auth ohne Passwort übermitteln
- Authentifizierung: HTTP-Basic-Auth
-- User: RFR-Benutzername
-- Passwort: UUID für Kombination aus Benutzername und User-Agent (mit Salt), generiert vom Client
- Jeder Client-ID wird über den **User-Agent**-Header übermittelt
- API prüft, ob für die Kombination von User und Client eine Lizenz existiert (Und User existiert, nicht gelöscht etc.). Wenn nicht:
-- automatische Freischaltung oder Benachrichtigung des Admins über Freigabeersuch (hier 401er Status)
- Freischaltung bedeutet: Eintragung der UUID + Client in Lizenz-Tabelle für User
- Keine Freischaltung möglich, wenn max. Lizenz-Anzahl erreicht ist

Es können auch Lizenzen für eigene Kunden-Clients (= kein User-Agent) definiert werden. Diese Lizenzen können für beliebig viele Clients eingesetzt werden.

ACHTUNG: Die Lizenzen sind KEINE CC-Lizenzen, da die API stateless ist!

### Status-Codes

Folgende HTTP-Status-Codes werden als Info zu der Verarbeitung eines Requests zurückgegeben:

- **200 OK**: Erfolgreicher Request für GET, PATCH/PUT
- **201 Created**: Erfolgreicher Request für POST
- **204 No Content**: Erfolgreicher DELETE
- **304 Not Modified**: Angeforderte Ressource wurde nicht geändert, gecachte Version kann benutzt werden
- **400 Bad Request**: Fehlerhafter Aufbau des Requests (Sollte nach Möglichkeit genauer mit entsprechendem 4xx-Code spezifiziert werden)
- **401 Unauthorized**: Keine gültige Authentifizeierung oder ausstehende Freigabe durch Admin
- **500 Internal Server Error**: Allgemeiner unerwarteter Fehler (Sollte nach Möglichkeit genauer mit entsprechendem 5xx-Code spezifiziert werden)

### HTTP-Caching

**ETag**- oder **Last-Modified**-Header mitliefern, welche beim nächsten Request als **If-None-Match**-, bzw. **If-Modified-Since**-Header mitgeliefert werden können.

Spart auf beiden Seiten (Server und Client) Zeit und Bandbreite.

### Error-Handling

Es wird ein möglichst sinnvoller HTTP-Status-Code aus dem 4xx- oder 5xx-Bereich zurückgegeben.
Dabei werden im Response-Body folgende JSON-Felder zurückgegeben: 

- **id**: Maschinenlesbare Fehler-ID (z.B. „not_found“)
- **message**: Lesbare Fehlermeldung (z.B. „Das gewünschte Element konnte nicht gefunden werden.“)

### Paginierung und Sortierung

Es werden immer max. 50 Elemente geliefert. Es kann aber mit den GET-Parametern **limit** und **offset** der gewünschte Ergebnisbereich eingegrenzt werden.

Oder: https://devcenter.heroku.com/articles/platform-api-reference#ranges

### CORS

`Access-Control-Allow-Origin: *` ist für die API immer für die benötigten HTTP-Methoden (HEAD, OPTIONS, GET, PUT; POST, DELETE) und HTTP-Header (User-Agent etc.) aktiviert, um Cross-Domain-Kommunikation zu ermöglichen

### Request-Id

Um ein Debugging durchführen zu können, immer eine eindeutige **Request-Id** als Response-Header mit schicken. Dieser kann von Client und Server geloggt werden.

### Ressourcen und Attribute

- Immer englische Schreibweise benutzen
- Resourcen klein schreiben, trennen mit Divis (-) (z.B. time-roles)
- Attribute ebenfall klein schreiben, trennen mit Underscorde (z.B. created_at)
- Keine Werte als Schlüssel
- Identifizierer: id
- Möglichst immer created_at und updated_at beifügen
- Zeiten immer in UTC nach ISO8601
- FK-Beziehungen als geschachtelte Elemente zurück liefern { „id“: 1234“, „name“: “test“, „owner“: { „id“: 5678, „name“: „hans“ } }

## Administrators
Arbeiten mit RFR-Admins

### Attributes
<table>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
  <tr>
    <td><strong>department</strong></td>
    <td><em>string</em></td>
    <td>Department (Abteilung)</td>
    <td><code>"HR"</code></td>
  </tr>
  <tr>
    <td><strong>email</strong></td>
    <td><em>email</em></td>
    <td>E mail</td>
    <td><code>"j.doe@example.com"</code></td>
  </tr>
  <tr>
    <td><strong>id</strong></td>
    <td><em>integer</em></td>
    <td>unique identifier of admin</td>
    <td><code>"1234"</code></td>
  </tr>
  <tr>
    <td><strong>name</strong></td>
    <td><em>string</em></td>
    <td>Full name</td>
    <td><code>"John Doe"</code></td>
  </tr>
  <tr>
    <td><strong>username</strong></td>
    <td><em>string</em></td>
    <td>Unique Username</td>
    <td><code>"JDoe"</code></td>
  </tr>
</table>

### Administrators Create
Create a new admin.

```
POST /admins
```


#### Curl Example
```term
$ curl -n -X POST https://rfr.example.com/api/v1234/admins
```

#### Response Example
```
HTTP/1.1 201 Created
```
```javascript```
{
  "id": "1234",
  "name": "John Doe",
  "email": "j.doe@example.com",
  "department": "HR",
  "username": "JDoe"
}
```
### Administrators Delete
Delete an existing admin.

```
DELETE /admins/{admin_id}
```


#### Curl Example
```term
$ curl -n -X DELETE https://rfr.example.com/api/v1234/admins/$ADMIN_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "id": "1234",
  "name": "John Doe",
  "email": "j.doe@example.com",
  "department": "HR",
  "username": "JDoe"
}
```
### Administrators Info
Info for existing admin.

```
GET /admins/{admin_id}
```


#### Curl Example
```term
$ curl -n -X GET https://rfr.example.com/api/v1234/admins/$ADMIN_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "id": "1234",
  "name": "John Doe",
  "email": "j.doe@example.com",
  "department": "HR",
  "username": "JDoe"
}
```
### Administrators List
List existing admins.

```
GET /admins
```


#### Curl Example
```term
$ curl -n -X GET https://rfr.example.com/api/v1234/admins
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
[
  {
    "id": "1234",
    "name": "John Doe",
    "email": "j.doe@example.com",
    "department": "HR",
    "username": "JDoe"
  }
]
```
### Administrators Update
Update an existing admin.

```
PUT /admins/{admin_id}
```


#### Curl Example
```term
$ curl -n -X PUT https://rfr.example.com/api/v1234/admins/$ADMIN_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "id": "1234",
  "name": "John Doe",
  "email": "j.doe@example.com",
  "department": "HR",
  "username": "JDoe"
}
```


