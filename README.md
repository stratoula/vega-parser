# vega-parser

Parse Vega specifications to runtime dataflow descriptions.

## API Reference

<a name="parse" href="#parse">#</a>
vega.<b>parse</b>(<i>specification</i>[, <i>config</i>])
[<>](https://github.com/vega/vega-loader/blob/master/src/parse.js "Source")

Parses a Vega JSON *specification* as input and produces a reactive dataflow
graph description for a visualization. The output description uses the format
of the [vega-runtime](https://github.com/vega/vega-runtime) module. To create
a visualization, use the runtime dataflow description as the input to a Vega
[View](https://github.com/vega/vega-view) instance.

The optional *config* object provides visual encoding defaults for marks,
scales, axes and legends. Different configuration settings can be used to
change choices of layout, color, type faces, font sizes and more to realize
different chart themes. For more, see the configuration documentation below
or view the source code defining Vega's
[default configuration](https://github.com/vega/vega-parser/blob/master/src/config.js).

In addition to passing configuration options to this [parse](#parse) method,
Vega JSON specifications may also include a top-level `"config"` block
specifying configuration properties. Configuration options defined within a
Vega JSON file take precedence over those provided to the parse method.

## Configuration Reference

The Vega parser accepts a configuration file that defines default settings
for a variety of visual encoding choices. Different configuration files can be
used to "theme" charts with a customized look and feel. A configuration file is
simply a JavaScript object with a set of named properties, grouped by type.

- [Top-Level Properties](#top-level-properties)
- [Mark Properties](#mark-properties)
- [Axis Properties](#axis-properties)
- [Legend Properties](#legend-properties)
- [Scale Range Properties](#scale-range-properties)

### Top-Level Properties

Properties defined in the top-level scope of the configuration object.

- *autosize*: Default automatic sizing setting. Options: `"none"`, `"pad"`, `"fit"`.
- *background*: Background color of the view component, or `null` for transparent.

### Mark Properties

Properties defining default attributes for visualized marks. These properties
are defined within blocks with names matching a valid mark type (e.g.,
`"area"`, `"line"`, `"rect"`, and `"group"`). The valid properties within each
block consist of the legal mark properties (e.g., `"fill"`, `"stroke"`,
`"size"`, `"font"`).

### Axis Properties

Properties defining default settings for axes. These properties are defined
within an `"axis"` property block, which applies to all axes. Additional
property blocks can target more specific axis types based on the orientation
(`"axisX"`, `"axisY"`, `"axisLeft"`, `"axisTop"`, etc.) or band scale type
(`"axisBand"`). For example, properties defined under the `"axisBand"` block
will only apply to axes visualizing `"band"` scales. If multiple axis config
blocks apply to a single axis, type-based options take precedence over
orientation-based options, which in turn take precedence over general options.

- *minExtent*: The minimum extent (in pixels) that axis ticks and labels should use. This determines a minimum offset value for axis titles.
- *maxExtent*: The maximum extent (in pixels) that axist ticks and labels should use. This determines a maximum offset value for axis titles.
- *bandPosition*: An interpolation fraction indicating where, for `band` scales, axis ticks should be positioned. A value of `0` places ticks at the left edge of their bands. A value of `0.5` places ticks in the middle of their bands.
- *domainDefault*: Boolean flag indicating if axis domain line should be included by default.
- *domainWidth*: Stroke width of axis domain line.
- *domainColor*: Color of axis domain line.
- *gridDefault*: Boolean flag indicating if axis grid lines should be included by default.
- *gridWidth*: Stroke width of axis grid lines.
- *gridColor*: Color of axis grid lines.
- *gridDash*: Stroke dash of axis grid lines (or `[]` for solid lines).
- *gridOpacity*: Opacity of axis grid lines.
- *tickColor*: Color for axis ticks.
- *tickExtra*: Boolean flag indicating if an extra axis tick should be added for the initial position of the axis. This flag is useful for styling axes for `band` scales such that ticks are placed on band boundaries rather in the middle of a band. Use in conjunction with `"bandPostion": 1` and an axis `"padding"` value of `0`.
- *tickRound*: Boolean flag indicating if pixel position values should be rounded to the nearest integer.
- *tickSize*: Size (or length, in pixels) of axis ticks.
- *tickWidth*: Width (in pixels) of axis ticks.
- *tickPadding*: Padding (in pixels) betweem axis ticks and tick labels.
- *tickLabelColor*: Text color for axis tick labels.
- *tickLabelFont*: Font name for axis tick labels.
- *tickLabelFontSize*: Font size for axis tick labels.
- *titleColor*: Text color for axis titles.
- *titleFont*: Font name for axis titles.
- *titleFontSize*: Font size for axis titles.
- *titleFontWeight*: Font weight for axis titles.
- *titleAlign*: Horizontal text alignment for legend titles.
- *titlePadding*: Padding (in pixels) between axis tick labels and titles.

### Legend Properties

Properties defining default settings for legends. These properties are defined
within a `"legend"` property block.

- *orient*: Default legend orientation (e.g., `"right"` or `"left"`).
- *offset*: Offset (in pixels) of the legend from the chart body.
- *padding*: Padding (in pixels) between legend border and contents.
- *entryPadding*: Padding (in pixels) between legend entries in a symbol legend.
- *gradientWidth*: Width (in pixels) of color ramp gradients.
- *gradientHeight*: Height (in pixels) of color ramp gradients.
- *gradientStrokeColor*: Stroke color for color ramp gradient borders.
- *gradientStrokeWidth*: Stroke width for color ramp gradient borders.
- *gradientLabelBaseline*: Text baseline for color ramp gradient labels.
- *gradientLabelOffset*: Vertical offset (in pixels) for color ramp gradient labels.
- *labelColor*: Text color for legend labels.
- *labelFont*: Font name for legend labels.
- *labelFontSize*: Font size (in pixels) for legend labels.
- *labelAlign*: Horizontal text alignment for legend labels.
- *labelBaseline*: Vertical text baseline for legend labels.
- *labelOffset*: Horizontal offset (in pixels) between legend symbols and labels.
- *symbolType*: Default shape type (such as `"circle"`) for legend symbols.
- *symbolSize*: Default symbol area size (in pixels<sup>2</sup>).
- *symbolColor*: Default legend symbol color.
- *symbolStrokeWidth*: Default legend symbol stroke width.
- *titleColor*: Text color for legend titles.
- *titleFont*: Font name for legend titles.
- *titleFontSize*: Font size (in pixels) for legend titles.
- *titleFontWeight*: Font weight for legend titles.
- *titleAlign*: Horizontal text alignment for legend titles.
- *titleBaseline*: Vertical text baseline for legend titles.
- *titlePadding*: Padding (in pixels) between the legend title and entries.

### Scale Range Properties

Properties defining named range arrays that can be used within scale
range definitions (such as `{"type": "ordinal", "range": "category"}`).
These properties are defined within a `"range"` block.

- *category*: Array of colors for the default categorical palette.
- *symbol*: Array of symbol names for the default shape palette.
