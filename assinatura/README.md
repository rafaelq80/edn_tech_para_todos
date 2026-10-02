# Guia de Prompts usados na Criação das Assinaturas de e-mail



Nesta seção, disponibilizamos os **prompts prontos** que você pode utilizar em ferramentas de Inteligência Artificial para gerar o código HTML da sua assinatura, os ícones personalizados e o logotipo da empresa.



## 1. Prompts para Gerar o Código HTML da Assinatura

Copie e cole o prompt desejado em um modelo de linguagem (como ChatGPT, Claude ou Gemini) para gerar a estrutura em HTML responsivo.

### Opção A: Assinatura Corporativa (Com Logo e Informações Completas)

> **Prompt:**
>
> "Atue como um desenvolvedor Front-end especializado em e-mail marketing. Crie o código HTML de uma assinatura de e-mail responsiva usando tabelas embutidas (`<table>`) para garantir total compatibilidade com o Gmail.
>
> **Estrutura e Estilo:**
>
> - **Fundo:** Card retangular com cantos arredondados (`border-radius: 12px`), fundo levemente azulado/cinza claro (`#F0F4F8`) e bordas suaves.
> - **Divisão Interna:** Duas colunas separadas por uma linha vertical sutil na cor azul-escuro.
> - **Coluna da Esquerda:**
>   - Nome completo em negrito e cor escura (`#102A43`).
>   - Nome da empresa em negrito.
>   - Cargo / Função em duas linhas.
> - **Coluna Central/Direita:**
>   - Lista vertical com 3 linhas (ícone + texto embutido):
>     1. Ícone do WhatsApp + Telefone
>     2. Ícone de E-mail + Endereço de E-mail
>     3. Ícone de Website + Domínio da Empresa
> - **Coluna da Direita:**
>   - Espaço para a imagem do logotipo da empresa alinhado à direita.
>
> **Regras do código:** Use apenas CSS inline e links temporários do tipo `[https://via.placeholder.com/](https://via.placeholder.com/)...` nas tags `<img>` para fácil substituição futura."

### Opção B: Assinatura Pessoal / Acadêmica (Com Redes Sociais)

> **Prompt:**
>
> "Crie o código HTML de uma assinatura de e-mail corporativa e enxuta para uso no Gmail, utilizando estruturas de tabelas HTML (`<table>`) e CSS inline.
>
> **Estrutura e Estilo:**
>
> - **Fundo:** Card retangular suave (`#EBF1F5`) com cantos arredondados (`border-radius: 12px`).
> - **Coluna da Esquerda:**
>   - Nome completo em destaque e negrito (`#102A43`).
>   - Cargo / Áreas de Especialização em cor secundária.
> - **Coluna da Direita:**
>   - Linha 1: Ícone do WhatsApp + Telefone.
>   - Linha 2: Ícone de E-mail + Endereço de E-mail.
>   - Linha 3: Três ícones circulares dispostos lado a lado na horizontal: **LinkedIn**, **GitHub** e **Website**.
>
> **Regras do código:** O código deve ser limpo, totalmente responsivo e utilizar links de placeholder para os ícones."

---

## 2. Prompt para Gerar os Ícones da Assinatura (Tamanho Pequeno)

Para criar a identidade visual dos ícones:

> **Prompt de Imagem:**
>
> *"Conjunto de ícones circulares minimalistas, círculo sólido em azul-marinho escuro preenchido com um pictograma vetorial branco e limpo de `[INSERIR O TIPO: WhatsApp / Envelope / Globe / LinkedIn / GitHub]`, design plano, ícone vetorial, isolado em fundo branco puro, alta resolução, 512x512 pixels --no 3d sombras gradientes"*

💡 **Dica de aplicação:** Após a geração, redimensione os ícones para **20px x 20px** ou **24px x 24px** e salve no formato `.png` com fundo transparente.

---

## 3. Prompt para Gerar a Logo da Empresa

Para criar a identidade visual do logotipo corporativo (exemplo: Nuvem Fluxo):

> **Prompt de Imagem:**
>
> *"Logotipo moderno de empresa de tecnologia para 'Nuvem Fluxo', apresentando um ícone de nuvem estilizada feita de linhas de circuitos tecnológicos, nós de dados e setas de crescimento voltadas para cima em seu interior, cores em gradiente azul e ciano, com tipografia profissional em negrito abaixo onde se lê 'NUVEM FLUXO' e o slogan 'SOLUÇÕES CLOUD ÁGEIS', design vetorial limpo, isolado em fundo branco --no fotos realistas renderização 3d"*

💡 **Dica de aplicação:** Ajuste as dimensões finais do logo para no máximo **180px de largura** por **60px de altura**, garantindo que o peso do arquivo não ultrapasse **30 KB**.

---

## 4. Hospedagem das Imagens e Atualização do Código HTML

Para que suas imagens (logo e ícones) apareçam corretamente nos e-mails enviados sem quebrarem ou serem bloqueadas como anexos, elas precisam estar hospedadas em um servidor seguro (HTTPS).

#### 💡 Dica Prática: Como Hospedar as Imagens no ImageKit.io

1. Acesse o site do [ImageKit.io](https://imagekit.io/) e crie uma conta gratuita.
2. No painel de controle, vá até **Media Library** e faça o upload das imagens do seu logo e dos ícones.
3. Clique sobre cada imagem enviada e copie a **URL pública (HTTPS)** fornecida (exemplo: `[https://ik.imagekit.io/suaconta/icon-whatsapp.png](https://ik.imagekit.io/suaconta/icon-whatsapp.png)`).

#### Prompt para Solicitar à IA a Substituição dos Links no Código HTML

Com os links das imagens em mãos, utilize o prompt abaixo para que a Inteligência Artificial atualize o código HTML da sua assinatura de forma automática:

> **Prompt:**
>
> "Tenho o código HTML da minha assinatura de e-mail e os links das imagens hospedadas no ImageKit. Por favor, substitua os endereços temporários (`src="..."`) das imagens no código HTML abaixo pelos links correspondentes que forneço a seguir:
>
> **Links das Imagens (ImageKit):**
>
> - Logo da Empresa: `[Cole aqui a URL do seu logo]`
> - Ícone do WhatsApp: `[Cole aqui a URL do ícone do WhatsApp]`
> - Ícone de E-mail: `[Cole aqui a URL do ícone de E-mail]`
> - Ícone de Website: `[Cole aqui a URL do ícone de Website]`
> - Ícone do LinkedIn: `[Cole aqui a URL do ícone do LinkedIn]`
> - Ícone do GitHub: `[Cole aqui a URL do ícone do GitHub]`
>
> **Código HTML Atual:**
>
> `[Cole aqui o código HTML gerado anteriormente]`
>
> Garanta que todas as tags `<img>` mantenham os atributos `alt` preenchidos, dimensões explícitas (`width` e `height`) e o estilo `border: 0; vertical-align: middle;`."