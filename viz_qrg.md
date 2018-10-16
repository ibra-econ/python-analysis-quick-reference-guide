
# visualizations-quick-reference-guide [wip]

### Setting up

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
eyJoaXN0b3J5IjpbLTE3MDI2NDc1MTAsMTUzNjQ1NDQ0MiwyMD
Y5MzI1NTg2XX0=
-->