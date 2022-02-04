# Protein_Expression
Visualizes a heatmap of distribution of protein expression spots in images of mouse brain physical slices acquired by widefield transmission microscopy.

**Plugin for [ImageJ/Fiji](https://fiji.sc/).**

### Short description

As an input the plugin takes a *2-channel 32-bit image data*.

In the 1st channel, left-in grey, there is a multi-tile picture of a physical slice of a mouse brain captured by Leica DM6000 widefield microscope in the transmission mode (provided by Dr. Helena Janíčková, Laboratory of Neurochemistry, Institute of Physiology of the Czech Academy of Sciences, Prague, Czech Republic). Protein expression, FOS protein, is depicted by bright spots. In the 2nd channel, middle, there is a result of a segmentation procedure with the bright spots in the 1st channel labeled by colors. Each segmented spot has been labeled uniquely by a different color. On the right there is the input for the plugin - both channels, the original image and labels, together in one composite image.

![FOS-EX01-Panel-Input](https://user-images.githubusercontent.com/63607289/152369509-913c61f3-02aa-4e02-be6d-da42d72cf0e8.jpg)

Protein expression (PE) spots were segmented with the help of [StarDist](https://github.com/stardist/stardist) project. A new DL model was created and trained with sub-images of PE spots manually annotated by [Labkit](https://imagej.net/plugins/labkit/). Left-a sub-image, right-an example of manual annotation.

![Labkit](https://user-images.githubusercontent.com/63607289/152375382-8ab50351-d277-458d-b7ab-93c95a31b23f.jpg)

When the plugin is applied, then three image windows appear. Left-an original composite image, middle-an image with labels filtered out according to mean intensity of PE spots in the 1st channel, right-the resulting heatmap of the size 20x20 with ratios of numbers of labels in grid areas in the filtered and original images, respectively. In the very right picture I added a LUT used.

![PluginAppliedWithLUT](https://user-images.githubusercontent.com/63607289/152383091-526f7efa-822b-40e4-b6fe-00876216b099.jpg)

The images above were obtained with the plugin dialog setup, please, see below. Each label in the 2nd channel correspond to a single PE spot in the 1st channel. Each PE spot area in the 1st channel has got its intensity mean.

**Parameters:**

*Mean PE Intensity <0, Max>*: Threshold - when a specific mean intensity (MI) is entered, then labels corresponding to PE spots with lower MI, i.e. darker ones, are removed from visualization in the 2nd channel (middle-Filtered image). In other words, for visualization in the filtered image we choose here only labels that correspond to PE spots with MI greater than the threshold. *Max* here is the maximum MI of a PE spot found in the open data. The first message below sliders, in **black**, shows the selected value of MI normalized to *Max* and expressed in percents.

*Grid Density <1-30>*: Defines number and sizes of areas of the heatmap. The size of the heatmap image matrix is the same like the size of original data. If the selected value is 1, the heatmap contains only 1 real value expressing a ratio of labels remaining in the filtered image with respect to all labels in the original image. If the value is 2, the heatmap is split to a 2x2 grid areas, original and filtered images as well, and these ratios are computed for all four areas separately etc. When moving with a cursor in such heatmap area, the corresponding ratio in percents is shown in the status of the Fiji window.

For each combination of both parameters, *Min* and *Max* ratios in the heatmap are visualized in the **red** message in the plugin dialog, just to understand which colors in the heatmap, accorging to LUT applied, correspond to minimum and maximum values, respectively.

The **blue** message diplays plugin status: *Computing...* or *Ready*.

![PE-Plugin-Dialog](https://user-images.githubusercontent.com/63607289/152386388-0b4b7efb-ad14-4372-b217-1b74caec84b1.jpg)

**Remarks**

- The plugin is used for visualization of spatial distribution of "superbright" PE spots and will be used for comparison of these distributions in normal and treated mouse brains.
- It is more efficient, firstly, to apply the threshold for label removing (*Mean PE Intensity*) and, secondly, to vary with *Grid Density*, since computation of multiple heatmap areas is more intensive. From this reason the computation was implemented in parallel threads.
- It is more efficient to enter values of the parameters into the boxes than to move with the sliders, just to avoid computing multiple intermediate results done by the slider movement.
- An example image in ZIP is available for downloading with the plugin file as well.

**Installation**

Download the *Protein_Expression.jar* file and put it into the plugins directory of ImageJ/Fiji installation. After restarting the program the plugin appears in *Plugins->LMCF-IMG->Protein_Expression* menu item.

**Sources**

Rename *Protein_Expression.jar* file to *Protein_Expression.zip* and uncompress to retrieve the source codes.

