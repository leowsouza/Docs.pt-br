---
uid: mvc/overview/deployment/docker
title: "Migrando aplicativos ASP.NET MVC para contêineres do Windows"
description: "Saiba como selecionar um aplicativo ASP.NET MVC existente e executá-lo em um contêiner do Docker do Windows"
keywords: Windows Containers,Docker,ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 02/01/2017
ms.topic: article
ms.prod: .net-framework
ms.technology: dotnet-mvc
ms.devlang: dotnet
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 336d0e9d2247dd2d63c779fd446f9a50be6dbc50
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a><span data-ttu-id="d6133-104">Migrando aplicativos ASP.NET MVC para contêineres do Windows</span><span class="sxs-lookup"><span data-stu-id="d6133-104">Migrating ASP.NET MVC Applications to Windows Containers</span></span>

<span data-ttu-id="d6133-105">Executar um aplicativo existente baseado no .NET Framework em um contêiner do Windows não requer alterações ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6133-105">Running an existing .NET Framework-based application in a Windows container doesn't require any changes to your app.</span></span> <span data-ttu-id="d6133-106">Para executar seu aplicativo em um contêiner do Windows, crie uma imagem de Docker contendo seu aplicativo e inicie o contêiner.</span><span class="sxs-lookup"><span data-stu-id="d6133-106">To run your app in a Windows container you create a Docker image containing your app and start the container.</span></span> <span data-ttu-id="d6133-107">Este tópico explica como selecionar um [aplicativo ASP.NET MVC](http://www.asp.net/mvc) existente e implantá-lo em um contêiner do Windows.</span><span class="sxs-lookup"><span data-stu-id="d6133-107">This topic explains how to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.</span></span>

<span data-ttu-id="d6133-108">Você começa com um aplicativo ASP.NET MVC existente e cria os ativos publicados usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6133-108">You start with an existing ASP.NET MVC app, then build the published assets using Visual Studio.</span></span> <span data-ttu-id="d6133-109">Você usa o Docker para criar a imagem que contém e executa o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6133-109">You use Docker to create the image that contains and runs your app.</span></span> <span data-ttu-id="d6133-110">Você navegará para o site em execução em um contêiner do Windows e verificará se que o aplicativo está funcionando.</span><span class="sxs-lookup"><span data-stu-id="d6133-110">You'll browse to the site running in a Windows container and verify the app is working.</span></span>

<span data-ttu-id="d6133-111">Este artigo pressupõe uma compreensão básica do Docker.</span><span class="sxs-lookup"><span data-stu-id="d6133-111">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="d6133-112">Saiba mais sobre o Docker lendo a [Visão Geral do Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="d6133-112">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

<span data-ttu-id="d6133-113">O aplicativo que você executará em um contêiner é um site simples que responde a perguntas aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="d6133-113">The app you'll run in a container is a simple website that answers questions randomly.</span></span> <span data-ttu-id="d6133-114">Esse aplicativo é um aplicativo MVC básico sem autenticação ou armazenamento de banco de dados; ele permite que você se concentre em mover a camada da Web para um contêiner.</span><span class="sxs-lookup"><span data-stu-id="d6133-114">This app is a basic MVC application with no authentication or database storage; it lets you focus on moving the web tier to a container.</span></span> <span data-ttu-id="d6133-115">Os tópicos futuros mostrarão como mover e gerenciar o armazenamento persistente em aplicativos em contêineres.</span><span class="sxs-lookup"><span data-stu-id="d6133-115">Future topics will show how to move and manage persistent storage in containerized applications.</span></span>

<span data-ttu-id="d6133-116">Mover seu aplicativo envolve estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d6133-116">Moving your application involves these steps:</span></span>

1. [<span data-ttu-id="d6133-117">Criar uma tarefa de publicação para compilar os ativos para uma imagem.</span><span class="sxs-lookup"><span data-stu-id="d6133-117">Creating a publish task to build the assets for an image.</span></span>](#publish-script)
1. [<span data-ttu-id="d6133-118">Criar uma imagem do Docker que executará o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6133-118">Building a Docker image that will run your application.</span></span>](#build-the-image)
1. [<span data-ttu-id="d6133-119">Iniciar um contêiner do Docker que execute sua imagem.</span><span class="sxs-lookup"><span data-stu-id="d6133-119">Starting a Docker container that runs your image.</span></span>](#start-a-container)
1. [<span data-ttu-id="d6133-120">Verificar o aplicativo usando o navegador.</span><span class="sxs-lookup"><span data-stu-id="d6133-120">Verifying the application using your browser.</span></span>](#verify-in-the-browser)

<span data-ttu-id="d6133-121">O [aplicativo finalizado](https://github.com/dotnet/docs/tree/master/samples/framework/docker/MVCRandomAnswerGenerator) está no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6133-121">The [finished application](https://github.com/dotnet/docs/tree/master/samples/framework/docker/MVCRandomAnswerGenerator) is on GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6133-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6133-122">Prerequisites</span></span>

<span data-ttu-id="d6133-123">A máquina de desenvolvimento deve estar em execução</span><span class="sxs-lookup"><span data-stu-id="d6133-123">The development machine must be running</span></span>

- <span data-ttu-id="d6133-124">[Atualização de Aniversário do Windows 10](https://www.microsoft.com/en-us/software-download/windows10/) (ou superior) ou [Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server) (ou superior).</span><span class="sxs-lookup"><span data-stu-id="d6133-124">[Windows 10 Anniversary Update](https://www.microsoft.com/en-us/software-download/windows10/) (or higher) or [Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server) (or higher).</span></span>
- <span data-ttu-id="d6133-125">[Docker para Windows](https://docs.docker.com/docker-for-windows/) – versão Stable 1.13.0 ou 1.12 Beta 26 (ou versões mais recentes)</span><span class="sxs-lookup"><span data-stu-id="d6133-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - version Stable 1.13.0 or 1.12 Beta 26 (or newer versions)</span></span>
- <span data-ttu-id="d6133-126">[Visual Studio de 2017](https://www.visualstudio.com/en-us/visual-studio-homepage-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6133-126">[Visual Studio 2017](https://www.visualstudio.com/en-us/visual-studio-homepage-vs.aspx).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6133-127">Se você estiver usando o Windows Server 2016, siga as instruções para [Implantação do Host do Contêiner – Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span><span class="sxs-lookup"><span data-stu-id="d6133-127">If you are using Windows Server 2016, follow the instructions for [Container Host Deployment - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span></span>

<span data-ttu-id="d6133-128">Após instalar e iniciar o Docker, clique com o botão direito do mouse no ícone de bandeja e selecione **Alternar para contêineres do Windows**.</span><span class="sxs-lookup"><span data-stu-id="d6133-128">After installing and starting Docker,  right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="d6133-129">Isso é necessário para executar imagens do Docker com base no Windows.</span><span class="sxs-lookup"><span data-stu-id="d6133-129">This is required to run Docker images based on Windows.</span></span> <span data-ttu-id="d6133-130">Este comando demora alguns segundos para ser executado:</span><span class="sxs-lookup"><span data-stu-id="d6133-130">This command takes a few seconds to execute:</span></span>

<span data-ttu-id="d6133-131">![Contêiner do Windows][windows-container]</span><span class="sxs-lookup"><span data-stu-id="d6133-131">![Windows Container][windows-container]</span></span>

## <a name="publish-script"></a><span data-ttu-id="d6133-132">Script de publicação</span><span class="sxs-lookup"><span data-stu-id="d6133-132">Publish script</span></span>

<span data-ttu-id="d6133-133">Colete todos os ativos que você precisa carregar em uma imagem do Docker em um único lugar.</span><span class="sxs-lookup"><span data-stu-id="d6133-133">Collect all the assets that you need to load into a Docker image in one place.</span></span> <span data-ttu-id="d6133-134">Você pode usar o comando **Publicar** do Visual Studio para criar um perfil de publicação para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6133-134">You can use the Visual Studio **Publish** command to create a publish profile for your app.</span></span> <span data-ttu-id="d6133-135">Esse perfil colocará todos os ativos em uma árvore de diretório que você copiará para sua imagem de destino posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6133-135">This profile will put all the assets in one directory tree that you copy to your target image later in this tutorial.</span></span>

<span data-ttu-id="d6133-136">**Etapas de publicação**</span><span class="sxs-lookup"><span data-stu-id="d6133-136">**Publish Steps**</span></span>

1. <span data-ttu-id="d6133-137">Clique com o botão direito do mouse no projeto Web no Visual Studio e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="d6133-137">Right click on the web project in Visual Studio, and select **Publish**.</span></span>
1. <span data-ttu-id="d6133-138">Clique no **botão Perfil personalizado** e selecione **Sistema de Arquivo** como o método.</span><span class="sxs-lookup"><span data-stu-id="d6133-138">Click the **Custom profile button**, and then select **File System** as the method.</span></span>
1. <span data-ttu-id="d6133-139">Selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="d6133-139">Choose the directory.</span></span> <span data-ttu-id="d6133-140">Por convenção, o exemplo baixado usa `bin\Release\PublishOutput`.</span><span class="sxs-lookup"><span data-stu-id="d6133-140">By convention, the downloaded sample uses `bin\Release\PublishOutput`.</span></span>

<span data-ttu-id="d6133-141">![Conexão da publicação][publish-connection]</span><span class="sxs-lookup"><span data-stu-id="d6133-141">![Publish Connection][publish-connection]</span></span>

<span data-ttu-id="d6133-142">Abra a seção **Opções de Publicação de Arquivo** da guia **Configurações**. Selecione **Pré-compilar durante a publicação**.</span><span class="sxs-lookup"><span data-stu-id="d6133-142">Open the **File Publish Options** section of the **Settings** tab. Select **Precompile during publishing**.</span></span> <span data-ttu-id="d6133-143">Essa otimização significa que você compilará as exibições no contêiner do Docker, está copiando as exibições pré-compiladas.</span><span class="sxs-lookup"><span data-stu-id="d6133-143">This optimization means that you'll be compiling views in the Docker container, you are copying the precompiled views.</span></span>

<span data-ttu-id="d6133-144">![Configurações de publicação][publish-settings]</span><span class="sxs-lookup"><span data-stu-id="d6133-144">![Publish Settings][publish-settings]</span></span>

<span data-ttu-id="d6133-145">Clique em **Publicar** e o Visual Studio copiará todos os ativos necessários para a pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="d6133-145">Click **Publish**, and Visual Studio will copy all the needed assets to the destination folder.</span></span>

## <a name="build-the-image"></a><span data-ttu-id="d6133-146">Criar a imagem</span><span class="sxs-lookup"><span data-stu-id="d6133-146">Build the image</span></span>

<span data-ttu-id="d6133-147">Defina a imagem de Docker em um Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="d6133-147">Define your Docker image in a Dockerfile.</span></span> <span data-ttu-id="d6133-148">O Dockerfile contém instruções para a imagem base, componentes adicionais, o aplicativo que você deseja executar e outras imagens de configuração.</span><span class="sxs-lookup"><span data-stu-id="d6133-148">The Dockerfile contains instructions for the base image, additional components, the app you want to run, and other configuration images.</span></span>  <span data-ttu-id="d6133-149">O Dockerfile é a entrada para o comando `docker build`, que cria a imagem.</span><span class="sxs-lookup"><span data-stu-id="d6133-149">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span>

<span data-ttu-id="d6133-150">Você criará uma imagem com base na imagem do `microsft/aspnet` localizada no [Hub do Docker](https://hub.docker.com/r/microsoft/aspnet/).</span><span class="sxs-lookup"><span data-stu-id="d6133-150">You will build an image based on the `microsft/aspnet` image located on [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span></span>
<span data-ttu-id="d6133-151">A imagem base, `microsoft/aspnet`, é uma imagem do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d6133-151">The base image, `microsoft/aspnet`, is a Windows Server image.</span></span> <span data-ttu-id="d6133-152">Ele contém o Windows Server Core, IIS e ASP.NET 4.6.2.</span><span class="sxs-lookup"><span data-stu-id="d6133-152">It contains Windows Server Core, IIS and ASP.NET 4.6.2.</span></span> <span data-ttu-id="d6133-153">Quando você executar essa imagem em seu contêiner, ela iniciará automaticamente o IIS e sites instalados.</span><span class="sxs-lookup"><span data-stu-id="d6133-153">When you run this image in your container, it will automatically start IIS and installed websites.</span></span>

<span data-ttu-id="d6133-154">O Dockerfile que cria a imagem tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="d6133-154">The Dockerfile that creates your image looks like this:</span></span>

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

<span data-ttu-id="d6133-155">Não há nenhum comando `ENTRYPOINT` neste Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="d6133-155">There is no `ENTRYPOINT` command in this Dockerfile.</span></span> <span data-ttu-id="d6133-156">Você não precisa de um.</span><span class="sxs-lookup"><span data-stu-id="d6133-156">You don't need one.</span></span> <span data-ttu-id="d6133-157">Ao executar o Windows Server com o IIS, o processo do IIS é o ponto de entrada, que é configurado para iniciar a imagem base do aspnet.</span><span class="sxs-lookup"><span data-stu-id="d6133-157">When running Windows Server with IIS, the IIS process is the entrypoint, which is configured to start in the aspnet base image.</span></span>

<span data-ttu-id="d6133-158">Execute o comando de compilação do Docker para criar a imagem que executa seu aplicativo ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d6133-158">Run the Docker build command to create the image that runs your ASP.NET app.</span></span> <span data-ttu-id="d6133-159">Para fazer isso, abra uma janela do PowerShell no diretório do projeto e digite o seguinte comando no diretório da solução:</span><span class="sxs-lookup"><span data-stu-id="d6133-159">To do this, open a PowerShell window in the directory of your project and type the following command in the solution directory:</span></span>

```console
docker build -t mvcrandomanswers .
```

<span data-ttu-id="d6133-160">Este comando criará a nova imagem usando as instruções em seu Dockerfile, nomear (-t marcação) a imagem como mvcrandomanswers.</span><span class="sxs-lookup"><span data-stu-id="d6133-160">This command will build the new image using the instructions in your Dockerfile, naming (-t tagging) the image as mvcrandomanswers.</span></span> <span data-ttu-id="d6133-161">Isso pode incluir efetuar o pull da imagem base do [Hub do Docker](http://hub.docker.com) e, em seguida, adicionar seu aplicativo àquela imagem.</span><span class="sxs-lookup"><span data-stu-id="d6133-161">This may include pulling the base image from [Docker Hub](http://hub.docker.com), and then adding your app to that image.</span></span>

<span data-ttu-id="d6133-162">Depois que o comando for concluído, você poderá executar o comando `docker images` para ver informações sobre a nova imagem:</span><span class="sxs-lookup"><span data-stu-id="d6133-162">Once that command completes, you can run the `docker images` command to see information on the new image:</span></span>

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

<span data-ttu-id="d6133-163">A ID da IMAGEM será diferente em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d6133-163">The IMAGE ID will be different on your machine.</span></span> <span data-ttu-id="d6133-164">Agora, vamos executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6133-164">Now, let's run the app.</span></span>

## <a name="start-a-container"></a><span data-ttu-id="d6133-165">Iniciar um contêiner</span><span class="sxs-lookup"><span data-stu-id="d6133-165">Start a container</span></span>

<span data-ttu-id="d6133-166">Inicie um contêiner executando o seguinte comando `docker run`:</span><span class="sxs-lookup"><span data-stu-id="d6133-166">Start a container by executing the following `docker run` command:</span></span>

```console
docker run -d --name randomanswers mvcrandomanswers
```

<span data-ttu-id="d6133-167">O argumento `-d` diz ao Docker para iniciar a imagem no modo desconectado.</span><span class="sxs-lookup"><span data-stu-id="d6133-167">The `-d` argument tells Docker to start the image in detached mode.</span></span> <span data-ttu-id="d6133-168">Isso significa que a imagem do Docker é executada desconectada do shell atual.</span><span class="sxs-lookup"><span data-stu-id="d6133-168">That means the Docker image runs disconnected from the current shell.</span></span>

<span data-ttu-id="d6133-169">Em muitos exemplos de docker, você poderá ver -p para mapear as portas do contêiner e o host.</span><span class="sxs-lookup"><span data-stu-id="d6133-169">In many docker examples, you may see -p to map the container and host ports.</span></span> <span data-ttu-id="d6133-170">A imagem padrão do aspnet já tiver configurado o contêiner para escutar na porta 80 e expô-lo.</span><span class="sxs-lookup"><span data-stu-id="d6133-170">The default aspnet image has already configured the container to listen on port 80 and expose it.</span></span> 

<span data-ttu-id="d6133-171">O `--name randomanswers` fornece um nome para o contêiner em execução.</span><span class="sxs-lookup"><span data-stu-id="d6133-171">The `--name randomanswers` gives a name to the running container.</span></span> <span data-ttu-id="d6133-172">Você pode usar esse nome em vez da ID do contêiner na maioria dos comandos.</span><span class="sxs-lookup"><span data-stu-id="d6133-172">You can use this name instead of the container ID in most commands.</span></span>

<span data-ttu-id="d6133-173">O `mvcrandomanswers` é o nome da imagem a ser iniciada.</span><span class="sxs-lookup"><span data-stu-id="d6133-173">The `mvcrandomanswers` is the name of the image to start.</span></span>

## <a name="verify-in-the-browser"></a><span data-ttu-id="d6133-174">Verificar no navegador</span><span class="sxs-lookup"><span data-stu-id="d6133-174">Verify in the browser</span></span>

> [!NOTE]
> <span data-ttu-id="d6133-175">Com a versão atual do contêiner do Windows, não é possível navegar para `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="d6133-175">With the current Windows Container release, you can't browse to `http://localhost`.</span></span>
> <span data-ttu-id="d6133-176">Esse é um comportamento conhecido no WinNAT e ele será resolvido no futuro.</span><span class="sxs-lookup"><span data-stu-id="d6133-176">This is a known behavior in WinNAT, and it will be resolved in the future.</span></span> <span data-ttu-id="d6133-177">Até que isso seja resolvido, você precisará usar o endereço IP do contêiner.</span><span class="sxs-lookup"><span data-stu-id="d6133-177">Until that is addressed, you need to use the IP address of the container.</span></span>

<span data-ttu-id="d6133-178">Após o contêiner ser iniciado, localize seu endereço IP para que possa se conectar ao seu contêiner em execução de um navegador:</span><span class="sxs-lookup"><span data-stu-id="d6133-178">Once the container starts, find its IP address so that you can connect to your running container from a browser:</span></span>

```console
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" randomanswers
172.31.194.61
```

<span data-ttu-id="d6133-179">Conecte-se ao contêiner em execução usando o endereço IPv4, `http://172.31.194.61` no exemplo mostrado.</span><span class="sxs-lookup"><span data-stu-id="d6133-179">Connect to the running container using the IPv4 address, `http://172.31.194.61` in the example shown.</span></span> <span data-ttu-id="d6133-180">Digite a URL no navegador e você deverá ver o site em execução.</span><span class="sxs-lookup"><span data-stu-id="d6133-180">Type that URL into your browser, and you should see the running site.</span></span>

> [!NOTE]
> <span data-ttu-id="d6133-181">Alguns softwares de proxy ou VPN podem impedir que você navegue para seu site.</span><span class="sxs-lookup"><span data-stu-id="d6133-181">Some VPN or proxy software may prevent you from navigating to your site.</span></span>
> <span data-ttu-id="d6133-182">Você pode desabilitá-los temporariamente para se certificar de que seu contêiner está funcionando.</span><span class="sxs-lookup"><span data-stu-id="d6133-182">You can temporarily disable it to make sure your container is working.</span></span>

<span data-ttu-id="d6133-183">O diretório de exemplo no GitHub contém um [script do PowerShell](https://github.com/dotnet/docs/tree/master/samples/framework/docker/MVCRandomAnswerGenerator/run.ps1) que executa esses comandos para você.</span><span class="sxs-lookup"><span data-stu-id="d6133-183">The sample directory on GitHub contains a [PowerShell script](https://github.com/dotnet/docs/tree/master/samples/framework/docker/MVCRandomAnswerGenerator/run.ps1) that executes these commands for you.</span></span> <span data-ttu-id="d6133-184">Abra uma janela do PowerShell, altere o diretório para o diretório da solução e digite:</span><span class="sxs-lookup"><span data-stu-id="d6133-184">Open a PowerShell window, change directory to your solution directory, and type:</span></span>

```console
./run.ps1
```

<span data-ttu-id="d6133-185">O comando acima cria a imagem, exibe a lista de imagens no seu computador, inicia um contêiner e exibe o endereço IP do contêiner.</span><span class="sxs-lookup"><span data-stu-id="d6133-185">The command above builds the image, displays the list of images on your machine, starts a container, and displays the IP address for that container.</span></span>

<span data-ttu-id="d6133-186">Para parar o seu contêiner, emita um comando `docker
stop`:</span><span class="sxs-lookup"><span data-stu-id="d6133-186">To stop your container, issue a `docker
stop` command:</span></span>

```console
docker stop randomanswers
```

<span data-ttu-id="d6133-187">Para remover o contêiner, emita um comando `docker rm`:</span><span class="sxs-lookup"><span data-stu-id="d6133-187">To remove the container, issue a `docker rm` command:</span></span>

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Alternar para o contêiner do Windows"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Publicar no sistema de arquivos"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Configurações de publicação"