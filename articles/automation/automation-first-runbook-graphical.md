---
title: Azure automation'da ilk grafik runbook aaaMy | Microsoft Docs
description: "Test ve basit bir grafik runbook yayımlama hello oluşturma adımlarını anlatan öğretici."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "runbook, runbook şablonu, runbook otomasyonu, azure runbook"
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>İlk grafik runbook uygulamam

> [!div class="op_single_selector"]
> * [Grafik](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell İş Akışı](automation-first-runbook-textual.md)
> 
> 

Bu öğreticide, hello oluşturulmasını açıklanmaktadır bir [grafik runbook](automation-runbook-types.md#graphical-runbooks) Azure Automation.  Biz sınayan ve biz nasıl tootrack hello hello runbook işinin durumunu açıklarken yayımlar basit bir runbook ile başlatın.  Biz hello runbook değiştirebilir sonra tooactually yönetmek Azure kaynaklarını, bu durumda bir Azure sanal makinesi başlatılıyor.  Ardından biz hello runbook'u daha sağlam runbook parametreleri ve koşula bağlı bağlantılar ekleyerek yaparak hello öğretici tamamlayın.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğreticiyi izleyerek hello gerekir.

* Azure aboneliği.  Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).
* [Azure Otomasyon hesabı](automation-sec-configure-azure-runas-account.md) toohold runbook hello ve tooAzure kaynakları kimlik doğrulaması.  Bu hesap, izin toostart sahip ve hello sanal makineyi durdurun.
* Azure sanal makinesi.  Bu makineyi durdurup başlatacağımız için makinenin üretime yönelik olmaması gerekir.

## <a name="step-1---create-runbook"></a>1. Adım - Runbook oluşturma
Merhaba metnini veren basit bir runbook oluşturarak başlangıç *Hello World*.

1. Hello Azure portal, Automation hesabınızı açın.  
   Merhaba Automation hesabı sayfası, bu hesapta hello kaynakların hızlı bir görünümünü sağlar.  Birkaç Varlığınız zaten olmalıdır.  Bunların çoğu, yeni bir Otomasyon hesabı içinde otomatik olarak dahil edilen hello modüllerdir.  Hello belirtiliyor hello kimlik bilgisi varlığı de olmalıdır [Önkoşullar](#prerequisites).
2. Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.<br> ![Runbook denetimi](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Merhaba üzerinde tıklatarak yeni bir runbook oluşturmak **runbook Ekle** düğmesine ve ardından **yeni bir runbook oluşturmak**.
4. Merhaba runbook hello adlandırın *MyFirstRunbook-Graphical*.
5. Bu durumda, toocreate yapacağız bir [grafik runbook](automation-graphical-authoring-intro.md) şekilde select **grafik** için **Runbook türü**.<br> ![Yeni runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Tıklatın **oluşturma** toocreate hello runbook ve açık hello grafik düzenleyici.

## <a name="step-2---add-activities-toohello-runbook"></a>2. adım - etkinlikleri toohello runbook Ekle
Merhaba hello hello Düzenleyicisi sol tarafındaki kitaplık denetimi tooselect etkinlikleri tooadd tooyour runbook sağlar.  Tooadd yapacağız bir **Write-Output** hello runbook'tan cmdlet toooutput metin.

1. Hello kitaplığı denetimi, hello arama metin kutusuna ve türü'i tıklatın **Write-Output**.  Merhaba arama sonuçları altında görüntülenir. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Merhaba listesinin toohello altında kaydırın.  Ya da sağ tıklatma yapabilecekleriniz **Write-Output** seçip **toocanvas eklemek** veya hello elips sonraki toohello cmdlet'ı tıklatın ve ardından **toocanvas eklemek**.
3. Merhaba tıklatın **Write-Output** hello tuval üzerinde etkinlik.  Bu tooconfigure hello etkinlik verir hello yapılandırma denetimi dikey açar.
4. Merhaba **etiket** toohello hello cmdlet'in adını varsayılan olarak, ancak biz toosomething daha kolay değiştirebilirsiniz. Çok değiştirme*yazma Hello World toooutput*.
5. Tıklatın **parametreleri** hello cmdlet parametreleri için tooprovide değerleri.  
   Bazı cmdlet'ler birden çok parametre kümesine sahiptir ve hangi, bir toouse tooselect gerekir. Bu durumda, **Write-Output** yalnızca bir parametre kümesine sahiptir, bu nedenle tooselect biri gerekmez. <br> ![Write-Output özellikleri](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Select hello **Inputobject** parametresi.  Bu hello biz hello metin toosend toohello çıkış akışı belirlediğiniz parametredir.
7. Merhaba, **veri kaynağı** açılan listesinde, select **PowerShell ifadesi**.  Merhaba **veri kaynağı** açılır farklı kaynaklar sağlar toopopulate bir parametre değeri kullanın.  
   Başka bir etkinlik, Automation varlığı ya da PowerShell ifadesi gibi böyle kaynaklardan alınan çıktıları kullanabilirsiniz.  Toooutput hello metin yalnızca bu durumda, istiyoruz *Hello World*. Bir PowerShell ifadesi kullanabilir ve dize belirtebiliriz.
8. Merhaba, **ifade** kutusuna *"Hello World"* ve ardından **Tamam** iki kez tooreturn toohello tuvale.<br> ![PowerShell İfadesi](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Tıklayarak Hello runbook'u kaydetmek **kaydetmek**.<br> ![Runbook’u kaydetme](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>3. adım - hello runbook sınaması
Biz hello runbook toomake yayımlamadan önce onu üretimde kullanılabilir tootest istiyoruz, toomake düzgün çalıştığından emin.  Bir runbook'u test ettiğinizde, bunun **Taslak** sürümünü çalıştırır ve çıktısını etkileşimli olarak görüntülersiniz.

1. Tıklatın **Test bölmesi** tooopen hello Test dikey penceresini.<br> ![Test bölmesi](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Tıklatın **Başlat** toostart hello test.  Bu, yalnızca etkin hello seçeneği olmalıdır.
3. A [runbook işi](automation-runbook-execution.md) oluşturulur ve durumu hello bölmesinde görüntülenir.  
   Merhaba iş durumunu başlatır olarak *sıraya alınan* bir runbook worker'hello bulut toobecome için bekleyen belirten.  Ardından çok taşır*başlangıç* bir çalışan hello işi talep ettiğinde ve ardından *çalıştıran* hello runbook gerçekten çalışmaya başladığında.  
4. Merhaba runbook işi tamamlandığında çıktısı görüntülenir. Örneğimizde, *Hello World* metnini görmeliyiz.<br> ![Hello World](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Merhaba Test dikey tooreturn toohello tuvale kapatın.

## <a name="step-4---publish-and-start-hello-runbook"></a>4. adım - yayımlama ve hello runbook başlatın
oluşturduğumuz hello runbook hala taslak modunda değil. Toopublish ihtiyacımız, biz üretimde çalıştırılabilmesi için önce.  Bir runbook yayımladığınızda, hello Taslak sürümü hello mevcut yayımlanmış sürümün üzerine.  Merhaba runbook oluşturduğumuz çünkü Örneğimizde, yayımlanan sürümü biz henüz yok.

1. Tıklatın **Yayımla** toopublish hello runbook ardından **Evet** istendiğinde.<br> ![Yayımlama](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Sol tooview hello hello runbook'ta kaydırırsanız **Runbook'lar** dikey penceresinde, gösterir bir **yazma durumu** , **yayımlanan**.
3. Kaydırma geri toohello sağ tooview hello dikey **MyFirstRunbook**.  
   Merhaba seçenekleri hello üstte bize toostart hello runbook izin, gelecekteki hello bazı zamanında toostart zamanlama veya oluşturma bir [Web kancası](automation-webhooks.md) başlatılmış olması için bir HTTP çağrısı aracılığıyla.
4. Yalnızca toostart hello runbook istiyoruz böylece tıklatın **Başlat** ve ardından **Evet** istendiğinde.<br> ![Runbook’u başlatma](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Oluşturduğumuz hello runbook işi için bir iş dikey penceresi açılır.  Biz bu dikey pencere kapatılabilir, ancak biz hello işin ilerleme durumunu izleyebilmek için bu durumda biz açık bırakın.
6. Merhaba iş durumu gösterilir **iş özeti** ve eşleşmeleri hello zaman hello runbook test gördüğümüz durumların.<br> ![İş Özeti](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Runbook durumu gösterir'bir kez hello *tamamlandı*, tıklatın **çıkış**. Merhaba **çıkış** dikey penceresi açılır ve görebiliriz bizim *Hello World* hello bölmesinde.<br> ![İş Özeti](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Çıktı Dikey penceresini kapat hello.
9. Tıklatın **tüm günlükleri** tooopen hello akışlar dikey hello runbook işi için.  Yalnızca görmeliyiz *Hello World* hello çıkış akışı, ancak bu ayrıntılı ve hata gibi runbook işine yönelik diğer akışlar hello runbook toothem yazıyorsa gösterebilir.<br> ![İş Özeti](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Merhaba tüm günlükler dikey penceresini ve hello iş dikey tooreturn toohello MyFirstRunbook dikey penceresini kapatın.
11. Tıklatın **işleri** tooopen hello işler dikey penceresinde bu runbook için.  Bu, bu runbook tarafından oluşturulan tüm hello işleri listeler. Yalnızca bir işin yalnızca hello iş kez karşılaştık beri listelendiğini görmeliyiz.<br> ![İşler](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. Bu iş tıklayabilirsiniz tooopen hello biz hello runbook'u başlattığımızda, görüntülediğimiz iş bölmesini.  Bu, toogo geri belirli bir runbook için oluşturulan herhangi bir işi zaman ve görünüm hello ayrıntılarını sağlar.

## <a name="step-5---create-variable-assets"></a>5. Adım - Değişken varlıkları oluşturma
Runbook uygulamamızı test ettik ve yayımladık, ancak şu ana kadar faydalı bir şey yapmadı. Azure kaynaklarını yönetmek toohave istiyoruz.  Biz hello runbook tooauthenticate yapılandırmadan önce size bir değişken toohold hello abonelik kimliği oluşturur ve biz hello etkinlik tooauthenticate aşağıda 6. adımda ayarladıktan sonra başvuru.  Başvuru toohello abonelik bağlamına dahil olmak üzere birden çok abonelik arasındaki tooeasily iş sağlar.  Devam etmeden önce hello abonelik seçeneği kapalı hello Gezinti bölmesini abonelik Kimliğinizi kopyalayın.  

1. Merhaba Automation hesapları dikey penceresinde hello tıklayın **varlıklar** döşeme ve hello **varlıklar** dikey penceresi açılır.
2. Merhaba varlıklar dikey penceresinde hello tıklayın **değişkenleri** döşeme.
3. Merhaba değişkenleri dikey penceresinde **değişken Ekle**.<br>![Automation Değişkeni](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. Merhaba yeni değişken dikey penceresinde hello içinde **adı** kutusuna **Azuresubscriptionıd** ve hello **değeri** kutusuna abonelik kimliğinizi girin  Tutmak *dize* hello için **türü** ve hello varsayılan değerini **şifreleme**.  
5. Tıklatın **oluşturma** toocreate hello değişkeni.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>6. adım - kimlik doğrulama toomanage ekleme Azure kaynakları
Abonelik Kimliğimizi değişken toohold sahibiz, biz bizim runbook tooauthenticate başvurulan tooin hello hello farklı çalıştır kimlik bilgileri ile yapılandırabilirsiniz [Önkoşullar](#prerequisites).  Hello Azure farklı çalıştır bağlantısı ekleyerek bunu **varlık** ve **Add-AzureRMAccount** cmdlet toohello tuvale.  

1. Tıklayarak grafik düzenleyicisini açın hello **Düzenle** hello MyFirstRunbook dikey.<br> ![Runbook’u düzenleme](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. Merhaba gerekmez **Hello World yazmak toooutput** artık, bu nedenle sağ tıklatın ve seçin **silmek**.
3. Hello kitaplığı denetimi, genişletin **bağlantıları** ve ekleme **AzureRunAsConnection** seçerek toohello tuvale **toocanvas eklemek**.
4. Merhaba tuval üzerinde seçin **AzureRunAsConnection** ve hello yapılandırma denetim bölmesinde yazın **farklı çalıştır bağlantısını Al** hello içinde **etiket** metin kutusu.  Bu hello bağlantıdır
5. Hello kitaplığı denetimi, yazın **Add-AzureRmAccount** hello arama metin kutusuna.
6. Ekle **Add-AzureRmAccount** toohello tuvale.<br> ![Add-AzureRMAccount](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Üzerine gelerek **farklı çalıştır bağlantısını Al** hello şekli hello sonuna bir daire görünene kadar. Merhaba daire sürükleyip hello ok çok**Add-AzureRmAccount**.  oluşturduğunuz hello ok olan bir *bağlantı*.  Merhaba runbook başlatır ile **farklı çalıştır bağlantısını Al** ve ardından çalıştırın **Add-AzureRmAccount**.<br> ![Etkinlikler arasında bağlantı oluşturma](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. Merhaba tuval üzerinde seçin **Add-AzureRmAccount** ve yapılandırma hello bölmesini denetlemenize **oturum açma tooAzure** hello içinde **etiket** metin kutusu.
9. Tıklatın **parametreleri** ve hello Etkinlik parametresi yapılandırma dikey penceresi görünür.
10. **Add-AzureRmAccount** biz parametre değerleri sağlamadan önce birini tooselect ihtiyacımız şekilde birden çok parametre kümesine sahiptir.  Tıklatın **parametre** seçip hello **ServicePrincipalCertificatewithSubscriptionId** parametre kümesi.
11. Merhaba parametre kümesini seçtiğinizde hello parametreleri hello Etkinlik parametresi yapılandırma dikey penceresinde görüntülenir.  **APPLICATIONID**’ye tıklayın.<br> ![Azure RM hesabı parametreleri ekleme](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. Merhaba parametre değeri dikey penceresinde, seçin **etkinlik çıkışı** hello için **veri kaynağı** seçip **farklı çalıştır bağlantısını Al** hello için hello listesinden **alan yol** metin kutusuna **ApplicationId**ve ardından **Tamam**.  Merhaba etkinlik birden fazla özelliğe sahip bir nesne çıkardığından biz hello alan yolu için hello özelliğinin hello adı belirtirsiniz.
13. Tıklatın **CERTIFICATETHUMBPRINT**, hello parametre değeri dikey penceresinde seçip **etkinlik çıkışı** hello için **veri kaynağı**.  Seçin **farklı çalıştır bağlantısını Al** hello için hello listesinden **alan yolu** metin kutusuna **CertificateThumbprint**ve ardından **Tamam**.
14. ' I tıklatın **SERVICEPRINCIPAL**, hello parametre değeri dikey penceresinde seçip **ConstantValue** hello için **veri kaynağı**, hello seçeneğini **True**ve ardından **Tamam**.
15. Tıklatın **TENANTID**, hello parametre değeri dikey penceresinde seçip **etkinlik çıkışı** hello için **veri kaynağı**.  Seçin **farklı çalıştır bağlantısını Al** hello için hello listesinden **alan yolu** metin kutusuna **Tenantıd**ve ardından **Tamam** iki kez.  
16. Hello kitaplığı denetimi, yazın **Set-AzureRmContext** hello arama metin kutusuna.
17. Ekleme **Set-AzureRmContext** toohello tuvale.
18. Merhaba tuval üzerinde seçin **Set-AzureRmContext** ve yapılandırma hello bölmesini denetlemenize **abonelik kimliği belirt** hello içinde **etiket** metin kutusu.
19. Tıklatın **parametreleri** ve hello Etkinlik parametresi yapılandırma dikey penceresi görünür.
20. **Set-AzureRmContext** biz parametre değerleri sağlamadan önce birini tooselect ihtiyacımız şekilde birden çok parametre kümesine sahiptir.  Tıklatın **parametre** seçip hello **Subscriptionıd** parametre kümesi.  
21. Merhaba parametre kümesini seçtiğinizde hello parametreleri hello Etkinlik parametresi yapılandırma dikey penceresinde görüntülenir.  **SubscriptionID**’e tıklayın.
22. Merhaba parametre değeri dikey penceresinde, seçin **değişken varlığı** hello için **veri kaynağı** seçip **Azuresubscriptionıd** hello listesi ve ardından **Tamam**  iki kez.   
23. Üzerine gelerek **oturum açma tooAzure** hello şekli hello sonuna bir daire görünene kadar. Merhaba daire sürükleyip hello ok çok**abonelik kimliği belirt**.

Runbook'unuzda bu noktada hello aşağıdaki gibi görünmelidir: <br>![Runbook kimlik doğrulama yapılandırması](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>7. adım - etkinlik toostart bir sanal makine ekleme
Burada eklediğimiz bir **Start-AzureRmVM** etkinlik toostart bir sanal makine.  Merhaba cmdlet'ine adı, stillerinizin artık Azure aboneliğinizde ve için herhangi bir sanal makine seçebilirsiniz.

1. Hello kitaplığı denetimi, yazın **Start-AzureRm** hello arama metin kutusuna.
2. Ekleme **Start-AzureRmVM** toohello tuvale ve ardından altına tıklayarak sürükleyin **abonelik kimliği belirt**.
3. Üzerine gelerek **abonelik kimliği belirt** hello şekli hello sonuna bir daire görünene kadar.  Merhaba daire sürükleyip hello ok çok**Start-AzureRmVM**.
4. **Start-AzureRmVM**’yi seçin.  Tıklatın **parametreleri** ve ardından **parametre** tooview hello ayarlar için **Start-AzureRmVM**.  Select hello **ResourceGroupNameParameterSetName** parametre kümesi. **ResourceGroupName** ve **Ad**’ın yanında ünlem işareti olduğuna dikkat edin.  Bu, bunların gerekli parametreler olduğunu gösterir.  Ayrıca, her ikisinin de dize değerleri beklediğini unutmayın.
5. **Ad**’ı seçin.  Seçin **PowerShell ifadesi** hello için **veri kaynağı** ve biz bu runbook'la Başlat çift tırnak işareti ile çevrelenmiş hello sanal makinenin hello ad yazın.  **Tamam** düğmesine tıklayın.<br>![Start-AzureRmVM Adı Parametre Değeri](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. **ResourceGroupName**’i seçin. Kullanım **PowerShell ifadesi** hello için **veri kaynağı** ve çift tırnakların arasına hello kaynak grubunun hello ad yazın.  **Tamam** düğmesine tıklayın.<br> ![Start-AzureRmVM Parametreleri](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Hello runbook'u test edebilmemiz için Test bölmesine tıklayın.
8. Tıklatın **Başlat** toostart hello test.  Tamamlandığında, sanal makine hello onay başlatıldı.

Runbook'unuzda bu noktada hello aşağıdaki gibi görünmelidir: <br>![Runbook kimlik doğrulama yapılandırması](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>8. adım - ek giriş parametreleri toohello runbook Ekle
Runbook uygulamamız şu hello belirtilen hello kaynak grubu hello sanal makine şu anda başlatır **Start-AzureRmVM** cmdlet'i.  Runbook uygulamamız hello runbook çalıştırıldığında her ikisini de belirtirseniz, daha kullanışlı olurdu.  Şimdi giriş parametreleri toohello runbook tooprovide bu işlevselliği ekleriz.

1. Tıklayarak grafik düzenleyicisini açın hello **Düzenle** hello üzerinde **MyFirstRunbook** bölmesi.
2. Tıklatın **giriş ve çıkış** ve ardından **giriş Ekle** tooopen hello Runbook giriş parametresi bölmesini.<br> ![Runbook Giriş ve Çıkış](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Belirtin *VMName* hello için **adı**.  Tutmak *dize* hello için **türü**, ancak değiştirmek **zorunlu** çok*Evet*.  **Tamam** düğmesine tıklayın.
4. Adlı ikinci bir zorunlu giriş parametresi oluşturun *ResourceGroupName* ve ardından **Tamam** tooclose hello **giriş ve çıkış** bölmesi.<br> ![Runbook Giriş Parametreleri](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Select hello **Start-AzureRmVM** etkinliği ve ardından **parametreleri**.
6. Değişiklik hello **veri kaynağı** için **adı** çok**Runbook giriş** ve ardından **VMName**.<br>
7. Değişiklik hello **veri kaynağı** için **ResourceGroupName** çok**Runbook giriş** ve ardından **ResourceGroupName**.<br> ![Start-AzureVM Parametreleri](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Merhaba runbook'u kaydedin ve hello Test bölmesini açın.  Artık değerleri Merhaba hello testinde kullanmak iki girdi değişkeni sağlayabileceğinizi unutmayın.
9. Kapat hello Test bölmesi.
10. Tıklatın **Yayımla** toopublish hello yeni sürümünü hello runbook.
11. Merhaba önceki adımda başlattığınız Hello sanal makineyi durdurun.
12. Tıklatın **Başlat** toostart hello runbook.  Merhaba türü **VMName** ve **ResourceGroupName** hello sanal makine toostart oluşturacağız.<br> ![Runbook’u başlatma](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Merhaba runbook tamamlandığında, sanal makine hello onay başlatıldı.

## <a name="step-9---create-a-conditional-link"></a>9. Adım - Koşullu bağlantı oluşturma
Zaten başlatılmadığında toostart hello sanal makine yalnızca deneme böylece biz şimdi hello runbook değiştirin.  Ekleyerek bunu bir **Get-AzureRmVM** hello örnek düzeyi durumunu hello sanal makine alır cmdlet toohello runbook. Adlı bir PowerShell iş akışı kodu modülü ekleyin ve sonra **Get Status** hello sanal makine durumu çalışıyor veya durdurulmuştur ise PowerShell parçacığıyla toodetermine kod.  Merhaba koşullu bağlantı **Get Status** modülü yalnızca çalışır **Start-AzureRmVM** hello geçerli çalışma durumu Durduruldu ise.  Son olarak, bir ileti tooinform başarıyla başlatıldı veya değil kullanarak hello VM isteyip PowerShell Write-Output cmdlet'ini hello çıktı.

1. Açık **MyFirstRunbook** hello grafik Düzenleyicisi'nde.
2. Arasında hello bağlantıyı Kaldır **abonelik kimliği belirt** ve **Start-AzureRmVM** üzerine tıklayarak ve ardından hello basarak *silmek* anahtarı.
3. Hello kitaplığı denetimi, yazın **Get-AzureRm** hello arama metin kutusuna.
4. Ekleme **Get-AzureRmVM** toohello tuvale.
5. Seçin **Get-AzureRmVM** ve ardından **parametre** tooview hello ayarlar için **Get-AzureRmVM**.  Select hello **Getvirtualmachineınresourcegroupnameparamset** parametre kümesi.  **ResourceGroupName** ve **Ad**’ın yanında ünlem işareti olduğuna dikkat edin.  Bu, bunların gerekli parametreler olduğunu gösterir.  Ayrıca, her ikisinin de dize değerleri beklediğini unutmayın.
6. **Ad** için **Veri kaynağı** altında, **Runbook girişi**’ni ve ardından **VMName**’i seçin.  **Tamam**’a tıklayın.
7. **ResourceGroupName** için **Veri kaynağı** altında, **Runbook girişi**’ni ve ardından **ResourceGroupName**’i seçin.  **Tamam** düğmesine tıklayın.
8. **Durum** için **Veri kaynağı** altında, **Sabit değer**’i seçin ve ardından **True** öğesine tıklayın.  **Tamam** düğmesine tıklayın.  
9. Bağlantı oluşturmak **abonelik kimliği belirt** çok**Get-AzureRmVM**.
10. Merhaba kitaplık denetiminde genişletin **Runbook denetimi** ve ekleme **kod** toohello tuvale.  
11. Bağlantı oluşturmak **Get-AzureRmVM** çok**kod**.  
12. Tıklatın **kod** değiştirip hello yapılandırma bölmesinde etiketi çok**Get Status**.
13. Seçin **kod** parametre ve hello **Kod düzenleyicisinde** dikey penceresi görünür.  
14. Merhaba Kod Düzenleyicisi'nde hello aşağıdaki kod parçacığını yapıştırın:
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. Bağlantı oluşturmak **Get Status** çok**Start-AzureRmVM**.<br> ![Kod Modülü ile Runbook](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Merhaba bağlantıyı seçin ve hello yapılandırma bölmesinde değiştirmek **koşul Uygula** çok**Evet**.   Not hello bağlantı hello koşulu tootrue çözümlenirse hello hedef etkinliğin yalnızca çalıştığını belirten kesikli tooa satır etkinleştirir.  
17. Hello için **koşul ifadesi**, türü *$ActivityOutput ['Get Status'] - eq "Stopped"*.  **Start-AzureRmVM** hello sanal makine durursa artık yalnızca çalıştırır.
18. Hello kitaplığı denetimi, genişletin **cmdlet'leri** ve ardından **Microsoft.PowerShell.Utility**.
19. Ekleme **Write-Output** toohello tuvale iki kez.<br> ![Write-Output ile Runbook](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. Merhaba üzerinde ilk **Write-Output** denetlemek, tıklatın **parametreleri** hello değiştirip **etiket** çok değer*VM başlatıldığında bildir*.
21. İçin **Inputobject**, değiştirme **veri kaynağı** çok**PowerShell ifadesi** ve hello ifade türü *"$VMName successfully started."* .
22. Merhaba üzerinde ikinci **Write-Output** denetlemek, tıklatın **parametreleri** hello değiştirip **etiket** çok değer*VM başlatma başarısız olduğunda bildir*
23. İçin **Inputobject**, değiştirme **veri kaynağı** çok**PowerShell ifadesi** ve hello ifade türü *"$VMName could not start."* .
24. Bağlantı oluşturmak **Start-AzureRmVM** çok**VM başlatıldığında bildir** ve **VM başlatma başarısız olduğunda bildir**.
25. Merhaba bağlantıyı çok seçin**VM başlatıldığında bildir** değiştirip **koşul Uygula** çok**doğru**.
26. Hello için **koşul ifadesi**, türü *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - eq $true*.  Bu Write-Output hello sanal makine başarıyla başlatıldığında artık yalnızca denetler.
27. Merhaba bağlantıyı çok seçin**VM başlatma başarısız olduğunda bildir** değiştirip **koşul Uygula** çok**doğru**.
28. Hello için **koşul ifadesi**, türü *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - ne $true*.  Bu Write-Output denetimi artık yalnızca çalıştırır hello sanal makine başarıyla başlatılmadığında.
29. Merhaba runbook'u kaydedin ve hello Test bölmesini açın.
30. Merhaba sanal makine kapalı iken Hello runbook'u başlatmak ve başlamanız gerekir.

## <a name="next-steps"></a>Sonraki adımlar
* Grafik yazma hakkında daha fazla toolearn bakın [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md)
* PowerShell runbook'ları ile çalışmaya tooget bakın [ilk PowerShell runbook'um](automation-first-runbook-textual-powershell.md)
* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)

