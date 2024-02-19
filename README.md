# Coding-Raja-Technologies-Internship Task 1 - To-Do List Application

from tkinter import *
from tkinter import ttk

class todo:
    def __init__(self, root):
        self.root = root
        self.root.title('TO-DO LIST')
        self.root.geometry("700x600")

        self.label = Label(self.root, text='To-do-List-App',
                            font=('Arial', 25, 'bold'), width=5, bd=5, bg='black', fg='white')
        self.label.pack(side='top', fill=BOTH)

        self.label2 = Label(self.root, text='Add Task',
                            font=('Arial', 18, 'bold'), width=10, bd=5, bg='white', fg='black')
        self.label2.place(x=40,y=80)

        self.label3 = Label(self.root, text='Tasks',
                            font=('Arial', 18, 'bold'), width=10, bd=5, bg='white', fg='black')
        self.label3.place(x=380,y=80)

        self.main_text = Listbox(self.root, height=9, bd=5, width=23, font='Arial, 20 italic bold')
        self.main_text.place(x=280,y=150)

        self.text = Text(self.root, bd=5, height=2, width=30, font='Arial, 10 bold')
        self.text.place(x=20,y=150)

        #================add task================#
        
        def add():
            content = self.text.get(1.0, END)
            self.main_text.insert(END, content)
            with open("data.txt", "a") as file:
                file.write(content)
                file.seek(0)
                file.close()
            self.text.delete(1.0, END)

        def delete():
            delete1 = self.main_text.curselection()
            look = self.main_text.get(delete1)
            with open("data.txt", "r+") as f:
                lines = f.readlines()
                f.seek(0)
                for line in lines:
                    item = str(look)
                    if item not in line:
                        f.write(line)
                f.truncate()
                self.main_text.delete(delete1)

        self.button = Button(self.root, text='Add', font=('Arial', 20, 'bold'),
                               width=10, bd=5, bg='grey', fg='black', command=add)
        self.button.place(x=30, y=250)

        self.button2 = Button(self.root, text='Delete', font=('Arial', 20, 'bold'),
                                width=10, bd=5, bg='grey', fg='black', command=delete)
        self.button2.place(x=30, y=320)
                

def main():
    root = Tk()
    ui = todo(root)
    root.mainloop()
    
if __name__ == "__main__":
    main()
