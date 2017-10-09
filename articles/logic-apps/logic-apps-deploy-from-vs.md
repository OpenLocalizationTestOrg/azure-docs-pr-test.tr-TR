---
title: "aaaCreate, derleme ve logic apps Visual Studio - Azure mantıksal uygulamaları dağıtma | Microsoft Docs"
description: "Tasarlama, derleme ve Azure mantıksal uygulamaları dağıtmak için Visual Studio projeleri oluşturma."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="48069-103">Tasarım, derleme ve Visual Studio'daki Azure mantıksal uygulamaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="48069-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="48069-104">Merhaba rağmen [Azure portal](https://portal.azure.com/) toocreate sizin için harika bir yol sunar ve Azure mantıksal uygulamaları yönetmek için Visual Studio tasarlamayı, derlemeyi ve mantıksal uygulamalarınızı dağıtma için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48069-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="48069-105">Visual Studio hello mantığı Uygulama Tasarımcısı gibi zengin araçları sizin için toocreate logic apps sağlar, dağıtım ve Otomasyon şablonları yapılandırın ve tooany ortamı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="48069-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="48069-106">Azure Logic Apps ile başlatılan tooget öğrenin [nasıl toocreate ilk mantıksal uygulamanızı hello Azure portal](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="48069-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="48069-107">Yükleme adımları</span><span class="sxs-lookup"><span data-stu-id="48069-107">Installation steps</span></span>

<span data-ttu-id="48069-108">tooinstall ve Visual Studio Araçları Azure mantıksal uygulamaları için yapılandırmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="48069-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="48069-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="48069-109">Prerequisites</span></span>

* <span data-ttu-id="48069-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) veya Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="48069-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="48069-111">[En son Azure SDK'sı](https://azure.microsoft.com/downloads/) (2.9.1 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="48069-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="48069-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="48069-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="48069-113">Merhaba katıştırılmış Tasarımcısı kullanırken erişim toohello web</span><span class="sxs-lookup"><span data-stu-id="48069-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="48069-114">Azure mantıksal uygulamaları için Visual Studio araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="48069-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="48069-115">Merhaba önkoşulları yüklendikten sonra:</span><span class="sxs-lookup"><span data-stu-id="48069-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="48069-116">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="48069-116">Open Visual Studio.</span></span> <span data-ttu-id="48069-117">Merhaba üzerinde **Araçları** menüsünde, select **Uzantılar ve güncelleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="48069-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="48069-118">Merhaba genişletin **çevrimiçi** çevrimiçi arama yapabilmeniz için kategori.</span><span class="sxs-lookup"><span data-stu-id="48069-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="48069-119">Göz atın veya arayın **Logic Apps** bulana kadar **Visual Studio için Azure Logic Apps Araçları**.</span><span class="sxs-lookup"><span data-stu-id="48069-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="48069-120">toodownload ve yükleme hello uzantısı,'ı **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="48069-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="48069-121">Yüklendikten sonra Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="48069-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="48069-122">Ayrıca indirebilirsiniz [Azure Logic Apps araçları Visual Studio 2017 için](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) ve hello [Visual Studio 2015 için Azure Logic Apps Araçları](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) hello Visual Studio Market'te doğrudan.</span><span class="sxs-lookup"><span data-stu-id="48069-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="48069-123">Yükleme işlemini tamamlandığınızda hello Azure kaynak grubu projesi mantığı uygulama tasarımcı ile birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48069-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="48069-124">Projenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="48069-124">Create your project</span></span>

1. <span data-ttu-id="48069-125">Merhaba üzerinde **dosya** menüsünde çok Git**yeni**seçip **proje**.</span><span class="sxs-lookup"><span data-stu-id="48069-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="48069-126">Veya tooadd çözüm, Git çok varolan, proje tooan**Ekle**seçip **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="48069-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![Dosya menüsü](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="48069-128">Merhaba, **yeni proje** penceresinde Bul **bulut**seçip **Azure kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="48069-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="48069-129">Projenizi adlandırın ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="48069-129">Name your project, and click **OK**.</span></span>

    ![Yeni Proje Ekle](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="48069-131">Select hello **mantıksal uygulama** boş mantığı uygulama dağıtım şablonu toouse sizin için oluşturduğu şablonu.</span><span class="sxs-lookup"><span data-stu-id="48069-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="48069-132">Şablonunuzu seçtikten sonra tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="48069-132">After you select your template, click **OK**.</span></span>

    ![Mantıksal uygulama şablonu seçin](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="48069-134">Şimdi mantıksal uygulama projesi tooyour çözümünüzü ekledik.</span><span class="sxs-lookup"><span data-stu-id="48069-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="48069-135">Hello Çözüm Gezgini, dağıtım dosyanızı görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="48069-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![Dağıtım dosyası](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="48069-137">Mantıksal uygulamanızı mantığı Uygulama Tasarımcısı ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="48069-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="48069-138">Bir mantıksal uygulama içeren bir Azure kaynak grubu projesi sahip olduğunuzda, iş akışınızı Visual Studio toocreate hello mantığı Uygulama Tasarımcısı açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48069-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="48069-139">internet bağlantısı çok bağlayıcıları kullanılabilir özellikler ve veri için sorgu Hello Tasarımcısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="48069-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="48069-140">Örneğin, hello Dynamics CRM Online bağlayıcısını kullanırsanız, hello Tasarımcısı varsayılan özellikleri ve CRM örneği tooshow kullanılabilir özel sorgular.</span><span class="sxs-lookup"><span data-stu-id="48069-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="48069-141">Sağ tıklayın, `<template>.json` dosyasını bulun ve seçin **mantığı Uygulama Tasarımcısı ile Aç**.</span><span class="sxs-lookup"><span data-stu-id="48069-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="48069-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="48069-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="48069-143">Azure abonelik, kaynak grubunu ve konumu, dağıtım şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="48069-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="48069-144">Bir mantıksal uygulama tasarlama API bağlantı kaynaklarını özellikleri sorgu tasarımı sırasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48069-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="48069-145">Visual Studio tasarım sırasında bu bağlantılar, seçili kaynak grubu toocreate kullanır.</span><span class="sxs-lookup"><span data-stu-id="48069-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="48069-146">tooview veya herhangi bir API bağlantısı değiştirmek, toohello Azure portalına gidin ve göz **API bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="48069-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![Abonelik Seçici](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="48069-148">Merhaba Tasarımcısı kullanır hello tanımı hello `<template>.json` dosya oluşturma işlemi için.</span><span class="sxs-lookup"><span data-stu-id="48069-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="48069-149">Oluşturun ve mantıksal uygulamanızı tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="48069-149">Create and design your logic app.</span></span> <span data-ttu-id="48069-150">Dağıtım şablonu, yaptığınız değişikliklerle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="48069-150">Your deployment template is updated with your changes.</span></span>

    ![Visual Studio'da mantığı Uygulama Tasarımcısı](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="48069-152">Visual Studio ekler `Microsoft.Web/connections` kaynakları çok, kaynak dosya için herhangi bir bağlantısı toofunction mantıksal uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48069-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="48069-153">Bu bağlantı özellikleri ayarlanabilir dağıttığınızda ve içinde dağıttıktan sonra yönetilen **API bağlantıları** hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="48069-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="48069-154">TooJSON kod görünümüne geçin</span><span class="sxs-lookup"><span data-stu-id="48069-154">Switch tooJSON code view</span></span>

<span data-ttu-id="48069-155">tooshow hello mantıksal uygulamanızı seçin hello için JSON gösterimi **kod görünümü** hello Designer hello altındaki sekmesi.</span><span class="sxs-lookup"><span data-stu-id="48069-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="48069-156">tooswitch toohello tam kaynak JSON yeniden, hello sağ `<template>.json` dosyasını bulun ve seçin **açık**.</span><span class="sxs-lookup"><span data-stu-id="48069-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="48069-157">Bağımlı kaynaklarla tooVisual Studio dağıtım şablonları için başvuruları ekleme</span><span class="sxs-lookup"><span data-stu-id="48069-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="48069-158">Mantıksal uygulama tooreference bağımlı kaynaklarınızı istediğinizde kullanabilirsiniz [Azure Resource Manager şablonu işlevleri](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) mantığı uygulama dağıtım şablonunuzda.</span><span class="sxs-lookup"><span data-stu-id="48069-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="48069-159">Örneğin, mantıksal uygulama tooreference mantıksal uygulamanızı toodeploy istediğiniz bir Azure işlevi veya tümleştirme hesap isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48069-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="48069-160">Mantıksal Uygulama Tasarımcısı hello şekilde dağıtım şablonunuzu toouse parametrelerinde nasıl işlediğini doğru hakkında aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="48069-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="48069-161">Bu türden tetikleyiciler ve Eylemler mantığı uygulama parametreleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48069-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="48069-162">Alt iş akışı</span><span class="sxs-lookup"><span data-stu-id="48069-162">Child workflow</span></span>
*   <span data-ttu-id="48069-163">İşlev uygulaması</span><span class="sxs-lookup"><span data-stu-id="48069-163">Function app</span></span>
*   <span data-ttu-id="48069-164">APIM çağrısı</span><span class="sxs-lookup"><span data-stu-id="48069-164">APIM call</span></span>
*   <span data-ttu-id="48069-165">API bağlantı çalışma zamanı URL'si</span><span class="sxs-lookup"><span data-stu-id="48069-165">API connection runtime URL</span></span>
*   <span data-ttu-id="48069-166">API bağlantı yolu</span><span class="sxs-lookup"><span data-stu-id="48069-166">API connection path</span></span>

<span data-ttu-id="48069-167">Ve şablon işlevleri parametreleri, değişkenleri, ResourceId, concat vb. gibi kullanabilirsiniz. Örneğin, işte hello Azure işlevi kaynak kimliği nasıl değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48069-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="48069-168">Ve burada parametreleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48069-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="48069-169">Başka bir örnek olarak Service Bus Gönder ileti işlemi hello Parametreleştirme:</span><span class="sxs-lookup"><span data-stu-id="48069-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="48069-170">host.runtimeUrl isteğe bağlıdır ve varsa, şablondan kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="48069-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="48069-171">Örneğin parametrelerini kullandığınızda hello mantığı Uygulama Tasarımcısı toowork için varsayılan değer sağlamalısınız:</span><span class="sxs-lookup"><span data-stu-id="48069-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="48069-172">Mantıksal uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="48069-172">Save your logic app</span></span>

<span data-ttu-id="48069-173">toosave mantığı uygulamanızı dilediğiniz zaman, Git çok**dosya** > **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="48069-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="48069-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="48069-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="48069-175">Uygulamanızı kaydederken mantıksal uygulamanızı herhangi bir hata varsa, hello Visual Studio göründükleri **çıkışları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="48069-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="48069-176">Mantıksal uygulamanızı Visual Studio'dan dağıtma</span><span class="sxs-lookup"><span data-stu-id="48069-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="48069-177">Uygulamanızı yapılandırdıktan sonra yalnızca birkaç adımda Visual Studio doğrudan dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48069-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="48069-178">Çözüm Gezgini'nde, projenize sağ tıklayın ve çok Git**dağıtma** > **yeni dağıtım...**</span><span class="sxs-lookup"><span data-stu-id="48069-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![Yeni dağıtım](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="48069-180">İstendiğinde, tooyour Azure aboneliği oturum açın.</span><span class="sxs-lookup"><span data-stu-id="48069-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="48069-181">Şimdi mantıksal uygulamanızı toodeploy istediğiniz yere hello kaynak grubu için hello ayrıntıları seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="48069-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="48069-182">İşiniz bittiğinde seçin **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="48069-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="48069-183">Merhaba doğru şablonu ve parametre dosyası hello kaynak grubu için seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="48069-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="48069-184">Örneğin, toodeploy tooa üretim ortamına istiyorsanız hello üretim parametreler dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="48069-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Tooresource grubunu dağıtma](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="48069-186">Merhaba dağıtım durumu görünür hello **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="48069-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="48069-187">Tooselect olabilir **Azure sağlama** hello içinde **Göster çıktı** listesi.</span><span class="sxs-lookup"><span data-stu-id="48069-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![Dağıtım durumu çıktı](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="48069-189">Hello gelecekteki, mantıksal uygulamanızı kaynak denetiminde düzenleyin ve Visual Studio toodeploy yeni sürümlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="48069-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="48069-190">Hello Azure portal hello tanımında doğrudan değiştirirseniz, sonraki Visual Studio'dan dağıttığınızda bu değişikliklerin üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="48069-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="48069-191">Mantıksal uygulama tooan mevcut kaynak grubu projenizi ekleme</span><span class="sxs-lookup"><span data-stu-id="48069-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="48069-192">Varolan bir kaynak grubu projesi varsa, logic app toothat projenizi hello JSON ana hattı penceresinde ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48069-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="48069-193">Daha önce oluşturduğunuz hello uygulama yanında başka bir mantıksal uygulama da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48069-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="48069-194">Açık hello `<template>.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="48069-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="48069-195">JSON ana hattı penceresinin tooopen hello Git çok**Görünüm** > **diğer pencereler** > **JSON ana hattı**.</span><span class="sxs-lookup"><span data-stu-id="48069-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="48069-196">tooadd bir kaynak toohello şablon dosyası tıklatın **kaynak ekleme** hello JSON ana hattı penceresinin hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="48069-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="48069-197">Veya hello JSON ana hattı penceresinde sağ **kaynakları**seçip **yeni kaynak ekleme**.</span><span class="sxs-lookup"><span data-stu-id="48069-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![JSON ana hattı penceresinin](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="48069-199">Merhaba, **kaynak ekleme** iletişim kutusu bulun ve seçin, **mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="48069-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="48069-200">Mantıksal uygulamanızı adlandırın ve seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="48069-200">Name your logic app, and choose **Add**.</span></span>

    ![Kaynak Ekle](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="48069-202">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="48069-202">Next Steps</span></span>

* [<span data-ttu-id="48069-203">Logic apps Visual Studio Cloud Explorer ile yönetme</span><span class="sxs-lookup"><span data-stu-id="48069-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="48069-204">Sık rastlanan örnekleri ve senaryoları inceleyin</span><span class="sxs-lookup"><span data-stu-id="48069-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="48069-205">Tooautomate iş Azure Logic Apps ile nasıl işlediği öğrenin</span><span class="sxs-lookup"><span data-stu-id="48069-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="48069-206">Bilgi nasıl toointegrate sistemlerinizi Azure Logic Apps ile</span><span class="sxs-lookup"><span data-stu-id="48069-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
