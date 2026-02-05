import tkinter as tk

# Janela principal
janela = tk.Tk()
janela.title("Calculadora")
janela.geometry("300x400")
janela.resizable(False, False)

# Campo de texto
entrada = tk.Entry(janela, font=("Arial", 20), borderwidth=5, relief="ridge", justify="right")
entrada.pack(fill="both", padx=10, pady=10)

# Funções
def clicar(valor):
    entrada.insert(tk.END, valor)

def limpar():
    entrada.delete(0, tk.END)

def calcular():
    try:
        resultado = eval(entrada.get())
        entrada.delete(0, tk.END)
        entrada.insert(0, resultado)
    except:
        entrada.delete(0, tk.END)
        entrada.insert(0, "Erro")

# Frame dos botões
frame = tk.Frame(janela)
frame.pack()

botoes = [
    '7','8','9','/',
    '4','5','6','*',
    '1','2','3','-',
    '0','.','=','+'
]

linha = 0
coluna = 0

for botao in botoes:
    acao = lambda x=botao: clicar(x) if x != "=" else calcular()
    b = tk.Button(frame, text=botao, width=5, height=2, font=("Arial", 16), command=acao)
    b.grid(row=linha, column=coluna, padx=5, pady=5)
    coluna += 1
    if coluna > 3:
        coluna = 0
        linha += 1

# Botão limpar
btn_limpar = tk.Button(janela, text="C", width=22, height=2, font=("Arial", 14), command=limpar)
btn_limpar.pack(pady=5)

# Loop principal
janela.mainloop()
