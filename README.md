# Python code for calculater


import tkinter as tk

# Function to update the screen
def update_screen(text):
    screen_var.set(text)

# Function to evaluate the expression
def evaluate():
    try:
        result = str(eval(screen_var.get()))
        update_screen(result)
    except Exception:
        update_screen("Error")

# Function to clear the screen
def clear():
    update_screen("")

# Create the main window
window = tk.Tk()
window.title("Calculator")

# Create a screen variable
screen_var = tk.StringVar()

# Create the screen (entry widget) and place it at the top
screen = tk.Entry(window, textvariable=screen_var, font=("Arial", 24), justify="right")
screen.grid(row=0, column=0, columnspan=4)

# Define the buttons
buttons = [
    '7', '8', '9', '/',
    '4', '5', '6', '*',
    '1', '2', '3', '-',
    '0', '.', '=', '+',
    'C'
]

# Create and place the buttons
row = 1
col = 0
for button_text in buttons:
    tk.Button(window, text=button_text, command=lambda text=button_text: on_button_click(text)).grid(row=row, column=col)
    col += 1
    if col > 3:
        col = 0
        row += 1

# Function to handle button clicks
def on_button_click(text):
    if text == "=":
        evaluate()
    elif text == "C":
        clear()
    else:
        current_text = screen_var.get()
        if current_text == "Error":
            current_text = ""
        update_screen(current_text + text)

# Start the GUI main loop
window.mainloop()
