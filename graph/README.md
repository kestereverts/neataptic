## Drawing a graph
Visualising neural networks gives insight on which node have a larger effect on the output. And especially in evolving neural networks, it shows the characteristics of an ideal network. Setting up a graph is fairly easy:

#### Index.html
The html file should include [d3v3](http://d3js.org/d3.v3.min.js) and [webcola](http://marvl.infotech.monash.edu/webcola/cola.v3.min.js). Ofcourse you should also provide the neataptic.js file and the graph.js file from above. This is an example of the html file:
```html
<html>
  <head>
    <script src="libs/d3v3.js"></script>
    <script src="libs/webcola.js"></script>

    <script src="/libs/neataptic.js"></script>
    <script src="/libs/graph.js"></script>
 
    <script src="script.js"></script>
    
    <link rel="stylesheet" type="text/css" href="/libs/graph.css">
  </head>
  <body>
    <div class="container">
      <div class="row">
        <svg class="draw" width="1000px" height="1000px"/>
      </div>
    </div>
  </body>
</html>
```

#### Script.js
If you want to work from a script, make sure to use the jquery `$( document ).ready()` function. Drawing the graph looks something like this then:

```javascript

// Global var
var network;

$( document ).ready(function() {
  network = new neataptic.Architect.Perceptron(2, 10, 6, 5, 35, 1);
  drawGraph(network.graph(1000, 1000), '.draw');
});
```

You can draw a graph using:
```javascript
drawGraph(data, dom_element);
```

Retrieve your networks graph:
```javascript
var data = myNetwork.graph(width, height);
```

#### Graph.js
In the graph.js file, make sure to set the `WIDTH` and `HEIGHT` to the desired amount.

```javascript
[...]
var NODE_RADIUS = 7;     // radius of circles on graph
var REPEL_FORCE = 10;    // force power between circles
var LINK_DISTANCE = 100; // length of a connection

var WIDTH = 1000;        // width of your graph
var HEIGHT = 500;        // height of your graph
[...]
```

#### Graph.css
Make sure to include graph.css in your html file. This makes sure your connections are visible and makes the nodes more eye-appealing.

## Disable constraints
Normally graphs look like the network on the left. If you want a more fluid design, disable constraints, and you'll get a graph like on the right:

<img src="https://camo.githubusercontent.com/4a9aa3c7ad75705ce1d3eaf5e0321a95f89882ac/68747470733a2f2f692e6779617a6f2e636f6d2f35663035323435656463303264346332383039376434303932383536386565312e706e67" width="50%"/><img src="https://i.gyazo.com/3a49943c195b454cf711e77b3bfbfd62.png" width="50%"/>

In `graph.js`, remove line 60:

```js
.constraints(graph.constraints) // remove this line
```

This basically makes the input and output nodes less distinguishable.

## Show activation
You can also draw graphs that display which nodes have a higher state linked to a certain input. Make sure to activate the network before visualising it. Something like this:

<img src="https://i.gyazo.com/84e731eab3b1fabf410ee0d14c18bacb.png"/>
<i>Light green is low activation, dark red is high activation</i>


All you have to is add an extra parameter to `drawGraph()`:

```javascript
drawGraph(network.graph(1000, 800), '.svg', true); // set it to true
```
