# 📝 Change Log

All changes to OPUS are documented here.

## \[0.6.0] - \~

## \[0.2.3] - 2023-08-11

### Added

* Introducing support for multi-floor buildings, including Apartment and Shop structures.
* OpenStreetMap (OSM) houses are now randomly assigned as Apartments, Shops, or Houses. Further control over this feature will be available in future versions.
* Introducing the Road structure, enabling the generation of random road networks with XODR and FBX output formats. An in-depth documentation can be found in [here](road\_supports.md) and Unreal Engine (UE) materials for roads can be downloaded from [here](https://drive.google.com/file/d/1wv0\_EHfYJGfHfEpv1x3QV50m9NI4kc7e/view?usp=sharing).
* Implemented a color system for materials, enhancing visual variety across our structures.
* Added the new `/get_attributes_with_name` endpoint that has more comprehensive result. More information can be found here.
* Improved error messaging for client-side errors, addressing previously ambiguous cases.

### Changed

* The extension list is now a mandatory field for `/create_house_with_floor_input`, `/create_opus_structure`, and `/create_opus_component` endpoints.
*   Job Status Changes

    ## Previous Job Statuses

    Our old statuses were as follows:

    * `PENDING`: The job was in queue, waiting to be processed.
    * `IN_PROGRESS`: The job was currently being processed.
    * `COMPLETED`: The job finished successfully.
    * `FAILED`: The job encountered an error and could not complete.
    * `CANCELLED`: The job was cancelled by the user or system.

    ## Updated Job Statuses

    Our new statuses provide more detail and are now as follows:

    * `Queued`: The job is in the queue, waiting for assignment.
    * `Pending`: The job is waiting for its dependencies to be satisfied.
    * `Running`: The job is currently in progress.
    * `Completed`: The job has successfully finished.
    * `Suspended`: The job is on hold or temporarily stopped.
    * `Failed`: The job encountered an error and could not complete.

### Fixed

* Resolved a bug related to parameters being provided outside their valid ranges.

## \[0.2.0] - 2023-06-16

### Added

\-`/create_house_with_floor_input` endpoint has been added to create houses with footprints from the given OSM file. These houses can optionally be placed onto the terrain provided by the user. A tutorial for this endpoint can be found in OPUSOSM file.

* Added I/O support for .glb, .gltf and .fbx file extensions to all of the generation endpoints. (FBX currently does not support transparent materials such as glass)
* Added output of all parameters in a JSON file called `opus_output.json`.
* Added `/create_opus_batch_component` and `/create_opus_batch_structure` endpoints that will create X amount of structures and components with one call. (There is a maximum limit of 10 in this version.)



*   With version 0.2.0, OPUS now supports creating houses from OSM footprints and placing the generated houses onto a terrain provided by the user. In this tutorial, we will go over the usage of this new endpoint: `/create_house_with_floor_input`.

    This endpoint contains 2 additional fields compared to `/create_opus_structure`:

    * `floor_file` **(Required)**
    * `ground_file` _(Optional)_

    The `floor_file` currently accepts files with .osm extensions, while `ground_file` accepts .obj files. Please note that these are subject to change and should be verified in the API schema.

    ## There are some preset limits and rules for the osm\_file:

    * Footprints with any tag indicating that it is not a residential building won't be created.
    * Houses that have footprints larger than 650m^2 won't be created.
    * The OSM file should not contain more than 100 footprints.
    * If there are two footprints closer than 2m on any side to each other in the OSM file and a `ground_file` is provided, meshes may overlap in the `ground_file` output.
    * Ground file and floor file positions should match each other.

    If any keywords/parameters are provided to this endpoint, all of the houses will inherit them as they would normally do in the `/create_opus_structure` or `/create_opus_component` endpoints.

### Changed

\-`/create_house_with_floor_input` and batch job endpoints will now return a list of results from the `/get_opus_job_result` endpoint. Warnings will be also provided upon submitting a `/create_house_with_floor_input` job, if there are any.

### Fixed

* Handled invalid/empty job ids that were throwing an internal server error.
* Fixed cases where GarageDoor, Stair, Mailbox, and Antenna assets were sometimes giving empty outputs.
* Fixed the cases where window had no materials on some part of the model.
* Resolved an issue causing job failure when parameters contained empty or invalid keys.
* Introduced an error message for instances when the specified parameter does not exist.
