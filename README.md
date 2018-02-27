# Tutorial for AppStudio/QT Creator for Map Customization and Adding Feature Layer
This is a how to guide on the basics of creating an application using QT and AppStudio by ESRI. This guide is focused on map making, customization, and adding features to develop a custom app.  
## Getting Started
## Prerequisites
The following items need to be downloaded and/or are required in order to build a custom application on your computer.
1. ESRI Account
2. ESRI AppStudio
3. QT Creator (comes part of the package when AppStudio is downloaded)
4. (optional, but recommended) mobile device

### 1. ESRI Account
This application will not work without an account with ESRI. A standard license is required with ArcGIS in order to access ESRI's app building services.

### 2. ESRI AppStudio
Navigate to this [website](https://doc.arcgis.com/en/appstudio/download/) to find Appstudio on ESRI's website. Based on your computer, download the accurate version of your computer's platform under the highlighted section in figure 1. There is no need to download AppStudio Player unless you want to visualize your applicaiton on your mobile device in which case you can access the app in iOS or Android. AppStudio software will also allow you to visualize the application on a small screen in its completion form. Note - for this tutorial, Windows x64 is the platform of choice. 

![Download Site for AppStudio](esriapp.PNG)

*Figure 1*

### 3. QT Creator
There is no need to download QT Creator as it comes with AppStudio. After AppStudio has been downloaded, a quick search in all programs for "AppStudio" will display "AppStudio for Desktop Version" as well as "QT Creator" as seen in figure 2. The necessary components of building an app are complete. Now let's begin with AppStudio to develop our application. 

![QT Creator](esriapp2.PNG)

*Figure 2*

## Installation
#### Below are the intial steps in creating the basic elements of the application starting with AppStudio. 
1. Create a new App (see figure 3)

![NewApp](esriapp3.PNG)

*Figure 3*

2. Toggle to Starter and click Hello World (Runtime) (see figure 4)
3. Name your app on the top right corner under title (for this example, the name of the app is MyMap)
4. Click on Create

![Create](esriapp4.PNG)

*Figure 4*

5. Double click the new app in AppStudio and you should have a generic map with basic functions display (see figure 5)
![MyMap](esriapp5.PNG)

*Figure 5*

Now you have a basic app to build upon. Lets move this app to QT creator to do some editing and changing so that we can customize our map to our needs and, later on, add feature layers.
To open the app in QT Creator, right click on the application when in AppStudio and click "Edit in QT Creator" (see figure 6).
![QTCreator](esriapp6.PNG)

*Figure 6*

You are ready to view some coding and work within QT to make changes in the app.

**Remember**: Any changes made in QT Creator can be directly seen in AppStudio by double clicking the app. Remember to "save all" in QT Creator and refresh your app in AppStudio before you open the application so you can view the changes. 

## App Development
First, lets figure out where our area of study is. Given where you pull the feature layer from, the geographic location is important so that the application does not open with a world view, but rather zoom in where your feature layer is located. The map is in world view so it is essential to include a latidude and longitude in your code as well as zoom level in QT Creator so that the focus of the map in these coordinates.  
In order to provide zoom level for your map, change this code to a zoom level that makes sense for your feature layer. The zoom level below for this code is a great distance if you want the United States in view. The lower the number, the closer the zoom level is to the map. 
```
targetScale: 40000000
```
Next, we want to change our location. This is done with using latitude and longitude coordiates which you can search on google for any given location.  
This map will focus on a feature service layer that will be displayed in Idaho. Thus, a good central coordinate of Idaho will work.  
Here is the code that specifies location. Change the x and y coordinate to your location of focus.  
```
        ViewpointCenter {
            id: vc
            center: Point {
                x: -12876752
                y: 5490404
                spatialReference: SpatialReference {wkid: 102100}
                }
                targetScale: 10000000
                }
             }
```

I am also going to change the `targetScale` to 10000000 so the focus will be on the state of Idaho. The `spatialReference` refers to the associated coordinate system. By default, this one is Web Mercator auxillary sphere.  
Finally, lets play with the basemap so you can customize it to your liking. I want a basemap that is satellite imagery to include labels. There are multiple options to choose from. See this [link](https://developers.arcgis.com/qt/latest/qml/api-reference/qml-esri-arcgisruntime-basemap.html) for a list of basemaps with QML.
```   Map {
            BasemapImageryWithLabelsVector {}
            initialViewpoint: vc
```
Now that we have changed the map to our liking, it is time to add a feature layer onto your map. We have a good zoom level on Idaho, the basemap is satellite imagery, and the focus is on the state. Double click the app in AppStudio and it should look something like figure 7.  

![finalmap](esriapp7.PNG)  

```
            FeatureLayer {
                ServiceFeatureTable {
                    url: "https://maps.idwr.idaho.gov/arcgis/rest/services/BP/_Geothermal/MapServer/1"
                }
            }
```
