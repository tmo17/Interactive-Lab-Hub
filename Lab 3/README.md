# Chatterboxes
**Caroline Granath, Joe Iovine**
[![Watch the video](https://user-images.githubusercontent.com/1128669/135009222-111fe522-e6ba-46ad-b6dc-d1633d21129c.png)](https://www.youtube.com/embed/Q8FWzLMobx0?start=19)

In this lab, we want you to design interaction with a speech-enabled device--something that listens and talks to you. This device can do anything *but* control lights (since we already did that in Lab 1).  First, we want you first to storyboard what you imagine the conversational interaction to be like. Then, you will use wizarding techniques to elicit examples of what people might say, ask, or respond.  We then want you to use the examples collected from at least two other people to inform the redesign of the device.

We will focus on **audio** as the main modality for interaction to start; these general techniques can be extended to **video**, **haptics** or other interactive mechanisms in the second part of the Lab.

## Prep for Part 1: Get the Latest Content and Pick up Additional Parts 

### Pick up Web Camera If You Don't Have One

Students who have not already received a web camera will receive their [IMISES web cameras](https://www.amazon.com/Microphone-Speaker-Balance-Conference-Streaming/dp/B0B7B7SYSY/ref=sr_1_3?keywords=webcam%2Bwith%2Bmicrophone%2Band%2Bspeaker&qid=1663090960&s=electronics&sprefix=webcam%2Bwith%2Bmicrophone%2Band%2Bsp%2Celectronics%2C123&sr=1-3&th=1) on Thursday at the beginning of lab. If you cannot make it to class on Thursday, please contact the TAs to ensure you get your web camera. 

### Get the Latest Content

As always, pull updates from the class Interactive-Lab-Hub to both your Pi and your own GitHub repo. There are 2 ways you can do so:

**\[recommended\]**Option 1: On the Pi, `cd` to your `Interactive-Lab-Hub`, pull the updates from upstream (class lab-hub) and push the updates back to your own GitHub repo. You will need the *personal access token* for this.

```
pi@ixe00:~$ cd Interactive-Lab-Hub
pi@ixe00:~/Interactive-Lab-Hub $ git pull upstream Fall2022
pi@ixe00:~/Interactive-Lab-Hub $ git add .
pi@ixe00:~/Interactive-Lab-Hub $ git commit -m "get lab3 updates"
pi@ixe00:~/Interactive-Lab-Hub $ git push
```

Option 2: On your your own GitHub repo, [create pull request](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/2022Fall/readings/Submitting%20Labs.md) to get updates from the class Interactive-Lab-Hub. After you have latest updates online, go on your Pi, `cd` to your `Interactive-Lab-Hub` and use `git pull` to get updates from your own GitHub repo.

## Part 1.

### Text to Speech 

In this part of lab, we are going to start peeking into the world of audio on your Pi! 

We will be using the microphone and speaker on your webcamera. In the home directory of your Pi, there is a folder called `text2speech` containing several shell scripts. `cd` to the folder and list out all the files by `ls`:

```
pi@ixe00:~/text2speech $ ls
Download        festival_demo.sh  GoogleTTS_demo.sh  pico2text_demo.sh
espeak_demo.sh  flite_demo.sh     lookdave.wav
```

You can run these shell files by typing `./filename`, for example, typing `./espeak_demo.sh` and see what happens. Take some time to look at each script and see how it works. You can see a script by typing `cat filename`. For instance:

```
pi@ixe00:~/text2speech $ cat festival_demo.sh 
#from: https://elinux.org/RPi_Text_to_Speech_(Speech_Synthesis)#Festival_Text_to_Speech

echo "Just what do you think you're doing, Dave?" | festival --tts
```

Now, you might wonder what exactly is a `.sh` file? Typically, a `.sh` file is a shell script which you can execute in a terminal. The example files we offer here are for you to figure out the ways to play with audio on your Pi!

You can also play audio files directly with `aplay filename`. Try typing `aplay lookdave.wav`.

\*\***Write your own shell file to use your favorite of these TTS engines to have your Pi greet you by name.**\*\*
(This shell file should be saved to your own repo for this lab.)

SEE REPO

Bonus: If this topic is very exciting to you, you can try out this new TTS system we recently learned about: https://github.com/rhasspy/larynx

### Speech to Text

Now examine the `speech2text` folder. We are using a speech recognition engine, [Vosk](https://alphacephei.com/vosk/), which is made by researchers at Carnegie Mellon University. Vosk is amazing because it is an offline speech recognition engine; that is, all the processing for the speech recognition is happening onboard the Raspberry Pi. 

In particular, look at `test_words.py` and make sure you understand how the vocab is defined. 
Now, we need to find out where your webcam's audio device is connected to the Pi. Use `arecord -l` to get the card and device number:
```
pi@ixe00:~/speech2text $ arecord -l
**** List of CAPTURE Hardware Devices ****
card 1: Device [Usb Audio Device], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```
The example above shows a scenario where the audio device is at card 1, device 0. Now, use `nano vosk_demo_mic.sh` and change the `hw` parameter. In the case as shown above, change it to `hw:1,0`, which stands for card 1, device 0.  

Now, look at which camera you have. Do you have the cylinder camera (likely the case if you received it when we first handed out kits), change the `-r 16000` parameter to `-r 44100`. If you have the IMISES camera, check if your rate parameter says `-r 16000`. Save the file using Write Out and press enter.

Then try `./vosk_demo_mic.sh`

\*\***Write your own shell file that verbally asks for a numerical based input (such as a phone number, zipcode, number of pets, etc) and records the answer the respondent provides.**\*\*

SEE REPO

### Serving Pages

In Lab 1, we served a webpage with flask. In this lab, you may find it useful to serve a webpage for the controller on a remote device. Here is a simple example of a webserver.

```
pi@ixe00:~/Interactive-Lab-Hub/Lab 3 $ python server.py
 * Serving Flask app "server" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 162-573-883
```
From a remote browser on the same network, check to make sure your webserver is working by going to `http://<YourPiIPAddress>:5000`. You should be able to see "Hello World" on the webpage.

### Storyboard

Storyboard and/or use a Verplank diagram to design a speech-enabled device. (Stuck? Make a device that talks for dogs. If that is too stupid, find an application that is better than that.) 

\*\***Post your storyboard and diagram here.**\*\*

Write out what you imagine the dialogue to be. Use cards, post-its, or whatever method helps you develop alternatives or group responses. 
![11717](https://user-images.githubusercontent.com/112022260/192379759-288a754f-243e-4e4d-a4ad-fa5466a01001.jpg)
![14208](https://user-images.githubusercontent.com/112022260/192379768-55c9ef13-a9b4-4a8a-b0ba-84bd003f11eb.jpg)


\*\***Please describe and document your process.**\*\*

1) I first started by discussing with my peers at my tables on our interests and potential thoughts for a design
2) I then began to ideate on what some of the best ideas that we came up with could look like as seen in the pictures above
3) I then brought my visualized and refined ideas to my group for more feedback. The consensus was that 
4)  After some iteration, I choose the leading idea and wrote a more thorough script

* Person: "Good morning Gary the Guitar"
* Guitar: "Good morning Trevor, start your day off with a tune?:

* Person: "You know what Gary I might, let's see if this is in tune"
* Guitar: "You last played 3 weeks ago, I doubt it!" 

* Person: "Yeah yeah, okay checking the E string, how does that sound?"
* Guitar: "Your a little flat try tuning up a step"

* Person: ** Move it up and playing **
* Guitar:  "That's better! now your ready to play"

* Person: " Great, but I'm blanking on a song, any suggestions from my library?:
* Guitar: "How about, Sweet Home Alabama?"
 
### Acting out the dialogue

Find a partner, and *without sharing the script with your partner* try out the dialogue you've designed, where you (as the device designer) act as the device you are designing.  Please record this interaction (for example, using Zoom's record feature).

* Please see below for link to the interaction!

https://drive.google.com/file/d/16wYQi18-BngfAFHCukiMX8VnizlBL6be/view?usp=sharing

\*\***Describe if the dialogue seemed different than what you imagined when it was acted out, and how.**\*\*

The dialogue was slightly different than imagined though largely held up to the situation.  One of the things I did not anticpate in the dialogue is timing and quick feedback was very important.  If you did not respond right away, people had moved on to another note or assumed they were playing correctly.  Additionally feedback was recieved there is often limited time to practice and it is frustrating to be waiting on the device to play.

Something else I didn't anticpate was misunderstanding around note e.g., are we talking about the high or low E string?  It would be important for the machine to sense this and clarify what the person is trying to play in case it is the wrong note or they are truly out of tune.

### Wizarding with the Pi (optional)
In the [demo directory](./demo), you will find an example Wizard of Oz project. In that project, you can see how audio and sensor data is streamed from the Pi to a wizard controller that runs in the browser.  You may use this demo code as a template. By running the `app.py` script, you can see how audio and sensor data (Adafruit MPU-6050 6-DoF Accel and Gyro Sensor) is streamed from the Pi to a wizard controller that runs in the browser `http://<YouPiIPAddress>:5000`. You can control what the system says from the controller as well!

\*\***Describe if the dialogue seemed different than what you imagined, or when acted out, when it was wizarded, and how.**\*\*

Did not wizard due to malfunctioning camera

# Lab 3 Part 2

For Part 2, you will redesign the interaction with the speech-enabled device using the data collected, as well as feedback from part 1.

## Prep for Part 2

1. What are concrete things that could use improvement in the design of your device? For example: wording, timing, anticipation of misunderstandings...

*Feedback from Carlos:* 
Overall the ideas were very creative. They explored areas in which voice assistants aren’t being used. The ideas are very clear and straightforward. 
I found the plant idea to be extremely useful to people. It is also my favorite. I can also see new plant owners wanting something like this.
Guitar Tuner is also interesting especially since I’m not too familiar with it. 
The study buddy seems like a voice enabled reminder. It might not be as cool as the others but maybe the easiest to tackle. 
Improvements:
I think the plant idea could be improved if it also talked to you unprompted. Sometimes people can forget about plants, so it’d be nice if it was like “hey ask me how I’m doing.”
For Guitar tuner I think it’d also be interesting if it was able to tell you how a string should sound. So when it tells you to tune up it plays what the tune should be 
Study buddy could be sent things to remind you about and when it should remind you about things/ how often. 

*Feedback from Professor Wu*

* Think more into the detail of the action, after they change it
	* Did it actually fix it?
	* If you just say flat flat and it it's like hot and cold
	 
  	* Could include things like "Tune up half X" or that "that was too much"
  	* What if a user pushes back thinking it's fine

	* Do you do it when it's plucked, other timing for jumping in
		* "Is now a good a time" example



2. What are other modes of interaction _beyond speech_ that you might also use to clarify how to interact?

Other ideas beyond speech include:
* Metronome for playing
* Having a variable pitch that get higher as the player gets closer to the correct note (sort of like hot or cold) - this could help clarify to the user how far to go   when they are tuning their instrument
* Give auditory feedback when they are getting notes right or wrong
* Playing the accompanying instruments
* Adding a "Whshhp" when users ask for the next song to imitate folder over the next disk in a record pile to give feedback th

3. Make a new storyboard, diagram and/or script based on these reflections.
![IDD HW3](https://user-images.githubusercontent.com/112022260/193709256-16df00b2-0000-41c1-991b-bda6bc22479e.jpg)

## Prototype your system

The system should:
* use the Raspberry Pi 
* use one or more sensors
* require participants to speak to it. 

*Document how the system works*

* I wizarded the device using two seperate phones. One phone acted as the "Guitar Buddy" that magically turned on (or was called) as a user picked up the guitar.  The second, was used by me to wizard the device from another room from the room that called the other to activate GuitarBuddy.

* I adopted this setup rather than using the Pi, as I was never able to fully get the camera to recognize any intelligible voice commands. Additionaly, it was complicated that I could not bring my Dad's guitar on campus and as a commuter student I cannot access the raspberry pi at home due to network errors (have tried to address with Alexandra to no avail). Due to these limitations, I went with the phone wizard setup.

*Include videos or screencaptures of both the system and the controller.*

Please see here for video of the system and controller: https://drive.google.com/file/d/1th_JHUxALDwgEcsZGNYAscwIsggoXToh/view?usp=sharing

## Test the system
Try to get at least two people to interact with your system. (Ideally, you would inform them that there is a wizard _after_ the interaction, but we recognize that can be hard.)

Answer the following:

### What worked well about the system and what didn't?

*Worked well*

* The phone worked well to simulate the wizard without having to be in the room in addition faking the "turning on" fairly well.  It efficiently made the user feel like they were interacting with the audio system with minimal overhead.

*A few things that did not work*
 
 * As a researcher I could not see my particpant which made things difficult. it also lacked any ability to "extend" the functionality by incorporating video of the user like a camera microphone could have done.  Lastly, when trying to achieve voice recognition, my microphone would not correctly pick up audio, especialy if there was any background noise at all.

 * My voice was echoed during the video'd simulation.
 
 * In the future, I would also like to explore situations where the tuner is wrong and the user pushes back and answer questions like: How should the GuitarBuddy handle this? What kind of things would it say?  What if it was calibrated properly?  What if not?  Could we resync up the device using the user? -> would love to explore this in future labs.  Could you sync the pi so when you hit a pan it a makes a sound of your choosing (e.g., percussion) then hitting the table makes a drum.  You could then use anywhere you are as a drumset or other instrument.

\*\**your answer here*\*\*

### What worked well about the controller and what didn't

\*\**your answer here*\*\*

* What did work well:*

* The tuning section was much better with significantly more realistic functionality on how that interaction would take 
* The overal concept worked well as a guitar teacher.  The lack of video made users focus on looking and playing guitar and listening for the vocal cues rather than   focusing on a video 

* What didn't work well:*

* I couldn't see when they were going to start nor did I script to include a countdown of when each action was happening.  in the future I would also need to include options like restart, go forward and go back upon further reflection

* Because I was wizarding live, you didn't see the frustrating moments that would accompany a more autonomous prototype.  These would likely give valuable insight into where the system needs to be built out further.  However, by wizarding it live, I was able to see far more of the different options people choose and could get much farther down a theoretical "tree" through this type of prototyping.

### What lessons can you take away from the WoZ interactions for designing a more autonomous version of the system?


\*\**your answer here*\*\*


* It would really help to be able to see user and the users hands in order to get a good understanding of what they are doing or asking about

* When asking user's a question, you should give them prompts on what are their possible options or actions to choose from

* You would have to design around background noise and other incidental sounds to give consistent and useful feedback to someone playing guitar

* To make it fully autonomous, the feature set or avenues needs to be paired down significantly (e.g., GuitarTunerBuddy would be a more realisticand doable product vs. a full GuitarBuddy that encompasses all training) -> This is also a lesson I will look to utilize in future works (e.g., how can I execute thoroughly on a smaller problem space that takes inspiration from larger ones)

### How could you use your system to create a dataset of interaction? What other sensing modalities would make sense to capture?

\*\**your answer here*\*\*

* I could use my system to capture what the types of actions different guitar players would like to take with a GuitarBuddy (e.g., play together, play metronome, play accompanying instruments, teach me scales, teach me notes etc..) as well as user data like what songs they choose, what notes they play, how in tune they normally are, what are the most commons topics asked for help on. 
* Other sensing modalities would be visual as mentioned so you could give feedback on body posture, hand positioning and better read their actions
* You could include additional analysis on topof the audio currently tracked such as the rythmn of strumming to see if it is on beat.

