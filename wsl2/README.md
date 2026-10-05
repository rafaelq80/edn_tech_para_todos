# Guia de Instalação do WSL2 (Linux)

<br />

## Requisitos 

- Windows 10 (versão 2004 ou superior, build 19041+) ou Windows 11
- Virtualização ativada na BIOS/UEFI do seu Notebook ou Computador.

<br />

## Versão do Windows 10



> [!WARNING]
>
> Este passo é exclusivo para computadores com **Windows 10**. Se o seu computador possui o **Windows 11** instalado, siga para o próximo passo.

<br />

1. Abra o **PowerShell** e execute o comando abaixo para descobrir qual é a versão do seu Windows 10

```powershell
Get-CimInstance Win32_OperatingSystem | Select-Object Caption, Version, BuildNumber
```

2. Se a versão for a **Build 19041** ou superior, pode instalar o WSL2 tranquilamente
3. Caso não seja, exceute o **Windows Update** para atualizar o Windows e verifique novamente

<br />

## Virtualização



1. Abra o **Gerenciador de Tarefas** pressionando as teclas `Ctrl + Shift + Esc` 

![](https://i.imgur.com/2FEe75N.png)

2. Na guia **Desempenho**, clique na guia **CPU** e verifique se o campo **Virtualização** está **Habilitado**, como mostra a imagem abaixo:

![](https://i.imgur.com/LEOGNOi.png)

3. Caso esteja, não precisa mexer na BIOS/UEFI.

<br />

> [!WARNING]
>
> No final deste guia, na seção **Problemas Comuns**, tem um tutorial explicando como habilitar a virtualização.

<br />

## Instalação



1. **Abra o PowerShell como administrador:** clique com o botão direito no menu Iniciar e clique na opção *Terminal (Administrador)* ou *Windows PowerShell (Administrador)*.

![](https://i.imgur.com/LcwsvwS.png)

2. **Instale o WSL:** execute o comando abaixo no Terminal (Modo Administrador)

```powershell
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



### ❌A Virtualização não está ativa no sistema 



1. Abra o **PowerShell** e execute o comando abaixo para descobrir qual é o fabricante da placa mãe do seu computador, caso você não saiba

```powershell
Get-CimInstance Win32_ComputerSystem | Select-Object Manufacturer, Model
```

2. Reinicie o computador e pressione repetidamente a tecla de acesso a BIOS/UEFI do seu computador assim que o logotipo do fabricante aparecer. 

![](https://i.imgur.com/ptDCrax.png)

Na tabela abaixo, você confere a tecla de acesso a BIOS/UEFI das placas-mãe e notebooks mais populares do mercado:

| Marca            | Tecla de Acesso                                       |
| ---------------- | ----------------------------------------------------- |
| ASUS             | Del ou F2                                             |
| Gigabyte / AORUS | Del ou F2                                             |
| MSI              | Del ou F2                                             |
| ASRock           | Del ou F2                                             |
| Dell / Alienware | F2                                                    |
| HP               | F10                                                   |
| Lenovo           | F1 (ThinkPad) / F2 ou Fn + F2 (IdeaPad, Yoga, Legion) |
| Acer             | F2                                                    |

3. Será aberta a janela BIOS/UEFI. No exemplo abaixo, vemos a BIOS/UEFI de um **Notebook ThinkPad Lenovo**:

![](https://i.imgur.com/KBZ96EN.png)

<br />

> [!TIP]
>
> A aparência da tela da BIOS/UEFI pode ser diferente da imagem acima, dependendo do fabricante da placa-mãe.

4. Localize na BIOS/UEFI do seu computador, uma das opções abaixo, de acordo com o processador da sua máquina:

- **Intel:** *Intel Virtualization Technology* ou *VT-x*
- **AMD:** *SVM Mode* ou *AMD-V*
- **Alguns notebooks:** *Virtualization Technology* ou *Virtualization Support*

No **ThinkPad Lenovo** fica na guia **Security → Virtualization**:

![](https://i.imgur.com/ruQOhW8.png)

Na tabela abaixo, você confere o caminho exato para ativar a virtualização Intel (Intel VT-x / SVM / VMX) nas marcas de placas-mãe e notebooks mais populares do mercado:

| Marca            | Caminho no Menu da BIOS                                      | Nome da Opção                        |
| ---------------- | ------------------------------------------------------------ | ------------------------------------ |
| ASUS             | Advanced Mode (F7) → Advanced → CPU Configuration            | Intel Virtualization Technology      |
| Gigabyte / AORUS | Advanced Mode (F2) → Tweaker → Advanced CPU Settings         | Intel Virtualization Technology      |
| MSI              | Advanced (F7) → OC → CPU Features (ou Overclocking → Processor Features) | Intel Virtualization Tech / SVM Mode |
| ASRock           | Advanced → CPU Configuration                                 | Intel Virtualization Technology      |
| Dell / Alienware | Virtualization Support → Virtualization                      | Intel Virtualization Technology      |
| HP               | Advanced → Device Options (ou System Configuration)          | Virtualization Technology (VTx)      |
| Lenovo           | Security → Virtualization                                    | Intel Virtualization Technology      |
| Acer             | Advanced (ou System Configuration)                           | Intel VTx / Virtualization Tech      |

<br />

> [!NOTE]
>
> * **Processadores AMD:** Caso o seu processador seja AMD em vez de Intel, o nome da opção muda para **SVM Mode (Secure Virtual Machine) ou AMD-V**, mas o caminho nas pastas da BIOS listadas acima costumam ser o mesmo. Em caso de dúvidas, consulte o manual do no site do fabricante.

<br />

5. Habilite a opção **Intel(R) Virtualization Technology** alterando para `Enabled`, como mostra a figura abaixo:

![](https://i.imgur.com/c9LXb1P.png)

<br />

> [!IMPORTANT]
>
> No **ThinkPad T14 - Lenovo**, a opção *Intel Virtualization Technology* só pôde ser alterada com o *Kernel DMA Protection* desativado. Em **Security → Virtualization**, foi seguida a seguinte ordem:
>
> 1. **Kernel DMA Protection:** `Disabled`
> 2. **Intel(R) Virtualization Technology:** `Enabled`
> 3. **Kernel DMA Protection:** `Enabled` *(reative; a virtualização continua habilitada)*
>
> Ao reativar o **Kernel DMA Protection**, será perguntado se a virtualização deve ser mantida habilitada. Pressione a tecla `y` para continuar. 

<br />

6. Pressione **F10** (salvar e sair) e confirme com **Yes** para reiniciar o computador
7. Verifique no **Gerenciador de Tarefas** se a virtualização foi habilitada

![](https://i.imgur.com/LEOGNOi.png)

<br />

> [!TIP]
>
> **Se não funcionar**
>
> - **Opção não aparece:** atualize a BIOS pelo site do fabricante ou confira se o modelo do processador suporta virtualização.
> - **Opção bloqueada (acinzentada):** pode haver senha de administrador na BIOS ou política da empresa. Isso é comum em computadores corporativos.

<br />

### ❌Comando `wsl --install` não reconhecido 

1. Execute o **Windows Update** para atualizar o Windows e tente instalar novamente
2. Caso não funcione, no menu iniciar localize o item **Ativar ou desativar recursos do Windows**

![](https://i.imgur.com/VMEwYGE.png)

3. Marque as opções **Plataforma de Máquina Virtual** e **Subsistema do Windows para Linux**, como vemos nas imagens abaixo:

| ![](https://i.imgur.com/RqlhFEs.png) | ![](https://i.imgur.com/sur9rV8.png) |
| ------------------------------------ | ------------------------------------ |

4. Reinicie o computador e tente novamente

