
**CODING**  
For this assignment, I decided to use three tiles to transform - two are p5js sketches of QR code and a barcode, the other one is a picture of a barcode, and fragments of the picture (mini tiles) are sprinkeld within this picture. 
Generated images look like this: 
  https://editor.p5js.org/sizalyth/sketches/NZxY9ndQphttps://editor.p5js.org/sizalyth/sketches/NZxY9ndQp
![image](https://git.arts.ac.uk/user-attachments/assets/e8bdae7c-6105-452c-9f40-3977c0f7c4eb)   ![image](https://git.arts.ac.uk/user-attachments/assets/0cbbbe21-cadb-4345-bd83-6f1d46bc1aa8)
![image](https://git.arts.ac.uk/user-attachments/assets/c3097f08-06fb-4e4e-b5e7-076ebcbee146)   ![image](https://git.arts.ac.uk/user-attachments/assets/6beba94e-df5f-4ebc-bb81-1c696d4686db)

QR Code Sketch:  
https://editor.p5js.org/sizalyth/sketches/Bt5IaZATz 
![image](https://git.arts.ac.uk/user-attachments/assets/b7c77170-4359-48b1-b89e-09239c794094)
Barcode Sketch (with random numbers generated each time)   
https://editor.p5js.org/sizalyth/sketches/wnbNuK5ct
![image](https://git.arts.ac.uk/user-attachments/assets/883ad313-4a4b-4495-90a1-bcee9c7b0db2)    
fragments of picture tiles:   
https://editor.p5js.org/sizalyth/sketches/EeFZ6wpqC  
![image](https://git.arts.ac.uk/user-attachments/assets/ae47a191-83f0-4113-b43a-178e7c1b34ff)

```js (QR Code)
let grids = [];
function setup() {
  createCanvas(400, 400);
  background(255);
  let x = 30;
  let y = 30;
  let s = 100;
  noFill();
  strokeWeight(15);
  rect(x, y, s);
  fill(0);
  rect(x * 2, y * 2, s * 0.4);
  let bx, by;
  do {
    bx = random(20, width - 50);
    by = random(20, height - 50);
  } while (bx > x && bx < x + s && by > y && by < y + s);
  let depth = 90;
  blobs(bx, by, depth, x, y, s);
}

function blobs(bx, by, depth, x, y, s) {
  if (depth == 0) {
    return;
  }

  let w = random(80);
  let h = random(80);
  bx = random(20, width - 30);
  by = random(20, height - 30);

  if (bx < x + s + 30 && by < y + s + 30) {
    blobs(bx, by, depth, x, y, s);
    return;
  }

  let overlaps = false;
  for (let i = 0; i < grids.length; i++) {
    if (
      bx < grids[i].x + grids[i].w &&
      bx + w > grids[i].x &&
      by < grids[i].y + grids[i].h &&
      by + h > grids[i].y
    ) {
      overlaps = true;
      break;
    }
  }

  if (overlaps) {
    blobs(bx, by, depth, x, y, s);
  } else {
    grids.push({ x: bx, y: by, w: w, h: h });
    noStroke();
    fill(0, 0, 0, random(130, 255));
    rect(bx, by, w, h);
    blobs(bx, by, depth - 1, x, y, s);
  }
}
```

```js (Barcode, but from corner, p5js sketch)
function setup() {
  createCanvas(400, 400);
  background(255);
   angleMode(DEGREES);

  for (let i = 0; i < 32; i++) {
    let v1 = map(i, 0, 16, 0, height);
    //console.log(v1);
    let v2 = map(i, 16, 32, 0, width);
    strokeWeight(random(4));
    line(width, 0, 0, v1);
    strokeWeight(random(3.5));
    line(width, 0, v2, height);
  }

  let nums = [];
  let ang = atan2(125,  width);
 
  console.log(ang);
  for (let i = 0; i < 8; i++) {
    nums.push(int(random(9)));
  }
  textSize(30);
  push();
  translate(20, 35);
  rotate(-ang);
  text(nums.join("  "), 10, 80);
  pop();
}

```

![image](https://git.arts.ac.uk/user-attachments/assets/32000f3d-019d-4e5e-8259-3c6810edb9b1)  
![image](https://git.arts.ac.uk/user-attachments/assets/fc3c318a-a2c3-4fa4-85c0-198e0e812e42)
```js
let img;
let img2;
let fragments = [];

function preload() {
  img = loadImage("Barcode.jpeg");
  img2 = loadImage("QRcode.jpeg");
}

function setup() {
  createCanvas(600, 600);
  background(50);
  
  loadPixels();
  let w;
  let h;
  let x;
  let y;

 
  for(i = 0; i<300; i++){
     w = random(2, 8);
  h = random(2, 8);
  x = random(img2.width);
  y = random(img2.height);
     let fragment = img2.get(x, y, w, h);
  fragments.push(fragment);
  }
 display();
}

function display(){
  let posX = 10;
  let posY = 50;
  for (i=0; i<fragments.length; i++){
    image(fragments[i], posX,posY)
    posX += 20
    if (posX >= width-20){
      posY = posY + 50;
      posX = 10;
    }
  }
}
```
I just don't understand why with scale(), some of the lines are still protruding. I tried asking AI but nothing worked to solve this issue.  
I'm trying to make the whole art half the size and be able to translate it, but some of the lines are not moving at all with it. 
![image](https://git.arts.ac.uk/user-attachments/assets/52236f82-8e54-41e3-af1f-e756c50bd410)

```js 
function setup() {
  createCanvas(400, 400);
  background(255);
  angleMode(DEGREES);

  scale(0.5);

  for (let i = 0; i < 32; i++) {
    let v1 = map(i, 0, 16, 0, height);
    let v2 = map(i, 16, 32, 0, width);

    strokeWeight(random(4));
    line(width, 0, 0, v1);

    strokeWeight(random(3.5));
    line(width, 0, v2, height);
  }

  let nums = [];
  let ang = atan2(125, width);

  console.log(ang);
  for (let i = 0; i < 8; i++) {
    nums.push(int(random(9)));
  }
  textSize(30);
  push();
  translate(20, 35);
  rotate(-ang);
  text(nums.join("  "), 10, 80);
  pop();
}
```
To initially make this shape, using one tile, I individually plotted the translate() and rotate() to figure out the pattern to make a for loop.   
![image](https://git.arts.ac.uk/user-attachments/assets/204e76d5-46c3-483c-bf03-48ae9248e0a3)

```js
function setup() {
  createCanvas(400, 400);
  background(255);
  angleMode(DEGREES);

  push();
  translate(50, 200)
  scale(0.35)
  skewedBarcode();
  translate(400, -400);
  rotate(90)
  skewedBarcode();
  translate(400, -400)
  rotate(90)
  skewedBarcode();
  translate(400, -400)
  rotate(90)
  skewedBarcode()
  pop();
}
``` 
