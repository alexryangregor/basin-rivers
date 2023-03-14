Resilient rivers and basins
===========================

Overview 
________
The Resilient rivers and basins beta app is a tool that describes forest cover and forest cover change from a watershed perspective by calculating statistics across sub-watersheds and over time. Watersheds of interest will be defined by the upstream basin draining to any given point. All these processes can be conducted directly in your SEPAL instance without the need for any other resources. 

To run this module, we recommend initializing a machine with at least 4GB RAM (a t2 or m2 instance). For more detailed instructions, please refer to `this documentation <https://docs.sepal.io/en/latest/modules/index.html#start-instance-manually>`_.

Inputs
______

Once you have started an instance an instance, `search in the apps tab <https://docs.sepal.io/en/latest/modules/index.html#start-applications>`_ for the “resilient rivers and basins” app.  Wait for some seconds and the app will show up. The module is composed of two main sections: (1) the left sidebar where you can find all the processes (inputs and results) at the top and some helpful links (bug report, wiki, source code…) at the bottom and (2) the right side panel where the process and inputs are displayed. 

By default, the input drawer will be active. The input drawer is divided into two main panels. On the left, you can find all the input parameters to derive statistics. On the right, you have the map view where calculated layers will be loaded. 

.. thumbnail:: https://raw.githubusercontent.com/sepal-contrib/basin-rivers/master/doc/img/inputs.png 
    :width: 80% 
    :title: Inputs view 
    :group: inputs 


The first input needed is a coordinate pair.  These coordinates will be used to calculate and retrieve all the upstream sub-basins that drain to that point for any given hydroBASIN level. To input coordinates, the module has two options: manual and automatic. Using manual selection, you can directly type the latitude and longitude coordinates.  You can then click :code:`next` and the map will set a blue marker at that point and zoom into the area of interest. To use automatic selection, switch off the manual switch and navigate through the map to find your desired area.  Click on the exact spot, usually a river confluence or a bridge but terrestrial areas work as well, and a blue marker will be displayed. 

 

.. thumbnail:: https://raw.githubusercontent.com/sepal-contrib/basin-rivers/master/doc/img/coordinates.png 
    :width: 55% 
    :title: Inputs view 
    :group: inputs 
 

.. note::

    When using the automatic coordinate selection method, the latitude and longitude input text fields will be deactivated. Notice that the coordinate will be automatically synchronized as you pass the cursor over the map. 

The next step is to select the HydroBASIN target level by using the dropdown list.  HydroBASINs are delineated basin the HydroATLAS database. HydroBASIN levels range from 5 to 12 where higher numbers indicated smaller basins nested inside larger sub-basins. For more info about how these data are obtained, please refer directly to the `HydroSHEDS documentation <https://www.hydrosheds.org/products/hydrobasins>`_.

The forest cover change map is based on the `Hansen et al., 2013 Global Forest Change product <https://www.science.org/doi/10.1126/science.1244693>`_ retrieved `Google Earth Engine <https://developers.google.com/earth-engine/datasets/catalog/UMD_hansen_global_forest_change_2021_v1_9>`_. This product was created to show forest cover change at a global scale based on Landsat imagery. This product has forest change data from the year 2001 to the year 2000 as the baseline. The resilient rivers and basins app will crop and summarize forest cover statistics for each of the forest cover classes at the selected basin scale (HydroBASIN level). To begin, select the start and end year using the sliders. Next, select the forest threshold. Forest threshold determines the level of tree cover required for a pixel in the Hansen product to be classified as forest. Constraining or unbridling the value will have alter the amount of forest cover or forest cover change observed. 

.. thumbnail:: https://raw.githubusercontent.com/sepal-contrib/basin-rivers/master/doc/img/levels.png 
    :width: 55% 
    :title: Settings levels 
    :group: inputs 

Click the :btn:`get upstream basins` button to run the process. After a few seconds, the results will be output as a map of forest cover change by sub-basin.  

.. note::
    Depending on the selected HydroBASIN level and the location of the downstream point, the calculation step will take more or less time. Also, the number of sub-basins displayed will vary by the downstream point. The watershed draining to a point at the mouth of a fairly mountainous area will include more upstream sub-basins than a watershed draining to a higher-level point in the same orography. 

To start a new process, you can use the top left trash bin button in the map to remove the downstream point or to remove the sub-basins selection (see the next section, how to constrain the analysis to a given set of sub-basins). 

.. thumbnail:: https://raw.githubusercontent.com/sepal-contrib/basin-rivers/master/doc/img/trash_bin.png 
    :width: 30% 
    :title: Trash bin 
    :group: inputs 


To calculate and display statistical results in the results dashboard, use the statistics tile. There are two selection methods: use all basins (e.g., no filter) and filter. When using the filter option, a new dropdown menu will appear at the bottom of the tile with all the sub-basin ids. Manually select or remove sub-basins by clicking each row. Notice that the map will automatically sync the selected basins by displaying a black boundary and zooming in. Click the “calculate statistics” button and wait until the state of the button changes from loading to fixed. 

Once the dashboard is calculated, a red dot will be displayed in the results drawer, as in the below image: 

.. thumbnail:: https://raw.githubusercontent.com/sepal-contrib/basin-rivers/master/doc/img/results_done.png 
    :width: 30% 
    :title: Done drawer 
    :group: inputs 
 

Dashboard
_________

The dashboard panel is divided into three main sections:, the top-left settings tile, the top-right overall pie chart, and detailed charts at the bottom. 

.. tip::

    All the graphs have an option for independent download directly to your browser. Simply hover the cursor in the top right corner and click on the :icon:`fa-solid fa-camera` icon.

In the settings tile, you can choose the variable to display: all, gain and loss, loss, non-forest, forest, and gain. By choosing one of these options, all graphs will display the selected statistics. From this menu you can also filter the data by one or more sub-basins, allowing also the possibility to generate dynamic comparisons between areas. 

.. thumbnail:: https://raw.githubusercontent.com/sepal-contrib/basin-rivers/master/doc/img/stats_card.png 
    :width: 73% 
    :title: Statistics card 
    :group: dashboard 
 

The overall ratio is an interactive pie chart that displays the output variable by proportion of each sub-category. This pie chart also allows you to directly select one sub-category to be used in the detailed charts. Simply click any sub-category and the corresponding slice will pop out. 

.. thumbnail:: https://raw.githubusercontent.com/sepal-contrib/basin-rivers/master/doc/img/overal_pie_ratio.png 
    :width: 55% 
    :title: Overall pie ratio 
    :group: dashboard 
 

The detailed charts at the bottom interactively display both the ratio and the total area of the selected variable. On the left, the pie chart shows the proportion of the area for each of the selected sub-basins while the right bar chart displays the absolute values. 

.. note::

    Remember that in the Hansen dataset, only forest loss has a temporal dimension.. When a new time period is selected, a new graph representing the trend of forest loss will be displayed at the bottom of the screen.

.. image:: https://raw.githubusercontent.com/sepal-contrib/basin-rivers/master/doc/img/interactive_stats.gif
