# csv_Mandarin_convert
This tool is designed to convert garbled characters in CSV files into proper Mandarin characters.
### step.1 python code to bilud GUI
```python
import csv
import codecs
import tkinter as tk
from tkinter import filedialog
from tkinter import messagebox

def convert_csv_to_utf8_with_bom(input_file, output_file):
    with codecs.open(input_file, 'r', 'utf-8-sig') as file:
        reader = csv.reader(file)
        rows = list(reader)

    with codecs.open(output_file, 'w', 'utf-8-sig') as file:
        writer = csv.writer(file)
        writer.writerows(rows)

def select_input_file():
    file_path = filedialog.askopenfilename(title="選擇CSV檔案", filetypes=(("CSV files", "*.csv"), ("all files", "*.*")))
    input_file_var.set(file_path)

def select_output_file():
    file_path = filedialog.asksaveasfilename(title="選擇保存位置", filetypes=(("CSV files", "*.csv"),), defaultextension=".csv")
    output_file_var.set(file_path)

def convert():
    input_file = input_file_var.get()
    output_file = output_file_var.get()

    if not input_file or not output_file:
        messagebox.showerror("錯誤", "請選擇輸入和輸出檔案!")
        return

    convert_csv_to_utf8_with_bom(input_file, output_file)
    messagebox.showinfo("成功", "檔案轉換成功!")

app = tk.Tk()
app.title("CSV轉碼工具")

input_file_var = tk.StringVar()
output_file_var = tk.StringVar()

tk.Label(app, text="輸入CSV檔案:").pack(pady=10)
tk.Entry(app, textvariable=input_file_var, width=40).pack(pady=10)
tk.Button(app, text="選擇檔案", command=select_input_file).pack(pady=10)

tk.Label(app, text="輸出CSV檔案:").pack(pady=10)
tk.Entry(app, textvariable=output_file_var, width=40).pack(pady=10)
tk.Button(app, text="選擇保存位置", command=select_output_file).pack(pady=10)

tk.Button(app, text="開始轉換", command=convert).pack(pady=20)

app.mainloop()```



### step.2 turn GUI to EXE
1. Save the code above as "py." file
2. Open the Command Prompt
```bash
cd C:\Users\yourpath
```
3.Package Script with pyinstaller ( install pyinstaller first)
```bash
pyinstaller --onefile --windowed csv_convert.py
```
Once completed, you'll find a new "dist" directory in the current location. This directory will contain an executable named csv_convert.exe.
