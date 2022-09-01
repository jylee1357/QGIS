# QGIS

```
#convert dataframe to geodataframe and setting epsg

df_meta = pd.read_csv('META.csv', dtype = str)
df_meta['경도'] = df_meta['경도'].astype(float)
df_meta['위도'] = df_meta['위도'].astype(float)
df_meta['geometry'] = df_meta.apply(lambda row : Point([row['경도'], row['위도']]), axis=1)
df_meta = gpd.GeoDataFrame(df_meta, geometry='geometry')
df_meta = df_meta[['지점명','위도','경도','geometry']]
df_meta

from fiona.crs import from_string
epsg4326 = from_string("+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs")

df_meta.crs = epsg4326
print(df_meta.crs)

epsg5179 = from_string("+proj=tmerc +lat_0=38 +lon_0=127.5 +k=0.9996 +x_0=1000000 +y_0=2000000 +ellps=GRS80 +units=m +no_defs")
df_meta = df_meta.to_crs(epsg5179)


```
