# Object-classification
Object classification in RGB-D images using Ensamble of Shape Functions mehtod


Whole undergraduate thesis is available here: https://zir.nsk.hr/en/islandora/object/etfos%3A1973

ABSTRACT

Object recognition for 2D or 3D images becomes more and more popular and technologies that are being developed are more efficiend and simpler, while quality and precision remain high. The method used in this project is ESF(Ensemble of shape functions). It is one of many methodes included in the PCL library. ESF is shape function that is simple and has various applications. This method is primarily designed for object recognition, but there are other applications like registration, calculating distances or calculating normals in geometric environment. In this project, a program for object classification using ESF method is described and it is tested on the 3DNet data set.


Object recognition is seperated into 2 parts. First part is ESF.cpp in which the program is using ESF function to make point cloud of every view on every object (file) ending with .ply. The second part is done in program called Mathlab in which the comparation between learn objects and new picture is done.
