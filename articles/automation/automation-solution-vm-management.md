---
title: "aaaStart/durdurma VM'ler yoğun olmayan saatlerde [Önizleme] çözüm sırasında | Microsoft Docs"
description: "Hello VM yönetim çözümleri başlatır ve Azure Resource Manager sanal makinelerinizi bir zamanlamaya göre durdurur ve önceden günlük analizi izleyin."
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Otomasyon’da VM’leri çalışma saatleri dışında Başlatma/Durdurma [Önizleme] çözümü

yoğun olmayan saatlerde [Önizleme] çözüm sırasında Hello Başlat/Durdur VM'ler başlatır ve Azure Resource Manager sanal makinelerinizi kullanıcı tanımlı bir zamanlamaya göre durdurur ve başlatma ve sanal makinelerinizi OMS ile durdurma hello Otomasyon işlerin hello başarılı bir anlayış sağlar Günlük analizi.  

## <a name="prerequisites"></a>Ön koşullar

- Merhaba runbook'ları ile çalışırsınız bir [Azure farklı çalıştır hesabı](automation-offering-get-started.md#authentication-methods).  süresi dolacak veya sık sık değişen parola yerine sertifika kimlik doğrulaması kullandığından hello farklı çalıştır hesabı hello tercih edilen kimlik doğrulama yöntemidir.  

- Bu çözüm yalnızca hello olan VM'ler yönetebilir hello Otomasyon hesabı bulunduğu olarak aynı abonelik.  

- Bu çözüm yalnızca Azure bölgeleri - Güneydoğu Avustralya, Doğu ABD, Güneydoğu Asya ve Batı Avrupa aşağıdaki toohello dağıtır.  Merhaba VM zamanlamasını yönetmek hello runbook'lar herhangi bir bölgede VM'ler hedefleyebilirsiniz.  

- Merhaba başlattığınızda ve VM runbook'lar tam Durdur toosend e-posta bildirimleri, bir Office 365 iş sınıfı aboneliği gereklidir.  

## <a name="solution-components"></a>Çözüm bileşenleri

Bu çözüm içeri aktarılacak ve tooyour Otomasyon hesabı eklenen kaynaklar aşağıdaki hello oluşur.

### <a name="runbooks"></a>Runbook'lar

Runbook | Açıklama|
--------|------------|
CleanSolution-MS-Mgmt-VM | Aboneliğinizden toodelete hello çözüm olduğunuzda bu runbook içerdiği tüm kaynaklar ve zamanlamaları kaldırır.|  
SendMailO365-MS-Mgmt | Bu runbook, Office 365 Exchange aracılığıyla e-posta gönderir.|
StartByResourceGroup-MS-Mgmt-VM | Bu runbook hedeflenen toostart VM'ler. (her iki Klasik ve ARM tabanlı VM'ler) belirli bir Azure kaynak gruplarını listesinde yer alıyor.
StopByResourceGroup-MS-Mgmt-VM | Bu runbook hedeflenen toostop VM'ler. (her iki Klasik ve ARM tabanlı VM'ler) belirli bir Azure kaynak gruplarını listesinde yer alıyor.|
<br>

### <a name="variables"></a>Değişkenler

Değişken | Açıklama|
---------|------------|
**SendMailO365-MS-Mgmt** Runbook ||
SendMailO365-IsSendEmail-MS-Mgmt | StartByResourceGroup-MS-Mgmt-VM ve StopByResourceGroup-MS-Mgmt-VM runbook'larının tamamlandıktan sonra bildirim e-postası gönderip gönderemeyeceklerini belirtir.  Seçin **True** tooenable ve **False** toodisable e-posta uyarı. Varsayılan ayar, **False** değeridir.| 
**StartByResourceGroup-MS-Mgmt-VM** Runbook ||
StartByResourceGroup ExcludeList-MS-Mgmt-VM | Yönetim işleminden hariç VM adları toobe girin; adları, boşluk olmadan virgül (;) kullanarak ayırın. Değerleri büyük/küçük harfe duyarlıdır ve joker karakter (yıldız işareti) kullanımı desteklenir.|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Olabilir metin hello e-posta ileti gövdesi toohello başına eklenir.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Merhaba hello e-posta runbook içeren bir Otomasyon hesabı Hello adını belirtir.  **Bu değişkeni değiştirmeyin.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Merhaba e-posta runbook Hello adını belirtir.  Bu hello StartByResourceGroup-MS-Mgmt-VM ve StopByResourceGroup-MS-Mgmt-VM runbook'lar toosend e-posta tarafından kullanılır.  **Bu değişkeni değiştirmeyin.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Merhaba hello e-posta runbook içeren hello kaynak grubunun adını belirtir.  **Bu değişkeni değiştirmeyin.**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Merhaba konu satırı hello e-postanın Hello metnini belirtir.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Merhaba alıcılara hello e-postanın belirtir.  Ayrı adları, boşluk olmadan virgül (;) kullanarak girin.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Yönetim işleminden hariç VM adları toobe girin; adları, boşluk olmadan virgül (;) kullanarak ayırın. Değerleri büyük/küçük harfe duyarlıdır ve joker karakter (yıldız işareti) kullanımı desteklenir.  Varsayılan değer (yıldız) tüm kaynak gruplarının hello abonelikte yer alır.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Bu çözümü tarafından yönetilen sanal makineleri toobe içeren hello abonelik belirtir.  Bu olmalıdır hello hello Automation hesabı, bu çözüme yönelik bulunduğu aynı abonelik.|
**StopByResourceGroup-MS-Mgmt-VM** Runbook ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Yönetim işleminden hariç VM adları toobe girin; adları, boşluk olmadan virgül (;) kullanarak ayırın. Değerleri büyük/küçük harfe duyarlıdır ve joker karakter (yıldız işareti) kullanımı desteklenir.|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Olabilir metin hello e-posta ileti gövdesi toohello başına eklenir.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Merhaba hello e-posta runbook içeren bir Otomasyon hesabı Hello adını belirtir.  **Bu değişkeni değiştirmeyin.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Merhaba hello e-posta runbook içeren hello kaynak grubunun adını belirtir.  **Bu değişkeni değiştirmeyin.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Merhaba konu satırı hello e-postanın Hello metnini belirtir.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Merhaba alıcılara hello e-postanın belirtir.  Ayrı adları, boşluk olmadan virgül (;) kullanarak girin.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Yönetim işleminden hariç VM adları toobe girin; adları, boşluk olmadan virgül (;) kullanarak ayırın. Değerleri büyük/küçük harfe duyarlıdır ve joker karakter (yıldız işareti) kullanımı desteklenir.  Varsayılan değer (yıldız) tüm kaynak gruplarının hello abonelikte yer alır.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Bu çözümü tarafından yönetilen sanal makineleri toobe içeren hello abonelik belirtir.  Bu olmalıdır hello hello Automation hesabı, bu çözüme yönelik bulunduğu aynı abonelik.|  
<br>

### <a name="schedules"></a>Zamanlamalar

Zamanlama | Açıklama|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | Bu çözümü tarafından yönetilen sanal makineleri hello başlatma gerçekleştirir StartByResourceGroup runbook için zamanlama. Oluşturduğunuzda, tooUTC saat dilimi varsayılan olarak ayarlanır.|
StopByResourceGroup-Schedule-MS-Mgmt | Bu çözümü tarafından yönetilen sanal makineleri hello kapatma gerçekleştirir StopByResourceGroup runbook için zamanlama. Oluşturduğunuzda, tooUTC saat dilimi varsayılan olarak ayarlanır.|

### <a name="credentials"></a>Kimlik Bilgileri

Kimlik Bilgisi | Açıklama|
-----------|------------|
O365Credential | Bir geçerli Office 365 kullanıcı hesabı toosend e-posta belirtir.  Yalnızca değişken SendMailO365-IsSendEmail-MS-Mgmt çok ayarlarsanız gerekli**doğru**.

## <a name="configuration"></a>Yapılandırma

Yoğun olmayan saatlerde [Önizleme] çözüm tooyour Otomasyon hesabı sırasında adımları tooadd hello Başlat/Durdur VM'ler aşağıdaki hello yapın ve ardından hello değişkenleri toocustomize hello çözüm yapılandırın.

1. Merhaba giriş-ekranından hello Azure portal'ın, hello seçin **Market** döşeme.  Merhaba kutucuğu artık sabitlenmiş tooyour giriş ekran, hello sol gezinti bölmesinden ise seçin **yeni**.  
2. Merhaba Market dikey penceresinde yazın **VM Başlat** hello arama kutusuna ve ardından hello çözüm **Başlat/Durdur VM'ler yoğun olmayan saatlerde [Önizleme] sırasında** hello Arama sonuçlarından.  
3. Merhaba, **Başlat/Durdur VM'ler yoğun olmayan saatlerde [Önizleme] sırasında** hello dikey penceresinde seçili çözüm, hello özet bilgileri gözden geçirin ve ardından **oluşturma**.  
4. Merhaba **Çözüm Ekle** Otomasyon aboneliğinizi içeri aktarmadan önce istendiğinde tooconfigure hello çözüm nerede dikey penceresi görünür.<br><br> ![VM Management Çözüm Ekleme dikey penceresi](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  Merhaba üzerinde **Çözüm Ekle** dikey penceresinde, select **çalışma** ve burada bağlantılı toohello Otomasyon hesabı hello aynı Azure aboneliği olan veya yeni bir OMS çalışma alanı oluşturma bir OMS çalışma alanını seçin.  Bir OMS çalışma alanı yoksa, seçebileceğiniz **yeni çalışma alanı oluştur** ve hello **OMS çalışma** dikey penceresinde hello aşağıdakileri gerçekleştirin: 
   - Merhaba yeni bir ad belirtin **OMS çalışma**.
   - Seçin bir **abonelik** hello varsayılan seçili uygun değilse toolink tooby hello aşağı açılan listeden seçerek..
   - **Kaynak Grubu** için, yeni bir kaynak grubu oluşturabilir veya mevcut bir kaynak grubunu seçebilirsiniz.  
   - Bir **Konum** seçin.  Geçerli seçim için sağlanan hello yalnızca konumlarının **Avustralya Güneydoğu**, **Doğu ABD**, **Güneydoğu Asya**, ve **Batı Avrupa**.
   - Bir **Fiyatlandırma katmanı** seçin.  Merhaba çözüm iki katmanlarda sunulur: boşaltın ve OMS Ücretli katmanı.  Merhaba ücretsiz katmanı hello günlük tutma süresi ve runbook iş çalışma zamanı dakika toplanan veri miktarına bir sınırı vardır.  Merhaba OMS katmanı Ücretli bir sınır hello günlük toplanan veri miktarına sahip değil.  

        > [!NOTE]
        > Merhaba katmanı Ücretli tek başına bir seçenek olarak görüntülendiği sırada geçerli değildir.  Seçip aboneliğinizde bu çözümün hello oluşturma işlemine devam edin, başarısız olur.  Bu çözüm resmi olarak yayımlandığında, bu sorun da ele alınacaktır.<br>Bu çözümü kullanırsanız, yalnızca otomasyon işi dakikaları ve günlük alımı kullanılır.  Merhaba çözüm ek OMS düğümleri tooyour ortam eklemez.  

6. Merhaba üzerinde hello gerekli bilgileri girdikten sonra **OMS çalışma** dikey penceresinde tıklatın **oluşturma**.  Merhaba bilgi doğrulanır ve hello çalışma alanı oluşturulur, ancak altında ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.  Toohello döndürülen **Çözüm Ekle** dikey.  
7. Merhaba üzerinde **Çözüm Ekle** dikey penceresinde, select **Otomasyon hesabı**.  Yeni bir OMS çalışma alanı oluşturuyorsanız, gerekli olacak tooalso Azure abonelik, kaynak grubu ve bölge gibi daha önce belirtilen hello yeni OMS çalışma alanı ile ilişkili yeni bir Otomasyon hesabı oluşturun.  Seçebileceğiniz **Automation hesabı oluşturma** ve hello **eklemek Otomasyon hesabı** dikey penceresinde hello şunları sağlar: 
  - Merhaba, **adı** alanında, hello hello Automation hesabı adını girin.

    Seçili hello OMS çalışma alanı temelli tüm diğer seçenekler otomatik olarak doldurulur ve bu seçenekleri değiştirilemez.  Bir Azure farklı çalıştır hesabı hello varsayılan kimlik doğrulama için bu çözümdeki hello runbook'ları yöntemidir.  Tıkladığınızda **Tamam**hello yapılandırma seçenekleri doğrulanır ve hello Otomasyon hesabı oluşturulur.  Altında ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde. 

    Aksi takdirde, mevcut bir Otomasyon Farklı Çalıştır hesabını seçebilirsiniz.  Seçtiğiniz hello hesabı zaten bağlı tooanother OMS çalışma olamaz, aksi takdirde bir ileti hello dikey tooinform, sunulacak dikkat edin.  Zaten bağlıysa, tooselect farklı bir Automation farklı çalıştır hesabı gerekiyor veya yeni bir tane oluşturun.<br><br> ![Otomasyon hesabı zaten bağlı tooOMS çalışma](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Son olarak hello üzerinde **Çözüm Ekle** dikey penceresinde, select **yapılandırma** ve hello **parametreleri** dikey penceresi görünür.  Merhaba üzerinde **parametreleri** dikey penceresinde istenir:  
   - Merhaba belirtin **hedef kaynak grubu adları**, bu çözümü tarafından yönetilen sanal makineleri toobe içeren bir kaynak grubu adı değil.  Her birini noktalı virgül ile ayırarak birden fazla ad girebilirsiniz (Değerler büyük küçük harfe duyarlıdır.)  Tootarget VM'ler hello Abonelikteki tüm kaynak gruplarında istiyorsanız bir joker karakter kullanılması desteklenir.
   - Seçin bir **zamanlama** olduğu bir yinelenen tarih ve saat için başlatma ve durdurma hello VM'in hello kaynak gruplarını hedefleyin.  Varsayılan olarak, hello zamanlama yapılandırılmış toohello UTC saat dilimi ve farklı bir bölge seçmek kullanılabilir değil.  Merhaba çözüm yapılandırdıktan sonra tooconfigure hello zamanlama tooyour belirli saat dilimi istiyorsanız, bkz: [değiştirme hello başlatma ve kapatma zamanlama](#modifying-the-startup-and-shutdown-schedule) aşağıda.    

10. Merhaba çözümü için gerekli hello ilk ayarları yapılandırmayı tamamladıktan sonra seçin **oluşturma**.  Tüm ayarlar doğrulanacak ve ardından toodeploy hello çözüm aboneliğinizde dener.  Bu işlem birkaç sürebilir saniye toocomplete ve altında ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde. 

## <a name="collection-frequency"></a>Toplama sıklığı

Otomasyon iş günlüğü ve iş akışı veri hello OMS depoya beş dakikada alınan.  

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak

Merhaba VM yönetim çözümü, OMS çalışma hello eklediğinizde **StartStopVM Görünüm** döşeme tooyour OMS Pano eklenir.  Bu kutucuğu sayısı ve başlamış olması ve başarıyla tamamladınız hello runbook'lar işleri hello çözüm için grafik gösterimi görüntüler.<br><br> ![VM Management StartStopVM Görünümü Kutucuğu](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

Otomasyon hesabınızda erişmek ve hello seçerek hello çözüm yönetmek **çözümleri** döşeme ve sonra hello **çözümleri** hello çözümü seçme dikey penceresinde **Start-Stop-VM [ Çalışma alanı]** hello listeden.<br><br> ![Otomasyon Çözümleri Listesi](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Merhaba çözümü seçme hello görüntüler **Start-Stop-VM [çalışma]** gözden geçirebileceğiniz hello gibi önemli ayrıntıları çözüm dikey **StartStopVM** gibi OMS çalışma alanınızda döşeme hangi sayı ve başlamış olması ve başarıyla tamamladınız hello runbook'lar işleri hello çözüm için grafik gösterimi görüntüler.<br><br> ![Otomasyon VM Çözümü Dikey Penceresi](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

Buradan, OMS çalışma alanını açın ve başka hello iş kaydı analizler yapmak.  Tıklatmanız **tüm ayarları**ve hello **ayarları** dikey penceresinde, seçin **Hızlı Başlangıç** ve ardından hello **Hızlı Başlangıç** Dikeyseçin **OMS portalı**.   Böylece, yeni bir sekme veya yeni tarayıcı oturumu açılacak ve Otomasyon hesabınız ile aboneliğinize ilişkin OMS çalışma alanınız sunulacaktır.  


### <a name="configuring-e-mail-notifications"></a>E-posta bildirimlerini yapılandırma

tooenable e-posta bildirimleri hello zaman başlatmanızı ve durdurmanızı VM tam, toomodify hello gerekir **O365Credential** kimlik bilgisi ve en azından değişkenleri hello:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

tooconfigure hello **O365Credential** kimlik bilgisi, hello aşağıdaki adımları gerçekleştirin:

1. Otomasyon hesabınızdan tıklatın **tüm ayarları** hello penceresinin hello üstünde. 
2. Merhaba üzerinde **ayarları** dikey penceresinde hello bölümünde **Automation kaynaklarını**seçin **varlıklar**. 
3. Merhaba üzerinde **varlıklar** dikey penceresinde, select hello **kimlik bilgisi** döşeme ve hello **kimlik bilgisi** dikey penceresinde, select hello **O365Credential**.  
4. Geçerli Office 365 kullanıcı adı ve parola girin ve ardından **kaydetmek** toosave değişikliklerinizi.  

daha önce vurgulanmış tooconfigure hello değişkenleri hello aşağıdaki adımları gerçekleştirin:

1. Otomasyon hesabınızdan tıklatın **tüm ayarları** hello penceresinin hello üstünde. 
2. Merhaba üzerinde **ayarları** dikey penceresinde hello bölümünde **Automation kaynaklarını**seçin **varlıklar**. 
3. Merhaba üzerinde **varlıklar** dikey penceresinde, select hello **değişkenleri** döşeme ve hello **değişkenleri** dikey penceresinde, yukarıda listelenen hello değişken seçin ve hello aşağıdaki değerini değiştirin Bunu hello belirtilen açıklamasını [değişkeni](##variables) bölümüne.  
4. Tıklatın **kaydetmek** toosave hello değişiklikleri toohello değişkeni.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Değiştirme hello başlatma ve kapatma zamanlama

Bu çözümdeki yönetme hello başlatma ve kapatma zamanlama izleyen kısmında özetlendiği gibi aynı adımları hello [Azure Otomasyon runbook'u zamanlama](automation-schedules.md).  Unutmayın, hello zamanlama yapılandırmasını değiştiremezsiniz.  Toodisable gerekir mevcut zamanlamayı hello ve ardından yeni bir tane oluşturun ve toohello bağlantı **StartByResourceGroup-MS-Mgmt-VM** veya **StopByResourceGroup-MS-Mgmt-VM** hello istediğiniz runbook tooapply için zamanlayın.   

## <a name="log-analytics-records"></a>Log Analytics kayıtları

Otomasyon kayıtları iki tür hello OMS deposunda oluşturur.

### <a name="job-logs"></a>İş günlükleri

Özellik | Açıklama|
----------|----------|
Çağıran |  Kimin hello işlemini başlattı.  Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir.|
Kategori | Merhaba tür veri sınıflandırması.  Otomasyon için hello JobLogs değerdir.|
CorrelationId | Merhaba hello runbook işi bağıntı kimliği olan GUID.|
JobId | Merhaba hello runbook işi kimliği olan GUID.|
operationName | Azure üzerinde gerçekleştirilen işlem Hello türünü belirtir.  Otomasyon için iş hello değer olacaktır.|
resourceId | Azure'da Hello kaynak türünü belirtir.  Otomasyon için hello hello runbook'la ilişkili hello Otomasyon hesabı değerdir.|
ResourceGroup | Merhaba runbook işi Hello kaynak grubu adını belirtir.|
ResourceProvider | Merhaba dağıtmak ve yönetmek hello kaynakları sağlayan Azure hizmeti belirtir.  Otomasyon için hello Azure Otomasyonu değerdir.|
ResourceType | Azure'da Hello kaynak türünü belirtir.  Otomasyon için hello hello runbook'la ilişkili hello Otomasyon hesabı değerdir.|
resultType | Merhaba runbook işinin durumunu Hello.  Olası değerler şunlardır:<br>- Başlatıldı<br>- Durduruldu<br>- Askıya alındı<br>- Başarısız oldu<br>- Başarılı oldu|
resultDescription | Merhaba runbook iş sonuç durumu açıklar.  Olası değerler şunlardır:<br>- İş başlatıldı<br>- İş Başarısız Oldu<br>- İş Tamamlandı|
RunbookName | Merhaba runbook Hello adını belirtir.|
SourceSystem | Merhaba kaynak sistem gönderilen hello veri için belirtir.  Otomasyon için hello değer olacaktır: OpsManager|
StreamType | Olay Hello türünü belirtir. Olası değerler şunlardır:<br>- Ayrıntılı<br>- Çıktı<br>- Hata<br>- Uyarı|
SubscriptionId | Merhaba iş Hello abonelik Kimliğini belirtir.
Zaman | Tarih ve saat hello runbook işi zaman yürütülür.|


### <a name="job-streams"></a>İş akışları

Özellik | Açıklama|
----------|----------|
Çağıran |  Kimin hello işlemini başlattı.  Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir.|
Kategori | Merhaba tür veri sınıflandırması.  Otomasyon için hello JobStreams değerdir.|
JobId | Merhaba hello runbook işi kimliği olan GUID.|
operationName | Azure üzerinde gerçekleştirilen işlem Hello türünü belirtir.  Otomasyon için iş hello değer olacaktır.|
ResourceGroup | Merhaba runbook işi Hello kaynak grubu adını belirtir.|
resourceId | Azure'da Hello kaynak kimliği belirtir.  Otomasyon için hello hello runbook'la ilişkili hello Otomasyon hesabı değerdir.|
ResourceProvider | Merhaba dağıtmak ve yönetmek hello kaynakları sağlayan Azure hizmeti belirtir.  Otomasyon için hello Azure Otomasyonu değerdir.|
ResourceType | Azure'da Hello kaynak türünü belirtir.  Otomasyon için hello hello runbook'la ilişkili hello Otomasyon hesabı değerdir.|
resultType | Başlangıç saati hello olay hello runbook işi Hello sonucunu oluşturuldu.  Olası değerler şunlardır:<br>- Devam Ediyor|
resultDescription | Merhaba runbook Hello çıkış akışından içerir.|
RunbookName | Merhaba runbook Hello adı.|
SourceSystem | Merhaba kaynak sistem gönderilen hello veri için belirtir.  Otomasyon için OpsManager hello değer olacaktır|
StreamType | İş akışı Hello türü. Olası değerler şunlardır:<br>- İlerleme durumu<br>- Çıktı<br>- Uyarı<br>- Hata<br>- Hata ayıklama<br>- Ayrıntılı|
Zaman | Tarih ve saat hello runbook işi zaman yürütülür.|

Kategorisini kayıtlarını döndürür tüm günlük arama yaptığınızda **JobLogs** veya **JobStreams**, hello seçebileceğiniz **JobLogs** veya **JobStreams** bir dizi döşeme hello araması tarafından döndürülen hello güncelleştirmeleri özetlemeye görüntüleyen görünümü.

## <a name="sample-log-searches"></a>Örnek günlük aramaları

Merhaba aşağıdaki tabloda bu çözüm tarafından toplanan iş kaydı için örnek günlük aramaları sağlar. 

Sorgu | Açıklama|
----------|----------|
StartVM runbook’una ilişkin başarıyla tamamlanmış işleri bul | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
StopVM runbook’una ilişkin başarıyla tamamlanmış işleri bul | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
StartVM ve StopVM runbook'ları için zaman içerisinde iş durumunu göster | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Merhaba Çözüm kaldırma

Artık toouse hello çözüm herhangi daha fazla gereksinim karar verirseniz, Automation hesabı hello silebilirsiniz.  Merhaba çözümünün silinmesi hello runbook'ları yalnızca kaldırır, hello zamanlamaları veya hello çözüm eklediğinizde, oluşturulan değişkenleri silmez.  El ile bunları ile diğer runbook'ları kullanmıyorsanız bu varlıkları toodelete gerekir.  

toodelete Merhaba çözüm, hello aşağıdaki adımları gerçekleştirin:

1.  Merhaba, Otomasyon hesabınızı seçin **çözümleri** döşeme.  
2.  Merhaba üzerinde **çözümleri** dikey penceresinde, select hello çözüm **Start-Stop-VM [çalışma]**.  Merhaba üzerinde **VMManagementSolution [çalışma]** hello menü tıklayın dikey **silmek**.<br><br> ![VM yönetimi çözümü Sil](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  Merhaba, **silmek çözüm** penceresinde toodelete hello çözüm istediğinizi onaylayın.
4.  Merhaba bilgi doğrulanır ve hello çözüm silinir, ancak altında ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.  Toohello döndürülen **VMManagementSolution [çalışma]** hello işlem tooremove çözüm başladıktan sonra dikey.  

Bu işlemin bir parçası olarak Hello Otomasyon hesabı ve OMS çalışma silinmez.  Tooretain hello OMS çalışma istemiyorsanız gerekir toomanually silin.  Bu da Azure portal hello gerçekleştirilebilir.   Merhaba giriş-ekranından hello Azure portal'ın, seçin **günlük analizi** ve ardından hello **günlük analizi** dikey penceresinde, select hello çalışma ve tıklatın **silmek** hello menüsünden Merhaba çalışma ayarlar dikey penceresi.  
      
## <a name="next-steps"></a>Sonraki adımlar

- Günlük analizi ile günlükleri nasıl tooconstruct farklı arama sorguları ve gözden geçirme hello Otomasyon iş hakkında daha fazla toolearn bakın [oturum aramaları günlük analizi](../log-analytics/log-analytics-log-searches.md)
- toolearn hakkında daha fazla runbook yürütme toomonitor runbook işleri ve diğer teknik ayrıntıları görmek nasıl [bir runbook işi izlenemedi](automation-runbook-execution.md)
- OMS günlük analizi ve veri toplama kaynakları hakkında daha fazla toolearn bakın [toplama Azure storage veri günlük analizi genel bakış](../log-analytics/log-analytics-azure-storage.md)






   

