# Object-classification
Object classification in RGB-D images using Ensamble of Shape Functions mehtod


Whole undergraduate thesis is available here: https://zir.nsk.hr/en/islandora/object/etfos%3A1973

*********************INSTALLATION OF PCL 1.8.0. rc2**************************
1. Copy the folder 'PCL' to your selected location/directory (let us assume that the path to this location/directory is '{PathToSelectedLocation}')

2. Add a new system (environment) variable in Windows with the following parameters:
Variable name: 'PCL180_ROOT'
Variable value: '{PathToSelectedLocation}\PCL'

3. Edit the existing "Path" system (environment) variable. Add the following: '%PCL180_ROOT%\bin'


4. When creating a new C++ project linking this PCL library, the property file 'PCL1.8.0_X64.props' may be imported into the project to simplify the process of defining the properties of the project.
This can be done using the property manager window (View -> Other Windows-> Property Manager). Right click on the project in this window and select 'Add Existing Property Sheet' and then import the file 'PCL1.8.0_X64.props'.

NOTE: The property file 'PCL1.8.0_X64.props' needs to be modified before importing.
Open the file using any text editor and change the string 'D:\Programming\External\PCL' to '{PathToSelectedLocation}\PCL'

