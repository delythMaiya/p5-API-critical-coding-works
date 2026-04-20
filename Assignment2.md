
## Assignment #2
**REVIEW**  
From this week and Coding Train videos, I understood the use of for and while loops in p5, and where they are suited to use.   
* draw() - they are like flipping pages in a book and refreshes with the rate you set as frame rate.
* By setting var offset = 0; and using this offset value with x coordinate (x + offset) and incrementing it each line (x = x +50), you can create a sequence of shapes. Rather than writing a line for every repetition, while loop can do this until the x meets its maximum. For loops makes this even more concise by having the conditions and incremental value and initial value all in one line. 
* Nested loop - for every x, for every y, two dimensional
* mouseIsPressed - event that is already defined within p5, so I can use it in if statements 'if (mouseIsPressed){}] or call it as function.
* var or let? - var can be used anywhere in the code but let can only be used in one block.
* && - for when you have multiple conditions to meet in an if statement.

Exercise i & ii  
i : As x is increasing, starting position of y is increasing, and there were 19 circles in the image with no gaps between and slight space on very left and right of the canvas next to the circles, so I assumed the diameter would be 20 pixels (380/19 = 20). 
![image](https://git.arts.ac.uk/user-attachments/assets/9fe3341b-6695-43f9-b17f-d932788cb778)

```js
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  var diameter = 20;
  var cols = 18;
  var rows = 18;
  
  for(let row = 0; row <= rows; row++){
    for(let col = cols - row; col>=0; col--){
      circle((20 + row*diameter),380-(col*diameter), 20);
    }
  }
}
```
ii: Highlighting the colour when mouse hovers over. 
```js
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
   noFill();
  var diameter = 20;
  var cols = 18;
  var rows = 18;
   if (mouseX >= 20 && mouseX <= 380 && mouseY >= 20 && mouseY <= 380){
    fill(100);
  } 
  for(let row = 0; row <= rows; row++){
    for(let col = cols - row; col>=0; col--){
      circle((20 + row*diameter),380-(col*diameter), 20);
    }
  }
 
}
```
This ended up colouring the whole set of circles when hovered over, even the blank space. 
![image](https://git.arts.ac.uk/user-attachments/assets/95aaa6ea-c79a-4b9b-9753-d17da47e5f9e)
After, this I created a condition where if the distance of mouse X and Y is less than diameter/2 from centre XY of the circle, it fills the circle. 
```js
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
   noFill();
  var diameter = 20;
  var cols = 18;
  var rows = 18;
  
  for(let row = 0; row <= rows; row++){
    for(let col = cols - row; col>=0; col--){
      if (dist(mouseX, mouseY,(20 + row*diameter) , 380-(col*diameter)) < diameter / 2) {
        fill(100);
      } else {
        fill(255);
      }
      circle((20 + row*diameter),380-(col*diameter), 20);
    }
  }
 
}
```


**REFLECTING**
Critical Consious Computing - Amy J. Ko   
It was fascinating to learn that Plato once said that the act of writing will "implant forgetfulness in their souls". Technological development always has consequences, even if we think of them as being neutral.   
This reminded me also of a video I watched in my physical computing module where the invention of an easy to open can openers (aluminium peg) caused pollution across the country because the peg was dettached after opening - something the inventor didn't see it coming.   
Then, the design was altered so the peg remains on the can after opening. I agree with the text that the technology is not just a binary code. It amplifies societal problems and doesn't address inequality.   
Just like the can, we have to take measures to adjust this ineqaulity and problems once we realise, or ideally before they start to excacerbate. Webforms and technology dealing with identification of people have to take into account our diversity, and for this to happen, developers of these softwares have to be consioucs of what they are writing and evaluate many times. When necessary, more human intervention is needed. However, humans also don't have a perfect set of value. Someone who is racist can take away an opportunity unlike a computer system which will judge without any discrimation as long as it fits a pre-determined criteria. The process of automation has helped productivity but are we using it in the right way? Data set does not have a holistic sense of view, and the part of the reading where it talked about medication and health insurannce being declined due to inncome inequality was astonishing.   
I really liked the way author wrote about how instead of systems being used to police travellers and monitor, why not instead implement softwares that can tackle the root causes of terrorism, such as facilliating dialog, diplomacy and creatng a support system across different cultures and backgrounds. 


**CODING**  
I decided to do the talk B, infinite loop. 
https://editor.p5js.org/sizalyth/sketches/kInKdORcG 
For this assignment, I followed this Youtube Video for inspiration and learning as it was close to what I wanted to crete and I didn't know where to start from.  
https://youtu.be/MpDUW_bvihE
My takeaways from this coding task: 
- Use sin or cosin functions to create oscillating movements.
- vector function and use of direction and magnitude, vector.sub to subtract between two vector points.
- Use of class and 'this.' on properties, creating of sub-files.

![myGif](https://git.arts.ac.uk/user-attachments/assets/f59d9d31-beac-4d26-9707-5cd30b93303b)

This was above my skill level, so I also made this for an infinite loop task. 
 I tried to make a Ryoji Ikeda style art. I used random() function for rectangles that are flickering, and a loop for the ellipse.   

![myGIF (1)](https://git.arts.ac.uk/user-attachments/assets/495dfb45-f133-4ac5-aa82-4046b7919f5e)
 

