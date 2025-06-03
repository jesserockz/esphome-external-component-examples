# Archived

Use https://github.com/esphome/starter-components



# ![ESPHome logo](esphome-logo.png) ESPHome External Component Examples

This repository provides examples and basic empty components that can be used as templates to quickly develop your own external components for the splendid [ESPHome](https://esphome.io/) ESP8266/ESP32 home automation system.

## How to use

All sample components can be found in the `components` directory. The `test_empty_components.yaml` file provides configuration examples for the various external components. To use a particular component for your project, do the following:

- Create a `components` directory in your esphome configuration directory (the directory where your `.yaml` files are)

- Copy the directory of an empty component to `components` in its entirety, so you end up with e.g. `components/empty_sensor/`

- Find the configuration entry for the empty component in `test_empty_components.yaml` and copy it into your own `.yaml` file.

- Add the `components` directory as an [external_component](https://esphome.io/components/external_components):

```yaml
external_components:
  - source: components
```

- Compile with `esphome compile your_config.yaml` (change `your_config.yaml` to your own `.yaml` file) or compile with the dashboard.

- No errors? Great! You can now start modifying the empty component into your own external component.

## Basic structure of a external component

Let's start with the simplest external component:

```
components
├── empty_component
│   ├── __init.py__
│   ├── empty_component.cpp
│   ├── empty_component.h
│  ...
```

The `__init.py__` file contains 2 main things:

- **configuration validation** or **cv**
- **code generation** or **cg**

**cv** handles validation of user input in the `.yaml` configuration file for this particular component: defining the available configuration options, whether they are _required_ or _optional_, any constraints on the types and values of an option, etc.

**cg** takes these validated configuration options and generates the code necessary to streamline them into your c++ code, as well as registering your component properly within the ESPHome runtime.

The `.cpp` and `.h` files are the main source code files for your component. You're free to add to or modify the structure of the source code within the constraints of `c++`, but your code needs at least one `class` derived from `Component` that will be registered in the `__init__.py`.

If your component yields a specific type of component, e.g. a `sensor` or a `switch`, ESPHome will instead look for a `sensor.py` or `switch.py`.
The structure of these is identical to that of `__init__.py`.

See for example:

```
components
├── empty_binary_sensor
│   ├── __init__.py
│   ├── binary_sensor.py
│   ├── empty_binary_sensor.cpp
│   ├── empty_binary_sensor.h
│  ...
```

There is an empty `__init__.py` and most of the content goes in a `binary_sensor.py`.
