# Atividade Prática: Terminal Linux (WSL-2 / Ubuntu)

**Objetivo:** Dominar a criação, organização, pesquisa, renomeação, cópia e movimentação de arquivos e pastas, controle de permissões e gestão de usuários no Terminal bash do Linux.

<br />

## ✅Instruções Iniciais

1. Abra o menu Iniciar do Windows e busque por **Ubuntu** ou **WSL** (ou abra o Terminal do Windows e selecione a guia do Ubuntu).

![](https://i.imgur.com/zeZVCyn.png)

<br />

> [!IMPORTANT]
>
> **Diferença importante em relação ao Windows:**
>
> Ao contrário do Windows (que ignora a diferença entre letras maiúsculas e minúsculas nos nomes de caminhos e arquivos), o **Linux é *Case Sensitive***.
>
> Isso significa que o Linux trata letras maiúsculas e minúsculas como caracteres completamente distintos. 
>
> Por exemplo, `Arquivo.txt`, `arquivo.txt` e `ARQUIVO.TXT` são reconhecidos pelo sistema Linux como **três arquivos diferentes**, mesmo que estejam dentro da mesma pasta. O mesmo vale para o nome de pastas e para a execução de comandos no terminal Linux.

<br />

## ✅ Verificação do Sistema e Informações Iniciais



> [!TIP]
>
> **Como copiar, colar e editar comandos no Terminal (WSL2 / Ubuntu):**
>
> - **Para copiar o comando deste guia:** Selecione o comando e pressione `Ctrl + C` (ou clique no botão **Copiar** no canto superior da caixa de código).
> - **Para colar no Terminal:** Pressione `Ctrl + Shift + V` (ou `Shift + Insert`), ou clique com o **botão direito do mouse** no terminal. *(Nota: O atalho simples `Ctrl + V` envia um caractere de escape no Linux Bash e não cola).*
> - **Para navegar e editar um comando no Terminal:**
>   - Use as setas `⬅` e `➡` para mover o cursor caractere por caractere.
>   - Para mover o cursor rapidamente palavra por palavra no Ubuntu, use **`Alt + B`** (voltar palavra) e **`Alt + F`** (avançar palavra), ou segure **`Ctrl + ⬅`** / **`Ctrl + ➡`** dependendo da configuração do terminal.
>   - Pressione `Ctrl + A` (ou `Home`) para ir ao início da linha e `Ctrl + E` (ou `End`) para ir ao final da linha.
> - **Uso do mouse:** Você pode clicar e arrastar para selecionar trechos de texto para copiar. *(Dica: Segure `Shift` enquanto clica se estiver em aplicativos CLI interativos como `tmux` ou `vim`).*   

Verifique a data, hora, informações do sistema operacional e limpe o terminal.

1. Exiba a data e hora atual do sistema:

```bash
date
```

<br />

> [!TIP]
>
>  **Para exibir a ajuda de um comando específico e consultar suas opções:**
> 
>  - **Adicione `--help` ao final do comando (Opção mais rápida):**
> 
>    Exibe um resumo das opções e parâmetros diretamente na tela.
> 
>    ```bash
>    date --help
>    ```
>    
>  - **Utilize o comando `man` antes dele (Manual detalhado):**
> 
>    Abre o manual completo e paginado do comando (pressione a tecla `q` para sair).
> 
>    ```bash
>    man date
>    ```

<br />

2. Exiba informações detalhadas do kernel Linux e da distribuição:

```bash
uname -a
```

3. Exiba informações da distribuição Ubuntu:

```bash
lsb_release -a
```

4. Verifique o usuário atual do sistema

```bash
whoami
```

5. Exiba o nome do computador

```bash
hostname
```

6. Limpe a tela do terminal:

```bash
clear
```

<br />

## ✅ Executar Comandos como Administrador (`sudo`)



No Linux e no WSL2 (Ubuntu), por questões de segurança, o seu usuário comum não tem permissão para alterar arquivos de sistema, instalar programas ou modificar configurações globais.

O comando **`sudo`** (*Superuser Do*) serve para executar um comando com **privilégios de administrador** (usuário *root*), equivalente à opção "Executar como Administrador" do Windows.

Sempre você for executar um comando exclusivo do administrador (usuário **root**), adicione a palavra `sudo` antes do comando que exija permissões elevadas, como por exemplo o utilitário de atualização dos pacotes do sistema, o `apt`:

```bash
sudo apt update
```

Ao executar pela primeira vez, o sistema pedirá a sua senha de usuário para confirmar a ação.

> [!IMPORTANT]
>
> Ao digitar a senha no terminal Linux, **os caracteres não aparecem na tela** (nem mesmo como asteriscos `***`). Isso é um recurso de segurança padrão. Digite a senha normalmente e pressione `Enter`.

<br />

> [!TIP]
>
> Se durante a instalação do WSL2 ocorreu algum problema com o cadastro da senha ou você não se lembre da senha, siga as instruções abaixo para alterar a senha do seu usuário:
>
> 1.  Abra o **Windows PowerShell**
> 2. Execute o comando abaixo para entrar no WSL2 no modo Super Usuário (root)
>
> ```powershell
> wsl -u root
> ```
>
> 3. Para alterar a senha, utilize o comando abaixo:
>
> ```powershell
> passwd nome_do_usuario
> ```
>
> 4. Cadastre a nova senha 
> 5. Digite o comando abaixo para sair do WSL2 - Modo Super Usuário
>
> ```powershell
> exit
> ```
>
> 6. Volte para o Terminal do WSL2 e teste a nova senha

<br />

### Casos de Uso Mais Comuns

- **Instalar ou atualizar programas:**

  ```bash
  sudo apt install tree
  ```

- **Editar arquivos do sistema (fora da sua pasta de usuário):**

  ```bash
  sudo nano /etc/hosts
  ```

> Para fechar o Nano, utilize a combinação de teclas **`Ctrl + x`**

<br />

## ✅ Criação de Usuário e Gestão de Permissões Básicas



Crie um novo usuário no sistema para podermos testar a alteração das propriedades dos arquivos (`chown`).

1. Crie um novo usuário chamado `aluno` (será solicitada a senha do seu usuário atual `sudo`):

```bash
sudo adduser aluno
```

> Preencha a nova senha para o usuário aluno (12345678) duas vezes e aperte a tecla `Enter` do seu teclado para confirmar as informações padrão até finalizar. 
>
> O comando `adduser` cria automaticamente o usuário **e** o seu grupo primário correspondente.

2. Confirme que o usuário foi criado listando as informações dele:

```bash
id aluno
```

> **Resultado:**
>
> ```bash
> uid=1001(aluno) gid=1001(aluno) groups=1001(aluno),100(users)
> ```

<br />

> [!NOTE]
>
> ### O que são Grupos no Linux?
>
> No Linux, além de cada usuário ter sua própria conta, o sistema utiliza **grupos** para organizar e facilitar a gestão de permissões de acesso.
>
> Um **grupo** é um conjunto de usuários que compartilham as mesmas permissões para determinados arquivos, pastas e comandos. Em vez de definir permissões individualmente para cada usuário, o administrador atribui essas permissões ao grupo e adiciona os usuários a ele.
>
> - **Grupo Primário:** Todo usuário criado possui um grupo principal (com o mesmo nome do usuário por padrão). Quando o usuário cria um arquivo, esse arquivo pertence ao seu grupo primário.
> - **Grupos Secundários:** Um usuário pode pertencer a vários outros grupos ao mesmo tempo (por exemplo, ao grupo `sudo` para executar comandos como administrador, ou ao grupo `docker` para gerenciar contêineres).

<br />

3. Crie um novo grupo chamado estudantes:

```bash
sudo groupadd estudantes
```

4. Adicione o usuário `aluno` no grupo estudantes:

```bash
sudo usermod -aG estudantes aluno
```

> *(O parâmetro `-aG` significa **append Group**, ou seja, adiciona ao novo grupo sem remover o usuário dos grupos antigos).*

5. Confirme que o usuário foi adicionado ao novo grupo:

```bash
id aluno
```

> **Resultado:**
>
> ```bash
> uid=1001(aluno) gid=1001(aluno) groups=1001(aluno),100(users),1002(estudantes)
> ```

6. Para visualizar todos os membros do grupo estudantes, utilize o comando:

```bash
getent group estudantes
```

<br />

## ✅ Navegação e Criação do Diretório Principal



Navegue até o diretório pessoal do usuário atual e crie a estrutura do laboratório.

<br />

> [!TIP]
>
> ### Boas Práticas para Nomenclatura de Arquivos e Pastas no Linux
>
> Ao trabalhar no terminal Linux (incluindo o WSL2/Ubuntu), adote as seguintes regras para evitar erros na execução de comandos, simplificar a navegação e facilitar a criação de scripts de automação:
>
> - **Use apenas letras minúsculas:** Como o Linux é **case-sensitive** (diferencia maiúsculas de minúsculas), os arquivos `Relatorio.txt`, `relatorio.txt` e `RELATORIO.TXT` são tratados como **três arquivos totalmente diferentes na mesma pasta**. Manter tudo em minúsculas previne erros de digitação e confusão ao buscar arquivos.
>   - *Prefira:* `projetos_2026`
>   - *Evite:* `Projetos_2026` ou `PROJETOS_2026`
> - **Nunca use espaços em branco:** No Linux, o espaço é o caractere usado pelo terminal para separar um comando de seus argumentos e parâmetros. Nomes com espaço obrigam o uso de aspas ou do caractere de escape `\` (ex: `cd "minha pasta"` ou `cd minha\ pasta`), o que dificulta o uso de autocompletar e quebra scripts automatizados.
>   - *Prefira:* `minha-pasta` ou `minha_pasta`
>   - *Evite:* `minha pasta`
> - **Evite acentuação e caracteres especiais:** Não utilize cedilha (`ç`), acentos (`á`, `ã`, `é`, `ô`), símbolos (`$`, `@`, `!`, `#`, `%`, `*`) ou parênteses. Eles têm significados especiais para o shell (Bash) ou podem ser corrompidos por variações de codificação de texto (*encoding*) entre servidores e sistemas.

<br />

1. Para identificar  em qual pasta você está, utilize o comando:

```bash
pwd
```

2. Navegue até a pasta do seu usuário (*Home Directory*):

```bash
cd ~
```

3. Crie uma pasta chamada `aula_terminal`:

```bash
mkdir aula_terminal
```

4. Entre na pasta recém-criada:

```bash
cd aula_terminal
```

<br />

> ### Outras opções do comando cd
>
> - Ir para a raiz absoluta do sistema de arquivos (`/`):
>
> ```bash
> cd /
> ```
>
> - Voltar para a pasta pai (um nível acima na árvore de diretórios):
>
> ```bash
> cd ..
> ```
> - Voltar para o último diretório onde você estava (recurso "Voltar"):
>
> ```bash
> cd -
> ```
>
> - Ir para a pasta do usuário
>
> ```bash
> cd ~
> ```

<br />

## ✅ Criação da Estrutura de Pastas e Arquivos



Crie diversas subpastas e arquivos de texto de uma só vez para compor o ambiente de testes.

1. Crie três pastas simultaneamente (`projetos`, `documentos`, `backup`):

```bash
mkdir projetos documentos backup
```

2. Crie três arquivos com conteúdos diferentes:

```bash
echo "Arquivo de Teste 1" > arquivo1.txt
echo "Arquivo de Teste 2" > arquivo2.txt
echo "Conteudo do Relatorio" > relatorio.txt
```

<br />

> [!TIP]
>
> Para criar um arquivo `txt` vazio, utilize o comando:
> 
>  ```bash
>  touch teste.txt
>  ```
>

<br />

3. Visualize todo o conteúdo criado usando variações do `dir`:

- Listagem padrão simples:

```bash
ls
```

- Listagem em formato longo (exibe permissões, dono, tamanho e data):

```bash
ls -l
```

- Listagem longa exibindo arquivos ocultos e tamanhos legíveis (KB, MB):

```bash
ls -la -h
```

- Listar todos os arquivos da pasta atual (incluindo os arquivos ocultos):

```bash
ls -a
```

> [!TIP]
>
> No Linux, os arquivos ocultos sempre começam com o caractere ponto (.). 

4. Exibir a estrutura gráfica de diretórios em árvore:

```bash
tree
```

> *Se o comando `tree` não estiver instalado, execute `sudo apt install tree`*.

5. Para editar o arquivo `arquivo1.txt` no Nano (Editor de Textos), utilize o comando:

```bash
nano arquivo1.txt
```

6. Para visualizar o conteúdo do arquivo direto no terminal utilize o comando: 

```bash
cat arquivo1.txt
```

<br />

## ✅ Localizar Pastas e Arquivos



O comando **`find`** é uma das ferramentas mais poderosas do Linux para localizar arquivos e diretórios em tempo real. 

Diferente de uma busca simples, ele varre a estrutura de pastas a partir do caminho que você especificar e permite filtrar por nome, tipo, tamanho, data de modificação e permissões.

1. Buscar por nome exato ou padrão (usando curingas)
   - O parâmetro `-name` faz a busca respeitando maiúsculas e minúsculas (*case-sensitive*). 
   - O parâmetro `-iname` ignore maiúsculas e minúsculas (*case-insensitive*). 

- Buscar o arquivo chamado `arquivo1.txt` na pasta atual (ponto .):

  ```bash
  find . -name "arquivo1.txt"
  ```

- Buscar todos os arquivos `.log` dentro do diretório `/var` (sem diferenciar maiúsculas/minúsculas):

  ```bash
  find /var -iname "*.log"
  ```

2. Filtrar apenas por Arquivos ou apenas por Pastas

Use o parâmetro **`-type`** para restringir o resultado:

- `-type f`: Apenas arquivos (*files*)
- `-type d`: Apenas diretórios/pastas (*directories*)

```bash
find ~ -type d -name "projetos*"
```

3. Buscar por tamanho de arquivo

Use o parâmetro **`-size`** com os sufixos `k` (Kilobytes), `M` (Megabytes) ou `G` (Gigabytes):

- Buscar arquivos maiores que 100 Megabytes na pasta pessoal:

  ```bash
  find ~ -type f -size +100M
  ```

<br />

## ✅ Manipulação de Arquivos (Renomear, Copiar e Mover)



Aprenda a modificar e organizar os arquivos.

1. **Copiar Arquivo (`cp`):**

- Copie `arquivo1.txt` para a pasta `backup`:

```bash
cp arquivo1.txt backup/
```

- Liste o conteúdo da pasta `backup`:

```bash
ls backup/
```

2. **Mover Arquivo (`mv`):**

- Mova `relatorio.txt` para a pasta `documentos`:

```bash
mv relatorio.txt documentos/
```

- Liste o conteúdo da pasta `documentos`:

```bash
ls documentos/
```

3. **Renomear Arquivo (`mv`):**

- Renomeie `arquivo2.txt` para `relatorio_final.txt`:

```bash
mv arquivo2.txt relatorio_final.txt
```

4. Conferir resultado com árvore de arquivos:

```bash
tree -f
```

<br />

> [!NOTE]
>
> ### Como o comando `mv` sabe que ele deve renomear ou mover?
>
> 
>
> O comando `mv` no Linux/Unix determina se deve **renomear** ou **mover** analisando a **natureza do destino** (se o destino existe e se é um diretório) .
>
> A regra segue três cenários principais:
>
> 1. **Se o destino NÃO existe**
>
> O `mv` interpreta o destino como um novo nome. O arquivo ou diretório é **renomeado**.
>
> - **Exemplo:** `mv arquivo.txt novo_nome.txt`
> - Se `novo_nome.txt` não existir, `arquivo.txt` passa a se chamar `novo_nome.txt`.
>
> 
>
>  2. **Se o destino existe e É UM DIRETÓRIO**
>
> O `mv` entende que você quer transferir a fonte para dentro dessa pasta. O arquivo/diretório é **movido** mantendo o seu nome original.
>
> - **Exemplo:** `mv arquivo.txt /caminho/para/pasta/`
> - O `arquivo.txt` será colocado dentro de `pasta/`.
>
> 
>
>  3. **Se o destino existe e NÃO É UM DIRETÓRIO (é um arquivo)**
>
> O `mv` entende que você quer **substituir (sobrescrever)** o arquivo de destino pelo arquivo de origem.
>
> - **Exemplo:** `mv foto1.png foto2.png`
> - Se `foto2.png` já existir, o conteúdo de `foto1.png` substitui `foto2.png` (a menos que a opção `-i` esteja ativa para pedir confirmação).

<br />

## ✅ Manipulação de Pastas (Renomear, Copiar e Mover)



Aprenda a renomear, mover e copiar estruturas inteiras de diretórios.

1. **Renomear Pasta (`mv`):**

- Renomeie a pasta `projetos` para `projetos_antigos`:

```bash
mv projetos projetos_antigos
```

- Conferir resultado com árvore de arquivos:

```bash
tree -f
```

2. **Mover Pasta (`mv`):**

- Mova `projetos_antigos` para dentro de `backup`:

```bash
mv projetos_antigos backup/
```

- Conferir resultado com árvore de arquivos:

```bash
tree -f
```

3. **Copiar Pasta inteira com Conteúdo (`cp -r`):**

- Copie a pasta `documentos` recursivamente para `documentos_copia`:

```bash
cp -r documentos documentos_copia
```

> A opção `-r` significa recursivamente, ou seja, pastas e subpastas, incluindo os arquivos.

- Conferir resultado com árvore de arquivos:

```bash
tree -f
```

<br />

## ✅ Gerenciamento de Permissões (chmod) e Propriedade (chown)



Aprenda a alterar quem pode ler/escrever nos arquivos e quem é o dono.

1. Navegue até a pasta `/tmp`:

```bash
cd /tmp
```

2. Crie uma pasta chamada `acesso`:

```bash
mkdir permissoes
```

3. Entre na pasta recém-criada:

```bash
cd permissoes
```

4. Crie os arquivos `acesso_negado.txt` e `aluno.txt`:

```bash
echo "Acesso Negado" > acesso_negado.txt
echo "Arquivo do aluno" > aluno.txt
```

5. Verifique as permissões atuais dos arquivos:

```
ls -l
```

6. **Alterar Permissões (`chmod`):**

Remova a permissão de leitura do "grupo" e dos "outros usuários" nos arquivos `acesso_negado.txt` e `aluno.txt`, usando o formato octal (`600` = **Dono:** leitura/escrita, **Grupo:** nenhuma, **Outros:** nenhuma):

```bash
chmod 600 acesso_negado.txt
chmod 600 aluno.txt
```

> [!TIP]
>
> ### Formato Octal das Permissões no Linux
>
> No Linux, as permissões de arquivos e diretórios também podem ser representadas por números no formato octal, utilizando valores de 0 a 7.
>
> Cada permissão possui um valor:
>
> | Permissão           | Valor |
> | ------------------- | ----- |
> | Leitura (`r`)       | 4     |
> | Escrita (`w`)       | 2     |
> | Execução (`x`)      | 1     |
> | Sem permissão (`-`) | 0     |
>
> Os valores são somados para representar as permissões de cada categoria de usuário:
>
> - Proprietário (u): primeiro dígito.
> - Grupo (g): segundo dígito.
> - Outros (o): terceiro dígito.
>
> **Exemplo:** `chmod 754 arquivo.txt`
>
> | Categoria    | Valor     | Permissões                          |
> | ------------ | --------- | ----------------------------------- |
> | Proprietário | 7 (4+2+1) | Leitura, escrita e execução (`rwx`) |
> | Grupo        | 5 (4+1)   | Leitura e execução (`r-x`)          |
> | Outros       | 4         | Somente leitura (`r--`)             |
>
> Assim, o comando `chmod 754 arquivo.txt` define as permissões do arquivo utilizando a representação numérica.

7. **Alterar Propriedade (`chown`):**

Altere o dono do arquivo `aluno.txt` para o usuário `aluno` criado no inicio do guia:

```bash
sudo chown aluno aluno.txt
```

> *Digite a senha do seu usuário para autorizar a mudança.*

8. Verifique a mudança do proprietário e permissões:

```bash
ls -l
```

9.  Para testar, vamos alternar para o usuário `aluno` (Troca de Usuário no WSL2):

```bash
su - aluno
```

> *Digite a senha definida para o usuário `aluno` na criação. Note que o prompt mudará para `aluno@nome-da-maquina:~$`.*

10. Navegue até a pasta onde o arquivo foi criado e tente ler o conteúdo dos dois arquivos:

```bash
cat /tmp/permissoes/acesso_negado.txt
```

- **Resultado Esperado:**

```bash
cat: /tmp/permissoes/acesso_negado.txt: Permission denied
```

> O sistema exibe **Permission denied** (Permissão negada) porque o arquivo pertence ao outro usuário e tem permissão `600` (apenas o dono pode ler).

```bash
cat /tmp/permissoes/aluno.txt
```

> Observe que o arquivo `aluno.txt` estará acessível, porque aluno é o dono do arquivo.

7. Para encerrar a sessão do usuário `aluno` e voltar à sua conta principal, digite:

```bash
exit
```

<br />

## ✅ Exclusão de Arquivos, Pastas e Limpeza



Exclua os arquivos e diretórios criados para manter o sistema limpo.

1. Volte para a pasta `aula_terminal`

```bash
cd ~/aula_terminal
```

2. Apague todos os arquivos do diretório atual:

```bash
rm *.txt
```

3. Volte um nível na estrutura de diretórios:

```bash
cd ..
```

4. Remova a pasta `aula_terminal` inteira e todo o seu conteúdo recursivamente:

```bash
rm -rf aula_terminal
```

> [!TIP]
>
> Para apagar pastas vazias, você pode utilizar o comando `rmdir`

5. Limpe a tela

```bash
clear
```

<br />

## ✅ Tabela Comparativa: CMD vs. PowerShell vs. Linux Bash (WSL)

| **Operação / Conceito**      | **CMD (Windows)**           | **PowerShell (Windows)**            | **Linux Bash (WSL-2 / Ubuntu)** |
| ---------------------------- | --------------------------- | ----------------------------------- | ------------------------------- |
| Exibir data/hora             | `date /t` / `time /t`       | `Get-Date`                          | `date`                          |
| Informações do sistema       | `systeminfo`                | `Get-ComputerInfo`                  | `uname -a` / `lsb_release -a`   |
| Limpar tela                  | `cls`                       | `Clear-Host` (`cls`)                | `clear`                         |
| Criar pasta                  | `mkdir pasta`               | `New-Item -Type Dir`                | `mkdir pasta`                   |
| Entrar / Subir pasta         | `cd pasta` / `cd ..`        | `Set-Location`                      | `cd pasta` / `cd ..`            |
| Listar conteúdo              | `dir`                       | `Get-ChildItem`                     | `ls` (detalhado: `ls -l`)       |
| Escrever em arquivo          | `echo Texto > arq.txt`      | `Set-Content -Value "Texto"`        | `echo "Texto" > arq.txt`        |
| Ler conteúdo no terminal     | `type arq.txt`              | `Get-Content arq.txt`               | `cat arq.txt`                   |
| Editor de texto via terminal | `notepad arq.txt`           | `notepad arq.txt`                   | `nano arq.txt` ou `vim arq.txt` |
| Renomear arquivo/pasta       | `ren antigo novo`           | `Rename-Item antigo novo`           | `mv antigo novo`                |
| Copiar arquivo               | `copy arq1.txt arq2.txt`    | `Copy-Item arq1.txt arq2.txt`       | `cp arq1.txt arq2.txt`          |
| Copiar pasta inteira         | `xcopy pasta1 pasta2 /E /I` | `Copy-Item pasta1 pasta2 -Recurse`  | `cp -r pasta1 pasta2`           |
| Mover arquivo ou pasta       | `move item destino\`        | `Move-Item item destino\`           | `mv item destino/`              |
| Deletar arquivo              | `del arq.txt`               | `Remove-Item arq.txt`               | `rm arq.txt`                    |
| Remover pasta e conteúdo     | `rmdir /s /q pasta`         | `Remove-Item pasta -Recurse -Force` | `rm -rf pasta`                  |
| Estrutura em árvore          | `tree /f`                   | `Get-ChildItem -Recurse`            | `tree`                          |
| **Alterar Permissões**       | `icacls` / `attrib`         | `Set-Acl`                           | `chmod 644 arquivo`             |
| **Alterar Proprietário**     | `takeown`                   | `Set-Acl`                           | `chown usuario arquivo`         |
| **Criar Usuário**            | `net user nome /add`        | `New-LocalUser`                     | `sudo adduser nome`             |