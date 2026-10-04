# Guia de Instalação do WSL2 (Linux)

<br />

## Requisitos 

- Windows 10 (versão 2004 ou superior, build 19041+) ou Windows 11
- Virtualização ativada na BIOS/UEFI do seu Notebook ou Computador.

<br />

## Instalação



1. **Abra o PowerShell como administrador:** clique com o botão direito no menu Iniciar e clique na opção *Terminal (Administrador)* ou *Windows PowerShell (Administrador)*.

![](https://i.imgur.com/LcwsvwS.png)

2. **Instale o WSL:** execute o comando abaixo no Terminal (Modo Administrador)

```cmd
wsl --install
```

> O comando acima ativa todos os recursos necessários para executar o WSL2.

3. Após a conclusão da instalação, reinicie o computador.

![](https://i.imgur.com/31stvbt.png)

4. Após reiniciar, procure por **Ubuntu** no menu Iniciar. Se ele não aparecer, abra a **Microsoft Store**

![](https://i.imgur.com/lNM3mGi.png)

5. Localize a distribuição Ubuntu e clique no botão **Adquirir**

![](https://i.imgur.com/5sk1HfW.png)

6. Após a conclusão da instalação, clique no botão **Abrir**

![](https://i.imgur.com/3mIwvMA.png)

7. O Terminal do Ubuntu será aberto. Crie seu nome de usuário. Como sugestão, o Ubuntu indicará o mesmo nome do seu usuário Windows. Pressione a tecla **enter**

![](https://i.imgur.com/sZxrJSb.png)

> [!IMPORTANT]
>
> A versão do Ubuntu pode ser diferente da versão exibida na imagem.

8. Digite uma senha para o seu usuário e pressione a tecla **enter**.

![](https://i.imgur.com/SKlUJzO.png)

> [!WARNING]
>
> Enquanto você estiver digitando senha, não será exibido nada na tela. Apenas digite a senha e pressione a tecla **enter**.

9. Digite a mesma senha novamente e pressione a tecla **enter**.

![](https://i.imgur.com/RW9MCAo.png)

10. Na sequência, será perguntado se você deseja compartilhar dados do Ubuntu. Responda **n** (não)

![](https://i.imgur.com/t2HqJ03.png)

11. O Ubuntu Linux estará pronto para uso

![](https://i.imgur.com/EzetBXE.png)

12. Para abrir o Linux da próxima vez, procure no menu iniciar por "Ubuntu".

![](https://i.imgur.com/lEY0dfw.png)

---

## Problemas comuns

<br />

### ❌Erro de virtualização 

Caso você receba uma das 2 mensagens abaixo durante a instalação do WSL2 ou do Ubuntu, siga os passos a seguir.

![](https://i.imgur.com/av6YKMi.png)

<br />

![](https://i.imgur.com/N2K281w.png)

<br />

1. Reinicie o computador e acesse a BIOS/UEFI do seu computador
2. Verifique na BIOS/UEFI se o *Intel VT-x* ou *AMD-V/SVM* estão ativos.

<br />

### ❌Comando `wsl --install` não reconhecido 

1. Execute o **Windows Update** para atualizar o Windows e tente instalar novamente
2. Caso não funcione, no menu iniciar localize o item **Ativar ou desativar recursos do Windows**

![](https://i.imgur.com/VMEwYGE.png)

3. Marque as opções **Plataforma de Máquina Virtual** e **Subsistema do Windows para Linux**, como vemos nas imagens abaixo:

| ![](https://i.imgur.com/RqlhFEs.png) | ![](https://i.imgur.com/sur9rV8.png) |
| ------------------------------------ | ------------------------------------ |

4. Reinicie o computador e tente novamente

