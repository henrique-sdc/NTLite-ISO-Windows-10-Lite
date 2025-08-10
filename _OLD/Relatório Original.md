# NTLite Windows 10 Pro Lite Configs
## Neste documento está a explicação de todas alterações que eu fiz na ISO do Windows 10 através do NTLite, caso você queira reativar algo que precise está tudo explicado aqui e caso você queira desativar mais coisas ainda para deixar mais leve recomendo entrar nesse CHAT que está registrado a função de absolutamente todas as coisas possíveis de se desativar no NTLite, nesse documento apenas deixei a explicação do que eu realmente desativei.
Link: https://aistudio.google.com/u/1/prompts/1rUz_38SC4EP48Ewz_8jv5LHaSki5FF_K

## Iniciar -> Imagem (1 Modificação)
Extrai apenas o Windows 10 Pro da imagem oficial da Microsoft

## Integrar -> Atualizações (10 Modificações)
###**Atualização Cumulativa**

1.  **Cumulative Update Preview (KB5028248)**
    *   **O que faz:** É uma atualização de "prévia" (preview). A Microsoft as lança no final do mês para que administradores de sistema possam testar as correções que virão na atualização oficial e obrigatória do mês seguinte. Elas não contêm atualizações de segurança e podem ter bugs.

2.  **Cumulative Update (KB5028166)**
    *   **O que faz:** Esta é a atualização cumulativa "oficial" e final do mês. Ela contém todas as correções de segurança e de bugs importantes até a data de seu lançamento. É a atualização mais importante da lista.

---

### **.NET Framework**

1.  **KB5026578, KB5026577, KB5011048 (.NET Framework Updates)**
    *   **O que faz:** São atualizações de segurança e qualidade para o .NET Framework, uma plataforma de software da Microsoft. Muitos programas, incluindo partes do Visual Studio, PowerToys e outras ferramentas que você usa, dependem de versões específicas do .NET para funcionar.

---

### **Aplicativos & Recursos**

1.  **KB2267602 & KB4052623 (Microsoft Defender Antivirus updates)**
    *   **O que faz:** Atualiza o motor e a plataforma do Windows Defender.
    *   **NÃO MARQUEI**

2.  **Windows Package Manager (App Installer, WinGet)**
    *   **O que faz:** É o gerenciador de pacotes oficial da Microsoft (como o `apt` do Linux ou `brew` do macOS). Permite instalar programas via linha de comando (ex: `winget install spotify`). É extremamente útil para desenvolvedores.

3.  **Microsoft.UI.Xaml & Microsoft Visual C++ UWP Runtime**
    *   **O que faz:** São bibliotecas de interface e de runtime para aplicativos modernos do Windows (UWP/WinUI). Muitos aplicativos, incluindo partes do próprio sistema como a Ferramenta de Captura (Win+Shift+S) e até mesmo os PowerToys, dependem desses pacotes para renderizar suas janelas e controles.

4.  **Windows Terminal**
    *   **O que faz:** É o novo aplicativo de terminal moderno da Microsoft, que unifica Prompt de Comando, PowerShell e terminais do WSL (Linux) em uma única janela com abas.
    *   **NÃO MARQUEI**

5.  **Windows Subsystem for Linux (WSL)**
    *   **O que faz:** É a atualização para a camada de compatibilidade que permite rodar Linux no Windows.

---

### **Outro**

1.  **Safe OS Dynamic Update & Dynamic Update for Windows setup**
    *   **O que faz:** São pequenas atualizações para o próprio ambiente de instalação e recuperação do Windows (WinRE e Windows Setup). Elas corrigem bugs que podem ocorrer *durante* a formatação do computador, tornando o processo mais confiável.

2.  **Intel Memory Mapped I/O Security Update**
    *   **O que faz:** É uma atualização de segurança de hardware (microcódigo) específica para processadores Intel. Ela corrige vulnerabilidades a nível de CPU.

---

## Integrar -> Registro (5 Modificações) 

1. Tweak_Accessibility_Keys_Flags.reg

```
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

2. Tweak_Disable_GameDVR_Policy.reg

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\default\ApplicationManagement\AllowGameDVR]
"value"=dword:00000000
```

3. Tweak_GlobalTimerResolution.reg

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\kernel]
"GlobalTimerResolutionRequests"=dword:00000001
```

4. Tweak_Graphics_DisablePreemption.reg
```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler]
"EnablePreemption"=dword:00000000
```

5. Tweak_Multimedia_Profile_Games.reg

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games]
"Scheduling Category"="High"
"SFIO Priority"="High"
```

## Integrar -> Pós Instalação (10 Modificações)
### **Antes do Logon**
- fundo.png para \Windows\Web\Wallpaper\Windows\fundo.PNG
- pasta icons para \Windows\Web\icons\

### **Após o Logon**
Comandos CMD:
- powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
- powercfg.exe /hibernate off
- bcdedit /set useplatformtick yes
- bcdedit /set disabledynamictick yes
- bcdedit /deletevalue useplatformclock
- bcdedit /set tscsyncpolicy Enhanced
- reg add "HKCU\Control Panel\Desktop" /v Wallpaper /t REG_SZ /d "C:\Windows\Web\Wallpaper\Windows\fundo.PNG" /f
- RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters

---

## Remover -> Componentes (106 Modificações)

Foram **DESATIVADOS**:

### **Apps do Sistema**
1.  **Aplicativo Bloqueio de Tela de Acesso Atribuído**
    *   **O que faz:** É o recurso de "Modo Kiosk", que permite travar o Windows para rodar um único aplicativo, usado em totens de atendimento ou displays públicos.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Você não tem uso para isso. É um recurso corporativo/comercial específico.

2.  **Caixa de diálogo Adicionar Sugestões de Pasta**
    *   **O que faz:** É a pequena janela que sugere adicionar pastas às suas "Bibliotecas" (Documentos, Imagens, etc.) quando você salva algo em um novo local.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Recurso totalmente secundário e dispensável.

3.  **Chamada**
    *   **O que faz:** É o antigo aplicativo "Discador" do Windows, usado para fazer chamadas por modem.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Completamente obsoleto.

4.  **Controle com os Olhos**
    *   **O que faz:** Recurso de acessibilidade que permite controlar o Windows com os olhos, usando hardware específico.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Se você não usa este tipo de hardware.

5. **Fazer um Teste**
    *   **O que faz:** Um aplicativo para professores criarem e aplicarem provas em um ambiente seguro e travado.

    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Inútil para o seu caso de uso.

6. **Gerenciador de Entrega de Conteúdo**
    *   **O que faz:** É um componente que instala automaticamente aplicativos "sugeridos" (lixo, como Candy Crush) após a instalação do Windows.
    *   **Reinstalável depois?:** Não.
    *   **Recomendação:** **REMOVER.** Este é um dos principais responsáveis por "inchar" uma instalação limpa do Windows com apps indesejados.

7. **Narrador**
    *   **O que faz:** Ferramenta de acessibilidade que lê o texto da tela em voz alta.
    *   **Reinstalável depois?:** Sim, através das Configurações -> Facilidade de Acesso.
    *   **Recomendação:** **REMOVER.** Você não mencionou a necessidade de recursos de acessibilidade.

8. **Recursos da familia Microsoft**
    *   **O que faz:** Controles parentais (Microsoft Family Safety).
    *   **Reinstalável depois?:** Não.
    *   **Recomendação:** **REMOVER.** Você não precisa de controle parental no seu próprio PC.

9. **Tela de Bloqueio padrão do Windows**
    *   **O que faz:** A tela que aparece antes da tela de login, mostrando uma imagem e notificações. Não é a tela de login em si.
    *   **Reinstalável depois?:** Não.
    *   **Recomendação:** **REMOVER.** Remove uma etapa desnecessária ao ligar/desbloquear o PC, levando você direto para a tela de senha. É uma remoção clássica para "enxugar" o Windows.

10. **Visualização de Código de Barras do Windows**
    *   **O que faz:** Um componente para aplicativos que precisam ler códigos de barra.
    *   **Reinstalável depois?:** Não.
    *   **Recomendação:** **REMOVER.** Inútil para o seu perfil.

11. **Windows Defender** **(Importante WINDOWS DEFENDER)**
    *   **O que faz:** O antivírus nativo do Windows.
    *   **Reinstalável depois?:** Não.
    *   **Recomendação:** **REMOVER.**Se você usar um antivírus pago a parte. Isso vai liberar recursos e evitar conflitos.

12. **Xbox Game UI**
    *   **O que faz:** Todos os componentes da Game Bar (gravação de clipes, painel social, etc.).
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** Você disse que não usa. Essa é uma das remoções mais comuns e seguras para liberar recursos, especialmente em jogos.

---

### **Apps**

13.  **Cortana**
    *   **O que faz:** A assistente digital da Microsoft.
    *   **Reinstalável depois?:** Não. A remoção é permanente.
    *   **Recomendação:** **REMOVER.** A Cortana consome recursos e raramente é usada por usuários avançados. A remoção dela é um passo clássico para um Windows mais leve.

14, 15 e 16.  **Dicas (Vamos Começar) / Feedback Hub / Get Help**
    *   **O que fazem:** São três aplicativos separados com um propósito similar: dar dicas sobre o Windows, coletar feedback para a Microsoft e oferecer ajuda.
    *   **Reinstalável depois?:** Sim, podem ser baixados novamente da Microsoft Store se necessário.
    *   **Recomendação:** **REMOVER TODOS.** São aplicativos que você usa uma vez (ou nunca) e que só ocupam espaço.

17.  **Mail and Calendar**
    *   **O que faz:** Os aplicativos nativos de Email e Calendário.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** Você mencionou usar o Teams e aplicativos Office. Provavelmente você usa o Outlook ou acessa e-mails via web, tornando estes apps desnecessários.

18 e 19.  **Microsoft Advertising SDK for XAML / Microsoft Engagement Framework**
    *   **O que fazem:** São kits para desenvolvedores incluírem propagandas e notificações em seus próprios aplicativos.
    *   **Reinstalável depois?:** Não.
    *   **Recomendação:** **REMOVER AMBOS.** São inúteis para um usuário final. Apenas "lixo" de desenvolvedor que não afeta a sua programação.

20.  **Microsoft Pay**
    *   **O que faz:** A carteira digital da Microsoft para pagamentos.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** Você não listou isso como um requisito.

21. **Microsoft People**
    *   **O que faz:** O aplicativo de contatos do Windows, que se integra com Email e Calendário.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** Já que vamos remover o Email e Calendário, este também perde a sua função principal.

22. **Microsoft Solitaire Collection**
    *   **O que faz:** Paciência e outros jogos de carta.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** "Bloatware" clássico.

23. **Microsoft Sticky Notes**
    *   **O que faz:** Aplicativo de notas autoadesivas para a área de trabalho.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** Como programador, você provavelmente tem métodos mais robustos para anotações. É um item dispensável para um sistema leve.

24 e 25. **MSN Weather / Windows Maps**
    *   **O que fazem:** Aplicativos de Clima e Mapas.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER AMBOS.** Você obtém essas informações muito melhor e mais rápido pelo navegador.

26 e 27. **Office / OneNote**
    *   **O que fazem:** Atenção, estes **NÃO** são os aplicativos reais. São apenas "atalhos" ou "hubs" que te incentivam a instalar ou assinar o Microsoft 365.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER AMBOS.** Você instalará o pacote Office verdadeiro (que inclui o Excel) e o OneNote, se precisar, por conta própria. Estes são apenas atalhos inúteis que poluem o Menu Iniciar.

28 e 29. **Paint 3D / Visualizador 3D**
    *   **O que fazem:** Ferramentas de modelagem e visualização 3D básicas.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER AMBOS.** Você usa Blender, que é infinitamente superior. Estes são "bloatware".

30. **Skype**
    *   **O que faz:** Versão do Skype que vem com o Windows.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** Você usa Discord e Teams, tornando o Skype redundante.

31.  **Xbox Game Bar Plugin**
    *   **O que faz:** São pequenos add-ons que outros aplicativos podem usar para adicionar funcionalidades à Xbox Game Bar.
    *   **Reinstalável depois?:** Sim, reinstalando a Game Bar ou aplicativos relacionados.
    *   **Recomendação:** **REMOVER.** Você afirmou que não usa a Game Bar (o overlay que aparece com Win+G). Portanto, os plugins para ela também são desnecessários. A funcionalidade principal de login e o app Xbox não dependem disso.

32.  **Xbox Game Bar**
    *   **O que faz:** Este é o aplicativo principal da Game Bar, o overlay que aparece com Win+G e permite gravar clipes, ver amigos, controlar áudio, etc.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** Baseado na sua afirmação explícita de que não a utiliza. Remover a Game Bar libera os recursos que ela consome (memória e processos em segundo plano), mas **não** remove o App Xbox ou a capacidade de fazer login, que são os recursos que você precisa.

33.  **Xbox Game Speech Window**
    *   **O que faz:** Gerencia as funcionalidades de chat de voz (party chat) do ecossistema Xbox.
    *   **Reinstalável depois?:** Sim, mas com dificuldade.
    *   **Recomendação:** **REMOVER** Pode ser que em algum momento queira usar o chat de grupo (party) nativo do Xbox para jogar com amigos que estão no console. Como você está mantendo o ecossistema Xbox funcional, remover isso pode quebrar o chat de voz de forma inesperada. É mais seguro manter.

34. **Your Phone (Seu Telefone)**
    *   **O que faz:** Aplicativo para integrar seu celular Android ou iOS com o Windows.
    *   **Reinstalável depois?:** Sim, pela Microsoft Store.
    *   **Recomendação:** **REMOVER.** Você não pediu por essa funcionalidade, e ela pode ser pesada, rodando vários serviços em segundo plano.

---

### **Comunicação Remota e Privacidade**

35.  **Assistência Remota**
    *   **O que faz:** Permite que um amigo ou técnico de suporte se conecte ao seu computador (com sua permissão) para ajudá-lo a resolver um problema. É um recurso de suporte técnico.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Você é um usuário avançado e provavelmente usaria ferramentas como Discord, TeamViewer ou Anydesk se precisasse de ajuda remota. Este é um recurso legado e dispensável.

36.  **Cliente BranchCache**
    *   **O que faz:** Recurso puramente corporativo que acelera o acesso a arquivos em redes de grandes empresas, criando um cache local de documentos que estão em um servidor central.
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** Completamente inútil fora de um ambiente de rede corporativa.

37.  **Cliente de Pastas de Trabalho**
    *   **O que faz:** Outro recurso corporativo que permite sincronizar arquivos entre seu PC e os servidores de arquivos da sua empresa. É como um OneDrive para redes corporativas.
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** Você usa o OneDrive, que é o equivalente para nuvem pessoal/pública. Este recurso é desnecessário.

38.  **Conector Multiponto**
    *   **O que faz:** Permite que um PC se conecte a um "Windows MultiPoint Server", um tipo especial de servidor que permite que vários usuários usem um único computador simultaneamente, cada um com seu próprio monitor, teclado e mouse.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** É para um cenário de sala de aula ou laboratório muito específico que você não utiliza.

39.  **Grupo Doméstico**
    *   **O que faz:** Era um recurso para simplificar o compartilhamento de arquivos e impressoras em uma rede doméstica. A Microsoft descontinuou e removeu oficialmente essa funcionalidade nas versões mais recentes do Windows 10, embora alguns componentes ainda existam.
    *   **Reinstalável depois?:** Não, e não seria desejável.
    *   **Recomendação:** **REMOVER.** É lixo legado. O compartilhamento de arquivos moderno não depende mais disso.

40.  **Gerenciador de Recursos do Servidor de Arquivos**
    *   **O que faz:** Ferramenta para administradores de TI gerenciarem servidores de arquivos, como definir cotas de armazenamento por usuário ou bloquear certos tipos de arquivos de serem salvos.
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** É uma ferramenta de gerenciamento de servidor, não tem utilidade em um PC cliente/notebook.

41.  **Microsoft Message Queue (MSMQ)**
    *   **O que faz:** É um serviço de enfileiramento de mensagens. Uma tecnologia mais antiga usada por alguns aplicativos (geralmente corporativos) para se comunicarem de forma confiável, mesmo que um deles esteja offline temporariamente.
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** Nenhum dos softwares modernos que você listou (Docker, VS Code, jogos, etc.) depende disso.

42.  **Internet Information Server (IIS)**
    *   **O que faz:** É o servidor web da Microsoft, usado para hospedar sites (principalmente sites feitos em ASP.NET).
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** Como você desenvolve com Node.js, Python, Docker, etc., você não usa o ecossistema de hospedagem da Microsoft. Se um dia precisar, pode instalar depois. É um componente grande e complexo que deve ser removido.

43.  **Protocolo de Gerenciamento de Rede Simples (SNMP)**
    *   **O que faz:** Um protocolo antigo usado para monitorar dispositivos de rede (roteadores, switches, servidores).
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** Outro recurso de gerenciamento de rede corporativa que é inútil para você.

44. **Redirecionador de Portas dos Serviços da Área de Trabalho Remota**
    *   **O que faz:** Componente usado em cenários complexos de Área de Trabalho Remota (VDI), geralmente envolvendo um Servidor Gateway de Área de Trabalho Remota para redirecionar conexões.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Isso não afeta a conexão padrão de Área de Trabalho Remota de um PC para outro. É para infraestruturas empresariais.

---

### **Multimídia**

45.  **Visualizador de Fotos / Visualizador de Fotos - 32 bits**
    *   **O que faz:** Este é o clássico, leve e rápido "Visualizador de Fotos do Windows" que existia no Windows 7. Não é o aplicativo moderno "Fotos" (que você já removeu).
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **MANTER.** Como você removeu o app "Microsoft Photos", você precisará de um programa para abrir imagens. Este visualizador é a melhor opção nativa: é extremamente leve e rápido, perfeito para uma ISO enxuta.

46.  **Serviço de Compartilhamento de Rede WMP - 32 bits**
    *   **O que faz:** É o serviço que permite compartilhar sua biblioteca de mídia do PC com outros dispositivos na rede (TVs, videogames) usando o protocolo DLNA.
    *   **Reinstalável depois?:** Não, está atrelado ao Windows Media Player.
    *   **Recomendação:** **REMOVER** Você não mencionou a necessidade de fazer streaming de mídia para outros aparelhos. Este serviço roda em segundo plano e pode ser removido com segurança.

47.  **Windows Media Player - 32 bits**
    *   **O que faz:** É o aplicativo reprodutor de mídia clássico, o "Windows Media Player".
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER** Se você usa Spotify e provavelmente usa seu navegador ou outro player para vídeos. O aplicativo em si é desnecessário. É importante notar que estamos removendo apenas a interface (o programa), não os codecs e frameworks (que mantivemos acima), garantindo a compatibilidade.

48.  **Ferramenta de Avaliação de Sistema do Windows (WinSAT)**
    *   **O que faz:** É a ferramenta que gera o antigo "Índice de Experiência do Windows", fazendo um benchmark do seu hardware.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Recurso totalmente legado e inútil hoje em dia. Nenhum dos seus softwares ou jogos modernos depende disso.

49.  **Painel de Controle - Compartilhar Mídia**
    *   **O que faz:** O ícone e a janela no Painel de Controle para configurar o "Serviço de Compartilhamento de Rede WMP".
    *   **Reinstalável depois?:** Não.
    *   **Recomendação:** **REMOVER.** Já que removemos o serviço, a interface para configurá-lo também se torna inútil.

50 e 51.  **Tela de Fundo da Área de Trabalho (Padrão) / Telas de Fundo da Área de Trabalho (Temas)**
    *   **O que faz:** São apenas os arquivos de imagem (.jpg) dos papéis de parede padrão que vêm com o Windows.
    *   **Reinstalável depois?:** Não, mas você usará suas próprias imagens de qualquer forma.
    *   **Recomendação:** **REMOVER AMBOS.** Isso economiza alguns megabytes e remove imagens que você provavelmente nunca usará. A remoção dos arquivos não afeta sua capacidade de definir um papel de parede personalizado.

---

### **Rede**

52.  **Data Center Bridging (DCB)**
    *   **O que faz:** Uma coleção de padrões de rede usados em ambientes de data center para gerenciar o tráfego em redes Ethernet de alta velocidade.
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** Tecnologia de servidor, completamente inútil para seu notebook.

53.  **Internet Explorer - 32 bits**
    *   **O que faz:** O navegador legado da Microsoft.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER** Este é um dos maiores componentes legados que podem ser removidos com segurança. Você usa Chrome e outros navegadores modernos. A remoção melhora a segurança e libera um espaço considerável.

54.  **Active Directory Lightweight Directory Services (AD LDS)**
    *   **O que faz:** Uma versão "leve" do Active Directory para cenários de desenvolvimento específicos, permitindo que aplicativos usem um serviço de diretório sem um domínio completo.
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** Não tem utilidade para o seu fluxo de trabalho de desenvolvimento (Node, Java, Python, Docker).

55.  **Serviço Wallet**
    *   **O que faz:** É o serviço de back-end para a funcionalidade de "Carteira" do Windows, como o Microsoft Pay.
    *   **Reinstalável depois?:** Não, está atrelado ao app Microsoft Pay que você já removeu.
    *   **Recomendação:** **REMOVER.** Você não usa o Microsoft Pay.

56. **Serviço de Acesso Remoto e Roteamento**
    *   **O que faz:** Permite que o seu computador funcione como um servidor de acesso remoto (por exemplo, para outras máquinas se conectarem a ele via VPN) ou como um roteador de rede.
    *   **Reinstalável depois?:** Sim, através do painel de serviços.
    *   **Recomendação:** **REMOVER.** Você usa um cliente VPN (Kaspersky), você não precisa hospedar um servidor VPN em seu notebook.

57. **Serviço de Autenticação da Internet (IAS)**
    *   **O que faz:** Componente de servidor (RADIUS) para autenticar usuários que se conectam a uma rede.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Tecnologia de servidor, inútil em um cliente.

---

### **Sistema**

58.  **Windows To Go**
    *   **O que faz:** Um recurso corporativo, já descontinuado pela Microsoft, que permitia criar uma versão portátil do Windows em um pendrive certificado.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Tecnologia legada e de nicho que não tem utilidade para você.

59.  **Bloqueio de Dispositivo (Experiência Incorporada)**
    *   **O que faz:** Funções para sistemas "embarcados", como quiosques ou caixas eletrônicos, para impedir que os usuários modifiquem o sistema.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Recurso industrial que não tem nenhuma aplicação no seu notebook.

60.  **Temas de Facilidade de Acesso**
    *   **O que faz:** Os temas de alto contraste para usuários com dificuldades de visão.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Você não solicitou recursos de acessibilidade. É seguro remover.

61.  **Conteúdo de ajuda do Windows**
    *   **O que faz:** São os próprios arquivos de ajuda (`.chm`) do Windows.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Mantemos o *motor* para abrir os arquivos (acima), mas removemos o *conteúdo* de ajuda do Windows, que você nunca usará.

62. **Tablet PC**
    *   **O que faz:** Adiciona suporte completo para canetas (pen input), reconhecimento de escrita, teclado virtual avançado e outras funções de tablet.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Seu MSI Katana é um notebook tradicional, não um 2-em-1. Remover este conjunto de recursos é uma das melhores maneiras de "enxugar" o sistema, pois ele carrega muitos serviços e componentes desnecessários para você.

63. **Gerenciador de Rotação Automática**
    *   **O que faz:** O serviço que gira a tela automaticamente em dispositivos conversíveis.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Diretamente ligado ao "Tablet PC". Inútil no seu notebook.

64. **Virtualização de Aplicativos (App-V)**
    *   **O que faz:** Tecnologia corporativa para fazer streaming de aplicativos para os usuários. Não tem relação com Hyper-V ou VirtualBox.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Recurso de nicho corporativo, pode ser removido com segurança.

65. **Virtualização de Experiência do Usuário (UE-V)**
    *   **O que faz:** Outra tecnologia corporativa para sincronizar as configurações do usuário e dos aplicativos entre diferentes máquinas em uma empresa.
    *   **Reinstalável depois?:** Não, a remoção é permanente.
    *   **Recomendação:** **REMOVER.** Recurso corporativo que você não precisa.

---

### **Suporte de hardware**

66.  **Impressão -> Cliente de Impressão via Internet**
    *   **O que faz:** Permite que seu PC se conecte a impressoras na internet usando o Internet Printing Protocol (IPP). É para um cenário de impressão remota bem específico.
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER.** Você afirmou que não usa impressora. Este componente é desnecessário.

67.  **Scanner / Fax**
    *   **O que fazem:** São os aplicativos "Windows Fax and Scan".
    *   **Remover?:** Sim, ambos.
    *   **Reinstalável depois?:** Sim, através do painel "Ativar ou desativar recursos do Windows".
    *   **Recomendação:** **REMOVER AMBOS.** São aplicativos legados e inúteis para você. É importante entender que estamos removendo o *aplicativo*, mas mantendo o *driver* (WIA), o que garante que o Photoshop continue funcionando, mas sem o lixo de aplicativos que você não usa.

---

### **Tradução**

Idioma:
68. Alemão
69. Amárico
70. Arábico
71. Búlgaro
72. Chinês Simplificado
73. Chinês Tradicional
74. Coreano
75. Croata
76. Dinamarquês
77. Editor do Método de Entrada (IME)
78. EJ Chinês Tradicional (IME)
79. E Coreano (IME)
80. LJ Japonês (IME)
81. Eslovaco
82. Esloveno
83. Estoniano
84. Finlandês
85. Francês (Canadense)
86. Francês
87. Grego
88. Hebraico
89. Holandês
90. Húngaro
91. Italiano
92. Japonês
93. Letão
94. Lituano
95. Norueguês
96. Polonês
97. Russo
98. Sueco
99. Tailandês
100. Tamil
101. Tcheco
102. Turco
103. Ucraniano

(Línguas Mantidas: Espanhol, Inglês (GB), Inglês (US), Português Brasil, Português e Pseudo-locale.)

--- 

## Configurar -> Recursos (12 Modificações)
Recursos que **DESATIVEI**:
### **Recursos sob Demanda (Capacitações)**

1.  **Exchange ActiveSync and Internet Mail Sync engine**
    *   **O que faz:** Motor de sincronização para contas de email corporativas (Exchange) e outras contas de internet (IMAP/POP3).
    *   **Recomendação:** **DESATIVAR.** Você removeu o aplicativo "Mail and Calendar". Este motor é o back-end para ele e é desnecessário para o seu uso com Teams e OneDrive.

2.  **Microsoft Quick Assist (App)**
    *   **O que faz:** Ferramenta de assistência remota da Microsoft.
    *   **Recomendação:** **DESATIVAR.** Você já removeu a "Assistência Remota" mais antiga. Esta é a versão mais nova, mas igualmente desnecessária, já que você é um usuário avançado.

3. **Portuguese (Brazil) speech recognition**
    *   **O que faz:** Reconhecimento de fala em português, usado para ditado e comandos de voz.
    *   **Recomendação:** **DESATIVAR.** Ligado à Cortana e a outras funções de acessibilidade que você não precisa.

4. **Portuguese (Brazil) text-to-speech**
    *   **O que faz:** A voz em português para funcionalidades de leitura de texto em voz alta.
    *   **Recomendação:** **DESATIVAR.** Ligado ao Narrador, que você removeu.

5. **Print Management**
    *   **O que faz:** O console de gerenciamento de impressão para administradores.
    *   **Recomendação:** **DESATIVAR.** Você não usa impressora.

6. **Steps Recorder**
    *   **O que faz:** Gravador de Passos, uma ferramenta para documentar ações para solução de problemas.
    *   **Recomendação:** **DESATIVAR.** Inútil para um usuário avançado.

7. **Windows Fax and Scan**
    *   **O que faz:** O aplicativo de Fax e Scanner.
    *   **Recomendação:** **DESATIVAR.** Consistente com a sua decisão anterior de remover os componentes de Fax e Scanner.

8. **Windows Media Player Legacy (App)**
    *   **O que faz:** O aplicativo clássico do Windows Media Player.
    *   **Recomendação:** **DESATIVAR.** Consistente com sua decisão de remover o componente principal do WMP.

9. **Windows PowerShell Integrated Scripting Environment (ISE)**
    *   **O que faz:** Um editor gráfico para escrever e depurar scripts PowerShell.
    *   **Recomendação:** **DESATIVAR.** Você é um usuário pesado do **Visual Studio Code**, que tem um terminal integrado e suporte a extensões de PowerShell muito superiores ao antigo ISE. Manter o ISE é redundante para você.

10.  **Microsoft XPS Document Writer**
    *   **O que faz:** A impressora virtual para criar arquivos no formato .XPS, um concorrente do PDF que foi abandonado pela Microsoft.
    *   **Recomendação:** **DESATIVAR.** Completamente inútil. Você já tem o "Imprimir para PDF" que é o padrão universal.

11.  **SMB Direct**
    *   **O que faz:** Um recurso para aceleração de transferência de arquivos em redes de altíssima velocidade (típicas de data centers) que usam hardware específico (RDMA).
    *   **Recomendação:** **DESATIVAR.** Não tem nenhuma aplicação para o seu notebook. É um recurso de servidor/data center.

12.  **Windows PowerShell 2.0**
    *   **O que faz:** Uma versão antiga e legada do PowerShell. O Windows hoje usa uma versão muito mais moderna e segura (5.1+).
    *   **Recomendação:** **DESATIVAR.** É considerado um risco de segurança e é desnecessário para o seu ambiente de desenvolvimento moderno, que já usa o VS Code e o Windows Terminal com a versão atual do PowerShell.

**ATIVE SE QUISER:**
Hyper-V
Virtual Machine Platform
Windows Hypervisor Platform
Windows Sandbox
Windows Subsystem for Linux
Windows TIFF IFilter

---

## Configurar -> Configurações (79 Modificações)

### **Controle de Energia**
1. Inicialização Rápida -> Desativado
2. Menu de Desligamento - Hibernar -> Desativado

### **Controle de travamento**
3. Salvar informações de depuração -> Despejo de memória pequeno (256 KB)

### **Explorer**
4. Abrir Explorador de Arquivos para -> Este PC
5. Exibir informações de tamanho do arquivo nas dicas de pasta -> Ativado
6. Exibição - Mostrar arquivos, pastas e unidades ocultas ->Ativado
7. Exibição - Mostrar extensões dos tipos de arquivos conhecidos -> Ativado
8. Exibição - Mostrar unidades vazias -> Ativado
9. Limpar histórico de documentos recentes ao sair -> Ativado
10. Manter histórico de documentos abertos recentemente -> Desativado
11. Mostrar botão Visualizar Tarefa -> Desativado
12. Reprodução Automática -> Desativado
13. Sempre exibir mais detalhes no diálogo de cópia de arquivo -> Ativado
14. Substituir o Prompt de Comando pelo Windows PowerShell no menu de atalho do botão iniciar -> Desativado

### **Menu Iniciar**
15. Lista de aplicativos - Aplicativos adicionados recentemente -> Desativado

### **Privacidade** 
16. Aplicativos OEM pré-instalados -> Desativado
17. Aplicativos pré-instalados -> Desativado
18. Automaticamente instalar aplicativos sugeridos -> Desativado
19. Botão da Cortana na Área de Notificação -> Desativado
20. Coletar contatos para permitir que o Windows e a Cortana lhe entendam melhor -> Desativado
21. Coletar o inventário de aplicativos -> Desativado
22. Coletar o texto digitado para permitir que o Windows e a Cortana lhe entendam melhor -> Desativado
23. Coletar o texto escrito (ink) para permitir que o Windows e a Cortana lhe entendam melhor -> Desativado
24. Conhecimentos de digitação -> Desativado
25. Cortana -> Desativado
26. Cortana - Recomendações de atividade ao alternar dispositivos -> Desativado
27. Cortana - Usar meu histórico de dispositivos conectados -> Desativado
28. Enviar informações à Microsoft de como escrevo para ajudar a aprimorar a digitação e escrita no futuro -> Desativado
29. Exibir entradas de pesquisa recentes na caixa de pesquisa do Ex plorador de Arquivos -> Desativado
30. Experiências Compartilhadas -> Desativado
31. Frequência do feedback -> Desativado
32. Histórico de pesquisas neste dispositivo -> Desativado
33. Instalação automática de apps patrocinados (Experiência do Consumidor) -> Desativado
34. Mostrar arquivos recentemente usados no Acesso Rápido -> Desativado
35. Mostrar conteúdo sugerido no aplicativo Configurações -> Desativado
36. Mostre-me notificações no aplicativo Configurações -> Desativado
37. Ocasionalmente mostrar sugestões no Menu Iniciar -> Desativado
38. Permitir acesso de aplicativos - Chamadas do telefone -> Desativado
39. Permitir acesso de aplicativos - Histórico de chamadas -> Desativado
40. Permitir acesso de aplicativos - Informações de diagnóstico -> Desativado
41. Permitir acesso de aplicativos - Mensagens (texto ou MMS) -> Desativado
42. Permitir Experimentação -> Desativado
43. Permitir o programa de aperfeiçoamento de experiência (driver da NVIDIA) -> Desativado
44. Permitir que a Microsoft forneça experiências mais adaptadas com dicas relevantes e recomendações usando seus dados de diagnóstico -> Desativado
45. Permitir que aplicativos usem meu ID de publicidade para experiências entre aplicativos -> Desativado
46. Permitir que o Skype (se instalado) lhe ajude a conectar com amigos do seu catálogo de endereços e verifique seu número de telefone móvel -> Desativado
47. Permitir que o Windows colete minhas atividades deste PC ('Linha do Tempo') -> Desativado
48. Permitir que o Windows monitore a inicialização de aplicativos para melhorar o Menu Iniciar e os resultados da pesquisa -> Desativado
49. Personalização de fala, digitação e escrita pelo envio dos seus dados de entrada para a Microsoft -> Desativado
50. Pesquisar - Incluir resultados do Bing -> Desativado
51. Serviços de reconhecimento de fala on-line -> Desativado
52. Windows Copilot -> Desativado
53. Windows Spotlight (Dicas e sugestões) -> Desativado

### **Rastreamento do AutoLogger**

54. DefenderApiLogger **(WINDOS DEFENDER)** -> Desativado
55. DefenderAuditLogger **(WINDOS DEFENDER)** -> Desativado
56. SpoolerLogger -> Desativado

### **Sistema**

57. Agendamento de GPU acelerado por hardware -> Ativado
58. Animação do primeiro logon -> Desativado
59. Criptografia automática de dispositivos (BitLocker) -> Desativado
60. Exibir a tela de bloqueio -> Desativado
61. Exigir entrada no Windows Hello para contas da Microsoft -> Desativado
62. ReadyBoost -> Desativado
63. Teclas de aderência (Ferramentas de Acessibilidade) -> Desativado

### **Windows Defender**

64. Aviso de Proteção de Conta do Defender para usar uma Conta da Microsoft -> Desativado
65. Central de Segurança - Notificação não cnticas -> Desativado
66. Central de Segurança - Todas as notificações -> Desativado
67. Proteção contra Adulteração -> Desativado
68. Windows Defender -> Desativado

### **Windows Update**

69. Atualização automática para os modelos de fala -> Desativado
70. Mostrar a experiência de boas-vindas do Windows após atualizações -> Desativado

### **Área de Trabalho**

71. Bloqueio dinâmico -> Desativado
72. Efeitos de animação -> Desativado
73. Exibir Pessoas na Barra de Tarefas -> Desativado
74. Modo escuro para aplicativos -> Ativado
75. Modo escuro para Windows -> Ativado
76. Notícias e Interesses - Wldget da Barra de Tarefas -> Desativado
77. Opções do ponteiro - Aprimorar precisão do ponteiro -> Desativado
78. Pesquisar (Barra de Tarefas) -> Desativado
79. Reunir Agora - Widget da Barra de Tarefas -> Desativado

---

## Configurar -> Serviços (44 Modificações)

Tudo o que eu DESATIVEI:

1.  **Agent Activation Runtime**
    *   **O que faz:** Serviço relacionado à ativação de aplicativos da Store por voz (Cortana).
    *   **Recomendação:** **DESATIVAR.** Ligado à Cortana, que você removeu.

2.  **Agente de Política IPsec**
    *   **O que faz:** Implementa políticas de segurança IPsec, usadas em conexões de VPN corporativas.
    *   **Recomendação:** **DESATIVAR.** Você usa o Kaspersky VPN, que tem seu próprio mecanismo. Este serviço é para um tipo específico de VPN que você não utiliza.

3. **Agrupamento de Rede de Par**
    *   **O que faz:** Protocolo de rede P2P legado.
    *   **Recomendação:** **DESATIVAR.** Obsoleto e não utilizado pelos seus programas.

4. **Alocador Remote Procedure Call (RPC)**
    *   **O que faz:** Um dos serviços mais fundamentais do Windows. Gerencia as chamadas de procedimento remoto, que é como muitos componentes e programas se comunicam.
    *   **Recomendação:** **MANTER (Automático).** **CRÍTICO.** Desativar isso faria o Windows parar de funcionar.

5. **Arquivos Offline**
    *   **O que faz:** Permite que você use arquivos de rede mesmo estando desconectado. Recurso corporativo.
    *   **Recomendação:** **DESATIVAR.** Você usa OneDrive para funcionalidade similar na nuvem.

6. **Backup do Windows**
    *   **O que faz:** O serviço legado de backup do Windows.
    *   **Recomendação:** **DESATIVAR.** Você usa OneDrive e provavelmente fará backups mais robustos de outras formas.

7. **Cartão inteligente:** **DESATIVAR.** Para leitores de cartão de segurança que você não possui.

8. **Conexão Fácil do Windows - Registrador de Configuração:** **DESATIVAR.** Legado.

9. **Configuração Automática de WWAN:** **DESATIVAR.** Para modems de internet móvel (celular) que você não tem.

10. **Configuração da Área de Trabalho Remota:** **DESATIVAR.** O serviço para *receber* conexões. Você só fará conexões de saída.

11.  **Dados de Contato**
    *   **O que faz:** Permite que aplicativos acessem e armazenem informações de contato.
    *   **Recomendação:** **DESATIVAR.** Ligado aos apps de Contato/Email que você removeu e à sua política de privacidade.

12. **Experiências do Usuário Conectado e Telemetria:** O principal serviço de telemetria da Microsoft. **DESATIVAR.** Este é o alvo número um para a sua política de privacidade.

13. **Gerenciador de Mapas Baixados:** Para o app Mapas. **DESATIVAR.**

14. **Gerenciador de NFC/SE e Pagamentos:** Para pagamentos por proximidade. **DESATIVAR.**

15.  **Hora da Rede Celular:** Sincroniza o relógio via rede celular. **DESATIVAR.** Você não tem um modem WWAN.

16. **Logs e alertas de desempenho:** Coleta dados de desempenho. **DESATIVAR.** A coleta é constante e desnecessária para o usuário final, que pode usar ferramentas ativas como o HWMonitor.

17.  **Módulos de Criação de Chaves IKE e AuthIP do IPSec:** Usado por algumas VPNs corporativas. **DESATIVAR.** O Kaspersky VPN não precisa disso.

18.  **Política de Remoção de Cartão Inteligente:** **DESATIVAR.** Você não usa cartão inteligente.

19. **PrintWorkflow:** Serviço para apps de impressão modernos. **DESATIVAR.** Você não usa impressora.

20. **Protocolo PNRP:** Protocolo P2P legado. **DESATIVAR.**

21. **Serviço AssignedAccessManager:** Para Modo Kiosk. **DESATIVAR.**

22.  **Serviço de Criptografia de Unidade de Disco BitLocker:** O serviço principal do BitLocker. **DESATIVAR.** Consistente com sua decisão de remover o recurso.

23. **Serviço de Demonstração de Revenda:** Para modo de demonstração em lojas. **DESATIVAR.**

24. **Serviço de Enumeração de Dispositivo de Cartão Inteligente:** **DESATIVAR.**

25. **Serviço de Gerenciamento de Aplicativos Empresariais:** Para gerenciamento de apps em empresas. **DESATIVAR.**

26. **Serviço de Histórico de Arquivos:** O serviço de backup do Histórico de Arquivos. **DESATIVAR.**

27. **Serviço de Hotspot Móvel do Windows:** Permite compartilhar sua internet via Wi-Fi. **DESATIVAR.** Se precisar, pode ser ativado depois.

28.  **Serviço de Política de Diagnóstico:** Permite a detecção, download e resolução de problemas de componentes do Windows. **DESATIVAR.** Ligado à telemetria.

29.  **Serviço de Publicação de Nome de Computador do PNRP:** Serviço legado de rede P2P. **DESATIVAR.**

30. **Serviço de Registro de Gerenciamento de Dispositivos:** Usado em cenários de gerenciamento corporativo. **DESATIVAR.**

31. **Serviço de Roteador AllJoyn:** Protocolo de descoberta de dispositivos IoT. **DESATIVAR.**

32. **Serviço de Roteador SMS do Microsoft Windows:** Para mensagens de texto. **DESATIVAR.**

33. **Serviço de Telefonia:** Fornece suporte à API de Telefonia (TAPI). **DESATIVAR.** Legado e desnecessário.

34. **Serviço de Usuário do GameDVR e Transmissão:** Serviço de back-end para a Game Bar. **DESATIVAR.** Você removeu a Game Bar.

35.  **Serviço do Participante do Programa Windows Insider:** Para receber versões beta do Windows. **DESATIVAR.** Você quer um sistema estável.

36.  **Serviço Iniciador Microsoft iSCSI:** Para conectar a sistemas de armazenamento de rede corporativos. **DESATIVAR.**

37.  **Serviço SSTP:** Um tipo de protocolo VPN. **DESATIVAR.** O Kaspersky VPN usa o seu próprio.

38. **Serviços de Área de Trabalho Remota:** O serviço para *receber* conexões. **DESATIVAR.** Boa prática de segurança.

39. **Spooler de Impressão:** Gerencia a fila de impressão. **DESATIVAR.** Você não usa impressora. O "Imprimir para PDF" não depende deste serviço estar sempre ativo.

40. **SysMain (Superfetch):** Pré-carrega aplicativos na RAM. **DESATIVAR.** Com seu SSD NVMe Gen4, este serviço é desnecessário e pode causar atividade de disco indesejada.

41. **System Guard Runtime Monitor Broker:** Segurança do Defender. **DESATIVAR.**

42. **Telefonia:** Legado. **DESATIVAR.**

43. **Uso de Dados:** Rastreia o uso de dados da rede. **DESATIVAR.** Privacidade.

44. **Windows Remote Management (WS-Management):** Para gerenciamento remoto. **DESATIVAR.**

## Configurar -> Serviços Extras (4 Modificações)

Tudo o que eu DESATIVEI:

1. **Driver de Filtro de Classe PnP de Cartão inteligente:** **DESATIVAR.**

2 e 3. **Driver TAPI NDIS de acesso remoto / Driver WAN NDIS HERDADO...:** Legados. **DESATIVAR (AMBOS).**

4. MBB Network Adapter Class Extension:** Para modems de celular. **DESATIVAR**

## Aplicar

Modo de salvamento -> Salvar a imagem e compactar as edições

Formato da imagem -> Alta compactação, somente leitura (ESD)