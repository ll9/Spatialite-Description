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

5b.
insert into test_geom2 values('bla23', GeomFromText('POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))', 4326));
6b.
select *, asText(geometry) from test_geom2;

## Spalten löschen (ACHTUNG: Spatialite geometry constraints gehen verloren, dafür bleiben aber primary key und datentypen erhalten)

1. Tabelle umbenennen
ALTER TABLE LDS_FEATURES RENAME TO _LDS_FEATURES;

2. Tabelle Klonen ('main' ist quasi die aktuelle Datenbank, 1 steht für eine atomaren Befehl, beim letzen Parameter wird die Spalte gelöscht)
SELECT CloneTable('main', '_LDS_FEATURES', 'LDS_FEATURES', 1, '::ignore::Temp');

3. Tabelle löschen
DROP TABLE _LDS_FEATURES;

## Geometrie entfernen
SELECT DiscardGeometryColumn('test_geom', 'the_geom');
