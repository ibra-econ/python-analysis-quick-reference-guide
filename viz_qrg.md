
# visualizations-quick-reference-guide [wip]

## Setting up

    import matplotlib.pyplot as plt
    %matplotlib notebook 	# essential to making visualizations show in iPython
    %matplotlib inline 		# another option for making visualizations show in iPython -- more lightweight.

### Figures and subplots
Plots exist in a Figure. Create a new figure using:

    fig_name = plt.figure()

You can then create subplots in the figure by using the add_subplot function. Below creates a 2x2 grid of subplots and populates three of them.

    ax1 = fig.add_subplot(2, 2, 1) 
    ax2 = fig.add_subplot(2, 2, 2) 
    ax3 = fig.add_subplot(2, 2, 3)

Then to plot on your subplots, simply use the axis name.

    ax1.plot(my_data.cumsum(), 'k---') # creates a cumulative dotted line chart

To quickly make subplots that share an axis, use:

    fig, axis = plt.subplots( 2, 2, sharey=True, sharex=True)

### Styling of subplots:
Remove and adjust space between and around subplots:

    plt.subplots_adjust(left=None, bottom=None, right=None, top=None, wspace=0, hspace=0)

**Color and style of lines:**
You can see the full set of line styles by looking at the docstring for plot (use plot? in IPython or Jupyter).

    ax.plot(x, y, linestyle='--', color='#CECECE')
    ax.plot(x, y, linestyle='dashed', marker='o')
    ax.plot(x, y, linestyle='-', drawstyle='steps-post')

Marker options provided by [Towards Data Science](https://towardsdatascience.com/all-your-matplotlib-questions-answered-420dd95cb4ff):
![Marker options provided by Towards Data Science](https://cdn-images-1.medium.com/max/1600/1*j9c5-jeNtFSomokdYMeaiA.png)

**Legends and labels:**
Add labels to each of your plots, then call those in the legend. You must call plt.legend (or ax.legend, if you have a reference to the axes) to create the legend, whether or not you passed the label options when plotting the data.

    plt.plot(data, 'k--', label='Default')
    plt.legend(loc='best')
If you aren’t picky, 'best' is a good option, as it will choose a location that is most out of the way. To exclude one or more elements from the legend, pass no label or label='_nolegend_'.

Set tick values and labels.

    plt.set_xticks([0,1,2,3])
    plt.set_xticklabels(['one', 'two', 'three'], rotation = 30, fontsize='small')
    plt.set_xlabel('x axis')
    OR
    plt.ylabel('X LABEL', fontsize = 15) #for y label  
    plt.xlabel('Y LABEL', fontsize = 15) #for x label

Set title.

    ax.set_title('My first matplotlib plot')
Add grid to plots.

    plt.grid(True)

**Axes Limits:**
Set x and y axis ranges for plot. Can also be set on the axes level using ax.xlim().

    plt.xlim([0, 10])
    plt.ylim([-10, 10])

**Add annotations:**

    ax.text(x, y, 'Hello world!', family='monospace', fontsize=10)
    ax.annotate(
	    label, 
	    xy=(x_var, my_df.y_var(x_var) + 75), 
	    xytext=(x_var, my_df.asof(x_var) + 225), 
	    arrowprops=dict(facecolor='black', headwidth=4, 
					    width=2, headlength=4), 
					    horizontalalignment='left', 
					    verticalalignment='top')

You can also add shapes to a plot by using `patches` including Rectangle, Circle and Polygon.

**Saving plots to a file:**

    plt.savefig('figpath.svg')

## Pandas plotting

**Pandas plotting basics:**
Most of pandas’s plotting methods accept an optional ax parameter, which can be a matplotlib subplot object. This gives you more flexible placement of subplots in a grid layout.

The plot attribute contains a “family” of methods for different plot types. For exam‐ ple, df.plot() is equivalent to df.plot.line(). 
- label: Label for plot legend ax matplotlib subplot object to plot on; if nothing passed, uses active matplotlib subplot 
- style: Style string, like 'ko--', to be passed to matplotlib 
- alpha: The plot fill *opacity* (from 0 to 1) 
- kind: Can be 'area', 'bar', 'barh', 'density', 'hist', 'kde', 'line', 'pie' 
- logy: Use logarithmic scaling on the y-axis 
- use_index: Use the object index for tick labels 
- rot: Rotation of tick labels (0 through 360) 
- xticks: Values to use for x-axis ticks 
- yticks: Values to use for y-axis ticks 
- xlim and ylim: axis limits (e.g., [0, 10]) 
- grid: Display axis grid (on by default)

**DataFrame plot arguments:**


## Scatterplots

    scatter(df['col_1'], df['col_2'])

OR 

    plot(df['col_name_x'], df['col_name_y'], marker='o', color='blue', linestyle='None')
    xlabel('col_name_x')
    ylabel('col_name_y')
    title('title')
    show()

**Markers**
-   marker='o' for circles. 
-   marker='s' for square marks
-   marker='p' for pentagons
-   marker='.' for points
-   marker='^' for upward-pointing triangle, and on and on.

**Linestyle**
-   linestyle='None' for no line
-   linestyle='-' for plain line
-   linestyle='--' for dashed line
-   linestyle='-.' for dotted-dashed line, and many others.

**Scatte

## Boxplots

    df['col1_groups'] = pd.qcut(df['col_1'], 2, labels=['label_1', 'label_2'])
    
    df.boxplot(column='col_2', by='col1_groups', figsize=(12,8), fontsize=28)

## Histogram
A histogram is a kind of bar plot that gives a discretized display of value frequency. The data points are split into discrete, evenly spaced bins, and the number of data points in each bin is plotted.

    my_df['column_name'].plot.hist(bins=50)

A related plot type is a density plot, which is formed by computing an estimate of a continuous probability distribution that might have generated the observed data.

    my_df['column_name'].plot.density()

**Histogram and density plot together with seaborn**
Seaborn makes histograms and density plots even easier through its distplot method, which can plot both a histogram and a continuous density estimate simultaneously.

    sns.distplot(values, bins=100, color='k')



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMDYzNzkzMjMsMTM2Nzg0MzcxMCwxND
Y5MTMzMDg2LC0yMDA3NDU5NTQ0LC0yMTE0MDA2NDA2LC0xNjg2
Mzc3NTc5LC05NzExOTYzODIsNDE1NjIwMjQ4LDkzNTk0OTQxNy
wxNTM2NDU0NDQyLDIwNjkzMjU1ODZdfQ==
-->