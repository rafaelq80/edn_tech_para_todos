# Laboratório Prático - Gerenciamento de Processos e Protocolos de Rede no Windows CMD



**Objetivo:** Utilizar a linha de comando do Windows (CMD) para diagnosticar, monitorar e administrar recursos do sistema e da rede. 

<br />

Ao final do laboratório, o aluno será capaz de:
- Mapear e controlar processos ativos no sistema operacional;
- Analisar o tráfego da pilha TCP/IP;
- Inspecionar a resolução de nomes (DNS);
- Mapear endereços físicos e lógicos (ARP);
- Compreender o caminho e as rotas que os pacotes percorrem através da rede local e do provedor de internet.

Neste laboratório, você utilizará o **CMD** para inspecionar e gerenciar processos do sistema, testar conexões da pilha TCP/IP, manipular o cache de resolução de nomes (DNS e ARP) e analisar a tabela de roteamento IP.

<br />

## Pré-requisitos



- **Sistema Operacional:** Windows 10 ou 11.
- **Prompt de Comando (CMD) como Administrador:**
  - Abra o **Windows Terminal**.
  - Clique na seta ao lado da aba aberta e, na sequência, clique com o **botão direito do mouse** sobre o ícone do **Prompt de Comando** e selecione a opção **Executar como administrador**, como mostra a figura abaixo:

    ![](https://i.imgur.com/FFJb967.png)

  - O Windows pedirá autorização para executar o CMD em Modo Administrador. Responda **Sim**.
  - Observe que na Barra de Título da janela do Terminal CMD, será exibida a mensagem: **Administrador: Prompt de Comando**, como vemos na imagem abaixo:

    ![](https://i.imgur.com/KLUt0qg.png)

> [!TIP]
> **Outra forma de abrir o Terminal CMD no Modo Administrador:**
> - Pressione as teclas **`Windows + R`** para abrir o Executar.
> - Digite **`cmd`** e pressione a combinação **`Ctrl + Shift + Enter`**.

<br />

## ✅ Gerenciamento e Inspeção de Processos



Inicie, monitore e finalize processos diretamente pela linha de comando.

1. Listar todos os processos em execução no sistema:
```cmd
tasklist
```

2. Iniciar uma instância do Bloco de Notas para teste:

```cmd
start notepad.exe
```

> O Bloco de Notas será aberto. **Não feche, apenas minimize a janela.**

3. Filtrar a lista para localizar apenas o processo do Bloco de Notas e obter seu PID:

```cmd
tasklist /fi "IMAGENAME eq notepad.exe"
```

4. Finalizar o Bloco de Notas de forma forçada usando o nome da imagem:

```cmd
taskkill /f /im notepad.exe
```

<br />

## ✅ Inspeção e Gerenciamento de Interfaces IP (ipconfig)



Exiba os detalhes da interface de rede, Gateway Padrão e simule a renovação do endereço IP atribuído via DHCP.

1. Exibir configurações básicas de IP de todos os adaptadores de rede:

```cmd
ipconfig
```

2. Exibir relatório detalhado (Endereço MAC, Servidor DHCP, DNS e o IP):

```cmd
ipconfig /all
```

<br />

> [!NOTE]
>
> ### ✅Entendendo os principais Campos do `ipconfig`
>
> 
>
>
> * **Endereço Físico (MAC Address):** Identificador único gravado de fábrica na placa de rede (Camada 2 - Enlace). Usado para comunicação na rede local.
> * **DHCP Habilitado (Sim/Não):** Indica se o computador recebe as configurações de IP automaticamente do roteador (`Sim`) ou se foi configurado manualmente/estático (`Não`).
> * **Endereço IPv4 (Preferencial):** O endereço IP lógico (Camada 3) atual do computador na rede local. *(Preferencial significa que é o IP principal em uso)*.
> * **Máscara de Sub-rede:** Define qual parte do endereço IP identifica a **rede** e qual parte identifica a **máquina**. O valor `255.255.255.0` indica que todos os dispositivos dessa rede começam com `192.168.0.X`.
> * **Gateway Padrão:** O endereço IP do seu **roteador**. É a "porta de saída" para pacotes que têm como destino redes externas (como a Internet).
> * **Servidor DHCP:** O IP do equipamento responsável por distribuir os endereços IP na rede (geralmente é o próprio roteador).
> * **Servidores DNS:** Os IPs dos servidores responsáveis por traduzir nomes de domínios (ex: `google.com`) em endereços IP legíveis para a rede.

<br />

## ✅ Testes de Conectividade e Rastreamento (Camada de Rede e Transporte)



Valide a conectividade ICMP e rastreie os saltos de rede até um servidor remoto.

1. Testar conectividade ICMP (Echo Request) com 4 pacotes:

```cmd
ping 8.8.8.8
```

**Resposta Esperada:**

```cmd
Disparando 8.8.8.8 com 32 bytes de dados:
Resposta de 8.8.8.8: bytes=32 tempo=12ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=10ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=11ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=12ms TTL=117
```

<br />

> [!NOTE]
> ### ✅ O que é o TTL (Time to Live)?
>
> 
>
>
> O **TTL (Time to Live)** é um contador no cabeçalho do pacote IP que limita o seu tempo de vida na rede para evitar que pacotes fiquem circulando infinitamente em loops de roteamento.
> * **Funcionamento:** O sistema de origem define um valor inicial (ex: 64 ou 128). Cada roteador pelo qual o pacote passa diminui esse valor em **1**. Se o TTL chegar a **0**, o pacote é descartado.
> * **Para que serve na prática:**
> 1. **Contar saltos:** Permite calcular por quantos roteadores o pacote passou até o destino através da fórmula:
>
>     $$
>     \text{Saltos} = \text{TTL Inicial} - \text{TTL Recebido}
>     $$
>
> 2. **Identificar o Sistema Operacional do destino:**
> * **TTL perto de 64:** Destino é **Linux / macOS / Android**.
> * **TTL perto de 128:** Destino é **Windows**.
> * **TTL perto de 255:** Destino é um equipamento de rede (**Cisco / Roteador**).
>

<br />

2. Rastrear os saltos (roteadores) no caminho até um domínio remoto:

```cmd
tracert google.com
```

<br />

## ✅ Mapeamento de Portas TCP/UDP



Identifique conexões estabelecidas, portas em escuta e descubra qual processo é responsável por cada conexão.

1. Listar todas as conexões ativas e portas em escuta exibindo o PID de cada processo:

```cmd
netstat -ano
```

2. Filtrar apenas as conexões TCP que estão no estado ESTABLISHED:

```cmd
netstat -ano | findstr "ESTABLISHED"
```

<br />

## ✅ Resolução de Nomes e Diagnóstico de Cache DNS



Consulte registros no servidor DNS e gerencie a tabela de cache DNS local da máquina.

1. Consultar o endereço IP (A) de um domínio usando o utilitário nslookup:

```cmd
nslookup google.com
```

2. Visualizar todo o cache de resoluções DNS armazenado localmente:

```cmd
ipconfig /displaydns
```

<br />

## ✅ Tabela ARP (Camada de Enlace / Interrede)



Inspecione o mapeamento entre endereços IP (L3) e endereços físicos MAC (L2) na rede local.

1. Exibir toda a tabela e cache de vizinhos ARP:

```cmd
arp -a
```

<br />

## ✅ Tabela de Roteamento IP (Camada de Rede)



Exiba e manipule as rotas de encaminhamento de pacotes do sistema operacional.

1. Exibir a tabela de roteamento IPv4 completa do Windows:

```cmd
route print
```

<br />

## ✅ Tabela Comparativa: Windows CMD vs. Linux (Bash)



| Categoria | Ação / Objetivo | Windows CMD | Equivalente Linux (Bash) |
| --- | --- | --- | --- |
| **Interface IP** | Exibir resumo das placas e IPs | `ipconfig` | `ip a` / `ifconfig` |
| **Interface IP** | Detalhar MAC, DHCP e DNS | `ipconfig /all` | `ip addr show` / `nmcli dev show` |
| **Processos** | Listar processos ativos | `tasklist` | `ps aux` / `top` |
| **Processos** | Filtrar processo pelo nome | `tasklist /fi "IMAGENAME eq nome.exe"` | `pgrep -l nome` / `ps aux | grep nome` |
| **Processos** | Encerrar processo forçadamente | `taskkill /f /im nome.exe` *(ou `/pid <PID>`)* | `kill -9 <PID>` / `pkill -f nome` |
| **Processos** | Iniciar programa em 2º plano | `start programa.exe` | `programa &` / `nohup programa &` |
| **Rede (L3/L4)** | Testar conectividade (ICMP) | `ping <IP/Host>` | `ping <IP/Host>` |
| **Rede (L3)** | Rastrear rota até o destino | `tracert <Host>` | `traceroute <Host>` / `tracepath <Host>` |
| **Rede (L4)** | Exibir conexões e PIDs | `netstat -ano` | `ss -tulpn` / `netstat -tulpn` |
| **DNS** | Consultar registros DNS | `nslookup <Host>` | `nslookup <Host>` / `dig <Host>` |
| **ARP (L2/L3)** | Exibir tabela/cache ARP | `arp -a` | `ip neighbor show` / `arp -an` |
| **Rotas (L3)** | Exibir tabela de roteamento | `route print` | `ip route show` / `route -n` |

