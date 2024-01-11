# New Endpoints
With version 0.2.0, OPUS now supports creating houses from OSM footprints and placing the generated houses onto a terrain provided by the user. In this tutorial, we will go over the usage of this new endpoint: `/create_house_with_floor_input`.

This endpoint contains 2 additional fields compared to `/create_opus_structure`:
- `floor_file` **(Required)**
- `ground_file` *(Optional)*

The `floor_file` currently accepts files with .osm extensions, while `ground_file` accepts .obj files. Please note that these are subject to change and should be verified in the API schema.

## There are some preset limits and rules for the osm_file:
- Footprints with any tag indicating that it is not a residential building won't be created.
- Houses that have footprints larger than 650m^2 won't be created.
- The OSM file should not contain more than 100 footprints.
- If there are two footprints closer than 2m on any side to each other in the OSM file and a `ground_file` is provided, meshes may overlap in the `ground_file` output.
- Ground file and floor file positions should match each other.

If any keywords/parameters are provided to this endpoint, all of the houses will inherit them as they would normally do in the `/create_opus_structure` or `/create_opus_component` endpoints.
