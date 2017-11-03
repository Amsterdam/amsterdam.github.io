---
abstract: End to end solution for processing, normalisation, anonimisation and serving 360° street view panoramas
---

# Open Panorama

An end to end solution for processing, normalisation, anonimisation and serving 360° street view panoramas. From raw files to API.

At the City of Amsterdam our civil servants need access to up to date street view images in order to do their job. We drive through the city multiple times per year to get the latest images.

You can see the 360° panorama images of the streets of Amsterdam on [data.amsterdam.nl](https://data.amsterdam.nl/#?mpb=topografie&mpz=11&mpo=pano::T&mpv=52.3714749:4.898476&sbf=Cu&sbh=5E&sbi=TMX7316010203-000222_pano_0000_000282&sbl=ZRJhS:3JV8j&sbp=c).

For more information on how to use, check out the [GitHub repository: Amsterdam/panorama](https://github.com/Amsterdam/panorama)

## What Open Panorama does

1. **Import panoramas**: from an objectstore including metadata CSVs into a database.
2. **Normalisation**: images are edited to face northwards and have a straight horizon.
3. **Image recognition and blurring**: finding sensitive data like people and licence plates and blurring those. With Docker Swarm cluster support.
4. **Tiling**: Making tiles out of the blurred 360° panorama images so they can be served with the API.
5. **Serving on an API**: An API that serves the locations and metadata over an OGC (WMS/WFS) server and tiles to users over a REST API.

We've published [a JavaScript library](panoviewer.md) that is built on [Marzipano](http://www.marzipano.net/) and allows others to integrate our Amsterdam streets into their sites.
