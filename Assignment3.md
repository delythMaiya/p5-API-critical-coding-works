

## Assignment #3

**REVIEW**  
From Coding Train and Happy Coding resources, I practiced making these first:   
```js

function draw() {
  background(220);
  
  for (let x = 10; x < 400; x+=10){
    line(x, 0, x, height);
  }
```
![image](https://git.arts.ac.uk/user-attachments/assets/074dcb70-7c90-4334-8711-0c2cb0f8b913)

_"Try thinking about the inner for loop as a single unit, and the outer for loop as a loop that executes that unit multiple times."  _  
Instead of using nested for loop, calling a function to illustrate this point.   
```js
function draw() {
  background(220);
  
  for (let x = 80; x < 350; x+=60){ 
    drawY(x);
  }
}

function drawY(x){
  for (let y = 80; y < 350; y+=60){
    circle(x,  y, 20);
  }
}
```
![image](https://git.arts.ac.uk/user-attachments/assets/64130de7-41dd-454f-ba15-6bee97098198)

And by accident I made this really nice lines. I initially tried to do straight lines going diagonally from bottom left corner to top right corner, but my code created this. 
![image](https://git.arts.ac.uk/user-attachments/assets/be3442ce-558b-489a-8ad1-c257c606eac7)

```js
function setup() { 
  createCanvas(400, 400);
}

function draw() { 
  background(220); 
  
  for (let y =380; y>0; y-=30){
    for (let x = 20; x<400; x+=30){ 
      line(0,y,x,400);
    }
  } 
  for (let x =380; x>0; x-=30){
    for (let y = 20; y<400; y+=30){ 
      line(x,0,400,y);
    }
  } 
}
```



**READING**

I think the underappreciation of software art often comes from a simplified understanding of the practice, particularly from people who have not engaged deeply with the field. This kind of perception is similar to the widespread paranoia that “AI will replace us”. Software art is a broad discipline that deserves even more recognition within the field of contemporary art. I found it interesting that unlike traditional art forms, software art requires the artist to define their creative intent precisely through code. (John F. puts it as "a form of creative writing". Given the same data or the same task, each artist can produce entirely different code for it. 

Regarding the question posed in the text — “Is software art more successful if one can see the algorithm at work?” — I agree with the text that the visibility of the algorithm should not determine the quality or success of the artwork. Revealing the source code might also be considered an artwork in itself, as it exposes the artist’s process and way of thinking. Not every artist writes code in the most efficient way, and these variations in approach can be expressive in their own right. The process of experimenting, revising, and problem-solving through code mirrors the sketches in traditional art. 

Finally, I find it very innovative and fun when software art draws from games and contemporary culture. Context becomes crucial in interpreting such works, and it provides a framework for grasping what the artist intends to communicate. The text states that software art in this field of game reimagination often requires a “different contextual frame,” where the viewer’s familiarity with certain games and technologies becomes essential for deeper appreciation. However, this is not unique to software art and shouldn't be seen as a barrier; many forms of traditional, experimental, and even contemporary classical music also rely on context and explanatory texts to be fully understood. Rather than being a barrier, I believe this contextual engagement brings audiences closer to software art, connecting it to the cultural and technological realities they already inhabit. 

**CODING**

[https://editor.p5js.org/sizalyth/sketches/JrV5Bk5s1]

I decided to randomise the frame rate and link it to the mouseY position. As the mouse moves from the top to the bottom of the canvas, the frame rate gradually decreases, causing the movement of the boxes to slow down. When the mouse reaches the very bottom (below y = 380), the motion stops completely, revealing a neatly arranged grid of blocks. To generate this grid, I used nested for-loops to draw the series of rectangles.


**REFLECTING**

![image](https://git.arts.ac.uk/user-attachments/assets/001ccd47-51e3-4913-8ecf-975970b82c78)

For this reflection, I selected UVA’s work Ensemble, which I saw in person at 180 Studios in London a few years ago. The piece, with a runtime of around eight minutes, explores the relationship between human bodily movement and rhythm or music. What I found most striking was how it portrayed humanity across different eras — from the physical gestures of hunting and gathering to the mechanical repetitions of agricultural labour, and finally to the subtle, almost digital movements of the modern age. For example, for the agricultural era, the dancer multiplied across the screen, performs motions reminiscent of farming, creating a visual rhythm that also links to the music.

I relate this work to the concept of order and chaos. The dancers’ movements are algorithmically mapped to the audio, influencing the rhythm of the music in a way that introduces unpredictability while still maintaining an underlying structure. I imagine that UVA programmed parameters that allow variation within a controlled range. Visually, the dancers’ arrangement in a grid suggests order, yet the flickering overlays, shifting tones, and sudden singular frames of a lone dancer introduce chaos. Together, these visual and sonic layers form a dynamic horizontal timeline — a continuous movement between organisation and disorder that mirrors the evolving rhythm of human existence itself.
