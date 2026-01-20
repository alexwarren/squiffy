# Squiffy Documentation Gaps Analysis

**Generated:** 2026-01-12
**Last Updated:** 2026-01-20

This document identifies missing or incomplete documentation in the Squiffy project (v6 alpha).

## Executive Summary

**Current State:**
- 13 documentation files exist (2 root-level, 4 package READMEs, 7 user guide pages)
- User-facing guides cover basic concepts, attributes/state management, dynamic text, helpers reference, CLI usage, and examples
- CLAUDE.md provides internal developer guidance but is not public documentation

**Recent Improvements (Jan 2026):**
- ✅ Added comprehensive attributes documentation (`attributes.mdx`)
- ✅ Added complete helpers reference (`helpers-reference.mdx`)
- ✅ Added examples page with interactive demos (`featured-examples.mdx`)
- ✅ Added input validation documentation to basic concepts

**Remaining Major Gaps:**
- No API reference documentation for developers
- Missing advanced user guides (deployment, troubleshooting)
- No plugin development documentation
- Incomplete package-level documentation
- No migration guide from v5 to v6

---

## 1. API Documentation (Critical Gap)

### 1.1 Runtime API Reference
**Status:** Missing
**Impact:** High - Developers cannot programmatically integrate Squiffy

**Missing Content:**
- `init()` options documentation (element, story, scroll, persist, onSet)
- API methods: `begin()`, `restart()`, `get()`, `set()`, `clickLink()`, `update()`, `goBack()`
- Event system: `on()`, `off()`, `once()` with return values
- Event types: `linkClick`, `set`, `canGoBackChanged`
- Complete TypeScript interface reference for `SquiffyApi`

**Example Use Case:** Developer wants to embed Squiffy in React app - no documentation exists

### 1.2 Compiler API Reference
**Status:** Missing
**Impact:** High - Developers cannot build tools that compile Squiffy

**Missing Content:**
- `compile()` function signature and parameters
- `CompilerSettings` interface (script, scriptBaseFilename, onWarning, externalFiles, globalJs)
- `CompileSuccess` and `CompileError` types
- `Output` structure (story.start, story.sections, story.js, story.id, story.uiJsIndex)
- Helper methods: `getJs()`, `getUiInfo()`
- Error handling and warning system

**Example Use Case:** Building a custom build tool or IDE plugin

### 1.3 Packager API Reference
**Status:** Missing
**Impact:** Medium - Developers cannot customize packaging

**Missing Content:**
- `createPackage()` function signature
- `Package` output structure (files, zip)
- Generated file descriptions (story.js, squiffy.runtime.global.js, index.html, style.css)
- Customization options for HTML/CSS templates

**Example Use Case:** Creating custom deployment pipeline with branded templates

### 1.4 Plugin API Reference
**Status:** Missing
**Impact:** High - Cannot create custom plugins

**Missing Content:**
- `SquiffyPlugin` interface (name, init, onWrite, onLoad)
- `PluginHost` interface and capabilities
- Helper registration: `registerHelper(name, fn)`
- Animation registration: `registerAnimation(name, handler, options)`
- Link handler registration
- Event access in plugins

**Example Use Case:** Creating a custom plugin for game mechanics (inventory, combat)

---

## 2. User Guide Gaps

### 2.1 Complete Syntax Reference
**Status:** Partial - improved but still scattered
**Impact:** High - Users cannot find complete reference in one place

**Now Documented (across multiple pages):**
- Attribute commands (@set, @inc, @dec, @unset) documented in `attributes.mdx`
- Link syntax with attribute settings documented in `attributes.mdx`
- All Handlebars helpers documented in `helpers-reference.mdx`

**Still Missing:**
- Complete link syntax reference (all variants in one place)
- Non-attribute metadata commands (@title, @start, @import, @ui)
- Screen control commands (@clear, ---, +++)
- Computed expressions in links (`:=` operator)
- Master sections/passages syntax and use cases
- Turn-based passages (@1, @2, @last)

**Recommended:** Create `syntax-reference.mdx` consolidating all syntax in one comprehensive page

### 2.2 Handlebars Helper Reference
**Status:** ✅ COMPLETED (Jan 2026)
**Location:** `site/src/content/docs/helpers-reference.mdx`

**Now Documented:**
- All attribute helpers: `{{set}}`, `{{unset}}`, `{{inc}}`, `{{dec}}`, `{{get}}`
- All conditional helpers: `{{#if}}`, `{{#else}}`, `{{#unless}}`
- All logic helpers: `{{and}}`, `{{or}}`, `{{not}}`, `{{eq}}`, `{{ne}}`, `{{gt}}`, `{{lt}}`, `{{gte}}`, `{{lte}}`
- All state helpers: `{{seen}}`, `{{at}}`, `{{embed}}`
- Link helpers: `{{section}}`, `{{passage}}`
- Array helper: `{{array}}`
- Dynamic content helpers: `{{random}}`, `{{#animate}}`, `{{#label}}`, `{{replace}}`, `{{rotate}}`, `{{sequence}}`, `{{live}}`
- Helper vs directive distinction explained
- Parameters and examples for each helper

### 2.3 State Management Guide
**Status:** ✅ MOSTLY COMPLETED (Jan 2026)
**Location:** `site/src/content/docs/attributes.mdx`

**Now Documented:**
- Setting attributes (directives and helpers)
- Reading attributes with `{{attribute}}` and `{{get}}`
- Conditional attribute changes (helper vs directive distinction)
- Comparing attributes with all comparison operators
- Logic helpers for complex conditions
- Tracking sections/passages with `{{seen}}` and `{{at}}`
- Embedding text from other sections
- Creating links with helpers
- Using attributes in JavaScript
- Interactive example (food menu) demonstrating state patterns

**Still Missing (minor gaps):**
- Built-in attributes documentation: `_section`, `_turncount`, `_seen_sections`, `_output`
- Persistence system details (localStorage keys, enabling/disabling)
- Debugging state issues

### 2.4 Plugin Usage Guide
**Status:** ✅ PARTIALLY COMPLETED (Jan 2026)
**Location:** Usage documented in `helpers-reference.mdx`; examples in `featured-examples.mdx`

**Now Documented (via helpers reference):**
- ReplaceLabel (`{{#label}}`, `{{replace}}`)
- Random (`{{random}}`)
- Rotate/Sequence (`{{rotate}}`, `{{sequence}}`)
- Live (`{{live}}`)
- Animate (`{{#animate}}`)
- Usage examples for each

**Still Missing:**
- What plugins are and how they work (conceptual overview)
- When to use which plugin (guidance)
- How to find/install community plugins
- Dedicated plugins.mdx page explaining the plugin system

**Recommended:** Create `plugins.mdx` with conceptual overview and link to helpers reference for details

### 2.5 Animation Guide
**Status:** ✅ PARTIALLY COMPLETED (Jan 2026)
**Location:** `helpers-reference.mdx` and `dynamic-text.mdx`

**Now Documented:**
- Built-in animation types: typewriter, toast, fadeIn, continue
- Basic animation syntax and usage
- Animation parameters: trigger, style, loop

**Still Missing:**
- Complete animation options (start, interval, fadeDuration)
- Animation timing and chaining
- Performance considerations
- Custom animation development (links to dev guide)

**Recommended:** Consider expanding `dynamic-text.mdx` for advanced animation topics

### 2.6 Deployment Guide
**Status:** Missing
**Impact:** High - Users don't know how to publish

**Missing Content:**
- How to generate production files (CLI --zip option)
- Hosting options: GitHub Pages, Netlify, itch.io, own server
- Step-by-step deployment tutorials
- Domain configuration
- Analytics integration
- SEO considerations for story pages
- Embedding in existing websites

**Recommended:** Create `deployment.mdx`

### 2.7 Troubleshooting Guide
**Status:** Missing
**Impact:** High - Users get stuck

**Missing Content:**
- Common compilation errors and fixes
- Link not working (section/passage name mismatch)
- JavaScript errors in story code
- State not persisting
- Animations not showing
- Import errors
- Browser compatibility issues
- Debugging techniques (browser console, localStorage inspection)

**Recommended:** Create `troubleshooting.mdx`

### 2.8 Best Practices Guide
**Status:** Missing
**Impact:** Medium - Users create suboptimal stories

**Missing Content:**
- Story structure recommendations (sections vs passages)
- When to use master sections/passages
- Performance tips for large stories
- Organizing complex branching narratives
- Testing interactive stories
- Accessibility considerations
- Mobile-friendly story design
- Code organization (splitting files with @import)

**Recommended:** Create `best-practices.mdx`

### 2.9 Examples Gallery
**Status:** ✅ PARTIALLY COMPLETED (Jan 2026)
**Location:** `site/src/content/docs/featured-examples.mdx`

**Now Documented:**
- Coffee Shop Story example (demonstrates text input, variable tracking, conditional text, relationship tracking, multiple endings)
- Game Show example (demonstrates animations, live updates, randomization, complex state tracking, nested conditionals, dynamic scoring)
- Both examples are interactive with playable demos

**Still Missing:**
- Additional common patterns: inventory systems, combat, dialogue trees, timers
- Integration examples (embedding Squiffy in apps)
- Links to community stories

### 2.10 Migration Guide (v5 → v6)
**Status:** Missing
**Impact:** High for v5 users

**Missing Content:**
- Breaking changes from v5
- New features in v6
- Migration steps
- API changes
- Syntax changes
- Update checklist

**Recommended:** Create `migration-v5-to-v6.mdx`

---

## 3. Developer Documentation Gaps

### 3.1 Plugin Development Guide
**Status:** Missing
**Impact:** High - Blocks ecosystem growth

**Missing Content:**
- Step-by-step plugin creation tutorial
- Plugin architecture explanation
- Implementing `SquiffyPlugin` interface
- Using `PluginHost` capabilities
- Creating custom Handlebars helpers
- Creating custom link handlers
- Creating custom animations
- Plugin testing strategies
- Plugin distribution (npm, CDN)
- Example: Complete plugin implementation

**Recommended:** Create `docs/plugin-development.md`

### 3.2 Architecture Documentation (Public)
**Status:** CLAUDE.md only (internal)
**Impact:** Medium - Developers can't contribute effectively

**Missing Content:**
- Monorepo structure explanation
- Package relationships and data flow
- Compiler internals (parser, code generator)
- Runtime internals (state, link handlers, plugins)
- Build system (Lerna, Vite)
- Testing architecture (Vitest, jsdom, E2E)

**Recommended:** Create `docs/architecture.md` based on CLAUDE.md

### 3.3 Contributing Guide
**Status:** Missing
**Impact:** Medium - Barriers to contribution

**Missing Content:**
- How to set up development environment
- Coding standards and conventions
- PR process and requirements
- Testing requirements
- How to report bugs
- How to propose features
- Code of conduct

**Recommended:** Create `CONTRIBUTING.md`

### 3.4 Package-Specific Documentation
**Status:** Minimal (only build commands)
**Impact:** Medium

**Missing Content:**

Each package needs comprehensive README with:
- **compiler/**: API reference, parser details, code generation
- **runtime/**: API reference, plugin system, event system, state management
- **packager/**: API reference, customization options, template system
- **cli/**: Command reference, configuration, dev server details
- **types/**: Type definitions explanation, Vite plugin usage
- **editor/**: Features, keyboard shortcuts, PWA details, local storage

**Recommended:** Expand all `*/README.md` files

---

## 4. Technical Documentation Gaps

### 4.1 Browser Compatibility
**Status:** Missing
**Impact:** Medium

**Missing Content:**
- Supported browsers and versions
- Required polyfills
- Known incompatibilities
- Mobile browser support
- Testing matrix

**Recommended:** Create `docs/browser-compatibility.md`

### 4.2 Performance Optimization
**Status:** Missing
**Impact:** Low-Medium

**Missing Content:**
- Performance considerations for large stories
- Lazy loading techniques
- Memory management
- Animation performance
- State size limits
- Profiling techniques

**Recommended:** Create section in best-practices.mdx

### 4.3 Accessibility
**Status:** Missing
**Impact:** Medium

**Missing Content:**
- Screen reader compatibility
- Keyboard navigation
- ARIA labels and roles
- Color contrast guidelines
- Focus management
- Testing with assistive technologies

**Recommended:** Create `accessibility.mdx`

### 4.4 PWA Features (Editor)
**Status:** Missing
**Impact:** Low

**Missing Content:**
- Offline functionality
- Service worker implementation
- Cache strategy
- Install prompts
- Update mechanism

**Recommended:** Document in `editor/README.md`

### 4.5 CSS Customization
**Status:** Missing
**Impact:** Medium

**Missing Content:**
- Default styles explanation
- How to override styles
- CSS variables/custom properties
- Theme creation
- Responsive design patterns
- Animation styling

**Recommended:** Create `styling.mdx`

### 4.6 Security Considerations
**Status:** Missing
**Impact:** Low-Medium

**Missing Content:**
- XSS prevention
- Input sanitization
- localStorage security
- Third-party script risks
- Content security policy

**Recommended:** Create `docs/security.md`

---

## 5. Project Management Documentation Gaps

### 5.1 Roadmap
**Status:** Missing
**Impact:** Low

**Missing Content:**
- v6 completion timeline
- Planned features
- Known limitations
- Future direction

**Recommended:** Create `ROADMAP.md` or GitHub Projects

### 5.2 Changelog
**Status:** Missing (only git commits)
**Impact:** Low-Medium

**Missing Content:**
- Version history with release notes
- Breaking changes highlighted
- Feature additions
- Bug fixes

**Recommended:** Create `CHANGELOG.md` following Keep a Changelog format

### 5.3 Community/Support
**Status:** Minimal mention in site
**Impact:** Medium

**Missing Content:**
- Where to get help (Discord, GitHub Discussions, Stack Overflow)
- How to report bugs vs ask questions
- Response time expectations
- Community resources

**Recommended:** Create `docs/community.md`

---

## 6. Priority Matrix

### Critical (Should be addressed first)
1. **Runtime API Reference** - Blocks developer adoption
2. **Complete Syntax Reference** - Essential user reference
3. **Deployment Guide** - Users can't publish stories
4. **Troubleshooting Guide** - Reduces support burden
5. ~~**State Management Guide**~~ ✅ Completed (see `attributes.mdx`)
6. **Migration Guide v5→v6** - Blocks v5 user upgrades

### High Priority
7. Plugin Development Guide - Enables ecosystem
8. Compiler API Reference - Enables tooling
9. Contributing Guide - Enables open source contributions
10. ~~**Handlebars Helper Reference**~~ ✅ Completed (see `helpers-reference.mdx`)
11. Package-Specific READMEs - Improves developer experience

### Medium Priority
12. Plugin Usage Guide - Improves user capability
13. Best Practices Guide - Improves story quality
14. ~~**Examples Gallery**~~ ✅ Partially completed (see `featured-examples.mdx`)
15. Architecture Documentation - Contributor onboarding
16. Accessibility Guide - Inclusivity
17. CSS Customization Guide - Branding/themes

### Low Priority
18. Browser Compatibility - Can be minimal
19. Performance Optimization - Edge cases
20. Security Considerations - Low risk for stories
21. PWA Features Documentation - Editor-specific
22. Changelog - Nice to have
23. Roadmap - Optional transparency

---

## 7. Documentation Structure Recommendations

### Proposed Site Organization

```
/docs/
├── index.mdx (Welcome - EXISTS)
├── getting-started/
│   ├── installation.mdx
│   ├── your-first-story.mdx
│   └── deployment.mdx (NEW)
├── guides/
│   ├── syntax-reference.mdx (NEW - consolidate all syntax)
│   ├── basic-concepts.mdx (EXISTS)
│   ├── dynamic-text.mdx (EXISTS)
│   ├── attributes.mdx (EXISTS ✅ - covers state management)
│   ├── plugins.mdx (NEW)
│   ├── styling.mdx (NEW)
│   ├── accessibility.mdx (NEW)
│   └── best-practices.mdx (NEW)
├── reference/
│   ├── cli.mdx (EXISTS)
│   ├── helpers-reference.mdx (EXISTS ✅)
│   ├── runtime-api.mdx (NEW)
│   ├── compiler-api.mdx (NEW)
│   ├── packager-api.mdx (NEW)
│   └── plugin-api.mdx (NEW)
├── examples/
│   └── featured-examples.mdx (EXISTS ✅ - interactive examples)
├── advanced/
│   ├── plugin-development.mdx (NEW)
│   ├── custom-animations.mdx (NEW)
│   └── architecture.mdx (NEW)
├── troubleshooting.mdx (NEW)
└── migration-v5-to-v6.mdx (NEW)
```

### Package README Structure

Each package should have:
1. Brief description
2. Installation
3. Basic usage
4. API reference (or link to docs site)
5. Examples
6. Links to full documentation

---

## 8. Action Items Summary

**Progress Update (Jan 2026):**
- ✅ Helpers reference page created
- ✅ State management (attributes) page created
- ✅ Examples page with interactive demos created
- ✅ Input validation documented in basic concepts

**Remaining work to achieve comprehensive documentation:**

1. **Create 12 new user guide pages** (syntax-reference, plugins, deployment, troubleshooting, best-practices, migration, styling, accessibility, installation, your-first-story, custom-animations, architecture)

2. **Create 4 new API reference pages** (runtime-api, compiler-api, packager-api, plugin-api)

3. **Create 3 new developer guides** (plugin-development, architecture, contributing)

4. **Expand 6 package READMEs** (compiler, runtime, packager, cli, types, editor)

5. **Create 4 project management docs** (CONTRIBUTING.md, CHANGELOG.md, ROADMAP.md, community.md)

6. **Reorganize site structure** to match proposed organization

**Estimated effort:** 30-45 hours of technical writing (reduced from 40-60)

**Quick wins (can be done in 1-2 hours each):**
- Contributing guide
- Browser compatibility matrix
- Community/support page
- Changelog from git history

---

## 9. Documentation Quality Issues

Beyond missing content, existing documentation has these issues:

1. **Inconsistent depth** - Some features deeply explained, others mentioned briefly
2. **No cross-references** - Related features not linked together
3. **No search keywords** - Missing metadata for discoverability
4. **Code examples scattered** - Not consistently formatted or highlighted
5. **No "Next steps"** - Docs don't guide users to related topics

**Recommendations:**
- Add "Related topics" sections to each page
- Implement consistent code formatting
- Add frontmatter with keywords/tags
- Include "What's next?" sections
- Add search functionality to docs site

---

## Conclusion

The Squiffy project has **strong foundational documentation** for basic usage and has made **significant progress** in January 2026 with comprehensive attributes/state management and helpers reference documentation. However, **critical gaps remain** in API references, deployment guides, and developer documentation. The v6 rewrite has introduced many powerful features (plugin system, modern runtime API, TypeScript) that are still **largely undocumented** for public use.

**Recent Accomplishments:**
- ✅ State management documentation (attributes.mdx)
- ✅ Complete helpers reference (helpers-reference.mdx)
- ✅ Interactive examples gallery (featured-examples.mdx)

**Remaining priorities** should focus on:
1. API documentation (enables developers)
2. Complete syntax reference (essential for all users)
3. Deployment guide (enables story publishing)
4. Troubleshooting guide (reduces support burden)

Addressing these remaining gaps would transform Squiffy from a tool with good user guides to one with **comprehensive, professional documentation** suitable for both casual creators and serious developers.
