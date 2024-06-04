# Calculator-
import tkinter as tk
from math import *

class Calculator:
    def __init__(self, root):
        self.root = root
        self.root.title("Calculator")
        self.root.geometry("400x500")
        
        self.expression = ""
        self.text_input = tk.StringVar()
        
        self.create_widgets()
    
    def create_widgets(self):
        # Display
        self.entry = tk.Entry(self.root, font=('arial', 20, 'bold'), textvariable=self.text_input, bd=30, insertwidth=4, width=14, borderwidth=4)
        self.entry.grid(row=0, column=0, columnspan=4)
        
        # Buttons
        buttons = [
        '@','#','{','}',
            '7', '8', '9', '/', 
            '4', '5', '6', '*', 
            '1', '2', '3', '-', 
            '0', '.', '=', '+'
        ]
        
        row = 1
        col = 0
        for button in buttons:
            if button == '=':
                btn = tk.Button(self.root, text=button, padx=20, pady=20, bd=8, fg='green', font=('arial', 20, 'bold'),
                                command=self.evaluate)
            else:
                btn = tk.Button(self.root, text=button, padx=20, pady=20, bd=8, fg='red', font=('arial', 20, 'bold'),
                                command=lambda x=button: self.btn_click(x))
                
            btn.grid(row=row, column=col)
            col += 1
            if col == 4:
                col = 0
                row += 1
        
        # Clear Button
        clear_btn = tk.Button(self.root, text='Clear', padx=20, pady=20, bd=8, fg='yellow', font=('arial', 20, 'bold'),
                              command=self.clear_display)
        clear_btn.grid(row=row, column=0, columnspan=4)
    
    def btn_click(self, item):
        self.expression += str(item)
        self.text_input.set(self.expression)
    
    def evaluate(self):
        try:
            result = str(eval(self.expression))
            self.text_input.set(result)
            self.expression = result
        except:
            self.text_input.set("invalid or not found")
            self.expression = ""
    
    def clear_display(self):
        self.expression = ""
        self.text_input.set("")

if __name__ == "__main__":
    root = tk.Tk()
    calc = Calculator(root)
    root.mainloop()
    
