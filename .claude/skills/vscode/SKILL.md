```markdown
# vscode Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill provides guidance on contributing to the `vscode` codebase, which is primarily written in TypeScript. It covers the project's coding conventions, common workflows (such as multi-package dependency upgrades), and testing patterns. By following these patterns, contributors can ensure consistency and maintainability across the repository.

## Coding Conventions

### File Naming
- Use **kebab-case** for all file names.
  - Example: `my-component.ts`, `utils-helper.ts`

### Import Style
- Use **relative imports** for modules within the project.
  - Example:
    ```typescript
    import { myFunction } from './utils-helper';
    ```

### Export Style
- Use **named exports** rather than default exports.
  - Example:
    ```typescript
    // utils-helper.ts
    export function myFunction() { /* ... */ }
    ```

### Commit Message Style
- Use **conventional commit** format.
- Common prefix: `build`
- Example:
  ```
  build: update dependencies in core and extensions (lodash, typescript)
  ```

## Workflows

### Multi-Package Dependency Upgrade
**Trigger:** When dependencies need to be updated across the monorepo, often by automated tools or for security/maintenance.
**Command:** `/upgrade-dependencies`

1. **Identify outdated dependencies** in all `package.json` files across subdirectories.
2. **Update** both `package.json` and `package-lock.json` in each affected directory.
3. **Summarize changes** in the commit message, often including a table of updated dependencies and links to changelogs.
4. **List all updated dependencies** and the directories they affect.

**Files involved:**
- `*/package.json`
- `*/package-lock.json`
- `package.json`
- `package-lock.json`

**Example commit message:**
```
build: upgrade dependencies

| Package     | From   | To     | Directory      |
|-------------|--------|--------|---------------|
| lodash      | 4.17.20| 4.17.21| core/          |
| typescript  | 4.4.3  | 4.5.2  | extensions/    |

See [changelog](https://github.com/lodash/lodash/releases).
```

## Testing Patterns

- **Framework:** [mocha](https://mochajs.org/)
- **Test file naming:** Use the `.test.ts` suffix.
  - Example: `my-component.test.ts`
- **Test structure:**
  ```typescript
  import { myFunction } from './my-component';

  describe('myFunction', () => {
    it('should do something', () => {
      // test implementation
    });
  });
  ```

## Commands
| Command               | Purpose                                                         |
|-----------------------|-----------------------------------------------------------------|
| /upgrade-dependencies | Automate multi-package dependency upgrades across the monorepo.  |
```
