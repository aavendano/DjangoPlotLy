# Integrating PlotLy into Django

## Notes

- Updated to use Django 2.0

## Intructions

Very simple introduction about using PlotLy in a Django webapp.

Create your regular Plotly `Figure` with `data` and `layout` :
```python
fig = go.Figure(data=data, layout=layout)
```

Import the function `from plotly.offline import plot` which creates a div to be rendered in the template:
```python
plot_div = plot(fig, output_type='div', include_plotlyjs=False)
```

In the view append the `div` above to the `context_data`:
```python
context['plot'] = plot_div
```

Then in respective template:

1. Add to HTML head:
```html
<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
```

2. Somewhere in the HTML body, call the context the variable and render it as safe:
```html
<div class="col-md-12">{{plot|safe}}</div>
```

Note that I used `include_plotlyjs=False` in the `plotly.offline.plot` and in the top of my template I explcity include the JavaScript for PlotLy. In the case you want to display several plots in same webapp the browser should be smart enough to cache the `plotly-latest.min.js` thus speeding up the the graphic display process.

# TLTR;

Tests using Plot.ly inside Django.

**Testing**

- 1D
- 2D
- 3D
- 1D generated from Ajax (to test plotly speed)
- 1D from CSV files
- Live 2D Plot

## Installation

Requirements are in the requirements.txt file.

Use `virtualenv`:

```bash
virtualenv -p python3 venv
source venv/bin/activate
pip install -U -r requirements.txt
```

# Run it:

```bash
cd site1/
./manage.py makemigrations
./manage.py migrate
./manage.py runserver 0.0.0.0:8000
```

Go to:
[http://127.0.0.1:8000](http://127.0.0.1:8000)


## Code:

The main code is in:
```
site1/app1
```

Views:
```
site1/app1/views.py
```

Code for plots is here:
```
site1/app1/plots.py
```

