---
title: "Azure Machine Learning Web Hizmetleri: Dağıtım ve kullanım | Microsoft Docs"
description: "Dağıtma ve web hizmetlerini tüketen kaynaklar."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="e5450-103">Azure Machine Learning Web Hizmetleri: Dağıtım ve kullanım</span><span class="sxs-lookup"><span data-stu-id="e5450-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="e5450-104">Machine learning iş akışları ve modelleri web Hizmetleri olarak dağıtmak için Azure Machine Learning'ı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5450-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="e5450-105">Bu web Hizmetleri, tahminlerin gerçek zamanlı veya toplu iş modunda yapmak için Internet üzerinden uygulamalardan machine learning modellerini çağrılacak sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e5450-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="e5450-106">Web hizmetleri RESTful olduğundan, bunları çeşitli programlama dillerini ve .NET ve Java gibi platformları ve Excel gibi uygulamalardan çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5450-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="e5450-107">Sonraki bölümlerde izlenecek yollar, kodu ve başlamanıza yardımcı olmak için belgeler için bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5450-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="e5450-108">Bir web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5450-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="e5450-109">Azure Machine Learning Studio ile</span><span class="sxs-lookup"><span data-stu-id="e5450-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="e5450-110">Machine Learning Studio ve Microsoft Azure Machine Learning Web Hizmetleri Portalı'nı dağıtma ve bir web hizmeti kod yazmadan yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e5450-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="e5450-111">Aşağıdaki bağlantılar, yeni bir web hizmetini dağıtma hakkında genel bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="e5450-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="e5450-112">Azure Resource Manager tabanlı yeni bir web hizmetini dağıtma hakkında bir genel bakış için bkz: [yeni bir web hizmetini dağıtma](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e5450-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="e5450-113">Bir web hizmeti dağıtma hakkında bir kılavuz için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e5450-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="e5450-114">Oluşturma ve bir web hizmetini dağıtma hakkında tam bir anlatım için bkz: [gözden geçirme adım 1: Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="e5450-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="e5450-115">Bir web hizmetini dağıtma belirli örnekler için bkz:</span><span class="sxs-lookup"><span data-stu-id="e5450-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="e5450-116">İzlenecek yol 5. adım: Azure Machine Learning web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5450-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="e5450-117">Bir web hizmeti için birden çok bölgeye dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5450-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="e5450-118">Web Hizmetleri kaynak sağlayıcı API'leri (Azure Resource Manager API'leri)</span><span class="sxs-lookup"><span data-stu-id="e5450-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="e5450-119">Web hizmetleri için Azure Machine Learning kaynak sağlayıcısı REST API çağrısı kullanarak dağıtım ve Yönetim web hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5450-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="e5450-120">Daha fazla bilgi için bkz: [Machine Learning Web hizmeti (REST)](/rest/api/machinelearning/index) başvurusu.</span><span class="sxs-lookup"><span data-stu-id="e5450-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="e5450-121">PowerShell cmdlet'leri ile</span><span class="sxs-lookup"><span data-stu-id="e5450-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="e5450-122">Azure Machine Learning kaynak sağlayıcısı web hizmetleri için dağıtım ve Yönetim web hizmetleri PowerShell cmdlet'lerini kullanarak etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="e5450-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="e5450-123">Cmdlet'lerini kullanmak için ilk kez Azure hesabınızdan PowerShell ortamında kullanarak oturum gerekir [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e5450-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="e5450-124">Resource Manager, temel alan PowerShell komutlarını nasıl bilginiz varsa bkz [Azure PowerShell kullanarak Azure Resource Manager ile](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="e5450-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="e5450-125">Tahmine dayalı denemenizi dışarı aktarmak için kullanın [Bu örnek kod](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="e5450-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="e5450-126">Koddan .exe dosyasını oluşturduktan sonra yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5450-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="e5450-127">Uygulama çalıştıran bir web hizmeti JSON şablonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5450-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="e5450-128">Bir web hizmeti dağıtmak için şablon kullanmak için aşağıdaki bilgileri eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5450-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="e5450-129">Depolama hesabı adı ve anahtar</span><span class="sxs-lookup"><span data-stu-id="e5450-129">Storage account name and key</span></span>

    <span data-ttu-id="e5450-130">Depolama hesabı adı ve anahtar herhangi birinden alabilirsiniz [Azure portal](https://portal.azure.com/) veya [Klasik Azure portalı](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5450-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="e5450-131">Taahhüt plan kimliği</span><span class="sxs-lookup"><span data-stu-id="e5450-131">Commitment plan ID</span></span>

    <span data-ttu-id="e5450-132">Plan Kimliğinden alabilirsiniz [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) oturum açma ve bir plan adı tıklatarak portal.</span><span class="sxs-lookup"><span data-stu-id="e5450-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="e5450-133">JSON şablonunu alt olarak eklemediğiniz *özellikleri* düğüm aynı düzeyde *MachineLearningWorkspace* düğümü.</span><span class="sxs-lookup"><span data-stu-id="e5450-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="e5450-134">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e5450-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="e5450-135">Daha fazla ayrıntı için örnek kod ve aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="e5450-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="e5450-136">[Azure Machine Learning cmdlet'lerini](https://msdn.microsoft.com/library/azure/mt767952.aspx) MSDN'de başvurusu</span><span class="sxs-lookup"><span data-stu-id="e5450-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="e5450-137">Örnek [izlenecek](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) github'da</span><span class="sxs-lookup"><span data-stu-id="e5450-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="e5450-138">Web hizmetlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="e5450-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="e5450-139">Azure Machine Learning Web Hizmetleri kullanıcı Arabirimi (test)</span><span class="sxs-lookup"><span data-stu-id="e5450-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="e5450-140">Azure Machine Learning Web Hizmetleri portalında web hizmetiniz test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5450-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="e5450-141">Bu istek-yanıt hizmeti (RRS) sınama içerir ve toplu yürütme hizmeti (BES) arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="e5450-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="e5450-142">Yeni bir web hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5450-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="e5450-143">Bir Azure Machine Learning web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5450-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="e5450-144">İzlenecek yol 5. adım: Azure Machine Learning web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5450-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="e5450-145">Excel'den</span><span class="sxs-lookup"><span data-stu-id="e5450-145">From Excel</span></span>
<span data-ttu-id="e5450-146">Web hizmeti tüketen Excel şablonunu indirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5450-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="e5450-147">Bir Azure Machine Learning web hizmetini Excel'den kullanma</span><span class="sxs-lookup"><span data-stu-id="e5450-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="e5450-148">Azure Machine Learning Web Hizmetleri için Excel Eklentisi</span><span class="sxs-lookup"><span data-stu-id="e5450-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="e5450-149">REST tabanlı bir istemciden</span><span class="sxs-lookup"><span data-stu-id="e5450-149">From a REST-based client</span></span>
<span data-ttu-id="e5450-150">Azure Machine Learning Web Hizmetleri RESTful API'lerini ' dir.</span><span class="sxs-lookup"><span data-stu-id="e5450-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="e5450-151">.NET, Python, R, Java, vb. gibi çeşitli platformlarda bu API'lerden kullanabilir. **Tüket** sayfasında web hizmetiniz için [Microsoft Azure Machine Learning Web Hizmetleri portalı](https://services.azureml.net) başlamanıza yardımcı olabilecek örnek koduna sahip.</span><span class="sxs-lookup"><span data-stu-id="e5450-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="e5450-152">Daha fazla bilgi için bkz. [Azure Machine Learning web hizmetini kullanma](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e5450-152">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
