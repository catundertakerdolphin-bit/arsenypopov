# Bottlenose dolphin skull and mandible

## Files

- `bottlenose-dolphin-skull.glb` — web asset, two separately named mesh nodes (`Skull`, `Mandible`), 2,485,888 bytes.
- `skull-contour-fallback.png` — 1600 × 1000 blue contour rendering of the reimported final GLB on white. Freestyle silhouette, occlusion, border and steep crease lines; no triangle wireframe.
- `skull-geometry-preview.png` — smooth blue diagnostic view of reduced geometry.
- `bottlenose-dolphin-skull.blend` — editable Blender source including the reduced meshes and inspection camera.
- `dolphin-skull-original.stl`, `dolphin-mandible-original.stl` — unmodified downloaded sources.
- `geometry-report.json` — exact bounds, source checksums, scale and 4 × 4 transform, reduction statistics and proposed cameras.
- `glb-validation.json` — counts from reimporting the actual exported GLB, checked for finite vertex coordinates.

## Source and credit

Source: [Dauphin Island Sea Lab — Educational Materials](https://www.disl.edu/research/marine-mammal-research-program/education/), downloaded 20 September 2026.

- [Skull STL](https://www.disl.edu/research/marine-mammal-research-program/education/dolphin_skull_1of2.stl)
- [Mandible STL](https://www.disl.edu/research/marine-mammal-research-program/education/dolphin_skull_2of2.stl)
- [Specimen factsheet](https://www.disl.edu/research/marine-mammal-research-program/education/Dolphin-Skull-Factsheet.pdf)

Specimen: bottlenose dolphin, *Tursiops truncatus*, 05DISL020919, a subadult male recovered at Orange Beach, Alabama, in February 2019. Dauphin Island Sea Lab's Alabama Marine Mammal Stranding Network recovered the specimen; CT work was performed at Auburn College of Veterinary Medicine; Dr. Ray Wilhite created the STL files.

Suggested brief attribution: “Bottlenose dolphin CT scan — Dauphin Island Sea Lab / ALMMSN; Auburn College of Veterinary Medicine, Dr. Ray Wilhite. Simplified and rendered for the web.”

## Rights note

No explicit Creative Commons, public-domain dedication or other open reuse license was found on the educational source page or factsheet. The source page says: “These files (.stl) can be used for visualizations or even printed on a 3D printer!” Preserve attribution and source links; do not label this asset CC0 or CC BY. This note records the posted visualization context, and does not assert a broader license.

## Geometry and orientation

The two STL files already share CT coordinates and form a plausibly aligned open-jaw skull. Their relative position and the jaw pose are retained exactly. There was no manual articulation, mirroring, anatomical fabrication or independent repositioning of either part.

Original coordinate axes: source Z is up, rostrum points towards source −Y, lateral thickness is source X. Original STL units are not declared by STL itself.

The common original bounding-box center is `[-15.135299682617188, -969.1671142578125, -1172.547119140625]`. Subtract this center, multiply all coordinates by `0.01420466367961825`, and map:

```
gltf.x = (source.y - center.y) * scale
gltf.y = (source.z - center.z) * scale
gltf.z = (source.x - center.x) * scale
```

The GLB is +Y up, rostrum towards −X (left when viewed from +Z), with lateral thickness along Z. Targeted full length before decimation is 6 units. Final bounds are approximately `[-2.999789, -1.737120, -1.432229]` to `[3.001672, 1.738343, 1.433014]`, a total extent of `[6.001461, 3.475463, 2.865243]`. Tiny bounding-box changes arose from mesh simplification.

## Processing and validation

Processed in Blender 5.2.0. Original binary STL contains 324,438 skull triangles and 100,840 mandible triangles. The importer discarded 11 duplicate skull triangles. Quadric edge-collapse decimation targeted 100,000 skull and 38,000 mandible triangles. Mesh validation then removed 221 duplicate skull faces and 28 duplicate mandible faces created by collapse. Smooth vertex shading was retained. No spatial smoothing, voxel remeshing or anatomical surface sculpting was applied.

Final GLB was reimported and rendered to inspect export geometry. It contains:

| Mesh | Triangles | GLB vertices |
|---|---:|---:|
| Skull | 99,779 | 49,894 |
| Mandible | 37,972 | 19,116 |
| Total | 137,751 | 69,010 |

All final vertex positions are finite. Teeth, orbits and thin zygomatic elements remain visible in inspected lateral and oblique views. No claim of watertightness is made; this is a CT-derived visualization mesh with the source surface's anatomical openings.

## Rendering guidance

Three.js camera suggestion: position `[-3.2, 3.0, 11.0]`, look at `[0, 0, 0]`, Y up, orthographic vertical span around `4.9`. Use sufficient horizontal span to show the full length; on narrow mobile displays derive the vertical span from the available aspect ratio.

A more lateral view is `[0, 1, 12]`; a more oblique view is `[-7, 4, 10]`; the upper/dorsal view is `[0, 12, 0.001]`. Two white meshes with blue silhouette/depth/normal edges will produce anatomical contours. The supplied fallback uses the recommended oblique view and approximate cobalt `#164FEB`. Avoid rendering every triangle as a line: it would obscure teeth and bone landmarks.
