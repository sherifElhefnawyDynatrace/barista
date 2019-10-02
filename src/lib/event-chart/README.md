---
title: 'Event chart (experimental)'
postid: event-chart
public: false
identifier: 'Ec'
category: 'components'
properties:
  - 'experimental'
  - 'work in progress'
contributors:
  dev:
    - thomas.pink
    - thomas.heller
  ux:
    - xavier.javaloyas
  tags:
    - 'chart'
    - 'event-chart'
    - 'component'
    - 'angular'
related:
  - chart
  - micro-chart
  - timeline-chart
---

# Event chart (experimental)

Note: This component is still experimental, use with caution! Help us get this
component out of the experimental state by providing feedback.

<docs-source-example example="EventChartDefaultExample"></docs-source-example>

## Imports

You have to import the `DtEventChartModule` when you want to use the
`<dt-event-chart>`:

```typescript
@NgModule({
  imports: [DtEventChartModule],
})
class MyModule {}
```

## Example setup

<docs-source-example example="EventChartSessionReplayExample"></docs-source-example>

## Initialization

To create a `dtEventChart` in a minimal configuration, only
`dt-event-chart-events` and `dt-event-chart-lane` elements are required to
create a valid output.

<docs-source-example example="EventChartDefaultExample"></docs-source-example>

## Options & Properties

### DtEventChartEvent<T>

The `dtEventChartEvent` component is used to provide event data to the parent
event chart. It will also accept an arbitrary `data` input, which can hold
metadata for this event.

#### Inputs

| Name       | Type                 | Default   | Description                                                                         |
| ---------- | -------------------- | --------- | ----------------------------------------------------------------------------------- |
| `value`    | `number`             | -         | Value of the event (most probably a timestamp).                                     |
| `lane`     | `string`             | -         | Lane that this event is associated with.                                            |
| `duration` | `number`             | 0         | Duration of the event (most probably milliseconds).                                 |
| `color`    | `DtEventChartColors` | `default` | Color of the event. This color property will override the one provided by the lane. |
| `data`     | `T`                  | -         | Any data for this event. This data will be emitted when an event is selected.       |

#### Outputs

| Name       | Type                                        | Description                                        |
| ---------- | ------------------------------------------- | -------------------------------------------------- |
| `selected` | `EventEmitter<DtEventChartSelectedEvent<T>` | Event that fires when a an eventBubble is clicked. |

### DtEventChartLane

The `dtEventChartLane` defines a lane, on which an event will be rendered. The
events are associated with the lanes via their names. This association is
case-sensitive.

#### Inputs

| Name    | Type                 | Default   | Description                                                                    |
| ------- | -------------------- | --------- | ------------------------------------------------------------------------------ |
| `name`  | `string`             | -         | Name identifier of the lane.                                                   |
| `label` | `string`             | -         | Label for the lane (will be rendered on the left hand side of the eventChart). |
| `color` | `DtEventChartColors` | `default` | Defines the color for the given lane.                                          |

### DtEventChartLegendItem

The `dtEventChartLegendItem` lets you provide possible legend items for all
varieties of events, that could be rendered within the EventChart. Depending on
which events are being rendered (default, error, conversion, duration events),
the correct legend items will be picked form the given items, and displayed
below the EventChart.

#### Inputs

| Name          | Type                 | Default   | Description                                                        |
| ------------- | -------------------- | --------- | ------------------------------------------------------------------ |
| `lanes`       | `string | string[]`  | -         | Defines for which lanes this legend item can be used for.          |
| `hasDuration` | `boolean`            | -         | Defines that this legend item is used for duration events.         |
| `color`       | `DtEventChartColors` | `default` | Defines that this legend item is only usable for the passed color. |

### DtEventChartOverlay

The `dtEventChartOverlay` directive applies to an `ng-template` element lets you
provide a template for the rendered overlay. The overlay will be shown when a
user hovers the event bubble. The EventChart will expose the hovered events
(this is always an array, as the events could be clustered) as `$implicit`
context to the overlay template, which can be used as following:

```html
<ng-template dtEventChartOverlay let-tooltip>
  <div *ngFor="let t of tooltip">
    <!-- Insert your template for one event here. -->
  </div>
</ng-template>
```

## DtEventChartColors

Currently, there are only four different colors which are applicable to a
`dtEventChartEvent`, `dtEventChartLane` or `dtEventChartLegendItem`.

- default
- error
- conversion
- filtered

## Examples

### Default

<docs-source-example example="EventChartDefaultExample"></docs-source-example>

### Setting custom colors on events

<docs-source-example example="EventChartCustomColorExample"></docs-source-example>

### Providing legend items for events

<docs-source-example example="EventChartLegendExample"></docs-source-example>

### Defining the overlay template

<docs-source-example example="EventChartOverlayExample"></docs-source-example>

### Handling event selection via click

<docs-source-example example="EventChartSelectionExample"></docs-source-example>

### Session replay example (simplified)

<docs-source-example example="EventChartSessionReplayExample"></docs-source-example>