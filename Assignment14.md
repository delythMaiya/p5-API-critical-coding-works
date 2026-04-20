***READING***  
The interactive presentation was really exciting to read, especially as I am interested in the practice of generative and aleatoric processes of music composition, and I touched on this a lot during my Bachelor's as a composition student. Brian Eno was mentioned, and "The Ship" is one of my favourite sound installation experience I ever attended and works on the same principle as Reich, each speaker outputting materials at different intervals, causing to overlap differently each time, but with more than 6 speakers. I also remember performing Ligeti's Poème Symphonique for 100 metronomes at conservatoire, where each metronome ticks at different speed until the last remaining one stops. Xenakis is another composer who I once played his work ('Herma') where the composition is based on applying logical operations to Boolean algebra. He was an architect with crazy mathematical precision who hated intuitive randomness. This score is his work 'Metastatis' and he uses stochastic processes and treated the orchesttra as a 'gas', as in kinetic motion of fluids, rather than polyphony. ![image](https://git.arts.ac.uk/user-attachments/assets/cbd49c66-e81a-432b-8b2d-6ce644ebb6a5) It's interesting how his composition methods are extremely precise but the result is the opposite.   
In Spiegel's reading, I really liked the part where Spiegel said _"The distinction between what I delegate to automated processes and what I reserve to the less-rationally-comprehensible methods of more intuitive specification is perhaps the most important aspect of my algorithmic design process."_  
Timbral automation (changing the character/brightness) of the sound has always been something that is achieved best when I do it intuitively. For exmaple, things like notating string players to play 'sul pont' to achieve a ghostly sound, or modulating the envelope of the synth by hand at using knobs, I can't imagine algorithms to nail this perfectly as good as producing MIDI notes or modulating rhythms, because it is a much more continuous motion rather than discrete. Also, I resonated with the statement _logic-based generative process, rather then any specific subset of its output, may be seen as a musical work in itself_. Generative processes go beyond mere auditory experience, it becomes an embodied experience specific to time and location everytime it is performed. I can think of Stockhausen's Aus den sieben Tagen, which only provides texts, no notation, exposing the performer's intuition. In Lutosławski's Jeux vénitiens, the conductor gives a sign to a group of an orchestra section to play a melodic fragment in their own time, the result is very fluid. 

***Final Project HTML***    
I couldn't do come to a conclusion last week with final project idea, here is my current idea:   https://git.arts.ac.uk/pages/d-field0620251/Final-Project-Idea/

***Coding***   
Sketch: https://editor.p5js.org/sizalyth/sketches/ph0B8Rmj- 
I used Kurt Schwitters' _Ursonate_ as my text material, a sound poem that is made up of gibberish, but instead explores the raw phoneic sounds of speech. 
While exploring what Rita grammers can do, I thought Rita.stresses function would work well, although I am still developing this aspect and not finished yet.  
I only got around to making it audio reactive and map with words but a bit arbitary. 
I stumbled on Coding Train's video on using microphone input & frequency analysis, and I wanted to integrate sound, which is essential for this poem.    
My current version doesn't use RiTa grammers yet, but only mapped to an array of stored words from the first page of the poem.     
While going through the poem and listening to difference versions of the performances, I wrote down charactersitcs of the phonetics, so that I could map this to visual charactersistics of the texts eventually. 

The whole point of this poemm was to strip meaning from human speech, convey emotions through pue musicality of the sound of speech. 
Simiarly, texts can evoke this feeling, the font, the shape of the each alphabet, size and shades of the text all contribute to how we perceive.  
![image](https://git.arts.ac.uk/user-attachments/assets/8ec5eb10-dab8-4a28-a1a6-3c12d974d9ae)  
As this poem only makes sense with sound, I wanted to explore how I could tie sound into p5js, and I found many Coding Train tutorials on this.   
I watched these two videos in particular (https://youtu.be/q2IDNkUws-A?si=yMrIOdT5FDCoCnQK), (https://youtu.be/2O3nm0Nvbi4?si=F1BO1VtQzRMZVuJz).   
Conviniently, I met my friend who plays the flute so I asked her to recite a bit of the poem through the flute, which has a wider frequency range than human voice to react.  

https://git.arts.ac.uk/user-attachments/assets/349232f0-0cc5-4a00-b1f3-ca20282ca493


I mapped the size and location of the text to amplitude and frequncy.   
The choice of words from the poem is mapped to amplitude band, which is not what I want at the end of the day. It would be nice to somehow use machine learning to recognise certain words or character (flucoma Max/msp plugin does timbral detections). Also, it would be nice to go beyond simply displaying text.
Next, I would like to extract the stresses using RiTa grammer, and analyse the structural grammer of the sonata form in the poem and create rules and syntax. 








