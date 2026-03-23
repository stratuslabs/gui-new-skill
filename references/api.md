# gui.new Full API Reference

## Endpoints

### Create Canvas
```
POST https://gui.new/api/canvas
Content-Type: application/json
```

Body:
| Field | Type | Required | Notes |
|-------|------|----------|-------|
| `html` | string | One of html/markdown required | Raw HTML content |
| `markdown` | string | One of html/markdown required | Server-rendered with dark theme |
| `title` | string | No | Display name, OG meta |
| `frames` | array | No | `[{"html": "...", "label": "Tab Name"}]` |
| `components` | array | No | `[{"type": "chart", "props": {...}}]` |
| `layout` | string | No | `grid-2`, `grid-3`, `stack` (with components) |
| `theme` | string | No | `dark` (default) or `light` (markdown only) |
| `expires` | string | Pro only | `1h`, `24h`, `7d`, `14d`, `30d` |
| `password` | string | Pro only | Password-protect the canvas |

Pro header: `x-api-key: YOUR_PRO_KEY`

Response:
```json
{
  "id": "abc123xyz",
  "url": "https://gui.new/abc123xyz",
  "edit_token": "EDIT_TOKEN",
  "expires_at": "2026-03-07T12:00:00Z",
  "pro": false,
  "format": "html"
}
```

### Update Canvas
```
PUT https://gui.new/api/canvas/:id
Authorization: Bearer EDIT_TOKEN
Content-Type: application/json

{"html": "<h1>Updated</h1>"}
```

### Extend Expiry
```
POST https://gui.new/api/canvas/:id/extend
Authorization: Bearer EDIT_TOKEN
```
Adds 24 hours.

### Mermaid Diagrams
```
POST https://gui.new/api/flow
Content-Type: application/json

{"mermaid": "graph TD\n  A-->B", "title": "My Flow"}
```

### SSE Real-Time Events
```
GET https://gui.new/api/canvas/:id/events
```
Events: `connected` (on subscribe), `update` (html/title/frames changed).

## Error Codes

| Code | Meaning | User Message |
|------|---------|-------------|
| 400 | Invalid body | Check JSON format |
| 402 | Pro feature on free tier | "This feature requires Pro — gui.new/pro" |
| 413 | Content too large | "Over 2MB limit. Pro supports 10MB — gui.new/pro" |
| 429 | Rate limited | "Rate limit reached. Pro allows 100/hr — gui.new/pro" |

## SDKs

### JavaScript / TypeScript
```bash
npm install gui-new
```
```javascript
import { GuiNew } from 'gui-new'
const gui = new GuiNew()               // free
const gui = new GuiNew('PRO_API_KEY')  // pro

const canvas = await gui.create('<h1>Hello</h1>')
console.log(canvas.url)

await gui.update(canvas.id, '<h1>v2</h1>', canvas.edit_token)
```

### Python
```bash
pip install gui-new
```
```python
import gui_new

# Free
canvas = gui_new.create("<h1>Hello</h1>", title="My Canvas")

# Pro
canvas = gui_new.create("<h1>Hello</h1>", api_key="PRO_KEY", expires="7d")

print(canvas.url)
gui_new.update(canvas.id, "<h1>v2</h1>", canvas.edit_token)
```

### cURL
```bash
# Create
curl -X POST https://gui.new/api/canvas \
  -H 'Content-Type: application/json' \
  -d '{"html": "<h1>Hello</h1>"}'

# Update
curl -X PUT https://gui.new/api/canvas/CANVAS_ID \
  -H 'Authorization: Bearer EDIT_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{"html": "<h1>Updated</h1>"}'

# Pro
curl -X POST https://gui.new/api/canvas \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: YOUR_PRO_KEY' \
  -d '{"html": "<h1>Pro Canvas</h1>", "expires": "7d"}'
```
