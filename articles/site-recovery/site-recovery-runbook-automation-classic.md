---
title: "aaaAdd Azure Otomasyonu runbook'ları toorecovery planları hello Klasik Portalı'nda | Microsoft Docs"
description: "Bu makalede, nasıl Azure Site Recovery şimdi kurtarma tooAzure sırasında Azure Otomasyon toocomplete karmaşık görevleri kullanarak tooextend kurtarma planlarını sağlar açıklanmaktadır"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Azure Otomasyonu runbook'ları toorecovery planları hello Klasik portalında ekleme
Bu öğretici, Azure Site Recovery Azure Otomasyonu tooprovide genişletilebilirlik toorecovery planları ile nasıl tümleşik çalıştığını açıklar. Kurtarma planları kurtarma hem çoğaltma toosecondary bulut hem de çoğaltma tooAzure senaryoları için Azure Site Recovery tarafından korunan sanal makinelerinizin düzenleyebilirsiniz. Ayrıca hello kurtarma yaparken yardımcı **tutarlı bir şekilde doğru**, **yinelenebilir**, ve **otomatik**. Sanal makineleri tooAzure başarısız oluyorsa, Azure Automation tümleştirme kurtarma planları genişletir ve yetenek tooexecute runbook'lar, böylece güçlü bir otomatikleştirme görevleri sağlar verir.

Azure Automation hakkında henüz duymuş değil, kaydolma [burada](https://azure.microsoft.com/services/automation/) ve bunların örnek komut dosyası yükleme [burada](https://azure.microsoft.com/documentation/scripts/). Daha fazla bilgi edinin [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) ve Kurtarma'yı kullanarak tooorchestrate kurtarma tooAzure nasıl planları [burada](https://azure.microsoft.com/blog/?p=166264).

Kısa Bu öğreticide, nasıl Azure Otomasyon çalışma kitabı kurtarma planları tümleştirebilirsiniz arar. Biz, daha önce el ile müdahale gerekli basit görevleri otomatik hale getirmek ve nasıl tooconvert bir çoklu adım kurtarma tek tıklamayla kurtarma eyleme bakın. Biz de sorun yaşanırsa nasıl basit bir komut dosyası giderebileceğinizi adresindeki arar.

## <a name="protect-hello-application-tooazure"></a>Merhaba uygulama tooAzure koruma
Bize iki sanal makine içeren basit bir uygulama ile başlar. Burada, Fabrikam HRweb uygulamasının sahip. Fabrikam HRweb frontend ve Fabrikam Hrweb arka Azure Site RECOVERY'yi kullanarak tooAzure korunan hello iki sanal makine var. Azure Site Recovery kullanarak tooprotect hello sanal makineleri hello adımları izleyin.

1. Sanal makineler için korumayı etkinleştirin.
2. Merhaba sanal makinelerin başlangıç çoğaltmasını tamamlamış olmanız ve çoğaltma yapıyorsanız emin olun.
3. Merhaba ilk çoğaltma işlemi tamamlandıktan ve korumalı hello çoğaltma durumunu bildiren kadar bekleyin.

## ![](media/site-recovery-runbook-automation/01.png)
Bu öğreticide, bir kurtarma planı hello Fabrikam HRweb uygulama toofailover hello uygulama tooAzure için oluşturacağız. Ardından biz bunu bir uç nokta Azure sanal makinesi tooserve web sayfalarını bağlantı noktası 80 üzerinden başarısız hello üzerinde oluşturacak bir runbook ile tümleştirir.

Öncelikle, uygulamamız için bir kurtarma planı oluşturalım.

## <a name="create-hello-recovery-plan"></a>Merhaba kurtarma planı oluşturun
toorecover hello uygulama tooAzure toocreate bir kurtarma planı gerekir.
Kurtarma sanal makinelerin hello sırasını belirttiğiniz bir kurtarma planı kullanıyor. 1 grupta Hello sanal makineyi kurtarmak ve ilk başlatın ve hello sanal makine 2 grubundaki izleyin.

Aşağıdaki gibi görünen bir kurtarma planı oluşturun.

![](media/site-recovery-runbook-automation/12.png)

belgeleri okuyun, Kurtarma planları hakkında daha fazla tooread [burada](https://msdn.microsoft.com/library/azure/dn788799.aspx "burada").

Ardından, hello Azure Otomasyonu'nda gerekli yapıları oluşturalım.

## <a name="create-hello-automation-account-and-its-assets"></a>Merhaba Otomasyon hesabı ve varlıklarını oluşturma
Bir Azure Otomasyonu hesabı toocreate runbook'ları gerekir. Bir hesap zaten yoksa tarafından gösterilen tooAzure Otomasyon sekmesine gidin ![](media/site-recovery-runbook-automation/02.png)ve yeni bir hesap oluşturun.

1. Merhaba hesabı adı tooidentify ile verin.
2. Coğrafi bölge tooplace hello hesap istediğiniz yeri belirtin.

Merhaba tooplace hello hesabında önerilen hello ASR kasasıyla aynı bölgede.

![](media/site-recovery-runbook-automation/03.png)

Ardından, hello hesap varlıkları aşağıdaki hello oluşturun.

### <a name="add-a-subscription-name-as-asset"></a>Abonelik adı varlık ekleme
1. Yeni bir ayar Ekle ![](media/site-recovery-runbook-automation/04.png) içinde Azure Otomasyon varlıkları hello ve çok seçin![](media/site-recovery-runbook-automation/05.png)
2. Merhaba değişken türü olarak seçin **dize**
3. Değişken adı olarak belirtmeniz **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Gerçek Azure aboneliği adınızı hello değişken değer olarak belirtin.

   ![](media/site-recovery-runbook-automation/07_1.png)

Aboneliğinizi hello Ayarları sayfasından hello Azure portalı hesabınıza hello adını belirleyebilirsiniz.

### <a name="add-an-azure-login-credential-as-asset"></a>Bir Azure oturum açma kimlik bilgileri varlık Ekle
Azure Otomasyonu, Azure PowerShell tooconnect toothe abonelik kullanır ve orada hello yapıları üzerine çalışır. Bunun için Microsoft hesabınızla veya bir iş veya Okul hesabı kullanarak kimlik doğrulaması gerekir.
Merhaba hesap kimlik bilgilerini güvenli bir şekilde hello runbook tarafından kullanılan bir varlık toobe depolayabilirsiniz.

1. Yeni bir ayar Ekle ![](media/site-recovery-runbook-automation/04.png) içinde Azure Otomasyon varlıkları hello ve seçin![](media/site-recovery-runbook-automation/09.png)
2. Merhaba kimlik bilgisi türü seçin **Windows PowerShell kimlik bilgisi**
3. Merhaba adı olarak belirtmeniz **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Merhaba kullanıcı adı ve parola toosign bileşeniyle birlikte belirtin.

Şimdi iki bu ayarlar, varlıkları kullanılabilir.

![](media/site-recovery-runbook-automation/11.png)

Tooconnect tooyour abonelik PowerShell aracılığıyla nasıl verilen hakkında daha fazla bilgi [burada](/powershell/azure/overview).

Ardından, Azure automation'da hello ön uç sanal makine için bir uç nokta yük devretme sonrasında ekleyebilirsiniz bir runbook oluşturun.

## <a name="azure-automation-context"></a>Azure Otomasyonu bağlamı
ASR geçirir bağlam değişken toohello runbook toohelp belirleyici betikler oluşturma. Bir hello bulut hizmeti ve sanal makine hello hello adları tahmin edilebilir, ancak, her zaman bir burada hello sanal makine adı hello adı nedeniyle değiştirilmiş olabilir hello gibi toocertain senaryoları owing hello durumda olmadığını olur karşıdır Azure toounsupported karakter. Bu nedenle bu bilgileri toohello ASR kurtarma planı hello bir parçası olarak geçirilen *bağlamı*.

Merhaba bağlamının nasıl göründüğünü örneği aşağıdadır.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


Merhaba tabloda hello bağlamda her bir değişken için ad ve açıklama içerir.

| **Değişken adı** | **Açıklama** |
| --- | --- |
| RecoveryPlanName |Çalıştırılan planının adı. Eylem adını kullanarak temel aldığınız yardımcı hello aynı komut dosyası |
| FailoverType |Merhaba yük devretme sınamasını olup olmadığını, planlı veya plansız belirtir. |
| FailoverDirection |Kurtarma tooprimary veya ikincil olup olmadığını belirtin |
| GroupID |Merhaba planı çalıştırırken hello Grup numarası hello kurtarma planı içinde tanımlayın |
| VmMap |Dizi, hello grubundaki tüm hello sanal makineler |
| VMMap anahtarı |Her VM için benzersiz anahtar (GUID). Bunu sahip hello hello sanal makinenin VMM kimliği uygunsa hello gibi aynı. |
| Rol adı |Merhaba kurtarılmakta olan Azure VM adı |
| CloudServiceName |Azure bulut hizmeti adı altında hangi hello sanal makine oluşturulur. |

Ayrıca toohello VM özellikleri sayfasını ASR Git ve hello VM GUID özelliği Ara hello bağlamda tooidentify hello VmMap anahtarı.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>Bir Otomasyon runbook'u Yaz
Şimdi hello runbook tooopen bağlantı noktası 80 üzerinde hello ön uç sanal makine oluşturun.

1. Hello Azure Automation hesabını hello ada sahip yeni bir runbook oluşturmak **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Toohello hello runbook Yazar görünümünü gidin ve hello taslak modunda girin.
3. İlk hello değişken toouse hello kurtarma planı bağlamı olarak belirtin

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. Sonraki toohello abonelik hello kimlik bilgisi ve abonelik adını kullanarak bağlan

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Hello Azure kullandığını unutmayın varlıklar – **AzureCredential** ve **AzureSubscriptionName** burada.
5. Şimdi hello uç nokta ayrıntılarını belirtin ve tooexpose hello endpoint istediğiniz hello sanal makine GUİD'si hello. Bu örneği hello ön uç sanal makine.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Bu, hello Azure uç noktası protokolü, yerel bağlantı noktası hello VM üzerinde ve eşlenen ortak bağlantı noktasını belirtir. Bu değişkenler parametreleri tarafından hello uç noktaları tooVMs eklemek Azure komutları gereklidir. Merhaba VMGUID hello GUID hello sanal makinenin üzerinde toooperate gereken tutar.
6. Hello betik şimdi VM GUID verilen hello hello bağlamının ayıklamak ve bir uç nokta hello sanal makine tarafından başvurulan oluşturabilirsiniz.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. Tamamlandığında, Yayımla isabet ![](media/site-recovery-runbook-automation/20.png) tooallow, komut dosyası toobe yürütme için kullanılabilir.

Merhaba tam komut dosyası başvuru için aşağıda verilmiştir

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Merhaba betik toohello kurtarma planına ekleyin
Merhaba betik hazır olduktan sonra daha önce oluşturduğunuz toohello kurtarma planı ekleyebilirsiniz.

1. Oluşturduğunuz hello kurtarma planında tooadd 2 gruptan sonra bir komut dosyası seçin. ![](media/site-recovery-runbook-automation/15.png)
2. Bir komut dosyası adı belirtin. Yalnızca hello kurtarma planı içinde gösteren için bu komut için bir kolay ad budur.
3. Merhaba yük devretme tooAzure komut dosyasında – hello Azure Otomasyon hesabı adı seçin.
4. Hello Azure runbook'ları, yazdığınız hello runbook'u seçin.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Birincil tarafı betikler
Bir yük devretme tooAzure yürütülürken birincil tarafı betikler tooexecute de seçebilirsiniz. Bu komut dosyaları, yük devretme sırasında hello VMM sunucusunda çalıştırılır.
Birincil tarafı komut dosyaları yalnızca yalnızca Kapatma öncesi için kullanılabilir ve kapatma aşamaları gönderin. Bir olağanüstü durum sağlar, hello birincil site toobe genellikle kullanılamaz bekliyoruz olmasıdır.
Planlanmamış bir yük devretme sırasında yalnızca birincil site işlemleri için kabul ederseniz toorun hello birincil tarafı betikler deneyecek. Bunlar erişilebilir değil veya zaman aşımı, hello yük devretme devam edecek toorecover sanal makineleri hello.
Birincil tarafı betikler beklemediğiniz -, yük devretme tooAzure sırasında korumalı VMM tooAzure olmadan VMware/fiziksel/Hyper-v siteler için kullanılabilir.
Ancak, ne zaman, yeniden çalışma Azure tooon içi, birincil tarafı komut dosyaları (Runbook'lar) VMware dışındaki tüm hedefler için kullanılabilir.

## <a name="test-hello-recovery-plan"></a>Test hello kurtarma planı
Merhaba runbook toohello planı ekledikten sonra eylemde bakın ve yük devretme testi başlatın. Her zaman bir sınama yük devretme tootest toorun önerilen hatalar yoktur, uygulama ve hello kurtarma planı tooensure.

1. Merhaba kurtarma planı seçin ve bir test yük devretme başlatın.
2. Merhaba planı yürütme sırasında hello runbook yürütüldü olup olmadığını veya durumunu aracılığıyla değil görebilirsiniz.

   ![](media/site-recovery-runbook-automation/17.png)
3. Ayrıca bkz hello ayrıntılı hello Azure Otomasyonu işleri sayfasında hello runbook için runbook yürütme durumu.

   ![](media/site-recovery-runbook-automation/18.png)
4. Merhaba yük devretme tamamlandığında hello runbook yürütme sonucu dışında hello yürütme başarılı olup olmadığını veya hello Azure sanal makinesi sayfasını ziyaret ve hello Uç noktalara arayarak tarafından görebilirsiniz.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Örnek komut dosyaları
Vazgeçtik sırada Bu öğreticide bir Azure sanal makine uç noktası tooan ekleme görev kullanılan bir genellikle otomatikleştirme, bir dizi Azure otomasyonu kullanarak diğer güçlü Otomasyon görevi yapabilirsiniz. Microsoft ve hello Azure Automation topluluk yardımcı olabilecek örnek runbook'lar kendi çözümleri ve daha büyük bir otomatikleştirme görevleri için yapı taşı olarak kullanabileceğiniz yardımcı programı runbook'lar oluşturmaya başlamak sağlar. Merhaba Galerisi'nden kullanmaya başlamak ve Azure Site Recovery kullanarak uygulamalarınızı için güçlü tek tıklatmayla kurtarma planları oluşturun.

## <a name="additional-resources"></a>Ek Kaynaklar
[Azure Otomasyonu genel bakış](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Otomasyonu genel bakış")

[Örnek Azure Otomasyon betikleri](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "örnek Azure Otomasyonu komutlar")
