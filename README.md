# Baie Ternay Marine Park mapping

High-resolution mapping of Baie Ternay Marine Park, Mahé, Seychelles, combining three drone surveys (70 m, 30 m and 10 m nominal flight altitudes) with close-range underwater photogrammetry of a reef area.

![70 m orthomosaic of Baie Ternay](assets/maps/full-bay-70m.jpg)

*Lower-resolution preview of the 70 m orthomosaic. Black areas contain no reconstructed imagery. The georeferenced full-resolution GeoTIFF is available on request.*

[Watch the 79-second mapping overview](assets/video/mapping-overview.mp4)

## Dataset at a glance

| Survey | Acquisition | Images | Pattern / overlap | Nominal orthomosaic resolution |
|---|---|---:|---|---:|
| Full bay | DJI FC3170 camera, 70 m altitude, 30 km/h | 1,604 | S-pattern, 75% overlap | 2.5 cm/px |
| Large reef area | DJI FC3170 camera, 30 m altitude, 6 km/h | 1,052 | S-pattern, 85% overlap | 1.1 cm/px |
| Reef detail | DJI FC3170 camera, 10 m altitude, 5 km/h | 324 | Grid pattern, 85% overlap | 0.4 cm/px |
| Underwater reef | Olympus TG-6, approximately 1 m above the seafloor | 2,605 | Three adjoining sections | approximately 1.9 mm/px[^1] |

The drone imagery was acquired on 11–12 December 2021. The underwater survey was acquired on 17 January 2022.

## Study area and georeferencing

The project is centred on [Baie Ternay, Mahé, Seychelles](https://www.openstreetmap.org/?mlat=-4.637902&mlon=55.373767#map=15/-4.637902/55.373767). Drone orthomosaics are georeferenced in **WGS 84 / UTM zone 40S (EPSG:32740)**.

| Orthomosaic | Raster extent on the ground | WGS 84 bounds (west, south, east, north) |
|---|---:|---|
| 70 m full bay | approximately 1,577 × 1,227 m | `55.366650, -4.643432, 55.380885, -4.632371` |
| 30 m reef area | approximately 202 × 223 m | `55.375748, -4.640630, 55.377576, -4.638618` |
| 10 m reef detail | approximately 31.4 × 31.4 m | `55.377100, -4.639419, 55.377383, -4.639136` |

Bounds and pixel sizes were read from the source GeoTIFF metadata. They describe the raster canvases, which can include transparent or empty margins beyond reconstructed image coverage.

## Methodology

### Drone surveys

All drone photographs are 4,000 × 3,000 pixels (12 MP), recorded with a DJI FC3170 camera at 4.5 mm focal length (24 mm full-frame equivalent) and f/2.8. Camera settings varied automatically with the available light:

- 70 m survey: ISO 100–210, shutter speed 1/640–1/15 s; flown near sunset over two days.
- 30 m survey: ISO 100–130, shutter speed 1/250–1/15 s; flown around sunrise.
- 10 m survey: ISO 100–110, shutter speed 1/160–1/60 s; flown near sunset.

The 70 m survey established full-bay context. The 30 m and 10 m surveys progressively increased spatial detail over the selected reef area. The source photographs' embedded GPS positions were used by WebODM to generate the georeferenced orthomosaics.

### Underwater photogrammetry

The underwater survey covered an approximately 27 m-long by 6 m-wide reef strip, processed as three adjoining sections of roughly 6 × 9 m each. A 50 cm graduated PVC bar was placed in each section for scale, and measuring tape marked the edge of the survey area.

The 2,605 Olympus TG-6 photographs are 4,000 × 3,000 pixels. The camera was held approximately 1 m above the seafloor at 5.4 mm focal length (30 mm full-frame equivalent). EXIF metadata records ISO 100–160, f/2.3–f/3.2, shutter speeds from 1/250 to 1/60 s, and flash use throughout.

Before reconstruction, the underwater images were sorted into batches with similar visual and lighting conditions. Each batch received a consistent RawTherapee treatment, including colour and exposure/illumination corrections appropriate to that group, and was then exported with RawTherapee 5.8. This reduced within-group appearance differences while allowing different conditions to receive different corrections.

Each section was reconstructed in WebODM. Because the underwater photographs contain no usable GPS positions, their initial reconstructions had no valid geographic placement. Derived underwater orthomosaics were then manually registered to the 70 m drone orthomosaic using visible reef features and reshaping tools. Their absolute position should therefore be treated as approximate rather than as an independent survey-grade measurement.

## Preview gallery

| 30 m reef area | 10 m reef detail |
|---|---|
| ![30 m reef orthomosaic](assets/maps/reef-30m.jpg) | ![10 m reef orthomosaic](assets/maps/reef-10m.jpg) |

| Underwater section 1 | Underwater section 2 | Underwater section 3 |
|---|---|---|
| ![Underwater orthomosaic section 1](assets/maps/underwater-section-1.jpg) | ![Underwater orthomosaic section 2](assets/maps/underwater-section-2.jpg) | ![Underwater orthomosaic section 3](assets/maps/underwater-section-3.jpg) |

## Data access

This repository intentionally contains only reduced-resolution JPEG previews and a compressed overview video so that it remains easy to browse and clone. The JPEG files are not georeferenced and should not be used as substitutes for the analysis-ready rasters.

The following material can be requested:

- original drone image sets for the 70 m, 30 m and 10 m surveys;
- edited Olympus TG-6 underwater image set;
- full-resolution orthomosaics and georeferenced GeoTIFF files; and
- additional processing outputs, subject to availability.

To request data, [open a data-request issue](https://github.com/GillesGaelBERNARD/baie-ternay-mapping/issues/new?template=data-request.yml) and describe the dataset, intended use and preferred format. GitHub issues are public, so do not include private contact details; a private contact route can be arranged after the initial request. No explicit reuse licence is currently attached to the source datasets, so please also state the intended reuse and attribution.

## Limitations

- The drone products rely on embedded consumer-drone GPS positions; no RTK, PPK or ground-control-point workflow is documented.
- Water-surface movement, refraction, depth and changing illumination can introduce geometric and radiometric artefacts.
- The underwater products were manually aligned to the drone orthomosaic and are not independently georeferenced.
- Nominal spatial resolutions describe output pixel size, not guaranteed positional or measurement accuracy.
- These products are for documentation and research use, not navigation.

## Repository contents

```text
assets/
  field-images/   Example source photographs
  maps/           Reduced-resolution orthomosaic previews
  video/          Compressed project overview
.github/
  ISSUE_TEMPLATE/ Data-request form
README.md          Project description and methodology
```

Project owner: [GillesGaelBERNARD](https://github.com/GillesGaelBERNARD)

[^1]: Approximate underwater output resolution recorded in the original processing notes. Manual registration and resampling can change the pixel size of derived aligned rasters.
