<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f5fc9776-a42e-4e2c-aa7f-38227648f61e" />

## _Six Steps From Me_  
_Delyth Field_   


**PROJECT DESCRIPTION**

I wanted to reflect on Vera Molnar's "Interruptions” series (1960s–1970s).   
Molnar introduces 'small error' to the ordered system which disrupts it gradually, with lines shifting, breaking or reconnecitng. 
I wanted to relate this to the idea, [Six Degrees of Separation](https://en.wikipedia.org/wiki/Six_degrees_of_separation), where a person is six or fewer social connections away from any other person in the world.   
This level of interconnectedness also means that a disruption, chaos and positive/negative influence can easily spread through human society starting from one single node. 
Some nodes are bigger than others with thicker lines, symbolizing influential figures. As you hover over, the nodes change to red.   
The number of connections (lines) a node has is randomised, just like how some people will have a large number of close ties whereas others smaller.   

My intention was to make the colour change red gradual across lines too, like an infectious spread, but even after many hours I couldn't work it out how to do it (yet). 

**CODE**  
Work: https://editor.p5js.org/sizalyth/full/BHTTFzesl   
Source Code : https://editor.p5js.org/sizalyth/sketches/BHTTFzesl   

**Changes**
In my concept, I talked of how any two nodes can be connected by six steps. Few days later, I thought that if this is the case, having += 1 for connections until it reaches 6 is not really accurate way. In the real world, some people have more connections than others. If someone has 17 close connections whereas someone has 3 close connections, my work of having six lines maximum each node is not really what I wanted to represent. I need to randomise the connection value, bigger nodes having bigger connections and smaller ones less. What I need to ensure is that any two node can be connected by six steps. Realising this flaw, I made adjustments to the connection values. I changed it to random(2, 12), and this makes the maximum value of connections allowed inconsistent and unpredictable each time, which for now works to vary the values of each node's connections. 
For bigger nodes, I made the strokeWeight greater to highlight more power.  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6affda35-e5d8-403d-80e7-ccf87c60e663" />

```js
 if (k>= 800){
      strokeWeight(2);
      line(nodes[startP].x, nodes[startP].y, nodes[endP].x, nodes[endP].y);
    }else{
       stroke(255, random(20, 150));
      strokeWeight(0.3);
      line(nodes[startP].x, nodes[startP].y, nodes[endP].x, nodes[endP].y);
    }
```

**My Process**

<img width="1133" height="1600" alt="image" src="https://github.com/user-attachments/assets/77d306a5-a6e5-411c-9e79-611327c3a05d" />

I began by experimenting with nodes to decide whether I prefer the nodes to be in the setup with lines emerging gradually or nodes emerge immediately.  
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/7c3d732e-15e3-4c6c-8fac-665fc862b35e" />    

```js                                                              

function setup() {
  createCanvas(400, 400);
  frameRate(2);
  background(100);
}

function draw() {
  
  strokeWeight(0);
  circle(random(400), random(400), random(5, 10));
}
```
The other version where nodes are all written out when we run the code:   
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/5e14d8a0-0a0d-46ad-a26c-d6900efae663" />   

```js                                                             
function setup() {
  createCanvas(400, 400);
  frameRate(2);
  background(100);
  strokeWeight(0);
  
  let nodes = [];
  
  for (i=0; i<600;i++){
   nodes[i] = circle(random(400), random(400), random(5, 10));
  }
  
}
```
I decided to make the nodes emerge from setup straightaway otherwise if I try to draw line(x, y with circle x, y), all the nodes must have another pairing six nodes, and human networks are not like that. Close, neibouring people doesn't mean you have strong ties with them.  
To make the line() connect one circle's xy to connect to another xy, I have to store them in array.   
Also, to represent the idea of powerful people, influential connectors (hubs), I created a separate for loop.   
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d682a3e7-ea78-4df4-ad8c-bff4af844147" />

```js                                                                          
et nodes = [];
  
  for (i=0; i<8000;i++){
   nodes[i] = circle(random(1920), random(1080), random(2, 6));
  }
  for (j = 0; j<20; j++){
    nodes[j] = circle(random(1920), random(1080), random(20,40));
  }
}

```
Then I realised while looking back at the notes, that I was storing nothing when I simply assigned nodes[i] = circle, and when I wanted to retrieve xy data afterward, since the xy values are not separated and stored I had to fix.   
```js
 for (let i = 0; i < 8000; i++) {
   let x;
   let y;
   let r;
  nodes.push({
    x: random(1920),
    y: random(1080),
    r: random(2, 6) 
  });
   circle(nodes[i].x, nodes[i].y, nodes[i].r);
}
  
for (j = 0; j<20; j++){

  nodes.push({
    x: random(1920),
    y: random(1080),
    r: random(20, 40), 
  });
   circle(nodes[j].x, nodes[j].y, nodes[j].r);
  }
```
I encountered another problem as I thought using different index of j would create a separate storage within nodes[], but they are all pushed into the same array and j=0 to 19 overlaps with i = 0 to 7999, hence why I couldn't see any big circles.    
I changed the j index to start from 8000.   
Before I start to think about limit of six connections and relationship of hubs, I wanted to focus on making the lines emerge that are connecting to another existing node.    
![image](https://git.arts.ac.uk/user-attachments/assets/711f8eaf-914f-4075-9506-ae230962c88c)    
In my first attempt to draw lines, it got covered in white in 2 seconds and couldn't see the nodes. 
```js
function setup() {
  createCanvas(1920, 1080);
  frameRate(2);
  background(0);
  strokeWeight(1);

 for (let i = 0; i < 8000; i++) {
   let x;
   let y;
   let r;
  nodes.push({
    x: random(1920),
    y: random(1080),
    r: random(2, 6) 
  });
   circle(nodes[i].x, nodes[i].y, nodes[i].r);
}
  
for (j = 8000; j<8020; j++){

  nodes.push({
    x: random(1920),
    y: random(1080),
    r: random(20, 40), 
  });
   circle(nodes[j].x, nodes[j].y, nodes[j].r);
  }
  
}


function draw() {
  
    
  for (k = 0; k<nodes.length; k++){
   let startP = floor(random(nodes.length)); //floor so that it doesnt return non integer
   let endP = floor(random(nodes.length));
    stroke(255);
    line(nodes[startP].x, nodes[startP].y, nodes[endP].x, nodes[endP].y);
    
  }
    
} 
```
Returning to my original concept, I have to make sure that each node is only connected to 6 including the big ones, which means I have to have a counter to store the number of connections it had made.  
I declared connections as global variable and moved xyr in the set up to global too. In the setup, I initialised connections to 0, and when drawing the lines, I incremented the value in each iteration. If the start and end node ends up being exactly the same after random(), or the number of connections is greater than 6, I made it skip to the next iteration. 
```js
function draw() {
  for (k = 0; k < nodes.length; k++) {
    let startP = floor(random(nodes.length)); //floor so that it doesnt return non integer
    let endP = floor(random(nodes.length));
    if (startP === endP) continue;
    if (nodes[startP].connections >= 6) continue;
    if (nodes[endP].connections >= 6) continue;
    stroke(255);
    line(nodes[startP].x, nodes[startP].y, nodes[endP].x, nodes[endP].y);
    
  }
}
```
It was still quite white, so I decided to randomise the transparancy of the line too.
To add interaction, I tried to change the colour of nodes and lines to red when hovered over, but it applied to the whole group.  
```js
  for (let c = 0; c < nodes.length; c++) {
    let node = nodes[c];
    let d = dist(mouseX, mouseY, node.x, node.y);
    if (d < node.r) {
      fill(255,0, 0); // turn red
    }
    circle(node.x, node.y, node.r);
  }
```
![image](https://git.arts.ac.uk/user-attachments/assets/4928f8a6-7e09-481f-af7f-a9347946995f)  
For the process of pinpointing the exact node, I asked ChatGPT to help me. "how can i pinpoint and extract specific node from the array that mouse hovers over?" (with copy paste of code)  
But actually, what I didn't do correctly was when I was creating fill() I should've used node.colour to make colour specific nodes, as it already is within the for loop and the position is stored in node.   
Now it worked: 
![image](https://git.arts.ac.uk/user-attachments/assets/63861053-f6a7-499b-adeb-c085f2ab7c54)  
Now, I wanted to turn the colours of the line red like an infectious spread, and I thought that the lerp() function that was covered in class could be useful.   
The part was the most difficult part and I strugggled for two days, so I am going to leave it here for the submission and continue trying to do it over the holidays.  

**CITATIONS/REFERENCES**  
- Vera Molnar's idea behind her work [_Interruptions_](https://visualalchemist.in/2024/09/15/artist-profile-vera-molnar/).
  Molnar introduces small 'errors' into the work and these deviations then begin to propel and create difference in the work. I wanted to reflect on this by having the colour red propagating through the nodes as user hovers over the node, just like in real life where if a well connected airport is delayed, so many other airports are affected.
- This video by [Veritasium](https://youtu.be/CYlon2tvywA?si=xmihEIm3O4E-fWQT) was very inspiring and it was my starting point of trying to incorporate this idea into my work. After watching this video, I was impressed with how well they visualised data and I wanted to create my own through p5. Below are screenshots from that video of the data visualisation that they did.
![image](https://git.arts.ac.uk/user-attachments/assets/24e2e1d4-3777-4748-80c3-bb9b8e6f6039)
![image](https://git.arts.ac.uk/user-attachments/assets/92559268-2796-48f3-8feb-a539467911ea)
- I used p5 reference multiple times such as fill(r,g, b, alpha) to reveiw the parameters. 

**LLM Use**   
_"why is the colour not changing at all even when mouse hovered over"_ (with pasted code)    
I had set the colour like this, but then I was not drawing a new circle, so I added circle(x, y,z) to be updated with the new colour. 
```js
if (d < node.r) {
  node.colour = [255, 0, 0]; // turn red
}
``` 
_"how can i pinpoint and extract a specific node and just turn that colour red instead of turning every node red?"_   
solution that LLM gave me was quite complicated and not what I needed anyway, and I managed to figure it out by using node.colour instead of using fill() and applying to everything.    

I tried to use it again when working out how to colour the lines gradually but it was very complicated at the moment for me to want to use it in my work so I will be going through step by step to make sure I understand so that I can do it myself. 







