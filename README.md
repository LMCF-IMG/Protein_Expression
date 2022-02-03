# Protein_Expression
Visualizes a heatmap of quantity ratios of protein expression spots in local areas of mouse brain physical slice images acquired by transmission microscopy.

**Plugin for [ImageJ/Fiji](https://fiji.sc/).**

### Short description

As an input the plugin takes a *2-channel 32-bit image data*.

In the 1st channel, left-in grey, there is a multi-tile picture of a physical slice of a mouse brain captured by Leica DM6000 widefield microscope in the transmission mode (provided by Dr. Helena Janíčková, Laboratory of Neurochemistry, Institute of Physiology of the Czech Academy of Sciences, Prague, Czech Republic). Protein expression, FOS protein, is depicted by bright spots. In the 2nd channel, middle, there is a result of a segmentation procedure with the bright spots labeled by colors. Each spot has been labeled uniquely. On the right there is the input for the plugin - both channels together in one composite image window.

![FOS-EX01-Panel-Input](https://user-images.githubusercontent.com/63607289/152369509-913c61f3-02aa-4e02-be6d-da42d72cf0e8.jpg)

Protein expression spots were segmented with the help of [StarDist](https://github.com/stardist/stardist) project. A new DL model was created and trained with sub-images of spots manually annotated by [Labkit](https://imagej.net/plugins/labkit/). Left-a sub-image, right-an example of manual annotation.

![Labkit](https://user-images.githubusercontent.com/63607289/152375382-8ab50351-d277-458d-b7ab-93c95a31b23f.jpg)

When the plugin is applied then three image windows appear. Left-an original composite image, middle-an image with spots filtered according to their mean intensity, right-the resulting heatmap of the size 20x20 with quantity spot ratios in corresponding local areas. In the very right picture I added a LUT used.

![PluginAppliedWithLUT](https://user-images.githubusercontent.com/63607289/152383091-526f7efa-822b-40e4-b6fe-00876216b099.jpg)

The images above were obtained with the following plugin dialog setup.
