Slippy dot maps for OpenAddresses have come up in a few ways:

- We have a Mapbox-hosted dotmap at https://openaddresses.io
- There's some desire for better previews at https://github.com/openaddresses/machine/issues/440
- Slippy maps are a way to improve previews at https://github.com/openaddresses/machine/issues/466

This is a placeholder repository for some thoughts on how we could add more
slippy maps with interactive dots to OpenAddresses, and the process and data
pipelines that would be required to make them work.

----

These scripts (in this order) generate monthly data over time for California:

- download-runs.py
- match-downloads.py
- tippecanoe-downloads.py

Cached and Tippecanoed data can be found here:

- https://s3.amazonaws.com/dotmaps.openaddresses.io/us-ca-monthly/downloaded/files.csv
- https://s3.amazonaws.com/dotmaps.openaddresses.io/us-ca-monthly/set_141476.mbtiles
- https://s3.amazonaws.com/dotmaps.openaddresses.io/us-ca-monthly/set_131277.mbtiles
- etc.

Set numbers are from the live data base, so the two above match:

- https://results.openaddresses.io/sets/141476/
- https://results.openaddresses.io/sets/131277/
- etc.

----

http://web.archive.org/web/20070227082525/http://fdo.osgeo.org/files/fdo/docs/FDG_FDODevGuide/files/WS7106c181349dd8d016672d6105df83c6e7-7fff.htm

    While geometry typically is two- or three-dimensional, it may also contain
    the measurement dimension (M) to provide the basis for dynamic segments.

http://postgis.17.x6.nabble.com/4D-points-td3598428.html

    'm' is 'measure' an extra axis of information not associated with the
    cartesian x/y/z space. The most common use for 'measure' is actually for
    'measurements', the adding of physically known measurements about a feature
    to the abstract 'feature' represented in x/y space in the GIS. For example,
    highway management systems often understand the location of facilities in
    terms of 'mile posts'. So, in addition to x/y coordinates, each vertex is
    also assigned a 'mile' measurement in 'm' which allows the system to
    accurately place facility information relative to the 'milepost' system.
    (Why not just use the x/y coordinates and calculate distances off of them?
    Because they are representational, the distances calculated from the x/y
    will not be the same as the actual milepost measurements.) 

source .vrt files could go to:

1.  PostGIS for whole-earth tile storage
2.  MBTiles for per-run slippy maps
