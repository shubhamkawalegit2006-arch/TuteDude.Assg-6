from tkinter import *

root = Tk()
root.title("Calculator")
root.geometry("300x400")

expression = ""

def press(num):
    global expression
    expression += str(num)
    equation.set(expression)

def equalpress():
    global expression
    try:
        total = str(eval(expression))
        equation.set(total)
        expression = total
    except:
        equation.set("Error")
        expression = ""

def clear():
    global expression
    expression = ""
    equation.set("")

equation = StringVar()

entry_field = Entry(root, textvariable=equation, font=("Arial", 20), bd=10, relief=RIDGE, justify="right")
entry_field.pack(fill="both")

frame = Frame(root)
frame.pack()

buttons = [
    '7','8','9','/',
    '4','5','6','*',
    '1','2','3','-',
    '0','.','=','+'
]

row = 0
col = 0

for button in buttons:
    if button == "=":
        btn = Button(frame, text=button, width=5, height=2, command=equalpress)
    else:
        btn = Button(frame, text=button, width=5, height=2, command=lambda x=button: press(x))
    btn.grid(row=row, column=col, padx=5, pady=5)
    col += 1
    if col > 3:
        col = 0
        row += 1

clear_btn = Button(root, text="Clear", font=("Arial", 14), command=clear)
clear_btn.pack(fill="both")

root.mainloop()
