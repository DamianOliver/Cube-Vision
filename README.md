# Cube Vision

## Goal
We all make mistakes. But when it comes to solving a Rubik’s cube very quickly, even the smallest mistakes add up very quickly. The problem is that reconstructing a solution, even with a video, is challenging and time consuming. As a result, common mistakes are identified slowly if at all. The goal of this project is to change that.

By tracking the moves made, it is possible to identify inefficient move algorithms, track how long different stages of the solve take, and reveal common mistakes. Software for such an application already exists, though these apps rely on “Smartcubes” - cubes with inbuilt computers to record moves. These cubes are expensive and heavy, making them impractical to practice with. This project aims to instead track moves using computer vision.

## Object Detection
On the first attempt, object detection served two purposes. First, a single class object detection model is used to locate the cube in the image. The image is then cropped to that box; the resulting image is passed into a second object detection model which locates the pieces and identifies them with their respective colors.

<img src="object-detection-1.png" height="500"> <img src="object-detection-2.png" height="500">

These boxes will then be passed into a simple heuristics algorithm which will calculate which boxes correspond to which pieces. The object detection model used is Retinanet with a mobilenet backbone to achieve real time inference speeds.

## Data
Object detection models require vast quantities of data to train, ideally in the tens if not hundreds of thousands of annotated images. Sadly no university or tech giant has gotten around to making a large annotated database of Rubik’s cube images, and so I’m on my own. Rather than spending the next two years dragging boxes onto images of cubes, I decided to create simulated data using Unity.

<img src="data-1.png" height="330" width="330"> <img src="data-2.png" height="330" width="330"><img src="data-3.png" height="330" width="330">
<img src="data-4.png" height="330" width="330"> <img src="data-5.png" height="330" width="330"><img src="data-6.png" height="330" width="330">

1. Instantiate scene and cube object
1. Randomize colors of pieces of cube
1. Rotate one side of the cube, move the entire cube, rotate the entire cube
1. Apply a random background image from the coco dataset
1. Match hands to position of cube, randomize angles of joints in hand
1. Randomize lighting location and color, shift RGB colors of pieces
