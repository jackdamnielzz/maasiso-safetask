# Unit Testing Guide

Purpose
- Short description of what this manual covers.
  Guide to writing, running, and organizing unit tests for the codebase, including best practices, test structure, and sample commands for the project's Jest setup.

Audience
- Who should read this.
  Developers and contributors writing unit tests for the frontend and backend logic.

Prerequisites
- What must be available or configured before following this guide.
  - Node.js and project dependencies installed (run npm install in repository root).
  - Familiarity with Jest and Testing Library concepts.
  - Access to the repository and ability to run npm scripts.

Quick start / Steps
1. Step 1 — Install dependencies: npm install
2. Step 2 — Run all unit tests: npm run test
3. Step 3 — Run tests in watch mode during development: npm run test:watch
4. Step 4 — Add new tests under web/src/**/__tests__ or adjacent to modules as fileName.test.ts

Examples / Commands
- Run tests once:
  npm run test
- Run watch mode:
  npm run test:watch
- Generate coverage report:
  npm run test -- --coverage

Links / Related
- docs/testing/02-e2e-testing-guide.md: End-to-end testing guide
- docs/testing/03-firebase-emulator-testing.md: Firebase emulator testing
- web/jest.config.js: Jest configuration file
- TESTING_STRATEGY.md: Project-wide testing strategy

TODO / Next work
- Add code examples demonstrating mocking Firebase services.
- Document conventions for test file naming and fixtures.
- Provide examples of common Jest matchers and testing-library patterns.