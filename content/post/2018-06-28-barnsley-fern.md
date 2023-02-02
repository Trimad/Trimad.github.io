---
author: Tristan Madden
categories: [Java, Processing]
date: 2018-06-28
tags: [fractal]
title: Barnsley Fern
---
hell yeah dude
![](https://res.cloudinary.com/deiub7j41/image/upload/v1649389439/barnsley_fern_hkv4cc.png)

{{< youtube V6b9nNOdKV4 >}}

```Java
float x = 0;
float y = 0;

float[][] magicX = {  
  {0.00, 0.00}, 
  {0.85, 0.04}, 
  {0.20, -0.26}, 
  {-0.15, 0.28}
};

float[][] magicY = {  
  {0.16, 0.00, 0.00}, 
  {-0.04, 0.85, 1.6}, 
  {0.23, 0.22, 1.6}, 
  {0.26, 0.24, 0.44}
};

//PGraphics pg;

int iterations = 123456;

void setup() {
  //fullScreen(P3D);
  size(2048, 2048, P3D);
  background(0);
  histogram = new int[width][height];
  //pg = createGraphics(width*2, height*2);
  //pg.beginDraw();
  //pg.background(0, 50);
  //pg.endDraw();
}

boolean record = false;
void draw() {
  /*
   background();
   translate(width*0.5, 0, 0);
   rotateY(frameCount*0.01);
   translate(-width*0.5, 0, 0);
   image(pg, -width, -height);
   */

  for (int i = 0; i < iterations; i++) {
    getPoint();
    drawPoint();
  }

  if (frameCount < 100) {
    saveFrame("frame-####.jpg");
  } else {
    exit();
  }
}

void getPoint() {

  float dx = 0;
  float dy = 0;

  float r1 = random(1);
  if (r1 < 0.01) {
    //1
    dx =  magicX[0][0];
    dy = magicY[0][0] * y;
  } else if (r1 < 0.86 ) {
    //2
    dx = magicX[1][0] * x + magicX[1][1] * y;
    dy = magicY[1][0] * x + magicY[1][1] * y + magicY[1][2];
  } else if (r1 < 0.93) {
    //3
    dx = magicX[2][0] * x + magicX[2][1] * y;
    dy = magicY[2][0] * x + magicY[2][1] * y + magicY[2][2];
  } else {
    //4
    dx = magicX[3][0] * x + magicX[3][1] * y;
    dy = magicY[3][0] * x + magicY[3][1] * y + magicY[3][2];
  }

  x = dx;
  y = dy;
}

int[][] histogram;
int highest = 0;

void drawPoint() {

  int px = (int)map(x, -2.1820, 2.6558, width*0.19, width*0.81);
  int py = (int)map(y, 0, 9.9983, height*0.99, height*0.01);

  histogram[px][py]++;

  if (histogram[px][py] > highest) {
    highest = histogram[px][py];
    set(px, py, 255);
  }

  if (highest > 1) {
    //float bright = map(histogram[px][py], 0, (float)Math.log(highest), 0, 255);
    //stroke(histogram[px][py], bright,0);
    float m = map(histogram[px][py], 0, log(highest), 0, 1);
    color from = color(#123556);
    color to = color(255);
    color l = lerpColor(from, to, m);

    // pixels[py*width+px] = l;
    set(px, py, l);
  }
}
```

Written using the Processing Java library: https://processing.org/download