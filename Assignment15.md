## Assignment #15

**READING**

***CODING***     
Gamma Ray Bursts in the Universe   
Gamma Ray Bursts (GRBs) are the most powerful explosions in the universe. If direted at Earth close enough, it will cause mass extinction. In 2022, a blast that happened 1.9 billion light years away still caused disturbances in the Earth's atmosphere. Also, 440 million years ago, a GRB close enough to Earth wiped out 85% of the species on the planet as well as another disturbance recorded from the 8th century.    
I downloaded the .csv file of the recorded GRBs from monitoring stations on Earth from NASA. There has been 147 explosions from last September when we started the course until now.   
The data is mapped to the flash on the screen, and duration of its exxplosion is relative to how fast the timelapse of this sketch is, so some of them lasted even 2 minutes. The whiter the flash, the greater intensity.   
Sketch Link: https://editor.p5js.org/sizalyth/sketches/OwBZbadS1


Before attempting flashes, I started with mapping each explosion according to its celestial latitude and longitude, to visualise all of them. 

![image](https://git.arts.ac.uk/user-attachments/assets/ee0b86d0-e528-4790-9e9b-ca08539d4e0e)

My starting point was when I revisited Richard Feynman's writings for physics for inspirations and I thought this was beautiful:   
_"..A vast pattern—of which I am a part—perhaps my stuff was belched from some forgotten star"_, in other words, heavy elements in our bodies such as carbon, nitrogen and oxygen came from dead stars (nucleosynthesis). They cosmic rays scatter across the planet. Every element heavier than hydrogen was forged in the cores of the stars that died billions of years ago. I didn't really think of this relationship between stars and us until now, so I was inspired.   
Cosmic rays from the universe including GRBs contribute towards the creation of heavy elements on the planet, so they are essential to our beings. 

**1. Finding the right data source.**
I used NASA's data for gamma ray bursts (GRB), the date is speicified from start of our course, September to now. <a href="https://heasarc.gsfc.nasa.gov/cgi-bin/W3Browse/w3table.pl?MissionHelp=gamma-ray_bursts">GRB Data</a>. 

![image](https://git.arts.ac.uk/user-attachments/assets/d34fc34d-d949-4e98-b7be-4406fb16fe30)
![image](https://git.arts.ac.uk/user-attachments/assets/47e9536e-9317-440c-8ac2-89b9f8759a20)
I got to know Modified Julian Date, a scientific way to represent the days like '604560' instead of 'March 3rd' for example.    

**2. Visualising them simply with latitude and longitude, loading csv data** 
![image](https://git.arts.ac.uk/user-attachments/assets/a63551c0-b64e-4846-a50e-b9d779081fa4)

```js
let burstdata;

function preload() {
  burstdata = loadTable("explosions.csv", "csv", "header");
}
function setup() {
  createCanvas(windowWidth, 400);
  background(255);
  let numRows = burstdata.getRowCount();
  print(numRows);
  //https://youtu.be/jCmh_eXwPH0?si=TJgrenoBvq4m9MOh this video helped me to format and use csv files.
  let longitude = burstdata.getColumn("Longitude");
  let latitude = burstdata.getColumn("Latitude");
  let date = burstdata.getColumn("Date"); //max 60928 to 61097
  let duration = burstdata.getColumn("duration"); //max 257 min 0
  let intensity = burstdata.getColumn("intensity"); //min 0.000000032368 max 0.000261

  for (let i = 0; i < numRows; i++) {
    let Xcord = map(longitude[i], 0, 357, 5, width - 5);
    let Ycord = map(latitude[i], -87, 76, height - 5, 5);

    fill(5);
    circle(Xcord, Ycord, 5);
  }
}
```
**3. Timelapse of September to now in 20s duration since running the program**  
![image](https://git.arts.ac.uk/user-attachments/assets/601d081b-8a1b-4f1d-a2dc-3e1ad352bbb2)
I struggled to do this, in Arduino millis() is the function for getting the time since running the code, and so was p5js. It would be easy to do this with map() using Modified Julian Date, but to convert this into English text format of Date, I thoght I should maybe have another set of array containing all the conversions and the program access that with For loop. I ended up struggling with this a lot, with not many tutorials so I used Claude ai to help me (chatlog: https://claude.ai/share/aa1b77fa-d45b-4ab8-85e6-82f4608213c4).   You first subtract the start of the Julian Date (1970) and then multiply by milliseconds in a day, and then use JavaScript function to convert that into a date.   
Apart from the conversion, a mistake I made was calling the function but not using the returned value 
```js
getCalendarDate(date[i]);
```
to   
```js
let formattedDate = getCalendarDate(float(date[i]))
```
Also, my csv file was not sorted properly with time from past to recent, so I reorganised and uploaded the file again.    
```js
 let elapsed = millis() - startTime; //how long the sketch has ran
  let progress = elapsed / SketchDuration
  let Remaining = floor(progress * numRows); //add floor to make it whole number
  console.log(Remaining) 

  for (let i = 0; i < Remaining; i++) {
    let Xcord = map(longitude[i], 0, 357, 5, width - 5);
    let Ycord = map(latitude[i], -87, 76, height - 5, 5);
    fill(5);
    circle(Xcord, Ycord, 5);
  }
```
The 'Remaining' increments by 1, as the time elapses, the number increases and draws the points in the duration of 20s relative to the date the star exploded. 
 
**4. adding other characteristics of the stars**  
I decided to map star explosion duration to the radius of the star, and intensity to the flickering speed.   
It was straightforward to map the radius and baseColour (higher the intensity, darker), but to make the colour flicker from transparent to its fill was tricky. 
```js
 let radius = map(duration[i], 0, 257, 7, 50)
    let baseColour = map(intensity[i], 0.000000032368, 0.000261,100, 255)
    let TremSpeed = map(intensity[i], 0.000000032368, 0.000261, 0, 1);
    
    fill(0, 0, 0, baseColour);
    circle(Xcord, Ycord, radius);
```
I didn't know how to assign this tremspeed variable that I made to the fill changing. It was more complicated than I thought, involving the use of millis() and sin() functions. (link is same LLM chatlog as before)   
![image](https://git.arts.ac.uk/user-attachments/assets/eca487d6-38e9-43c7-824f-d343234943fc)
```js
 let TremSpeed = map(intensity[i], 0.000000032368, 0.000261, 20, 30);
     let pulse = map(sin(millis() * 0.001 * TremSpeed + i), -1, 1, 0.5, 1);
  let opacity = baseColour * pulse; // fades in and out at TremSpeed
    
    fill(0, 0, 0, opacity);
    noStroke();
    circle(Xcord, Ycord, radius);
  }
```
sin() was used for the fade in and out motion of the transparency and this was multiplied by the tremspeed so that each star has its own speed. This was multiplied by baseColour. 

**5. Linking this to the news headlines as a timelapse**   
I tried to use New York Times API to retrieve news data because this was free for past articles, but to use in this project, the data retrivval was too fast and exceeded the maxixmum rate allowed, so I decided to do csv again, especially since I am only working with past dates. I tried Wikipedia but it was very difficult to filter out headlines for each day and my code began to look really messy so I decided not to pursue this for now. 




