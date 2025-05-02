# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build Commands
- Build: `npm run build`
- Start: `npm run start`
- Development mode: `npm run dev`

## Test Commands
- Run all tests: `npm test`
- Run single test: `jest path/to/file.test.ts`
- Run tests with pattern: `jest -t "test description"`
- Watch tests: `npm run test:watch`
- Coverage: `npm run test:coverage`
- Integration tests: `npm run test:integration`

## Code Style Guidelines
- Use ES Modules (import/export) with .js extension in import paths
- TypeScript with strict mode enabled
- Class-based architecture with handler pattern for features
- PascalCase for classes and interfaces; camelCase for variables and methods
- Use async/await for asynchronous code
- Error handling: Use McpError with appropriate ErrorCode
- Required parameters should be validated with validateRequiredParams method
- Document public methods with JSDoc comments
- Group imports by external dependencies first, then internal