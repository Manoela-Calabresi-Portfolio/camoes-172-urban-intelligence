# CamÃµes 172 â€” Urban Intelligence

Territorial intelligence and WebGIS case study for real-estate decision-making.

This portfolio page shows the full system, not just a map demo: cadastral and regulatory reading, urban context, market intelligence, scenario design, interactive viewer, and the editorial dossier used to present the project.

## Project at a glance

| Item | Summary |
| --- | --- |
| Territory | CamÃµes 172 |
| Goal | Translate territory into a product and scale decision |
| Main output | WebGIS viewer + editorial dossier |
| 2D engine | Leaflet in the browser |
| Complement | MapLibre scenes for selected 3D / contextual views |
| Data base | PostGIS, GeoJSON, public datasets, OSM, LiDAR, market layers |

## What the project demonstrates

- A complete territorial workflow, from parcel diagnosis to final recommendation.
- Integration of public spatial data, curated layers, and market signals.
- A clear way to read urban context, accessibility, morphology, and product potential.
- An interface that turns analysis into a client-ready story.

## End-to-end workflow

1. Spatial data is organized in `PostGIS`.
2. Analysis views and export tables are published for delivery.
3. Python scripts export the relevant layers to `GeoJSON` and `JSON`.
4. The browser viewer loads those files and renders the 2D map in `Leaflet`.
5. Icons, colors, tooltips, and popups are handled in the viewer logic.
6. The HTML dossier embeds the viewer and organizes the narrative.
7. `MapLibre` appears in complementary 3D or contextual scenes when needed.

In other words: the database prepares the truth, the viewer renders it, and the dossier frames it for decision.

## What is inside the dossier

The CamÃµes reading path is structured as a decision funnel:

- `T0` - parcel, ownership, legal base, allowed uses, and core constraints
- `T1` - urban insertion, accessibility, centralities, and spatial context
- `T2` - market reading, comparables, demand, value, and positioning
- `T3` - envelope, buildability, and development potential
- `T4` - product scenarios, recommendation, and next steps

This is why the project is more than a map: it is a decision system.

## Viewer features

- Interactive layers by theme
- Custom markers and SVG icons
- Tooltips and popups tied to feature attributes
- Layer toggles and thematic legends
- Contextual 2D maps for territory reading
- Complementary 3D scenes where a second level of understanding is useful

The important distinction is that the visual elements live in the viewer logic, while the dossier HTML acts as the editorial wrapper.

## My role

I led the framing, the data selection, the reading structure, and the validation of what should be shown.

That means I was responsible for:

- deciding which layers mattered for the story
- organizing the project from diagnosis to recommendation
- shaping the narrative for client presentation
- checking that the output was legible and defensible
This is the part of the work I would highlight in a meeting: the project direction, the editorial judgment, and the ability to turn territory into a clear decision story.

## Stack

- `PostGIS`
- `SQL`
- `Python`
- `GeoJSON`
- `Leaflet`
- `MapLibre`
- `HTML / CSS / JavaScript`
- `WMS / WFS`
- `OSM`
- public cadastral and urban data sources

## Why this matters

CamÃµes 172 is the piece I would use to show that the work is not only technical.

It combines:

- urbanism
- territory
- cartography
- spatial systems
- product thinking
- and communication for decision-makers

That combination is the core value of the project.

## Suggested way to present it

If you need a short explanation in a meeting:

> I structured CamÃµes 172 as a territorial intelligence workflow: data goes into PostGIS, relevant layers are published and exported, the viewer renders the map in Leaflet, and the HTML dossier turns that analysis into a clear product decision narrative.
> My role was to frame the problem, curate the layers, and validate what should be shown.

## Visual references

![Pipeline overview](https://github.com/user-attachments/assets/cc7cadad-9dac-464c-91fd-e01854626077)

![Pipeline phases](https://github.com/user-attachments/assets/083472a4-7c8e-4f90-afcd-cd45ad0bbb0e)

![Viewer overview](https://github.com/user-attachments/assets/d6c2b30b-e13e-4df0-a25b-7050e2ca1ddb)

---

Built as part of the Ombu territorial intelligence workflow for real-estate decision support.
