---
title: "VM’leri çalışma saatleri dışında Başlatma/Durdurma [Önizleme] Çözümü | Microsoft Belgeleri"
description: "VM Management çözümleri, Azure Resource Manager Sanal Makinelerinizi bir zamanlama dahilinde başlatıp durdurmanın yanı sıra Log Analytics aracılığıyla izler."
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
ms.openlocfilehash: e44f04b3492ac07822b0842864f84a5f16dc3f5b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Otomasyon’da VM’leri çalışma saatleri dışında Başlatma/Durdurma [Önizleme] çözümü

VM’leri çalışma saatleri dışında Başlatma/Durdurma [Önizleme] çözümü, Azure Resource Manager sanal makinelerinizi kullanıcının belirlediği bir zamanlamada başlatır ve durdurur. Ayrıca, OMS Log Analytics aracılığıyla, sanal makinelerinizi başlatan ve durduran Otomasyon işlerinin başarı durumu hakkında öngörüler sağlar.  

## <a name="prerequisites"></a>Önkoşullar

- Runbook'lar, [Azure Farklı Çalıştır hesabı](automation-offering-get-started.md#authentication-methods) ile çalışır.  Süresi dolabilecek ya da sık değişebilecek olan bir parola yerine sertifika doğrulaması kullandığından Farklı Çalıştır hesabı, tercih edilen kimlik doğrulama yöntemidir.  

- Bu çözüm yalnızca Otomasyon hesabının bulunduğu olarak aynı abonelikte bulunan sanal makineleri yönetebilirsiniz.  

- Bu çözüm, yalnızca şu Azure bölgelerine dağıtılır: Avustralya Güneydoğu, Doğu ABD, Güneydoğu Asya ve Batı Avrupa.  VM zamanlamasını yöneten runbook'lar herhangi bir bölgedeki VM'leri hedefleyebilir.  

- VM runbook'larının başlatılması ve durdurulması tamamlandığında e-posta bildirimleri gönderilebilmesi için iş sınıfı bir Office 365 aboneliği gereklidir.  

## <a name="solution-components"></a>Çözüm bileşenleri

Bu çözüm, içe aktarılıp Otomasyon hesabınıza eklenecek olan aşağıdaki kaynakları içerir.

### <a name="runbooks"></a>Runbook'lar

Runbook | Açıklama|
--------|------------|
CleanSolution-MS-Mgmt-VM | Bu runbook, çözümü aboneliğinizden silmeye karar verdiğinizde, çözümün içerdiği tüm kaynak ve zamanlamaları kaldırır.|  
SendMailO365-MS-Mgmt | Bu runbook, Office 365 Exchange aracılığıyla e-posta gönderir.|
StartByResourceGroup-MS-Mgmt-VM | Bu runbook, belirli bir Azure kaynak grupları listesinde yer alan VM'leri (klasik ve ARM tabanlı VM'ler) başlatmak üzere tasarlanmıştır.
StopByResourceGroup-MS-Mgmt-VM | Bu runbook, belirli bir Azure kaynak grupları listesinde yer alan VM'leri (klasik ve ARM tabanlı VM'ler) durdurmak üzere tasarlanmıştır.|
<br>

### <a name="variables"></a>Değişkenler

Değişken | Açıklama|
---------|------------|
**SendMailO365-MS-Mgmt** Runbook ||
SendMailO365-IsSendEmail-MS-Mgmt | StartByResourceGroup-MS-Mgmt-VM ve StopByResourceGroup-MS-Mgmt-VM runbook'larının tamamlandıktan sonra bildirim e-postası gönderip gönderemeyeceklerini belirtir.  Etkinleştirmek için **True** ve e-posta uyarılarını devre dışı bırakmak için **False** seçeneğini belirleyin. Varsayılan ayar, **False** değeridir.| 
**StartByResourceGroup-MS-Mgmt-VM** Runbook ||
StartByResourceGroup ExcludeList-MS-Mgmt-VM | Yönetim işleminden hariç tutulacak VM adlarını girin; adları, boşluk olmadan virgül (;) kullanarak ayırın. Değerleri büyük/küçük harfe duyarlıdır ve joker karakter (yıldız işareti) kullanımı desteklenir.|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | E-posta ileti gövdesinin başına eklenebilecek metin.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | E-posta runbook’unu içeren Otomasyon Hesabı’nın adını belirtir.  **Bu değişkeni değiştirmeyin.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | E-posta runbook’unun adını belirtir.  StartByResourceGroup-MS-Mgmt-VM ve StopByResourceGroup-MS-Mgmt-VM runbook'ları tarafından e-posta göndermek amacıyla kullanılır.  **Bu değişkeni değiştirmeyin.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | E-posta runbook’unu içeren Kaynak grubunun adını belirtir.  **Bu değişkeni değiştirmeyin.**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | E-postanın konu satırı metnini belirtir.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | E-postanın alıcılarını belirtir.  Ayrı adları, boşluk olmadan virgül (;) kullanarak girin.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Yönetim işleminden hariç tutulacak VM adlarını girin; adları, boşluk olmadan virgül (;) kullanarak ayırın. Değerleri büyük/küçük harfe duyarlıdır ve joker karakter (yıldız işareti) kullanımı desteklenir.  Varsayılan değer (yıldız işareti) aboneliğe tüm kaynak gruplarını dahil eder.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Çözüm tarafından yönetilecek VM’leri içeren aboneliği belirtir.  Bu abonelik, bu çözümün Otomasyon hesabının bulunduğu aboneliğin aynısı olmalıdır.|
**StopByResourceGroup-MS-Mgmt-VM** Runbook ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Yönetim işleminden hariç tutulacak VM adlarını girin; adları, boşluk olmadan virgül (;) kullanarak ayırın. Değerleri büyük/küçük harfe duyarlıdır ve joker karakter (yıldız işareti) kullanımı desteklenir.|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | E-posta ileti gövdesinin başına eklenebilecek metin.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | E-posta runbook’unu içeren Otomasyon Hesabı’nın adını belirtir.  **Bu değişkeni değiştirmeyin.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | E-posta runbook’unu içeren Kaynak grubunun adını belirtir.  **Bu değişkeni değiştirmeyin.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | E-postanın konu satırı metnini belirtir.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | E-postanın alıcılarını belirtir.  Ayrı adları, boşluk olmadan virgül (;) kullanarak girin.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Yönetim işleminden hariç tutulacak VM adlarını girin; adları, boşluk olmadan virgül (;) kullanarak ayırın. Değerleri büyük/küçük harfe duyarlıdır ve joker karakter (yıldız işareti) kullanımı desteklenir.  Varsayılan değer (yıldız işareti) aboneliğe tüm kaynak gruplarını dahil eder.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Çözüm tarafından yönetilecek VM’leri içeren aboneliği belirtir.  Bu abonelik, bu çözümün Otomasyon hesabının bulunduğu aboneliğin aynısı olmalıdır.|  
<br>

### <a name="schedules"></a>Zamanlamalar

Zamanlama | Açıklama|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | VM’lerin bu çözüm tarafından yönetilen başlatma işlemlerini yürüten StartByResourceGroup runbook’u için zamanlama belirleyin. Oluşturduğunuzda, UTC saat dilimine varsayılan olarak ayarlanır.|
StopByResourceGroup-Schedule-MS-Mgmt | VM’lerin bu çözüm tarafından yönetilen durdurma işlemlerini yürüten StopByResourceGroup runbook’u için zamanlama belirleyin. Oluşturduğunuzda, UTC saat dilimine varsayılan olarak ayarlanır.|

### <a name="credentials"></a>Kimlik Bilgileri

Kimlik Bilgisi | Açıklama|
-----------|------------|
O365Credential | E-posta göndermek için geçerli bir Office 365 kullanıcı hesabı belirtir.  Yalnızca, SendMailO365-IsSendEmail-MS-Mgmt değişkeni **True** olarak ayarlanırsa gereklidir.

## <a name="configuration"></a>Yapılandırma

VM’leri çalışma saatleri dışında Başlatma/Durdurma [Önizleme] çözümünü Otomasyonu hesabınızı ekleyip ardından çözümü özelleştirmek üzere değişkenlerini yapılandırmak için aşağıdaki adımları uygulayın.

1. Azure portalının ana ekranında **Market** kutucuğunu seçin.  Kutucuk ana ekranınızda sabitlenmiş değilse sol gezinti bölmesinden **Yeni**’yi seçin.  
2. Market dikey penceresinde arama kutusuna **VM Başlat** yazın ve arama sonuçlarının arasından **VM’leri çalışma saatleri dışında Başlatma/Durdurma [Önizleme]** çözümünü seçin.  
3. Seçili çözümün **VM’leri çalışma saatleri dışında Başlatma/Durdurma [Önizleme]** dikey penceresinde özet bilgileri gözden geçirin ve **Oluştur**’a tıklayın.  
4. **Çözüm Ekle** dikey penceresi görünür ve çözümü Otomasyon aboneliğinize aktarmadan önce yapılandırmanız istenir.<br><br> ![VM Management Çözüm Ekleme dikey penceresi](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  **Çözüm Ekle** dikey penceresinde, **Çalışma alanı**’nı seçin. Burada, Otomasyon hesabının bulunduğu Azure aboneliğine bağlı olan bir OMS çalışma alanı seçmeniz ya da yeni bir OMS çalışma alanı oluşturmanız gerekir.  OMS çalışma alanınız yoksa **Yeni Çalışma Alanı Oluştur**’u seçip **OMS Çalışma Alanı** dikey penceresinde aşağıdakileri yapabilirsiniz: 
   - Yeni **OMS Çalışma Alanı** için bir ad belirtin.
   - Varsayılan seçili abonelik uygun değilse açılan listeden bağlanacak bir **Abonelik** seçin.
   - **Kaynak Grubu** için, yeni bir kaynak grubu oluşturabilir veya mevcut bir kaynak grubunu seçebilirsiniz.  
   - Bir **Konum** seçin.  Şu anda seçimde kullanılabilecek konumlar **Avustralya Güneydoğu**, **Doğu ABD**, **Güneydoğu Asya** ve **Batı Avrupa**’dır.
   - Bir **Fiyatlandırma katmanı** seçin.  Çözüm iki katmanda sunulur: ücretsiz ve OMS ücretli katmanı.  Ücretsiz katmanında günlük toplanan veri miktarı, elde tutma süresi ve runbook işi çalışma zamanı dakika sayısına ilişkin sınırlar vardır.  OMS ücretli katmanında günlük toplanan veri miktarı için bir sınır yoktur.  

        > [!NOTE]
        > Ücretli katman tek başına bir seçenek olarak görüntülenir, ancak geçerli değildir.  Bu katmanı seçerek aboneliğinizde bu çözümü oluşturmaya çalışırsanız, işlem başarısız olur.  Bu çözüm resmi olarak yayımlandığında, bu sorun da ele alınacaktır.<br>Bu çözümü kullanırsanız, yalnızca otomasyon işi dakikaları ve günlük alımı kullanılır.  Çözüm, ortamınıza ek OMS düğümleri eklemez.  

6. **OMS çalışma alanı** dikey penceresinde gerekli bilgileri girdikten sonra **Oluştur**’a tıklayın.  Bilgilerin doğrulanıp çalışma alanının oluşturulması sırasında işlemin ilerleme durumunu menüdeki **Bildirimler**’in altından izleyebilirsiniz.  **Çözüm Ekle** dikey penceresine döndürülürsünüz.  
7. **Çözüm Ekle** dikey penceresinde **Otomasyon Hesabı**’nı seçin.  Yeni bir OMS çalışma alanı oluşturuyorsanız Azure aboneliğiniz, kaynak grubunuz ve bölgeniz dahil olmak üzere belirtilen yeni OMS çalışma alanı ile ilişkilendirilecek olan yeni bir Otomasyon hesabı da oluşturmanız gerekir.  **Otomasyon hesabı oluştur**’u seçerek, **Otomasyon hesabı ekle** dikey penceresinde aşağıdakileri girebilirsiniz: 
  - **Ad** alanına Otomasyon hesabının adını girin.

    Tüm diğer seçenekler, seçili OMS çalışma alanına dayalı olarak otomatik doldurulur ve bu seçenekler değiştirilemez.  Bu çözüme dahil olan runbook'lar için varsayılan kimlik doğrulama yöntemi, bir Azure Farklı Çalıştır hesabıdır.  **Tamam**’a tıkladığınızda yapılandırma seçenekleri doğrulanır ve Otomasyon hesabı oluşturulur.  Bu işlemin ilerleme durumunu menüdeki **Bildirimler**’in altından izleyebilirsiniz. 

    Aksi takdirde, mevcut bir Otomasyon Farklı Çalıştır hesabını seçebilirsiniz.  Seçtiğiniz hesap önceden başka bir OMS çalışma alanına bağlı olamaz, böyle olması durumunda dikey pencerede bunu belirten bir ileti görürsünüz.  Önceden bağlıysa, farklı bir Otomasyon Farklı Çalıştır hesabı seçmeniz veya yeni bir hesap oluşturmanız gerekir.<br><br> ![Otomasyon Hesabı Önceden OMS Çalışma Alanına Bağlı](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Son olarak, **Çözüm Ekle** dikey penceresinde **Yapılandırma**’yı seçin. Böylece **Parametreler** dikey penceresi görüntülenir.  **Parametreler** dikey penceresinde aşağıdakileri yapmanız istenir:  
   - Bu çözüm tarafından yönetilecek VM’leri içeren bir kaynak grubu adı olan **Hedef ResourceGroup Adları**’nı belirtin.  Her birini noktalı virgül ile ayırarak birden fazla ad girebilirsiniz (Değerler büyük küçük harfe duyarlıdır.)  Abonelikte yer alan tüm kaynak gruplarındaki sanal makineleri hedeflemek istiyorsanız, joker karakter kullanılması desteklenir.
   - Hedef kaynak gruplarındaki VM’lerin başlatılmasına ve durdurulmasına ilişkin yinelenen bir tarih ve saat olan bir **Zamanlama** seçin.  Varsayılan olarak, zamanlama için UTC saat dilimi yapılandırılır ve başka bir bölge seçmeyi kullanılabilir değil.  Çözüm yapılandırdıktan sonra belirli saat diliminiz için zamanlama yapılandırmak istiyorsanız bkz [başlatma ve kapatma zamanlamasını değiştirme](#modifying-the-startup-and-shutdown-schedule) aşağıda.    

10. Çözüm için gereken ilk ayarların yapılandırılmasını tamamlandığınızda **Oluştur**’u seçin.  Tüm ayarlar doğrulanır ve çözümün aboneliğinize dağıtılması denenir.  Bu işlemin tamamlanması birkaç saniye alabilir ve ilerleme durumunu menüdeki **Bildirimler**’in altından izleyebilirsiniz. 

## <a name="collection-frequency"></a>Toplama sıklığı

Otomasyon iş günlüğü ve iş akışı verileri her beş dakikada bir OMS deposuna alınır.  

## <a name="using-the-solution"></a>Çözümü kullanma

VM Management çözümünü OMS çalışma alanınıza eklediğinizde, OMS panonuza **StartStopVM Görünümü** kutucuğu eklenir.  Bu kutucuk, çözüme ait başlatılmış ve başarıyla tamamlanmış runbook işlerinin sayısını ve grafik temsilini görüntüler.<br><br> ![VM Management StartStopVM Görünümü Kutucuğu](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

Otomasyon hesabınızda **Çözümler** kutucuğunu seçip **Çözümler** dikey penceresindeki listeden çözüme ait **Başlat-Durdur-VM[Çalışma Alanı]** seçeneğini belirleyerek çözüme erişebilir ve çözümü yönetebilirsiniz.<br><br> ![Otomasyon Çözümleri Listesi](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Çözümün seçilmesi, **Başlat-Durdur-VM[Çalışma Alanı]** çözüm dikey penceresini görüntüler. Bu pencerede, OMS çalışma alanınızda olduğu gibi çözüme ait başlatılmış ve başarıyla tamamlanmış runbook işlerinin sayısını ve grafik temsilini görüntüleyen **StartStopVM** kutucuğu benzeri önemli ayrıntıları gözden geçirebilirsiniz.<br><br> ![Otomasyon VM Çözümü Dikey Penceresi](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

Burada kendi OMS çalışma alanınızı açabilir ve iş kayıtlarıyla ilgili başka analizler alabilirsiniz.  **Tüm ayarlar**’a tıklamanız ve **Ayarlar** dikey penceresinde **Hızlı Başlangıç**’ı ve **Hızlı Başlangıç** dikey penceresinde **OMS Portalı**’nı seçmeniz yeterlidir.   Böylece, yeni bir sekme veya yeni tarayıcı oturumu açılacak ve Otomasyon hesabınız ile aboneliğinize ilişkin OMS çalışma alanınız sunulacaktır.  


### <a name="configuring-e-mail-notifications"></a>E-posta bildirimlerini yapılandırma

VM runbook'larının başlatılması ve durdurulması tamamlandığında e-posta bildirimlerini etkinleştirmek için, **O365Credential** kimlik bilgisini ve en azından aşağıdaki değişkenleri değiştirmeniz gerekir:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

**O365Credential** kimlik bilgisini yapılandırmak için aşağıdaki adımları uygulayın:

1. Otomasyon hesabınızda, pencerenin en üst kısmında **Tüm Ayarlar**’a tıklayın. 
2. **Ayarlar** dikey penceresindeki **Otomasyon Kaynakları** bölümünün altında **Varlıklar**’ı seçin. 
3. **Varlıklar** dikey penceresinde **Kimlik Bilgisi** kutucuğunu seçin ve **Kimlik Bilgisi** dikey penceresinde **O365Credential**’ı seçin.  
4. Geçerli bir Office 365 kullanıcı adı ve parolası girip **Kaydet**’e tıklayarak yaptığınız değişiklikleri kaydedin.  

Daha önce vurgulanan değişkenleri yapılandırmak için aşağıdaki adımları gerçekleştirin:

1. Otomasyon hesabınızda, pencerenin en üst kısmında **Tüm Ayarlar**’a tıklayın. 
2. **Ayarlar** dikey penceresindeki **Otomasyon Kaynakları** bölümünün altında **Varlıklar**’ı seçin. 
3. **Varlıklar** dikey penceresinde **Değişkenler** kutucuğunu seçin ve **Değişkenler** dikey penceresinde yukarıda listelenen değişkenleri seçip yukarıdaki [değişken](##variables) bölümünde sağlanan tanımlar uyarınca bunların değerlerini değiştirin.  
4. Değişkene yapılan değişiklikleri kaydetmek için **Kaydet**’e tıklayın.   

### <a name="modifying-the-startup-and-shutdown-schedule"></a>Başlatma ve kapatma zamanlamasını değiştirme

Bu çözümde başlatma ve kapatma zamanlamasının yönetimi için [Azure Otomasyonu’nda runbook zamanlama](automation-schedules.md) bölümünde açıklanan adımlar uygulanır.  Zamanlama yapılandırmasını değiştiremeyeceğinizi unutmayın.  Mevcut zamanlamayı devre dışı bırakmanız ve yeni bir zamanlama oluşturup bu zamanlama için geçerli olmasını istediğiniz **StartByResourceGroup-MS-Mgmt-VM** veya **StopByResourceGroup-MS-Mgmt-VM** runbook’una bağlamanız gerekir.   

## <a name="log-analytics-records"></a>Log Analytics kayıtları

Otomasyon, OMS deposunda iki tür kayıt oluşturur.

### <a name="job-logs"></a>İş günlükleri

Özellik | Açıklama|
----------|----------|
Çağıran |  İşlemi başlatandır.  Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir.|
Kategori | Veri türü sınıflandırması.  Otomasyon için değer JobLogs olacaktır.|
CorrelationId | Runbook işinin Bağıntı Kimliği olan GUID.|
JobId | Runbook işinin Kimliği olan GUID.|
operationName | Azure’da gerçekleştirilen işlem türünü belirtir.  Otomasyon için değer İş olacaktır.|
resourceId | Azure’daki kaynak türünü belirtir.  Otomasyon için değer, runbook ile ilişkilendirilmiş Otomasyon hesabı olacaktır.|
ResourceGroup | Runbook işine ait kaynak grubunun adını belirtir.|
ResourceProvider | Dağıtıp yönetebileceğiniz kaynakları sağlayan Azure hizmetini belirtir.  Otomasyon için değer, Azure Otomasyonu olacaktır.|
ResourceType | Azure’daki kaynak türünü belirtir.  Otomasyon için değer, runbook ile ilişkilendirilmiş Otomasyon hesabı olacaktır.|
resultType | Runbook işinin durumudur.  Olası değerler şunlardır:<br>- Başlatıldı<br>- Durduruldu<br>- Askıya alındı<br>- Başarısız oldu<br>- Başarılı oldu|
resultDescription | Runbook iş sonucu durumunu açıklar.  Olası değerler şunlardır:<br>- İş başlatıldı<br>- İş Başarısız Oldu<br>- İş Tamamlandı|
RunbookName | Runbook’un adını belirtir.|
SourceSystem | Gönderilen verilere ilişkin kaynak sistemi belirtir.  Otomasyon için değer, :OpsManager olacaktır|
StreamType | Olay türünü belirtir. Olası değerler şunlardır:<br>- Ayrıntılı<br>- Çıktı<br>- Hata<br>- Uyarı|
SubscriptionId | İşin abonelik kimliğini belirtir.
Zaman | Runbook işinin yürütüldüğü tarih ve saat.|


### <a name="job-streams"></a>İş akışları

Özellik | Açıklama|
----------|----------|
Çağıran |  İşlemi başlatandır.  Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir.|
Kategori | Veri türü sınıflandırması.  Otomasyon için değer JobStreams olacaktır.|
JobId | Runbook işinin Kimliği olan GUID.|
operationName | Azure’da gerçekleştirilen işlem türünü belirtir.  Otomasyon için değer İş olacaktır.|
ResourceGroup | Runbook işine ait kaynak grubunun adını belirtir.|
resourceId | Azure’daki kaynak kimliğini belirtir.  Otomasyon için değer, runbook ile ilişkilendirilmiş Otomasyon hesabı olacaktır.|
ResourceProvider | Dağıtıp yönetebileceğiniz kaynakları sağlayan Azure hizmetini belirtir.  Otomasyon için değer, Azure Otomasyonu olacaktır.|
ResourceType | Azure’daki kaynak türünü belirtir.  Otomasyon için değer, runbook ile ilişkilendirilmiş Otomasyon hesabı olacaktır.|
resultType | Runbook işinin, olayın oluşturulduğu andaki sonucu.  Olası değerler şunlardır:<br>- Devam Ediyor|
resultDescription | Runbook’un çıktı akışını içerir.|
RunbookName | Runbook’un adı.|
SourceSystem | Gönderilen verilere ilişkin kaynak sistemi belirtir.  Otomasyon için değer, OpsManager olacaktır|
StreamType | İş akışı türü. Olası değerler şunlardır:<br>- İlerleme durumu<br>- Çıktı<br>- Uyarı<br>- Hata<br>- Hata ayıklama<br>- Ayrıntılı|
Zaman | Runbook işinin yürütüldüğü tarih ve saat.|

**JobLogs** veya **JobStreams** kategorisinde kayıtlar döndüren bir günlük araması yaptığınızda, arama tarafından döndürülen güncelleştirmeleri özetleyen bir grup kutucuk görüntüleyen **JobLogs** veya **JobStreams** görünümlerini seçebilirsiniz.

## <a name="sample-log-searches"></a>Örnek günlük aramaları

Aşağıdaki tabloda, bu çözüm tarafından toplanan iş kayıtlarına ilişkin örnek günlük aramaları sunulmaktadır. 

Sorgu | Açıklama|
----------|----------|
StartVM runbook’una ilişkin başarıyla tamamlanmış işleri bul | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
StopVM runbook’una ilişkin başarıyla tamamlanmış işleri bul | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
StartVM ve StopVM runbook'ları için zaman içerisinde iş durumunu göster | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-the-solution"></a>Çözüm kaldırma

Artık daha fazla çözüm herhangi kullanmanıza gerek karar verirseniz, Otomasyon hesabı silebilirsiniz.  Çözüm silme runbook'ları yalnızca kaldırır, zamanlamaları veya çözümü eklediğinizde, oluşturulan değişkenleri silmez.  Bu varlıkları, bunları ile diğer runbook'ları kullanmıyorsanız el ile silmeniz gerekir.  

Çözümü silmek için aşağıdaki adımları gerçekleştirin:

1.  Otomasyon hesabınızdan seçin **çözümleri** döşeme.  
2.  Üzerinde **çözümleri** dikey penceresinde, çözümü seçin **Start-Stop-VM [çalışma]**.  Üzerinde **VMManagementSolution [çalışma]** dikey penceresinde, menü öğesini **silmek**.<br><br> ![VM yönetimi çözümü Sil](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  İçinde **silmek çözüm** penceresinde çözümü silmek istediğinizi onaylamak.
4.  Bilgi doğrulanır ve çözüm silinmiş olsa da, altında ilerleme durumunu izleyebilirsiniz **bildirimleri** menüsünde.  İçin döndürülecek **VMManagementSolution [çalışma]** Çözüm kaldırma işlemini başladıktan sonra dikey.  

Bu işlemin bir parçası olarak, OMS çalışma ve Automation hesabı silinmez.  OMS çalışma korumak istemiyorsanız, el ile silmeniz gerekir.  Bu, Azure portalından da gerçekleştirilebilir.   Giriş-ekranından Azure portalında, seçin **günlük analizi** ve daha sonra **günlük analizi** dikey penceresinde, çalışma alanını seçin ve tıklatın **silmek** menüsünden çalışma ayarları dikey penceresi.  
      
## <a name="next-steps"></a>Sonraki adımlar

- Farklı arama sorguları oluşturma ve Log Analytics ile Otomasyon iş günlüklerini gözden geçirme hakkında daha fazla bilgi edinmek için bkz. [Log Analytics’te günlük aramaları](../log-analytics/log-analytics-log-searches.md)
- Runbook yürütme, runbook işlerini izleme ve diğer teknik ayrıntılar hakkında daha fazla bilgi edinmek için bkz. [Runbook işi izleme](automation-runbook-execution.md)
- OMS Log Analytics ve veri toplama kaynakları hakkında daha fazla bilgi edinmek için bkz. [Log Analytics’te Azure depolama verileri toplamaya genel bakış](../log-analytics/log-analytics-azure-storage.md)






   

