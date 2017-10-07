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
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Operations Management Suite (OMS) yönetim çözümleri (Önizleme) görünümlerde
> [!NOTE]
> Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir. Aşağıda açıklanan herhangi bir şema konu toochange ' dir.    
>
>

[Yönetim çözümleri Operations Management Suite (OMS)](operations-management-suite-solutions.md) genellikle bir veya daha fazla görünümleri toovisualize verileri içerir.  Bu makalede tooexport bir görünüm hello tarafından nasıl oluşturulacağını açıklar [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) ve bir yönetim çözümü içerir.  

> [!NOTE]
> Merhaba bu makaledeki örnekler parametreleri ve ya da gerekli veya ortak toomanagement çözümleri ve açıklanan değişkenleri kullanma [Operations Management Suite (OMS) yönetimi çözümleri oluşturma](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Ön koşullar
Bu makale, zaten çok konusunda bilgi sahibi olduğunuzu varsayar[bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md) ve bir çözüm dosyasının hello yapısı.

## <a name="overview"></a>Genel Bakış
bir yönetim çözümü bir görünümde tooinclude, oluşturduğunuz bir **kaynak** hello içinde için [çözüm dosyasını](operations-management-suite-solutions-creating.md).  Merhaba hello görünümün ayrıntılı yapılandırma tanımlayan JSON ancak ve bir şey yok tipik çözüm Yazar mümkün toocreate el ile olacaktır genellikle karmaşıktır.  Merhaba en yaygın yöntem hello kullanarak toocreate hello görünümdür [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md)dışa aktarın ve ardından ayrıntılı yapılandırma toohello çözümünün ekleyin.

Merhaba temel adımlar tooadd bir görünüm tooa çözümü aşağıdaki gibidir.  Her adım, aşağıdaki hello bölümlerde daha ayrıntılı açıklanmıştır.

1. Merhaba görünüm tooa dosyası dışarı aktarın.
2. Merhaba görünüm kaynak hello çözümde oluşturun.
3. Merhaba görünümü ayrıntıları ekleyin.

## <a name="export-hello-view-tooa-file"></a>Merhaba görünüm tooa dosyası dışarı aktarma
Merhaba yönergeleri izleyin [günlük analizi Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) tooexport tooa dosyasını görüntüle.  Merhaba dışarı aktarılan dosyayı olması ile JSON biçiminde hello aynı [öğeleri hello çözüm dosyası olarak](operations-management-suite-solutions-solution-file.md).  

Merhaba **kaynakları** hello görünüm dosyasının öğesi türüne sahip bir kaynak olacaktır **Microsoft.OperationalInsights/workspaces** temsil OMS çalışma hello.  Bu öğe bir alt öğe türüne sahip olacaktır **görünümleri** hello görünümü temsil eder ve ayrıntılı yapılandırmasını içerir.  Bu öğenin hello ayrıntıları kopyalamanız ve çözümünüze kopyalayın.

## <a name="create-hello-view-resource-in-hello-solution"></a>Merhaba çözümde Hello görünüm kaynağı oluşturma
Görünüm kaynak toohello aşağıdaki hello eklemek **kaynakları** çözüm dosyanızı öğesidir.  Bu, aynı zamanda eklemelisiniz seçeneklerdir değişkenleri kullanır.  Bu hello Not **Pano** ve **OverviewTile** hello dışarı aktarılan görünüm dosyasından hello karşılık gelen özelliklerle kılacak yer tutucuları özelliklerdir.

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

Değişkenleri toohello değişkenleri hello çözüm dosyasının öğesinin aşağıdaki hello ekleyin ve başlangıç değerleri toothose çözümünüz için değiştirin.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


Dışarı aktarılan görünüm dosyanızdan hello tüm görünüm kaynak kopyalamak, ancak toowork, çözümünüz için aşağıdaki değişiklikler toomake hello gerekir unutmayın.  

* Merhaba **türü** hello görünüm için kaynak değiştirildi toobe gereken **görünümleri** çok**Microsoft.OperationalInsights/workspaces**.
* Merhaba **adı** hello görünüm kaynak için özellik değişti toobe tooinclude hello çalışma alanı adı gerekiyor.
* Merhaba çalışma Hello bağımlılığını hello çalışma kaynak hello çözümde tanımlı değil beri kaldırılan toobe gerekir.
* **DisplayName** özelliği gereksinimlerini toobe toohello görünüm eklendi.  Merhaba **kimliği**, **adı**, ve **DisplayName** tüm eşleşmesi gerekir.
* Parametre adları değiştirilmelidir toomatch hello gerekli parametre kümesi.
* Değişkenleri hello çözümde tanımlanan ve hello uygun özelliklerinde kullanılır.

## <a name="add-hello-view-details"></a>Merhaba görünüm ayrıntılarını Ekle
Merhaba Hello görünüm kaynak dosya hello iki öğelerinde içerecek görünüm dışarı **özellikleri** adlı öğe **Pano** ve **OverviewTile** hello içerir ayrıntılı yapılandırma hello görünümünün.  Bu iki öğenin ve içerikleri hello kopyalamak **özellikleri** hello görünüm kaynak çözüm dosyanızdaki öğesidir.

## <a name="example"></a>Örnek
Örneğin, aşağıdaki örnek hello basit çözüm dosyasını bir görünümle gösterir.  Üç nokta (...) Merhaba gösterilen **Pano** ve **OverviewTile** alanı nedeniyle içeriği.

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




## <a name="next-steps"></a>Sonraki adımlar
* Oluşturma ayrıntılarının öğrenin [yönetim çözümleri](operations-management-suite-solutions-creating.md).
* Dahil [Otomasyon runbook'ları yönetim çözümünüzdeki](operations-management-suite-solutions-resources-automation.md).
