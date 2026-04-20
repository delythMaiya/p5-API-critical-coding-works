# Assignment #9: Points, Lines, Curves


<img src="../images/lines.jpg" width=800>


_Due 9am on the day of your class via your github notebook (plus your printout)_

## Quiz
* Points, Lines, Curves (from lecture/slides)
* Pixels in p5.js: [Reference](https://p5js.org/reference/p5/pixels/), [Coding Train](https://www.youtube.com/watch?v=nMUMZ5YRxHI), [IDM-NYU](https://idmnyu.github.io/p5.js-image/)



### Coding   
Creating a puddle hand drawn texture  
https://editor.p5js.org/sizalyth/sketches/a5oD_Q5Pb 
![image](https://git.arts.ac.uk/user-attachments/assets/d3042bef-4a91-475f-b68a-e1ad4a4ccc19)



I wanted to create something similar to this (sketch):   
![image](https://git.arts.ac.uk/user-attachments/assets/7343fb1e-da9e-453c-9240-44db231cca6b)

Puddle has an oval structure with some gaps (that are not random). In class, we made a walker from point A to point B, but I wanted my sketch to follow the path of an oval. 
I first create the shape of oval.   
![image](https://git.arts.ac.uk/user-attachments/assets/e06bfe7c-a429-4b32-bbd9-e6c0e25165dc)
It ended up as a circle first because I used just one radius value, but an ellipse has different radius value for x and y direction, therefore 
```js
let x = cx + r*cx * cos(a);
let y = cy + r*cy * sin(a);
```
![image](https://git.arts.ac.uk/user-attachments/assets/f9146741-a2bf-4900-b1f9-a0c56d98ef27)
The first ellipse I made had less gap between other circles but looked thick and nice so I am going to keep this and make another for loop with ellipse with more variation of rx and ry.   

I had a problem with one line protruding from the outer circle like this. I resolved this by having beginShape() and endShape() in both for loops. 
![image](https://git.arts.ac.uk/user-attachments/assets/9344d467-40b4-43c0-88a4-b2ce6f48df8e) ![image](https://git.arts.ac.uk/user-attachments/assets/75097a43-d1f5-4017-8c18-dcb453742355)



### In - Class Exercises   
sorry I had to leave at 4:30 pm this friday but I have watched the rest of the class on panopto and caught up, I hope it wasn't rude.  

Creating a gradient:   
![image](https://git.arts.ac.uk/user-attachments/assets/e5eb6860-9de4-4291-a69c-70b4d2e2e781)  

```js  
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  for(x = 0;x<400;x+=1){
    stroke(x*1);
    line(x,0,x, height);
  };
}
```  
100 calls to create line circle: 
x = starting point + cos(angle) * length   
y = starting point + sin(angle) * length  
![image](https://git.arts.ac.uk/user-attachments/assets/87d8a8d9-dfb4-46ae-94c9-1baa1b88639a)    

```js 
let x = 100, y = 100, angle = 30;
function setup() {
  createCanvas(400, 400);
  angleMode(DEGREES);
}

function draw() {
  background(0);
 
  
  
  for(n = 0; n < 100; n++){
    let angle = map(n, 0, 100, 0, 360);
    let cx = 200;
    let cy = 200;
    let x = cx + cos(angle) * 200;
    let y = cy + sin(angle) * 200;
    strokeWeight(3);
   stroke(255);
    line(cx, cy, x, y);
  }
}
```
random position 20 lines :  
![image](https://git.arts.ac.uk/user-attachments/assets/d1788260-3c06-44fc-ad99-d9c3c70ac8d7)  

```js  
let x;
let y;
let x1;
let y1;

function setup() {
  createCanvas(400, 400);
  background(0);
  
  for (n = 0; n < 19; n++) {
    x = random(400);
    y = random(400);
    x1 = random(400);
    y1 = random(400);
    stroke(255);
    strokeWeight(2);
    line(x, y, x1, y1);
  }
}
```
but this time, all the lines connected together. (updating x1 and y1 as new starting of x and y)  
![image](https://git.arts.ac.uk/user-attachments/assets/261dc78a-9743-4e6f-b417-1aa956a040fc)  

```js
function setup() {
  createCanvas(400, 400);
  let x = random(width);
  let y = random(height);
  for (let i = 0; i < 19; i++) {
    let x1 = random(width);
    let y1 = random(width);
    line(x, y, x1, y1);
    x = x1;
    y = y1;
  }
}
```
fixed length + setting p1 = p2 , 100 lines. 
This example I struggled at first but I understood the logic by looking at the answer code, and I then closed the answer and tried to write down the code myself without looking.   
One thing that made me wonder is the second inner loop doesn't have to be <350? as long as it checks through available angles it's fine?   

![image](https://git.arts.ac.uk/user-attachments/assets/081fe3de-e521-4a60-8f9a-ffbd8a1a9979)  

```js
function setup() {
  createCanvas(400, 400);
  background(220);
  angleMode(DEGREES);

  let p1 = { x: random(20, width - 20), y: random(20, height - 20) };
  fill("red");
  circle(p1.x, p1.y, 10);

  for (let i = 0; i < 99; i++) {
    let ang = random(360);

    for (let j = 0; j < 350; j++) {
      let p2 = { x: p1.x + cos(ang+j) * 200, y: p1.y + sin(ang+j) * 200 };

      if (
        p2.x >= 20 &&
        p2.x <= width - 20 &&
        p2.y >= 20 &&
        p2.y <= height - 20
      ) {
        line(p1.x, p1.y, p2.x, p2.y);
        p1 = p2;
        break;
      }
    }
  }
}
```

Line segmentation :    ![image](https://git.arts.ac.uk/user-attachments/assets/c661ed0b-d455-468e-9829-9f7d7fe46586)  
```js
Circles at regular interval with lerp()  
function setup() {
  createCanvas(400, 400);
  background(220);
  let p1 = { x: 50, y: 100 };
  let p2 = { x: 320, y: 100 };

  let Steps = 10;

  createCircles(p1, p2, Steps, 10);
  p1.y += 50;
  p2.y += 50;
  createCircles(p1, p2, Steps, 6);
}

function createCircles(a, b, steps, radius) {
  line(a.x, a.y, b.x, b.y);
  for (i = 0; i < 11; i++) {
    let progress = i / steps;
    let x = lerp(a.x, b.x, progress);
    let y = lerp(a.y, b.y, progress);
    circle(x, y, 10);
  }
}
```

![image](https://git.arts.ac.uk/user-attachments/assets/72cf6966-13e7-442a-93c1-dc1747c035c6)  

```js
function setup() {
  createCanvas(400, 400);
  background(220);
  angleMode(DEGREES);
  let p1 = { x: 20, y: 100 };
  let p2 = { x: 380, y: 120 };

  let Steps = 10;
  let ang = atan2(p1, p2);

  createCircles(p1, p2, Steps, 10);
  p1.y += 50;
  p2.y += 50;
  createCircles(p1, p2, Steps, 6);
}

function createCircles(a, b, steps, len) {
  let ang = atan2(b.y - a.y,b.x - a.x);

  for (i = 0; i < 11; i++) {
    let progress = i / steps;
    let x = lerp(a.x, b.x, progress);
    let y = lerp(a.y, b.y, progress);
    //making additional point that moves as it lerps through 
    let x1 = x + cos(ang)*len;
    let y1 = y + sin(ang)*len;
    ang += random(10);
    line(x, y, x1, y1);
  }
}
```
stroke weight size change   
![image](https://git.arts.ac.uk/user-attachments/assets/06f62dcc-7fa7-4536-8768-edd6cd086ea9)  
```js
let ang = atan2(b.y - a.y, b.x - a.x);
  let minimumW = 2;
  let maxW = 20;

  for (i = 0; i < 11; i++) {
    let progress = i / steps;
    let x = lerp(a.x, b.x, progress);
    let y = lerp(a.y, b.y, progress);
    //making additional point that moves as it lerps through
    let x1 = x + cos(ang) * len;
    let y1 = y + sin(ang) * len;
    let weight = map(i, 0, 10, 2, 20);
    ang += random(10);
    strokeWeight(weight);
    line(x, y, x1, y1);
```

curves & curveVertex exercises   
straight lines between point= vertex, curves between points = curveVertex  















