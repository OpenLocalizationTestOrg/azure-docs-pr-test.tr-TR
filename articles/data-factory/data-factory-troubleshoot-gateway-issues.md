---
title: "Veri Yönetimi ağ geçidi aaaTroubleshoot sorunları | Microsoft Docs"
description: "İpuçları tootroubleshoot sorunları ilgili tooData Yönetimi ağ geçidi sağlar."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Veri Yönetimi Ağ Geçidi kullanımıyla ilgili sorunları giderme
Bu makalede, veri yönetimi ağ geçidi kullanarak sorunlarını giderme hakkında bilgi sağlar.

> [!NOTE]
> Merhaba bkz [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) hello ağ geçidi hakkında ayrıntılı bilgi için makalenin. Merhaba bkz [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) hello ağ geçidi kullanarak bir şirket içi SQL Server veritabanı tooMicrosoft Azure Blob Depolama veri taşıma makale kılavuz.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Tooinstall veya kaydı başarısız ağ geçidi
### <a name="1-problem"></a>1. Sorun
Yüklerken ve hello ağ geçidi yükleme dosyası indirilirken bir ağ geçidi özellikle kaydetme bu hata iletisini görürsünüz.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Nedeni
Merhaba makine tooinstall hello ağ geçidi çalıştığınız toodownload hello son ağ geçidi yükleme dosyasını hello İndirme Merkezi'nden tooa ağ sorunu nedeniyle başarısız oldu.

#### <a name="resolution"></a>Çözüm
Merhaba bilgisayar toohello hello ağ bağlantısından Hello ayarları engelleyip engellemeyeceğini, güvenlik duvarı proxy sunucusu ayarları toosee denetleyin [İndirme Merkezinden](https://download.microsoft.com/)ve güncelleştirme hello ayarları buna göre.

Alternatif olarak, hello hello en son ağ geçidi için hello yükleme dosyası indirebilirsiniz [İndirme Merkezinden](https://www.microsoft.com/download/details.aspx?id=39717) diğer makinelere hello Yükleme Merkezi'nden erişebilirsiniz. Kopya hello yükleyici dosya toohello ağ geçidi ana bilgisayarı ve tooinstall ve güncelleştirme hello ağ geçidi el ile çalıştırın sonra kullanabilirsiniz.

### <a name="2-problem"></a>2. Sorun
Tıklayarak tooinstall bir ağ geçidi denediğiniz olduğunda bu hata bkz **doğrudan bu bilgisayar Yükle** hello Azure Portalı'nda.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Nedeni
Bir ağ geçidi hello makinede zaten yüklü.

#### <a name="resolution"></a>Çözüm
Merhaba hello makinedeki mevcut ağ geçidi kaldırın ve hello tıklatın **doğrudan bu bilgisayar Yükle** yeniden bağlanın.

### <a name="3-problem"></a>3. Sorun
Yeni bir ağ geçidi kaydederken, bu hatayı görebilirsiniz.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Nedeni
Merhaba aşağıdaki nedenlerden biri için bu iletiyi görebilirsiniz:

* Merhaba ağ geçidi anahtarı Hello biçimi geçersiz.
* Merhaba ağ geçidi anahtarı geçersiz kılındı.
* Merhaba ağ geçidi anahtarı hello portalından yeniden.  

#### <a name="resolution"></a>Çözüm
Merhaba portalından hello doğru ağ geçidi anahtarı kullanarak doğrulayın. Gerekirse, bir anahtarın yeniden oluşturulması ve hello anahtar tooregister hello ağ geçidi kullanın.

### <a name="4-problem"></a>4. Sorun
Bir ağ geçidi kaydedilirken hata iletisi aşağıdaki hello görebilirsiniz.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![İçerik veya anahtar biçimi geçersiz](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Nedeni
Merhaba içerik veya hello giriş ağ geçidi anahtarı biçimi doğru değil. Merhaba nedenlerden biri dolayısıyla hello anahtarının yalnızca bir kısmını hello portalından kopyalandığından veya geçersiz bir anahtar kullandığınız olabilir.

#### <a name="resolution"></a>Çözüm
Hello Portalı'nda bir ağ geçidi anahtarı oluşturur ve hello Kopyala düğmesine toocopy hello tüm tuşunu kullanın. Ardından bu pencere tooregister hello ağ geçidi yapıştırın.

### <a name="5-problem"></a>5. Sorun
Bir ağ geçidi kaydedilirken hata iletisi aşağıdaki hello görebilirsiniz.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Ağ geçidi anahtarı geçersiz veya boş değil](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Nedeni
Merhaba ağ geçidi anahtarı yeniden veya hello Azure portal hello ağ geçidi silinmiş olabilir. Merhaba veri yönetimi ağ geçidi Kurulum en son değilse de oluşabilir.

#### <a name="resolution"></a>Çözüm
Merhaba veri yönetimi ağ geçidi Kurulum hello en son sürüm ise, bulabilirsiniz hello en son sürümünü Microsoft hello üzerinde kontrol [İndirme Merkezinden](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Kurulum geçerli / son ve ağ geçidi portalında hala var, hello ağ geçidi anahtarı hello Azure portal'ın yeniden hello Kopyala düğmesine toocopy hello tüm tuşunu kullanın ve bu pencere tooregister hello ağ geçidi yapıştırın. Aksi takdirde hello ağ geçidi yeniden oluşturun ve baştan başlayın.

### <a name="6-problem"></a>6. Sorun
Bir ağ geçidi kaydedilirken hata iletisi aşağıdaki hello görebilirsiniz.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Ağ geçidi anahtarı geçersiz veya boş değil](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Nedeni
Bu hata, hello ağ geçidi silinmiş olabilir ya da hello ilişkili ağ geçidi anahtarı yeniden olmadığından gerçekleşebilir.

#### <a name="resolution"></a>Çözüm
Merhaba ağ geçidi silinip hello ağ geçidi hello portalından yeniden oluşturmak, tıklatın **kaydetmek**hello portalından hello anahtarı kopyalayın, yapıştırın ve tooregister hello ağ geçidi deneyin.

Merhaba ağ geçidi hala var, ancak kendi anahtarı yeniden hello yeni anahtar tooregister hello ağ geçidi kullanın. Merhaba anahtar yoksa, hello portalından yeniden hello tuşunu yeniden oluşturun.

### <a name="7-problem"></a>7. Sorun
Bir ağ geçidi kaydedilirken tooenter yolu ve parola için bir sertifika gerekebilir.

![Sertifika belirtin](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Nedeni
Merhaba ağ geçidi, önce diğer makinelere kaydedildi. Merhaba ilk kaydı bir ağ geçidi sırasında bir şifreleme sertifikası hello ağ geçidi ile ilişkilendirilmiş. Merhaba sertifika hello ağ geçidi tarafından otomatik olarak oluşturulan veya hello kullanıcı tarafından sağlanan.  Bu sertifika hello veri deposu (bağlantılı hizmeti) kullanılan tooencrypt kimlik bilgileridir.  

![Sertifika verme](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Ne zaman bu sertifika toodecrypt daha önce kimlik bilgileri için farklı bir konak makinesi üzerinde hello ağ geçidi hello Kayıt Sihirbazı'nı ister geri Bu sertifika ile şifrelenir.  Bu sertifika olmadan hello kimlik hello yeni ağ geçidi tarafından şifresi çözülemiyor ve bu yeni ağ geçidi ile ilişkili sonraki kopyalama etkinliği yürütmeleri başarısız olur.  

#### <a name="resolution"></a>Çözüm
Merhaba kimlik bilgileri sertifikası hello kullanarak hello özgün ağ geçidi makineden dışarı aktardıysanız **verme** hello düğmesinde **ayarları** sekmesinde Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi'nde, hello kullanın Burada sertifikası.

Bu aşamada, ağ geçidi kurtarırken atlayamazsınız. Merhaba sertifika yoksa, hello portalından toodelete hello ağ geçidine gereksinimi ve yeni bir ağ geçidi yeniden oluşturun.  Ayrıca, kullanıcıların kimlik bilgilerini yeniden girme ilgili toohello ağ geçidi olan tüm bağlantılı Hizmetleri güncelleştirin.

### <a name="8-problem"></a>8. Sorun
Aşağıdaki hata iletisini hello görebilirsiniz.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Nedeni
Ağ geçidiniz bir HTTP proxy tooaccess Internet kaynakların gerektiren bir ortamda olduğunda bu hata oluşur veya proxy'nın kimlik doğrulaması parola değiştirilir, ancak uygun şekilde güncelleştirilmesi ağ geçidiniz içinde.

#### <a name="resolution"></a>Çözüm
Merhaba Hello yönergeleri izleyin [Proxy sunucusu hususları](#proxy-server-considerations) bu bölümü makalesi ve veri yönetimi ağ geçidi Yapılandırma Yöneticisi ile proxy ayarlarını yapılandırın.

## <a name="gateway-is-online-with-limited-functionality"></a>Ağ geçidi ile sınırlı işlevsellik çevrimiçi duruma
### <a name="1-problem"></a>1. Sorun
Sınırlı işlevlerle çevrimiçi olarak hello ağ geçidi hello durumunu görebilir.

#### <a name="cause"></a>Nedeni
Hello durum hello ağ geçidinin çevrimiçi hello aşağıdaki nedenlerden biri için sınırlı işlevsellik ile görürsünüz:

* Ağ geçidi, Azure Service Bus toocloud hizmetine bağlanılamıyor.
* Bulut hizmeti, hizmet veri yolu toogateway bağlanamıyor.

Merhaba ağ geçidi ile sınırlı işlevsellik çevrimiçi olduğunda, şirket içi veri depolarına veri tooor kopyalama mümkün toouse hello Data Factory Kopyalama Sihirbazı toocreate veri ardışık olmayabilir. Geçici bir çözüm olarak, Data Factory Düzenleyici hello portal, Visual Studio ya da Azure PowerShell kullanabilirsiniz.

#### <a name="resolution"></a>Çözüm
Bu sorun için çözüm (sınırlı işlevsellik ile çevrimiçi) olup olmadığını hello ağ geçidi olamaz toohello bulut hizmetine bağlanın ya da başka bir şekilde hello temel alan. Aşağıdaki bölümlerde hello bu çözümleri sağlar.

### <a name="2-problem"></a>2. Sorun
Aşağıdaki hata hello bakın.

`Error: Gateway cannot connect toocloud service through service bus`

![Ağ geçidi toocloud hizmetine bağlanılamıyor](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Nedeni
Ağ geçidi Service Bus toohello bulut hizmetine bağlanılamıyor.

#### <a name="resolution"></a>Çözüm
Bu adımları tooget hello ağ geçidi tekrar çevrimiçi izleyin:

1. IP adresi hello ağ geçidi makinesindeki ve hello Kurumsal güvenlik duvarı giden kuralları izin verir. Merhaba Windows olay günlüğü IP adreslerinden bulabilirsiniz (kimliği 401 ==): bir girişim yapıldı, erişim izinleri XX Yasak şekilde yuva tooaccess yapılan. XX. XX. XX:9350.
* Merhaba ağ geçidinde proxy ayarlarını yapılandırın. Merhaba bkz [Proxy sunucusu hususları](#proxy-server-considerations) ayrıntıları bölümü.
* Giden bağlantı noktası 5671 ve 9350-9354 hem ' % s'hello Windows Güvenlik Duvarı hello ağ geçidi makinesindeki ve hello Kurumsal güvenlik duvarı üzerinde etkinleştirin. Merhaba bkz [bağlantı noktalarını ve Güvenlik Duvarı](#ports-and-firewall) ayrıntıları bölümü. Bu adım isteğe bağlıdır, ancak performans açıklamasında öneririz.

### <a name="3-problem"></a>3. Sorun
Aşağıdaki hata hello bakın.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Nedeni
Ağ bağlantısı geçici bir hata.

#### <a name="resolution"></a>Çözüm
Bu adımları tooget hello ağ geçidi tekrar çevrimiçi izleyin:

1. Birkaç dakika bekleyin, hello hata kaldırılmıştır olduğunda hello bağlantısı otomatik olarak kurtarılacak.
* Merhaba hata devam ederse hello ağ geçidi hizmeti yeniden başlatın.

## <a name="failed-tooauthor-linked-service"></a>Başarısız tooauthor bağlı hizmet
### <a name="problem"></a>Sorun
Yeni bağlı hizmet için hello portal tooinput kimlik bilgilerini toouse kimlik bilgileri Yöneticisi deneyin ya da mevcut bir bağlı hizmeti için kimlik bilgilerini güncelleştirmeniz bu hatayı görebilirsiniz.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

Bu hatayı gördüğünüzde hello Ayarları sayfası veri yönetimi ağ geçidi Yapılandırma Yöneticisi'nin ekran görüntüsü aşağıdaki hello gibi görünebilir.

![Veritabanına erişilemiyor](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Nedeni
Merhaba SSL sertifikası hello ağ geçidi makinede kesilmiş olabilir. Merhaba ağ geçidi bilgisayarı SSL şifreleme için kullanılan hello sertifika şu anda yüklenemiyor. Bir hata iletisi hello olay günlüğünde, iletiden benzer toohello olduğunu da görebilirsiniz.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Çözüm
Bu adımları toosolve hello sorunu izleyin:

1. Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi'ni başlatın.
2. Geçiş toohello **ayarları** sekmesi.  
3. Merhaba tıklatın **değişiklik** düğmesini toochange hello SSL sertifikası.

   ![Değişiklik sertifika düğmesi](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Merhaba SSL sertifikası olarak yeni bir sertifika seçin. Sizin tarafınızdan oluşturulan herhangi bir SSL sertifikası veya herhangi bir kuruluştaki kullanabilirsiniz.

   ![Sertifika belirtin](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>Kopyalama etkinliği başarısız
### <a name="problem"></a>Sorun
Ardışık Düzen hello portalında ayarladıktan sonra "UserErrorFailedToConnectToSqlserver" hatasının ardından hello fark edebilirsiniz.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Nedeni
Bu farklı nedenlerden kaynaklanabilir ve azaltma buna göre değişir.

#### <a name="resolution"></a>Çözüm
Tooan SQL veritabanına bağlanmadan önce bağlantı noktası TCP/1433 hello veri yönetimi ağ geçidi istemci tarafı üzerinden giden TCP bağlantılarını sağlar.

Hello hedef veritabanının Azure SQL veritabanını, SQL Server için Güvenlik Duvarı ayarlarını Azure de kontrol edin.

Aşağıdaki bölümde tootest hello bağlantı toohello şirket içi veri deposu hello bakın.

## <a name="data-store-connection-or-driver-related-errors"></a>Veri deposu bağlantısı veya sürücüsü ile ilgili hataları
Veri deposunda bağlantı veya sürücü ilgili hatalar görürseniz, hello aşağıdaki adımları tamamlayın:

1. Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi hello ağ geçidi makinede başlatın.
2. Geçiş toohello **tanılama** sekmesi.
3. İçinde **Bağlantıyı Sına**, hello ağ geçidi Grup değerlerini ekleyin.
4. Tıklatın **Test** toohello bağlanabiliyorsa toosee şirket içi veri kaynağından hello ağ geçidi makinesi hello bağlantı bilgilerini ve kimlik bilgilerini kullanarak. Bir sürücü yükledikten sonra hello bağlantı testi yine başarısız olursa yeniden hello ağ geçidi için toopick hello son değişiklik ayarlama.

![Tanılama sekmesinde bağlantıyı Sına](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Ağ geçidi günlükleri
### <a name="send-gateway-logs-toomicrosoft"></a>Ağ geçidi günlüklerini tooMicrosoft Gönder
Ağ geçidi sorunlarını giderme ile Microsoft Support tooget Yardım başvurduğunuzda tooshare istenebilir ağ geçidi günlüklerinizi. Merhaba ağ geçidinin Hello sürümle birlikte, gerekli ağ geçidi günlüklerini iki düğme tıklama veri yönetimi ağ geçidi Yapılandırma Yöneticisi ile paylaşabilirsiniz.    

1. Geçiş toohello **tanılama** sekmesini veri yönetimi ağ geçidi Yapılandırma Yöneticisi.

    ![Veri Yönetimi ağ geçidi Tanılama sekmesi](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Tıklatın **günlükleri Gönder** iletişim kutusunda aşağıdaki toosee hello.

    ![Veri Yönetimi ağ geçidi Gönder günlükleri](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (İsteğe bağlı) Tıklatın **günlüklerini görüntülemek** tooreview hello Olay Görüntüleyicisi'nde kaydeder.
4. (İsteğe bağlı) Tıklatın **gizlilik** tooreview Microsoft web hizmetleri gizlilik bildirimi.
5. Tooupload hakkında olan ile memnun kaldığınızda, tıklatın **günlükleri Gönder** tooactually hello sorunlarını gidermeye yönelik olarak son yedi gün tooMicrosoft gelen hello günlüklerini gönderme. Hello ekran aşağıdaki gösterildiği gibi hello günlükleri gönderme işlemi hello durumunu görmeniz gerekir.

    ![Veri Yönetimi ağ geçidi gönderme durumu günlüğe kaydeder](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Merhaba işlemi tamamlandıktan sonra hello ekran aşağıdaki gösterildiği gibi bir iletişim kutusu görürsünüz.

    ![Veri Yönetimi ağ geçidi gönderme durumu günlüğe kaydeder](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Merhaba Kaydet **rapor kimliği** ve Microsoft Support paylaşın. Hello rapor sorun giderme için karşıya kullanılan toolocate hello ağ geçidi günlüklerini kimliktir.  Merhaba rapor kimliği de hello Olay Görüntüleyicisi'nde kaydedilir.  Merhaba olay kimliği "25" bakarak bulun ve başlangıç tarihi ve saati denetleyin.

    ![Veri Yönetimi ağ geçidi Gönderme Raporu Kimliği günlüğe kaydeder](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>Ağ geçidi ana makinede arşiv gateway günlükleri
Burada ağ geçidi sorunları varsa ve ağ geçidi günlüklerini doğrudan paylaşamaz bazı senaryolar vardır:

* El ile Merhaba ağ geçidi yükleyin ve hello ağ geçidini kaydedin.
* Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi yeniden anahtar ile tooregister hello ağ geçidi deneyin.
* Toosend günlükleri deneyin ve hello ağ geçidi ana bilgisayar hizmeti bağlanamaz.

Bu senaryolarda, ağ geçidi günlüklerini bir zip dosyası olarak kaydetmek ve Microsoft desteğe başvurduğunuzda paylaşın. Merhaba ağ geçidi olarak kaydettiğiniz sırada bir hata alırsanız, örneğin, ekran aşağıdaki hello gösterilir.   

![Veri Yönetimi ağ geçidi kayıt hatası](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Merhaba tıklatın **arşiv gateway günlükleri** tooarchive bağlamak ve günlükleri kaydedin ve sonra hello zip dosyası Microsoft desteği ile paylaşabilirsiniz.

![Veri Yönetimi ağ geçidi arşiv günlükleri](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Ağ geçidi günlüklerini bulun
Merhaba Windows Olay günlüklerinde ayrıntılı ağ geçidi günlük bilgilerini bulabilirsiniz.

1. Windows Başlat **Olay Görüntüleyicisi'ni**.
2. Hello günlüklerini bulmak **uygulama ve hizmet günlükleri** > **veri yönetimi ağ geçidi** klasör.

 Ağ geçidi ile ilgili sorunları gidermeye çalışıyorsanız, hata düzeyi olayları hello Olay Görüntüleyicisi'nde arayın.

![Veri Yönetimi ağ geçidi Olay Görüntüleyicisi'nde günlüğe kaydeder](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
