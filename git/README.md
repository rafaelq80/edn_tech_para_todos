# Atividade Prática: Git no Terminal Git Bash



**Objetivo:** Criar um projeto na pasta *Documentos*, versionar arquivos, desfazer commits com segurança, enviar ao GitHub, baixar alterações remotas, clonar um repositório e navegar pelo histórico de commits.

**Pré-requisitos:**

- Windows 10 ou 11.
- Git instalado (caso não tenha, baixe em [git-scm.com](https://git-scm.com/)).
- Conta no GitHub (caso não tenha, crie a sua conta em [github.com](https://github.com))

<br />

## Git Bash



O Git for Windows fornece uma emulação do **Terminal BASH - Terminal padrão do Linux**, chamado de **Git Bash**, para executar os comandos Git a partir da linha de comando do Linux. O Git Bash se comporta exatamente como o Terminal BASH do ambientes LINUX. Na imagem abaixo, temos a tela do Git Bash:

<div align="center"><img src="https://i.imgur.com/6zzIwgN.png" title="source: imgur.com" width="90%"/></div>

Observe que o prompt do Git Bash é diferente do Git Bash.

---

## Passo 1: Configuração Inicial do Git



1. Abra o Terminal **Git Bash**

2. Para verificar se o Git está instalado no sistema e qual é a versão, digite o comando:

```bash
git version
```

3. Para listar todas as configurações do Git, digite o comando:

```bash
git config --list
```

> 💡 Para sair da listagem do comando, caso seja necessário, pressione a letra **q** do seu teclado.

<br />

> [!WARNING]
>
> *Caso não apareça nenhuma configuração, significa que você ainda não configurou o seu Git.*

<br />

4. Para configurar o seu **nome** no Git, digite o comando:

```bash
git config --global user.name "seu_nome"
```

> *Substitua seu_nome, pelo seu nome completo.*

5. Para verificar se o seu **nome** foi configurado corretamente no Git, digite o comando:

```bash
git config user.name
```

6. Para configurar o seu **e-mail** no Git, digite o comando:

```bash
git config --global user.email "seu_email@email.com"
```

> *Substitua seu_email, pelo e-mail que você utilizou para criar a sua conta no GitHub.*

7. Para verificar se o seu **e-mail** foi configurado corretamente no Git, digite o comando:

```bash
git config user.email
```

8. Para configurar o **nome padrão da branch principal** do repositório Git, digite o comando:

```bash
git config --global init.defaultBranch main
```

> Essa configuração é importante para garantir que, em todos os seus repositórios, a branch principal seja criada automaticamente com o nome **main**, substituindo o antigo padrão **master**.

9. Para verificar se o **nome padrão da branch principal** foi configurado como main, digite o comando:

```bash
git config init.defaultBranch
```

10. Para utilizar a estratégia de mesclagem padrão ao invés do **rebase**, execute o comando:

```bash
git config --global pull.rebase false
```

<br />

> [!WARNING]
>
> Quando o repositório local e o remoto divergem, o `git pull` precisa de uma estratégia. O **merge** preserva o histórico como ele aconteceu e é mais simples para quem está começando. O rebase reescreve commits locais e fica para um estudo futuro.
>
> O comando acima desativa o rebase como comportamento padrão para todos os seus repositórios.

---

## Passo 2: Criando a Estrutura de Pastas e Arquivos



1. Execute a sequência de comandos a seguir no Git Bash para acessar a pasta do seu usuário, criar a pasta do exercício (**aula_git**) e navegar até a pasta:

```bash
cd ~
mkdir aula_git
cd aula_git
```

2. Crie a pasta **docs**:

```bash
mkdir docs
```

3. Crie os dois arquivos abaixo dentro da pasta **aula_git**:

```bash
echo '# Projeto Aula Git' > README.md
echo 'print("Ola, Git!")' > main.py
```

4. Digite o comando abaixo para visualizar a estrutura de arquivos e pastas:

```bash
ls
```

5. O comando `ls` exibirá o seguinte conteúdo:

```bash
docs  main.py  README.md
```

---

## Passo 3: Inicializando o Repositório e Primeiro Commit



1. **Inicialize o repositório Git:**

   ```bash
   git init
   ```

> Observe que aparece a mensagem **(main)** no prompt do Git Bash, indicando que a pasta `aula_git` se tronou um repositório git.
>
> ![](https://i.imgur.com/jXoJeZh.png)

2. **Verifique o status do repositório:**

   ```bash
   git status
   ```

   > *Observe que os arquivos `README.md` e `main.py` aparecem em vermelho como "untracked".*
   >
   > ![](https://i.imgur.com/VDWhweY.png)

3. **Adicione os arquivos para a Staging Area:**

   ```bash
   git add .
   ```

4. **Verifique o status novamente:**

   ```bash
   git status
   ```

   > *Os arquivos agora aparecem em verde, prontos para o commit.*
   >
   > ![](https://i.imgur.com/VlKySB4.png)

5. **Faça o primeiro commit:**

   ```bash
   git commit -m "Commit inicial: estrutura básica do projeto"
   ```

> *Será exibida a mensagem abaixo confirmando o commit:*
>
> ![](https://i.imgur.com/AiKxCsl.png)

<br />

> [!NOTE]
>
> ### Tipos de Commits
>
> | **Tipo**               | **Descrição**                                                | **Exemplo de Mensagem**                                      |
> | ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
> | **`init` / `initial`** | **Commit Inicial:** Cria a estrutura base do projeto, o repositório do zero e os arquivos fundamentais inicializadores. | `init: commit inicial do projeto` *ou* `feat: initial commit` |
> | **`feat`**             | **Funcionalidade:** Adiciona um novo recurso ou funcionalidade ao sistema. | `feat: adiciona autenticação por token JWT`                  |
> | **`fix`**              | **Correção:** Corrige um erro, falha ou bug no código.       | `fix: corrige validação de e-mail no formulário`             |
> | **`docs`**             | **Documentação:** Alterações exclusivamente na documentação (ex: README.md, wiki). | `docs: atualiza instruções de instalação no README`          |
> | **`style`**            | **Estilização/Formatação:** Mudanças de formatação que não alteram a lógica do código (espaços, indentação, ponto e vírgula). | `style: ajusta indentação do arquivo main.py`                |
> | **`refactor`**         | **Refatoração:** Mudança de estrutura do código sem alterar seu comportamento nem corrigir bugs. | `refactor: simplifica lógica da função de cálculo`           |
> | **`test`**             | **Testes:** Adição, alteração ou criação de testes automatizados. | `test: adiciona testes unitários para rota de login`         |
> | **`chore`**            | **Tarefas Diversas:** Atualizações de dependências, tarefas de build, ajustes de `.gitignore` ou configurações gerais. | `chore: atualiza dependências do arquivo requirements.txt`   |
> | **`perf`**             | **Performance:** Alterações focadas estritamente em melhorar o desempenho do código. | `perf: otimiza consulta SQL da busca de usuários`            |
> | **`ci`**               | **Integração Contínua:** Modificações nos fluxos de automação/CI/CD (ex: GitHub Actions, GitLab CI). | `ci: adiciona pipeline de teste automatizado`                |
> | **`revert`**           | **Reversão:** Desfaz/reverte um commit que foi realizado anteriormente. | `revert: desfaz commit de funcionalidade de relatórios`      |

<br />

6. Digite o comando abaixo para visualizar o histórico de commits:

```bash
git log
```

> *Será exibida a lista de commits do repositório:*
>
> ![](https://i.imgur.com/SDwB9sk.png)

---

## Passo 4: Modificando Arquivos e Visualizando Alterações

1. Adicione uma nova linha ao arquivo `main.py`:

   ```bash
   echo 'print("Nova funcionalidade adicionada")' >> main.py
   ```

2. **Compare as alterações feitas em relação ao último commit:**

   ```bash
   git diff
   ```

   > Na imagem abaixo, vemos o antes e o depois das alterações:
   >
   > ![](https://i.imgur.com/tiHiM6b.png)

3. Adicione o arquivo modificado na ***Stage Area*** e faça um novo commit:

   ```bash
   git add main.py
   git commit -m "feat: adiciona mensagem de nova funcionalidade no main.py"
   ```

> *Será exibida a mensagem abaixo confirmando o commit:*
>
> ![](https://i.imgur.com/aDQDqzi.png)

4. Digite o comando abaixo para visualizar o histórico de commits:

```bash
git log
```

> *Será exibida a lista atualizada de commits do repositório:*
>
> ![](https://i.imgur.com/ZCYoS3F.png)

---

## Passo 5: Desfazendo um Commit com `git revert`

Às vezes um commit já foi feito e depois percebemos que ele estava errado. O `git revert` desfaz o efeito desse commit **criando um novo commit** com a alteração inversa. 

O commit original continua no histórico, e por isso o `revert` é a forma segura de desfazer algo, inclusive depois de enviar o código ao GitHub.

### 5.1 Criando um commit com erro

1. Adicione uma linha indesejada ao `main.py` e faça o commit:

   ```bash
   echo 'print("Linha com erro")' >> main.py
   git add main.py
   git commit -m "feat: adiciona linha com erro no main.py"
   ```

2. Veja o histórico de forma compacta:

   ```bash
   git log --oneline
   ```

   > *O commit "adiciona linha com erro" aparece no topo da lista. Para sair da listagem, caso seja necessário, pressione **q**.*
   >
   > ![](https://i.imgur.com/3iMfo0h.png)

### 5.2 Revertendo o commit

1. Desfaça o último commit:

   ```bash
   git revert HEAD --no-edit
   ```

   > *`HEAD` representa o commit mais recente. A opção `--no-edit` aceita a mensagem automática e evita que o Git abra um editor de texto.*
   >
   > Observe na imagem abaixo que um novo commit foi criado, indicando que o commit anterior foi desfeito.
   >
   > ![](https://i.imgur.com/PG5HWI2.png)

2. Confira o resultado:

   ```bash
   type main.py
   git log --oneline
   ```

   > *A linha com erro desapareceu do arquivo. No histórico, o commit original continua lá e acima dele surgiu um novo commit com a mensagem `Revert "feat: adiciona linha com erro no main.py"`.*
   >
   > ![](https://i.imgur.com/cMm8x8H.png)

### 5.3 Revertendo um commit mais antigo

Para desfazer um commit que não é o último, informe o identificador (hash) dele, que aparece no `git log --oneline`:

```bash
git revert <hash> --no-edit
```

> *Substitua `<hash>` pelos primeiros caracteres do commit, por exemplo `9fdb9a9`, destacado na imagem abaixo.*
>
> ![](https://i.imgur.com/i4SmDTJ.png)

<br />

> [!NOTE]
>
> - O `revert` **não apaga** o histórico. Ele acrescenta um novo commit, o que o torna seguro em repositórios compartilhados.
> - Se alterações posteriores mexerem nas mesmas linhas do commit revertido, o Git pode pedir que o conflito seja resolvido manualmente. Isso fica para uma próxima etapa.
> - Esse é o tipo `revert` da tabela "Tipos de Commits".

### Resumo

| Situação                          | Comando                      | O que acontece                                   |
| :-------------------------------- | :--------------------------- | :----------------------------------------------- |
| Desfazer o **último** commit      | `git revert HEAD --no-edit`  | Cria um novo commit que anula o anterior.        |
| Desfazer um commit **específico** | `git revert <hash> --no-edit`| Cria um novo commit que anula o commit indicado. |

---

## Passo 6: Conectando com o GitHub e Enviando o Código

1. Acesse a sua conta no **GitHub**, clique no botão **"+"** (canto superior direito) → **New repository**.

![](https://i.imgur.com/WJT0B3Y.png)

2. Dê o nome de `aula_git`. **Não** marque as opções de criar README, .gitignore ou Licença. Clique em **Create repository**.

![](https://i.imgur.com/VaFxHmC.png)

3. Copie a URL do repositório gerado (exemplo: `https://github.com/seu-usuario/aula_git.git`).

![](https://i.imgur.com/1hxmhAo.png)

4. Volte ao Git Bash e vincule o repositório local ao remoto:

```bash
git remote add origin https://github.com/seu-usuario/aula_git.git
```

> *Substitua `seu-usuario` pelo seu usuário do GitHub.*

5. Para confirmar o vínculo, utilize o comando abaixo:

```bash
git remote -v
```

> Será exibida a mensagem abaixo, confirmando a conexão com o repositório remoto:
>
> ![](https://i.imgur.com/thksDnr.png)

6. **Envie os dados ao GitHub:**

```bash
git push origin main
```

> *Na primeira vez, o Windows abrirá a janela abaixo pedindo para autenticar sua conta do GitHub.*
>
> ![](https://i.imgur.com/B2gBUFM.png)
>
> 1. Clique no botão **Sign in with your browser** 
> 2. Você será redirecionado para o navegador 
> 3. Informe suas credenciais (usuário e senha) 
> 4. Autorize a conexão da sua máquina com o GitHub
> 5. Após concluir o processo de autenticação e autorizar o acesso ao repositório, volte para o terminal e refaça push.

7. Será exibida a mensagem abaixo, confirmando o commit

![](https://i.imgur.com/rIM98F6.png)

8. Digite o comando abaixo para visualizar o histórico de commits atualizados:

```bash
git log --oneline
```

> *O histórico enviado inclui todos os commits, inclusive o commit de reversão.*
>
> ![](https://i.imgur.com/ro3LUBN.png)

9. Volte no repositório do GitHub e atualize a página para visualizar os arquivos enviados.

![](https://i.imgur.com/1v24Fnx.png)

<br />

> [!WARNING]
>
> Observe que a pasta `docs` não foi versionada porque ela está vazia. O Git versiona apenas pastas com conteúdo.

<br />

---

## Passo 7: Simulando Alterações Remotas e Baixando com `git pull`

1. No **GitHub**, abra o arquivo `README.md` em modo de edição, clicando no **lápis (Edit)**:

![](https://i.imgur.com/B0740Xa.png)

2. Adicione a linha: `## Descricao do Projeto` no final do arquivo e faça o commit direto pelo site no botão **Commit changes...**.

![](https://i.imgur.com/RUbTU7t.png)

3. O **GitHub** irá sugerir uma mensagem para o seu commit. Clique em **Commit changes** para concluir

<div align="center"><img src="https://i.imgur.com/t7UMuZV.png" title="source: imgur.com" /></div>

4. Volte ao seu **Git Bash** e atualize o seu repositório local com as alterações realizadas no GitHub:

```bash
git pull origin main
```

5. Será exibida a mensagem abaixo:

![](https://i.imgur.com/Zrd5SiJ.png)

6. Visualize o conteúdo do arquivo `README.md` da sua máquina e observe que ele foi atualizado com sucesso.

```bash
cat README.md
```

> **Resultado Esperado**
>
> ```markdown
> # Projeto Aula Git
> ## Descricao do Projeto
> ```

7. Digite o comando abaixo para visualizar o histórico de commits atualizados:

```bash
git log --oneline
```

> Observe que o commit feito no GitHub agora faz parte do histórico do seu repositório local
>
> ![](https://i.imgur.com/O5BPpxN.png)

---

## Passo 8: Clonando o Repositório (Clone)

Para simular o trabalho em outro computador ou pasta:

1. Volte para a pasta do seu usuário:

   ```bash
   cd ~
   ```

2. Clone o repositório `clone_github`, através do comando abaixo:

   ```bash
   git clone https://github.com/rafaelq80/clone_github.git
   ```

   > Será exibida a mensagem de confirmação abaixo:
   >
   > ![](https://i.imgur.com/CFmfEHM.png)

3. Entre na pasta clonada e verifique os arquivos clonados:

   ```bash
   cd clone_github
   ls
   ```

   > Será exibido o arquivo `index.html`
   >
   > ```bash
   > index.html
   > ```

4. Para abrir a página no navegador, execute o comando abaixo no terminal:

```bash
explorer index.html
```

> No MAC, utilize o comando:
>
> ```bash
> open index.html
> ```
>
> No Linux, utilize o comando:
>
> ```bash
> xdg-open index.html
> ```

5. A página será aberta no seu navegado padrão:

![](https://i.imgur.com/XpiZu38.png)

---

## Comandos Utilizados

| Comando                       | Descrição                                                    |
| :---------------------------- | :----------------------------------------------------------- |
| `git version`                 | Exibe a versão do Git instalada.                             |
| `git config`                  | Consulta e define as configurações do Git (nome, e-mail, branch padrão e estratégia de pull). |
| `git init`                    | Inicializa o repositório Git local.                          |
| `git status`                  | Exibe o estado atual dos arquivos (modificados, staged, untracked). |
| `git add <arquivo>`           | Adiciona alterações à área de preparação (Staging Area).     |
| `git commit -m "msg"`         | Salva as alterações na linha do tempo local com uma mensagem. |
| `git diff`                    | Mostra as alterações feitas desde o último commit.           |
| `git log`                     | Exibe o histórico de commits.                                |
| `git log --oneline`           | Exibe o histórico de commits de forma compacta.              |
| `git revert <hash>`           | Desfaz um commit criando um novo commit com a alteração inversa. |
| `git remote add origin <url>` | Conecta o repositório local ao repositório remoto no GitHub. |
| `git remote -v`               | Lista os repositórios remotos vinculados.                    |
| `git push origin main`        | Envia os commits locais para o servidor remoto no GitHub.    |
| `git pull origin main`        | Baixa e aplica as alterações do repositório remoto na máquina local. |
| `git clone <url>`             | Cria uma cópia completa de um repositório remoto no computador. |