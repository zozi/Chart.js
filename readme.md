Chart.js
=======
*Simple HTML5 Charts using the canvas element* [chartjs.org](http://www.chartjs.org)

## Changes
This adds a mouseover and mouseout event to the data points in a line graph (events for all graphs may follow shortly). I implemented it because I needed to add tooltips for the data points, but you can use the event to do whatever you like.

To hook into the events, just specify a mouseover and mouseout event handler for your dataset. This works for browser mouse events as well as mobile touch events.
```javascript
var data = {
  labels : labels,
  datasets : [
    {
      fillColor : "rgba(151,187,205,0.5)",
      strokeColor : "rgba(151,187,205,1)",
      pointColor : "rgba(151,187,205,1)",
      pointStrokeColor : "#fff",
      data : values,
      mouseover: function(data) {
        // data returns details about the point hovered, such as x and y position and index, as
        // well as details about the hover event in data.event
        // You can do whatever you like here, but here is a sample implementation of a tooltip
        var active_value = values[data.point.dataPointIndex];
        var active_date = labels[data.point.dataPointIndex];
        // For details about where this tooltip came from, read below
        tooltip.html(active_date + " - " + active_value).css("position", "absolute").css("left", data.point.x-17).css("top", data.point.y-55).css("display", 'block');
      },
      mouseout: function (data) {
        // Hide the tooltip
        tooltip.html("").css("display", "none");
      }
    }
  ]
};

var ctx = document.getElementById("myCanvasElement").getContext("2d");
var chart = new Chart(ctx).Line(data);
```

As you can see above, we can easily add an HTML tooltip to the data point by using the x and y position of the point hovered. Above, I offset the tooltip by a few pixels, position it absolutely, and format using plain old CSS/HTML. The absolute position works because I wrap my canvas in a relative div and put the tooltip as a sibling to the canvas:
```html
<div style="position: relative;">
  <canvas id="myCanvasElement" width="400" height="400"></canvas>
  <div id="tooltip"></div>
</div>
```

Make your tooltips as fancy as you like now! My implementation:
![Sample Chart.js Tooltip](http://github.com/jhdavids8/Chart.js/raw/master/sample_tooltip.png)

Documentation
-------
You can find documentation at [chartjs.org/docs](http://www.chartjs.org/docs).

License
-------
Chart.js was taken down on the 19th March. It is now back online for good and IS available under MIT license.

Chart.js is available under the [MIT license] (http://opensource.org/licenses/MIT).