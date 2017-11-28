---
title: "Operations Management Suite (OMS) Yönetimi çözümlerinde aaaViews | Microsoft Docs"
description: "Yönetim çözümleri Operations Management Suite (OMS) genellikle bir veya daha fazla görünümleri toovisualize verileri içerir.  Bu makalede nasıl tooexport bir görünüm hello Görünüm Tasarımcısı tarafından oluşturulan ve bir yönetim çözümü içerir. "
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
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="51e92-104">Operations Management Suite (OMS) yönetim çözümleri (Önizleme) görünümlerde</span><span class="sxs-lookup"><span data-stu-id="51e92-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="51e92-105">Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir.</span><span class="sxs-lookup"><span data-stu-id="51e92-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="51e92-106">Aşağıda açıklanan herhangi bir şema konu toochange ' dir.</span><span class="sxs-lookup"><span data-stu-id="51e92-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="51e92-107">[Yönetim çözümleri Operations Management Suite (OMS)](operations-management-suite-solutions.md) genellikle bir veya daha fazla görünümleri toovisualize verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="51e92-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="51e92-108">Bu makalede tooexport bir görünüm hello tarafından nasıl oluşturulacağını açıklar [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) ve bir yönetim çözümü içerir.</span><span class="sxs-lookup"><span data-stu-id="51e92-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="51e92-109">Merhaba bu makaledeki örnekler parametreleri ve ya da gerekli veya ortak toomanagement çözümleri ve açıklanan değişkenleri kullanma [Operations Management Suite (OMS) yönetimi çözümleri oluşturma](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="51e92-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="51e92-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="51e92-110">Prerequisites</span></span>
<span data-ttu-id="51e92-111">Bu makale, zaten çok konusunda bilgi sahibi olduğunuzu varsayar[bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md) ve bir çözüm dosyasının hello yapısı.</span><span class="sxs-lookup"><span data-stu-id="51e92-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="51e92-112">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="51e92-112">Overview</span></span>
<span data-ttu-id="51e92-113">bir yönetim çözümü bir görünümde tooinclude, oluşturduğunuz bir **kaynak** hello içinde için [çözüm dosyasını](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="51e92-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="51e92-114">Merhaba hello görünümün ayrıntılı yapılandırma tanımlayan JSON ancak ve bir şey yok tipik çözüm Yazar mümkün toocreate el ile olacaktır genellikle karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="51e92-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="51e92-115">Merhaba en yaygın yöntem hello kullanarak toocreate hello görünümdür [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md)dışa aktarın ve ardından ayrıntılı yapılandırma toohello çözümünün ekleyin.</span><span class="sxs-lookup"><span data-stu-id="51e92-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="51e92-116">Merhaba temel adımlar tooadd bir görünüm tooa çözümü aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="51e92-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="51e92-117">Her adım, aşağıdaki hello bölümlerde daha ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="51e92-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="51e92-118">Merhaba görünüm tooa dosyası dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="51e92-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="51e92-119">Merhaba görünüm kaynak hello çözümde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="51e92-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="51e92-120">Merhaba görünümü ayrıntıları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="51e92-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="51e92-121">Merhaba görünüm tooa dosyası dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="51e92-121">Export hello view tooa file</span></span>
<span data-ttu-id="51e92-122">Merhaba yönergeleri izleyin [günlük analizi Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) tooexport tooa dosyasını görüntüle.</span><span class="sxs-lookup"><span data-stu-id="51e92-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="51e92-123">Merhaba dışarı aktarılan dosyayı olması ile JSON biçiminde hello aynı [öğeleri hello çözüm dosyası olarak](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="51e92-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="51e92-124">Merhaba **kaynakları** hello görünüm dosyasının öğesi türüne sahip bir kaynak olacaktır **Microsoft.OperationalInsights/workspaces** temsil OMS çalışma hello.</span><span class="sxs-lookup"><span data-stu-id="51e92-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="51e92-125">Bu öğe bir alt öğe türüne sahip olacaktır **görünümleri** hello görünümü temsil eder ve ayrıntılı yapılandırmasını içerir.</span><span class="sxs-lookup"><span data-stu-id="51e92-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="51e92-126">Bu öğenin hello ayrıntıları kopyalamanız ve çözümünüze kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="51e92-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="51e92-127">Merhaba çözümde Hello görünüm kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51e92-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="51e92-128">Görünüm kaynak toohello aşağıdaki hello eklemek **kaynakları** çözüm dosyanızı öğesidir.</span><span class="sxs-lookup"><span data-stu-id="51e92-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="51e92-129">Bu, aynı zamanda eklemelisiniz seçeneklerdir değişkenleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="51e92-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="51e92-130">Bu hello Not **Pano** ve **OverviewTile** hello dışarı aktarılan görünüm dosyasından hello karşılık gelen özelliklerle kılacak yer tutucuları özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="51e92-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

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

<span data-ttu-id="51e92-131">Değişkenleri toohello değişkenleri hello çözüm dosyasının öğesinin aşağıdaki hello ekleyin ve başlangıç değerleri toothose çözümünüz için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="51e92-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="51e92-132">Dışarı aktarılan görünüm dosyanızdan hello tüm görünüm kaynak kopyalamak, ancak toowork, çözümünüz için aşağıdaki değişiklikler toomake hello gerekir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="51e92-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="51e92-133">Merhaba **türü** hello görünüm için kaynak değiştirildi toobe gereken **görünümleri** çok**Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="51e92-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="51e92-134">Merhaba **adı** hello görünüm kaynak için özellik değişti toobe tooinclude hello çalışma alanı adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="51e92-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="51e92-135">Merhaba çalışma Hello bağımlılığını hello çalışma kaynak hello çözümde tanımlı değil beri kaldırılan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="51e92-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="51e92-136">**DisplayName** özelliği gereksinimlerini toobe toohello görünüm eklendi.</span><span class="sxs-lookup"><span data-stu-id="51e92-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="51e92-137">Merhaba **kimliği**, **adı**, ve **DisplayName** tüm eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="51e92-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="51e92-138">Parametre adları değiştirilmelidir toomatch hello gerekli parametre kümesi.</span><span class="sxs-lookup"><span data-stu-id="51e92-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="51e92-139">Değişkenleri hello çözümde tanımlanan ve hello uygun özelliklerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51e92-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="51e92-140">Merhaba görünüm ayrıntılarını Ekle</span><span class="sxs-lookup"><span data-stu-id="51e92-140">Add hello view details</span></span>
<span data-ttu-id="51e92-141">Merhaba Hello görünüm kaynak dosya hello iki öğelerinde içerecek görünüm dışarı **özellikleri** adlı öğe **Pano** ve **OverviewTile** hello içerir ayrıntılı yapılandırma hello görünümünün.</span><span class="sxs-lookup"><span data-stu-id="51e92-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="51e92-142">Bu iki öğenin ve içerikleri hello kopyalamak **özellikleri** hello görünüm kaynak çözüm dosyanızdaki öğesidir.</span><span class="sxs-lookup"><span data-stu-id="51e92-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="51e92-143">Örnek</span><span class="sxs-lookup"><span data-stu-id="51e92-143">Example</span></span>
<span data-ttu-id="51e92-144">Örneğin, aşağıdaki örnek hello basit çözüm dosyasını bir görünümle gösterir.</span><span class="sxs-lookup"><span data-stu-id="51e92-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="51e92-145">Üç nokta (...) Merhaba gösterilen **Pano** ve **OverviewTile** alanı nedeniyle içeriği.</span><span class="sxs-lookup"><span data-stu-id="51e92-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="51e92-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51e92-146">Next steps</span></span>
* <span data-ttu-id="51e92-147">Oluşturma ayrıntılarının öğrenin [yönetim çözümleri](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="51e92-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="51e92-148">Dahil [Otomasyon runbook'ları yönetim çözümünüzdeki](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="51e92-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
