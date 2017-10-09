---
title: "aaaAzure Media Services kavramları | Microsoft Docs"
description: "Bu konu Azure Media Services kavramlarına genel bir fikir veren"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Azure Media Services kavramları
Bu konuda hello en önemli Media Services kavramlara genel bakış sağlar.

## <a id="assets"></a>Varlıklar ve depolama
### <a name="assets"></a>Varlıklar
Bir [varlık](https://docs.microsoft.com/rest/api/media/operations/asset) dijital dosyaları (video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil) içerir ve bu dosyalar hakkındaki meta verileri hello. Merhaba dijital dosyalar bir varlığa karşıya yükledikten sonra hello medya kodlama ve iş akışları akış Hizmetleri'nde kullanılabilir.

Eşlenen tooa blob kapsayıcısı'hello Azure depolama hesabındaki bir varlıktır ve bu kapsayıcı blok blobları olarak hello varlık hello dosyalarında depolanır. Sayfa bloblarını Azure Media Services tarafından desteklenmiyor.

Hangi medya içerik tooupload ve bir varlığı deposunda ilgili önemli noktalar aşağıdaki hello uygulamak karar verirken:

* Bir varlık yalnızca bir tek, benzersiz örneği medya içeriği içermelidir. Örneğin, bir tek düzen TV bölüm, film veya reklam.
* Bir varlık, birden çok yorumlama veya bir görsel ve işitsel dosyasının düzenlemeleri içeremez. Bir varlığın yanlış bir kullanım örneği toostore birden fazla TV bölüm, tanıtım veya bir varlık içindeki tek bir üretimden birden fazla Kamera Açısı girişimi. Birden çok yorumlama veya düzenlemeleri görsel ve işitsel bir dosyanın bir varlığı depolama akış ve daha sonra iş akışında hello hello varlık hello teslimini güvenli hale getirme kodlama işlerini göndermenin sorunlar neden olabilir.  

### <a name="asset-file"></a>Varlık dosyası
Bir [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) bir blob kapsayıcısında depolanan asıl ses veya video dosyası temsil eder. Bir varlık dosyası her zaman bir varlıkla ilişkilidir ve bir varlığı bir veya daha çok dosyalar içerebilir. bir varlık dosyası nesne bir blob kapsayıcısında dijital bir dosyayla ilişkili değilse hello Media Services Kodlayıcısı görev başarısız olur.

Merhaba **AssetFile** örneği ve hello gerçek medya dosyası olan iki farklı nesneler. Merhaba medya dosyası hello gerçek medya içeriği içerirken hello AssetFile örneği hello medya dosyası hakkındaki meta verileri içerir.

Medya hizmeti API'ları kullanmadan Media Services tarafından oluşturulan blob kapsayıcıları toochange Merhaba içeriğine denememeniz gerekir.

### <a name="asset-encryption-options"></a>Varlık şifreleme seçenekleri
İçerik Hello türüne bağlı olarak tooupload, depolama ve teslim istediğiniz, Media Services aralarından seçim yapabileceğiniz çeşitli şifreleme seçenekleri sağlar.

>[!NOTE]
>Şifreleme kullanılmaz. Merhaba varsayılan değer budur. Bu seçenek kullanıldığında, içeriğinizin aktarım veya deposunda kalan korunmaz.

Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçenek tooupload içeriğinizi kullanın.

**StorageEncrypted** – bu seçenek tooencrypt Temizle içeriğinizi AES 256 bit şifreleme kullanarak yerel olarak kullanın ve tooAzure depolanır depolama şifrelenen karşıya yükleyin. Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir. Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızın güçlü şifrelemeyle diskte rest toosecure istediğiniz durumdur. 

Sipariş toodeliver depolama şifrelenmiş varlık'da, Media Services toodeliver içeriğinizi nasıl istediğiniz bilmesi için hello varlığın teslim ilkesini yapılandırmanız gerekir. Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini (örneğin, AES, PlayReady veya şifreleme) belirtildi. 

**CommonEncryptionProtected** -tooencrypt (veya karşıya yükleme zaten şifrelenmiş) içerik ortak şifreleme veya PlayReady DRM (örneğin, PlayReady DRM ile korunan kesintisiz akış) istiyorsanız bu seçeneği kullanın.

**EnvelopeEncryptionProtected** – tooprotect (veya zaten korumalı karşıya yükleme) istiyorsanız bu seçeneği kullanın HTTP canlı akışı (Gelişmiş Şifreleme Standardı (AES ile) şifrelenmiş HLS). Zaten AES ile şifrelenmiş HLS yüklüyorsanız bu Transform Manager tarafından şifrelenmiş gerekir.

### <a name="access-policy"></a>Erişim İlkesi
Bir [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) (örneğin, okuma, yazma ve liste) izinler ve erişim tooan varlık süreyi tanımlar. Bir varlığı bulunan kullanılan tooaccess hello dosyalara sonra olacak bir AccessPolicy nesne tooa Bulucu genellikle geçirirsiniz.

>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

### <a name="blob-container"></a>BLOB kapsayıcısı
Bir blob kapsayıcı BLOB'lar kümesinin bir gruplandırma sağlar. BLOB kapsayıcıları Media Services'de, erişim denetimi ve paylaşılan erişim imzası (SAS) bulucular varlıklar üzerinde sınır noktası olarak kullanılır. Bir Azure Storage hesabı sınırsız sayıda blob kapsayıcı içerebilir. Kapsayıcıda sınırsız sayıda blob depolanabilir.

>[!NOTE]
> Medya hizmeti API'ları kullanmadan Media Services tarafından oluşturulan blob kapsayıcıları toochange Merhaba içeriğine denememeniz gerekir.
> 
> 

### <a id="locators"></a>Belirleyicileri
[Bulucu](https://docs.microsoft.com/rest/api/media/operations/locator)s bir varlıkta bulunan dosyalara bir giriş noktası tooaccess hello sağlayın. Bir erişim ilkesi kullanılan toodefine hello izinler ve bir istemcinin varlık verilen erişim tooa olduğu süre ' dir. Bulucular bir erişim ilkesi ile birçok tooone ilişki için gibi farklı bulucular farklı başlangıç zamanlarını sağlayabilir ve bağlantı türleri toodifferent istemcileri tüm kullanırken aynı izni ve süresi ayarları hello; Ancak, Azure storage services tarafından ayarlanan bir paylaşılan erişim ilkesi kısıtlama nedeniyle, aynı anda belirli bir varlıkla ilişkilendirilen beşten fazla benzersiz bulucular sahip olamaz. 

Media Services iki tür Bulucuyu destekler: OnDemandOrigin bulucuları toostream medya (örneğin, MPEG DASH, HLS veya kesintisiz akış) kullanılan veya medya ve SAS URL bulucular, kullanılan tooupload ya da indirme medya dosyaları to\from Azure depolama aşamalı indirmek. 

>[!NOTE]
>Merhaba listesi izni (AccessPermissions.List) bir OnDemandOrigin Bulucu oluştururken kullanılmamalıdır. 

### <a name="storage-account"></a>Depolama hesabı
Tüm erişim tooAzure depolama bir depolama hesabıyla yapılır. Bir ortam hizmet hesabı bir veya daha fazla depolama hesapları ile ilişkilendirebilirsiniz. Altında 500 TB depolama hesabı başına toplam kendi boyuttur sürece bir hesapta sınırsız sayıda kapsayıcı, olabilir.  Media Services SDK düzeyi tooallow tooling sağlar, toomanage birden çok depolama hesabı ve Yük Dengelemesi varlıklarınızı hello dağıtım ölçümleri veya rastgele dağıtım göre karşıya yükleme toothese hesapları sırasında. Daha fazla bilgi için bkz. Working with [Azure Storage](https://msdn.microsoft.com/library/azure/dn767951.aspx). 

## <a name="jobs-and-tasks"></a>İşler ve görevler
A [iş](https://https://docs.microsoft.com/rest/api/media/operations/job) genellikle kullanılan tooprocess olduğu (örneğin, dizin veya kodlamak) bir ses/video sunu. Birden çok video işleme, kodlanmış her video toobe için bir proje oluşturun.

Bir işi gerçekleştirilen hello işleme toobe hakkındaki meta verileri içerir. Her işi bir veya daha fazla içeren [görev](https://docs.microsoft.com/rest/api/media/operations/task)giriş varlıklarını bir atomik işlem görevi belirtin s çıktı varlıklar, medya işlemcisi ve ilişkili ayarları. İşindeki görevleri birbirine zincirlenebilir, varlık toohello sonraki görev giriş hello çıkış varlık bir görev hello burada verilir. Bu şekilde bir iş hello işleme medya sunumu için gerekli tüm içerebilir.

## <a id="encoding"></a>Kodlama
Azure Media Services hello hello bulutta medya kodlama için birden fazla seçeneği sağlar.

Media Services ile başlıyor codec bileşenleri ve dosya biçimlerini arasındaki önemli toounderstand hello fark olur.
Codec bileşenleri hello sıkıştırma/açma algoritmaları dosya biçimleri sıkıştırılmış hello video tutan kapsayıcılar ise uygulayan hello yazılımlardır.

Media Services, toore-package bu kalmadan olmadan, bit hızı Uyarlamalı MP4 veya kesintisiz akış kodlanmış (MPEG DASH, HLS, kesintisiz akış) Media Services tarafından desteklenen akış biçimlerinde içeriği toodeliver sağlayan dinamik paketleme sağlar. Akış biçimlerine.

tootake avantajlarından [dinamik paketleme](media-services-dynamic-packaging-overview.md), en az bir standart veya premium akış uç sahip ve tooencode Ara (kaynak) dosyanızı Uyarlamalı bit hızlı MP4 veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesine gerekir. Durum başlatılır.

Media Services, bu makalede açıklanan isteğe bağlı kodlayıcılar aşağıdaki hello destekler:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium İş Akışı](media-services-encode-asset.md#media-encoder-premium-workflow)

Desteklenen kodlayıcılar hakkında daha fazla bilgi için bkz: [kodlayıcılar](media-services-encode-asset.md).

## <a name="live-streaming"></a>Canlı Akış
Azure Media Services ile bir kanal canlı akış içeriğinin işlemek için bir işlem hattı temsil eder. Bir kanal Canlı giriş akışları iki yoldan biriyle alır:

* Bir şirket içi gerçek zamanlı Kodlayıcı, Çoklu bit hızlı RTMP veya kesintisiz akış (parçalanmış MP4) toohello kanal gönderir. Çoklu bit hızlı kesintisiz akış çıkışı gerçek zamanlı kodlayıcılar aşağıdaki hello kullanabilirsiniz: MediaExcel, Ateme, düşünün iletişimleri, Envivio, Cisco ve Elemental. Merhaba şu gerçek zamanlı kodlayıcılar RTMP çıkışı: Adobe Flash Live Kodlayıcı, Telestream Wirecast, Teradek, Haivision ve Tricaster kodlayıcılar. Merhaba alınan akışların kanallardan başka kodlama dönüştürme ve kodlama geçirin. İstendiğinde, Media Services hello akış toocustomers sunar.
* Tek bit hızlı akış (biçimleri aşağıdaki hello birinde: RTP (MPEG-TS)), RTMP veya kesintisiz akış (parçalanmış MP4)) toohello kanal etkin tooperform Media Services ile kodlama Canlı gönderilir. Merhaba kanal gerçekleştirir gerçek zamanlı kodlama Merhaba gelen tek bit hızlı akış tooa Çoklu bit hızlı (Uyarlamalı) video akışına. İstendiğinde, Media Services hello akış toocustomers sunar.

### <a name="channel"></a>Kanal
Media Services [kanal](https://docs.microsoft.com/rest/api/media/operations/channel)s canlı akış içeriğinin işlemekten sorumlu. Bir giriş uç noktası bir kanal sağlar (URL alma) tooa Canlı dönüştürücü ardından sağlayın. Merhaba kanal hello Canlı dönüştürücü Canlı giriş akışları alır ve bir veya daha fazla Akış akış için kullanılabilir hale getirir. Kanal ayrıca toopreview kullanmak ve başka bir işleme ve teslimat önce akışınızı doğrulamak bir önizleme uç noktası (Önizleme URL) sağlar.

Merhaba alabilirsiniz hello kanal oluşturduğunuzda, URL ve hello Önizleme URL'sini alın. tooget bu URL'leri, başlatılan hello durumda toobe hello kanal yok. Veri canlı bir dönüştürücü hello kanal dağıtmaya hazır toostart olduğunda hello kanal başlatılması gerekir. Veri alma Hello Canlı dönüştürücü başladıktan sonra akışınızın önizlemesini.

Her Media Services hesabı birden fazla kanal, birden çok program ve birden çok akış içerebilir. Hello bant genişliği ve güvenlik gereksinimlerine bağlı olarak, ayrılmış tooone veya daha fazla kanalları StreamingEndpoint Hizmetleri olabilir. Tüm StreamingEndpoint herhangi bir kanaldan çeker.

### <a name="program-event"></a>Program (olay)
A [Program (olay)](https://docs.microsoft.com/rest/api/media/operations/program) toocontrol hello yayımlama ve canlı akıştaki kesimleri depolama sağlar. Kanallar, programları (olayları) yönetir. Merhaba kanal ve Program burada bir kanal sabit bir içerik akışının bulunduğu ve bir programın bu kanalda zaman aşımına kapsamlı toosome olay benzer tootraditional medya ilişkidir.
İstediğiniz tooretain kaydedilen hello içerik hello programı ayarını hello tarafından saatleri hello sayısını belirtebilirsiniz **ArchiveWindowLength** özelliği. Bu değer en az 5 dakika tooa en çok 25 saat ayarlayabilirsiniz.

ArchiveWindowLength hello maksimum istemcileri hello geçerli Canlı konumdan geçmişe arama süre miktarını da belirler. Merhaba belirtilen sürede programları çalıştırabilir, ancak hello pencere uzunluğunun gerisine düşen içerik sürekli olarak atılır. Bu özelliğin bu değeri bildirimleri büyüyebilir ne kadar süreyle hello istemci de belirler.

Her bir program (olay) bir varlıkla ilişkilidir. Varlık ilişkili toopublish hello program hello yönelik bir Bulucu oluşturmanız gerekir. Bu bulucuya sahip olmak tooyour istemcileri sağlayabilen bir akış URL'si toobuild olanak sağlar.

Bir kanal hello birden çok arşivini oluşturabilmesi için eşzamanlı olarak çalışan programlar toothree destekler, aynı gelen akışın. Bu, gerektiği gibi bir olay toopublish ve Arşiv farklı kısımlarını sağlar. Örneğin, iş gereksiniminiz tooarchive 6 saatlik bir program, ancak toobroadcast yalnızca son 10 dakikadır. tooaccomplish Bu, iki eşzamanlı olarak çalışan program toocreate gerekir. Bir program tooarchive hello olay 6 saatlik ayarlandı ancak hello program yayımlanamaz. Merhaba başka bir programı kümesi tooarchive 10 dakika için ve bu program yayımlanır.

Daha fazla bilgi için bkz.

* [Etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md)
* [Şirket İçi Kodlayıcılardan Çoklu Bit Hızlı Canlı Akış Alan Kanallar ile Çalışma](media-services-live-streaming-with-onprem-encoders.md)
* [Kotalar ve kısıtlamaları](media-services-quotas-and-limitations.md).

## <a name="protecting-content"></a>İçerik koruma
### <a name="dynamic-encryption"></a>Dinamik şifreleme
Azure Media Services, toosecure, depolama, işleme ve teslim üzerinden bilgisayarınıza hello çıkışında medyanızdan sağlar. Media Services, içeriğinizin dinamik olarak Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES) ve ortak şifreleme kullanarak PlayReady ve/veya Widevine DRM (CENC) ile şifrelenmiş toodeliver sağlar. Media Services de AES anahtarları ve PlayReady lisansları tooauthorized istemcileri teslim etmek için bir hizmet sunar.

Şu anda, akış biçimlerine aşağıdaki hello şifreleyebilirsiniz: HLS, MPEG DASH ve kesintisiz akış. Aşamalı indirme şifrelenemiyor.

Bir varlık için Media Services tooencrypt istiyorsanız, varlıkla tooassociate bir şifreleme anahtarı (CommonEncryption veya EnvelopeEncryption) gerekir ve ayrıca hello anahtarı için yetkilendirme ilkelerini yapılandırabilirsiniz.

Toostream depolama şifrelenmiş varlık istiyorsanız, sipariş toospecify hello varlığın teslim ilkesini yapılandırmanız gerekir nasıl Varlığınızı toodeliver istiyor.

Bir akış player tarafından istendiğinde Media Services belirtilen hello kullanan anahtar toodynamically bir zarf şifrelemeyle (AES) veya ortak şifreleme (PlayReady veya Widevine) kullanarak içeriğinizi şifreleyin. toodecrypt hello akış hello anahtar teslim hizmetinden hello anahtar hello player isteyin. tooget hello anahtar desteklemediğini hello kullanıcıdır toodecide yetkili, hello hizmet hello anahtar için belirtilen hello yetkilendirme ilkelerini değerlendirir.

### <a name="token-restriction"></a>Belirteç kısıtlama
Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açın, simge restriction ya da IP kısıtlaması. Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir. Media Services, hello basit Web belirteçleri (SWT) biçimi ve JSON Web Token (JWT) biçimlerindeki belirteçleri destekler. Media Services, güvenli belirteç hizmetleri sağlamaz. Özel bir STS oluşturabilir veya Microsoft Azure ACS tooissue belirteçleri yararlanın. Merhaba STS bir belirteci imzalayan belirtilen hello ile yapılandırılmış toocreate olmalıdır hello belirteç kısıtlamasına yapılandırmasında belirtilen anahtarı ve çıkış talep. Bu yapılandırılmış hello belirteci için eşleşme hello anahtarı (veya lisans) Hello Media Services anahtar teslim hizmeti hello istenen hello belirteci geçerliyse, anahtarı (veya lisans) toohello istemci ve hello döndürülecek talepleri.

Merhaba belirteç kısıtlamalı ilkenin yapılandırırken hello birincil doğrulama anahtarı, veren ve İzleyici parametreleri belirtmeniz gerekir. Merhaba birincil doğrulama anahtarı içeren hello hello belirteci imzalayan, veren hello belirteci veren hello güvenli belirteç hizmeti olan anahtar. Merhaba kaynak hello belirteci erişimini yetkilendirir veya (bazen kapsam denir) hello İzleyici hello belirteci hello amacı açıklanır. Merhaba Media Services anahtar teslim hizmeti bu değerleri hello belirteci hello değerleri hello şablonunda eşleştiğini doğrular.

Daha fazla bilgi için aşağıdaki makaleler hello bakın:

[İçerik genel bakış korumak](media-services-content-protection-overview.md)
[AES-128 ile koru](media-services-protect-with-aes128.md)
[DRM ile koru](media-services-protect-with-drm.md)

## <a name="delivering"></a>Teslim etme
### <a id="dynamic_packaging"></a>Dinamik paketleme
Media Services ile çalışırken, bir bit hızı Uyarlamalı MP4 içine mezzanine dosyalarınızı ayarlamak ve ardından hello dönüştürmek tooencode ayarlamak hello kullanarak toohello istenen biçimine önerilir [dinamik paketleme](media-services-dynamic-packaging-overview.md).

### <a name="streaming-endpoint"></a>Akış uç noktası
İçerik doğrudan tooa istemci oynatıcı uygulaması ya da daha fazla (Azure Media Services şimdi sağlar hello Azure CDN tümleştirme.) dağıtım için tooa içerik teslim ağı (CDN) teslim akış bir hizmeti bir StreamingEndpoint temsil hello bir akış uç noktası hizmetinden giden akış canlı akış veya isteğe bağlı varlığı Media Services hesabınızda olabilir. Media Services müşterileri seçin ya da bir **standart** uç noktası veya bir veya daha fazla akış **Premium** akış uç noktaları, tootheir gereksinimlerine göre. Akış uç noktası standart çoğu akış iş yükleri için uygundur. 

Standart Akış Uç Noktası çoğu akış iş yükü için uygundur. Standart akış uç noktaları, içerik toovirtually hello esneklik toodeliver teklif HLS, MPEG-DASH, ve kesintisiz akış dinamik paketleme ve bunun yanı sıra Microsoft PlayReady, Google Widevine, Apple Fairplay dinamik şifreleme aracılığıyla her bir aygıtı ve AES128.  Bunlar ayrıca Azure CDN tümleştirme yoluyla eşzamanlı görüntüleyiciler binlerce çok küçük toovery büyük izleyicileri'nden ölçeklendirin. Gelişmiş bir iş yükü varsa veya akış kapasite gereksinimlerinizi uç nokta üretilen iş hedeflerini akış toostandard uygun olmayan veya toocontrol hello kapasitesini istiyorsanız hello StreamingEndpoint hizmet toohandle artan bant genişliği gerekiyor, önerilir. tooallocate ölçek birimi (akış birimleri olarak da bilinen premium).

Toouse dinamik paketleme ve/veya dinamik şifreleme önerilir.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 

Daha fazla bilgi için [bu](media-services-portal-manage-streaming-endpoints.md) konu başlığına bakın.

Varsayılan olarak, Media Services hesabınızı too2 akış uç noktalarını olabilir. toorequest daha yüksek bir sınır bkz [kotaları ve kısıtlamaları](media-services-quotas-and-limitations.md).

StreamingEndpoint çalışır durumda olduğunda yalnızca faturalandırılır.

### <a name="asset-delivery-policy"></a>Varlık teslim ilkesini
Merhaba Media Services olan içerik teslim iş akışı yapılandırma hello adımlardan [varlıklar için teslim ilkeleri ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)akışı toobe istiyor. Merhaba varlık teslim ilkesini Media Services nasıl teslim, varlık toobe için istediğinizi söyler: toodynamically istediğiniz olup olmadığına bakılmaksızın hangi akış protokolüne Varlığınızı dinamik olarak (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü için), paketlenmiş Varlığınızı şifrelemek ve nasıl (Zarf veya ortak şifreleme).

Varlığınızı akışı önce depolama şifrelenmiş varlık varsa, sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini belirtildi. Örneğin, toodeliver, varlık kümesi hello İlkesi türü tooDynamicEnvelopeEncryption olan Gelişmiş Şifreleme Standardı (AES) şifreleme anahtarı ile şifrelenir. tooremove depolama şifreleme ve hello Temizle, akış hello varlığı hello İlkesi türü tooNoDynamicEncryption ayarlayın.

### <a name="progressive-download"></a>Aşamalı indirme
Aşamalı indirme hello dosyanın tamamı indirilmeden önce media çalma toostart sağlar. Bir MP4 dosyası yalnızca aşamalı olarak indirebilirsiniz.

>[!NOTE]
>Bunlar için isterseniz, şifrelenmiş varlıklar şifresini toobe aşamalı indirme için kullanılabilir.

tooprovide kullanıcılarla aşamalı indirme URL'lerini, önce bir OnDemandOrigin Bulucu oluşturmanız gerekir. Merhaba Bulucu, temel yolu toohello varlık hello verir oluşturuluyor. Daha sonra tooappend hello MP4 dosyası adını de gerekir. Örneğin:

http://amstest1.Streaming.mediaservices.Windows.NET/3c5fe676-199c-4620-9B03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>Akış URL'leri
İçerik tooclients akış. Akış URL'leri tooprovide kullanıcılar, önce bir OnDemandOrigin Bulucu oluşturmanız gerekir. Merhaba Bulucu, toostream istediğiniz hello içeriği temel yolu toohello varlık hello verir oluşturuluyor. Ancak, toobe mümkün toostream bu içerik daha fazla bu yol toomodify gerekir. bildirim dosyası akış tam bir URL toohello hello Bulucu'nın yolu birleştirme gerekir tooconstruct değeri ve hello bildirimi (filename.ism) dosya adı. Ardından, /Manifest ve (gerekirse) uygun biçimde toohello Bulucu yolu ekleyin.

Ayrıca, bir SSL bağlantısı üzerinden içeriğinizin akışını sağlayabilirsiniz. toodo Bu, HTTPS ile akış URL'leri başlatma emin olun. Şu anda AMS SSL ile özel etki alanlarını desteklemiyor.  

>[!NOTE]
>Akış uç noktası içeriğinizi teslim etmek hello 10 Eylül 2014 sonra oluşturduysanız yalnızca SSL üzerinden akışını sağlayabilirsiniz. Akış URL'leri akış uç noktaları Eylül 10 sonra oluşturulan hello dayanır, hello URL "streaming.mediaservices.windows.net" (Merhaba yeni biçim) içerir. "Origin.mediaservices.windows.net" (Merhaba eski biçimi) içeren akış URL'leri SSL desteklemez. URL'niz hello eski biçiminde ve SSL üzerinden toobe mümkün toostream istediğiniz varsa, yeni bir akış uç noktası oluşturun. Yeni uç nokta toostream içeriğinizi SSL üzerinden akış hello temel alınarak oluşturulan URL kullanın.

liste aşağıdaki hello farklı akış biçimlerine açıklar ve örnekler verilmektedir:

* Kesintisiz Akış

{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest

* MPEG DASH

{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf) akış

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest(Format=mpd-Time-CSF)

* Apple HTTP canlı akış (HLS) V4

{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl) akış

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest(Format=m3u8-aapl)

* Apple HTTP canlı akış (HLS) V3

{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3) akış

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest(Format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

