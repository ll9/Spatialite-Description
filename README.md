# Downloads (Mod_Spatialite und Spatialite Selbst)
http://www.gaia-gis.it/gaia-sins/windows-bin-x86/

0. Packe den Inhalt vom Mod_Spatialite Ordner in den Selben Ordner, wo sich sqlite befinden (z.B bin)
1. Spatialite Laden:
SELECT load_extension('mod_spatialite');
2. Initialisiere Metadata
SELECT InitSpatialMetaData();
3. Erstelle eine Tabelle
CREATE TABLE test_geom(name varchar(30));
4. Füge Geometriespalte dazu (dazu benötigt es seperaten Schritt, nicht mit 3. kombinierbar)
SELECT AddGeometryColumn('test_geom', 'geometry', 4326, 'POINT', 'XY');

5. Füge Daten ein:
insert into test_geom values('bla', GeomFromText('POINT(1.01 2.02)', 4326));
6. Lies Daten aus:
select *, asText(geometry) from test_geom;