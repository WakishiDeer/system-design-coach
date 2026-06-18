# Mermaid Diagram Palette

Copy-paste building blocks for system-design diagrams, color-matched to
[`diagram-palette.drawio`](./diagram-palette.drawio). Same conventions: **components colored by
type, edges coded by direction** — write = red, read = green, async = dashed purple, optional =
dotted gray.

> Mermaid renders in VS Code's Markdown preview and on GitHub — no extension needed. You edit the
> text; the coach reads and grades it directly.

## 1. Copy-paste skeleton (start here)

Copy the whole block, delete what you don't need, and rewire the arrows.

```mermaid
flowchart LR
    client([Client])
    lb[Load Balancer]
    svc[Service]
    cache(Cache)
    store[("Database / Store")]

    client -->|request| lb
    lb --> svc
    svc -->|read| cache
    cache -.->|miss| store
    svc -->|write| store

    %% direction coding (edges counted from 0 in source order)
    linkStyle 2 stroke:#82b366,stroke-width:2px
    linkStyle 3 stroke:#82b366,stroke-width:1.5px,stroke-dasharray:4 3
    linkStyle 4 stroke:#b85450,stroke-width:2px

    %% component coding (type = color)
    classDef lb fill:#dae8fc,stroke:#6c8ebf
    classDef svc fill:#d5e8d4,stroke:#82b366
    classDef cache fill:#fff2cc,stroke:#d6b656
    classDef store fill:#f8cecc,stroke:#b85450
    class lb lb
    class svc svc
    class cache cache
    class store store
```

## 2. Component palette (copy a styled node)

Each node carries its type's color via an inline `:::class`. Copy any node line plus its matching
`classDef`.

```mermaid
flowchart LR
    client([Client]):::client
    lb[Load Balancer]:::lb
    svc["Service - stateless"]:::svc
    cache("Cache / Redis"):::cache
    store[("Database / Store")]:::store
    queue[[Message Queue]]:::queue
    cdn["CDN / Edge"]:::cdn
    gw["API Gateway / Rate limiter"]:::gw
    ext["External / 3rd-party"]:::ext

    classDef client fill:#ffffff,stroke:#333333
    classDef lb fill:#dae8fc,stroke:#6c8ebf
    classDef svc fill:#d5e8d4,stroke:#82b366
    classDef cache fill:#fff2cc,stroke:#d6b656
    classDef store fill:#f8cecc,stroke:#b85450
    classDef queue fill:#ffe6cc,stroke:#d79b00
    classDef cdn fill:#b0e3e6,stroke:#0e8088
    classDef gw fill:#e1d5e7,stroke:#9673a6
    classDef ext fill:#f5f5f5,stroke:#666666,stroke-dasharray:5 5
```

| Type | Node shape | `classDef` fill / stroke |
| --- | --- | --- |
| Client | `([Client])` stadium | `#ffffff` / `#333333` |
| Load Balancer / network | `[Load Balancer]` rect | `#dae8fc` / `#6c8ebf` (blue) |
| Service (stateless) | `[Service]` rect | `#d5e8d4` / `#82b366` (green) |
| Cache | `(Cache)` rounded | `#fff2cc` / `#d6b656` (yellow) |
| Database / Store | `[(Store)]` cylinder | `#f8cecc` / `#b85450` (red) |
| Message Queue | `[[Queue]]` subroutine | `#ffe6cc` / `#d79b00` (orange) |
| CDN / Edge | `[CDN]` rect | `#b0e3e6` / `#0e8088` (teal) |
| Gateway / Rate limiter | `[Gateway]` rect | `#e1d5e7` / `#9673a6` (purple) |
| External / 3rd-party | `[External]` rect | `#f5f5f5` / `#666666` dashed (gray) |

## 3. Edge conventions (direction = line + color)

```text
write            A -->|write| B        solid  red     stroke:#b85450
read             A -->|read| B         solid  green   stroke:#82b366
async / event    A -.->|async| B       dashed purple  stroke:#9673a6
optional / back  A -.->|optional| B    dotted gray    stroke:#999999
```

`linkStyle` is **index-based** — edges are numbered 0, 1, 2… in source order. Add the styles after
the edges:

```mermaid
flowchart LR
    a[Service] -->|write| b[("Store")]
    a -->|read| c(Cache)
    a -.->|async| d[[Queue]]
    linkStyle 0 stroke:#b85450,stroke-width:2px
    linkStyle 1 stroke:#82b366,stroke-width:2px
    linkStyle 2 stroke:#9673a6,stroke-width:2px
```

## 4. Data model (erDiagram) starter

```mermaid
erDiagram
    URL ||--o{ CLICK : has
    URL {
        string code PK
        string original_url
        datetime expires_at
    }
    CLICK {
        string id PK
        string code FK
        datetime ts
    }
```
