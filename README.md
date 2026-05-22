# Camões 172 — Urban Intelligence

Territorial intelligence workflow for real-estate decision-making.

![Architecture overview](https://github.com/user-attachments/assets/5f1b282c-aeec-4647-a567-9bf0973f1fa6)

<details>
<summary><strong>Runtime registry</strong> - central dataset contract used by the viewer</summary>

```javascript
// Central dataset registry — every map layer is declared here.
// Derived datasets (block-level metrics) are computed from base GeoJSON
// rather than stored as separate files, keeping exports minimal.

const DATASETS = Object.freeze({
  // Urban context
  edificacoes:          { file: 'footprints_1000m.geojson' },
  t1_03_alturas:        { file: 't1_03_building_height_02.geojson' },
  t1_04_intensidade:    { file: 't1_04_built_density_02.geojson' },
  t1_05_tipologias:     { file: 't1_05_morphology_type_02.geojson' },
  zoneamento_aoi:       { file: 'zoneamento_aoi.geojson' },

  // Market data (updated monthly from HOT pipeline)
  hotspots_venda:               { file: 'hotspots_venda.geojson' },
  hotspots_venda_basefina_novo:  { file: 'hotspots_venda_basefina_novo.geojson' },
  s7_developments_points:        { file: 's7_developments_points.geojson' },
  s7_market_points_total:        { file: 's7_market_points_total.geojson' },
  aoi_submercado:                { file: 'aoi_t02_submercado_camoes.geojson' },

  // Derived: block-level density computed from building footprints at runtime
  t1_04_quadras: {
    derived: () => buildBlockMetricGeojson({
      dataset: 't1_04_intensidade',
      metricFields: ['densidade_construida_m2_ha'],
      outputField:  'densidade_construida_m2_ha'
    })
  },
});

// Runtime base URL resolution: probes for a known file across candidate paths.
// Works identically in local dev (Live Server) and production (GitHub Pages / R2).
async function getResolvedDataBase() {
  const primary   = new URL('../../data/map_geojson/', window.location.href);
  const candidates = [primary];

  const probeFile = 'lote_camoes.geojson';
  for (const base of candidates) {
    const url = new URL(probeFile, base);
    try {
      const r = await fetch(url.href, { method: 'HEAD', cache: 'no-store' });
      if (r.ok) { resolvedDataBase = base; return base; }
    } catch (_) { /* try next */ }
  }
  return primary; // fallback — will surface 404s clearly in the network tab
}
```
</details>

## At a glance

| Item | Summary |
| --- | --- |
| Territory | Camões 172 |
| Goal | Translate territory into a product and scale decision |
| Main output | WebGIS viewer + editorial dossier |
| 2D engine | Leaflet in the browser |
| Complement | MapLibre scenes for selected 3D / contextual views |
| Data base | PostGIS, GeoJSON, public datasets, OSM, LiDAR, market layers |

## What the system shows

- End-to-end territorial workflow from parcel diagnosis to final recommendation
- Integration of public spatial data, curated layers, and market signals
- Urban context, accessibility, morphology, and product potential in one reading path
- A client-ready interface that turns analysis into a decision story

## Reading path

| Stage | Focus |
| --- | --- |
| `T0` | Parcel, ownership, legal base, allowed uses, core constraints |
| `T1` | Urban insertion, accessibility, centralities, spatial context |
| `T2` | Market reading, comparables, demand, value, positioning |
| `T3` | Envelope, buildability, development potential |
| `T4` | Product scenarios, recommendation, next steps |

## End-to-end flow

1. Spatial data is organized in `PostGIS`.
2. Analysis views and export tables are published for delivery.
3. Python scripts export relevant layers to `GeoJSON` and `JSON`.
4. The browser viewer renders the 2D map in `Leaflet`.
5. Icons, colors, tooltips, and popups are handled in viewer logic.
6. The HTML dossier embeds the viewer and organizes the narrative.
7. `MapLibre` appears in complementary 3D or contextual scenes when needed.

## Viewer features

- Interactive layers by theme
- Custom markers and SVG icons
- Tooltips and popups tied to feature attributes
- Layer toggles and thematic legends
- Contextual 2D maps for territory reading
- Complementary 3D scenes when a second layer of understanding is useful

## My role

- I framed the problem and selected the layers that mattered
- I organized the project from diagnosis to recommendation
- I shaped the narrative for client presentation
- I validated that the output was legible and defensible

## Why this matters

- Urbanism
- Territory
- Cartography
- Spatial systems
- Product thinking
- Communication for decision-makers

That combination is the core value of the project.

## Suggested way to present it

> I structured Camões 172 as a territorial intelligence workflow: data goes into PostGIS, relevant layers are published and exported, the viewer renders the map in Leaflet, and the HTML dossier turns that analysis into a clear product decision narrative.

> My role was to frame the problem, curate the layers, and validate what should be shown.

## Visual references

![Pipeline phases](https://github.com/user-attachments/assets/083472a4-7c8e-4f90-afcd-cd45ad0bbb0e)

![Viewer overview](https://github.com/user-attachments/assets/d6c2b30b-e13e-4df0-a25b-7050e2ca1ddb)

---

Built as part of the Ombu territorial intelligence workflow for real-estate investment decisions.
