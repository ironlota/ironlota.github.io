---
layout: post
title: Personal Assistant using Speech Recognition
---

![speech_recog.png](http://copia.com.au/wp-content/themes/copia/images/medicalspeech.png)
(taken from [Speech Recognition](http://copia.com.au/medical-speech-recognition/))

# Definition

> A personal assistant, also referred to as personal aide (PA) or personal secretary (PS), is a job title describing a person who assists a specific person with their daily business or personal tasks.
(taken from [Personal Assistant Wikipedia](https://en.wikipedia.org/wiki/Personal_assistant))

Atau terjemahannya, asisten pribadi adalah pekerjaan yang dilakukan orang untuk membantu orang lain dalam melakukan pekerjaan dan tugas-tugasnya.

Seiring berjalannya waktu, *personal assistant* tidak lagi dilakukan oleh orang saja. Aplikasi pun dapat menggantikan peran manusia menjadi *personal assistant* bagi manusia lainnya.

Sebut saja aplikasi seperti *Siri* kepunyaan *Apple*, *Google Now* dan *Google Assistant* kepunyaan *Google*.

# How it Works?

Bagaimana aplikasi tersebut dapat bekerja?

## Yeah, the answer is **Speech Recognition**

> Speech recognition is the ability of a machine or program to identify words and phrases in spoken language and convert them to a machine-readable format.
(taken from [Speech Recognition](http://searchcrm.techtarget.com/definition/speech-recognition))

*Speech Recognition* akan mengidentifikasi kata-kata yang diucapkan oleh *user* dan akan langsung menerjemahkannya kedalam format yang dimengerti oleh mesin.

Sistem yang memiliki fasilitas *Speech Recognition* akan mengambil data dari dalam "kamus pribadi" untuk diterjemahkan agar *output* yang dikeluarkan sesuai dengan permintaan *user*

# Let's see the Demo!
## *Google Assistant*
![google_asisstant.gif](https://i.kinja-img.com/gawker-media/image/upload/s--fakpVmLm--/c_scale,fl_progressive,q_80,w_800/mebn1kjo7jylfhmakgfw.gif)
(taken from [Google Assistant Is a Mega AI Bot That Wants To Be Absoutely Everywhere](http://gizmodo.com/google-assistant-is-a-mega-chatbot-that-wants-to-be-abs-1777351140))

## *Siri*
![siri.gif](https://cdn.dribbble.com/users/30252/screenshots/2176533/siri-el-capitan.gif)
(taken from [Siri Animation on Mac](https://dribbble.com/shots/2176533-Siri-animation-on-Mac))

# Can we build our own personal assistant?
> __YES WE CAN__

Sekarang sudah banyak *APIs* yang bisa dipakai untuk membuat *personal assistant using speech recognition*
Salah satunya adalah *Google Text to Speech API or known as gTTS* dengan menggunakan bahasa pemrograman *Python*

Penggunaan gTTS sangatlah simpel dan tidak memerlukan banyak kode.

Aplikasi berikut seperti dikutip dari [Personal Assistant (Jarvis) in Python](https://pythonspot.com/en/personal-assistant-jarvis-in-python/) dapat menunjukkan kabar dari *personal assistant*, waktu sistem saat ini, dan juga lokasi *user* saat ini.

```
#!/usr/bin/env python3
# Requires PyAudio and PySpeech.
 
import speech_recognition as sr
from time import ctime
import time
import os
from gtts import gTTS
 
def speak(audioString):
    print(audioString)
    tts = gTTS(text=audioString, lang='en')
    tts.save("audio.mp3")
    os.system("mpg321 audio.mp3")
 
def recordAudio():
    # Record Audio
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Say something!")
    audio = r.listen(source)
 
    # Speech recognition using Google Speech Recognition
    data = ""
    try:
        # Uses the default API key
        # To use another API key: `r.recognize_google(audio, key="GOOGLE_SPEECH_RECOGNITION_API_KEY")`
        data = r.recognize_google(audio)
        print("You said: " + data)
    except sr.UnknownValueError:
        print("Google Speech Recognition could not understand audio")
    except sr.RequestError as e:
        print("Could not request results from Google Speech Recognition service; {0}".format(e))
 
    return data
 
def jarvis(data):
    if "how are you" in data:
        speak("I am fine")
 
    if "what time is it" in data:
        speak(ctime())
 
    if "where is" in data:
        data = data.split(" ")
        location = data[2]
        speak("Hold on Frank, I will show you where " + location + " is.")
        os.system("chromium-browser https://www.google.nl/maps/place/" + location + "/&amp;")
 
# initialization
time.sleep(2)
speak("Hi Frank, what can I do for you?")
while 1:
    data = recordAudio()
    jarvis(data)
```

## So are you ready to built your own personal assistant?
