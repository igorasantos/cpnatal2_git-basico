# Comandos de software Git

Os comandos aqui usados não são necessariamente os mais rápidos de se praticar diariamente (há alguns que agrupam fases diferentes em uma mesma linha de comando). Mas para uma prática iniciante, vamos utilizar estes mesmo.

Com o Git CLI instalado em seu SO, seja [Linux](https://git-scm.com/download/linux) (geralmente, as distribuições o incluem nativamente), [Mac](https://git-scm.com/download/mac) ou [Windows](https://git-scm.com/download/win), abra o terminal do programa.

## First things first

Para começar, vamos praticar o "lado cliente".

Cadastre as configurações globais em sua máquina para te identificar nos commits (use suas informações reais!):
```bash
git config --global user.name "Seu Nome"
git config --global user.email "nome@email.com"
```

## Local de teste
Navegue até o diretório onde poderás fazer testes.

```bash
cd /home/yourUser
```

Crie um diretório vazio e acesse-o.
```bash
mkdir my_first_repo
cd my_first_repo
```

Inicie um repositório e verifique sua situação (ao usar Git diariamente, você fará essa consulta <em>muitas</em> vezes).
```bash
git init
git status
```

### Adicione um arquivo de teste
Agora crie um arquivo de texto em linguagem de marcação [Markdown](https://daringfireball.net/projects/markdown/) *(a linguagem que os repositórios dos serviços Git usam para renderizar texto)* chamado `README.md`:
```markdown
# Hello World!
Este é meu primeiro texto em Markdown.
```

Verifique novamente seu repositório:
```bash
git status
```

Muito bem. Há um arquivo que não está sendo acompanhado pelo Git. Vamos incluí-lo:
```bash
git add .
```

### Primeiro commit
Agora vamos ao primeiro commit:
```bash
git commit -m "msg significativa e curta sobre o que você fez"
```

Verifique novamente seu repositório:
```bash
git status
```

Analise agora como fica o registro dos commits:
```bash
git log
```

Muita informação na tela?
```bash
git log --oneline
```

Quer visualizar o "movimento" dos commits nas branches?
```bash
git log --oneline --graph
```
Como no momento só há 1 branch e 1 commit, só aparecerá um `*`.

### `.gitignore`

Em programação, é uma prática comum desenvolver sistemas que se conectem com um Banco de Dados, por exemplo. Para tal operação, utiliza-se senha de determinado usuário do BD. Durante o desenvolvimento, essa senha fica no diretório do projeto, onde há um repositório Git sendo acompanhado. O que fazer, por exemplo, para o Git não acompanhar esse arquivo com a senha?

Cria-se um arquivo `.gitignore` no diretório raíz do repositório.
Nele, você escreverá o caminho (a partir dessa raíz) para o arquivo ou diretório que desem ser ignorados.

Crie um segundo arquivo, chamado `vcNaoMePega.md` com o texto:
```markdown
### Oi, eu sei uma senha
Será?
```

Verifique (somente verifique) seu repositório:
```bash
git status
```

Agora crie o arquivo `.gitignore` (sem formato de arquivo ao final), com o conteúdo:
```markdown
vcNaoMePega.md
```

Mais uma vez:
```bash
git status
```

### Vamos navegar nas branches
Crie uma nova branch.
```bash
git branch teste
```

Verifique a branch atual:
```bash
git branch
```

Entre nela (o workspace mudará para o da branch teste - cuidado com arquivos ainda não commitados na branch anterior):
```bash
git checkout teste
```

Verifique a branch atual:
```bash
git branch
```

Na branch teste, crie o arquivo `teste_branch_teste.md` com o texto:
```markdown
Esse arquivo foi criado na branch teste.
```

Verifique o repositório:
```bash
git status
git log --oneline --graph --all
```
O `--all` aqui é para incluir os logs de todas as branches.


Commite-o:
```bash
git commit -m "test on test branch"
```

Agora retorne à branch main:
```bash
git checkout main
```

Verifique a branch atual:
```bash
git branch
```

Verifique o repositório:
```bash
git status
git log --oneline --graph --all
```

Agora implemente as mudanças da branch teste (uma nova funcionalidade que passou pelos testes e demais fases de implementação) na branch main:
```bash
git merge teste
```
Isso seria mais ou menos "Git, merge [from] <branch_source>"

Verifique o repositório:
```bash
git status
git log --oneline --graph --all
```


### Para praticar em casa
#### Diferença de conteúdo
Voltemos ao arquivo `README.md` e acrescente uma nova linha com o seguinte:
```markdown
E esta é a minha segunda linha.
```

Consulte a diferença de conteúdo entre o último commit nesse arquivo e o momento atual:
```bash
git diff README.md
```

#### Retificações
Vamos commitar a 2a linha do README com uma mensagem com erros:
```bash
git add .
git commit -m "eita, esqueci o q ia escrever"
```

No momento, as alterações foram efetivadas no repositório local. O conteúdo da mensagem que o descreve pode ser retificado assim:
```bash
git commit --amend -m "agora sim - 2a edição"
```

Crie o arquivo `unstage.md` com o conteúdo:
```markdown.md
Eu vou e volto.
```

Consulte o repositório:
```bash
git status
```

Ok, esse arquivo `unstage.md` no momento está na *Working area*. Vamos colocá-lo na *staged area* e depois desistir da sua adição (antes de commita-lo!).
```bash
git add .
```

Consulte:
```bash
git status
```

Faça o unstage:
Consulte:
```bash
git reset HEAD unstage.md
```

Consulte:
```bash
git status
```

Agora você desistiu mesmo do que você fez depois de determinado commit (aqui, voltaremos ao estágio do último commit):
```bash
git checkout -- unstage.md
```

Consulte:
```bash
git status
```

### Tags
Funcionamento bem parecido com os comandos relativos a branches. Vale a pena praticar também.

### Conflito de commits em equipe
Esse tópico já é assunto de outra palestra ;)