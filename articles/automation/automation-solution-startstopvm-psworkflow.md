---
title: "Başlatma ve durdurma Azure Otomasyonu - PowerShell iş akışı sanal makinelerle | Microsoft Docs"
description: "Klasik sanal makineleri durdurmak ve başlatmak için runbook'ları da dahil olmak üzere Azure otomasyonu senaryosu grafik sürümü."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
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

Bu PowerShell iş akışı runbook bu senaryo sürümüdür. Ayrıca kullanılabilir kullanarak olan [grafik runbook'lar](automation-solution-startstopvm-graphical.md).

## <a name="getting-the-scenario"></a>Senaryoyu alma
Bu senaryo, aşağıdaki bağlantılardan birini yükleyebilirsiniz iki PowerShell iş akışı runbook oluşur.  Bkz: [grafik sürümünü](automation-solution-startstopvm-graphical.md) bağlantıları grafik runbook'lar için bu senaryonun.

| Runbook | Bağlantı | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Azure Klasik sanal makineleri Başlat](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |PowerShell iş akışı |Tüm Klasik sanal makineleri bir Azure subscriptionor içinde tüm sanal makinelerin belirli bir hizmet adı ile başlar. |
| Stop-AzureVMs |[Azure Klasik Vm'leri Durdur](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |PowerShell iş akışı |Tüm sanal makinelerin bir Otomasyon hesabı veya belirli bir hizmet adı ile tüm sanal makineleri durdurur. |

## <a name="installing-and-configuring-the-scenario"></a>Yükleme ve yapılandırma senaryosu
### <a name="1-install-the-runbooks"></a>1. Runbook'ları yükleyin
Runbook'ları indirdikten sonra bunları yordamı kullanarak aktarabilirsiniz [bir Runbook'u içeri aktarma](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-the-description-and-requirements"></a>2. Açıklama ve gereksinimleri gözden geçirin
Runbook'ları bir açıklama ve gerekli varlıkları içerir açıklamalı Yardım metni içerir.  Bu makalede aynı bilgiler de alabilirsiniz.

### <a name="3-configure-assets"></a>3. Varlıklar yapılandırın
Runbook'ları oluşturma ve uygun değerlerle doldurmak şu varlıkları gerektirir.

| Varlık türü | Varlık adı | Açıklama |
|:--- |:--- |:--- |:--- |
| Kimlik Bilgisi |AzureCredential |Azure Abonelikteki sanal makineleri durdurmak ve başlatmak için yetkili olan bir hesabın kimlik bilgilerini içerir.  Alternatif olarak, başka bir kimlik bilgisi varlığı belirtebilirsiniz **kimlik bilgisi** parametresinin **Add-AzureAccount** etkinlik. |
| Değişken |Azuresubscriptionıd |Azure aboneliğiniz abonelik Kimliğini içerir. |

## <a name="using-the-scenario"></a>Senaryo kullanma
### <a name="parameters"></a>Parametreler
Her runbook aşağıdaki parametreleri var.  Zorunlu parametreler için değer sağlamalısınız ve değerleri gereksinimlerinize bağlı olarak diğer parametreleri için isteğe bağlı olarak sağlayabilir.

| Parametre | Tür | Zorunlu | Açıklama |
|:--- |:--- |:--- |:--- |
| ServiceName |Dize |Hayır |Bir değer belirtilirse, hizmet adının tüm sanal makinelerle başlatıldığı veya durdurulduğu sonra.  Herhangi bir değer sağlanmazsa, ardından Azure Abonelikteki tüm Klasik sanal makineleri başlatıldığı veya durdurulduğu. |
| AzureSubscriptionIdAssetName |Dize |Hayır |Adını içeren [değişken varlığı](#installing-and-configuring-the-scenario) , Azure aboneliğinizin abonelik Kimliğini içerir.  Bir değer belirtmezseniz *Azuresubscriptionıd* kullanılır. |
| AzureCredentialAssetName |Dize |Hayır |Adını içeren [kimlik bilgisi varlığı](#installing-and-configuring-the-scenario) runbook'un kimlik bilgilerini içerir.  Bir değer belirtmezseniz *AzureCredential* kullanılır. |

### <a name="starting-the-runbooks"></a>Runbook'ları başlatma
Yöntemlerden birini kullanabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) runbook'ları ya da bu senaryoda başlatmak için.

Aşağıdaki örnek komutlar çalıştırmak için Windows PowerShell kullanan **StartAzureVMs** tüm sanal makinelerin hizmet adı ile başlatmak için *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Çıktı
Runbook'ları olacak [bir çıktı mesajı](automation-runbook-output-and-messages.md) Başlat veya Durdur yönerge başarıyla gönderildi olup olmadığını belirten her sanal makine için.  Her runbook için sonucu belirlemek için çıktı belirli bir dizeyi arayabilirsiniz.  Olası çıktı dizeler aşağıdaki tabloda listelenmiştir.

| Runbook | Koşul | İleti |
|:--- |:--- |:--- |
| Start-AzureVMs |Sanal makine zaten çalışıyor |MyVM zaten çalışıyor |
| Start-AzureVMs |Başlatma isteği başarıyla gönderildi bir sanal makine için |MyVM başlatıldı |
| Start-AzureVMs |Sanal makine başlatma isteği başarısız oldu |MyVM başlatılamadı |
| Stop-AzureVMs |Sanal makine zaten durdurulmuş |MyVM zaten durdurulmuş |
| Stop-AzureVMs |Durdurma isteği başarıyla gönderildi bir sanal makine için |MyVM durduruldu |
| Stop-AzureVMs |Sanal makine durdurma isteği başarısız oldu |MyVM durdurulamadı |

Örneğin, tüm sanal makinelerin hizmet adı ile başlatmak aşağıdaki kod parçacığını bir runbook'tan çalışır *MyServiceName*.  Varsa Başlangıç istekleri başarısız hata eylemleri alınabilir.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Ayrıntılı dökümü
Bu senaryoda runbook'ları ayrıntılı bir dökümünü aşağıdadır.  Runbook'ları özelleştirme veya sadece kendi Otomasyon senaryoları yazmak için bunlardan öğrenmek için bu bilgileri kullanın.

### <a name="parameters"></a>Parametreler
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

İş akışı için değerleri alarak başlatır [giriş parametreleri](#using-the-scenario).  Varlık adları sağlanmadığında varsayılan adları kullanılır.

### <a name="output"></a>Çıktı
    # Returns strings with status messages
    [OutputType([String])]

Bu satır, runbook çıkışını bir dize olacağını bildirir.  Bu gerekli değildir, ancak runbook olarak kullanıldığında için en iyi uygulamadır bir [alt runbook](automation-child-runbooks.md) üst runbook beklenecek çıktı türü bilmesini.

### <a name="authentication"></a>Kimlik Doğrulaması
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

Sonraki satırları kümesi [kimlik bilgileri](automation-credentials.md) ve runbook geri kalanı için kullanılacak Azure aboneliği.
İlk kullanırız **Get-AutomationPSCredential** Azure Abonelikteki sanal makineleri durdurmak ve başlatmak için erişim kimlik bilgilerini tutan varlık almak için. **Add-AzureAccount** kimlik bilgilerini ayarlamak için bu varlık kullanır.  Runbook çıktısında dahil edilmemiştir böylece çıkış kukla bir değişkene atanır.  

Değişken varlığı kimliği ile alınan sonra abonelik ile **Get-AutomationVariable** ve kümesiyle abonelik **Select-AzureSubscription**.

### <a name="get-vms"></a>VM Al
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** runbook ile çalışır sanal makineleri almak için kullanılır.  İçinde bir değer sağlanmazsa **ServiceName** giriş değişken, yalnızca sanal makineler, hizmet adı ile alınan sonra.  Varsa **ServiceName** tüm sanal makineleri aldıktan sonra boştur.

### <a name="startstop-virtual-machines-and-send-output"></a>Sanal makineleri Başlat/Durdur ve çıktı gönderin
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

Sonraki satırların her sanal makineye üzerinden adım.  İlk **PowerState** sanal makinesini, zaten çalışıyor veya durdurulmuştur runbook'a bağlı olup olmadığını görmek için denetlenir.  Bunu zaten hedef durumdaysa, bir ileti çıkış ve runbook sona erer gönderilir.  Aksi durumda, ardından **Start-AzureVM** veya **Stop-AzureVM** başlatmak veya durdurmak için bir değişken depolanan isteğinin sonucunu sanal makineyle girişimi için kullanılır.  Bir ileti başlatma veya durdurma isteği başarıyla gönderildi belirtme çıktı gönderilir.

## <a name="next-steps"></a>Sonraki adımlar
* Alt runbook'larla çalışma hakkında daha fazla bilgi için bkz: [Azure Otomasyonu'nda alt runbook'lar](automation-child-runbooks.md)
* Runbook yürütme ve gidermenize yardımcı olması için günlüğe kaydetme sırasında çıkış iletileri hakkında daha fazla bilgi için bkz: [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md)

