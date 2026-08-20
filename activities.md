# Activities

1. [Control simulation](#1-control-simulation)
2. [Change Widget inputs](#2-change-widget-inputs)
3. [Add new Widgets](#3-add-new-widgets)
4. [Check a custom code Widget](#4-check-a-custom-code-widget)
5. [Add a custom code Widget](#5-add-a-custom-code-widget)
6. [Customize a built-in Widget](#6-customize-a-built-in-widget)
7. [Add a custom Widget](#7-add-a-custom-widget)

## 1. Control simulation

- Connect / Disconnect / Resume / Pause
  - Using icons on the main app bar
  - Sticky bar (bar showing `Frame`, `Time`, etc) color indicates current status
- Check Universe Configuration
  - 'Settings > Universe Configuration'
  - Disabled when connected to the simulation
  - Editable when disconnected
    - All MDAnalysis Universe related config
    - Can add custom code to setup Universe - Eg: transformations
- Disable display of session info and energies on dashboard
  - 'Settings > Dashboard Configuration'
- Dashboard icon on top left from any page always navigates to the main dashboard

## 2. Change Widget inputs

Change `COMDistance` Widget inputs

- Double click on the `COMDistance` Widget on the dashboard
  - Check input validations for selection phrase changes
  - Check Widget output updates in real-time when simulation running
  - Check the documentation for this Widget

> Tip: Double clicking on the Widget opens the Widget details. Alternatively, click on the three dots icon on the Widget title and select `Edit` 

## 3. Add new Widgets

- Click on the 'Add Widget' button on main dashboard
  - Add `DSSP` Widget
  - Add a Velocity Autocorrelation (VACF) plot (`ACF` Widget)
    - Enable 'Show running integral' to observe diffusion coefficient
- Check layout presets, customize as required

## 4. Check a custom code Widget

- Check the `Kinetic Energy` Widget on dashboard
  - Go to Widget details
- Check Notebooks to see where `SimplePlot` class is defined
- Check Widget documentation

## 5. Add a custom code Widget

Add a custom code widget to display 'Box Volume'

- Select `Custom Code` from `Add Widget` list from main dashboard
- Create a plot variable in `Setup code` section and run the cell
  ```py
  bv_plot = SimplePlot(u)
  ```
- Print and show plot in `Execute code` section
  ```py
  print(f"Volume = {u.trajectory.ts.volume:.2f} Å³")
  bv_plot.show("Box Volume", u.trajectory.ts.volume)
  ```
- See real-time plot in the `Output` section and on dashboard when simulation is running

## 6. Customize a built-in Widget

Customize the `COMDistance` widget to print the distance in addition to the plot.

- Go to Notebooks
- Select the `Custom COMDistance` Notebook
- Run the Notebook cell
  - The code is already updated to add a `print`
  - The Notebook was created by cloning the built-in `COMDistance` Widget code
  - 'Run on Launch' not enabled for this Notebook, hence needed the manual run
- The `COMDistance` widget on the dashboard should automatically get refreshed

## 7. Add a custom Widget

Add a custom Widget to show and plot the center-of-mass (COM) of a selection.

- Go to Notebooks
- Create a new Notebook
- Add the following custom widget class and run the cell

  ```py
  from mdadash.backend.widgets.base import WidgetBase

  class ShowCOM(WidgetBase):
      name = "Show COM"
      description = "Show COM of a selection"
      _override_name = True

      _inputs = [
          {
              "attribute": "selection",
              "name": "String",
              "description": "MDAnalysis selection phrase",
              "type": "str",
          },
      ]

      def __init__(self):
          super().__init__()
          self.selection = "protein"

      def on_post_connect(self):
          self.plot = SimplePlot(self.u)

      def run_every_frame(self):
          com = self.u.select_atoms(self.selection).center_of_mass()
          print(f"COM of {self.selection} is ", com)
          self.plot.show(f"COM of {self.selection}", com)
  ```
- Go to main dashboard and dd a new `Show COM` widget instance
- Check Widget details and update selection phrase to see updated plot
- Create new instances of this widget with different input selections

> Note: The above simple Widget class has no validations and plot reset when input changes
