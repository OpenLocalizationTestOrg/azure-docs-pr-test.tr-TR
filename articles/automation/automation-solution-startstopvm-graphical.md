---
title: "Başlatma ve sanal makineler - grafik durdurma | Microsoft Docs"
description: "Azure otomasyonu senaryosu Klasik sanal makineleri durdurmak ve başlatmak için runbook'ları da dahil olmak üzere bir PowerShell iş akışı sürümü."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 338d5712239356e13cbf480d9655ca3ca499701d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Başlatma ve durdurma sanal makineler, azure otomasyonu senaryosu-
Bu Azure otomasyonu senaryosu Klasik sanal makineleri durdurmak ve başlatmak için runbook'ları içerir.  Bu senaryo herhangi birini kullanabilirsiniz:  

* Değişiklik yapmadan runbook'ları, kendi ortamınızda kullanın.
* Özelleştirilmiş işlevleri gerçekleştirmek için runbook'ları değiştirin.  
* Runbook'ları çözümü genelinin bir parçası olarak başka bir runbook'tan çağırın.
* Runbook'ları öğreticileri runbook kavramları yazma öğrenmek için kullanın.

> [!div class="op_single_selector"]
> * [Grafik](automation-solution-startstopvm-graphical.md)
> * [PowerShell İş Akışı](automation-solution-startstopvm-psworkflow.md)
>
>

Bu senaryo grafik runbook sürümüdür. Ayrıca kullanılabilir kullanarak olan [PowerShell iş akışı runbook'ları](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-the-scenario"></a>Senaryoyu alma
Bu senaryo iki oluşur, aşağıdaki bağlantılardan birini yükleyebilirsiniz iki grafik runbook'lar.  Bkz: [PowerShell iş akışı sürümü](automation-solution-startstopvm-psworkflow.md) PowerShell iş akışı runbook'ları bağlantılar için bu senaryonun.

| Runbook | Bağlantı | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Azure Klasik VM grafik Runbook başlatın](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Grafik |Tüm Klasik sanal makineleri bir Azure aboneliği veya tüm sanal makinelerin belirli bir hizmet adı ile başlatır. |
| StopAzureClassicVM |[Azure Klasik VM grafik Runbook'u durdurun](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Grafik |Tüm sanal makinelerin bir Otomasyon hesabı veya belirli bir hizmet adı ile tüm sanal makineleri durdurur. |

## <a name="installing-and-configuring-the-scenario"></a>Yükleme ve yapılandırma senaryosu
### <a name="1-install-the-runbooks"></a>1. Runbook'ları yükleyin
Runbook'ları indirdikten sonra bunları yordamı kullanarak aktarabilirsiniz [grafik runbook yordamları](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-the-description-and-requirements"></a>2. Açıklama ve gereksinimleri gözden geçirin
Adlı bir etkinliği runbook'ları dahil **beni oku** bir açıklama ve gerekli varlıkları içerir.  Bu bilgileri seçerek görüntüleyebilirsiniz **beni oku** etkinliği ve ardından **iş akışı betiği** parametresi.  Bu makalede aynı bilgiler de alabilirsiniz.

### <a name="3-configure-assets"></a>3. Varlıklar yapılandırın
Runbook'ları oluşturma ve uygun değerlerle doldurmak şu varlıkları gerektirir.  Varsayılan adlardır.  Bu adları belirtirseniz, farklı adlara sahip varlıklar kullanabilirsiniz [giriş parametreleri](#using-the-runbooks) runbook'u başlattığınızda.

| Varlık türü | Varsayılan adı | Açıklama |
|:--- |:--- |:--- |:--- |
| [Kimlik bilgisi](automation-credentials.md) |AzureCredential |Azure Abonelikteki sanal makineleri durdurmak ve başlatmak için yetkili olan bir hesabın kimlik bilgilerini içerir. |
| [Değişken](automation-variables.md) |Azuresubscriptionıd |Azure aboneliğiniz abonelik Kimliğini içerir. |

## <a name="using-the-scenario"></a>Senaryo kullanma
### <a name="parameters"></a>Parametreler
Her runbook aşağıdakilere sahip [giriş parametreleri](automation-starting-a-runbook.md#runbook-parameters).  Zorunlu parametreler için değer sağlamalısınız ve değerleri gereksinimlerinize bağlı olarak diğer parametreleri için isteğe bağlı olarak sağlayabilir.

| Parametre | Tür | Zorunlu | Açıklama |
|:--- |:--- |:--- |:--- |
| ServiceName |Dize |Hayır |Bir değer belirtilirse, hizmet adının tüm sanal makinelerle başlatıldığı veya durdurulduğu sonra.  Herhangi bir değer sağlanmazsa, ardından Azure Abonelikteki tüm Klasik sanal makineleri başlatıldığı veya durdurulduğu. |
| AzureSubscriptionIdAssetName |Dize |Hayır |Adını içeren [değişken varlığı](#installing-and-configuring-the-scenario) , Azure aboneliğinizin abonelik Kimliğini içerir.  Bir değer belirtmezseniz *Azuresubscriptionıd* kullanılır. |
| AzureCredentialAssetName |Dize |Hayır |Adını içeren [kimlik bilgisi varlığı](#installing-and-configuring-the-scenario) runbook'un kimlik bilgilerini içerir.  Bir değer belirtmezseniz *AzureCredential* kullanılır. |

### <a name="starting-the-runbooks"></a>Runbook'ları başlatma
Yöntemlerden birini kullanabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) runbook'ları ya da bu makalede başlatmak için.

Aşağıdaki örnek komutlar çalıştırmak için Windows PowerShell kullanan **StartAzureClassicVM** tüm sanal makinelerin hizmet adı ile başlatmak için *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Çıktı
Runbook'ları olacak [bir çıktı mesajı](automation-runbook-output-and-messages.md) Başlat veya Durdur yönerge başarıyla gönderildi olup olmadığını belirten her sanal makine için.  Her runbook için sonucu belirlemek için çıktı belirli bir dizeyi arayabilirsiniz.  Olası çıktı dizeler aşağıdaki tabloda listelenmiştir.

| Runbook | Koşul | İleti |
|:--- |:--- |:--- |
| StartAzureClassicVM |Sanal makine zaten çalışıyor |MyVM zaten çalışıyor |
| StartAzureClassicVM |Başlatma isteği başarıyla gönderildi bir sanal makine için |MyVM başlatıldı |
| StartAzureClassicVM |Sanal makine başlatma isteği başarısız oldu |MyVM başlatılamadı |
| StopAzureClassicVM |Sanal makine zaten çalışıyor |MyVM zaten durdurulmuş |
| StopAzureClassicVM |Başlatma isteği başarıyla gönderildi bir sanal makine için |MyVM başlatıldı |
| StopAzureClassicVM |Sanal makine başlatma isteği başarısız oldu |MyVM başlatılamadı |

Aşağıdadır kullanmanın bir görüntü **StartAzureClassicVM** olarak bir [alt runbook](automation-child-runbooks.md) bir örnek grafik runbook'ta.  Bu aşağıdaki tabloda koşullu bağlantıları kullanır.

| Bağlantı | Ölçütler |
|:--- |:--- |
| Başarılı bağlantı |$ActivityOutput ['StartAzureClassicVM']-gibi "\* başlatıldı" |
| Hata bağlantısı |$ActivityOutput ['StartAzureClassicVM']-notlike "\* başlatıldı" |

![Alt runbook örneği](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Ayrıntılı dökümü
Bu senaryoda runbook'ları ayrıntılı bir dökümünü aşağıdadır.  Runbook'ları özelleştirme veya sadece kendi Otomasyon senaryoları yazmak için bunlardan öğrenmek için bu bilgileri kullanın.

### <a name="authentication"></a>Kimlik Doğrulaması
![Kimlik Doğrulaması](media/automation-solution-startstopvm/graphical-authentication.png)

Runbook ayarlamak için etkinlikleri ile başlayan [kimlik bilgileri](automation-credentials.md) ve runbook geri kalanı için kullanılacak Azure aboneliği.

İlk iki etkinlik **abonelik kimliği Al** ve **Azure kimlik bilgisi almak**, almak [varlıklar](#installing-the-runbook) sonraki iki etkinlikler tarafından kullanılır.  Bu etkinlikler doğrudan varlıklar belirtebilirsiniz, ancak bunlar varlık adları gerekir.  Biz bu adlarında belirtmesini izin vererek bu yana [giriş parametreleri](#using-the-runbooks), bir giriş parametresi tarafından belirtilen bir adla varlıkları almak için bu etkinlikler ihtiyacımız.

**Add-AzureAccount** runbook geri kalanı için kullanılacak kimlik bilgilerini ayarlar.  Gelen alır. kimlik bilgisi varlığı **Azure kimlik bilgisi almak** Azure Abonelikteki sanal makineleri durdurmak ve başlatmak için erişimi olmalıdır.  Tarafından kullanılan abonelik seçili **Select-AzureSubscription** abonelik kimliği kullanan gelen **abonelik kimliği Al**.

### <a name="get-virtual-machines"></a>Sanal makinelerini Al
![VM Al](media/automation-solution-startstopvm/graphical-getvms.png)

Runbook ile çalışacaksınız hangi sanal makinelerin ve olup Bunlar zaten başlatıldığında veya (bağlı olarak runbook) durduruldu belirlemesi gerekir.   İki etkinliklerden birini VM'ler alır.  **Sanal makineleri hizmetinde almak** çalışacak *ServiceName* runbook giriş parametresi bir değer içeriyor.  **Tüm sanal makineleri almak** çalışacak *ServiceName* runbook giriş parametresi değeri içermiyor.  Bu mantık, her etkinlik önceki koşullu bağlantılar tarafından gerçekleştirilir.

Her iki etkinlikleri kullanmak **Get-AzureVM** cmdlet'i.  **Tüm sanal makineleri almak** kullanan **ListAllVMs** parametre tüm sanal makineleri dönün.  **Sanal makineleri hizmetinde almak** kullanan **GetVMByServiceAndVMName** parametre kümesi ve sağlayan **ServiceName** giriş parametresi için **ServiceName** parametre.  

### <a name="merge-vms"></a>Sanal makineleri birleştirme
![Sanal makineleri birleştirme](media/automation-solution-startstopvm/graphical-mergevms.png)

**Birleştirme VM'ler** etkinliktir giriş sağlamak için gerekli **Start-AzureVM** hizmeti başlatmak için sanal makine adını ve adı gerekiyor.  Giriş herhangi birinden gelebilir **tüm sanal makineleri almak** veya **alma VM'ler hizmetindeki**, ancak **Start-AzureVM** yalnızca kendi giriş için bir etkinlik belirtebilirsiniz.   

Senaryo oluşturmaktır **birleştirme VM'ler** çalıştığı **Write-Output** cmdlet'i.  **Inputobject** Bu cmdlet'i yönelik parametre, önceki iki etkinlik girişi birleştiren bir PowerShell ifadesi değil.  Bu etkinlikler yalnızca biri dolayısıyla yalnızca tek bir çıktı kümesini beklenen çalışır.  **Start-AzureVM** bu çıkışı giriş parametreleri için kullanabilirsiniz.

### <a name="startstop-virtual-machines"></a>Sanal makineleri Başlatma/Durdurma
![Sanal makineleri Başlat](media/automation-solution-startstopvm/graphical-startvm.png) ![Sanal makineleri Durdur](media/automation-solution-startstopvm/graphical-stopvm.png)

Runbook bağlı olarak sonraki etkinlikleri başlatmak veya runbook kullanmayı girişiminde **Start-AzureVM** veya **Stop-AzureVM**.  Etkinlik tarafından ardışık düzen bağlantısına öncesinde olduğundan, bu kez döndürülen her nesne için çalışır **birleştirme VM'ler**.  Etkinlik varsa yalnızca çalıştıracağı koşullu bağlantıdır *RunningState* sanal makinenin *durduruldu* için **Start-AzureVM** ve *başlatıldı*  için **Stop-AzureVM**. Bu durum, ardından uyulmazsa **zaten başlatıldığında bildir** veya **bildir zaten durdurulmuş** bir ileti göndermek için Çalıştır'ı kullanarak **Write-Output**.

### <a name="send-output"></a>Çıktı Gönder
![Başlangıç VM'ler bildir](media/automation-solution-startstopvm/graphical-notifystart.png) ![Stop VM'ler bildir](media/automation-solution-startstopvm/graphical-notifystop.png)

Son adım runbook'taki her bir sanal makine için başlatma veya durdurma isteği başarıyla gönderildi olup olmadığını çıkış göndermektir. Ayrı bir yoktur **Write-Output** her biri için etkinlik ve hangisinin koşullu bağlantılarla çalıştırmak için belirleriz.  **VM başlatıldığında bildir** veya **bildir VM durduruldu** çalıştırılır *OperationStatus* olan *başarılı*.  Varsa *OperationStatus* diğer herhangi bir değer ise **bildir başarısız başlatmak** veya **Dur için başarısız olduğunda bildir** çalıştırılır.

## <a name="next-steps"></a>Sonraki adımlar
* [Grafik Azure Otomasyonu'nda yazma](automation-graphical-authoring-intro.md)
* [Azure Otomasyonu'nda alt runbook'lar](automation-child-runbooks.md)
* [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md)
