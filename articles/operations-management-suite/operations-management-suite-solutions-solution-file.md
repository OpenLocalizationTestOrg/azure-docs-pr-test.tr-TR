---
title: "Operations Management Suite (OMS) yönetimi çözümleri oluşturma | Microsoft Docs"
description: "Yönetim çözümleri, müşterilerin kendi OMS çalışma alanına ekleyebilirsiniz paketlenmiş yönetim senaryoları sağlayarak Operations Management Suite (OMS) işlevselliği genişletir.  Bu makalede, kendi ortamınızda kullanılacak yönetim çözümleri nasıl oluşturabileceğinizi hakkında ayrıntılar sağlar veya müşterileriniz için kullanılabilir."
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
ms.openlocfilehash: ee3462c13101d18921dc488b08c79e1e4e02ff3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="73dc5-104">Operations Management Suite (OMS) (Önizleme) bir yönetim çözümü dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="73dc5-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="73dc5-105">Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="73dc5-106">Aşağıda açıklanan herhangi bir şema değiştirilebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-106">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="73dc5-107">Yönetim çözümleri Operations Management Suite (OMS) olarak uygulanır [Resource Manager şablonları](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="73dc5-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="73dc5-108">Yönetim çözümleri yazmak öğrenme için ana görev öğrenme nasıl [şablon Yazar](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="73dc5-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="73dc5-109">Bu makale şablonları çözümleri ve nasıl tipik çözüm kaynaklarını yapılandırmak için kullanılan benzersiz ayrıntılarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="73dc5-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="73dc5-110">Araçlar</span><span class="sxs-lookup"><span data-stu-id="73dc5-110">Tools</span></span>

<span data-ttu-id="73dc5-111">Çözüm dosyaları ile çalışmak için herhangi bir metin düzenleyicisi kullanabilirsiniz, ancak Visual Studio veya Visual Studio Code aşağıdaki makalelerde açıklanan sağlanan özellikler yararlanarak öneririz.</span><span class="sxs-lookup"><span data-stu-id="73dc5-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span></span>

- [<span data-ttu-id="73dc5-112">Oluşturma ve Visual Studio üzerinden Azure kaynak gruplarını dağıtma</span><span class="sxs-lookup"><span data-stu-id="73dc5-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="73dc5-113">Visual Studio code'da Azure Resource Manager şablonları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="73dc5-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="73dc5-114">yapısı</span><span class="sxs-lookup"><span data-stu-id="73dc5-114">Structure</span></span>
<span data-ttu-id="73dc5-115">Bir yönetim çözümü dosyasının temel yapısı aynıdır bir [Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md#template-format) olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="73dc5-116">Aşağıdaki bölümlerde üst düzey öğeleri açıklanmıştır ve ve içerikleri bir çözümde.</span><span class="sxs-lookup"><span data-stu-id="73dc5-116">Each of the sections below describes the top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="73dc5-117">Parametreler</span><span class="sxs-lookup"><span data-stu-id="73dc5-117">Parameters</span></span>
<span data-ttu-id="73dc5-118">[Parametreleri](../azure-resource-manager/resource-group-authoring-templates.md#parameters) yönetim çözümü yüklediğinizde, kullanıcıdan gerektiren değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span></span>  <span data-ttu-id="73dc5-119">Tüm çözümleri olan standart parametreler vardır ve ek parametreler gerektiği gibi belirli çözümünüz için ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73dc5-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="73dc5-120">Çözümünüzü yüklediğinizde kullanıcılar parametre değerlerini nasıl sağlayacak belirli parametre ve çözümün nasıl yüklendiği değişir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span></span>

<span data-ttu-id="73dc5-121">Kullanıcı Yönetimi çözümünüz aracılığıyla yüklendiğinde [Azure Marketi](operations-management-suite-solutions.md#finding-and-installing-management-solutions) veya [Azure hızlı başlangıç şablonlarını](operations-management-suite-solutions.md#finding-and-installing-management-solutions) seçim yapması istenir bir [HesapOMSçalışmaveOtomasyon](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="73dc5-121">When a user installs your management solution through the [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted to select an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="73dc5-122">Bunlar, her bir standart parametrelerinin değerleri doldurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-122">These are used to populate the values of each of the standard parameters.</span></span>  <span data-ttu-id="73dc5-123">Kullanıcının doğrudan standart parametrelerin değerlerini sağlamasını istenmez, ancak bunlar ek parametreler için değerler sağlamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span></span>

<span data-ttu-id="73dc5-124">Kullanıcı çözümünüzü yüklendiğinde [başka bir yöntem](operations-management-suite-solutions.md#finding-and-installing-management-solutions), tüm standart parametreleri ve tüm ek parametreleri için bir değer girmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="73dc5-124">When the user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="73dc5-125">Bir örnek parametre aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="73dc5-126">Aşağıdaki tabloda bir parametre öznitelikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-126">The following table describes the attributes of a parameter.</span></span>

| <span data-ttu-id="73dc5-127">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="73dc5-127">Attribute</span></span> | <span data-ttu-id="73dc5-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73dc5-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="73dc5-129">type</span><span class="sxs-lookup"><span data-stu-id="73dc5-129">type</span></span> |<span data-ttu-id="73dc5-130">Parametre veri türü.</span><span class="sxs-lookup"><span data-stu-id="73dc5-130">Data type for the parameter.</span></span> <span data-ttu-id="73dc5-131">Kullanıcı için görüntülenen giriş denetimi veri türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-131">The input control displayed for the user depends on the data type.</span></span><br><br><span data-ttu-id="73dc5-132">bool - açılan kutuya</span><span class="sxs-lookup"><span data-stu-id="73dc5-132">bool - Drop down box</span></span><br><span data-ttu-id="73dc5-133">String - metin kutusu</span><span class="sxs-lookup"><span data-stu-id="73dc5-133">string - Text box</span></span><br><span data-ttu-id="73dc5-134">int - metin kutusu</span><span class="sxs-lookup"><span data-stu-id="73dc5-134">int - Text box</span></span><br><span data-ttu-id="73dc5-135">SecureString - parola alanı</span><span class="sxs-lookup"><span data-stu-id="73dc5-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="73dc5-136">category</span><span class="sxs-lookup"><span data-stu-id="73dc5-136">category</span></span> |<span data-ttu-id="73dc5-137">Parametre isteğe bağlı kategorisi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-137">Optional category for the parameter.</span></span>  <span data-ttu-id="73dc5-138">Aynı kategoride parametreleri birlikte gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-138">Parameters in the same category are grouped together.</span></span> |
| <span data-ttu-id="73dc5-139">denetimi</span><span class="sxs-lookup"><span data-stu-id="73dc5-139">control</span></span> |<span data-ttu-id="73dc5-140">Ek işlevsellik dizesi parametreleri için.</span><span class="sxs-lookup"><span data-stu-id="73dc5-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="73dc5-141">DateTime - Datetime denetim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="73dc5-142">GUID - GUID değeri otomatik olarak oluşturulur ve parametre görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="73dc5-142">guid - Guid value is automatically generated, and the parameter is not displayed.</span></span> |
| <span data-ttu-id="73dc5-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73dc5-143">description</span></span> |<span data-ttu-id="73dc5-144">Parametre isteğe bağlı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="73dc5-144">Optional description for the parameter.</span></span>  <span data-ttu-id="73dc5-145">Bir bilgi balonu parametresi yanında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-145">Displayed in an information balloon next to the parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="73dc5-146">Standart Parametreler</span><span class="sxs-lookup"><span data-stu-id="73dc5-146">Standard parameters</span></span>
<span data-ttu-id="73dc5-147">Aşağıdaki tabloda, tüm yönetim çözümleri için standart parametreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="73dc5-147">The following table lists the standard parameters for all management solutions.</span></span>  <span data-ttu-id="73dc5-148">Bu değerleri çözümünüzü Azure Marketi ya da Quickstart şablondan yüklendiğinde bunların istenmesi yerine kullanıcı için doldurulur.</span><span class="sxs-lookup"><span data-stu-id="73dc5-148">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="73dc5-149">Çözüm başka bir yöntemle yüklüyse, kullanıcı bunlar için değer sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="73dc5-149">The user must provide values for them if the solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="73dc5-150">Hızlı Başlangıç şablonları ve Azure Marketi kullanıcı arabiriminde parametre adları tabloda bekliyor.</span><span class="sxs-lookup"><span data-stu-id="73dc5-150">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span></span>  <span data-ttu-id="73dc5-151">Farklı parametre adları kullanırsanız, sonra kullanıcı bunlar için istenir ve bunların değil otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="73dc5-151">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="73dc5-152">Parametre</span><span class="sxs-lookup"><span data-stu-id="73dc5-152">Parameter</span></span> | <span data-ttu-id="73dc5-153">Tür</span><span class="sxs-lookup"><span data-stu-id="73dc5-153">Type</span></span> | <span data-ttu-id="73dc5-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73dc5-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="73dc5-155">accountName</span><span class="sxs-lookup"><span data-stu-id="73dc5-155">accountName</span></span> |<span data-ttu-id="73dc5-156">Dize</span><span class="sxs-lookup"><span data-stu-id="73dc5-156">string</span></span> |<span data-ttu-id="73dc5-157">Azure Otomasyon hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="73dc5-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="73dc5-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="73dc5-158">pricingTier</span></span> |<span data-ttu-id="73dc5-159">Dize</span><span class="sxs-lookup"><span data-stu-id="73dc5-159">string</span></span> |<span data-ttu-id="73dc5-160">Hem günlük analizi çalışma alanı hem de Azure Otomasyonu hesabı fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="73dc5-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="73dc5-161">RegionID</span><span class="sxs-lookup"><span data-stu-id="73dc5-161">regionId</span></span> |<span data-ttu-id="73dc5-162">Dize</span><span class="sxs-lookup"><span data-stu-id="73dc5-162">string</span></span> |<span data-ttu-id="73dc5-163">Azure Otomasyonu hesabı bölgesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-163">Region of the Azure Automation account.</span></span> |
| <span data-ttu-id="73dc5-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="73dc5-164">solutionName</span></span> |<span data-ttu-id="73dc5-165">Dize</span><span class="sxs-lookup"><span data-stu-id="73dc5-165">string</span></span> |<span data-ttu-id="73dc5-166">Çözüm adı.</span><span class="sxs-lookup"><span data-stu-id="73dc5-166">Name of the solution.</span></span>  <span data-ttu-id="73dc5-167">Çözümünüzü hızlı başlangıç şablonlarıyla dağıtıyorsanız, bunun yerine bir tane belirtmek kullanıcının gerektiren bir dize tanımlamak için daha sonra solutionName parametre olarak tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span></span> |
| <span data-ttu-id="73dc5-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="73dc5-168">workspaceName</span></span> |<span data-ttu-id="73dc5-169">Dize</span><span class="sxs-lookup"><span data-stu-id="73dc5-169">string</span></span> |<span data-ttu-id="73dc5-170">Günlük analizi çalışma alanı adı.</span><span class="sxs-lookup"><span data-stu-id="73dc5-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="73dc5-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="73dc5-171">workspaceRegionId</span></span> |<span data-ttu-id="73dc5-172">Dize</span><span class="sxs-lookup"><span data-stu-id="73dc5-172">string</span></span> |<span data-ttu-id="73dc5-173">Günlük analizi çalışma alanı bölgesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-173">Region of the Log Analytics workspace.</span></span> |


<span data-ttu-id="73dc5-174">Çözüm dosyanıza kopyalayıp standart parametreleri yapısını aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-174">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span></span>  

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
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="73dc5-175">Parametre değerleri sözdizimiyle çözümün diğer öğelerinde başvurmak **parametreleri ('parametre adı')**.</span><span class="sxs-lookup"><span data-stu-id="73dc5-175">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="73dc5-176">Örneğin, çalışma alanı adı erişmek için kullanacağınız **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="73dc5-176">For example, to access the workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="73dc5-177">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="73dc5-177">Variables</span></span>
<span data-ttu-id="73dc5-178">[Değişkenleri](../azure-resource-manager/resource-group-authoring-templates.md#variables) yönetim çözümü geri kalanı kullanacağınız değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span></span>  <span data-ttu-id="73dc5-179">Bu değerleri çözüm yükleme kullanıcıya sunulmaz.</span><span class="sxs-lookup"><span data-stu-id="73dc5-179">These values are not exposed to the user installing the solution.</span></span>  <span data-ttu-id="73dc5-180">Birden çok kez çözümün kullanılabilir değerler yönetebileceği tek bir konuma yazar sağlamak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-180">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span></span> <span data-ttu-id="73dc5-181">Herhangi bir değere belirli bunları kodlamak aksine değişkenlerine çözümünüze yerleştirileceği **kaynakları** öğesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-181">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span></span>  <span data-ttu-id="73dc5-182">Bu kodu daha okunabilir hale getirir ve sonraki sürümlerinde bu değerleri kolayca değiştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="73dc5-182">This makes the code more readable and allows you to easily change these values in later versions.</span></span>

<span data-ttu-id="73dc5-183">Aşağıdaki örneği verilmiştir bir **değişkenleri** çözümlerinde kullanılan tipik parametrelerle öğesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="73dc5-184">Değişken değerleri sözdizimiyle çözüm aracılığıyla başvurmak **değişkenleri ('değişkeni')**.</span><span class="sxs-lookup"><span data-stu-id="73dc5-184">You refer to variable values through the solution with the syntax **variables('variable name')**.</span></span>  <span data-ttu-id="73dc5-185">Örneğin, SolutionName değişkeni erişmek için kullanacağınız **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="73dc5-185">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="73dc5-186">Ayrıca, karmaşık değişkenleri tanımlayabilirsiniz, birden çok değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="73dc5-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="73dc5-187">Burada farklı türdeki kaynakların için birden çok özellik tanımlama bu yönetim çözümlerine özellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="73dc5-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="73dc5-188">Örneğin, yukarıda aşağıdaki gösterilen çözüm değişkenleri yapılandırmayı.</span><span class="sxs-lookup"><span data-stu-id="73dc5-188">For example, you could restructure the solution variables shown above to the following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="73dc5-189">Bu durumda, söz dizimi çözümüyle değişken değerlerini başvuruda **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="73dc5-189">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="73dc5-190">Örneğin, çözüm adı değişkeni erişmek için kullanacağınız **variables('Solution'). Ad**.</span><span class="sxs-lookup"><span data-stu-id="73dc5-190">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="73dc5-191">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="73dc5-191">Resources</span></span>
<span data-ttu-id="73dc5-192">[Kaynakları](../azure-resource-manager/resource-group-authoring-templates.md#resources) Yönetimi çözümünüzü yükleyecekleri ve yapılandıracakları farklı kaynakları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="73dc5-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="73dc5-193">Bu şablon en büyük ve en karmaşık kısmı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-193">This will be the largest and most complex portion of the template.</span></span>  <span data-ttu-id="73dc5-194">Kaynak öğelerin tam bir açıklaması ve yapısı elde edebilirsiniz [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="73dc5-194">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="73dc5-195">Genellikle tanımlayacaksınız farklı kaynaklar bu belgede diğer makalelerinde ayrıntılı olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="73dc5-196">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="73dc5-196">Dependencies</span></span>
<span data-ttu-id="73dc5-197">**DependsOn** öğeleri belirten bir [bağımlılık](../azure-resource-manager/resource-group-define-dependencies.md) başka bir kaynak üzerinde.</span><span class="sxs-lookup"><span data-stu-id="73dc5-197">The **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="73dc5-198">Çözüm yüklendiğinde, tüm bağımlılıkları oluşturulmuş kadar kaynak oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="73dc5-198">When the solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="73dc5-199">Örneğin, çözümünüzü olabilir [bir runbook başlatın](operations-management-suite-solutions-resources-automation.md#runbooks) kullanarak yüklendiğinde bir [işi kaynak](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="73dc5-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="73dc5-200">İş kaynak iş oluşturulmadan önce runbook oluşturulduğundan emin olmak için runbook kaynağına bağlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-200">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="73dc5-201">OMS çalışma ve Automation hesabı</span><span class="sxs-lookup"><span data-stu-id="73dc5-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="73dc5-202">Yönetim çözümleri gerektiren bir [OMS çalışma](../log-analytics/log-analytics-manage-access.md) görünümleri içerecek şekilde ve bir [Otomasyon hesabı](../automation/automation-security-overview.md#automation-account-overview) runbook'ları ve ilgili kaynakları içerecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="73dc5-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span>  <span data-ttu-id="73dc5-203">Çözüm kaynaklarında oluşturulur ve çözümde tanımlanmamalıdır önce bu kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-203">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span></span>  <span data-ttu-id="73dc5-204">Kullanıcı [çalışma ve hesabı belirtin](operations-management-suite-solutions.md#oms-workspace-and-automation-account) zaman çözümünüzü dağıtmak, ancak yazarı olarak, aşağıdaki noktaları dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-204">The user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="73dc5-205">Çözüm kaynağı</span><span class="sxs-lookup"><span data-stu-id="73dc5-205">Solution resource</span></span>
<span data-ttu-id="73dc5-206">Kaynak girişi her çözüm gerektirir **kaynakları** çözümü tanımlar öğesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-206">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span></span>  <span data-ttu-id="73dc5-207">Bu bir türü olacak **Microsoft.OperationsManagement/solutions** ve aşağıdaki yapı ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span></span> <span data-ttu-id="73dc5-208">Bu içerir [standart parametreler](#parameters) ve [değişkenleri](#variables) , genellikle çözümün özelliklerini tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span></span>


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




### <a name="dependencies"></a><span data-ttu-id="73dc5-209">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="73dc5-209">Dependencies</span></span>
<span data-ttu-id="73dc5-210">Çözüm kaynağı olmalıdır bir [bağımlılık](../azure-resource-manager/resource-group-define-dependencies.md) gerektiği çözümü oluşturulabilmesi için önce mevcut Bu çözümdeki her bir kaynak üzerinde.</span><span class="sxs-lookup"><span data-stu-id="73dc5-210">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span></span>  <span data-ttu-id="73dc5-211">Her kaynak için bir giriş ekleyerek bunu **dependsOn** öğesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-211">You do this by adding an entry for each resource in the **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="73dc5-212">Özellikler</span><span class="sxs-lookup"><span data-stu-id="73dc5-212">Properties</span></span>
<span data-ttu-id="73dc5-213">Çözüm kaynağı aşağıdaki tabloda özelliklerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-213">The solution resource has the properties in the following table.</span></span>  <span data-ttu-id="73dc5-214">Bu, başvurulan ve çözüm yüklendikten sonra kaynak nasıl yönetildiğini tanımlar çözümü tarafından bulunan kaynaklar içerir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-214">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span></span>  <span data-ttu-id="73dc5-215">Çözümdeki her bir kaynağın ya da listelenmelidir **referencedResources** veya **containedResources** özelliği.</span><span class="sxs-lookup"><span data-stu-id="73dc5-215">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span></span>

| <span data-ttu-id="73dc5-216">Özellik</span><span class="sxs-lookup"><span data-stu-id="73dc5-216">Property</span></span> | <span data-ttu-id="73dc5-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73dc5-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="73dc5-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="73dc5-218">workspaceResourceId</span></span> |<span data-ttu-id="73dc5-219">Günlük analizi çalışma alanı biçiminde Kimliğini  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<çalışma alanı adı\>*.</span><span class="sxs-lookup"><span data-stu-id="73dc5-219">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="73dc5-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="73dc5-220">referencedResources</span></span> |<span data-ttu-id="73dc5-221">Çözüm kaldırıldığında kaldırılmamalıdır çözümü kaynaklarında listesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-221">List of resources in the solution that should not be removed when the solution is removed.</span></span> |
| <span data-ttu-id="73dc5-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="73dc5-222">containedResources</span></span> |<span data-ttu-id="73dc5-223">Çözüm kaldırıldığında kaldırılmalıdır çözümü kaynaklarında listesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-223">List of resources in the solution that should be removed when the solution is removed.</span></span> |

<span data-ttu-id="73dc5-224">Yukarıdaki örnekte, bir runbook, zamanlama ve görünüm ile bir çözüm içindir.</span><span class="sxs-lookup"><span data-stu-id="73dc5-224">The example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="73dc5-225">Zamanlama ve runbook *başvurulan* içinde **özellikleri** çözüm kaldırıldığında bunlar kaldırılmaz şekilde öğesi.</span><span class="sxs-lookup"><span data-stu-id="73dc5-225">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span></span>  <span data-ttu-id="73dc5-226">Görünüm *bulunan* çözüm kaldırıldığında kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-226">The view is *contained* so it is removed when the solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="73dc5-227">Planlama</span><span class="sxs-lookup"><span data-stu-id="73dc5-227">Plan</span></span>
<span data-ttu-id="73dc5-228">**Planı** çözüm kaynak varlığı aşağıdaki tabloda özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="73dc5-228">The **plan** entity of the solution resource has the properties in the following table.</span></span>

| <span data-ttu-id="73dc5-229">Özellik</span><span class="sxs-lookup"><span data-stu-id="73dc5-229">Property</span></span> | <span data-ttu-id="73dc5-230">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73dc5-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="73dc5-231">ad</span><span class="sxs-lookup"><span data-stu-id="73dc5-231">name</span></span> |<span data-ttu-id="73dc5-232">Çözüm adı.</span><span class="sxs-lookup"><span data-stu-id="73dc5-232">Name of the solution.</span></span> |
| <span data-ttu-id="73dc5-233">Sürüm</span><span class="sxs-lookup"><span data-stu-id="73dc5-233">version</span></span> |<span data-ttu-id="73dc5-234">Yazar tarafından belirlenen çözümü sürümü.</span><span class="sxs-lookup"><span data-stu-id="73dc5-234">Version of the solution as determined by the author.</span></span> |
| <span data-ttu-id="73dc5-235">Ürün</span><span class="sxs-lookup"><span data-stu-id="73dc5-235">product</span></span> |<span data-ttu-id="73dc5-236">Çözümü tanımlamak için benzersiz bir dize.</span><span class="sxs-lookup"><span data-stu-id="73dc5-236">Unique string to identify the solution.</span></span> |
| <span data-ttu-id="73dc5-237">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="73dc5-237">publisher</span></span> |<span data-ttu-id="73dc5-238">Çözüm Yayımcısı.</span><span class="sxs-lookup"><span data-stu-id="73dc5-238">Publisher of the solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="73dc5-239">Örnek</span><span class="sxs-lookup"><span data-stu-id="73dc5-239">Sample</span></span>
<span data-ttu-id="73dc5-240">Çözüm dosyaları aşağıdaki konumlarda bir çözüm kaynakla örnekleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73dc5-240">You can view samples of solution files with a solution resource at the following locations.</span></span>

- [<span data-ttu-id="73dc5-241">Otomasyon kaynakları</span><span class="sxs-lookup"><span data-stu-id="73dc5-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="73dc5-242">Arama ve uyarı kaynakları</span><span class="sxs-lookup"><span data-stu-id="73dc5-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="73dc5-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73dc5-243">Next steps</span></span>
* <span data-ttu-id="73dc5-244">[Kaydedilmiş aramaları ve Uyarıları Ekle](operations-management-suite-solutions-resources-searches-alerts.md) Yönetimi çözümünüz için.</span><span class="sxs-lookup"><span data-stu-id="73dc5-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="73dc5-245">[Görünümler ekleme](operations-management-suite-solutions-resources-views.md) Yönetimi çözümünüz için.</span><span class="sxs-lookup"><span data-stu-id="73dc5-245">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="73dc5-246">[Runbook'ları ve diğer Automation kaynaklarına eklemek](operations-management-suite-solutions-resources-automation.md) Yönetimi çözümünüz için.</span><span class="sxs-lookup"><span data-stu-id="73dc5-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>
* <span data-ttu-id="73dc5-247">Ayrıntılarını öğrenmek [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="73dc5-247">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="73dc5-248">Arama [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates) farklı Resource Manager şablonları örneklerini için.</span><span class="sxs-lookup"><span data-stu-id="73dc5-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
