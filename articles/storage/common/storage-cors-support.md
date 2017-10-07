---
title: "aaaCross-Origin kaynak paylaşımı (CORS) desteği | Microsoft Docs"
description: "Bilgi tooenable hello Microsoft Azure Storage Hizmetleri için CORS desteği nasıl."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Hello Azure Storage Hizmetleri için çıkış noktaları arası kaynak paylaşımı (CORS) desteği
Sürüm 2013-08-15'den başlayarak, hello Azure storage Hizmetleri için hello Blob, tablo, kuyruk ve Dosya Hizmetleri çıkış noktaları arası kaynak paylaşımı (CORS) destekler. CORS başka bir etki alanındaki bir etki alanı tooaccess kaynaklarına çalışan bir web uygulaması sağlayan bir HTTP özelliğidir. Web tarayıcıları uygulamak olarak bilinen bir güvenlik kısıtlama [kaynak aynı ilke](http://www.w3.org/Security/wiki/Same_Origin_Policy) arama API'leri; farklı bir etki alanındaki bir web sayfasından engelleyen CORS güvenli şekilde tooallow bir etki alanı (Merhaba kaynak etki alanı) toocall başka bir etki alanındaki API'ler sağlar. Merhaba bkz [CORS belirtimi](http://www.w3.org/TR/cors/) CORS hakkında ayrıntılı bilgi için.

CORS kuralları tek tek her hello için depolama hizmetleri çağırarak ayarlayabileceğiniz [Blob hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452235.aspx), [kuyruk hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452232.aspx), ve [tablo hizmeti özellikleriniAyarla](https://msdn.microsoft.com/library/hh452240.aspx). Ardından hello hizmetinin hello CORS kurallarını ayarladıktan sonra belirttiğiniz toohello kuralları göre izin verilip verilmeyeceğini hello hizmet karşı farklı bir etki alanından yapılan düzgün bir şekilde kimliği doğrulanmış bir isteği değerlendirilen toodetermine olacaktır.

> [!NOTE]
> CORS bir kimlik doğrulama mekanizması olmadığını unutmayın. CORS etkinleştirildiğinde bir depolama kaynağı karşı yapılan herhangi bir istek doğru kimlik imza ya da sahip olmalı veya genel kaynağı karşı yapılması gerekir.
> 
> 

## <a name="understanding-cors-requests"></a>CORS isteklerini anlama
Bir kaynak etki alanı CORS isteğinden iki ayrı isteklerinin oluşabilir:

* Merhaba hizmeti tarafından uygulanan hello CORS kısıtlamalar sorgular bir denetim öncesi isteği. Merhaba istek yöntemi olmadığı sürece Hello denetim öncesi isteği gerekli olup bir [basit yöntem](http://www.w3.org/TR/cors/), GET, HEAD veya POST anlamına gelir.
* Merhaba, istenen hello kaynak karşı yapılan gerçek isteği.

### <a name="preflight-request"></a>Denetim öncesi isteği
Merhaba denetim öncesi isteği sorguları hello hesap sahibi tarafından hello depolama hizmeti için kurulmuş CORS kısıtlamaları hello. Merhaba web tarayıcısı (veya diğer kullanıcı aracısı) gönderir hello istek üstbilgileri içeren bir seçenekleri isteği yöntemi ve kaynak etki alanı. hangi kaynak etki alanlarını belirtin, request yöntemleri CORS kuralları önceden yapılandırılmış bir kümesini temel hedeflenen hello işlemi Hello depolama hizmeti değerlendirir ve istek üstbilgileri depolama kaynağı karşı gerçek bir istekte belirtilebilir.

CORS hello hizmeti için etkinleştirilip etkinleştirilmeyeceğini ve hello denetim öncesi isteği eşleşen bir CORS kuralı ise hello hizmet (Tamam) 200 durum koduyla yanıt verir ve gerekli hello erişim denetimi üstbilgileri hello yanıtta içerir.

CORS hello hizmeti için etkin değil veya hello denetim öncesi isteği hiçbir CORS kuralıyla eşleşen hello hizmet durum kodu 403 (Yasak) ile yanıt verir.

Gerekli CORS üstbilgilerini (Merhaba kaynağı ve Access-Control-Request-Method üstbilgileri) OPTIONS isteğini içermiyor hello Merhaba, hello hizmet durum kodu 400 (Hatalı istek) ile yanıt verir.

İstenen kaynak Not hello hizmetini (Blob, kuyruk ve tablo) hello adlarla değil ve bir denetim öncesi isteği değerlendirilir. Merhaba hesap sahibi hello hesabı hizmet özellikleri hello isteği toosucceed sırada bir parçası olarak CORS etkinleştirmiş olmanız gerekir.

### <a name="actual-request"></a>Gerçek isteği
Merhaba denetim öncesi isteği kabul edilir ve hello yanıt döndürdü sonra hello tarayıcı hello depolama kaynağı karşı hello gerçek isteği gönderme. Merhaba denetim öncesi isteği reddedilir hemen hello tarayıcı hello gerçek isteği reddeder.

Merhaba gerçek isteği hello depolama hizmeti karşı normal istek olarak kabul edilir. hello kaynak üstbilgisi Hello varlığını hello isteği CORS istek olduğunu ve hello hizmet eşleştirme CORS kuralları hello denetleyecektir gösterir. Bir eşleşme bulunamazsa hello erişim denetimi üstbilgileri eklenen toohello yanıt ve geri toohello istemci gönderilir. Bir eşleşme bulunmazsa hello CORS Access-Control üstbilgileri döndürülmez.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>CORS hello Azure Storage Hizmetleri için etkinleştirme
CORS kuralları, hello hizmet düzeyinde ayarlanır, tooenable gerekir ya da her hizmet için (Blob, kuyruk ve tablo) CORS devre dışı bırakmak için ayrı olarak. Varsayılan olarak, her hizmet için CORS devre dışıdır. CORS tooenable, gereksinim duyduğunuz sürüm 2013-08-15 kullanarak tooset hello uygun hizmet özellikleri veya sonraki bir sürümü ve CORS kuralları toohello hizmet özellikleri ekleyin. Hakkında ayrıntılar için tooenable veya bir hizmet ve nasıl tooset CORS, lütfen kurallar için CORS devre dışı çok başvurmak[Blob hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452235.aspx), [kuyruk hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452232.aspx), ve [tablo ayarlayın Hizmet Özellikleri](https://msdn.microsoft.com/library/hh452240.aspx).

Hizmet özelliklerini ayarlama işlemi belirtilen tek bir CORS kural örneği şöyledir:

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Merhaba CORS kurala dahil her öğe aşağıda açıklanmıştır:

* **AllowedOrigins**: toomake izin verilen hello kaynak etki alanlarının bir isteğine hello depolama karşı hizmet CORS. Merhaba kaynak etki alanı hangi hello İsteğin kaynaklandığı hello etki alanıdır. Merhaba kaynak tam büyük/küçük harfe eşleşme hello kullanıcı yaş toohello hizmeti gönderir hello kaynağına sahip olması gerektiğini unutmayın. Ayrıca hello joker karakterini kullanabilirsiniz ' *' tooallow CORS aracılığıyla tüm kaynak etki alanları toomake istekleri. Merhaba yukarıdaki örnekte, etki alanları hello [http://www.contoso.com](http://www.contoso.com) ve [http://www.fabrikam.com](http://www.fabrikam.com) CORS kullanarak hello hizmet isteklerinde yapabilirsiniz.
* **AllowedMethods**: hello yöntemleri (HTTP isteği fiiller) bu hello kaynak etki alanı için CORS istek kullanabilir. Merhaba yukarıdaki örnekte, yalnızca PUT ve GET isteklerini izin verilir.
* **AllowedHeaders**: hello istek üstbilgileri bu hello kaynak etki alanı hello CORS isteğini belirtebilir. Merhaba yukarıdaki örnekte, x-ms-meta veri ile x-ms-meta-hedef ve x-ms-meta-abc başlayan tüm meta veri üstbilgileri izin verilir. Bu hello joker karakter Not ' *' hello herhangi üstbilgi başlayarak önek verilir belirtilen gösterir.
* **ExposedHeaders**: hello tarayıcı toohello isteği veren tarafından kullanıma sunulan ve hello yanıt toohello CORS istekte gönderilen olabilir yanıt üstbilgilerini hello. Yukarıdaki hello tarayıcı hello örnekte belirtildiği tooexpose herhangi üst bilgisi x-ms-meta ile başlangıçtır.
* **MaxAgeInSeconds**: hello maksimum zaman hello denetim öncesi seçenekleri isteği bir tarayıcı önbellek.

Hello Azure depolama belirten önekli üstbilgileri hem hello için Destek Hizmetleri **AllowedHeaders** ve **ExposedHeaders** öğeleri. tooallow üstbilgileri kategorisi, ortak bir önek toothat kategorisi belirtebilirsiniz. Örneğin, belirten *x-ms-meta** gibi önekli üst bilgisi x-ms-meta ile başlayan tüm üstbilgileri eşleşecek bir kural oluşturur.

aşağıdaki sınırlamalar hello tooCORS kurallar geçerlidir:

* Depolama Birimi hizmetini (Blob, tablo ve Kuyruk) başına CORS kuralları toofive belirtebilirsiniz.
* XML etiketleri hariç tüm CORS kuralları ayarları hello isteğinde Hello en büyük boyutu 2 KB aşamaz.
* bir izin verilen üst bilgi, sunulan üstbilgisi veya izin verilen kaynağı Hello uzunluğu 256 karakteri aşamaz.
* İzin verilen üstbilgileri ve sunulan üstbilgileri ya da olabilir:
  * Değişmez değer üst bilgiler, burada hello tam üstbilgi adı sağlanır, gibi **x-ms-meta-işlenen**. En fazla 64 değişmez değer üstbilgileri hello isteğinde belirtilebilir.
  * Üst bilgiler, burada bir önek hello üstbilgisinin sağlanır, gibi önekli **x-ms-meta-data***. Bu şekilde bir önek belirtme izin verir veya önek verilen hello ile başlayan herhangi bir başlığını kullanıma sunar. En fazla iki önekli üstbilgi hello isteğinde belirtilebilir.
* hello belirtilen yöntemleri (veya HTTP fiilleri) Hello **AllowedMethods** öğesi Azure depolama hizmeti API tarafından desteklenen toohello yöntemleri uygun olmalıdır. Desteklenen yöntemler, silme, GET, HEAD, birleştirme, POST, seçenekleri ve PUT ' tur.

## <a name="understanding-cors-rule-evaluation-logic"></a>CORS kural değerlendirme mantığı anlama
Bir depolama birimi hizmeti denetim öncesi ya da gerçek bir istek aldığında, hello uygun hizmet özelliklerini ayarlama işlemi aracılığıyla hello hizmeti için oluşturulan hello CORS kurallar temel alınarak bu isteği değerlendirir. CORS kuralları hello istek gövdesinde hello hizmet özelliklerini ayarlama işlemi ayarlanan hello sırayla değerlendirilir.

CORS kuralları aşağıdaki gibi değerlendirilir:

1. İlk olarak, hello kaynak etki alanı hello isteğinin hello etki alanları için hello listelenen karşılaştırılarak **AllowedOrigins** öğesi. Merhaba kaynak etki alanı hello listesinde bulunan ya da tüm etki alanları hello joker karakter izin verilen ' *', değerlendirme kazançlar kuralları. Merhaba kaynak etki alanı dahil edilmezse, hello isteği başarısız olur.
2. Ardından, hello isteğinin hello yöntemi (veya HTTP fiili) hello listelenen hello yöntemleri karşılaştırılarak **AllowedMethods** öğesi. Merhaba yöntemi hello listesinde yer alıyorsa kuralları değerlendirme devam eder; Aksi durumda, hello isteği başarısız olur.
3. Merhaba isteği, kaynak etki alanı ve onun yöntemi kuralında eşleşiyorsa, bu kural seçilen tooprocess hello istek ve başka hiçbir kural değerlendirilir. Merhaba istek başarılı olabilmesi için önce ancak hello istekte belirtilen üstbilgileri hello listelenen hello üstbilgileri karşı denetlenir **AllowedHeaders** öğesi. Gönderilen Merhaba üstbilgileri üstbilgileri izin hello eşleşmiyorsa hello isteği başarısız olur.

Merhaba kuralları hello istek gövdesinde hello sırada işlenir olduğundan, en iyi yöntemler böylece bunlar ilk olarak değerlendirilir hello en kısıtlayıcı kurallarıyla tooorigins hello listede ilk saygı belirtilmesi önerilir. Daha az kısıtlayıcı – Örneğin, bir kural tooallow kuralları – hello listesi hello sonunda tüm kaynaklara belirtin.

### <a name="example--cors-rules-evaluation"></a>Örnek – değerlendirme CORS kuralları
Merhaba aşağıdaki örnek bir işlem tooset CORS kuralları hello depolama hizmetleri için bir kısmi istek gövdesi gösterir. Bkz: [Blob hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452235.aspx), [kuyruk hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452232.aspx), ve [tablo hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452240.aspx) hello isteği oluşturma hakkında bilgi.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

Ardından, CORS isteklerini aşağıdaki hello göz önünde bulundurun:

| İstek |  |  | Yanıt |  |
| --- | --- | --- | --- | --- |
| **Yöntemi** |**Kaynak** |**İstek üstbilgileri** |**Kural eşleştirme** |**Sonuç** |
| **PUT** |http://www.contoso.com |x-ms-blob-content-type |İlk kural |Başarılı |
| **AL** |http://www.contoso.com |x-ms-blob-content-type |İkinci kuralı |Başarılı |
| **AL** |http://www.contoso.com |x-ms-istemci-request-id |İkinci kuralı |Hata |

Merhaba ilk istek hello ilk kuralıyla eşleşen – hello kaynak etki alanı kaynakları izin hello eşleşir, hello yöntemi yöntemlerine izin hello eşleştirir ve hello üstbilgi üstbilgileri – izin hello eşleşen ve böylece başarılı.

Merhaba yöntemi yöntemlerine izin hello eşleşmediğinden hello ikinci isteği hello ilk kural eşleşmiyor. Başarılı şekilde hello ikinci kural, ancak eşleşen.

Daha fazla kural değerlendirilir şekilde hello üçüncü isteği yöntemi ve kaynak etki alanı içinde hello ikinci kuralı eşleşir. Ancak, hello *x-ms-istemci-request-id üstbilgi* hello üçüncü kural hello semantiği, toosucceed izin vermiş hello olgu rağmen hello isteği başarısız şekilde hello ikinci kural tarafından izin verilmiyor.

> [!NOTE]
> Bu örnek daha az kısıtlayıcı bir kural önce daha kısıtlayıcı bir gösterir, ancak genel hello en iyi toolist hello en kısıtlayıcı kurallar ilk uygulamadır.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Merhaba ayırmayı üstbilgi nasıl belirlendiğini anlama
Merhaba *ayırmayı* başlığıdır bir dizi hello tarayıcı veya kullanıcı aracısı hello sunucu tooprocess hello isteği tarafından seçilmedi hello ölçütleri hakkında öneri isteği üstbilgi alanları içeren standart bir HTTP/1.1 üstbilgi. Merhaba *ayırmayı* üstbilgisi, proxy'leri, tarayıcılar ve toodetermine kullanmak CDN'ler tarafından hello yanıt önbelleğe nasıl önbelleğe alma işlemi için temel olarak kullanılır. Ayrıntılar için bkz: hello belirtimi hello için [ayırmayı üstbilgi](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

Merhaba tarayıcı veya başka bir kullanıcı aracısı CORS istek hello yanıtı önbelleğe alır, hello kaynak etki alanı kaynak izin hello önbelleğe alınır. İkinci bir zaman etki alanı sorunlarının Merhaba depolama kaynağı için aynı istekte hello önbelleği etkin durumdayken, hello kullanıcı aracısı hello önbelleğe alınan kaynak etki alanı alır. Aksi takdirde başarılı olabilirler hello isteği başarısız oluyor şekilde hello ikinci etki alanının hello önbelleğe alınan etki alanı eşleşmiyor. Merhaba ayırmayı üstbilgisini Azure Storage belirli durumlarda, çok ayarlar**kaynak** kaynak etki hello farklıdır isteyen hello önbelleğe alındığında tooinstruct hello kullanıcı aracısı toosend hello sonraki CORS istek toohello hizmeti.

Azure depolama ayarlar hello *ayırmayı* üstbilgisi çok**kaynak** durumlarda aşağıdaki hello içindeki gerçek GET/HEAD istekleri için:

* Ne zaman hello isteği kaynak hello tam olarak eşleşen bir CORS kuralı tarafından tanımlanan kaynak izin. tam bir eşleşme toobe hello CORS kuralı bir joker karakter içeremez ' * ' karakteri.
* Hiçbir kural eşleştirme hello istek kaynağı yoktur, ancak CORS hello depolama hizmeti için etkinleştirilir.

GET/HEAD isteği tüm kaynaklara izin veren bir CORS kuralı eşleştiği hello durumda hello yanıt tüm çıkış noktaları kullanılabilir ve hello önbellek etkinken hello kullanıcı aracısı önbellek herhangi bir kaynak etki alanı gelen sonraki istekleri sağlayacak gösterir.

Yanıtları toothese yöntemleri kullanıcı aracıları tarafından önbelleğe alınmaz beri GET/HEAD dışındaki yöntemlerle istekleri için hello depolama hizmetleri hello ayırmayı üstbilgi ayarlamaz olduğunu unutmayın.

Merhaba aşağıdaki tabloda gösterir nasıl Azure depolama hello üzerinde önceden dayalı tooGET/HEAD isteklerini belirtildiği durumlarda yanıt verir:

| İstek | Hesabı ayarı ve kural değerlendirme sonucu |  |  | Yanıt |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **İstekte mevcut kaynak üstbilgisi** |**Bu hizmet için belirtilen CORS kuralları** |**Eşleşen kural mevcut tüm kaynaklara izin veren (*)** |**Tam kaynak eşleşme için eşleşen bir kural var** |**Yanıt ayırmayı üstbilgi kümesi tooOrigin içeriyor** |**Access-Control-izin verilen-Origin yanıtı içerir: "*"** |**Access-Control-kullanıma sunulan-Headers yanıtı içerir** |
| Hayır |Hayır |Hayır |Hayır |Hayır |Hayır |Hayır |
| Hayır |Yes |Hayır |Hayır |Yes |Hayır |Hayır |
| Hayır |Evet |Evet |Hayır |Hayır |Evet |Evet |
| Evet |Hayır |Hayır |Hayır |Hayır |Hayır |Hayır |
| Evet |Evet |Hayır |Evet |Evet |Hayır |Evet |
| Evet |Evet |Hayır |Hayır |Yes |Hayır |Hayır |
| Evet |Evet |Evet |Hayır |Hayır |Evet |Evet |

## <a name="billing-for-cors-requests"></a>CORS isteklerini faturalama
Başarılı ön istekleri hesabınızın hello depolama hizmetlerinden herhangi biri için CORS etkinleştirilirse faturalandırılır (çağırarak [Blob hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452235.aspx), [kuyruk hizmeti özelliklerini ayarla](https://msdn.microsoft.com/library/hh452232.aspx), veya [ Tablo hizmeti özelliklerini ayarlama](https://msdn.microsoft.com/library/hh452240.aspx)). toominimize ücretleri göz önünde bulundurun hello ayarı **MaxAgeInSeconds** , CORS öğesinde kuralları tooa büyük değer böylece hello kullanıcı aracısı hello isteği önbelleğe alır.

Başarısız denetim öncesi isteklerde fatura değil.

## <a name="next-steps"></a>Sonraki adımlar
[Blob hizmeti özelliklerini ayarlama](https://msdn.microsoft.com/library/hh452235.aspx)

[Sıra Hizmeti özelliklerini ayarlama](https://msdn.microsoft.com/library/hh452232.aspx)

[Tablo hizmeti özelliklerini ayarlama](https://msdn.microsoft.com/library/hh452240.aspx)

[W3C çıkış noktaları arası kaynak paylaşımı belirtimi](http://www.w3.org/TR/cors/)

