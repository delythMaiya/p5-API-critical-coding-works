

## Assignment #6

**READING**

My main takeaways from Kestral Gaian's 'Code is Never Neutral' video are these:   
1. Responsibility of harm caused by software (or anything else) cannot be reduced to one single source/person, and we must think about the chain of process behind each software.
2. The code doesn't just sit in our system, it leaks into our real life - how we behave, how we think.
3. When developers write a code for a software, it's important to evaluate whether a certain demographic is excluded or not, and to speculate the data carefully for bias.
4. Software now makes the decisions - which community's voices are amplified or omitted. (links to amplification in previous reading) 
5. When we write code for hobby, or database or infrastructure, we shape the power dynamics in the world.
6. Give people more options (for example, webforms reducing diversity into limited boxes).

I felt very sorry and frustrated for the workers who were accused of theft in the Post Office Horizon Scandal, and I feel it's unacceptable that Tesla concluded that 51 deaths were "acceptable margins of error". In cases involving users who commit suicide after interacting with ChatGPT, or harm linked to social media, responsibility is far more complex, particularly because these cases often involve mentally vulnerable individuals. By contrast, with Tesla, if the phrase “sole fault of the system” is taken to mean that neither human behaviour nor environmental factors influenced the system’s actions, then there was nothing other people could have done to prevent it.   

I really liked the part of the video where he said ethics in technology is like literacy. I would like to consicously think about these things when I develop things, especially if am going to collect data as part of a project.   

**CODING** 
My final code: 
https://editor.p5js.org/sizalyth/sketches/ICfFSWwwz   
View-Only : https://editor.p5js.org/sizalyth/full/ICfFSWwwz 
<img width="798" alt="Screenshot 2025-12-28 at 17 57 41" src="https://git.arts.ac.uk/user-attachments/assets/0c3bd64b-9a12-45dc-95df-6f095d8aec31" />  

My choice of landscape is a place called Yodoyabashi in Osaka, Japan, which is where I lived until 14.   
![image](https://git.arts.ac.uk/user-attachments/assets/17ae338a-66df-4a39-bcc3-fdb0bf7cbf66)  
- I find the flickering and glowing of lights of the urban buildings beautiful, especially when they're reflected on the river. This place has always been my favourite place to come and ponder while seeing this view of lights illuminating on to the waterline.   
- I could use a set of rectangles to draw buildings and windows, and I could add a controlled random() for colouring the window lights and other urban flickering lights.
- For water, I am going to use this tutorial https://youtu.be/kUexPZMIwuA?si=M_-SFpjczCWPVY1C, and I would love to also have flickering of lights that are mirrored from buildings.
- FOr bridge, I can use triangle shape on both sides.

Background : Stars and night sky, slightly grey.  
Middleground : Buildings, bridge, windows.  
Foreground : Lights flickering. Water flowing. Stars glowing. (dynamic elements).   

Setup: I can use a for loop to construct buildings along the river on both sides. Windows can also fit each of these and sequenced using for loops. 

For the night sky, instead of single colour, I wanted to create a gradient from dark colour to lighter from top to bottom, so I used a for loop with lerpColor() function to achieve this. Using map() to reduce the height of 400 into a value 0 to 1, and each increase in this value leading to new line with a closer colour to blue drawn as it descends. 
```js
 for(let y=0; y<height; y++){
    n = map(y,0,height,0,1);
    let newc = lerpColor(c1,c2,n);
    stroke(newc);
    line(0,y,width, y);
  }
```
Using nested for loops for windows, and single for loop for buildings on both sides, I created this landscape:   
<img width="795" alt="Screenshot 2025-12-27 at 16 25 10" src="https://git.arts.ac.uk/user-attachments/assets/29c2fa5c-2ee0-4f10-95ee-0b25e5ba0ad4" />  
The next step was to create an evolving waterscape between the buildings. I researched the loadPixel() function, and understanding how each index is calculated (x + y*width), multiplying by width for each row of image). Everytime it gets refreshed, the size of the windows differ slightly, along with the heights of the building too.   




**REFLECTING**
The positions of bridges and buildngs have all been a trial and error process, adjusting the values as the canvas updates. I don't know if this was the most efficient way, but I managed to successfully crete an impression of the night city with buildings changing every time when it refreshes.   
I couldn't get around to creating an evolving sense of the flowing water between the bridges.  
I also wanted to create the windows to glow with light, change colour from yellow to white, but the project page became very glitchy and difficult to use, and seemed like the processing power of the p5 page was not enough. I couldn't work on it further, I would like to learn more about code optimisation for this reason. 

