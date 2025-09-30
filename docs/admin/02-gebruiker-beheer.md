# Gebruiker Beheer - Administrator Handleiding

**Doelgroep**: Hoofdbeheerder/Eigenaar van SafeWork Pro  
**Versie**: 1.0.0  
**Laatste Update**: 30 september 2025

## 🎯 Doel van deze Handleiding

Deze handleiding laat zien hoe je als hoofdbeheerder gebruikers kunt aanmaken, beheren, rollen toewijzen en troubleshooten binnen SafeWork Pro.

## 📋 Vereisten

- Toegang tot Firebase Console
- Admin rechten in de applicatie
- Toegang tot Firebase Authentication
- Kennis van [Organisatie Beheer](01-organisatie-beheer.md)

## 👥 Gebruiker Rollen Systeem

SafeWork Pro heeft 4 hiërarchische rollen:

| Rol | Level | Beschrijving | Rechten |
|-----|--------|-------------|---------|
| **Admin** | 4 | Organisatie beheerder | Alle rechten, gebruiker beheer, organisatie instellingen |
| **Safety Manager** | 3 | Veiligheidsmanager | TRA goedkeuring, rapporten, team overzicht |
| **Supervisor** | 2 | Uitvoerder/Supervisor | TRA review, LMRA toewijzing, team coaching |
| **Field Worker** | 1 | Veldwerker | LMRA uitvoering, basis rapportage |

## 1️⃣ Nieuwe Gebruiker Toevoegen

### Via API (Aanbevolen)

```bash
# Stap 1: Gebruiker registreren
curl -X POST https://safeworkpro.com/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "jan.jansen@bouwbedrijf.nl",
    "password": "TempPassword123!",
    "firstName": "Jan",
    "lastName": "Jansen",
    "companyName": "Bouwbedrijf Van der Berg"
  }'

# Stap 2: Custom claims instellen
curl -X POST https://safeworkpro.com/api/auth/set-claims \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ADMIN_TOKEN" \
  -d '{
    "targetUserId": "nieuwe-user-uid",
    "organizationId": "org-uuid",
    "role": "supervisor"
  }'
```

### Via Firebase Console

1. **Firebase Authentication**
   - Ga naar Firebase Console > Authentication > Users
   - Klik "Add user"
   - Vul email en tijdelijk wachtwoord in

2. **Firestore User Profile**
   - Ga naar Firestore Database
   - Navigeer naar `users/{userId}`
   - Voeg user document toe:

```json
{
  "uid": "firebase-user-uid",
  "email": "jan.jansen@bouwbedrijf.nl",
  "firstName": "Jan",
  "lastName": "Jansen",
  "organizationId": "org-uuid-here",
  "role": "supervisor",
  "createdAt": "2025-09-30T17:00:00Z",
  "lastLoginAt": null,
  "emailVerified": false,
  "profileComplete": true
}
```

3. **Custom Claims Instellen**
   - Gebruik Firebase Admin SDK of API endpoint
   - Stel `orgId` en `role` custom claims in

## 2️⃣ Gebruiker Rollen Beheren

### Rol Wijzigen

```bash
# POST /api/auth/set-claims
curl -X POST https://safeworkpro.com/api/auth/set-claims \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ADMIN_TOKEN" \
  -d '{
    "targetUserId": "user-uid-hier",
    "organizationId": "org-uuid-hier", 
    "role": "safety_manager"
  }'
```

### Batch Rol Updates

Voor meerdere gebruikers tegelijk:

```javascript
// Firebase Admin SDK script
const users = [
  { uid: 'user1', role: 'supervisor' },
  { uid: 'user2', role: 'field_worker' },
  { uid: 'user3', role: 'safety_manager' }
];

for (const user of users) {
  await admin.auth().setCustomUserClaims(user.uid, {
    orgId: 'your-org-id',
    role: user.role
  });
  
  // Update Firestore profile
  await admin.firestore()
    .doc(`users/${user.uid}`)
    .update({ role: user.role });
}
```

### Rol Verificatie

```bash
# Check huidige custom claims
curl -X GET https://safeworkpro.com/api/auth/user/user-uid \
  -H "Authorization: Bearer ADMIN_TOKEN"
```

## 3️⃣ Gebruiker Status Beheer

### Gebruiker Deactiveren

```bash
# Firebase Admin SDK
admin.auth().updateUser(uid, {
  disabled: true
});

# Of via Firestore
admin.firestore().doc(`users/${uid}`).update({
  status: 'disabled',
  disabledAt: admin.firestore.FieldValue.serverTimestamp()
});
```

### Gebruiker Reactiveren

```bash
admin.auth().updateUser(uid, {
  disabled: false
});

admin.firestore().doc(`users/${uid}`).update({
  status: 'active',
  reactivatedAt: admin.firestore.FieldValue.serverTimestamp()
});
```

### Wachtwoord Reset Forceren

```bash
# Via Firebase Console of Admin SDK
admin.auth().generatePasswordResetLink(email)
  .then(link => {
    console.log('Reset link:', link);
    // Stuur link naar gebruiker
  });
```

## 4️⃣ Gebruiker Data Management

### Gebruiker Profile Updaten

```bash
# PATCH /api/users/{userId}
curl -X PATCH https://safeworkpro.com/api/users/user-uid \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ADMIN_TOKEN" \
  -d '{
    "firstName": "Jan-Willem",
    "lastName": "van der Jansen",
    "competencies": ["VCA", "Hoogwerker", "Hijskraan"]
  }'
```

### Gebruiker Verplaatsen naar Andere Organisatie

```bash
# Stap 1: Update Firestore profile
curl -X PATCH https://safeworkpro.com/api/users/user-uid \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ADMIN_TOKEN" \
  -d '{
    "organizationId": "nieuwe-org-uuid"
  }'

# Stap 2: Update custom claims
curl -X POST https://safeworkpro.com/api/auth/set-claims \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ADMIN_TOKEN" \
  -d '{
    "targetUserId": "user-uid",
    "organizationId": "nieuwe-org-uuid",
    "role": "field_worker"
  }'
```

## 5️⃣ Bulk Operaties

### Bulk Import Gebruikers

```javascript
// CSV import script
const users = [
  { email: 'user1@company.nl', firstName: 'Jan', lastName: 'A', role: 'field_worker' },
  { email: 'user2@company.nl', firstName: 'Piet', lastName: 'B', role: 'supervisor' },
  // ... meer gebruikers
];

for (const userData of users) {
  try {
    // 1. Create Firebase Auth user
    const userRecord = await admin.auth().createUser({
      email: userData.email,
      password: generateTempPassword(),
      emailVerified: false
    });

    // 2. Set custom claims
    await admin.auth().setCustomUserClaims(userRecord.uid, {
      orgId: YOUR_ORG_ID,
      role: userData.role
    });

    // 3. Create Firestore profile
    await admin.firestore().doc(`users/${userRecord.uid}`).set({
      uid: userRecord.uid,
      email: userData.email,
      firstName: userData.firstName,
      lastName: userData.lastName,
      organizationId: YOUR_ORG_ID,
      role: userData.role,
      createdAt: admin.firestore.FieldValue.serverTimestamp(),
      profileComplete: true
    });

    console.log(`✅ User created: ${userData.email}`);
  } catch (error) {
    console.error(`❌ Failed to create ${userData.email}:`, error);
  }
}
```

### Bulk Export Gebruikers

```javascript
// Export alle gebruikers van een organisatie
const users = await admin.firestore()
  .collection('users')
  .where('organizationId', '==', 'your-org-id')
  .get();

const userData = users.docs.map(doc => ({
  uid: doc.id,
  ...doc.data(),
  // Haal ook Firebase Auth data op
}));

// Export naar CSV of JSON
```

## 6️⃣ Monitoring & Analytics

### Actieve Gebruikers

```javascript
// Query laatste 30 dagen
const thirtyDaysAgo = new Date();
thirtyDaysAgo.setDate(thirtyDaysAgo.getDate() - 30);

const activeUsers = await admin.firestore()
  .collection('users')
  .where('organizationId', '==', 'your-org-id')
  .where('lastLoginAt', '>=', thirtyDaysAgo)
  .get();

console.log(`Actieve gebruikers: ${activeUsers.size}`);
```

### Rol Distributie

```javascript
const users = await admin.firestore()
  .collection('users')
  .where('organizationId', '==', 'your-org-id')
  .get();

const roleCount = {};
users.docs.forEach(doc => {
  const role = doc.data().role;
  roleCount[role] = (roleCount[role] || 0) + 1;
});

console.log('Rol distributie:', roleCount);
```

## 7️⃣ Troubleshooting

### Probleem: Gebruiker kan niet inloggen

**Diagnose stappen**:

1. **Check Firebase Auth status**:
```bash
# Firebase Console > Authentication > Users
# Zoek gebruiker op email
# Check: disabled status, email verified
```

2. **Check Custom Claims**:
```javascript
admin.auth().getUser(uid).then(user => {
  console.log('Custom Claims:', user.customClaims);
});
```

3. **Check Firestore Profile**:
```bash
# Firestore Console > users/{uid}
# Controleer: organizationId, role, status
```

### Probleem: "Insufficient Permissions" error

**Mogelijke oorzaken**:
- Custom claims niet juist ingesteld
- Rol te laag voor gevraagde actie  
- Organisatie mismatch

**Oplossing**:
```bash
# Herinstalleer custom claims
curl -X POST https://safeworkpro.com/api/auth/set-claims \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ADMIN_TOKEN" \
  -d '{
    "targetUserId": "problem-user-uid",
    "organizationId": "correct-org-id",
    "role": "appropriate-role"
  }'
```

### Probleem: Gebruiker ziet verkeerde organisatie data

**Diagnose**:
1. Check `organizationId` in user profile
2. Check `orgId` in custom claims
3. Controleer of beide overeenkomen

**Fix**:
```javascript
// Sync user profile with custom claims
const userDoc = await admin.firestore().doc(`users/${uid}`).get();
const userClaims = await admin.auth().getUser(uid);

if (userDoc.data().organizationId !== userClaims.customClaims?.orgId) {
  // Fix de mismatch
  await admin.auth().setCustomUserClaims(uid, {
    orgId: userDoc.data().organizationId,
    role: userDoc.data().role
  });
}
```

## 8️⃣ Best Practices

### Security
- Gebruik sterke tijdelijke wachtwoorden bij gebruiker aanmaak
- Forceer wachtwoord wijziging bij eerste login
- Review gebruiker rechten regelmatig (quarterly)
- Log alle admin acties

### Data Integriteit
- Houd custom claims en Firestore profile synchronized
- Maak backups voor bulk operaties
- Test rol wijzigingen in development eerst

### User Experience
- Stuur welkomst emails met instructies
- Provide training materiaal per rol
- Monitor user adoption en engagement

## 📚 Gerelateerde Documentatie

- [Organisatie Beheer](01-organisatie-beheer.md)
- [Data Manipulatie](03-data-manipulatie.md)
- [Authentication Testing](../testing/04-authentication-testing.md)
- [API Endpoints Guide](../backend/01-api-endpoints-guide.md)

---

**Volgende Stap**: Lees [Data Manipulatie](03-data-manipulatie.md) voor direct database beheer.