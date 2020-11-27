---
layout: post
title: Bokeh Interactive Visualization in Python App
date: 2019-11-01
comments: true
---

# Why Bokeh?
When building Python web-based apps, we usually need to insert some interactive graphs to make the webpage pretty. JavaScript can easily
do the job. However, if we want to simplify our toolkit, for example, focus in using Python, and don't waste time learning JavaScript, we 
need Python based tools for interactive visualization. Bokeh is a powerful open source Python library that allows developers to generate 
JavaScript data visualization for their web applications without writting any JavaScript. It is one of the easiest way to build interactive visualizations using all Python.

# How to use Bokeh to create interactive visualization?
Assume you have all other packages needed, are using Flask for the web-based part and is running the app in an activated virtual environment. All you need to do now is to add some interactive visualizations into the webpages.
First, install Bokeh into the activated virtual environment using pip:
```
pip install boken=0.12.5
```
Next, create a python file named _interactive_visualization.py_ in the app folder and paste the following code block into it. This code
block has defined a hover tool and a bar chart with customized format. You can modify the format of the bar charts and the hover tool according to your needs.

```
from bokeh.models import HoverTool, FactorRange, Plot, LinearAxis, Grid, Range1d, LabelSet
from bokeh.models.glyphs import VBar
from bokeh.plotting import figure
from bokeh.embed import components
from bokeh.models.sources import ColumnDataSource

def create_hover_tool():
    """Generates the HTML for the Bokeh's hover data tool on our graph."""
    hover_html = """
      <div>
        <span class="hover-tooltip">relative frequency = @frequency</span>
      </div>
    """
    return HoverTool(tooltips=hover_html)

def create_bar_chart(data, title, x_name, y_name, hover_tool=None, width=1060, height=500):
    """ Creates a bar chart plot with the exact styling for the centcom dashboard. Pass in data
    as a dictionary, desired plot title, name of x axis, y axis and the hover tool HTML.
    """

    source = ColumnDataSource(data)
    xdr = FactorRange(factors=data[x_name])
    ydr = Range1d(start=0, end=max(data[y_name])*1.05)

    tools = []
    if hover_tool:
        tools = [hover_tool, ]

    plot = figure(title='', x_range=xdr, y_range=ydr, plot_width=width, plot_height=height, 
                  h_symmetry=False, v_symmetry=False, min_border=0, toolbar_location="above",
                  tools=tools, outline_line_color="#666666")
    
    glyph = VBar(x=x_name, top=y_name, bottom=0, width=0.8, fill_color="#b3de69")
    plot.add_glyph(source, glyph)

    xaxis = LinearAxis()
    yaxis = LinearAxis()

    plot.add_layout(Grid(dimension=0, ticker=xaxis.ticker))
    plot.add_layout(Grid(dimension=1, ticker=yaxis.ticker))
    plot.legend.label_text_font_size = '15pt'
    plot.toolbar.logo = None
    plot.min_border_top = 0
    plot.xgrid.grid_line_color = None
    plot.ygrid.grid_line_color = "#999999"
    plot.yaxis.axis_label = "Frequency"
    plot.yaxis.axis_label_text_font_size = '20pt'
    plot.ygrid.grid_line_alpha = 0.3
    plot.xaxis.axis_label = "Word/Phrase"
    plot.xaxis.axis_label_text_font_size = '20pt'
    plot.xaxis.major_label_orientation = 1
    
    return plot
```

Then, you need to import the above python module, prepare the data for visualization and add the following code into the right place in the _app.py_ file.
```
from interactive_visualization import create_hover_tool, create_bar_chart
```

```
hover = create_hover_tool()
plot = create_bar_chart(data, "Most Frequent Words In Crawled Tweets", "keywords", "frequency", hover)
script, div = components(plot)
```

Keep in mind that _script_ and _div_ are two binary files that contains all information about the interactive graph. They need to be passed into the designated html page as parameters.

Last, we embed _script_ and _div_ into the designated html page so that it will show up in the webpage. This can be achieved by adding
the interactive graph style into the header of the html file.

```
<link href="http://cdn.pydata.org/bokeh/release/bokeh-1.0.4.min.css" rel="stylesheet">
<link href="http://cdn.pydata.org/bokeh/release/bokeh-widgets-1.0.4.min.css" rel="stylesheet">
```

Then add the following part into html file where the interactive graph should be.

```
{{ div|safe }}
<script src="http://cdn.pydata.org/bokeh/release/bokeh-1.0.4.min.js"></script>
<script src="http://cdn.pydata.org/bokeh/release/bokeh-widgets-1.0.4.min.js"></script>
{{ script|safe }}
```
You are done! Relaunch the app and see what happens when you hover your mouse on top of the graph!


# References:
1, https://www.fullstackpython.com/blog/responsive-bar-charts-bokeh-flask-python-3.html
