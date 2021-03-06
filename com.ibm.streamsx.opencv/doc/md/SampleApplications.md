Sample Applications
===================

The sample applications illustrate how to [use the toolkit](UsingToolkit.html) in Streams applications. They are defined in the Streams namespace ’samples’, and use the [operators and types](OperatorsAndTypes.html) in the namespace ’com.ibm.streamsx.opencv’.

All of the sample applications are compiled when the toolkit is [installed](InstallingToolkit.html). The sample applications can also be built individually within Streams Studio, or with the ’sc’ command, like this:

        cd .../streams.opencv/com.ibm.streamsx.opencv
        make sample-application-name
        ./output/sample-application-name/bin/standalone -t 3

Below are descriptions of each sample application, including which operators it uses.

addtext.spl
-----------

Reads a stream of images from a video file. Prints width, height, and frame count on the image. The resulting video is displayed in a X11 window.

toolkit operators used:

- `AddText`
- `CaptureFromFile`
- `X11Viewer`

blank2.spl
----------

Creates a stream of blank images with a specific height, width, fps, and color. The stream stats are printed on the image. The resulting video is output to a HTTPViewer on a specific port.

toolkit operators used:

- `Blank`
- `HTTPViewer`
- `Stats`

blank.spl
---------

Creates a stream of blank images with a specific height, width, fps, and color. The stream stats are printed on the image. The resulting video is output to a MJPEGStreamer on a specific port.

toolkit operators used:

- `Blank`
- `MJPEGStreamer`
- `Stats`

box.spl
-------

Periodically polls for an image from a url. A box is added to the retrieved images. The resulting video is displayed in a X11 window.

toolkit operators used:

- `CaptureFromURL`
- `MakeBox`
- `X11Viewer`

cam\_proxy.spl
--------------

Captures video from a local webcam. The resulting video is output through a proxy connection.

(See src\_proxy demo for the receiving proxy demo)

toolkit operators used:

- `CaptureFromCAM`
- `DisplayProxy`

cam.spl
-------

Captures video from a local webcam. The resulting video is displayed in a X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `X11Viewer`

codebook.spl
------------

Reads a stream of images from a video file. The images are smoothed before background/foreground detection is done. For the first 1s, the background is “learned”, then only the foreground connected objects will be displayed in a X11 window.

The image from the CodeBook operator is a binary matrix of pixels of whether a foreground object is present(255) or not(0). This needed to be converted to a color image before the binary image was “ANDed” with the original image. This results in the foreground color image showing through and the background remaining black(0).

toolkit operators used:

- `Apply2`
- `CaptureFromFile`
- `CodeBook`
- `ConnectedComponents`
- `CvtColor`
- `Smooth`
- `X11Viewer`

common.spl
----------

This is not a sample application, although it does have the .spl file extension.

This file is used to define all of the common tuple types, so the tuple definitions did not have to be included at the top of each sample application.

toolkit operators used: none

contours\_on\_file.spl
----------------------

Reads a stream of images from a video file. The images are converted to grey and smoothed before thresholding is done. All pixels with value 75 or less are changed to zero(black). Then white contours are drawn on the image.

In order to display the new image next to the original, they first have to have the same number of color channels. So the new image is converted to color first. The result is displayed in a X11 window and saved to an output file at the same frame rate as the input file.

toolkit operators used:

- `CaptureFromFile`
- `Collage`
- `CvtColor`
- `DrawContours`
- `SaveToFile`
- `Smooth`
- `Threshold`
- `X11Viewer`

contours\_on\_jpg.spl
---------------------

Creates a stream of images from a single jpg file. The images are converted to grey and smoothed before thresholding is done. All pixels with value 150 or less are changed to zero(black). Then white contours are drawn on the image. The result is displayed in a X11 window. Then the stats <span>tuples/s, bytes/s, and number of seconds</span> are written to a log.

toolkit operators used:

- `BitBucket`
- `Blank`
- `CvtColor`
- `DrawContours`
- `Smooth`
- `Threshold`
- `X11Viewer`

copy.spl
--------

Reads a stream of images from a video file. The images are then saved to an output video file with same rate as the input file. The video is also displayed in a X11 window.

toolkit operators used:

- `CaptureFromFile`
- `SaveToFile`
- `X11Viewer`

crawler.spl
-----------

Scans two directories, one for all files and another only for files matching a specific REGEX pattern. The file names are output to files.

For some operators (i.e. ReadImage), this could be used as an input specification mechanism (see imgcrawler demo.)

toolkit operators used: none

demo1b.spl
----------

Reads a stream of images from a video file. The resulting video is output to a MJPEGStreamer on a specific port.

toolkit operators used:

- `CaptureFromFile`
- `MJPEGStreamer`

demo1.spl
---------

Captures video from a local webcam. The resulting video is displayed in a X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `X11Viewer`

demo2b.spl
----------

Reads a stream of images from a video file. Images are converted to grey scale and output to a MJPEGStreamer on a specific port.

Grey scale images are then passed through erode and dilate functions before outputing to a second MJPEGStreamer on a different port.

The original video is smoothed and outputted to a third MJPEGStreamer on a different port.

Using the original grey scale images, high and low thresholds are applied. The low value indicates pixels with a value less than are converted to black(0). The high value indicates pixels with larger values are converted to max(255) and less/equal are converted to black (0). Trackbars are used to allow the user to adjust the threshold values for the high and low thresholds. The two thresholded images are “ORed” together resulting in all “max” pixels being kept from the high threshold image and then all remaining pixels being kept from the low threshold image. The resulting video is output to a fourth MJPEGStreamer on a different port.

Using the eroded/dilated grey scale images, the same high and low thresholds as above are applied. The resulting video is output to a fifth MJPEGStreamer on a different port.

toolkit operators used:

- `Apply2`
- `CaptureFromFile`
- `CvtColor`
- `Dilate`
- `Erode`
- `MJPEGStreamer`
- `Smooth`
- `Threshold`
- `TrackBar`

demo2.spl
---------

Captures video from a local webcam. Images are converted to grey scale and displayed in a X11 window.

Grey scale images are then passed through erode and dilate functions before displaying in a second X11 window.

The original video is smoothed and displayed in a third X11 window.

Using the original grey scale images, high and low thresholds are applied. The low value indicates pixels with a value less than are converted to black(0). The high value indicates pixels with larger values are converted to max(255) and less/equal are converted to black (0). Trackbars are used to allow the user to adjust the threshold values for the high and low thresholds. The two thresholded images are “ORed” together resulting in all “max” pixels being kept from the high threshold image and then all remaining pixels being kept from the low threshold image. The resulting video is displayed in a fourth X11 window.

Using the eroded/dilated grey scale images, the same high and low thresholds as above are applied. The resulting video is displayed in a fifth X11 window.

toolkit operators used:

- `Apply2`
- `CaptureFromCAM`
- `CvtColor`
- `Dilate`
- `Erode`
- `Smooth`
- `Threshold`
- `TrackBar`
- `X11Viewer`

demo3b2.spl
-----------

Captures video from a input file. Images are converted to grey scale. High and low thresholds are applied. The low value indicates pixels with a value less than are converted to black(0). The high value indicates pixels with larger values are converted to max(255) and less/equal are converted to black(0). Trackbars are used to allow the user to adjust the threshold values for the high and low thresholds. The two thresholded images are “ORed” together resulting in all “max” pixels being kept from the high threshold image and then all remaining pixels being kept from the low threshold image. The resulting video is output to a MJPEGStreamer on a specific port. Then contours are drawn in white on a black image and output to a second MJPEGStreamer on a different port.

For comparison the original grey images are smoothed first prior to thresholding and drawing contours. The resulting contour images are output to a third MJPEGStreamer on a different port.

toolkit operators used:

- `Apply2`
- `CaptureFromFile`
- `CvtColor`
- `DrawContours`
- `MJPEGStreamer`
- `Smooth`
- `Threshold`
- `TrackBar`

demo3b.spl
----------

Captures video from a input file. Images are converted to grey scale. High and low thresholds are applied. The low value indicates pixels with a value less than are converted to black(0). The high value indicates pixels with larger values are converted to max(255) and less/equal are converted to black(0). Trackbars are used to allow the user to adjust the threshold values for the high and low thresholds. The two thresholded images are “ORed” together resulting in all “max” pixels being kept from the high threshold image and then all remaining pixels being kept from the low threshold image. The resulting video is output to a MJPEGStreamer on a specific port. Then contours are drawn in white on a black image and output to a second MJPEGStreamer on a different port.

For comparison the original grey images are smoothed first prior to thresholding and drawing contours. The resulting contour images are output to a third MJPEGStreamer on a different port.

In order to display the new contour image next to the original, the two must have the same number of color channels. So the new image is converted to color first. The result is output to a forth MJPEGStreamer on a different port and saved to an output file at 15 frames/s.

toolkit operators used:

- `Apply2`
- `CaptureFromFile`
- `Collage`
- `CvtColor`
- `DrawContours`
- `MJPEGStreamer`
- `SaveToFile`
- `Smooth`
- `Threshold`
- `TrackBar`

demo3.spl
---------

Captures video from a local web cam. Images are converted to grey scale. High and low thresholds are applied. The low value indicates pixels with a value less than are converted to black(0). The high value indicates pixels with larger values are converted to max(255) and less/equal are converted to black(0). Trackbars are used to allow the user to adjust the threshold values for the high and low thresholds. The two thresholded images are “ORed” together resulting in all “max” pixels being kept from the high threshold image and then all remaining pixels being kept from the low threshold image. The resulting video is displayed in a X11 window. Then contours are drawn in white on a black image and displayed in a second X11 window.

For comparison the original grey images are smoothed first prior to thresholding and drawing contours. The resulting contour images are displayed in a third X11 window.

toolkit operators used:

- `Apply2`
- `CaptureFromCAM`
- `CvtColor`
- `DrawContours`
- `Smooth`
- `Threshold`
- `TrackBar`
- `X11Viewer`

demo4b.spl
----------

Reads a stream of images from a video file. The images are smoothed before background/foreground detection is done. For the first 1s, the background is “learned”, then only the foreground connected objects will be output to a MJPEGStreamer on a specific port.

The image from the CodeBook operator is a binary matrix of pixels of whether a foreground object is present(255) or not(0). This needed to be converted to a color image before the binary image was “ANDed” with the original image. This results in the foreground color image showing through and the background remaining black(0).

toolkit operators used:

- `Apply2`
- `CaptureFromFile`
- `CodeBook`
- `ConnectedComponents`
- `CvtColor`
- `MJPEGStreamer`
- `Smooth`

demo4.spl
---------

Captures video through a proxy connection. The images are smoothed before background/foreground detection is done. For the first 1s, the background is “learned”, then only the foreground connected objects will be displayed in a X11 window.

The image from the CodeBook operator is a binary matrix of pixels of whether a foreground object is present(255) or not(0). This needed to be converted to a color image before the binary image was “ANDed” with the original image. This results in the foreground color image showing through and the background remaining black(0).

toolkit operators used:

- `Apply2`
- `CodeBook`
- `ConnectedComponents`
- `CvtColor`
- `Smooth`
- `SourceProxy`
- `X11Viewer`

demo5b.spl
----------

Reads a stream of images from a video file. The images are passed through face detection model. Then circles are drawn around the detected faces. The result is outputted to a MJPEGStreamer on a specific port.

toolkit operators used:

- `CaptureFromFile`
- `DrawCircles`
- `FaceDetection`
- `MJPEGStreamer`

demo5.spl
---------

Captures video through a proxy connection. The images are passed through face detection model. Then circles are drawn around the detected faces. The result is displayed in a X11 window.

toolkit operators used:

- `DrawCircles`
- `FaceDetection`
- `SourceProxy`
- `X11Viewer`

demo6b.spl
----------

Reads a stream of images from a video file. The motion between consecutive images is detected and motion vectors are drawn on the image. The stream stats are printed on the image before outputing to a MJPEGStreamer on a specific port.

toolkit operators used:

- `CaptureFromFile`
- `MJPEGStreamer`
- `MotionDetection`
- `Stats`

demo6.spl
---------

Captures video from a local webcam. The motion between consecutive images is detected and motion vectors are drawn on the image. The stream stats are printed on the image before displaying in a X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `MotionDetection`
- `Stats`
- `X11Viewer`

demo7b.spl
----------

Reads a stream of images from a video file. The motion between consecutive images is detected and motion vectors are drawn on the image. The stream stats are printed on the image before outputing to a MJPEGStreamer on a specific port.

The parameters for the motion detection algorithm are input by the user via trackbars.

toolkit operators used:

- `CaptureFromFile`
- `MJPEGStreamer`
- `MotionDetection`
- `Stats`
- `TrackBar`

demo7.spl
---------

Captures video from a local webcam. The motion between consecutive images is detected and motion vectors are drawn on the image. The stream stats are printed on the image before displaying in a X11 window.

The parameters for the motion detection algorithm are input by the user via trackbars.

toolkit operators used:

- `CaptureFromCAM`
- `MotionDetection`
- `Stats`
- `TrackBar`
- `X11Viewer`

draw\_contours\_on\_cam.spl
---------------------------

Captures video from a local webcam. The images are converted to grey and smoothed before thresholding is done. All pixels with value greater than 128 are changed to zero(black). Contours are detected and drawn in white on a black image. When this contour image is “ORed” with the black/white webcam image the result is white contour lines on top of the black/white webcam image. Images are displayed in a X11 window.

toolkit operators used:

- `Apply2`
- `CaptureFromCAM`
- `CvtColor`
- `DrawContours`
- `Smooth`
- `Threshold`
- `X11Viewer`

draw\_contours\_on\_url.spl
---------------------------

Periodically polls for an image from a url. The images are converted to grey and smoothed before thresholding is done. All pixels with value greater than 128 are changed to zero(black). Contours are detected and drawn in white on a black image. When this contour image is “ORed” with the black/white webcam image the result is white contour lines on top of the black/white webcam image. Images are displayed in a X11 window.

toolkit operators used:

- `Apply2`
- `CaptureFromURL`
- `CvtColor`
- `DrawContours`
- `Smooth`
- `Threshold`
- `X11Viewer`

equalizehist.spl
----------------

Captures video from a local webcam. The average luminosity of all the pixels in the image is computed and printed on the image. Then image frames are tagged with a unique ascending id value.

For (potential) parallel processing the input image stream is passed through a ThreadedSplit operator. Images will be sent to one of three operators (two equalize the image histograms and the third performs no operation). The three streams are then merged using a Custom operator.

At this point the images are not necessarily in order, so the image stream is passed through a Sequencer to guarantee image order. The average luminosity of the new images is computed again.

The original image stream is displayed next to the new images in a X11 window.

toolkit operators used:

- `Average`
- `CaptureFromCAM`
- `Collage`
- `EqualizeHist`
- `Nop`
- `Sequencer`
- `Tagger`
- `X11Viewer`

facedetect.spl
--------------

Captures video from a local webcam. The images are passed through face detection model, and rectangles are drawn around the detected faces. The result is displayed in a X11 window, and a sampling of the faces detected are written to files in JPEG format.

toolkit operators used:

- `CaptureFromCAM`
- `CropBoxes`
- `DrawRectangles`
- `FaceDetection`
- `SaveImage`
- `X11Viewer`

faces\_edges\_cam.spl
---------------------

Captures video from a camera attached to the machine, passes the images through a face detection model and an edge detector on separate threads, and displays the results side-by-side in an X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `Collage`
- `CvtColor`
- `DrawRectangles`
- `FaceDetection`
- `Resize`
- `Sobel`
- `Threshold`
- `TrackBar`
- `X11Viewer`

faces\_edges\_file.spl
----------------------

Reads a stream of images from a video file, passes the images through a face detection model and an edge detector on separate threads, and streams a side-by-side video to an external viewer on TCP port 9001.

toolkit operators used:

- `CaptureFromFile`
- `Collage`
- `CvtColor`
- `DrawRectangles`
- `FaceDetection`
- `MJPEGStreamer`
- `Resize`
- `Sobel`
- `Threshold`

file\_proxy.spl
---------------

Reads a stream of images from a video file. The resulting video is output through a proxy connection. Then video is captured through a proxy connection. The resulting video is displayed in a X11 window.

(See cam\_proxy and src\_proxy demos for a similar split version of this proxy demo)

toolkit operators used:

- `CaptureFromFile`
- `DisplayProxy`
- `SourceProxy`
- `X11Viewer`

file.spl
--------

Reads a stream of images from a video file. Images are timestamped with a time relative to the start of the stream. The resulting video is displayed in a X11 window.

toolkit operators used:

- `CaptureFromFile`
- `TimeStamp`
- `X11Viewer`

fun.spl
-------

Captures video from a local web cam. Images are converted to grey scale and smoothed. A low threshold is applied. The low value indicates pixels with a value less than are converted to black(0). A Trackbar is used to allow the user to adjust the threshold value. Then contours are drawn in white on a black image followed by dilating the contours to make the lines thicker.

The dilated contour image is converted to a 3 channel image and then “ORed” with a smoothed version of the original web cam image. This keeps all of the color from the original image while outlining the contours in thick white lines. The stream stats are printed on the image before displaying in a X11 window.

toolkit operators used:

- `Apply2`
- `CaptureFromCAM`
- `CvtColor`
- `Dilate`
- `DrawContours`
- `Smooth`
- `Stats`
- `Threshold`
- `TrackBar`
- `X11Viewer`

imgcrawler.spl
--------------

Creates a stream of blank images with a specific height, width, and color at 1 frame/s. Scans a directory, one for all image files (matching a specific REGEX pattern.) The file names are input to the ReadImage operator which creates a tuple for each image. Images are combined with the blank image with 50 is added to the image and the result is displayed in a X11 window.

toolkit operators used:

- `AddText`
- `Blank`
- `CombineImg`
- `ReadImage`
- `X11Viewer`

log.spl
-------

Demonstrates the DoLog operator functionality. Web cam images are passed through the DoLog operator both regular and inverted. The results are displayed next to the original image in a X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `Collage`
- `DoLog`
- `X11Viewer`

mix\_cam\_snow.spl
------------------

Captures video from a local webcam. Images are converted to grey. The snow operator creates a stream of random snow images the same dimensions as the web cam images. The grey web cam images and the snow images are “ORed” together, effectively creating a snowy cam image displayed in a X11 window.

toolkit operators used:

- `Apply2`
- `CaptureFromCAM`
- `CvtColor`
- `Snow`
- `X11Viewer`

modec.spl
---------

Captures video from a local webcam. The motion between consecutive images is detected and motion vectors are drawn on the image. The stream stats are printed on the image before displaying in a X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `MotionDetection`
- `Stats`
- `X11Viewer`

multiple\_cameras.spl
---------------------

Captures video from one or more cameras attached to the machine, passes the images through a face detection model, adds text labels to the images, and displays the results side-by-side in an X11 window.

toolkit operators used:

- `AddText`
- `CaptureFromCAM`
- `Collage`
- `DrawRectangles`
- `FaceDetection`
- `X11Viewer`

onc1.spl
--------

Reads a stream of images from a video file as fast as possible. Images have a black box drawn on them hiding some feature of the input video (e.g. timestamp or logo), then any resulting empty frames are discarded.

The frames are then paced to the same rate as the input video and output to a MJPEGStreamer on a specific port.

toolkit operators used:

- `CaptureFromFile`
- `FramePacer`
- `MakeBox`
- `MJPEGStreamer`
- `SkipEmpty`

onc2.spl
--------

Captures video from a input file. Images are converted to grey scale. High and low thresholds are applied. The low value indicates pixels with a value less than are converted to black(0). The high value indicates pixels with larger values are converted to max(255) and less/equal are converted to black(0). Trackbars are used to allow the user to adjust the threshold values for the high and low thresholds. The two thresholded images are “ORed” together resulting in all “max” pixels being kept from the high threshold image and then all remaining pixels being kept from the low threshold image. Connected components are detected in the resulting image, components are white(255) and non-component pixels are black(0).

The thresholded video is displayed in a X11 window and the connect component video is displayed in a second X11 window.

toolkit operators used:

- `Apply2`
- `CaptureFromFile`
- `ConnectedComponents`
- `CvtColor`
- `Threshold`
- `TrackBar`
- `X11Viewer`

onc3.spl
--------

Captures video from a local webcam. Any empty frames are skipped prior to flipping the image vertically and displaying in a X11 window.

Also the flipped images are smoothed before background/foreground detection is done. For the first 5s, the background is “learned”, then the foreground connected objects are detected. Components are displayed white(255) and non-component pixels are displayed black(0) in a second X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `CodeBook`
- `ConnectedComponents`
- `Flip`
- `SkipEmpty`
- `Smooth`
- `X11Viewer`

onc4.spl
--------

Captures video from a local webcam. Any empty frames are skipped prior to pacing the input image stream to the same as an input file. The images are converted to grey before thresholding is done. All pixels with value greater than are changed to zero(black). A trackbar is used to allow the user to adjust the threshold value.

Connect components are detected in the threshold image and contours are detected and drawn in white on a black image. The threshold images and contour images are output to separate MJPEGStreamers.

toolkit operators used:

- `CaptureFromCAM`
- `ConnectedComponents`
- `CvtColor`
- `DrawContours`
- `FramePacer`
- `MJPEGStreamer`
- `SkipEmpty`
- `Threshold`
- `TrackBar`

onc5.spl
--------

Captures video from a local webcam. The images are converted to grey before the Canny operator is used to detect image contours. Trackbars are used to allow the user to adjust the threshold values to the Canny operator. Any empty frames (no contours) are skipped prior to displaying the results in a X11 window.

Also the images from the Canny operator are converted to 3 channel images in order to display next to the original input video. This image collage is saved to an output file at the same rate as an input video.

toolkit operators used:

- `Canny`
- `CaptureFromCAM`
- `Collage`
- `CvtColor`
- `SaveToFile`
- `SkipEmpty`
- `TrackBar`
- `X11Viewer`

onc\_f.spl
----------

Remove empty frames from a video file. Captures video from a input file. Any empty frames are skipped prior to saving to an output file.

toolkit operators used:

- `CaptureFromFile`
- `SaveToFile`
- `SkipEmpty`

proxy2.spl
----------

Captures video from a local webcam. The resulting video is output through a proxy connection. Then video is captured through a proxy connection. The resulting video is displayed in a X11 window.

(See cam\_proxy and src\_proxy demos for a similar split version of this proxy demo)

toolkit operators used:

- `CaptureFromCAM`
- `DisplayProxy`
- `SourceProxy`
- `X11Viewer`

rank.spl
--------

Captures video from a local webcam.

Frames are adaptively skipped prior to performing minimum rank filtering. The stream stats are printed on the image before displaying in a X11 window.

Frames are adaptively skipped prior to performing median rank filtering. The stream stats are printed on the image before displaying in a X11 window.

Frames are adaptively skipped prior to performing maximum rank filtering. The stream stats are printed on the image before displaying in a X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `RankFilter`
- `SkipFrame`
- `Stats`
- `X11Viewer`

record.spl
----------

Reads a stream of images from a video file. Images are flipped and timestamped with a time relative to the start of the stream.

The original and flipped/timestamp videos are displayed in separate X11 windows. Also the flipped/timestamp video is saved to an output file.

toolkit operators used:

- `CaptureFromFile`
- `Flip`
- `SaveToFile`
- `TimeStamp`
- `X11Viewer`

rotate.spl
----------

Rotates and crops an image stream from a webcam (assumes a 640x480 input image.) Captures video from a local webcam. Images are rotates 90 degrees around a specified point and scaled to 75 image is the same size as the input image and has black background where the rotated image is not. The black background is cropped out of the image. The original, rotated, and cropped images are displayed side-by-side in a X11 window.

toolkit operators used:

- `CaptureFromCAM`
- `Collage`
- `Crop`
- `Rotate`
- `X11Viewer`

snow.spl
--------

Random snow images are created at 10 frames/s. The frames are resized to 640x480 before smoothing and displaying in a X11 window.

toolkit operators used:

- `Resize`
- `Smooth`
- `Snow`
- `X11Viewer`

speed.spl
---------

A rough speed test. Creates a stream of 1000 blank images with a specific height, width, and color as fast as possible. The images are smoothed. Then the stats <span>tuples/s, bytes/s, and number of seconds</span> are written to a log.

toolkit operators used:

- `BitBucket`
- `Blank`
- `Smooth`

src\_proxy.spl
--------------

Captures video through a proxy connection. The resulting video is displayed in a X11 window.

(See cam\_proxy demo for the transmitting proxy demo)

toolkit operators used:

- `SourceProxy`
- `X11Viewer`

threshold.spl
-------------

Captures video from a input file. Images are converted to grey scale. High and low thresholds are applied. The low value indicates pixels with a value less than are converted to black(0). The high value indicates pixels with larger values are converted to max(255) and less/equal are converted to black(0). Trackbars are used to allow the user to adjust the threshold values for the high and low thresholds. The two thresholded images are “ORed” together resulting in all “max” pixels being kept from the high threshold image and then all remaining pixels being kept from the low threshold image. The resulting video is displayed in a X11 window.

toolkit operators used:
 
- `Apply2`
- `CaptureFromFile`
- `CvtColor`
- `Threshold`
- `TrackBar`
- `X11Viewer`

url.spl
-------

Periodically polls for an image from a url. Images are displayed in a X11 window.

toolkit operators used:

- `CaptureFromURL`
- `X11Viewer`

video\_stream.spl
-----------------

Reads a stream of images from a video file. Images are output to a MJPEGStreamer on a specific port and output to a HTTPViewer on a specific port.

toolkit operators used:

- `CaptureFromFile`
- `HTTPViewer`
- `MJPEGStreamer`

xcombine.spl
------------

Reads a stream of images from a video file. A second image is created by resizing the first to 130 with an offset and 30 second image does not overlap the first, the pixels are discarded. The result is displayed in a X11 window.

toolkit operators used:

- `CaptureFromFile`
- `CombineImg`
- `Resize`
- `X11Viewer`

----

&copy; Copyright 2012, 2016, International Business Machines Corporation, All Rights Reserved 
