# **Relatório Detalhado de Modificações da ISO – Windows 10 Pro Lite (NTLite)**

## **Introdução**

Este documento é um registro completo e detalhado de todas as alterações aplicadas a uma imagem oficial do Windows 10 Pro através do software NTLite. O objetivo é servir como um guia de referência preciso, tanto para conferência pessoal quanto para que outros usuários possam entender, replicar ou adaptar estas configurações para suas próprias necessidades.

A estrutura deste relatório segue fielmente a ordem das seções e itens apresentados na interface do NTLite, facilitando a localização de cada ajuste. Todas as explicações originais sobre a função de cada componente foram mantidas para garantir a clareza para todos os níveis de usuário.

É fundamental deixar claro que **este relatório lista exclusivamente as configurações e componentes que foram efetivamente modificados**.

Para uma referência completa e exaustiva, que cobre a função de **absolutamente todos os componentes, serviços e configurações disponíveis no NTLite** (incluindo os itens que não foram alterados neste projeto), consulte o registro completo da conversa com a IA que auxiliou no processo.

> **Fonte de Consulta Original:**
> Para um aprofundamento sobre o "porquê" de cada decisão, a conversa completa com a IA que auxiliou no processo está registrada no seguinte link:
> [Acessar Histórico da Conversa no AI Studio](https://aistudio.google.com/u/1/prompts/1rUz_38SC4EP48Ewz_8jv5LHaSki5FF_K)

### **Download e Instalação da ISO**

A imagem ISO finalizada, resultado de todas as modificações descritas abaixo, está disponível para download no seguinte link:

> **Link para Download:**
> [ISO-Windows-10-22H2-PT-BR-Lite](https://drive.google.com/drive/folders/1nhJ59p_-GoKv2LkxFX0lCGs30B7hkZ8t?usp=sharing)

Para instalar este sistema operacional, o processo é simples: utilize a ferramenta gratuita **Rufus** para gravar o arquivo ISO em um pendrive, tornando-o inicializável (bootável). Após isso, basta iniciar o computador pelo pendrive para começar a instalação.

---

## **Iniciar -> Imagem (1 Modificação)**

-   **Ação Realizada:** Apenas a imagem do **Windows 10 Pro** foi extraída e selecionada para modificação, descartando outras edições contidas no arquivo ISO original da Microsoft.

---

## **Integrar -> Atualizações (10 Modificações)**

### **Atualização Cumulativa**

1.  **Cumulative Update Preview (KB5028248)**
    -   **O que faz:** É uma atualização de "prévia" (preview). A Microsoft as lança no final do mês para que administradores de sistema possam testar as correções que virão na atualização oficial e obrigatória do mês seguinte. Elas não contêm atualizações de segurança e podem ter bugs.

2.  **Cumulative Update (KB5028166)**
    -   **O que faz:** Esta é a atualização cumulativa "oficial" e final do mês. Ela contém todas as correções de segurança e de bugs importantes até a data de seu lançamento. É a atualização mais importante da lista.

---

### **.NET Framework**

3.  **KB5026578, KB5026577, KB5011048 (.NET Framework Updates)**
    -   **O que fazem:** São atualizações de segurança e qualidade para o .NET Framework, uma plataforma de software da Microsoft. Muitos programas, incluindo partes do Visual Studio, PowerToys e outras ferramentas que você usa, dependem de versões específicas do .NET para funcionar.

---

### **Aplicativos & Recursos**

4.  **KB2267602 & KB4052623 (Microsoft Defender Antivirus updates)** `(IMPORTANTE: WINDOWS DEFENDER)`
    -   **O que fazem:** Atualizam o motor e a plataforma do Windows Defender.
    -   **Status:** **NÃO MARCADOS** para integração, pois o Defender será removido.

5.  **Windows Package Manager (App Installer, WinGet)**
    -   **O que faz:** É o gerenciador de pacotes oficial da Microsoft (como o `apt` do Linux ou `brew` do macOS). Permite instalar programas via linha de comando (ex: `winget install spotify`). É extremamente útil para desenvolvedores.

6.  **Microsoft.UI.Xaml & Microsoft Visual C++ UWP Runtime**
    -   **O que fazem:** São bibliotecas de interface e de runtime para aplicativos modernos do Windows (UWP/WinUI). Muitos aplicativos, incluindo partes do próprio sistema como a Ferramenta de Captura (Win+Shift+S) e até mesmo os PowerToys, dependem desses pacotes para renderizar suas janelas e controles.

7.  **Windows Terminal**
    -   **O que faz:** É o novo aplicativo de terminal moderno da Microsoft, que unifica Prompt de Comando, PowerShell e terminais do WSL (Linux) em uma única janela com abas.
    -   **Status:** **NÃO MARCADO** para integração, pois pode ser instalado via WinGet posteriormente.

8.  **Windows Subsystem for Linux (WSL)**
    -   **O que faz:** É a atualização para a camada de compatibilidade que permite rodar Linux no Windows.

---

### **Outro**

9.  **Safe OS Dynamic Update & Dynamic Update for Windows setup**
    -   **O que fazem:** São pequenas atualizações para o próprio ambiente de instalação e recuperação do Windows (WinRE e Windows Setup). Elas corrigem bugs que podem ocorrer *durante* a formatação do computador, tornando o processo mais confiável.

10. **Intel Memory Mapped I/O Security Update**
    -   **O que faz:** É uma atualização de segurança de hardware (microcódigo) específica para processadores Intel. Ela corrige vulnerabilidades a nível de CPU.

---

## **Integrar -> Registro (5 Modificações)**

1.  **Tweak_Accessibility_Keys_Flags.reg**
    ```reg
    Windows Registry Editor Version 5.00

    [HKEY_CURRENT_USER\Control Panel\Accessibility\MouseKeys]
    "Flags"="0"

    [HKEY_CURRENT_USER\Control Panel\Accessibility\StickyKeys]
    "Flags"="0"

    [HKEY_CURRENT_USER\Control Panel\Accessibility\Keyboard Response]
    "Flags"="0"

    [HKEY_CURRENT_USER\Control Panel\Accessibility\ToggleKeys]
    "Flags"="0"
    ```

2.  **Tweak_Disable_GameDVR_Policy.reg**
    ```reg
    Windows Registry Editor Version 5.00

    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\default\ApplicationManagement\AllowGameDVR]
    "value"=dword:00000000
    ```

3.  **Tweak_GlobalTimerResolution.reg**
    ```reg
    Windows Registry Editor Version 5.00

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\kernel]
    "GlobalTimerResolutionRequests"=dword:00000001
    ```

4.  **Tweak_Graphics_DisablePreemption.reg**
    ```reg
    Windows Registry Editor Version 5.00

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler]
    "EnablePreemption"=dword:00000000
    ```

5.  **Tweak_Multimedia_Profile_Games.reg**
    ```reg
    Windows Registry Editor Version 5.00

    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games]
    "Scheduling Category"="High"
    "SFIO Priority"="High"
    ```

---

## **Integrar -> Pós Instalação (10 Modificações)**

### **Antes do Logon**

-   Arquivo `fundo.png` copiado para `\Windows\Web\Wallpaper\Windows\fundo.PNG`
-   Pasta `icons` copiada para `\Windows\Web\icons\`

### **Após o Logon**

-   **Comandos CMD Executados:**
    ```cmd
    :: Adiciona e ativa o plano de energia de "Desempenho Máximo"
    powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61

    :: Desativa a hibernação, liberando espaço em disco (equivalente ao tamanho da RAM)
    powercfg.exe /hibernate off

    :: Ajustes de timer do sistema para potencializar performance e reduzir latência
    bcdedit /set useplatformtick yes
    bcdedit /set disabledynamictick yes
    bcdedit /deletevalue useplatformclock
    bcdedit /set tscsyncpolicy Enhanced

    :: Define o papel de parede personalizado e força a atualização da interface
    reg add "HKCU\Control Panel\Desktop" /v Wallpaper /t REG_SZ /d "C:\Windows\Web\Wallpaper\Windows\fundo.PNG" /f
    RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters
    ```

---

## **Remover -> Componentes (104 Modificações)**

Foram **REMOVIDOS** os seguintes componentes:

### **Apps do Sistema**

1.  **Aplicativo Bloqueio de Tela de Acesso Atribuído**
    -   **O que faz:** É o recurso de "Modo Kiosk", que permite travar o Windows para rodar um único aplicativo, usado em totens de atendimento ou displays públicos.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

2.  **Caixa de diálogo Adicionar Sugestões de Pasta**
    -   **O que faz:** É a pequena janela que sugere adicionar pastas às suas "Bibliotecas" (Documentos, Imagens, etc.) quando você salva algo em um novo local.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

3.  **Chamada**
    -   **O que faz:** É o antigo aplicativo "Discador" do Windows, usado para fazer chamadas por modem.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

4.  **Controle com os Olhos**
    -   **O que faz:** Recurso de acessibilidade que permite controlar o Windows com os olhos, usando hardware específico.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

5.  **Fazer um Teste**
    -   **O que faz:** Um aplicativo para professores criarem e aplicarem provas em um ambiente seguro e travado.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

6.  **Gerenciador de Entrega de Conteúdo**
    -   **O que faz:** É um componente que instala automaticamente aplicativos "sugeridos" (lixo, como Candy Crush) após a instalação do Windows.
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.**

7.  **Narrador**
    -   **O que faz:** Ferramenta de acessibilidade que lê o texto da tela em voz alta.
    -   **Reinstalável depois?:** Sim, através das Configurações -> Facilidade de Acesso.
    -   **Recomendação:** **REMOVER.**

8.  **Recursos da familia Microsoft**
    -   **O que faz:** Controles parentais (Microsoft Family Safety).
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.**

9.  **Tela de Bloqueio padrão do Windows**
    -   **O que faz:** A tela que aparece antes da tela de login, mostrando uma imagem e notificações. Não é a tela de login em si.
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.**

10. **Visualização de Código de Barras do Windows**
    -   **O que faz:** Um componente para aplicativos que precisam ler códigos de barra.
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.**

11. **Windows Defender** `(IMPORTANTE: WINDOWS DEFENDER)`
    -   **O que faz:** O antivírus nativo do Windows.
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.** (Pois será utilizado um antivírus de terceiros).

12. **Xbox Game UI**
    -   **O que faz:** Todos os componentes da Game Bar (gravação de clipes, painel social, etc.).
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**
    -   **IMPORTANTE** voltei nessa alteração e mantive ele.

---

### **Apps**

13. **Cortana**
    -   **O que faz:** A assistente digital da Microsoft.
    -   **Reinstalável depois?:** Não. A remoção é permanente.
    -   **Recomendação:** **REMOVER.**

14. **Dicas (Vamos Começar)**, 15. **Feedback Hub**, 16. **Get Help**
    -   **O que fazem:** São três aplicativos separados com um propósito similar: dar dicas sobre o Windows, coletar feedback para a Microsoft e oferecer ajuda.
    -   **Reinstalável depois?:** Sim, podem ser baixados novamente da Microsoft Store.
    -   **Recomendação:** **REMOVER TODOS.**

17. **Mail and Calendar**
    -   **O que faz:** Os aplicativos nativos de Email e Calendário.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**

18. **Microsoft Advertising SDK for XAML** e 19. **Microsoft Engagement Framework**
    -   **O que fazem:** São kits para desenvolvedores incluírem propagandas e notificações em seus próprios aplicativos.
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER AMBOS.**

20. **Microsoft Pay**
    -   **O que faz:** A carteira digital da Microsoft para pagamentos.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**

21. **Microsoft People**
    -   **O que faz:** O aplicativo de contatos do Windows, que se integra com Email e Calendário.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**

22. **Microsoft Solitaire Collection**
    -   **O que faz:** Paciência e outros jogos de carta.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**

23. **Microsoft Sticky Notes**
    -   **O que faz:** Aplicativo de notas autoadesivas para a área de trabalho.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**

24. **MSN Weather** e 25. **Windows Maps**
    -   **O que fazem:** Aplicativos de Clima e Mapas.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER AMBOS.**

26. **Office** e 27. **OneNote**
    -   **O que fazem:** Atenção, estes **NÃO** são os aplicativos reais. São apenas "atalhos" ou "hubs" que te incentivam a instalar ou assinar o Microsoft 365.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER AMBOS.**

28. **Paint 3D** e 29. **Visualizador 3D**
    -   **O que fazem:** Ferramentas de modelagem e visualização 3D básicas.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER AMBOS.**

30. **Skype**
    -   **O que faz:** Versão do Skype que vem com o Windows.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**

31. **Xbox Game Bar Plugin**
    -   **O que faz:** São pequenos add-ons que outros aplicativos podem usar para adicionar funcionalidades à Xbox Game Bar.
    -   **Reinstalável depois?:** Sim, reinstalando a Game Bar ou aplicativos relacionados.
    -   **Recomendação:** **REMOVER.**

32. **Xbox Game Bar**
    -   **O que faz:** Este é o aplicativo principal da Game Bar, o overlay que aparece com Win+G.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**

33. **Xbox Game Speech Window**
    -   **O que faz:** Gerencia as funcionalidades de chat de voz (party chat) do ecossistema Xbox.
    -   **Reinstalável depois?:** Sim, mas com dificuldade.
    -   **Recomendação:** **REMOVER.**

34. **Your Phone (Seu Telefone)**
    -   **O que faz:** Aplicativo para integrar seu celular com o Windows.
    -   **Reinstalável depois?:** Sim, pela Microsoft Store.
    -   **Recomendação:** **REMOVER.**

---

### **Comunicação Remota e Privacidade**

35. **Assistência Remota**
    -   **O que faz:** Permite que um técnico de suporte se conecte ao seu computador (com sua permissão).
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

36. **Cliente BranchCache**
    -   **O que faz:** Recurso corporativo que acelera o acesso a arquivos em redes de grandes empresas.
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

37. **Cliente de Pastas de Trabalho**
    -   **O que faz:** Outro recurso corporativo que permite sincronizar arquivos entre seu PC e os servidores da empresa.
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

38. **Conector Multiponto**
    -   **O que faz:** Permite que um PC se conecte a um "Windows MultiPoint Server".
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

39. **Grupo Doméstico**
    -   **O que faz:** Recurso descontinuado para compartilhamento de arquivos e impressoras em rede doméstica.
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.**

40. **Gerenciador de Recursos do Servidor de Arquivos**
    -   **O que faz:** Ferramenta para administradores de TI gerenciarem servidores de arquivos.
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

41. **Microsoft Message Queue (MSMQ)**
    -   **O que faz:** Serviço de enfileiramento de mensagens, usado por alguns aplicativos corporativos antigos.
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

42. **Internet Information Server (IIS)**
    -   **O que faz:** É o servidor web da Microsoft (para hospedar sites).
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

43. **Protocolo de Gerenciamento de Rede Simples (SNMP)**
    -   **O que faz:** Protocolo antigo usado para monitorar dispositivos de rede.
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

44. **Redirecionador de Portas dos Serviços da Área de Trabalho Remota** (RDP)
    -   **O que faz:** Componente usado em cenários complexos de Área de Trabalho Remota (VDI).
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   REATIVEI - Fullscreen Sandbox

---

### **Multimídia**

45. **Serviço de Compartilhamento de Rede WMP - 32 bits**
    -   **O que faz:** Permite compartilhar a biblioteca do Windows Media Player na rede (DLNA).
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.**

46. **Windows Media Player - 32 bits**
    -   **O que faz:** O aplicativo reprodutor de mídia clássico.
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

47. **Ferramenta de Avaliação de Sistema do Windows (WinSAT)**
    -   **O que faz:** Ferramenta que gera o antigo "Índice de Experiência do Windows".
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

48. **Painel de Controle - Compartilhar Mídia**
    -   **O que faz:** O ícone e a janela no Painel de Controle para configurar o serviço de compartilhamento.
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.**

49. **Tela de Fundo da Área de Trabalho (Padrão)** e 50. **Telas de Fundo da Área de Trabalho (Temas)**
    -   **O que fazem:** São os arquivos de imagem (.jpg) dos papéis de parede padrão do Windows.
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER AMBOS.**

---

### **Rede**

51. **Data Center Bridging (DCB)**
    -   **O que faz:** Padrões de rede usados em ambientes de data center.
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

52. **Internet Explorer - 32 bits**
    -   **O que faz:** O navegador legado da Microsoft.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

53. **Active Directory Lightweight Directory Services (AD LDS)**
    -   **O que faz:** Versão "leve" do Active Directory para cenários de desenvolvimento específicos.
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

54. **Serviço Wallet**
    -   **O que faz:** Serviço de back-end para a "Carteira" do Windows (Microsoft Pay).
    -   **Reinstalável depois?:** Não.
    -   **Recomendação:** **REMOVER.**

55. **Serviço de Acesso Remoto e Roteamento**
    -   **O que faz:** Permite que o PC funcione como um servidor de acesso remoto (VPN) ou roteador.
    -   **Reinstalável depois?:** Sim, através do painel de serviços.
    -   **Recomendação:** **REMOVER.**

56. **Serviço de Autenticação da Internet (IAS)**
    -   **O que faz:** Componente de servidor (RADIUS) para autenticar usuários em uma rede.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

---

### **Sistema**

57. **Windows To Go**
    -   **O que faz:** Recurso descontinuado que permitia criar uma versão portátil do Windows em um pendrive.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

58. **Bloqueio de Dispositivo (Experiência Incorporada)**
    -   **O que faz:** Funções para sistemas "embarcados", como quiosques ou caixas eletrônicos.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

59. **Temas de Facilidade de Acesso**
    -   **O que faz:** Os temas de alto contraste para usuários com dificuldades de visão.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

60. **Conteúdo de ajuda do Windows**
    -   **O que faz:** São os próprios arquivos de ajuda (`.chm`) do Windows.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

61. **Tablet PC**
    -   **O que faz:** Adiciona suporte completo para canetas (pen input), reconhecimento de escrita e outras funções de tablet.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

62. **Gerenciador de Rotação Automática**
    -   **O que faz:** O serviço que gira a tela automaticamente em dispositivos conversíveis.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

63. **Virtualização de Aplicativos (App-V)**
    -   **O que faz:** Tecnologia corporativa para fazer streaming de aplicativos para os usuários.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

64. **Virtualização de Experiência do Usuário (UE-V)**
    -   **O que faz:** Tecnologia corporativa para sincronizar as configurações do usuário entre diferentes máquinas.
    -   **Reinstalável depois?:** Não, a remoção é permanente.
    -   **Recomendação:** **REMOVER.**

---

### **Suporte de hardware**

65. **Impressão -> Cliente de Impressão via Internet** `(IMPORTANTE: IMPRESSÃO)`
    -   **O que faz:** Permite conectar a impressoras na internet usando o Internet Printing Protocol (IPP).
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER.**

66. **Scanner / Fax** `(IMPORTANTE: IMPRESSÃO)`
    -   **O que fazem:** São os aplicativos "Windows Fax and Scan".
    -   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    -   **Recomendação:** **REMOVER AMBOS.**

---

### **Tradução (Idiomas Removidos)**

67 a 103. **Foram removidos 37 pacotes de idiomas**, mantendo-se apenas Espanhol, Inglês (GB), Inglês (US), Português (Brasil), Português e Pseudo-locale. Entre os removidos estão: Alemão, Chinês, Japonês, Francês, Russo, Italiano, Coreano, Holandês, todos os Editores de Método de Entrada (IME), entre outros.

---

## **Configurar -> Recursos (13 Modificações)**

Os seguintes recursos foram **DESATIVADOS**:

1.  **Exchange ActiveSync and Internet Mail Sync engine**
    -   **O que faz:** Motor de sincronização para contas de email corporativas (Exchange) e outras (IMAP/POP3).
    -   **Recomendação:** **DESATIVAR.**

2.  **Microsoft Quick Assist (App)**
    -   **O que faz:** Ferramenta de assistência remota da Microsoft.
    -   **Recomendação:** **DESATIVAR.**

3.  **Portuguese (Brazil) speech recognition**
    -   **O que faz:** Reconhecimento de fala em português, usado para ditado e comandos de voz.
    -   **Recomendação:** **DESATIVAR.**

4.  **Portuguese (Brazil) text-to-speech**
    -   **O que faz:** A voz em português para funcionalidades de leitura de texto em voz alta.
    -   **Recomendação:** **DESATIVAR.**

5.  **Print Management** `(IMPORTANTE: IMPRESSÃO)`
    -   **O que faz:** O console de gerenciamento de impressão para administradores.
    -   **Recomendação:** **DESATIVAR.**

6.  **Steps Recorder**
    -   **O que faz:** Gravador de Passos, uma ferramenta para documentar ações para solução de problemas.
    -   **Recomendação:** **DESATIVAR.**

7.  **Windows Fax and Scan** `(IMPORTANTE: IMPRESSÃO)`
    -   **O que faz:** O aplicativo de Fax e Scanner.
    -   **Recomendação:** **DESATIVAR.**

8.  **Windows Media Player Legacy (App)**
    -   **O que faz:** O aplicativo clássico do Windows Media Player.
    -   **Recomendação:** **DESATIVAR.**

9.  **Windows PowerShell Integrated Scripting Environment (ISE)**
    -   **O que faz:** Um editor gráfico para escrever e depurar scripts PowerShell.
    -   **Recomendação:** **DESATIVAR.** (Pois o VS Code é superior).

10. **Microsoft XPS Document Writer** `(IMPORTANTE: IMPRESSÃO)`
    -   **O que faz:** Impressora virtual para criar arquivos .XPS, um formato abandonado.
    -   **Recomendação:** **DESATIVAR.**

11. **SMB Direct**
    -   **O que faz:** Recurso para aceleração de transferência de arquivos em redes de data center.
    -   **Recomendação:** **DESATIVAR.**

12. **Windows PowerShell 2.0**
    -   **O que faz:** Versão antiga e legada do PowerShell.
    -   **Recomendação:** **DESATIVAR.**

12. **Remote Desktop Connection**
    -   **O que faz:** O aplicativo para se conectar a outros computadores remotamente.
    -   **Recomendação:** **DESATIVAR.**

> **Recursos que podem ser ativados posteriormente pelo usuário:**
> Hyper-V, Virtual Machine Platform, Windows Hypervisor Platform, Windows Sandbox, Windows Subsystem for Linux, Windows TIFF IFilter.

---

## **Configurar -> Configurações (79 Modificações)**

Foram aplicados os seguintes ajustes para otimizar a performance, a interface e a privacidade do sistema operacional.

### **Controle de Energia**

1.  **Inicialização Rápida -> Desativado**
    -   **O que faz:** Salva parte dos dados do sistema em um arquivo ao desligar, permitindo um boot mais rápido. No entanto, pode causar problemas com drivers, dual boot e acesso ao disco por outro sistema. Desativar garante um desligamento completo e "limpo".

2.  **Menu de Desligamento - Hibernar -> Desativado**
    -   **O que faz:** Remove a opção "Hibernar" do menu de energia. A hibernação salva todo o conteúdo da RAM no disco rígido, permitindo retomar a sessão exatamente como estava. Desativar essa opção é consistente com o comando `powercfg /hibernate off` usado na pós-instalação para economizar espaço em disco.

### **Controle de travamento**

3.  **Salvar informações de depuração -> Despejo de memória pequeno (256 KB)**
    -   **O que faz:** Em caso de uma Tela Azul (BSOD), o Windows salva um arquivo de "dump" com informações para diagnóstico. A configuração "pequeno" salva apenas o essencial para identificar a causa do erro, ocupando um espaço mínimo em disco em comparação com os despejos completos, que podem ter vários gigabytes.

### **Explorer**

4.  **Abrir Explorador de Arquivos para -> Este PC**
    -   **O que faz:** Altera a visualização padrão do Explorador de Arquivos. Em vez de abrir no "Acesso Rápido" (que mostra pastas frequentes e arquivos recentes), ele abrirá diretamente em "Este PC", exibindo as unidades de disco.

5.  **Exibir informações de tamanho do arquivo nas dicas de pasta -> Ativado**
    -   **O que faz:** Ao passar o mouse sobre uma pasta, a dica de ferramenta exibirá o tamanho total da pasta.

6.  **Exibição - Mostrar arquivos, pastas e unidades ocultas -> Ativado**
    -   **O que faz:** Exibe arquivos e pastas que o Windows oculta por padrão (geralmente arquivos de sistema). Essencial para usuários avançados que precisam de acesso a esses arquivos.

7.  **Exibição - Mostrar extensões dos tipos de arquivos conhecidos -> Ativado**
    -   **O que faz:** Mostra a extensão de todos os arquivos (ex: `.txt`, `.exe`, `.dll`). É uma configuração de segurança crucial para identificar o tipo real de um arquivo e evitar a execução de malware disfarçado.

8.  **Exibição - Mostrar unidades vazias -> Ativado**
    -   **O que faz:** Garante que leitores de cartão ou drives de CD/DVD apareçam em "Este PC" mesmo quando não há mídia inserida.

9.  **Limpar histórico de documentos recentes ao sair -> Ativado**
    -   **O que faz:** É uma configuração de privacidade que apaga a lista de arquivos e documentos abertos recentemente cada vez que o sistema é desligado.

10. **Manter histórico de documentos abertos recentemente -> Desativado**
    -   **O que faz:** Impede que o Windows rastreie os arquivos que você abre. Isso desativa a funcionalidade de "Arquivos recentes" no Acesso Rápido.

11. **Mostrar botão Visualizar Tarefa -> Desativado**
    -   **O que faz:** Remove o ícone "Visão de Tarefas" (usado para gerenciar desktops virtuais) da barra de tarefas, liberando espaço. A funcionalidade continua acessível pelo atalho `Win + Tab`.

12. **Reprodução Automática -> Desativado**
    -   **O que faz:** Desativa a janela que aparece ao conectar um pendrive, HD externo ou outra mídia, perguntando qual ação executar. É uma medida de segurança importante para prevenir a execução automática de vírus.

13. **Sempre exibir mais detalhes no diálogo de cópia de arquivo -> Ativado**
    -   **O que faz:** A janela que mostra o progresso de cópia ou movimentação de arquivos sempre aparecerá no modo detalhado (com gráfico de velocidade) por padrão.

14. **Substituir o Prompt de Comando pelo Windows PowerShell no menu de atalho do botão iniciar -> Desativado**
    -   **O que faz:** Reverte o menu que aparece ao clicar com o botão direito no Menu Iniciar (`Win + X`), fazendo com que ele mostre "Prompt de Comando" em vez de "Windows PowerShell".

### **Menu Iniciar**

15. **Lista de aplicativos - Aplicativos adicionados recentemente -> Desativado**
    -   **O que faz:** Impede que o Menu Iniciar destaque os aplicativos que foram instalados recentemente na lista de programas.

### **Privacidade**

16. **Aplicativos OEM pré-instalados -> Desativado**
    -   **O que faz:** Impede que o Windows instale automaticamente softwares (bloatware) do fabricante do computador.

17. **Aplicativos pré-instalados -> Desativado**
    -   **O que faz:** Impede que o Windows instale aplicativos genéricos pré-selecionados pela Microsoft.

18. **Automaticamente instalar aplicativos sugeridos -> Desativado**
    -   **O que faz:** Bloqueia a instalação automática de aplicativos que a Microsoft "sugere" com base no uso.

19. **Botão da Cortana na Área de Notificação -> Desativado**
    -   **O que faz:** Remove o ícone da Cortana da barra de tarefas.

20. a 28. **(Todas as opções de coleta de dados da Cortana e Digitação)**
    -   **O que fazem:** Desativam coletivamente toda a telemetria relacionada à Cortana e ao seu comportamento de digitação e escrita, impedindo que a Microsoft colete informações sobre contatos, inventário de apps, texto digitado/escrito e histórico de dispositivos.

29. **Exibir entradas de pesquisa recentes na caixa de pesquisa do Explorador de Arquivos -> Desativado**
    -   **O que faz:** Impede que o Explorador de Arquivos salve e exiba seu histórico de pesquisas.

30. **Experiências Compartilhadas -> Desativado**
    -   **O que faz:** Desabilita a função que permite iniciar uma tarefa em um dispositivo e continuar em outro conectado à mesma conta Microsoft.

31. **Frequência do feedback -> Desativado**
    -   **O que faz:** Impede que o Windows solicite feedback sobre a experiência de uso.

32. **Histórico de pesquisas neste dispositivo -> Desativado**
    -   **O que faz:** Impede que o Windows salve o histórico de pesquisas realizadas no Menu Iniciar.

33. **Instalação automática de apps patrocinados (Experiência do Consumidor) -> Desativado**
    -   **O que faz:** Desativa a "Experiência do Consumidor da Microsoft", que é a principal responsável por instalar jogos e aplicativos indesejados (bloatware) após a instalação.

34. **Mostrar arquivos recentemente usados no Acesso Rápido -> Desativado**
    -   **O que faz:** Remove a seção "Arquivos recentes" do Acesso Rápido no Explorador de Arquivos.

35. **Mostrar conteúdo sugerido no aplicativo Configurações -> Desativado**
    -   **O que faz:** Impede que a Microsoft exiba dicas, sugestões ou propagandas dentro do aplicativo de Configurações.

36. **Mostre-me notificações no aplicativo Configurações -> Desativado**
    -   **O que faz:** Bloqueia o envio de notificações com dicas e sugestões do Windows.

37. **Ocasionalmente mostrar sugestões no Menu Iniciar -> Desativado**
    -   **O que faz:** Impede que o Menu Iniciar mostre sugestões de aplicativos da Microsoft Store.

38. a 41. **(Permitir acesso de aplicativos - Chamadas, Histórico, Diagnóstico, Mensagens)**
    -   **O que fazem:** Bloqueiam globalmente o acesso de aplicativos da plataforma UWP (da Store) a essas informações sensíveis.

42. **Permitir Experimentação -> Desativado**
    -   **O que faz:** Impede que a Microsoft teste novos recursos ou alterações em seu sistema sem um aviso prévio, tornando a experiência mais estável.

43. **Permitir o programa de aperfeiçoamento de experiência (driver da NVIDIA) -> Desativado**
    -   **O que faz:** Desativa a coleta de dados (telemetria) do painel de controle da NVIDIA.

44. **Permitir que a Microsoft forneça experiências mais adaptadas... -> Desativado**
    -   **O que faz:** Impede que a Microsoft use seus dados de diagnóstico para personalizar dicas, anúncios e recomendações.

45. **Permitir que aplicativos usem meu ID de publicidade... -> Desativado**
    -   **O que faz:** Impede que aplicativos rastreiem seu uso para exibir anúncios personalizados.

46. **Permitir que o Skype (se instalado) lhe ajude a conectar com amigos... -> Desativado**
    -   **O que faz:** Impede que o Skype acesse sua lista de contatos para sugerir amigos automaticamente.

47. **Permitir que o Windows colete minhas atividades deste PC ('Linha do Tempo') -> Desativado**
    -   **O que faz:** Desativa completamente o recurso "Linha do Tempo", que registra um histórico de aplicativos e documentos que você abriu.

48. **Permitir que o Windows monitore a inicialização de aplicativos para melhorar o Menu Iniciar... -> Desativado**
    -   **O que faz:** Desativa a telemetria que informa à Microsoft quais aplicativos você inicia e com que frequência.

49. **Personalização de fala, digitação e escrita pelo envio dos seus dados... -> Desativado**
    -   **O que faz:** É um interruptor geral de privacidade que desativa o envio de dados de voz, digitação e escrita para os servidores da Microsoft.

50. **Pesquisar - Incluir resultados do Bing -> Desativado**
    -   **O que faz:** Remove os resultados da web (do buscador Bing) da pesquisa do Menu Iniciar, tornando-a uma pesquisa exclusivamente local e mais rápida.

51. **Serviços de reconhecimento de fala on-line -> Desativado**
    -   **O que faz:** Impede que o sistema use os servidores da Microsoft para reconhecimento de voz, desativando funções de ditado online.

52. **Windows Copilot -> Desativado**
    -   **O que faz:** Desativa completamente a integração do assistente de IA Copilot no sistema operacional.

53. **Windows Spotlight (Dicas e sugestões) -> Desativado**
    -   **O que faz:** Desativa as imagens, dicas e sugestões dinâmicas da tela de bloqueio e de outras áreas do Windows.

### **Rastreamento do AutoLogger**

54. **DefenderApiLogger** `(IMPORTANTE: WINDOWS DEFENDER)` -> **Desativado**
    -   **O que faz:** Desativa um log de telemetria específico que registra eventos de chamadas da API do Windows Defender.

55. **DefenderAuditLogger** `(IMPORTANTE: WINDOWS DEFENDER)` -> **Desativado**
    -   **O que faz:** Desativa um log de telemetria específico que registra eventos de auditoria do Windows Defender.

56. **SpoolerLogger** `(IMPORTANTE: IMPRESSÃO)` -> **Desativado**
    -   **O que faz:** Desativa um log de telemetria específico que registra a atividade do serviço de impressão (spooler).

### **Sistema**

57. **Agendamento de GPU acelerado por hardware -> Ativado**
    -   **O que faz:** Permite que a placa de vídeo gerencie sua própria memória diretamente, o que pode reduzir a latência e melhorar o desempenho em jogos e aplicativos gráficos. **Esta opção foi ativada intencionalmente.**

58. **Animação do primeiro logon -> Desativado**
    -   **O que faz:** Remove a tela de boas-vindas animada ("Olá", "Estamos preparando tudo para você...") que aparece ao entrar em uma nova conta de usuário pela primeira vez.

59. **Criptografia automática de dispositivos (BitLocker) -> Desativado**
    -   **O que faz:** Impede que o Windows ative automaticamente a criptografia de disco BitLocker, mesmo em hardware compatível.

60. **Exibir a tela de bloqueio -> Desativado**
    -   **O que faz:** Remove a tela de imagem que aparece antes da tela de login. Ao ligar ou acordar o PC, você será levado diretamente para o campo de senha.

61. **Exigir entrada no Windows Hello para contas da Microsoft -> Desativado**
    -   **O que faz:** Permite que você use uma senha tradicional para contas Microsoft, em vez de forçar a configuração de um PIN ou biometria (Windows Hello).

62. **ReadyBoost -> Desativado**
    -   **O que faz:** Desativa a tecnologia legada que permitia usar um pendrive como cache de disco. É completamente inútil em sistemas com SSDs.

63. **Teclas de aderência (Ferramentas de Acessibilidade) -> Desativado**
    -   **O que faz:** Impede que recursos de acessibilidade como as Teclas de Aderência sejam ativados acidentalmente ao pressionar a tecla Shift repetidamente.

### **Windows Defender** `(IMPORTANTE: WINDOWS DEFENDER)`

64. **Aviso de Proteção de Conta do Defender para usar uma Conta da Microsoft -> Desativado**
    -   **O que faz:** Remove as notificações que insistem para que você vincule uma Conta da Microsoft para melhorar a proteção da conta.

65. **Central de Segurança - Notificação não criticas -> Desativado**
    -   **O que faz:** Desativa notificações informativas e de baixa prioridade do antivírus.

66. **Central de Segurança - Todas as notificações -> Desativado**
    -   **O que faz:** Desativa completamente todas as notificações provenientes da Central de Segurança do Windows Defender.

67. **Proteção contra Adulteração -> Desativado**
    -   **O que faz:** Desativa um recurso de segurança que impede que o próprio Windows Defender e suas configurações sejam alterados por outros programas (ou pelo usuário). É necessário desativar isso para poder remover/desabilitar o Defender.

68. **Windows Defender -> Desativado**
    -   **O que faz:** É a chave principal que desativa a funcionalidade do antivírus Windows Defender.

### **Windows Update**

69. **Atualização automática para os modelos de fala -> Desativado**
    -   **O que faz:** Impede que o Windows Update baixe e instale atualizações para os pacotes de reconhecimento de fala.

70. **Mostrar a experiência de boas-vindas do Windows após atualizações -> Desativado**
    -   **O que faz:** Impede que o Windows mostre uma tela de "tour" com as novidades após a instalação de uma grande atualização de recursos.

### **Área de Trabalho**

71. **Bloqueio dinâmico -> Desativado**
    -   **O que faz:** Desativa o recurso que bloqueia automaticamente o PC quando um dispositivo Bluetooth emparelhado (como um celular) sai do alcance.

72. **Efeitos de animação -> Desativado**
    -   **O que faz:** Remove as animações de janelas (minimizar, maximizar, abrir, fechar) para uma resposta visual mais instantânea e "seca".

73. **Exibir Pessoas na Barra de Tarefas -> Desativado**
    -   **O que faz:** Remove o ícone "Pessoas" da barra de tarefas, um recurso que foi descontinuado pela Microsoft.

74. **Modo escuro para aplicativos -> Ativado**
    -   **O que faz:** Define o tema padrão para os aplicativos compatíveis como escuro.

75. **Modo escuro para Windows -> Ativado**
    -   **O que faz:** Define o tema da interface do próprio Windows (Menu Iniciar, barra de tarefas, Explorador de Arquivos) como escuro.

76. **Notícias e Interesses - Widget da Barra de Tarefas -> Desativado**
    -   **O que faz:** Remove o widget de clima e notícias que fica na barra de tarefas.

77. **Opções do ponteiro - Aprimorar precisão do ponteiro -> Desativado**
    -   **O que faz:** Desativa a aceleração do mouse. Isso resulta em um movimento 1:1 entre o mouse e o cursor, o que é preferido por muitos jogadores para obter maior precisão muscular.

78. **Pesquisar (Barra de Tarefas) -> Desativado**
    -   **O que faz:** Oculta a caixa ou o ícone de pesquisa da barra de tarefas para um visual mais limpo. A pesquisa continua acessível ao abrir o Menu Iniciar e começar a digitar.

79. **Reunir Agora - Widget da Barra de Tarefas -> Desativado**
    -   **O que faz:** Remove o ícone "Reunir Agora" (um atalho para o Skype Meet Now) da área de notificação.

---

## **Configurar -> Serviços (44 Modificações)**

Os seguintes serviços foram revisados e configurados. A lista abaixo detalha a função de cada um e a ação final tomada (desativar ou manter).

1.  **Agent Activation Runtime**
    -   **O que faz:** Um serviço relacionado à ativação de aplicativos da Microsoft Store por voz, principalmente ligado à funcionalidade da Cortana.
    -   **Ação Final:** **DESATIVAR.**

2.  **Agente de Política IPsec**
    -   **O que faz:** Gerencia e aplica políticas de segurança de rede para conexões VPN corporativas que usam o protocolo IPsec. É desnecessário para VPNs de consumidor, como a do Kaspersky.
    -   **Ação Final:** **DESATIVAR.**

3.  **Agrupamento de Rede de Par**
    -   **O que faz:** Habilita um protocolo de rede P2P (ponto a ponto) legado, que era utilizado por recursos como o "Grupo Doméstico" para compartilhamento em rede.
    -   **Ação Final:** **DESATIVAR.**

4.  **Alocador Remote Procedure Call (RPC)**
    -   **O que faz:** É um dos serviços mais fundamentais do Windows. Atua como um gerente de comunicação, permitindo que diferentes programas e partes do sistema operacional conversem entre si.
    -   **Ação Final:** **MANTER (Automático).** Este serviço é **CRÍTICO** para o funcionamento do Windows. Desativá-lo faria o sistema parar de funcionar completamente.

5.  **Arquivos Offline**
    -   **O que faz:** Permite que o usuário acesse cópias locais de arquivos que estão em uma rede corporativa, mesmo quando o computador está desconectado da rede.
    -   **Ação Final:** **DESATIVAR.**

6.  **Backup do Windows**
    -   **O que faz:** O serviço que executa a ferramenta de backup legada do Windows 7, conhecida como "Backup e Restauração".
    -   **Ação Final:** **DESATIVAR.**

7.  **Cartão inteligente**
    -   **O que faz:** Gerencia o acesso e a utilização de leitores de cartão inteligentes (Smart Cards), usados para autenticação de segurança em ambientes corporativos e governamentais.
    -   **Ação Final:** **DESATIVAR.**

8.  **Conexão Fácil do Windows - Registrador de Configuração**
    -   **O que faz:** Serviço legado relacionado à configuração de dispositivos de rede sem fio através do WPS (Wi-Fi Protected Setup).
    -   **Ação Final:** **DESATIVAR.**

9.  **Configuração Automática de WWAN**
    -   **O que faz:** Gerencia modems e placas de banda larga móvel (placas de celular 3G/4G/5G) para conexão à internet.
    -   **Ação Final:** **DESATIVAR.**

10. **Configuração da Área de Trabalho Remota**
    -   **O que faz:** Serviço auxiliar que gerencia as configurações para conexões de Área de Trabalho Remota.
    -   **Ação Final:** **DESATIVAR.**

11. **Dados de Contato**
    -   **O que faz:** Permite que aplicativos (como Email e Calendário) acessem e armazenem informações de contato do aplicativo "Pessoas".
    -   **Ação Final:** **DESATIVAR.**

12. **Experiências do Usuário Conectado e Telemetria**
    -   **O que faz:** Este é o principal serviço responsável por coletar e enviar dados de uso, desempenho e diagnóstico (telemetria) para os servidores da Microsoft.
    -   **Ação Final:** **DESATIVAR.**

13. **Gerenciador de Mapas Baixados**
    -   **O que faz:** Serviço utilizado pelo aplicativo "Mapas" do Windows para baixar e atualizar mapas para uso offline.
    -   **Ação Final:** **DESATIVAR.**

14. **Gerenciador de NFC/SE e Pagamentos**
    -   **O que faz:** Gerencia dispositivos NFC (Near Field Communication) para interações como pagamentos por aproximação e transferência de arquivos.
    -   **Ação Final:** **DESATIVAR.**

15. **Hora da Rede Celular**
    -   **O que faz:** Sincroniza o relógio do sistema utilizando a hora fornecida pela rede de celular (WWAN), em vez da internet.
    -   **Ação Final:** **DESATIVAR.**

16. **Logs e alertas de desempenho**
    -   **O que faz:** Coleta constantemente dados de desempenho do sistema para gerar logs e alertas, uma função mais voltada para administradores de TI.
    -   **Ação Final:** **DESATIVAR.**

17. **Módulos de Criação de Chaves IKE e AuthIP do IPSec**
    -   **O que faz:** Outro serviço de suporte essencial para a negociação de chaves em conexões VPN corporativas do tipo IPsec.
    -   **Ação Final:** **DESATIVAR.**

18. **Política de Remoção de Cartão Inteligente**
    -   **O que faz:** Controla o que acontece quando um usuário remove um cartão inteligente do leitor (por exemplo, bloquear a sessão do Windows).
    -   **Ação Final:** **DESATIVAR.**

19. **PrintWorkflow** `(IMPORTANTE: IMPRESSÃO)`
    -   **O que faz:** Fornece suporte para o fluxo de trabalho de aplicativos de impressão modernos (da Microsoft Store).
    -   **Ação Final:** **DESATIVAR.**

20. **Protocolo PNRP**
    -   **O que faz:** Habilita o Peer Name Resolution Protocol, um protocolo de rede P2P legado para descoberta de outros computadores na rede.
    -   **Ação Final:** **DESATIVAR.**

21. **Serviço AssignedAccessManager**
    -   **O que faz:** Serviço de back-end que gerencia e aplica as políticas do "Modo Kiosk" (Acesso Atribuído).
    -   **Ação Final:** **DESATIVAR.**

22. **Serviço de Criptografia de Unidade de Disco BitLocker**
    -   **O que faz:** É o serviço principal que executa e gerencia a criptografia de disco do BitLocker.
    -   **Ação Final:** **DESATIVAR.**

23. **Serviço de Demonstração de Revenda**
    -   **O que faz:** Utilizado para colocar o computador em um "modo de demonstração" com conteúdo e restrições específicas para exibição em lojas.
    -   **Ação Final:** **DESATIVAR.**

24. **Serviço de Enumeração de Dispositivo de Cartão Inteligente**
    -   **O que faz:** Detecta e prepara (enumera) leitores de cartão inteligente conectados ao sistema para que possam ser usados.
    -   **Ação Final:** **DESATIVAR.**

25. **Serviço de Gerenciamento de Aplicativos Empresariais**
    -   **O que faz:** Permite que empresas gerenciem e implantem aplicativos de forma centralizada em seus dispositivos.
    -   **Ação Final:** **DESATIVAR.**

26. **Serviço de Histórico de Arquivos**
    -   **O que faz:** É o serviço que roda em segundo plano para executar os backups automáticos da funcionalidade "Histórico de Arquivos".
    -   **Ação Final:** **DESATIVAR.**

27. **Serviço de Hotspot Móvel do Windows**
    -   **O que faz:** Permite que o seu computador compartilhe sua conexão de internet com outros dispositivos, funcionando como um roteador Wi-Fi.
    -   **Ação Final:** **DESATIVAR.**

28. **Serviço de Política de Diagnóstico**
    -   **O que faz:** Componente ligado à telemetria que permite a detecção, download e resolução de problemas de componentes do Windows.
    -   **Ação Final:** **DESATIVAR.**

29. **Serviço de Publicação de Nome de Computador do PNRP**
    -   **O que faz:** Publica o nome do computador na rede local usando o protocolo P2P legado PNRP para que outros possam encontrá-lo.
    -   **Ação Final:** **DESATIVAR.**

30. **Serviço de Registro de Gerenciamento de Dispositivos**
    -   **O que faz:** Usado para registrar o dispositivo em um sistema de gerenciamento de dispositivos móveis (MDM) corporativo.
    -   **Ação Final:** **DESATIVAR.**

31. **Serviço de Roteador AllJoyn**
    -   **O que faz:** Gerencia um protocolo de código aberto para a descoberta e comunicação entre dispositivos de "Internet das Coisas" (IoT) na rede.
    -   **Ação Final:** **DESATIVAR.**

32. **Serviço de Roteador SMS do Microsoft Windows**
    -   **O que faz:** Permite que aplicativos leiam mensagens de texto (SMS) recebidas por um modem de banda larga móvel ou celular conectado ao PC.
    -   **Ação Final:** **DESATIVAR.**

33. **Serviço de Telefonia**
    -   **O que faz:** Fornece suporte à API de Telefonia (TAPI), usada por programas legados para controlar dispositivos de telefonia, como modems dial-up.
    -   **Ação Final:** **DESATIVAR.**

34. **Serviço de Usuário do GameDVR e Transmissão**
    -   **O que faz:** Serviço de back-end que gerencia as funcionalidades de gravação de clipes de jogos (Game DVR) e transmissão da Xbox Game Bar.
    -   **Ação Final:** **DESATIVAR.**

35. **Serviço do Participante do Programa Windows Insider**
    -   **O que faz:** Gerencia o download e a instalação de compilações de pré-visualização (beta) do Windows para testadores.
    -   **Ação Final:** **DESATIVAR.**

36. **Serviço Iniciador Microsoft iSCSI**
    -   **O que faz:** Permite que o computador se conecte a sistemas de armazenamento de rede corporativos (SANs) usando o protocolo iSCSI.
    -   **Ação Final:** **DESATIVAR.**

37. **Serviço SSTP**
    -   **O que faz:** Fornece suporte para o Secure Socket Tunneling Protocol, um tipo de protocolo de VPN geralmente usado em ambientes Microsoft.
    -   **Ação Final:** **DESATIVAR.**

38. **Serviços de Área de Trabalho Remota**
    -   **O que faz:** Permite que outros computadores se conectem e controlem o seu PC via Conexão de Área de Trabalho Remota.
    -   **Ação Final:** **DESATIVAR.**

39. **Spooler de Impressão** `(IMPORTANTE: IMPRESSÃO)`
    -   **O que faz:** Gerencia a fila de trabalhos de impressão e a comunicação com as impressoras. Desativá-lo impede a impressão em dispositivos físicos.
    -   **Ação Final:** **DESATIVAR.**

40. **SysMain (Superfetch)**
    -   **O que faz:** Tenta prever quais aplicativos você usará com frequência e os pré-carrega na memória RAM. Em SSDs rápidos, seu benefício é mínimo e pode causar atividade de disco desnecessária.
    -   **Ação Final:** **DESATIVAR.**

41. **System Guard Runtime Monitor Broker** `(IMPORTANTE: WINDOWS DEFENDER)`
    -   **O que faz:** Um serviço de segurança ligado ao Windows Defender que monitora a integridade de componentes críticos do sistema durante a execução.
    -   **Ação Final:** **DESATIVAR.**

42. **Telefonia**
    -   **O que faz:** Versão moderna do serviço TAPI, também ligada a funcionalidades de comunicação por voz que são desnecessárias no contexto atual.
    -   **Ação Final:** **DESATIVAR.**

43. **Uso de Dados**
    -   **O que faz:** Rastreia e registra o uso de dados de rede por aplicativo, exibindo as informações nas Configurações.
    -   **Ação Final:** **DESATIVAR.**

44. **Windows Remote Management (WS-Management)**
    -   **O que faz:** Permite que administradores de sistema executem scripts e gerenciem o computador remotamente, principalmente via PowerShell (WinRM).
    -   **Ação Final:** **DESATIVAR.**

---

## **Configurar -> Serviços Extras (4 Modificações)**

Os seguintes serviços (drivers de baixo nível) foram definidos como **DESATIVADO**:

1.  **Driver de Filtro de Classe PnP de Cartão inteligente**
    -   **O que faz:** Driver de baixo nível que habilita a funcionalidade de cartão inteligente no sistema.
    -   **Ação Final:** **DESATIVAR.**

2.  **Driver TAPI NDIS de acesso remoto**
    -   **O que faz:** Driver legado usado para redes dial-up (acesso discado) através da API de Telefonia (TAPI).
    -   **Ação Final:** **DESATIVAR.**

3.  **Driver WAN NDIS HERDADO de Acesso Remoto**
    -   **O que faz:** Outro driver legado para redes de longa distância (WAN), como conexões dial-up.
    -   **Ação Final:** **DESATIVAR.**

4.  **MBB Network Adapter Class Extension**
    -   **O que faz:** Driver de sistema para adaptadores de rede de banda larga móvel (celular).
    -   **Ação Final:** **DESATIVAR.**

---

## **Aplicar**

-   **Modo de salvamento:** Salvar a imagem e compactar as edições.
-   **Formato da imagem:** Alta compactação, somente leitura (ESD).
