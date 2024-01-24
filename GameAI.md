import tkinter as tk
from tkinter import messagebox

class QuizApp:
    def __init__(self, master):
        self.master = master
        self.master.title("Human Or AI")
        self.master.geometry("400x300")
        self.master.configure(bg='#3498db')

        self.questions = [
            {"question": "Climate change is an increasing problem that we need to take serious action on.", "options": ["Human", "AI"], "correct_option": "Human"},
            {"question": "Water scarcity may not seem like a big problem but if we dont take action and save water soon we'll run out.", "options": ["Human", "AI"], "correct_option": "Human"},
            {"question": "Burning fossil fuels, such as coal and oil, harms the environment by emitting harmful gases.", "options": ["Human", "AI"], "correct_option": "AI"},
            {"question": "Plastic pollution harms oceans, affecting marine life and ecosystems, demanding urgent attention for solutions.", "options": ["Human", "AI"], "correct_option": "AI"},
            {"question": "Deforestation is when humans cut trees to create items for their comfort, due to the mass deduction of trees the earth is being affected.", "options": ["Human", "AI"], "correct_option": "Human"}
        ]

        self.current_question_index = 0
        self.score = 0

        self.setup_ui()
        self.display_question()

    def setup_ui(self):
        self.question_label = tk.Label(self.master, text="", font=("Helvetica", 25), bg='#3498db', fg='#ffffff', wraplength=350)
        self.question_label.pack(pady=10)

        self.option_buttons = []
        for i in range(2):
            button = tk.Button(self.master, text="", command=lambda i=i: self.check_answer(i),
                               bg='#2ecc71', fg='#ffffff', activebackground='#27ae60', height=4, width=30, font=("Helvetica",30 ))
            button.pack(pady=20)  # Increase the pady for more spacing
            self.option_buttons.append(button)

    def display_question(self):
        current_question = self.questions[self.current_question_index]
        self.question_label.config(text=current_question["question"])

        for i, option in enumerate(current_question["options"]):
            self.option_buttons[i].config(text=option)

    def check_answer(self, selected_option_index):
        current_question = self.questions[self.current_question_index]
        correct_option_index = current_question["options"].index(current_question["correct_option"])

        if selected_option_index == correct_option_index:
            self.score += 1

        self.current_question_index += 1

        if self.current_question_index < len(self.questions):
            self.display_question()
        else:
            self.quiz_complete()

    def quiz_complete(self):
        messagebox.showinfo("Quiz Complete", f"Your score: {self.score}/{len(self.questions)}")
        self.reset_quiz()

    def reset_quiz(self):
        self.current_question_index = 0
        self.score = 0
        self.display_question()

if __name__ == "__main__":
    root = tk.Tk()
    app = QuizApp(root)
    root.mainloop()
