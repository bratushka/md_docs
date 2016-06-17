# Matplotlib
[Documentation](http://matplotlib.org/api/pyplot_summary.html) 

**Table of Contents**

[TOC]

---

### Jupyter
*run this in Jupiter Notebook to have inline plots with `plt.show()`*

```python
%matplotlib inline
```

---

### Import

*`plt` is a common practice to rename matplotlib.pyplot*

```python
import matplotlib.pyplot as plt
```

---

### plt.plot()

*Function to construct a plot.*
Syntax:
```python
plt.plot(*args, **kwargs)

    x = (0, 1, 2, 3)     # values of x (optional) 
    y = (12, 45, 22, 39) # values of y

    plot(x, y)        # plot x and y using default line style and color
    plot(x, y, 'bo')  # plot x and y using blue circle markers
    plot(y)           # plot y using x as index array 0..N-1
    plot(y, 'r+')     # ditto, but with red plusses
```

`plot(x1, y1, 'g^', x2, y2, 'g-')` will create 2 plots, which will be shown together on the same image when `plt.show()`

There is a number of `**kwargs`, which can be used during plotting. If you make multiple lines with one plot command, the `**kwargs` apply to all those lines.
Example:
```python
plot(x1, y1, x2, y2, antialiased=False, color='green', linestyle='dashed', marker='o', markerfacecolor='blue')
```
To check all the `**kwargs` use `help(plt.plot)`

---

### plt.scatter()

*Make a scatter plot of **x** vs **y**, where x and y are sequence like objects of the same lengths.*

Syntax:
```python
plt.scatter(x, y, s=20, c=None, marker='o', cmap=None, norm=None, vmin=None, vmax=None, alpha=None, linewidths=None, verts=None, edgecolors=None, hold=None, data=None, **kwargs)
```

---

### plt labels

```python
plt.xlabel("Day")     # Label for x axis (horisontal)
plt.ylabel("Celsius") # Label for y axis (vertical)
```

---

### plt.axis

*Function to set dimentions to the plot.*
Syntax:
```python
plt.axis([xmin, xmax, ymin, ymax])
```

---

### plt.fill_between

*Makes filled polygons between two curves.*

Syntax:
```python
plt.fill_between(x, y1, y2=0, where=None, interpolate=False, step=None, hold=None, data=None, **kwargs)
```

---

### plt.figure

*Creates a new figure.*
Syntax:
```python
plt.figure(num=None, figsize=None, dpi=None, facecolor=None, edgecolor=None, frameon=True, FigureClass=<class 'matplotlib.figure.Figure'>, **kwargs)
```

---

### plt.subplot

*Creates a new plot inside the current figure.*
Syntax:
```python
plt.subplot(nrows, ncols, plot_number, **kwargs)
# or
plt.subplot(nrows-ncols-plot_number: int, **kwargs)
```

---

### plt.title

*Add a title to current plot*
Syntax:
```python
plt.title(s, *args, **kwargs)
```

---

### plt.text

*Add text in string `s` to axis at location `x`, `y`, data coordinates.*
Syntax:
```python
plt.text(x, y, s, fontdict=None, withdash=False, **kwargs)
```
