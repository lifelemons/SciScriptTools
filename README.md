# SciScriptTools

Small set of tools and functions for scientific code and scripts.

## Install

### pip
```bash
pip install sciscripttools
```

### Build from Source
```
git clone https://github.com/lifelemons/sciscripttools.git
cd sciscripttools
python setup.py install
```
## Examples 
### IO
An example to get started with the IO tools.
It can save relatively basic python objects, such a values, strings, arrays, and 
dictionaries of those items.
```python
import sciscripttools as st

power = [4,5,6]
st.save_data("power_exp_01", power) # save a value, arrary, or dictionary

exp_info = {"id": 20200117, "wire_r" : 0.005, 
            "lengths_1": [0.1, 0.5, 1.5]}
st.save_data("exp_01", exp_info, directory="data/")

w1 = [0.1, 0.5, 1.5]
w2 = [0.1, 0.3, 1.7]
w3 = [0.1, 0.6, 1.2]
radii = st.create_dictionary("w1",w1, "w2", w2, "w3", w3)
st.save_data("radii", radii)
```
Load the previous saved data with
```python
import sciscripttools as st

exp_info = st.load_dictionary("exp_01", directory="data/")
keys, radii = st.load_data("radii", keys = ["w1", "w3"]) # load straight into arrays
power = st.load_item("power_exp_01")
```

### Plot
An example to get started with the plotting tools.
Note: `standard_font` class and the unit functions of the `standard_figure` class require LaTeX!

```python
import numpy as np
import matplotlib.pyplot as plt
import sciscripttools as st

# data
x = np.linspace(0, 2)
y = x + np.random.rand(len(x))
y2 = x + np.random.rand(len(x))

# figure

fig_params = st.figure_parameters() # generate parameters
st.standard_font(font_size = fig_params.font_size) # standarise the font

# normal matplotlib plotting
fig, axes = plt.subplots(1, 2, sharey = True) # create matplotlib figure
ax1, ax2 = axes

# plot data
ax1.plot(x, y)
ax2.plot(x, y2)
for ax in axes:
    ax.set_ylim(0, 3) 

fig.subplots_adjust(wspace = fig_params.adjust_subplot_wspace) # set subplot width spacing
sf = st.standard_figure(fig, axes, fig_params) # create standard_figure
sf.add_subplot_labels()

# add units
ylabel = "Power"; yunit = "\\watt"
sf.ylabel(ax1, ylabel, yunit)
xlabel = "Time"; xunit = "\\second"
sf.xlabel(axes, xlabel, xunit)

fig.savefig("quick_plot.png")
```
![example quick plot](examples/readme_plot_example.png)

## Contribute
Found a bug, want to add functionality, or fixed a bug?
Create an [issue](https://github.com/lifelemons/sciscripttools/issues) or [pull request](https://github.com/lifelemons/sciscripttools/pulls).
Any comments or feedback, please write them down in an [issue](https://github.com/lifelemons/sciscripttools/issues).

## Links
[GitHub](https://github.com/lifelemons/sciscripttools)