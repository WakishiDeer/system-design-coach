# API Design Template — copy & fill

Copy this into your `design/vN.md` (or a scratch file) during the **API design** phase and fill
it in. The point: *you* control everything — verbs, status codes, **headers**, idempotency,
pagination — unlike fill-in-the-box tools.

> Tip: keep it small. Define the 2–4 endpoints that matter for the core flow, not every CRUD.

## A. Endpoint summary

| Method | Path | Purpose | Auth | Idempotent? |
| ------ | ---- | ------- | ---- | ----------- |
| POST | /api/v1/… | create … | Bearer | via Idempotency-Key |
| GET | /api/v1/…/{id} | read … | Bearer | yes (safe) |
| GET | /api/v1/… | list … (paginated) | Bearer | yes (safe) |

## B. Per-endpoint detail (copy this block per endpoint)

### `POST /api/v1/<resource>`

- **Purpose:**
- **Auth:** `Authorization: Bearer <token>`
- **Request headers:**
  - `Content-Type: application/json`
  - `Idempotency-Key: <uuid>`   # safe retries, no duplicate writes
- **Request body:**

  ```json
  { "field": "value" }
  ```

- **Responses:**
  - `201 Created` — `Location: /api/v1/<resource>/{id}`

    ```json
    { "id": "…", "field": "value" }
    ```

  - `400 Bad Request` — validation error (see error format in §C)
  - `401 Unauthorized` / `403 Forbidden`
  - `409 Conflict` — duplicate / idempotency replay
  - `429 Too Many Requests` — `Retry-After: <seconds>`
- **Notes:** side effects? async (202 + status URL)?

### `GET /api/v1/<resource>?cursor=&limit=`

- **Purpose:** list (paginated)
- **Query:** `limit` (default 20, max 100), `cursor` (opaque)
- **Response `200 OK`:**
  - Headers: `Cache-Control: …`
  - Body:

    ```json
    { "items": [ ], "nextCursor": "<opaque>" }
    ```

- **Pagination:** cursor-based (stable under inserts) — prefer over offset.

## C. Cross-cutting conventions (fill once)

- **Versioning:** URL `/api/v1/…` (or header `Accept: application/vnd.app.v1+json`).
- **Auth:** Bearer / JWT? API key? scopes?
- **Error format (keep it consistent):**

  ```json
  { "error": { "code": "RESOURCE_NOT_FOUND", "message": "…", "requestId": "…" } }
  ```

- **Rate-limit headers:** `X-RateLimit-Limit` / `-Remaining` / `-Reset`, plus `Retry-After` on 429.
- **Pagination style:** cursor (default) vs offset; default & max page size.
- **Idempotency:** which writes accept `Idempotency-Key`?

---

## D. (Optional) OpenAPI / Swagger — run it locally

Prefer a real spec you can render and click through? Copy this minimal starter into `openapi.yaml`:

```yaml
openapi: 3.0.3
info:
  title: <Service> API
  version: 1.0.0
servers:
  - url: https://api.example.com
paths:
  /api/v1/resource:
    post:
      summary: Create a resource
      parameters:
        - in: header
          name: Idempotency-Key
          required: false
          schema: { type: string, format: uuid }
      requestBody:
        required: true
        content:
          application/json:
            schema: { $ref: '#/components/schemas/ResourceInput' }
      responses:
        '201':
          description: Created
          headers:
            Location: { schema: { type: string } }
          content:
            application/json:
              schema: { $ref: '#/components/schemas/Resource' }
        '429':
          description: Too Many Requests
          headers:
            Retry-After: { schema: { type: integer } }
components:
  schemas:
    ResourceInput:
      type: object
      required: [name]
      properties:
        name: { type: string }
    Resource:
      type: object
      properties:
        id: { type: string }
        name: { type: string }
```

### Edit it hands-on with a live Swagger UI

Swagger UI itself is **view-only** — to *edit* with a live preview, pick one and go:

**A) In VS Code (stays in your editor):**

1. Install the extension: `code --install-extension 42Crunch.vscode-openapi`
2. Open `openapi.yaml`, then click **Preview** (top-right) for a live Swagger UI / ReDoc.
3. Edit with IntelliSense; use **"Try it"** to exercise an endpoint.

**B) In the browser (zero install):**

1. Open <https://editor.swagger.io> (or local `docker run --rm -p 8080:8080 swaggerapi/swagger-editor`).
2. Paste your `openapi.yaml` on the left — live Swagger UI renders on the right.
3. Edit, then save it back to `design/openapi.yaml`.

### View-only preview

- **Redocly (ReDoc):** `npx @redocly/cli preview-docs openapi.yaml` → `http://localhost:8080`.
- **Swagger UI (docker):** `docker run --rm -p 8080:8080 -e SWAGGER_JSON=/spec/openapi.yaml -v ${PWD}:/spec swaggerapi/swagger-ui`

### Make the spec your API answer

Prefer editing the spec over markdown? **Submit `openapi.yaml` as your API-design answer.** The
coach reads YAML and grades the **API design** dimension straight from it — save it as
`design/openapi.yaml` and reference it from your design doc.

> Scope: the spec covers the **API phase** only. You still cover requirements, estimation,
> architecture (draw.io or Mermaid), data model, and scaling for a full interview answer.
