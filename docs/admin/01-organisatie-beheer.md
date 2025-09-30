# Organisatie Beheer - Administrator Handleiding

**Doelgroep**: Hoofdbeheerder/Eigenaar van SafeWork Pro  
**Versie**: 1.0.0  
**Laatste Update**: 30 september 2025

## 🎯 Doel van deze Handleiding

Deze handleiding laat zien hoe je als hoofdbeheerder organisaties kunt aanmaken, beheren en configureren in SafeWork Pro.

## 📋 Vereisten

- Toegang tot Firebase Console
- Admin rechten in de applicatie
- Basis kennis van Firestore database
- Toegang tot de web applicatie

## 🏢 Organisatie Structuur

SafeWork Pro gebruikt een multi-tenant architectuur waarbij elke organisatie volledig geïsoleerd is:

```
organizations/
├── {organizationId}/
    ├── id: string
    ├── name: string
    ├── slug: string (uniek)
    ├── settings: object
    ├── subscription: object
    ├── createdAt: timestamp
    └── createdBy: string (userId)
```

## 1️⃣ Nieuwe Organisatie Aanmaken

### Via API (Aanbevolen)

```bash
# POST naar /api/organizations
curl -X POST https://safeworkpro.com/api/organizations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_FIREBASE_TOKEN" \
  -d '{
    "name": "Bouwbedrijf Van der Berg",
    "slug": "bouwbedrijf-vd-berg",
    "settings": {
      "industry": "construction",
      "complianceFramework": "vca",
      "timeZone": "Europe/Amsterdam",
      "language": "nl"
    }
  }'
```

### Via Firebase Console (Manual)

1. **Open Firebase Console**
   - Ga naar [Firebase Console](https://console.firebase.google.com)
   - Select project `hale-ripsaw-403915`

2. **Navigate naar Firestore Database**
   - Klik op "Firestore Database" in het menu
   - Zorg dat je in "Data" tab bent

3. **Maak nieuwe organisatie aan**
   - Klik op "Start collection"
   - Collection ID: `organizations`
   - Document ID: Genereer automatisch of gebruik UUID

4. **Voeg organisatie data toe**:
```json
{
  "id": "generated-uuid-here",
  "name": "Bouwbedrijf Van der Berg",
  "slug": "bouwbedrijf-vd-berg",
  "settings": {
    "industry": "construction",
    "complianceFramework": "vca",
    "timeZone": "Europe/Amsterdam",
    "language": "nl"
  },
  "subscription": {
    "tier": "trial",
    "status": "active",
    "trialEndsAt": "2025-10-15T00:00:00Z"
  },
  "createdAt": "2025-09-30T17:00:00Z",
  "createdBy": "admin-user-id"
}
```

## 2️⃣ Organisatie Instellingen

### Basis Instellingen

| Setting | Beschrijving | Opties |
|---------|-------------|--------|
| `name` | Officiële bedrijfsnaam | Tekst (2-100 karakters) |
| `slug` | URL-vriendelijke naam (uniek) | lowercase, nummers, koppeltekens |
| `industry` | Industrie sector | construction, industrial, offshore, etc. |
| `complianceFramework` | Compliance standaard | vca, iso45001, both |
| `timeZone` | Tijdzone | Europe/Amsterdam, Europe/London, etc. |
| `language` | Interface taal | nl, en |

### Subscription Instellingen

| Setting | Beschrijving | Opties |
|---------|-------------|--------|
| `tier` | Abonnement type | trial, starter, professional, enterprise |
| `status` | Account status | active, suspended, cancelled |
| `trialEndsAt` | Trial einde datum | ISO 8601 timestamp |
| `maxUsers` | Maximum gebruikers | Nummer (gebaseerd op tier) |
| `maxProjects` | Maximum projecten | Nummer (gebaseerd op tier) |

## 3️⃣ Organisatie Beheren

### Organisatie Details Opvragen

```bash
# GET /api/organizations/{organizationId}
curl -X GET https://safeworkpro.com/api/organizations/org-uuid \
  -H "Authorization: Bearer YOUR_FIREBASE_TOKEN"
```

### Organisatie Bijwerken

```bash
# PATCH /api/organizations/{organizationId}
curl -X PATCH https://safeworkpro.com/api/organizations/org-uuid \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_FIREBASE_TOKEN" \
  -d '{
    "settings": {
      "complianceFramework": "both",
      "maxUsers": 50
    }
  }'
```

### Organisatie Deactiveren

```bash
# PATCH subscription status
curl -X PATCH https://safeworkpro.com/api/organizations/org-uuid \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_FIREBASE_TOKEN" \
  -d '{
    "subscription": {
      "status": "suspended"
    }
  }'
```

## 4️⃣ Organisatie Statistieken

### Gebruikers per Organisatie

```javascript
// Firebase Console > Firestore > Query
// Collection: users
// Where: organizationId == "org-uuid"
```

### Projecten per Organisatie

```javascript
// Collection: organizations/{orgId}/projects
// Count documents
```

### TRAs per Organisatie

```javascript
// Collection: organizations/{orgId}/tras
// Group by status: draft, review, approved, active
```

## 5️⃣ Troubleshooting

### Probleem: Organisatie slug al in gebruik

**Symptoom**: Error bij aanmaken nieuwe organisatie
```json
{
  "error": {
    "code": "RESOURCE_ALREADY_EXISTS",
    "message": "Organization with identifier 'slug' already exists"
  }
}
```

**Oplossing**: 
1. Kies een andere slug
2. Check bestaande slugs in Firestore:
```javascript
// Query: organizations where slug == "gewenste-slug"
```

### Probleem: Gebruiker kan niet inloggen na organisatie wijziging

**Symptoom**: "Organization mismatch" error

**Oplossing**:
1. Check custom claims van gebruiker:
```bash
# Firebase Admin SDK
admin.auth().getUser(uid).then(user => {
  console.log(user.customClaims);
});
```

2. Update custom claims:
```bash
curl -X POST https://safeworkpro.com/api/auth/set-claims \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ADMIN_TOKEN" \
  -d '{
    "targetUserId": "user-uid",
    "organizationId": "correct-org-id",
    "role": "admin"
  }'
```

## 6️⃣ Best Practices

### Organisatie Naamgeving
- Gebruik duidelijke, professionele namen
- Vermijd speciale karakters in slug
- Houd slugs kort maar beschrijvend

### Data Beheer
- Maak regelmatig backups van organisatie data
- Monitor subscription status en trial einddatums
- Houd gebruiker counts bij voor facturering

### Security
- Controleer regelmatig gebruiker rollen per organisatie
- Review admin toegang per kwartaal
- Monitor voor ongebruikelijke activiteit

## 📚 Gerelateerde Documentatie

- [Gebruiker Beheer](02-gebruiker-beheer.md)
- [Data Manipulatie](03-data-manipulatie.md)
- [API Endpoints Guide](../backend/01-api-endpoints-guide.md)
- [Firebase Admin Guide](../backend/02-firebase-admin-guide.md)

---

**Volgende Stap**: Lees [Gebruiker Beheer](02-gebruiker-beheer.md) voor het beheren van gebruikers binnen organisaties.