from tkinter import *
from tkinter import messagebox
from tkinter.ttk import Combobox

# Function for hover effect
def on_enter(button):
    button['bg'] = 'lightblue'

def on_leave(button):
    button['bg'] = 'blue'

def change_to_black(button):
    button['fg'] = 'black'

# Function to open the next page
def open_next_page():
    next_page = Toplevel(a1)
    next_page.geometry("600x500")
    next_page.title("ABOUT ME")
    next_page.configure(bg='blue')

    Label(next_page, text="Tell us more about yourself", font=("Arial", 14, "bold"), bg='blue', fg='white').grid(row=0, column=0, columnspan=3, pady=10)

    # Name
    Label(next_page, text="Name", bg='blue', fg='white').grid(row=1, column=0, padx=10, pady=5)
    name_z = Entry(next_page)
    name_z.grid(row=1, column=1)

    # Date of Birth
    Label(next_page, text="Date of Birth", bg='blue', fg='white').grid(row=2, column=0, padx=10, pady=5)
    dob_day = Spinbox(next_page, from_=1, to=31, width=4)
    dob_day.grid(row=2, column=1)
    dob_month = Spinbox(next_page, from_=1, to=12, width=4)
    dob_month.grid(row=2, column=2)
    dob_year = Spinbox(next_page, from_=1950, to=2024, width=6)
    dob_year.grid(row=2, column=3)

    # Place
    Label(next_page, text="Place", bg='blue', fg='white').grid(row=3, column=0, padx=10, pady=5)
    place_z = Combobox(next_page, values=["Chennai", "Trichy", "Coimbatore", "Madurai", "Salem", "Tirunelveli",
                                          "Erode", "Vellore", "Thanjavur", "Kanyakumari", "Tiruppur",
                                          "Dharmapuri", "Karur", "Namakkal", "Pudukottai", "Cuddalore", "Dindigul"])
    place_z.grid(row=3, column=1)

    # Years of Experience
    Label(next_page, text="Years Of Experience", bg='blue', fg='white').grid(row=4, column=0, padx=10, pady=5)
    experience_z = Spinbox(next_page, from_=0, to=50)
    experience_z.grid(row=4, column=1)

    # Gender Selection
    Label(next_page, text="Gender", bg='blue', fg='white').grid(row=5, column=0, padx=10, pady=5)
    gender_z = StringVar(value="Male")  # Default value
    male_button = Radiobutton(next_page, text="Male", variable=gender_z, value="Male", bg='blue', fg='white', command=lambda: change_to_black(male_button))
    male_button.grid(row=5, column=1, sticky='w')
    female_button = Radiobutton(next_page, text="Female", variable=gender_z, value="Female", bg='blue', fg='white', command=lambda: change_to_black(female_button))
    female_button.grid(row=5, column=2, sticky='w')
    other_button = Radiobutton(next_page, text="Other", variable=gender_z, value="Other", bg='blue', fg='white', command=lambda: change_to_black(other_button))
    other_button.grid(row=5, column=3, sticky='w')

    # Add hover effect
    for button in [male_button, female_button, other_button]:
        button.bind("<Enter>", lambda e, btn=button: on_enter(btn))
        button.bind("<Leave>", lambda e, btn=button: on_leave(btn))

    # Degree Section
    Label(next_page, text="Degree", bg='blue', fg='white').grid(row=6, column=0, padx=10, pady=5)
    degrees = {
        "HSC": BooleanVar(),
        "SSLC": BooleanVar(),
        "Diploma": BooleanVar(),
        "B.Sc": BooleanVar(),
        "MCA": BooleanVar(),
        "B.Tech": BooleanVar(),
        "MBA": BooleanVar(),
    }

    # Using Checkbuttons for Degrees
    for i, (degree, var) in enumerate(degrees.items()):
        checkbutton = Checkbutton(next_page, text=degree, variable=var, bg='blue', fg='white')
        checkbutton.grid(row=6 + i, column=1, sticky='w')

        # Capture the current checkbutton in the lambda function
        checkbutton.config(command=lambda cb=checkbutton: change_to_black(cb))

        # Add hover effect
        checkbutton.bind("<Enter>", lambda e, btn=checkbutton: on_enter(btn))
        checkbutton.bind("<Leave>", lambda e, btn=checkbutton: on_leave(btn))

    # University
    Label(next_page, text="University", bg='blue', fg='white').grid(row=13, column=0, padx=10, pady=5)
    university_z = Entry(next_page)
    university_z.grid(row=13, column=1)

    # About Experience
    Label(next_page, text="About Your Experience", bg='blue', fg='white').grid(row=14, column=0, padx=10, pady=5)
    abexperience_z = Text(next_page, height=5, width=40)
    abexperience_z.grid(row=14, column=1, columnspan=3)

    def summarize_details():
        name = name_z.get().strip()
        dob = f"{dob_day.get()}/{dob_month.get()}/{dob_year.get()}"
        place = place_z.get().strip()
        experience = experience_z.get()
        gender = gender_z.get()
        qualifications = [degree for degree, var in degrees.items() if var.get()]
        university = university_z.get().strip()
        about_experience = abexperience_z.get("1.0", END).strip()

        if not name or not place or not gender or not university:
            messagebox.showwarning("Incomplete Information", "Please fill all the required fields.")
        else:
            summary = (f"Name: {name}\nDate of Birth: {dob}\nPlace: {place}\n"
                       f"Years of Experience: {experience}\nGender: {gender}\n"
                       f"Qualifications: {', '.join(qualifications)}\n"
                       f"University: {university}\nAbout Your Experience: {about_experience}")
            messagebox.showinfo("Summary", summary)

    Button(next_page, text="Save", command=summarize_details, bg='green', fg='white', padx=10, pady=5).grid(row=15, column=1, pady=10)
    Button(next_page, text="Clear", command=lambda: [name_z.delete(0, END), place_z.set(""), abexperience_z.delete("1.0", END)], bg='red', fg='white', padx=10, pady=5).grid(row=15, column=2, pady=10)

# Main window
a1 = Tk()
a1.title("FreeFolks")
a1.geometry("400x200")
a1.configure(bg='orange')

# Custom welcome label
welcome_label = Label(a1, text="Welcome to FreeFolks", font=("Arial", 16, "bold"), bg='orange', fg='white')
welcome_label.grid(row=0, column=0, columnspan=2, pady=10)

# Username label and entry
Label(a1, text="Username", bg='orange', fg='black').grid(row=1, column=0, padx=10, pady=5)
username_entry = Entry(a1)
username_entry.grid(row=1, column=1, padx=10)

# Password label and entry
Label(a1, text="Password", bg='orange', fg='black').grid(row=2, column=0, padx=10, pady=5)
password_entry = Entry(a1, show='*')
password_entry.grid(row=2, column=1, padx=10)

# Function to validate login credentials
def validate_login():
    username = username_entry.get().strip()
    password = password_entry.get().strip()
    if username == "Member" and password == "0987":
        messagebox.showinfo("Login Successful", "Welcome, Folks!")
        open_next_page()
    else:
        messagebox.showerror("Login Failed", "Invalid username or password")

# Function to clear the form
def clear_form():
    username_entry.delete(0, END)
    password_entry.delete(0, END)

Button(a1, text="Login", bg='gray', fg='white', command=validate_login).grid(row=3, column=0, pady=10, padx=10)
Button(a1, text="Clear", bg='red', fg='white', command=clear_form).grid(row=3, column=1, pady=10, padx=10)

a1.mainloop()
