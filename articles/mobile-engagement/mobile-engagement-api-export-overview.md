---
title: "aaaMobile katılım verme API genel bakış"
description: "Ham verilerinizi dışarı aktarma hakkında hello temelleri kendi araçlarında oluşturan kullanıcı aygıtları tooleverage tarafından öğrenin"
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Mobil katılım verme API genel bakış
## <a name="introduction"></a>Giriş
Bu belgede, ham verileri dışarı aktarma hakkında hello temelleri kendi araçlarında oluşturan kullanıcı aygıtları tooleverage tarafından öğreneceksiniz.

## <a name="pre-requisites"></a>Ön koşullar
Mobile Engagement'tan Hello ham verileri dışarı aktarma gerektirir:

* API kimlik doğrulama Kurulumu toobe mümkün toouse hello API'leri (bkz [kimlik doğrulama el ile kuruluma](mobile-engagement-api-authentication-manual.md)),
* Merhaba REST API'leri veya hello kullan [.net SDK](mobile-engagement-dotnet-sdk-service-api.md),
* Bir Azure depolama hesabı.

> [!NOTE]
> Biz de hello mükemmel bildirmek [Microsoft Azure Storage Gezgini](http://storageexplorer.com/), en az hello geliştirme aşaması sırasında kolay bir toouse UI Azure Storage ile etkileşmek için sağlar.
> 
> 

## <a name="what-can-be-exported"></a>Ne verilebilir mi?
Mobile Engagement, kullanıcıların toocollect pek çok veri türünü sağlar ve bu nedenle verme çeşitli türlerde toothese farklı veri türleri uygun sahip.
Dışarı aktarma 2 temel türleri şunlardır:

* Anlık görüntü: genellikle bir durumu temsil eden ve Mobile Engagement bir geçmişini yok tooexport veri kullanılır. Bu etiketler (app-info) belirteçleri veya itme kampanya geribildirimler örneğin içerir. Sonuç olarak bu tür verme olmayan ilgili tooa tarih.
* Geçmiş: Bu dışarı aktarma türü olayları veya etkinlikleri gibi zamana örneğin öğelerden veriler için kullanılır.

Merhaba tabloda ayrıntısına tüm hello olası dışarı açıklanmaktadır:

| Dışarı aktarma türü | Veri türü | Açıklama |
| --- | --- | --- |
| Anlık Görüntü |İstek bildirimi |Anında iletme kampanyalarını geribildirimler başına DeviceID/UserID temelinde verilmesini oluşturur |
| Anlık Görüntü |Etiket |Bir verme hello ilişkili etiketleri (app-info) tooeach aygıtların oluşturur |
| Anlık Görüntü |Cihaz |Merhaba technicals (modeli, yerel ayar, saat dilimi,...), hello etiketleri, ilk görülen zamanı gibi cihazlar hakkında hello verilerin çoğu verilmesini oluşturur... |
| Anlık Görüntü |Belirteç |Tüm hello geçerli belirteçleri verme oluşturur |
| Geçmiş |Etkinlik |Belirli bir süre üzerinde her cihazlar için tüm hello etkinlikleri verme oluşturur |
| Geçmiş |Olay |Belirli bir süre üzerinde her cihazlar için tüm hello etkinlikleri verme oluşturur |
| Geçmiş |İş |Her cihaz için tüm hello işleri verme üzerinde belirli bir süre oluşturur |
| Geçmiş |Hata |Belirli bir süre üzerinde her cihazlar için tüm hello hataları verme oluşturur |

## <a name="how-does-it-work"></a>Nasıl çalışır?
Dışarı aktarma uzun çalışan görevler büyük veri dosyalarını oluşturabilir. Bu nedenle, çağrılan tooreturn hemen bir dosya toodownload olamazlar.
Sipariş tooexport verilerden Mobile Engagement, toocreate olacaktır bir **dışarı aktarma işi** genellikle belirlediğiniz API aracılığıyla:

* dışarı aktarma (anlık görüntü veya geçmiş) Hello türü
* Merhaba veri türü
* Merhaba **Azure depolama kapsayıcısının** (yazma erişimi olan geçerli bir SAS dahil) hello verme hello sonucunu yazılacağı.
* Örneğin örnek kapsayıcı URL parametresi https://[StorageAccountName].blob.core.windows.net/[ContainerName olacaktır]? [SASWritePermissionsToken]  

Gerçek dünya örneği aşağıda verilmiştir. https://testazmeexport.BLOB.Core.Windows.NET/test1234azme?sv=2015-12-11&SS=b&SRT=SCO&SP=rwdlac&SE=2016-12-17T04:59:26Z & st = 2016-12-16T20:59:26Z & spr https = & SIG = KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q % 3B

Lütfen başlatıldı, iş toobe birkaç dakika sürebilir ve ardından gelen çok fazla kullanıcı ya da etkinlik uygulamalarla için çok küçük uygulamaları tooseveral saat birkaç saniye çalışabilir unutmayın.

Merhaba işi oluşturulduktan sonra olası toocheck olduğundan hala çalışıyor veya Tamamlandı durumunda ise, durumu toosee.

Merhaba iş başarılı sonra hello ortaya çıkan veri dosyası depolama kapsayıcısı sağlanan hello üzerinde kullanılabilir.

