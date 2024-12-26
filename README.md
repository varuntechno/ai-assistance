# ai-assistance
import speech_recognition as sr
import os
import pyttsx3

def speak(text):
    engine = pyttsx3.init()
    engine.say(text)
    engine.runAndWait()

def listen_command():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening for a command...")
        audio = recognizer.listen(source)

        try:
            command = recognizer.recognize_google(audio)
            print(f"You said: {command}")
            return command.lower()
        except sr.UnknownValueError:
            print("Sorry, I did not understand that.")
            return None
        except sr.RequestError:
            print("Could not request results from Google Speech Recognition service.")
            return None

def execute_command(command):
    if "open notepad" in command:
        os.system("notepad")
        speak("notepad")
    elif "open calculator" in command:
        os.system("calc")
        speak("Opening Calculator")
    else:
        speak("Command not recognized.")

if __name__ == "__main__":
    while True:
        command = listen_command()
        if command:
            execute_command(command)
