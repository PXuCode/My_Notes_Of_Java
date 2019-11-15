# Project1 Features

> 小组成员：
>
> 苏志华 19125238
>
> 徐    鹏 19125258

## 实验一：

### 题目摘要：

>  Project materials including writeup template PA_Features.zip.  
>
>  Two assignments including an acquaintance of Image File and an implementation of Edge Detection.  
>
> 1.  读文件Madrill.bmp  
> 2.  将读入的图像转换成8bit bmp，保存变换后的图像 
> 3.  编写程序将黑白图像按照下图示进行变换： 

### 代码：

```c++
#include<opencv2/opencv.hpp>
#include<opencv2/features2d.hpp>
#include<iostream>
using namespace std;
using namespace cv;
int main()
{
	Mat image = imread("mandrill.bmp", IMREAD_GRAYSCALE);
	if (image.empty())
	{
		cout << "error..." << endl;
		return -1;
	}
	imshow("原图", image);
//将读入的图像转换成8bit bmp，保存变换后的图像
Mat image_8;
image.convertTo(image_8, CV_8UC1);
//imshow("8bit", image_8);
imwrite("mandrill_8.bmp", image_8);
/*line(image_8, Point(0, 10), Point(image_8.cols, 10), Scalar(255, 0, 0), 1);
line(image_8, Point(0, 40), Point(image_8.cols, 40), Scalar(255, 0, 0), 1);
line(image_8, Point(65, 10), Point(65, 40), Scalar(255, 0, 0), 1);
line(image_8, Point(195, 10), Point(195, 40), Scalar(255, 0, 0), 1);*/
//rectangle(image_8, Rect(65, 10, 130,30), Scalar(255, 0, 0), 2);
Mat rio = image_8(Rect(65, 10, 130, 30));
Mat fliprio = image_8(Rect(65, 10, 130, 40));
Mat imageRio = image_8(Rect(65, 50, 130, 30));
Mat flipImage = image_8.clone();
Mat imageFlipRio = flipImage(Rect(65, 50, 130, 40));
Mat RectImage = image_8.clone();
rectangle(RectImage, Rect(50, 10, 160, 50), Scalar(255, 0, 0), 2);
imshow("画矩形", RectImage);
imwrite("Rect_img.jpg", RectImage);// 保存矩形图像
flip(fliprio, fliprio, 0);
//imshow("翻转", fliprio);
rio.copyTo(imageRio);
fliprio.copyTo(imageFlipRio);
imshow("平移后", image_8);
imwrite("平移后.jpg", image_8); // 保存
imshow("翻转", flipImage);
imwrite("filp_img.jpg", flipImage); // save
waitKey(0);
return 0;
}
```

### 实验结果：

![1573176855403](D:\徐鹏\Documents\cloud\我的坚果云\Typora\JavaNotes\JavaSE\1573176855403.png)

## 实验2：

### 题目摘要：

> The main steps of edge detection are: 
>
> (1) assign a score to each pixel; 
>
> (2)  find local maxima along the direction perpendicular to the edge. Sometimes a third  step is performed where local evidence is propagated so that long contours are more  confident or strong edges boost the confidence of nearby weak edges.
>
>  Optionally, a  thresholding step can then convert from soft boundaries to hard binary boundaries.    

### 代码：

~~~c++

~~~



### 实验结果：

![1573177294044](D:\徐鹏\Documents\cloud\我的坚果云\Typora\JavaNotes\JavaSE\1573177294044.png)



![1573177301248](D:\徐鹏\Documents\cloud\我的坚果云\Typora\JavaNotes\JavaSE\1573177301248.png)

![1573177416142](D:\徐鹏\Documents\cloud\我的坚果云\Typora\JavaNotes\JavaSE\1573177416142.png)

![1573177426661](D:\徐鹏\Documents\cloud\我的坚果云\Typora\JavaNotes\JavaSE\1573177426661.png)

