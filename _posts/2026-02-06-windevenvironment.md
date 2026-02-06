---
title:  "Configuração do meu Windows voltado para o desenvolvimento DotNET/C#"
subtitle:
---

## Sumário
0. [Prefácio](#prefácio)
1. [Introdução: Configurações básicas](#introdução-configurações-básicas)
2. [Containers: WSL e Windows SandBox](#containers-wsl-e-windows-sandbox)
3. [Instalando a versão mais recente do PowerShell](#instalando-a-versão-mais-recente-do-powershell)
4. [Configurando o Windows Terminal](#configurando-o-windows-terminal)
5. [Fontes](#fontes)
6. [StarShip](#starship)
7. [NeoVim](#neovim)

## Prefácio
Últimamente usar o **Windows 11** têm-se tornado uma tarefa desafiadora para alguns quando se trata de _otimização_, _estabilidade_ e _segurança_.

De maneira definitiva, permaneci no **Windows** mesmo depois de ter passado os últimos 5 anos usando **Linux** como sistema operacional principal.

O porque de eu me manter no **Windows** foi quando comecei a ter o seguinte pensamento: _Não faz o menor sentido passar horas configurando um ambiente Linux e ainda ter certa falta de suporte em certos softwares/games (sem generalização, amo **Linux**)._ Além de me ocorrer problemas de desempenho e suporte relacionado a minha **GPU**.

Então, aqui, compartilho minha configuração do meu ambiente de desenvolvimento **DotNET**/**C#** com base **NeoVim**, **PowerShell 7** + **Windows Terminal** + **StarShip**.

## Introdução: Configurações básicas
Para um melhor suporte a softwares de terceiros, sem assinaturas (ou até seus softwares) e execução de scripts **PowerShell**, ative o modo desenvolvedor que pode ser encontrado em:

```Settings -> System -> Advanced -> Developer Mode```

Também defina o **Windows Terminal** como aplicativo de terminal padrão. Essa opção pode ser localizada na mesma seção do modo desenvolvedor.

Por questões práticas, recomendo ativar o '**sudo**' também (vai ajudar bastante, você não vai precisar reabrir um terminal como adminstrador).

## Containers: WSL e Windows SandBox
Este passo é opcional, mas caso queira ter um sistema linux dentro do seu windows, ative em:

```Settings -> System -> Optional features -> More Windows Features```

Ative a opção **Windows Subsystem for Linux** e **Windows Sandbox** (ambiente isolado, uso para testar softwares).

Após isso reinicie seu computador e entre até o repositório do GitHub:
[WSL](https://github.com/microsoft/WSL/releases)

Baixe e instale a versão mais recente (isso vai instalar a última versão do WSL).

Para listar as distros disponíveis para instalar, rode o seguinte comando:
```powershell
wsl --list -o
```
Em seguida instale o sistema de sua preferência com:
```powershell
wsl --install <nome>
```

## Instalando a versão mais recente do PowerShell
As versões que estão pré-instaladas no windows são versões antigas (5.1) e com certos problemas de desempenho (além de não possuir um autocomplete que preste kk).

Para resolver este problema, abra o seu windows terminal e digite:
```powershell
winget install Microsoft.PowerShell
```

## Configurando o Windows Terminal
Se por acaso o windows terminal não existir na sua máquina, instale atráves deste repositório:
[Terminal](https://github.com/microsoft/terminal/releases)

(Ou pela Microsoft Store).

KeyMaps úteis:
- **CTRL** + **Shift** + **T** - Nova Aba
- **CTRL** + **Shift** + **W** - Fecha aba atual
- **CTRL** + **ALT** + **1/2/3...** - Troca de aba
- **CTRL** + **Shift** + **1/2/3...** - Abre um perfil diferente (ex: cmd, windows powershell, wsl...)

Abra as configurações do windows terminal, logo em seguida, no canto inferior esquerdo clique em:

```Open JSON file```

Então cole a seguinte configuração [settings.json](https://github.com/joaostack/WinDev-Environment/blob/main/configuracoes/settings.json)
salve e reabra o terminal.

Se quiser, pode definir como fundo este wallpaper:
[gavrl-snowy-forest.jpg](https://github.com/joaostack/WinDev-Environment/blob/main/configuracoes/gavrl-snowy-forest.jpg)

## Fontes
No seguinte diretório você irá localizar a fonte que uso:
[Consolas Nerd](https://github.com/joaostack/WinDev-Environment/tree/main/configuracoes/fontes)

A fonte de sua preferência deve ser do tipo "nerd", pois o **neovim** e **starship** carregam alguns icones específicos para esse tipo de fonte.

[Nerd Fonts](https://www.nerdfonts.com/font-downloads)

## StarShip
O **StarShip** é um prompt escrito na linguagem **Rust**, altamente personalizável e rápido (como **ZSH**).

A instalação é simples, semelhante a instalação do **PowerShell 7**.

```powershell
winget install --id Starship.Starship
```

Após concluir a instalação, execute o seguinte comando:
```powershell
mkdir ~/.config
```

Crie um arquivo "**~/.config/starship.toml**" e cole o conteúdo deste:
[starship.toml](https://github.com/joaostack/WinDev-Environment/blob/main/configuracoes/starship.toml)

Para defini-lo como prompt padrão, abra o arquivo da variável **$PROFILE** com seu editor de preferência (ex: **notepad $PROFILE**).

Logo em seguida cole o conteúdo do arquivo:
[Microsoft.PowerShell_profile.ps1](https://github.com/joaostack/WinDev-Environment/blob/main/configuracoes/Microsoft.PowerShell_profile.ps1) salve e feche.

## NeoVim
O **NeoVim** (_NVim_) é um editor de código altamente personalizavel e versátil, ele é perfeito para quem busca performance e produtividade.

A instalação do **NeoVim** pode ser feita diretamente pelo [site oficial](https://neovim.io/doc/install/) ou pelo **winget**.

```powershell
winget install Neovim.Neovim
```

Minha configuração **NeoVim** é baseada na distro [AstroNvim](https://astronvim.com/).
Escolhi a **AstroNvim** em respeito a sua reputação quanto ao desempenho.

Antes de iniciar a instalação da distro, você precisa das seguintes dependências:
- [Python3+](http://python.org/)
- [NodeJS + npm/npx](https://nodejs.org/en)
- [TDM-GCC](https://jmeubank.github.io/tdm-gcc/download/)
- [Git](https://git-scm.com/install/windows)

Uma vez que a instalação concluída, execute o seguinte comando:
```powershell
git clone https://github.com/joaostack/stacknvim $env:LOCALAPPDATA\nvim
```

Inicie o **NeoVim** e aguarde o processo de instalação dos pacotes finalizar.
```
nvim
```

Com o **NeoVim** aberto, pressione a tecla "**:**" e digite o seguinte comando para instalar o servidor **LSP Roslyn** usando o **Mason**:
```
MasonInstall roslyn
```
