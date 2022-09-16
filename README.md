# my-alexa
FOR DUBEM
import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)


def talk(text):
    engine.say(text)
    engine.runAndWait()


def take_command():
    try:
        with sr.Microphone() as source:
            print('listening...')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'alexa' in command:
                command = command.replace('alexa', '')
                print(command)
    except:
        pass
    return command


def run_alexa():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif 'Send' in command:
        send = command.replace('send', '')
        talk('To whom do you want to send a message to')
        talk('sending message to' + send)
        pywhatkit.sendwhatmsg(send)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('Current time is ' + time)
    elif 'who the heck is' in command:
        person = command.replace('who the heck is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'date' in command:
        talk('sorry, I have a headache')
    elif 'are you single' in command:
        talk('I am in a relationship with wifi')
    elif 'joke' in command:
        talk(pyjokes.get_joke())
        print(pyjokes.get_joke())
    elif 'what is your name' in command:
        talk('My name is Alexa')
    elif 'how old are you' in command:
        talk('I am the same age as you')
    elif 'are you a baby' in command:
        talk('No i am not a baby')
    elif 'do you have a car' in command:
        talk('Yes i drive a lamborghini')
    elif 'who created you' in command:
        talk('Megbele David')
    elif 'who is david' in command:
        print('Megbele David is a boy who schools in razeva his friends are kizito opeyemi daniel and emmanuel otika he is 14 years old')
        talk('Megbele David is a boy who schools in razeva his friends are kizito opeyemi daniel and emmanuel otika he is 14 years old')
    elif 'who is kizito' in command:
        talk('Kizito is one of megbele david friends who likes to watch anime')
    elif 'who is daniel' in command:
        talk('daniel aguguo who wants to change his name to michael angelo is one of megbele davids friend in ss1 gold his siblings are francis and daniella with his small brother david forgot his name while writing this code')
    elif 'who is Mr Megbele' in command:
        talk('Davids father is Mr megbele married to his mother Mrs Megbele')
    else:
        talk('Please say the command again.')


while True:
    run_alexa()
