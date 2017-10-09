---
title: "Tanılama & ileti Çözümleyicisi ile Azure depolama aaaTroubleshooting | Microsoft Docs"
description: "Azure Storage Analytics, AzCopy ve Microsoft Message Analyzer uçtan uca sorun giderme gösteren bir öğretici"
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 6b23cba5-0d53-439e-870b-de8e406107d8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 74ee126bab30b9a45f4904a065b6fe3006f76101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>Azure Storage ölçümleri ve günlüğe kaydetme, AzCopy ve ileti Çözümleyicisi'ni kullanarak uçtan uca sorun giderme
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../includes/storage-selector-portal-e2e-troubleshooting.md)]

## <a name="overview"></a>Genel Bakış
Tanılama ve sorun giderme oluşturma ve Microsoft Azure Storage ile istemci uygulamalarını desteklemek için anahtar bir yetenektir. Azure uygulaması dağıtılmış toohello yapısı, tanılama ve sorun giderme hataları ve performans sorunlarını geleneksel ortamlarda daha karmaşık olabilir.

Bu öğreticide, biz gösterilmektedir nasıl tooidentify istemci performansını etkiler ve uçtan uca bu hataları giderin belirli hataları sipariş toooptimize hello istemci uygulamasında Microsoft ve Azure Storage tarafından sağlanan araçları kullanarak.

Bu öğretici, uçtan uca bir sorun giderme senaryosu uygulamalı incelenmesi sağlar. Bir kapsamlı kavramsal kılavuz tootroubleshooting Azure depolama uygulamalar için bkz [izleme, tanılama ve Microsoft Azure Storage sorun giderme](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Azure Storage uygulamaları sorun giderme araçları
Microsoft Azure depolama kullanan tootroubleshoot istemci uygulamalar bir sorun oluştuğunda araçları toodetermine ve hello sorunun hangi hello nedeni olabilir bir bileşimini kullanabilirsiniz. Bu araçlar şunları içerir:

* **Azure depolama çözümlemeleri**. [Azure Storage Analytics](http://msdn.microsoft.com/library/azure/hh343270.aspx) ölçümleri ve Azure Storage için günlük kaydını sağlar.

  * **Depolama ölçümleri** işlem ölçümlerini ve depolama hesabınız için kapasite ölçümlerini izler. Ölçümleri kullanarak, uygulamanızın farklı ölçüleri according tooa çeşitli nasıl gerçekleştirmekte belirleyebilirsiniz. Bkz: [Storage Analytics Ölçüm tablosu şeması](http://msdn.microsoft.com/library/azure/hh343264.aspx) depolama analizi tarafından izlenen ölçümleri hello türleri hakkında daha fazla bilgi için.
  * **Depolama günlük** her isteği toohello Azure Storage Hizmetleri tooa sunucu-tarafı günlüğüne kaydeder. Merhaba durumunu hello işlemi ve gecikme bilgileri Hello günlük parçaları ayrıntılı veri hello işlemi de dahil olmak üzere her istek için gerçekleştirilecek. Bkz: [depolama Analytics günlük biçimi](http://msdn.microsoft.com/library/azure/hh343259.aspx) toohello günlükleri depolama analizi tarafından yazılmış hello istek ve yanıt veriler hakkında daha fazla bilgi için.

> [!NOTE]
> Çoğaltma türü, bölge olarak yedekli depolama (ZRS) depolama hesaplarıyla hello ölçümleri veya şu anda etkin günlüğe kaydetme özelliğine sahip değilsiniz.
>
>

* **Klasik Azure portalı**. Depolama hesabınızdaki hello için ölçümleri ve günlük yapılandırabilirsiniz [Klasik Azure portalı](https://manage.windowsazure.com). Ayrıca, grafikler ve uygulamanızı zaman içinde nasıl gerçekleştirmekte gösteren grafikleri görüntüleyin ve uygulamanızı daha farklı gerçekleştirirse, belirtilen bir ölçüm için beklenen uyarıları toonotify yapılandırın.

    Bkz: [hello Azure Portal'da depolama hesabı izleme](storage-monitor-storage-account.md) hello Klasik Azure portalı izlemeyi yapılandırma hakkında bilgi için.
* **AzCopy**. Microsoft Message Analyzer kullanarak analiz için AzCopy toocopy hello günlük BLOB'lar tooa yerel dizin kullanabilmeniz için Azure Storage için sunucu günlüklerine BLOB olarak depolanır. Bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md) AzCopy hakkında daha fazla bilgi.
* **Microsoft Message Analyzer**. İleti Çözümleyicisi günlük dosyalarını kullanır ve kolay toofilter, arama ve veri tooanalyze hataları ve performans sorunlarını kullanabileceğiniz yararlı ayarlar oturum Grup kolaylaştırır görsel bir biçimde günlük verileri görüntüleyen bir araçtır. Bkz: [Microsoft Message Analyzer işletim kılavuzu](http://technet.microsoft.com/library/jj649776.aspx) ileti Çözümleyicisi hakkında daha fazla bilgi.

## <a name="about-hello-sample-scenario"></a>Merhaba Örnek senaryo hakkında
Bu öğreticide, biz burada düşük yüzde başarı oranı Azure depolama çağıran bir uygulama için Azure Storage ölçümlerini gösterir bir senaryo inceleyeceğiz. düşük yüzde başarı oranı ölçüm hello (olarak gösterilen **PercentSuccess** hello Klasik Azure portalı ve hello ölçümleri tablolar), başarılı, ancak 299 büyük bir HTTP durum kodu döndürür işlemlerini izler. Merhaba sunucu tarafı depolama günlük dosyalarında bir işlem durumuyla işlemlerini kaydedilir **ClientOtherErrors**. Merhaba düşük yüzde başarı ölçüm hakkında daha fazla ayrıntı için [ölçümleri Göster düşük PercentSuccess veya analytics günlük girdilerine sahip ClientOtherErrors işlem durumundaki işlemlerini](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success).

Azure depolama işlemleri HTTP durum kodları 299 büyük normal işlevleri bir parçası olarak döndürebilir. Ancak bazı durumlarda bu hatalar istemci uygulamanız için mümkün toooptimize olabileceğini gösteriyor geliştirilmiş performans.

Bu senaryoda, biz düşük yüzde başarı oranı toobe % 100 altındaki her şeyi ele alacağız. Tooyour gereksinimlerine göre farklı bir ölçüm düzeyi, ancak seçebilirsiniz. Uygulamanızın veya test sırasında bir taban çizgisi dayanıklılık için temel performans ölçümlerini oluşturmanızı öneririz. Örneğin, karar verebilir temel test üzerinde % 90 veya % 85 tutarlı yüzde başarı oranını uygulamanızın olması gerekir. Ölçüm verilerini Merhaba uygulaması bulunan sayının deviating olduğunu gösteriyorsa, hello artış neden olabilecek araştırabilirsiniz.

Biz kurduktan sonra hello yüzde başarı Oranı % 100 ölçümüdür, biz toohello ölçümleri ilişkilendirmek hello günlükleri toofind hello hataları inceleyin ve bunları bizim Örnek senaryo için hello düşük yüzde başarı oranı ne toofigure neden oluyor. Özellikle hello 400 aralıktaki hataları inceleyeceğiz. Ardından biz daha yakından (bulunamadı) 404 hatalarını araştırın.

### <a name="some-causes-of-400-range-errors"></a>400-range hataların bazı nedenler
Merhaba örneklere örnekleme Azure Blob Storage'a karşı istek için bazı 400-range hataları ve bunların olası nedenleri gösterir. Bu hata, yanı sıra hello 300 aralığı ve hello 500 aralık, hatalar hiçbirini tooa düşük yüzde başarı oranı katkıda bulunabilir.

Merhaba listelerde gölgeden uzak tam olduğuna dikkat edin. Bkz: [durum ve hata kodları](http://msdn.microsoft.com/library/azure/dd179382.aspx) genel Azure Storage hataları ve belirli hataları tooeach hello depolama hizmetleri hakkında ayrıntılar için.

**Durum kodu 404 (bulunamadı) örnekleri**

Merhaba blob veya kapsayıcı bulunmadığı için bir kapsayıcı veya blob karşı okuma işlemi başarısız olduğunda oluşur.

* Bir kapsayıcı veya blob bu isteği önce başka bir istemci tarafından silindiyse oluşur.
* Merhaba kapsayıcı veya blob var olup olmadığını denetledikten sonra oluşturan bir API çağrısı kullanılıyorsa oluşur. Merhaba CreateIfNotExists API'leri hello varlığını hello kapsayıcı veya blob ilk toocheck çağrısı HEAD olun; yoksa, 404 hatası döndürülür ve ardından ikinci PUT çağrı toowrite hello kapsayıcı veya blob yapılır.

**Durum kodu 409 (Çakışma) örnekleri**

* Bir API oluşturma toocreate yeni bir kapsayıcı veya blob, varlık için önce denetlemeden kullanırsanız ve bir kapsayıcı veya bu adı taşıyan blob zaten oluşur.
* Bir kapsayıcı silindi ve toocreate hello hello silme işlemi tamamlanmadan önce aynı ad ile yeni bir kapsayıcı çalışırsanız oluşur.
* Bir kapsayıcı veya blob kira belirtin ve zaten mevcut bir kira ise oluşur.

**Durum kodu 412 (önkoşul başarısız oldu) örnekleri**

* Koşullu üstbilgisi tarafından belirtilen hello koşulu karşılanmadı oluşur.
* Belirtilen hello kira kimliği hello kapsayıcı veya blob hello kira Kimliğiyle eşleşmiyor oluşur.

## <a name="generate-log-files-for-analysis"></a>Analiz için günlük dosyaları oluşturma
Bunlardan herhangi biriyle toowork seçebilir ancak bu öğreticide, ileti Çözümleyicisi toowork üç farklı türde günlük dosyaları ile kullanacağız:

* Merhaba **sunucu günlüğü**, Azure Storage günlüğü etkinleştirdiğinizde oluşturuldu. Merhaba sunucu günlüğü hello Azure Storage Hizmetleri - blob, kuyruk, tablo ve dosya birini karşı olarak adlandırılan her işlemi hakkındaki verileri içerir. hangi işlemi çağrıldı ve hangi durum kodu döndürülen yanı sıra diğer ayrıntılarını hello istek ve yanıt Hello server günlüğünü gösterir.
* Merhaba **.NET istemci günlüğü**, .NET uygulama içinde istemci tarafı günlüğe etkinleştirdiğinizde oluşturuldu. Merhaba istemci günlüğü nasıl hello istemci hello isteği hazırlar ve alır ve hello yanıt işlediği hakkında ayrıntılı bilgi içerir.
* Merhaba **HTTP ağ izleme günlüğü**, hangi verileri toplar Azure Storage'a karşı işlemleri dahil olmak üzere HTTP/HTTPS istek ve yanıt verileri. Bu öğreticide, biz hello ağ izleme ileti Çözümleyicisi aracılığıyla oluşturacaksınız.

### <a name="configure-server-side-logging-and-metrics"></a>Sunucu tarafı günlüğe kaydetme ve ölçümleri yapılandırın
Böylece hello istemci uygulaması tooanalyze verilerden sahibiz ilk olarak, biz tooconfigure Azure Storage günlüğe kaydetme ve ölçümleri, gerekir. Günlüğe kaydetme ve ölçümleri çeşitli şekillerde - hello yoluyla yapılandırabileceğiniz [Klasik Azure portalı](https://manage.windowsazure.com), PowerShell kullanarak veya program aracılığıyla. Bkz: [depolama ölçümlerini etkinleştirme ve ölçüm verilerini görüntüleme](http://msdn.microsoft.com/library/azure/dn782843.aspx) ve [depolama günlüğünü etkinleştirme ve erişim günlüğü verilerini](http://msdn.microsoft.com/library/azure/dn782840.aspx) günlüğe kaydetme ve ölçümleri yapılandırma hakkında ayrıntılar için.

**Merhaba Klasik Azure portalı**

tooconfigure günlüğe kaydetme ve hello portal kullanarak depolama hesabınız için ölçümleri izleyin hello yönergeleri [hello Azure Portal'da depolama hesabı izleme](storage-monitor-storage-account.md).

> [!NOTE]
> Şu olası tooset minute ölçümleri hello Klasik Azure portalı kullanarak da değil. Ancak, bunları bu öğreticinin hello amaçları ve uygulamanız ile performans sorunları incelemeye ayarlamanızı öneririz. Aşağıda ya da program aracılığıyla gösterildiği gibi PowerShell kullanarak dakika ölçümleri ayarlayın veya Klasik Azure Portalı aracılığıyla hello.
>
> Klasik Azure portalı hello Not dakika ölçümleri, saatlik ölçümleri yalnızca görüntülenemiyor.
>
>

**PowerShell yoluyla**

Azure, PowerShell kullanmaya tooget bkz [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

1. Kullanım hello [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) cmdlet tooadd Azure kullanıcı hesabı toohello PowerShell penceresinde:

    ```powershell
     Add-AzureAccount
    ```

2. Merhaba, **tooMicrosoft Azure oturum** penceresinde hello e-posta adresini yazın ve hesabınızla ilişkili parola. Azure kimliğini doğrular ve hello kimlik bilgileri kaydeder ve hello penceresini kapatır.
3. Merhaba PowerShell penceresinde aşağıdaki komutları yürüterek hello öğretici için kullanmakta olduğunuz hello varsayılan depolama hesabı toohello depolama hesabı ayarlayın:

    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. Blob hizmeti için Hello günlük depolama etkinleştirin:

    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Merhaba emin tooset yapmadan Blob hizmeti için depolama ölçümlerini etkinleştirme **- MetricsType** çok`Minute`:

    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>.NET istemci-tarafı günlüğünü yapılandırma
tooconfigure istemci-tarafı .NET uygulaması için oturum .NET tanılama hello uygulamanın yapılandırma dosyasında (web.config veya app.config) etkinleştirin. Bkz: [istemci-tarafı .NET depolama istemci kitaplığı hello ile oturum](http://msdn.microsoft.com/library/azure/dn782839.aspx) ve [istemci-tarafı hello Java için Microsoft Azure depolama SDK'sı ile oturum](http://msdn.microsoft.com/library/azure/dn782844.aspx) Ayrıntılar için.

Merhaba istemci-tarafı günlük nasıl hello istemci hello isteği hazırlar ve alır ve hello yanıt işlediği hakkında ayrıntılı bilgi içerir.

Hello depolama istemci kitaplığı hello uygulamanın yapılandırma dosyasında (web.config veya app.config) belirtilen hello konumdaki istemci-tarafı günlük verilerini depolar.

### <a name="collect-a-network-trace"></a>Bir ağ izlemesi Topla
İstemci uygulamanızı çalışırken ileti Çözümleyicisi toocollect bir HTTP/HTTPS ağ izleme kullanabilirsiniz. İleti Çözümleyicisi kullanır [Fiddler](http://www.telerik.com/fiddler) hello üzerinde arka uç. Merhaba ağ izleme toplamak önce Fiddler şifrelenmemiş toorecord HTTPS trafiği yapılandırmanızı öneririz:

1. Yükleme [Fiddler](http://www.telerik.com/download/fiddler).
2. Fiddler'ı başlatın.
3. Seçin **Araçlar | Fiddler seçenekleri**.
4. Merhaba Seçenekleri iletişim kutusunda emin **yakalama HTTPS bağlanır** ve **şifresini HTTPS trafiği** her ikisi de, aşağıda gösterildiği gibi seçilir.

![Fiddler seçeneklerini yapılandırma](./media/storage-e2e-troubleshooting-classic-portal/fiddler-options-1.png)

Merhaba öğretici için toplamak ve bir ağ izlemesi ilk ileti Çözümleyicisi'nde kaydedin sonra bir analiz oturum tooanalyze hello izleme oluşturun ve günlükleri hello. İleti Çözümleyicisi'nde bir ağ izlemesi toocollect:

1. İleti Çözümleyicisi'nde seçin **dosya | Hızlı İzleme | Şifrelenmemiş HTTPS**.
2. Merhaba izleme hemen başlar. Seçin **durdurmak** toostop hello izleme böylece biz yalnızca tootrace depolama trafiği yapılandırabilirsiniz.
3. Seçin **Düzenle** tooedit hello izleme oturumu.
4. Select hello **yapılandırma** toohello hello sağındaki bağlantı **Microsoft Pef WebProxy** ETW sağlayıcı.
5. Merhaba, **Gelişmiş ayarları** iletişim kutusunda, hello tıklatın **sağlayıcı** sekmesi.
6. Merhaba, **Hostname filtre** alanında, boşlukla ayrılmış depolama noktalarınızı belirtin. Örneğin, aşağıdaki gibi noktalarınızı belirtebilirsiniz; değiştirme `storagesample` toohello depolama hesabınızın adını:

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Merhaba iletişim çıkmak ve tıklatın **yeniden** böylece yalnızca Azure depolama ağ trafiği hello izleme dahil, yerinde hello hostname filtreli hello iz toplamadan toobegin.

> [!NOTE]
> Ağ izleme toplama tamamladıktan sonra Fiddler toodecrypt HTTPS trafiği değişmiş olabilir hello ayarları geri kesinlikle öneririz. Merhaba Fiddler Seçenekleri iletişim kutusunda hello seçimini **yakalama HTTPS bağlanır** ve **şifresini HTTPS trafiği** onay kutularını.
>
>

Bkz: [hello ağ izleme özelliklerini kullanmayı](http://technet.microsoft.com/library/jj674819.aspx) daha ayrıntılı bilgi için TechNet'teki.

## <a name="review-metrics-data-in-hello-azure-classic-portal"></a>Ölçüm verilerini hello Klasik Azure Portalı'nda gözden geçirin
Uygulamanızı bir süre çalıştıran sonra hizmetiniz bir nasıl gerçekleştirmekte hello Klasik Azure portalı tooobserve görünür hello ölçümleri grafikleri gözden geçirebilirsiniz. İlk olarak, hello ekleyeceğiz **başarı oranı** ölçüm toohello izleme sayfası:

1. Depolama hesabınızdaki hello için Pano toohello gidin [Klasik Azure portalı](https://manage.windowsazure.com)seçeneğini belirleyip **İzleyici** tooview hello sayfa izleme.
2. Tıklatın **ölçüm Ekle** toodisplay hello **ölçüm Seç** iletişim.
3. Toofind hello aşağı **başarı oranı** grup, genişletin ve ardından **toplama**hello aşağıda gösterildiği gibi. Bu ölçüm, tüm Blob işlemlerinden başarı yüzdesi verileri toplar.

![Ölçümleri Seç](./media/storage-e2e-troubleshooting-classic-portal/choose-metrics-portal-1.png)

Hello Klasik Azure Portalı'da, artık göreceğiniz **başarı oranı** grafik izleme hello yanı sıra diğer bir ölçümleri eklediğiniz (toosix hello grafikte aynı anda görüntülenebilir). Merhaba resimde, o hello yüzde başarı oranı biraz biz sonraki ileti Çözümleyicisi'nde hello günlüklerini analiz araştırmak hello senaryodur %100 aşağıda olduğunu görebilirsiniz:

![Portal, ölçümleri grafik](./media/storage-e2e-troubleshooting-classic-portal/portal-metrics-chart-1.png)

Ölçümleri toohello izleme sayfası ekleme hakkında daha fazla ayrıntı için bkz: [nasıl yapılır: ölçümleri toohello ölçümleri tablo eklemek](storage-monitor-storage-account.md#add-metrics-charts-to-the-portal-dashboard).

> [!NOTE]
> Depolama ölçümleri etkinleştirdikten sonra bunu hello Klasik Azure portalı ölçümleri veri tooappear için biraz zaman alabilir. Merhaba geçerli saatte sona ermeden önceki saat hello için saatlik ölçümleri hello Klasik Azure portalı görüntülenmez olmasıdır. Ayrıca, dakika ölçümleri hello Klasik Azure portalı görüntülenmez. Bu nedenle bağlı olarak ölçümleri etkinleştirdiğinizde, tootwo saatleri toosee ölçümleri verileri alabilir.
>
>

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>AzCopy toocopy sunucu günlüklerini tooa yerel dizin kullanın
Ölçümleri tootables yazılır sırasında azure Storage server günlük veri tooblobs yazar. Merhaba iyi bilinen günlük BLOB'lar kullanılabilir `$logs` depolama hesabınız için kapsayıcı. Böylece hello tooinvestigate istediğiniz zaman aralığını kolayca bulabilir günlük BLOB'lar yıl, ay, gün ve saat tarafından hiyerarşik olarak adlandırılır. Örneğin, hello içinde `storagesample` hesabıdır 02/01/2015 ' dan 8-09: 00, hello günlük BLOB hello kapsayıcısı `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`. Bu kapsayıcıda Hello tek tek bloblar adlı ardışık olarak itibaren `000000.log`.

Bu sunucu tarafı günlük dosyaları tooa konumu tercih ettiğiniz hello AzCopy komut satırı aracı toodownload yerel makinenizde kullanabilirsiniz. Merhaba sürdü blobu işlemleri yerleştirmek için aşağıdaki komutu toodownload hello günlük dosyaları gibi kullanabilirsiniz 2 Ocak 2015 toohello klasörü `C:\Temp\Logs\Server`; Değiştir `<storageaccountname>` depolama hesabınızın hello adla ve `<storageaccountkey>` ile Hesap erişim anahtarı:

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```

AzCopy hello üzerinde yüklenebilir [Azure indirmeleri](https://azure.microsoft.com/downloads/) sayfası. AzCopy kullanma hakkında daha fazla bilgi için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).

Sunucu tarafı günlüklerini indirme hakkında ek bilgi için bkz: [indirme depolama günlüğü günlük verileri](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata).

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Microsoft Message Analyzer tooanalyze günlük verileri kullanma
Microsoft Message Analyzer, yakalama, görüntüleme ve trafik, olaylar ve sorun giderme ve tanılama senaryolarda diğer sistem veya uygulama iletileri Mesajlaşma Protokolü çözümlemek için kullanılan bir araçtır. İleti Çözümleyicisi'ni de tooload, toplama, etkinleştirir ve günlük verileri çözümlemek ve izleme dosyaları kaydedilir. İleti Çözümleyicisi hakkında daha fazla bilgi için bkz: [Microsoft Message Analyzer işletim kılavuzu](http://technet.microsoft.com/library/jj649776.aspx).

İleti Çözümleyicisi varlıklar Azure Storage için tooanalyze sunucusu, istemci ve ağ günlükleri Yardım içerir. Bu bölümde, toouse Bu araçlar tooaddress düşük yüzde başarılı şekilde sorunun nasıl hello biz ele alacağız hello depolama günlükleri.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>İleti Çözümleyicisi ve hello Azure depolama varlıklar yükleyip
1. Karşıdan [ileti Çözümleyicisi](http://www.microsoft.com/download/details.aspx?id=44226) gelen Microsoft Download Center hello ve hello yükleyiciyi çalıştırın.
2. İleti Çözümleyicisi'ni başlatın.
3. Merhaba gelen **Araçları** menüsünde, select **varlık Yöneticisi**. Merhaba, **varlık Yöneticisi** iletişim kutusunda **indirmeleri**, sonra filtre **Azure Storage**. Hello Azure depolama varlıklar, hello aşağıda gösterildiği gibi göreceksiniz.
4. Tıklatın **eşitleme tüm görüntülenen öğelerin** tooinstall hello Azure depolama varlıklar. Merhaba kullanılabilir varlıklar şunları içerir:
   * **Azure depolama renk kurallarını:** Azure depolama renk kurallarını etkinleştirin, metin, bir renk kullanan toodefine özel filtreler ve yazı tipi stilleri bir izleme belirli bilgiler içeren toohighlight iletileri.
   * **Azure depolama grafikler:** Azure depolama grafikleri olan sunucu günlüğü verileri grafik önceden tanımlanmış grafikler. Şu anda Azure Storage toouse grafikleri, yalnızca yük hello server günlüğünü analiz kılavuz hello olabilir dikkat edin.
   * **Azure depolama ayrıştırıcıları:** hello Azure Storage ayrıştırıcıları ayrıştırma hello Azure Storage istemci, sunucu ve HTTP günlükleri sipariş toodisplay bunları hello analiz kılavuz.
   * **Azure depolama filtreler:** Azure depolama filtreleridir önceden tanımlanmış ölçütleri tooquery hello analiz kılavuz verilerinizi kullanabilirsiniz.
   * **Azure depolama görünüm düzenler:** Azure depolama görünüm düzenler: önceden tanımlanmış sütun düzenleri ve hello analiz Kılavuz içindeki gruplandırmalar.
5. Merhaba varlıklar yükledikten sonra ileti Çözümleyicisi'ni yeniden başlatın.

![İleti Çözümleyicisi varlık Yöneticisi](./media/storage-e2e-troubleshooting-classic-portal/mma-start-page-1.png)

> [!NOTE]
> Tüm hello Bu öğreticinin amaçları doğrultusunda gösterilen hello Azure Storage varlıklar yükleyin.
>
>

### <a name="import-your-log-files-into-message-analyzer"></a>Günlük dosyalarınızın ileti çözümleyicisine alma
Tüm kaydedilmiş günlük dosyalarınızı (sunucu tarafı, istemci tarafı ve ağ), Microsoft Message Analyzer tek bir oturumda çözümleme için içine aktarabilirsiniz.

1. Merhaba üzerinde **dosya** Microsoft Message Analyzer'nde menüsünü **yeni oturum**ve ardından **boş oturum**. Merhaba, **yeni oturum** iletişim kutusunda, analiz oturumunuz için bir ad girin. Merhaba, **oturumun ayrıntılarına** paneli, üzerinde hello tıklatın **dosyaları** düğmesi.
2. İleti Çözümleyicisi tarafından oluşturulan tooload hello ağ izleme verilerini tıklayın **dosyaları Ekle**, kaydettiğiniz .matp dosyanızı, web izleme oturumunuzda, select hello .matp dosya toohello konumunu bulun ve tıklatın **açın**.
3. tooload hello sunucu tarafı günlük verilerini tıklayın **dosyaları Ekle**, sunucu tarafı günlüklerinizi indirdiğiniz toohello konumunu bulun, seçin tooanalyze istediğiniz ve tıklatın hello zaman aralığı için hello günlük dosyalarını **açmak**. Ardından hello **oturumun ayrıntılarına** paneli, kümesi hello **metin günlüğü Yapılandırması** her sunucu tarafı günlük dosyası için çok açılan**AzureStorageLog** tooensure Microsoft İleti Çözümleyicisi hello günlük dosyası doğru ayrıştıramıyor.
4. tooload hello istemci-tarafı günlük verilerini tıklayın **dosyaları Ekle**, istemci-tarafı günlüklerinizi kaydettiğiniz toohello konumunu bulun, seçin tooanalyze istediğiniz ve tıklatın hello günlük dosyalarını **açık**. Ardından hello **oturumun ayrıntılarına** paneli, kümesi hello **metin günlüğü Yapılandırması** her istemci-tarafı günlük dosyası için çok açılan**AzureStorageClientDotNetV4** tooensure, Microsoft Message Analyzer hello günlük dosyası doğru ayrıştıramıyor.
5. Tıklatın **Başlat** hello içinde **yeni oturum** iletişim tooload ve ayrıştırma hello günlük verileri. Merhaba ileti Çözümleyicisi çözümleme kılavuz Hello günlük verilerini görüntüler.

Sunucu, istemci ve ağ izleme günlük dosyaları ile yapılandırılmış bir örnek oturumu Hello resimde gösterilmektedir.

![İleti Çözümleyicisi oturum yapılandırma](./media/storage-e2e-troubleshooting-classic-portal/configure-mma-session-1.png)

İleti Çözümleyicisi belleğe günlük dosyalarını yükler unutmayın. Çok sayıda günlük verileri varsa, toofilter isteyeceksiniz sipariş tooget hello en iyi performansı Message Analyzer içinde.

İlk olarak, gözden geçirme ilgilendiğiniz hello zaman çerçevesi belirlemek ve bu zaman dilimi olabildiğince küçük tutun. Çoğu durumda tooreview dakika veya en çok saat dilimi isteyeceksiniz. Merhaba küçük gereksinimlerinizi karşılayan günlükleri kümesini içeri aktarın.

Büyük miktarda günlük veri hala varsa, bu yükleme önce sonra toospecify oturum filtre toofilter günlük verilerinizi isteyebilirsiniz. Merhaba, **oturum filtre** kutusu, select hello **Kitaplığı** düğmesini toochoose önceden tanımlanmış bir filtre; Örneğin, tercih **genel zaman filtresi ı** Azure Storage filtreler hello gelen bir zaman aralığı üzerinde toofilter. Merhaba filtre ölçütü toospecify hello başlangıç sonra düzenleyebilirsiniz ve zaman damgası başlangıç aralığı için bitiş toosee istiyorsunuz. Bir özel durum kodu de filtre uygulayabilirsiniz; Örneğin, hello durum kodu 404 olduğu tooload yalnızca günlük girişlerini seçebilirsiniz.

Microsoft Message Analyzer günlük verilerini alma hakkında daha fazla bilgi için bkz: [ileti verilerini alma](http://technet.microsoft.com/library/dn772437.aspx) TechNet'te.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Merhaba istemci istek kimliği toocorrelate günlük dosyası verilerini kullanın
Hello Azure Storage istemci kitaplığı, benzersiz istemci istek kimliği her istek için otomatik olarak oluşturur. İleti Çözümleyicisi içindeki tüm üç günlüklerini arasında toocorrelate veri kullanabilmek için bu değeri toohello istemci günlüğü, hello sunucu günlüğü ve hello ağ izleme, yazılır. Bkz: [istemci istek kimliği](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) hello istemci hakkında ek bilgi için kimliği isteyin.

Merhaba aşağıdaki önceden yapılandırılmış toouse ve toocorrelate ve grup verilerini hello istemci isteği temel alarak özel yerleşim görünümlerin nasıl kimliği bölümlerde

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>Hello analiz Izgara Görünümü düzeni toodisplay seçin
İleti Çözümleyicisi için Hello depolama varlıkların önceden yapılandırılmış görünümler, toodisplay verilerinizi yararlı gruplandırmaları ve sütunlarla farklı senaryolar için kullanabileceğiniz Azure depolama görünüm düzenleri içerir. Ayrıca, özel görünüm düzenleri oluşturabilir ve bunları yeniden kullanmak üzere kaydedin.

Merhaba resimde gösterilmektedir hello **görünüm düzeni** menüsünde seçerek kullanılabilir **görünüm düzeni** hello araç şeridinden. Azure Storage için Hello görünüm düzenleri hello altında gruplandırılır **Azure Storage** hello menüde düğümü. Arayabilirsiniz `Azure Storage` hello arama kutusu toofilter Azure depolama üzerinde yalnızca düzenleri görüntüleyin. Merhaba yıldız sonraki tooa görünüm düzeni toomake öğesini de seçebilirsiniz sık kullanılan bir BT ve başlangıç menüsünde hello üstünde görüntüle.

![Düzen menüsü görüntüleme](./media/storage-e2e-troubleshooting-classic-portal/view-layout-menu.png)

ile select toobegin **ClientRequestID ve modül göre gruplandırılmış**. Bu görünüm düzeni üç günlüğü verileri ilk istemci istek kimliği, sonra bir kaynak günlük dosyasını günlük (veya **Modülü** ileti Çözümleyicisi). Bu görünüm ile belirli bir istemci istek kimliği detaya ve tüm üç günlük dosyaları için istemci istek kimliği verilerden bakın

Merhaba resimde bu düzeni görünüm uygulanmış toohello örnek günlük verileri, görüntülenen bir sütun alt kümesini gösterir. Belirli bir istemci istek kimliği için hello istemci günlüğü, sunucu günlüğü ve ağ izleme verilerini hello analiz kılavuz görüntüler görebilirsiniz.

![Azure depolama görünüm düzeni](./media/storage-e2e-troubleshooting-classic-portal/view-layout-client-request-id-module.png)

> [!NOTE]
> Farklı günlük dosyaları farklı sütuna sahip birden çok günlük dosyalarından veri hello analiz kılavuz görüntülendiğinde, belirli bir satır için herhangi bir veri bazı sütunları içermeyebilir şekilde. Örneğin, yukarıdaki hello resim istemci günlük satırları hello için herhangi bir veri gösterme **zaman damgası**, **TimeElapsed**, **kaynak**, ve **hedef** sütunları, çünkü bu sütunlar hello istemci günlüğünde yok ancak hello ağ izlemesinde mevcut. Benzer şekilde, hello **zaman damgası** sütunu zaman damgası veri hello sunucu günlüğünden görüntüler, ancak hiçbir veri Merhaba görüntülenir **TimeElapsed**, **kaynak**, ve  **Hedef** hello sunucu günlüğü parçası olmayan sütunları.
>
>

Ayrıca toousing hello Azure Storage görünüm düzenleri, ayrıca tanımlamak ve kendi görünüm düzenleri kaydedin. Verileri gruplandırma diğer istediğiniz alanları seçin ve hello gruplandırma özel düzeniniz de bir parçası olarak kaydedin.

### <a name="apply-color-rules-toohello-analysis-grid"></a>Renk kurallarını toohello analiz kılavuz Uygula
Merhaba depolama varlıklar bir görsel tooidentify hello analiz kılavuz hataları farklı türlerde anlamına gelir. teklif renk kurallarını da içerir. yalnızca hello sunucu günlüğü ve ağ izleme için görüntülenecek şekilde hello önceden tanımlanmış renk kurallarını tooHTTP hatalar, geçerlidir.

tooapply renk kurallarını seçin **renk kurallarını** hello araç şeridinden. Hello Azure Storage renk kurallarını hello menüde görürsünüz. Merhaba öğreticide seçin **istemci hataları (durum kodu 400-499 arasında)**hello aşağıda gösterildiği gibi.

![Azure depolama görünüm düzeni](./media/storage-e2e-troubleshooting-classic-portal/color-rules-menu.png)

Ayrıca toousing hello Azure Storage renk kuralları, ayrıca tanımlamak ve kendi renk kurallarını kaydedin.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>Grup ve filtre veri toofind 400-range hatalarını günlüğe
Ardından, grubu ve hello günlük veri toofind hello 400 aralığındaki tüm hataları filtre.

1. Merhaba bulun **StatusCode** hello analiz kılavuz, sağ hello sütun başlığını ve select sütununda **grup**.
2. Ardından, hello üzerinde Grup **ClientRequestId** sütun. Analiz kılavuz şimdi durumu tarafından düzenlenen hello hello verilerde kod ve tarafından istemci istek kimliği görürsünüz
3. Zaten görüntülenmiyorsa, hello Görünüm filtresi araç penceresi görüntüler. Merhaba araç şeridinde seçin **aracı Windows**, ardından **Görünüm Filtresi**.
4. toofilter hello günlük veri toodisplay yalnızca 400 aralığı hataları, filtre ölçütü toohello aşağıdaki hello eklemek **Görünüm Filtresi** penceresi ve tıklatın **Uygula**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

Merhaba resimde bu gruplandırma ve filtre hello sonuçları gösterilmektedir. Genişleyen hello **ClientRequestID** bu durum kodunda sonuçlanan bir işlem gösterir Durum kodu için 409, örneğin, gruplandırma hello alan.

![Azure depolama görünüm düzeni](./media/storage-e2e-troubleshooting-classic-portal/400-range-errors1.png)

Bu filtre uygulandıktan sonra göreceğiniz hello istemci günlüğü satırları dışlanır, hello istemci günlüğü içermemesi bir **StatusCode** sütun. toobegin ile biz hello sunucu ve ağ izleme günlükleri toolocate 404 hataları gözden geçirin ve ardından toothem eden toohello istemci günlük tooexamine hello istemci işlemleri getireceğiz.

> [!NOTE]
> Merhaba üzerinde filtreleyebilirsiniz **StatusCode** sütun ve yine de dahil olmak üzere, tüm üç günlükleri görüntüleme verilerden hello durum kodu olduğu null günlük girişlerini içeren bir ifade toohello filtre eklerseniz, istemci günlük hello. tooconstruct Bu filtre ifadesi kullanın:
>
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
>
> Bu filtre tüm satırları hello istemciden günlük ve yalnızca hello sunucu günlüğü ve HTTP günlüğü satırlarından hello durum kodu 400'den büyük olduğu döndürür. İstemci istek kimliği ve modül göre gruplandırılmış toohello görünüm düzeni uygularsanız, arama yapabilir veya hello arasında kaydırma günlük girişleri toofind olanları üç günlüğü burada gösterilir.   
>
>

### <a name="filter-log-data-toofind-404-errors"></a>Günlük veri toofind 404 hatalarını filtre
Merhaba depolama varlıklar toonarrow veri toofind hello hataları günlüğe veya aradığınız eğilimleri kullanabileceğiniz önceden tanımlanmış filtreler aşağıdakileri içerir. Ardından, şu iki önceden tanımlanmış filtre uygulamak: hello sunucusu ve ağ izleme günlükleri 404 hataları filtreleyen ve hello verileri belirtilen zaman aralığı üzerinde filtreleyen bir.

1. Zaten görüntülenmiyorsa, hello Görünüm filtresi araç penceresi görüntüler. Merhaba araç şeridinde seçin **aracı Windows**, ardından **Görünüm Filtresi**.
2. Merhaba Görünüm Filtresi penceresinde seçin **Kitaplığı**ve arama `Azure Storage` toofind hello Azure Storage filtreler. Select hello filtresini **404 (bulunamadı) tüm günlüklerde iletileri**.
3. Görüntü hello **Kitaplığı** menü yeniden bulun ve seçin hello **genel zaman filtresi**.
4. Merhaba zaman damgaları tooview istediğiniz Hello filtre toohello aralığında gösterilen düzenleyin. Bu, veri tooanalyze toonarrow hello aralığı yardımcı olur.
5. Filtre aşağıdaki benzer toohello örnek görüntülenmesi gerekir. Tıklatın **Uygula** tooapply hello filtre toohello analiz kılavuz.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

![Azure depolama görünüm düzeni](./media/storage-e2e-troubleshooting-classic-portal/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>Günlük verileri analiz etme
Gruplandırılmış ve verilerinizi filtre göre üretilen 404 hatalarını tek tek isteklerin hello ayrıntıları inceleyebilirsiniz. Merhaba geçerli görünümü düzende hello veri günlüğü kaynağı tarafından sonra istemci istek kimliği göre gruplandırılır. Biz isteklerinde, 404 hello StatusCode alan içerdiği filtre olduğundan, yalnızca hello sunucu ve ağ izleme verilerini, hello istemci günlük verileri değil göreceğiz.

Merhaba resimde belirli bir istek hello blob mevcut olmadığından bir Blob alma işlemi bir 404 burada verdiğini gösterir. Bazı sütunları görünümden hello standart sipariş toodisplay hello ilgili verileri kaldırılmış unutmayın.

![Filtrelenen sunucu ve ağ izleme günlükleri](./media/storage-e2e-troubleshooting-classic-portal/server-filtered-404-error.png)

Ardından, biz bu istemci istek kimliği hello istemci günlük veri toosee ile Merhaba hata oluştuğunda hangi eylemleri hello istemci sürüyordu ilişkilendirilmesi. İkinci bir pencerede açılır bu oturumu tooview hello istemci günlük verileri için yeni bir analiz Izgara Görünümü görüntüleyebilirsiniz:

1. İlk olarak, hello hello değerini kopyalayın **ClientRequestId** alan toohello Pano. Her iki satır seçerek hello bulma bunu yapabilirsiniz **ClientRequestId** hello veri değeri sağ tıklayarak ve seçme alan **Kopyala 'ClientRequestId'**.
2. Merhaba araç şeridinde seçin **yeni Viewer**seçeneğini belirleyip **analiz kılavuz** tooopen yeni sekmesini hello yeni bir sekme gösteren tüm verileri gruplandırma, filtre veya renk kurallarını olmadan, günlük dosyalarında.
3. Merhaba araç şeridinde seçin **görünüm düzeni**seçeneğini belirleyip **tüm .NET istemci sütunları** hello altında **Azure Storage** bölümü. Bu görünüm düzeni, sunucu ve ağ izleme günlükleri hello istemci günlüğü ve bunun yanı sıra hello verileri gösterir. Varsayılan olarak üzerinde hello sıralanır **MessageNumber** sütun.
4. İleri arama hello istemci günlüğü hello istemci istek kimliği için Merhaba araç şeridinde seçin **iletileri Bul'u**, hello hello istemci istek kimliği üzerinde bir özel filtre belirtmek **Bul** alan. Kendi istemci istek kimliği belirtme hello filtre için aşağıdaki sözdizimini kullanın:

    ```  
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

İleti Çözümleyicisi'ni bulur ve burada hello arama ölçütleriyle eşleşen hello istemci istek kimliği hello ilk günlük girişi seçer Merhaba istemci günlüğüne vardır her istemci istek kimliği için birden çok girişi toogroup isteyebilirsiniz hello uygulamaları **ClientRequestId** alan toomake bunu daha kolay toosee hepsini bir araya bunları. Merhaba resmin tüm hello İstemcisi'nde hello iletilerinin Merhaba günlük gösterir altında istemci istek kimliği belirtildi.

![İstemci günlük gösteren 404 hataları](./media/storage-e2e-troubleshooting-classic-portal/client-log-analysis-grid1.png)

Bu iki sekme hello görünüm düzenleri gösterilen hello verileri kullanarak ne hello hataya neden hello isteği veri toodetermine çözümleyebilirsiniz. Ayrıca, önceki bir olayı toohello 404 hatası neden, bu bir toosee öncesinde isteklerinin da bakabilirsiniz. Örneğin, bu istemci istek kimliği toodetermine hello blob silinmiş olup olmadığını veya hello hata nedeniyle bir kapsayıcı veya blob CreateIfNotExists API çağırma toohello istemci uygulaması ise önceki hello istemci günlük girişlerini gözden geçirebilirsiniz. Merhaba istemci günlüğünde hello hello blob'un adresi bulabilirsiniz **açıklama** alan; hello sunucu ve ağ izleme günlükleri, bu bilgileri hello görünür **Özet** alan.

Başlangıç adresi hello 404 hatası verdiğini hello BLOB öğrendikten sonra daha fazla araştırabilirsiniz. Merhaba günlük girişlerini ile ilişkili diğer iletiler için arama yaparsanız hello işlemleri aynı blob, hello istemci hello varlık daha önce silinmiş olup olmadığını denetleyin.

## <a name="analyze-other-types-of-storage-errors"></a>Başka tür depolama hataları çözümleme
İleti Çözümleyicisi tooanalyze günlük verilerinizi kullandıysanız, başka tür görünümünü kullanarak hataları çözümleyebilirsiniz düzenleri, renk kurallarını ve arama ve filtreleme. Merhaba tabloları listelerde bazı sorunlar karşılaşırsanız ve toolocate kullanabileceğiniz filtreleme ölçütlerini hello bunları. Dil filtresi filtreleri ve hello ileti Çözümleyicisi oluşturma hakkında daha fazla bilgi için bkz [ileti verileri filtreleme](http://technet.microsoft.com/library/jj819365.aspx).

| tooInvestigate... | Filtre ifadesi kullan... | İfade uygulanacağı tooLog (istemci, sunucu, ağ, tüm) |
| --- | --- | --- |
| Bir kuyruk iletisi Teslimde beklenmeyen gecikme |"Yeniden deneniyor, işlem başarısız oldu." AzureStorageClientDotNetV4.Description içerir |İstemci |
| HTTP PercentThrottlingError artış |HTTP. Response.StatusCode 500 &#124; &#124; == HTTP. Response.StatusCode 503 == |Ağ |
| İçinde PercentTimeoutError artırın |HTTP. Response.StatusCode 500 == |Ağ |
| (Tümü) PercentTimeoutError içinde artırın |* StatusCode 500 == |Tümü |
| İçinde PercentNetworkError artırın |AzureStorageClientDotNetV4.EventLogEntry.Level < 2 |İstemci |
| HTTP 403 (Yasak iletileri) |HTTP. Response.StatusCode 403 == |Ağ |
| HTTP 404 (bulunamadı) iletileri |HTTP. Response.StatusCode 404 == |Ağ |
| 404 (Tümü) |* StatusCode 404 == |Tümü |
| Paylaşılan erişim imzası (SAS) yetkilendirme sorunu |AzureStorageLog.RequestStatus "SASAuthorizationError" == |Ağ |
| HTTP 409 (Çakışma) iletileri |HTTP. Response.StatusCode 409 == |Ağ |
| 409 (Tümü) |* StatusCode 409 == |Tümü |
| Düşük PercentSuccess veya analytics günlük girişlerini ClientOtherErrors işlem durumundaki işlemlerini sahip |AzureStorageLog.RequestStatus "ClientOtherError" == |Sunucu |
| Nagle uyarı |((AzureStorageLog.EndToEndLatencyMS-AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS * 1.5)) ve (AzureStorageLog.RequestPacketSize < 1460) ve (AzureStorageLog.EndToEndLatencyMS - AzureStorageLog.ServerLatencyMS > = 200) |Sunucu |
| Sunucu ve ağ günlüklerine zaman aralığı |#Timestamp > = 2014-10-20T16:36:38 ve #Timestamp < = 2014-10-20T16:36:39 |Sunucu, ağ |
| Sunucu günlüklerindeki zaman aralığı |AzureStorageLog.Timestamp > = 2014-10-20T16:36:38 ve AzureStorageLog.Timestamp < = 2014-10-20T16:36:39 |Sunucu |

## <a name="next-steps"></a>Sonraki adımlar
Azure storage'da sorun giderme uçtan uca senaryoları hakkında daha fazla bilgi için şu kaynaklara bakın:

* [İzleme, tanılama ve Microsoft Azure Storage sorunlarını giderme](storage-monitoring-diagnosing-troubleshooting.md)
* [Depolama Analizi](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [İzleyici hello Azure Portal'da depolama hesabı](storage-monitor-storage-account.md)
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](storage-use-azcopy.md)
* [Microsoft Message Analyzer işletim kılavuzu](http://technet.microsoft.com/library/jj649776.aspx)
