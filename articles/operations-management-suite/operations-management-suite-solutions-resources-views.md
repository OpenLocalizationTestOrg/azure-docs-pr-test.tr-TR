---
title: "Operations Management Suite (OMS) yönetim çözümleri görünümlerde | Microsoft Docs"
description: "Yönetim çözümleri Operations Management Suite (OMS) genellikle verileri görselleştirmek için bir veya daha fazla görünümleri içerir.  Bu makalede, Görünüm Tasarımcısı tarafından oluşturulan bir görünüm vermek ve bir yönetim çözümü dahil açıklar. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="96f3a-104">Operations Management Suite (OMS) yönetim çözümleri (Önizleme) görünümlerde</span><span class="sxs-lookup"><span data-stu-id="96f3a-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="96f3a-105">Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="96f3a-106">Aşağıda açıklanan herhangi bir şema değiştirilebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="96f3a-107">[Yönetim çözümleri Operations Management Suite (OMS)](operations-management-suite-solutions.md) genellikle verileri görselleştirmek için bir veya daha fazla görünümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="96f3a-108">Bu makalede tarafından oluşturulan bir görünüm dışarı aktarma [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) ve bir yönetim çözümü içerir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="96f3a-109">Bu makaledeki örnekler parametreleri ve gerekli olduğunu veya yönetim çözümleri için ortak olduğunu ve açıklanan değişkenleri kullanma [Operations Management Suite (OMS) yönetimi çözümleri oluşturma](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="96f3a-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="96f3a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96f3a-110">Prerequisites</span></span>
<span data-ttu-id="96f3a-111">Bu makale, zaten nasıl hakkında bilgi sahibi olduğunuzu varsayar [bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md) ve çözüm dosya yapısı.</span><span class="sxs-lookup"><span data-stu-id="96f3a-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="96f3a-112">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="96f3a-112">Overview</span></span>
<span data-ttu-id="96f3a-113">Bir yönetim çözümü bir görünüm eklemek için oluşturduğunuz bir **kaynak** içinde için [çözüm dosyasını](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="96f3a-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="96f3a-114">Görünümün ayrıntılı yapılandırma tanımlayan JSON ancak ve bir şey yok tipik çözüm Yazar el ile oluşturmak mümkün olacaktır genellikle karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="96f3a-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="96f3a-115">Görünümü kullanarak oluşturmak için kullanılan en yaygın yöntem olan [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md)dışa aktarın ve ardından ayrıntılı yapılandırmasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="96f3a-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="96f3a-116">Görünüm bir çözüme eklemek için temel adımlar aşağıda belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="96f3a-117">Her adım, aşağıdaki bölümlerde daha ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="96f3a-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="96f3a-118">Görünüm bir dosyaya aktarın.</span><span class="sxs-lookup"><span data-stu-id="96f3a-118">Export the view to a file.</span></span>
2. <span data-ttu-id="96f3a-119">Görünüm kaynak çözümde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96f3a-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="96f3a-120">Ayrıntıları Görüntüle ekleyin.</span><span class="sxs-lookup"><span data-stu-id="96f3a-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="96f3a-121">Görünüm bir dosyaya dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="96f3a-121">Export the view to a file</span></span>
<span data-ttu-id="96f3a-122">Bölümündeki yönergeleri izleyin [günlük analizi Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) bir görünüm bir dosyaya vermek için.</span><span class="sxs-lookup"><span data-stu-id="96f3a-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="96f3a-123">Dışarı aktarılan dosyayı aynı JSON biçiminde olacaktır [öğeleri çözüm dosyası olarak](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="96f3a-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="96f3a-124">**Kaynakları** görünüm dosyası öğe türüne sahip bir kaynak olacaktır **Microsoft.OperationalInsights/workspaces** , OMS çalışma alanını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="96f3a-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="96f3a-125">Bu öğe bir alt öğe türüne sahip olacaktır **görünümleri** görünümü temsil eder ve ayrıntılı yapılandırmasını içerir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="96f3a-126">Bu öğenin ayrıntılarını kopyalamanız ve ardından çözümünüze kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="96f3a-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="96f3a-127">Çözümde görünüm kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="96f3a-127">Create the view resource in the solution</span></span>
<span data-ttu-id="96f3a-128">Aşağıdaki görünüm kaynağa eklemek **kaynakları** çözüm dosyanızın öğesi.</span><span class="sxs-lookup"><span data-stu-id="96f3a-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="96f3a-129">Bu, aynı zamanda eklemelisiniz seçeneklerdir değişkenleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="96f3a-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="96f3a-130">Unutmayın **Pano** ve **OverviewTile** dışarı aktarılan görünüm dosyasından karşılık gelen özelliklerle kılacak yer tutucuları özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="96f3a-131">Çözüm dosyası değişkenleri öğesine aşağıdaki değişkenleri eklemek ve bu çözümünüz için değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96f3a-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="96f3a-132">Dışarı aktarılan görünüm dosyanızdan tüm görünüm kaynak kopyalamak, ancak bunu çözümünüzde çalıştırmak aşağıdaki değişiklikleri yapmanız gerekir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96f3a-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="96f3a-133">**Türü** görünüm için kaynak gelen değiştirilmesi gereken **görünümleri** için **Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="96f3a-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="96f3a-134">**Adı** görünüm kaynak için özellik çalışma alanı adı içerecek şekilde değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="96f3a-135">Çalışma alanı bağımlılığını çalışma kaynak çözümde tanımlı değil bu yana kaldırılması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="96f3a-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="96f3a-136">**DisplayName** özelliği görünümüne eklenmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="96f3a-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="96f3a-137">**Kimliği**, **adı**, ve **DisplayName** tüm eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="96f3a-138">Parametre adları gerekli parametrelerinin eşleşecek şekilde değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="96f3a-139">Değişkenleri çözümde tanımlanan ve uygun özelliklerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="96f3a-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="96f3a-140">Görünüm ayrıntılarını Ekle</span><span class="sxs-lookup"><span data-stu-id="96f3a-140">Add the view details</span></span>
<span data-ttu-id="96f3a-141">Dışarı aktarılan görünüm dosyası görünüm kaynak iki öğelerinde içerecek **özellikleri** adlı öğe **Pano** ve **OverviewTile** ayrıntılı içerir Görünüm yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="96f3a-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="96f3a-142">Bu iki öğenin ve içerikleri içine kopyalamak **özellikleri** çözüm dosyanızdaki görünüm kaynak öğesidir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="96f3a-143">Örnek</span><span class="sxs-lookup"><span data-stu-id="96f3a-143">Example</span></span>
<span data-ttu-id="96f3a-144">Örneğin, aşağıdaki örnek basit çözüm dosyasını bir görünümle gösterir.</span><span class="sxs-lookup"><span data-stu-id="96f3a-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="96f3a-145">Üç nokta (...) için gösterilen **Pano** ve **OverviewTile** alanı nedeniyle içeriği.</span><span class="sxs-lookup"><span data-stu-id="96f3a-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="96f3a-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96f3a-146">Next steps</span></span>
* <span data-ttu-id="96f3a-147">Oluşturma ayrıntılarının öğrenin [yönetim çözümleri](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="96f3a-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="96f3a-148">Dahil [Otomasyon runbook'ları yönetim çözümünüzdeki](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="96f3a-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
