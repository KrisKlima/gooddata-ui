---
title: Pivot Table
sidebar_label: Pivot Table
copyright: (C) 2007-2018 GoodData Corporation
id: pivot_table_component
---

Pivot table shows data in columns and rows. In contrast to the standard [table](table_component.md), a pivot table allows you to break measures into columns by setting attributes in the ```columns``` prop. In pivot tables, you can choose to display only attributes (without any measures). Also, pivot tables have higher limits for the number of datapoints to display than charts.

![Pivot Table Component](assets/pivot_table.png "Pivot Table Component")

## Structure

```jsx
import '@gooddata/react-components/styles/css/main.css';
import { PivotTable } from '@gooddata/react-components';

<PivotTable
    projectId={<project-id>}
    measures={<measures>}
    …
/>
```

## Examples

### Standard table

```jsx
const measures = [
    {
        measure: {
            localIdentifier: 'franchiseFees',
            definition: {
                measureDefinition: {
                    item: {
                        identifier: franchiseFeesIdentifier
                    }
                }
            },
            format: '#,##0'
        }
    }
];

const rows = [
    {
        visualizationAttribute: {
            displayForm: {
                identifier: locationStateDisplayFormIdentifier
            },
            localIdentifier: 'location'
        }
    }
];

<div style={{ height: 300 }}>
    <PivotTable
        projectId={projectId}
        measures={measures}
        rows={rows}
        columns={columns}
    />
</div>
```

### Pivot table

```jsx
const measures = [
    {
        measure: {
            localIdentifier: 'franchiseFees',
            definition: {
                measureDefinition: {
                    item: {
                        identifier: franchiseFeesIdentifier
                    }
                }
            },
            format: '#,##0'
        }
    }
];

const columns = [
    {
        visualizationAttribute: {
            displayForm: {
                identifier: monthDateIdentifier
            },
            localIdentifier: 'month'
        }
    }
];

const rows = [
    {
        visualizationAttribute: {
            displayForm: {
                identifier: locationStateDisplayFormIdentifier
            },
            localIdentifier: 'location'
        }
    }
];

<div style={{ height: 300 }}>
    <PivotTable
        projectId={projectId}
        measures={measures}
        rows={rows}
        columns={columns}
    />
</div>
```

## Sorting

You can [sort](result_specification.md#sorting) rows and attribute columns. Measures are always listed in the same order they were defined in the ```measures``` prop.

### Example: Sorting by measure

```jsx
// ...using Pivot Table Example

const sortBy = [
    {
        measureSortItem: {
            direction: 'desc',
            locators: [
                {
                    attributeLocatorItem: {
                        attributeIdentifier: 'month',
                        element: monthDateIdentifierJanuary
                    }
                },
                {
                    measureLocatorItem: {
                        measureIdentifier: 'franchiseFeesIdentifier'
                    }
                }
            ]
        }
    }
];

<div style={{ height: 300 }}>
    <PivotTable
        projectId={projectId}
        measures={measures}
        rows={rows}
        columns={columns}
        sortBy={sortBy}
    />
</div>
```

## Totals

Defining aggregation with the ```totals``` prop adds one or more fixed rows below the table with aggregated measure data.

Supported aggregation functions:
* sum
* count
* average
* minimum
* maximum
* median
* running sum

For information about the aggregation functions, see [Aggregate Table Data](https://help.gooddata.com/display/doc/Aggregate+Table+Data).

```jsx
    // ...using Pivot Table Example

    const totals = {
        measureIdentifier: 'franchiseFeesIdentifier',
        // Aggregation type; possible values: 'sum' | 'count' | 'avg' | 'min' | 'max' | 'median' | 'runsum'
        'sum',
        // local identifier of the first attribute in rows
        attributeIdentifier: 'location'
    };

    <PivotTable
        projectId={projectId}
        measures={measures}
        rows={rows}
        columns={columns}
        totals={totals}
    />
```

## Properties

| Name | Required? | Type | Description |
| :--- | :--- | :--- | :--- |
| projectId | true | string | The project ID |
| measures | false | Measure[] | An array of measure definitions (either measures, or rows, or columns must be provided for the pivot table to render properly) |
| rows | false | Attribute[] | An array of attribute definitions that breaks measure data into rows (either measures, or rows, or columns must be provided for the pivot table to render properly) |
| columns | false | Attribute[] | An array of attribute definitions that breaks measure data into columns (either measures, or rows, or columns must be provided for the pivot table to render properly) |
| totals | false | Total[] | An array of total definitions |
| filters | false | [Filter[]](filter_visual_components.md) | An array of filter definitions |
| config | false | [ChartConfig](chart_config.md) | The configuration object |
| sortBy | false | [SortItem[]](result_specification.md#sorting) | An array of sort definitions |
| locale | false | string | The localization of the table. Defaults to `en-US`. For other languages, see the [full list of available localizations](https://github.com/gooddata/gooddata-react-components/tree/master/src/translations). |
| drillableItems | false | [DrillableItem[]](drillable_item.md) | An array of points and attribute values to be drillable. |
| ErrorComponent | false | Component | A component to be rendered if this component is in error state. See [ErrorComponent](error_component.md).|
| LoadingComponent | false | Component | A component to be rendered if this component is in loading state. See [LoadingComponent](loading_component.md).|
| onError | false | Function | A callback when component updates its error state |
| onLoadingChanged | false | Function | A callback when component updates its loading state |

<!-- These internals are intentionally undocumented
| afterRender | false | Function | A callback after component is rendered |
| dataSource | false | DataSource class | A class that is used to resolve AFM |
| height | false | number | Height of the component in pixels |
| pushData | false | Function | A callback after AFM is resolved |
-->
