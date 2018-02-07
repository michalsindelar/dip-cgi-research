# ARKit notes

## ARSCNView

*A view for displaying AR experiences that augment the camera view with 3D SceneKit content.*


- The world **coordinate** **system** of the view's SceneKit scene directly **responds** to the **AR world coordinate system** established by the session configuration.
- The view automatically moves its SceneKit camera to match the real-world movement of the device.

=> placing object to real world requires only SceneKit position



## ARWorldTrackingSessionConfiguration
- tells ARSession we want **six degrees of freedom**
![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1509195044570_image.png)











- (ARSessionConfiguration if user still)



- ARKit and SceneKit coordinate system
  - camera faces in the negative Z direction



![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1509195220143_image.png)



## SCNScene

*A scene graph—a hierarchy of nodes with attached geometries, lights, cameras and other attributes that together form a displayable 3D scene.*



**Lights**

`var lightingEnvironment: SCNMaterialProperty`

A **cube map texture** that depicts the environment surrounding the scene’s contents, used for advanced lighting effects.



- official tops
  - For realistic results, reuse the same contents for both the lighting environment and the `[background](https://developer.apple.com/documentation/scenekit/scnscene/1523665-background)` property.


**Fog**

- could be useful for simulating different environment
- all of them are **Animatable**


    var fogStartDistance: CGFloat
    var fogEndDistance: CGFloat
    var fogDensityExponent: CGFloat
    var fogColor: Any


**Particle Systems**
A **particle system** is a technique in [game physics](https://en.wikipedia.org/wiki/Game_physics), [motion graphics](https://en.wikipedia.org/wiki/Motion_graphics), and [computer graphics](https://en.wikipedia.org/wiki/3D_computer_graphics) that uses a large number of very small [sprites](https://en.wikipedia.org/wiki/Sprite_(computer_graphics)), [3D models](https://en.wikipedia.org/wiki/3D_model), or other graphic objects to simulate certain kinds of "fuzzy" phenomena


- **Physics** 
- **Casts Shadow**
## SCNNode
- important class for interposing objects into the scene

**CI Filters**

- tons of difital image processing tools

https://developer.apple.com/library/content/documentation/GraphicsImaging/Reference/CoreImageFilterReference/index.html


    CIBoxBlur
    CIDiscBlur
    CIGaussianBlur
    CIMaskedVariableBlur
    CIMedianFilter
    CIMotionBlur
    CINoiseReduction
    CIZoomBlur





# Plane Detection

:tldr: SIFT (Scale Invariant Feature transform)


## Problems
1. Poor lightning
2. Lack of texture
3. Fast movement 
  - in terms of blurred images



- is neabled with `ARWorldTrackingConfiguration()` `planeDetection` flag
  - after we start getting callbacks to delegate methods for the [ARSCNViewDelegate](https://developer.apple.com/documentation/arkit/arscnviewdelegate) protocol
  - `**func**` `renderer(_` `*renderer*``: SCNSceneRenderer,` `**didAdd | didUpdate**` ```*node*``: SCNNode, for` `*anchor*``: ARAnchor) {`
  - in these functions we handle planes




----------
# Development notes


- Storyboards have Dynamic cells by default therefor not visible anything after build
  - Set to Static
![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1509230282642_image.png)

## Data Management
1. Each scene should have own Controller
- keep in mind that `CustomClass` could be  set only for “compatible” superclasses


- e.g. `UITabController` could these Custom Class which extends `UITableViewController` 
- ❗ Only `ViewController` is not enough


![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1509292625228_image.png)



2. How to handle global state
- **global** struct is not such a bad idea
- in controllers other controllers could be references


# Machine Learning & Vision

https://developer.apple.com/documentation/vision



## Vision framework

*Apply high-performance image analysis and computer vision techniques to identify faces, detect features, and classify scenes in images and video.*

**

- provides Models of pretrained sets
  - dominant objects recognition
    - Inception v3
    - ResNet
    - VGG16
  - places
    - places205-GoogLeNet
![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1509297173443_image.png)


 **Labeling objects in scene**


https://www.youtube.com/watch?v=Sno-r2xQeRQ&


[https://youtu.be/Sno-r2xQeRQ](https://youtu.be/Sno-r2xQeRQ)


# Libraries coopeartion
## Vuforia
- not supported yet
- according to official Vuforia docs in version 7 will come integration to ARKit 
  - framework **Vuforia Fusion** *(a new capability designed to provide the best possible AR experience on a wide range of devices)*
  - source: https://www.vuforia.com/press-releases/ptc-announces-major-new-release-to-vuforia-augmented-reality-platform.html
- **developer licence?**


## Kudan
- not so perspective future with ARKit


2017-10-30 

## Future Notes
- orientation of planes investigate
- other libraries **(?)**
  - …
- in case libraries not possible to use
  - detection of **markers**
    - https://github.com/likedan/Awesome-CoreML-Models
  - based on 4 corners based on perspective -> estimate position in scene
  - try opencv methods for position
    - compare with apple inside — calibration inside ARKit
- **aruco**
- light map
  - how to create?



----------




# Running extings Unity on iOS


## Compilation problems 😡 -> Scene Ammends

**Linear vs Gamma Color space**

![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1510506405496_image.png)



**Memory Issues**

![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1510508486498_image.png)



**BuildPlayerWindowBuildMethods Exceptions in Unity**

- try to reimport all Assets takes about an hour
- restart unity
- restart mac



**IOExceptions**

- flush all built files and create new folder 🤦‍♂️ 
- Player 2 Error without explanation
![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1510508698998_image.png)



**Could not write to device**

- restart XCode & Unity


**Memory Issues**

> Message from debugger: Terminated due to memory issue


- this is critical — terminates app
- possible causes
  - infinite loop internal while recompiling from Unity to C++
  - used too much memory which iOS cannot handle



**Limit only to GameScene**

![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1510510444506_image.png)



## Scene related
![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1510511388358_image.png)





## ARKit plugin settings
## Camera

**Main Camera**

- main camera should load camera stream from the device and interpose scene after
  - sphere collider
  - rigid body
  - connect with `UnityARVideo` script


![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1510520865046_image.png)




# Advanced Unity  & ARKit Cooperation


## imareculture-excavation
- placing the scene even with the rendering scripts into the real world


https://www.dropbox.com/s/pg01vjo78k4megz/imare_ios.m4v?dl=0

- simple support for cardboard virtual reality 
https://www.dropbox.com/s/x0265tejg44dlly/virtual_cardboard.mov?dl=0



# Gesture recognition
- simple example based on Core ML https://github.com/hanleyweng/Gesture-Recognition-101-CoreML-ARKit
  - powered by super simple model with only few test images (< 100) — intended to work only as an example
  - could be easily extended to work much more robust
https://www.dropbox.com/s/1vnh664on6sepqi/gesture_recognition.m4v?dl=0

- gesture recognition directly in unity
  - commercial https://www.assetstore.unity3d.com/en/#!/content/14458


- touch gesture recognizer
  - https://developer.apple.com/documentation/uikit/uigesturerecognizer
    


# Measurement
- https://github.com/DroidsOnRoids/MeasureARKit
- simple app - choosing closest feature point to the center 


![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1511117947904_image.png)
https://www.youtube.com/watch?v=KcWByTLTqlo&&feature=youtu.be


[https://youtu.be/KcWByTLTqlo](https://youtu.be/KcWByTLTqlo)




## Measurement
- seems as a combination of computer vision + accelerometer  sensors


- steps
  - image 1
    - detection of feature points
  - image 2
    - detection of feature points
  - image 1 and image 2
    - **compared** distance between the **position** of the camera where image 1 and image 2 are acquired using **accelerometer sensors**
    - compares **all** shared **feature points**
    - *(like eyes distance)*

Error

https://www.dropbox.com/s/vet0y1kzhbegzpr/ScreenRecording_12-03-2017%2020-21-28.m4v?dl=0


[https://www.dropbox.com/s/vet0y1kzhbegzpr/ScreenRecording_12-03-2017%2020-21-28.m4v?dl=0](https://www.dropbox.com/s/vet0y1kzhbegzpr/ScreenRecording_12-03-2017%2020-21-28.m4v?dl=0)



- hypothesis - storing the initial anchor
  - try


# “Marker” detection
- possible using the Vision Framework — powered by Core ML training set
- tracking is done in 2D and then transformed to 3D position
- done by postprocessing of image
  - delay could be visible

=> marker like detection is possible via **postprocessing of images**

- ML data models
  - depends on model quality & robustness
- 3rd party libraries - not many 


## Applications

**⬆️ Labeling objects in scene** 

- video from Core ML block


**Face Detection**


![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1512324962718_image.png)


[https://youtu.be/RdAqD4uIbX0](https://youtu.be/RdAqD4uIbX0)

- jak vypocita hloubku pozici ve 3D
  - seems as a fake 
    - 2 possible solution
      - working with true depth front iPhone X camera
      - same distances from people


🔲 **Simple QR codes detection**

- placing 3D objects to the scene
- demo app live


- sample video
https://www.dropbox.com/s/z3dlrxt81rur7cj/ScreenRecording_12-03-2017%2019-22-17.m4v?dl=0


[https://www.dropbox.com/s/z3dlrxt81rur7cj/ScreenRecording_12-03-2017%2019-22-17.m4v?dl=0](https://www.dropbox.com/s/z3dlrxt81rur7cj/ScreenRecording_12-03-2017%2019-22-17.m4v?dl=0)
[https://github.com/CocoaHeadsDetroit/CocoaHeadsDetroit.github.io/raw/master/arkit%2B2dtrack-1.gif](https://github.com/CocoaHeadsDetroit/CocoaHeadsDetroit.github.io/raw/master/arkit%2B2dtrack-1.gif)



📰 Based on Text detection

https://www.dropbox.com/s/lhlkuw3h1on1zdr/ScreenRecording_12-04-2017%2015-58-54.m4v?dl=0


[https://www.dropbox.com/s/lhlkuw3h1on1zdr/ScreenRecording_12-04-2017%2015-58-54.m4v?dl=0](https://www.dropbox.com/s/lhlkuw3h1on1zdr/ScreenRecording_12-04-2017%2015-58-54.m4v?dl=0)



# Last Week


- try to reveal how the 3D position is obtained — especially with face detection / text
- examples with **OpenCV** app
  - calibration - squares
  - cooperation Arkit & OpenCV
- uncompressed video app
- DIP notes links


----------
## DIP powered by Apple
- docs
  - https://developer.apple.com/library/content/documentation/GraphicsImaging/Reference/CoreImageFilterReference/index.html#//apple_ref/doc/uid/TP30000136-SW29
![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1512941732487_image.png)
![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1512941774962_image.png)



    CICategoryBlur
    - blur filters
    
    CICategoryColorAdjustment
    
    - CIColorClamp, CIColorControls, CIColorMatrix, CIColorPolynomial, CIExposureAdjust, CIGammaAdjust
    
    CICategoryColorEffect
    - CIColorPosterize, CIFalseColor, CIMaskToAlpha, CIMaximumComponent, CIMinimumComponent
    
    CICategoryCompositeOperation
    - blend modes,  darken, difference, max / min composition, blend
    
    CICategoryDistortionEffect
    - distortion, wrapping, stretching
    
    CICategoryGenerator
    - Aztec generator, QR generator
    
    
    CICategoryGeometryAdjustment
    - affine transform, crop, straighten
    
    
    CICategoryGradient
    - gaussian gradient, linear, radial
    
    CICategoryHalftoneEffect
    
    CICategoryReduction
    - CIAreaAverage, CIAreaHistogram
    
    
    CICategorySharpen
    - sharpenning
    
    
    CICategoryStylize
    - CIBlendWithAlphaMask, CIBlendWithMask, CIBloom, CIComicEffect, CIConvolution
    
    CICategoryTileEffect
    
    CICategoryTransition
    


- tons of features — sufficient to omit other libraries


## Revealing 3D anchor from 2D position

**ARHitTestResult**

- all of the demonstrated apps uses this class
- doc
  - https://developer.apple.com/documentation/arkit/arhittestresult
- raycasting and checking intersection with detected planes 
  - method returns an array of sorted intersection by distance (the floor is the last == farthest one)
  - => the video with the emojis above the faces was took by the true-depth iPhone X camera whic creates accurate depth map


https://www.youtube.com/watch?v=YhnwBx3Tr3w&


[https://youtu.be/YhnwBx3Tr3w](https://youtu.be/YhnwBx3Tr3w)



- another example detecting objects in scen 2D -> 3D raycast to planes
  - https://github.com/hanleyweng/CoreML-in-ARKit


- some applications uses only fake transformation to 3D -> place the anchor `x metres` in fron of the camera


## Face
- great features with the fron true-depth camera
- doc
  - https://developer.apple.com/documentation/arkit/creating_face_based_ar_experiences
  - https://developer.apple.com/documentation/arkit/arfacetrackingconfiguration
  - https://developer.apple.com/documentation/arkit/arfaceanchor



## Video without Compression
## **Go Game Custom Video Module**


- github: https://github.com/thegogame/native_video_module


![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1512943906215_image.png)

## OpenCv & ARkit


- more combinations - **Unity & OpenCV & ARKit**
https://www.youtube.com/watch?v=v6x6Aa9qLXE&


[https://youtu.be/v6x6Aa9qLXE](https://youtu.be/v6x6Aa9qLXE)



- for native cooperation iOS & OpenCV
  - tutorials for creating OpenCVWrapper
  - https://docs.opencv.org/2.4/doc/tutorials/ios/video_processing/video_processing.html#including-opencv-library-in-your-ios-project



- I tried several applications, all of them outdated / impossible to compile
  - only one implementation working


![](https://d2mxuefqeaa7sj.cloudfront.net/s_A6B884960D7D4FC1923B55431122D92E5574BE8F7FF9CB86DB894CE88DC1985E_1512949590341_image.png)




- resumé
  - support of OpenCV for iOS + ARKit exists but a way more common way how to use OpenCV in cooperation with iOS seems to be connected with Unity



----------

Resources
https://developer.apple.com/arkit/
https://blog.markdaws.net/arkit-by-example-part1-7830677ef84d

