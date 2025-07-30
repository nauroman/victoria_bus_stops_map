# Victoria Bus Stops — Interactive Map  
*Greater Victoria, British Columbia (Canada)*  

[**Live demo → victoria_bus_stops_map**](https://nauroman.github.io/victoria_bus_stops_map/)

---

## Project Overview
This repository delivers a **single‑page web map** (`index.html`) showing **every public‑transit stop** (≈ 2 500) in Greater Victoria, BC.  
The map is fully client‑side—no backend, database, or API key required.

---

## File Structure

| Path | Purpose |
|------|---------|
| **index.html** | Self‑contained web page with the Leaflet map and all markers. |
| **data/victoria_bus_stops.csv** | (Optional) Raw list of stops: OSM ID, name, latitude, longitude. |
| **scripts/** | Helper resources for regenerating data & map (not needed to view the map). |

Only `index.html` is required for end‑users; other files support reproducibility.

---

## Data Pipeline

| Step | Details |
|------|---------|
| **1 · Fetch stops** | OpenStreetMap Overpass API, bounding box 48.30 – 48.70 ° N, −123.80 – −123.00 ° W. Query selects nodes with `highway=bus_stop`, `public_transport=platform`, or `amenity=bus_station`. |
| **2 · Clean** | Duplicate coordinates removed; unnamed stops labelled “Unnamed stop \<OSM ID\>”. |
| **3 · Build map** | Leaflet + MarkerCluster. Base tiles from OpenStreetMap. Pop‑ups show stop name & OSM ID. |
| **4 · Deploy** | `index.html` committed to a GitHub Pages branch. GitHub serves the static map automatically. |

> **Why OpenStreetMap?**  
> While BC Transit publishes GTFS feeds, direct links are occasionally blocked by regional CORS/TLS rules. OpenStreetMap offers an open, consistently accessible fallback and is typically accurate within a few metres of official coordinates.

---

## CSV Schema

| Column | Example | Description |
|--------|---------|-------------|
| `id`   | 277640691 | OpenStreetMap node ID |
| `name` | Shelbourne at Feltham | Stop name; “Unnamed stop \<id\>” if blank in OSM |
| `lat`  | 48.4756411 | WGS‑84 latitude |
| `lon`  | −123.332597 | WGS‑84 longitude |

---

## Running Locally

1. **Clone** the repository  
   ```bash
   git clone https://github.com/your‑user/victoria_bus_stops_map.git
   cd victoria_bus_stops_map
