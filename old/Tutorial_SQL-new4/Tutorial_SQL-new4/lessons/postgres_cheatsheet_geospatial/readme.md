## **PostgreSQL Geospatial Data - Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  
| Feature | Description |
|---------|-------------|
| **PostGIS** | Extension that enables geospatial support in PostgreSQL. |
| **Geometry vs. Geography** | `geometry` for Cartesian coordinates, `geography` for geodetic (lat/lon). |
| **Spatial Indexing** | Uses GiST (`CREATE INDEX ... USING GIST`). |
| **SRID (Spatial Reference System Identifier)** | Defines coordinate system (e.g., `4326` for WGS 84). |

---

## **2. Enabling PostGIS**  

### **Check if PostGIS is Installed**  
```sql
SELECT PostGIS_Full_Version();
```

### **Enable PostGIS Extension**  
```sql
CREATE EXTENSION postgis;
```

---

## **3. Geospatial Data Types**  

| Data Type | Description |
|-----------|-------------|
| `geometry` | Stores planar (Cartesian) coordinates. |
| `geography` | Stores spherical (geodetic) coordinates. |
| `point` | A single point (x, y). |
| `linestring` | A sequence of points (a line). |
| `polygon` | A closed shape with an outer boundary. |
| `multipoint` | Multiple points. |
| `multilinestring` | Multiple lines. |
| `multipolygon` | Multiple polygons. |
| `geometrycollection` | A collection of geometry objects. |

---

## **4. Creating Geospatial Columns**  

### **Geometry Column (Planar)**  
```sql
ALTER TABLE locations ADD COLUMN geom geometry(Point, 4326);
```

### **Geography Column (Geodetic)**  
```sql
ALTER TABLE locations ADD COLUMN geog geography(Point, 4326);
```

---

## **5. Inserting Geospatial Data**  

### **Insert a Point**  
```sql
INSERT INTO locations (name, geom)  
VALUES ('City Center', ST_GeomFromText('POINT(-73.9857 40.7484)', 4326));
```

### **Insert a Polygon**  
```sql
INSERT INTO areas (name, geom)  
VALUES ('Park', ST_GeomFromText('POLYGON((-73.98 40.74, -73.99 40.74, -73.99 40.75, -73.98 40.75, -73.98 40.74))', 4326));
```

---

## **6. Geospatial Queries**  

### **Find Distance Between Two Points**  
```sql
SELECT ST_Distance(
  ST_GeomFromText('POINT(-73.9857 40.7484)', 4326),
  ST_GeomFromText('POINT(-73.9850 40.7480)', 4326)
);
```

### **Find Locations Within a Radius**  
```sql
SELECT name FROM locations  
WHERE ST_DWithin(geom, ST_GeomFromText('POINT(-73.9857 40.7484)', 4326), 500);
```
- Finds locations within **500 meters**.

### **Check If a Point is Inside a Polygon**  
```sql
SELECT name FROM areas  
WHERE ST_Contains(geom, ST_GeomFromText('POINT(-73.9857 40.7484)', 4326));
```

---

## **7. Spatial Indexing**  

### **Create a GiST Index**  
```sql
CREATE INDEX locations_geom_idx ON locations USING GIST (geom);
```
- Improves spatial query performance.

---

## **8. Common Spatial Functions**  

| Function | Description |
|----------|-------------|
| `ST_Area(geom)` | Returns the area of a polygon. |
| `ST_Length(geom)` | Returns the length of a linestring. |
| `ST_Transform(geom, srid)` | Converts between coordinate systems. |
| `ST_Intersects(a, b)` | Returns `TRUE` if two geometries intersect. |
| `ST_Within(a, b)` | Returns `TRUE` if `a` is inside `b`. |
| `ST_Buffer(geom, radius)` | Creates a buffer zone around a geometry. |
| `ST_Union(geom1, geom2)` | Merges multiple geometries. |
