**Working with data and API**   

Tutorial playlist #1 <a href="https://www.youtube.com/playlist?list=PLRqwX-V7Uu6YxDKpFzf_2D84p0cyk4T7X"> Coding Train </a>  
Fetch() <a href= "https://www.youtube.com/watch?v=cuEtnrL9-H0"> Web Dev Simplified </a> 
Blobs <a href= "https://youtu.be/T0jmr8m-M9Y?si=UGdUj-HVYhkkiDX8"> Azul Coding </a> 
Reference <a href="https://developer.mozilla.org/en-US/docs/Web/API/Response/Response"> Web API references </a> 
EventSource <a href="https://developer.mozilla.org/en-US/docs/Web/API/EventSource"> EventSource </a> 
JSON Parse <a href="https://www.w3schools.com/js/js_json_parse.asp"> JSON Parse </a> 

<ul> id in <img> is identifier tag </ul>
<ul> 'blob' is a file like object of raw data, binary, hold data more efficiently </ul>
<ul> Inside response() there can be two objects, body (blob, arraybuffer, formdata etc) and options. response.blob() converts data into blob. </ul>
<ul> 'promise' is used for handling pending events, representing that event. </ul>
<ul> The fetch() has to be in its own script tag to work. </ul>

```html  
   <script>
   fetch('https://newsdata.io/api/1/latest?apikey=pub_3cf33aee2b304c5aab3429b494bc92c9')
        .then(response => response.json())  
        .then(data => console.log(data))   
    </script>
```
res.json() analysing the string of data (the type of data), and .then(data => gets the actual data. 
<ul> 'DOM' (Document Object Model) represents web pages as nodes and objects, like body, script img tags. </ul>

```html  
 <body>
    <img src = "" id = "music"/>
    <script>
          fetch('score.png').then(response1 => {
        console.log(response1)
        return response1.blob()})
        .then(blob => {console.log(blob); document.getElementById('music').src = URL.createObjectURL(blob)})
    </script>
    <main>
```
This displays the image uploaded onto p5js when the image doesn't have link in 'src'. It assigns URL for it.   

For handling erros, .catch can be used.  But async function makes it even simpler.

```html
  .catch(error  => 
        console.log(error));
```
All of the above code is now reduced to this with async function. 
```html
  <img src="" id="music" width="400" />
    <script>
       CatchScore();
      async function CatchScore(){
        const response = await fetch('score.png');
        const blob = await response.blob();
        document.getElementById('music').src = URL.createObjectURL(blob);
      }
```

**Working with HTML**    

<ul> createP creates paragraph, h1.position adjusts the position of the element. </ul>
<ul> createElement('h1', 'waiting') name of the tag, and 'waiting' is the default value. h1.html('hello') later can overwrite that content, for exampled when mouse click happens.
Texts to manipulate, keep them in javascript, texts that are stable, move to index.html </ul>  
<ul> Event Callbacks </ul>
By using id, we can create variable. 

```html
 <textarea id="textfield"></textarea>
 <p id="output"></p>
<button id="submit">submit</button>
```
and in p5, it can look like this to link them.  
```js
 output = select("#output");
  submit = select("#submit");
```
loadJSON() - creates an object from JSON file. first argument is path, second is destination of success, third is failed.   
EventSource() - handles receiving server-sent events from URL.   
.onmessage - executes a funciton when message/data is received. 
JSON.parse - converts JSON data into an object 
```js
 const stream = new EventSource('https://stream.wikimedia.org/v2/stream/recentchange');
 stream.onmessage = (event) => {
 const data = JSON.parse(event.data);
```

**Interaction**   
<ul> creating a simple button to change background colour</ul> 

```js
var colour; 
var button;

function setup() {
  createCanvas(400, 400);
  colour = color(200);
  button = createButton("click");
  button.mousePressed(ChangeColour);
}

function ChangeColour(){
  colour = color(random(50));
}

function draw() {
  background(colour);
}
```
<ul> input text and display. name.changed, name.input (everytime new input is entered), name.value()</ul>

```js
var word; 

function setup() {
 noCanvas()
  word = createInput();
  word.changed(newText);//whenever the input changed, when user types
}

function newText(){
  console.log(word.value());
  createP(word.value());
}
```


**Wikipedia API practice**   
I discovered that without 'jsonp', CORS (cross origin resource sharing) is blocked because browsers have a built in security rule of responses can only be read from same origin.   
To bypass this, jsonp injects script tags (instead of fetch that servers block). However, with Wikipedia, this is not necessary and can be replaced wuth &origin=* because Wikipedia chooses to trust these access. 

```js
function goWiki() {
  let term = userInput.value();
  let url = searchURL + term;
  loadJSON(url, gotData, 'jsonp');
  console.log(url);
}

function gotData(data){
  console.log(data);
}
```
now it shows the search hits! 
![image](https://git.arts.ac.uk/user-attachments/assets/e64d25cd-1ad3-4cf8-b442-06dc68809348)  
Based on the data structure returned on my result, this worked to retrieve a random title from the search result: 
```js
function gotData(data){
  console.log(data);
  let len = data.query.search.length;
  let index = floor(random(len));
  console.log(data.query.search[index].title);
}
```
split(/\s+/) = any white space found, 
```js
 theme = theme.replace(/\s+/, '_');
```
this replaces the white space with _, the format that Wiki uses for spaces in URL.   
![image](https://git.arts.ac.uk/user-attachments/assets/acce4e85-4c2b-4e1d-8a98-bdfb62257973)  
But it only does that for the first space, so I have to make it global by   
```js
  theme = theme.replace(/\s+/g, '_');
```
However, while working on this,especially after discovering Faucoult's "Order of Things" and "Archeology of Things" which Hunter suggested, I thought that it might be better idea to display the names of categories that the word belongs to, rather than the most appearing words. This whill show the taxonomy the word belongs to and how people decided to group it with.   
The format of the API for retriving the category data was   
"https://en.wikipedia.org/w/api.php?action=query&prop=categories&titles=Music&format=json&cllimit=max", where you can replace the word 'Music' here with the title you wish to see.    
Initially, the JSON file was filled with "contains Spanish, contains Japnese, contains German" or "failed verification" etc, a maintenance data of the page which I did not want, not necessarily order of knowledge. To filter out the maintenance categories of the Wiki page, I found that adding the 'clshow: "!hidden"' worked to hide maintenance tags. (same API reference page)   
It would be really nice to compare the result wit the "First Link" phenomenon of Wikipidia page, where clicking the first appearing link takes you eventually to Philosophy page eventually. Doing this with fractal graphics would be very nice.   
<a href="https://www.mediawiki.org/wiki/API:Categories">WIKI API category sample code</a> 
It is good to know that a Wikipedia page cannot have the same title.    

```js
var url = "https://en.wikipedia.org/w/api.php"; 

var params = { //the following items get combined into URL. flexible way. 
    action: "query",
    format: "json",
    prop: "categories", //specifically fetch categories
    titles: "University of the Arts London", //the search title 
    clshow: "!hidden",   // ← only visible categories
};

url = url + "?origin=*"; //to let the brower accept, not block the request 
Object.keys(params).forEach(function(key){url += "&" + key + "=" + params[key];}); 

fetch(url)
    .then(function(response){return response.json();})
    .then(function(response) {
        var pages = response.query.pages;
        for (var p in pages) {
            for (var cat of pages[p].categories) {
                console.log(cat.title);
            }
        }
    })
    .catch(function(error){console.log(error);});
```
This search of UAL returned:   
Category:1986 establishments in England 
Category:Art schools in London   

Now, this code (taken from API reference) can successfully display categories from the Wiki page, and the next step would be to combine this with suggestions pop-up so that the user don't have to know the exact Wiki title, but can select the correct one without having to enter the full title.   


This was my previous code for showing suggestions and displaying the most appearing words :  
```js
let input;
let suggestions = [];
let keywords = [];
let showingSuggestions = true;

const stopWords = new Set([
  'the', 'a', 'an', 'and', 'or', 'but', 'in', 'on', 'at', 'to',
  'for', 'of', 'with', 'by', 'from', 'is', 'was', 'are', 'were',
  'it', 'its', 'this', 'that', 'he', 'she', 'they', 'we', 'as',
  'be', 'has', 'had', 'have', 'not', 'also', 'which', 'who', 'his',
  'her', 'their', 'been', 'into', 'than', 'then', 'when', 'there',
  'after', 'before', 'about', 'would', 'could', 'should', 'will',
  'more', 'most', 'such', 'some', 'over', 'other', 'while', 'from'
]);

function stem(word) {
  if (word.endsWith('ies'))  return word.slice(0, -3) + 'y';
  if (word.endsWith('ves'))  return word.slice(0, -3) + 'f';
  if (word.endsWith('ses'))  return word.slice(0, -2);
  if (word.endsWith('es'))   return word.slice(0, -2);
  if (word.endsWith('ing'))  return word.slice(0, -3);
  if (word.endsWith('ed'))   return word.slice(0, -2);
  if (word.endsWith('ly'))   return word.slice(0, -2);
  if (word.endsWith('s'))    return word.slice(0, -1);
  return word;
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  textFont('Georgia');

  input = createInput('');
  input.position(20, 20);
  input.size(300);
  input.attribute('placeholder', 'Search Wikipedia...');

  input.input(() => {
    let term = input.value();
    keywords = [];
    showingSuggestions = true;
    if (term.length > 2) {
      fetchSuggestions(term);
    } else {
      suggestions = [];
    }
  });
}

function fetchSuggestions(term) {
  fetch(`https://en.wikipedia.org/w/api.php?action=opensearch&search=${encodeURIComponent(term)}&limit=5&format=json&origin=*`)
    .then(r => r.json())
    .then(data => {
      suggestions = data[1].map((title, i) => ({
        title: title,
        description: data[2][i],
        url: data[3][i]
      }));
    });
}

function fetchAnalyse(title) {
  fetch(`https://en.wikipedia.org/w/api.php?action=query&titles=${encodeURIComponent(title)}&prop=extracts&explaintext=true&format=json&origin=*`)
    .then(r => r.json())
    .then(data => {
      let pageId = Object.keys(data.query.pages)[0];
      let text = data.query.pages[pageId].extract;
      keywords = getKeywords(text, 60, title);
      showingSuggestions = false;
      suggestions = [];
    });
}

function getKeywords(text, limit, title) {
  let titleWords = title.toLowerCase()
    .replace(/[^a-z\s]/g, '')
    .split(/\s+/);

  let wordCount = {};
  text.toLowerCase()
    .replace(/[^a-z\s]/g, '')
    .split(/\s+/)
    .forEach(word => {
      let stemmed = stem(word);
      if (stemmed.length > 3 && !stopWords.has(stemmed) && !titleWords.includes(stemmed)) {
        wordCount[stemmed] = (wordCount[stemmed] || 0) + 1;
      }
    });

  return Object.entries(wordCount)
    .sort((a, b) => b[1] - a[1])
    .slice(0, limit)
    .map(([word, count]) => ({
      word,
      count,
      x: random(100, width - 100),
      y: random(100, height - 50)
    }));
} 

function draw() {
  background(255);
  noStroke();

  if (!showingSuggestions && keywords.length > 0) {
    let maxCount = keywords[0].count;

    keywords.forEach(kw => {
      let size = map(kw.count, 0, maxCount, 12, 72);
      let darkness = map(kw.count, 0, maxCount, 200, 0);
      fill(darkness);
      textSize(size);
      textAlign(CENTER);
      text(kw.word, kw.x, kw.y);
    });

    fill(0);
    textSize(12);
    textAlign(LEFT);
    text(`"${input.value()}" — word map`, 20, height - 20);
  }

  if (showingSuggestions) {
    suggestions.forEach((s, i) => {
      let y = 60 + i * 50;
      let isHovered = mouseY > y && mouseY < y + 45 && mouseX > 20 && mouseX < 340;

      fill(isHovered ? color(220) : color(240));
      rect(20, y, 320, 45, 5);

      fill(0);
      textSize(14);
      textAlign(LEFT);
      text(s.title, 30, y + 16);

      fill(80);
      textSize(11);
      text(s.description ? s.description.substring(0, 50) + '...' : '', 30, y + 32);

      cursor(isHovered ? HAND : ARROW);
    });
  }
}

function mousePressed() {
  if (showingSuggestions) {
    suggestions.forEach((s, i) => {
      let y = 60 + i * 50;
      if (mouseY > y && mouseY < y + 45 && mouseX > 20 && mouseX < 340) {
        fetchAnalyse(s.title);
        input.value(s.title);
      }
    });
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```
![Screenshot 2026-03-20 133035](https://git.arts.ac.uk/user-attachments/assets/8b4c8c9e-94b7-4ca5-ba5b-c0dc5f430f4b)
![Screenshot 2026-03-20 133043](https://git.arts.ac.uk/user-attachments/assets/485f9942-02a5-4651-a5c6-692843e41d99)  

The first link was really interesting :      
I copied the code from StackOverflow and this was written in Python, so I convered into JavaScript using Claude AI, and then tweaked from there. 
<a href="https://stackoverflow.com/questions/18916616/get-first-link-of-wikipedia-article-using-wikipedia-api">StackOverflow</a>   
```js

async function getFirstLink(wikipage) {
  const url = `https://en.wikipedia.org/w/api.php?action=parse&page=${encodeURIComponent(wikipage)}&prop=text&format=json&origin=*`;
  const response = await fetch(url);
  const data = await response.json();

  const div = document.createElement('div');
  div.innerHTML = data.parse.text["*"];

  const content = div.querySelector('.mw-parser-output');
  if (!content) return null;

  const blocks = Array.from(content.children).filter(el => {
    return el.tagName === 'P' || el.tagName === 'UL';
  });

  for (let block of blocks) {
    const links = block.querySelectorAll('a');
    for (let link of links) {
      const ref = link.getAttribute('href');
      if (isValid(ref, block, link)) {
        return decodeURIComponent(ref.replace('/wiki/', '').replace(/_/g, ' '));
      }
    }
  }

  return null;
}

function isValid(ref, block, linkEl) {
  if (!ref) return false;
  if (ref.includes('#')) return false;
  if (ref.includes('//')) return false;
  if (!ref.includes('/wiki/')) return false;

  // only block colon in article part e.g. File: Help: Wikipedia:
  const articlePart = ref.replace('/wiki/', '');
  if (articlePart.includes(':')) return false;

  // count open/close parens in text nodes BEFORE this link in the DOM
  let openCount = 0;
  let closeCount = 0;

  const walker = document.createTreeWalker(block, NodeFilter.SHOW_TEXT);
  while (walker.nextNode()) {
    const node = walker.currentNode;
    // stop when we reach text inside the link
    if (linkEl.contains(node)) break;
    // stop if we've passed the link
    if (linkEl.compareDocumentPosition(node) & Node.DOCUMENT_POSITION_FOLLOWING) break;

    openCount  += (node.textContent.match(/\(/g) || []).length;
    closeCount += (node.textContent.match(/\)/g) || []).length;
  }

  if (openCount !== closeCount) return false;
  return true;
}

async function followChain(title, steps = 10) {
  let visited = [];
  let current = title;

  while (steps > 0) {
    if (visited.includes(current)) {
      console.log("Loop detected at:", current);
      break;
    }

    console.log("→", current);
    visited.push(current);

    const next = await getFirstLink(current);
    if (!next) {
      console.log("No valid link found for:", current);
      break;
    }

    current = next;
    steps--;
  }
}

followChain("Hello");
```
Search result "Royal College of Music", so far the argument of everything leading back to philosophy is true. 
![image](https://git.arts.ac.uk/user-attachments/assets/9fc18f73-1c6d-4450-8ed4-8e9ebb88c2f8)  
![image](https://git.arts.ac.uk/user-attachments/assets/3fa625a0-8180-470c-a30f-a50b432faee8)  
Now, I wanted to visulise this with line and nodes graphics, and reminded me of recursive functins and random walks, where lines are generated and the starting point shifts each time to the last ending point, but changing direction. I wanted this to happen for eveyrtime the first link tag is generated. 

## Learning About Rate Limiting and Queueing   
As opposed to fetching an exisitng data, I was dealing with rapid, large quantity of data streams happening each second, so I had to implement a buffer and not request too often to Wiki because otherwise I was blocked and kept getting 429 error when I opened the console. Instead of letting every edit trigger an immediate API call, I had to create a buffer space, a cache to manage the chaotic traffic with EventSource stream.   
For understanding Timeout and Promise, this series on Coding Train youtube helped me a lot <a href="https://youtu.be/AwyoVjVXnLk?si=9WLf1IMrCn7nZR40">CODING TRAIN async/await </a>   
For resolving 429 requests and building the function module for cache, I had to use multiple LLMs to point me to the right direction and resources, because it was not straightforward, and afterawhile, Claude AI was helpful. 
<a href="https://claude.ai/share/c860a00e-29a0-4deb-881c-a58d4a46c1ea">Clude AI LLM Chatlink</a>   


