---
title: "Azure Data factory'de veri yönetimi ağ geçidi ile aaaHigh kullanılabilirliğini | Microsoft Docs"
description: "Bu makalede daha fazla düğüm ve ölçek ekleyerek veri yönetimi ağ geçidi nasıl ölçeklendirebilirsiniz açıklanmaktadır yukarı bir düğümde çalıştırılabilen eşzamanlı iş sayısını artırarak."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>Veri Yönetimi ağ geçidi - yüksek kullanılabilirlik ve ölçeklenebilirlik (Önizleme)
Bu makalede veri yönetimi ağ geçidi ile yüksek kullanılabilirlik ve ölçeklenebilirlik çözümü yapılandırmanıza yardımcı olur.    

> [!NOTE]
> Bu makale, veri yönetimi ağ geçidi temelleri ile bilginiz olduğunu varsayar. Emin değilseniz, bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).

>**Bu önizleme özelliği resmi olarak veri yönetimi ağ geçidi sürümü 2.12.xxxx.x ve üzeri sürümlerde desteklenen**. Lütfen sürüm 2.12.xxxx.x kullandığınızdan emin olun veya üstü. Veri Yönetimi ağ geçidi Hello en son sürümünü indirme [burada](https://www.microsoft.com/download/details.aspx?id=39717).

## <a name="overview"></a>Genel Bakış
Tek bir mantıksal ağ geçidi hello portalından sahip birden çok şirket içi makinelerde yüklü veri yönetimi ağ geçidi ilişkilendirebilirsiniz. Bu makineler adlı **düğümleri**. Çok bulunabilir**dört düğüm** mantıksal bir ağ geçidi ile ilişkilendirilmiş. mantıksal bir ağ geçidi için birden çok düğüm (yüklü ağ geçidi ile şirket içi makineler) sahip hello avantajları şunlardır:  

- Şirket içi ve bulut arasında veri taşıma performansını verileri depolar.  
- Herhangi bir nedenden dolayı hello düğümlerinden biri arıza yaparsa, diğer düğümler hello veri taşımak için hala kullanılabilmektedir. 
- Merhaba düğümlerinden biri bakım için çevrimdışına toobe ihtiyacınız varsa, diğer düğümlere hello veri taşımak için hala kullanılabilmektedir.

Merhaba sayısı da yapılandırabilirsiniz **eş zamanlı veri taşıma işleri** düğümü tooscale şirket içi ve bulut arasında veri taşıma hello yetenek yukarı üzerinde çalışabilir veri depolarına. 

Hello Azure portal kullanarak, hello karar vermenize yardımcı olan bu düğümler durumunu izleyebilirsiniz olup olmadığını tooadd veya bir düğüm hello mantıksal ağ geçidi'nden kaldırın. 

## <a name="architecture"></a>Mimari 
Merhaba Aşağıdaki diyagramda hello mimarisine genel bakış ölçeklenebilirlik ve kullanılabilirlik özelliğini hello veri yönetimi ağ geçidi sağlar: 

![Veri Yönetimi ağ geçidi - yüksek kullanılabilirlik ve ölçeklenebilirlik](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

A **mantıksal ağ geçidi** hello ağ geçidi hello Azure portal tooa veri fabrikası ekleyin. Daha önce veri yönetimi ağ geçidi mantıksal bir ağ geçidi ile yüklü olan yalnızca bir şirket içi Windows makine ilişkilendirme. Bu ağ geçidi makinesi bir düğüm olarak adlandırılan şirket içi. Şimdi, Yukarı çok ilişkilendirebilirsiniz**dört fiziksel düğüm** mantıksal bir ağ geçidi ile. Mantıksal bir ağ geçidi birden çok düğüm ile adlı bir **çok düğümlü ağ geçidi**.  

Bu düğümler **etkin**. Tüm şirket içi ve bulut arasında veri taşıma işleri toomove veri işleyebilir verileri depolar. Merhaba düğümlerinden biri dağıtıcısı ve çalışan davranır. Diğer düğümlere hello gruplar halinde çalışan düğümleri ' dir. A **dağıtıcısı** düğümü veri taşıma görevleri/işleri hello bulut hizmetinden çeker ve tooworker düğümleri (kendisi dahil) gönderir. A **çalışan** düğümü yürütür şirket içi ve bulut arasında veri taşıma işleri toomove verileri veri depoları. Tüm düğümleri çalışanlardır. Yalnızca bir düğüm, gönderme ve çalışan olabilir.    

Tek bir düğüm genellikle başlayabilir ve **ölçeğini** varolan düğümlerini hello gibi daha fazla düğüm hello veri taşıma yük ile çok tooadd. Ayrıca **ölçeği** hello veri taşıma özelliği bir ağ geçidi düğümünün hello toorun hello düğümünde izin verilen eşzamanlı iş sayısını artırarak. Bu özellik, tek bir düğüm ile ağ geçidi (Merhaba ölçeklenebilirlik ve kullanılabilirlik özelliği etkin değilse bile) de kullanılabilir. 

Bir ağ geçidi birden çok düğüm ile Merhaba veri deposu kimlik tüm düğümlere eşitlenmiş tutar. Bir düğümden düğüme bağlantı sorunu varsa, hello kimlik eşitlenmemiş olabilir. Bir ağ geçidi kullanan bir şirket içi veri deposu için kimlik bilgilerini ayarladığınızda, hello dağıtıcısı/çalışan düğümünde kimlik bilgileri kaydeder. Merhaba dağıtıcısı düğümü eşitlemeler diğer alt düğümü. Bu işlem olarak bilinir **kimlik eşitleme**. düğümler arasındaki iletişim kanalını hello olabilir **şifrelenmiş** ortak SSL/TLS sertifikası tarafından. 

## <a name="set-up-a-multi-node-gateway"></a>Bir çok düğümlü ağ geçidi kurun
Bu bölümde, iki makaleler veya bu makalelerde açıklanan kavramlar bilmiyorsanız aşağıdaki hello aracılığıyla ilerlemiş varsayılır: 

- [Veri Yönetimi ağ geçidi](data-factory-data-management-gateway.md) -hello ağ geçidi ayrıntılı bir genel bakış sağlar.
- [Şirket içi ve bulut arasında veri taşıma veri depolarına](data-factory-move-data-between-onprem-and-cloud.md) -bir ağ geçidi ile tek bir düğüm kullanmak için adım adım yönergeleri içeren bir kılavuz içerir.  

> [!NOTE]
> Bir şirket içi Windows makinesinde veri yönetimi ağ geçidi'ni yüklemeden önce listelenen önkoşullara bakın [hello Ana Makalesi](data-factory-data-management-gateway.md#prerequisites).

1. Merhaba, [izlenecek](data-factory-move-data-between-onprem-and-cloud.md#create-gateway), mantıksal bir ağ geçidi oluştururken, hello etkinleştirmek **yüksek kullanılabilirlik ve ölçeklenebilirlik** özelliği. 

    ![Veri Yönetimi ağ geçidi - enable yüksek kullanılabilirlik ve ölçeklenebilirlik](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. Merhaba, **yapılandırma** sayfasında, kullanın ya da **Express Kurulum** veya **el ile Kurulum** tooinstall hello ilk düğümü (şirket içi Windows makine) üzerinde bir ağ geçidi bağlantı.

    ![Veri Yönetimi ağ geçidi - hızlı veya el ile Kurulum](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > Merhaba hızlı kurulum seçeneğini kullanırsanız, başlangıç düğümü, düğümü iletişimi şifreleme olmadan yapılır. Merhaba düğüm adı hello makine adıyla aynıdır. El ile kuruluma hello düğümler iletişiminin şifrelenmiş toobe veya toospecify tercih ettiğiniz bir düğüm adı istiyorsanız kullanın. Düğüm adı daha sonra düzenlenemez.
3. Seçerseniz **hızlı kurulumu**
    1. Merhaba ağ geçidi başarıyla yüklendikten sonra iletiden hello bakın:

        ![Veri Yönetimi ağ geçidi - hızlı Kurulumu başarılı](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. İzleyerek hello ağ geçidi için veri yönetimi Yapılandırma Yöneticisi başlatma [bu yönergeleri](data-factory-data-management-gateway.md#configuration-manager). Gördüğünüz hello ağ geçidi adı, düğüm adı, durum, vs.

        ![Veri Yönetimi ağ geçidi - yükleme başarılı](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. Seçerseniz **el ile kuruluma**:
    1. Merhaba Microsoft Download Center, yükleme hello yükleme paketini çalıştırın tooinstall ağ geçidi makinenizde.
    2. Kullanım hello **kimlik doğrulama anahtarı** hello gelen **yapılandırma** sayfa tooregister hello ağ geçidi.
    
        ![Veri Yönetimi ağ geçidi - yükleme başarılı](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. Merhaba, **yeni ağ geçidi düğümü** sayfasında, özel bir sağlayabilir **adı** toohello ağ geçidi düğümü. Varsayılan olarak, düğüm adı hello makine adıyla aynı.    

        ![Veri Yönetimi ağ geçidi - adını belirtin](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. Merhaba sonraki sayfada, çok olup olmadığını seçebilirsiniz**düğümü düğümü iletişimi için şifrelemeyi etkinleştirmeniz**. Tıklatın **atla** toodisable şifreleme (varsayılan).

        ![Veri Yönetimi ağ geçidi - enable şifreleme](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > Şifreleme modunu değiştirme, yalnızca bir tek ağ geçidi düğümü hello mantıksal ağ geçidi olduğunda desteklenir. bir ağ geçidi birden fazla düğüme sahip olduğunda toochange hello şifreleme modu adımları izleyerek hello: bir düğüm dışındaki tüm hello düğümleri silerseniz, hello şifreleme modunu değiştirme ve hello düğümleri tekrar ekleyin.
        > 
        > Bkz: [TLS/SSL sertifika gereksinimlerini](#tlsssl-certificate-requirements) bir TLS/SSL sertifikası kullanmak için gereksinimleri listesi bölümü. 
    5. Merhaba ağ geçidi başarıyla yüklendikten sonra başlatma Configuration Manager'ı tıklatın:
    
        ![El ile kuruluma - başlatma Yapılandırma Yöneticisi](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi bağlantısı durumunu gösteren hello düğümde (şirket içi Windows makine), bkz. **ağ geçidi adı**, ve **düğüm adı**.  

        ![Veri Yönetimi ağ geçidi - yükleme başarılı](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > Bir Azure VM ağ geçidinde hello sağlıyorsanız, kullanabileceğiniz [github'daki bu Azure Resource Manager şablonu](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway). Bu komut, mantıksal bir ağ geçidi oluşturur, veri yönetimi ağ geçidi yazılımı yüklü Vm'leri ayarlar ve hello mantıksal ağ geçidi ile kaydeder. 
6. Azure portalında hello başlatma **ağ geçidi** sayfa: 
    1. Merhaba portalında Hello data factory giriş sayfası üzerinde tıklatın **bağlı hizmetler**.
    
        ![Data factory giriş sayfası](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. Merhaba seçin **ağ geçidi** toosee hello **ağ geçidi** sayfa:
    
        ![Data factory giriş sayfası](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. Merhaba gördüğünüz **ağ geçidi** sayfa:   

        ![Tek düğüm görünümü ile ağ geçidi](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. Tıklatın **düğüm Ekle** hello araç tooadd düğümü toohello mantıksal bir ağ geçidi üzerinde. Toouse hızlı kurulum planlıyorsanız, bu adımı bir düğüm toohello ağ geçidi olarak eklenecek hello şirket içi makineden yapın. 

    ![Veri Yönetimi ağ geçidi - düğüm menü ekleme](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. Merhaba ilk düğümü yukarı benzer toosetting adımlardır. Merhaba Yapılandırma Yöneticisi kullanıcı Arabirimi, hello el ile yüklemesi seçeneğini belirlerseniz hello düğüm adı ayarlamanızı sağlar: 

    ![Configuration Manager - yükleme ikinci ağ geçidi](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Merhaba ağ geçidi hello düğümde başarıyla yüklendikten sonra hello Yapılandırma Yöneticisi Aracı ekran aşağıdaki hello görüntüler:  

    ![Configuration Manager - yükleme ikinci ağ geçidi başarılı](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. Merhaba açarsanız **ağ geçidi** sayfa hello Portalı'nda, iki ağ geçidi düğümleri şimdi görürsünüz: 

    ![Ağ geçidi hello portalında iki düğümü](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. toodelete bir ağ geçidi düğümü tıklatın **silmek düğümü** hello araç çubuğunda toodelete istediğiniz ve ardından hello düğümü seçin **silmek** hello araç çubuğundan. Bu eylemin hello Seçili düğümün hello grubundan siler. Bu eylemin hello düğümden (şirket içi Windows makine) hello veri yönetimi ağ geçidi yazılımının kaldırmaz unutmayın. Kullanım **Program Ekle veya Kaldır'ı** hello şirket içi toouninstall hello ağ geçidi üzerinde Denetim Masası'nda. Ağ geçidi hello düğümden kaldırdığınızda, hello Portalı'nda otomatik olarak silinir.   

## <a name="upgrade-an-existing-gateway"></a>Mevcut bir ağ geçidi yükseltme
Varolan ağ geçidi toouse hello yüksek kullanılabilirlik ve ölçeklenebilirlik özelliği yükseltebilirsiniz. Bu özellik hello veri yönetimi ağ geçidi sürümü olan düğümler ile çalışır > 2.12.xxxx =. Veri Yönetimi ağ geçidi hello bir makinede yüklü hello sürümünü görebilirsiniz **yardımcı** hello veri yönetimi ağ geçidi Yapılandırma Yöneticisi sekmesinde. 

1. Güncelleştirme hello ağ geçidi izleyerek hello şirket içi makineyi toohello en son sürümünü indirip hello bir MSI kurulum paketi çalıştıran [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717). Bkz: [yükleme](data-factory-data-management-gateway.md#installation) ayrıntıları bölümü.  
2. Toohello Azure portalına gidin. Merhaba başlatma **Data Factory sayfasını** veri fabrikanızın. Bağlı hizmetler döşeme toolaunch hello tıklatın **bağlantılı Hizmetler Sayfası**. Select hello ağ geçidi toolaunch hello **ağ geçidi sayfa**. ' I tıklatın ve etkinleştirme **önizleme özelliği** hello görüntü aşağıdaki gösterildiği gibi: 

    ![Veri Yönetimi ağ geçidi - önizleme özelliğini etkinleştir](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. Merhaba önizleme özelliği hello Portalı'nda etkinleştirildikten sonra tüm sayfaları kapatın. Merhaba yeniden **ağ geçidi sayfa** toosee hello yeni önizleme kullanıcı arabirimi (UI).
 
    ![Veri Yönetimi ağ geçidi - enable önizleme özelliği başarılı](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![Veri Yönetimi ağ geçidi - UI Önizleme](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Merhaba yükseltme sırasında hello ilk düğümün adı hello hello makinenin adıdır. 
3. Şimdi, bir düğüm ekleyin. Merhaba, **ağ geçidi** sayfasında, **düğüm Ekle**.  

    ![Veri Yönetimi ağ geçidi - düğüm menü ekleme](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    Merhaba önceki bölümde tooset hello düğümü yukarı gelen yönergeleri izleyin. 

### <a name="installation-best-practices"></a>Yükleme için en iyi yöntemler

- Böylece Hello makine değil hazırda bekleme güç planı hello konak hello ağ geçidi için yapılandırın. Merhaba ana makine hazırda bekleme durumunda hello ağ geçidi toodata istekleri yanıt vermez.
- Merhaba ağ geçidiyle ilişkili hello sertifikayı yedekleyin.
- Tüm düğümler (ideal performans için önerilen) benzer yapılandırmasının emin olun. 
- En az iki düğüme tooensure yüksek kullanılabilirlik ekleyin.  

### <a name="tlsssl-certificate-requirements"></a>TLS/SSL sertifika gereksinimleri
Ağ geçidi düğümleri arasındaki iletişimi korumak için kullanılan hello TLS/SSL sertifikası hello gereksinimleri şunlardır:

- Merhaba sertifika, genel olarak güvenilir X509 olmalıdır v3 sertifikası.
- Tüm ağ geçidi düğümleri bu sertifikaya güvenmeleri gerekir. 
- Ortak (üçüncü taraf) sertifika yetkilisi (CA) tarafından verilen sertifikaların kullanmanızı öneririz.
- SSL sertifikaları için Windows Server 2012 R2 tarafından desteklenen herhangi bir anahtar boyutunu destekler.
- CNG anahtarları kullanan sertifikaları desteklemez.
- Joker karakteriyle sertifikalar desteklenir. 


## <a name="monitor-a-multi-node-gateway"></a>İzleyici bir çok düğümlü ağ geçidi
### <a name="multi-node-gateway-monitoring"></a>Birden çok düğümlü ağ geçidi izleme
Hello Azure portal'da, ağ geçidi düğümleri durumları yanı sıra her bir düğümde neredeyse gerçek zamanlı anlık görüntüsünü kaynak kullanımı (CPU, bellek, network(in/out), vb.) görüntüleyebilirsiniz. 

![Veri Yönetimi ağ geçidi - birden çok düğüm izleme](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

Etkinleştirebilirsiniz **Gelişmiş ayarları** hello içinde **ağ geçidi** sayfasında ölçümleri gibi gelişmiş toosee **ağ**(in/out), **rol & kimlik bilgisi durum**, ağ geçidi sorunları, hata ayıklamaya yardımcı olduğu ve **eşzamanlı iş** (çalışan / sınırlamak) hangi olması değiştirilmiş / sırasında buna göre değişen performans ayarlama. Merhaba aşağıdaki tabloda verilmiştir hello sütunlarında açıklamalarını **ağ geçidi düğümleri** listesi:  

İzleme özelliği | Açıklama
:------------------ | :---------- 
Ad | Merhaba mantıksal ağ geçidi ve hello ağ geçidiyle ilişkilendirilen düğüm adı.  
Durum | Merhaba mantıksal ağ geçidi ve hello ağ geçidi düğümleri durumu. Örnek: Çevrimiçi/çevrimdışı/sınırlı/vs. Bu durumlar hakkında daha fazla bilgi için bkz: [ağ geçidi durumu](#gateway-status) bölümü. 
Sürüm | Merhaba mantıksal ağ geçidi Hello sürümü ve her ağ geçidi düğümü gösterir. Hello hello mantıksal ağ geçidi sürümü hello grubu düğüm çoğunluğu sürümüne göre belirlenir. Farklı sürümlerde hello mantıksal ağ geçidi ile düğüm varsa, yalnızca hello düğümleriyle aynı sürüm numarasına hello mantıksal ağ geçidi işlevi düzgün şekilde hello. Başkalarının hello sınırlı modda ve (yalnızca otomatik güncelleştirmeler başarısız olursa) el ile güncelleştirilmiş toobe gerekir. 
Kullanılabilir bellek | Bir ağ geçidi düğümü kullanılabilir bellek. Bu değer yakın gerçek zamanlı anlık görüntüsüdür. 
CPU kullanımı | Bir ağ geçidi düğümünün CPU kullanımı. Bu değer yakın gerçek zamanlı anlık görüntüsüdür. 
Ağ (çıkış) | Bir ağ geçidi düğümünün ağ kullanımı. Bu değer yakın gerçek zamanlı anlık görüntüsüdür. 
(Çalışan / sınırlamak) eşzamanlı işleri | İşlerini veya her bir düğümde çalışan görevlerin sayısıdır. Bu değer yakın gerçek zamanlı anlık görüntüsüdür. Her düğüm için en fazla eşzamanlı iş hello sınırı belirtir. Bu değer hello makine boyutuna göre tanımlanır. Gelişmiş senaryolarda eşzamanlı iş yürütme yukarı hello sınırı tooscale artırabilirsiniz burada CPU / bellek / ağ altında kullanılan ancak etkinlik zaman aşımı. Bu özellik, tek bir düğüm ile ağ geçidi (Merhaba ölçeklenebilirlik ve kullanılabilirlik özelliği etkin değilse bile) de kullanılabilir. Daha fazla bilgi için bkz: [ölçeklendirme konuları](#scale-considerations) bölümü. 
Rol | Dağıtıcı ve çalışan rolleri – iki tür vardır. Tüm düğümleri, yani tüm kullanılan tooexecute işleri olabilirler çalışanlardır. Kullanılan toopull görevler/işleri bulut hizmetlerinden ve toodifferent çalışan düğümleri (kendisi dahil) gönderme yalnızca bir dağıtıcı düğüm yok. 

![Veri Yönetimi ağ geçidi - Gelişmiş birden çok düğüm izleme](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>Ağ geçidi durumu

Merhaba aşağıdaki tabloda sağlar, olası durumlar bir **ağ geçidi düğümü**: 

Durum  | Yorumlar/senaryoları
:------- | :------------------
Çevrimiçi | Düğüm tooData Fabrika hizmete bağlı.
Çevrimdışı | Çevrimdışı düğümdür.
Yükseltme | Merhaba düğümü otomatik olarak güncelleştirilir.
Sınırlı | TooConnectivity sorunu nedeniyle. TooHTTP bağlantı noktası 8050 sorunu, hizmet veri yolu bağlantı sorunu veya kimlik bilgisi eşitleme sorunu olabilir. 
Etkin olmayan | Diğer Çoğunluk düğüm hello yapılandırmasından farklı bir yapılandırmada düğümdür.<br/><br/> Tooother düğümleri bağlanamadığında bir düğüm etkin olabilir. 


Merhaba aşağıdaki tabloda sağlar, olası durumlar bir **mantıksal ağ geçidi**. Merhaba ağ geçidi durumu hello ağ geçidi düğümleri durumları üzerinde bağlıdır. 

Durum | Yorumlar
:----- | :-------
Kaydedilmesi gerekiyor | Hiçbir düğümü henüz kayıtlı toothis mantıksal ağ geçididir
Çevrimiçi | Ağ geçidi düğümleri çevrimiçi
Çevrimdışı | Çevrimiçi durumu düğümü yok.
Sınırlı | Bu ağ geçidi tüm düğümler sağlıklı durumda. Bu durum bazı düğümü kapalı olabilir bir uyarıdır! <br/><br/>Dağıtıcı/çalışan düğümünde toocredential eşitleme sorunu nedeniyle olabilir. 

### <a name="pipeline-activities-monitoring"></a>Ardışık Düzen / etkinliklerini izleme
Hello Azure portal izleme deneyimine ayrıntılı düğümü düzey ayrıntılara sahip bir işlem hattı sağlar. Örneğin, hangi etkinlikler hangi düğümde çalışan gösterir. Bu bilgiler performans sorunları toonetwork azaltma nedeniyle deyin belirli bir düğümde anlamak yararlı olabilir. 

![Veri Yönetimi ağ geçidi - birden çok düğüm işlem hatlarını izleme](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![Veri Yönetimi ağ geçidi - ardışık düzen ayrıntıları](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>Ölçek konuları

### <a name="scale-out"></a>Ölçeği genişletme
Ne zaman hello **kullanılabilir bellek düşük** ve hello **CPU kullanımının yüksek olduğu**, makine genelinde yardımcı hello yük genişletme yeni bir düğüm ekleme. Etkinlikler çevrimdışı olmasından tootime genişletme veya ağ geçidi düğümü başarısız oluyorsa, bir düğüm toohello ağ geçidi eklerseniz yardımcı olur.
 
### <a name="scale-up"></a>Ölçeği artırma
Merhaba kullanılabilir bellek ve CPU değil kullanıldığı iyi ancak hello boşta kapasite 0 olduğu durumlarda ölçeklendirmeniz gerekir yukarı hello bir düğümde çalıştırılabilen eşzamanlı iş sayısını artırarak. Merhaba ağ geçidi aşırı yüklendiği için etkinlikler zaman aşımına uğruyor olduğunda, tooscale ayarlamak isteyebilirsiniz. Görüntü aşağıdaki hello gösterildiği gibi bir düğüm için maksimum kapasite hello artırabilir. İle toostart Katlama öneririz.  

![Veri Yönetimi ağ geçidi - ölçek konuları](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>Bilinen sorunlar/sonu değiştirir

- Şu anda, tek bir mantıksal ağ geçidi için toofour fiziksel ağ geçidi düğümleri olabilir. Performansı artırmak için dörtten fazla düğüm gerekirse, bir e-posta çok gönderme[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com).
- Bir ağ geçidi düğümü hello geçerli mantıksal ağ geçidi alanından başka bir mantıksal ağ geçidi tooswitch hello kimlik doğrulama anahtarı ile yeniden kaydedilemiyor. toore kaydını hello gateway hello düğümden kaldırmak, hello ağ geçidini yeniden yükleyin ve diğer mantıksal ağ geçidi hello için hello kimlik doğrulama anahtarı ile kaydeder. 
- HTTP proxy tüm ağ geçidi düğümleri için gerekliyse, diahost.exe.config ve diawp.exe.config hello proxy ayarlayın ve hello Sunucu Yöneticisi'ni toomake tüm düğümlere sahip hello aynı diahost.exe.config ve diawip.exe.config emin kullanın. Bkz: [proxy ayarlarını yapılandırma](data-factory-data-management-gateway.md#configure-proxy-server-settings) ayrıntıları bölümü. 
- toochange şifreleme modu düğümü düğümü iletişimi Ağ Geçidi Yapılandırma Yöneticisi ' nde hello portal dışındaki tüm hello düğümler silin. Ardından düğümler hello şifreleme modu geri değiştirdikten sonra ekleyin.
- Tooencrypt hello düğümü düğümü iletişim kanalını seçerseniz resmi bir SSL sertifikası kullanın. Otomatik olarak imzalanan sertifika, aynı sertifikayı diğer makinelere sertifika yetkilisi listesinin içinde güvenilmiyor hello olarak bağlantı sorunlarına neden olabilir. 
- Merhaba düğümü sürüm hello mantıksal ağ geçidi sürümden daha düşük olduğunda bir ağ geçidi düğümü tooa mantıksal ağ geçidi'ni kaydedilemiyor. Tüm düğümleri hello mantıksal ağ geçidinin portalından silmeniz daha düşük bir sürüm node(downgrade) kaydedebilirsiniz. Mantıksal bir ağ geçidi'nin tüm düğümleri silerseniz, el ile yükleyin ve yeni düğümler toothat mantıksal ağ geçidini kaydedin. Hızlı Kurulum, bu durumda desteklenmiyor.
- Bulut kimlik bilgilerini kullanmaya devam hızlı kurulum tooinstall düğümleri tooan var olan mantıksal ağ geçidi, kullanamazsınız. Merhaba ağ geçidi Yapılandırma Yöneticisi hello ayarları sekmesinde ndan hello kimlik bilgilerinin depolandığı kontrol edebilirsiniz.
- Düğümü düğümü şifreleme etkin olan hızlı kurulum tooinstall düğümleri tooan var olan mantıksal ağ geçidi kullanamazsınız. Sertifikaları el ile eklenmesi hello şifreleme modu ayarı gerektirir, hızlı yükleme seçeneği artık aynıdır. 
- Şirket içi ortamından bir dosya kopyalama için kullanılamaz \\localhost veya artık bu yana localhost veya yerel sürücü C:\files olabilir tüm düğümler erişilebilir. Bunun yerine, kullanın \\ServerName\files toospecify dosyaları konumu.


## <a name="rolling-back-from-hello-preview"></a>Merhaba Önizlemesi'nden geri alınıyor 
tooroll geri hello preview sürümünden bir düğüm dışındaki tüm düğümleri silin. Silme, ancak en az bir düğümü hello mantıksal ağ geçidi olduğundan emin olun hangi düğümlerin önemli değildir. Bir düğüm hello makinedeki ağ geçidi kaldırma veya hello Azure portal kullanarak silebilirsiniz. Hello Azure portalında, hello içinde **Data Factory** sayfasında, bağlı hizmetler toolaunch hello **bağlantılı Hizmetleri** sayfası. Select hello ağ geçidi toolaunch hello **ağ geçidi** sayfası. Merhaba ağ geçidi sayfasında hello ağ geçidiyle ilişkili hello düğümleri görebilirsiniz. Merhaba sayfa hello ağ geçidi'nden bir düğüm silmenize olanak sağlar.
 
Sildikten sonra tıklatın **Önizleme özellikleri** hello aynı Azure portal sayfası ve hello önizleme özelliğini devre dışı bırakın. Ağ geçidi tooone düğümü GA (genel kullanılabilirlik) ağ geçidi sıfırladınız.


## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki makaleleri hello gözden geçirin:
- [Veri Yönetimi ağ geçidi](data-factory-data-management-gateway.md) -hello ağ geçidi ayrıntılı bir genel bakış sağlar.
- [Şirket içi ve bulut arasında veri taşıma veri depolarına](data-factory-move-data-between-onprem-and-cloud.md) -bir ağ geçidi ile tek bir düğüm kullanmak için adım adım yönergeleri içeren bir kılavuz içerir. 
