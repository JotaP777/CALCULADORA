# CALCULADORA
CALCULADORA
import tkinter as tk
import re

def clicar(botao):
    entrada_var.set(entrada_var.get() + str(botao))

def limpar():
    entrada_var.set("")

def calcular():
    expr = entrada_var.get()
    try:
        # remove zeros à esquerda em números inteiros (ex: 05 -> 5)
        expr = re.sub(r'\b0+(\d)', r'\1', expr)
        resultado = eval(expr)
        entrada_var.set(str(resultado))
    except ZeroDivisionError:
        entrada_var.set("Divisão por 0")
    except:
        entrada_var.set("Erro")

# Janela
janela = tk.Tk()
janela.title("Calculadora")
entrada_var = tk.StringVar()

entrada = tk.Entry(janela, textvariable=entrada_var, font=("Arial", 20), bd=10, relief="ridge", justify="right")
entrada.grid(row=0, column=0, columnspan=4, ipadx=8, ipady=8)

botoes = [
    ("7",1,0),("8",1,1),("9",1,2),("/",1,3),
    ("4",2,0),("5",2,1),("6",2,2),("*",2,3),
    ("1",3,0),("2",3,1),("3",3,2),("-",3,3),
    ("0",4,0),(".",4,1),("=",4,2),("+",4,3),
]

for (t,l,c) in botoes:
    cmd = calcular if t=="=" else lambda x=t: clicar(x)
    tk.Button(janela,text=t,width=5,height=2,font=("Arial",18),command=cmd)\
        .grid(row=l,column=c,padx=5,pady=5)

tk.Button(janela,text="C",width=5,height=2,font=("Arial",18),
          command=limpar).grid(row=5,column=0,columnspan=4,sticky="we",padx=5,pady=5)

janela.mainloop()
