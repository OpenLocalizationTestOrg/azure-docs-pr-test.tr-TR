---
title: Azure automation'da ilk PowerShell runbook aaaMy | Microsoft Docs
description: "Test ve basit bir PowerShell runbook yayımlama hello oluşturma adımlarını anlatan öğretici."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "azure powershell, powershell betik öğreticisi, powershell otomasyonu"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: abff94abe666cd8423c35b970b4162ba9247bcf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-runbook"></a>İlk PowerShell runbook’um

> [!div class="op_single_selector"]
> * [Grafik](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell İş Akışı](automation-first-runbook-textual.md)
> 
> 

Bu öğreticide, hello oluşturulmasını açıklanmaktadır bir [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) Azure Automation. Biz, test ve biz nasıl tootrack hello hello runbook işinin durumunu açıklarken basit bir runbook ile başlatın. Biz hello runbook değiştirebilir sonra tooactually yönetmek Azure kaynaklarını, bu durumda bir Azure sanal makinesi başlatılıyor. Son olarak, runbook parametreleri ekleyerek runbook'u daha sağlam hello olun.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Azure aboneliği. Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).
* [Otomasyon hesabı](automation-sec-configure-azure-runas-account.md) toohold runbook hello ve tooAzure kaynakları kimlik doğrulaması.  Bu hesap, izin toostart sahip ve hello sanal makineyi durdurun.
* Azure sanal makinesi. Bu makineyi durdurup başlatacağımız için makinenin üretime yönelik bir VM olmaması gerekir.

## <a name="step-1---create-new-runbook"></a>1. Adım - Yeni runbook oluşturma
Merhaba metnini veren basit bir runbook oluşturarak başlayacağız *Hello World*.

1. Hello Azure portal, Automation hesabınızı açın.  
   Merhaba Automation hesabı sayfası, bu hesapta hello kaynakların hızlı bir görünümünü sağlar. Birkaç varlığınız zaten olmalıdır. Bunların çoğu, yeni bir Otomasyon hesabı içinde otomatik olarak dahil edilen hello modüllerdir. Hello belirtiliyor hello kimlik bilgisi varlığı de olmalıdır [Önkoşullar](#prerequisites).
2. Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.<br><br> ![RunbooksControl](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. Merhaba tıklatarak yeni bir runbook oluşturmak **runbook Ekle** düğmesine ve ardından **yeni bir runbook oluşturmak**.
4. Merhaba runbook hello adlandırın *MyFirstRunbook-PowerShell*.
5. Bu durumda, toocreate yapacağız bir [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) şekilde select **Powershell** için **Runbook türü**.<br><br> ![Runbook Türü](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. Tıklatın **oluşturma** toocreate hello runbook ve açık hello metin düzenleyicisini.

## <a name="step-2---add-code-toohello-runbook"></a>2. adım - kod toohello runbook Ekle
Doğrudan hello runbook'a kodu olabilir veya bunları toohello runbook ilgili parametrelerle ekledikten ve kitaplığı denetimi hello cmdlet'leri, runbook'ları ve varlıkları seçebilir. Bu kılavuzda doğrudan hello runbook'ta yazın.

1. Runbook şu anda boş, *Write-Output "Hello World."* yazın.<br><br> ![Hello World](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. Tıklayarak Hello runbook'u kaydetmek **kaydetmek**.<br><br> ![Kaydet Düğmesi](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-hello-runbook"></a>3. adım - hello runbook sınaması
Biz hello runbook toomake yayımlamadan önce onu üretimde kullanılabilir tootest istiyoruz, toomake düzgün çalıştığından emin. Bir runbook'u test ettiğinizde, bunun **Taslak** sürümünü çalıştırır ve çıktısını etkileşimli olarak görüntülersiniz.

1. Tıklatın **Test bölmesi** tooopen hello Test bölmesi.<br><br> ![Test Bölmesi](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. Tıklatın **Başlat** toostart hello test. Bu, yalnızca etkin hello seçeneği olmalıdır.
3. Bir [runbook işi](automation-runbook-execution.md) oluşturulur ve durumu görüntülenir.  
   Merhaba iş durumunu başlatır olarak *sıraya alınan* bir runbook worker'hello bulut toocome için bekleyen belirten. Ardından, çok taşınır*başlangıç* bir çalışan hello işi talep ettiğinde ve ardından *çalıştıran* hello runbook gerçekten çalışmaya başladığında.  
4. Merhaba runbook işi tamamlandığında çıktısı görüntülenir. Örneğimizde, *Hello World* metnini görmeliyiz.<br><br> ![Test Bölmesi Çıktısı](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. Merhaba Test bölmesi tooreturn toohello tuvale kapatın.

## <a name="step-4---publish-and-start-hello-runbook"></a>4. adım - yayımlama ve hello runbook başlatın
oluşturduğumuz hello runbook hala taslak modunda değil. Toopublish ihtiyacımız, biz üretimde çalıştırılabilmesi için önce.  Bir runbook yayımladığınızda, hello Taslak sürümü hello mevcut yayımlanmış sürümün üzerine.  Merhaba runbook oluşturduğumuz çünkü Örneğimizde, yayımlanan sürümü biz henüz yok.

1. Tıklatın **Yayımla** toopublish hello runbook ardından **Evet** istendiğinde.<br><br> ![Yayımla düğmesi](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. Sol tooview hello hello runbook'ta kaydırırsanız **Runbook'lar** bölmesinde şimdi gösterilir bir **yazma durumu** , **yayımlanan**.
3. Kaydırma geri toohello sağ tooview hello bölmesini için **MyFirstRunbook-PowerShell**.  
   Merhaba seçenekleri hello üstte bize toostart hello runbook izin, hello runbook görüntülemek, hello gelecekteki bazı zamanında toostart zamanlama veya oluşturma bir [Web kancası](automation-webhooks.md) başlatılmış olması için bir HTTP çağrısı aracılığıyla.
4. Toostart hello runbook istediğiniz, bu nedenle tıklatın **Başlat** ve ardından **Tamam** zaman hello Runbook'u Başlat dikey pencere açılır.<br><br> ![Başlat düğmesi](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. Oluşturduğumuz hello runbook işi için bir iş bölmesi açıldı. Biz bu bölme kapatılabilir, ancak biz hello işin ilerleme durumunu izleyebilmek için bu durumda biz açık bırakın.
6. Merhaba iş durumu gösterilir **iş özeti** ve eşleşmeleri hello zaman hello runbook test gördüğümüz durumların.<br><br> ![İş Özeti](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. Runbook durumu gösterir'bir kez hello *tamamlandı*, tıklatın **çıkış**. Merhaba çıktı bölmesi açılır ve görebiliriz bizim *Hello World*.<br><br> ![İş Çıktısı](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. Kapat hello çıkış bölmesi.
9. Tıklatın **tüm günlükleri** tooopen hello akışlar bölmesini hello runbook işi için. Yalnızca görmeliyiz *Hello World* hello çıkış akışı, ancak bu ayrıntılı ve hata gibi runbook işine yönelik diğer akışlar hello runbook toothem yazıyorsa gösterebilir.<br><br> ![Tüm Günlükler](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. Merhaba akışlar bölmesini ve hello iş tooreturn toohello MyFirstRunbook-PowerShell bölmesini kapatın.
11. Tıklatın **işleri** tooopen hello işleri bölmesinde bu runbook için. Bu, tüm bu runbook tarafından oluşturulan hello işlerini listeler. Yalnızca bir işin yalnızca hello iş kez karşılaştık beri listelendiğini görmeliyiz.<br><br> ![İş Listesi](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. Bu iş tıklayabilirsiniz tooopen hello biz hello runbook'u başlattığımızda, görüntülediğimiz iş bölmesini. Bu, toogo geri belirli bir runbook için oluşturulan herhangi bir işi zaman ve görünüm hello ayrıntılarını sağlar.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>5. adım - kimlik doğrulama toomanage ekleme Azure kaynakları
Runbook uygulamamızı test ettik ve yayımladık, ancak şu ana kadar faydalı bir şey yapmadı. Azure kaynaklarını yönetmek toohave istiyoruz. Biz kimlik doğrulaması ancak hello kimlik bilgilerini kullanarak tooin hello başvurulan olduğunu mümkün toodo olmayacaktır [Önkoşullar](#prerequisites). Merhaba ile bunu **Add-AzureRmAccount** cmdlet'i.

1. Tıklayarak metin düzenleyicisini açın hello **Düzenle** hello MyFirstRunbook-PowerShell bölmesinde.<br><br> ![Runbook’u Düzenleme](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. Merhaba gerekmez **Write-Output** satırı artık, bu nedenle bir tane silin.
3. Yazın veya kopyalayıp hello kimlik doğrulaması Automation farklı çalıştır hesabınız ile işleyen kodu aşağıdaki hello yapıştırın:
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. Tıklatın **Test bölmesi** böylece hello runbook test edebilirsiniz.
5. Tıklatın **Başlat** toostart hello test. Tamamlandığında, aşağıdaki, hesabınızdaki temel bilgileri görüntüleyen benzer toohello çıkış almanız gerekir. Bu, o hello kimlik bilgisi geçerli olduğunu doğrular.<br><br> ![Kimlik Doğrulaması](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>6. adım - kod toostart bir sanal makine ekleme
Runbook uygulamamız tooour Azure aboneliği kimlik doğrulaması, kaynakları yönetebiliriz. Şu komutu toostart bir sanal makine ekleyin. Tüm sanal makineler Azure aboneliğinizde seçebilirsiniz ve şimdilik biz stillerinizin hello runbook ad olacaktır.

1. Sonra *Add-AzureRmAccount*, türü *Start-AzureRmVM-Name 'VMName' - ResourceGroupName 'NameofResourceGroup'* hello adını ve kaynak grubu adını hello sanal makine toostart sağlama.  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. Merhaba runbook'u kaydedin ve ardından **Test bölmesi** böylece test edebiliriz.
3. Tıklatın **Başlat** toostart hello test. Tamamlandığında, sanal makine hello onay başlatıldı.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>7. adım - bir giriş parametresi toohello runbook Ekle
Runbook uygulamamız şu anda başlar hello sanal makineyi sabit kodlanmış hello runbook'taki ancak hello runbook başlatıldığında biz hello sanal makine belirtirseniz, daha kullanışlı olurdu. Giriş parametreleri toohello runbook tooprovide şimdi bu işlevselliği ekleyeceksiniz.

1. Parametrelerini ekleyin *VMName* ve *ResourceGroupName* toohello runbook ve bu değişkenleri ile Merhaba **Start-AzureRmVM** hello örnekte olduğu gibi cmdlet.  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. Merhaba runbook'u kaydedin ve hello Test bölmesini açın. Şimdi, Merhaba hello testinde kullanılan iki girdi değişkeni değerleri sağlayabilir.
3. Kapat hello Test bölmesi.
4. Tıklatın **Yayımla** toopublish hello yeni sürümünü hello runbook.
5. Merhaba önceki adımda başlattığınız Hello sanal makineyi durdurun.
6. Tıklatın **Başlat** toostart hello runbook. Merhaba türü **VMName** ve **ResourceGroupName** hello sanal makine toostart oluşturacağız.<br><br> ![Parametre Geçirme](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. Merhaba runbook tamamlandığında, sanal makine hello onay başlatıldı.

## <a name="differences-from-powershell-workflow"></a>PowerShell İş Akışı ile arasındaki farklar
PowerShell runbook'ları sahip hello aynı yaşam döngüsü, yetenekler ve yönetim PowerShell iş akışı runbook'ları olarak ancak bazı farklar ve sınırlamalar vardır:

1. Derleme adımı yok gibi PowerShell runbook'ları hızlı karşılaştırılan tooPowerShell iş akışı runbook'ları çalıştırın.
2. PowerShell iş akışı runbook'ları kontrol noktalarının kullanılması destek, PowerShell runbook'ları yalnızca hello baştan devam edebilirsiniz ancak PowerShell iş akışı runbook'ları hello runbook'ta herhangi bir noktadan sürdürebilirsiniz.
3. PowerShell İş Akışı runbook'ları paralel ve seri yürütmeyi desteklerken, PowerShell runbook'ları yalnızca komutların seri olarak yürütülmesini destekler.
4. PowerShell İş Akışı runbook'unda bir etkinliğin, komutun veya betik bloğunun kendi çalışma alanı bulunabilirken, PowerShell runbook'unda betikteki her şey tek bir çalışma alanında çalıştırılır. Ayrıca yerel bir PowerShell runbook'u ile bir PowerShell İş Akışı runbook'u arasında bazı [söz dizimi farklılıkları](https://technet.microsoft.com/magazine/dn151046.aspx) vardır.

## <a name="next-steps"></a>Sonraki adımlar
* Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md)
* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)
* runbook türleri, avantajları ve sınırlamaları, hakkında daha fazla tooknow bakın [Azure Automation runbook türleri](automation-runbook-types.md)
* PowerShell betik desteği özelliği hakkında daha fazla bilgi için bkz. [Azure Automation’da Yerel PowerShell betik desteği](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

