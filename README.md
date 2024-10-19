from tkinter import *
from tkinter import Button, Entry, Label, Spinbox, Radiobutton, Toplevel, messagebox, Text
from tkinter.ttk import Combobox, Checkbutton
import tkinter as tk
from tkinter import ttk


a1 = Tk()
a1.title("FreeFolks")
a1.geometry("300x150")
a1.configure(bg='orange')

# Username label and entry
Label(a1, text="Username",bg='orange', fg='black').grid(row=0, column=0)
username_entry = Entry(a1)
username_entry.grid(row=0, column=1)

# Password label and entry
Label(a1, text="Password",bg='orange', fg='black').grid(row=1, column=0)
password_entry = Entry(a1, show='*')
password_entry.grid(row=1, column=1)

# Function to validate login credentials
def validate_login():
    username = username_entry.get()
    password = password_entry.get()
    if username == "Member" and password == "0987":
        messagebox.showinfo("Login Successful", "Welcome, Folks!")
        open_next_page()
    else:
        messagebox.showerror("Login Failed", "Invalid username or password")


# Function to open the next page
def open_next_page():
    next_page = Toplevel(a1)
    next_page.geometry("400x300")
    next_page.title("ABOUT ME")
    next_page.configure(bg='light pink')

    Label(next_page, text="Name",bg='light pink',fg='Black').grid(row=0, column=0)
    name_z = Entry(next_page,bg='light pink',fg='black')
    name_z.grid(row=0, column=1)

    Label(next_page, text="Place",bg='light pink',fg='Black').grid(row=1, column=0)
    place_z = Combobox(next_page, values=["Chennai", "Trichy", "Coimbatore", "Madhurai"])
    place_z.grid(row=1, column=1)


    # Label(next_page, text="Degree").grid(row=2, column=0)
    # degree_entry = Entry(next_page)
    # degree_entry.grid(row=2, column=1)

    Label(next_page, text="Years Of Experience",bg='light pink',fg='Black').grid(row=3, column=0)
    experience_z= Spinbox(next_page, from_=0, to=50)
    experience_z.grid(row=3, column=1)

    Label(next_page, text="Gender",bg='light pink',fg='Black').grid(row=4, column=0)
    gender_z = StringVar()
    Radiobutton(next_page, text="Male", variable=gender_z, value="Male",bg='light pink').grid(row=4, column=1)
    Radiobutton(next_page, text="Female", variable=gender_z, value="Female",bg='light pink').grid(row=4, column=2)

    Label(next_page, text="Degree",bg='light pink',fg='Black').grid(row=5, column=0)
    hsc_z = BooleanVar()
    sslc_z = BooleanVar()
    diploma_z = BooleanVar()
    mca_z = BooleanVar()
    Checkbutton(next_page, text="HSC", variable=hsc_z).grid(row=5, column=1)
    Checkbutton(next_page, text="SSLC", variable=sslc_z).grid(row=6, column=1)
    Checkbutton(next_page, text="Diploma", variable=diploma_z).grid(row=7, column=1)
    Checkbutton(next_page, text="MCA", variable=mca_z).grid(row=8, column=1)

    Label(next_page, text="About Your Experience",bg='light pink',fg='Black').grid(row=9, column=0)
    abexperience_z = Text(next_page, height=5, width=30)
    abexperience_z.grid(row=9, column=1, columnspan=3)



    def summarize_details():
        name = name_z.get()
        place = place_z.get()
        experience = experience_z.get()
        gender = gender_z.get()
        qualifications = []
        if hsc_z.get():
            qualifications.append("HSC")
        if sslc_z.get():
            qualifications.append("SSLC")
        if diploma_z.get():
            qualifications.append("Diploma")
        if mca_z.get():
            qualifications.append("MCA")
        about_experience = abexperience_z.get("1.0", END).strip()

        

        summary = f"Name: {name}\nPlace: {place}\nYears of Experience: {experience}\nGender: {gender}\nQualifications: {', '.join(qualifications)}\nAbout Your Experience: {about_experience}"
        messagebox.showinfo("Summary", summary)

    Button(next_page, text="Save", command=summarize_details).grid(row=10, column=1)

Button(a1, text="Login",bg='gray' ,command=validate_login).grid(row=2, column=1)

a1.mainloop()
