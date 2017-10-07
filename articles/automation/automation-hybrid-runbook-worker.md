---
title: "aaaAzure Otomasyon karma Runbook çalışanları | Microsoft Docs"
description: "Bu makalede, yükleme ve toorun runbook'ları, yerel veri merkezi ya da bulut sağlayıcınız makinelerde sağlayan Azure Automation'ın bir özellik olan karma Runbook çalışanı kullanma hakkında bilgiler sağlar."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Veri merkezi veya karma Runbook çalışanı ile bulut kaynakları otomatikleştirme
Hello Azure bulut çalıştırdıkları beri Azure Otomasyonu'nda Runbook'lar diğer Bulut veya şirket içi ortamınız kaynaklarına erişemez.  Merhaba karma Runbook çalışanı Özelliği Azure Automation'ın toorun runbook'ları doğrudan hello rolünü barındıran hello bilgisayarda ve hello ortamı toomanage kaynaklara karşı bu yerel kaynakları sağlar. Runbook'ları depolanan ve Azure Otomasyonu'nda yönetilir ve tooone veya daha fazla atanmış bilgisayarlara teslim.  

Bu işlev görüntü aşağıdaki hello gösterilmiştir:<br>  

![Karma Runbook çalışanı genel bakış](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Merhaba karma Runbook çalışanı rolü ve dağıtım konuları teknik bir genel bakış için bkz: [Otomasyon mimarisine genel bakış](automation-offering-get-started.md#automation-architecture-overview).    

## <a name="hybrid-runbook-worker-groups"></a>Karma Runbook çalışan grupları
Her karma Runbook çalışanı hello aracı yüklediğinizde, belirttiğiniz bir karma Runbook çalışanı grubunun bir üyesidir.  Bir gruba bir aracıyı ekleyebilirsiniz, ancak yüksek kullanılabilirlik grubunda birden çok aracı yükleyebilirsiniz.

Bir karma Runbook çalışanını bir runbook'u başlattığınızda, üzerinde çalıştığı hello grubu belirtin.  Merhaba grubunun üyeleri, hello hello isteği hangi çalışan hizmetleri belirleyin.  Belirli bir çalışan belirtemezsiniz.

## <a name="relationship-tooservice-management-automation"></a>İlişki tooService Yönetimi Otomasyonu
[Service Management Automation (SMA)](https://technet.microsoft.com/library/dn469260.aspx) sağlar toorun Merhaba, yerel veri merkezinde Azure Automation tarafından desteklenen aynı runbook'ları. Windows Azure Pack SMA yönetimi için bir grafik arabirim içerdiğinden SMA genellikle Windows Azure paketi ile birlikte dağıtılır. Azure Otomasyonu, SMA web sunucuları toohost hello API, bir veritabanı toocontain runbook'ları ve SMA yapılandırma ve Runbook çalışanları tooexecute runbook işleri içeren yerel bir yükleme gerektirir. Azure Otomasyonu hello bulutta bu hizmetler sağlar ve yalnızca yerel ortamınızdaki toomaintain hello karma Runbook çalışanları gerektirir.

Varolan bir SMA kullanıcı varsa, bunlar açıklandığı gibi kendi kimlik doğrulama tooresources gerçekleştireceğini varsayılarak herhangi bir değişiklik yapmadan karma Runbook çalışanı ile kullanılan, runbook'ları tooAzure Otomasyon toobe taşıyabilirsiniz [runbook'lar bir karma Runbook üzerinde çalışır Çalışan](automation-hrw-run-runbooks.md).  Merhaba hizmet hesabı, kimlik doğrulamasının hello runbook'lar için sağlayabilir hello çalışan sunucu üzerindeki hello bağlamında SMA runbook'ları çalıştırın.

Azure Otomasyon karma Runbook çalışanı ya da hizmet yönetimi Otomasyonu ile gereksinimleriniz için daha uygun olup olmadığını ölçütleri toodetermine aşağıdaki hello kullanabilirsiniz.

* SMA grafiksel Yönetim arabirimine gerekliyse, bağlı tooWindows Azure Pack bileşenlerinin temel alınan yerel olarak yüklenmesini gerektirir. Daha fazla yerel kaynaklar yalnızca yerel runbook çalışanları üzerinde yüklü bir aracı gereken Azure Otomasyonu daha yüksek bakım maliyetleri gereklidir. Merhaba aracıları daha fazla bakım maliyetlerini azaltmak Operations Management Suite tarafından yönetilir.
* Azure Otomasyonu runbook hello bulutta depolar ve bunları tooon içi karma Runbook çalışanları sunar. Güvenlik ilkeniz Bu davranış izin vermez, SMA kullanmanız gerekir.
* System Center ile SMA bulunur; ve bu nedenle, System Center 2012 R2 lisansı gerektirir. Azure Otomasyonu, bir katmanlı abonelik modeline dayanır.
* Azure Otomasyonu Gelişmiş Özellikler SMA'da kullanılamaz grafik runbook'lar gibi.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>Windows karma Runbook çalışanı Hello yükleme 

tooinstall ve bir Windows karma Runbook çalışanı yapılandırma, kullanılabilir iki yöntem vardır.  Merhaba önerilen yöntemiyle bir Otomasyon runbook toocompletely otomatikleştirmek hello işlem gerekli tooconfigure bir Windows bilgisayar.  Merhaba ikinci yöntem, bir adım adım yordam toomanually yükleme aşağıdaki ve hello yapılandırın.  

> [!NOTE]
> toomanage hello yapılandırma hello karma Runbook çalışanı rolü istenen durum yapılandırması (DSC) ile destekleme sunucularınızın tooadd ihtiyacınız DSC düğümleri olarak bunları.  Ekleme hakkında daha fazla bilgi için DSC ile yönetimine görebileceği [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md).           
><br>
>Merhaba etkinleştirirseniz [güncelleştirme yönetimi çözümü](../operations-management-suite/oms-solution-update-management.md), herhangi bir Windows bilgisayarda bağlı tooyour OMS çalışma bu çözümde bulunan karma Runbook çalışanı toosupport runbook'lar otomatik olarak yapılandırılır.  Ancak, bu Otomasyon hesabında zaten tanımlanmış bir karma çalışanı grubu kayıtlı değil.  Merhaba çözüm ve karma Runbook çalışanı grup üyeliği için aynı hesabı hello kullanmakta olduğunuz sürece hello bilgisayar, Otomasyon hesabı toosupport Otomasyon runbook'ları tooa karma Runbook çalışanı grubu eklenebilir.  Bu işlev tooversion 7.2.12024.0 hello karma Runbook çalışanı olarak eklendi.  

Gözden geçirme hello hello ilgili bilgiler aşağıdaki [donanım ve yazılım gereksinimleri](automation-offering-get-started.md#hybrid-runbook-worker) ve [ağınıza hazırlamaya yönelik bilgi](automation-offering-get-started.md#network-planning) bir karma Runbook çalışanı dağıtmaya başlamadan önce.  Bir runbook worker başarıyla dağıttıktan sonra gözden [runbook'lar bir karma Runbook çalışanı üzerinde çalışacak](automation-hrw-run-runbooks.md) toolearn, şirket içi veri merkezi veya başka bir bulut ortamında tooconfigure runbook'lar tooautomate nasıl işler.  
 
### <a name="automated-deployment"></a>Otomatik dağıtım

Hello aşağıdaki gerçekleştirme adımları tooautomate hello yükleme ve yapılandırma hello Windows karma çalışanı rolü.  

1. Merhaba karşıdan *yeni OnPremiseHybridWorker.ps1* hello betikten [PowerShell Galerisi](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) hello karma Runbook çalışanı rolü çalıştıran bilgisayardan doğrudan hello veya başka bir bilgisayardan, ortam ve toohello çalışan kopyalayın.  

    Merhaba *yeni OnPremiseHybridWorker.ps1* komut dosyası yürütme sırasında şu parametreler hello gerektirir:

  * *AutomationAccountName* (zorunlu) - hello Otomasyon hesabınızın adını.  
  * *ResourceGroupName* (zorunlu) - hello Otomasyon hesabınızla ilişkili hello kaynak grubunun adını.  
  * *HybridGroupName* (zorunlu) - hello runbook'lar bu senaryoyu desteklemek için hedef olarak belirttiğiniz bir karma Runbook çalışanı grubunun hello adı. 
  *  *Subscriptionıd* (zorunlu) - Azure abonelik kimliği'de, Automation hesabınızı bulunduğu hello.
  *  *WorkspaceName* (isteğe bağlı) - hello OMS çalışma alanı adı.  Bir OMS çalışma alanı yoksa, hello betiği oluşturur ve bir yapılandırır.  

     > [!NOTE]
     > Şu anda hello OMS ile tümleştirme için desteklenen tek Otomasyon bölgeleri şunlardır: - **Avustralya Güneydoğu**, **Doğu ABD 2**, **Güneydoğu Asya**, ve **Batı Avrupa**.  Otomasyon hesabınızı bu bölgeler içinde değilse, bir OMS çalışma hello komut dosyası oluşturur ama, bunları birlikte bağlayamazsınız, sizi uyarır.
     > 
2. Bilgisayarınızda Başlat **Windows PowerShell** hello gelen **Başlat** ekran Yönetici modunda.  
3. PowerShell komut satırı kabuğu Hello indirilir ve bunu parametrelerinin hello değerleri değiştirme yürütme hello betik içeren toohello klasörüne gidin *- AutomationAccountName*, *- ResourceGroupName* , *- HybridGroupName*, *- Subscriptionıd*, ve *- WorkspaceName*.

     > [!NOTE] 
     > Hello betiği yürüttükten sonra Azure ile istendiğinde tooauthenticate olursunuz.  **Gerekir** hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla oturum açın.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. İstendiğinde tooagree tooinstall olduğunuz **NuGet** ve istendiğinde tooauthenticate Azure kimlik bilgilerinizle.<br><br> ![Yeni OnPremiseHybridWorker betik yürütme işlemi](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Merhaba betik tamamlandıktan sonra hello karma çalışan grupları dikey penceresinde hello yeni Grup ve üye sayısı gösterilir veya varolan bir grubu, üye hello sayısı artar.  Merhaba üzerinde hello listesinden hello grup seçebilirsiniz **karma çalışan grupları** dikey penceresinde ve select hello **karma çalışanları** döşeme.  Merhaba üzerinde **karma çalışanları** dikey penceresinde hello Grup listelenen her bir üyesi bakın.  

### <a name="manual-deployment"></a>El ile dağıtımı 
Merhaba ilk iki kez Otomasyon ortamınız için adımları ve her bir çalışan bilgisayar adımları kalan hello yineleyin.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Operations Management Suite çalışma alanı oluşturma
Bir Operations Management Suite çalışma alanı zaten yoksa yönergeleri kullanarak bir tane oluşturmak [çalışma alanınızı yönetmek](../log-analytics/log-analytics-manage-access.md). Zaten varsa, varolan bir çalışma alanını kullanabilirsiniz.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. Otomasyon çözümünü tooOperations Management Suite çalışma alanı Ekle
Çözümleri işlevselliği tooOperations Management Suite ekleyin.  Merhaba Otomasyon çözümünü Azure Otomasyon karma Runbook çalışanı desteği dahil olmak üzere için işlevsellik ekler.  Merhaba çözüm tooyour çalışma eklediğinizde, otomatik olarak hello sonraki adımda yükleyecek çalışan bileşenleri toohello aracı bilgisayar aşağı iter.

Merhaba yönergeleri izleyin [tooadd hello Çözümleri Galerisi kullanarak bir çözüm](../log-analytics/log-analytics-add-solutions.md) tooadd hello **Otomasyon** çözüm tooyour Operations Management Suite çalışma.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Merhaba Microsoft İzleme Aracısı yükleme
Merhaba Microsoft İzleme Aracısı Bilgisayarları tooOperations Management Suite bağlanır.  Şirket içi bilgisayarınıza hello aracı yüklediğinizde ve tooyour çalışma bağlayın karma Runbook çalışanı için gerekli hello bileşenleri otomatik olarak indirir.

Merhaba yönergeleri izleyin [bağlanmak Windows bilgisayarları tooLog Analytics](../log-analytics/log-analytics-windows-agents.md) hello şirket içi bilgisayarda tooinstall hello Aracısı.  Birden çok çalışanları tooyour ortamı için birden çok bilgisayar tooadd bu işlemi yineleyebilirsiniz.

Merhaba Aracısı başarıyla tooOperations Management Suite bağlandığında, üzerinde hello listelenecektir **bağlı kaynakları** hello Operations Management Suite sekmesinde **ayarları** bölmesi.  Bu hello aracı karşıdan düzgün hello Otomasyon çözümünü adlı bir klasör olduğunda doğrulayabilirsiniz **AzureAutomationFiles** C:\Program Files\Microsoft Monitoring Agent\Agent içinde.  Merhaba sürümü hello karma Runbook çalışanı tooconfirm, tooC:\Program Files\Microsoft izleme Agent\Agent\AzureAutomation\ ve Not hello gidin \\ *sürüm* alt klasörü.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Merhaba runbook ortamını yüklemek ve tooAzure Otomasyon bağlanın
Bir aracı tooOperations Management Suite eklediğinizde, hello Otomasyon çözümünü hello iter **HybridRegistration** hello içeren PowerShell Modülü **Add-HybridRunbookWorker** cmdlet'i.  Bu cmdlet'i tooinstall hello runbook ortamını hello bilgisayarda kullanmak ve Azure Automation ile kaydeder.

Yönetici modunda bir PowerShell oturumu açın ve aşağıdaki komutları tooimport hello modülü hello çalıştırın.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

Merhaba çalıştırmak **Add-HybridRunbookWorker** cmdlet sözdizimi aşağıdaki hello kullanarak:

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Bu cmdlet hello gelen gerekli hello bilgi edinebilirsiniz **anahtarları Yönet** dikey penceresinde hello Azure portalı.  Merhaba seçerek bu dikey penceresini açmak **anahtarları** hello seçeneğinden **ayarları** dikey penceresinde, Automation hesabı.

![Karma Runbook çalışanı genel bakış](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** hello karma Runbook çalışan grubu hello adıdır. Bu grubun hello automation hesabında zaten varsa, hello geçerli bilgisayar tooit eklenir.  Daha sonra zaten yoksa eklenir.
* **Uç nokta** hello olan **URL** hello alanındaki **anahtarları Yönet** dikey.
* **Belirteç** hello olan **birincil erişim anahtarını** hello içinde **anahtarları Yönet** dikey.  

Kullanım hello **-Verbose** anahtarı ile **Add-HybridRunbookWorker** tooreceive hakkında ayrıntılı bilgi hello yükleme.

#### <a name="5-install-powershell-modules"></a>5. PowerShell modülleri yükleme
Runbook'ları hello etkinlikleri ve Azure Otomasyonu ortamınızda yüklü hello modüllerdeki tanımlanan cmdlet'leri herhangi birini kullanabilirsiniz.  El ile yüklemeniz gerekir böylece bu modüllerin otomatik olarak dağıtılan tooon içi bilgisayarlar yine de olup olmadığı.  Merhaba, hello erişim toocmdlets tüm Azure Hizmetleri ve etkinlikleri için Azure otomasyonu için varsayılan olarak yüklenen Azure modülü istisnadır.

Merhaba birincil amacı hello karma Runbook çalışanı özelliğinin toomanage yerel kaynaklar olduğundan, büyük olasılıkla destek bu kaynakları tooinstall hello modülleri gerek vardır.  Çok başvurabilir[yükleme modülleri](http://msdn.microsoft.com/library/dd878350.aspx) Windows PowerShell modülleri yükleme hakkında bilgi için.  Yüklü modülleri, böylece hello karma çalışanı tarafından otomatik olarak içe aktarılır PSModulePath ortam değişkeni tarafından başvurulan bir konumda olması gerekir.  Daha fazla bilgi için bkz: [değiştirme hello PSModulePath yükleme yolu](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx). 

## <a name="removing-hybrid-runbook-worker"></a>Karma Runbook çalışanı kaldırma 
Bir veya daha fazla karma Runbook çalışanları bir gruptan kaldırmak veya gereksinimlerinize bağlı olarak hello grup kaldırabilirsiniz.  tooremove bir karma Runbook çalışanı bir şirket içi bilgisayardan hello aşağıdaki adımları gerçekleştirin.

1. Hello Azure portal, tooyour Otomasyon hesabı gidin.  
2. Merhaba gelen **ayarları** dikey penceresinde, select **anahtarları** ve alan hello değerlerini not edin **URL** ve **birincil erişim anahtarını**.  Bu bilgiler sonraki adımda hello gerekir.
3. Yönetici modunda bir PowerShell oturumu açın ve hello aşağıdaki komutu çalıştırarak command - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`.  Kullanım hello **-Verbose** geçiş hello kaldırma işleminin ayrıntılı günlüğü için.

> [!NOTE]
> Bu hello Microsoft İzleme Aracısı hello bilgisayardan yalnızca hello işlevselliği ve hello karma Runbook çalışanı rolü yapılandırmasını kaldırmaz.  

## <a name="remove-hybrid-worker-groups"></a>Karma çalışan grupları kaldırın
bir grup tooremove, öncelikle daha önce gösterilen hello yordamı kullanarak hello grubunun bir üyesi olan her bir bilgisayardan tooremove hello karma Runbook çalışanı gerekir ve ardından aşağıdaki adımları tooremove hello Grup hello gerçekleştirebilirsiniz.  

1. Hello Azure portal Hello Automation hesabını açın.
2. Select hello **karma çalışan grupları** döşeme ve hello **karma çalışan grupları** dikey penceresinde, select hello grubu toodelete istiyor.  Merhaba belirli bir grup seçtikten sonra hello **karma çalışanı grubu** özellikleri dikey penceresi görüntülenir.<br> ![Karma Runbook çalışan grubu dikey penceresi](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. Merhaba özellikleri dikey penceresinde hello seçilen grup, tıklatın **silmek**.  Bu eylem, seçin, soran tooconfirm bir ileti görüntülenir **Evet** tooproceed istediğinizden eminseniz.<br> ![Grubu Sil onay iletişim kutusu](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> Bu işlem birkaç sürebilir saniye toocomplete ve altında ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.  

## <a name="troubleshooting"></a>Sorun giderme 
Durum raporu ve runbook işleri almak veya Hello karma Runbook çalışanı üzerinde hello ile Otomasyon hesabı tooregister hello çalışan Microsoft Monitoring Agent toocommunicate bağlıdır. Merhaba çalışan kaydı başarısız olursa hello hata bazı olası nedenleri şunlardır:  

1. Merhaba karma çalışanı bir proxy veya güvenlik duvarı arkasında ' dir.  
    Merhaba bilgisayarın giden erişim too*.azure-automation.net bağlantı noktası 443 üzerinde olduğunu doğrulayın.  

2. Merhaba bilgisayar hello karma çalışanı daha az üzerinde çalıştığı hello en düşük donanım daha [gereksinimleri](automation-offering-get-started.md#hybrid-runbook-worker).  
    Karma Runbook çalışanı karşılamalıdır hello çalıştıran bilgisayarlar toohost atamadan önce en düşük donanım gereksinimleri hello bu özellik. Aksi takdirde, diğer arka plan işlemleri ve yürütme sırasında runbook'lar tarafından neden Çekişme hello kaynak kullanımı, bağlı olarak hello bilgisayar üzerinde kullanılan haline gelir ve runbook işi gecikmeler veya zaman aşımlarına neden.
   Toorun hello karma Runbook çalışanı özelliği belirlenmiş hello bilgisayar hello en düşük donanım gereksinimlerini karşılayan onaylayın.  Destekliyorsa, CPU ve bellek kullanımı toodetermine karma Runbook çalışanı işlemlerin hello performansını ile Windows arasında herhangi bir bağıntı izleyin.  Bellek veya CPU baskısı ise, bu hello gerek tooupgrade belirtmek veya ek işlemciler ekleme veya artış bellek tooaddress kaynak performans sorunu hello ve hello hatayı giderin. Alternatif olarak, hello en düşük gereksinimlerini destekleyen ve iş yükü taleplerini artıştır gerekli belirttiğinizde ölçeklendirme farklı işlem kaynak seçin.
    
3. Merhaba Microsoft İzleme Aracısı hizmeti çalışmıyor.  
    Merhaba Microsoft İzleme Aracısı Windows hizmeti çalışmıyorsa bu hello karma Runbook çalışanı Azure Automation ile iletişim kurmasını engeller.  Merhaba aracı PowerShell komutunda aşağıdaki hello girerek çalıştığını doğrulayın: `get-service healthservice`.  Merhaba hizmeti durdurulursa, PowerShell toostart hello hizmeti komutunda aşağıdaki hello girin: `start-service healthservice`.  

4. Merhaba, **uygulama ve Hizmetleri Logs\Operations Yöneticisi** olay günlüğü olay 4502 ve EventMessage içeren gördüğünüz **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**açıklama aşağıdaki hello ile: *hello hizmeti tarafından sunulan hello sertifika <wsid>. oms.opinsights.azure.com Microsoft Hizmetleri için kullanılan bir sertifika yetkilisi tarafından değil yayınlandı. TLS/SSL iletişimi karşılar bir proxy kullanıyorsanız, ağ yöneticisi toosee temasa geçin. Merhaba KB3126513 makalesine ek sorun giderme bilgileri için bağlantı sorunları var.*
    Bu, proxy veya ağ güvenlik duvarı blockking iletişim tooMicrosoft tarafından Azure neden olabilir.  Merhaba bilgisayarın, 443 numaralı bağlantı noktalarına giden erişim too*.azure-automation.net olduğunu doğrulayın.

Günlükleri yerel olarak her karma çalışanı C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes konumunda depolanır.  Herhangi bir uyarı veya hata olayları toohello yazılmış olup olmadığını denetleyebilir **uygulama ve Hizmetleri Logs\Microsoft-SMA\Operations** ve **uygulama ve Hizmetleri Logs\Operations Yöneticisi** olay günlüğü bir bağlantı veya ekleme hello rol tooAzure Otomasyon veya sorun normal işlemleri gerçekleştirirken etkileyen diğer sorunu gösterir.  

## <a name="next-steps"></a>Sonraki adımlar
Gözden geçirme [runbook'lar bir karma Runbook çalışanı üzerinde çalışacak](automation-hrw-run-runbooks.md) toolearn, şirket içi veri merkezi veya başka bir bulut ortamında tooconfigure runbook'lar tooautomate nasıl işler.
