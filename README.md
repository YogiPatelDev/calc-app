mport tkinter as tk

def calculate():
    try:
        result.set(eval(entry.get()))  # Evaluate the expression safely
    except Exception:
        result.set("Error")

def open_calculator():
    # Create a popup window
    popup = tk.Toplevel()
    popup.title("Simple Calculator")
    popup.geometry("300x400")

    # Create UI components in the popup
    global entry, result
    entry = tk.Entry(popup, width=20, font=("Arial", 16))
    entry.grid(row=0, column=0, columnspan=4)

    result = tk.StringVar()
    result_label = tk.Label(popup, textvariable=result, font=("Arial", 16))
    result_label.grid(row=1, column=0, columnspan=4)

    # Buttons
    buttons = [
        ('7', 2, 0), ('8', 2, 1), ('9', 2, 2), ('/', 2, 3),
        ('4', 3, 0), ('5', 3, 1), ('6', 3, 2), ('*', 3, 3),
        ('1', 4, 0), ('2', 4, 1), ('3', 4, 2), ('-', 4, 3),
        ('0', 5, 0), ('.', 5, 1), ('+', 5, 2), ('=', 5, 3)
    ]

    for text, row, col in buttons:
        if text == '=':
            button = tk.Button(popup, text=text, font=("Arial", 16), command=calculate)
        else:
            button = tk.Button(popup, text=text, font=("Arial", 16), command=lambda t=text: entry.insert(tk.END, t))
        button.grid(row=row, column=col)

# Main application window
root = tk.Tk()
root.title("Main Application")

# Button to open the calculator popup
open_calc_btn = tk.Button(root, text="Open Calculator", font=("Arial", 16), command=open_calculator)
open_calc_btn.pack(pady=20)

# Run the main application
root.mainloop()
