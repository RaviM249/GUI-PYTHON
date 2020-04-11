# GUI-PYTHON
This is a small GUI application
import tkinter as tk
import os
from csv import DictWriter
from tkinter import ttk
win=tk.Tk()
win.title('Ravi')

name_label=ttk.Label(win, text='Enter your name: ')
name_label.grid(row=0, column=0, sticky=tk.W)

age_label=ttk.Label(win, text='Enter your age: ')
age_label.grid(row=2,column=0, sticky=tk.W)

gender_var=tk.StringVar()
gender_label=ttk.Label(win, text='Gender: ')
gender_label.grid(row=3,column=0,sticky=tk.W)
gender_combobox=ttk.Combobox(win,width=13, textvariable=gender_var,state='readonly')
gender_combobox['values']=('Male','Female','Other')
gender_combobox.current(0)
gender_combobox.grid(row=3,column=1)

email_label=ttk.Label(win, text='Enter your email:')
email_label.grid(row=1,column=0,sticky=tk.W)
name_var=tk.StringVar()
email_var=tk.StringVar()
age_var=tk.IntVar()

usertype=tk.StringVar()
radiobtn1=ttk.Radiobutton(win,text='Student',value='Student',variable=usertype)
radiobtn1.grid(row=4,column=0)

radiobtn2=ttk.Radiobutton(win, text='Teacher', value='Teacher', variable=usertype)
radiobtn2.grid(row=4,column=1)

name_entrybox=ttk.Entry(win,width=16, textvariable=name_var)
name_entrybox.grid(row=0,column=1)
name_entrybox.focus()

checkbtn_var=tk.IntVar()
checkbtn=ttk.Checkbutton(win, text='I agree to terms and conditions', variable=checkbtn_var)
checkbtn.grid(row=5,column=0,columnspan=3)


email_entrybox=ttk.Entry(win,width=16, textvariable=email_var)
email_entrybox.grid(row=1,column=1)

age_entrybox=ttk.Entry(win,width=16, textvariable=age_var)
age_entrybox.grid(row=2,column=1)

#---------------------This comment code is for writing in normal txt file----------------------------.

# def action():
#     username=name_var.get()
#     userage=age_var.get()
#     useremail=email_var.get()
#     usergender=gender_var.get()
#     user_type=usertype.get()
#     if checkbtn_var.get() ==0:
#         subscribed='NO'
#     else:
#         subscribed='YES'
#     print(f'{username} is {usergender} and is {userage} years old. His EmailID is {useremail} ')
#     print(f'He is a {user_type} Subscription status {subscribed}')

#     with open('file.txt', 'a') as f:
#         f.write(f'{username},{userage},{useremail},{usergender},{user_type},{subscribed}\n')
    
#     name_entrybox.delete(0,tk.END)
#     age_entrybox.delete(0,tk.END)
#     email_entrybox.delete(0,tk.END)
#     # name_label.configure(foreground="Blue")

# ----------------This is the code if you want to write in csv file----------------------
def action():
    username=name_var.get()
    userage=age_var.get()
    useremail=email_var.get()
    usergender=gender_var.get()
    user_type=usertype.get()
    if checkbtn_var.get() ==0:
        subscribed='NO'
    else:
        subscribed='YES'

    with open('file.csv','a',newline='') as f:
        dict_writer=DictWriter(f, fieldnames=['Username','Email Address','Age', 'User type','Gender','Subscribed'])
        if os.stat('file.csv').st_size==0:
            dict_writer.writeheader()
        dict_writer.writeheader()
        dict_writer.writerow({
            'Username': username,
            'Email Address': useremail,
            'Age': userage,
            'Gender': usergender,
            'User type': usertype,
            'Subscribed': subscribed
        })

    name_entrybox.delete(0,tk.END)
    age_entrybox.delete(0,tk.END)
    email_entrybox.delete(0,tk.END)

submit_button=ttk.Button(win, text='Submit',command=action)
submit_button.grid(row=6,column=0)


win.mainloop()
