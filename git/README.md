# Atividade Prática: Git no Terminal CMD - Windows

**Objetivo:** Criar um projeto na pasta *Documentos*, versionar arquivos, desfazer commits com segurança, enviar ao GitHub, baixar alterações remotas, clonar um repositório e navegar pelo histórico de commits.

**Pré-requisitos:**

- Windows 10 ou 11.
- Git instalado (caso não tenha, baixe em [git-scm.com](https://git-scm.com/)).
- Conta no GitHub (caso não tenha, crie a sua conta em [github.com](https://github.com))

<br />

## Passo 1: Configuração Inicial do Git

1. Abra o Terminal **Windows CMD**

2. Para verificar se o Git está instalado no sistema e qual é a versão, digite o comando:

```cmd
git version
```

3. Para listar todas as configurações do Git, digite o comando:

```cmd
git config --list
```

> 💡 Para sair da listagem do comando, caso seja necessário, pressione a letra **q** do seu teclado.

<br />

> [!WARNING]
>
> *Caso não apareça nenhuma configuração, significa que você ainda não configurou o seu Git.*

<br />

4. Para configurar o seu **nome** no Git, digite o comando:

```cmd
git config --global user.name "seu_nome"
```

> *Substitua seu_nome, pelo seu nome completo.*

5. Para verificar se o seu **nome** foi configurado corretamente no Git, digite o comando:

```cmd
git config user.name
```

6. Para configurar o seu **e-mail** no Git, digite o comando:

```cmd
git config --global user.email "seu_email@email.com"
```

> *Substitua seu_email, pelo e-mail que você utilizou para criar a sua conta no GitHub.*

7. Para verificar se o seu **e-mail** foi configurado corretamente no Git, digite o comando:

```cmd
git config user.email
```

8. Para configurar o **nome padrão da branch principal** do repositório Git, digite o comando:

```cmd
git config --global init.defaultBranch main
```

> Essa configuração é importante para garantir que, em todos os seus repositórios, a branch principal seja criada automaticamente com o nome **main**, substituindo o antigo padrão **master**.

9. Para verificar se o **nome padrão da branch principal** foi configurado como main, digite o comando:

```cmd
git config init.defaultBranch
```

10. Para utilizar a estratégia de mesclagem padrão ao invés do **rebase**, execute o comando:

```cmd
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

1. Execute os comandos a seguir no CMD para acessar a pasta **Documentos**, criar o diretório do exercício e navegar até a pasta:

```cmd
cd %USERPROFILE%\Documents
mkdir aula_git
cd aula_git
```

<br />

> [!TIP]
>
> Se sua pasta Documentos estiver no OneDrive, use os comandos abaixo:
>
> ```cmd
> cd %USERPROFILE%\OneDrive\Documents
> mkdir aula_git
> cd aula_git
> ```

<br />

2. Crie a pasta **docs**:

```cmd
mkdir docs
```

3. Crie os dois arquivos abaixo dentro da pasta **aula_git**:

```cmd
echo # Projeto Aula Git > README.md
echo print("Ola, Git!") > app.py
```

---

## Passo 3: Inicializando o Repositório e Primeiro Commit

1. **Inicialize o repositório Git:**

   ```cmd
   git init
   ```

2. **Verifique o status do repositório:**

   ```cmd
   git status
   ```

   > *Observe que os arquivos `README.md` e `app.py` aparecem em vermelho como "untracked".*
   >
   > ![](https://ik.imagekit.io/46hheoxm3/2026-10-13%2001_28_13-Untitled_%20-%20Typora.png)

3. **Adicione os arquivos para a Staging Area:**

   ```cmd
   git add .
   ```

4. **Verifique o status novamente:**

   ```cmd
   git status
   ```

   > *Os arquivos agora aparecem em verde, prontos para o commit.*
   >
   > ![](https://ik.imagekit.io/46hheoxm3/2026-10-13%2001_46_52-Untitled_%20-%20Typora.png)

5. **Faça o primeiro commit:**

   ```cmd
   git commit -m "Commit inicial: estrutura básica do projeto"
   ```

> *Será exibida a mensagem abaixo confirmando o commit:*
>
> ![](https://ik.imagekit.io/46hheoxm3/2026-10-13%2001_49_38-Untitled_%20-%20Typora.png)

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
> | **`style`**            | **Estilização/Formatação:** Mudanças de formatação que não alteram a lógica do código (espaços, indentação, ponto e vírgula). | `style: ajusta indentação do arquivo app.py`                 |
> | **`refactor`**         | **Refatoração:** Mudança de estrutura do código sem alterar seu comportamento nem corrigir bugs. | `refactor: simplifica lógica da função de cálculo`           |
> | **`test`**             | **Testes:** Adição, alteração ou criação de testes automatizados. | `test: adiciona testes unitários para rota de login`         |
> | **`chore`**            | **Tarefas Diversas:** Atualizações de dependências, tarefas de build, ajustes de `.gitignore` ou configurações gerais. | `chore: atualiza dependências do arquivo requirements.txt`   |
> | **`perf`**             | **Performance:** Alterações focadas estritamente em melhorar o desempenho do código. | `perf: otimiza consulta SQL da busca de usuários`            |
> | **`ci`**               | **Integração Contínua:** Modificações nos fluxos de automação/CI/CD (ex: GitHub Actions, GitLab CI). | `ci: adiciona pipeline de teste automatizado`                |
> | **`revert`**           | **Reversão:** Desfaz/reverte um commit que foi realizado anteriormente. | `revert: desfaz commit de funcionalidade de relatórios`      |

<br />

6. Digite o comando abaixo para visualizar o histórico de commits:

```cmd
git log
```

> *Será exibida a lista de commits do repositório:*
>
> ![](https://ik.imagekit.io/46hheoxm3/2026-10-13%2001_51_37-Untitled_%20-%20Typora.png)

---

## Passo 4: Modificando Arquivos e Visualizando Alterações

1. Adicione uma nova linha ao arquivo `app.py`:

   ```cmd
   echo print("Nova funcionalidade adicionada") >> app.py
   ```

2. **Compare as alterações feitas em relação ao último commit:**

   ```cmd
   git diff
   ```

   > Na imagem abaixo, vemos o antes e o depois das alterações:
   >
   > ![](https://ik.imagekit.io/46hheoxm3/2026-10-13%2001_54_50-Untitled_%20-%20Typora.png)

3. Adicione o arquivo alterado e faça um novo commit:

   ```cmd
   git add app.py
   git commit -m "feat: adiciona mensagem de nova funcionalidade no app.py"
   ```

> *Será exibida a mensagem abaixo confirmando o commit:*
>
> ![](https://ik.imagekit.io/46hheoxm3/2026-10-13%2001_57_48-Untitled_%20-%20Typora.png)

4. Digite o comando abaixo para visualizar o histórico de commits:

```cmd
git log
```

> *Será exibida a lista atualizada de commits do repositório:*
>
> ![](https://ik.imagekit.io/46hheoxm3/2026-10-13%2001_59_01-Untitled_%20-%20Typora.png)

---

## Passo 5: Desfazendo um Commit com `git revert`

Às vezes um commit já foi feito e depois percebemos que ele estava errado. O `git revert` desfaz o efeito desse commit **criando um novo commit** com a alteração inversa. 

O commit original continua no histórico, e por isso o `revert` é a forma segura de desfazer algo, inclusive depois de enviar o código ao GitHub.

### 5.1 Criando um commit com erro

1. Adicione uma linha indesejada ao `app.py` e faça o commit:

   ```cmd
   echo print("Linha com erro") >> app.py
   git add app.py
   git commit -m "feat: adiciona linha com erro no app.py"
   ```

2. Veja o histórico de forma compacta:

   ```cmd
   git log --oneline
   ```

   > *O commit "adiciona linha com erro" aparece no topo da lista. Para sair da listagem, pressione **q**.*

### 5.2 Revertendo o commit

1. Desfaça o último commit:

   ```cmd
   git revert HEAD --no-edit
   ```

   > *`HEAD` representa o commit mais recente. A opção `--no-edit` aceita a mensagem automática e evita que o Git abra um editor de texto.*

2. Confira o resultado:

   ```cmd
   type app.py
   git log --oneline
   ```

   > *A linha com erro desapareceu do arquivo. No histórico, o commit original continua lá e acima dele surgiu um novo commit com a mensagem `Revert "feat: adiciona linha com erro no app.py"`.*

### 5.3 Revertendo um commit mais antigo

Para desfazer um commit que não é o último, informe o identificador (hash) dele, que aparece no `git log --oneline`:

```cmd
git revert <hash> --no-edit
```

> *Substitua `<hash>` pelos primeiros caracteres do commit, por exemplo `a1b2c3d`.*

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

1. Vá ao **GitHub**, clique no botão **"+"** (canto superior direito) → **New repository**.

2. Dê o nome de `aula_git`. **Não** marque as opções de criar README, .gitignore ou Licença. Clique em **Create repository**.

3. Copie a URL do repositório gerado (exemplo: `https://github.com/seu-usuario/aula_git.git`).

4. Volte ao CMD e vincule o repositório local ao remoto:

   ```cmd
   git remote add origin https://github.com/seu-usuario/aula_git.git
   ```

   > *Substitua `seu-usuario` pelo seu usuário do GitHub.*

5. Para confirmar o vínculo, utilize o comando abaixo:

```cmd
git remote -v
```

6. **Envie os dados ao GitHub:**

```cmd
git push origin main
```

> *Na primeira vez, o Windows abrirá uma janela do navegador pedindo para autenticar sua conta do GitHub.*

7. Digite o comando abaixo para visualizar o histórico de commits atualizados:

```cmd
git log
```

> *O histórico enviado inclui os commits do Passo 5: o commit com erro e o commit de reversão.*

8. Volte no repositório do GitHub e atualize a página para visualizar os arquivos enviados.

<br />

> [!WARNING]
>
> Observe que a pasta `docs` não foi versionada porque ela está vazia. O Git versiona apenas pastas com conteúdo.

<br />

---

## Passo 7: Simulando Alterações Remotas e Baixando com `git pull`

1. Vá ao **GitHub** pelo navegador e abra o arquivo `README.md`.

2. Clique no ícone de **lápis (Edit)**, adicione a linha: `## Descricao do Projeto` e faça o commit direto pelo site no botão **Commit changes...**.

3. Volte ao seu **CMD** e baixe essas alterações remotas para a sua máquina:

   ```cmd
   git pull origin main
   ```

4. Veja que o arquivo `README.md` local foi atualizado com sucesso.

5. Digite o comando abaixo para visualizar o histórico de commits atualizados:

```cmd
git log
```

---

## Passo 8: Clonando o Repositório (Clone)

Para simular o trabalho em outro computador ou pasta:

1. Volte para a pasta `Documents`:

   ```cmd
   cd %USERPROFILE%\Documents
   ```

2. Clone o repositório `helloworld_python`, através do comando abaixo:

   ```cmd
   git clone https://github.com/rafaelproinfo/helloworld_python
   ```

3. Entre na pasta clonada e verifique os arquivos baixados:

   ```cmd
   cd helloworld_python
   dir
   ```

---

## Tabela de Resumo dos Comandos Utilizados

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