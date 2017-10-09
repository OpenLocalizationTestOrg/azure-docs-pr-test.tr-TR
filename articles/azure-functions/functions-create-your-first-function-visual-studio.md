---
title: "ilk işlev Visual Studio kullanarak Azure'da aaaCreate | Microsoft Docs"
description: "Oluşturma ve Visual Studio için Azure işlevleri araçları kullanarak basit bir HTTP tetiklenen işlevi tooAzure yayımlama."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, işlem, sunucusuz mimari"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="b69ac-104">Visual Studio kullanarak ilk işlevinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b69ac-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="b69ac-105">Azure işlevleri sağlayan bir VM oluşturun veya bir web uygulaması yayımlama toofirst gerek kalmadan sunucusuz bir ortamda kodunuzu yürütün.</span><span class="sxs-lookup"><span data-stu-id="b69ac-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="b69ac-106">Bu konuda, nasıl toouse Azure işlevleri toocreate için Visual Studio 2017 araçları hello ve bir "hello world" işlevi yerel olarak test öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b69ac-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="b69ac-107">Merhaba işlevi kod tooAzure sonra yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b69ac-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="b69ac-108">Bu araçları, Visual Studio 2017 sürüm 15.3 hello Azure geliştirme iş yükü parçası veya sonraki bir sürümü kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b69ac-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Visual Studio projesinde Azure İşlevleri kodu](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="b69ac-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b69ac-110">Prerequisites</span></span>

<span data-ttu-id="b69ac-111">toocomplete Bu öğretici, yükleme:</span><span class="sxs-lookup"><span data-stu-id="b69ac-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="b69ac-112">[Visual Studio 2017 sürüm 15.3](https://www.visualstudio.com/vs/preview/), hello dahil olmak üzere **Azure geliştirme** iş yükü.</span><span class="sxs-lookup"><span data-stu-id="b69ac-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Visual Studio 2017 hello Azure geliştirme yüküyle yükleyin](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="b69ac-114">Yükleme veya tooVisual Studio 2017 sürüm 15.3 yükselttikten sonra Azure işlevleri için toomanually güncelleştirme hello Visual Studio 2017 araçları da gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b69ac-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="b69ac-115">Merhaba hello araçlarından güncelleştirebilirsiniz **Araçları** menüsünün altında **Uzantılar ve güncelleştirmeler...**   >  **Güncelleştirmeleri** > **Visual Studio Marketi'ine** > **Azure işlevleri ve Web Araçları işleri**  >  **Güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="b69ac-116">Visual Studio'da bir Azure İşlevleri projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b69ac-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="b69ac-117">Merhaba proje oluşturduğunuza göre ilk işlevinizi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b69ac-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="b69ac-118">Create Hello işlevi</span><span class="sxs-lookup"><span data-stu-id="b69ac-118">Create hello function</span></span>

1. <span data-ttu-id="b69ac-119">**Çözüm Gezgini**’nde, proje düğümünüze sağ tıklayın ve **Yeni** > **Öğe Ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b69ac-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="b69ac-120">**Azure İşlevi**’ni seçin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b69ac-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="b69ac-121">**HttpTrigger**’ı seçin, **İşlev Adı** yazın, **Erişim Hakları** için **Anonim**’i seçin ve **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b69ac-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="b69ac-122">oluşturulan hello işlevi herhangi bir istemciden bir HTTP isteği tarafından erişilir.</span><span class="sxs-lookup"><span data-stu-id="b69ac-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![Yeni bir Azure İşlevi oluşturma](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="b69ac-124">Kod dosyası işlevi kodunuzu uygulayan bir sınıf içeren tooyour projesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="b69ac-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="b69ac-125">Bu kod adı değeri ve geri kırmak alan bir şablona temel alır.</span><span class="sxs-lookup"><span data-stu-id="b69ac-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="b69ac-126">Merhaba **FunctionName** öznitelik işlevinizi hello adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b69ac-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="b69ac-127">Merhaba **HttpTrigger** öznitelik hello işlevi tetikler selamlama iletisine gösterir.</span><span class="sxs-lookup"><span data-stu-id="b69ac-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![İşlev kod dosyası](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="b69ac-129">HTTP ile tetiklenen işlev oluşturduğunuza göre, artık bunu yerel bilgisayarınızda test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b69ac-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="b69ac-130">Yerel olarak test hello işlevi</span><span class="sxs-lookup"><span data-stu-id="b69ac-130">Test hello function locally</span></span>

<span data-ttu-id="b69ac-131">Azure İşlevleri Temel Araçları, Azure İşlevleri projenizi yerel geliştirme bilgisayarınızda çalıştırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b69ac-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="b69ac-132">Bu araçları ilk kez Visual Studio'dan bir işlev başlattığınızda hello istendiğinde tooinstall var.</span><span class="sxs-lookup"><span data-stu-id="b69ac-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="b69ac-133">tootest işlevinizi, F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b69ac-133">tootest your function, press F5.</span></span> <span data-ttu-id="b69ac-134">İstenirse, Visual Studio toodownload hello isteğini kabul edin ve Azure işlevleri çekirdek (CLI) Araçları'nı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b69ac-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="b69ac-135">Böylece Hello araçları HTTP isteklerini işleyebilir tooenable bir güvenlik duvarı özel durumu da gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b69ac-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="b69ac-136">Kopya hello hello Azure işlevleri çalışma zamanı, işlevinden URL'sini çıktı.</span><span class="sxs-lookup"><span data-stu-id="b69ac-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Azure yerel çalışma zamanı](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="b69ac-138">Merhaba HTTP isteği Hello URL'sini tarayıcınızın adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b69ac-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="b69ac-139">Merhaba sorgu dizesi eklemek `&name=<yourname>` toothis URL ve hello istek yürütülemiyor.</span><span class="sxs-lookup"><span data-stu-id="b69ac-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="b69ac-140">Merhaba aşağıdaki hello yanıt hello işlevi tarafından döndürülen hello tarayıcı toohello yerel GET isteğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="b69ac-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Merhaba tarayıcıda işlev localhost yanıtı](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="b69ac-142">hata ayıklama, toostop tıklatın hello **durdurmak** hello Visual Studio araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="b69ac-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="b69ac-143">Hello işlevi, yerel bilgisayarınızda düzgün çalıştığını doğruladıktan sonra zaman toopublish hello proje tooAzure olur.</span><span class="sxs-lookup"><span data-stu-id="b69ac-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="b69ac-144">Yayımlama Hello proje tooAzure</span><span class="sxs-lookup"><span data-stu-id="b69ac-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="b69ac-145">Projenizi yayımlayabilmeniz için önce Azure aboneliğinizde bir işlev uygulamanızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b69ac-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="b69ac-146">Visual Studio'dan bir işlev uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b69ac-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="b69ac-147">Azure'da işlevinizi test etme</span><span class="sxs-lookup"><span data-stu-id="b69ac-147">Test your function in Azure</span></span>

1. <span data-ttu-id="b69ac-148">Merhaba işlevi uygulamasının temel URL'si Hello hello yayımlama profili sayfadan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b69ac-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="b69ac-149">Hello yerine `localhost:port` hello işlevi hello yeni temel URL ile yerel olarak test edilirken kullanılan hello URL'sinin.</span><span class="sxs-lookup"><span data-stu-id="b69ac-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="b69ac-150">Önceki gibi emin tooappend hello sorgu dizesi yapmak `&name=<yourname>` toothis URL ve hello istek yürütülemiyor.</span><span class="sxs-lookup"><span data-stu-id="b69ac-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="b69ac-151">Bu işlev görülüyor, HTTP çağrıları hello URL tetiklenen:</span><span class="sxs-lookup"><span data-stu-id="b69ac-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="b69ac-152">Bu yeni URL hello HTTP isteği için tarayıcınızın adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b69ac-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="b69ac-153">Merhaba aşağıdaki hello yanıt hello işlevi tarafından döndürülen hello tarayıcı toohello uzak GET isteğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="b69ac-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Merhaba tarayıcıda işlev yanıtı](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="b69ac-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b69ac-155">Next steps</span></span>

<span data-ttu-id="b69ac-156">Visual Studio toocreate C# işlev uygulaması basit bir HTTP tetiklenen işleviyle kullandınız.</span><span class="sxs-lookup"><span data-stu-id="b69ac-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="b69ac-157">toolearn nasıl tooconfigure proje toosupport Tetikleyicileri ve bağlamaları, diğer türlerini görmek hello [yapılandırma hello proje yerel geliştirme için](functions-develop-vs.md#configure-the-project-for-local-development) bölümüne [Visual Studio için Azure işlevleri Araçları](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="b69ac-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="b69ac-158">Yerel test ve hello Azure işlevleri çekirdek araçlarını kullanarak hata ayıklama hakkında daha fazla toolearn bkz [koduna ve test Azure işlevleri yerel olarak](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="b69ac-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="b69ac-159">.NET sınıf kitaplıkları işlevleri geliştirme hakkında daha fazla toolearn bkz [Azure işlevlerini kullanarak .NET sınıf kitaplıkları](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="b69ac-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

