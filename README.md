d3-state-visualizer
===================
Enables real-time visualization of your application state.

[Demo](http://romseguy.github.io/d3-state-visualizer)

[Demo source code](https://github.com/romseguy/d3-state-visualizer/tree/boilerplate)

## Installation

`npm install d3-state-visualizer`

## Usage

```javascript
import { charts } from 'd3-state-visualizer';

const appState = {
  todoStore: {
    todos: [
      { title: 'd3'},
      { title: 'state' },
      { title: 'visualizer' },
      { title: 'tree' }
    ],
    completedCount: 1
  }
};

const render = charts.tree(document.getElementById('root'), {
  state: appState,
  id: 'treeExample',
  size: 1000,
  aspectRatio: 0.5,
  isSorted: false,
  widthBetweenNodesCoeff: 1.5,
  heightBetweenNodesCoeff: 2,
  style: {border: '1px solid black'},
  tooltipOptions: {offset: {left: 30, top: 10}, indentationSize: 2}
});

render();
```
## Charts API

The APIs are minimal and consists of a single function you provide with:
- a DOM element
- a plain old JS object for options.

#### Tree

 This chart is a bit special as it accepts either one of the two following options, but **not both**:
 
- `tree`: a properly formed tree structure such as one generated by [map2tree](https://github.com/romseguy/map2tree) or [react2tree](https://github.com/romseguy/react2tree)
- `state`: a plain javascript object mapping arbitrarily nested keys to values – which will be transformed into a tree structure, again using [map2tree](https://github.com/romseguy/map2tree).

Other options are listed below and have reasonable default values if you want to omit them:

Option                    | Type     | Default     | Description
--------------------------|----------|-------------|-------------------------------------------------------------------------
`id`                      | String   | `'d3svg'`   | Sets the identifier of the SVG element —i.e your chart— that will be added to the DOM element you passed as first argument
`style`                   | Object   | `{}`        | Sets the CSS style of the chart
`size`                    | Number   | `500`       | Sets size of the chart in pixels
`aspectRatio`             | Float    | `1.0`       | Sets the chart height to `size * aspectRatio` and [viewBox](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/viewBox) in order to preserve the aspect ratio of the chart. [Great video](https://www.youtube.com/watch?v=FCOeMy7HrBc) if you want to learn more about how SVG works
`widthBetweenNodesCoeff`  | Float    | `1.0`       | Alters the horizontal space between each node
`heightBetweenNodesCoeff` | Float    | `1.0`       | Alters the vertical space between each node
`isSorted`                | Boolean  | `false`     | Sorts the chart in alphabetical order
`transitionDuration`      | Number   | `750`       | Sets the duration of all the transitions used by the chart
`tooltipOptions`          | Object   | [here](https://github.com/romseguy/d3tooltip) | Sets the options for the [tooltip](https://github.com/romseguy/d3tooltip) that is showing up when you're hovering the nodes
`rootKeyName`             | String   | `'state'`   | Sets the first node's name of the resulting tree structure. **Warning**: only works if you provide a `state` option
`pushMethod`              | String   | `'push'`    | Sets the method that shall be used to add array children to the tree. **Warning**: only works if you provide a `state` option

More to come...

## Bindings

View components are now provided along with the charts, but it makes sense to have different repositories if this project gets some attention.

### Plain React

[TreeChart](https://github.com/romseguy/d3-state-visualizer/blob/master/src/components/TreeChart.js) component.

```javascript
import { components } from 'd3-state-visualizer'

const { TreeChart } = components;
const options = {
  id: 'chartSvgId',
  size: 1000,
  aspectRation: 0.5,
  heightBetweenNodesCoeff: 1,
  widthBetweenNodesCoeff: 1.5,
  style: {float: 'left'},
  tooltipOptions: {left: 0, top: 0, indentationSize: 2}
};

class MyApp extends React.Component {
  render() {
    return (
      <div>
        <TreeChart state={this.props.state} ...options />
        <Container/>
      </div>
    );
  }
}
```

[example](https://github.com/romseguy/d3-state-visualizer/tree/master/examples/react-tree) implementation.

## Roadmap

* Provide more components such as `DockedTreeChart`
* Search box to filter the tree down
* Threshold for large arrays so only a single node is displayed instead of all the children. That single node would be exclude from searching until selected.
