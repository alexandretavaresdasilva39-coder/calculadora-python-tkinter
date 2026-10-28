# calculadora-python-tkinter
calculadora simples com código que roda fácil.


import tkinter as tk

def clique_botao(valor):
    atual = visor.get()
    visor.delete(0, tk.END)
    visor.insert(0, atual + str(valor))

def limpar():
    visor.delete(0, tk.END)

def calcular():
    try:
        expressao = visor.get()
    
        expressao = expressao.replace('×', '*').replace('÷', '/')
        resultado = eval(expressao)
        visor.delete(0, tk.END)
        visor.insert(0, str(resultado))
    except ZeroDivisionError:
        visor.delete(0, tk.END)
        visor.insert(0, "Erro: Divisão por 0")
    except Exception:
        visor.delete(0, tk.END)
        visor.insert(0, "Erro")


janela = tk.Tk()
janela.title("Calculadora")
janela.geometry("300x420")
janela.resizable(False, False)


visor = tk.Entry(janela, font=("Arial", 22), justify="right", bd=8, relief=tk.FLAT)
visor.grid(row=0, column=0, columnspan=4, padx=10, pady=15, ipady=10, sticky="nsew")


botoes = [
    ('C', 1, 0), ('÷', 1, 1), ('×', 1, 2), ('-', 1, 3),
    ('7', 2, 0), ('8', 2, 1), ('9', 2, 2), ('+', 2, 3),
    ('4', 3, 0), ('5', 3, 1), ('6', 3, 2), ('=', 3, 3),
    ('1', 4, 0), ('2', 4, 1), ('3', 4, 2), 
    ('0', 5, 0)
]

for texto, linha, coluna in botoes:
    if texto == '=':
        btn = tk.Button(janela, text=texto, font=("Arial", 14, "bold"), bg="#4CAF50", fg="white",
                        command=calcular)
        btn.grid(row=linha, column=coluna, rowspan=2, sticky="nsew", padx=3, pady=3)
    elif texto == 'C':
        btn = tk.Button(janela, text=texto, font=("Arial", 14, "bold"), bg="#f44336", fg="white",
                        command=limpar)
        btn.grid(row=linha, column=coluna, sticky="nsew", padx=3, pady=3)
    elif texto == '0':
        btn = tk.Button(janela, text=texto, font=("Arial", 14), bg="#e0e0e0",
                        command=lambda t=texto: clique_botao(t))
        btn.grid(row=linha, column=coluna, columnspan=3, sticky="nsew", padx=3, pady=3)
    elif texto in ['+', '-', '×', '÷', '.']:
        btn = tk.Button(janela, text=texto, font=("Arial", 14, "bold"), bg="#ff9800", fg="white",
                        command=lambda t=texto: clique_botao(t))
        btn.grid(row=linha, column=coluna, sticky="nsew", padx=3, pady=3)
    else:
        btn = tk.Button(janela, text=texto, font=("Arial", 14), bg="#f5f5f5",
                        command=lambda t=texto: clique_botao(t))
        btn.grid(row=linha, column=coluna, sticky="nsew", padx=3, pady=3)


for i in range(6):
    janela.rowconfigure(i, weight=1)
for i in range(4):
    janela.columnconfigure(i, weight=1)

janela.mainloop()


https://github.com/user-attachments/assets/e4a60e6f-20c6-4015-a17f-d70bd9a04b8e

