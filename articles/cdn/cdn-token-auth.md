---
title: "belirteç kimlik doğrulama ile aaaSecuring Azure CDN varlıklar | Microsoft Docs"
description: "Belirteç kimlik doğrulama toosecure erişim tooyour Azure CDN varlıklar kullanma."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>Azure CDN varlıklar belirteci kimlik doğrulaması ile güvenli hale getirme

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>Genel Bakış

Belirteç kimlik doğrulama tooprevent Azure CDN varlıklar toounauthorized istemcilerine hizmet etmesini sağlayan bir mekanizmadır.  Bu genellikle tooprevent "hotlinking", ileti panosu genellikle, farklı bir Web izniniz olmadan varlıklarınızı nerede kullanır, içeriği gerçekleştirilir.  Bu içerik teslim maliyetleriniz üzerinde etkisi olabilir. Bu özelliği CDN etkinleştirerek, istekleri CDN kenarı hello içerik teslim etmeden POP tarafından doğrulanır. 

## <a name="how-it-works"></a>Nasıl çalışır?

Belirteç kimlik doğrulama isteklerini hello isteyenin kodlanmış bilgilerini içeren bir belirteç değeri istekleri toocontain kılarak güvenilen bir site tarafından oluşturulan doğrular. Merhaba bilgi karşılayan hello gereksinimleri şifrelendiğinde içeriği yalnızca toorequester sunulacak, aksi takdirde isteği reddedilir. Aşağıdaki bir veya birden çok parametre kullanarak hello gereksinimini ayarlayabilirsiniz.

- Ülke: izin ver veya belirtilen ülkelerden kaynaklanan istekleri reddedin.  [Geçerli ülke kodlarının listesi.](https://msdn.microsoft.com/library/mt761717.aspx) 
- URL: yalnızca belirtilen varlık veya yol toorequest izin verir.  
- Ana bilgisayarı: izin ver veya hello istek başlığında belirtilen ana kullanan isteklerinin reddedin.
- Başvuran: izin ver veya Reddet belirtilen başvuran toorequest.
- IP adresi: yalnızca belirli bir IP adresi veya IP alt ağı kaynaklanan istekleri izin verin.
- Protokol: izin verin veya hello protokolünü temel blok istekleri toorequest hello içerik kullanılır.
- Süre sonu: bir tarih atamak ve bir bağlantı yalnızca sınırlı bir süre için geçerli olmaya devam ettiğinden dönem tooensure saat.

Her bir parametreyi ayrıntılı yapılandırma örneği bakın.

## <a name="reference-architecture"></a>Başvuru mimarisi

Web uygulamanız ile CDN toowork belirteci kimlik doğrulamasını ayarlama referans mimarisi aşağıya bakın.

![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>CDN uç noktasında belirteci Doğrulama mantığı
    
Bu grafik, nasıl Azure CDN belirteci kimlik doğrulaması CDN uç yapılandırıldığında, istemci isteği doğrular açıklar.

![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Belirteç kimlik doğrulamayı ayarlama

1. Merhaba gelen [Azure portal](https://portal.azure.com), tooyour CDN profili göz atın ve hello ardından **Yönet** düğmesini toolaunch hello ek portal.

    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-rules-engine/cdn-manage-btn.png)

2. Üzerine gelerek **HTTP büyük**ve ardından **belirteci Auth** hello çıkma içinde. Şifreleme anahtarı ve bu sekmedeki şifreleme parametreleri ayarlayacaksınız.

    1. Benzersiz bir şifreleme anahtarı için girin **birincil anahtar**.  İçin başka bir girin **yedekleme anahtarı**

        ![CDN belirteci auth kurulum anahtarı](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. Şifreleme parametreleri şifreleme aracıyla ayarlayın (izin ver veya Reddet istekleri göre süre sonu, ülke, başvuran, protokol, istemci IP. "Herhangi bir birleşimini kullanabilirsiniz.)

        ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - EC-sona: bir belirteç sona erme süresi belirli bir süre sonra atar. Merhaba süre sonu zamanı reddedilir sonra gönderilen istek sayısı. Bu parametre UNIX zaman damgası kullanır (standart dönemi: 1/1/1970'ten beri geçen saniye göre 00:00:00 GMT. "Çevrimiçi araçları tooprovide dönüştürme Standart Saati UNIX zaman arasında kullanabilirsiniz.)  Örneğin, Yukarı tooset istiyorsanız hello belirteci toobe 31/12/2016 süresi 12:00:00 GMT, hello UNIX saat: 1483185600 aşağıdaki gibi kullanın:
    
        ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - EC url izin: tootailor belirteçleri tooa belirli varlık veya yolu sağlar. Erişim toorequests URL'si Başlat belirli bir göreli yol kısıtlar. Her yol virgül ile ayırarak birden fazla yol girebilirsiniz. URL'leri büyük/küçük harfe duyarlıdır. Merhaba gereksinimi bağlı olarak farklı bir değer tooprovide farklı erişim düzeyini ayarlayabilir. Aşağıda birkaç senaryo vardır:
        
            Bir URL varsa: http://www.mydomain.com/pictures/city/strasbourg.png. Giriş değeri bkz: "" ve buna göre erişim düzeyi

            1. Giriş değeri "/": tüm istekleri izin verilir
            2. Giriş değeri "/ resim": istekleri izleyen tüm hello izin ver olabilir
            
                - http://www.mydomain.com/Pictures.PNG
                - http://www.mydomain.com/Pictures/City/strasbourg.PNG
                - http://www.mydomain.com/picturesnew/City/strasbourgh.PNG
            3. Giriş değeri "/ resimler /": /pictures/ izin verilmesi yalnızca istekleri
            4. Giriş değeri "/ pictures/city/strasbourg.png": yalnızca bu varlık için istek sağlar
    
        ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - AB Ülke izin: yalnızca bir veya daha fazla belirtilen ülkelerden kaynaklanan isteklere izin verir. Diğer tüm ülkelerden kaynaklı istekler reddedilir. Ülke kodu tooset hello parametreleri ve her ülke kodu virgül ile ayırarak kullanın. Örneğin, Amerika Birleşik Devletleri ve Fransa tooallow erişmek istiyorsanız, BİZE FR hello sütununda girin.  
        
        ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - AB Ülke reddetme: bir veya daha fazla belirtilen ülkelerden kaynaklanan istekleri reddeder. Diğer tüm ülkelerden kökenli isteklerine izin verilir. Ülke kodu tooset hello parametreleri ve her ülke kodu virgül ile ayırarak kullanın. Örneğin, Amerika Birleşik Devletleri ve Fransa toodeny erişmek istiyorsanız, BİZE hello sütununda FR girin.
    
        - EC ref izin: yalnızca belirtilen başvuran isteklere izin verir. Bir başvuran hello web sayfasının, istenen toohello kaynak bağlı hello URL'sini tanımlar. Merhaba başvuran parametre değeri hello Protokolü içermemelidir. Bir ana bilgisayar adı ve/veya bu ana bilgisayar üzerinde belirli bir yol girebilirsiniz. Ayrıca, her biri virgül ile ayırarak tek bir parametre içinde birden çok başvuran ekleyebilirsiniz. Bir başvuran değer belirttiniz, ancak hello başvuran bilgileri toosome tarayıcı yapılandırması nedeniyle hello isteğindeki gönderilmez, bu istekleri varsayılan olarak reddedilir. Başvuran bilgileri eksik olan bu istekleri "Eksik" veya hello parametresi tooallow boş bir değer atayabilirsiniz. Aynı zamanda "*. consoto.com" tooallow consoto.com tüm alt etki alanları.  Örneğin, www.consoto.com, consoto2.com ve boş veya eksik reffers ile erquests altındaki tüm alt etki gelen istekleri için tooallow erişmek istiyorsanız, aşağıda değeri giriş:
        
        ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - EC ref reddetme: Belirtilen başvuran istekleri reddeder. Toodetails ve "AB-ref-izin ver" parametresi örnekte bakın.
         
        - EC proto izin: yalnızca belirtilen protokol gelen isteklere izin verir. Örneğin, http veya https.
        
        ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - EC proto reddetme: Belirtilen protokolünden istekleri reddeder. Örneğin, http veya https.
    
        - EC clientip: erişim toospecified sahibinin IP adresi kısıtlar. IPv4 ve IPv6 desteklenir. Tek istek IP adresi veya IP alt ağı belirtebilirsiniz.
            
        ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. Belirtecinizi hello tanımı aracıyla test edebilirsiniz.

    4. İstek reddedildiğinde toouser dönen yanıtının türünü hello özelleştirebilirsiniz. Varsayılan olarak 403 kullanırız.

3. Şimdi **kurallar altyapısı** altında sekmesinde **HTTP büyük**. Sekmesini toodefine yolları tooapply hello ve bu özelliği kullanın, hello belirteç kimlik doğrulama özelliği etkinleştirmek, etkinleştirme ek belirteci kimlik doğrulaması ile ilgili özellikler.

    - "IF" sütun toodefine varlık veya tooapply belirteci kimlik doğrulaması istediğiniz yolu kullanın. 
    - Tooadd "Belirteci Auth" Merhaba özelliği açılır tooenable belirteci kimlik doğrulaması'ndan ' ı tıklatın.
        
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. Merhaba, **kurallar altyapısı** sekmesinde, etkinleştirebilirsiniz birkaç ek özellikler vardır.
    
    - Belirteç kimlik doğrulama reddi kod: hello bir istek reddedildiğinde toouser dönen yanıtının türünü belirler. Burada ayarlanan kuralları hello belirteci auth sekmesinde hello reddi kodu ayarı geçersiz kılar.
    - Belirteç kimlik doğrulama yoksay: kullanılan URL toovalidate belirteci büyük küçük harfe duyarlı olup olmayacağını belirler.
    - Belirteç kimlik doğrulama parametresi: hello belirteci auth sorgu dizesi parametresi hello gösteren istenen URL yeniden adlandırın. 
        
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-token-auth/cdn-rules-engine2.png)

5. Belirteç tabanlı kimlik doğrulama özellikleri için belirteci oluşturan bir uygulama olan belirtecinizi özelleştirebilirsiniz. Kaynak kodu erişilebilir burada içinde [GitHub](https://github.com/VerizonDigital/ectoken).
Kullanılabilir diller şunlardır:
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Azure CDN özellikler ve fiyatlandırma sağlayıcısı

Merhaba bkz [CDN'ye genel bakış](cdn-overview.md) konu.
