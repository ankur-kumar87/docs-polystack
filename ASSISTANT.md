# Xloud Documentation — Project Rules

## Stack
- **Platform**: Mintlify (docs-as-code)
- **Format**: MDX (Markdown + JSX components)
- **Config**: `docs.json` (site config, navigation, theme)
- **Branch strategy**: `main` = production, `staging` = working branch

## CRITICAL: NEVER commit or push. Make file edits only. Wait for the user to explicitly say "commit" or "push" before running any git command.

## CRITICAL: Always invoke `/mintlify` skill before creating or editing any documentation page.

## CRITICAL: Commit and push to `origin/staging` after EVERY change. Never batch multiple steps without pushing.

## CRITICAL: Never create documentation pages with invented content. Only write pages when the user provides source material (OpenStack doc links, screenshots, or explicit instructions).

## Branding
- **Company**: Xloud Technologies
- **Colors**: Primary `#197560`, Light `#3F8F7E`, Dark `#145C4C`
- **Fonts**: Gilroy (headings), Tenorite (body)
- **Products**: XAVS, XIMP, XHCI, XDR, XSDS, XNAS, XNexus, XOS
- **Support**: support@xloud.tech

## Documentation Authoring Standard

Every page in this repo MUST follow the enterprise documentation standard defined in:
- `.claude/doc-authoring-guidelines.mdx` — the canonical reference for all content rules

### Quick Rules (full detail in the guidelines file)

0. **ABSOLUTE: No emojis anywhere** — never use emojis in any MDX file, docs.json, or any other file in this repo. Not in text, not in descriptions, not in table cells, not anywhere.
1. **Never plain markdown** — every page uses rich Mintlify MDX components
2. **OpenStack → Xloud** — rebrand all OpenStack references
3. **KVM → hypervisor** — never mention KVM directly
4. **GUI/CLI tabs** — every procedural page has `<Tabs>` with Dashboard and CLI
5. **Enterprise tone** — AWS/Azure quality, no casual language
6. **Prerequisites** → **Overview** → **Content** → **Validation** → **Next Steps** structure
7. **Component density** — minimum 5+ MDX components per page (Steps, Tabs, CodeGroup, Callouts, Cards)
8. **Cross-links** — every page links to 2+ related pages, never orphan a page
9. **Always update `docs.json`** navigation when adding new pages

## File Structure
```
docs.json                    # Site configuration
introduction.mdx             # Landing page (homepage)
quickstart.mdx               # Quickstart — XDeploy deployment flow
authentication.mdx           # Dashboard login + CLI openrc auth
images/                      # Static assets (logo, favicon)
resources/                   # Fonts (Gilroy, Tenorite)
snippets/                    # Reusable MDX snippets
.claude/                     # Authoring guidelines
.mcp.json                    # Mintlify MCP server config
```

## Navigation
- Update `docs.json` → `navigation.groups[].pages[]` for every new page
- Page slugs are relative paths without `.mdx` extension
- Only add pages to navigation when they have real, verified content

## Commit Convention
- Prefix: `docs:` for content, `config:` for docs.json/meta changes
- Example: `docs: Add compute instances user guide`
