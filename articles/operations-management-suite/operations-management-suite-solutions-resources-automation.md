---
title: "OMS çözümlerinde aaaAzure Automation kaynaklarını | Microsoft Docs"
description: "OMS çözümlerinde, toplama ve izleme verilerini işleme gibi Azure Otomasyonu tooautomate işlemlerde runbook'ları genellikle dahil edilir.  Bu makalede nasıl tooinclude runbook'ları ve ilgili kaynaklarını bir çözümde."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Azure Otomasyonu kaynakları tooan OMS yönetim çözümü (Önizleme) ekleme
> [!NOTE]
> Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir. Aşağıda açıklanan herhangi bir şema konu toochange ' dir.   


[OMS yönetim çözümlerine](operations-management-suite-solutions.md) toplama ve izleme verilerini işleme gibi Azure Otomasyonu tooautomate işlemlerde runbook'ları tipik olarak içerecektir.  Ayrıca toorunbooks, Automation hesaplarını içerir değişkenleri ve hello çözümde kullanılan hello runbook'ları destek zamanlamaları gibi varlıklar.  Bu makalede nasıl tooinclude runbook'ları ve ilgili kaynaklarını bir çözümde.

> [!NOTE]
> Merhaba bu makaledeki örnekler parametreleri ve ya da gerekli veya ortak toomanagement çözümleri ve açıklanan değişkenleri kullanma [Operations Management Suite (OMS) yönetimi çözümleri oluşturma](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>Ön koşullar
Bu makale, zaten ile Merhaba aşağıdaki bilgilerle aşina olduğunuzu varsayar.

- Nasıl çok[bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md).
- Merhaba yapısını bir [çözüm dosyasını](operations-management-suite-solutions-solution-file.md).
- Nasıl çok[Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Otomasyon hesabı
Azure Otomasyonu tüm kaynakları bulunan bir [Otomasyon hesabı](../automation/automation-security-overview.md#automation-account-overview).  Bölümünde açıklandığı gibi [OMS çalışma ve Automation hesabı](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Otomasyon hesabı hello Yönetimi çözümünde dahil değildir ancak hello çözüm yüklenmeden önce mevcut olması gerekir.  Kullanılabilir değilse, hello çözüm yükleme başarısız olur.

Her Otomasyon kaynağı Hello adını kendi Automation hesabı hello adını içerir.  Bu hello ile Merhaba çözümde yapılır **accountName** runbook kaynak örneği aşağıdaki hello olduğu gibi parametre.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Runbook'lar
Merhaba çözüm yüklendiğinde, oluşturuldukları hello Çözüm dosyasındaki hello çözüm tarafından kullanılan tüm runbook içermelidir.  Yayımlama hello runbook tooa ortak konumu burada çözümünüzü yükleme herhangi bir kullanıcı tarafından erişilebilir şekilde hello şablon hello runbook'ta hello gövdesi yine de içeremez.

[Azure Otomasyonu runbook'u](../automation/automation-runbook-types.md) kaynaklarınız türü **Microsoft.Automation/automationAccounts/runbooks** ve yapı izlenerek hello sahip. Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


Aşağıdaki tablonun hello runbook'lar için Hello özellikleri açıklanmaktadır.

| Özellik | Açıklama |
|:--- |:--- |
| runbookType |Merhaba runbook Hello türlerini belirtir. <br><br> Komut dosyası - PowerShell komut dosyası <br>PowerShell - PowerShell iş akışı <br> GraphPowerShell - grafik PowerShell komut dosyası runbook <br> GraphPowerShellWorkflow - grafik PowerShell iş akışı runbook |
| logProgress |Belirtir olup olmadığını [ilerleme kayıtlarını](../automation/automation-runbook-output-and-messages.md) hello runbook için oluşturulması gerekir. |
| logVerbose |Belirtir olup olmadığını [ayrıntılı kayıtları](../automation/automation-runbook-output-and-messages.md) hello runbook için oluşturulması gerekir. |
| açıklama |Merhaba runbook için isteğe bağlı bir açıklama. |
| publishContentLink |Merhaba runbook Merhaba içeriğine belirtir. <br><br>URI - URI toohello hello runbook'unun içeriğini.  Bu, PowerShell ve komut dosyası runbook'lar için bir .ps1 dosyası ve bir grafik runbook'u dışarı aktarılan grafik runbook dosyası olacaktır.  <br> Sürüm - hello runbook kendi izleme için sürümü. |


## <a name="automation-jobs"></a>Otomasyon işleri
Azure Automation'da bir runbook başlattığınızda bir Otomasyonu işi oluşturur.  Merhaba yönetim çözümü yüklendiğinde bir runbook bir Otomasyon iş kaynak tooyour çözüm tooautomatically başlangıç ekleyebilirsiniz.  Bu yöntem hello çözüm'in ilk yapılandırması için kullanılan genellikle kullanılan toostart runbook'ları kullanılır.  toostart düzenli aralıklarla bir runbook oluşturmak bir [zamanlama](#schedules) ve [iş zamanlaması](#job-schedules)

İş kaynaklarınız türü **Microsoft.Automation/automationAccounts/jobs** ve yapı izlenerek hello sahiptir.  Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

Aşağıdaki tablonun hello Otomasyon işleri için Hello özellikleri açıklanmaktadır.

| Özellik | Açıklama |
|:--- |:--- |
| runbook |Tek bir ad varlık hello runbook toostart hello adı. |
| parametreler |Varlık hello runbook tarafından gerekli her parametre değeri. |

Merhaba iş hello runbook adı ve toohello runbook gönderilen tüm parametre değerleri toobe içerir.  Merhaba iş gereken [bağımlı](operations-management-suite-solutions-solution-file.md#resources) bu yana hello runbook başlatma hello runbook, hello işten daha önce oluşturulmuş olması gerekir.  Başlatılması gereken birden çok runbook varsa, ilk çalışması gereken tüm diğer işler bağımlı bir iş sağlayarak sıralarına tanımlayabilirsiniz.

bir iş kaynağı Hello adı genellikle parametresi tarafından atanan bir GUID içermelidir.  Daha fazla bilgiyi GUID parametreler hakkında [Operations Management Suite (OMS) çözümleri oluşturma](operations-management-suite-solutions-solution-file.md#parameters).  


## <a name="certificates"></a>Sertifikalar
[Azure Otomasyonu sertifika](../automation/automation-certificates.md) bir türüne sahip **Microsoft.Automation/automationAccounts/certificates** ve yapı izlenerek hello sahiptir. Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



Aşağıdaki tablonun hello sertifikaları kaynakların Hello özellikleri açıklanmaktadır.

| Özellik | Açıklama |
|:--- |:--- |
| base64value değeri |Merhaba sertifika Base 64 değeri. |
| parmak izi |Merhaba sertifika parmak izi. |



## <a name="credentials"></a>Kimlik Bilgileri
[Azure Otomasyonu kimlik](../automation/automation-credentials.md) bir türüne sahip **Microsoft.Automation/automationAccounts/credentials** ve yapı izlenerek hello sahiptir.  Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

Aşağıdaki tablonun hello kimlik bilgisi kaynakların Hello özellikleri açıklanmaktadır.

| Özellik | Açıklama |
|:--- |:--- |
| Kullanıcı adı |Merhaba kimlik bilgisi için kullanıcı adı. |
| password |Merhaba kimlik bilgileri parolası. |


## <a name="schedules"></a>Zamanlamalar
[Azure Otomasyon zamanlamaları](../automation/automation-schedules.md) bir türüne sahip **Microsoft.Automation/automationAccounts/schedules** ve yapı izlenerek hello hello sahiptir. Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

Aşağıdaki tablonun hello zamanlama kaynakların Hello özellikleri açıklanmaktadır.

| Özellik | Açıklama |
|:--- |:--- |
| açıklama |Merhaba zamanlama için isteğe bağlı bir açıklama. |
| startTime |Merhaba başlangıç zamanı, zamanlamanın bir DateTime nesnesi olarak belirtir. Dönüştürülen tooa olabiliyorsa bir dize sağlanabilir geçerli tarih saat. |
| IsEnabled |Merhaba zamanlama etkinleştirilip etkinleştirilmeyeceğini belirtir. |
| interval |Merhaba tür hello zamanlaması için aralık.<br><br>günü<br>saat |
| frequency |Zamanlama hello sıklığı gün veya saat cinsinden harekete. |

Zamanlama başlangıç zamanı geçerli saati hello büyük bir değere sahip olması gerekir.  Devam eden toobe yüklü olduğunda bilmesinin yolu yoktur olduğundan bu değer sahip bir değişken sağlayamaz.

İki stratejileri zamanlama kaynakları bir çözümde kullanırken aşağıdaki hello birini kullanın.

- Bir parametre hello başlangıç zamanı hello zamanlama için kullanın.  Merhaba çözüm yüklediğinizde bu hello kullanıcı tooprovide bir değer ister.  Birden çok zamanlama varsa, tek bir parametre birden fazla bunlardan biri için kullanabilirsiniz.
- Merhaba çözüm yüklendiğinde başlayan bir runbook ile Merhaba zamanlamalar oluşturun.  Bu bir saat, ancak içeremez hello kullanıcı toospecify hello gereksinimini kaldırır çözümünüzdeki hello çözüm kaldırıldığında kaldırılacak şekilde hello zamanlama.


### <a name="job-schedules"></a>İş zamanlamaları
İş zamanlaması kaynakları runbook zamanlama ile ilişkilendirin.  Bir türüne sahip **Microsoft.Automation/automationAccounts/jobSchedules** ve yapı izlenerek hello hello sahiptir.  Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


İş zamanlamaları Hello özelliklerini aşağıdaki tablonun hello açıklanmaktadır.

| Özellik | Açıklama |
|:--- |:--- |
| Zamanlama adı |Tek **adı** hello tablosunun hello adı olan varlık. |
| runbook adı  |Tek **adı** hello runbook'un hello ada sahip varlık.  |



## <a name="variables"></a>Değişkenler
[Azure Otomasyon değişkenleri](../automation/automation-variables.md) bir türüne sahip **Microsoft.Automation/automationAccounts/variables** ve yapı izlenerek hello sahiptir.  Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

Aşağıdaki tablonun hello değişken kaynakların Hello özellikleri açıklanmaktadır.

| Özellik | Açıklama |
|:--- |:--- |
| açıklama | Merhaba değişkeni için isteğe bağlı bir açıklama. |
| Isencrypted | Merhaba değişkeni şifrelenmesi gerekip gerekmediğini belirtir. |
| type | Bu özellik şu anda hiçbir etkisi yoktur.  Hello hello değişkeninin veri türü hello ilk değeri tarafından belirlenir. |
| değer | Merhaba değişken değeri. |

> [!NOTE]
> Merhaba **türü** özelliği şu anda hiçbir etkisi oluşturulmakta hello değişkeni.  Merhaba veri türü hello değişkeni için hello değeri tarafından belirlenir.  

Merhaba değişken hello ilk değeri ayarlarsanız, hello doğru veri türü olarak yapılandırılması gerekir.  Aşağıdaki tablonun hello hello farklı veri türlerine izin verilen ve bunların sözdizimi sağlar.  JSON değerlerde beklenen tooalways olduğunu unutmayın hello tırnak işareti içinde özel karakterler ile tırnak içine alınması.  Örneğin, bir dize değeri hello dize tırnak tarafından belirtilmesi (Merhaba kaçış karakteri kullanarak (\\)) sırada sayısal bir değer tek tırnak işareti kümesiyle belirtilmesi.

| Veri türü | Açıklama | Örnek | Çok çözümler|
|:--|:--|:--|:--|
| Dize   | Değeri çift tırnak içine alın.  | "\"Merhaba Dünya\"" | "Hello world" |
| sayısal  | Tek tırnak sahip bir sayısal değer.| "64" | 64 |
| Boole değeri  | **doğru** veya **false** tırnak.  Bu değer küçük harfli olması gerektiğini unutmayın. | "true" | TRUE |
| Tarih saat | Serileştirilmiş tarih değeri.<br>Bu değer için belirli bir tarih PowerShell toogenerate hello ConvertTo-Json cmdlet'ini kullanabilirsiniz.<br>Örnek: get-date "24/5/2017 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>Modüller
Yönetim çözümünüzü toodefine gerekmez [genel modülleri](../automation/automation-integration-modules.md) bunlar her zaman Otomasyon hesabınızda kullanılabilir olacağından, runbook'lar tarafından kullanılır.  Runbook'lar tarafından kullanılan başka bir modül için bir kaynak tooinclude gerekir.

[Tümleştirme modülleri](../automation/automation-integration-modules.md) bir türüne sahip **Microsoft.Automation/automationAccounts/modules** ve yapı izlenerek hello sahiptir.  Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


Aşağıdaki tablonun hello modülü kaynakların Hello özellikleri açıklanmaktadır.

| Özellik | Açıklama |
|:--- |:--- |
| contentLink |Merhaba modülü Merhaba içeriğine belirtir. <br><br>URI - hello modülü URI toohello içeriği.  Bu, PowerShell ve komut dosyası runbook'lar için bir .ps1 dosyası ve bir grafik runbook'u dışarı aktarılan grafik runbook dosyası olacaktır.  <br> Sürüm - hello modülü kendi izleme sürümü. |

Merhaba runbook hello runbook önce oluşturduğu hello modülü kaynak tooensure bağlı.

### <a name="updating-modules"></a>Modülleri güncelleştiriliyor
Bir zamanlama kullanan bir runbook içeren bir yönetim çözümü güncelleştirin ve bu runbook tarafından kullanılan yeni bir modül çözümünüzün hello yeni sürüme sahip hello runbook hello modülü eski sürümü hello kullanabilir.  Runbook'ları çözümünüzdeki aşağıdaki hello içerir ve iş toorun oluşturmak diğer runbook'lar önce.  Bu, herhangi bir modül runbook'lar yüklenen önce gerekli hello güncelleştirildiğini güvence altına alır.

* [Güncelleştirme ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) tüm runbook'ları çözümünüzdeki tarafından kullanılan hello modülleri hello en son sürümü olduğundan emin olun.  
* [ReRegisterAutomationSchedule MS Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) tüm hello runbook'ları kullanmak hello son modüllerle toothem bağlı hello zamanlama kaynakları tooensure yeniden kaydettirin.




## <a name="sample"></a>Örnek
Aşağıdaki kaynakları izleyerek hello içeren içeren bir çözüm örneğidir:

- Runbook.  Ortak bir GitHub deposunda bulunan bir örnek runbook budur.
- Merhaba çözüm yüklendiğinde hello runbook başlatır Otomasyonu işi.
- Zamanlama ve iş toostart hello runbook düzenli aralıklarla zamanlayın.
- Sertifika.
- Kimlik bilgileri.
- Değişkeni.
- Modül.  Merhaba budur [OMSIngestionAPI Modülü](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) veri tooLog Analytics yazma. 

Merhaba örnek kullanır [standart çözüm parametreleri](operations-management-suite-solutions-solution-file.md#parameters) bir çözüm olarak, yaygın olarak kullanılacak değişkenleri toohardcoding değerleri hello kaynak tanımlarında değil.


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>Sonraki adımlar
* [Görünüm tooyour çözüm eklemek](operations-management-suite-solutions-resources-views.md) toovisualize toplanan verileri.
