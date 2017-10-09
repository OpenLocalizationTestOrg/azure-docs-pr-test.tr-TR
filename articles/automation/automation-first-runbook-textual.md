---
title: "Azure automation'da ilk PowerShell iş akışı runbook aaaMy | Microsoft Docs"
description: "Test ve PowerShell iş akışı kullanarak basit bir runbook yayımlama hello oluşturma adımlarını anlatan öğretici."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "powershell iş akışı, powershell iş akışı örnekleri, iş akışı powershell"
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b5a34d363ef4865878f3f68119833367b5280f83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-workflow-runbook"></a>İlk PowerShell İş Akışı runbook uygulamam

> [!div class="op_single_selector"]
> * [Grafik](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell İş Akışı](automation-first-runbook-textual.md)
> 
> 

Bu öğreticide, hello oluşturulmasını açıklanmaktadır bir [PowerShell iş akışı runbook'u](automation-runbook-types.md#powershell-workflow-runbooks) Azure Automation. Test ve nasıl tootrack hello hello runbook işinin durumunu açıklayan sırasında yayımlama basit bir runbook ile başlatın. Biz hello runbook değiştirebilir sonra tooactually yönetmek Azure kaynaklarını, bu durumda bir Azure sanal makinesi başlatılıyor. Son olarak runbook parametreleri ekleyerek runbook'u daha sağlam hello olun.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğreticiyi izleyerek hello gerekir:

* Azure aboneliği. Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).
* [Otomasyon hesabı](automation-sec-configure-azure-runas-account.md) toohold runbook hello ve tooAzure kaynakları kimlik doğrulaması.  Bu hesap, izin toostart sahip ve hello sanal makineyi durdurun.
* Azure sanal makinesi. Bu makineyi durdurup başlatacağımız için makinenin üretime yönelik bir VM olmaması gerekir.

## <a name="step-1---create-new-runbook"></a>1. Adım - Yeni runbook oluşturma
Merhaba metnini veren basit bir runbook oluşturarak başlayacağız *Hello World*.

1. Hello Azure portal, Automation hesabınızı açın.  
   Merhaba Automation hesabı sayfası, bu hesapta hello kaynakların hızlı bir görünümünü sağlar. Birkaç varlığınız zaten olmalıdır. Bunların çoğu, yeni bir Otomasyon hesabı içinde otomatik olarak dahil edilen hello modüllerdir. Hello belirtiliyor hello kimlik bilgisi varlığı de olmalıdır [Önkoşullar](#prerequisites).
2. Tıklatın hello üzerinde **Runbook'lar** döşeme tooopen hello listesini.<br><br> ![Runbook denetimi](media/automation-first-runbook-textual/runbooks-control-tiles.png)
3. Merhaba üzerinde tıklatarak yeni bir runbook oluşturmak **runbook Ekle** düğmesine ve ardından **yeni bir runbook oluşturmak**.
4. Merhaba runbook hello adlandırın *MyFirstRunbook-Workflow*.
5. Bu durumda, toocreate yapacağız bir [PowerShell iş akışı runbook'u](automation-runbook-types.md#powershell-workflow-runbooks) şekilde select **Powershell iş akışı** için **Runbook türü**.<br><br> ![Yeni runbook](media/automation-first-runbook-textual/new-runbook-properties.png)
6. Tıklatın **oluşturma** toocreate hello runbook ve açık hello metin düzenleyicisini.

## <a name="step-2---add-code-toohello-runbook"></a>2. adım - kod toohello runbook Ekle
Doğrudan hello runbook'a kodu olabilir veya bunları toohello runbook ilgili parametrelerle ekledikten ve kitaplığı denetimi hello cmdlet'leri, runbook'ları ve varlıkları seçebilir. Bu kılavuz için sizi doğrudan hello runbook'a yazmanız gerekir.

1. Yalnızca gerekli hello ile runbook uygulamamız şu anda boş *iş akışı* anahtar sözcüğü, bizim runbook ve hello tüm iş akışını içerecek hello küme ayraçları hello adı.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. Ayraçlar arasına *Write-Output "Hello World."* Hello yazın.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. Tıklayarak Hello runbook'u kaydetmek **kaydetmek**.<br><br> ![Runbook’u kaydetme](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)

## <a name="step-3---test-hello-runbook"></a>3. adım - hello runbook sınaması
Biz hello runbook toomake yayımlamadan önce onu üretimde kullanılabilir tootest istiyoruz, toomake düzgün çalıştığından emin. Bir runbook'u test ettiğinizde, bunun **Taslak** sürümünü çalıştırır ve çıktısını etkileşimli olarak görüntülersiniz.

1. Tıklatın **Test bölmesi** tooopen hello Test bölmesi.<br><br> ![Test bölmesi](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)
2. Tıklatın **Başlat** toostart hello test. Bu, yalnızca etkin hello seçeneği olmalıdır.
3. Bir [runbook işi](automation-runbook-execution.md) oluşturulur ve durumu görüntülenir.  
   Merhaba iş durumu olarak başlayacak *sıraya alınan* bir runbook worker'hello bulut toocome için bekleyen belirten. Ardından, çok taşınır*başlangıç* bir çalışan hello işi talep ettiğinde ve ardından *çalıştıran* hello runbook gerçekten çalışmaya başladığında.  
4. Merhaba runbook işi tamamlandığında çıktısı görüntülenir. Örneğimizde, *Hello World* metnini görmeliyiz.<br><br> ![Hello World](media/automation-first-runbook-textual/test-output-hello-world.png)
5. Merhaba Test bölmesi tooreturn toohello tuvale kapatın.

## <a name="step-4---publish-and-start-hello-runbook"></a>4. adım - yayımlama ve hello runbook başlatın
Yeni oluşturduğumuz hello runbook hala taslak modunda değil. Toopublish ihtiyacımız, biz üretimde çalıştırılabilmesi için önce. Bir runbook yayımladığınızda, hello Taslak sürümü hello mevcut yayımlanmış sürümün üzerine. Merhaba runbook oluşturduğumuz çünkü Örneğimizde, yayımlanan sürümü biz henüz yok.

1. Tıklatın **Yayımla** toopublish hello runbook ardından **Evet** istendiğinde.<br><br> ![Yayımlama](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)
2. Sol tooview hello hello runbook'ta kaydırırsanız **Runbook'lar** bölmesinde şimdi gösterilir bir **yazma durumu** , **yayımlanan**.
3. Kaydırma geri toohello sağ tooview hello bölmesini için **MyFirstRunbook-Workflow**.  
   Merhaba seçenekleri hello üstte bize toostart hello runbook izin, gelecekteki hello bazı zamanında toostart zamanlama veya oluşturma bir [Web kancası](automation-webhooks.md) başlatılmış olması için bir HTTP çağrısı aracılığıyla.
4. Yalnızca toostart hello runbook istiyoruz böylece tıklatın **Başlat** ve ardından **Evet** istendiğinde.<br><br> ![Runbook’u başlatma](media/automation-first-runbook-textual/automation-runbook-controls-start.png)
5. Yeni oluşturduğumuz hello runbook işi için bir iş bölmesi açıldı. Biz bu bölme kapatılabilir, ancak biz hello işin ilerleme durumunu izleyebilmek için bu durumda, açık bırakacağız.
6. Merhaba iş durumu gösterilir **iş özeti** ve eşleşmeleri hello zaman hello runbook test gördüğümüz durumların.<br><br> ![İş Özeti](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)
7. Runbook durumu gösterir'bir kez hello *tamamlandı*, tıklatın **çıkış**. Merhaba çıktı bölmesi açılır ve görebiliriz bizim *Hello World*.<br><br> ![İş Özeti](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)  
8. Kapat hello çıkış bölmesi.
9. Tıklatın **tüm günlükleri** tooopen hello akışlar bölmesini hello runbook işi için. Yalnızca görmeliyiz *Hello World* hello çıkış akışı, ancak bu ayrıntılı ve hata gibi runbook işine yönelik diğer akışlar hello runbook toothem yazıyorsa gösterebilir.<br><br> ![İş Özeti](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)
10. Merhaba akışlar bölmesini ve hello iş tooreturn toohello MyFirstRunbook bölmesini kapatın.
11. Tıklatın **işleri** tooopen hello işleri bölmesinde bu runbook için. Bu, tüm bu runbook tarafından oluşturulan hello işlerini listeler. Yalnızca bir işin yalnızca hello iş kez karşılaştık beri listelendiğini görmeliyiz.<br><br> ![İşler](media/automation-first-runbook-textual/runbook-control-job-tile.png)
12. Bu iş tooopen hello aynı tıklatabilirsiniz biz hello runbook'u başlattığımızda, görüntülediğimiz iş bölmesini. Bu, toogo geri belirli bir runbook için oluşturulan herhangi bir işi zaman ve görünüm hello ayrıntılarını sağlar.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>5. adım - kimlik doğrulama toomanage ekleme Azure kaynakları
Runbook uygulamamızı test ettik ve yayımladık, ancak şu ana kadar faydalı bir şey yapmadı. Azure kaynaklarını yönetmek toohave istiyoruz. Biz kimlik doğrulaması ancak hello kimlik bilgilerini kullanarak tooin hello başvurulan olduğunu mümkün toodo olmayacaktır [Önkoşullar](#prerequisites). Merhaba ile bunu **Add-AzureRMAccount** cmdlet'i.

1. Tıklayarak metin düzenleyicisini açın hello **Düzenle** hello MyFirstRunbook-Workflow bölmesi.<br><br> ![Runbook’u düzenleme](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)
2. Merhaba gerekmez **Write-Output** satırı artık, bu nedenle bir tane silin.
3. Merhaba ayraçlar arasında boş bir satıra Hello imleç Konumlandır.
4. Yazın veya kopyalayıp Automation farklı çalıştır hesabınız ile Merhaba kimlik doğrulamasını işleyecek kod aşağıdaki hello yapıştırın:

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. Tıklatın **Test bölmesi** böylece hello runbook test edebilirsiniz.
6. Tıklatın **Başlat** toostart hello test. Tamamlandığında, aşağıdaki, hesabınızdaki temel bilgileri görüntüleyen benzer toohello çıkış almanız gerekir. Bu, o hello kimlik bilgisi geçerli olduğunu doğrular.<br><br> ![Kimlik Doğrulaması](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>6. adım - kod toostart bir sanal makine ekleme
Runbook uygulamamız tooour Azure aboneliği kimlik doğrulaması, kaynakları yönetebiliriz. Şu komutu toostart bir sanal makine ekleyin. Azure aboneliğinizde herhangi bir sanal makine seçin ve şu an için biz hello runbook'ta adı cmdlet'e kod olacaktır.

1. Sonra *Add-AzureRmAccount*, türü *Start-AzureRmVM-Name 'VMName' - ResourceGroupName 'NameofResourceGroup'* hello adını ve kaynak grubu adını hello sanal makine toostart sağlama.  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. Merhaba runbook'u kaydedin ve ardından **Test bölmesi** böylece test edebiliriz.
3. Tıklatın **Başlat** toostart hello test. Tamamlandığında, sanal makine hello onay başlatıldı.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>7. adım - bir giriş parametresi toohello runbook Ekle
Runbook uygulamamız şu anda başlar hello sanal makineyi sabit kodlanmış hello runbook'taki ancak hello runbook başlatıldığında hello sanal makine belirtirseniz, daha kullanışlı olurdu. Giriş parametreleri toohello runbook tooprovide şimdi bu işlevselliği ekleyeceksiniz.

1. Parametrelerini ekleyin *VMName* ve *ResourceGroupName* toohello runbook ve bu değişkenleri ile Merhaba **Start-AzureRmVM** hello örnekte olduğu gibi cmdlet.

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. Merhaba runbook'u kaydedin ve hello Test bölmesini açın. Artık değerleri Merhaba hello testte kullanılacak olan iki girdi değişkeni sağlayabileceğinizi unutmayın.
3. Kapat hello Test bölmesi.
4. Tıklatın **Yayımla** toopublish hello yeni sürümünü hello runbook.
5. Merhaba önceki adımda başlattığınız Hello sanal makineyi durdurun.
6. Tıklatın **Başlat** toostart hello runbook. Merhaba türü **VMName** ve **ResourceGroupName** hello sanal makine toostart oluşturacağız.<br><br> ![Runbook’u başlatma](media/automation-first-runbook-textual/automation-pass-params.png)<br>  
7. Merhaba runbook tamamlandığında, sanal makine hello onay başlatıldı.  

## <a name="next-steps"></a>Sonraki adımlar
* Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md)
* PowerShell runbook'ları ile çalışmaya tooget bakın [ilk PowerShell runbook'um](automation-first-runbook-textual-powershell.md)
* runbook türleri, avantajları ve sınırlamaları, hakkında daha fazla toolearn bakın [Azure Automation runbook türleri](automation-runbook-types.md)
* PowerShell betik desteği özelliği hakkında daha fazla bilgi için bkz. [Azure Automation’da Yerel PowerShell betik desteği](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
