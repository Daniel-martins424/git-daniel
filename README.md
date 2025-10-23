🧩 Aula Prática -- Git Local (sem GitHub)
========================================

🎯 Objetivo
-----------

Aprender a utilizar o **Git** localmente para versionar projetos, criando commits, branches e manipulando o histórico de forma segura.

🧱 1. Configuração inicial
--------------------------

Esses comandos configuram o nome e o e-mail do usuário (necessário para registrar os commits).

```
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@exemplo.com"
git config --global core.editor "code --wait"   # Define o VS Code como editor padrão (opcional)
git config --list                                # Verifica as configurações atuais

```

📂 2. Criar e iniciar um repositório
------------------------------------

```
mkdir meu_projeto
cd meu_projeto
git init

```

> O comando `git init` cria um repositório local, gerando a pasta oculta `.git`.

🏷️ 3. Alterar a branch padrão de `master` para `main`
------------------------------------------------------

Por padrão, o Git pode criar a branch inicial como master.  

Para padronizar e seguir boas práticas, altere para main:

```
git branch -m master main

```

Se quiser definir **main** como padrão para novos repositórios:

```
git config --global init.defaultBranch main

```

📄 4. Criar arquivos e verificar status
---------------------------------------

```
echo "Meu primeiro arquivo" > readme.txt
git status

```

> `git status` mostra arquivos novos, modificados ou prontos para commit.

🧺 5. Adicionar arquivos à área de staging
------------------------------------------

```
git add readme.txt       # adiciona um arquivo específico
git add .                # adiciona todos os arquivos do diretório
git status

```

> A área de staging é onde os arquivos ficam "preparados" antes do commit.

💾 6. Fazer o primeiro commit
-----------------------------

```
git commit -m "Primeiro commit - adiciona readme.txt"

```

> Um commit é o "salvamento" oficial no histórico do repositório.

🔍 7. Ver histórico e detalhes
------------------------------

```
git log
git log --oneline
git show

```

> Use `--oneline` para visualizar um resumo simplificado.

✏️ 8. Editar arquivos e registrar mudanças
------------------------------------------

```
echo "Adicionando nova linha" >> readme.txt
git status
git diff
git add readme.txt
git commit -m "Atualiza readme.txt com nova linha"

```

> `git diff` mostra as diferenças entre a versão atual e a anterior.

♻️ 9. Desfazer mudanças
-----------------------

```
git restore readme.txt              # descarta mudanças não adicionadas
git restore --staged readme.txt     # remove da área de staging

```

> Ideal para corrigir erros antes de um commit.

🌿 10. Criar e alternar entre branches
--------------------------------------

```
git branch                         # lista branches
git branch nova_funcionalidade     # cria nova branch
git switch nova_funcionalidade     # muda para ela

```

> Cada branch é uma linha independente de desenvolvimento.

🧬 11. Fazer commits em outra branch
------------------------------------

```
echo "Nova feature" > feature.txt
git add feature.txt
git commit -m "Adiciona nova feature"

```

🔀 12. Voltar e mesclar mudanças
--------------------------------

```
git switch main
git merge nova_funcionalidade

```

> Junta as alterações da branch `nova_funcionalidade` na `main`.

🗑️ 13. Excluir branches locais
-------------------------------

```
git branch -d nova_funcionalidade

```

🧹 14. Ignorar arquivos com `.gitignore`
----------------------------------------

Crie um arquivo chamado `.gitignore` e adicione:

```
*.log
*.tmp
node_modules/

```

Depois:

```
git add .gitignore
git commit -m "Adiciona arquivo .gitignore"

```

🧠 15. Visualizar informações úteis
-----------------------------------

```
git status
git log --oneline --graph --decorate
git diff
git show HEAD

```

> `--graph` mostra o histórico com ramificações visualmente.

💡 16. Exemplo de fluxo completo
--------------------------------

```
git init
echo "Aula prática Git local" > readme.txt
git add .
git commit -m "Primeiro commit"
git branch dev
git switch dev
echo "Nova versão em desenvolvimento" >> readme.txt
git add .
git commit -m "Atualiza versão dev"
git switch main
git merge dev
git log --oneline --graph

```

🛰️ Aula Prática -- Git Remote (com GitHub)
==========================================

🎯 Objetivo
-----------

Aprender a conectar o repositório local a um repositório remoto (GitHub), enviar (`push`) e receber (`pull`) alterações, e entender o fluxo básico de colaboração.

☁️ 17. Criar um repositório no GitHub
-------------------------------------

1.  Acesse o [GitHub](https://github.com/ "null") e faça login.

2.  Clique em "New" (Novo) ou no ícone de `+` no canto superior e selecione "New repository".

3.  Dê um nome ao repositório (ex: `meu_projeto`).

4.  Escolha se será Público ou Privado.

5.  **Importante:** NÃO marque as opções "Add a README file", "Add .gitignore" ou "Choose a license", pois já temos nosso projeto local pronto.

6.  Clique em "Create repository".

🔗 18. Conectar o repositório local ao remoto
---------------------------------------------

Na página do seu repositório recém-criado no GitHub, copie a URL (HTTPS ou SSH).

No seu terminal (dentro da pasta `meu_projeto`), execute:

```
# Substitua a URL pela URL do SEU repositório
git remote add origin [https://github.com/seu-usuario/meu_projeto.git](https://github.com/seu-usuario/meu_projeto.git)

# Verifica se o remoto foi adicionado
git remote -v

```

> `origin` é o nome padrão (um apelido) para a conexão com o repositório remoto.

📤 19. Enviar (Push) pela Primeira Vez
--------------------------------------

Vamos enviar nossa branch `main` local para o repositório `origin` (GitHub).

```
git push -u origin main

```

> O `-u` (ou `--set-upstream`) serve para linkar sua branch local `main` com a branch remota `main`. Você só precisa fazer isso na primeira vez.

🔄 20. O Fluxo de Trabalho: Edição, Commit e Push (2.3 e 2.4)
-------------------------------------------------------------

Este é o fluxo que você usará diariamente.

1\. Edição da Documentação (Local)

Edite seus arquivos (ex: README.md ou readme.txt).

```
echo "Adicionando link do GitHub" >> readme.txt

```

2\. Commit (Local)

Adicione e "salve" a alteração localmente.

```
git add readme.txt
git commit -m "Adiciona link do repositório no readme"

```

3\. Push das Alterações (Remoto)

Envie seus commits locais para o GitHub.

```
git push

```

> Como já usamos `-u` antes, o Git agora sabe que `git push` deve enviar a branch `main` para `origin`.

📥 21. Como integrar o Git Local ao GitHub (Clone)
--------------------------------------------------

Se o projeto já existe no GitHub e você quer baixá-lo para sua máquina (ou se um colaborador quiser baixar):

```
# Apague sua pasta local (se for o caso) e suba um nível
cd ..
# rm -rf meu_projeto (CUIDADO: isso apaga a pasta)

# Clone o projeto a partir do GitHub
git clone [https://github.com/seu-usuario/meu_projeto.git](https://github.com/seu-usuario/meu_projeto.git)

# Entre na pasta recém-criada
cd meu_projeto

```

> `git clone` automaticamente baixa o projeto e já configura o `origin`.

🤝 22. Como adicionar colaboradores ao repositório (Passo 3)
------------------------------------------------------------

Para que outras pessoas possam fazer `push` no seu repositório privado, você precisa adicioná-las como colaboradoras:

1.  No GitHub, vá até o seu repositório.

2.  Clique em **Settings** (Configurações).

3.  Na barra lateral, clique em **Collaborators** (Colaboradores).

4.  Clique em **Add people** (Adicionar pessoas).

5.  Digite o nome de usuário, nome completo ou e-mail do GitHub do seu colega.

6.  Clique no usuário correto e depois em "Add [usuário] to this repository".

7.  O usuário receberá um convite por e-mail que deverá ser aceito.

📥 23. Receber atualizações de colaboradores (Pull)
---------------------------------------------------

Se um colaborador fez `push` de uma alteração, você precisa "puxar" (pull) essa mudança para o seu repositório local:

```
git pull origin main

```

> `git pull` busca as alterações do remoto e as mescla (faz `merge`) automaticamente no seu local.

🤖 24. Como usar o GitFluence (Breve Menção)
--------------------------------------------

O [GitFluence](https://www.gitfluence.com/ "null") é uma ferramenta de IA que ajuda a encontrar o comando Git correto usando linguagem natural.

Em vez de decorar comandos complexos, você pode digitar o que quer fazer:

-   **Exemplo 1:** "desfazer o último commit"

    -   *GitFluence sugere:* `git reset HEAD~1`

-   **Exemplo 2:** "mudar o nome da branch atual"

    -   *GitFluence sugere:* `git branch -m novo-nome-da-branch`

É útil quando você está aprendendo ou esqueceu um comando específico.

📘 Créditos
-----------

Material criado para fins educacionais nas aulas práticas de Git Local e Git Remote,

ministradas por Anderson R. M. Gomes 🧑‍🏫
