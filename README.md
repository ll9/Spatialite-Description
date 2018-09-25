# Downloads (Mod_Spatialite und Spatialite Selbst)
http://www.gaia-gis.it/gaia-sins/windows-bin-x86/

0. Packe den Inhalt vom Mod_Spatialite Ordner in den Selben Ordner, wo sich sqlite befinden (z.B bin)
1. Spatialite Laden:
SELECT load_extension('mod_spatialite');
2. Initialisiere Metadata
SELECT InitSpatialMetaData();