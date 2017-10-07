---
title: "aaaMedia Hizmetleri sürüm notları | Microsoft Docs"
description: "Sürüm Notları medya Hizmetleri"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Azure Media Services sürüm notları
Bu sürüm notları değişikliklerden önceki sürümlerden ve bilinen sorunlar özetler.

> [!NOTE]
> Biz toohear müşterilerimizden aldığımız istediğiniz ve, etkileyen sorunları düzeltmeye odaklanabilirsiniz. tooreport bir sorun veya soru sormak, lütfen hello sonrası [Azure Media Services MSDN Forumu].
> 
> 

## <a id="issues"></a>Şu anda bilinen sorunlar
### <a id="general_issues"></a>Media Services genel sorunları
| Sorun | Açıklama |
| --- | --- |
| Birçok ortak HTTP üst bilgilerini hello REST API sağlanmaz. |Merhaba REST API kullanarak Media Services uygulama geliştiriyorsanız, bazı ortak HTTP üstbilgi alanları Bul (CLIENT-REQUEST-ID dahil olmak üzere istek kimliği ve RETURN-CLIENT-REQUEST-ID) desteklenmez. Merhaba üstbilgileri gelecek bir güncelleştirmede eklenir. |
| Yüzde kodlama izin verilmiyor. |Media Services URL'leri içeriği (örneğin, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) akış Merhaba oluştururken hello hello IAssetFile.Name özellik değerini kullanır Bu nedenle, yüzde kodlama izin verilmiyor. Merhaba hello değerini **adı** özelliği hello aşağıdakilerden herhangi birini içeremez [yüzde kodlama-ayrılmış karakterleri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Ayrıca, yalnızca bir olabilir '.' Merhaba dosya adı uzantısı. |
| parçasıdır ListBlobs yöntemi hello hello Azure depolama SDK sürümü 3.x başarısız olur. |Media Services oluşturur SAS üzerinde hello göre URL'leri [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) sürümü. Bir blob kapsayıcısında toouse Azure depolama SDK'sı toolist BLOB'lar istiyorsanız hello kullanın [CloudBlobContainer.ListBlobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) Azure depolama SDK'sı sürüm parçası olmayan bir yöntemle 2.x. parçasıdır ListBlobs yöntemi hello hello Azure depolama SDK sürümü 3.x başarısız olur. |
| Media Services mekanizması azaltma hello kaynak kullanımı aşırı isteği toohello hizmet uygulamalar için sınırlar. Merhaba hizmet hello Hizmet kullanılamıyor (503) HTTP durum kodu döndürebilir. |Merhaba 503 HTTP durum kodunu hello hello açıklaması daha fazla bilgi için bkz [Azure Media Services hata kodları](media-services-encoding-error-codes.md) konu. |
| Varlıkları sorgulanırken ortak REST v2 sorgu sonuçları too1000 sonuçları sınırladığından aynı anda döndürülen 1000 varlıkların bir sınırı yoktur. |Toouse gerek **atla** ve **ele** (.NET) / **üst** (açıklandığı gibi REST) [bu .NET örnek](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) ve [bu REST API'si örnek](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). |
| Bazı istemciler, kesintisiz akış hello bildiriminde bir yineleme etiketi sorunu arasında gelebilir. |Daha fazla bilgi için [bu](media-services-deliver-content-overview.md#known-issues) bölüme bakın. |
| Azure Media Services .NET SDK'sı nesneleri seri hale getirilemez ve sonuç olarak Azure önbelleğe alma ile çalışmaz. |Tooserialize hello SDK AssetCollection nesne tooadd çalışırsanız, tooAzure önbelleğe alma, bir özel durum oluşur. |
| Kodlama işleri başarısız bir ileti dizeyle "Aşama: DownloadFile. Kod: System.NullReferenceException ". |Merhaba tipik kodlama tooupload giriş video dosyaları tooan varlık giriş ve teslim etme veya daha fazla kodlama işleri, varlık, başka varlık giriş değiştirmeden giriş iş akışıdır. Ancak, değiştirirseniz hello varlık (örneğin tarafından hello varlık içindeki dosyaların ekleme/silme/yeniden adlandırma) girin ve ardından sonraki işleri DownloadFile hatasıyla başarısız olabilir. Merhaba geçici bir çözüm değildir toodelete hello giriş varlık ve yeniden karşıya yüklemeniz girdi dosyaları tooa yeni varlık. |

## <a id="rest_version_history"></a>REST API sürümü geçmişi
Merhaba Media Services REST API sürümü geçmişi hakkında daha fazla bilgi için bkz: [Azure Media Services REST API Başvurusu].

## <a name="june-2017-release"></a>Haziran 2017 sürüm

Media Services destekler [Azure Active Directory (Azure AD)-tabanlı kimlik doğrulaması](media-services-use-aad-auth-to-access-ams-api.md).

> [!IMPORTANT]
> Şu anda, Media Services hello Azure erişim denetimi hizmeti kimlik doğrulama modelini destekler. Ancak, erişim denetimi yetkilendirme 1 Haziran 2018 kullanım dışı kalacaktır. Mümkün olan en kısa sürede toohello Azure AD kimlik doğrulama modeli geçirmek öneririz.

## <a name="march-2017-release"></a>Mart 2017 sürüm

Artık Azure medya standart çok kullanabilirsiniz[bit hızı Merdiveni otomatik oluşturma](media-services-autogen-bitrate-ladder-with-mes.md) hello "Uyarlamalı akış" Önayar dize kodlama bir görev oluştururken belirterek. Media Services ile akış için tooencode video istiyorsanız "Uyarlamalı akış" Merhaba önerilen hazır ' dir. Bir kodlama Önayarı toocustomize belirli senaryonuz için gerekiyorsa, ile başlayabilirsiniz [bu](media-services-mes-presets-overview.md) hazır.

Artık Azure medya standart veya Medya Kodlayıcısı Premium iş akışı çok kullanabilirsiniz[fMP4 öbekleri oluşturan bir kodlama görev oluşturma](media-services-generate-fmp4-chunks.md). 


## <a name="febuary-2017-release"></a>Febuary 2017 sürüm

Merhaba toplam kayıt sayısı hello en yüksek kota altında olsa bile 1 Nisan 2017 başlangıç 90 günden daha eski hesabınızda herhangi bir işi kaydının otomatik olarak, ilişkili görev kayıtlarını yanı sıra, silinir. Tooarchive hello iş/görevi bilgiye ihtiyacınız varsa, açıklanan hello kodu kullanabilirsiniz [burada](media-services-dotnet-manage-entities.md).

## <a name="january-2017-release"></a>Ocak 2017 sürüm

Microsoft Azure Media Services (AMS) içinde bir **akış uç noktası** içerik doğrudan tooa istemci oynatıcı uygulaması ya da daha fazla dağıtım tooa içerik teslim ağı (CDN) teslim bir akış hizmetini temsil eder. Media Services, ayrıca Azure CDN entegrasyon sağlar. Merhaba giden akış StreamingEndpoint hizmetinden canlı akış, isteğe bağlı veya aşamalı indirme Media Services hesabınızda, varlık, bir video olabilir. Her Azure Media Services hesabı varsayılan StreamingEndpoint içerir. Ek akış hello hesabı altında oluşturulabilir. Akış, 1.0 ve 2. 0'ın iki sürümü vardır. 10 Ocak 2017 ile başlayarak, yeni oluşturulan tüm AMS hesapları sürüm 2.0 içerecektir **varsayılan** StreamingEndpoint. Aynı zamanda sürüm 2.0 akış uç noktaları toothis hesabı eklemek ek olacaktır. Bu değişiklik hello var olan hesapları etkilemez; Varolan akış sürüm 1.0 olacaktır ve yükseltilmiş tooversion 2.0 olabilir. Bu değişiklikle olacaktır davranışı, faturalama ve özellik değişiklikleri (daha fazla bilgi için bkz: [bu](media-services-streaming-endpoints-overview.md) konu).

Ayrıca, hello 2.15 sürümünden başlayarak, Azure Media Services özellikleri toohello akış uç noktası varlık aşağıdaki hello eklenen: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Bu özellikleri ayrıntılı bakış için bkz: [bu](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

## <a name="december-2016-release"></a>Aralık 2016 sürüm

Azure Media Services şimdi hizmetlerinin tooaccess telemetri/ölçüm verilerini sağlar. AMS geçerli sürümü Hello Canlı kanal, StreamingEndpoint, telemetri verilerini toplamak ve Arşiv varlıklar Canlı olanak sağlar. Daha fazla bilgi için [bu](media-services-telemetry-overview.md) konu başlığına bakın.

## <a id="july_changes16"></a>Temmuz 2016 sürüm
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>Güncelleştirmeler toomanifest dosyasına (*. ISM) oluşturulan görevleri kodlama
Bir kodlama görev gönderilen tooMedia Kodlayıcısı standart ya da Azure medya Kodlayıcı olduğunda hello kodlama görev oluşturur bir [akış bildirim dosyası](media-services-deliver-content-overview.md) (* .ism) hello dosyasında çıkış varlık. Merhaba en son hizmet sürümle birlikte, bu akış bildirim dosyası hello söz dizimi güncelleştirildi.

> [!NOTE]
> bildirimi (.ism) dosya akışı hello Hello sözdizimi iç kullanım için ayrılmıştır ve sonraki sürümlerde konu toochange durumda. Lütfen değiştirmeyin veya bu dosyanın içeriğini hello yönlendirebilir.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>Yeni bir istemci bildirimi (*. ISMC) dosya hello oluşturulan bir veya daha fazla MP4 dosyaları bir kodlama görev çıktısını alır, varlık çıktı
Daha fazla bir MP4 dosyaları oluşturan bir kodlama görev hello tamamlandıktan sonra Hello en son hizmet sürümünden başlayarak, varlık ayrıca bir akış istemci bildirimi (*.ismc) dosyasını içerecek hello çıktı. Merhaba .ismc dosya dinamik akış hello performansının artırılmasına yardımcı olur. 

> [!NOTE]
> Merhaba sözdizimi hello istemci bildirimi (.ismc) dosyasının iç kullanım için ayrılmıştır ve konu toochange sonraki sürümlerde durumda. Lütfen değiştirmeyin veya bu dosyanın içeriğini hello yönlendirebilir.
> 
> 

Daha fazla bilgi için bkz: [bu](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) blogu.

### <a name="known-issues"></a>Bilinen sorunlar
Bazı istemciler, kesintisiz akış hello bildiriminde bir yineleme etiketi sorunu arasında gelebilir. Daha fazla bilgi için [bu](media-services-deliver-content-overview.md#known-issues) bölüme bakın.

## <a id="apr_changes16"></a>Nisan 2016 sürüm
### <a name="azure-media-analytics"></a>Azure medya analizi
Azure medya Hizmetleri Azure medya analizi için güçlü video gösterimi kullanıma sunuldu. Ayrıntılı bilgi için bkz: [Azure Media Services Analizi'ne genel bakış](media-services-analytics-overview.md).

### <a name="apple-fairplay-preview"></a>Apple FairPlay (Önizleme)
Apple FairPlay ile etkinleştirir, toodynamically şifrelemek, HTTP canlı akışı (HLS) içerik artık azure Media Services. AMS lisans teslimat hizmeti toodeliver FairPlay lisansları tooclients de kullanabilirsiniz. Daha ayrıntılı bilgi için bkz: [kullanım Azure Media Services tooStream HLS içeriğinizi korumalı Apple FairPlay ile ](media-services-protect-hls-with-fairplay.md).

## <a id="feb_changes16"></a>Şubat 2016 sürüm
Azure Media Services SDK .NET (3.5.3) için en son sürümünü Hello Widevine ilgili hata düzeltmesi içerir. Merhaba sorun oluştu: AssetDeliveryPolicy uygulanamadı yeniden kullanılabilir Widevine ile şifrelenmiş birden çok varlıklar. Bu hata düzeltmesi hello bir parçası olarak özelliği aşağıdaki toohello SDK eklendi: **WidevineBaseLicenseAcquisitionUrl**.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>Ocak 2016 sürüm
Kodlama ayrılan birimler tooreduce karışıklığı Kodlayıcı adlarla yeniden adlandırıldı.

Merhaba temel, standart ve Premium kodlama ayrılmış olarak yeniden adlandırıldı tooS1, S2, birimleridir ve S3 ayrılmış birimleri, sırasıyla.  Temel kodlama RUs bugün kullanan müşteriler S1 standart sırasında hello etiket Azure Portalı'nda (ve hello fatura), olarak görür ve Premium hello etiket S2 ve S3 sırasıyla görürsünüz. 

## <a id="dec_changes_15"></a>Aralık 2015 sürümü

### <a name="azure-media-encoder-deprecation-announcement"></a>Azure medya Kodlayıcı kullanımdan Duyurusu

Azure medya Kodlayıcı yaklaşık olarak 12 ay sürümündeki hello Medya Kodlayıcısı standart başlayarak kullanım dışı kalacaktır.

### <a name="azure-sdk-for-php"></a>PHP için Azure SDK
Hello Azure SDK'sı takım yayımlanan hello yeni bir sürümünü [PHP için Azure SDK](http://github.com/Azure/azure-sdk-for-php) güncelleştirmeleri ve yeni özellikleri için Microsoft Azure Media Services içeren paket. Özellikle, desteklediği en son hello artık PHP için Azure Media Services SDK'sı hello [içerik koruma](media-services-content-protection-overview.md) özellikleri: dinamik şifreleme AES ve DRM (PlayReady ve Widevine) ile birlikte ve belirteç kısıtlama olmadan. Ayrıca ölçeklendirmeyi destekler [kodlama birimleri](media-services-dotnet-encoding-units.md).

Daha fazla bilgi için bkz.

* Merhaba [PHP için Microsoft Azure Media Services SDK](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) blogu.
* Merhaba aşağıdaki [kod örnekleri](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp hızla başlamanıza alın:
  * **vodworkflow_aes.php**: Bu gösteren bir PHP dosyasıdır nasıl toouse AES-128 dinamik şifreleme ve anahtar teslim hizmeti. Merhaba .NET örnek açıklandığı dayanır [bu](media-services-protect-with-aes128.md) makalesi.
  * **vodworkflow_aes.php**: Bu gösteren bir PHP dosyasıdır nasıl toouse PlayReady dinamik şifreleme ve lisans teslimat hizmeti. Merhaba .NET örnek açıklandığı dayanır [bu](media-services-protect-with-drm.md) makalesi.
  * **scale_encoding_units.php**: Bu tooscale kodlama birim nasıl ayrılmış gösteren bir PHP dosyasıdır.

## <a id="nov_changes_15"></a>Kasım 2015 sürüm
Azure Media Services artık Google Widevine lisans teslim hello bulut hizmetinde sunar. Daha fazla ayrıntı için çok başvurun[Bu duyuru blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/). Ayrıca bkz [Bu öğretici](media-services-protect-with-drm.md) ve [GitHub deposunu](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm). 

Azure Media izlemesi tarafından sağlanan Widevine lisans teslim hizmetleri önizlemede olduğuna dikkat edin. Daha fazla bilgi için bkz: [bu blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/).

## <a id="oct_changes_15"></a>Ekim 2015 sürüm
Azure Media Services (AMS) canlı veri merkezleri aşağıdaki hello şimdi: Brezilya Güney, Hindistan Batı, Hindistan Güney ve Hindistan orta. Hello Azure portal çok artık kullanabilirsiniz[Media Service hesapları oluşturmak](media-services-portal-create-account.md) ve açıklanan çeşitli görevleri gerçekleştirmek [burada](https://azure.microsoft.com/documentation/services/media-services/). Ancak, Live Encoding bu veri merkezlerinde etkin değildir. Ayrıca, bu veri merkezlerinde Kodlamaya Ayrılan Birimlerin tüm türleri kullanılabilir değildir.

* Brezilya Güney:                                          Yalnızca Standart ve Temel Kodlamaya Ayrılan Birimler kullanılabilir
* Hindistan Batı, Hindistan Güney ve Hindistan Orta:             Yalnızca Temel Kodlamaya Ayrılan Birimler kullanılabilir

## <a id="september_changes_15"></a>Eylül 2015 sürüm
* Teklifler özelliği tooprotect hello artık AMS isteğe bağlı video (VOD) ve modüler Widevine DRM teknolojisi ile canlı akış. Widevine lisansları teslim teslim hizmetleri ortakları toohelp aşağıdaki hello kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Daha fazla bilgi için bkz: [bu blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).
  
    Kullanabileceğiniz [AMS .NET SDK'sı](https://www.nuget.org/packages/windowsazure.mediaservices/) (3.5.1 hello sürümünden başlayarak) veya API tooconfigure, AssetDeliveryConfiguration toouse Widevine getirin.  
* AMS Apple ProRes videolar desteği eklendi. Artık Apple ProRes veya diğer codec bileşenleri kullanan QuickTime kaynak videoları dosyalarınız karşıya yükleyebilirsiniz. Daha fazla bilgi için bkz: [bu blog](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/).
* Medya Kodlayıcısı standart toodo alt kırpma ve canlı arşiv ayıklama artık kullanabilirsiniz. Daha fazla bilgi için bkz: [bu blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).
* şu filtreleme güncelleştirmeleri hello yapıldı: 
  
  * Apple HTTP canlı akışı (HLS) biçimi yalnızca ses filtresiyle artık kullanabilirsiniz. Bu güncelleştirme, tooremove yalnızca ses izleme belirterek sağlar (yalnızca ses = false) hello URL.
  * Varlıklarınızı filtrelerini tanımlarken, artık birden çok (yukarı too3) tek bir URL'de filtreler özelliği toocombine sahipsiniz.
    
    Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blogu.
* AMS t-çerçeveler HLS v4 artık destekler. T-çerçeve desteği İleri ve geri sarma işlemleri en iyi duruma getirir. Varsayılan olarak, tüm HLS v4 çıkışları t-çerçeve çalma listesi (EXT-X-I-FRAME-STREAM-INF) içerir.
  
    Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blogu.

## <a id="august_changes_15"></a>Ağustos 2015 sürüm
* Azure Media Services SDK Java V0.8.0 sürüm ve yeni örnekler için hazırdır. Daha fazla bilgi için bkz.
  
  * [Blog gönderisi](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Java örnekleri deposu](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* Birden çok ses akışı desteğiyle Azure Media Player güncelleştirme. Daha fazla bilgi için bkz.
  * [Blog gönderisi](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>Temmuz 2015 sürüm
* Merhaba genel kullanılabilirliğini Medya Kodlayıcısı standart sunuyoruz. Daha fazla bilgi için bkz: [bu blog gönderisine](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/).
  
    Medya Kodlayıcısı standart kullanan açıklanan hazır [bu](http://go.microsoft.com/fwlink/?LinkId=618336) bölümü. 4 k kodlar için bir hazır kullanırken, hello alınması gerektiğini unutmayın **Premium** ayrılmış birim türü. Daha fazla bilgi için bkz: [nasıl tooScale kodlama](media-services-scale-media-processing-overview.md).
* Azure Media Services ve oyuncu ile gerçek zamanlı resim yazıları dinamik. Daha fazla bilgi için bkz: [bu blog gönderisine](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/)

### <a name="media-services-net-sdk-updates"></a>.NET SDK güncelleştirmeleri medya Hizmetleri
Azure Media Services .NET SDK'sı sürüm 3.4.0.0 sunulmuştur. Bu sürümde aşağıdaki işlevselliği hello eklendi:  

* Canlı arşiv uygulanan desteği. Canlı bir arşiv içeren bir varlık indirilemiyor unutmayın.
* Dinamik filtre uygulanmış desteği.
* Varlık silinirken kullanıcılar tookeep depolama kapsayıcısı sağlar uygulanan işlevselliği.
* Hata düzeltmeleri kanalları tooretry ilkelerinde ilgili.
* Etkin **Medya Kodlayıcısı Premium iş akışı**.

## <a id="june_changes_15"></a>Haziran 2015 sürüm
### <a name="media-services-net-sdk-updates"></a>.NET SDK güncelleştirmeleri medya Hizmetleri
Azure Media Services .NET SDK'sı sürüm 3.3.0.0 sunulmuştur. Bu sürümde aşağıdaki işlevselliği hello eklendi:  

* Openıd Connect bulma spec desteği,
* Kimlik sağlayıcısı tarafında anahtarları rollover işlemek için destek. 

Openıd Connect bulma belge sunan bir kimlik sağlayıcısı kullanıyorsanız (hello aşağıdaki sağlayıcıları yapın: Azure Active Directory, Google, Salesforce), Azure Media Services tooobtain JWT belirtecinden doğrulanması için anahtarları imzalama isteyin Openıd connect bulma belirtimi. 

Daha fazla bilgi için bkz: [kullanarak Json Web anahtarları bulma belirtim toowork Openıd Connect ile JWT belirteci kimlik doğrulaması Azure Media Services](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/).

## <a id="may_changes_15"></a>Mayıs 2015 sürüm
Yeni özellikler aşağıdaki hello tanışın:

* [Media Services ile gerçek zamanlı kodlama önizlemesi](media-services-manage-live-encoder-enabled-channels.md)
* [Dinamik bildirimi](media-services-dynamic-manifest-overview.md)
* [Azure medya Hyperlapse medya işlemcisi önizlemesi](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>Nisan 2015 güncelleştirmesinden
### <a name="general-media-services-updates"></a>Güncelleştirmeleri genel medya Hizmetleri
* [Azure Media Player Duyurusu](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/).
* Yapılandırılmış tooingest bir RTMP protokolü olan kanalları Media Services REST 2.10 ile başlayan birincil ile oluşturulur ve ikincil URL'leri alma. Daha fazla bilgi için bkz: [kanal yapılandırmaları alma](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Azure Media Indexer güncelleştirir
* İspanyolca dil desteği
* Yeni yapılandırma xml biçimi

Daha fazla bilgi için bkz: [bu blog](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

### <a name="media-services-net-sdk-updates"></a>.NET SDK güncelleştirmeleri medya Hizmetleri
Azure Media Services .NET SDK sürüm 3.2.0.0 sunulmuştur.

Merhaba güncelleştirmeleri karşılıklı hello müşteri bazıları şunlardır:

* **Değişiklik çiğnemekten**: değiştirilen **TokenRestrictionTemplate.Issuer** ve **TokenRestrictionTemplate.Audience** toobe bir dize türü.
* Güncelleştirmeleri toocreating özel yeniden deneme ilkelerini ilgili.
* Hata düzeltmeleri ilgili toouploading ve yükleme dosyaları.
* Merhaba **MediaServicesCredentials** sınıf artık birincil ve ikincil erişim denetim uç noktası tooauthenticate karşı kabul eder.

## <a id="march_changes_15"></a>Mart 2015 sürüm
### <a name="general-media-services-updates"></a>Güncelleştirmeleri genel medya Hizmetleri
* Media Services, artık Azure CDN tümleştirme sağlar. toosupport hello tümleştirmesi, hello **CdnEnabled** özelliği çok eklenen**StreamingEndpoint**.  **CdnEnabled** 2.9 sürümünden başlayarak REST API'leri ile kullanılabilir (daha fazla bilgi için bkz: [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)).  **CdnEnabled** .NET SDK'sı 3.1.0.2 sürümünden başlayarak kullanılabilir (daha fazla bilgi için bkz: [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx)).
* Duyuru, **Medya Kodlayıcısı Premium iş akışı**. Daha fazla bilgi için bkz: [Azure Media Services kodlama giriş Premium](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/).

## <a id="february_changes_15"></a>Şubat 2015 sürüm
### <a name="general-media-services-updates"></a>Güncelleştirmeleri genel medya Hizmetleri
Media Services REST API sürümü 2.9 sunulmuştur. Bu sürümünden başlayarak, hello akış uç noktalarını ile Azure CDN tümleştirme etkinleştirebilirsiniz. Daha fazla bilgi için bkz: [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx).

## <a id="january_changes_15"></a>Ocak 2015 sürüm
### <a name="general-media-services-updates"></a>Güncelleştirmeleri genel medya Hizmetleri
Duyuru, genel kullanılabilirlik (GA) dinamik şifreleme ile içerik koruma. Daha fazla bilgi için bkz: [Azure Media Services Genel kullanılabilirlik DRM teknolojisi ile akış güvenliği artırır](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/).

### <a name="media-services-net-sdk-updates"></a>.NET SDK güncelleştirmeleri medya Hizmetleri
Azure Media Services .NET SDK'sı sürüm 3.1.0.1 sunulmuştur.

Bu sürüm hello varsayılan Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate Oluşturucusu geçersiz olarak işaretlendi. Merhaba yeni Oluşturucusu TokenType bağımsız değişken olarak alır.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>Aralık 2014 sürümü
### <a name="general-media-services-updates"></a>Güncelleştirmeleri genel medya Hizmetleri
* Bazı güncelleştirmeleri ve yeni özellikleri toohello Azure dizin oluşturucu medya işlemcisi eklendi. Daha fazla bilgi için bkz: [Azure Media Indexer sürüm 1.1.6.7 Sürüm Notları](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/).
* Ayrılan birimler kodlama tooupdate sağlayan yeni bir REST API eklenen: [EncodingReservedUnitType REST ile](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype).
* Eklenen CORS anahtar teslim hizmeti için destek.
* Yetkilendirme İlkesi seçenekleri sorgulama performans iyileştirmeleri yapıldığını.
* Çin veri merkezinde hello [anahtar teslim URL'si](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) müşteri sunulmuştur (diğer veri merkezlerinde olduğu gibi).
* Eklenen HLS otomatik hedef süresi. Canlı akış yaparken HLS her zaman dinamik olarak paketlenir. Varsayılan olarak, Media Services hello ana kare ya da aralığı (KeyFrameInterval) tooas grubu, resimleri – hello Canlı kodlayıcıdan alınan GOP, temel HLS segment paketleme oranı (FragmentsPerSegment) otomatik olarak hesaplar. Daha fazla bilgi için bkz: [Azure Media Services canlı akış ile çalışma].

### <a name="media-services-net-sdk-updates"></a>.NET SDK güncelleştirmeleri medya Hizmetleri
* [Azure Media Services .NET SDK'sı](http://www.nuget.org/packages/windowsazure.mediaservices/) şimdi 3.1.0.0 sürümüdür.
* Yükseltme .net SDK hello bağımlılık too.NET 4.5 Framework.
* Ayrılan birimler kodlama tooupdate sağlayan yeni bir API eklendi. Daha fazla bilgi için bkz: [güncelleştirme ayrılmış birim türü ve kodlama .NET kullanarak RUs artırma](media-services-dotnet-encoding-units.md).
* Eklenen JWT (JSON Web belirteci) belirteci kimlik doğrulaması için destek. Daha fazla bilgi için bkz: [JWT belirteci kimlik doğrulaması Azure Media Services ve dinamik şifreleme](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).
* Merhaba PlayReady lisans şablonunda BeginDate ve ExpirationDate için eklenen göreli uzaklık.

## <a id="november_changes_14"></a>Kasım 2014 sürümü
* Media Services şimdi tooingest bir canlı kesintisiz akış (FMP4) içerik bir SSL bağlantısı üzerinden sağlar. SSL üzerinden tooingest URL tooHTTPS alma emin tooupdate hello olun.  Şu anda AMS SSL ile özel etki alanlarını, desteklemez.  Canlı akış hakkında daha fazla bilgi için bkz: [Azure Media Services canlı akış ile çalışma].
* Şu anda bir SSL bağlantısı üzerinden RTMP canlı akış alma olamaz.
* Akış uç noktası içeriğinizi teslim etmek hello 10 Eylül 2014 sonra oluşturduysanız yalnızca SSL üzerinden akışını sağlayabilirsiniz. Akış URL'leri akış uç noktaları Eylül 10 sonra oluşturulan hello dayanır, hello URL "streaming.mediaservices.windows.net" (Merhaba yeni biçim) içerir. "Origin.mediaservices.windows.net" (Merhaba eski biçimi) içeren akış URL'leri SSL desteklemez. URL'niz hello eski biçimindedir ve SSL üzerinden toobe mümkün toostream istiyorsanız [yeni bir akış uç noktası oluşturma](media-services-portal-manage-streaming-endpoints.md). Yeni uç nokta toostream içeriğinizi SSL üzerinden akış hello temel alınarak oluşturulan URL kullanın.

## <a id="october_changes_14"></a>Ekim 2014 sürümü
### <a id="new_encoder_release"></a>Medya Kodlayıcısı yayın Hizmetleri
Media Services Azure Medya Kodlayıcısı yeni sürümü Hello sunuyoruz. Merhaba ile en son Azure medya Kodlayıcı yalnızca için ücretlendirilirsiniz GB çıktı, ancak Aksi halde hello yeni Kodlayıcı özelliği hello önceki encoder ile uyumlu. Daha fazla bilgi için [Media Services fiyatlandırma ayrıntıları]).

### <a id="oct_sdk"></a>Media Services .NET SDK'sı
.NET uzantıları için Media Services SDK'sı sürüm 2.0.0.3 sunulmuştur.

.NET için Media Services SDK'sı sürüm 3.0.0.8 sunulmuştur.

Merhaba aşağıdaki değişiklikler yapıldı:

* Yeniden deneme ilkesi sınıfları yeniden düzenleme.
* Kullanıcı aracısı dizesi toohttp istek üstbilgileri ekleme.
* Nuget restore derleme adımı ekleme.
* Senaryo testleri toouse x509 sertifika deposundan düzeltme.
* Kanal güncelleştirme ve akış sonlandırdığınızda, ayarlar doğrulanıyor.

### <a name="new-github-repository-toohost-media-services-samples"></a>Yeni GitHub depo toohost Media Services örnekleri
Örnekleri bulunur [Azure Media Services örnekleri GitHub deposunu](https://github.com/Azure/Azure-Media-Services-Samples).

## <a id="september_changes_14"></a>Eylül 2014 sürümü
Media Services REST meta veri sürümü 2.7 sunulmuştur. Hello son KALAN güncelleştirmeleri hakkında daha fazla bilgi için bkz: [Azure Media Services REST API Başvurusu].

.NET için Media Services SDK'sı sürüm 3.0.0.7 sunulmuştur

### <a id="sept_14_breaking_changes"></a>Yeni değişiklikler
* **Kaynak** çok adlandırıldı[StreamingEndpoint].
* Merhaba kullanırken hello varsayılan davranış değişikliği **Azure portal** tooencode ve MP4 dosyaları yayımlayın.

Daha önce hello Klasik Azure portalı toopublish kullanırken tek dosya MP4 varlığı bir SAS URL'si oluşturulacak (SAS URL'leri izin, toodownload hello bir blob depolama biriminden video). Şu anda hello Klasik Azure portalı tooencode kullandığınızda ve tek dosya MP4 varlığı yayımlama hello URL noktaları tooan Azure Media Services akış uç noktası oluşturulur.  Bu değişiklik, doğrudan karşıya yüklenen tooMedia Services ve Azure Media Services tarafından kodlanmış olmadan yayımlanan MP4 videolar etkilemez.

Şu anda, aşağıdaki iki seçenek toosolve hello sorun hello yok.

* Akış birimleri etkinleştirin ve dinamik paketleme toostream hello .mp4 varlık kesintisiz akış sunuyu olarak kullanın.
* Merhaba .mp4 bir SAS URL'si toodownload oluşturun (veya aşamalı olarak Yürüt). Hakkında daha fazla bilgi için bir SAS Bulucu toocreate bkz [teslim içerik].

### <a id="sept_14_GA_changes"></a>Yeni özellikler/GA sürümü parçası olan senaryolar
* **Dizin Oluşturucu medya işlemcisi**. Daha fazla bilgi için bkz: [ortam dosyalarıyla dizin Azure Media Indexer].
* Merhaba [StreamingEndpoint] varlık şimdi tooadd özel etki alanı (ana) adları, sağlar.
  
    Uç nokta adı akış Hello Media Services kullanılan bir özel etki alanı adı toobe için akış uç noktası tooadd özel ana bilgisayar adları tooyour gerekir. Merhaba Media Services REST API'leri veya .NET SDK'sı tooadd özel ana bilgisayar adları kullanın.
  
    ilgili önemli noktalar aşağıdaki hello Uygula:
  
  * Merhaba sahipliğini hello özel etki alanı adı olması gerekir.
  * Merhaba sahipliği hello etki alanı adını Azure Media Services tarafından doğrulanması gerekir. toovalidate hello etki alanı, eşleşen bir CName oluşturmanız <MediaServicesAccountId>.<parent domain> tooverifydns. < mediaservices dns bölge >. 
  * Merhaba özel ana bilgisayar adı (örneğin, sports.contoso.com) tooyour Media Services StreamingEndpont'ın ana bilgisayar adı (örneğin, amstest.streaming.mediaservices.windows.net) eşlemeleri başka bir CName oluşturmanız gerekir.

    Daha fazla bilgi için bkz: Merhaba **CustomHostNames** hello özelliğinde [StreamingEndpoint] konu.

### <a id="sept_14_preview_changes"></a>Yeni özellikler/hello genel Önizleme sürümü parçası olan senaryolar
* Canlı akış Önizleme. Daha fazla bilgi için bkz: [Azure Media Services canlı akış ile çalışma].
* Anahtar teslim hizmeti. Daha fazla bilgi için bkz: [AES-128 dinamik şifreleme kullanarak ve anahtar teslim hizmeti].
* AES dinamik şifreleme. Daha fazla bilgi için bkz: [AES-128 dinamik şifreleme kullanarak ve anahtar teslim hizmeti].
* PlayReady lisans teslimat hizmeti. Daha fazla bilgi için bkz: [dinamik şifreleme kullanarak PlayReady ve lisans teslimat hizmeti].
* PlayReady dinamik şifreleme. Daha fazla bilgi için bkz: [dinamik şifreleme kullanarak PlayReady ve lisans teslimat hizmeti].
* Medya PlayReady lisans şablonu Hizmetleri. Daha fazla bilgi için bkz: [Media Services PlayReady lisans şablonu genel bakış].
* Depolama akış varlıklarını şifrelenir. Daha fazla bilgi için bkz: [akış depolama şifrelenmiş içerik].

## <a id="august_changes_14"></a>Ağustos 2014 sürümü
Bir varlık kodlama, bir çıkış varlığı hello kodlama işi tamamlandıktan sonra oluşturulur. Bu sürüm kadar Azure Media Services Encoder çıkış varlıklar hakkında meta veriler üretti. Bu sürüm hello encoder ile başlayarak, giriş varlıklar hakkında meta veriler üretir. Merhaba daha fazla bilgi için bkz [giriş meta veri] ve [çıkış meta veri] Konular.

## <a id="july_changes_14"></a>Temmuz 2014 sürümü
hata düzeltmeleri aşağıdaki hello hello için Azure Media Services Paketleyici ve Şifreleyici yapılmıştır:

* Yalnızca ses geri çoğullama dönüşümü Canlı arşiv varlık tooHTTP canlı akış – bu sabit ve ses ve video şimdi oynatılır yürütülür.
* Bir varlık tooHTTP canlı akış ve AES 128-bit Zarf şifreleme paketleme, paketlenmiş hello akışları Android cihazlarda kayıttan değil – Bu hatanın düzeltildiğini ve hello paketlenmiş akış HTTP canlı akış destek Android cihazlarda geri oynar.

## <a id="may_changes_14"></a>Mayıs 2014 sürümü
### <a id="may_14_changes"></a>Güncelleştirmeleri genel medya Hizmetleri
Artık kullanabilirsiniz [dinamik paketleme] toostream HTTP canlı akışı (HLS) v3. toostream HLS v3 biçimi toohello Kaynak Konum Belirleyicisi yolu izleyerek hello ekleyin: * .ism/manifest(format=m3u8-aapl-v3). Daha fazla bilgi için bkz: [Nick Drouin'ın blogu].

Ayrıca PlayReady ile şifrelenmiş HLS (v3 hem de v4) teslim destekler statik olarak PlayReady ile şifrelenmiş kesintisiz akış dayalı artık dinamik paketleme. Hakkında bilgi için bkz tooencrypt kesintisiz akış PlayReady ile [PlayReady ile koruma kesintisiz akış].

### <a name="may_14_donnet_changes"></a>.NET SDK güncelleştirmeleri medya Hizmetleri
aşağıdaki geliştirmeleri hello hello Media Services .NET SDK'sı 3.0.0.5 yayın bulunmaktadır:

* Daha iyi hızı ve karşıya yükleme/indirme ortam varlıkları esnekliği.
* Yeniden deneme mantığı ve geçici özel durum işleme geliştirmeleri: 
  
  * Geçici hata algılama ve yeniden deneme mantığı gelişmiş sorgulama, değişiklikleri kaydetmeden, karşıya yükleme veya dosyaları indirme neden özel durumlar için. 
  * Web özel durumları (örneğin, bir ACS belirteci isteği sırasında) alırken, önemli hataları daha hızlı şimdi başarısız olduğunu fark edeceksiniz.

Daha fazla bilgi için bkz: [yeniden deneme mantığı hello .NET için Media Services SDK'sı,].

## <a id="april_changes_14"></a>Nisan 2014 Kodlayıcı sürümü
### <a name="april_14_enocer_changes"></a>Kodlayıcı güncelleştirmeleri medya Hizmetleri
* Merhaba Çimen vadisi EDIUS doğrusal Düzenleyicisi kullanılarak yazılan AVI dosyalarını hello video hafifçe olduğu alma için destek eklendi Çimen vadisi denetim merkezini/HQX codec kullanılarak sıkıştırılmış. Daha fazla bilgi için bkz: [Çimen vadisi bildirdi EDIUS 7 akış aracılığıyla bulut hello].
* Merhaba medya Kodlayıcı tarafından üretilen hello dosyaları için adlandırma kuralı hello belirtmek için destek eklendi. Daha fazla bilgi için bkz: [denetleme medya hizmeti Kodlayıcı çıkışı dosya adları].
* Video ve/veya ses yer paylaşımları desteği eklendi. Daha fazla bilgi için bkz: [oluşturma yer paylaşımları].
* Birden çok video kesimi birlikte Dikiş için destek eklendi. Daha fazla bilgi için bkz: [Dikiş Video kesimleri].
* İlgili hatanın düzeltildiğini burada hello ses kodlanmış MPEG-1 ses Katman 3 (diğer adıyla MP3) MP4s tootranscoding.

## <a id="jan_feb_changes_14"></a>Ocak/Şubat 2014 sürümleri
### <a name="jan_fab_14_donnet_changes"></a>Azure Media Services .NET SDK'sı 3.0.0.1, 3.0.0.2 ve 3.0.0.3
3.0.0.1 ve 3.0.0.2 Hello değişiklikleri şunlardır:

* Giderilen sorunlar OrderBy ifadelerle LINQ sorgularını toousage ilgili.
* Test çözümlerinde bölme [GitHub] birim tabanlı testleri ve senaryo tabanlı testleri.

Merhaba değişiklikler hakkında daha fazla ayrıntı için bkz: [Azure Media Services .NET SDK 3.0.0.1 ve 3.0.0.2 serbest].

içinde 3.0.0.3 hello aşağıdaki değişiklikler yapıldı:

* Azure depolama bağımlılıkları toouse sürüm 3.0.3.0 yükseltilmiştir. 
* Geriye dönük uyumluluk sorunu 3.0 için sabit. *.* serbest bırakır. 

## <a id="december_changes_13"></a>Aralık 2013'ün yayın
### <a name="dec_13_donnet_changes"></a>Azure Media Services .NET SDK'sı 3.0.0.0
> [!NOTE]
> 3.0.x.x sürümleri 2.4.x.x sürümleriyle geriye dönük olarak uyumlu değildir.
> 
> 

Merhaba Media Services SDK en son sürümünü Hello 3.0.0.0 sunulmuştur. Nuget'ten hello son paketini indirin ya da hello bitten alma [GitHub].

Media Services SDK'sı sürüm 3.0.0.0 Hello ile başlayarak, hello yeniden kullanabilir [Azure Active Directory erişim denetimi Hizmeti'nden (ACS)] belirteçleri. Merhaba "yeniden erişim denetimi hizmeti belirteçleri" daha fazla bilgi için bkz: hello bölümünde [tooMedia Hizmetleri .NET için Media Services SDK'sı hello ile bağlanma] konu.

### <a name="dec_13_donnet_ext_changes"></a>Azure Media Services .NET SDK uzantıları 2.0.0.0
Hello Azure Media Services .NET SDK uzantıları, genişletme yöntemleri ve, kodunuzu basitleştirerek Azure Media Services ile daha kolay toodevelop olun yardımcı işlevleri kümesidir. Merhaba son bitten alabilirsiniz [Azure Media Services .NET SDK uzantıları].

## <a id="november_changes_13"></a>Kasım 2013 sürümü
### <a name="nov_13_donnet_changes"></a>Azure Media Services .NET SDK değişiklikleri
Bu sürümünden başlayarak, hello .NET için Media Services SDK çağrıları toohello Media Services REST API katmanı yaparken oluşabilir geçici hata hatalarını ele alır.

## <a id="august_changes_13"></a>Ağustos 2013'ün yayın
### <a name="aug_13_powershell_changes"></a>Azure Sdk Araçları'nın içerdiği Media Services PowerShell cmdlet'leri
Medya Hizmetleri PowerShell cmdlet'leri aşağıdaki hello şimdi dahil edilmiştir [azure sdk Araçları].

* Get-AzureMediaServices 
  
    Örneğin, `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    Örneğin, `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    Örneğin, `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    Örneğin, `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>Haziran 2013'ün yayın
### <a name="june_13_general_changes"></a>Azure Media Services değişiklikleri
Bu bölümde belirtilen hello değişiklikleri Haziran 2013 Media Services yayımları hello dahil güncelleştirmelerdir.

* Özelliği toolink tooa medya hizmeti hesabı birden çok depolama hesapları. 
  
    StorageAccount
  
    Asset.StorageAccountName ve Asset.StorageAccount
* Özelliği tooupdate Job.Priority. 
* Bildirim varlıkları ve özellikler ile ilgili: 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    İş
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Azure Media Services .NET SDK'sı değişiklikleri
Merhaba aşağıdaki değişiklikler dahil edilen Haziran 2013'te Media Services SDK'sı serbest bırakır. Merhaba son Media Services SDK'sı Github'da kullanılabilir.

* 2.3.0.0, birden çok depolama hesapları tooa Media Services hesabı bağlama Media Services SDK'sı destekleyen hello Hello sürümüyle başlatılıyor. Merhaba aşağıdaki API'leri bu özelliği desteklemez:
  
    Merhaba IStorageAccount türü.
  
    Merhaba Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts özelliği.
  
    Merhaba StorageAccount özelliği.
  
    Merhaba StorageAccountName özelliği.
  
    Daha fazla bilgi için bkz: [yönetme Media Services varlıklar birden çok depolama hesapları arasında].
* Bildirim ilgili API'leri gösterir. Merhaba özelliği toolisten tooAzure kuyruk depolama bildirimleri sahip 2.2.0.0 Hello sürümüyle başlatılıyor. Daha fazla bilgi için [Media Services işi bildirimlerini işleme].
  
    Merhaba Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions özelliği.
  
    Merhaba Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint türü.
  
    Merhaba Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription türü.
  
    Merhaba Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection türü.
  
    Merhaba Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType türü.
  
    Merhaba Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState türü.
* Hello Azure Storage istemci SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll) bağımlılığı.
* OData 5.5 (Microsoft.Data.OData.dll) bağımlılığı.

## <a id="december_changes_12"></a>Kasım 2012 sürüm
### <a name="dec_12_dotnet_changes"></a>Azure Media Services .NET SDK'sı değişiklikleri
* IntelliSense: pek çok türü eksik IntelliSense belgeleri eklendi.
* Microsoft.Practices.TransientFaultHandling.Core: Burada hello SDK hala bir bağımlılık tooan eski bir sürümü bu olan bir sorun düzeltilmiştir. Merhaba SDK şimdi başvuruları 5.1.1209.1 Bu derlemesinin sürümü.

Kasım 2012 SDK hello bulunan sorunlarını giderir:

* IAsset.Locators.Count: tüm bulucular silinen sonra Bu sayaç artık doğru yeni IAsset arabirimlerde bildirilir.
* IAssetFile.ContentFileSize: Bu değer şimdi düzgün bir şekilde karşıya yükleme IAssetFile.Upload(filepath) tarafından ayarlanır.
* IAssetFile.ContentFileSize: Bu özellik artık bir varlık dosyası oluşturulurken ayarlanabilir. Daha önce salt okunurdu.
* IAssetFile.Upload(filepath): Bu zaman uyumlu karşıya yükleme yöntemi aşağıdaki birden çok dosya toohello varlık karşıya yüklenirken hata hello burada atma olan bir sorun düzeltilmiştir. "sunucu tooauthenticate hello isteği başarısız oldu. Hello hata. Authorization Üstbilgisi Hello değeri doğru hello imza dahil olmak üzere biçimlendirildiğinden emin olun."
* IAssetFile.UploadAsync: Burada en fazla 5 dosyaları aynı anda karşıya yüklenemedi bir sorun düzeltilmiştir.
* IAssetFile.UploadProgressChanged: Bu olay artık hello SDK tarafından sağlanır.
* IAssetFile.DownloadAsync (dize, BlobTransferClient, ILocator, CancellationToken): Bu yöntem aşırı şimdi sağlanır.
* IAssetFile.DownloadAsync: Burada en fazla 5 dosyaları aynı anda karşıdan yüklenemedi bir sorun düzeltilmiştir.
* IAssetFile.Delete(): hiçbir dosya Merhaba IAssetFile karşıya yüklediyseniz burada silme çağrısından bir özel durum atabilir bir sorun düzeltilmiştir.
* İşleri: bir sorun olduğu bir "MP4 tooSmooth akışları görev" ile bir "PlayReady koruma proje şablonunu kullanarak görev" zincirleme değil oluşturacak herhangi bir görevi hiç sabit.
* EncryptionUtils.GetCertificateFromStore(): Bu yöntem artık hello sertifika sertifika yapılandırma sorunlarını tabanlı bulma tooa hataları nedeniyle bir null başvuru özel durumu oluşturur.

## <a id="november_changes_12"></a>Kasım 2012 sürüm
Merhaba Bu bölümde belirtilen değişiklikler oldu hello Kasım 2012 (sürüm 2.0.0.0) bulunan güncelleştirmeler SDK. Bu değişiklikler değiştirilmiş veya yeniden yazılmıştır hello Haziran 2012 Önizleme SDK sürüm toobe için yazılmış herhangi bir kod gerektirebilir.

* Varlıklar
  
    IAsset.Create(assetName) hello yalnızca varlık oluşturma işlevdir. IAsset.Create hello yöntem çağrısı bir parçası olarak artık dosyaları karşıya yükler. IAssetFile yüklemek için kullanın.
  
    Merhaba IAsset.Publish yöntemi ve hello AssetState.Publish numaralandırma değeri Services SDK'sı hello kaldırıldı. Bu değeri kullanır herhangi bir kod yeniden yazılmış olmalıdır.
* FileInfo
  
    Bu sınıf kaldırılır ve IAssetFile tarafından değiştirilir.
  
    IAssetFiles
  
    IAssetFile FileInfo değiştirir ve farklı bir davranışı vardır. toouse, hello IAssetFiles nesne örneği, bir dosyayı karşıya yükleyin ve ardından her iki kullanarak hello Media Services SDK'sı veya hello Azure depolama SDK'sı. IAssetFile.Upload aşırı aşağıdaki hello kullanılabilir:
  
  * IAssetFile.Upload(filePath): hello iş parçacığı engeller ve yalnızca tek bir dosyayı karşıya yüklenirken önerilen bir zaman uyumlu yöntemi.
  * IAssetFile.UploadAsync (filePath, blobTransferClient, Bulucu, cancellationToken): zaman uyumsuz bir yöntem. Tercih edilen hello karşıya yükleme mekanizması budur. 
    
    Bilinen hata: hello cancellationToken kullanarak gerçekten iptal eder hello karşıya yükleme; Ancak, hello iptal hello görevlerin durumunu durumlardan birini olabilir. Düzgün catch ve özel durumları işleme gerekir.
* Belirleyicileri
  
    Merhaba kaynak özgü sürümleri kaldırılmıştır. Merhaba SAS özgü bağlamı. Locators.CreateSasLocator (varlık, accessPolicy) kullanım dışı bırakılan veya kaldırılan İST tarafından işaretlenir Merhaba Belirleyicileri bkz güncelleştirilmiş davranışı için yeni işlevsellik altında bölümü.

## <a id="june_changes_12"></a>Haziran 2012 Önizleme sürümü
işlevselliği aşağıdaki hello'hello SDK hello Kasım sürümünde yeni.

* Varlıkları silme
  
    IAsset, IAssetFile, ILocator, IAccessPolicy, IContentKey nesneleri hello nesne düzeyinde hello cloudMediaContext.ObjCollection.Delete(objInstance) koleksiyonu, bir Sil gerektirmek yerine yani IObject.Delete(), şimdi silinir.
* Belirleyicileri
  
    Bulucular hello CreateLocator yöntemi kullanılarak oluşturulmalıdır ve hello LocatorType.SAS veya LocatorType.OnDemandOrigin enum değerleri kullanmak hello belirli tür Bulucu için bağımsız değişken olarak toocreate istiyor.
  
    Yeni özellikleri tooLocators toomake eklendi bunu daha kolay tooobtain içeriğiniz için kullanılabilir URI. Bu yeniden tasarlanması Bulucuyu edildi tooprovide daha fazla esneklik için gelecekteki üçüncü taraf genişletilebilirlik anlamına gelir ve kolaylığı kullanım medya istemci uygulamaları için artırın.
* Zaman uyumsuz yöntem desteği
  
    Zaman uyumsuz destek tooall yöntemler eklenmiştir.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[Azure Media Services MSDN Forumu]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[Azure Media Services REST API Başvurusu]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[Media Services fiyatlandırma ayrıntıları]: http://azure.microsoft.com/pricing/details/media-services/
[giriş meta veri]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[çıkış meta veri]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[teslim içerik]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[ortam dosyalarıyla dizin Azure Media Indexer]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[Azure Media Services canlı akış ile çalışma]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[AES-128 dinamik şifreleme kullanarak ve anahtar teslim hizmeti]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[dinamik şifreleme kullanarak PlayReady ve lisans teslimat hizmeti]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[Media Services PlayReady lisans şablonu genel bakış]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[akış depolama şifrelenmiş içerik]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[dinamik paketleme]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[Nick Drouin'ın blogu]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[PlayReady ile koruma kesintisiz akış]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[yeniden deneme mantığı hello .NET için Media Services SDK'sı,]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[Çimen vadisi bildirdi EDIUS 7 akış aracılığıyla bulut hello]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[denetleme medya hizmeti Kodlayıcı çıkışı dosya adları]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[oluşturma yer paylaşımları]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[Dikiş Video kesimleri]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[Azure Media Services .NET SDK 3.0.0.1 ve 3.0.0.2 serbest]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory erişim denetimi Hizmeti'nden (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[tooMedia Hizmetleri .NET için Media Services SDK'sı hello ile bağlanma]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[Azure Media Services .NET SDK uzantıları]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure sdk Araçları]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[yönetme Media Services varlıklar birden çok depolama hesapları arasında]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[Media Services işi bildirimlerini işleme]: http://msdn.microsoft.com/library/azure/dn261241.aspx

