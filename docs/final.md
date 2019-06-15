---
layout:	default
title:	Final Report
---

## Video
<iframe width="560" height="315" src="https://www.youtube.com/embed/Dd0KOZKiN7k" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Project Summary
ArchitectSteve is a tool that takes a 2D image provided by the user and constructs a replica of the building in Minecraft but in 3D form. Steve, our intelligent “agent” as we call our tool takes the image and processes that image into a series of what we loosely will call coordinates, making it easier to work in Malmo Minecraft, but can be seen as the list of vertices that determine the shape of the object. This subroutine is made possible using the external OpenCV shape detection resource from the pyimagesearch website. The result is a 3D diamond block replica, in the Minecraft world environment, of the 2D building image that was “uploaded” to ArchitectSteve. Of course, due to the height restriction of 256 blocks that exists in Minecraft due to the fact that the Minecraft world is made of 16x16x256 'chunks’, we would resize the image so that the replicated structure would not be cutoff. The 2D building-view image also gets translated in order for the resulting replica to be perceived as having depth in Minecraft, thus having a 3D pop-up structure.

## Approaches
We started off by using OpenCV’s shape contouring and detection functions. OpenCV recognizes shapes due to the difference in contrast, which is why we decided to pass in completely black and white photos. We initially thought of breaking down the buildings into shapes and using OpenCV’s shape recognition, but we later realized that OpenCV can return the pixel coordinates for the perimeter of any polygon using the findContours function. We also. We created a getArea() function using OpenCV’s pointPolygonTest() To test each pixel in the image and determine if those points are or are not within the shape. getArea() thus returns every coordinate where a block should be placed in the Minecraft world as a 2D object.

Once we finally got a 2D object into Minecraft, we realized that the objects were being made upside down, we figured that an easy solution to this issue was to simply pass in upside down images into OpenCV.

![BW](https://i.imgur.com/Plzw845.png)
![2dPic](https://i.imgur.com/eJpJmCv.png)

Next, we thought about how we could turn our 2D object into 3D object in Minecraft.
We realized that if a building was symmetrical all around then by expanding the corners of the 2D object, the result would be a 3D building.  We made this possible by finding the corner Y coordinates into an array. We would then build for z in range length of Y corner arrays. For each z, the section of the 2D array that was less than the current Y from the Y corners array would get built, which leads the 3D construction of 2D models. 

![sideOne](https://i.imgur.com/nYl1KPN.png)
![sideTwo](https://i.imgur.com/kqPHHhJ.png)

## Evaluation
Our evaluation criteria is primarily focused on the qualitative, measured by the quality, size and appearance  of the building our algorithm created. At its essence we are trying to answer the following evaluation question: does the 3D Minecraft representation of the building look like the original 2D image of the building. To assess this part of the evaluation we perform a simple visual comparison between the 3D Minecraft diamond block replica and the original 2D image. The dimension and depth are two of the criteria we focused on, in order to create a much more realistic structure. Through the peer grading, we will hopefully gather feedback from four other students on our accuracy of the building replication.

The evaluation criteria also includes a quantitative assessment that is the focused on the extent of building images that it can successfully build replicas of. With the algorithm we have in place we are able to work with geometric structures that often resemble some kind of symmetry. We compare the results of asymmetrical building images and their replicas to symmetrical building images and the number of successful replicas is a lot higher for symmetrical structures.

## Refrences
Imutils: image processing functions such as translation, rotation, resizing, skeletonization, sorting contours and detecting edges with OpenCV and Python 3.
https://pypi.org/project/imutils/

OpenCV Shape Detection: identify the contour or the outline of the shape using contour approximation in order to carry out shape detection. This approximation algorithm is commonly known as the Ramer-Douglas-Peucker algorithm. This essentially reduces the number of points on a curve or line to a simplified approximated version.
https://pypi.org/project/opencv-python/
https://www.pyimagesearch.com/2016/02/08/opencv-shape-detection/

Minecraft Selfies: This resource is simlar to the Sketchy AI project that was created during the Spring of 2017 by Alex Chapp, Katherine Fitzpatrick, and Edwin Ho. The inspiration we drew from it, similar to the Sketchy AI, is the idea of rendering an image's colors in the form of pixels into Minecraft 3D structures. Reading through this resource we learned how to convert images into RGB values.
https://projects.raspberrypi.org/en/projects/minecraft-selfies/