Reading Images and videos
cv.imread(Path, 0 or 1 for rgb or black and white) - It takes the path of the image and returns the image in form of a matrix.
cv.imshow('Name of window', name of matrix of pixels)- It displays the matrix of the pixels of an images in a separate window.
cv.VideoCapture(0,1,2  or path to the video)- 0 represents the webcam and 1,2 represents first second camera connected to the computer respectively. A video is read frame by frame using the imshow method using a file loop. Snippet-
capture = cv2.VideoCapture('Videos/dog.mp4')  
while True:  
    isTrue, frame = capture.read()  
    cv2.imshow('Video', frame)  
    if cv2.waitKey(20) & 0xFF == 'd':  
        break  
capture.release()  
cv2.destroyAllWindows()
-215 assertion failed is usually thrown when a wrong path is spceified or if the video runs out of frames.

Resizing and Rescaling images-
  
def rescaleframe(frames, scale=0.75):  
    width = int(frames.shape[1]*scale)  
    height = int(frames.shape[0]*scale)  
  
    dimensions=(width,height)  
    return cv2.resize(frame , dimensions, interpolation=cv2.INTER_AREA)  
  
capture = cv2.VideoCapture('Videos/dog.mp4')  
while True:  
    isTrue, frame = capture.read()  
    frame_resized = rescaleframe(frame)  
    cv2.imshow('Video', frame)  
    cv2.imshow('resize_video', frame_resized)  
    if cv2.waitKey(20) & 0xFF == 'd':  
        break  
capture.release()  
cv2.destroyAllWindows()  
cv2.waitKey()

Exclusive to Live videos only-
def changeRes(width,height)
    capture.set(3,width)
    capture.set(4,height)
2X2 transformations-
parallel lines remains parallel
closed under compostion
orgin mapps to origin 
line mapps to lines

Projective mapping mapps one plan to other through a point.

Converting to grayscale-gray= cv2.cvtColor(img, cv.COLOR_BGR2GRAY)
Bluring-cv2.GaussianBlur(img,(3,3),cv2.BORDER_DEFAULT)
(3,3)- Values must be odd and is called kernel size,
Edge detection and Cascading-canny=cv2.Canny(img, 125,175)
edges reduce on bluring.
Dilation-cv2.dilated(canny, (7,7), iterations=3)- It is bascially used to dilated or increase the input property in this case edges.
Eroding- cv2.erode(dilated,(3,3), iterations=1)- Used to reverse the effect of dilation.
Resize- cv2.resize(img, (500, 500), interpolation=cv.INTER_AREA,scaling factor of x, scaling factor y)- (500,500 ) is the destination size.
For scaling up the image use INTER_LINEAR OR INTER_CUBIC  inter_cubic is the slowest but produces the image of the hightest quality.
Cropping - img[50:200 , 200:400]
Translation-
def translate(img, x, y)
               transMat = np.float([1,0,x],[0,1,y])
               dimensions = (img.shape[1], img.shape[0])
               return cv2.wrapAffine(img, transMat, dimensions)
 x and y in function defination is the number of pixels of x and y axis by which it the image has to be shifted.
 +x - right
 -x - left
 -y - up 
 +x - down 
Rotation- 
def rotation( img, angle, rotpoint=None)
               (height,width) = img.shape[ :2]
               if rotpoint=None
                rotpoint = (width//2, height//2)
             rotMat = cv2.getRotationMatrix2D(rotpoint, angle, scale=1.0)

Flipping - cv2.flip(img, 0/1/-1)
0 - flip vertical about x-axis
1 - flip horizontal about y-axis
-1 - flip both horizontally and vertically

Contours are the joints or curves of the boundaries of an object.
contours,hierearchies = cv2.findContours(canny, cv2.RETR_LIST, cv2.CHAIN_APPROX_SIMPLE)
chain_approx_simple returns only the end points of the point while 
chain_approx_none returns not only the end points but also all the points lying in the line.

threshold is an alternative to canny edge detection. It takes the image and tries to binarize the image.
ret, threshold = cv2.threshold(gray,125,255, cv2.THRESH_BINARY)
125 and 255 means that all the pixel below the pixel density of 125 will be converted to black and all the pixels which have the pixel density of 255 will have white color.
Types of color channel - HSV, BGR, LAB,RGB
In order  to get the three channel color use the command
b,g,r = cv2.split(img)
To merge all the three b,g,r images use-
merge= cv2.merge([b,g,r])
To get the images with respective colors instead of there grayscale color-density image 
blank = np.zeroes([ :2] dtype='uint8')
blue = cv2.merge([b,blank,blank])
Blurring- 
Types of blurring- medianBlur,blur,GaussianBlur,bilateralFilter
Bilateral blur blurs the image while retaining the number of edges in the image.Its syntax is as following
cv2.bilateralFilter(img, diameter, sigmaColor , sigmaSpace)
Sigma space and color are  used to specify pixels of color and space how farther influence the calculation of the current pixel.
In median blur instead of passing a tuple a single constant value is passed.
Bitwise operations
bitwise_and(img1 , img2)- intersectiong region
bitwise_or(    "    ) - all the regions
bitwise_xor(    "   )- non intersecting region

Masking -
cv2.bitwise_and(img, img, mask=mask)