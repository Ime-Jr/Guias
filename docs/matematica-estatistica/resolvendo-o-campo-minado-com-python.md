contribuitors: jedmario16
# Resolvendo o Campo Minado com Python
----
Neste guia, você aprenderá a implementar um jogo de Campo Minado utilizando Python e a resolver o jogo de forma eficiente. Meu objetivo é apresentar como podemos utilizar diferentes modelagens matemáticas e algoritmos para resolver o jogo de forma eficiente. Cada um dos métodos apresentados tem suas vantagens e desvantagens, e exigem um certo nivel de conhecimento x e y, mas nada proibitivo.
Este guia é estruturado da seguinte forma:

- Parte 1: Implementação do jogo de Campo Minado
> Nesta parte, apresento uma implementação do jogo de Campo Minado utilizando Python. A implementação é feita de forma simples e eficiente, e é utilizada como base para os métodos de resolução apresentados nas próximas partes.

- Parte 2: Resolvendo o Campo Minado com Teoria da Informação
> Nesta parte, apresento um método para resolver o jogo de Campo Minado utilizando Teoria da Informação. A Teoria da Informação é uma área da matemática que estuda a quantificação da informação e é utilizada em diversas áreas, como ciência da computação, estatística e física.

- Parte 3: Resolvendo o Campo Minado com Busca em Largura
> Nesta parte, apresento um método para resolver o jogo de Campo Minado utilizando Busca em Largura. A Busca em Largura é um algoritmo de busca em grafos que é utilizado para encontrar o caminho mais curto entre dois vértices de um grafo.

- Parte 4: Resolvendo o Campo Minado com Redes Neurais
> Nesta parte, apresento um método para resolver o jogo de Campo Minado utilizando Redes Neurais. As Redes Neurais são modelos computacionais inspirados no sistema nervoso dos animais e são utilizadas em diversas áreas, como reconhecimento de padrões, processamento de linguagem natural e visão computacional. Além disso, irei mostrar a relação entre as Redes Neurais e outros métodos de resolução apresentados neste guia.

## Parte 1: Implementação do jogo de Campo Minado
----
Antes de começarmos, vamos entender como funciona o jogo de Campo Minado. O jogo é composto por uma matriz de células, onde cada célula pode estar vazia ou conter uma mina. O objetivo do jogo é descobrir todas as células vazias sem detonar uma mina. Para isso, o jogador pode clicar em uma célula para revelar seu conteúdo. Se a célula clicada contiver uma mina, o jogo acaba e o jogador perde. Se a célula clicada estiver vazia, o jogo continua e o jogador pode clicar em outras células até que todas as células vazias sejam reveladas.

Ao clicar em uma célula vazia, existem duas possibilidades: ou há minas adjacentes à célula, ou não há. Se houver minas adjacentes à célula, a célula exibirá o número de minas adjacentes. Se não houver minas adjacentes, a célula será revelada e as células adjacentes também serão reveladas automaticamente, de forma recursiva. Em outras palavras, quando não há minas adjacentes, o jogo revela todas as células adjacentes até que a fronteira de minas seja atingida.

<div class="examples" style="display: flex; justify-content: space-between" markdown="1">
<figure markdown="span">
    ![alt text](/../assets/images/matematica-estatistica/sudoku-1.png){ width=200}
    <figcaption>Figura 1: Exemplo de jogo de Campo Minado 3x3 , após clicar na célula (2, 2)</figcaption>
</figure>
<figure markdown="span">
    ![alt text](image.png){ width=200}
    <figcaption>Figura 2: Exemplo de Campo Minado após clicar na célula (2,2) <br> Astrisco(*) representa minas</figcaption>
</figure>
</div>

Nas imagens acima, a figura 1 mostra um exemplo de jogo de Campo Minado 3x3, onde o jogador clicou na célula (2, 2). Neste caso, foram reveladas duas
bombas adjacentes à célula clicada. A figura 2 mostra o mesmo jogo após clicar na mesma célula, mas desta vez, a célula clicada não possui bombas adjacentes. Neste caso, todas as células adjacentes à célula clicada foram reveladas automaticamente.

!!! Nota
    Neste guia, iremos sempre considerar que o índice da primeira linha e coluna é 0. Ou seja, a célula (0, 0) é a célula no canto superior esquerdo da matriz.

Agora que entendemos as regras do jogo, vamos implementar o jogo de Campo Minado em Python. A nossa estratégia será utilizar POO para criar uma classe que representará o jogo e seus métodos.

```Python
from random import sample

class CampoMinado:
    __BOMB_INDICATOR = "*"
    __UNKNOWN_CELL_INDICATOR = "?"

    def __init__(self, rows, cols, bombs):
        self.nrows = rows
        self.ncols = cols
        self.nbombs = bombs
        self.board = [self.__UNKNOWN_CELL_INDICATOR for _ in range(self.ncols) for _ in range(self.nrows)]
        self.__secret_board = self.generate_secret_board()


    def generate_secret_board(self):
        """
        Gera um tabuleiro secreto com as bombas em posições aleatórias
        """
        # Inicializa o tabuleiro com todas as células vazias
        board = [0 for _ in range(self.nrows) for __ in range(self.ncols)]

        # Cria uma amostra aleatória de índices e insere as bombas no tabuleiro
        bombs_index = sample(range(self.nrows*self.ncols), self.nbombs)
        for bi in bombs_index:
            board[bi] = self.__BOMB_INDICATOR
        return board
```

O código acima implementa a classe CampoMinado, que representa o jogo de Campo Minado. A classe possui um construtor que inicializa o tabuleiro do jogo com células desconhecidas e gera um tabuleiro secreto com as bombas. O método generate_secret_board() é responsável por gerar o tabuleiro secreto com as bombas de forma aleatória.
Nós também definimos alguns atributos privados, como __BOMB_INDICATOR e __UNKNOWN_CELL_INDICATOR, que são utilizados para representar as bombas e as células desconhecidas no tabuleiro, respectivamente.
Vamos testar a nossa implementação do jogo de Campo Minado:

```Python
game = CampoMinado(3, 3, 2)
print(game.board)
# Vamos também imprimir o tabuleiro secreto apenas para ver as bombas
print(game._CampoMinado__secret_board)
```

O código acima cria um jogo de Campo Minado 3x3 com 2 bombas e imprime o tabuleiro do jogo e o tabuleiro secreto com as bombas. A saída do código será algo como:

```
['?', '?', '?', '?', '?', '?', '?', '?', '?']
[0, 0, 0, 0, 0, 0, '*', 0, '*']
```
!!! Nota
    Aqui, estamos tratando o tabuleiro como uma lista unidimensional. Uma outra alternativa seria representar o tabuleiro como uma lista de listas, onde cada lista interna representa uma linha do tabuleiro. A escolha entre as duas representações não irá afetar a implementação dos métodos de resolução do jogo.
    A minha escolha por representar o tabuleiro como uma lista unidimensional é que o índice de uma célula é calculado como `i = row * ncols + col`, o que facilita a conversão entre as coordenadas (row, col) e o índice da célula na lista.

Nossos testes nos revelam duas coisas que precisaremos nos preocupar na próxima parte: 1. Uma boa visualização do tabuleiro e 2. A implementação de um método para revelar as células do tabuleiro. Como veremos adiante, o método para revelar as células do tabuleiro é um tanto complexo, então vamos nos concentrar em implementar um método para visualizar o tabuleiro, o que nos permitirá validar a nossa implementação do jogo.

```Python
# ... outros imports
import colorama

class CampoMinado:
    # ... Outros atributos privados
    DISPLAY_CELL_CHARS = 6 # Quantidade de caracteres para exibir cada célula

    # ... outros métodos

    def colorize(self, color_code, content):
        # O dict COLORS_MAP mapeia os códigos de cores aos códigos ANSI.
        # Você pode adicionar mais cores ao dict, se desejar. As chaves são possíveis 
        # valores na célula e os valores são os códigos ANSI correspondentes.
        # Desta forma, verde será usado para células vazias, ciano para células com 1 mina adjacente, etc.
        color_code = str(color_code)
        COLORS_MAP = {
            "0": colorama.Fore.GREEN,
            "1": colorama.Fore.CYAN,
            "2": colorama.Fore.BLUE,
            "3": colorama.Fore.RED,
            "4": colorama.Fore.RED,
            "5": colorama.Fore.MAGENTA,
            "6": colorama.Fore.MAGENTA,
            self.__BOMB_INDICATOR: colorama.Fore.RED,
            self.__UNKNOWN_CELL_INDICATOR: colorama.Fore.WHITE,
            "C": colorama.Fore.WHITE # Usado para as colunas de coordenadas
        }

        return f"{COLORS_MAP[color_code]}{content}{colorama.Fore.RESET}"

    def show_board(self, target_board: list):
        """
        Mostra o tabuleiro na tela
        """
        board_str = f"{colorama.Back.BLACK}" # Adiciona um fundo preto ao tabuleiro
        # Calcula a largura da linha do tabuleiro. Adicionamos 1 ao número de colunas para incluir as coordenadas,
        # um ao número de caracteres por célula para incluir a '|' entre as células e um ao final para incluir o último '|'
        row_width = (self.ncols+1) * (self.DISPLAY_CELL_CHARS + 1) + 1

        # Agora, vamos gerar um pequeno cabeçalho com as coordenadas das colunas
        header = ""
        header += f" Campo Minado {self.nrows}x{self.ncols} ".center(row_width, "-") + "\n"
        header += "-" * row_width + "\n" # Adiciona uma linha horizontal para separar o cabeçalho do tabuleiro
        # Gera os índices das colunas e os formata para exibição, aplicando a função colorize e centralizando o texto
        header_col_indexer = [self.colorize(content=str(v).center(self.DISPLAY_CELL_CHARS), color_code="C") for v in range(self.ncols)]
        # Veja que aqui adicionamos uma coluna adicional com '/' para separar as coordenadas das células e as células em si. 
        header += f"|{'/'.center(self.DISPLAY_CELL_CHARS)}|" + "|".join(c for c in header_col_indexer) + "|\n" 
        header += "-"*row_width + "\n"

        # finalmente, vamos adicionar o cabeçalho ao tabuleiro
        board_str += header

        # Agora, vamos adicionar as linhas do tabuleiro
        for ri in range(self.nrows):
            start_index = self.cols * ri
            end_index = self.ncols * (ri + 1)         
            cells = [self.colorize(content=str(v).center(self.DISPLAY_CELL_CHARS), color_code=v) for v in target_board[start_index:end_index]]
            # Vamos adicioar, de uma vez só, a linha e sua respectiva coordenada na coluna
            board_str += f"|{self.colorize('C', str(ri).center(self.DISPLAY_CELL_CHARS))}|" + "|".join(c for c in cells) + "|\n"
        board_str += f"{colorama.Back.RESET}"
        print(board_str)

    @property
    def show(self):
        return self.show_board(target_board=self.board)

    @property
    def show_answer(self):
        self.show_board(target_board=self.__secret_board)
``` 

O código acima implementa o método show_board(), que é responsável por exibir o tabuleiro do jogo na tela. O método gera uma representação visual do tabuleiro, com cores diferentes para as células vazias, as células com minas adjacentes e as bombas. O método utiliza a biblioteca colorama para adicionar cores ao texto exibido no terminal. Além disso, o método show_board() também cria um cabeçalho, uma linha e uma coluna de coordenadas para facilitar a visualização do tabuleiro. Além disso, criamos duas propriedades, show e show_answer, que exibem o tabuleiro do jogo e o tabuleiro secreto, respectivamente. Vamos testar a nossa implementação do método show_board():

```Python
game = CampoMinado(3, 3, 2)
game.show
game.show_answer
```

Você deve ver algo como:

```bash
------ Campo Minado 3x3 -----
-----------------------------
|  /   |  0   |  1   |  2   |
-----------------------------
|  0   |  ?   |  ?   |  ?   |
|  1   |  ?   |  ?   |  ?   |
|  2   |  ?   |  ?   |  ?   |
-----------------------------
```
E o tabuleiro secreto, onde no lugar de '?' você verá as bombas:

```bash
------ Campo Minado 3x3 -----
-----------------------------
|  /   |  0   |  1   |  2   |
-----------------------------
|  0   |  *   |  0   |  0   |
|  1   |  *   |  0   |  0   |
|  2   |  0   |  0   |  0   |
-----------------------------
```


Ótimo! Estamos quase prontos para começar a implementar os métodos de resolução do jogo. Agora podemos nos concentrar em implementar um método para revelar as células do tabuleiro. A estratégia que utilizarei será o seguinte: Primeiro, criarei um método que retorna o índice de todas as células válidas adjacentes a uma célula dada. Em seguida, criarei um método que conta a quantidade de bombas adjacentes. Neste momento, iremos intercalar o uso de indices e coordenadas(linha, coluna), então vamos criar um método para converter entre os dois sistemas de referência.

```Python
class CampoMinado:
    # ... Outros métodos

    def coord_to_index(self, row, col):
        """
        Converte as coordenadas (linha, coluna) em um índice da lista unidimensional
        """
        return row * self.ncols + col
    
    def index_to_coord(self, index):
        """
        Converte um índice da lista unidimensional em coordenadas (linha, coluna)
        """
        return divmod(index, self.ncols) 
    
    def get_valid_adjacent_cells(self, row, col):
        """
        Retorna os índices das células válidas adjacentes à célula (row, col)
        """
        cindex = self.coord_to_index(row, col)

        adjacent_indexes = [
            cindex-self.nrows-1, cindex-self.nrows, cindex-self.nrows+1,
            cindex-1,            -1000             ,cindex+1,
            cindex+self.nrows-1, cindex+self.nrows, cindex+self.nrows+1
        ] 

        # a constante -1000 é um valor simbolico para que os indices fiquem coerentes.
        # Agora, deveremos remover os indices de celulas vizinhas seguindo o seguinte criterio:
        # 1. Se o index for negativo (significa que nao existe linha 'acima', ou eh a constante simbolica)
        # 2. Se o index for maior q o tabuleiro(neste caso, nao existe linha 'abaixo')
        # 3. Se cindex % ncol = 1, deveremos remover os indices(do adjacent_indexes) 2, 5, e 8
        # 4. se cindex % ncol = ncol, deveremos remover os indices(do adjacent_indexes) 0, 3 e 6
        # obs: os passos 3 e 4 usam cindex(o valor de input). Ambos referem-se ao caso onde
        # o indice de target está ou na coluna final, ou na coluna inicial. Logo nao existe "esquerda" ou "direita"
        
        # Como os passos  3. e 4. removem valores do vetor de indice usando seus indices, vamos começar por eles 
        to_remove = []
        if cindex % self.ncols == self.ncols - 1:
            to_remove.extend([2, 5, 8])
        elif cindex % self.ncols == 0:
            to_remove.extend([0, 3, 6])

        # Agora, vamos remover os indices que nao existem
        # board_ index = indice da celula no tabuleiro; adj_index = indice no vetor de adjacent_indexes
        adjacent_cells = [board_index for adj_index, board_index in enumerate(adjacent_indexes) if board_index >= 0 and board_index < self.nrows*self.ncolumns and adj_index not in to_remove]
        return adjacent_cells
    
    def count_adjacent_bombs(self, row, col):
        """
        Conta o número de bombas adjacentes à célula (row, col)
        """
        cindex = self.coord_to_index(row, col)

        adjacent_cells = self.get_valid_adjacent_cells(row, col)
        return sum(1 for adj_index in adjacent_cells if self.__secret_board[adj_index] == self.__BOMB_INDICATOR)

    def recursive_count_adjacent_bombs(self, row, col):
        """
        Conta o número de bombas adjacentes à célula (row, col) e às células adjacentes a ela, de forma recursiva
        """
        bombs_count = self.count_adjacent_bombs(row, col)
        cindex = self.coord_to_index(row, col)
        self.board[cindex] = bombs_count
        if b_count > 0:
            return
        
        adjacent_cells = self.get_valid_adjacent_cells(row, col)
        for adj_index in adjacent_cells:
            adj_row, adj_col = self.index_to_coord(adj_index)
            if self.board[adj_index] == self.__UNKNOWN_CELL_INDICATOR:
                self.recursive_count_adjacent_bombs(adj_row, adj_col)
        return
```

Uuuufa! Muita coisa, não é? Vamos entender o que fizemos. Primeiro, criamos dois métodos, coord_to_index() e index_to_coord(), que convertem entre coordenadas (linha, coluna) e índices da lista unidimensional. Em seguida, criamos o método get_valid_adjacent_cells(), que retorna os índices das células válidas adjacentes a uma célula dada. O método count_adjacent_bombs() conta o número de bombas adjacentes a uma célula dada. Por fim, o método recursive_count_adjacent_bombs() conta o número de bombas adjacentes a uma célula dada e às células adjacentes a ela, de forma recursiva. Este método é responsável por revelar as células do tabuleiro que não possuem bombas adjacentes. A Noticia boa é que a nossa implementação do metodo `reveal` é bem simples, então vamos implementá-lo e testá-lo.

```Python
class GameOverError(Exception):
    pass 

class CampoMinado:
    # ... Outros métodos

    def reveal(self, row, col):
        """
        Revela a célula (row, col) e as células adjacentes a ela
        """
        cindex = self.coord_to_index(row, col)
        if self.__secret_board[cindex] == self.__BOMB_INDICATOR:
            raise GameOverError("Você clicou em uma bomba! Game Over!")
            return
        self.recursive_count_adjacent_bombs(row, col)
```

O método reveal() é responsável por revelar a célula (row, col) e as células adjacentes a ela. Se a célula clicada contiver uma bomba, o método lança uma exceção GameOverError. Vamos testar a nossa implementação do método reveal():

```Python
game = CampoMinado(5, 5, 3)
game.show
game.reveal(0, 1)
game.show
```

Você deve ver algo como:

```bash
------------- Campo Minado 5x5 ------------
-------------------------------------------
|  /   |  0   |  1   |  2   |  3   |  4   |
-------------------------------------------
|  0   |  0   |  0   |  1   |  ?   |  ?   |
|  1   |  0   |  0   |  1   |  ?   |  ?   |
|  2   |  1   |  1   |  2   |  ?   |  ?   |
|  3   |  ?   |  ?   |  ?   |  ?   |  ?   |
|  4   |  ?   |  1   |  ?   |  ?   |  ?   |
-------------------------------------------
```

Para que você possa testar a implementação do jogo com um pouco mais de calma, vamos criar um método que permita ao jogador interagir com o jogo. Vamos implementar um método play() que solicita ao jogador as coordenadas da célula a ser revelada e revela a célula. O método play() deve continuar solicitando as coordenadas até que o jogador clique em uma bomba ou revele todas as células vazias. Vamos implementar o método play() e testá-lo:

```Python
import os

class CampoMinado:
    # ... Outros métodos

    def play(self):
        """
        Permite ao jogador interagir com o jogo
        """
        while True:
            self.show
            row = int(input("Digite a linha da célula a ser revelada: "))
            col = int(input("Digite a coluna da célula a ser revelada: "))
            try:
                os.system('cls' if os.name == 'nt' else 'clear')
                self.reveal(row, col)
            except GameOverError as e:
                print(e)
                break
            if self.board.count(self.__UNKNOWN_CELL_INDICATOR) == self.nbombs:
                print("Parabéns! Você revelou todas as células vazias!")
                break
```

O método play() exibe o tabuleiro do jogo e solicita ao jogador as coordenadas da célula a ser revelada. O método continua solicitando as coordenadas até que o jogador clique em uma bomba ou revele todas as células vazias. 

??? example "Implementação do jogo de Campo Minado"
    ```Python
    from random import sample
    from typing import Literal
    import colorama
    import os

    class GameOverError(Exception):
        pass 

    class CampoMinado:
        __BOMB_INDICATOR = "*"
        __UNKNOWN_CELL_INDICATOR = "?"
        DISPLAY_CELL_CHARS = 6 # Quantidade de caracteres para exibir cada célula


        def __init__(self, rows, cols, bombs):
            self.nrows = rows
            self.ncols = cols
            self.nbombs = bombs
            self.board = [self.__UNKNOWN_CELL_INDICATOR for _ in range(self.ncols) for _ in range(self.nrows)]
            self.__secret_board = self.generate_secret_board()


        def generate_secret_board(self):
            """
            Gera um tabuleiro secreto com as bombas em posições aleatórias
            """
            # Inicializa o tabuleiro com todas as células vazias
            board = [0 for _ in range(self.nrows) for __ in range(self.ncols)]

            # Cria uma amostra aleatória de índices e insere as bombas no tabuleiro
            bombs_index = sample(range(self.nrows*self.ncols), self.nbombs)
            for bi in bombs_index:
                board[bi] = self.__BOMB_INDICATOR
            return board

        def colorize(self, color_code, content):
            # O dict COLORS_MAP mapeia os códigos de cores aos códigos ANSI.
            # Você pode adicionar mais cores ao dict, se desejar. As chaves são possíveis 
            # valores na célula e os valores são os códigos ANSI correspondentes.
            # Desta forma, verde será usado para células vazias, ciano para células com 1 mina adjacente, etc.
            color_code = str(color_code)
            COLORS_MAP = {
                "0": colorama.Fore.GREEN,
                "1": colorama.Fore.CYAN,
                "2": colorama.Fore.BLUE,
                "3": colorama.Fore.RED,
                "4": colorama.Fore.RED,
                "5": colorama.Fore.MAGENTA,
                "6": colorama.Fore.MAGENTA,
                self.__BOMB_INDICATOR: colorama.Fore.RED,
                self.__UNKNOWN_CELL_INDICATOR: colorama.Fore.WHITE,
                "C": colorama.Fore.WHITE # Usado para as colunas de coordenadas
            }

            return f"{COLORS_MAP[color_code]}{content}{colorama.Fore.RESET}"

        def show_board(self, target_board: list):
            """
            Mostra o tabuleiro na tela
            """
            board_str = f"{colorama.Back.BLACK}" # Adiciona um fundo preto ao tabuleiro
            # Calcula a largura da linha do tabuleiro. Adicionamos 1 ao número de colunas para incluir as coordenadas,
            # um ao número de caracteres por célula para incluir a '|' entre as células e um ao final para incluir o último '|'
            row_width = (self.ncols+1) * (self.DISPLAY_CELL_CHARS + 1) + 1

            # Agora, vamos gerar um pequeno cabeçalho com as coordenadas das colunas
            header = ""
            header += f" Campo Minado {self.nrows}x{self.ncols} ".center(row_width, "-") + "\n"
            header += "-" * row_width + "\n" # Adiciona uma linha horizontal para separar o cabeçalho do tabuleiro
            header_col_indexer = [self.colorize(content=str(v).center(self.DISPLAY_CELL_CHARS), color_code="C") for v in range(self.ncols)]
            header += f"|{'/'.center(self.DISPLAY_CELL_CHARS)}|" + "|".join(c for c in header_col_indexer) + "|\n" 
            header += "-"*row_width + "\n"

            # finalmente, vamos adicionar o cabeçalho ao tabuleiro
            board_str += header

            # Agora, vamos adicionar as linhas do tabuleiro
            for ri in range(self.nrows):
                start_index = self.ncols * ri
                end_index = self.ncols * (ri + 1)         
                cells = [self.colorize(content=str(v).center(self.DISPLAY_CELL_CHARS), color_code=v) for v in target_board[start_index:end_index]]
                # Vamos adicioar, de uma vez só, a linha e sua respectiva coordenada na coluna
                board_str += f"|{self.colorize('C', str(ri).center(self.DISPLAY_CELL_CHARS))}|" + "|".join(c for c in cells) + "|\n"
            board_str += f"{colorama.Back.RESET}"
            print(board_str)

        @property
        def show(self):
            return self.show_board(target_board=self.board)

        @property
        def show_answer(self):
            self.show_board(target_board=self.__secret_board)
            
        def coord_to_index(self, row, col):
            """
            Converte as coordenadas (linha, coluna) em um índice da lista unidimensional
            """
            return row * self.ncols + col
        
        def index_to_coord(self, index):
            """
            Converte um índice da lista unidimensional em coordenadas (linha, coluna)
            """
            return divmod(index, self.ncols) 
        
        def get_valid_adjacent_cells(self, row, col):
            """
            Retorna os índices das células válidas adjacentes à célula (row, col)
            """
            cindex = self.coord_to_index(row, col)

            adjacent_indexes = [
                cindex-self.nrows-1, cindex-self.nrows, cindex-self.nrows+1,
                cindex-1,            -1000             ,cindex+1,
                cindex+self.nrows-1, cindex+self.nrows, cindex+self.nrows+1
            ] 

            # a constante -1000 é um valor simbolico para que os indices fiquem coerentes.
            # Agora, deveremos remover os indices de celulas vizinhas seguindo o seguinte criterio:
            # 1. Se o index for negativo (significa que nao existe linha 'acima', ou eh a constante simbolica)
            # 2. Se o index for maior q o tabuleiro(neste caso, nao existe linha 'abaixo')
            # 3. Se cindex % ncol = 1, deveremos remover os indices(do adjacent_indexes) 2, 5, e 8
            # 4. se cindex % ncol = ncol, deveremos remover os indices(do adjacent_indexes) 0, 3 e 6
            # obs: os passos 3 e 4 usam cindex(o valor de input). Ambos referem-se ao caso onde
            # o indice de target está ou na coluna final, ou na coluna inicial. Logo nao existe "esquerda" ou "direita"
            
            # Como os passos  3. e 4. removem valores do vetor de indice usando seus indices, vamos começar por eles 
            to_remove = []
            if cindex % self.ncols == self.ncols - 1:
                to_remove.extend([2, 5, 8])
            elif cindex % self.ncols == 0:
                to_remove.extend([0, 3, 6])

            # Agora, vamos remover os indices que nao existem
            # board_ index = indice da celula no tabuleiro; adj_index = indice no vetor de adjacent_indexes
            adjacent_cells = [board_index for adj_index, board_index in enumerate(adjacent_indexes) if board_index >= 0 and board_index < self.nrows*self.ncols and adj_index not in to_remove]
            return adjacent_cells
        
        def count_adjacent_bombs(self, row, col):
            """
            Conta o número de bombas adjacentes à célula (row, col)
            """
            cindex = self.coord_to_index(row, col)

            adjacent_cells = self.get_valid_adjacent_cells(row, col)
            return sum(1 for adj_index in adjacent_cells if self.__secret_board[adj_index] == self.__BOMB_INDICATOR)

        def recursive_count_adjacent_bombs(self, row, col):
            """
            Conta o número de bombas adjacentes à célula (row, col) e às células adjacentes a ela, de forma recursiva
            """
            bombs_count = self.count_adjacent_bombs(row, col)
            cindex = self.coord_to_index(row, col)
            self.board[cindex] = bombs_count
            if bombs_count > 0:
                return
            
            adjacent_cells = self.get_valid_adjacent_cells(row, col)
            for adj_index in adjacent_cells:
                adj_row, adj_col = self.index_to_coord(adj_index)
                if self.board[adj_index] == self.__UNKNOWN_CELL_INDICATOR:
                    self.recursive_count_adjacent_bombs(adj_row, adj_col)
            return
        
        def reveal(self, row, col):
            """
            Revela a célula (row, col) e as células adjacentes a ela
            """
            cindex = self.coord_to_index(row, col)
            if self.__secret_board[cindex] == self.__BOMB_INDICATOR:
                raise GameOverError("Você clicou em uma bomba! Game Over!")
                return
            self.recursive_count_adjacent_bombs(row, col)
            
        def play(self):
            """
            Permite ao jogador interagir com o jogo
            """
            while True:
                self.show
                row = int(input("Digite a linha da célula a ser revelada: "))
                col = int(input("Digite a coluna da célula a ser revelada: "))
                try:
                    os.system("cls" if os.name == "nt" else "clear")
                    self.reveal(row, col)
                except GameOverError as e:
                    print(e)
                    self.show_answer
                    self.show
                    break
                if self.board.count(self.__UNKNOWN_CELL_INDICATOR) == self.nbombs:
                    print("Parabéns! Você revelou todas as células vazias!")
                    self.show_answer
                    self.show
                    break
    ```

## Parte 2 - Usando sistemas de equações lineares para resolver o Campo Minado
----
TODO: Escrever a parte 2