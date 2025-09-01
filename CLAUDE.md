# CLAUDE.md - Luke Route Globe Project Instructions

## 🚨 CRITICAL PROJECT REQUIREMENTS - DO NOT SIMPLIFY OR REMOVE

### PRIMARY GOAL
Create a high-fidelity 3D globe application for visualizing Luke's athletic routes (cycling and running) with **GOOGLE MAPS/GOOGLE EARTH LEVEL SATELLITE IMAGERY QUALITY**. This is the #1 priority and must never be compromised for "simplification".

### 🛰️ IMAGERY REQUIREMENTS (NON-NEGOTIABLE)
1. **HIGH-RESOLUTION SATELLITE IMAGERY** - Must provide 15cm resolution in urban areas
2. **Use Bing Maps Aerial imagery** (`BingMapsImageryProvider`) as primary source
3. **Maximum zoom level 20** for street-level detail
4. **Google Earth-quality visualization** - Users must be able to zoom from space to individual buildings
5. **NEVER simplify to basic Cesium Ion imagery** - this defeats the entire purpose

### 🌍 CORE TECHNICAL SPECIFICATIONS

#### Cesium Configuration (REQUIRED)
```javascript
// PRIMARY IMAGERY - NEVER CHANGE THIS TO "SIMPLE" ALTERNATIVES
imageryProvider: await Cesium.BingMapsImageryProvider.fromUrl('https://dev.virtualearth.net', {
    key: 'AqTGBsziZHIJYYxgivLBf0hVdrAk9mWO5cQcb8Yux8sW5M8c8opEC2lZqKR1ZZXf',
    mapStyle: Cesium.BingMapsStyle.AERIAL,
    maximumLevel: 20 // CRITICAL for detailed zoom
}),

// HIGH-RESOLUTION TERRAIN
terrainProvider: await Cesium.createWorldTerrainAsync({
    requestWaterMask: true,
    requestVertexNormals: true
}),
```

#### Globe Optimization Settings (REQUIRED)
- `globe.enableLighting = false` (better for satellite imagery)
- `globe.maximumScreenSpaceError = 1.5` (higher quality)
- `globe.tileCacheSize = 200` (performance with quality)
- `controller.minimumZoomDistance = 0.5` (allow extreme close-ups)
- `viewer.resolutionScale = 1.0` (full resolution rendering)

### 📍 APPLICATION FEATURES

#### User Interface Requirements
1. **Left Sidebar (350px width)**
   - Header: "🌍 Luke's Routes" 
   - Filter buttons: All, 🚴‍♂️ Cycling, 🏃‍♂️ Running
   - Statistics display: Routes, Distance, Time, Countries
   - Scrollable routes list with activity icons and details

2. **Main Globe Area**
   - Full-screen 3D Cesium globe
   - High-resolution satellite imagery
   - Interactive route overlays
   - Loading screen with spinner

#### Route Visualization Requirements
1. **Cycling routes: BLUE (#3b82f6)**
2. **Running routes: RED (#ef4444)**
3. **Route width: 6px with 0.9 alpha**
4. **Start markers: GREEN with "START" label**
5. **End markers: RED with "END" label**
6. **Routes must clamp to terrain**

### 🔗 STRAVA INTEGRATION (FUTURE)

#### API Framework Requirements
1. **StravaAPI class** with methods:
   - `authenticate()` - OAuth flow
   - `getActivities()` - Fetch user activities  
   - `getActivityStream(activityId)` - Get GPS coordinates
2. **Data transformation** from Strava format to route objects
3. **Real-time route loading** and caching

### 🎨 DESIGN SPECIFICATIONS

#### Color Scheme
- Background: `#1a1a2e` (dark blue-gray)
- Sidebar: `linear-gradient(180deg, #16213e 0%, #0f172a 100%)`
- Header: `linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%)`
- Text: White and light grays
- Accent: Blue (#3b82f6)

#### Responsive Design
- Mobile: Stack sidebar above globe (40vh/60vh)
- Desktop: Side-by-side layout
- Smooth animations and transitions

### 🚫 THINGS TO NEVER DO

1. **NEVER simplify imagery to basic Cesium Ion** - this removes the core value
2. **NEVER disable high-resolution settings** "for performance"
3. **NEVER remove Bing Maps provider** in favor of "simpler alternatives"
4. **NEVER reduce maximumLevel below 20**
5. **NEVER increase maximumScreenSpaceError above 2**
6. **NEVER enable lighting** (it interferes with satellite clarity)
7. **NEVER remove terrain water masks** (they enhance visual quality)

### 🎯 SUCCESS CRITERIA

The application is successful when:
1. Users can zoom from space to individual buildings/streets
2. Satellite imagery is crystal clear at all zoom levels  
3. Routes are clearly visible overlaid on realistic terrain
4. Cycling routes appear blue, running routes appear red
5. Interface is professional and responsive
6. Loading is smooth with proper progress indication
7. Ready for real Strava data integration

### 🛠️ DEVELOPMENT NOTES

#### Local Development Issues
- CORS errors are expected when running locally via `file://`
- Always test final version on GitHub Pages (HTTPS)
- URL handling errors resolve when served over HTTP/HTTPS

#### Performance Considerations
- Use `requestRenderMode: true` for explicit rendering
- Implement proper camera movement listeners
- Cache imagery tiles appropriately
- Request renders after route changes

#### Token Information
- Cesium Ion Token: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJjMjM3NTEzMi1mMDJmLTQyMDUtYjA5OC1jNmU0NDA3NDlmNWQiLCJpZCI6MzM2NzUyLCJpYXQiOjE3NTY1NTU2NzR9.AoxR_iV8YYTrhRnncxGBZQYyjfsaq5J2WckHrpB6wpA`
- GitHub Pages URL: `https://zshumake.github.io/luke-route-globe/`

## 🎯 CESIUM ION ACCOUNT OPTIMIZATION (2024 Best Practices)

### Account Setup Recommendations
1. **Monitor Usage Dashboard** regularly at https://ion.cesium.com/dashboard
2. **Use Sentinel-2 imagery** for development/testing to save Bing Maps sessions
3. **Avoid Bing Maps in automated tests** - each test run = 1 session
4. **Update to latest CesiumJS** for improved caching (currently using 1.111 ✓)
5. **Session Management**: One Bing Maps session per page load (optimized)

### Quota Management
- **Bing Maps Sessions**: Session-based billing, minimize with caching
- **Storage**: Use compressed formats, upload ZIP files
- **Data Streaming**: Enable WebP, optimize screen space error
- **Geocoding**: Disable if not needed to save quota

### Performance Optimizations Applied
1. **Explicit Rendering Mode** - `requestRenderMode: true`
2. **Dynamic Screen Space Error** - Optimized for horizon views  
3. **Logarithmic Depth Buffer** - Better precision at all zoom levels
4. **WebGL Anisotropic Filtering** - Enhanced imagery quality
5. **Optimized Tile Loading** - Better cache management and timeouts
6. **3D Tiles Performance** - 2024 updates for street-level views

### Development vs Production Strategy
- **Development**: Use Asset ID 2 (Sentinel-2) or local imagery
- **Production**: Use Asset ID 3 (Bing Maps Aerial) for maximum quality
- **Testing**: Implement feature flags to switch imagery providers

## 💡 REMEMBER: This is NOT a basic mapping application. It's a premium athletic route visualization tool that requires MAXIMUM IMAGERY QUALITY. Every decision should prioritize visual fidelity and user experience over "simplicity".

---

**Last Updated**: September 2025  
**Optimization Level**: 2024 Cesium Best Practices Applied ✓  
**Next Phase**: Implement real Strava API integration  
**Status**: High-performance satellite imagery with optimized rendering pipeline