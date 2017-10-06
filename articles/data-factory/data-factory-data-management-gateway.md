---
title: "Veri Fabrikası için yönetim ağ geçidi aaaData | Microsoft Docs"
description: "Şirket içi ve hello arasında veri ağ geçidi toomove veri ayarlama bulut. Veri Yönetimi ağ geçidi, verilerinizi Azure Data Factory toomove kullanın."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>Veri Yönetimi Ağ Geçidi
Merhaba veri yönetimi ağ geçidi şirket içi ortamına toocopy verilerinizde Bulut ve şirket içi veri depoları arasında yüklemeniz gereken bir istemci aracısıdır. Merhaba şirket içi veri depoları Data Factory ile desteklenen hello listelenen [desteklenen veri kaynakları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) bölümü.

Bu makalede hello hello kılavuzda tamamlar [şirket içi ve bulut arasında veri taşıma veri depolarına](data-factory-move-data-between-onprem-and-cloud.md) makalesi. Merhaba kılavuzda, bir şirket içi SQL Server veritabanı tooan Azure blob hello ağ geçidi toomove verileri kullanan bir işlem hattı oluşturun. Bu makalede hello veri yönetimi ağ geçidi hakkında ayrıntılı bilgi sağlar. 

Veri Yönetimi ağ geçidi hello ağ geçidi ile birden çok şirket içi makineler ilişkilendirerek ölçeklendirebilirsiniz. Ölçeklendirmek yukarı bir düğümde aynı anda çalıştırabilirsiniz veri taşıma işlerinin sayısını artırarak. Bu özellik, tek bir düğüme sahip mantıksal bir ağ geçidi için de kullanılabilir. Bkz: [ölçeklendirme veri yönetimi ağ geçidi Azure veri fabrikası'nda](data-factory-data-management-gateway-high-availability-scalability.md) Ayrıntılar için makale.

> [!NOTE]
> Şu anda, ağ geçidi yalnızca hello kopyalama etkinliği ve saklı yordam etkinliği veri fabrikasında destekler. Bir özel etkinlik tooaccess şirket içi veri kaynaklarından olası toouse hello ağ geçidi olmadığı.      

## <a name="overview"></a>Genel Bakış
### <a name="capabilities-of-data-management-gateway"></a>Veri Yönetimi ağ geçidi özelliklerini
Veri Yönetimi ağ geçidi hello aşağıdaki özellikleri sağlar:

* Model veri kaynakları şirket içi ve bulut veri kaynaklarında içinde aynı veri fabrikası hello ve veri taşıma.
* Acil Durum İzleme ve ağ geçidi durumu hello Data Factory sayfasından görünürlük ile yönetim için tek bir bölme vardır.
* Erişim tooon içi veri kaynaklarına güvenli bir şekilde yönetin.
  * Hiçbir değişiklik toocorporate güvenlik duvarı gereklidir. Ağ geçidi yalnızca giden HTTP tabanlı bağlantılar tooopen yapar Internet.
  * Sertifikanız ile şirket içi veri depoları için kimlik bilgilerini şifreler.
* Veri verimli bir şekilde hareket – veri paralel, esnek toointermittent ağ sorunları otomatik yeniden deneme mantığı ile aktarılır.

### <a name="command-flow-and-data-flow"></a>Komut akışının ve veri akışı
Şirket içi ve bulut arasında kopyalama etkinliği toocopy veri kullandığınızda hello etkinlik bir ağ geçidi tootransfer verileri şirket içi veri kaynağı toocloud ve bunun tersi de kullanır.

Hello üst düzey veri akışı için ve adımları için veri ağ geçidi kopyayla özeti aşağıdadır: ![ağ geçidini kullanarak veri akışı](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Veri Geliştirici oluşturur bir ağ geçidi ya da hello kullanarak bir Azure Data Factory'deki [Azure portal](https://portal.azure.com) veya [PowerShell cmdlet'ini](https://msdn.microsoft.com/library/dn820234.aspx).
2. Veri Geliştirici hello ağ geçidi belirterek bir şirket içi veri deposu için bağlı hizmet oluşturur. Bağlantılı hizmetinin hello kurulumunun bir parçası olarak veri Geliştirici hello kimlik bilgilerini ayarlama uygulama toospecify kimlik doğrulama türleri ve kimlik bilgilerini kullanır.  Merhaba uygulama iletişim hello veri ile iletişim kurar kimlik bilgilerini ayarlama tootest bağlantı ve hello ağ geçidi toosave kimlik bilgileri depolar.
3. Ağ geçidi hello bulutta hello kimlik bilgilerini kaydetmeden önce (veri geliştirici tarafından sağlanan), hello ağ geçidi ile ilişkili hello sertifikasıyla hello kimlik bilgilerini şifreler.
4. Data Factory Hizmeti'ne zamanlama & işlerin bir paylaşılan Azure service bus kuyruğu kullanan bir denetim kanalı üzerinden Yönetim için hello ağ geçidi ile iletişim kurar. Bir kopyalama etkinliği iş başlayacağı zamana toobe gerektiğinde, veri fabrikası kimlik bilgileri ile birlikte hello isteğini sıraya koyar. Ağ geçidi hello sıra yoklama sonra hello işi başlatır.
5. Merhaba ağ geçidi hello kimlik bilgileriyle aynı sertifika ve ardından uygun kimlik doğrulama türü ve kimlik bilgileri ile toohello şirket içi veri deposu bağlanır hello şifresini çözer.
6. Merhaba ağ geçidi, bir şirket içi depolama tooa bulut depolama biriminden veya tersi hello kopyalama etkinliği hello veri ardışık düzeninde nasıl yapılandırıldığına bağlı olarak veri kopyalar. Bu adım için hello ağ geçidi doğrudan Azure Blob Depolama gibi bulut tabanlı depolama hizmetleri güvenli (HTTPS) kanal üzerinden iletişim kurar.

### <a name="considerations-for-using-gateway"></a>Ağ geçidini kullanma konuları
* Veri Yönetimi ağ geçidi tek bir örneği birden çok şirket içi veri kaynakları için kullanılabilir. Ancak, **bağlı tooonly bir Azure veri fabrikası bir tek ağ geçidi örneği olan** ve başka bir data factory ile paylaşılamaz.
* Sağlayabilirsiniz **veri yönetimi ağ geçidi yalnızca bir örneği** tek bir makinede yüklü. Tooaccess şirket içi veri kaynakları gereken iki veri fabrikaları olduğunu varsayalım iki şirket içi bilgisayarlarda tooinstall ağ geçitleri gerekir. Diğer bir deyişle, bir ağ geçidi bağlı tooa belirli veri fabrikası olur
* Merhaba **ağ geçidi hello hello veri kaynağı olarak aynı makine üzerinde toobe gerek yoktur**. Ancak, ağ geçidi daha yakından toohello veri kaynağına sahip hello ağ geçidi tooconnect toohello veri kaynağı hello süresini azaltır. Bir ana bilgisayar şirket içi veri kaynağına hello farklı bir makinede hello ağ geçidi yüklemenizi öneririz. Merhaba ağ geçidi ve veri kaynağı farklı makinelerde olduğunda hello ağ geçidi veri kaynağı ile kaynaklar için rekabet edemez.
* Sağlayabilirsiniz **birden çok ağ geçidi toohello bağlanma farklı makinelerde aynı şirket içi veri kaynağına**. Örneğin, iki veri fabrikaları ancak her iki hello veri fabrikaları ile aynı şirket içi veri kaynağına kayıtlı hello hizmet veren iki ağ geçidi olabilir.
* Bilgisayar hizmet yüklü bir ağ geçidi zaten varsa bir **Power BI** senaryosu, yükleme bir **Azure Data Factory için ayrı bir ağ geçidi** başka bir makinede.
* Ağ geçidi kullandığınızda da kullanılmalıdır **ExpressRoute**.
* Veri kaynağı (bir güvenlik duvarının arkasında olan) bir şirket içi veri kaynağı olarak davran kullandığınızda bile **ExpressRoute**. Merhaba hizmet hello veri kaynağı arasında Hello ağ geçidi tooestablish bağlantısı kullanın.
* Yapmanız gerekenler **hello ağ geçidini kullanan** hello veri deposu hello bulutta üzerinde olsa bile bir **Azure Iaas sanal**.

## <a name="installation"></a>Yükleme
### <a name="prerequisites"></a>Ön koşullar
* desteklenen hello **işletim sistemi** sürümleri Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Bir etki alanı denetleyicisinde hello veri yönetimi ağ geçidi yüklemesi şu anda desteklenmiyor.
* .NET framework 4.5.1 veya üzeri gereklidir. Windows 7 makinede ağ geçidi yüklüyorsanız, .NET Framework 4.5 veya üstünü yükleyin. Bkz: [.NET Framework sistem gereksinimleri](https://msdn.microsoft.com/library/8z6watww.aspx) Ayrıntılar için.
* Önerilen hello **yapılandırma** hello ağ geçidi makinesi en az 2 GHz, 4 çekirdek, 8 GB RAM ve 80 GB disk için.
* Merhaba ana makine hazırda bekleme durumunda hello ağ geçidi toodata istekleri yanıt vermez. Bu nedenle, uygun bir yapılandırma **güç planı** hello ağ geçidi'ı yüklemeden önce hello bilgisayarda. Merhaba makine yapılandırılmış toohibernate ise, hello ağ geçidi yükleme isteyen bir ileti alırsınız.
* Merhaba makine tooinstall yönetici olmanız ve hello veri yönetimi ağ geçidi başarılı bir şekilde yapılandırmanız gerekir. Ek kullanıcılar toohello ekleyebilirsiniz **veri yönetimi ağ geçidi kullanıcıları** yerel Windows grubu. Merhaba, bu grubun üyesi mümkün toouse hello **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** aracı tooconfigure hello ağ geçidi.

Etkinlik çalışması üzerinde belirli bir sıklık durum kopyalama gibi hello hello makinede kaynak kullanımı (CPU, bellek) de aynı yoğun ve boşta saatlerle desen hello izler. Kaynak Kullanımı Yoğun olarak da hello taşınan veri miktarına bağlıdır. Birden çok kopyası işleri devam ederken, kaynak kullanımı yoğun zamanlarda gidebilir bakın.

### <a name="installation-options"></a>Yükleme Seçenekleri
Veri Yönetimi ağ geçidi yolları aşağıdaki hello yüklenebilir:

* Merhaba bir MSI kurulum paketi yükleyerek [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).  Merhaba MSI kullanılan tooupgrade mevcut veri yönetimi ağ geçidi toohello en son sürümü, korunan tüm ayarlar ile de olabilir.
* Tıklayarak **veri ağ geçidi yükleyip** bağlantıyı el ile Kurulumu altında veya **doğrudan bu bilgisayar Yükle** EXPRESS Kurulumu altında. Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalede hızlı kurulum kullanma hakkında adım adım yönergeler için. Merhaba el ile adım toohello İndirme Merkezi alır.  karşıdan yükleme ve İndirme Merkezi'nden hello ağ geçidi için hello hello sonraki bölümde yönergelerdir.

### <a name="installation-best-practices"></a>Yükleme için en iyi yöntemler:
1. Böylece Hello makine değil hazırda bekleme güç planı hello konak hello ağ geçidi için yapılandırın. Merhaba ana makine hazırda bekleme durumunda hello ağ geçidi toodata istekleri yanıt vermez.
2. Merhaba ağ geçidiyle ilişkili hello sertifikayı yedekleyin.

### <a name="install-hello-gateway-from-download-center"></a>İndirme Merkezi'nden Hello ağ geçidi yükleyin
1. Çok gidin[Microsoft Veri Yönetimi ağ geçidi yükleme sayfası](https://www.microsoft.com/download/details.aspx?id=39717).
2. ' I tıklatın **karşıdan**, select hello uygun sürümünü (**32-bit** vs. **64-bit**), tıklatıp **sonraki**.
3. Merhaba çalıştırmak **MSI** doğrudan veya tooyour sabit diske kaydetmek ve çalıştırın.
4. Merhaba üzerinde **Hoş Geldiniz** sayfasında, bir **dil** tıklatın **sonraki**.
5. **Kabul** tıklayın ve son kullanıcı lisans sözleşmesi hello **sonraki**.
6. Seçin **klasörü** tooinstall hello ağ geçidi ve tıklayın **sonraki**.
7. Merhaba üzerinde **hazır tooinstall** sayfasında, **yükleme**.
8. Tıklatın **son** toocomplete yükleme.
9. Başlangıç anahtarı hello Azure portal ' alın. Adım adım yönergeler için Hello sonraki bölüme bakın.
10. Merhaba üzerinde **kayıt ağ geçidi** sayfasında **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** , makinede çalışan adımları izleyerek hello:
    1. Başlangıç anahtarı hello metni yapıştırın.
    2. İsteğe bağlı olarak, tıklayın **Göster ağ geçidi anahtarı** toosee hello anahtar metin.
    3. Tıklatın **kaydetmek**.

### <a name="register-gateway-using-key"></a>Anahtarı kullanarak ağ geçidini kaydedin
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Merhaba Portalı'nda mantıksal bir ağ geçidi oluşturmadıysanız
bir ağ geçidi hello portal ve get hello anahtarında hello toocreate **yapılandırma** sayfası, hello izlenecek adımları izleyin [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Merhaba Portalı'nda hello mantıksal ağ geçidi oluşturduysanız
1. Azure portalında toohello gidin **Data Factory** sayfasında ve tıklayın **bağlı hizmetler** döşeme.

    ![Veri Fabrikası sayfası](media/data-factory-data-management-gateway/data-factory-blade.png)
2. Merhaba, **bağlı hizmetler** sayfası, select hello mantıksal **ağ geçidi** hello portalında oluşturulan.

    ![mantıksal ağ geçidi](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. Merhaba, **veri ağ geçidi** sayfasında, **veri ağ geçidi yükleyip**.

    ![Merhaba Portalı'nda bağlantı indirin](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. Merhaba, **yapılandırma** sayfasında, **yeniden oluşturun anahtar**. Evet hello uyarı iletisi dikkatle okuduktan sonra'i tıklatın.

    ![Yeniden anahtar](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Kopyala düğmesine bir sonraki toohello anahtar'ı tıklatın. Merhaba, kopyalanan toohello Pano anahtardır.

    ![Anahtarı kopyalayın](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Sistem Tepsisi Simgeleri / bildirimleri
Merhaba aşağıdaki görüntüde bazılarını hello gördüğünüz Tepsisi simgeleri gösterir.

![Sistem Tepsisi Simgeleri](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

İmleç hello sistem tepsisi simgesi/bildirim iletisi taşırsanız, açılan penceresinde hello ağ geçidi/güncelleştirme işlemini hello durumu hakkında ayrıntılar bakın.

### <a name="ports-and-firewall"></a>Bağlantı noktaları ve güvenlik duvarı
İki güvenlik duvarı tooconsider ihtiyacınız vardır: **Kurumsal Güvenlik Duvarı** hello merkezi yönlendirici hello kuruluşunuzun üzerinde çalışan ve **Windows Güvenlik Duvarı** hello yerel makine üzerinde bir arka plan programı olarak hello burada yapılandırılan Ağ Geçidi yüklü.  

![Güvenlik duvarları](./media/data-factory-data-management-gateway/firewalls2.png)

Kurumsal güvenlik duvarı düzeyinde hello aşağıdaki yapılandırmayı etki alanları ve giden bağlantı noktaları:

| Etki alanı adları | Bağlantı Noktaları | Açıklama |
| --- | --- | --- |
| *. servicebus.windows.net |443, 80 |Veri Taşıma hizmeti arka uç ile iletişim için kullanılan |
| *. core.windows.net |443 |Azure Blob (yapılandırılmışsa) kullanarak hazırlanmış kopyalama için kullanılan|
| *. frontend.clouddatahub.net |443 |Veri Taşıma hizmeti arka uç ile iletişim için kullanılan |


Windows Güvenlik Duvarı düzeyde, bu giden bağlantı noktaları normal şekilde etkinleştirilir. Merhaba etki alanları ve bağlantı noktalarını uygun şekilde yapılandırabilirsiniz, varsa ağ geçidi makinesi üzerinde.

> [!NOTE]
> 1. Kaynağını temel alan / havuzlarını toowhitelist ek etki alanları ve giden bağlantı noktaları olabilir, Kurumsal/Windows Güvenlik Duvarı.
> 2. Bazı bulut veritabanları için (örneğin: [Azure SQL veritabanı](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), vb.), ağ geçidi makinede güvenlik duvarı yapılandırmalarını toowhitelist IP adresini gerekebilir.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>Bir kaynak veri deposu tooa havuz veri deposundan veri kopyalama
Merhaba güvenlik duvarı kurallarının düzgün şekilde hello Kurumsal güvenlik duvarı, Windows Güvenlik Duvarı hello gateway makinesinde, üzerinde etkindir ve kendisini hello verileri depolamak emin olun. Bu kurallar etkinleştirme hello ağ geçidi tooconnect tooboth kaynak ve havuz başarıyla sağlar. Merhaba kopyalama işleminde dahil her veri deposu için kuralları etkinleştirin.

Örneğin, gelen toocopy **bir şirket içi veri deposu tooan Azure SQL veritabanı havuzunu veya bir Azure SQL Data Warehouse havuz**, adımları hello:

* Gidene izin ver **TCP** iletişim bağlantı noktası **1433** Windows Güvenlik Duvarı ve kurumsal güvenlik duvarı için.
* Azure SQL server tooadd hello IP adresinin hello ağ geçidi makinesi toohello izin verilen IP adreslerinin listesi Hello güvenlik duvarı ayarlarını yapılandırın.

> [!NOTE]
> Güvenlik duvarını giden bağlantı noktası 1433 izin vermez, ağ geçidi doğrudan Azure SQL erişemiyor. Bu durumda, kullanabilir [hazırlanan kopyalama](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure veritabanı / SQL Azure DW. Bu senaryoda, yalnızca HTTPS (443 numaralı) hello veri taşıma için gerektirir.
>
>


### <a name="proxy-server-considerations"></a>Proxy sunucusu hususları
Kurumsal ağ ortamınızın bir proxy kullanıyorsa, sunucu tooaccess Internet Merhaba, veri yönetimi ağ geçidi toouse uygun proxy ayarlarını yapılandırın. Merhaba ilk kayıt aşamasında hello proxy ayarlayabilirsiniz.

![Kayıt sırasında kümesi proxy](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

Ağ geçidi hello proxy sunucusu tooconnect toohello bulut hizmeti kullanır. Tıklatın **değişiklik** ilk kurulum sırasında bağlantı. Merhaba gördüğünüz **proxy ayarını** iletişim.

![Yapılandırma Yöneticisi'ni kullanarak küme proxy](media/data-factory-data-management-gateway/SetProxySettings.png)

Üç yapılandırma seçeneği vardır:

* **Proxy kullanmayın**: ağ geçidi proxy tooconnect toocloud hizmetlerin açıkça kullanmaz.
* **Sistem proxy kullanacak**: ağ geçidi olarak yapılandırılmış diahost.exe.config ve diawp.exe.config ayarının hello proxy kullanır.  Proxy diahost.exe.config ve diawp.exe.config yapılandırılmışsa, ağ geçidi toocloud hizmeti proxy üzerinden geçmeden doğrudan bağlanır.
* **Özel ara sunucu kullanmak**: hello HTTP proxy ayarı toouse diahost.exe.config ve diawp.exe.config yapılandırmalarında kullanmak yerine ağ geçidi için yapılandırın.  Adresi ve bağlantı noktası gereklidir.  Kullanıcı adı ve parola, proxy'nin kimlik doğrulama ayarını bağlı olarak isteğe bağlıdır.  Tüm ayarlar hello kimlik bilgileri sertifikası hello ağ geçidi ile şifrelenir ve hello ağ geçidi ana makinede yerel olarak depolanır.

Merhaba güncelleştirilen proxy ayarlarını kaydettikten sonra hello veri yönetimi ağ geçidi ana bilgisayar hizmeti otomatik olarak yeniden başlatılır.

Tooview veya proxy ayarlarını güncelleştirmek istiyorsanız ağ geçidi başarıyla, kaydedildikten sonra veri yönetimi ağ geçidi Yapılandırma Yöneticisi'ni kullanın.

1. Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi**.
2. Geçiş toohello **ayarları** sekmesi.
3. Tıklatın **değişiklik** bağlamak **HTTP Proxy** bölüm toolaunch hello **Set HTTP Proxy** iletişim.  
4. Merhaba tıklattıktan sonra **sonraki** düğmesi, ağ geçidi ana bilgisayar hizmeti izni toosave hello proxy ayarını ve yeniden başlatma hello için soran bir uyarı iletişim kutusu görürsünüz.

Görüntüleyin ve Configuration Manager aracını kullanarak HTTP proxy güncelleştirin.

![Yapılandırma Yöneticisi'ni kullanarak küme proxy](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Bir proxy sunucusu NTLM kimlik doğrulaması ile ayarladıysanız, ağ geçidi ana bilgisayar hizmeti hello etki alanı hesabı altında çalışır. Daha sonra hello etki alanı hesabı hello parolayı değiştirirseniz, hello hizmeti için yapılandırma ayarlarını tooupdate unutmayın ve uygun şekilde yeniden başlatın. Toothis gereksinim tooupdate hello parola sık gerektirmeyen özel etki alanı hesabı tooaccess hello proxy sunucusu kullan öneririz.
>
>

### <a name="configure-proxy-server-settings"></a>Proxy sunucusu ayarlarını yapılandırın
Seçerseniz **sistem proxy kullanacak** hello HTTP Proxy'si için ayarı, ağ geçidi hello proxy diahost.exe.config ve diawp.exe.config ayarını kullanır.  Proxy diahost.exe.config ve diawp.exe.config belirtilirse, ağ geçidi toocloud hizmeti proxy üzerinden geçmeden doğrudan bağlanır. Merhaba aşağıdaki yordamı hello diahost.exe.config dosyasını güncelleştirmek için yönergeler sağlar.  

1. Dosya Gezgini'nde, C:\Program Files\Microsoft veri yönetimi Gateway\2.0\Shared\diahost.exe.config tooback güvenli bir kopyasını hello özgün dosyasının yedeğini oluşturun.
2. Yönetici olarak çalıştırarak Notepad.exe başlatın ve metin dosyasını "C:\Program Files\Microsoft veri yönetimi Gateway\2.0\Shared\diahost.exe.config. açın Hello kod aşağıdaki gösterildiği gibi hello varsayılan etiket için system.net bulun:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   Proxy sunucu ayrıntıları hello aşağıdaki örnekte gösterildiği gibi daha sonra ekleyebilirsiniz:

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Ek özellikler scriptLocation gibi hello proxy etiketi toospecify gerekli hello ayarları içinde izin verilir. Çok başvuran[proxy öğesi (ağ ayarları)](https://msdn.microsoft.com/library/sa91de1e.aspx) sözdizimi hakkında.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Merhaba özgün konumuna Hello yapılandırma dosyasını kaydetmek sonra hello hello değişiklikleri toplar veri yönetimi ağ geçidi ana bilgisayar hizmeti yeniden başlatın. toorestart hello hizmet: hello Denetim Masası'ndan veya hello hizmetler uygulamasını kullanın **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** > merhaba tıklatın **Hizmeti Durdur** düğmesine ve ardından hello **Hizmetini başlatmak**. Merhaba Hizmet başlatılmazsa, hatalı bir XML etiket söz dizimini, düzenlendiği hello uygulama yapılandırma dosyasına eklendi olasıdır.

> [!IMPORTANT]
> Tooupdate unutmadığınızdan **her ikisi de** diahost.exe.config ve diawp.exe.config.  


Ayrıca toothese noktaları ayrıca toomake Microsoft Azure, şirketinizin beyaz olmasını gerekir. Geçerli Microsoft Azure IP adreslerinin listesi Hello hello indirilebilir [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Güvenlik Duvarı ve proxy sunucusu ile ilgili sorunlar için olası Belirtiler
Hataları benzer toohello olanları aşağıdaki sorunlarla karşılaşırsanız, tooimproper hangi bağlantı tooData Fabrika tooauthenticate kendisini ağ geçidinden engeller hello güvenlik duvarı veya proxy sunucusunun yapılandırmasını, son olasıdır. Güvenlik Duvarı ve proxy sunucunuz düzgün yapılandırılmış tooprevious bölüm tooensure bakın.

1. Tooregister hello ağ geçidi çalıştığınızda, aşağıdaki hata hello alırsınız: "başarısız tooregister hello ağ geçidi anahtarı. Tooregister hello ağ geçidi anahtarı yeniden denemeden önce veri yönetimi ağ geçidi bağlı bir durumda hello ve hello veri yönetimi ağ geçidi ana bilgisayar hizmeti başlatıldığında onaylayın."
2. Yapılandırma Yöneticisi'ni açın, durum "Bağlantı kesildi" veya "Bağlanıyor." görürsünüz Windows olay günlükleri, "Olay Görüntüleyici" görüntülerken > "Uygulama ve hizmet günlükleri" > "Veri yönetimi ağ geçidi", aşağıdaki hata hello gibi hata iletilerine bakın:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Kimlik bilgisi şifreleme için 8050 numaralı bağlantı noktasını açın
Merhaba **kimlik bilgilerini ayarlama** uygulamanız tarafından kullanılan bağlantı noktasına gelen hello **8050** bir şirket içi yedekleme ayarladığınızda toorelay kimlik bilgileri toohello ağ geçidi hello Azure portal hizmetinde bağlı. Ağ geçidi Kurulum sırasında varsayılan olarak, hello ağ geçidi yükleme hello ağ geçidi makinede açar.

Bir üçüncü taraf güvenlik duvarı kullanıyorsanız, başlangıç bağlantı noktası 8050 el ile açabilirsiniz. Ağ geçidi Kurulum sırasında güvenlik duvarı sorunu yaşayıp çalıştırırsanız, komut tooinstall hello ağ geçidi hello güvenlik duvarını yapılandırma olmadan aşağıdaki hello kullanmayı deneyebilirsiniz.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Merhaba gateway makinesinde hello bağlantı noktası 8050 değil tooopen seçerseniz, hello kullanma dışındaki mekanizmalarını kullanmak **kimlik bilgilerini ayarlama** uygulama tooconfigure verilerini depolamak kimlik bilgileri. Örneğin, kullanabilirsiniz [yeni AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet'i. Bkz: [kimlik bilgilerini ayarlama ve güvenlik](#set-credentials-and-securityy) nasıl veri kimlik bilgilerini depolamak üzerinde bölüm ayarlanabilir.

## <a name="update"></a>Güncelleştirme
Varsayılan olarak, veri yönetimi ağ geçidi hello ağ geçidi daha yeni bir sürümü kullanılabilir olduğunda otomatik olarak güncelleştirilir. Tüm hello zamanlanmış görevler tümü tamamlanıncaya kadar hello ağ geçidi güncelleştirilmez. Merhaba güncelleştirme işlemi tamamlanana kadar başka görev hello ağ geçidi tarafından işlenir. Merhaba güncelleştirmesi başarısız olursa, ağ geçidi toohello eski sürümünü geri alınır.

Zamanlanmış hello güncelleştirme yerler aşağıdaki hello zamanında bakın:

* hello Azure Portalı'ndaki Hello ağ geçidi özellikleri sayfasında.
* Merhaba veri yönetimi ağ geçidi Yapılandırma Yöneticisi giriş sayfası
* Sistem tepsisi bildirimi iletisi.

hello veri yönetimi ağ geçidi Yapılandırma Yöneticisi Hello Giriş sekmesinde hello güncelleştirme zamanlaması görüntüler ve hello son zaman hello ağ geçidi yüklü/güncelleştirildi.

![Güncelleştirmeleri zamanlama](media/data-factory-data-management-gateway/UpdateSection.png)

Merhaba güncelleştirmeyi hemen yükleyin veya hello ağ geçidi toobe Zamanlanmış Başlangıç zamanında otomatik olarak güncelleştirilmesini bekleyin. Örneğin, hello ağ geçidi Yapılandırma Yöneticisi tooinstall tıklayabilirsiniz hello Güncelleştir düğmesini yanı sıra, hemen gösterilen bildirim iletisi hello görüntü gösterir aşağıdaki hello.

![Güncelleştirme DMG Yapılandırma Yöneticisi'nde](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

Merhaba bildirim iletisi hello sistem tepsisindeki hello görüntü aşağıdaki gösterildiği gibi görünür:

![Sistem tepsisi iletisi](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Güncelleştirme işlemi (el ile veya otomatik) hello sistem tepsisindeki hello durumunu bakın. Ağ geçidi Yapılandırma Yöneticisi'ni başlattığınızda başlattığında, o hello ağ geçidi çubuğu hello bildirim iletide güncelleştirilmiştir birlikte bağlantı çok bkz[yeni konu nedir](data-factory-gateway-release-notes.md).

### <a name="toodisableenable-auto-update-feature"></a>toodisable/etkinleştirme otomatik güncelleştirme özelliği
Devre dışı bırak/hello otomatik güncelleştirme özelliği aşağıdaki adımları hello yaparak etkinleştirebilirsiniz:

[Tek düğüm için ağ geçidi]
1. Merhaba gateway makinesindeki Windows PowerShell'i başlatın.
2. Toohello C:\Program Files\Microsoft veri yönetimi Gateway\2.0\PowerShellScript klasörüne geçin.
3. Komut tooturn hello otomatik güncelleştirme aşağıdaki çalışma hello özelliği (devre dışı bırakın).   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. tekrar açma tooturn:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Çok düğümlü yüksek oranda kullanılabilir ve Ölçeklenebilir Ağ Geçidi (Önizleme)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Merhaba gateway makinesindeki Windows PowerShell'i başlatın.
2. Toohello C:\Program Files\Microsoft veri yönetimi Gateway\2.0\PowerShellScript klasörüne geçin.
3. Komut tooturn hello otomatik güncelleştirme aşağıdaki çalışma hello özelliği (devre dışı bırakın).   

    Yüksek kullanılabilirlik özelliği (Önizleme) ile ağ geçidi için fazladan bir AuthKey param gereklidir.
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. tekrar açma tooturn:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
Merhaba ağ geçidi makineden farklı bir makineden hello portal erişirseniz Merhaba kimlik bilgileri Yöneticisi uygulaması toohello ağ geçidi makinesi bağlanabilir emin olmanız gerekir. Merhaba uygulaması hello ağ geçidi makinesi bağlanamazsa, bunu, hello veri kaynağı ve tootest bağlantı toohello veri kaynağı için kimlik bilgilerini tooset izin vermiyor.  

Merhaba kullandığınızda **kimlik bilgilerini ayarlama** uygulama hello portal şifreler hello kimlik hello belirtilen hello sertifikayla **sertifika** hello sekmesinde **ağ geçidi Configuration Manager** hello gateway makinesinde.

Merhaba kimlik bilgilerini şifrelemek için API tabanlı bir yaklaşım arıyorsanız hello kullanabilirsiniz [yeni AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt kimlik bilgileri. Merhaba cmdlet hello sertifikasını bu ağ geçidi yapılandırılmış toouse tooencrypt hello kimlik bilgilerini kullanır. Şifrelenmiş kimlik bilgileri toohello ekleme **EncryptedCredential** hello öğesinin **connectionString** hello JSON içinde. Merhaba JSON hello ile kullandığınız [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet'ini veya hello Data Factory Düzenleyici.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Data Factory düzenleyici kullanarak kimlik bilgilerini ayarlama daha fazla bir yaklaşım vardır. Bir SQL Server bağlantılı oluşturursanız ve hello Düzenleyicisi'ni kullanarak hizmet kimlik bilgilerini düz metin olarak girin, hello kimlik bilgileri hello Data Factory hizmetine sahip bir sertifika kullanılarak şifrelenir. Merhaba sertifikasını bu ağ geçidi yapılandırılmış toouse kullanmaz. Bu yaklaşım bazı durumlarda biraz daha hızlı olabilir ancak daha az güvenlidir. Bu nedenle, yalnızca geliştirme ve Test amaçları için bu yaklaşım izlemenizi öneririz.

## <a name="powershell-cmdlets"></a>PowerShell cmdlet'leri
Bu bölümde açıklanmıştır nasıl toocreate ve Azure PowerShell cmdlet'lerini kullanarak ağ geçidini kaydedin.

1. Başlatma **Azure PowerShell** Yönetici modunda.
2. Çalıştırarak tooyour Azure hesabı oturum komutu aşağıdaki ve Azure kimlik bilgilerinizi girerken hello.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Kullanım hello **yeni AzureRmDataFactoryGateway** cmdlet toocreate şekilde mantıksal bir ağ geçidi:

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **Örnek komut ve çıktı**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. Azure PowerShell'de toohello klasörüne geçin: **C:\Program Files\Microsoft veri yönetimi Gateway\2.0\PowerShellScript\**. Çalıştırma **RegisterGateway.ps1** hello yerel değişkeni ile ilişkilendirilmiş **$Key** hello komutu aşağıdaki gösterildiği gibi. Bu komut dosyasını daha önce oluşturduğunuz hello mantıksal ağ geçidi ile makinenizde yüklü hello istemci Aracısı kaydeder.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Uzak makinedeki hello ağ geçidi hello IsRegisterOnRemoteMachine parametresini kullanarak kaydedebilirsiniz. Örnek:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. Merhaba kullanabilirsiniz **Get-AzureRmDataFactoryGateway** cmdlet tooget hello ağ geçidi, veri fabrikası'nda listesi. Ne zaman hello **durum** gösterir **çevrimiçi**, ağ geçidiniz hazır toouse olduğu anlamına gelir.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Hello kullanarak bir ağ geçidi kaldırabilirsiniz **Kaldır AzureRmDataFactoryGateway** hello kullanarak bir ağ geçidi için cmdlet ve güncelleştirme açıklama **kümesi AzureRmDataFactoryGateway** cmdlet'leri. Data Factory Cmdlet başvurusu sözdizimi ve bu cmdlet'ler hakkında diğer ayrıntılar için bkz.  

### <a name="list-gateways-using-powershell"></a>PowerShell kullanarak listesi ağ geçitleri

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>PowerShell kullanarak ağ geçidi kaldırma

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [şirket içi ve bulut arasında veri taşıma veri depolarına](data-factory-move-data-between-onprem-and-cloud.md) makalesi. Merhaba kılavuzda, bir şirket içi SQL Server veritabanı tooan Azure blob hello ağ geçidi toomove verileri kullanan bir işlem hattı oluşturun.  
