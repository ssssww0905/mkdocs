# 绘图工具Matplotlib

## Markers

### Marker Reference

| Marker | Description    |
| ------ | -------------- |
| 'o'    | Circle         |
| '*'    | Star           |
| '.'    | Point          |
| ','    | Pixel          |
| 'x'    | X              |
| 'X'    | X (filled)     |
| '+'    | Plus           |
| 'P'    | Plus (filled)  |
| 's'    | Square         |
| 'D'    | Diamond        |
| 'd'    | Diamond (thin) |
| 'p'    | Pentagon       |
| 'H'    | Hexagon        |
| 'h'    | Hexagon        |
| 'v'    | Triangle Down  |
| '^'    | Triangle Up    |
| '<'    | Triangle Left  |
| '>'    | Triangle Right |
| '1'    | Tri Down       |
| '2'    | Tri Up         |
| '3'    | Tri Left       |
| '4'    | Tri Right      |
| '\|'   | Vline          |
| '_'    | Hline          |



### Line Reference

| Line Syntax | Description        |
| ----------- | ------------------ |
| '-'         | Solid line         |
| ':'         | Dotted line        |
| '--'        | Dashed line        |
| '-.'        | Dashed/dotted line |



### Color Reference

| Color Syntax | Description |
| ------------ | ----------- |
| 'r'          | Red         |
| 'g'          | Green       |
| 'b'          | Blue        |
| 'c'          | Cyan        |
| 'm'          | Magenta     |
| 'y'          | Yellow      |
| 'k'          | Black       |
| 'w'          | White       |



### Format Strings `fmt`

!!! note "note: This argument cannot be passed as keyword."
    fmt = '[marker] [line] [color]'

### Marker Size

`markersize` or `ms`

### Marker Color

`markeredgecolor` or `mec`

`markerfacecolor` or `mfc`

```python
...
plt.plot(ypoints, marker = 'o', ms = 20, mec = '#4CAF50', mfc = '#4CAF50')
...
```



## Line



### Line Styles

`linestyle` or `ls`

| Style             | Or        |
| ----------------- | --------- |
| 'solid' (default) | '-'       |
| 'dotted'          | ':'       |
| 'dashed'          | '--'      |
| 'dashdot'         | '-.'      |
| 'None'            | '' or ' ' |



### Line Color

`color` or `c`



### Line Width

`linewidth` or `lw`



## Labels

```python
font1 = {'family':'serif','color':'blue','size':20}
font2 = {'family':'serif','color':'darkred','size':15}

plt.title("Sports Watch Data", fontdict = font1)
plt.xlabel("Average Pulse", fontdict = font2)
plt.ylabel("Calorie Burnage", fontdict = font2)
```



## Grid

Display only grid lines for the x-axis:

`plt.grid(axis = 'x')` 

Display only grid lines for the y-axis:

`plt.grid(axis = 'y')`

Set the line properties of the grid:

`plt.grid(color = 'green', linestyle = '--', linewidth = 0.5)`



## Subplot

The `subplot()` function takes three arguments that describes the layout of the figure.

The layout is organized in rows and columns, which are represented by the *first* and *second* argument.

The third argument represents the index of the current plot.

```python
plt.subplot(1, 2, 1)
# the figure has 1 row, 2 columns, and this plot is the first plot.
plt.subplot(1, 2, 2)
# the figure has 1 row, 2 columns, and this plot is the second plot.
```

* You can add a title to each plot with the title() function.
* You can add a title to the entire figure with the suptitle() function.



## Scatter



### ColorMap

The Matplotlib module has a number of available colormaps.

A colormap is like a list of colors, where each color has a value that ranges from 0 to 100.

```python
plt.scatter(x, y, c=colors, cmap='viridis')
plt.colorbar()
```



### Available ColorMaps

[Choosing Colormaps in Matplotlib](https://matplotlib.org/3.4.3/tutorials/colors/colormaps.html)



### Size

You can change the size of the dots with the `s` argument.



### Alpha

You can adjust the transparency of the dots with the `alpha` argument.

```python title="Combine Color Size and Alpha"
import matplotlib.pyplot as plt
import numpy as np

x = np.random.randint(100, size=(100))
y = np.random.randint(100, size=(100))
colors = np.random.randint(100, size=(100))
sizes = 10 * np.random.randint(100, size=(100))

plt.scatter(x, y, c=colors, s=sizes, alpha=0.5, cmap='nipy_spectral')
plt.colorbar()
plt.show()
```



