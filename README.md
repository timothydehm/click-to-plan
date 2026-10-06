# Land Use Planner

A lightweight, browser-based interactive mapping tool built with Leaflet.js that allows urban planners, researchers, or city officials to visualize and assign land use categories to local parcels. 

## Features

* **Interactive Map Interface:** View parcels on a responsive map with toggleable basemaps (Simple/Light, Satellite, and Streets).
* **Click-to-Assign Land Use:** Simply click on any parcel polygon to cycle through different land use categories (Unassigned, Green Space, Residential, Commercial, Other).
* **Real-time Analytics:** A dynamic legend automatically tracks the number of parcels and calculates the total acreage assigned to each land use category.
* **Version Control (Branching):** Create new "versions" of your map to experiment with different zoning scenarios without overwriting your main data.
* **Import/Export Data:** Save your current land use assignments by downloading them as a new GeoJSON file, or upload an existing GeoJSON to resume work.

## Setup & Installation

This application runs entirely in the browser using HTML, CSS, and vanilla JavaScript. However, because it fetches a local JSON file on startup, you must run it through a local web server to avoid CORS (Cross-Origin Resource Sharing) errors.

1. **Place your files in a single directory:**
   Ensure your `index.html` (the app) and your starting data file (`City_Landbank_2552617068183058004.geojson`) are in the same folder.
2. **Start a local web server:**
   * **Using Python:** Open your terminal in the folder and run `python -m http.server 8000` (or `python3 -m http.server 8000`).
   * **Using VS Code:** Install the "Live Server" extension, right-click the HTML file, and select "Open with Live Server".
   * **Using Node.js:** Run `npx http-server`.
3. **Open the app:** Navigate to `http://localhost:8000` in your web browser.

## Data Requirements

The application relies on standard **GeoJSON** formatted data. To take full advantage of the analytics engine, the `properties` object of your GeoJSON features should ideally contain:

* `landUse` *(String)*: The current category. Matches to 'Unassigned', 'Green Space', 'Residential', 'Commercial', or 'Other'.
* `total_square_ft` *(Number)*: The square footage of the parcel, used to dynamically calculate the acreage shown in the control panel.

## Usage Guide

1. **Assigning Categories:** Click on any gray (Unassigned) parcel on the map. It will instantly turn green (Green Space). Click again to cycle to blue (Residential), orange (Commercial), gray (Other), and back to white (Unassigned).
2. **Testing Scenarios:** Want to see what a neighborhood looks like with more commercial zoning, but don't want to ruin your current map? Look at the **Version Control** panel. Click **Create New Version**, give it a name (e.g., "proposal-A"), and make your changes. You can switch back and forth using the dropdown menu.
3. **Saving Work:** Under **Save/Load Data**, click **Download GeoJSON**. This will export the *currently selected version* of your map to your computer, appending the date and branch name to the file.
4. **Changing Basemaps:** Use the layer icon in the top right corner of the map to switch between Simple, Satellite, and Street views.

## Technical Stack

* **Frontend:** HTML5, CSS3, Vanilla JavaScript
* **Mapping Library:** [Leaflet.js](https://leafletjs.com/) (v1.9.4)
* **Basemaps Provided by:** CARTO, Esri, OpenStreetMap

## Limitations / Configurations

* **Category Limits:** By default, the code enforces a limit of `5000` parcels for Residential and Commercial categories. You can modify the `landUseLimits` object in the `<script>` tag to adjust or remove these constraints.
* **Map Centering:** The default map view is centered on Cleveland, Ohio `[41.49, -81.68]` at zoom level `13`. If you load data for a different city, you may want to update the `L.map('map').setView(...)` coordinates.
