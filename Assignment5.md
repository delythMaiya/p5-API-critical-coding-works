

## Assignment #5

**READING**  
I really liked the line "When you are vulnerable you can attack. When you are safe, you stay safe", highlighting that we must be prepared for criticisms and feedback and also have our own set of ideas and parameteres of thought when seeing other works so that we can form critical opinions. Having an 'antibody' (works we hate), we actually learn from this or see who we are and what we like even better. I think it sharpens our sense of identity. I have works that I hate, but also works that neither love or hate, a middle-ground. Maybe these are works that doesn't 'cut' through my thought ? If I hate something that means I am passionate to criticise, but it doesn't mean I am immersed in it. I think this only happens when it triggers my values, so it's not actually about the art? 
For example, I don't really like ndy Warhol style art, just purely from the kinds of colour he uses, not because I don't like these artists personally.    
The way Warhol uses multiple saturated colours is so flashy and ugly to me, I only like his banana velvet underground cover and tomato can design. Why do I feel this way?  
However, that's not to say he revolutionalised the way commercial products look and made amazing advertisements. If I were to critique his colours, should I be aware of this commercial background?
In the reading, I totally agree that the new media format works lack the critical gaze, it's all new and traditional critics have to be familiar with this area first, I disagree that people have to understand fully before they criticise. People should also be able to critique from what they see first without any context like Kant says in his Critique of Judgement. This reading was really nice and reminded me of the values of evaluation and reflection, and being able to properly criticise is a skill necessary for artists. Constructing a healthy critical environment is important, and using the appropriate language to my friend when critiquing each other is essential. I think that the fear of 'I'm not educated enough' only applies to politics or medicine or any areas other than aesthetic judgement. Everyone can have an opinion on someone's art. My grandmother with no experience in computer could find Vera Molnar's works pleasing and relaxing or boring and 'anyone can do it' - knowledge doesn't really matter. After watching her interview about her practice, I would still pick her favourite works based on how they look like, not based on process behind it.   

**LEARNING** 
- lerp() linear interporation 
  For easing and smoothing out.  
 ![lerp](https://git.arts.ac.uk/user-attachments/assets/f7f5d5b7-9f65-4176-84bb-a86a18ca92bb)
```js
let target= 300;
let x = 0;
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  x = lerp(x,target, 0.01);
  circle(target, 200, 50, 50);
  circle(x, 200, 50, 50);
  
}

function keyPressed(){
  if (key === 's'){
    saveGif('lerp', 5);
  }
}
```
- sin()
  ![filz](https://git.arts.ac.uk/user-attachments/assets/0736b083-986b-4e40-95a7-a8a0100f6d19)
```js
let angle = -1;
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(0);
  translate(200, 200);
  let r = map(sin(angle), -1, 1, 0, 200);
  circle(0, 0, r);
  angle += 0.1;
}
```  
![filz (1)](https://git.arts.ac.uk/user-attachments/assets/255159b3-1d6a-4bb0-80a5-186fae10f14d)  
```js
let angle = -1;
let angleV = 0;
function setup() {
  createCanvas(400, 400);
  frameRate(30);
}

function draw() {
  background(0);
  translate(200, 200);
  let y = map(sin(angle), -1, 1, -200, 200);
  let r = map(sin(angle), -1, 1, 0, 50); 
  let x = -150;
  for (i = 0; i<5; i++){
   circle(x + 75*i, y + i*random(-40, 40), r);
  stroke(255);
  line(x + 75*i, 0, x + 75*i, y);
  }
   angle += angleV;
   angleV += random(0.001, 0.05);
   if (angleV > 0.5){
    angle = -1;
    angleV = 0;
  }
}
```
- perlin noise() - range metween 0 and 1, non-uniform distribution, unless refreshed noise() will always return same value.   
  Unlike random() values, it is smoothed out. It is based on previous values, random walk. Use offset value to randomise further.
  method1:
 ```js                                                                                                                ![perlin](https://git.arts.ac.uk/user-attachments/assets/9ed8efec-4998-4b5b-9e78-55a0902aae89)

  var offset1 = 0;
var offset2 = 10000;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  var x = map(noise(offset1), 0, 1, 0, width);
  var y = map(noise(offset2), 0, 1, 0, height);
  
  offset1 += 0.02;
  offset2 += 0.02;
  
  ellipse(x, y, 24, 24);
}
```

![image](https://git.arts.ac.uk/user-attachments/assets/70219d26-cd55-4b03-9642-6f95bcbe3e99)  
beginShape() endShape() - create custom shapes using verticies. noLoop() - prevent looping in draw()  
```js

function draw() {
  background(100);
   beginShape();
  noFill();
   for (x = 0; x<400;x++){
     stroke(255);
     vertex(x, random(200));
   }
  endShape();
  noLoop();
}
```
  ![perlin (1)](https://git.arts.ac.uk/user-attachments/assets/94353ab9-e514-48d8-940a-811129351055)  
```js
var inc = 0.01;
var start = 0;

function setup() {
  createCanvas(400, 400);

}

function draw() {
  background(100);
   beginShape();
  noFill();
 var offset1 = start;
   for (x = 0; x<400;x++){
  
     stroke(255);
     var y = noise(offset1)*height;
     vertex(x, y);
 
     offset1 += inc;
   }
  endShape();
 start += inc
}
```



**CODING**
Step1. In Substrate, the lines grow until it hits another, which then new directions form roughly perpendicular to the intersecting point. The starting points are random.




**REFLECTING**

I really enjoyed getting to know Jared Tarbell's Substrate, and I had looked at the source code and noticed many things that I would love to incorporate in my own work.  
There is a class called 'crack' which stores x,y coordinate and t, the direction it travels, perpendicular to the origin. The random points px and py are plotted as starting points until it meets a crack. I kept looking for line() object, but actually it plots the line of cracks using thousands of points. As the crack advances, black point is drawn, he even has random(-z, z) to give a more organic feel.  
It was also interesting that it had a function to check for open space, or whether the pixel has gone through any cracks. To do this he has an if statement using 10001 for comparion, where angles are I wa0 to 359.  
I was confused first why 10001, but it's just an arbitary number that is way out of the angle's range, just to check whether a pixel has a crack. 
Furthermore, I really like the way he extracted colours from Pollock's picture to store in palette and to use it in this. Texturising to make it look like sand paper is amazing too. 


