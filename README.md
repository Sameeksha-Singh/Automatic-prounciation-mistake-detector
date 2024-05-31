# Automatic-prounciation-mistake-detector
import difflib
import tkinter as tk
from tkinter import scrolledtext

def detect_mistakes():
    original_text = original_textbox.get("1.0", tk.END)
    recorded_text = recorded_textbox.get("1.0", tk.END)
    
    # Use difflib to find differences between two texts
    differ = difflib.Differ()
    differences = list(differ.compare(original_text.split(), recorded_text.split()))
    
    mistake_indices = [i for i, diff in enumerate(differences) if diff.startswith('+ ') or diff.startswith('- ')]
    
    if mistake_indices:
        mistakes = [differences[i] for i in mistake_indices]
        mistake_output.configure(text="Mistakes found:\n" + "\n".join(mistakes))
    else:
        mistake_output.configure(text="No mistakes detected.")

# Create main window
root = tk.Tk()
root.title("Pronunciation Mistake Detector")

# Create text boxes for original and recorded text
original_textbox = scrolledtext.ScrolledText(root, width=40, height=10, wrap=tk.WORD)
original_textbox.grid(row=0, column=0, padx=5, pady=5)

recorded_textbox = scrolledtext.ScrolledText(root, width=40, height=10, wrap=tk.WORD)
recorded_textbox.grid(row=0, column=1, padx=5, pady=5)

# Button to trigger mistake detection
detect_button = tk.Button(root, text="Detect Mistakes", command=detect_mistakes)
detect_button.grid(row=1, column=0, columnspan=2, pady=5)

# Output label for mistakes
mistake_output = tk.Label(root, text="")
mistake_output.grid(row=2, column=0, columnspan=2, pady=5)

root.mainloop()
