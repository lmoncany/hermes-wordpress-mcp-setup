# hermes-wordpress-mcp-setup

![hero](assets/hero.png)

A [Hermes Agent](https://github.com/NousResearch/hermes-agent) skill that connects your AI agent to WordPress + Elementor via MCP (Model Context Protocol).

Build pages, edit layouts, update global styles, manage templates, inject code snippets — all through natural language. No clicking required.

---

## 📦 Install

```bash
hermes skills tap add lmoncany/hermes-wordpress-skill
hermes skills install wordpress-mcp-setup
```

Then load it in a session:

```bash
hermes -s wordpress-mcp-setup
```

Or inside a running session:

```
/skill wordpress-mcp-setup
```

---

## 🚀 Onboarding

Once the skill is loaded, run the onboarding to connect your site:

```
Set up my WordPress site with MCP
```

The agent will:
1. Ask for your site URL, username, and Application Password
2. Detect which MCP plugins are already installed and active
3. Offer to install and activate any missing plugins via the WP REST API
4. Generate your `config.yaml` MCP server entries automatically
5. Confirm what tools are now available (`mcp_wordpress_*`, `mcp_elementor_*`)

---

## ✅ Requirements

### WordPress Plugins

| Plugin | Where to get it | Required for |
|--------|----------------|-------------|
| **MCP Adapter** | [github.com/WordPress/mcp-adapter](https://github.com/WordPress/mcp-adapter) | Core MCP endpoint — **required** |
| **WordPress MCP** | WordPress.org plugin directory | Posts, pages, users, media, settings — **required** |
| **MCP Tools for Elementor** | WordPress.org plugin directory | All Elementor MCP tools — optional |
| **Elementor** | WordPress.org plugin directory | Required only if using Elementor tools |
| **Elementor Pro** | [elementor.com](https://elementor.com) | Pro widgets, theme builder, popups, dynamic tags — optional |

> The onboarding flow can automatically install and activate free plugins from WordPress.org. Elementor Pro requires a manual license-based install.

### Hermes Agent

- Hermes Agent installed → [installation guide](https://hermes-agent.nousresearch.com/docs/)
- `mcp` Python package supporting the 2025-06-18 spec (StreamableHTTP transport)

---

## 🔧 What It Covers

### Setup (step-by-step)
- Verify MCP plugins are active on your WP site
- Discover MCP endpoint routes
- Generate Basic Auth header from your WP Application Password
- Configure both MCP servers in `~/.hermes/config.yaml`
- Handle SSL issues for local dev environments (ServBay, LocalWP, MAMP, etc.)

### WordPress MCP
- Ability-based API: discover → inspect → execute any WP operation
- Posts, pages, users, media, settings and more

### Elementor MCP (100 tools)
- **Discovery** — list widgets, schemas, pages, templates, dynamic tags
- **Read** — get full page structure, find elements, read settings
- **Build** — create pages, add containers, add any widget
- **Edit** — update elements, batch-update, move, duplicate, remove
- **Templates** — save/apply templates, create theme builder templates (header, footer, archive, 404...)
- **Global styles** — update site-wide color palette and typography
- **Popups** — create and configure Elementor Pro popups
- **Dynamic tags** — bind dynamic data to any element setting
- **Media** — search CC-licensed images (Openverse), sideload to media library
- **Custom code** — inject CSS/JS per element or site-wide

---

## 💡 Example Workflows

**Build a full page in one call:**
```
mcp_elementor_elementor-mcp-build-page { "title": "Landing Page", "structure": [ ... ] }
```

**Inspect then edit an existing page:**
```
1. elementor-mcp-list-pages
2. elementor-mcp-get-page-structure  { "post_id": 42 }
3. elementor-mcp-find-element        { "post_id": 42, "widget_type": "heading" }
4. elementor-mcp-update-widget       { "post_id": 42, "element_id": "abc123", "settings": { "title": "New Title" } }
```

**Update brand colors globally:**
```
elementor-mcp-update-global-colors {
  "colors": [
    { "id": "primary", "title": "Primary", "color": "#FF6B35" },
    { "id": "secondary", "title": "Secondary", "color": "#1A1A2E" }
  ]
}
```

---

## 👤 Author

**Loic Moncany** — [github.com/lmoncany](https://github.com/lmoncany)

---

## 📄 License

MIT
