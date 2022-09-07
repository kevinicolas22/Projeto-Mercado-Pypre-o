#BIBLIOTECA
import pandas as pd
from google.colab import drive

#BANCO DE DADOS
drive.mount('/content/drive')
tabela = pd.read_excel('/content/drive/MyDrive/Colab_Notebooks/projeto/dados_mercado.xlsx')

#VARIÁVEIS DO CARRINHO
listaproduto_escolhido = []
listaquantidade = []
listavalordasquantidades = []

valortotal_compras = 0.0

#FUNÇÕES
def linha(tam=42):
  return '-' * tam

def cabecalho(txt):
  print(linha())
  print(txt.center(42))
  print(linha())

def menu(descricoes):
  escolha = ""
  numeroOpcoes = 1
  
  for descricaoOpcao in descricoes:
    print(f'{numeroOpcoes} - {descricaoOpcao}')
    numeroOpcoes += 1
  
  print(linha())
  
  while(verificarVazio(escolha) == ""):
    escolha = verificarVazio(input('Digite uma opção: '))

  print(linha())
  
  return escolha

# Verificar se um texto é um número
def verificarVazio(texto):
  try:
    return int(texto)
  except:
    return ""

def imprimir_carrinho():
  cabecalho('CARRINHO')

  for counter in range(len(listaproduto_escolhido)):
    print(f"{counter} {listaproduto_escolhido[counter]} {listaquantidade[counter]} - R$ {listavalordasquantidades[counter]:.2f}")

  print(linha())

def excluir_produto(id):
  listaproduto_escolhido.pop(id)
  listaquantidade.pop(id)
  listavalordasquantidades.pop(id)

def adicionar_produto(a, b, c):
  listaproduto_escolhido.append(a)
  listaquantidade.append(b)
  listavalordasquantidades.append(c)

def finalizar_compra():
  imprimir_carrinho()
  print(f'O total da compra deu: R$ {valortotal_compras:.2f}')

def imprimir_erro_generico():
  print('\033[31mERRO! Digite uma opção válida.\033[0m')
  
def remover_produto_da_prateleira(id, quantidade):
  tabela.loc[id, 'Estoque'] -= quantidade
  
def adicionar_produto_a_prateleira(id, quantidade):
  tabela.loc[id, 'Estoque'] += quantidade

##########################

#COMEÇO DO PROGRAMA
cabecalho('MERCADO PY-PREÇO')

while True:
  cabecalho('MENU PRINCIPAL')
  escolha = menu(['Começar Suas Compras.', 'Finalizar Programa'])
  
 #ENTRAR NA SESSÃO DE COMPRAS
  if escolha == 1:
    while True:

      cabecalho('Sessão de Compras')
      segunda_escolha = menu(['Prateleira', 'Mostrar Carrinho','Finalizar Compra'])
      if segunda_escolha == 1:

        display(tabela)
        print(linha())
        
        while True:
          terceira_escolha = menu(['Escolher Produto', 'Voltar'])
          
          #ESCOLHER PRODUTO
          if terceira_escolha == 1:
            id = verificarVazio(input('Digite o identificador do produto: '))

            if 0 <= id <= 23:
              produto_escolhido = tabela['Produtos'][id]
              print(f"Você escolheu o produto ", produto_escolhido)

              quantidade = verificarVazio(input('Digite a quantidade desejada: '))
              
              valor = float(tabela['Valores'][id])
              estoque = int(tabela['Estoque'] [id])
              
              if estoque == 0:
                print(f'Estamos sem estoque de', produto_escolhido, 'no momento, sentimos muito!')

              elif quantidade > estoque:
                print('Você só pode comprar até', estoque, 'quantidades desse produto!')

              else:
                valordasquantidades = quantidade * valor
                valortotal_compras += valordasquantidades

                print(f'{quantidade} quantidade(s) de {produto_escolhido} custa R$ {valordasquantidades:.2f}')

                remover_produto_da_prateleira(id, quantidade)
                adicionar_produto(produto_escolhido, quantidade, valordasquantidades)
            else:
              imprimir_erro_generico()
              
          #VOLTAR PARA SESSÃO DE COMPRAS
          elif terceira_escolha == 2: 
            break
          
          #TRATAMENTO DE ERRO
          else: 
              imprimir_erro_generico()
      
      #MOSTRAR CARRINHO
      elif segunda_escolha == 2:
        while True:
          if listaproduto_escolhido == []:
            print('Carrinho Vazio')
            break

          else:
            imprimir_carrinho()
            terceira_escolha = menu(['Excluir Produto', 'Voltar'])

            #EXCLUIR PRODUTO
            if terceira_escolha == 1:
              iden = verificarVazio(input('Digite o identificador do produto: '))
              adicionar_produto_a_prateleira(id, listaquantidade[iden])
              excluir_produto(iden)

            #VOLTAR PARA SESSÃO DE COMPRAS
            elif terceira_escolha == 2:
              break

            #TRATAMENTO DE ERRO
            else: 
              imprimir_erro_generico()
      
      #FINALIZAR COMPRA
      elif segunda_escolha == 3: 
        finalizar_compra()
        break
      
      #TRATAMENTO DE ERRO
      else: 
        imprimir_erro_generico()
  
  elif escolha == 2:
    cabecalho('Saindo do sistema... Volte Sempre!')
    break

  #TRATAMENTO DE ERRO
  else:
    imprimir_erro_generico()