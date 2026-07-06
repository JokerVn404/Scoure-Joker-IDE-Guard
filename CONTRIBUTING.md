# Contributing Guide — Scoure v0.1.0

Thank you for considering contributing to Scoure! We welcome bug reports, feature requests, documentation, and code contributions.

**Important:** This is a **private project during v1 MVP phase**. Public contributions will be welcomed after v1.0 release and community review.

---

## Code of Conduct

- Be respectful and inclusive.
- Assume good intent.
- Report violations to maintainers.

---

## How to Contribute (Private Phase)

### Reporting Bugs

1. Check existing private issues (avoid duplicates).
2. Create a new issue with:
   - **Title:** Clear, concise description.
   - **Reproduction steps:** How to trigger the bug.
   - **Expected vs actual:** What should happen vs. what happens.
   - **Environment:** OS, Node version, browser, etc.
   - **Logs/screenshots:** Paste error or screenshots.

### Requesting Features

1. Check existing discussions (private).
2. Create issue with:
   - **Use case:** Why you need this.
   - **Proposed solution:** How you'd implement it.
   - **Alternatives:** Other approaches considered.

### Code Contributions (Private Phase)

During v1 MVP (private), contributions are limited to invited collaborators. After v1 release (public), we welcome community contributions.

#### For Invited Collaborators:

```bash
git clone https://github.com/JokerVn404/Scoure-Joker-IDE-Guard.git
cd Scoure-Joker-IDE-Guard
git checkout feat/v1-complete
git checkout -b feat/my-feature
```

Make changes, test locally, then:

```bash
npm run lint
npm run test
git commit -m "feat: description"
git push origin feat/my-feature
# Open PR to feat/v1-complete (not main)
```

---

## Code Style

### JavaScript/TypeScript

- Use **ES6+ syntax** (const/let, arrow functions, destructuring).
- Use **semicolons** always.
- Use **2-space indentation**.
- Use **camelCase** for variables/functions, **PascalCase** for classes.
- Comments for non-obvious logic.

### SQL

- Use **lowercase** keywords (SELECT, WHERE, etc.).
- Use **clear table/column names**.
- Comment complex queries.

### Markdown

- Use **heading hierarchy** correctly (h1 > h2 > h3, no skipping).
- Use **code blocks** with language.
- Keep lines under 100 chars when possible.

---

## Testing Requirements

Before submitting PR:

```bash
npm run lint
npm run test
npm run build
```

Aim for >80% coverage on new code.

---

## Review Process (Private Phase)

1. **Automated checks:** CI runs tests, linting.
2. **Maintainer review:** Code quality, design, docs.
3. **Adjustments:** Address feedback or clarify.
4. **Merge:** Squash-and-merge or rebase.

---

## What We're Looking For (v1)

### High Priority

- Bug fixes (especially security or privacy).
- Documentation improvements.
- Test coverage increases.
- Usability enhancements (UX/UI).

### Lower Priority (for v1)

- Scoring/comparator logic (v2 feature).
- Non-MVP features (see roadmap).
- Refactors without clear benefit.

---

## License & Copyright

By contributing, you agree that your contributions are owned by the project and can be used under the project's license (proprietary, v1). You retain copyright; the project uses your code under the proprietary license.

---

## Questions?

- **GitHub Issues:** Ask in issue tracker.
- **Email:** maintainers@scoure.example.com
