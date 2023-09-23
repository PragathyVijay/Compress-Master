'''import webbrowser
import tkinter as tk
my_w = tk.Tk()
my_w.title('File Zipper')

my_link = tk.Label(my_w, text = 'Compress', fg = 'black', cursor = 'hand2', font = ('Times', 20, 'bold'))
my_link.grid(row=0, column=0, padx=300, pady=300)

my_link.bind('<Button-1>', lambda x : webbrowser.open_new("http://localhost:8888/notebooks/Documents/Python/ADS%20Project/File%20Zipper.ipynb"))

my_w.mainloop()'''

from tkinter import *
import tkinter as tk
from FileZipper import *
from PIL import ImageTk, Image
import os
from matplotlib import pyplot as plt
from matplotlib.figure import Figure
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg

root = Tk()
root.title('File Zipper')
root.geometry("1500x750")

window = Toplevel(root)
window.geometry("1500x750")
window1 = Toplevel(root)
window1.geometry("1500x750")

#root.config(bg="black")
bg1 = Image.open("bg.png.png")
resized = bg1.resize((1500, 750), Image.Resampling.LANCZOS)
bg = ImageTk.PhotoImage(resized)

def compress(path):
    try:
        if path:
            h = Huffmancode(path)
            compressed_file = h.compression()
            txt3 = Label(window, text = "The file is compressed successfully!", font = ("Helvetica", 24))
            txt3.pack(pady = 20)
        else:
            txt1 = Label(window, text = "Enter a file name...", font = ("Helvetica", 24))
            txt1.pack(pady = 20)
    except FileNotFoundError:
        txt2 = Label(window, text = "No such file exists.", font = ("Helvetica", 24))
        txt2.pack(pady = 20)
        
def decompress(path):
    try:
        if path:
            h = Huffmancode(path)
            h.decompress(path)
            txt3 = Label(window1, text = "The file is decompressed successfully!", font = ("Helvetica", 24))
            txt3.pack(pady = 20)
        else:
            txt1 = Label(window1, text = "Enter a file name...", font = ("Helvetica", 24))
            txt1.pack(pady = 20)
    except FileNotFoundError:
        txt2 = Label(window1, text = "No such file exists.", font = ("Helvetica", 24))
        txt2.pack(pady = 20)

def filecomp():
    #root.destroy()
    window.tkraise()
    label1 = Label(window, text = "ENTER THE PATH OF YOUR FILE....", font = ("Helvetica", 24))
    label1.pack(pady = 24)
    path = Entry(window, font = ("Helvetica", 20), justify = CENTER)
    path.pack(pady = 20)
    btn3 = Button(window, text = "Compress", command = lambda : compress(path.get()), fg = 'Black', cursor = 'hand2', font = ("onedork", 22, 'bold'))
    btn3.pack(pady = 20)
    window.mainloop()
    
def filedecomp():
    window1.tkraise()
    label2 = Label(window1, text = "ENTER THE PATH OF YOUR COMPRESSED FILE....", font = ("Helvetica", 24))
    label2.pack(pady = 24)
    path1 = Entry(window1, font = ("Helvetica", 20), justify = CENTER)
    path1.pack(pady = 20)
    btn4 = Button(window1, text = "Decompress", command = lambda : decompress(path1.get()), fg = 'Black', cursor = 'hand2', font = ("onedork", 22, 'bold'))
    btn4.pack(pady = 20)
    window1.mainloop()
    
def graph():
    bina = []
    text = []
    w = os.path.getsize("textfile.bin")
    bina.append(w)
    x = os.path.getsize("textfile.txt")
    text.append(x)
    y = os.path.getsize("textfile1.bin")
    bina.append(y)
    z = os.path.getsize("textfile1.txt")
    text.append(z)
    
    f = Figure(figsize=(5,5), dpi=100)
    a = f.add_subplot(111)
    a.plot(bina, text)
    canvas = FigureCanvasTkAgg(f)
    canvas.draw()
    canvas.get_tk_widget().pack(side = BOTTOM, fill = BOTH, expand = True)
    
label = Label(root, image = bg)
label.pack(pady = 50)
label.place(x=0, y=0)

label = Label(root, text = "Click the button of your choice...", font = ("Helvetica", 34))
label.pack(pady = 50)

btn1 = Button(root, text = "Upload File", command = filecomp, fg = 'Red', cursor = 'hand2', font = ("onedork", 24, 'bold'))
btn1.pack(pady = 20)

btn2 = Button(root, text = "Download File", command = filedecomp, fg = 'Green', cursor = 'hand2', font = ("onedork", 24, 'bold'))
btn2.pack(pady = 20)

'''btns = Button(root, text = "Comparison", command = graph, fg = 'Blue', cursor = 'hand2', font = ("onedork", 24, 'bold'))
btns.pack(pady = 20)'''

root.mainloop()

