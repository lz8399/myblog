+++
title= "[Math]如何检测某个点是否在多边形内部或者直线上"
date= "2016-06-23T19:14:02+08:00"
categories= ["Math"]
tags= ["Math"]
+++

##### 点在多边形内的判别方法

    int pnpoly(int nvert, float *vertx, float *verty, float testx, float testy)
    {
        int i, j, c = 0;
        for (i = 0, j = nvert-1; i < nvert; j = i++) 
        {
            if (((verty[i] > testy) != (verty[j] > testy)) &&
                (testx < (vertx[j] - vertx[i]) * (testy - verty[i]) / (verty[j] - verty[i]) + vertx[i]) )
            {
                c = !c;
            }
        }
        return c;
    }
    
Arguments

+ nvert: Number of vertices in the polygon. Whether to repeat the first vertex at the end has been discussed in the article referred above.
+ vertx, verty: Arrays containing the x- and y-coordinates of the polygon's vertices.
+ testx, testy: X- and y-coordinate of the test point.

https://stackoverflow.com/a/2922778/1645289


##### 点在两点之间的直线上的判别方法

    bool isLieOnLine()
    {
        dxc = currPoint.x - point1.x;
        dyc = currPoint.y - point1.y;

        dxl = point2.x - point1.x;
        dyl = point2.y - point1.y;

        //point lies on the line if and only if (dxc * dyl - dyc * dxl) is equal to zero.
        bool isCrossLine = dxc * dyl - dyc * dxl == 0;

        if(isCrossLine)
        {
            if (abs(dxl) >= abs(dyl))
              return dxl > 0 ? 
                point1.x <= currPoint.x && currPoint.x <= point2.x :
                point2.x <= currPoint.x && currPoint.x <= point1.x;
            else
              return dyl > 0 ? 
                point1.y <= currPoint.y && currPoint.y <= point2.y :
                point2.y <= currPoint.y && currPoint.y <= point1.y;
        }

        return false;
    }

https://stackoverflow.com/a/11908158/1645289


##### 参考

How to check if a given point lies inside or outside a polygon?  
http://www.geeksforgeeks.org/how-to-check-if-a-given-point-lies-inside-a-polygon/

How to check if a point is inside a rectangle?  
http://math.stackexchange.com/questions/190111/how-to-check-if-a-point-is-inside-a-rectangle

How can I determine whether a 2D Point is within a Polygon?  
http://stackoverflow.com/questions/217578/how-can-i-determine-whether-a-2d-point-is-within-a-polygon#

How to check if a point lies on a line between 2 other points  
https://stackoverflow.com/questions/11907947/how-to-check-if-a-point-lies-on-a-line-between-2-other-points

Check if a point belongs on a line segment  
https://www.lucidar.me/en/mathematics/check-if-a-point-belongs-on-a-line-segment/