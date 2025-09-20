# tree_canopy_cover_nigeria

![](https://github.com/Okikiola-Michael/gee_fire_apps/blob/main/gee_fire_image.jpg) 

This repository contains a [Google Earth Engine](https://code.earthengine.google.com/) JavaScript-based script that can be used directly to access and download the tree canopy cover for Nigeria. We developed the first national-level tree canopy cover (TCC) for Nigeria,  using a random forest model on the GEE platform. The TCC was developed by training a regression-based random forest model using 3,047 sample points at the [Landsat](https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LC08_C02_T1_L2) pixel level (30m). Please read our [publication]() for more details.

There is a [GEE-based application](https://ee-alegbeleyeokiki.projects.earthengine.app/view/tree-canopy-cover-in-nigeria) that users can use to visualize, do simple analysis, and download the tree canopy cover. However, if you prefer to use GEE directly, below is a script to access the data.

## Direct Download using GEE platform - JavaScript


                                                                                                                   


 
Generally, these apps enable users to: 
  1. upload their area of interest (AOI) - Upload your shapefile to your GEE Asset and make it publicly available. 
  2. select desired pre-fire and post-fire dates
  3. select and compare different vegetation indices using maps and charts for the pre-fire and post-fire dates, and 
  4. download the indices geotiff file.

At the backend, this app filters [Sentinel 2](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR_HARMONIZED) or 
[Landsat 8](https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LC08_C02_T1_L2) data (Cloud cover = 10%) based on user's AOI and calculates vegetation indices.


  1. The [`Landsat_GEE_Fire_App`](https://ee-alegbeleyeokiki-fireapp.projects.earthengine.app/view/vegetation-indices-comparison-using-landsat-8-data) currently support 17 vegetation indices using Landsat 8 surface reflectance imageries and the source for the app is [here](https://github.com/Okikiola-Michael/gee_fire_apps/blob/main/Landsat_8_gee_app.md).
  2. The [`Sentinel_GEE_Fire_App`](https://ee-alegbeleyeokiki-fireapp.projects.earthengine.app/view/vegetation-indices-comparison-using-sentinel-2-data) currently support 18 vegetation indices using Landsat 8 surface reflectance imageries and the source for the app is [here](https://github.com/Okikiola-Michael/gee_fire_apps/blob/main/Sentinel_2_gee_app.md).
     

See our publication for details:
```


```

  ## Export to Google Drive
  ```javascript

  //TCC 2024
    Export.image.toDrive({
      image: tcc_2024,
      description: "Your Image Description",
      folder: "GEE_Exports", // your folder
      fileNamePrefix: " TCC " + tcc_2024,
      scale: 30, 
      region: geometry,
      maxPixels: 1e13  
      });
  

  ```

  ## Export to Cloud Storage
  ```javascript
  // TCC 2024
    Export.image.toCloudStorage({
      image: tcc_2024,
      description: "Your Image Description", // edit the 
      bucket: "my-cloud-bucket", //your bucket name
      fileNamePrefix: " TCC " + tcc_2024,
      scale: 30, 
      region: geometry,
      maxPixels: 1e13 
      });

  

  ```

  
If you use this app or any of its derived products, do not forget to cite our [publication]().

