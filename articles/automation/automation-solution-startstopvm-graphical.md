---
title: aaaStarting ve durdurma sanal makineleri - Graph | Microsoft Docs
description: "PowerShell iş akışı runbook'ları toostart ve durdurma Klasik sanal makineler de dahil olmak üzere Azure otomasyonu senaryosu sürümü."
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
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Başlatma ve durdurma sanal makineler, azure otomasyonu senaryosu-
Bu Azure otomasyonu senaryosu runbook'lar toostart ve durdurma Klasik sanal makineleri içerir.  Bu senaryo hello aşağıdakilerden birini kullanabilirsiniz:  

* Değişiklik yapmadan Hello runbook'ları, kendi ortamınızda kullanın.
* Merhaba runbook'lar özelleştirilmiş tooperform işlevlerini değiştirin.  
* Merhaba runbook çözümü genelinin bir parçası olarak başka bir runbook'tan çağırın.
* Merhaba runbook'lar öğreticileri toolearn runbook kavramları yazma kullanın.

> [!div class="op_single_selector"]
> * [Grafik](automation-solution-startstopvm-graphical.md)
> * [PowerShell İş Akışı](automation-solution-startstopvm-psworkflow.md)
>
>

Bu hello grafik runbook bu senaryonun sürümüdür. Ayrıca kullanılabilir kullanarak olan [PowerShell iş akışı runbook'ları](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Merhaba senaryo alma
Bu senaryo iki oluşur indirebileceğiniz iki grafik runbook'lar hello bağlantılar.  Merhaba bkz [PowerShell iş akışı sürümü](automation-solution-startstopvm-psworkflow.md) bu senaryonun bağlantılar toohello PowerShell iş akışı runbook'ları için.

| Runbook | Bağlantı | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Azure Klasik VM grafik Runbook başlatın](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Grafik |Tüm Klasik sanal makineleri bir Azure aboneliği veya tüm sanal makinelerin belirli bir hizmet adı ile başlatır. |
| StopAzureClassicVM |[Azure Klasik VM grafik Runbook'u durdurun](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Grafik |Tüm sanal makinelerin bir Otomasyon hesabı veya belirli bir hizmet adı ile tüm sanal makineleri durdurur. |

## <a name="installing-and-configuring-hello-scenario"></a>Yükleme ve yapılandırma hello senaryosu
### <a name="1-install-hello-runbooks"></a>1. Merhaba runbook'ları yükleyin
Merhaba runbook'ları indirdikten sonra bunları aktarabilirsiniz hello yordamda kullanarak [grafik runbook yordamları](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Gözden geçirme hello açıklama ve gereksinimleri
Merhaba runbook'ları dahil olarak adlandırılan bir etkinlik **beni oku** bir açıklama ve gerekli varlıkları içerir.  Merhaba seçerek bu bilgiyi görüntüleyebilirsiniz **beni oku** etkinliği ve hello **iş akışı betiği** parametresi.  Ayrıca alabilirsiniz hello Bu makale aynı bilgileri.

### <a name="3-configure-assets"></a>3. Varlıklar yapılandırın
Merhaba runbook'lar oluşturmak ve uygun değerlerle doldurmak varlıklar aşağıdaki hello gerektirir.  Merhaba, varsayılan adlardır.  Bu adları hello belirtirseniz, farklı adlara sahip varlıklar kullanabilirsiniz [giriş parametreleri](#using-the-runbooks) hello runbook başlattığınızda.

| Varlık türü | Varsayılan adı | Açıklama |
|:--- |:--- |:--- |:--- |
| [Kimlik bilgisi](automation-credentials.md) |AzureCredential |Yetkilisi toostart ve durdurma sanal makineler hello Azure aboneliğine sahip bir hesabın kimlik bilgilerini içerir. |
| [Değişken](automation-variables.md) |Azuresubscriptionıd |Merhaba abonelik kimliği, Azure aboneliğinizin yer alır. |

## <a name="using-hello-scenario"></a>Merhaba senaryo kullanma
### <a name="parameters"></a>Parametreler
Merhaba runbook'lar her hello aşağıdakilere sahip [giriş parametreleri](automation-starting-a-runbook.md#runbook-parameters).  Zorunlu parametreler için değer sağlamalısınız ve değerleri gereksinimlerinize bağlı olarak diğer parametreleri için isteğe bağlı olarak sağlayabilir.

| Parametre | Tür | Zorunlu | Açıklama |
|:--- |:--- |:--- |:--- |
| ServiceName |Dize |Hayır |Bir değer belirtilirse, hizmet adının tüm sanal makinelerle başlatıldığı veya durdurulduğu sonra.  Herhangi bir değer sağlanmazsa, ardından hello Azure aboneliği tüm Klasik sanal makinelerin başlatıldığı veya durdurulduğu. |
| AzureSubscriptionIdAssetName |Dize |Hayır |Merhaba Hello adını içeren [değişken varlığı](#installing-and-configuring-the-scenario) hello abonelik kimliği, Azure aboneliğinizin içerir.  Bir değer belirtmezseniz *Azuresubscriptionıd* kullanılır. |
| AzureCredentialAssetName |Dize |Hayır |Merhaba Hello adını içeren [kimlik bilgisi varlığı](#installing-and-configuring-the-scenario) hello runbook toouse hello kimlik bilgilerini içerir.  Bir değer belirtmezseniz *AzureCredential* kullanılır. |

### <a name="starting-hello-runbooks"></a>Başlangıç hello runbook'ları
Merhaba yöntemlerden herhangi birini kullanabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) toostart ya da bu makalede hello runbook'lar.

Aşağıdaki örnek komutlar hello kullanan Windows PowerShell toorun **StartAzureClassicVM** toostart hello hizmet adı ile tüm sanal makineleri *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Çıktı
Merhaba runbook'ları olacak [bir çıktı mesajı](automation-runbook-output-and-messages.md) her sanal makine belirten desteklemediğini hello Başlat veya Durdur yönerge başarıyla gönderildiği.  Merhaba çıktı toodetermine hello sonuç her runbook için belirli bir dizeyi arayabilirsiniz.  Merhaba olası çıktı dizeleri aşağıdaki tablonun hello listelenir.

| Runbook | Koşul | İleti |
|:--- |:--- |:--- |
| StartAzureClassicVM |Sanal makine zaten çalışıyor |MyVM zaten çalışıyor |
| StartAzureClassicVM |Başlatma isteği başarıyla gönderildi bir sanal makine için |MyVM başlatıldı |
| StartAzureClassicVM |Sanal makine başlatma isteği başarısız oldu |MyVM toostart başarısız oldu |
| StopAzureClassicVM |Sanal makine zaten çalışıyor |MyVM zaten durdurulmuş |
| StopAzureClassicVM |Başlatma isteği başarıyla gönderildi bir sanal makine için |MyVM başlatıldı |
| StopAzureClassicVM |Sanal makine başlatma isteği başarısız oldu |MyVM toostart başarısız oldu |

Aşağıdadır hello kullanarak bir görüntü **StartAzureClassicVM** olarak bir [alt runbook](automation-child-runbooks.md) bir örnek grafik runbook'ta.  Bu, aşağıdaki tablonun hello hello koşullu bağlantıları kullanır.

| Bağlantı | Ölçütler |
|:--- |:--- |
| Başarılı bağlantı |$ActivityOutput ['StartAzureClassicVM']-gibi "\* başlatıldı" |
| Hata bağlantısı |$ActivityOutput ['StartAzureClassicVM']-notlike "\* başlatıldı" |

![Alt runbook örneği](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Ayrıntılı dökümü
Bu senaryoda hello runbook'lar ayrıntılı bir dökümünü aşağıdadır.  Bu bilgileri kullanabilir tooeither özelleştirme hello runbook'ları veya bunlardan yalnızca toolearn kendi Otomasyon senaryoları yazma.

### <a name="authentication"></a>Kimlik Doğrulaması
![Kimlik Doğrulaması](media/automation-solution-startstopvm/graphical-authentication.png)

Merhaba runbook etkinlikleri tooset hello ile başlatır [kimlik bilgileri](automation-credentials.md) ve hello runbook hello kalanı için kullanılacak Azure aboneliği.

ilk iki etkinlik hello **abonelik kimliği Al** ve **Azure kimlik bilgisi almak**, hello almak [varlıklar](#installing-the-runbook) hello sonraki iki etkinlikler tarafından kullanılır.  Bu etkinlikler doğrudan hello varlıklar belirtebilirsiniz, ancak bunlar hello varlık adları gerekir.  Biz hello kullanıcı toospecify hello adları izin beri [giriş parametreleri](#using-the-runbooks), bu etkinlikler tooretrieve hello varlıkları bir giriş parametresi tarafından belirtilen bir adla ihtiyacımız.

**Add-AzureAccount** hello hello runbook hello kalanı için kullanılacak kimlik bilgilerini ayarlar.  Bunu alır hello kimlik bilgisi varlığı **Azure kimlik bilgisi almak** erişim toostart ve durdurma sanal makineleri hello Azure aboneliğinizin olması gerekir.  Merhaba kullanılan abonelik tarafından seçilen **Select-AzureSubscription** hello abonelik kimliği kullanan gelen **abonelik kimliği Al**.

### <a name="get-virtual-machines"></a>Sanal makinelerini Al
![VM Al](media/automation-solution-startstopvm/graphical-getvms.png)

Merhaba runbook hangi sanal makinelerin bu ile çalışacaksınız toodetermine ve olup Bunlar zaten başlatıldığında veya (Merhaba runbook bağlı olarak) durduruldu gerekir.   İki etkinliklerden birini hello VM'ler alır.  **Hizmetinde VM'ler alma** hello çalışacak *ServiceName* giriş parametresi hello runbook için bir değer içeriyor.  **Tüm sanal makineleri almak** hello çalışacak *ServiceName* hello runbook giriş parametresi değeri içermiyor.  Bu mantık hello koşullu bağlantıları her etkinlik önceki tarafından gerçekleştirilir.

Her iki etkinlikleri hello kullanır **Get-AzureVM** cmdlet'i.  **Tüm sanal makineleri almak** kullanır hello **ListAllVMs** parametre tooreturn tüm sanal makineler.  **Hizmetinde VM'ler alma** kullanır hello **GetVMByServiceAndVMName** parametre kümesi ve hello sağlayan **ServiceName** hello için giriş parametresi **ServiceName**parametresi.  

### <a name="merge-vms"></a>Sanal makineleri birleştirme
![Sanal makineleri birleştirme](media/automation-solution-startstopvm/graphical-mergevms.png)

Merhaba **birleştirme VM'ler** etkinliktir çok giriş gerekli tooprovide**Start-AzureVM** hello adı ve hello sanal makine toostart hizmet adı gerekiyor.  Giriş herhangi birinden gelebilir **tüm sanal makineleri almak** veya **alma VM'ler hizmetindeki**, ancak **Start-AzureVM** yalnızca kendi giriş için bir etkinlik belirtebilirsiniz.   

Merhaba senaryodur toocreate **birleştirme VM'ler** hello çalıştığı **Write-Output** cmdlet'i.  Merhaba **Inputobject** Bu cmdlet parametresi hello giriş hello önceki iki etkinlik birleştiren bir PowerShell ifadesi olmalıdır.  Bu etkinlikler yalnızca biri dolayısıyla yalnızca tek bir çıktı kümesini beklenen çalışır.  **Start-AzureVM** bu çıkışı giriş parametreleri için kullanabilirsiniz.

### <a name="startstop-virtual-machines"></a>Sanal makineleri Başlatma/Durdurma
![Sanal makineleri Başlat](media/automation-solution-startstopvm/graphical-startvm.png) ![Sanal makineleri Durdur](media/automation-solution-startstopvm/graphical-stopvm.png)

Merhaba runbook'a bağlı hello sonraki etkinlikleri toostart denemek veya runbook hello kullanmayı **Start-AzureVM** veya **Stop-AzureVM**.  Ardışık Düzen bağlantısına tarafından Hello etkinlik öncesinde olduğundan, bu kez döndürülen her nesne için çalışır **birleştirme VM'ler**.  Merhaba etkinliği yalnızca hello çalışacak hello bağlantı koşullu, böylelikle *RunningState* Merhaba bir sanal makinedir *durduruldu* için **Start-AzureVM** ve  *Başlatılan* için **Stop-AzureVM**. Bu durum, ardından uyulmazsa **zaten başlatıldığında bildir** veya **bildir zaten durdurulmuş** toosend bir iletiyi kullanarak çalıştırılan **Write-Output**.

### <a name="send-output"></a>Çıktı Gönder
![Başlangıç VM'ler bildir](media/automation-solution-startstopvm/graphical-notifystart.png) ![Stop VM'ler bildir](media/automation-solution-startstopvm/graphical-notifystop.png)

Merhaba son hello runbook toosend çıkış olup başlangıç hello veya her sanal makine durdurma isteği başarıyla gönderildi adımdır. Ayrı bir yoktur **Write-Output** her biri için etkinlik ve hangi bir toorun koşullu bağlantılarla belirleriz.  **VM başlatıldığında bildir** veya **bildir VM durduruldu** çalıştırılır *OperationStatus* olan *başarılı*.  Varsa *OperationStatus* diğer herhangi bir değer ise **başarısız olduğunda bildir tooStart** veya **başarısız olduğunda bildir tooStop** çalıştırılır.

## <a name="next-steps"></a>Sonraki adımlar
* [Grafik Azure Otomasyonu'nda yazma](automation-graphical-authoring-intro.md)
* [Azure Otomasyonu'nda alt runbook'lar](automation-child-runbooks.md)
* [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md)
