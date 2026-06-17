```markdown
# servers Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill introduces the core development patterns and workflows used in the `servers` TypeScript repository. The codebase is organized into multiple server modules, each with its own package management, and follows consistent coding conventions for maintainability. While no specific framework is detected, the repository emphasizes modularity, clear import/export patterns, and streamlined dependency management across packages.

## Coding Conventions

### File Naming
- **Style:** camelCase
- **Example:**  
  ```
  userService.ts
  fileManager.ts
  ```

### Import Style
- **Relative imports** are used throughout the codebase.
- **Example:**
  ```typescript
  import { validateUser } from './validators';
  import { FileSystem } from '../filesystem/fileSystem';
  ```

### Export Style
- **Named exports** are preferred.
- **Example:**
  ```typescript
  // In userService.ts
  export function createUser() { ... }
  export const USER_ROLE = 'admin';
  ```

## Workflows

### Upgrade Dependencies Across Packages
**Trigger:** When you need to update a shared dependency (such as zod or an SDK) in multiple server modules at once.  
**Command:** `/upgrade-dependency`

1. **Update dependency versions**  
   Edit the `package.json` file in each affected server package (e.g., `src/everything/package.json`, `src/filesystem/package.json`) to reference the new version of the dependency.
   ```json
   // Example in src/filesystem/package.json
   {
     "dependencies": {
       "zod": "^3.22.0"
     }
   }
   ```
2. **Update the lockfile**  
   Run your package manager (e.g., `npm install`) at the repository root to regenerate `package-lock.json` with the updated dependency versions.
3. **Update code if necessary**  
   If the new dependency version introduces breaking changes or new APIs, update the relevant TypeScript files (e.g., `src/everything/tools/*.ts`) to accommodate these changes.
   ```typescript
   // Example: Adapting to a new zod API
   import { z } from 'zod';
   const schema = z.object({ name: z.string() });
   ```
4. **Test your changes**  
   Run all tests to ensure that the upgrade does not break existing functionality.

## Testing Patterns

- **Test file pattern:** Files are named with the `*.test.*` convention, such as `userService.test.ts`.
- **Testing framework:** Not explicitly detected; review test files for framework details.
- **Example:**
  ```typescript
  // userService.test.ts
  import { createUser } from './userService';

  test('should create a user', () => {
    expect(createUser('alice')).toBeDefined();
  });
  ```

## Commands

| Command              | Purpose                                                              |
|----------------------|----------------------------------------------------------------------|
| /upgrade-dependency  | Upgrade a shared dependency across multiple server packages at once.  |
```
