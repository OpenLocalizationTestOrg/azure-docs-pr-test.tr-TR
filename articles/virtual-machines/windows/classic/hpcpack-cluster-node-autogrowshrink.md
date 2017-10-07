---
title: "aaaAutoscale HPC paketi küme düğümleri | Microsoft Docs"
description: "Otomatik olarak Büyüt ve HPC paketi küme işlem düğümleri azure'da hello sayısı Daralt"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Otomatik olarak Büyüt ve toohello küme iş yükü göre azure'da hello HPC paketi küme kaynaklarını Daralt
HPC Pack kümenizdeki Azure "veri bloğu" düğümlerini dağıtmak ya da Azure Vm'lerde bir HPC paketi küme oluşturmak, bir şekilde otomatik olarak büyütür veya düğümleri veya çekirdek hello küme hello iş yüküne göre gibi hello küme kaynaklarını küçültmek isteyebilirsiniz. Bu şekilde Hello küme kaynaklarını ölçeklendirme sağlar toouse Azure kaynaklarınızı daha etkili ve bunların maliyetlerini denetlemenize.

Bu makalede HPC Pack tooautoscale işlem kaynakları sağlayan iki yolunu gösterir:

* Merhaba HPC paketi küme özelliği **AutoGrowShrink**

* Merhaba **AzureAutoGrowShrink.ps1** HPC PowerShell Betiği

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Şu anda, yalnızca otomatik olarak Büyüt ve Windows Server işletim sistemi çalıştırılan HPC Pack işlem düğümleri daraltma.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Merhaba AutoGrowShrink küme özelliğini ayarlayın
### <a name="prerequisites"></a>Ön koşullar

* **HPC Pack 2012 R2 güncelleştirme 2 veya sonraki bir küme** -hello küme baş düğümüne olabilir ya da şirket içi dağıtılan veya bir Azure VM. Bkz: [HPC paketi ile karma küme ayarlama](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget bir şirket içi baş düğüm ve Azure "veri bloğu" düğümleri ile başlatıldı. Merhaba bkz [HPC Pack Iaas dağıtım betiği](hpcpack-cluster-powershell-script.md) tooquickly Azure VM'de HPC paketi küme dağıtın.

* **Bir küme baş düğümü Azure (Resource Manager dağıtım modeli) bulunan** - HPC Pack 2016'dan itibaren sertifika kimlik doğrulaması Azure Active Directory uygulamada otomatik olarak artan için kullanılır ve küçültme küme VM'ler dağıtılabilir kullanma Azure Resource Manager. Bir sertifika aşağıdaki gibi yapılandırın:

  1. Küme dağıtıldıktan sonra Uzak Masaüstü tooone baş düğümü tarafından bağlayın.

  2. Merhaba (PFX biçimi özel anahtara sahip) sertifika tooeach baş düğüm karşıya yükleme ve tooCert:\LocalMachine\My ve Cert: \LocalMachine\Root yükleyin.

  3. Azure PowerShell'i yönetici olarak başlatın ve komutları bir baş düğüm üzerinde aşağıdaki hello çalıştırın:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Hesabınızın birden fazla Azure Active Directory kiracısı veya Azure aboneliği varsa, hello aşağıdaki çalıştırabilirsiniz komutu tooselect hello doğru Kiracı ve abonelik:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Komut tooview aşağıdaki hello hello şu anda Kiracı ve abonelik Seçileni çalıştır:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Komut dosyası izleyen hello çalıştırın

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    Burada

    **DisplayName** -Azure Active uygulama görünen adı. Merhaba uygulaması yoksa, Azure Active Directory içinde oluşturulur.

    **Giriş sayfası** -hello uygulamasının hello giriş sayfası. Hello önceki örnekte olduğu gibi bir kukla URL yapılandırabilirsiniz.

    **IdentifierUri** -hello uygulama tanıtıcısı. Hello önceki örnekte olduğu gibi bir kukla URL yapılandırabilirsiniz.

    **CertificateThumbprint** -1. adımda hello baş düğümünde yüklü hello sertifikanın parmak izi.

    **Tenantıd** -Kiracı kimliği, Azure Active Directory. Merhaba Kiracı kimliği hello Azure Active Directory Portalı'ndan elde edebilirsiniz **özellikleri** sayfası.

    Hakkında daha fazla ayrıntı için **ConfigARMAutoGrowShrinkCert.ps1**, çalışma `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **Bir küme baş düğümü Azure (Klasik dağıtım modeli) bulunan** - hello Klasik dağıtım modeli etkinleştir hello hello HPC Pack Iaas dağıtım komut dosyası toocreate hello kümesi kullanıyorsanız **AutoGrowShrink** küme Merhaba küme yapılandırma dosyasında hello AutoGrowShrink seçeneği ayarlayarak özelliği. Ayrıntılar için hello eşlik hello belgelerine bakın [komut dosyası indirme](https://www.microsoft.com/download/details.aspx?id=44949).

    Alternatif olarak, hello etkinleştirmek **AutoGrowShrink** HPC PowerShell'i kullanarak hello küme dağıttıktan sonra küme özelliği komutları açıklanan bölümden hello. Aşağıdaki ilk tam hello tooprepare Bu adımlar:

  1. Azure yönetim sertifikası hello baş düğüm ve hello Azure aboneliği yapılandırın. Bir sınama dağıtımı için HPC Pack Merhaba baş düğümüne yükleyen hello varsayılan Microsoft HPC Azure otomatik olarak imzalanan sertifika kullan ve bu sertifikayı tooyour Azure aboneliği karşıya yükleyin. Merhaba seçenekleri ve adımlar için bkz: [TechNet Kitaplığı Kılavuzu](https://technet.microsoft.com/library/gg481759.aspx).

  2. Çalıştırma **regedit** hello baş düğümünde tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo gidin ve bir dize değeri ekleyin. Merhaba değer adı çok Ayarla "Parmak izi" ve değer veri toohello sertifikanın parmak izini hello 1. adımda.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>HPC PowerShell komutları tooset hello AutoGrowShrink özelliği
Aşağıdaki örnek HPC PowerShell komutları tooset olan **AutoGrowShrink** ve tootune davranışını ek parametrelere sahip. Bkz: [AutoGrowShrink parametreleri](#AutoGrowShrink-parameters) hello ayarlarının tam listesi için bu makalede daha sonra.

toorun Bu komutlar, başlangıç HPC PowerShell'i hello küme baş düğümünde yönetici olarak.

**tooenable hello AutoGrowShrink özelliği**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**toodisable hello AutoGrowShrink özelliği**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**toochange hello aralığı dakika cinsinden Büyüt**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**toochange hello aralığı dakika cinsinden Daralt**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**tooview hello geçerli yapılandırmasını AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**tooexclude düğüm AutoGrowShrink gruplarından**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Bu parametre HPC Pack 2016'dan itibaren desteklenir
>

### <a name="autogrowshrink-parameters"></a>AutoGrowShrink parametreleri
Merhaba hello kullanarak değiştirebilirsiniz AutoGrowShrink Parametreler şunlardır **kümesi HpcClusterProperty** komutu.

* **EnableGrowShrink** - geçiş tooenable veya hello devre dışı **AutoGrowShrink** özelliği.
* **ParamSweepTasksPerCore** -parametrik tarama sayısı toogrow bir çekirdek görevler. Merhaba, görev başına bir çekirdek toogrow varsayılandır.

  > [!NOTE]
  > HPC Pack QFE KB3134307 değişiklikleri **ParamSweepTasksPerCore** çok**TasksPerResourceUnit**. Merhaba iş kaynak türüne göre ve düğüm, yuva veya çekirdek olabilir.
  >
  >
* **GrowThreshold** -kuyruğa alınmış görevlerin tootrigger otomatik büyüme eşiği. Merhaba varsayılan 1, 1 veya daha fazla görevlerinde sıraya alınan durum hello anlamına gelir, düğümlerin otomatik olarak büyütün.
* **GrowInterval** -dakika tootrigger otomatik büyüme aralığı. Merhaba varsayılan aralığı 5 dakikadır.
* **ShrinkInterval** -dakika tootrigger otomatik küçültme içinde aralığı. Merhaba varsayılan zaman aralığı olan 5 dakika. |
* **ShrinkIdleTimes** -sürekli denetimleri tooshrink tooindicate hello düğüm sayısını boş. Merhaba, 3 kez varsayılandır. Örneğin, hello **ShrinkInterval** 5 dakika, HPC Pack Merhaba düğümü 5 dakikada bir boş olup olmadığını denetler. 3 sürekli (15 dakika) denetledikten sonra hello düğümleri hello boşta durumunda ise, HPC Pack bu düğüme küçültür.
* **ExtraNodesGrowRatio** -ileti geçirme arabirimi (MPI) işleri için düğümleri toogrow ek yüzdesi. HPC Pack %1 MPI işlerini için düğümleri büyür anlamına gelir 1 Hello varsayılan değerdir.
* **GrowByMin** -hello minimum kaynaklardaki hello iş için gereken hello otomatik büyüme İlkesi tabanlı olup olmadığını tooindicate geçin. Merhaba varsayılan HPC Pack Merhaba en fazla kaynak hello işleri için gerekli temel işleri için düğümleri büyür başka bir deyişle, false değeridir.
* **SoaJobGrowThreshold** -eşiğini gelen SOA istekleri tootrigger hello otomatik büyüme işlemi. 50000 Hello varsayılan değerdir.

  > [!NOTE]
  > Bu parametre, HPC Pack 2012 R2 güncelleştirme 3'te itibaren desteklenmektedir.
  >
  >
* **SoaRequestsPerCore** -toogrow bir çekirdek istekleri Gelen SOA sayısı. 20000 Hello varsayılan değerdir.

  > [!NOTE]
  > Bu parametre, HPC Pack 2012 R2 güncelleştirme 3'te itibaren desteklenmektedir.
  >
* **ExcludeNodeGroups** – hello düğümler belirtilen düğüm grupları otomatik olarak Büyüt ve daraltma.
  
  > [!NOTE]
  > Bu parametre, HPC Pack 2016'dan itibaren desteklenir.
  >

### <a name="mpi-example"></a>MPI örneği
Varsayılan olarak, %1 HPC Pack büyür MPI işlerini için ek düğümleri (**ExtraNodesGrowRatio** too1 ayarlanır). Merhaba MPI birden çok düğüm gerektirebilir ve tüm düğümleri hazır olduğunuzda hello işi yalnızca çalıştırabilirsiniz nedenidir. Zaman zaman Azure düğümleri başladığında, tek bir düğüm o düğümü tooget için hazır beklerken boşta diğer düğümleri toobe neden diğerlerine göre daha fazla zaman toostart gerekebilir. Ek düğümler büyüyen HPC Pack bu kaynak bekleme süresini azaltır ve maliyetleri potansiyel olarak kaydeder. tooincrease hello yüzdesi ek düğümleri MPI işlerini (örneğin, too10%) için benzer bir komutu çalıştırın

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>SOA örneği
Varsayılan olarak, **SoaJobGrowThreshold** too50000 ayarlanır ve **SoaRequestsPerCore** too200000 ayarlanır. Bir SOA işi 70000 isteği göndermek, bir Sıraya alınan görev olduğunu ve gelen istekleri 70000. Bu durumda Hello görev sıraya alındı ve (70000-50000) gelen istekler için büyür HPC Pack 1 çekirdek büyür / 20000 = 1 çekirdek, bu nedenle, toplam bu SOA işi için 2 Çekirdek büyür.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Merhaba AzureAutoGrowShrink.ps1 komut dosyasını çalıştır
### <a name="prerequisites"></a>Ön koşullar

* **HPC Pack 2012 R2 güncelleştirme 1 veya sonraki bir küme** - hello **AzureAutoGrowShrink.ps1** betik hello % CCP_HOME % bin klasörüne yüklenir. Merhaba küme baş düğümüne olabilir ya da şirket içi dağıtılan veya bir Azure VM. Bkz: [HPC paketi ile karma küme ayarlama](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget bir şirket içi baş düğüm ve Azure "veri bloğu" düğümleri ile başlatıldı. Merhaba bkz [HPC Pack Iaas dağıtım betiği](hpcpack-cluster-powershell-script.md) tooquickly Azure VM'de HPC paketi küme dağıtın veya kullanın bir [Azure Hızlı Başlangıç şablonu](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **Azure PowerShell 1.4.0** -hello komut dosyası şu anda Azure PowerShell belirli bu sürümünde bağlıdır.
* **Azure ile bir küme düğümleri veri bloğu** -HPC Pack yüklü olduğu bir istemci bilgisayarı veya hello baş düğüm hello komut dosyasını çalıştırın. Bir istemci bilgisayarda çalışıyorsa, değişken $env hello ayarlamak emin olun: CCP_SCHEDULER toopoint toohello baş düğüm. Hello Azure "veri bloğu" düğümleri toohello küme eklenmesi gerekir, ancak hello değil dağıtılan durum olabilir.
* **Azure VM'ler (Resource Manager dağıtım modeli) dağıtılan bir küme için** -Azure hello Resource Manager dağıtım modelinde dağıtılan VM'ler küme için hello komut dosyası Azure kimlik doğrulaması için iki yöntemi destekler: tooyour Azure hesabı oturum toorun hello komut dosyası her zaman (çalıştırarak `Login-AzureRmAccount`, veya bir hizmet asıl tooauthenticate bir sertifika ile yapılandırın. HPC Pack Merhaba komut dosyası sağlar **ConfigARMAutoGrowShrinkCert.ps** toocreate sertifika ile bir hizmet sorumlusu. Merhaba betik bir Azure Active Directory (Azure AD) uygulama ve hizmet sorumlusu oluşturur ve hello katkıda bulunan rolü toohello hizmet sorumlusu atar. toorun hello komut dosyası, Azure PowerShell'i yönetici olarak başlatın ve hello aşağıdaki komutları çalıştırın:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Hakkında daha fazla ayrıntı için **ConfigARMAutoGrowShrinkCert.ps1**, çalışma `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,

* **Azure VM'ler (Klasik dağıtım modeli) dağıtılan bir küme için** -hello üzerinde bağımlı olduğundan dolayı hello baş düğümünde VM hello komut dosyasını çalıştırmak **başlangıç HpcIaaSNode.ps1** ve **Stop-HpcIaaSNode.ps1**yüklü komut dosyaları. Bu komut ayrıca bir Azure yönetim sertifikası gerektirir veya yayımlama ayarları dosyası (bkz [bir HPC Pack Yönet işlem düğümleri küme Azure'da](hpcpack-cluster-node-manage.md)). İşlem düğümü ihtiyacınız VM'ler zaten toohello küme eklenen tüm hello emin olun. Bunlar hello durduruldu durumunda olabilir.



### <a name="syntax"></a>Sözdizimi
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>Parametreler
* **NodeTemplates** -hello düğümü şablonları toodefine adlarını hello hello düğümleri toogrow için kapsam ve daraltma. Belirtilmezse, (hello varsayılan değer: @()) hello tüm düğümlerde **AzureNodes** düğüm grubu içinde olduğunda kapsam olan **NodeType** hello AzureNodes ve tüm düğümleri değerine sahip **ComputeNodes** düğüm grubu içinde olduğunda kapsam olan **NodeType** ComputeNodes değerine sahip.
* **JobTemplates** -hello adlarını proje şablonları toodefine hello hello düğümleri toogrow kapsamın.
* **NodeType** - hello düğümü toogrow türünü ve daraltma. Desteklenen değerler şunlardır:

  * **AzureNodes** – bir şirket içi Azure PaaS (veri bloğu) düğümler için ya da Azure Iaas küme.
  * **ComputeNodes** - işlem düğümünde VM'ler yalnızca bir Azure Iaas kümesi.

* **NumOfQueuedJobsPerNodeToGrow** -sıraya alınmış işlerin sayısı gerekli toogrow bir düğümü.
* **NumOfQueuedJobsToGrowThreshold** -hello eşik sıraya alınan işleri toostart hello sayısı büyümesine işlemi.
* **NumOfActiveQueuedTasksPerNodeToGrow** -etkin kuyruğa alınmış görevlerin hello sayısı gerekli toogrow bir düğümü. Varsa **NumOfQueuedJobsPerNodeToGrow** belirtilen 0'dan büyük bir değer ile bu parametre yoksayılır.
* **NumOfActiveQueuedTasksToGrowThreshold** -hello eşik etkin kuyruğa alınmış görevlerin toostart hello sayısı büyümesine işlemi.
* **NumOfInitialNodesToGrow** - hello kapsamdaki tüm hello düğüm gerekirse düğümleri toogrow en az sayıda ilk **değil dağıtılan** veya **durduruldu (Deallocated)**.
* **GrowCheckIntervalMins** -hello aralığı dakika arasında toogrow denetler.
* **ShrinkCheckIntervalMins** -hello aralığı dakika arasında tooshrink denetler.
* **ShrinkCheckIdleTimes** -hello sürekli küçültme denetimlerinin sayısının (ayırarak **ShrinkCheckIntervalMins**) tooindicate hello düğümler boşta.
* **UseLastConfigurations** -hello bağımsız değişkeni dosyasında kaydedilen önceki yapılandırmaların hello.
* **ArgFile**- hello hello bağımsız değişkeni kullanılan dosyası toosave adını ve güncelleştirmek hello yapılandırmaları toorun hello komut dosyası.
* **LogFilePrefix** -hello günlük dosyasının hello ön ek adı. Bir yolu belirtebilirsiniz. Varsayılan olarak hello günlüğü yazılı toohello geçerli çalışma dizini bulunmaktadır.

### <a name="example-1"></a>Örnek 1
Merhaba aşağıdaki örnek Azure ile varsayılan AzureNode şablonu toogrow dağıtılan düğümleri bloğu ve otomatik olarak küçültme hello yapılandırır. Tüm düğümleri başlangıçta hello varsa **değil dağıtılan** durumunda, en az 3 düğümleri başlatılacağı. Merhaba sıraya alınmış işlerin sayısı 8 aşarsa, kuyruğa alınmış işleri hello oranını kendi sayıyı aşıyor kadar hello komut dosyasını düğümleri başlatır **NumOfQueuedJobsPerNodeToGrow**. Bir düğüm 3 ardışık boşta zamanlarında boşta toobe bulunursa durdurulur.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Örnek 2
Merhaba aşağıdaki örnek Azure hello varsayılan ComputeNode şablonu toogrow ile dağıtılan düğümü VM'ler işlem ve otomatik olarak küçültme hello yapılandırır.
Merhaba varsayılan proje şablonu tarafından yapılandırılan hello işleri hello kümede iş yükü hello kapsamını tanımlayın. Tüm hello düğümleri başlangıçta durdurduysanız, en az 5 düğümleri başlatılır. Etkin kuyruğa alınmış görevlerin Hello sayısı 15 aşarsa, kendi sayıyı aşıyor active kuyruğa alınmış görevlerin hello oranı çok kadar hello komut dosyasını düğümleri başlatır**NumOfActiveQueuedTasksPerNodeToGrow**. Bir düğüm 10 ardışık boşta zamanlarında boşta toobe bulunursa durdurulur.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
