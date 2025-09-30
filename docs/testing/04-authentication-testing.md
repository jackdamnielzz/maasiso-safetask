# Authentication Testing Handleiding

**Doelgroep**: Developers, QA Engineers  
**Versie**: 1.0.0  
**Laatste Update**: 30 september 2025

## 🎯 Doel van deze Handleiding

Complete handleiding voor het testen van het authentication systeem in SafeWork Pro, inclusief unit tests, integration tests en end-to-end testing.

## 📋 Vereisten

- Firebase Emulators geïnstalleerd
- Jest en Cypress geconfigureerd
- Toegang tot test database
- Node.js 18+ en npm

## 🧪 Test Categorieën

### 1. Unit Tests - Authentication Functions

**Locatie**: `web/src/__tests__/auth-system.test.ts`

```bash
# Run authentication unit tests
npm run test -- auth-system.test.ts

# Run with coverage
npm run test:coverage -- auth-system.test.ts
```

**Test Scenarios**:
- ✅ Gebruiker registratie met email/password
- ✅ Google SSO authenticatie
- ✅ Password reset functionaliteit
- ✅ Email verificatie
- ✅ Custom claims management
- ✅ Role-based access control
- ✅ Error handling scenarios

### 2. Integration Tests - Firebase Services

```javascript
// Voorbeeld Firebase Emulator test
describe('Firebase Integration Tests', () => {
  beforeAll(async () => {
    // Start Firebase Emulators
    await exec('firebase emulators:start --only auth,firestore');
  });

  test('User registration creates profile in Firestore', async () => {
    const userCredential = await createUserWithEmailAndPassword(
      auth, 
      'test@example.com', 
      'TestPassword123!'
    );
    
    // Check if user profile was created
    const userDoc = await getDoc(doc(db, 'users', userCredential.user.uid));
    expect(userDoc.exists()).toBe(true);
    expect(userDoc.data().email).toBe('test@example.com');
  });
});
```

### 3. API Integration Tests

```javascript
// Test API authentication endpoints
describe('API Authentication Tests', () => {
  test('POST /api/auth/set-claims requires admin role', async () => {
    const response = await fetch('/api/auth/set-claims', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer non-admin-token'
      },
      body: JSON.stringify({
        targetUserId: 'user-id',
        organizationId: 'org-id',
        role: 'admin'
      })
    });
    
    expect(response.status).toBe(403);
  });
});
```

## 🔧 Test Setup

### Firebase Emulators Configureren

```bash
# Start emulators voor testing
npm run emulators:test

# Of handmatig
firebase emulators:start --only auth,firestore,storage
```

### Test Data Setup

```javascript
// Test data helper functions
export async function createTestUser(email: string, role: string) {
  const userCredential = await createUserWithEmailAndPassword(
    auth, 
    email, 
    'TestPassword123!'
  );
  
  await setDoc(doc(db, 'users', userCredential.user.uid), {
    uid: userCredential.user.uid,
    email,
    organizationId: 'test-org-id',
    role,
    createdAt: new Date(),
    profileComplete: true
  });
  
  return userCredential.user;
}

export async function createTestOrganization(id: string, name: string) {
  await setDoc(doc(db, 'organizations', id), {
    id,
    name,
    slug: name.toLowerCase().replace(/\s+/g, '-'),
    settings: {
      complianceFramework: 'vca',
      language: 'nl'
    },
    subscription: {
      tier: 'trial',
      status: 'active'
    },
    createdAt: new Date()
  });
}
```

## 🎭 End-to-End Testing

### Cypress Authentication Tests

**Locatie**: `web/cypress/e2e/authentication.cy.ts`

```javascript
describe('Authentication E2E Tests', () => {
  beforeEach(() => {
    cy.visit('/auth/login');
  });

  it('should login with valid credentials', () => {
    cy.get('[data-cy=email-input]').type('admin@test.com');
    cy.get('[data-cy=password-input]').type('TestPassword123!');
    cy.get('[data-cy=login-button]').click();
    
    cy.url().should('include', '/dashboard');
    cy.contains('Welcome').should('be.visible');
  });

  it('should show error for invalid credentials', () => {
    cy.get('[data-cy=email-input]').type('wrong@test.com');
    cy.get('[data-cy=password-input]').type('wrongpassword');
    cy.get('[data-cy=login-button]').click();
    
    cy.get('[data-cy=error-alert]').should('contain', 'Invalid email or password');
  });

  it('should register new user successfully', () => {
    cy.visit('/auth/register');
    
    cy.get('[data-cy=company-name]').type('Test Company');
    cy.get('[data-cy=full-name]').type('John Doe');
    cy.get('[data-cy=email]').type('john@testcompany.com');
    cy.get('[data-cy=password]').type('SecurePassword123!');
    cy.get('[data-cy=confirm-password]').type('SecurePassword123!');
    cy.get('[data-cy=terms-checkbox]').check();
    cy.get('[data-cy=register-button]').click();
    
    cy.url().should('include', '/auth/verify-email');
    cy.contains('Check your email').should('be.visible');
  });
});
```

### Run E2E Tests

```bash
# Headless mode
npm run cypress:run

# Interactive mode
npm run cypress:open

# Specific test file
npm run cypress:run -- --spec "cypress/e2e/authentication.cy.ts"
```

## 🔍 Performance Testing

### Load Testing Authentication

```javascript
// Performance test example using Jest
describe('Authentication Performance Tests', () => {
  test('Login should complete within 2 seconds', async () => {
    const startTime = Date.now();
    
    await signInWithEmailAndPassword(auth, 'test@example.com', 'password');
    
    const duration = Date.now() - startTime;
    expect(duration).toBeLessThan(2000);
  });

  test('Batch user creation should handle 100 users', async () => {
    const users = Array.from({length: 100}, (_, i) => ({
      email: `user${i}@test.com`,
      password: 'TestPassword123!'
    }));
    
    const startTime = Date.now();
    
    const results = await Promise.all(
      users.map(user => 
        createUserWithEmailAndPassword(auth, user.email, user.password)
      )
    );
    
    const duration = Date.now() - startTime;
    expect(results).toHaveLength(100);
    expect(duration).toBeLessThan(30000); // 30 seconds max
  });
});
```

## 🛠️ Test Utilities

### Mock Firebase Services

```javascript
// Jest mock setup
jest.mock('@/lib/firebase', () => ({
  auth: {
    createUserWithEmailAndPassword: jest.fn(),
    signInWithEmailAndPassword: jest.fn(),
    signOut: jest.fn(),
    onAuthStateChanged: jest.fn()
  },
  db: {},
  googleProvider: {}
}));

// Mock AuthProvider
const MockAuthProvider = ({ children, mockUser = null }) => {
  const mockValue = {
    user: mockUser,
    loading: false,
    signIn: jest.fn().mockResolvedValue({}),
    signUp: jest.fn().mockResolvedValue({}),
    signInWithGoogle: jest.fn().mockResolvedValue({}),
    signOutUser: jest.fn().mockResolvedValue({}),
    resetPassword: jest.fn().mockResolvedValue({}),
    error: null,
    clearError: jest.fn()
  };

  return (
    <AuthContext.Provider value={mockValue}>
      {children}
    </AuthContext.Provider>
  );
};
```

### Test Data Factories

```javascript
// Factory functions voor test data
export const userFactory = (overrides = {}) => ({
  uid: 'test-uid-' + Math.random(),
  email: 'test@example.com',
  firstName: 'Test',
  lastName: 'User',
  organizationId: 'test-org-id',
  role: 'field_worker',
  createdAt: new Date(),
  profileComplete: true,
  ...overrides
});

export const organizationFactory = (overrides = {}) => ({
  id: 'test-org-' + Math.random(),
  name: 'Test Organization',
  slug: 'test-org',
  settings: {
    complianceFramework: 'vca',
    language: 'nl',
    timeZone: 'Europe/Amsterdam'
  },
  subscription: {
    tier: 'trial',
    status: 'active'
  },
  createdAt: new Date(),
  ...overrides
});
```

## 📊 Test Coverage Requirements

### Minimum Coverage Thresholds

```javascript
// jest.config.js coverage thresholds
module.exports = {
  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.d.ts',
  ],
  coverageThreshold: {
    global: {
      branches: 80,
      functions: 80,
      lines: 80,
      statements: 80
    },
    './src/components/AuthProvider.tsx': {
      branches: 95,
      functions: 95,
      lines: 95,
      statements: 95
    },
    './src/lib/api/auth.ts': {
      branches: 90,
      functions: 90,
      lines: 90,
      statements: 90
    }
  }
};
```

## 🚨 Common Test Failures & Solutions

### 1. Firebase Emulator Connection Issues

**Probleem**: `Error: Could not connect to Firestore emulator`

**Oplossing**:
```bash
# Controleer of emulators draaien
firebase emulators:start --only auth,firestore

# Check poorten
lsof -i :9099  # Auth emulator
lsof -i :8080  # Firestore emulator
```

### 2. Custom Claims Not Updating

**Probleem**: Tests falen omdat custom claims niet worden toegepast

**Oplossing**:
```javascript
// Force token refresh in tests
await auth.currentUser?.getIdToken(true);
```

### 3. Race Conditions in Async Tests

**Probleem**: Tests falen sporadisch door timing issues

**Oplossing**:
```javascript
// Gebruik waitFor utilities
import { waitFor } from '@testing-library/react';

await waitFor(() => {
  expect(auth.currentUser).not.toBeNull();
}, { timeout: 5000 });
```

## 📈 Test Metrics & Monitoring

### Key Test Metrics

- **Test Execution Time**: < 30 seconden voor unit tests
- **Code Coverage**: > 80% overall, > 95% voor kritieke auth functies  
- **E2E Test Success Rate**: > 95%
- **Performance**: Login < 2s, Registration < 3s

### CI/CD Integration

```yaml
# GitHub Actions example
- name: Run Authentication Tests
  run: |
    npm run emulators:start &
    npm run test:auth
    npm run cypress:run -- --spec "**/authentication.cy.ts"
```

## 📚 Gerelateerde Documentatie

- [Firebase Emulator Testing](03-firebase-emulator-testing.md)
- [Unit Testing Guide](01-unit-testing-guide.md)
- [E2E Testing Guide](02-e2e-testing-guide.md)
- [API Endpoints Guide](../backend/01-api-endpoints-guide.md)

---

**Tip**: Run altijd de volledige test suite voor authentication changes:
```bash
npm run test:all -- --testPathPattern=auth