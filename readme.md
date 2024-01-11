# README

## Introduction to OPUS

### What is OPUS?

OPUS is a service that enables you to create your own parametrizable high-quality 3D assets for use in simulations, games, or any other application. We offer many configurations and multi degrees-of-freedom. Our endpoints are designed for granular configurations, but we also support controlled-randomization for those who want to randomize parameters easily.

In this tutorial, we'll cover how to randomize different objects at various levels of control.

![Granuality Levels](.gitbook/assets/OPUSGranualityLevels.jpg)

### What is a Component?

#### Definition:

A component refers to an individual or standalone part that can be used to build or assemble larger objects.

#### Key Points:

* **Granularity**: Components are often smaller elements with a specific purpose or function.
* **Independence**: They can exist independently or be integrated into larger structures.
* **Examples**: Windows, doors, stairs, antennas, fire hydrants, and parking meters.
* **Function**: Components typically serve specific roles. For instance, a door allows for entry and exit, while a window lets in light.

### What is a Structure?

#### Definition:

A structure refers to a more complex assembly made up of multiple components. It represents a higher-level entity that houses various components in an organized manner.

#### Key Points:

* **Complexity**: Structures are comprehensive entities comprising multiple components.
* **Composition**: By nature, structures combine multiple components. For example, a house may include windows, doors, and stairs.
* **Examples**: A house is a primary example of a structure in the context of 3D modeling.
* **Purpose**: Structures often serve broader purposes. A house, for example, provides shelter, while its components serve specific functions within that shelter.

To put it succinctly, while components are individual parts or elements that can be used independently or as part of larger assemblies, structures are those larger entities that group and organize multiple components. Grasping this distinction is essential for effective 3D design, especially when using a tool like OPUS.

### Getting all supported objects

Use the **Get All Model Names** endpoint to retrieve a list of currently available models. Models are divided into two categories: "Structure" and "Component". Structures are larger objects comprising multiple components.

### Getting Model Attributes

After choosing your desired model, use the **Get Attributes of a Model** endpoint to retrieve its attributes, which are divided into "keywords" and "parameters".

### Creating a Structure

You can request either a fully or partially randomized structure using the **Create Structure** endpoint.

* For a totally randomized "House" with simple window components.
* For a large "House" with all large components.
* For more specific structures, like a generally small "House" but with large windows.

You can also specify exact parameter values.

### Create Components

Components are the smaller objects that constitute a structure. Like structures, components can also be created by controlling either keywords, parameters, or both.

For example, to create a window with specific dimensions.

### Texture Resolution

Specify your preferred texture resolution using the `texture_resolution` option. Options include 1024, 2048, and 4096.

### Getting Job Results

![Polling](.gitbook/assets/OPUSPolling.jpg)

We use an asynchronous request pattern. Each **Create Component** or **Create Structure** call will return a job ID, which you can use to check the status of your request.

Job statuses include:

* **PENDING**: Job hasn't started.
* **IN\_PROGRESS**: Job is currently in process.
* **COMPLETED**: Job has finished successfully.
* **FAILED**: Job has failed.
* **CANCELLED**: Job has been cancelled.

In the event of a failure, please provide the timestamp of the request and contact [genel@capoom.com](mailto:genel@capoom.com) for a quota increase.

Please begin polling status after a 30-second wait for structures and 15 seconds for components. Download links expire in 24 hours, so caching is recommended for frequent access.

**Happy developing with our OPUS APIs!** For support and suggestions, please email [genel@capoom.com](mailto:genel@capoom.com).

## Appendix: Additional Tutorials

For those looking to delve deeper into the subject of creating components and structures, the following tutorials provide comprehensive insights, starting from the basics (A) to the advanced techniques (Z).

### Tutorials:

1. **Fundamentals of Creating Components and Structures**
   * [Creating Models from A-Z](tutorial1.md)

## Appendix: Change Logs

Throughout our software's development, several pivotal updates have been implemented to enhance functionality, improve user experience, and rectify previous limitations. Here's a summary of some of our most impactful changes along with links to detailed changelog files:

### Change Logs:

#### 1. OSM Road Network Support

* **Date**: 2023-06-16
* **Description**: Integrated support for OpenStreetMap (OSM) road networks. This feature allows users to integrate and utilize road network data from OSM within the application.
* **Detailed Changelog**: [OSM Road Network Support Changelog](road\_supports.md)

#### 2. Multistory Building Support

* **Date**: 2023-08-11
* **Description**: New functionality supports the design and rendering of multistory buildings. Users can now create and visualize structures with multiple levels, enhancing urban simulation realism.
* **Detailed Changelog**: [Multistory Building Support Changelog](./)

***

To stay updated of the latest features and improvements, we recommend reviewing our change logs regularly.
