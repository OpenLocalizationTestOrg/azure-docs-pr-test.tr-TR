---
title: "Azure Otomasyonu - PowerShell iş akışı aaaStarting ve durdurma sanal makinelerle | Microsoft Docs"
description: "Runbook'ları toostart ve durdurma Klasik sanal makineler de dahil olmak üzere Azure otomasyonu senaryosu grafik sürümü."
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
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

Merhaba PowerShell iş akışı runbook sürümü bu senaryonun budur. Ayrıca kullanılabilir kullanarak olan [grafik runbook'lar](automation-solution-startstopvm-graphical.md).

## <a name="getting-hello-scenario"></a>Merhaba senaryo alma
Bu senaryo bağlantılar aşağıdaki hello indirebilirsiniz iki PowerShell iş akışı runbook oluşur.  Merhaba bkz [grafik sürümünü](automation-solution-startstopvm-graphical.md) Bağlantılar toohello grafik runbook'lar için bu senaryonun.

| Runbook | Bağlantı | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Azure Klasik sanal makineleri Başlat](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |PowerShell iş akışı |Tüm Klasik sanal makineleri bir Azure subscriptionor içinde tüm sanal makinelerin belirli bir hizmet adı ile başlar. |
| Stop-AzureVMs |[Azure Klasik Vm'leri Durdur](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |PowerShell iş akışı |Tüm sanal makinelerin bir Otomasyon hesabı veya belirli bir hizmet adı ile tüm sanal makineleri durdurur. |

## <a name="installing-and-configuring-hello-scenario"></a>Yükleme ve yapılandırma hello senaryosu
### <a name="1-install-hello-runbooks"></a>1. Merhaba runbook'ları yükleyin
Merhaba runbook'ları indirdikten sonra bunları aktarabilirsiniz hello yordamda kullanarak [bir Runbook'u içeri aktarma](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-hello-description-and-requirements"></a>2. Gözden geçirme hello açıklama ve gereksinimleri
Merhaba runbook'ları bir açıklama ve gerekli varlıkları içerir açıklamalı Yardım metni içerir.  Ayrıca alabilirsiniz hello Bu makale aynı bilgileri.

### <a name="3-configure-assets"></a>3. Varlıklar yapılandırın
Merhaba runbook'lar oluşturmak ve uygun değerlerle doldurmak varlıklar aşağıdaki hello gerektirir.

| Varlık türü | Varlık adı | Açıklama |
|:--- |:--- |:--- |:--- |
| Kimlik Bilgisi |AzureCredential |Yetkilisi toostart ve durdurma sanal makineler hello Azure aboneliğine sahip bir hesabın kimlik bilgilerini içerir.  Alternatif olarak, başka bir kimlik bilgisi varlığı hello belirtebilirsiniz **kimlik bilgisi** hello parametresinin **Add-AzureAccount** etkinlik. |
| Değişken |Azuresubscriptionıd |Merhaba abonelik kimliği, Azure aboneliğinizin yer alır. |

## <a name="using-hello-scenario"></a>Merhaba senaryo kullanma
### <a name="parameters"></a>Parametreler
Merhaba runbook'lar şu parametreler hello vardır.  Zorunlu parametreler için değer sağlamalısınız ve değerleri gereksinimlerinize bağlı olarak diğer parametreleri için isteğe bağlı olarak sağlayabilir.

| Parametre | Tür | Zorunlu | Açıklama |
|:--- |:--- |:--- |:--- |
| ServiceName |Dize |Hayır |Bir değer belirtilirse, hizmet adının tüm sanal makinelerle başlatıldığı veya durdurulduğu sonra.  Herhangi bir değer sağlanmazsa, ardından hello Azure aboneliği tüm Klasik sanal makinelerin başlatıldığı veya durdurulduğu. |
| AzureSubscriptionIdAssetName |Dize |Hayır |Merhaba Hello adını içeren [değişken varlığı](#installing-and-configuring-the-scenario) hello abonelik kimliği, Azure aboneliğinizin içerir.  Bir değer belirtmezseniz *Azuresubscriptionıd* kullanılır. |
| AzureCredentialAssetName |Dize |Hayır |Merhaba Hello adını içeren [kimlik bilgisi varlığı](#installing-and-configuring-the-scenario) hello runbook toouse hello kimlik bilgilerini içerir.  Bir değer belirtmezseniz *AzureCredential* kullanılır. |

### <a name="starting-hello-runbooks"></a>Başlangıç hello runbook'ları
Merhaba yöntemlerden herhangi birini kullanabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) toostart ya da bu senaryoda hello runbook'lar.

Aşağıdaki örnek komutlar hello kullanan Windows PowerShell toorun **StartAzureVMs** toostart hello hizmet adı ile tüm sanal makineleri *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Çıktı
Merhaba runbook'ları olacak [bir çıktı mesajı](automation-runbook-output-and-messages.md) her sanal makine belirten desteklemediğini hello Başlat veya Durdur yönerge başarıyla gönderildiği.  Merhaba çıktı toodetermine hello sonuç her runbook için belirli bir dizeyi arayabilirsiniz.  Merhaba olası çıktı dizeleri aşağıdaki tablonun hello listelenir.

| Runbook | Koşul | İleti |
|:--- |:--- |:--- |
| Start-AzureVMs |Sanal makine zaten çalışıyor |MyVM zaten çalışıyor |
| Start-AzureVMs |Başlatma isteği başarıyla gönderildi bir sanal makine için |MyVM başlatıldı |
| Start-AzureVMs |Sanal makine başlatma isteği başarısız oldu |MyVM toostart başarısız oldu |
| Stop-AzureVMs |Sanal makine zaten durdurulmuş |MyVM zaten durdurulmuş |
| Stop-AzureVMs |Durdurma isteği başarıyla gönderildi bir sanal makine için |MyVM durduruldu |
| Stop-AzureVMs |Sanal makine durdurma isteği başarısız oldu |MyVM toostop başarısız oldu |

Örneğin, bir runbook'tan kod parçacığını aşağıdaki hello toostart hello hizmet adı ile tüm sanal makineler çalışır *MyServiceName*.  Merhaba hiçbirini istekleri başarısız başlatırsanız, hata eylemleri alınabilir.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Ayrıntılı dökümü
Bu senaryoda hello runbook'lar ayrıntılı bir dökümünü aşağıdadır.  Bu bilgileri kullanabilir tooeither özelleştirme hello runbook'ları veya bunlardan yalnızca toolearn kendi Otomasyon senaryoları yazma.

### <a name="parameters"></a>Parametreler
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Merhaba iş akışı için hello başlangıç değerleri alma başlatır [giriş parametreleri](#using-the-scenario).  Merhaba varlık adları sağlanmadığında varsayılan adları kullanılır.

### <a name="output"></a>Çıktı
    # Returns strings with status messages
    [OutputType([String])]

Bu satır hello runbook hello çıkışını bir dize olacağını bildirir.  Bu gerekli değildir ancak hello runbook olarak kullanıldığında için en iyi uygulamadır bir [alt runbook](automation-child-runbooks.md) üst runbook hello çıkış bilmesini tooexpect yazın.

### <a name="authentication"></a>Kimlik Doğrulaması
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

Merhaba sonraki satırları ayarlamak hello [kimlik bilgileri](automation-credentials.md) ve hello runbook hello kalanı için kullanılacak Azure aboneliği.
İlk kullanırız **Get-AutomationPSCredential** hello kimlik bilgileriyle erişim toostart ve durdurma sanal makineleri hello Azure aboneliği tutan tooget hello varlık. **Add-AzureAccount** bu varlık tooset hello kimlik bilgilerini kullanır.  Böylece hello runbook çıktısında dahil edilmemiştir hello çıktı tooa kukla değişkeni atanır.  

Merhaba değişken varlığı kimliği ile alınan sonra hello aboneliğiyle **Get-AutomationVariable** ve kümesiyle hello abonelik **Select-AzureSubscription**.

### <a name="get-vms"></a>VM Al
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** kullanılan tooretrieve olan hello sanal makineleri hello runbook ile çalışır.  Bir değer hello sağladıysanız **ServiceName** giriş değişken sonra yalnızca hello sanal makinelerle hizmet adının alınır.  Varsa **ServiceName** tüm sanal makineleri aldıktan sonra boştur.

### <a name="startstop-virtual-machines-and-send-output"></a>Sanal makineleri Başlat/Durdur ve çıktı gönderin
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

Merhaba sonraki satırları adım her bir sanal makine aracılığıyla.  İlk hello **PowerState** çalışıyor veya durdurulmuştur hello runbook'a bağlı zaten Merhaba sanal makine checked toosee ise.  Zaten bir hello hedef durumda ise, bir ileti toooutput ve hello runbook sona erer gönderilir.  Aksi durumda, ardından **Start-AzureVM** veya **Stop-AzureVM** hello isteği saklı tooa değişkeni hello sonucu ile kullanılan tooattempt toostart veya stop hello sanal makine.  Merhaba isteği toostart veya stop başarıyla gönderildi olup olmadığını toooutput belirten bir ileti sonra gönderilir.

## <a name="next-steps"></a>Sonraki adımlar
* alt runbook'ları ile çalışma hakkında daha fazla toolearn bakın [Azure Otomasyonu'nda alt runbook'lar](automation-child-runbooks.md)
* hakkında daha fazla bilgi toolearn çıkış runbook yürütme ve günlüğe kaydetme toohelp sırasında iletilerinde sorun gidermek için bkz: [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md)

