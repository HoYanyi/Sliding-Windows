# Sliding-Windows
#視窗預設 128*128

Step1.匯入需要使用的涵式庫
*.Opencv
*.Numpy
*.Os



import cv2
import numpy as np
import os

if __name__ == "__main__":
    img = cv2.imread("img")
    
    img_width = img.shape[1]
    img_height = img.shape[0]
    initial_coords = [0, 0]
    
    #windowsize = (128,128)
    window_size = 128
    stride = 128
    
    
    direction ="right"
    
    img_copy = img.copy()
    idx = 0

    while True:
        if direction == "right":
            initial_coords[0] += 128
            
            idx += 1
            #cv2.imwrite(str(idx) + ".jpg", roi)
            
        bottom_right_coord = (initial_coords[0] + stride , initial_coords[1]+ stride)
        cv2.rectangle(img_copy, (initial_coords[0], initial_coords[1]) , bottom_right_coord, (255,0,255), 2)
        roi=img[initial_coords[1]: initial_coords[1]+ stride, initial_coords[0]:initial_coords[0] + stride]
        #cv2.write()
        
        cv2.imwrite('cropped_image_' + str(idx) + '_.jpg', roi)
        print(roi.shape)
        #initial_coords[0] += 1 #move window by one unit
        cv2.imshow("img",img_copy)
        cv2.waitKey(10)
        img_copy = img.copy()
        print(bottom_right_coord, img_width, img_height)
        if bottom_right_coord[0] >= img_width:
            initial_coords[0] = 0
            initial_coords[1] +=128
            
            
        if bottom_right_coord[0] >= img_width and bottom_right_coord[1] >= img_height:
            break
            
    cv2.destroyAllWindows()
