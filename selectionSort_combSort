from tkinter import*
from tkinter import ttk
import random
import time
import sys
import threading

root = Tk()
root.title('sorting')
root.maxsize(1920, 1080)
root.config(bg='pink')

#variable
selected_alg = StringVar()
data = []
data2 = []

def drawData(data, colorArray):
    canvas.delete("all")
    c_height = 380
    c_width = 600
    x_width = c_width / (len(data) + 1)
    offset = 1
    spacing = 1
    normalizeData = [i / max(data) for i in data]
    for i, height in enumerate(normalizeData):
        #top
        x0 = i * x_width + offset + spacing
        y0 = c_height - height * 340
        #botton
        x1 = (i + 1) * x_width + offset
        y1 = c_height
        canvas.create_rectangle(x0, y0, x1, y1, fill=colorArray[i])
    root.update_idletasks()


def drawData2(data2, colorArray):
    canvas2.delete("all")
    c_height = 380
    c_width = 600
    x_width = c_width / (len(data2) + 1)
    offset = 1
    spacing = 1
    normalizeData = [i / max(data2) for i in data2]
    for i, height in enumerate(normalizeData):
        #top
        x0 = i * x_width + offset + spacing
        y0 = c_height - height * 340
        #botton
        x1 = (i + 1) * x_width + offset
        y1 = c_height
        canvas2.create_rectangle(x0, y0, x1, y1, fill=colorArray[i])
    root.update_idletasks()

def buat():
    global data
    global data2
    
    try:
        minVal = int(minEntry.get())
    except:
        minVal = 1
    try:
        maxVal = int(maxEntry.get())
    except:
        maxVal = 10
    try:
        size = int(sizeEntry.get())
    except:
        size = 10
    
    if minVal < 0 : minVal = 0
    if maxVal > 100 : maxVal = 100
    if size > 1000 or size < 3: size = 25
    if minVal > maxVal : minVal, maxVal = maxVal, minVal

    data = []
    data2 = []

    for _ in range(size):
        data.append(random.randrange(minVal, maxVal+1))
    
    data2 = data.copy()

    drawData(data, ['red' for x in range (len(data))])
    drawData2(data2, ['red' for x in range(len(data2))])


def combSort(data, drawData):
    start_time2 = time.time()
    gap = len(data)
    swaps = True
    while gap > 1 or swaps:
        gap = max(1, int(gap / 1.3))  # minimum gap is 1
        swaps = False
        for i in range(len(data) - gap):
            j = i+gap
            if data[i] > data[j]:
                data[i], data[j] = data[j], data[i]
                swaps = True
                drawData(data, ['green' if x == i or x == j else 'red' for x in range(len(data))])
                time.sleep(0.1)
    drawData(data, ['green' for x in range(len(data))])
    Label(text=("--- %s seconds ---" % (time.time() - start_time2))).grid(row=3, column=0, padx=5, pady=5)
    


def selectionSort(data2, drawData2):
    start_time = time.time()
    n = len(data2)
    for i in range(n):
        minimum = i
        for j in range(i+1, n):
            if (data2[j] < data2[minimum]):
                minimum = j
                drawData2(data2, ['green' if x == i or x == minimum else 'red' for x in range(len(data2))])
                time.sleep(0.1)
        temp = data2[i]
        data2[i] = data2[minimum]
        data2[minimum] = temp
    drawData2(data2, ['green' for x in range(len(data2))])
    Label(text=("--- %s seconds ---" % (time.time() - start_time))).grid(row=3, column=2, padx=5, pady=5)



def startAlgorithm():
    global data
    global data2
    threading.Thread(target=selectionSort, args=(data2, drawData2)).start()
    threading.Thread(target=combSort, args=(data, drawData)).start()

Label(text="").grid( row=3, column=0, padx=5, pady=5)
Label(text="").grid( row=3, column=2, padx=5, pady=5)


#frame
UI_frame = Frame(root, width = 600, height = 200, bg = 'white')
UI_frame.grid(row = 0, column = 0, padx = 10, pady = 5)

Label(text="Comb Sort").grid( row=2, column=0, padx=5, pady=5)
canvas = Canvas(root, width=600, height=380, bg = 'grey')
canvas.grid(row=4, column=0, padx=10, pady=5)

Label(text="Selection Sort").grid(row=2, column=2, padx=5, pady=5)
canvas2 = Canvas(root, width=600, height=380, bg='grey')
canvas2.grid(row=4, column=2, padx=10, pady=5)
Button(text="Start", command=startAlgorithm, bg="red").grid(row=2, column=1, padx=5, pady=5)


#UI
#row[1]
Button(UI_frame, text = "Buat", command = buat, bg = 'green').grid(row = 1, column = 6, padx = 5, pady = 5)

#row[2]
Label(UI_frame, text="ukuran: ", bg='white').grid(row=1, column=0, padx=5, pady=5, sticky=W)
sizeEntry = Entry(UI_frame)
sizeEntry.grid(row=1, column=1, padx=5, pady=5, sticky=W)

#row[3]
Label(UI_frame, text="minimal value: ", bg='white').grid(row=1, column=2, padx=5, pady=5, sticky=W)
minEntry = Entry(UI_frame)
minEntry.grid(row=1, column=3, padx=5, pady=5, sticky=W)

#row[4]
Label(UI_frame, text="maksimal value: ", bg='white').grid(row=1, column=4, padx=5, pady=5, sticky=W)
maxEntry = Entry(UI_frame)
maxEntry.grid(row=1, column=5, padx=5, pady=5, sticky=W)


root.mainloop()
