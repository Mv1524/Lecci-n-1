import tkinter as tk
from tkinter import messagebox, ttk


class StudentManagerApp:
    def __init__(self, root):
        self.students = {}

        # Root window configuration
        root.title("Gestión de Calificaciones")
        root.geometry("800x600")
        root.configure(bg="#f7f7f7")

        # Title
        title = tk.Label(root, text="Gestión de Calificaciones", font=("Arial", 20, "bold"), bg="#4caf50", fg="white")
        title.pack(fill="x", pady=10)

        # Frame for inputs
        input_frame = tk.Frame(root, bg="#f7f7f7")
        input_frame.pack(pady=10, fill="x")

        tk.Label(input_frame, text="DNI", bg="#f7f7f7").grid(row=0, column=0, padx=5, pady=5)
        self.dni_entry = tk.Entry(input_frame)
        self.dni_entry.grid(row=0, column=1, padx=5, pady=5)

        tk.Label(input_frame, text="Apellidos", bg="#f7f7f7").grid(row=0, column=2, padx=5, pady=5)
        self.surname_entry = tk.Entry(input_frame)
        self.surname_entry.grid(row=0, column=3, padx=5, pady=5)

        tk.Label(input_frame, text="Nombre", bg="#f7f7f7").grid(row=1, column=0, padx=5, pady=5)
        self.name_entry = tk.Entry(input_frame)
        self.name_entry.grid(row=1, column=1, padx=5, pady=5)

        tk.Label(input_frame, text="Nota", bg="#f7f7f7").grid(row=1, column=2, padx=5, pady=5)
        self.grade_entry = tk.Entry(input_frame)
        self.grade_entry.grid(row=1, column=3, padx=5, pady=5)

        # Buttons
        button_frame = tk.Frame(root, bg="#f7f7f7")
        button_frame.pack(pady=10)

        tk.Button(button_frame, text="Agregar Alumno", command=self.add_student, bg="#4caf50", fg="white").grid(
            row=0, column=0, padx=5, pady=5)
        tk.Button(button_frame, text="Eliminar Alumno", command=self.delete_student, bg="#f44336", fg="white").grid(
            row=0, column=1, padx=5, pady=5)
        tk.Button(button_frame, text="Consultar Alumno", command=self.consult_student, bg="#03a9f4", fg="white").grid(
            row=0, column=2, padx=5, pady=5)
        tk.Button(button_frame, text="Modificar Nota", command=self.modify_grade, bg="#ff9800", fg="white").grid(
            row=0, column=3, padx=5, pady=5)
        tk.Button(button_frame, text="Mostrar Suspensos", command=self.show_failed, bg="#9c27b0", fg="white").grid(
            row=1, column=0, padx=5, pady=5)
        tk.Button(button_frame, text="Mostrar Aprobados", command=self.show_passed, bg="#607d8b", fg="white").grid(
            row=1, column=1, padx=5, pady=5)
        tk.Button(button_frame, text="Candidatos a MH", command=self.show_mh_candidates, bg="#795548", fg="white").grid(
            row=1, column=2, padx=5, pady=5)
        tk.Button(button_frame, text="Mostrar Todos", command=self.show_all, bg="#009688", fg="white").grid(
            row=1, column=3, padx=5, pady=5)

        # Text area for displaying information
        self.text_area = tk.Text(root, height=15, wrap="word", bg="#e8f5e9", fg="black", font=("Courier", 10))
        self.text_area.pack(pady=10, fill="both", expand=True)

    def calculate_qualification(self, grade):
        if grade < 5:
            return "SS"
        elif 5 <= grade < 7:
            return "AP"
        elif 7 <= grade < 9:
            return "NT"
        else:
            return "SB"

    def add_student(self):
        dni = self.dni_entry.get()
        surname = self.surname_entry.get()
        name = self.name_entry.get()
        try:
            grade = float(self.grade_entry.get())
        except ValueError:
            messagebox.showerror("Error", "La nota debe ser un número válido")
            return

        if dni in self.students:
            messagebox.showerror("Error", "El DNI ya existe en el sistema")
            return

        self.students[dni] = {
            "surname": surname,
            "name": name,
            "grade": grade,
            "qualification": self.calculate_qualification(grade)
        }
        messagebox.showinfo("Éxito", f"Alumno {name} agregado correctamente")
        self.clear_inputs()

    def delete_student(self):
        dni = self.dni_entry.get()
        if dni in self.students:
            del self.students[dni]
            messagebox.showinfo("Éxito", f"Alumno con DNI {dni} eliminado")
        else:
            messagebox.showerror("Error", "El DNI no existe en el sistema")
        self.clear_inputs()

    def consult_student(self):
        dni = self.dni_entry.get()
        student = self.students.get(dni)
        if student:
            self.text_area.delete(1.0, tk.END)
            self.text_area.insert(tk.END, f"DNI: {dni}\nApellidos: {student['surname']}\n"
                                          f"Nombre: {student['name']}\nNota: {student['grade']}\n"
                                          f"Calificación: {student['qualification']}\n")
        else:
            messagebox.showerror("Error", "El DNI no existe en el sistema")

    def modify_grade(self):
        dni = self.dni_entry.get()
        try:
            new_grade = float(self.grade_entry.get())
        except ValueError:
            messagebox.showerror("Error", "La nota debe ser un número válido")
            return

        if dni in self.students:
            self.students[dni]["grade"] = new_grade
            self.students[dni]["qualification"] = self.calculate_qualification(new_grade)
            messagebox.showinfo("Éxito", f"Nota modificada para el alumno con DNI {dni}")
        else:
            messagebox.showerror("Error", "El DNI no existe en el sistema")

    def show_all(self):
        self.text_area.delete(1.0, tk.END)
        for dni, student in self.students.items():
            self.text_area.insert(tk.END, f"{dni} {student['surname']}, {student['name']} "
                                          f"{student['grade']} {student['qualification']}\n")

    def show_failed(self):
        self.text_area.delete(1.0, tk.END)
        for dni, student in self.students.items():
            if student["grade"] < 5:
                self.text_area.insert(tk.END, f"{dni} {student['surname']}, {student['name']} "
                                              f"{student['grade']} {student['qualification']}\n")

    def show_passed(self):
        self.text_area.delete(1.0, tk.END)
        for dni, student in self.students.items():
            if student["grade"] >= 5:
                self.text_area.insert(tk.END, f"{dni} {student['surname']}, {student['name']} "
                                              f"{student['grade']} {student['qualification']}\n")

    def show_mh_candidates(self):
        self.text_area.delete(1.0, tk.END)
        for dni, student in self.students.items():
            if student["grade"] == 10:
                self.text_area.insert(tk.END, f"{dni} {student['surname']}, {student['name']} "
                                              f"{student['grade']} {student['qualification']}\n")

    def clear_inputs(self):
        self.dni_entry.delete(0, tk.END)
        self.surname_entry.delete(0, tk.END)
        self.name_entry.delete(0, tk.END)
        self.grade_entry.delete(0, tk.END)


if __name__ == "__main__":
    root = tk.Tk()
    app = StudentManagerApp(root)
    root.mainloop()
