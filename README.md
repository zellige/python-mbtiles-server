# simple-mbtiles-server
The simple mbtiles server is a quick and easy way to get starting with the mapbox vector tiles ecosystem.

The server can serve a file built using [tippecanoe](https://github.com/mapbox/tippecanoe).

With the "browser" option, the server will open a web page where you can view the tile layers in the mbtiles file on a simple map.

## Getting Started

At this stage, its a "build your own" kinda deal, but I have plans to make some releases for various platforms soon.

To set up, first clone this repo: 

```
git clone git@github.com:zellige/simple-mbtiles-server.git"
cd simple-mbtiles-server
```

Assuming you have stack installed and set up (if not, see [here](<https://docs.haskellstack.org/en/stable/README/>)) for instructions )

```
stack build
```

## Running

```
stack exec -- simple-mbtiles-server --mbtilesFile your_mbtiles_file.mbtiles -b
```

## Code formating
Use Ormolu: <https://github.com/tweag/ormolu>

### Content Encoding

By default, Tippecanoe produces gzipped tiles. This causes a `Unimplimented type: 3` error if the content-encoding header on the response is not set correctly.

Simple mbtiles uses the "generator_opts" field in the tile metadata to determine whether the last generator command included the -pC option to produce uncompressed tiles (see Tippecanoe readme for explanation). If if did, it will set content encoding to "identity" or uncompressed. Otherwise, it will set "gzip" as the content encoding.
