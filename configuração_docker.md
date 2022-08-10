## Configurando o Docker em sua máquina:

A fim de facilitar o desenvolvimento das etapas do projeto, abaixo segue um passo a passo de preparação de ambiente.

### Download Docker e Docker Compose:

### Download Docker - Windows

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Instalação Docker - Windows

1. Verificar se o Windows está atualizado. Caso seja inferiro a 18362, clique no link ao lado para atualizar o Windows 10. [Atualizar o Windows](https://www.microsoft.com/pt-br/software-download/windows10);
2. Pesquise por Ativar ou desativar recursos do Windows e siga os passos abaixo:
    - Desativar Hyper-V;
    - Desativar Plataforma do Hipervisor do Windows;
    - Habilitar a Plataforma de Máquina Virtual;
    - Habilitar o Subsistema do Windows para Linux (WSL).
3. Faça o Download do WSL 2 clicando no link ao lado: [Download WSL 2](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi);
4. Acesse a Microsoft Store, e faça download e instale a distribuição Linux Ubuntu 20.04 LTS (recomendado);
5. Instale o Docker Desktop no Windows: [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows);
    - Obs: Abra o Docker Desktop e verifique se estão habilitados o "Enable integration with my default WSL distro" e "Ubuntu-20.04" em Settings->Resource->WSL Integration.

### Instalação Docker - Linux

- [Link para instalação do Docker Engine](https://docs.docker.com/engine/install/)
- [Link para instalação do Docker Compose](https://docs.docker.com/compose/install/)

### Instalação Docker - Mac
- [Link para instalação do Docker Desktop no Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac/)
