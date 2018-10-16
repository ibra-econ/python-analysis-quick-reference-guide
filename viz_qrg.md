
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

**Legends:**
Add labels to each of your plots, then call those in the legend. You must call plt.legend (or ax.legend, if you have a reference to the axes) to create the legend, whether or not you passed the label options when plotting the data.

    plt.plot(data, 'k--', label='Default')
    plt.legend(loc='best')



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

## Boxplots

    df['col1_groups'] = pd.qcut(df['col_1'], 2, labels=['label_1', 'label_2'])
    
    df.boxplot(column='col_2', by='col1_groups', figsize=(12,8), fontsize=28)


<!--stackedit_data:
eyJoaXN0b3J5IjpbNDE1NjIwMjQ4LDkzNTk0OTQxNywxNTM2ND
U0NDQyLDIwNjkzMjU1ODZdfQ==
-->