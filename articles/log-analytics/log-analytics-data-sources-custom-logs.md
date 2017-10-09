---
title: "aaaCollect özel günlükleri OMS günlük analizi | Microsoft Docs"
description: "Günlük analizi, hem Windows hem de Linux bilgisayarlarda metin dosyalarından olayları toplayabilir.  Bu makalede nasıl toodefine yeni bir özel günlük ve hello kayıtları ayrıntılarını hello OMS deposunda oluşturdukları açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Günlük analizi özel günlükleri
Günlük analizi Hello özel günlükleri veri kaynağında Windows ve Linux bilgisayarlarda metin dosyalarından toocollect olayları sağlar. Birçok uygulama bilgisi tootext dosyaları Windows olay günlüğü veya Syslog gibi standart günlük hizmetlerini yerine oturum açın.  Toplandığında, her kayıt hello kullanarak tooindividual alanları hello günlüğünde ayrıştıramıyor [özel alanlar](log-analytics-custom-fields.md) günlük analizi özelliğidir.

![Özel günlük toplama](media/log-analytics-data-sources-custom-logs/overview.png)

toplanan hello günlük dosyaları toobe ölçütleri aşağıdaki hello eşleşmesi gerekir.

- Hello günlüğü, her satırda tek bir giriş olması gerekir ya da bir hello aşağıdakilerden birini hello her girişin başında biçimleri, zaman damgası eşleşen kullanın.

    YYYY-AA-GG SS: DD:<br>D.M.YYYY HH: MM: SS AM/PM <br>MON DD, YYYY SS: dd:

- Hello günlük dosyası hello dosyanın yeni girişlerle burada üzerine döngüsel güncelleştirmeleri izin vermemelidir.
- Merhaba günlük dosyası, ASCII veya UTF-8 kodlamasını kullanmanız gerekir.  UTF-16 gibi diğer biçimlere desteklenmez.

>[!NOTE]
>Günlük analizi hello günlük dosyasında yinelenen girişler varsa bunları toplar.  Ancak, hello arama sonuçları hello filtre sonuçları hello sonuç sayısından daha fazla olay show burada tutarsız olur.  Merhaba günlük toodetermine oluşturduğu Merhaba uygulaması bu davranış neden olup olmadığını doğrulayın ve mümkünse hello özel günlük koleksiyonu tanımı oluşturmadan önce adres önemli olacaktır.  
>
  
## <a name="defining-a-custom-log"></a>Özel günlük tanımlama
Yordam toodefine özel günlük dosyası aşağıdaki hello kullanın.  Özel günlük ekleme bir örnek bir kılavuz için bu makalenin toohello sonuna kaydırın.

### <a name="step-1-open-hello-custom-log-wizard"></a>1. Adım Merhaba özel günlük Sihirbazı'nı açın
Merhaba özel günlük sihirbaz hello OMS portalında çalışır ve toodefine yeni bir özel günlük toocollect sağlar.

1. Merhaba OMS portalında çok Git**ayarları**.
2. Tıklayın **veri** ve ardından **özel günlükleri**.
3. Varsayılan olarak, tüm yapılandırma değişiklikleri otomatik olarak tooall aracıları gönderilir.  Linux aracıları için bir yapılandırma dosyası toohello Fluentd veri toplayıcı gönderilir.  Bu dosyada el ile her Linux Aracısı toomodify isterseniz hello kutunun işaretini *aşağıdaki yapılandırma toomy Linux makineler Uygula*.
4. Tıklatın **Ekle +** tooopen hello özel günlük Sihirbazı.

### <a name="step-2-upload-and-parse-a-sample-log"></a>2. Adım Karşıya yükleme ve bir örnek günlük ayrıştırma
Merhaba özel günlük örneği yükleyerek başlatın.  Merhaba Sihirbazı ayrıştırma ve bu dosyada, toovalidate hello girişleri görüntüleyin.  Günlük analizi her kayıt tooidentify belirtin hello sınırlayıcı kullanır.

**Yeni satır** hello varsayılan sınırlayıcı ve her satırda tek bir giriş sahip günlük dosyaları için kullanılır.  Bir tarih ve saat hello kullanılabilir biçimlerden birinde ile başlayan Hello satır ardından belirtebilirsiniz bir **zaman damgası** birden fazla satır span girişler destekleyen sınırlayıcısı.

Bir zaman damgası ayırıcısı kullanılırsa, OMS içinde depolanan her kayıt hello TimeGenerated özelliği hello bu girişi hello günlük dosyası için belirtilen tarih ile doldurulur.  Yeni satır ayırıcı kullanılırsa, TimeGenerated tarih ve saat günlük analizi hello girişi toplanan ile doldurulur.

> [!NOTE]
> Günlük analizi, şu anda hello tarih/saat UTC zaman damgası sınırlayıcıyı kullanarak günlüğünden toplanan değerlendirir.  Bu, değiştirilen toouse hello saat dilimi hello aracısında yakında sunulacaktır.
>
>

1. Tıklatın **Gözat** ve tooa örnek dosyasını bulun.  Bu düğme Not etiketli **Dosya Seç** bazı tarayıcılarda.
2. **İleri**’ye tıklayın.
3. Merhaba özel günlük Sihirbazı'nı tanımladığı hello dosya ve liste hello kayıtları karşıya yükler.
4. Kullanılan tooidentify yeni bir kayıt olan hello sınırlayıcı ve en iyi şekilde hello kayıtları, günlük dosyasında tanımlar select hello sınırlayıcı değiştirin.
5. **İleri**’ye tıklayın.

### <a name="step-3-add-log-collection-paths"></a>3. Adım Günlük koleksiyonu yolları Ekle
Bir veya daha fazla yol hello özel günlük burada bulabilirsiniz hello aracısında tanımlamanız gerekir.  Merhaba adı için bir joker karakter içeren bir yol belirtin veya özel bir yol ve hello günlük dosyasının adını ya da sağlayabilir.  Bu, her gün veya bir dosya belirli bir boyuta ulaştığında yeni bir dosya oluşturun uygulamaları destekler.  Ayrıca, tek bir günlük dosyası için birden fazla yol sağlayabilir.

Örneğin, log20100316.txt olduğu gibi hello adı dahil başlangıç tarihi ile bir uygulama bir günlük dosyası her gün oluşturabilirsiniz. Bu tür bir oturum için bir desen olabilir *günlük\*.txt* düzeni adlandırma Merhaba uygulaması aşağıdaki tooany günlük dosyası geçerli olur.

Merhaba aşağıdaki tabloda geçerli düzeni örnekleri toospecify farklı günlük dosyaları verilmiştir.

| Açıklama | Yol |
|:--- |:--- |
| Tüm dosyaları *C:\Logs* .txt uzantısı Windows aracı |C:\Logs\\\*.txt |
| Tüm dosyaları *C:\Logs* günlüğünü ve Windows aracısında .txt uzantısı ile başlayan bir ada sahip |C:\Logs\log\*.txt |
| Tüm dosyaları */var/log/audit* Linux Aracısı .txt uzantısı ile |/var/log/audit/*.txt |
| Tüm dosyaları */var/log/audit* günlük ve Linux aracısı üzerinde .txt uzantısı ile başlayan bir ada sahip |/var/log/Audit/log\*.txt |

1. Hangi yol biçimi eklediğiniz Windows veya Linux toospecify seçin.
2. Merhaba yolunda yazıp hello tıklatın  **+**  düğmesi.
3. Merhaba işlemi, tüm ek yollar için yineleyin.

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>4. Adım. Bir ad ve açıklama hello günlüğü sağlayın
Merhaba, belirttiğiniz ad hello günlük türü için yukarıda açıklandığı gibi kullanılır.  Bu her zaman _CL toodistinguish ile özel bir günlük sona erer.

1. Merhaba günlük için bir ad yazın.  Merhaba  **\_CL** soneki otomatik olarak sağlanır.
2. İsteğe bağlı bir ekleme **açıklama**.
3. Tıklatın **sonraki** toosave hello özel günlük tanımı.

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>5. Adım. Merhaba özel günlükler toplanmakta olan doğrula
Tooan saat için günlük analizi içinde yeni bir özel günlük tooappear ilk verilerden hello yukarı sürebilir.  Hello girişleri toplamaya başlayacaktır günlükleri tanımlı hello özel oturum hello noktasından belirtilen hello yolda bulunamadı.  Merhaba özel günlük oluşturma sırasında karşıya hello girişleri bulamayacaktır ancak bulmadığı hello günlük dosyası zaten mevcut olan girişleri toplar.

Günlük analizi hello özel günlüğünden toplama başladıktan sonra bir günlük arama kayıtlarını kullanılabilir.  Merhaba özel günlük hello olarak vermiş hello adını kullan **türü** Sorgunuzdaki.

> [!NOTE]
> Merhaba aramadan Hello RawData özelliği yoksa, tooclose gerekir ve tarayıcınızı yeniden açın.
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>6. Adım. Merhaba özel günlük girişlerini ayrıştırılamıyor
Merhaba tüm günlük girişi olarak adlandırılan tek bir özellikte depolanacağı **RawData**.  Büyük olasılıkla tooseparate hello farklı bilgi parçalarını hello kayıtta depolanan ayrı ayrı Özellikler içinde her girişinde isteyeceksiniz.  Hello kullanarak bunu [özel alanlar](log-analytics-custom-fields.md) günlük analizi özelliğidir.

Merhaba özel günlük girişi ayrıştırma için ayrıntılı adımlar burada sağlanmaz.  Lütfen toohello bakın [özel alanlar](log-analytics-custom-fields.md) bu bilgi için.

## <a name="disabling-a-custom-log"></a>Özel günlük devre dışı bırakma
Özel günlük tanımı oluşturulmuş, ancak tüm koleksiyon yollar kaldırarak devre dışı bırakabilirsiniz sonra kaldıramazsınız.

1. Merhaba OMS portalında çok Git**ayarları**.
2. Tıklayın **veri** ve ardından **özel günlükleri**.
3. Tıklatın **ayrıntıları** sonraki toohello özel günlük tanımı toodisable.
4. Merhaba koleksiyonu yolların hello özel günlük tanımı için her biri kaldırın.

## <a name="data-collection"></a>Veri toplama
Günlük analizi yaklaşık her 5 dakikada her özel günlüğünden yeni girişler toplar.  Merhaba Aracısı onun yerine üzerinden topladığı her günlük dosyasına kaydeder.  Merhaba Aracısı bir süre için çevrimdışı olursa, hello Aracısı çevrimdışıyken girişler oluşturulmuş olsalar bile sonra günlük analizi girişleri son devre dışı kaldığı toplar.

Merhaba günlük girişi tüm içeriğini Hello adlı tooa tek özellik yazılır **RawData**.  Bu, analiz ve ayrı olarak tanımlayarak aranır birden fazla özelliklerini içine ayrıştıramıyor [özel alanlar](log-analytics-custom-fields.md) hello özel günlük oluşturduktan sonra.

## <a name="custom-log-record-properties"></a>Özel günlük kaydı Özellikler
Özel günlük kayıtları sağlayan ve aşağıdaki tablonun hello özelliklerinde hello hello günlük ada sahip bir türe sahip.

| Özellik | Açıklama |
|:--- |:--- |
| TimeGenerated |Tarih ve saat kaydı hello günlük analizi tarafından toplanmıştır.  Zamana bağlı bir sınırlayıcı Hello günlük kullanıyorsa, ardından bu hello girdisinden toplanan hello zamandır. |
| SourceSystem |Aracı hello kayıt türü toplandığı. <br> OpsManager – Windows aracı, ya da doğrudan bağlanın veya System Center Operations Manager <br> Linux – tüm Linux aracıları |
| RawData |Merhaba, tam metin girişi toplanır. |
| ManagementGroupName |System Center Operations yönetmek aracılar için hello yönetim grubunun adı.  Diğer aracılar için AOI - budur\<çalışma alanı kimliği\> |

## <a name="log-searches-with-custom-log-records"></a>Özel günlük kayıtları ile günlük aramalar
Özel günlükler kayıtlardan herhangi bir veri kaynağına ait kayıtları gibi hello OMS deposunda depolanır.  Bunlar, belirli bir günlüğünden toplanan arama tooretrieve kayıtlarında hello Type özelliği kullanabilmeniz için hello günlük tanımladığınızda, sağladığınız hello adıyla eşleşen bir tür gerekir.

Merhaba aşağıdaki tabloda özel günlüklerinden kayıtları almak günlük arama farklı örnekleri sağlar.

| Sorgu | Açıklama |
|:--- |:--- |
| Tür MyApp_CL = |Özel bir tüm olayları adlandırılmış MyApp_CL oturum açın. |
| Tür MyApp_CL Severity_CF = hata = |Özel bir tüm olayları adlandırılmış MyApp_CL değeriyle oturum *hata* adlı özel bir alandaki *Severity_CF*. |

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra.

> | Sorgu | Açıklama |
|:--- |:--- |
| MyApp_CL |Özel bir tüm olayları adlandırılmış MyApp_CL oturum açın. |
| MyApp_CL &#124; Burada Severity_CF "error" == |Özel bir tüm olayları adlandırılmış MyApp_CL değeriyle oturum *hata* adlı özel bir alandaki *Severity_CF*. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>Özel günlük ekleme örnek gözden geçirme
Merhaba aşağıdaki bölümde özel günlük oluşturma örneği anlatılmaktadır.  toplanmakta olan hello örnek günlük bir tarih ve saat ve ardından virgülle ayrılmış alanlar için kodu, durum ve iletinizi başlayarak her satırda tek bir giriş vardır.  Aşağıda birkaç örnek girdileri gösterilmektedir.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>Karşıya yükleme ve bir örnek günlük ayrıştırma
Biz hello günlük dosyalarının sağlayın ve bu toplama hello olayları görebilirsiniz.  Bu durumda yeni bir yeterli ayırıcısı satırıdır.  Tek bir giriş hello günlüğüne çok satırlı ancak kapsayabilir, bir zaman damgası ayırıcısı kullanılan toobe gerekir.

![Karşıya yükleme ve bir örnek günlük ayrıştırma](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>Günlük koleksiyonu yolları Ekle
Merhaba günlük dosyaları oluşturulur *C:\MyApp\Logs*.  Her gün hello desende hello tarih içeren bir ad ile yeni bir dosya oluşturulur *appYYYYMMDD.log*.  Bu günlük dosyası için yeterli bir deseni olacaktır *C:\MyApp\Logs\\\*.log*.

![Günlük koleksiyonu yolu](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>Bir ad ve açıklama hello günlüğü sağlayın
Adını kullanıyoruz *MyApp_CL* ve yazın bir **açıklama**.

![Günlük adı](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>Merhaba özel günlükler toplanmakta olan doğrula
Bir sorgu kullanırız *türü MyApp_CL =* tooreturn tüm hello toplanan günlüğünden kaydeder.

![Hiçbir özel alanlarla günlüğü sorgusu](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>Merhaba özel günlük girişlerini ayrıştırılamıyor
Özel alanlar toodefine hello kullanırız *EventTime*, *kod*, *durum*, ve *ileti* alanları ve biz hello hello farkı görebilirsiniz Merhaba sorgu tarafından döndürülen kaydeder.

![Özel alanlarla günlüğü sorgusu](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [özel alanlar](log-analytics-custom-fields.md) tooindividual alanları hello özel günlüğünde tooparse hello girişleri.
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.
