# Dashboard

The [Dashboard](https://app.uniot.io/dashboard) is your central hub for interacting with connected devices. Build custom interfaces with drag-and-drop widgets that let you monitor sensor data, control actuators, and visualize device behavior in real-time. Whether you're managing a single prototype or a fleet of production devices, the dashboard adapts to your workflow.

## Overview

The dashboard interface provides a flexible workspace where you can organize widgets to match your specific needs. Each dashboard supports both desktop and mobile layouts, ensuring your device interfaces work seamlessly across all screen sizes.

The main dashboard view displays your configured widgets arranged in a grid layout. From here, you can quickly switch between view and edit modes and access all device interactions in one place. The interface is designed to be intuitive - focus on your devices, not on learning complex UI patterns.

<div><figure><img src="../.gitbook/assets/dashboard_main.png" alt=""><figcaption></figcaption></figure></div>

## Edit/View Modes

The dashboard operates in two distinct modes:

- **View Mode** - Your default working state for monitoring and controlling devices. Interact with widgets, view real-time data, and manage your devices without accidentally modifying the layout.
- **Edit Mode** - The configuration state where you can add, remove, rearrange, and configure widgets to build your ideal dashboard interface.

### Layout Types

Each dashboard supports two independent layout types: **desktop** and **mobile**. This means you can arrange widgets differently for each screen size, optimizing the experience for both laptop/desktop and mobile device.

When in edit mode, switch between layouts to customize each one separately. Changes made to the desktop layout won't affect the mobile layout, and vice versa. This gives you complete control over how your dashboard appears on different devices.

<div><figure><img src="../.gitbook/assets/dashboard_view_modes.png" alt=""><figcaption></figcaption></figure></div>

### Working in Edit Mode

In edit mode, you have full control over your dashboard structure:

- **Add widgets** from the widget dropdown menu
- **Drag and drop** widgets to reposition them in the grid
- **Resize widgets** by dragging their corners or edges
- **Configure widget settings** by clicking on the widget's settings icon
- **Delete widgets** that are no longer needed

Remember to switch between desktop and mobile layouts while editing to ensure both versions of your dashboard provide a great user experience.

### Dashboard Thumbnails

When you switch from edit mode to view mode, the platform automatically captures a screenshot of your dashboard. This screenshot is used as a thumbnail preview in your dashboard list, making it easy to identify and navigate between multiple dashboards at a glance.

The screenshot captures the currently active layout - if you're viewing the desktop layout when you save, the thumbnail will show the desktop version. If you're in the mobile layout, the thumbnail will display the mobile version. To update a dashboard's thumbnail, simply switch to the desired layout in edit mode and then save by switching back to view mode.

## Widgets

Widgets are the building blocks of your dashboard. Each widget serves as an interface component that either displays data from your devices (like charts, gauges, or indicators) or sends commands to them (like buttons, switches, or sliders). Think of widgets as the bridge between your physical hardware and your dashboard interface.

### Adding Widgets

To add a widget to your dashboard:

1. Switch to **edit mode**
2. Click the **widget dropdown menu** to see all available widget types
3. Select the widget that matches your needs

<div><figure><img src="../.gitbook/assets/dashboard_widget_select.png" alt=""><figcaption></figcaption></figure></div>

{% hint style="info" %}

The widget library is continuously expanding. New widgets are added regularly based on user needs and common IoT use cases. If you need a specific widget type, share your request on our [community forum](https://community.uniot.io/) - we actively consider user feedback when planning new features.

{% endhint %}

### Widget Configuration

Every widget requires two essential settings:

- **Name** - A descriptive label that appears on the dashboard. Choose names that clearly indicate the widget's purpose (e.g., "Temperature Sensor", "Living Room Light", "Motor Speed").
- **Event** - The device event this widget subscribes to or publishes. This links the widget to specific data streams or control channels on your device.

<div><figure><img src="../.gitbook/assets/dashboard_widget_settings.png" alt=""><figcaption></figcaption></figure></div>

### Additional Settings

Beyond the basic configuration, widgets offer type-specific settings:

**Control Widgets** (Push Button, Switch, Slider):

- **Retain parameter** - When enabled, the broker stores the last message and automatically sends it to devices that connect later. This ensures devices receive the most recent command even if they were offline. [Learn more about retained messages](../api-reference/mqtt-convention.md#retained-messages).

**Display Widgets** may include:

- Visual customization (colors, themes, ranges)
- Data formatting options
- Update intervals
- Historical data settings

Each widget type has settings tailored to its specific function - explore them to create the most effective interface for your devices.
