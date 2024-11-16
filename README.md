# Cube Vision

## Goal
We all make mistakes. But when it comes to solving a Rubik’s cube very quickly, even the smallest mistakes add up very quickly. The problem is that reconstructing a solution, even with a video, is challenging and time consuming. As a result, common mistakes are identified slowly if at all. The goal of this project is to change that.

By tracking the moves made, it is possible to identify inefficient move algorithms, track how long different stages of the solve take, and reveal common mistakes. Software for such an application already exists, though these apps rely on “Smartcubes” - cubes with inbuilt computers to record moves. These cubes are expensive and heavy, making them impractical to practice with. This project aims to instead track moves using computer vision.

## Object Detection
On the first attempt, object detection served two purposes. First, a single class object detection model is used to locate the cube in the image. The image is then cropped to that box; the resulting image is passed into a second object detection model which locates the pieces and identifies them with their respective colors.

<img src="object-detection-1.png" height="500"> <img src="object-detection-2.png" height="500">

These boxes will then be passed into a simple heuristics algorithm which will calculate which boxes correspond to which pieces. The object detection model used is Retinanet with a mobilenet backbone to achieve real time inference speeds.
