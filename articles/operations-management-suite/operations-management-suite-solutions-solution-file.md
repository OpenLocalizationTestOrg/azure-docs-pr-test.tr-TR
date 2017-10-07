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
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Operations Management Suite (OMS) (Önizleme) bir yönetim çözümü dosyası oluşturma
> [!NOTE]
> Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir. Aşağıda açıklanan herhangi bir şema konu toochange ' dir.  

Yönetim çözümleri Operations Management Suite (OMS) olarak uygulanır [Resource Manager şablonları](../azure-resource-manager/resource-manager-template-walkthrough.md).  Merhaba ana görev nasıl tooauthor yönetim çözümleri öğrenme nasıl çok öğrenmek[şablon Yazar](../azure-resource-manager/resource-group-authoring-templates.md).  Bu makale şablonları çözümleri için kullanılan benzersiz ayrıntılarını sağlar ve nasıl tooconfigure tipik çözüm kaynakları.


## <a name="tools"></a>Araçlar

Çözüm dosyalarını bir metin düzenleyicisi toowork kullanabilirsiniz, ancak Visual Studio veya Visual Studio Code makaleler hello açıklandığı gibi sağlanan hello özellikleri yararlanarak öneririz.

- [Oluşturma ve Visual Studio üzerinden Azure kaynak gruplarını dağıtma](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Visual Studio code'da Azure Resource Manager şablonları ile çalışma](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>yapısı
bir yönetim çözümü dosyasının temel yapısı Hello aynı hello olan bir [Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md#template-format) olduğu gibi.  Her biri aşağıdaki hello bölümler hello en üst düzey öğeleri açıklar ve ve içerikleri bir çözümde.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>Parametreler
[Parametreleri](../azure-resource-manager/resource-group-authoring-templates.md#parameters) hello yönetim çözümü yükleyen hello kullanıcının gerektiren değerlerdir.  Tüm çözümleri olan standart parametreler vardır ve ek parametreler gerektiği gibi belirli çözümünüz için ekleyebilirsiniz.  Çözümünüzü yüklediğinizde kullanıcılar parametre değerlerini nasıl sağlayacak hello belirli parametre ve hello çözümü nasıl yüklendiği değişir.

Kullanıcı Yönetimi çözümünüzü hello aracılığıyla yüklendiğinde [Azure Marketi](operations-management-suite-solutions.md#finding-and-installing-management-solutions) veya [Azure hızlı başlangıç şablonlarını](operations-management-suite-solutions.md#finding-and-installing-management-solutions) istendiğinde tooselect oldukları bir [OMS çalışma ve Automation hesabı ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  Bunlar kullanılan toopopulate hello her hello standart parametrelerinin değerlerdir.  Merhaba kullanıcı istenmedi toodirectly hello standart parametreler için değerler sağlayın, ancak bunlar istendiğinde tooprovide ek parametreler değerler.

Merhaba kullanıcı çözümünüzü yüklendiğinde [başka bir yöntem](operations-management-suite-solutions.md#finding-and-installing-management-solutions), tüm standart parametreleri ve tüm ek parametreleri için bir değer girmelisiniz.

Bir örnek parametre aşağıda gösterilmiştir.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

Aşağıdaki tablonun hello parametresinin hello öznitelikleri açıklanmaktadır.

| Öznitelik | Açıklama |
|:--- |:--- |
| type |Merhaba parametresinin veri türü. Merhaba giriş denetiminin Hello kullanıcı için görüntülenen hello veri türüne bağlıdır.<br><br>bool - açılan kutuya<br>String - metin kutusu<br>int - metin kutusu<br>SecureString - parola alanı<br> |
| category |Merhaba parametresi için isteğe bağlı kategorisi.  Aynı kategoride birlikte gruplandırılır hello parametreleri. |
| denetimi |Ek işlevsellik dizesi parametreleri için.<br><br>DateTime - Datetime denetim görüntülenir.<br>GUID - GUID değeri otomatik olarak oluşturulur ve hello parametre görüntülenmez. |
| Açıklama |Merhaba parametresi için isteğe bağlı bir açıklama.  Bir bilgi balonu sonraki toohello parametresinde görüntülenir. |

### <a name="standard-parameters"></a>Standart Parametreler
Merhaba aşağıdaki tabloda tüm yönetim çözümleri için hello standart parametreleri listeler.  Bu değerleri çözümünüzü hello Azure Marketi veya hızlı başlangıç şablonlarından yüklendiğinde yerine bunların istenmesi hello kullanıcı için doldurulur.  Merhaba çözüm başka bir yöntemle yüklediyseniz hello kullanıcı bunlar için değer sağlamalısınız.

> [!NOTE]
> Merhaba kullanıcı arabirimi hello Azure Marketi ve hızlı başlangıç şablonlarında hello parametre adları hello tabloda bekliyor.  Farklı parametre adları kullanırsanız, ardından hello kullanıcı bunlar için istenir ve bunların değil otomatik olarak doldurulur.
>
>

| Parametre | Tür | Açıklama |
|:--- |:--- |:--- |
| accountName |Dize |Azure Otomasyon hesabı adı. |
| pricingTier |Dize |Hem günlük analizi çalışma alanı hem de Azure Otomasyonu hesabı fiyatlandırma katmanı. |
| RegionID |Dize |Hello Azure Automation hesabı bölgesi. |
| solutionName |Dize |Merhaba çözüm adı.  Çözümünüzü hızlı başlangıç şablonlarıyla dağıtıyorsanız, bunun yerine hello kullanıcı toospecify bir gerektiren bir dize tanımlamak için daha sonra solutionName parametre olarak tanımlamanız gerekir. |
| workspaceName |Dize |Günlük analizi çalışma alanı adı. |
| workspaceRegionId |Dize |Merhaba günlük analizi çalışma alanı bölgesi. |


Aşağıda, çözüm dosyanıza kopyalayıp hello standart parametreleri hello yapısıdır.  

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


Merhaba sözdizimi ile Merhaba çözümün diğer öğeleri tooparameter değerleri bkz **parametreleri ('parametre adı')**.  Örneğin, tooaccess Merhaba çalışma alanı adı, kullanacağınız **parameters('workspaceName')**

## <a name="variables"></a>Değişkenler
[Değişkenleri](../azure-resource-manager/resource-group-authoring-templates.md#variables) hello Yönetimi çözümünün hello kalan kullanacağınız değerlerdir.  Bu değerleri hello çözüm yükleme gösterilen toohello kullanıcı olmayan.  Hedeflenen tooprovide hello Yazar birden çok kez hello çözüm kullanılabilir değerler yönetebileceği tek bir konuma sahip oldukları. Hello kodlama karşılıklı toohard olarak değişkenleri herhangi bir değer belirli tooyour çözümü yerleştirileceği **kaynakları** öğesi.  Bu hello kodunu daha okunabilir hale getirir ve sağlar tooeasily sonraki sürümlerinde bu değerlerini değiştirin.

Aşağıdaki örneği verilmiştir bir **değişkenleri** çözümlerinde kullanılan tipik parametrelerle öğesi.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Merhaba sözdizimi ile Merhaba çözüm aracılığıyla toovariable değerleri bkz **değişkenleri ('değişkeni')**.  Örneğin, tooaccess Merhaba SolutionName değişkeni, kullanacağınız **variables('SolutionName')**.

Ayrıca, karmaşık değişkenleri tanımlayabilirsiniz, birden çok değerlerini ayarlar.  Burada farklı türdeki kaynakların için birden çok özellik tanımlama bu yönetim çözümlerine özellikle yararlı olur.  Örneğin, yukarıda toohello aşağıda gösterilen hello çözüm değişkenleri yapılandırmayı.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Bu durumda, hello sözdizimi hello çözümüyle toovariable değerlerini başvurmak **variables('variable name').property**.  Örneğin, tooaccess Merhaba çözüm adı değişkeni, kullanacağınız **variables('Solution'). Ad**.

## <a name="resources"></a>Kaynaklar
[Kaynakları](../azure-resource-manager/resource-group-authoring-templates.md#resources) Yönetimi çözümünüzü yükleyecekleri ve yapılandıracakları hello farklı kaynakları tanımlayın.  Bu hello en büyük ve en karmaşık hello şablonu kısmı olacaktır.  Merhaba yapısı ve kaynak öğelerinde eksiksiz bir açıklaması alabilirsiniz [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md#resources).  Genellikle tanımlayacaksınız farklı kaynaklar bu belgede diğer makalelerinde ayrıntılı olarak belirtilir. 


### <a name="dependencies"></a>Bağımlılıklar
Merhaba **dependsOn** öğeleri belirten bir [bağımlılık](../azure-resource-manager/resource-group-define-dependencies.md) başka bir kaynak üzerinde.  Merhaba çözüm yüklendiğinde, tüm bağımlılıkları oluşturulmuş kadar kaynak oluşturulmaz.  Örneğin, çözümünüzü olabilir [bir runbook başlatın](operations-management-suite-solutions-resources-automation.md#runbooks) kullanarak yüklendiğinde bir [işi kaynak](operations-management-suite-solutions-resources-automation.md#automation-jobs).  Merhaba iş kaynak hello runbook kaynak toomake üzerinde hello iş oluşturulmadan önce bu hello runbook oluşturulduğundan emin bağımlı olacaktır.

### <a name="oms-workspace-and-automation-account"></a>OMS çalışma ve Automation hesabı
Yönetim çözümleri gerektiren bir [OMS çalışma](../log-analytics/log-analytics-manage-access.md) toocontain görünümleri ve bir [Otomasyon hesabı](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook'ları ve ilgili kaynakları.  Bu kaynaklar hello çözümde oluşturulur ve hello çözümüne kendisi tanımlanmamalıdır hello önce kullanılabilir olması gerekir.  Merhaba kullanıcı [çalışma ve hesabı belirtin](operations-management-suite-solutions.md#oms-workspace-and-automation-account) zaman çözümünüzü dağıtmak, ancak hello yazarı olarak hello aşağıdaki noktaları göz önünde bulundurmalısınız.

## <a name="solution-resource"></a>Çözüm kaynağı
Her çözüm hello kaynak girişi gerektirir **kaynakları** hello çözümü kendisini tanımlar öğesi.  Bu bir türü olacak **Microsoft.OperationsManagement/solutions** ve yapı izlenerek hello sahiptir. Bu içerir [standart parametreler](#parameters) ve [değişkenleri](#variables) hello çözüm özelliklerini genellikle kullanılan toodefine olan.


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




### <a name="dependencies"></a>Bağımlılıklar
Merhaba çözüm kaynağı olmalıdır bir [bağımlılık](../azure-resource-manager/resource-group-define-dependencies.md) hello çözüm oluşturulmadan önce tooexist gerektiğinden hello çözümdeki her bir kaynak üzerinde.  Her kaynak için bir giriş hello ekleyerek bunu **dependsOn** öğesi.

### <a name="properties"></a>Özellikler
Merhaba çözüm kaynak tablosu aşağıdaki hello hello özelliklere sahiptir.  Bu, başvurulan ve hello çözüm yüklendikten sonra hello kaynak nasıl yönetildiğini tanımlar hello çözümü tarafından bulunan hello kaynakları içerir.  Merhaba çözümdeki her bir kaynağın her iki hello listelenmelidir **referencedResources** veya hello **containedResources** özelliği.

| Özellik | Açıklama |
|:--- |:--- |
| workspaceResourceId |Merhaba formunda hello günlük analizi çalışma alanı kimliği * <Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<çalışma alanı adı\>*. |
| referencedResources |Merhaba çözüm kaldırıldığında kaldırılmamalıdır hello çözümü kaynaklarında listesi. |
| containedResources |Merhaba çözüm kaldırıldığında kaldırılmalıdır hello çözümü kaynaklarında listesi. |

bir runbook, zamanlama ve görünüm ile bir çözüm için yukarıdaki Hello örnek verilebilir.  Merhaba zamanlama ve runbook *başvurulan* hello içinde **özellikleri** hello çözüm kaldırıldığında bunlar kaldırılmaz şekilde öğesi.  Merhaba görünümdür *bulunan* hello çözüm kaldırıldığında kaldırılır.

### <a name="plan"></a>Planlama
Merhaba **planı** hello çözüm kaynak varlığı aşağıdaki tablonun hello hello özellikleri vardır.

| Özellik | Açıklama |
|:--- |:--- |
| ad |Merhaba çözüm adı. |
| Sürüm |Merhaba yazar tarafından belirlendiği şekilde hello çözümü sürümü. |
| Ürün |Benzersiz bir dize tooidentify hello çözümü. |
| Yayımcı |Merhaba Çözüm Yayımcısı. |



## <a name="sample"></a>Örnek
Aşağıdaki konumlardan hello çözüm dosyalarını bir çözüm kaynakla örnekleri görüntüleyebilirsiniz.

- [Otomasyon kaynakları](operations-management-suite-solutions-resources-automation.md#sample)
- [Arama ve uyarı kaynakları](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Sonraki adımlar
* [Kaydedilmiş aramaları ve Uyarıları Ekle](operations-management-suite-solutions-resources-searches-alerts.md) tooyour yönetim çözümü.
* [Görünümler ekleme](operations-management-suite-solutions-resources-views.md) tooyour yönetim çözümü.
* [Runbook'ları ve diğer Automation kaynaklarına eklemek](operations-management-suite-solutions-resources-automation.md) tooyour yönetim çözümü.
* Merhaba ayrıntılarını öğrenmek [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).
* Arama [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates) farklı Resource Manager şablonları örneklerini için.
