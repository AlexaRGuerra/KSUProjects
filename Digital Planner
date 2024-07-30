import calendar
import tkinter as tk
from tkinter import ttk, messagebox, simpledialog

class DigitalPlanner:
    def __init__(self):
        self.calendar = calendar.Calendar()
        self.tasks = {}
    
    def add_task(self, date, task):
        if date not in self.tasks:
            self.tasks[date] = []
        self.tasks[date].append(task)
    
    def remove_task(self, date, task):
        if date in self.tasks:
            if task in self.tasks[date]:
                self.tasks[date].remove(task)
                if len(self.tasks[date]) == 0:
                    del self.tasks[date]
    
    def display_tasks(self, date):
        if date in self.tasks:
            tasks = f"Tasks for {date}:\n"
            for i, task in enumerate(self.tasks[date], 1):
                tasks += f"{i}. {task}\n"
            return tasks
        else:
            return f"No tasks found for {date}."

    def display_calendar(self, year, month):
        cal = self.calendar.monthdayscalendar(year, month)
        header = calendar.month_name[month] + " " + str(year)

        # Create a new window to display the calendar
        calendar_window = tk.Toplevel()
        calendar_window.title("Calendar")

        # Create a Treeview widget to display the calendar
        tree = ttk.Treeview(calendar_window, columns=[str(i) for i in range(7)], show='headings')

        # Set column headings for weekdays
        for i, day in enumerate(calendar.day_name):
            tree.heading(str(i), text=day)

        # Insert calendar data into the Treeview widget
        for week in cal:
            tree.insert('', 'end', values=[str(day) if day != 0 else '' for day in week])

        # Pack the Treeview widget
        tree.pack()
    
    def clear_tasks(self):
        self.tasks = {}


class Authentication:
    def __init__(self):
        self.users = {}

    def register(self):
        while True:
            username = simpledialog.askstring("Registration", "Enter a username:")
            if username in self.users:
                messagebox.showerror("Registration", "Username already exists. Please choose a different username.")
            else:
                password = simpledialog.askstring("Registration", "Enter a password:")
                self.users[username] = password
                messagebox.showinfo("Registration", "Registration successful!")
                return

    def login(self):
        while True:
            username = simpledialog.askstring("Login", "Enter your username:")
            password = simpledialog.askstring("Login", "Enter your password:")

            if self.validate_credentials(username, password):
                messagebox.showinfo("Login", "Login successful!")
                return True
            else:
                messagebox.showerror("Login", "Invalid username or password!")
                choice = messagebox.askquestion("Try Again?", "Do you want to try again?")
                if choice.lower() != "yes":
                    return False

    def validate_credentials(self, username, password):
        if username in self.users and self.users[username] == password:
            return True
        else:
            return False


def show_main_menu():
    root.withdraw()  # Hide the main registration window
    main_menu_window = tk.Toplevel(root)
    main_menu_window.title("Digital Planner Menu")

    def display_calendar():
        year = int(year_entry.get())
        month = int(month_entry.get())
        planner.display_calendar(year, month)

    def add_task():
        date = date_entry.get()
        task = task_entry.get()
        planner.add_task(date, task)
        messagebox.showinfo("Task Added", "Task added successfully!")

    def display_tasks():
        date = date_entry.get()
        tasks = planner.display_tasks(date)
        tasks_text.delete(1.0, tk.END)  # Clear previous entries
        tasks_text.insert(tk.END, tasks)

    def back_to_registration():
        main_menu_window.withdraw()  # Hide the current window
        root.deiconify()  # Show the main registration page

    # Create labels, entries, and buttons for menu options using grid layout
    year_label = tk.Label(main_menu_window, text="Enter the year:")
    year_label.grid(row=0, column=0, padx=10, pady=10)
    year_entry = tk.Entry(main_menu_window)
    year_entry.grid(row=0, column=1, padx=10, pady=10)

    month_label = tk.Label(main_menu_window, text="Enter the month (1-12):")
    month_label.grid(row=1, column=0, padx=10, pady=10)
    month_entry = tk.Entry(main_menu_window)
    month_entry.grid(row=1, column=1, padx=10, pady=10)

    display_calendar_button = tk.Button(main_menu_window, text="Display Calendar", command=display_calendar)
    display_calendar_button.grid(row=2, column=0, columnspan=2, padx=10, pady=10)

    date_label = tk.Label(main_menu_window, text="Enter the date (YYYY-MM-DD):")
    date_label.grid(row=3, column=0, padx=10, pady=10)
    date_entry = tk.Entry(main_menu_window)
    date_entry.grid(row=3, column=1, padx=10, pady=10)

    task_label = tk.Label(main_menu_window, text="Enter the task:")
    task_label.grid(row=4, column=0, padx=10, pady=10)
    task_entry = tk.Entry(main_menu_window)
    task_entry.grid(row=4, column=1, padx=10, pady=10)

    add_task_button = tk.Button(main_menu_window, text="Add Task", command=add_task)
    add_task_button.grid(row=5, column=0, columnspan=2, padx=10, pady=10)

    display_tasks_button = tk.Button(main_menu_window, text="Display Tasks", command=display_tasks)
    display_tasks_button.grid(row=6, column=0, columnspan=2, padx=10, pady=10)

    tasks_text = tk.Text(main_menu_window, width=40, height=10)
    tasks_text.grid(row=7, column=0, columnspan=2, padx=10, pady=10)

    clear_tasks_button = tk.Button(main_menu_window, text="Clear All Tasks", command=planner.clear_tasks)
    clear_tasks_button.grid(row=8, column=0, columnspan=2, padx=10, pady=10)

    back_button = tk.Button(main_menu_window, text="Back to Registration", command=back_to_registration)
    back_button.grid(row=10, column=0, columnspan=2, padx=10, pady=10)

# Create a Tkinter window
root = tk.Tk()
root.title("Digital Planner")

authentication = Authentication()
planner = DigitalPlanner()

def register():
    authentication.register()
    messagebox.showinfo("Registration", "Registration successful!")

def login():
    if authentication.login():
        show_main_menu()

# Create labels and buttons for the initial menu
welcome_label = tk.Label(root, text="Welcome to Digital Planner!", font=("Helvetica", 16))
welcome_label.pack(pady=20)

register_button = tk.Button(root, text="Register", command=register)
register_button.pack()

login_button = tk.Button(root, text="Login", command=login)
login_button.pack()

exit_button = tk.Button(root, text="Exit", command=root.quit)
exit_button.pack()

# Start the Tkinter event loop
root.mainloop()
