---
title: "aaaCreating yönetim çözümleri Operations Management Suite (OMS) | Microsoft Docs"
description: "Yönetim çözümleri genişletmek hello işlevselliği Operations Management Suite (OMS) paketlenmiş yönetim senaryoları sağlayarak müşteriler tootheir OMS çalışma ekleyebilirsiniz.  Bu makalede, yönetim çözümleri toobe nasıl oluşturabileceğinizi Ayrıntılar, kendi ortamınızda kullanılan veya kullanılabilir tooyour müşteriler yapılan sağlar."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="575fa-104">Operations Management Suite (OMS) (Önizleme) bir yönetim çözümü dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="575fa-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="575fa-105">Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir.</span><span class="sxs-lookup"><span data-stu-id="575fa-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="575fa-106">Aşağıda açıklanan herhangi bir şema konu toochange ' dir.</span><span class="sxs-lookup"><span data-stu-id="575fa-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="575fa-107">Yönetim çözümleri Operations Management Suite (OMS) olarak uygulanır [Resource Manager şablonları](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="575fa-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="575fa-108">Merhaba ana görev nasıl tooauthor yönetim çözümleri öğrenme nasıl çok öğrenmek[şablon Yazar](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="575fa-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="575fa-109">Bu makale şablonları çözümleri için kullanılan benzersiz ayrıntılarını sağlar ve nasıl tooconfigure tipik çözüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="575fa-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="575fa-110">Araçlar</span><span class="sxs-lookup"><span data-stu-id="575fa-110">Tools</span></span>

<span data-ttu-id="575fa-111">Çözüm dosyalarını bir metin düzenleyicisi toowork kullanabilirsiniz, ancak Visual Studio veya Visual Studio Code makaleler hello açıklandığı gibi sağlanan hello özellikleri yararlanarak öneririz.</span><span class="sxs-lookup"><span data-stu-id="575fa-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="575fa-112">Oluşturma ve Visual Studio üzerinden Azure kaynak gruplarını dağıtma</span><span class="sxs-lookup"><span data-stu-id="575fa-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="575fa-113">Visual Studio code'da Azure Resource Manager şablonları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="575fa-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="575fa-114">yapısı</span><span class="sxs-lookup"><span data-stu-id="575fa-114">Structure</span></span>
<span data-ttu-id="575fa-115">bir yönetim çözümü dosyasının temel yapısı Hello aynı hello olan bir [Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md#template-format) olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="575fa-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="575fa-116">Her biri aşağıdaki hello bölümler hello en üst düzey öğeleri açıklar ve ve içerikleri bir çözümde.</span><span class="sxs-lookup"><span data-stu-id="575fa-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="575fa-117">Parametreler</span><span class="sxs-lookup"><span data-stu-id="575fa-117">Parameters</span></span>
<span data-ttu-id="575fa-118">[Parametreleri](../azure-resource-manager/resource-group-authoring-templates.md#parameters) hello yönetim çözümü yükleyen hello kullanıcının gerektiren değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="575fa-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="575fa-119">Tüm çözümleri olan standart parametreler vardır ve ek parametreler gerektiği gibi belirli çözümünüz için ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="575fa-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="575fa-120">Çözümünüzü yüklediğinizde kullanıcılar parametre değerlerini nasıl sağlayacak hello belirli parametre ve hello çözümü nasıl yüklendiği değişir.</span><span class="sxs-lookup"><span data-stu-id="575fa-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="575fa-121">Kullanıcı Yönetimi çözümünüzü hello aracılığıyla yüklendiğinde [Azure Marketi](operations-management-suite-solutions.md#finding-and-installing-management-solutions) veya [Azure hızlı başlangıç şablonlarını](operations-management-suite-solutions.md#finding-and-installing-management-solutions) istendiğinde tooselect oldukları bir [OMS çalışma ve Automation hesabı ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="575fa-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="575fa-122">Bunlar kullanılan toopopulate hello her hello standart parametrelerinin değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="575fa-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="575fa-123">Merhaba kullanıcı istenmedi toodirectly hello standart parametreler için değerler sağlayın, ancak bunlar istendiğinde tooprovide ek parametreler değerler.</span><span class="sxs-lookup"><span data-stu-id="575fa-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="575fa-124">Merhaba kullanıcı çözümünüzü yüklendiğinde [başka bir yöntem](operations-management-suite-solutions.md#finding-and-installing-management-solutions), tüm standart parametreleri ve tüm ek parametreleri için bir değer girmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="575fa-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="575fa-125">Bir örnek parametre aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="575fa-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="575fa-126">Aşağıdaki tablonun hello parametresinin hello öznitelikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="575fa-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="575fa-127">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="575fa-127">Attribute</span></span> | <span data-ttu-id="575fa-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="575fa-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="575fa-129">type</span><span class="sxs-lookup"><span data-stu-id="575fa-129">type</span></span> |<span data-ttu-id="575fa-130">Merhaba parametresinin veri türü.</span><span class="sxs-lookup"><span data-stu-id="575fa-130">Data type for hello parameter.</span></span> <span data-ttu-id="575fa-131">Merhaba giriş denetiminin Hello kullanıcı için görüntülenen hello veri türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="575fa-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="575fa-132">bool - açılan kutuya</span><span class="sxs-lookup"><span data-stu-id="575fa-132">bool - Drop down box</span></span><br><span data-ttu-id="575fa-133">String - metin kutusu</span><span class="sxs-lookup"><span data-stu-id="575fa-133">string - Text box</span></span><br><span data-ttu-id="575fa-134">int - metin kutusu</span><span class="sxs-lookup"><span data-stu-id="575fa-134">int - Text box</span></span><br><span data-ttu-id="575fa-135">SecureString - parola alanı</span><span class="sxs-lookup"><span data-stu-id="575fa-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="575fa-136">category</span><span class="sxs-lookup"><span data-stu-id="575fa-136">category</span></span> |<span data-ttu-id="575fa-137">Merhaba parametresi için isteğe bağlı kategorisi.</span><span class="sxs-lookup"><span data-stu-id="575fa-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="575fa-138">Aynı kategoride birlikte gruplandırılır hello parametreleri.</span><span class="sxs-lookup"><span data-stu-id="575fa-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="575fa-139">denetimi</span><span class="sxs-lookup"><span data-stu-id="575fa-139">control</span></span> |<span data-ttu-id="575fa-140">Ek işlevsellik dizesi parametreleri için.</span><span class="sxs-lookup"><span data-stu-id="575fa-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="575fa-141">DateTime - Datetime denetim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="575fa-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="575fa-142">GUID - GUID değeri otomatik olarak oluşturulur ve hello parametre görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="575fa-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="575fa-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="575fa-143">description</span></span> |<span data-ttu-id="575fa-144">Merhaba parametresi için isteğe bağlı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="575fa-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="575fa-145">Bir bilgi balonu sonraki toohello parametresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="575fa-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="575fa-146">Standart Parametreler</span><span class="sxs-lookup"><span data-stu-id="575fa-146">Standard parameters</span></span>
<span data-ttu-id="575fa-147">Merhaba aşağıdaki tabloda tüm yönetim çözümleri için hello standart parametreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="575fa-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="575fa-148">Bu değerleri çözümünüzü hello Azure Marketi veya hızlı başlangıç şablonlarından yüklendiğinde yerine bunların istenmesi hello kullanıcı için doldurulur.</span><span class="sxs-lookup"><span data-stu-id="575fa-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="575fa-149">Merhaba çözüm başka bir yöntemle yüklediyseniz hello kullanıcı bunlar için değer sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="575fa-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="575fa-150">Merhaba kullanıcı arabirimi hello Azure Marketi ve hızlı başlangıç şablonlarında hello parametre adları hello tabloda bekliyor.</span><span class="sxs-lookup"><span data-stu-id="575fa-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="575fa-151">Farklı parametre adları kullanırsanız, ardından hello kullanıcı bunlar için istenir ve bunların değil otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="575fa-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="575fa-152">Parametre</span><span class="sxs-lookup"><span data-stu-id="575fa-152">Parameter</span></span> | <span data-ttu-id="575fa-153">Tür</span><span class="sxs-lookup"><span data-stu-id="575fa-153">Type</span></span> | <span data-ttu-id="575fa-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="575fa-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="575fa-155">accountName</span><span class="sxs-lookup"><span data-stu-id="575fa-155">accountName</span></span> |<span data-ttu-id="575fa-156">Dize</span><span class="sxs-lookup"><span data-stu-id="575fa-156">string</span></span> |<span data-ttu-id="575fa-157">Azure Otomasyon hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="575fa-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="575fa-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="575fa-158">pricingTier</span></span> |<span data-ttu-id="575fa-159">Dize</span><span class="sxs-lookup"><span data-stu-id="575fa-159">string</span></span> |<span data-ttu-id="575fa-160">Hem günlük analizi çalışma alanı hem de Azure Otomasyonu hesabı fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="575fa-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="575fa-161">RegionID</span><span class="sxs-lookup"><span data-stu-id="575fa-161">regionId</span></span> |<span data-ttu-id="575fa-162">Dize</span><span class="sxs-lookup"><span data-stu-id="575fa-162">string</span></span> |<span data-ttu-id="575fa-163">Hello Azure Automation hesabı bölgesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="575fa-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="575fa-164">solutionName</span></span> |<span data-ttu-id="575fa-165">Dize</span><span class="sxs-lookup"><span data-stu-id="575fa-165">string</span></span> |<span data-ttu-id="575fa-166">Merhaba çözüm adı.</span><span class="sxs-lookup"><span data-stu-id="575fa-166">Name of hello solution.</span></span>  <span data-ttu-id="575fa-167">Çözümünüzü hızlı başlangıç şablonlarıyla dağıtıyorsanız, bunun yerine hello kullanıcı toospecify bir gerektiren bir dize tanımlamak için daha sonra solutionName parametre olarak tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="575fa-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="575fa-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="575fa-168">workspaceName</span></span> |<span data-ttu-id="575fa-169">Dize</span><span class="sxs-lookup"><span data-stu-id="575fa-169">string</span></span> |<span data-ttu-id="575fa-170">Günlük analizi çalışma alanı adı.</span><span class="sxs-lookup"><span data-stu-id="575fa-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="575fa-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="575fa-171">workspaceRegionId</span></span> |<span data-ttu-id="575fa-172">Dize</span><span class="sxs-lookup"><span data-stu-id="575fa-172">string</span></span> |<span data-ttu-id="575fa-173">Merhaba günlük analizi çalışma alanı bölgesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="575fa-174">Aşağıda, çözüm dosyanıza kopyalayıp hello standart parametreleri hello yapısıdır.</span><span class="sxs-lookup"><span data-stu-id="575fa-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="575fa-175">Merhaba sözdizimi ile Merhaba çözümün diğer öğeleri tooparameter değerleri bkz **parametreleri ('parametre adı')**.</span><span class="sxs-lookup"><span data-stu-id="575fa-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="575fa-176">Örneğin, tooaccess Merhaba çalışma alanı adı, kullanacağınız **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="575fa-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="575fa-177">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="575fa-177">Variables</span></span>
<span data-ttu-id="575fa-178">[Değişkenleri](../azure-resource-manager/resource-group-authoring-templates.md#variables) hello Yönetimi çözümünün hello kalan kullanacağınız değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="575fa-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="575fa-179">Bu değerleri hello çözüm yükleme gösterilen toohello kullanıcı olmayan.</span><span class="sxs-lookup"><span data-stu-id="575fa-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="575fa-180">Hedeflenen tooprovide hello Yazar birden çok kez hello çözüm kullanılabilir değerler yönetebileceği tek bir konuma sahip oldukları.</span><span class="sxs-lookup"><span data-stu-id="575fa-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="575fa-181">Hello kodlama karşılıklı toohard olarak değişkenleri herhangi bir değer belirli tooyour çözümü yerleştirileceği **kaynakları** öğesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="575fa-182">Bu hello kodunu daha okunabilir hale getirir ve sağlar tooeasily sonraki sürümlerinde bu değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="575fa-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="575fa-183">Aşağıdaki örneği verilmiştir bir **değişkenleri** çözümlerinde kullanılan tipik parametrelerle öğesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="575fa-184">Merhaba sözdizimi ile Merhaba çözüm aracılığıyla toovariable değerleri bkz **değişkenleri ('değişkeni')**.</span><span class="sxs-lookup"><span data-stu-id="575fa-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="575fa-185">Örneğin, tooaccess Merhaba SolutionName değişkeni, kullanacağınız **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="575fa-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="575fa-186">Ayrıca, karmaşık değişkenleri tanımlayabilirsiniz, birden çok değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="575fa-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="575fa-187">Burada farklı türdeki kaynakların için birden çok özellik tanımlama bu yönetim çözümlerine özellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="575fa-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="575fa-188">Örneğin, yukarıda toohello aşağıda gösterilen hello çözüm değişkenleri yapılandırmayı.</span><span class="sxs-lookup"><span data-stu-id="575fa-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="575fa-189">Bu durumda, hello sözdizimi hello çözümüyle toovariable değerlerini başvurmak **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="575fa-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="575fa-190">Örneğin, tooaccess Merhaba çözüm adı değişkeni, kullanacağınız **variables('Solution'). Ad**.</span><span class="sxs-lookup"><span data-stu-id="575fa-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="575fa-191">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="575fa-191">Resources</span></span>
<span data-ttu-id="575fa-192">[Kaynakları](../azure-resource-manager/resource-group-authoring-templates.md#resources) Yönetimi çözümünüzü yükleyecekleri ve yapılandıracakları hello farklı kaynakları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="575fa-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="575fa-193">Bu hello en büyük ve en karmaşık hello şablonu kısmı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="575fa-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="575fa-194">Merhaba yapısı ve kaynak öğelerinde eksiksiz bir açıklaması alabilirsiniz [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="575fa-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="575fa-195">Genellikle tanımlayacaksınız farklı kaynaklar bu belgede diğer makalelerinde ayrıntılı olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="575fa-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="575fa-196">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="575fa-196">Dependencies</span></span>
<span data-ttu-id="575fa-197">Merhaba **dependsOn** öğeleri belirten bir [bağımlılık](../azure-resource-manager/resource-group-define-dependencies.md) başka bir kaynak üzerinde.</span><span class="sxs-lookup"><span data-stu-id="575fa-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="575fa-198">Merhaba çözüm yüklendiğinde, tüm bağımlılıkları oluşturulmuş kadar kaynak oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="575fa-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="575fa-199">Örneğin, çözümünüzü olabilir [bir runbook başlatın](operations-management-suite-solutions-resources-automation.md#runbooks) kullanarak yüklendiğinde bir [işi kaynak](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="575fa-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="575fa-200">Merhaba iş kaynak hello runbook kaynak toomake üzerinde hello iş oluşturulmadan önce bu hello runbook oluşturulduğundan emin bağımlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="575fa-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="575fa-201">OMS çalışma ve Automation hesabı</span><span class="sxs-lookup"><span data-stu-id="575fa-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="575fa-202">Yönetim çözümleri gerektiren bir [OMS çalışma](../log-analytics/log-analytics-manage-access.md) toocontain görünümleri ve bir [Otomasyon hesabı](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook'ları ve ilgili kaynakları.</span><span class="sxs-lookup"><span data-stu-id="575fa-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="575fa-203">Bu kaynaklar hello çözümde oluşturulur ve hello çözümüne kendisi tanımlanmamalıdır hello önce kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="575fa-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="575fa-204">Merhaba kullanıcı [çalışma ve hesabı belirtin](operations-management-suite-solutions.md#oms-workspace-and-automation-account) zaman çözümünüzü dağıtmak, ancak hello yazarı olarak hello aşağıdaki noktaları göz önünde bulundurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="575fa-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="575fa-205">Çözüm kaynağı</span><span class="sxs-lookup"><span data-stu-id="575fa-205">Solution resource</span></span>
<span data-ttu-id="575fa-206">Her çözüm hello kaynak girişi gerektirir **kaynakları** hello çözümü kendisini tanımlar öğesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="575fa-207">Bu bir türü olacak **Microsoft.OperationsManagement/solutions** ve yapı izlenerek hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="575fa-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="575fa-208">Bu içerir [standart parametreler](#parameters) ve [değişkenleri](#variables) hello çözüm özelliklerini genellikle kullanılan toodefine olan.</span><span class="sxs-lookup"><span data-stu-id="575fa-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="575fa-209">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="575fa-209">Dependencies</span></span>
<span data-ttu-id="575fa-210">Merhaba çözüm kaynağı olmalıdır bir [bağımlılık](../azure-resource-manager/resource-group-define-dependencies.md) hello çözüm oluşturulmadan önce tooexist gerektiğinden hello çözümdeki her bir kaynak üzerinde.</span><span class="sxs-lookup"><span data-stu-id="575fa-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="575fa-211">Her kaynak için bir giriş hello ekleyerek bunu **dependsOn** öğesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="575fa-212">Özellikler</span><span class="sxs-lookup"><span data-stu-id="575fa-212">Properties</span></span>
<span data-ttu-id="575fa-213">Merhaba çözüm kaynak tablosu aşağıdaki hello hello özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="575fa-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="575fa-214">Bu, başvurulan ve hello çözüm yüklendikten sonra hello kaynak nasıl yönetildiğini tanımlar hello çözümü tarafından bulunan hello kaynakları içerir.</span><span class="sxs-lookup"><span data-stu-id="575fa-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="575fa-215">Merhaba çözümdeki her bir kaynağın her iki hello listelenmelidir **referencedResources** veya hello **containedResources** özelliği.</span><span class="sxs-lookup"><span data-stu-id="575fa-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="575fa-216">Özellik</span><span class="sxs-lookup"><span data-stu-id="575fa-216">Property</span></span> | <span data-ttu-id="575fa-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="575fa-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="575fa-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="575fa-218">workspaceResourceId</span></span> |<span data-ttu-id="575fa-219">Merhaba formunda hello günlük analizi çalışma alanı kimliği * <Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<çalışma alanı adı\>*.</span><span class="sxs-lookup"><span data-stu-id="575fa-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="575fa-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="575fa-220">referencedResources</span></span> |<span data-ttu-id="575fa-221">Merhaba çözüm kaldırıldığında kaldırılmamalıdır hello çözümü kaynaklarında listesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="575fa-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="575fa-222">containedResources</span></span> |<span data-ttu-id="575fa-223">Merhaba çözüm kaldırıldığında kaldırılmalıdır hello çözümü kaynaklarında listesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="575fa-224">bir runbook, zamanlama ve görünüm ile bir çözüm için yukarıdaki Hello örnek verilebilir.</span><span class="sxs-lookup"><span data-stu-id="575fa-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="575fa-225">Merhaba zamanlama ve runbook *başvurulan* hello içinde **özellikleri** hello çözüm kaldırıldığında bunlar kaldırılmaz şekilde öğesi.</span><span class="sxs-lookup"><span data-stu-id="575fa-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="575fa-226">Merhaba görünümdür *bulunan* hello çözüm kaldırıldığında kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="575fa-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="575fa-227">Planlama</span><span class="sxs-lookup"><span data-stu-id="575fa-227">Plan</span></span>
<span data-ttu-id="575fa-228">Merhaba **planı** hello çözüm kaynak varlığı aşağıdaki tablonun hello hello özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="575fa-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="575fa-229">Özellik</span><span class="sxs-lookup"><span data-stu-id="575fa-229">Property</span></span> | <span data-ttu-id="575fa-230">Açıklama</span><span class="sxs-lookup"><span data-stu-id="575fa-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="575fa-231">ad</span><span class="sxs-lookup"><span data-stu-id="575fa-231">name</span></span> |<span data-ttu-id="575fa-232">Merhaba çözüm adı.</span><span class="sxs-lookup"><span data-stu-id="575fa-232">Name of hello solution.</span></span> |
| <span data-ttu-id="575fa-233">Sürüm</span><span class="sxs-lookup"><span data-stu-id="575fa-233">version</span></span> |<span data-ttu-id="575fa-234">Merhaba yazar tarafından belirlendiği şekilde hello çözümü sürümü.</span><span class="sxs-lookup"><span data-stu-id="575fa-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="575fa-235">Ürün</span><span class="sxs-lookup"><span data-stu-id="575fa-235">product</span></span> |<span data-ttu-id="575fa-236">Benzersiz bir dize tooidentify hello çözümü.</span><span class="sxs-lookup"><span data-stu-id="575fa-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="575fa-237">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="575fa-237">publisher</span></span> |<span data-ttu-id="575fa-238">Merhaba Çözüm Yayımcısı.</span><span class="sxs-lookup"><span data-stu-id="575fa-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="575fa-239">Örnek</span><span class="sxs-lookup"><span data-stu-id="575fa-239">Sample</span></span>
<span data-ttu-id="575fa-240">Aşağıdaki konumlardan hello çözüm dosyalarını bir çözüm kaynakla örnekleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="575fa-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="575fa-241">Otomasyon kaynakları</span><span class="sxs-lookup"><span data-stu-id="575fa-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="575fa-242">Arama ve uyarı kaynakları</span><span class="sxs-lookup"><span data-stu-id="575fa-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="575fa-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="575fa-243">Next steps</span></span>
* <span data-ttu-id="575fa-244">[Kaydedilmiş aramaları ve Uyarıları Ekle](operations-management-suite-solutions-resources-searches-alerts.md) tooyour yönetim çözümü.</span><span class="sxs-lookup"><span data-stu-id="575fa-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="575fa-245">[Görünümler ekleme](operations-management-suite-solutions-resources-views.md) tooyour yönetim çözümü.</span><span class="sxs-lookup"><span data-stu-id="575fa-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="575fa-246">[Runbook'ları ve diğer Automation kaynaklarına eklemek](operations-management-suite-solutions-resources-automation.md) tooyour yönetim çözümü.</span><span class="sxs-lookup"><span data-stu-id="575fa-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="575fa-247">Merhaba ayrıntılarını öğrenmek [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="575fa-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="575fa-248">Arama [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates) farklı Resource Manager şablonları örneklerini için.</span><span class="sxs-lookup"><span data-stu-id="575fa-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
