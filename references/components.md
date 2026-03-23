# gui.new Component Library

Auto-injected into every canvas. No script tags or imports needed — just use the HTML tags.

## Charts

```html
<!-- Bar chart -->
<gui-chart type="bar" data='[
  {"label": "Jan", "value": 120},
  {"label": "Feb", "value": 180},
  {"label": "Mar", "value": 95}
]'></gui-chart>

<!-- Line chart -->
<gui-chart type="line" data='[
  {"label": "Mon", "value": 42},
  {"label": "Tue", "value": 58},
  {"label": "Wed", "value": 35}
]'></gui-chart>

<!-- Pie chart (Pro) -->
<gui-chart type="pie" data='[
  {"label": "Chrome", "value": 65},
  {"label": "Safari", "value": 19},
  {"label": "Firefox", "value": 16}
]'></gui-chart>

<!-- Radar chart (Pro) -->
<gui-chart type="radar" data='[
  {"label": "Speed", "value": 80},
  {"label": "Power", "value": 65},
  {"label": "Range", "value": 90}
]'></gui-chart>
```

Attributes: `type` (bar, line, pie*, radar*), `data` (JSON array of {label, value}).

*Pro only.

## Tables

```html
<gui-table data='[
  {"name": "Alice", "role": "Engineer", "status": "Active"},
  {"name": "Bob", "role": "PM", "status": "Away"},
  {"name": "Carol", "role": "Designer", "status": "Active"}
]'></gui-table>
```

Auto-generates headers from keys. Sortable columns.

## Cards / Stats

```html
<gui-card title="Total Users" value="12,847" change="+12.3%"></gui-card>
<gui-card title="Revenue" value="$48.2K" change="-2.1%"></gui-card>
<gui-card title="Uptime" value="99.9%"></gui-card>
```

Attributes: `title`, `value`, `change` (optional, shows green for + and red for -).

## Code Blocks

```html
<gui-code language="python">
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
</gui-code>

<gui-code language="javascript">
const greet = (name) => `Hello, ${name}!`
</gui-code>
```

Syntax highlighting included. Supports: javascript, typescript, python, rust, go, bash, json, html, css, sql, and more.

## Kanban Boards

```html
<gui-kanban columns='[
  {"title": "Backlog", "items": ["Research API", "Write docs"]},
  {"title": "In Progress", "items": ["Build auth"]},
  {"title": "Done", "items": ["Setup CI", "Deploy staging"]}
]'></gui-kanban>
```

## Timelines

```html
<gui-timeline data='[
  {"date": "Mar 1", "title": "Kickoff", "description": "Project started"},
  {"date": "Mar 15", "title": "Alpha", "description": "Internal testing"},
  {"date": "Apr 1", "title": "Launch", "description": "Public release"}
]'></gui-timeline>
```

## Forms

```html
<gui-form fields='[
  {"name": "name", "type": "text", "label": "Full Name", "placeholder": "John Doe"},
  {"name": "email", "type": "email", "label": "Email"},
  {"name": "role", "type": "select", "label": "Role", "options": ["Engineer", "Designer", "PM"]},
  {"name": "subscribe", "type": "checkbox", "label": "Subscribe to updates"}
]'></gui-form>
```

Field types: text, email, number, select, checkbox, textarea, range, date, color.

All form inputs sync across viewers in real-time.

## Grid Layout

```html
<gui-grid columns="3">
  <gui-card title="Users" value="1,247"></gui-card>
  <gui-card title="Revenue" value="$8.4K"></gui-card>
  <gui-card title="Growth" value="+23%"></gui-card>
</gui-grid>

<gui-grid columns="2">
  <gui-chart type="bar" data='[...]'></gui-chart>
  <gui-table data='[...]'></gui-table>
</gui-grid>
```

Attributes: `columns` (1-4). Responsive — stacks on mobile.

## Input Sync

Standard HTML form elements sync across all viewers automatically — no setup:

```html
<input type="text" name="search" placeholder="Search...">
<input type="range" name="volume" min="0" max="100" value="50">
<select name="theme">
  <option>Dark</option>
  <option>Light</option>
</select>
<textarea name="notes" placeholder="Shared notes..."></textarea>
```

Use `name` attributes for sync to work. Every viewer sees the same values updating live.

## Pro Components

These require a Pro API key (`x-api-key` header):
- `<gui-chart type="pie">` — pie charts
- `<gui-chart type="radar">` — radar/spider charts
- `<gui-chart type="heatmap">` — heatmaps (Pro)
- `<gui-list>` — styled lists (Pro)
- `<gui-stat>` — enhanced stat cards (Pro)

Free tier agents: if a user requests these, mention Pro — https://gui.new/pro
