# API Endpoints Guide - SafeWork Pro

**Doelgroep**: Backend Developers, Frontend Developers, Testers  
**Versie**: 1.0.0  
**Laatste Update**: 30 september 2025

## 🎯 Doel van deze Handleiding

Complete referentie voor alle API endpoints in SafeWork Pro, inclusief authenticatie, request/response formaten, en error handling.

## 📋 Base URL & Authentication

### Base URL
```
Production:  https://safeworkpro.com/api
Development: http://localhost:3000/api
```

### Authentication
Alle beschermde endpoints vereisen een Firebase ID token:

```http
Authorization: Bearer <firebase_id_token>
```

### Standard Response Format

#### Success Response
```json
{
  "success": true,
  "data": {
    // Response data hier
  },
  "message": "Optional success message"
}
```

#### Error Response
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Technical error message", 
    "userMessage": "User-friendly message",
    "details": {},
    "requestId": "uuid",
    "timestamp": "2025-09-30T17:00:00.000Z",
    "documentation": "https://docs.safeworkpro.com/errors/ERROR_CODE"
  }
}
```

---

## 🔐 Authentication Endpoints

### Set User Custom Claims

**Endpoint**: `POST /api/auth/set-claims`  
**Beschrijving**: Stel custom claims in voor role-based access control  
**Authenticatie**: Vereist `admin` role

#### Request Body
```json
{
  "targetUserId": "firebase-user-uid",
  "organizationId": "organization-uuid", 
  "role": "admin|safety_manager|supervisor|field_worker"
}
```

#### Response
```json
{
  "success": true,
  "message": "Successfully set role 'admin' for user in organization 'org-name'",
  "data": {
    "userId": "firebase-user-uid",
    "organizationId": "organization-uuid",
    "role": "admin"
  }
}
```

#### cURL Example
```bash
curl -X POST https://safeworkpro.com/api/auth/set-claims \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_FIREBASE_TOKEN" \
  -d '{
    "targetUserId": "target-user-uid",
    "organizationId": "your-org-uuid",
    "role": "safety_manager"
  }'
```

#### Error Responses
- `401` - Unauthorized (geen geldig token)
- `403` - Forbidden (niet admin of organization mismatch)
- `404` - User not found
- `400` - Validatie error

---

## 🏢 Organization Endpoints

### Create Organization

**Endpoint**: `POST /api/organizations`  
**Beschrijving**: Maak nieuwe organisatie aan (alleen voor nieuwe gebruikers)  
**Authenticatie**: Vereist geldig Firebase token

#### Request Body
```json
{
  "name": "Bouwbedrijf Van der Berg",
  "slug": "bouwbedrijf-vd-berg",
  "settings": {
    "industry": "construction",
    "complianceFramework": "vca|iso45001|both",
    "timeZone": "Europe/Amsterdam", 
    "language": "nl"
  }
}
```

#### Response
```json
{
  "success": true,
  "message": "Organization created successfully",
  "data": {
    "organization": {
      "id": "generated-uuid",
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
        "trialEndsAt": "2025-10-14T17:00:00Z"
      }
    },
    "user": {
      "organizationId": "generated-uuid",
      "role": "admin"
    }
  }
}
```

### Get Organization

**Endpoint**: `GET /api/organizations`  
**Beschrijving**: Haal organisatie details op  
**Authenticatie**: Vereist lid van organisatie

#### Response
```json
{
  "success": true,
  "data": {
    "organization": {
      "id": "organization-uuid",
      "name": "Bouwbedrijf Van der Berg",
      "slug": "bouwbedrijf-vd-berg", 
      "settings": {
        "industry": "construction",
        "complianceFramework": "vca",
        "timeZone": "Europe/Amsterdam",
        "language": "nl"
      },
      "subscription": {
        "tier": "professional",
        "status": "active",
        "maxUsers": 50,
        "maxProjects": 100
      },
      "createdAt": "2025-09-01T10:00:00Z",
      "createdBy": "creator-user-id"
    }
  }
}
```

---

## 👥 User Management Endpoints

### Get User Profile

**Endpoint**: `GET /api/users/{userId}`  
**Beschrijving**: Haal gebruiker profiel op  
**Authenticatie**: Vereist toegang tot zelfde organisatie

#### Response
```json
{
  "success": true,
  "data": {
    "user": {
      "uid": "firebase-user-uid",
      "email": "jan.jansen@bouwbedrijf.nl",
      "firstName": "Jan",
      "lastName": "Jansen", 
      "organizationId": "organization-uuid",
      "role": "supervisor",
      "competencies": ["VCA", "Hoogwerker", "Hijskraan"],
      "createdAt": "2025-09-15T10:00:00Z",
      "lastLoginAt": "2025-09-30T08:30:00Z",
      "emailVerified": true,
      "profileComplete": true,
      "status": "active"
    }
  }
}
```

### Update User Profile

**Endpoint**: `PATCH /api/users/{userId}`  
**Beschrijving**: Werk gebruiker profiel bij  
**Authenticatie**: User zelf of admin

#### Request Body
```json
{
  "firstName": "Jan-Willem",
  "lastName": "van der Jansen",
  "competencies": ["VCA", "Hoogwerker", "Hijskraan", "Eerst Hulp"],
  "phone": "+31 6 12345678"
}
```

#### Response
```json
{
  "success": true,
  "message": "User profile updated successfully",
  "data": {
    "user": {
      // Updated user object
    }
  }
}
```

### List Organization Users

**Endpoint**: `GET /api/organizations/users`  
**Beschrijving**: Haal alle gebruikers van organisatie op  
**Authenticatie**: Vereist `supervisor` role of hoger

#### Query Parameters
- `role` (optional): Filter op rol
- `status` (optional): Filter op status (active, disabled)
- `limit` (optional): Aantal resultaten (default: 50)
- `offset` (optional): Pagination offset

#### Response
```json
{
  "success": true,
  "data": {
    "users": [
      {
        "uid": "user-1-uid",
        "email": "admin@company.com",
        "firstName": "Admin",
        "lastName": "User",
        "role": "admin",
        "status": "active",
        "lastLoginAt": "2025-09-30T08:00:00Z"
      }
    ],
    "pagination": {
      "total": 25,
      "limit": 50,
      "offset": 0,
      "hasMore": false
    }
  }
}
```

---

## 📊 Health & Monitoring Endpoints

### Health Check

**Endpoint**: `GET /api/health`  
**Beschrijving**: System health check  
**Authenticatie**: Geen

#### Response
```json
{
  "success": true,
  "data": {
    "status": "healthy|degraded|unhealthy",
    "timestamp": "2025-09-30T17:00:00Z",
    "services": {
      "database": {
        "status": "healthy",
        "responseTime": 45
      },
      "authentication": {
        "status": "healthy",
        "responseTime": 23
      },
      "storage": {
        "status": "healthy", 
        "responseTime": 67
      }
    },
    "version": "1.0.0",
    "environment": "production"
  }
}
```

---

## 🚨 Error Codes Reference

### Authentication Errors (4xx)
- `AUTH_REQUIRED` (401) - Authentication vereist
- `AUTH_INVALID_TOKEN` (401) - Ongeldig of verlopen token
- `AUTH_INSUFFICIENT_PERMISSIONS` (403) - Onvoldoende rechten
- `AUTH_ORGANIZATION_MISMATCH` (403) - Organisatie mismatch

### Validation Errors (4xx)
- `VALIDATION_ERROR` (400) - Algemene validatie fout
- `VALIDATION_REQUIRED_FIELD` (400) - Verplicht veld ontbreekt
- `VALIDATION_INVALID_FORMAT` (400) - Ongeldig formaat

### Resource Errors (4xx)
- `RESOURCE_NOT_FOUND` (404) - Resource niet gevonden
- `RESOURCE_ALREADY_EXISTS` (409) - Resource bestaat al
- `RESOURCE_CONFLICT` (409) - Resource conflict
- `RESOURCE_LOCKED` (409) - Resource vergrendeld

### Business Logic Errors (4xx)
- `BUSINESS_QUOTA_EXCEEDED` (422) - Quota overschreden
- `BUSINESS_INVALID_STATE_TRANSITION` (422) - Ongeldige status wijziging

### Rate Limiting (4xx)
- `RATE_LIMIT_EXCEEDED` (429) - Te veel requests

### Server Errors (5xx)
- `SERVER_ERROR` (500) - Algemene server fout
- `SERVER_DATABASE_ERROR` (500) - Database fout
- `SERVER_EXTERNAL_SERVICE_ERROR` (503) - Externe service niet beschikbaar

---

## 🔧 Development Tools

### API Testing met cURL

```bash
# Get authentication token
TOKEN="your-firebase-id-token"

# Test health endpoint
curl https://safeworkpro.com/api/health

# Test authenticated endpoint
curl -X GET https://safeworkpro.com/api/organizations \
  -H "Authorization: Bearer $TOKEN"

# Create organization
curl -X POST https://safeworkpro.com/api/organizations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{
    "name": "Test Organization",
    "slug": "test-org"
  }'
```

### Postman Collection

Importeer de Postman collection voor complete API testing:

```json
{
  "info": {
    "name": "SafeWork Pro API",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "auth": {
    "type": "bearer",
    "bearer": [
      {
        "key": "token",
        "value": "{{firebase_token}}"
      }
    ]
  },
  "variable": [
    {
      "key": "base_url",
      "value": "https://safeworkpro.com/api"
    },
    {
      "key": "firebase_token", 
      "value": "your-token-here"
    }
  ]
}
```

### Rate Limiting

Alle authenticated endpoints hebben rate limits:

- **Per User**: 100 requests per minuut
- **Per Organization**: 1000 requests per uur
- **Health Check**: Geen limiet

Rate limit headers:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1696089600
```

---

## 🛠️ Request/Response Middleware

### Request Validation

Alle requests worden gevalideerd met [Zod schemas](https://zod.dev/):

```typescript
// Voorbeeld request schema
const createOrganizationSchema = z.object({
  name: z.string().min(2, 'Naam moet minimaal 2 karakters zijn'),
  slug: z.string().regex(/^[a-z0-9-]+$/, 'Slug alleen lowercase, nummers en streepjes'),
  settings: z.object({
    industry: z.string().optional(),
    complianceFramework: z.enum(['vca', 'iso45001', 'both']).default('vca')
  }).optional()
});
```

### Response Headers

Alle API responses bevatten standaard headers:

```
Content-Type: application/json
X-Request-ID: uuid-v4-request-identifier
X-Response-Time: 123ms
Cache-Control: no-cache, no-store, must-revalidate
```

---

## 📚 Gerelateerde Documentatie

- [Authentication Testing](../testing/04-authentication-testing.md)
- [Firebase Admin Guide](02-firebase-admin-guide.md)
- [Database Management](03-database-management.md)
- [Organisatie Beheer](../admin/01-organisatie-beheer.md)
- [Flow Diagrammen](../admin/flow-diagrams.md)

---

**Laatste Update**: Deze API documentatie wordt automatisch bijgewerkt bij nieuwe endpoint releases. Check de versie datum bovenaan.