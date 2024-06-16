<figure markdown="span">
    ![Logo](https://github.com/Ime-Jr/Guias/assets/56650001/57ebbc3c-dc6d-4ff9-b89d-b9b387ca37d5#only-dark){ width=300px }
    ![Logo](https://github.com/Ime-Jr/Guias/assets/56650001/57ebbc3c-dc6d-4ff9-b89d-b9b387ca37d5#only-light){ width=300px }
</figure>
  

<p align="center">

<h1 align="center"> IME Jr. </h1>
</p align="center" style="font-size: 20px; text-wrap: balance;">
O repositório de guias da Júnior tem como objetivo centralizar informações e guias para os membros da empresa. Desejamos que este repositório se torne uma referência para todos, servindo como um guia essencial para o desenvolvimento de suas atividades. Os guias podem abranger tanto aspectos técnicos, relacionados às ferramentas e workflows utilizados na empresa, quanto tópicos de interesse dos membros para aprendizado e compartilhamento. Com essa visão, o repositório está aberto a contribuições de todos os membros, e esperamos que todos colaborem com guias e informações relevantes.
</p>


## Organização 🧹💨
---

A parte escrita do seu guia deve ser feita em Markdown, um formato de escrita simples e fácil de aprender. Além disso, utilizamos o MkDocs para a organização e visualização dos guias como um site. O site é gerado a partir dos arquivos Markdown presentes no repositório e é atualizado automaticamente a cada push na branch main. Para contribuir com o repositório, basta criar um arquivo Markdown com o conteúdo do seu guia e submetê-lo via pull request.

Ao adicionar uma nova contribuição, você deve verificar em qual categoria o guia se encaixa e adicionar o arquivo na pasta correspondente. Caso a categoria não exista, você pode criar uma nova pasta e adicionar o arquivo lá. Se for o caso de uma nova categoria, você também deve adicioná-la ao arquivo mkdocs.yml para que o guia seja exibido no site e na barra de navegação.

As categorias existentes são:

- Matemática e Estatística
- Ciência de Dados
- Desenvolvimento Web
- Automação
- Design
- Outros

Por exemplo, um guia sobre "Como criar uma API REST com Flask" poderia ser adicionado na pasta Desenvolvimento Web, e um guia sobre "Como fazer um gráfico de barras no Python" poderia ser adicionado na pasta Ciência de Dados. Caso seu guia se encaixe em mais de uma categoria, escolha a que mais se adequa e adicione tags no arquivo Markdown para facilitar a busca.

Se o seu guia incluir código-fonte ou qualquer outro tipo de arquivo que não seja um arquivo Markdown, você pode adicionar esses arquivos na pasta `src/<categoria>/<nome-do-guia>`. Por exemplo, se o guia "Como criar uma API REST com Flask" incluir um arquivo app.py, você pode adicioná-lo na pasta `src/desenvolvimento-web/como-criar-uma-api-rest-com-flask/app.py`.

Se sentir a necessidade de modificar a estrutura do repositório, sinta-se livre para abrir uma issue e discutir a mudança com os demais membros.

## Como contribuir 🤝
---
Para contribuir neste projeto, basta criar uma pull request e aguardar que um administrador da organização avalie e forneça um feedback. Se a sua contribuição incluir algum material novo, é importante manter a organização atual do repositório devidamente documentada (afinal, o objetivo é ajudar os outros!). Sinta-se à vontade para compartilhar o que você achar necessário; todo conhecimento é bem-vindo!

Abaixo, temos um guia rápido de como contribuir com o repositório:

    1. Clone o repositório
    2. Crie uma nova branch  
    3. Adicione o guia na pasta correspondente
    4. Adicione tags ao guia, se necessário
    5. Adicione arquivos extras na pasta `src` se necessário
    6. Adicione seu nome e contato no arquivo `AUTHORS.md` na pasta do guia
    7. Faça um commit e push das alterações
    8. Crie uma pull request

Assim que a pull request for aprovada, o guia será adicionado ao site e estará disponível para todos os membros da empresa.

Se um conteúdo compartilhado é oferecido por terceiro, não se esqueça de dar os devidos créditos. Se deseja ser creditado por sua contribuição, adicione um arquivo `AUTHORS.md` na pasta do guia com seu nome e contato.

## Como rodar o site localmente 🖥️
---

Como dito anteriormente, o site é gerado a partir dos arquivos Markdown presentes no repositório. Para visualizar o site localmente, você precisará instalar o MkDocs e rodar o servidor localmente. Para isso, siga os passos abaixo:

1. Instale as dependências do MkDocs:
    ```bash
    pip install pyproject.toml
    ```
2. Rode o servidor local:
    ```bash 
    mkdocs serve
    ```
3. Acesse o site em `http://localhost:8000`

## Dúvidas e sugestões 🤔
---
Caso tenha alguma dúvida ou sugestão, sinta-se à vontade para usar a aba de discussões do repositório. Estamos sempre abertos a sugestões e feedbacks para melhorar o repositório e torná-lo mais útil para todos os membros da empresa.
