An interactive map that displays the service area for Same Day Garage Door Services and allows users to check if their address is within the service area. 

Hosted on GitHub Pages: https://4thstagency.github.io/Maps/

## Configuration

Configurable constants are listed in `index.html` under the "Configurable constants" section:

| Constant | Description |
|----------|-------------|
| `API_KEY` | Your MapTiler public API key |
| `style` | The map style URL (MapTiler style.json) |
| `getServiceTarget` | The target URL for the "Get Service Now" button |

## Map Data

The service area is loaded from an external file in the `assets/` folder. The script will look for:

1. **`assets/map.geojson`** (primary)
2. **`assets/map.csv`** (fallback)

### GeoJSON Format

The GeoJSON file should contain either:
- A `Feature` with a `Polygon` geometry, or
- A `FeatureCollection` (the first feature will be used)

```json
{
  "type": "Feature",
  "properties": {},
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-112.0, 33.0], [-111.5, 33.0], [-111.5, 33.5], [-112.0, 33.5], [-112.0, 33.0]]]
  }
}
```

Use a tool like [geojson.studio](https://geojson.studio) to create or edit GeoJSON polygons.

### CSV Format (Google MyMaps Export)

The CSV fallback supports exports from Google MyMaps with WKT geometry. The script will:

1. Look for the first `POLYGON` geometry, or
2. Collect all `LINESTRING` geometries with matching names and chain them into a polygon

**To export from Google MyMaps:**
1. Open your map in Google MyMaps
2. Click the three-dot menu (⋮) on the layer containing your service area
3. Select **Export data → CSV**
4. Save as `assets/map.csv`

The script automatically handles:
- LineStrings that are out of order in the CSV
- LineStrings that need to be reversed to connect properly
- Small gaps between LineString endpoints
