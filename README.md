# Projetando-Uma-Aplica-o-Desktop
Projetando uma aplicação desktop - Missão Certificação nivel 5
import tkinter as tk
from tkinter import ttk
import datetime as dt
import pandas as pd

# ==================================================================================================

#data = dt.datetime.today()
#data = data.strftime("%d/%m/%Y %H:%M")
#data_post = data

# ==================================================================================================

janela = tk.Tk()
janela.title('Sistema de Ferramentas')
janela.geometry()
#"650x350"
global Qi
Qi=1
# ==================================== Cadastrar_Ferramentas =======================================
def Cadastrar_Ferramentas():
    import tkinter as tk
    from tkinter import ttk
    import datetime as dt
    import pandas as pd
    # ==============================================================================================

    data = dt.datetime.today()
    #data = data.strftime("%d%m%Y %H:%M")
    data = data.strftime("%d%m%Y")
    data_post = data
    data_post = int(data)

    print(type(data))
    print(type(data_post))
    print(data_post)

    # Criando Janela:

    janela2 = tk.Tk()
    janela2.title('Cadastro de Ferramentas')
    janela2.geometry()
    # "650x350"
    global Nindex
    global Nome
    global Fabricante
    global PN_Mod
    global Tamanho
    global rpm
    global Mat_de_Compos
    global tipo_ferr
    global unimed
    # --------------------------------Verificando se tem arquivo----------------------
    try:
        x = pd.read_csv('Cadastro_Ferr.csv')
        x.to_csv('Cadastro_Ferr.csv', index = False)
        x.to_excel('Cadastro_Ferr.xlsx', index=False)
    except:
        Nome = Fabricante = PN_Mod = Tamanho = rpm = Mat_de_Compos = tipo_ferr = unimed = []

        lN = len(Nome)
        Nindex = []
        for a in range(1, lN + 1):
            Nindex = Nindex + [a]

        Cad_Ferram = {'Nindex': Nindex, 'Nome': Nome, 'Fabricante': Fabricante,
                      'PN_Mod': PN_Mod, 'Tamanho': Tamanho, 'rpm': rpm, 'Mat_de_Compos': Mat_de_Compos,
                      'tipo_ferr': tipo_ferr, 'unimed': unimed}
        print(Cad_Ferram)

        Cadastro = pd.DataFrame(data=Cad_Ferram)

        Cadastro.to_csv('Cadastro_Ferr.csv', index = False)
        Cadastro.to_excel('Cadastro_Ferr.xlsx', index = False)

        x = pd.read_csv('Cadastro_Ferr.csv')

    #print(x)

    # ---------------- converter de objeto tabela devolta pra lista  --------------------
    lN = len(x['Nome'])

    Nome = Fabricante = PN_Mod = Tamanho = rpm = Mat_de_Compos = tipo_ferr = unimed = []

    for a in range(0, lN):
        Nome = Nome + [x['Nome'][a]]
        Fabricante = Fabricante + [x['Fabricante'][a]]
        PN_Mod = PN_Mod + [x['PN_Mod'][a]]
        Tamanho = Tamanho + [x['Tamanho'][a]]
        rpm = rpm + [x['rpm'][a]]
        Mat_de_Compos = Mat_de_Compos + [x['Mat_de_Compos'][a]]
        tipo_ferr = tipo_ferr + [x['tipo_ferr'][a]]
        unimed = unimed + [x['unimed'][a]]

    # _________________________________ Cadastramento _______________________________
    def cadastrar_ferramenta():
        NomeN = locals()
        global Nindex, Nome, Fabricante, PN_Mod, Tamanho, rpm, Mat_de_Compos, tipo_ferr, unimed
        NomeN = entry_Nome.get()
        if NomeN != "":
            Nome = Nome + [NomeN]
            Fabricante = Fabricante + [entry_Fabricante.get()]
            PN_Mod = PN_Mod + [entry_PN_Mod.get()]
            Tamanho = Tamanho + [entry_Tamanho.get()]
            rpm = rpm + [entry_rpm.get()]
            Mat_de_Compos = Mat_de_Compos + [entry_Mat_de_Compos.get()]
            tipo_ferr = tipo_ferr + [combobox_tipo_ferr.get()]
            unimed = unimed + [combobox_unimed.get()]
            lN = len(Nome)
            Nindex = []
            for a in range(1, lN + 1):
                Nindex = Nindex + [a]
            #print(Nindex)
            Cad_Ferram = {'Nindex': Nindex, 'Nome': Nome, 'Fabricante': Fabricante,
                          'PN_Mod': PN_Mod, 'Tamanho': Tamanho, 'rpm': rpm, 'Mat_de_Compos': Mat_de_Compos,
                          'tipo_ferr': tipo_ferr, 'unimed': unimed}
            #print(Cad_Ferram)

            Cadastro = pd.DataFrame(data=Cad_Ferram)

            Cadastro.to_csv('Cadastro_Ferr.csv', index = False)
            Cadastro.to_excel('Cadastro_Ferr.xlsx', index = False)

            #print(Cadastro)

    # ****************************************************************************

    def apagar_valores():
        # #Apaga os valores das caixas de entrada
        entry_Nome.delete(0, "end")
        entry_Fabricante.delete(0, "end")
        entry_PN_Mod.delete(0, "end")
        entry_Tamanho.delete(0, "end")
        entry_rpm.delete(0, "end")
        entry_Mat_de_Compos.delete(0, "end")
        combobox_tipo_ferr.delete(0, "end")
        combobox_unimed.delete(0, "end")

    # ****************************************************************************
    '''
    def Voltar_tela_inicial():
        return
        janela.title('Tela Inicial')
        janela.geometry()

        for CLS in range(0, 8):
            label_Nome = tk.Label(janela2, text='  ' * 600)
            label_Nome.grid(row=CLS, column=0, padx=0, pady=0)
        for CLS in range(0, 8):
            label_Nome = tk.Label(janela2, text='  ' * 600)
            label_Nome.grid(row=CLS, column=1, padx=0, pady=0)

        print('telainicial')
    '''
    # ***************************  Variáveis combo BOX  ****************************

    lista_tipo_ferr = ['110v', '220v', "Bivolt", 'Bateria', 'Manual', 'Mecânica']
    lista_unimed = ['Centimetros - Cm', 'Polegadas - inch']

    # ***************************   Rótulos Entradas *******************************

    label_Nome = tk.Label(janela2, text=' "Nome" Descrição da Ferramenta ')
    label_Nome.grid(row=0, column=0, sticky="e", padx=10, pady=10)

    label_Fabricante = tk.Label(janela2, text=' Fabricante ')
    label_Fabricante.grid(row=1, column=0, sticky="e", padx=10, pady=10, )

    label_PN_Mod = tk.Label(janela2, text=' P/Number/Modelo ')
    label_PN_Mod.grid(row=2, column=0, sticky="e", padx=10, pady=10)

    label_Tamanho = tk.Label(janela2, text=' Tamanho ')
    label_Tamanho.grid(row=3, column=0, sticky="e", padx=10, pady=10)

    label_rpm = tk.Label(janela2, text=' rpm ')
    label_rpm.grid(row=4, column=0, sticky="e", padx=10, pady=10)

    label_Mat_de_Compos = tk.Label(janela2, text=' Material de Composição da Ferramenta ')
    label_Mat_de_Compos.grid(row=5, column=0, sticky="e", padx=10, pady=10)

    # Caixas Entradas:

    entry_Nome = tk.Entry(janela2, width=60)
    entry_Nome.grid(row=0, column=1, sticky="w", padx=10, pady=10)

    entry_Fabricante = tk.Entry(janela2, width=30)
    entry_Fabricante.grid(row=1, column=1, sticky="w", padx=10, pady=10)

    entry_PN_Mod = tk.Entry(janela2, width=25)
    entry_PN_Mod.grid(row=2, column=1, sticky="w", padx=10, pady=10)

    entry_Tamanho = tk.Entry(janela2, width=20)
    entry_Tamanho.grid(row=3, column=1, sticky="w", padx=10, pady=10)

    entry_rpm = tk.Entry(janela2, width=20)
    entry_rpm.grid(row=4, column=1, sticky="w", padx=10, pady=10)

    entry_Mat_de_Compos = tk.Entry(janela2, width=20)
    entry_Mat_de_Compos.grid(row=5, column=1, sticky="w", padx=10, pady=10)

    # Combo Box - Tipo de ferramenta

    combobox_tipo_ferr = ttk.Combobox(janela2,values=lista_tipo_ferr)
    combobox_tipo_ferr.grid(row=2, column=1, sticky="e", padx=10, pady=10)

    # Combo Box - Unidade de medida

    combobox_unimed = ttk.Combobox(janela2,values=lista_unimed)
    combobox_unimed.grid(row=3, column=1, sticky="e", padx=10, pady=10)

    # Botão de Cadastrar

    botao_cadastrar = tk.Button(janela2,text='Cadastrar Ferramenta', command=cadastrar_ferramenta)
    botao_cadastrar.grid(row=7, column=1, columnspan=2, sticky="e", padx=10, pady=10, ipadx=70)

    # Botão de Sair voltar tela inicial

    botao_Sair = tk.Button(janela2,text='Encerrar esta janela', command=janela2.destroy)
    botao_Sair.grid(row=6, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=60)

    # Botão de Apagar

    botao_Apagar = tk.Button(janela2,text='Limpar', command=apagar_valores)
    botao_Apagar.grid(row=6, column=1, columnspan=2, sticky="e", padx=10, pady=10, ipadx=35)

    janela2.mainloop()
# =========================== FIM === Cadastrar_Ferramentas === FIM ================================
# ==================================== Consulta_de_Ferramentas =====================================
def Consulta_de_Ferramentas():
    import tkinter as tk
    from tkinter import ttk
    import pandas as pd
    # ==============================================================================================
    '''
    global Nome
    global Fabricante
    global PN_Mod
    global Tamanho
    global rpm
    global Mat_de_Compos
    global tipo_ferr
    global unimed
    '''
    # ==============================================================================================
    try:
        x = pd.read_excel('Cadastro_Ferr.xlsx')

        # x = pd.read_csv('Cadastro_Ferr.csv', encoding='utf-8')
    except:
        Nome = Fabricante = PN_Mod = Tamanho = rpm = Mat_de_Compos = tipo_ferr = unimed = []

        lN = len(Nome)
        Nindex = []
        for a in range(1, lN + 1):
            Nindex = Nindex + [a]

        Cad_Ferram = {'Nindex': Nindex, 'Nome': Nome, 'Fabricante': Fabricante,
                      'PN_Mod': PN_Mod, 'Tamanho': Tamanho, 'rpm': rpm, 'Mat_de_Compos': Mat_de_Compos,
                      'tipo_ferr': tipo_ferr, 'unimed': unimed}
        # print(Cad_Ferram)

        Cadastro = pd.DataFrame(data=Cad_Ferram)

        Cadastro.to_csv('Cadastro_Ferr.csv', index=False)
        Cadastro.to_excel('Cadastro_Ferr.xlsx', index=False)

        x = pd.read_excel('Cadastro_Ferr.xlsx')
        # x = pd.read_csv('Cadastro_Ferr.csv')
        # x.dropna(axis=0, how='all')
    # ==================================================================================================

    janela3 = tk.Tk()
    janela4 = tk.Tk()

    global Qi
    Qi = 1
    global bi, bf, Q, Pag

    # ---------------- converter de objeto tabela devolta pra lista  --------------------

    lN = len(x['Nome'])
    print(lN)
    Nome = Fabricante = PN_Mod = Tamanho = rpm = Mat_de_Compos = tipo_ferr = unimed = []

    for a in range(0, lN):
        Nome = Nome + [x['Nome'][a]]
        Fabricante = Fabricante + [x['Fabricante'][a]]
        PN_Mod = PN_Mod + [x['PN_Mod'][a]]
        Tamanho = Tamanho + [x['Tamanho'][a]]
        rpm = rpm + [x['rpm'][a]]
        Mat_de_Compos = Mat_de_Compos + [x['Mat_de_Compos'][a]]
        tipo_ferr = tipo_ferr + [x['tipo_ferr'][a]]
        unimed = unimed + [x['unimed'][a]]

        lN = len(Nome)
        Nindex = []
        for a in range(1, lN + 1):
            Nindex = Nindex + [a]
        print(Nindex)

    Cad_Ferram = {'Nindex': Nindex, 'Nome': Nome, 'Fabricante': Fabricante,
                  'PN_Mod': PN_Mod, 'Tamanho': Tamanho, 'rpm': rpm, 'Mat_de_Compos': Mat_de_Compos,
                  'tipo_ferr': tipo_ferr, 'unimed': unimed}
    # print(Cad_Ferram)

    Cadastro = pd.DataFrame(data=Cad_Ferram)

    print('Cadastro', Cadastro)

    # -----------------------------------------------------------------------------------

    # x2 = x
    Pag = 6
    listcol = []

    for col in x:
        listcol = listcol + [col]
    # print('Listcol',listcol)
    cont = len(listcol)

    # ---------------------------------------------------------------------------------------
    def menos_list():
        janela4 = tk.Tk()

        global bi, bf, Qi, Q, Pag

        Qi = Qi - 1
        bi = bi - Pag
        bf = bf - Pag

        if bi <= 0:
            bf = Pag
            bi = 0
        if Qi == Q:
            bf = bf + Pag - R

        # print(bi, bf, Qi, lN)

        for a in range(0, cont):
            label_Col = tk.Label(janela4, text=listcol[a])
            label_Col.grid(row=0, column=a, padx=10, pady=10)

            for b in range(bi, bf):
                label_Col = tk.Label(janela4, text=Nindex[b])
                label_Col.grid(row=b + 1, column=0, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Nome[b])
                label_Col.grid(row=b + 1, column=1, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Fabricante[b])
                label_Col.grid(row=b + 1, column=2, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=PN_Mod[b])
                label_Col.grid(row=b + 1, column=3, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Tamanho[b])
                label_Col.grid(row=b + 1, column=4, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=rpm[b])
                label_Col.grid(row=b + 1, column=5, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Mat_de_Compos[b])
                label_Col.grid(row=b + 1, column=6, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=tipo_ferr[b])
                label_Col.grid(row=b + 1, column=7, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=unimed[b])
                label_Col.grid(row=b + 1, column=8, padx=10, pady=10)

                label_Col = tk.Label(janela4, text="  ")
                label_Col.grid(row=b + 2, column=8, padx=10, pady=10)

        botao_Sair = tk.Button(janela4, text='Encerrar', command=janela4.destroy)
        botao_Sair.grid(row=lN + 3, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=60)

    # ---------------------------------------------------------------------------------------
    def mais_list():

        janela4 = tk.Tk()

        global bi, bf, Q, Qi, Pag

        Qi = Qi + 1
        bi = bi + Pag
        bf = bf + Pag

        if bf >= lN:
            bf = lN
            bi = Pag * Q
            Qi = Q + 1

        # print(bi,bf,Qi,lN)

        for a in range(0, cont):
            label_Col = tk.Label(janela4, text=listcol[a])
            label_Col.grid(row=0, column=a, padx=10, pady=10)

            for b in range(bi, bf):
                label_Col = tk.Label(janela4, text=Nindex[b])
                label_Col.grid(row=b + 1, column=0, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Nome[b])
                label_Col.grid(row=b + 1, column=1, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Fabricante[b])
                label_Col.grid(row=b + 1, column=2, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=PN_Mod[b])
                label_Col.grid(row=b + 1, column=3, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Tamanho[b])
                label_Col.grid(row=b + 1, column=4, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=rpm[b])
                label_Col.grid(row=b + 1, column=5, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Mat_de_Compos[b])
                label_Col.grid(row=b + 1, column=6, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=tipo_ferr[b])
                label_Col.grid(row=b + 1, column=7, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=unimed[b])
                label_Col.grid(row=b + 1, column=8, padx=10, pady=10)

                label_Col = tk.Label(janela4, text="  ")
                label_Col.grid(row=b + 2, column=8, padx=10, pady=10)

        botao_Sair = tk.Button(janela4, text='Encerrar', command=janela4.destroy)
        botao_Sair.grid(row=lN + 3, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=60)

    # ---------------------------------------------------------------------------------------
    def Editar():
        janela5 = tk.Tk()

        def Re_Ca():
            janela6 = tk.Tk()
            global Nindex
            NindexAlt = int(entry_Alt.get())
            Nindex = NindexAlt - 1

            # --------------------------------- Recadastramentro (Alteração)--------------------------
            def Recadastrar_ferramenta():
                NomeN = locals()
                global Nome, Fabricante, PN_Mod, Tamanho, rpm, Mat_de_Compos, tipo_ferr, unimed
                # NomeN = entry_Nome.get()
                # if NomeN != "":
                x.at[Nindex, 'Nome'] = entry_Nome.get()
                x.at[Nindex, 'Fabricante'] = entry_Fabricante.get()
                x.at[Nindex, 'PN_Mod'] = entry_PN_Mod.get()
                x.at[Nindex, 'Tamanho'] = entry_Tamanho.get()
                x.at[Nindex, 'rpm'] = entry_rpm.get()
                x.at[Nindex, 'Mat_de_Compos'] = entry_Mat_de_Compos.get()
                x.at[Nindex, 'tipo_ferr'] = combobox_tipo_ferr.get()
                x.at[Nindex, 'unimed'] = combobox_unimed.get()
                # x.iloc[Nindex-1:]
                print(Nindex, x)
                x.to_csv('Cadastro_Ferr.csv', index=False, encoding='utf-8')
                x.to_excel('Cadastro_Ferr.xlsx', index=False, )

            # ***************************************************************

            def apagar_valores():
                # #Apaga os valores das caixas de entrada
                entry_Nome.delete(0, "end")
                entry_Fabricante.delete(0, "end")
                entry_PN_Mod.delete(0, "end")
                entry_Tamanho.delete(0, "end")
                entry_rpm.delete(0, "end")
                entry_Mat_de_Compos.delete(0, "end")
                combobox_tipo_ferr.delete(0, "end")
                combobox_unimed.delete(0, "end")

            # ***************************  Variáveis combo BOX  ****************************

            lista_tipo_ferr = ['110v', '220v', "Bivolt", 'Bateria', 'Manual', 'Mecânica']
            lista_unimed = ['Centimetros - Cm', 'Polegadas - inch']

            # ***************************   Rótulos Entradas *******************************

            label_Nome = tk.Label(janela6, text=' "Nome" Descrição da Ferramenta ')
            label_Nome.grid(row=0, column=0, sticky="e", padx=10, pady=10)

            label_Fabricante = tk.Label(janela6, text=' Fabricante ')
            label_Fabricante.grid(row=1, column=0, sticky="e", padx=10, pady=10, )

            label_PN_Mod = tk.Label(janela6, text=' P/Number/Modelo ')
            label_PN_Mod.grid(row=2, column=0, sticky="e", padx=10, pady=10)

            label_Tamanho = tk.Label(janela6, text=' Tamanho ')
            label_Tamanho.grid(row=3, column=0, sticky="e", padx=10, pady=10)

            label_rpm = tk.Label(janela6, text=' rpm ')
            label_rpm.grid(row=4, column=0, sticky="e", padx=10, pady=10)

            label_Mat_de_Compos = tk.Label(janela6, text=' Material de Composição da Ferramenta ')
            label_Mat_de_Compos.grid(row=5, column=0, sticky="e", padx=10, pady=10)

            # Caixas Entradas:

            entry_Nome = tk.Entry(janela6, width=60)
            entry_Nome.grid(row=0, column=1, sticky="w", padx=10, pady=10)

            entry_Fabricante = tk.Entry(janela6, width=30)
            entry_Fabricante.grid(row=1, column=1, sticky="w", padx=10, pady=10)

            entry_PN_Mod = tk.Entry(janela6, width=25)
            entry_PN_Mod.grid(row=2, column=1, sticky="w", padx=10, pady=10)

            entry_Tamanho = tk.Entry(janela6, width=20)
            entry_Tamanho.grid(row=3, column=1, sticky="w", padx=10, pady=10)

            entry_rpm = tk.Entry(janela6, width=20)
            entry_rpm.grid(row=4, column=1, sticky="w", padx=10, pady=10)

            entry_Mat_de_Compos = tk.Entry(janela6, width=20)
            entry_Mat_de_Compos.grid(row=5, column=1, sticky="w", padx=10, pady=10)

            # Combo Box - Tipo de ferramenta

            combobox_tipo_ferr = ttk.Combobox(janela6, values=lista_tipo_ferr)
            combobox_tipo_ferr.grid(row=2, column=1, sticky="e", padx=10, pady=10)

            # Combo Box - Unidade de medida

            combobox_unimed = ttk.Combobox(janela6, values=lista_unimed)
            combobox_unimed.grid(row=3, column=1, sticky="e", padx=10, pady=10)

            # Botão de Cadastrar

            botao_cadastrar = tk.Button(janela6, text=f'Re-Cadastrar Ferramenta {NindexAlt}',
                                        command=Recadastrar_ferramenta)
            botao_cadastrar.grid(row=7, column=1, columnspan=2, sticky="e", padx=10, pady=10, ipadx=70)

            # Botão de Sair voltar tela inicial

            botao_Sair = tk.Button(janela6, text='Encerrar esta janela', command=janela6.destroy)
            botao_Sair.grid(row=6, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=60)

            # Botão de Apagar

            botao_Apagar = tk.Button(janela6, text='Apagar', command=apagar_valores)
            botao_Apagar.grid(row=6, column=1, columnspan=2, sticky="e", padx=10, pady=10, ipadx=35)

            janela6.mainloop()
            # ------------------------------------ fim recadastro -----------------------------------

        label_NAlt = tk.Label(janela5, text=' Digite o (Nindex) da Ferramenta que deseja alterar ')
        label_NAlt.grid(row=1, column=0, sticky="e", padx=10, pady=10)
        # Caixas Entradas:
        entry_Alt = tk.Entry(janela5, width=5)
        entry_Alt.grid(row=1, column=1, sticky="w", padx=10, pady=10)
        # Botão de Cadastrar
        botao_cadastrar = tk.Button(janela5, text='Re-Cadastrar', command=Re_Ca)
        botao_cadastrar.grid(row=3, column=0, columnspan=2, sticky="e", padx=10, pady=10, ipadx=10)

    # ---------------------------------------------------------------------------------------
    if Pag > lN:
        Pag = lN

    Q = lN // Pag
    R = lN % Pag

    # print(Q, R)
    bi = 0
    bf = Pag

    for a in range(0, cont):
        label_Col = tk.Label(janela4, text=listcol[a])
        label_Col.grid(row=0, column=a, padx=10, pady=10)

        for b in range(bi, bf):
            label_Col = tk.Label(janela4, text=Nindex[b])
            label_Col.grid(row=b + 1, column=0, padx=10, pady=10)
            label_Col = tk.Label(janela4, text=Nome[b])
            label_Col.grid(row=b + 1, column=1, padx=10, pady=10)
            label_Col = tk.Label(janela4, text=Fabricante[b])
            label_Col.grid(row=b + 1, column=2, padx=10, pady=10)
            label_Col = tk.Label(janela4, text=PN_Mod[b])
            label_Col.grid(row=b + 1, column=3, padx=10, pady=10)
            label_Col = tk.Label(janela4, text=Tamanho[b])
            label_Col.grid(row=b + 1, column=4, padx=10, pady=10)
            label_Col = tk.Label(janela4, text=rpm[b])
            label_Col.grid(row=b + 1, column=5, padx=10, pady=10)
            label_Col = tk.Label(janela4, text=Mat_de_Compos[b])
            label_Col.grid(row=b + 1, column=6, padx=10, pady=10)
            label_Col = tk.Label(janela4, text=tipo_ferr[b])
            label_Col.grid(row=b + 1, column=7, padx=10, pady=10)
            label_Col = tk.Label(janela4, text=unimed[b])
            label_Col.grid(row=b + 1, column=8, padx=10, pady=10)

            label_Col = tk.Label(janela4, text="  ")
            label_Col.grid(row=b + 2, column=8, padx=10, pady=10)

    botao_Sair = tk.Button(janela4, text='Encerrar', command=janela4.destroy)
    botao_Sair.grid(row=lN + 3, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=60)

    # mais_list()
    label_Col = tk.Label(janela3, text=f"Ferramentas Cadastradas = {lN}")
    label_Col.grid(row=1, column=0, padx=10, pady=10)

    # Botão de menos list

    botao_EDIT = tk.Button(janela3, text='Subir lista', command=menos_list)
    botao_EDIT.grid(row=3, column=2, columnspan=2, sticky="e", padx=10, pady=10, ipadx=35)

    # Botão de mais list

    botao_EDIT = tk.Button(janela3, text='Descer lista', command=mais_list)
    botao_EDIT.grid(row=4, column=2, columnspan=2, sticky="e", padx=10, pady=10, ipadx=35)

    # Botão de Sair voltar tela inicial

    botao_Sair = tk.Button(janela3, text='Encerrar esta janela', command=janela3.destroy)
    botao_Sair.grid(row=4, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=35)

    # Botão de Editar

    botao_EDIT = tk.Button(janela3, text='           Editar           ', command=Editar)
    botao_EDIT.grid(row=3, column=0, columnspan=2, sticky="e", padx=10, pady=10, ipadx=35)

    janela3.mainloop()
    janela4.mainloop()
# =========================== FIM === Consulta_de_Ferramentas === FIM ==============================
# ======================================= Cadastrar_Tecnicos =======================================
def Cadastrar_Tecnicos():
    import tkinter as tk
    from tkinter import ttk, Entry
    import pandas as pd
    from validate_docbr import CPF

    # ==================================== Criando Janela:==========================================
    janela2 = tk.Tk()
    janela2.title('Cadastro de Técnicos')
    janela2.geometry()
    global Nindex, Nome, Fabricante, PN_Mod, Tamanho, rpm, Mat_de_Compos
    # --------------------------------Verificando se tem arquivo----------------------
    try:
        x = pd.read_csv('Cadastro_Técn.csv')
    except:
        Nome = Fabricante = PN_Mod = Tamanho = rpm = Mat_de_Compos = []

        lN = len(Nome)
        Nindex = []
        for a in range(1, lN + 1):
            Nindex = Nindex + [a]

        Cad_Tecn = {'Matr': Nindex, 'Nome': Nome, 'CPF': Fabricante,
                    'Turno': PN_Mod, 'Celular': Tamanho, 'Radio': rpm,
                    'Equipe': Mat_de_Compos}
        print(Cad_Tecn)

        Cadastro = pd.DataFrame(data=Cad_Tecn)

        Cadastro.to_csv('Cadastro_Técn.csv', index=False)
        Cadastro.to_excel('Cadastro_Técn.xlsx', index=False)

        x = pd.read_csv('Cadastro_Técn.csv')

    print(x)

    # ---------------- converter de objeto tabela devolta pra lista  --------------------
    lN = len(x['Nome'])

    Nome = Fabricante = PN_Mod = Tamanho = rpm = Mat_de_Compos = tipo_ferr = unimed = []

    for a in range(0, lN):
        Nome = Nome + [x['Nome'][a]]
        Fabricante = Fabricante + [x['CPF'][a]]
        PN_Mod = PN_Mod + [x['Turno'][a]]
        Tamanho = Tamanho + [x['Celular'][a]]
        rpm = rpm + [x['Radio'][a]]
        Mat_de_Compos = Mat_de_Compos + [x['Equipe'][a]]

    # _________________________________ Cadastramento _______________________________
    def cadastrar_tecnico():
        # x = pd.read_excel('Cadastro_Técn.xlsx')
        x = pd.read_csv('Cadastro_Técn.csv')
        NomeN = locals()
        NomeN = entry_Nome.get()
        # Validar CPF cpfcheck = 04096352195 - 01234567890 - 04869753472 - 50772743711 - 94513157992
        # 36671514119 - 56212771200 - 35545870105 - 07280216099 - 06974284608 - 61345732724#True
        cpf = CPF()

        cpfcheck = [str(entry_Fabricante.get())]

        cpfc = cpf.validate(cpfcheck)  # True or False
        # print(CPF,cpfcheck,cpfc)
        # print('lista compl',x['CPF'])

        for cpfl in x['CPF']:
            # print('imp cpf cadast',cpfl)
            # print("comparando",cpfcheck, cpfl)
            cpf2 = str(cpfcheck)
            cpf1 = str(cpfl)
            if cpf2 == cpf1:
                entry_Fabricante.delete(0, "end")
                label_Fabricante = tk.Label(janela2, text='CPF Já cadastrado         ')
                label_Fabricante.grid(row=1, column=1, sticky="e", padx=10, pady=10, )
                NomeN = ""

        if cpfc == True:
            global Nindex, Nome, Fabricante, PN_Mod, Tamanho, rpm, Mat_de_Compos, tipo_ferr, unimed
            # NomeN = entry_Nome.get()

            if NomeN != "":
                label_Fabricante = tk.Label(janela2, text='                                           ')
                label_Fabricante.grid(row=1, column=1, padx=10, pady=10, )
                Nome = Nome + [NomeN]
                Fabricante = Fabricante + [[str(entry_Fabricante.get())]]
                PN_Mod = PN_Mod + [entry_PN_Mod.get()]
                Tamanho = Tamanho + [entry_Tamanho.get()]
                rpm = rpm + [entry_rpm.get()]
                Mat_de_Compos = Mat_de_Compos + [entry_Mat_de_Compos.get()]

                lN = len(Nome)
                Nindex = []
                for a in range(1, lN + 1):
                    Nindex = Nindex + [a]
                # print(Nindex)
                Cad_Tecn = {'Matr': Nindex, 'Nome': Nome, 'CPF': Fabricante,
                            'Turno': PN_Mod, 'Celular': Tamanho, 'Radio': rpm,
                            'Equipe': Mat_de_Compos}
                # print(Cad_Ferram)

                Cadastro = pd.DataFrame(data=Cad_Tecn)

                Cadastro.to_csv('Cadastro_Técn.csv', index=False)
                Cadastro.to_excel('Cadastro_Técn.xlsx', index=False)

                print(Cadastro)
                label_Fabricante = tk.Label(janela2, text='         Cadastro Realizado')
                label_Fabricante.grid(row=6, column=0, sticky="w", padx=10, pady=10, )
        else:
            entry_Fabricante.delete(0, "end")
            label_Fabricante = tk.Label(janela2, text='Digite um CPF Válido     ')
            label_Fabricante.grid(row=1, column=1, sticky="e", padx=10, pady=10, )

    # ****************************************************************************

    def apagar_valores():
        # #Apaga os valores das caixas de entrada
        entry_Nome.delete(0, "end")
        entry_Fabricante.delete(0, "end")
        entry_PN_Mod.delete(0, "end")
        entry_Tamanho.delete(0, "end")
        entry_rpm.delete(0, "end")
        entry_Mat_de_Compos.delete(0, "end")

        label_Fabricante = tk.Label(janela2, text='                                          ')
        label_Fabricante.grid(row=6, column=0, sticky="w", padx=10, pady=10, )
        label_Fabricante = tk.Label(janela2, text='                                          ')
        label_Fabricante.grid(row=1, column=1, sticky="e", padx=10, pady=10, )

    # ***************************   Rótulos Entradas *******************************

    label_Nome = tk.Label(janela2, text=' Nome')
    label_Nome.grid(row=0, column=0, sticky="e", padx=10, pady=10)

    label_Fabricante = tk.Label(janela2, text=' CPF/Só Num ')
    label_Fabricante.grid(row=1, column=0, sticky="e", padx=10, pady=10, )

    label_PN_Mod = tk.Label(janela2, text=' Turno(M-T-N)')
    label_PN_Mod.grid(row=2, column=0, sticky="e", padx=10, pady=10)

    label_Tamanho = tk.Label(janela2, text=' Celular com DDD ')
    label_Tamanho.grid(row=3, column=0, sticky="e", padx=10, pady=10)

    label_rpm = tk.Label(janela2, text=' Rádio ')
    label_rpm.grid(row=4, column=0, sticky="e", padx=10, pady=10)

    label_Mat_de_Compos = tk.Label(janela2, text=' Equipe ')
    label_Mat_de_Compos.grid(row=5, column=0, sticky="e", padx=10, pady=10)

    # Caixas Entradas:

    entry_Nome = tk.Entry(janela2, width=45)
    entry_Nome.grid(row=0, column=1, sticky="w", padx=10, pady=10)

    entry_Fabricante: Entry = tk.Entry(janela2, width=12)
    entry_Fabricante.grid(row=1, column=1, sticky="w", padx=10, pady=10)

    entry_PN_Mod = tk.Entry(janela2, width=4)
    entry_PN_Mod.grid(row=2, column=1, sticky="w", padx=10, pady=10)

    entry_Tamanho = tk.Entry(janela2, width=12)
    entry_Tamanho.grid(row=3, column=1, sticky="w", padx=10, pady=10)

    entry_rpm = tk.Entry(janela2, width=9)
    entry_rpm.grid(row=4, column=1, sticky="w", padx=10, pady=10)

    entry_Mat_de_Compos = tk.Entry(janela2, width=31)
    entry_Mat_de_Compos.grid(row=5, column=1, sticky="w", padx=10, pady=10)

    label_Fabricante = tk.Label(janela2, text='                                          ')
    label_Fabricante.grid(row=6, column=0, sticky="w", padx=10, pady=10, )

    # Botão de Cadastrar

    botao_cadastrar = tk.Button(janela2, text='Cadastrar Técnico', command=cadastrar_tecnico)
    botao_cadastrar.grid(row=6, column=1, columnspan=2, sticky="e", padx=10, pady=10, ipadx=30)

    # Botão de Sair voltar tela inicial

    botao_Sair = tk.Button(janela2, text='Encerrar esta janela', command=janela2.destroy)
    botao_Sair.grid(row=7, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=30)

    # Botão de Apagar

    botao_Apagar = tk.Button(janela2, text='         Limpar         ', command=apagar_valores)
    botao_Apagar.grid(row=7, column=1, columnspan=2, sticky="e", padx=10, pady=10, ipadx=30)

    janela2.mainloop()
# =========================== FIM ======= Cadastrar_Tecnicos ======= FIM ===========================
# ======================================== Consulta_Tecnicos =======================================
def Consulta_Tecnicos():
    import tkinter as tk
    import pandas as pd
    from validate_docbr import CPF
    # ---------------------------------------------------------------------------------------
    global bi, bf, Q, Pag, Qi, lN
    Qi = 1
    # ---------------------------------------------------------------------------------------
    try:
        x = pd.read_csv('Cadastro_Técn.csv')

    except:
        Nome = Fabricante = PN_Mod = Tamanho = rpm = Mat_de_Compos = []

        lN = len(Nome)
        Nindex = []
        for a in range(1, lN + 1):
            Nindex = Nindex + [a]

        Cad_Tecn = {'Matr': Nindex, 'Nome': Nome, 'CPF': Fabricante,
                    'Turno': PN_Mod, 'Celular': Tamanho, 'Radio': rpm,
                    'Equipe': Mat_de_Compos}
        print(Cad_Tecn)

        Cadastro = pd.DataFrame(data=Cad_Tecn)

        Cadastro.to_csv('Cadastro_Técn.csv', index=False)
        Cadastro.to_excel('Cadastro_Técn.xlsx', index=False)

        x = pd.read_csv('Cadastro_Técn.csv')

    # print(x)

    # =======================================================================================

    janela3 = tk.Tk()

    # ------------------ converter de objeto tabela devolta pra lista  ----------------------

    lN = len(x['Nome'])
    print(lN)
    Nome = Fabricante = PN_Mod = Tamanho = rpm = Mat_de_Compos = []

    for a in range(0, lN):
        Nome = Nome + [x['Nome'][a]]
        Fabricante = Fabricante + [x['CPF'][a]]
        PN_Mod = PN_Mod + [x['Turno'][a]]
        Tamanho = Tamanho + [x['Celular'][a]]
        rpm = rpm + [x['Radio'][a]]
        Mat_de_Compos = Mat_de_Compos + [x['Equipe'][a]]

        lN = len(Nome)
        Nindex = []
        for a in range(1, lN + 1):
            Nindex = Nindex + [a]
        print("Nindex", Nindex)

    Cad_Tecn = {'Matr': Nindex, 'Nome': Nome, 'CPF': Fabricante,
                'Turno': PN_Mod, 'Celular': Tamanho, 'Radio': rpm,
                'Equipe': Mat_de_Compos}

    Cadastro = pd.DataFrame(data=Cad_Tecn)

    print('Cadastro', Cadastro)

    # ---------------------------------------------------------------------------------------

    Pag = 10
    listcol = []

    for col in x:
        listcol = listcol + [col]

    cont = len(listcol)

    # ---------------------------------------------------------------------------------------
    def menos_list():
        janela4 = tk.Tk()
        janela4.title('Cadastro de Técnicos')
        global bi, bf, Qi, Pag, lN

        Qi = Qi - 1
        if Qi < 1:
            Qi = 1

        bf = Qi * Pag

        if lN < bf:
            bf = lN
            Qi = Qi - 1

        bi = bf - Pag
        if bi<0:
            bi=0

        print(bi, bf, Qi, lN)

        for a in range(0, cont):
            label_Col = tk.Label(janela4, text=listcol[a])
            label_Col.grid(row=0, column=a, padx=10, pady=10)

            for b in range(bi, bf):
                # print('b',b,bi,bf)
                label_Col = tk.Label(janela4, text=Nindex[b])
                label_Col.grid(row=b + 1, column=0, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Nome[b])
                label_Col.grid(row=b + 1, column=1, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Fabricante[b])
                label_Col.grid(row=b + 1, column=2, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=PN_Mod[b])
                label_Col.grid(row=b + 1, column=3, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Tamanho[b])
                label_Col.grid(row=b + 1, column=4, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=rpm[b])
                label_Col.grid(row=b + 1, column=5, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Mat_de_Compos[b])
                label_Col.grid(row=b + 1, column=6, padx=10, pady=10)

                label_Col = tk.Label(janela4, text="  ")
                label_Col.grid(row=b + 2, column=8, padx=10, pady=10)

        botao_Sair = tk.Button(janela4, text='Encerrar', command=janela4.destroy)
        botao_Sair.grid(row=lN + 3, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=60)

    # ---------------------------------------------------------------------------------------
    def mais_list():

        janela4 = tk.Tk()
        janela4.title('Cadastro de Técnicos')
        global bi, bf, Qi, Pag, lN

        Qi = Qi + 1
        bf = Qi * Pag

        if lN < bf:
            bf = lN
            Qi = Qi - 1

        bi = bf - Pag
        if bi<0:
            bi=0

        print('antes if', bi, bf, Qi, lN)

        for a in range(0, cont):
            label_Col = tk.Label(janela4, text=listcol[a])
            label_Col.grid(row=0, column=a, padx=10, pady=10)

            for b in range(bi, bf):
                # print('b',b,bi,bf)
                label_Col = tk.Label(janela4, text=Nindex[b])
                label_Col.grid(row=b + 1, column=0, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Nome[b])
                label_Col.grid(row=b + 1, column=1, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Fabricante[b])
                label_Col.grid(row=b + 1, column=2, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=PN_Mod[b])
                label_Col.grid(row=b + 1, column=3, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Tamanho[b])
                label_Col.grid(row=b + 1, column=4, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=rpm[b])
                label_Col.grid(row=b + 1, column=5, padx=10, pady=10)
                label_Col = tk.Label(janela4, text=Mat_de_Compos[b])
                label_Col.grid(row=b + 1, column=6, padx=10, pady=10)

                label_Col = tk.Label(janela4, text="  ")
                label_Col.grid(row=b + 2, column=8, padx=10, pady=10)

        botao_Sair = tk.Button(janela4, text='Encerrar', command=janela4.destroy)
        botao_Sair.grid(row=lN + 3, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=60)

    # ---------------------------------------------------------------------------------------
    def Editar():
        janela5 = tk.Tk()
        janela5.title('Alteração de Técnico')

        def Re_Ca():

            janela6 = tk.Tk()
            janela6.title('Recadastro de Técnico')
            global Nindex
            NindexAlt = int(entry_Alt.get())
            Nindex = NindexAlt - 1
            for col in x:
                x.at[Nindex, col] = ""
                print(x)

            # --------------------------------- Recadastramentro (Alteração)--------------------------
            def cadastrar_tecnico():
                x = pd.read_csv('Cadastro_Técn.csv')
                NomeN = locals()
                NomeN = entry_Nome.get()
                # Validar CPF cpfcheck = 04096352195 - 01234567890 - 04869753472 - 50772743711 - 94513157992
                # 36671514119 - 56212771200 - 35545870105 - 07280216099 - 06974284608 - 61345732724#True
                cpf = CPF()

                cpfcheck = [str(entry_Fabricante.get())]

                cpfc = cpf.validate(cpfcheck)  # True or False
                # print(CPF,cpfcheck,cpfc)
                # print('lista compl',x['CPF'])

                for cpfl in x['CPF']:
                    # print('imp cpf cadast',cpfl)
                    # print("comparando",cpfcheck, cpfl)
                    cpf2 = str(cpfcheck)
                    cpf1 = str(cpfl)
                    if cpf2 == cpf1:
                        entry_Fabricante.delete(0, "end")
                        label_Fabricante = tk.Label(janela6, text='CPF Já cadastrado         ')
                        label_Fabricante.grid(row=1, column=1, sticky="e", padx=10, pady=10, )
                        NomeN = ""

                if cpfc == True:
                    global Nindex, Nome, Fabricante, PN_Mod, Tamanho, rpm, Mat_de_Compos, tipo_ferr, unimed
                    # NomeN = entry_Nome.get()
                    if NomeN != "":
                        x.at[Nindex, 'Nome'] = [entry_Nome.get()]
                        x.at[Nindex, 'CPF'] = [str(entry_Fabricante.get())]
                        x.at[Nindex, 'Turno'] = [entry_PN_Mod.get()]
                        x.at[Nindex, 'Celular'] = [entry_Tamanho.get()]
                        x.at[Nindex, 'Radio'] = [entry_rpm.get()]
                        x.at[Nindex, 'Equipe'] = [entry_Mat_de_Compos.get()]

                        print(Nindex, x)
                        x.to_csv('Cadastro_Técn.csv', index=False, encoding='utf-8')
                        x.to_excel('Cadastro_Técn.xlsx', index=False)
                        label_Fabricante = tk.Label(janela6, text='         Cadastro Realizado')
                        label_Fabricante.grid(row=6, column=0, sticky="w", padx=10, pady=10, )

                else:
                    entry_Fabricante.delete(0, "end")
                    label_Fabricante = tk.Label(janela6, text='Digite um CPF Válido     ')
                    label_Fabricante.grid(row=1, column=1, sticky="e", padx=10, pady=10, )

            # ***************************************************************

            def apagar_valores():
                # #Apaga os valores das caixas de entrada
                entry_Nome.delete(0, "end")
                entry_Fabricante.delete(0, "end")
                entry_PN_Mod.delete(0, "end")
                entry_Tamanho.delete(0, "end")
                entry_rpm.delete(0, "end")
                entry_Mat_de_Compos.delete(0, "end")
                label_Fabricante = tk.Label(janela6, text='                                          ')
                label_Fabricante.grid(row=6, column=0, sticky="w", padx=10, pady=10, )
                label_Fabricante = tk.Label(janela6, text='                                          ')
                label_Fabricante.grid(row=1, column=1, sticky="e", padx=10, pady=10, )

            # ***************************   Rótulos Entradas *******************************

            label_Nome = tk.Label(janela6, text=' Nome')
            label_Nome.grid(row=0, column=0, sticky="e", padx=10, pady=10)

            label_Fabricante = tk.Label(janela6, text=' CPF/Só Num ')
            label_Fabricante.grid(row=1, column=0, sticky="e", padx=10, pady=10, )

            label_PN_Mod = tk.Label(janela6, text=' Turno(M-T-N)')
            label_PN_Mod.grid(row=2, column=0, sticky="e", padx=10, pady=10)

            label_Tamanho = tk.Label(janela6, text=' Celular com DDD ')
            label_Tamanho.grid(row=3, column=0, sticky="e", padx=10, pady=10)

            label_rpm = tk.Label(janela6, text=' Rádio ')
            label_rpm.grid(row=4, column=0, sticky="e", padx=10, pady=10)

            label_Mat_de_Compos = tk.Label(janela6, text=' Equipe ')
            label_Mat_de_Compos.grid(row=5, column=0, sticky="e", padx=10, pady=10)

            # Caixas Entradas:

            entry_Nome = tk.Entry(janela6, width=45)
            entry_Nome.grid(row=0, column=1, sticky="w", padx=10, pady=10)

            entry_Fabricante = tk.Entry(janela6, width=12)
            entry_Fabricante.grid(row=1, column=1, sticky="w", padx=10, pady=10)

            entry_PN_Mod = tk.Entry(janela6, width=4)
            entry_PN_Mod.grid(row=2, column=1, sticky="w", padx=10, pady=10)

            entry_Tamanho = tk.Entry(janela6, width=12)
            entry_Tamanho.grid(row=3, column=1, sticky="w", padx=10, pady=10)

            entry_rpm = tk.Entry(janela6, width=9)
            entry_rpm.grid(row=4, column=1, sticky="w", padx=10, pady=10)

            entry_Mat_de_Compos = tk.Entry(janela6, width=31)
            entry_Mat_de_Compos.grid(row=5, column=1, sticky="w", padx=10, pady=10)

            label_Fabricante = tk.Label(janela6, text='                                          ')
            label_Fabricante.grid(row=6, column=0, sticky="w", padx=10, pady=10, )

            # Botão de Cadastrar

            botao_cadastrar = tk.Button(janela6, text='Re-Cadastrar Técn', command=cadastrar_tecnico)
            botao_cadastrar.grid(row=6, column=1, columnspan=2, sticky="e", padx=10, pady=10, ipadx=30)

            # Botão de Sair voltar tela inicial

            botao_Sair = tk.Button(janela6, text='Encerrar esta janela', command=janela6.destroy)
            botao_Sair.grid(row=7, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=30)

            # Botão de Apagar

            botao_Apagar = tk.Button(janela6, text='         Limpar         ', command=apagar_valores)
            botao_Apagar.grid(row=7, column=1, columnspan=2, sticky="e", padx=10, pady=10, ipadx=30)

            janela6.mainloop()
            # ------------------------------------ fim recadastro -----------------------------------

        label_NAlt = tk.Label(janela5, text=' Digite a (Matrícula) do Técnico que deseja alterar')
        label_NAlt.grid(row=1, column=0, sticky="e", padx=10, pady=10)
        # Caixas Entradas:
        entry_Alt = tk.Entry(janela5, width=5)
        entry_Alt.grid(row=1, column=1, sticky="w", padx=10, pady=10)
        # Botão de Re-Cadastrar Lv1
        botao_cadastrar = tk.Button(janela5, text='Re-Cadastrar', command=Re_Ca)
        botao_cadastrar.grid(row=3, column=0, columnspan=2, sticky="e", padx=10, pady=10, ipadx=10)

    # ---------------------------------------------------------------------------------------
    menos_list()
    # ---------------------------------------------------------------------------------------

    janela3.title('Cadastro de Técnicos')

    # mais_list()
    label_Col = tk.Label(janela3, text=f"Técnicos Cadastrados = {lN}")
    label_Col.grid(row=1, column=0, padx=10, pady=10)

    # Botão de menos list

    botao_EDIT = tk.Button(janela3, text='Subir lista', command=menos_list)
    botao_EDIT.grid(row=3, column=2, columnspan=2, sticky="e", padx=10, pady=10, ipadx=35)

    # Botão de mais list

    botao_EDIT = tk.Button(janela3, text='Descer lista', command=mais_list)
    botao_EDIT.grid(row=4, column=2, columnspan=2, sticky="e", padx=10, pady=10, ipadx=35)

    # Botão de Sair

    botao_Sair = tk.Button(janela3, text='Encerrar esta janela', command=janela3.destroy)
    botao_Sair.grid(row=4, column=0, columnspan=2, sticky="w", padx=10, pady=10, ipadx=35)

    # Botão de Editar

    botao_EDIT = tk.Button(janela3, text='           Editar           ', command=Editar)
    botao_EDIT.grid(row=3, column=0, columnspan=2, sticky="e", padx=10, pady=10, ipadx=35)

    janela3.mainloop()
# ================================ FIM === Consulta_Tecnicos === FIM ===============================
# ============================================ Locacao =============================================
def Locacao():
    import tkinter as tk
    import datetime as dt
    import pandas as pd

    # ==============================================================================================

    OrdemR = Matr = NomeT = CPF = Turno = Celular = Radio = Equipe = []
    # Nindex = NomeF = Fabricante = []
    # iT = iF = 1
    global NomeTR, CPFR, TurnoR, CelularR, RadioR, EquipeR, iT
    global Nindex, NomeFR, FabricanteR, iF
    global iiT, iiF
    global CadRes, CadTec, CadFer, CadastroT, CadastroF
    global dataR, horaR, data_post, hora_post

    data = dt.datetime.today()
    hora = data.strftime("%H:%M")
    data = data.strftime("%d/%m/%Y")
    # data = data.strftime("%d/%m/%Y %H:%M")
    # data_post=data.strftime("%d/%m/%Y %H:%M")
    data_post = data
    # data_post = int(data)

    print(type(data))
    print(type(data_post))
    print(hora, data_post)
    # ==================================================================================================
    # Criando Janela:

    janela7 = tk.Tk()
    janela7.title('Reserva de ferramentas')
    janela7.geometry()
    # "650x350"

    # --------------------------------------Verificando se tem arquivo---------------------------------
    try:
        CadFer = pd.read_csv('Cadastro_Ferr.csv')
        CadTec = pd.read_csv('Cadastro_Técn.csv')
        CadRes = pd.read_csv('Cadastro_Reserv.csv')

    except:
        print('Erro - Não consegui ler o arquivo')

        Reserv = {'OrdemR': OrdemR, 'DataRet': data, 'HoraRet': hora, 'DataDev': data_post, 'HoraDev': hora, 'Matr': iT,
                  'Nome_Tec': NomeTR, 'Celular': CelularR, 'Radio': RadioR, 'Equipe': EquipeR,
                  'Nindex': iF, 'Nome_Fer': NomeFR, 'Fabricante': FabricanteFR}

        CadastroRes = pd.DataFrame(data=Reserv)

        CadastroRes.to_csv('Cadastro_Reserv.csv')
        CadastroRes.to_excel('Cadastro_Reserv.xlsx')

        CadRes = pd.read_csv('Cadastro_Reserv.csv')

    # print(x)
    # ==================================================================================================
    # -------------------- converter de objeto Ferramentas de volta pra lista --------------------------
    CadastroF = CadFer.to_dict('list')
    # print('CadastroF', CadastroF)
    # ==================================================================================================
    # --------------------- converter de objeto Técnico de volta pra lista  ----------------------------
    CadastroT = CadTec.to_dict('list')
    # print('CadastroT', CadastroT)
    # ==================================================================================================
    # --------------------- converter de objeto Reserva de volta pra lista  ----------------------------
    '''
    lOR = len(CadRes['OrdemR'])
    Reserv = {'OrdemR': OrdemR,'DataRet': dataR, 'HoraRet': horaR,
                      'DataDev': data_post, 'HoraDev': hora_post, 'Matr': iT,
                      'Nome_Tec': NomeTR, 'Celular': CelularR, 'Radio': RadioR, 'Equipe': EquipeR,
                      'Nindex': iF, 'Nome_Fer': NomeFR, 'Fabricante': FabricanteFR}

    for a in range(0, lOR):
        dataR = dataR + [CadRes[data]
        horaR = horaR + [CadRes[hora]
        data_post = data_post + [CadRes[data_post]
        hora_post = hora_post + [CadRes[hora]
        iT = iT + [CadRes[iT]
        iF = iF + [CadRes[iF]

        NomeFR = NomeFR + [CadRes['Nome_Fer'][iF]]
        FabricanteFR = FabricanteFR + [CadRes['Fabricante'][iF]]

        NomeTR = NomeTR + [CadRes['Nome_Tec'][iT]]
        CPFR = CPFR + [CadRes['CPF'][iT]]
        TurnoR = TurnoR + [CadRes['Turno'][iT]]
        CelularR = CelularR + [CadRes['Celular'][iT]]
        RadioR = RadioR + [CadRes['Radio'][iT]]
        EquipeR = EquipeR + [CadRes['Equipe'][iT]]
    '''
    CadRes = CadRes.to_dict('list')
    print(CadRes)

    # ==================================================================================================
    def Registrar():
        global CadRes
        global NomeTR, CPFR, TurnoR, CelularR, RadioR, EquipeR, iT, CadTec, CadastroT
        global NomeFR, FabricanteFR, iF, CadFer, CadastroF
        global dataR, horaR, data_post, hora_post
        OrdemR = NomeTR = CPFR = TurnoR = CelularR = RadioR = EquipeR = []
        NomeFR = FabricanteFR = []

        # lOR=len(CadRes['Nome_Tec'])+1
        # print("ordem=",lOR)

        # print('OrdemR',OrdemR,lOR)
        iTM = len(CadTec['Matr'])
        iFM = len(CadFer['Nindex'])
        print('iTM', iTM, 'iFM', iFM)

        iT = (int(entry_Matr.get())) - 1
        iF = (int(entry_Nindex.get())) - 1
        data_post = (entry_data_post.get())
        print(iT, iF)
        if iT > iTM:
            print('indice de Tec fora de cadastro ')
            label_Div = tk.Label(janela7, text='Algum Indice Inválido')
            label_Div.grid(row=4, column=1, sticky="e", padx=10, pady=10)

        if iF > iFM:
            print('indice de Ferramenta fora de cadastro ')
            label_Div = tk.Label(janela7, text='Algum Indice Inválido')
            label_Div.grid(row=4, column=1, sticky="e", padx=10, pady=10)
        else:
            print('tudo Certo')
            print(iT, iF)
            print(CadFer['Nome'][iF])
            print(CadRes)

            label_CadTec = tk.Label(janela7, text=f' Registro Feito para {CadTec["Nome"][iT]}')
            label_CadTec.grid(row=5, column=0, sticky="e", padx=10, pady=10)
            # +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
            label_RetFe = tk.Label(janela7, text=f' Registro Feito para Ferramenta [{CadFer["Nome"][iF]}]')
            label_RetFe.grid(row=6, column=0, sticky="e", padx=10, pady=10)
            label_Hora = tk.Label(janela7, text=f' hora de retirada {hora}   Data de devolução {data_post} ({hora})')
            label_Hora.grid(row=7, column=0, sticky="e", padx=10, pady=10)

            print('cad tec1', NomeTR, CPFR, TurnoR, CelularR, RadioR, EquipeR, NomeFR, FabricanteFR)
            print('NF e F', NomeFR, FabricanteFR)
            '''
            dataR = dataR + [data]
            horaR = horaR + [hora]
            data_post = data_post + [data_post]
            hora_post = hora_post + [hora]
            iT = iT + [iT]
            iF = iF + [iF]
            '''
            NomeTR = NomeTR + [CadTec['Nome'][iT]]
            CPFR = CPFR + [CadTec['CPF'][iT]]
            TurnoR = TurnoR + [CadTec['Turno'][iT]]
            CelularR = CelularR + [CadTec['Celular'][iT]]
            RadioR = RadioR + [CadTec['Radio'][iT]]
            EquipeR = EquipeR + [CadTec['Equipe'][iT]]

            NomeFR = NomeFR + [CadFer['Nome'][iF]]
            FabricanteFR = FabricanteFR + [CadFer['Fabricante'][iF]]

            print('cad tec2', NomeTR, CPFR, TurnoR, CelularR, RadioR, EquipeR, NomeFR, FabricanteFR)
            # --------------------------------------------------------------------------------------------
            Reserv = {'OrdemR': OrdemR, 'DataRet': dataR, 'HoraRet': horaR,
                      'DataDev': data_post, 'HoraDev': hora_post, 'Matr': iT,
                      'Nome_Tec': NomeTR, 'Celular': CelularR, 'Radio': RadioR, 'Equipe': EquipeR,
                      'Nindex': iF, 'Nome_Fer': NomeFR, 'Fabricante': FabricanteFR}

            CadRes = pd.DataFrame(data=Reserv)

            CadRes.to_csv('Cadastro_Reserv.csv')
            CadRes.to_excel('Cadastro_Reserv.xlsx')

            print('CadastroRes', CadRes)

        print('Ok!!!!')

    # ---------------------------------------------------------------------------------------------------
    def Registrar_outro():
        # print('registro outro')
        entry_Matr.delete(0, "end")
        entry_Nindex.delete(0, "end")
        entry_data_post.delete(0, "end")

        label_Div = tk.Label(janela7, text='       ' * 6)
        label_Div.grid(row=4, column=1, sticky="e", padx=10, pady=10)

        label_Fabricante = tk.Label(janela7, text='          ' * 10)
        label_Fabricante.grid(row=5, column=0, sticky="e", padx=10, pady=10, )
        label_Fabricante = tk.Label(janela7, text='          ' * 10)
        label_Fabricante.grid(row=6, column=0, sticky="e", padx=10, pady=10, )
        label_Fabricante = tk.Label(janela7, text='          ' * 10)
        label_Fabricante.grid(row=7, column=0, sticky="e", padx=10, pady=10, )

    # ---------------------------------------------------------------------------------------------------
    # --------------------------------- Hora do sistema
    label_Nome = tk.Label(janela7, text=f'     Data/Hora do sistema: {data} - {hora}')
    label_Nome.grid(row=0, column=0, sticky="w", padx=10, pady=10)
    # ---------------------------------------------------------------------------------------------------
    label_Matr = tk.Label(janela7, text=' Digite a ( Matr ) do técnico desejado')
    label_Matr.grid(row=1, column=0, sticky="e", padx=10, pady=10)
    entry_Matr = tk.Entry(janela7, width=10)
    entry_Matr.grid(row=1, column=1, sticky="w", padx=10, pady=10)
    # ---------------------------------------------------------------------------------------------------
    label_Nindex = tk.Label(janela7, text=' Digite (Nindex) da ferramenta desejada')
    label_Nindex.grid(row=2, column=0, sticky="e", padx=10, pady=10)
    entry_Nindex = tk.Entry(janela7, width=10)
    entry_Nindex.grid(row=2, column=1, sticky="w", padx=10, pady=10)
    # ---------------------------------------------------------------------------------------------------
    label_data_post = tk.Label(janela7, text=' Digite a data de Devolução (dd/mm)')
    label_data_post.grid(row=3, column=0, sticky="e", padx=10, pady=10)
    entry_data_post = tk.Entry(janela7, width=10)
    entry_data_post.grid(row=3, column=1, sticky="w", padx=10, pady=10)

    label_Div = tk.Label(janela7, text='==' * 20)
    label_Div.grid(row=4, column=0, sticky="e", padx=10, pady=10)
    # ---------------------------------------------------------------------------------------------------
    '''
    label_CadTec = tk.Label(janela7, text=f' Registro Feito para {CadTec["Nome"][1]}')
    label_CadTec.grid(row=5, column=0, sticky="e", padx=10, pady=10)
    #+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
    label_RetFe = tk.Label(janela7, text=f' Registro Feito para Ferramenta [{CadFer["Nome"][3]}]')
    label_RetFe.grid(row=6, column=0, sticky="e", padx=10, pady=10)
    label_Hora = tk.Label(janela7, text=f' hora de retirada {hora}   Data de devolução {data_post} ({hora})')
    label_Hora.grid(row=7, column=0, sticky="e", padx=10, pady=10)
    '''
    # ------------------------------------------ botões -------------------------------------------------
    botao_Sair = tk.Button(janela7, text='Encerrar', command=janela7.destroy)
    botao_Sair.grid(row=9, column=0, sticky="w", padx=10, pady=10, ipadx=45)

    botao_REG = tk.Button(janela7, text='Registrar', command=Registrar)
    botao_REG.grid(row=9, column=1, sticky="e", padx=10, pady=10, ipadx=45)

    botao_REGO = tk.Button(janela7, text='Registrar outro', command=Registrar_outro)
    botao_REGO.grid(row=9, column=0, sticky="e", padx=5, pady=10, ipadx=45)
    # ------------------
    janela7.mainloop()
# ====================================== FIM === Locacao === FIM ===================================
# =============================================== E_mail ===========================================
def E_mail():
    print('E_mail')
# ======================================= FIM === E_mail === FIM ===================================
# ==================================================================================================

label_Nome = tk.Label(janela, text=' Menu principal do sistema ')
label_Nome.grid(row=0, column=1, sticky="nswe", padx=10, pady=20)

# ==================================================================================================
# Botão de Cadastrar Ferramenta e Consulta

botao_CadastrarF = tk.Button(text='Cadastrar Ferramentas', command=Cadastrar_Ferramentas)
botao_CadastrarF.grid(row=1, column=0, sticky="e", padx=15, pady=15, ipadx=40)

botao_ConsultaF = tk.Button(text='Consulta de Ferramentas', command=Consulta_de_Ferramentas)
botao_ConsultaF.grid(row=3, column=0, sticky="e", padx=15, pady=15 , ipadx=35)

# Botão de Locação de Ferramentas:

botao_LocacaoF = tk.Button(text='Locação\n\nReserva', command=Locacao)
botao_LocacaoF.grid(row=1, column=1, padx=15, pady=15, ipadx=50)

botao_ConsultaT = tk.Button(text='Email', command=E_mail)
botao_ConsultaT.grid(row=3, column=1, padx=15, pady=15, ipadx=50)

# Botão de Cadastrar Técnicos

botao_CadastrarT = tk.Button(text='Cadastrar Técnicos', command=Cadastrar_Tecnicos)
botao_CadastrarT.grid(row=1, column=2, sticky="e", padx=15, pady=15, ipadx=50)

botao_ConsultaT = tk.Button(text='Consulta Técnicos', command=Consulta_Tecnicos)
botao_ConsultaT.grid(row=3, column=2, sticky="e", padx=15, pady=15 , ipadx=50)


# ==================================================================================================
janela.mainloop()
https://youtu.be/yvcj0AV3P-k
