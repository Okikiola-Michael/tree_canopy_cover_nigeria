# Tree Canopy Cover for Nigeria
 <img width="975" height="631" alt="image" src="https://github.com/user-attachments/assets/07793f81-a450-4765-8ac5-8b1d19d647c0" />
 


This repository contains a [Google Earth Engine](https://code.earthengine.google.com/) JavaScript-based script that can be used directly to access and download the tree canopy cover for Nigeria. We developed the first national-level tree canopy cover (TCC) for Nigeria,  using a random forest model on the GEE platform. The TCC was developed by training a regression-based random forest model using 3,047 sample points at the [Landsat](https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LC08_C02_T1_L2) pixel level (30m). Please read our [publication]() for more details:




There is a [GEE-based application](https://ee-alegbeleyeokiki.projects.earthengine.app/view/tree-canopy-cover-in-nigeria) that users can use to visualize, perform simple analyses, and download  tree canopy cover data. However, if you prefer to use GEE directly, the script below provides access to the data.


## Direct Download using GEE platform - JavaScript

                                                                                                            
```javascript
    // Load your boundary
    var boundary = ee.Feature('your boundary asset link') // You can also directly create your boundary on GEE using the drawing tools

    // Tree canopy cover assets
    var tcc_2017 = ee.Image('projects/ee-alegbeleyeokiki/assets/tcc_nigeria/tcc_2017_masked') //2017
    var tcc_2020 = ee.Image('projects/ee-alegbeleyeokiki/assets/tcc_nigeria/tcc_2020_masked') //2020
    var tcc_2024 = ee.Image('projects/ee-alegbeleyeokiki/assets/tcc_nigeria/tcc_2024_masked') //2024

    // Clip to your study area
    
    var clipped_tcc_2024 = tcc_2024.clip(boundary)

    // Visualization palette
    var tcc_vis = {min: 0, max: 100, palette: ['white','lightgreen','green','darkgreen']}

    // Center to a specific location 
    Map.centerObject(boundary, 13);

    
    // View boundary layer
    Map.addLayer(boundary, {color: 'red'}, 'Boundary');
    // View the clipped TCC data
    Map.addLayer(clipped_tcc_2024, tcc_vis, 'Clipped 2024 TCC');

   // Export to Google Drive

  //TCC 2024
    Export.image.toDrive({
      image: clipped_tcc_2024, // The clipped TCC layer
      description: "Your Image Description",
      folder: "GEE_Exports", // your Google Drive folder
      fileNamePrefix: " [Year] Clipped TCC  ",
      scale: 30, 
      region: boundary,
      maxPixels: 1e13  
      });
  

  // Export to Cloud Storage

  // TCC 2024
    Export.image.toCloudStorage({
      image: clipped_tcc_2024, // The clipped TCC layer
      description: "Your Image Description",  
      bucket: "my-cloud-bucket", //your bucket name
      fileNamePrefix: " [Year] Clipped TCC " ,
      scale: 30, 
      region: boundary,
      maxPixels: 1e13 
      });

  
  ```


## Independent validation results after model training and testing.

 | Accuracy Metrics               | 2017   | 2020   |2024    |
 |--------------------------------|--------|--------|--------|
 | 1. R2                          |72      |64      |83      |     
 | 2. R                           |85      |80      |91      | 
 | 3. RMSE                        |16.58   |19.29   |15.05   | 
 | 4. MAE                         |9.59    |11.07   |7.94    | 
 | 5. Number of observation       |188     |219     |264     |  

                                          

  
If you use this app or any of its derived products, do not forget to cite our [publication]().


```javascript

Publication Reference:
Alegbeleye, O.M., Alegbeleye, Y.O., Adeleke, O.S., Shomide, P.O., Ibeh, K.G., Ogundipe, O.C., Oyediran, A., <br>
Aderinola, A.D., Ojeleye, J.O. and Akintunde-Alo, A., 2026. First National-level Tree Canopy Cover: <r>
Integrating AlphaEarth Embeddings with Landsat for Forest Monitoring in a Tropical Region. <br>
Remote Sensing Applications: Society and Environment, p.102213.

```




