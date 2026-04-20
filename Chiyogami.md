## Chiyogami Papers With Code! 
**CODING**  
<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/0d179e9e-969e-4124-b538-f03c2781e31e" />

View link: https://editor.p5js.org/sizalyth/full/O0tsCNZMK 
Sketch Link: https://editor.p5js.org/sizalyth/sketches/O0tsCNZMK

I took inspiration from Japanese Chiyogami papers. Specififically, the pattern in this image; 
<img width="768" height="432" alt="image" src="https://github.com/user-attachments/assets/ef7e1cf9-9e6e-481b-9292-ddde2f8e99b4" />

Also, I wanted to add sensu fans like this with fractals inside.     
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/890c3bbc-0320-4603-aea0-142ddd7064a8" />

```js
function setup() {
  createCanvas(400, 400);
  background(0);
  let x = 0;
  let y = 0;
  let w = width;
  let h = height;
  let depth = 2;
  drawRect(x, y, w, h, depth);
}

function drawRect(x, y, w, h, depth) {
  if (random() < 0.22 || depth > 3) {
    drawRect(x, y, w / 2, h / 2, depth - 1);
    drawRect(x + w / 2, y, w / 2, h / 2, depth - 1);
    drawRect(x, y + h / 2, w / 2, h / 2, depth - 1);
    drawRect(x + w / 2, y + h / 2, w / 2, h / 2, depth - 1);
  } else if (random() < 0.02 || depth > 0) {
    drawRect(x, y, w / 4, h / 4, depth - 1);
    drawRect(x + w / 4, y, w / 4, h / 4, depth - 1);
    drawRect(x, y + h / 4, w / 4, h / 4, depth - 1);
    drawRect(x + w / 2, y + h / 2, w / 2, h / 2, depth - 1);
  } else {
    noFill();
    stroke(255);
    rect(x, y, w, h);
  }
}
```
Square inside the square, and then adding two lines across.  
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/5a8ee1d1-d049-4223-8eff-f20fb2c3cd4b" />


```js
    quad(x + w / 2, y, x + w, y + h / 2, x + w / 2, y + h, x, y + h / 2); //square inside the sqaure
    let pointA = { x: (x + w / 2 + (x + w)) / 2, y: (y + (y + h / 2)) / 2 };
    let pointB = { x: (x + w / 2 + x) / 2, y: (y + h / 2 + (y + h)) / 2 };
    let pointC = { x: ((x + w / 2) + x) / 2, y: (y + (y + h / 2)) / 2 };
    let pointD = { x: ((x + w / 2) + (x+w)) / 2, y: ((y + h / 2) + (y + h)) / 2 };
    line(pointA.x, pointA.y, pointB.x, pointB.y); //the two lines inside the inner circle.
    line(pointC.x, pointC.y, pointD.x, pointD.y);
```  
I initially made the mistake of adding ellipse by incrementing +10 pixels but I had to make it relative to each size of the square, so I took the distance of one quad and divided it by a number that looked the best.  
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/39416699-3fbb-4a78-98ed-9bf9ed0ae498" />


```js
   fill(255);
    ellipse(centre.x+(d/3), centre.y,d/2 ,d/10) //ellipse shape for the inside 
    ellipse(centre.x-(d/3), centre.y,d/2 ,d/10)
    ellipse(centre.x, centre.y+(d/3),d/10 ,d/2)
    ellipse(centre.x, centre.y-(d/3),d/10 ,d/2)
    noFill()
    rect(x, y, w, h); //main square
```  
Now, I wanted to add arcs for the sensu fans and hopefully place fractals inside it too.  
I first made a simple template of the arc with arbitary values.     
<img width="214" height="198" alt="image" src="https://github.com/user-attachments/assets/f0d9cbc3-562c-4e60-b2da-7dbaafb0fcc4" />  

```js
function setup() {
  createCanvas(400, 400);
  background(100);
  angleMode(DEGREES);
  let x = 140
  let y = 280
  let w = 200
  let h = 200;
  let start = 270;
  let end = 30;
  arc(x, y, w, h, start, end)
  arc(x, y, w/4, h/4, start, end)
}
```
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/210e265a-dd55-408b-8f0d-6f4edb8ead87" />  

The division wasb't really working with the mapping of the angle. I just changed the angle to start from lower number, as I couldn't figure out how to map lines when angles go from a higher value to low after going clockwise. 
```js
function setup() {
  createCanvas(400, 400);
  background(100);
  angleMode(DEGREES);
  let x = 140
  let y = 280
  let w = 200
  let h = 200;
  let start = 90;
  let end = 230;
  let depth=3;
  arc(x, y, w, h, start, end)
  arc(x, y, w/4, h/4, start, end)

  
  for (let i = 0; i<7; i++){
    let ang = map(i, 0, 7, start, end);
    let px = x + cos(ang)*(w/2)
    let py = y + sin(ang)*h/2
    line(x, y, px, py); 
    
  }
}
```
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/8665bf01-f3f3-423a-9d6f-17992fcf18bb" />  

Using the for loop, I created a triangle that connects between one point on the inner arc with two points on the outer arc, using two angle variables one for the current i and one for the next i. 
Then, using recursion and from exercises with Tyler Hobbs website, I passed these parameters to a fucntion to divide it in a random skewed way.     
```js
function setup() {
  createCanvas(400, 400);
  background(100);
  angleMode(DEGREES);
  let x = 140;
  let y = 280;
  let w = 200;
  let h = 200;
  let starta = 90;
  let end = 230;
  let depth = 8;
  let segments = 7;
  arc(x, y, w, h, starta, end);
  arc(x, y, w / 4, h / 4, starta, end);

  for (let i = 0; i < segments; i++) {
    let ang = map(i, 0, segments, starta, end);
    let px = x + cos(ang) * (w / 2);
    let py = y + sin(ang) * (h / 2);
    line(x, y, px, py);
    let ang1 = map(i, 0, segments, starta, end);
    let ang2 = map(i + 1, 0, segments, starta, end); //angle of the next i so that we can connect when making triangle.
    let outX1 = x + cos(ang1) * (w / 2); //points across the arc
    let outY1 = y + sin(ang1) * (h / 2);
    let outX2 = x + cos(ang2) * (w / 2);
    let outY2 = y + sin(ang2) * (h / 2);
    let inX1 = x + cos(ang1) * (w / 8);
    let inY1 = y + sin(ang1) * (h / 8);
    // Draw the triangle segment
    fill(random(200, 255), 100, 100, 150); // Semi-transparent fill
    sensuRecur(inX1, inY1, outX1, outY1, outX2, outY2, depth); //taking this first triangle, I will be diving this with recursion
  }
}

function sensuRecur(ax, ay, bx, by, cx, cy, depth) {
  if (depth > 0) {
    let mpx = (bx + cx) / 2;
    let mpy = (by + cy) / 2;
    let options = [1, 2, 3];
    if (random(options) == 1) {
      sensuRecur(bx, by, ax, ay, bx, by, depth - 1);
      sensuRecur(bx, by, ax, ay, cx, cy, depth - 1);
    } else if (random(options) == 2) {
      sensuRecur(cx, cy, ax, ay, bx, by, depth - 1);
      sensuRecur(cx, cy, ax, ay, cx, cy, depth - 1);
    } else {
      sensuRecur(mpx, mpy, ax, ay, bx, by, depth - 1);
      sensuRecur(mpx, mpy, ax, ay, cx, cy, depth - 1);
    }
  } else {
    triangle(ax, ay, bx, by, cx, cy);
  }
}
```
Now I am going to combine this into one sketch.    
<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/c46c1b75-82aa-441b-95be-4da2ef135a68" />

```js
function setup() {
  createCanvas(600, 600);
  background(100, 100, 100);
  let x = 0;
  let y = 0;
  let w = width;
  let h = height;
  let depth = 2;
  drawRect(x, y, w, h, depth);
  
 angleMode(DEGREES);
   translate(140, 280);
  
  let xS =200;
  let yS = -200;
  let wS = 200;
  let hS = 200;
  let starta = 90;
  let end = 230;
  let depthS = 8;
  let segments = 6;

  
  scale(1.5);
  rotate(50);

  arc(xS, yS, wS, hS, starta, end);
  arc(xS, yS, wS / 4, hS / 4, starta, end);

  for (let i = 0; i < segments; i++) {
    let ang = map(i, 0, segments, starta, end);
    let px = xS + cos(ang) * (wS / 2);
    let py = yS + sin(ang) * (hS / 2);
    line(xS, yS, px, py);
    let ang1 = map(i, 0, segments, starta, end);
    let ang2 = map(i + 1, 0, segments, starta, end); //angle of the next i so that we can connect when making triangle.
    let outX1 = xS + cos(ang1) * (wS / 2); //points across the arc
    let outY1 = yS + sin(ang1) * (hS / 2);
    let outX2 = xS + cos(ang2) * (wS / 2);
    let outY2 = yS + sin(ang2) * (hS / 2);
    let inX1 = xS + cos(ang1) * (wS / 8);
    let inY1 = yS + sin(ang1) * (hS / 8);
    // Draw the triangle segment
    fill(random(200, 255), 100, 100); // Semi-transparent fill
    sensuRecur(inX1, inY1, outX1, outY1, outX2, outY2, depthS); //taking this first triangle, I will be diving this with recursion
  }
}

function drawRect(x, y, w, h, depth) {
  if (random() < 0.1 || depth > 3) {
    drawRect(x, y, w / 2, h / 2, depth - 1);
    drawRect(x + w / 2, y, w / 2, h / 2, depth - 1);
    drawRect(x, y + h / 2, w / 2, h / 2, depth - 1);
    drawRect(x + w / 2, y + h / 2, w / 2, h / 2, depth - 1);
  } else if (random() < 0.16 || depth > 0) {
    drawRect(x, y, w / 4, h / 4, depth - 1);
    drawRect(x + w / 4, y, w / 4, h / 4, depth - 1);
    drawRect(x, y + h / 4, w / 4, h / 4, depth - 1);
    drawRect(x + w / 2, y + h / 2, w / 2, h / 2, depth - 1);
  } else {
    noFill();
    stroke(255);
    quad(x + w / 2, y, x + w, y + h / 2, x + w / 2, y + h, x, y + h / 2); //square inside the sqaure
    let pointA = { x: (x + w / 2 + (x + w)) / 2, y: (y + (y + h / 2)) / 2 };
    let pointB = { x: (x + w / 2 + x) / 2, y: (y + h / 2 + (y + h)) / 2 };
    let pointC = { x: (x + w / 2 + x) / 2, y: (y + (y + h / 2)) / 2 };
    let pointD = { x: (x + w / 2 + (x + w)) / 2, y: (y + h / 2 + (y + h)) / 2 };
    line(pointA.x, pointA.y, pointB.x, pointB.y); //the two lines inside the inner circle.
    line(pointC.x, pointC.y, pointD.x, pointD.y);
    let centre = { x: (pointA.x + pointB.x) / 2, y: (pointA.y + pointB.y) / 2 };
    let d = dist(centre.x, centre.y, pointA.x, pointA.y); //get the size of the square to plan ellipse size
    fill(255);

    ellipse(centre.x + d / 3, centre.y, d / 2, d / 10); //ellipse shape for the inside
    ellipse(centre.x - d / 3, centre.y, d / 2, d / 10);
    ellipse(centre.x, centre.y + d / 3, d / 10, d / 2);
    ellipse(centre.x, centre.y - d / 3, d / 10, d / 2);

    noFill();
    rect(x, y, w, h); //main square
  }
}
  function sensuRecur(ax, ay, bx, by, cx, cy, depth) {
  if (depth > 0) {
    let mpx = (bx + cx) / 2;
    let mpy = (by + cy) / 2;
    let options = [1, 2, 3];
    if (random(options) == 1) {
      sensuRecur(bx, by, ax, ay, bx, by, depth - 1);
      sensuRecur(bx, by, ax, ay, cx, cy, depth - 1);
    } else if (random(options) == 2) {
      sensuRecur(cx, cy, ax, ay, bx, by, depth - 1);
      sensuRecur(cx, cy, ax, ay, cx, cy, depth - 1);
    } else {
      sensuRecur(mpx, mpy, ax, ay, bx, by, depth - 1);
      sensuRecur(mpx, mpy, ax, ay, cx, cy, depth - 1);
    }
  } else {
    triangle(ax, ay, bx, by, cx, cy);
  }
  
}
```



I also tried Tyler Hobbs' webiste to practice triangles! 

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/0914d9f9-3b5d-4094-ba51-b4c1237209a5" />

```js
function setup() {
  createCanvas(400, 400);
  background(220);
  
  let ax = 0; 
  let ay = 0; 
  let a2x = width;
  let a2y = height;
  let bx = width; 
  let by = 0; 
  let cx = 0; 
  let cy = height;
  let depth = 8;
  splitTriangle(ax, ay, bx, by, cx, cy, depth)
  splitTriangle(a2x, a2y, bx, by, cx, cy, depth)
}

function splitTriangle(ax, ay, bx, by, cx, cy, depth){
  
  if (depth>0){
     let mp = {x: (bx+cx)/2, y: (by + cy)/2};
     splitTriangle(mp.x, mp.y, ax, ay, bx, by,depth-1);
     splitTriangle(mp.x, mp.y, ax, ay, cx, cy, depth-1);
  } else {
    triangle(ax, ay, bx, by, cx, cy);
  }
}
```

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/e6515815-cbf9-4cfa-9202-0342482fa1f0" />

```js
//3 options probability
function setup() {
  createCanvas(400, 400);
  background(220);

  let ax = 0;
  let ay = 0;
  let a2x = width;
  let a2y = height;
  let bx = width;
  let by = 0;
  let cx = 0;
  let cy = height;
  let depth = 8;

  splitTriangle(ax, ay, bx, by, cx, cy, depth);
  splitTriangle(a2x, a2y, bx, by, cx, cy, depth);
}

function splitTriangle(ax, ay, bx, by, cx, cy, depth) {
  let options = [0, 0.5, 1];
  if (depth > 0) {
    let mp = { x: (bx + cx) / 2, y: (by + cy) / 2 };
    if (random(options) == 0) {//when 0 out of 3 options, D = B
     splitTriangle(bx, by, ax, ay, bx, by, depth - 1);
      splitTriangle(bx, by, ax, ay, cx, cy, depth - 1);
    } else if (random(options) == 1) {
     splitTriangle(cx, cy, ax, ay, bx, by, depth - 1);
      splitTriangle(cx, cy, ax, ay, cx, cy, depth - 1);
    } else {
      splitTriangle(mp.x, mp.y, ax, ay, bx, by, depth - 1);
      splitTriangle(mp.x, mp.y, ax, ay, cx, cy, depth - 1);
    }
  } else {
    triangle(ax, ay, bx, by, cx, cy);
  }
}
```
Self balancing  
For this, I compared the longest sides of the triangles and for the longest one, I used the lerp function to place a point.   
When I did it with random(), some triangles became too thin, random(0.4, 0.8) worked the best. 
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/5b423442-83f0-40ec-b38c-09ac5c60d158" />

```js
function splitTriangle(ax, ay, bx, by, cx, cy, depth) {
  let disAB = dist(ax, ay, bx, by);
  let disBC = dist(bx, by, cx, cy);
  let disAC = dist(ax, ay, cx, cy);
  let options = [0, 0.5, 1];
  if (depth > 0) {
    let t = random(0.4, 0.8);
    if (disAC >= disBC && disAC >= disAB) {
      let mp = { x: lerp(cx, ax, t), y: lerp(cy,ay,t) };
         splitTriangle(mp.x,mp.y, bx, by, ax, ay, depth - 1);
      splitTriangle(mp.x,mp.y, bx, by, cx, cy, depth - 1);
      
    }else if (disBC >= disAC && disBC >= disAB) {
      let mp = { x: lerp(cx, bx,t), y: lerp(cy,by,t) };
      splitTriangle(mp.x, mp.y, ax, ay, bx, by, depth - 1);
      splitTriangle(mp.x, mp.y, ax, ay, cx, cy, depth - 1);
    } else { //AB longest
      let mp = { x: lerp(bx, ax, t), y: lerp(by,ay,t) };
      splitTriangle(mp.x, mp.y, cx, cy, bx, by, depth - 1);
      splitTriangle(mp.x, mp.y, cx, cy, ax, ay, depth - 1);
    }
  } else {
    triangle(ax, ay, bx, by, cx, cy);
}
}
```
Non-deterministic base case   
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/fab74c90-e5eb-437a-b6ac-af09b7b6de0e" />

I wasn't sure how to do this but I achieved this by adjusting the following values.
```js
 if (random()<0.5 || depth > 6) {
```
Some cool textures:  
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/263f8d7f-cf37-4e1d-a1f2-2be5b2abb977" />

```js
function setup() {
  createCanvas(400, 400);
  background(0);
  let x = 0;
  let y = 0;
  let w = width;
  let h = height;
  let depth = 10;
  drawRect(x, y, w, h, depth);
}

function drawRect(x, y, w, h, depth) {
  if (depth > 0) {
    let mp = { x: lerp(x, w, random()), y: lerp(y, h, random()) };
    drawRect(x, y, mp.x, h, depth - 1);
    drawRect(mp.x, y, w, h, depth - 1);
  } else {
    rect(x, y, w, h);
  }
}
```
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/52128cf5-53be-4862-8520-4e7ab2bb832f" />

```js
function setup() {
  createCanvas(400, 400);
  background(0);
  let x = 0;
  let y = 0;
  let w = width;
  let h = height;
  let depth = 3;
  drawRect(x, y, w, h, depth);
}

function drawRect(x, y, w, h, depth) {
  if (depth > 0) {
    let mp = { x: w / 2, y: h / 2 };
    drawRect(x, y, x + mp.x, h, depth - 1);
    drawRect(mp.x, y, mp.x, h, depth - 1);
    drawRect(x, y, w, mp.y, depth - 1);
    drawRect(x, y + mp.y, w, mp.y, depth - 1);
  } else {
    noFill();
    stroke(255);
    line(x, y, w, h + y);
    line(x, y + h, w, y);
    rect(x, y, w, h);
  }
}
```
