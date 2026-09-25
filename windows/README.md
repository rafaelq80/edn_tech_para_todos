# Windows - Terminal CMD



**Objetivo:** Dominar a criação, organização, pesquisa, renomeação, cópia e movimentação de arquivos e pastas no Windows CMD.

<br />

## ✅ Verificação do Sistema e Informações Iniciais



> [!TIP]
>
> **Como copiar, colar e editar comandos no Terminal:**
>
> - **Para copiar o comando deste guia:** Selecione o comando e pressione `Ctrl + C` (ou clique no botão **Copiar** no canto superior da caixa de código).
> - **Para colar no Terminal:** Pressione `Ctrl + V` (ou `Shift + Insert` / `Ctrl + Shift + V`), ou simplesmente clique com o **botão direito do mouse** dentro da janela do Terminal.
> - **Para navegar e editar um comando no Terminal:** Use as setas `⬅` e `➡` para mover o cursor caractere por caractere. Para mover rapidamente entre palavras inteiras, segure `Ctrl` enquanto pressiona as setas (`Ctrl + ⬅` ou `Ctrl + ➡`). Use `Home` para ir ao início da linha e `End` para ir ao final.
> - **Uso do mouse:** Você pode usar o mouse para selecionar trechos de texto clicando e arrastando.

Verifique a data, a hora atual e as especificações da máquina antes de iniciar.

1. Exiba a data atual do sistema:

```cmd
date /t
```

> A opção `/t` faz com que o comando `date` apenas exiba a data atual, sem solicitar a digitação de uma nova data.

<br />

> [!TIP]
>
> **Para exibir a ajuda para um comando específico e consultar as suas opções:** 
>
> - Adicione `/?` ao final do comando:
>
> ```cmd
> date /?
> ```
>
> - Ou ou digite a palavra `help` antes dele:
>
> ```cmd
> help date
> ```
>

<br />

2. Exiba a hora atual do sistema:

```cmd
time /t
```

> A opção `/t` faz com que o comando `time` apenas exiba a hora atual, sem solicitar a digitação de uma nova hora.

3. Obtenha informações detalhadas sobre o sistema operacional e hardware:

```cmd
systeminfo
```

4. Obtenha a versão do Windows:

```cmd
ver
```

5. Verifique o usuário atual do sistema

```cmd
echo %username%
```

6. Limpe a tela do terminal para organizar o espaço de trabalho:

```cmd
cls
```

<br />

> [!TIP]
>
> **Histórico de Comandos:**
>
> - **Para navegar pelo histórico:** Use as setas para cima `⬆` e para baixo `⬇` para alternar entre os comandos digitados anteriormente.
> - **Busca rápida:** Pressione `F7` para abrir uma lista com o histórico recente ou use `Ctrl + R` para pesquisar um comando específico digitando parte dele.
> - **Persistência:** Geralmente, o histórico de comandos não fica salvo depois que você fecha o Terminal ou reinicia o computador.

<br />

## ✅ Navegação e Criação do Diretório Principal



Acesse a pasta de documentos do seu usuário e crie a estrutura inicial do exercício.



> [!TIP]
>
> **Boas Práticas para Nomenclatura de Arquivos e Pastas:**
>
> Ao trabalhar no terminal (seja Windows, Linux ou macOS), adote as seguintes regras para evitar erros em scripts e facilitar a automação:
>
> 1. **Evite letras maiúsculas:** Mantenha os nomes em letras minúsculas (ex: `projetos_antigos` em vez de `Projetos_Antigos`). O Linux é *case-sensitive* (diferencia maiúsculas de minúsculas), o que pode gerar confusão ao migrar entre sistemas.
> 2. **Não use espaços em branco:** Substitua espaços por hífen (`-`) ou sublinhado (`_`). Nomes com espaço exigem o uso de aspas duplas no terminal (ex: `cd "minha pasta"`).
> 3. **Não use acentuação nem caracteres especiais:** Evite caracteres como `ç`, `á`, `ã`, `é`, `ô`. Eles podem ser corrompidos por diferenças de codificação (*encoding*) no terminal ou servidores.
>
> **Exemplo correto:** `relatorio_final_2026.txt` ou `dados-projeto`
>
> **Exemplo a evitar:** `Relatório Final 2026.txt` ou `Dados Projeto`

<br />

1. Navegue até a pasta **Documentos** do seu usuário:

```cmd
cd %USERPROFILE%\Documents
```

2. Crie uma pasta chamada `aula_cmd`:

```cmd
md aula_cmd
```

3. Entre na pasta recém-criada:

```cmd
cd aula_cmd
```

<br />

> ### Outras opções do comando cd
>
> - Ir para o diretório raiz (C:)
>
> ```cmd
> cd /
> ```
>
> - Ir para a pasta do usuário
>
> ```cmd
> cd %USERPROFILE%
> ```
>
> - Voltar uma pasta anterior
>
> ```cmd
> cd ..
> ```

<br />

## ✅ Criação da Estrutura de Pastas e Arquivos



Crie diversas subpastas e arquivos de texto de uma só vez para compor o ambiente de testes.

1. Crie três pastas simultaneamente (`projetos`, `documentos`, `backup`):

```cmd
md projetos documentos backup
```

2. Crie três arquivos de texto com conteúdos diferentes:

```cmd
echo Arquivo de Teste 1 > arquivo1.txt
echo Arquivo de Teste 2 > arquivo2.txt
echo Conteudo do Relatorio > relatorio.txt
```

> [!TIP]
>
> Para criar um arquivo `txt` vazio, utilize o comando:
>
> ```cmd
> type nul > texte.txt
> ```

3. Visualize todo o conteúdo criado usando variações do `dir`:

- Listar todos os arquivos da pasta:

```cmd
dir
```

- Listar apenas os nomes em formato simples:

```cmd
dir /b
```

- Listar apenas pastas/diretórios:

```cmd
dir /ad
```

- Listar apenas arquivos:

```cmd
dir /a:-d
```

- Listar apenas os arquivos `.txt` na pasta atual:

```cmd
dir *.txt
```

- Listar todos os arquivos `.txt` em todas as subpastas da pasta atual:

```cmd
dir *.txt /s
```

>**Outras opções do comando `dir`:**
>
>- Listar todos os arquivos `.txt` do computador:
>
>```cmd
>dir c:\ *.txt /s
>```
>
>> [!TIP]
>>
>> **Interromper a busca:** Pressione a combinação de teclas `Ctrl + C` para cancelar a listagem a qualquer momento.
>
>- Listar todos os arquivos `.txt` do computador com paginação (pausa a cada tela):
>
>```cmd
>dir c:\ *.txt /s /p
>```
>
>- Listar todos os arquivos da pasta atual (incluindo os arquivos ocultos):
>
>```cmd
>dir /a
>```

4. Para editar o arquivo `arquivo1.txt` no Notepad (Bloco de Notas), utilize o comando:

```cmd
notepad arquivo1.txt
```

<br />

## ✅ Manipulação de Arquivos (Renomear, Copiar e Mover)



Aprenda a modificar e organizar os arquivos.

1. **Renomear Arquivo (`ren` ou `rename`):**
- Renomeie `relatorio.txt` para `relatorio_final.txt`:

```cmd
ren relatorio.txt relatorio_final.txt
```

2. **Copiar Arquivo (`copy`):**

- Crie uma cópia de segurança de `arquivo1.txt` na pasta `backup`:

```cmd
copy arquivo1.txt backup\
```

- Liste o conteúdo da pasta `backup`:

```cmd
dir backup
```

- Faça uma cópia do arquivo `arquivo2.txt` no mesmo diretório trocando o nome para `arquivo2_copia.txt`:

```cmd
copy arquivo2.txt arquivo2_copia.txt
```

3. **Mover Arquivo (`move`):**

Mova o arquivo `relatorio_final.txt` para a pasta `documentos`:

```cmd
move relatorio_final.txt documentos\
```

4. **Conferir resultado com árvore de arquivos:**

```cmd
tree /f
```

<br />

## ✅ Manipulação de Pastas (Renomear, Copiar e Mover)



Aprenda a renomear, mover e copiar estruturas inteiras de diretórios.

1. **Renomear Pasta (`ren` ou `rename`):**
- Renomeie a pasta `projetos` para `projetos_antigos`:

```cmd
ren projetos projetos_antigos
```

2. **Mover Pasta (`move`):**

- Mova a pasta `projetos_antigos` para dentro da pasta `backup`:

```cmd
move projetos_antigos backup\
```

3. **Copiar Pasta com Conteúdo (`xcopy` / `robocopy`):**

> [!WARNING]
>
> O comando `copy` copia apenas arquivos. Para copiar pastas e subpastas inteiras no CMD, utiliza-se `xcopy` .

- Copie a pasta `documentos` e todo o seu conteúdo para uma nova pasta chamada `documentos_copia`:

```cmd
xcopy documentos documentos_copia /E /I
```

> - **`/E`:** Copia todas as subpastas mesmo se estiverem vazias
> - **`/I`:** Assume que o destino final é uma pasta

4. Exiba a estrutura geral atualizada:

```cmd
tree /f
```

<br />

## ✅ Exclusão de Arquivos, Pastas e Limpeza



Exclua os arquivos e diretórios criados para manter o sistema limpo.

1. Apague todos os arquivos do diretório atual:

```cmd
del *.txt
```

>  Confirme digitando `S` se for solicitado.

2. Saia da pasta atual:

```cmd
cd ..
```

3. remova toda a estrutura do exercício:

```cmd
rmdir /s /q aula_cmd
```

> - **`/s`**: Apaga a árvore de diretórios inteira (a pasta, todas as subpastas e todos os arquivos dentro delas).
> - **`/q`**: Modo silencioso (*quiet*), ou seja, ele executa a exclusão sem perguntar "Tem certeza que deseja excluir?" na tela.

4. Limpe a tela do terminal:

```cmd
cls
```

<br />

## ✅ Tabela Comparativa - CMD vs PowerShell

| **Operação**             | **Comando CMD**               | **Comando PowerShell (Nativo)**                      | **Alias no PowerShell**         |
| ------------------------ | ----------------------------- | ---------------------------------------------------- | ------------------------------- |
| Exibir data atual        | `date /t`                     | `Get-Date -Format "dd/MM/yyyy"`                      | `Get-Date`                      |
| Exibir hora atual        | `time /t`                     | `Get-Date -Format "HH:mm"`                           | `Get-Date`                      |
| Informações do sistema   | `systeminfo`                  | `Get-ComputerInfo`                                   | `systeminfo`                    |
| Limpar tela              | `cls`                         | `Clear-Host`                                         | `cls` / `clear`                 |
| Criar pasta              | `md pasta`                    | `New-Item -ItemType Directory -Name "pasta"`         | `md`                            |
| Entrar / Subir pasta     | `cd pasta` / `cd ..`          | `Set-Location -Path "pasta"` / `Set-Location ..`     | `cd` / `cd ..`                  |
| Listar conteúdo          | `dir`                         | `Get-ChildItem`                                      | `dir` / `ls`                    |
| Escrever em arquivo      | `echo Texto > arquivo.txt`    | `Set-Content -Path "arquivo.txt" -Value "Texto"`     | `echo "Texto" > arquivo.txt`    |
| Criar arquivo vazio      | `type nul > arquivo.txt`      | `New-Item -ItemType File -Name "arquivo.txt"`        | `ni arquivo.txt -ItemType File` |
| Exibir ajuda do comando  | `help comando` / `comando /?` | `Get-Help comando`                                   | `help` / `man`                  |
| Abrir no Bloco de Notas  | `notepad arquivo.txt`         | `Start-Process notepad "arquivo.txt"`                | `notepad`                       |
| Renomear Arquivo/Pasta   | `ren antigo.txt novo.txt`     | `Rename-Item -Path "antigo.txt" -NewName "novo.txt"` | `ren` / `rnm`                   |
| Copiar Arquivo           | `copy arq.txt destino\`       | `Copy-Item -Path "arq.txt" -Destination "destino\"`  | `copy` / `cp`                   |
| Copiar Pasta inteira     | `xcopy pasta1 pasta2 /E /I`   | `Copy-Item -Path "pasta1" -Destination "pasta2"`     | `copy -Recurse` / `cp -r`       |
| Mover Arquivo ou Pasta   | `move item destino\`          | `Move-Item -Path "item" -Destination "destino\"`     | `move` / `mv`                   |
| Deletar arquivo          | `del arquivo.txt`             | `Remove-Item -Path "arquivo.txt"`                    | `del` / `rm`                    |
| Remover pasta e conteúdo | `rmdir /s /q pasta`           | `Remove-Item -Path "pasta" -Recurse -Force`          | `rmdir -Recurse` / `rm -r`      |
| Estrutura em árvore      | `tree /f`                     | `Get-ChildItem -Recurse`                             | `tree`                          |

