---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: "Tutorial: Introdução ao SignalR 2 e MVC 5 | Microsoft Docs"
author: pfletcher
description: "Este tutorial mostra como usar o ASP.NET SignalR 2 para criar um aplicativo de bate-papo em tempo real. Você adicionará o SignalR para um aplicativo MVC 5 e criar uma exibição de bate-papo..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.openlocfilehash: 96a6f6446b26d96b2bcffe4354375ab9c444bbbb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="tutorial-getting-started-with-signalr-2-and-mvc-5"></a><span data-ttu-id="5ceda-104">Tutorial: Introdução ao SignalR 2 e 5 do MVC</span><span class="sxs-lookup"><span data-stu-id="5ceda-104">Tutorial: Getting Started with SignalR 2 and MVC 5</span></span>
====================
<span data-ttu-id="5ceda-105">por [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="5ceda-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[<span data-ttu-id="5ceda-106">Baixe o projeto concluído</span><span class="sxs-lookup"><span data-stu-id="5ceda-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

> <span data-ttu-id="5ceda-107">Este tutorial mostra como usar o ASP.NET SignalR 2 para criar um aplicativo de bate-papo em tempo real.</span><span class="sxs-lookup"><span data-stu-id="5ceda-107">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="5ceda-108">Você adicionará o SignalR para um aplicativo MVC 5 e criar uma exibição de bate-papo para enviar e exibir as mensagens.</span><span class="sxs-lookup"><span data-stu-id="5ceda-108">You will add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span> 
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5ceda-109">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="5ceda-109">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="5ceda-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5ceda-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="5ceda-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5ceda-111">.NET 4.5</span></span>
> - <span data-ttu-id="5ceda-112">MVC 5</span><span class="sxs-lookup"><span data-stu-id="5ceda-112">MVC 5</span></span>
> - <span data-ttu-id="5ceda-113">SignalR versão 2</span><span class="sxs-lookup"><span data-stu-id="5ceda-113">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="5ceda-114">Usando o Visual Studio 2012 com este tutorial</span><span class="sxs-lookup"><span data-stu-id="5ceda-114">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="5ceda-115">Para usar o Visual Studio 2012 com este tutorial, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5ceda-115">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="5ceda-116">Atualização de seu [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="5ceda-116">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="5ceda-117">Instalar o [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ceda-117">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="5ceda-118">No Web Platform Installer, procurar e instalar **ASP.NET e Web 2013.1 de ferramentas para Visual Studio 2012**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-118">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="5ceda-119">Isso irá instalar os modelos do Visual Studio para SignalR classes como **Hub**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-119">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="5ceda-120">Alguns modelos (como **classe de inicialização OWIN**) não estará disponível; para isso, use um arquivo de classe em vez disso.</span><span class="sxs-lookup"><span data-stu-id="5ceda-120">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="5ceda-121">Versões do tutoriais</span><span class="sxs-lookup"><span data-stu-id="5ceda-121">Tutorial Versions</span></span>
> 
> <span data-ttu-id="5ceda-122">Para obter informações sobre versões anteriores do SignalR, consulte [versões mais antigas do SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="5ceda-122">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="5ceda-123">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="5ceda-123">Questions and comments</span></span>
> 
> <span data-ttu-id="5ceda-124">Deixe comentários em como você gostou neste tutorial e o que podemos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="5ceda-124">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5ceda-125">Se você tiver dúvidas que não estão diretamente relacionadas ao tutorial, você poderá postá-los para o [ASP.NET SignalR fórum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="5ceda-125">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="5ceda-126">Visão Geral</span><span class="sxs-lookup"><span data-stu-id="5ceda-126">Overview</span></span>

<span data-ttu-id="5ceda-127">Este tutorial o apresenta ao desenvolvimento de aplicativos web em tempo real com ASP.NET SignalR 2 e 5 do ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="5ceda-127">This tutorial introduces you to real-time web application development with ASP.NET SignalR 2 and ASP.NET MVC 5.</span></span> <span data-ttu-id="5ceda-128">O tutorial usa o mesmo código de aplicativo de bate-papo, como o [tutorial de Introdução SignalR](tutorial-getting-started-with-signalr.md), mas mostra como adicioná-lo a um aplicativo MVC 5.</span><span class="sxs-lookup"><span data-stu-id="5ceda-128">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 5 application.</span></span>

<span data-ttu-id="5ceda-129">Neste tópico, você aprenderá as seguintes tarefas de desenvolvimento SignalR:</span><span class="sxs-lookup"><span data-stu-id="5ceda-129">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="5ceda-130">Adicionar a biblioteca de SignalR para um aplicativo MVC 5.</span><span class="sxs-lookup"><span data-stu-id="5ceda-130">Adding the SignalR library to an MVC 5 application.</span></span>
- <span data-ttu-id="5ceda-131">Criando hub e classes de inicialização OWIN para transferir conteúdo para clientes.</span><span class="sxs-lookup"><span data-stu-id="5ceda-131">Creating hub and OWIN startup classes to push content to clients.</span></span>
- <span data-ttu-id="5ceda-132">Usando a biblioteca de jQuery SignalR em uma página da web para enviar mensagens e exibir as atualizações do hub.</span><span class="sxs-lookup"><span data-stu-id="5ceda-132">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="5ceda-133">A captura de tela a seguir mostra o aplicativo de chat concluído em execução em um navegador.</span><span class="sxs-lookup"><span data-stu-id="5ceda-133">The following screen shot shows the completed chat application running in a browser.</span></span>

![Instâncias de bate-papo](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

<span data-ttu-id="5ceda-135">Seções:</span><span class="sxs-lookup"><span data-stu-id="5ceda-135">Sections:</span></span>

- [<span data-ttu-id="5ceda-136">Configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="5ceda-136">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="5ceda-137">Executar o exemplo</span><span class="sxs-lookup"><span data-stu-id="5ceda-137">Run the Sample</span></span>](#run)
- [<span data-ttu-id="5ceda-138">Examine o código</span><span class="sxs-lookup"><span data-stu-id="5ceda-138">Examine the Code</span></span>](#code)
- [<span data-ttu-id="5ceda-139">Próximas Etapas</span><span class="sxs-lookup"><span data-stu-id="5ceda-139">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="5ceda-140">Configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="5ceda-140">Set up the Project</span></span>

<span data-ttu-id="5ceda-141">Pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="5ceda-141">Prerequisites:</span></span>

- <span data-ttu-id="5ceda-142">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="5ceda-142">Visual Studio 2013.</span></span> <span data-ttu-id="5ceda-143">Se você não tiver o Visual Studio, consulte [ASP.NET Downloads](https://www.asp.net/downloads) para obter o Visual Studio 2013 Express desenvolvimento ferramenta gratuita.</span><span class="sxs-lookup"><span data-stu-id="5ceda-143">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express Development Tool.</span></span>

<span data-ttu-id="5ceda-144">Esta seção mostra como criar um aplicativo ASP.NET MVC 5, adicione a biblioteca de SignalR e criar o aplicativo de bate-papo.</span><span class="sxs-lookup"><span data-stu-id="5ceda-144">This section shows how to create an ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="5ceda-145">No Visual Studio, criar um aplicativo c# ASP.NET que tem como destino o .NET Framework 4.5, nomeie-o SignalRChat e clique em Okey.</span><span class="sxs-lookup"><span data-stu-id="5ceda-145">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![Criar web](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)
2. <span data-ttu-id="5ceda-147">No `New ASP.NET Project` caixa de diálogo e selecione **MVC**e clique em **alterar autenticação**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-147">In the `New ASP.NET Project` dialog, and select **MVC**, and click **Change Authentication**.</span></span>

    ![Criar web](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)
3. <span data-ttu-id="5ceda-149">Selecione **sem autenticação** no **alterar autenticação** caixa de diálogo e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-149">Select **No Authentication** in the **Change Authentication** dialog, and click **OK**.</span></span>

    ![Selecione sem autenticação](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="5ceda-151">Se você selecionar um provedor de autenticação diferentes para o seu aplicativo, um `Startup.cs` classe será criada para você; você não precisará criar seus próprios `Startup.cs` classe na etapa 10 abaixo.</span><span class="sxs-lookup"><span data-stu-id="5ceda-151">If you select a different authentication provider for your application, a `Startup.cs` class will be created for you; you will not need to create your own `Startup.cs` class in step 10 below.</span></span>
4. <span data-ttu-id="5ceda-152">Clique em **Okey** no **novo projeto ASP.NET** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ceda-152">Click **OK** in the **New ASP.NET Project** dialog.</span></span>
5. <span data-ttu-id="5ceda-153">Abra o **ferramentas | Gerenciador de biblioteca de pacote | Package Manager Console** e execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="5ceda-153">Open the **Tools | Library Package Manager | Package Manager Console** and run the following command.</span></span> <span data-ttu-id="5ceda-154">Esta etapa adiciona ao projeto um conjunto de arquivos de script e referências de assembly que habilitar a funcionalidade do SignalR.</span><span class="sxs-lookup"><span data-stu-id="5ceda-154">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

    `install-package Microsoft.AspNet.SignalR`
6. <span data-ttu-id="5ceda-155">Em **Solution Explorer**, expanda a pasta de Scripts.</span><span class="sxs-lookup"><span data-stu-id="5ceda-155">In **Solution Explorer**, expand the Scripts folder.</span></span> <span data-ttu-id="5ceda-156">Observe que as bibliotecas de scripts para o SignalR foram adicionadas ao projeto.</span><span class="sxs-lookup"><span data-stu-id="5ceda-156">Note that script libraries for SignalR have been added to the project.</span></span>

    ![Pasta de scripts](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)
7. <span data-ttu-id="5ceda-158">Em **Solution Explorer**, clique com o botão direito, selecione **adicionar | Nova pasta**, e adicione uma nova pasta chamada **Hubs**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-158">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
8. <span data-ttu-id="5ceda-159">Clique com botão direito do **Hubs** pasta, clique em **adicionar | Novo Item**, selecione o **Visual c# | Web | SignalR** nó o **instalado** painel, selecione **classe de Hub SignalR (v2)** no painel central e criar um novo hub denominado **ChatHub.cs**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-159">Right-click the **Hubs** folder, click **Add | New Item**, select the **Visual C# | Web | SignalR** node in the **Installed** pane, select **SignalR Hub Class (v2)** from the center pane, and create a new hub named **ChatHub.cs**.</span></span> <span data-ttu-id="5ceda-160">Você usará essa classe como um hub de servidor do SignalR que envia mensagens para todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="5ceda-160">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

    ![Criar novo hub](tutorial-getting-started-with-signalr-and-mvc/_static/image6.png)
9. <span data-ttu-id="5ceda-162">Substitua o código no **ChatHub** classe com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="5ceda-162">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]
10. <span data-ttu-id="5ceda-163">Crie uma nova classe chamada Startup.cs.</span><span class="sxs-lookup"><span data-stu-id="5ceda-163">Create a new class called Startup.cs.</span></span> <span data-ttu-id="5ceda-164">Altere o conteúdo do arquivo para o seguinte.</span><span class="sxs-lookup"><span data-stu-id="5ceda-164">Change the contents of the file to the following.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]
11. <span data-ttu-id="5ceda-165">Editar o `HomeController` classe encontrada no **Controllers/HomeController.cs** e adicione o seguinte método à classe.</span><span class="sxs-lookup"><span data-stu-id="5ceda-165">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="5ceda-166">Esse método retorna o **bate-papo** modo de exibição que você criará em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="5ceda-166">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]
12. <span data-ttu-id="5ceda-167">Clique com botão direito do **exibições/inicial** pasta e selecione **adicionar.... | Exibição**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-167">Right-click the **Views/Home** folder, and select **Add... | View**.</span></span>
13. <span data-ttu-id="5ceda-168">No **adicionar exibição** caixa de diálogo, o nome do novo modo de exibição **bate-papo**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-168">In the **Add View** dialog, name the new view **Chat**.</span></span>

    ![Adicionar uma exibição](tutorial-getting-started-with-signalr-and-mvc/_static/image7.png)
14. <span data-ttu-id="5ceda-170">Substitua o conteúdo do **Chat.cshtml** com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="5ceda-170">Replace the contents of **Chat.cshtml** with the following code.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5ceda-171">Quando você adiciona o SignalR e outras bibliotecas de script ao seu projeto do Visual Studio, o Gerenciador de pacotes pode instalar uma versão do arquivo de script SignalR é mais recente que a versão mostrada neste tópico.</span><span class="sxs-lookup"><span data-stu-id="5ceda-171">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="5ceda-172">Certifique-se de que a referência de script em seu código corresponde à versão da biblioteca de script instalada em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="5ceda-172">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]
15. <span data-ttu-id="5ceda-173">**Salvar todos os** para o projeto.</span><span class="sxs-lookup"><span data-stu-id="5ceda-173">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="5ceda-174">Executar o exemplo</span><span class="sxs-lookup"><span data-stu-id="5ceda-174">Run the Sample</span></span>

1. <span data-ttu-id="5ceda-175">Pressione F5 para executar o projeto no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="5ceda-175">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="5ceda-176">Na linha de endereço do navegador, acrescente **inicial/bate-papo** para a URL da página padrão para o projeto.</span><span class="sxs-lookup"><span data-stu-id="5ceda-176">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="5ceda-177">A página de bate-papo carrega em uma instância do navegador e solicitará um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="5ceda-177">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![Insira o nome de usuário](tutorial-getting-started-with-signalr-and-mvc/_static/image8.png)
3. <span data-ttu-id="5ceda-179">Insira um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="5ceda-179">Enter a user name.</span></span>
4. <span data-ttu-id="5ceda-180">Copie a URL da linha de endereço do navegador e usá-lo para abrir duas ou mais instâncias de navegador.</span><span class="sxs-lookup"><span data-stu-id="5ceda-180">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="5ceda-181">Em cada instância do navegador, digite um nome de usuário exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5ceda-181">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="5ceda-182">Em cada instância do navegador, adicione um comentário e clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-182">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="5ceda-183">Os comentários devem exibir em todas as instâncias do navegador.</span><span class="sxs-lookup"><span data-stu-id="5ceda-183">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ceda-184">Este aplicativo de chat simples não mantém o contexto de discussão no servidor.</span><span class="sxs-lookup"><span data-stu-id="5ceda-184">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="5ceda-185">O hub transmite comentários para todos os usuários atuais.</span><span class="sxs-lookup"><span data-stu-id="5ceda-185">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="5ceda-186">Os usuários que entram no bate-papo posteriormente verá mensagens adicionadas desde o momento que entrarem.</span><span class="sxs-lookup"><span data-stu-id="5ceda-186">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="5ceda-187">A captura de tela a seguir mostra o aplicativo de chat em execução em um navegador.</span><span class="sxs-lookup"><span data-stu-id="5ceda-187">The following screen shot shows the chat application running in a browser.</span></span>

    ![Navegadores de chat](tutorial-getting-started-with-signalr-and-mvc/_static/image9.png)
7. <span data-ttu-id="5ceda-189">Em **Solution Explorer**, inspecione o **documentos de Script** nó para o aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="5ceda-189">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="5ceda-190">Esse nó é visível no modo de depuração, se você estiver usando o Internet Explorer como navegador.</span><span class="sxs-lookup"><span data-stu-id="5ceda-190">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="5ceda-191">Há um arquivo de script denominado **hubs** que a biblioteca de SignalR gera dinamicamente em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5ceda-191">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="5ceda-192">Este arquivo gerencia a comunicação entre jQuery script e código do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="5ceda-192">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="5ceda-193">Se você usar um navegador que não seja o Internet Explorer, você também pode acessar dinâmico **hubs** arquivo navegando até ele diretamente, por exemplo http://mywebsite/signalr/hubs.</span><span class="sxs-lookup"><span data-stu-id="5ceda-193">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="5ceda-194">Examine o código</span><span class="sxs-lookup"><span data-stu-id="5ceda-194">Examine the Code</span></span>

<span data-ttu-id="5ceda-195">O aplicativo de chat SignalR demonstra duas tarefas básicas de desenvolvimento SignalR: Criando um hub de como o objeto de coordenação principal no servidor e, usando a biblioteca de jQuery SignalR para enviar e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="5ceda-195">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="5ceda-196">Hubs de SignalR</span><span class="sxs-lookup"><span data-stu-id="5ceda-196">SignalR Hubs</span></span>

<span data-ttu-id="5ceda-197">No exemplo de código a **ChatHub** classe deriva o **Microsoft.AspNet.SignalR.Hub** classe.</span><span class="sxs-lookup"><span data-stu-id="5ceda-197">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="5ceda-198">Derivando de **Hub** classe é uma maneira útil para criar um aplicativo do SignalR.</span><span class="sxs-lookup"><span data-stu-id="5ceda-198">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="5ceda-199">Você pode criar métodos públicos em sua classe de hub e, em seguida, esses métodos de acesso chamando-los a partir de scripts em uma página da web.</span><span class="sxs-lookup"><span data-stu-id="5ceda-199">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="5ceda-200">No código de bate-papo, clientes chamar o **ChatHub.Send** para enviar uma nova mensagem.</span><span class="sxs-lookup"><span data-stu-id="5ceda-200">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="5ceda-201">O hub por sua vez envia a mensagem a todos os clientes chamando **Clients.All.addNewMessageToPage**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-201">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="5ceda-202">O **enviar** método demonstra vários conceitos de hub:</span><span class="sxs-lookup"><span data-stu-id="5ceda-202">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="5ceda-203">Declare métodos públicos em um hub para que os clientes podem chamá-los.</span><span class="sxs-lookup"><span data-stu-id="5ceda-203">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="5ceda-204">Use o **Microsoft.AspNet.SignalR.Hub.Clients** propriedade para acessar todos os clientes conectados a esse hub.</span><span class="sxs-lookup"><span data-stu-id="5ceda-204">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="5ceda-205">Chamar uma função no cliente (como o `addNewMessageToPage` função) para atualizar clientes.</span><span class="sxs-lookup"><span data-stu-id="5ceda-205">Call a function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="5ceda-206">SignalR e jQuery</span><span class="sxs-lookup"><span data-stu-id="5ceda-206">SignalR and jQuery</span></span>

<span data-ttu-id="5ceda-207">O **Chat.cshtml** exibir o arquivo no exemplo de código mostra como usar a biblioteca de jQuery SignalR para se comunicar com um hub SignalR.</span><span class="sxs-lookup"><span data-stu-id="5ceda-207">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="5ceda-208">As tarefas essenciais no código estão criando uma referência para o proxy geradas automaticamente para o hub, declarar uma função que o servidor pode chamar para conteúdo por push aos clientes e iniciar uma conexão para enviar mensagens para o hub.</span><span class="sxs-lookup"><span data-stu-id="5ceda-208">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="5ceda-209">O código a seguir declara uma referência a um proxy do hub.</span><span class="sxs-lookup"><span data-stu-id="5ceda-209">The following code declares a reference to a hub proxy.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="5ceda-210">Em JavaScript a referência para a classe de servidor e seus membros está em minúsculas concatenadas.</span><span class="sxs-lookup"><span data-stu-id="5ceda-210">In JavaScript the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="5ceda-211">O exemplo de código referencia o c# **ChatHub** classe em JavaScript como **chatHub**.</span><span class="sxs-lookup"><span data-stu-id="5ceda-211">The code sample references the C# **ChatHub** class in JavaScript as **chatHub**.</span></span> <span data-ttu-id="5ceda-212">Se você quiser fazer referência a `ChatHub` classe jQuery com Pascal convencional maiusculas e minúsculas como você faria no c#, editar o arquivo de classe ChatHub.cs.</span><span class="sxs-lookup"><span data-stu-id="5ceda-212">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="5ceda-213">Adicionar um `using` instrução para fazer referência a `Microsoft.AspNet.SignalR.Hubs` namespace.</span><span class="sxs-lookup"><span data-stu-id="5ceda-213">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="5ceda-214">Em seguida, adicione o `HubName` de atributo para o `ChatHub` classe, por exemplo `[HubName("ChatHub")]`.</span><span class="sxs-lookup"><span data-stu-id="5ceda-214">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="5ceda-215">Por fim, atualize sua referência jQuery para o `ChatHub` classe.</span><span class="sxs-lookup"><span data-stu-id="5ceda-215">Finally, update your jQuery reference to the `ChatHub` class.</span></span>


<span data-ttu-id="5ceda-216">O código a seguir mostra como criar uma função de retorno de chamada no script.</span><span class="sxs-lookup"><span data-stu-id="5ceda-216">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="5ceda-217">A classe de hub no servidor chama esta função para enviar atualizações de conteúdo para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="5ceda-217">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="5ceda-218">A chamada opcional para o `htmlEncode` função mostra uma maneira para HTML codifica o conteúdo da mensagem antes de exibi-lo na página, como uma maneira de impedir injeção de script.</span><span class="sxs-lookup"><span data-stu-id="5ceda-218">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="5ceda-219">O código a seguir mostra como abrir uma conexão com o hub.</span><span class="sxs-lookup"><span data-stu-id="5ceda-219">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="5ceda-220">O código começa a conexão e, em seguida, passa uma função para manipular o evento de clique no **enviar** botão na página de bate-papo.</span><span class="sxs-lookup"><span data-stu-id="5ceda-220">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="5ceda-221">Essa abordagem garante que a conexão seja estabelecida antes de executa o manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="5ceda-221">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="5ceda-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5ceda-222">Next Steps</span></span>

<span data-ttu-id="5ceda-223">Você aprendeu SignalR é uma estrutura para criar aplicativos web em tempo real.</span><span class="sxs-lookup"><span data-stu-id="5ceda-223">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="5ceda-224">Você também aprendeu diversas tarefas de desenvolvimento SignalR: como adicionar SignalR para um aplicativo ASP.NET, como criar uma classe de hub e como enviar e receber mensagens do hub.</span><span class="sxs-lookup"><span data-stu-id="5ceda-224">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="5ceda-225">Para obter instruções sobre como implantar o aplicativo de exemplo de SignalR no Azure, consulte [usando SignalR com aplicativos Web no serviço de aplicativo do Azure](../deployment/using-signalr-with-azure-web-sites.md).</span><span class="sxs-lookup"><span data-stu-id="5ceda-225">For a walkthrough on how to deploy the sample SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="5ceda-226">Para obter informações detalhadas sobre como implantar um projeto da web do Visual Studio para um Site do Windows Azure, consulte [criar um aplicativo web ASP.NET no serviço de aplicativo do Azure](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-get-started/).</span><span class="sxs-lookup"><span data-stu-id="5ceda-226">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<span data-ttu-id="5ceda-227">Para saber mais avançados conceitos de desenvolvimentos SignalR, visite os seguintes sites para SignalR código-fonte e recursos:</span><span class="sxs-lookup"><span data-stu-id="5ceda-227">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="5ceda-228">Projeto de SignalR</span><span class="sxs-lookup"><span data-stu-id="5ceda-228">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="5ceda-229">SignalR Github e exemplos</span><span class="sxs-lookup"><span data-stu-id="5ceda-229">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="5ceda-230">Wiki do SignalR</span><span class="sxs-lookup"><span data-stu-id="5ceda-230">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)