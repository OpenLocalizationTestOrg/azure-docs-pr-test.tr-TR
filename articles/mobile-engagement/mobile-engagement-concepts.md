---
title: "aaaMobile Engagement kavramları | Microsoft Docs"
description: "Azure Mobile Engagement kavramları"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Azure Mobile Engagement kavramları
Mobile Engagement birkaç kavram ortak tooall desteklenen platformları tanımlar. Bu makalede, söz konusu kavramlar kısaca açıklanmaktadır.

Yeni tooMobile katılım olduğunda bu makale iyi bir başlangıç noktasıdır. Daha fazla bilgi ve örnekler yanı sıra olası sınırlamaları sunarak bu makalede açıklanan hello kavramları netleştirecektir Ayrıca, kullanmakta olduğunuz emin tooread hello belgeleri belirli toohello platform haline.

## <a name="devices-and-users"></a>Cihazlar ve kullanıcılar
Mobile Engagement, her cihaz için benzersiz bir tanımlayıcı oluşturarak kullanıcıları tanımlar. Bu tanımlayıcı hello cihaz tanımlayıcısı olarak adlandırılır (veya `deviceid`). Çalışan tüm uygulamaların Merhaba, aynı yolla oluşturulan cihaz paylaşımı hello aynı cihaz tanımlayıcısı.

Örtük olarak, Mobile Engagement bir cihazı toobelong tooexactly bir kullanıcı olarak değerlendirir ve bu nedenle, kullanıcıların ve aygıtların eşdeğer kavramlar şeklinde anlamına gelir.

## <a name="sessions-and-activities"></a>Oturumlar ve etkinlikler
Bir oturum, hello kullanıcı durmasına kadar kullanarak Merhaba uygulaması hello zaman hello kullanıcıdan bir kullanıcı tarafından gerçekleştirilen bir kullanımını başlatır değil.

Bir etkinlik tek bir kullanıcı tarafından gerçekleştirilen hello uygulamanın belirli bir alt bölümü kullanımıdır (genellikle bir ekran bağlıdır, ancak herhangi bir şey uygun toohello uygulaması olabilir).

Bir kullanıcı, bir seferde yalnızca bir etkinlik gerçekleştirebilir.

Bir etkinlik adı (sınırlı too64 karakter) tarafından tanımlanır ve isteğe bağlı olarak bazı ek veriler (Merhaba 1024 bayt) eklenebilir.

Oturumlar, kullanıcılar tarafından gerçekleştirilen etkinliklerin hello serisinden otomatik olarak hesaplanır. Merhaba kullanıcı ilk etkinliğini başlar ve kendisine son etkinliğini bitirdiğinde durur bir oturum başlatır. Başka bir deyişle, bir oturumun açıkça başlatılan veya durdurulan toobe gerekmez. Bunun yerine, etkinlikler açıkça başlatılır veya durdurulur. Hiçbir etkinlik bildirilmezse, hiçbir oturum da bildirilmez.

## <a name="events"></a>Olaylar
Kullanılan tooreport anlık eylemleri (basılan düğme veya kullanıcılar tarafından okunan makaleler gibi) olaylardır.

Bir olay ilgili toohello geçerli oturum işi, tooa olabilir veya tek başına bir olay olabilir.

Bir olay adı (sınırlı too64 karakter) tarafından tanımlanır ve isteğe bağlı olarak bazı ek veriler (Merhaba 1024 bayt) eklenebilir.

## <a name="error"></a>Hata
Hataları (yanlış kullanıcı eylemleri veya API çağrısı hataları gibi) hello uygulama tarafından doğru şekilde algılanan kullanılan tooreport sorunlardır.

İlgili toohello geçerli oturum tooa işi, bir hata olabilir veya tek başına bir hata olabilir.

Hata bir ad (sınırlı too64 karakter) tarafından tanımlanır ve isteğe bağlı olarak bazı ek veriler (Merhaba 1024 bayt) eklenebilir.

## <a name="job"></a>İş
İşlerini olan bir süresi olan kullanılan tooreport eylemleri (API çağrılarının süresi gibi görüntüleme süresi, reklamların gösterilme, arka plan görevlerinin süresi veya kullanıcı eylemlerinin süresi).

Bir görev herhangi bir kullanıcı etkileşimi olmadan hello arka planda gerçekleştirilebildiğinden bir iş ilgili tooa oturum değil.

Bir iş adıyla (sınırlı too64 karakter) tanımlanır ve isteğe bağlı olarak bazı ek veriler (Merhaba 1024 bayt) eklenebilir.

## <a name="crash"></a>Kilitlenme
Kilitlenme hello burada hello uygulama tarafından algılanmayan sorunların olun hataları kilitlenme Mobile Engagement SDK'sı tooreport uygulama tarafından otomatik olarak verilir.

## <a name="application-information"></a>Uygulama bilgileri
Uygulama bilgileri (veya uygulama bilgisi) bazı veri toohello kullanıcıları (Bu, benzer tooweb tanımlama bilgileri, uygulama bilgileri hello hello Azure Mobile Engagement platformunda sunucu tarafında depolanır) bir uygulamanın kullanılan tootag kullanıcılar, diğer bir deyişle, tooassociate içindir.

Uygulama bilgileri, Mobile Engagement SDK API'si hello kullanarak veya hello Mobile Engagement platformu cihaz API'si kullanılarak kaydedilebilir.

Uygulama bilgileri bir anahtar/değer çifti ilişkili tooa aygıttır. başlangıç anahtarı hello hello uygulama bilgileri (sınırlı too64 ASCII harf [a-zA-Z], rakamlar [0-9] ve alt çizgi [_]) adıdır. Merhaba değer (sınırlı too1024 karakter), dize, tamsayı, tarih (yyyy-aa-gg) veya Boolean (true veya false) olabilir.

Herhangi bir sayıda uygulama bilgisi hello Mobile Engagement fiyatlandırma koşulları tarafından tanımlanan hello sınırları içinde ilişkili tooa cihaz olabilir. Belirli bir anahtar için Mobile Engagement yalnızca hello son değer kümesini (Geçmiş yok) izler. Ayarlama veya bir uygulama bilgisi hello değerinin değiştirilmesi Mobile Engagement toore zorlar-bu uygulama üzerinde ayarlanmış hedef kitle ölçüt değerlendirme yani uygulama bilgileri bilgileri (varsa), kullanılan tootrigger gerçek zamanlı gönderimleri olabilir.

## <a name="extra-data"></a>Ek veriler
Ek veriler (veya ekler) ekli tooevents, hatalar, etkinlikler ve işler olabilecek bazı rastgele verilerdir.

Ek özellikler yapılandırılır benzer şekilde tooJSON nesneleri: anahtar/değer çiftleri ağacının yapılır. Anahtarları: sınırlı too64 ASCII harf [a-zA-Z], rakamlar [0-9] ve alt çizgi [_]) ve hello toplam boyutu (kez hello Mobile Engagement SDK'sı tarafından JSON'da kodlanmış) sınırlı too1024 karakter.

Merhaba oluşan ağacın tamamı anahtar/değer çiftlerinin bir JSON nesnesi olarak depolanır. Erişilebilir toosome işlevleri Segmentler gibi gelişmiş doğrudan yine de, yalnızca hello ilk anahtarları/değerleri ayrıştırılmış toobe düzeyidir (örneğin, kolayca, en az 10 kez hello olay gönderen tüm kullanıcılardan oluşan "Bilim Kurgu severler" adlı bir segment tanımlayabilirsiniz Merhaba ek anahtarı "content_type" olan "content_viewed" kümesi toohello değer "Bilim Kurgu" hello, geçen ay olarak adlandırılır). Bu nedenle (örneğin, dizeler, tarihler, tamsayı veya Boolean) skaler değerler kullanan anahtar/değer çiftleri basit listelerinden yapılmış toosend yalnızca ek özellikler önerilir.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Mobile Engagement için Windows Evrensel SDK’ya genel bakış](mobile-engagement-windows-store-sdk-overview.md)
* [Azure Mobile Engagement için Windows Phone Silverlight SDK’sına genel bakış](mobile-engagement-windows-phone-sdk-overview.md)
* [Azure Mobile Engagement için iOS SDK’sı](mobile-engagement-ios-sdk-overview.md)
* [Azure Mobile Engagement için Android SDK’sı](mobile-engagement-android-sdk-overview.md)

