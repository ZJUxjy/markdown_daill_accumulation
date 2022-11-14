# Mat.at

at操作是一种直接简单的对单个像素的操作方式，用于获取图像矩阵某点的值或改变某点的值
```cpp
//原型：
cv::MAT.at<>();

//实际应用
lidar2camera.at<float>(0, 0) = 1.0;

uchar srcPixel_value = cv::Mat.at<uchar>(row, col);  
cv::Mat.at<uchar>(row, col) = srcPixel_value ;
```

