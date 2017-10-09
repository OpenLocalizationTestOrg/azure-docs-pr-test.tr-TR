---
title: "aaaAzure Media Services hata kodları | Microsoft Docs"
description: "Merhaba konu Azure Media Services hata kodları genel bir bakış sağlar."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Azure Media Services hata kodları
Microsoft Azure Media Services kullanırken, Media Services desteklenmez tooactions zaman aşımına uğramak kimlik doğrulama belirteçleri gibi sorunları bağlı olarak hello hizmetinden HTTP hata kodları alabilirsiniz. Merhaba bir listesi aşağıda verilmiştir **HTTP hata kodları** , döndürülüp döndürülmediğini Media Services tarafından ve bunlar için hello olası neden olur.  

## <a name="400-bad-request"></a>400 Hatalı istek
Merhaba isteği geçersiz bilgiler içeriyor ve son reddedilir nedenleri aşağıdaki hello tooone:

* Desteklenmeyen bir API sürümü belirtildi. Merhaba en güncel sürümü için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).
* Media Services Hello API sürümü belirtilmedi. Nasıl toospecify hello API sürümü hakkında daha fazla bilgi için bkz: [Media Services Operations REST API Başvurusu](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).
  
  > [!NOTE]
  > Merhaba .NET veya Java SDK'ları tooconnect tooMedia kullanıyorsanız, hizmetleri, hello API sürümü belirtildi sizin için ne zaman deneyin ve Media Services karşı bazı eylemler gerçekleştirme.
  > 
  > 
* Tanımlanmamış özellik belirtilmedi. Merhaba hata iletisinde Hello özelliği adıdır. Belirli bir varlık üyeleri olan özellikler belirtilebilir. Bkz: [Azure Media Services REST API Başvurusu](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) varlıkları ve özelliklerinin listesi.
* Geçersiz bir özellik değeri belirtildi. Merhaba hata iletisinde Hello özelliği adıdır. Merhaba önceki bağlantı için geçerli özellik türleri ve değerleri bakın.
* Bir özellik değeri eksik ve gereklidir.
* Belirtilen hello URL parçası hatalı bir değer içeriyor.
* Bir girişim yapıldı WriteOnce özelliği tooupdate yapılan.
* Bir girişim yapıldı belirtilmedi veya belirlenemedi birincil bir AssetFile Giriş bir varlığı olan bir işi toocreate yapılan.
* Bir girişim yapıldı tooupdate bir SAS Bulucu yapılan. SAS bulucular yalnızca oluşturulan veya silinebilir. Bulucular akış güncelleştirilebilir. Daha fazla bilgi için bkz: [Bulucular](https://docs.microsoft.com/rest/api/media/operations/locator).
* Desteklenmeyen bir işlem veya sorgu gönderildi.

## <a name="401-unauthorized"></a>401 Yetkisiz
Hello isteği olmayan kimlik doğrulaması (bunu yetkilendirilebilir önce) son tooone hello aşağıdaki nedenlerden biri:

* Kimlik doğrulama üstbilgisi eksik.
* Hatalı kimlik doğrulaması üstbilgi değeri.
  * Merhaba belirtecinin süresi doldu. 
  * Merhaba belirteci geçersiz bir imza içeriyor.

## <a name="403-forbidden"></a>403 Yasak
Merhaba isteği son verilmez nedenleri aşağıdaki hello tooone:

* Merhaba Media Services hesabı bulunamadı veya silinmiş olabilir.
* Merhaba Media Services hesabı devre dışı bırakılır ve HTTP GET hello istek türü değil. Hizmet işlemleri de 403 bir yanıt döndürür.
* Merhaba kimlik doğrulama belirteci hello kullanıcının kimlik bilgileri içermiyor: AccountName ve/veya Subscriptionıd. Media Services hesabınızı hello Azure Yönetim Portalı için hello Media Services UI uzantısı bu bilgileri bulabilirsiniz.
* Merhaba kaynak erişilemez.
  
  * Bir girişim yapıldı Media Services hesabınız için kullanılabilir olmayan bir MediaProcessor toouse yapılan.
  * Media Services tarafından tanımlanan bir JobTemplate tooupdate girişimde bulunuldu.
  * Bir girişim yapıldı toooverwrite bazı diğer Media Services hesabı Bulucu yapılan.
  * Bir girişim yapıldı bazı diğer Media Services hesabı ContentKey toooverwrite yapılan.
* Merhaba kaynak hello Media Services hesabı için ulaşıldı tooa hizmet kotasını nedeniyle oluşturulamadı. Merhaba Hizmeti kotaları hakkında daha fazla bilgi için bkz: [kotaları ve kısıtlamaları](media-services-quotas-and-limitations.md).

## <a name="404-not-found"></a>404 Bulunamadı
Merhaba isteği bir kaynakta izin verilmiyor, aşağıdaki nedenlerden hello son tooone:

* Bir girişim yapıldı var olmayan bir varlık tooupdate yapılan.
* Bir girişim yapıldı var olmayan bir varlık toodelete yapılan.
* Bir girişim yapıldı toocreate yok tooan varlık bağlantıları varlıkta yapılan.
* Bir girişim yapıldı var olmayan bir varlık tooGET yapılan.
* Bir girişim yapıldı hello Media Services hesabı ile ilişkili olmayan bir depolama hesabı toospecify yapılan.  

## <a name="409-conflict"></a>409 çakışma
Merhaba isteği son verilmez nedenleri aşağıdaki hello tooone:

* Birden fazla AssetFile hello varlık içindeki hello belirtilen ada sahip.
* İkinci bir toocreate birincil girişimde bulunuldu AssetFile hello varlık içinde.
* Girişiminde bulunuldu toocreate ContentKey hello ile belirtilen kimliği zaten kullanılıyor.
* Girişiminde bulunuldu toocreate hello bulucuyla belirtilen kimliği zaten kullanılıyor.
* Birden fazla IngestManifestFile hello IngestManifest içinde hello belirtilen ada sahip.
* Bir girişim yapıldı ikinci bir depolama şifreleme ContentKey toohello toolink yapılan depolama şifrelenmiş varlık.
* Girişiminde bulunuldu toolink hello aynı ContentKey toohello varlık.
* Bir Bulucu tooan, depolama kapsayıcısı artık eksik veya varlık hello varlık ile ilişkili toocreate girişimde bulunuldu.
* Bir girişim yapıldı toocreate yapılan bir Bulucu tooan 5 bulucular zaten kullanımda olan varlık. (Azure depolama bir depolama kapsayıcısı üzerinde beş paylaşılan erişim ilkeleri hello sınırının zorlar.)
* Bir varlık tooan IngestManifestAsset depolama hesabına bağlama hello depolama hesabıyla aynı kullanılan hello hello üst IngestManifest tarafından değil.  

## <a name="500-internal-server-error"></a>500 İç sunucu hatası
Merhaba hello istek işlenirken, Media Services hello işleme devam etmesini engelleyen bazı hatayla karşılaşıyor. Bu son olabilir nedenleri aşağıdaki hello tooone:

* Merhaba Media Services hesabın hizmet kota bilgileri geçici olarak kullanılamadığından bir varlık veya iş oluşturma başarısız olur.
* Merhaba hesabın depolama hesabı bilgilerini geçici olarak kullanılamadığından bir varlık veya IngestManifest blob depolama kapsayıcısını oluşturma başarısız olur.
* Diğer beklenmeyen hata oluştu.

## <a name="503-service-unavailable"></a>503 Hizmet kullanılamıyor
Merhaba, şu anda işleyemiyor tooreceive istekleri sunucusudur. Aşırı istekleri toohello hizmeti tarafından bu hataya neden. Media Services mekanizması azaltma hello kaynak kullanımı aşırı isteği toohello hizmet uygulamalar için sınırlar.

> [!NOTE]
> Aldığınız hello nedeni hakkında daha ayrıntılı bilgi onay hello hata iletisi ve hata kodu dize tooget hello 503 hatası. Bu hata, azaltma her zaman gelmez.
> 
> 

Olası durum açıklamaları şunlardır:

* "Sunucu meşgul. Bu istek türü önceki çalışmalarını birden çok {0} saniye sürdü."
* "Sunucu meşgul. Birden çok saniyede {0} istekler kısıtlanan."
* "Sunucu meşgul. Fazlasını {0} istekleri {1} saniye içinde kısıtlanan."

toohandle bu hatayı üstel geri alma yeniden deneme mantığı kullanılmasını öneririz. Ardışık hata yanıtları denemeler arasındaki aşamalı olarak uzun bekler kullanarak anlamına gelir.  Daha fazla bilgi için bkz: [geçici hata işleme uygulama blok](https://msdn.microsoft.com/library/hh680905.aspx).

> [!NOTE]
> Kullanıyorsanız [.Net için Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services/tree/master), hello hello 503 hatası için yeniden deneme mantığı hello SDK tarafından uygulandıktan.  
> 
> 

## <a name="see-also"></a>Ayrıca Bkz.
[Yönetim hata kodları medya Hizmetleri](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

