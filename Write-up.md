# **Finding Lane Lines on the Road** 


### 1. Pipeline

1. Read in images
2. Convert to grayscale
3. Apply Gaussian blur
4. Define a region of interest to mask using x,y coordinates of image. Set all regions outside mask to black.
5. Using grayed, blurred image, use Canny edge detection to find lane lines within region of interest.
6. With images of edges within region of interest, use Hough transform to turn those edges into lines.
7. With Hough lines created, separate lines into left and right lane lines using the slope of the lines. Extrapolate single line for each set of left and right lane lines.
8. Make these new lines transparent, add red color, and draw them on top of original image.

### 2. Shortcomings

Initially, the lines along the broken lane lines in the videos were pretty jumpy. I've tried increasing rho - the pixel resolution of the radius, r, in the Hough transform - to 2 to help smooth the definition of the lines. I then increased the threshold - the number of hough curve intersections before declaring a line - quite a bit. This had the most noticeable stabilizing effect on the lines in the videos. Increasing the min line length and the max gap between lines also improved line stability and accuracy.

My pipeline really broke down in the challenge video though. It turns out that the biggest problem with the challenge video is that it needed to be resized to match the parameters that I set up in the region_of_interest function. Once resized it created lines on to of the lane lines more or less as expected. However, it doesn't seem to be able to process the whole video. The breakdown happens 4-5 seconds into the challenge video where we see the change in the pavement where the bridge crossing is. Here the pavement changes from black asphalt to gray concrete then back again at the end of the bridge. This is where the line overlays really jump around.

According to the error message in the challenge_output cell, it seems that the draw_lines function isn't getting the data it's expecting. Specifically, I'm using the numpy polyfit function to create the lines. I may need a different process here to create the line.

### 3. Improvements

I'm not really sure what improvements could be made for this process. The only problem I'm really having is that the challenge video can't process beyond where the road turns into the bridge. Not really sure how to handle that just now.
