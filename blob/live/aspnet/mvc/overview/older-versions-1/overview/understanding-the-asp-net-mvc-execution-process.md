---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: "Noções básicas sobre o processo de execução do ASP.NET MVC | Microsoft Docs"
author: microsoft
description: "Saiba como a estrutura ASP.NET MVC processa uma solicitação do navegador passo a passo."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 5837c6e49709d6b86ee52cd88ffd4759c1850544
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="f7f35-103">Noções básicas sobre o processo de execução do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f7f35-103">Understanding the ASP.NET MVC Execution Process</span></span>
====================
<span data-ttu-id="f7f35-104">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f7f35-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="f7f35-105">Saiba como a estrutura ASP.NET MVC processa uma solicitação do navegador passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f7f35-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>


<span data-ttu-id="f7f35-106">Solicitações para um aplicativo Web do ASP.NET MVC primeiro passam o **UrlRoutingModule** objeto, que é um módulo HTTP.</span><span class="sxs-lookup"><span data-stu-id="f7f35-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="f7f35-107">Este módulo analisa a solicitação e executa a seleção de rotas.</span><span class="sxs-lookup"><span data-stu-id="f7f35-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="f7f35-108">O **UrlRoutingModule** objeto seleciona o primeiro objeto de rota que corresponda à solicitação atual.</span><span class="sxs-lookup"><span data-stu-id="f7f35-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="f7f35-109">(Um objeto de rota é uma classe que implementa **RouteBase**, e normalmente é uma ocorrência da **rota** classe.) Se nenhum rotas corresponderem, o **UrlRoutingModule** objeto não faz nada e permite que a solicitação de fallback para a solicitação ASP.NET ou IIS regular processamento.</span><span class="sxs-lookup"><span data-stu-id="f7f35-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="f7f35-110">Do selecionado **rota** objeto, o **UrlRoutingModule** objeto obtém o **IRouteHandler** objeto que está associado com o **rota**objeto.</span><span class="sxs-lookup"><span data-stu-id="f7f35-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="f7f35-111">Normalmente, em um aplicativo MVC, isso será uma instância de **MvcRouteHandler**.</span><span class="sxs-lookup"><span data-stu-id="f7f35-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="f7f35-112">O **IRouteHandler** instância cria um **IHttpHandler** de objeto e transmite o **IHttpContext** objeto.</span><span class="sxs-lookup"><span data-stu-id="f7f35-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="f7f35-113">Por padrão, o **IHttpHandler** instância para MVC é o **MvcHandler** objeto.</span><span class="sxs-lookup"><span data-stu-id="f7f35-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="f7f35-114">O **MvcHandler** objeto, em seguida, seleciona o controlador que, por fim, tratará a solicitação.</span><span class="sxs-lookup"><span data-stu-id="f7f35-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="f7f35-115">Quando um aplicativo ASP.NET MVC é executado no IIS 7.0, nenhuma extensão de nome de arquivo é necessária para projetos MVC.</span><span class="sxs-lookup"><span data-stu-id="f7f35-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="f7f35-116">No entanto, no IIS 6.0, o manipulador requer que você mapear a extensão de nome de arquivo. MVC para a DLL ISAPI do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f7f35-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>


<span data-ttu-id="f7f35-117">O módulo e o manipulador são os pontos de entrada para a estrutura ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f7f35-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="f7f35-118">Eles executar as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="f7f35-118">They perform the following actions:</span></span>

- <span data-ttu-id="f7f35-119">Selecione o controlador apropriado em um aplicativo MVC.</span><span class="sxs-lookup"><span data-stu-id="f7f35-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="f7f35-120">Obtenha uma instância do controlador específico.</span><span class="sxs-lookup"><span data-stu-id="f7f35-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="f7f35-121">Chame o controlador **Execute** método.</span><span class="sxs-lookup"><span data-stu-id="f7f35-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="f7f35-122">A seguir lista as etapas de execução para um projeto MVC Web:</span><span class="sxs-lookup"><span data-stu-id="f7f35-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="f7f35-123">Receber a primeira solicitação para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7f35-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="f7f35-124">No arquivo global. asax, **rota** objetos são adicionados para o **RouteTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="f7f35-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="f7f35-125">Executar o roteamento</span><span class="sxs-lookup"><span data-stu-id="f7f35-125">Perform routing</span></span> 

    - <span data-ttu-id="f7f35-126">O **UrlRoutingModule** módulo usa a primeira correspondência **rota** objeto o **RouteTable** coleção para criar o **RouteData** objeto que ele usa para criar um **RequestContext** (**IHttpContext**) objeto.</span><span class="sxs-lookup"><span data-stu-id="f7f35-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="f7f35-127">Criar um manipulador de solicitação do MVC</span><span class="sxs-lookup"><span data-stu-id="f7f35-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="f7f35-128">O **MvcRouteHandler** objeto cria uma instância do **MvcHandler** classe e transmite o **RequestContext** instância.</span><span class="sxs-lookup"><span data-stu-id="f7f35-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="f7f35-129">Criar o controlador</span><span class="sxs-lookup"><span data-stu-id="f7f35-129">Create controller</span></span> 

    - <span data-ttu-id="f7f35-130">O **MvcHandler** objeto usa o **RequestContext** instância para identificar o **IControllerFactory** objeto (normalmente uma instância do  **DefaultControllerFactory** classe) para criar a instância do controlador com.</span><span class="sxs-lookup"><span data-stu-id="f7f35-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="f7f35-131">Controlador execute - o **MvcHandler** instância chama o controlador s **Execute** método.</span><span class="sxs-lookup"><span data-stu-id="f7f35-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="f7f35-132">Invocação de ação</span><span class="sxs-lookup"><span data-stu-id="f7f35-132">Invoke action</span></span> 

    - <span data-ttu-id="f7f35-133">A maioria dos controladores herdam o **controlador** classe base.</span><span class="sxs-lookup"><span data-stu-id="f7f35-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="f7f35-134">Para controladores que fazê-lo, o **ControllerActionInvoker** objeto que está associado com o controlador determina qual método de ação da classe do controlador para chamar e, em seguida, chama esse método.</span><span class="sxs-lookup"><span data-stu-id="f7f35-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="f7f35-135">Execute o resultado</span><span class="sxs-lookup"><span data-stu-id="f7f35-135">Execute result</span></span> 

    - <span data-ttu-id="f7f35-136">Um método de ação típica pode receber entrada do usuário, preparar os dados de resposta apropriado e, em seguida, execute o resultado ao retornar um tipo de resultado.</span><span class="sxs-lookup"><span data-stu-id="f7f35-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="f7f35-137">Os tipos de resultados internos que podem ser executados incluem o seguinte: **ViewResult** (que renderiza uma exibição e é o tipo de resultado com mais frequência usado), **RedirectToRouteResult**,  **RedirectResult**, **ContentResult**, **JsonResult**, e **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="f7f35-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>