import tkinter as tk
from tkinter import messagebox

# Funciones para operaciones básicas
def add(x, y):
    return x + y

def subtract(x, y):
    return x - y

def multiply(x, y):
    return x * y

def divide(x, y):
    if y == 0:
        messagebox.showerror("Error", "¡No puedes dividir por cero!")
        return None
    return x / y

def calculate():
    try:
        # Obtener la expresión de la pantalla
        expression = screen.get()
        # Evaluar la expresión
        result = eval(expression)
        screen.delete(0, tk.END)  # Limpiar la pantalla
        screen.insert(tk.END, str(result))  # Mostrar el resultado
    except Exception as e:
        messagebox.showerror("Error", "Hubo un problema con la expresión.")
        screen.delete(0, tk.END)  # Limpiar la pantalla

# Función para manejar los clics de los botones
def on_button_click(text):
    if text == "C":
        screen.delete(0, tk.END)  # Limpiar la pantalla
    elif text == "=":
        calculate()  # Calcular el resultado
    else:
        screen.insert(tk.END, text)  # Agregar el texto del botón a la pantalla

# Crear la ventana principal
root = tk.Tk()
root.title("Calculadora Simple")

# Crear la pantalla de entrada
screen = tk.Entry(root, borderwidth=2, relief="solid", font=("Arial", 16))
screen.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

# Crear los botones
buttons = [
    '7', '8', '9', '/',
    '4', '5', '6', '*',
    '1', '2', '3', '-',
    '0', '.', '=', '+',
    'C'
]

# Agregar los botones a la ventana
row = 1
col = 0
for button_text in buttons:
    button = tk.Button(root, text=button_text, width=5, height=2, font=("Arial", 14),
                       command=lambda text=button_text: on_button_click(text))
    button.grid(row=row, column=col, padx=5, pady=5)
    col += 1
    if col > 3:
        col = 0
        row += 1

# Ejecutar la ventana
root.mainloop()
