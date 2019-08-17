# Comandos de Serviços de Git
## Consulta rápida a conteúdo de repositório (mesmo que de outras pessoas)
No trabalho ou consulta de repositórios públicos armazenados em serviços de Git, é comum apenas fazer uma consulta local aos arquivos rodando em sua máquina.

Vamos escolher um projeto qualquer no GitLab.
Entre neste [link](https://gitlab.com/explore) para escolher algum.
Ao entrar no projeto, busque o botão "clone" e copie o que estiver em "Clone with HTTPS".

Muito bem, você tem o endereço de um repositório para consultar ou ter localmente.
Retorne para o diretório dos testes e execute:
```bash
git clone <endereço que você acabou de copiar>
```

Os arquivos do repositório local serão baixados (pode demorar)...

## Preparando para usar o serviço de Git
Em seu terminal, adquira um par de chaves SSH com o comando:
```bash
ssh-keygen
```

O programa irá levar um tempo para processar, mas gerará arquivos com a chave pública e privada. Copie a chave pública.

## Crie uma conta no serviço de Git
No serviço de Git que for trabalhado, criar uma conta de usuário.
Nas configurações da sua conta, busque por SSH Keys.
Insira o código que você acabou de gerar.

## Vamos ao projeto online
No serviço de Git, crie novo projeto, escolha a opção com README incluso.

## No terminal
Retorne ao diretório de testes e crie uma nova pasta para "conectar" ao repositório remoto.
```bash
mkdir teste_gitlab
cd teste_gitlab
```

Inicie um repositório local vazio.
```bash
git init
```

Agora, a parte mais importante (para evitar problemas no acesso do repositório remoto - apesar de haver outras soluções).
ANTES de criar qual conteúdo no diretório local, com o git já iniciado, use o seguinte comando:
```bash
git remote add origin <link SSH que você irá copiar lá daquele botão azul no projeto online>
```

Para verificar se o link foi inserido corretamente, execute:
```bash
git remote -v
```

## Recuperando o repositório remoto para o seu local
Antes de começar a trabalhar localmente no projeto, execute:
```bash
git pull origin master
```
Isso significa: "Git, puxe do repositório remoto que chamei (por padrão) de 'origin' a branch master, pra branch master no meu repositório local".

## Agora sim, pode trabalhar!
Esse é o momento, considerando um fluxo de trabalho sozinho, em que tudo bem começar a realizar edições no projeto.

Use as mesmas práticas de commit para repositório local (explicados no arquivo [Commands_soft](Commands_soft.md).)

Quando terminar (ou quando quiser fazer um 'backup' no repositório remoto)...

## Envie atualizações para o repositório remoto!
Essa é uma das partes mais legais (pois é quando você verá seu código online!), mas uma das que pode acontecer mais problemas (se não tiver configurado direitinho o remote origin lá no início).

Com as devidas edições feitas localmente nas devidas branches, escolha a branch a qual quer enviar para o repositório remoto.
Se seu projeto tiver mais de uma branch e quiser que todas elas sejam enviadas para o repositório remoto, cada uma delas passará pelo mesmo comando.
Ok, o comando é simplesmente:
```bash
git push <nome do repositório remoto> <nome da branch que quer atualizar remotamente>
``` 

Se for a branch master e o padrão:
```bash
git push origin master
```
Isso significa: "Git, mande para o repositório remoto que chamei de 'origin' a branch master, a partir da branch master do meu repositório local".