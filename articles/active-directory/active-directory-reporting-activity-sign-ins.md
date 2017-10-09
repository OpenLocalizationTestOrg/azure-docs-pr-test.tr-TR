---
title: "hello Azure Active Directory portalında aaaSign bileşenini etkinlik raporları | Microsoft Docs"
description: "Hello Azure Active Directory portalında giriş toosign bileşenini etkinlik raporları"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Hello Azure Active Directory portalında oturum açma etkinliği raporları

Azure Active Directory (Azure AD) hello Raporlama ile [Azure portal](https://portal.azure.com), toodetermine ortamınızı nasıl yapılması gereken hello bilgi edinebilirsiniz.

Raporlama mimarisi Azure Active Directory'de hello bileşenleri aşağıdaki Merhaba oluşur:

- **Etkinlik** 
    - **Oturum açma etkinliklerini** – yönetilen uygulamalar ve kullanıcı oturum açma etkinliklerini hello kullanımı hakkında bilgi
    - **Denetim günlükleri**: Kullanıcılar ve grup yönetimi, yönetilen uygulamalarınız ve dizin etkinlikleriniz hakkında sistem etkinliği bilgileri.
- **Güvenlik** 
    - **Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir. Daha fazla bilgi için bkz. Riskli oturum açma işlemleri.
    - **Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir. Daha fazla bilgi için bkz. Riskli oldukları belirlenen kullanıcılar.

Bu konuda, oturum açma hello etkinlikleri genel bir bakış sağlar.

## <a name="pre-requisite"></a>Önkoşul

### <a name="who-can-access-hello-data"></a>Merhaba veri erişebilecek mi?
* Merhaba Güvenlik Yöneticisi veya güvenlik okuyucu roldeki kullanıcılar
* Genel Yöneticiler
* Tüm kullanıcılar (yönetici olmayan) kendi oturum açma etkinliklerine erişebilirler 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>Hangi Azure AD lisans tooaccess oturum açma etkinliği gerekiyor mu?
* Kiracı kendisiyle ilişkili bir Azure AD Premium lisansına sahip olması gerekir toosee hello tüm kadar oturum açma etkinliği raporu


## <a name="signs-in-activities"></a>Oturum açma etkinlikleri

Oturum açma Hello kullanıcı raporu tarafından sağlanan hello bilgilerle yanıtlar tooquestions gibi bulun:

* Bir kullanıcı oturum açma hello desenini nedir?
* Bir hafta içerisinde kaç adet kullanıcı oturum açtı?
* Bu oturum açma işlemleri hello durumu nedir?

Verilerin ilk giriş noktası tooall oturum açma etkinliklerinizi **oturum açma işlemleri** hello etkinlik bölümünde **Azure Active**.


![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/61.png "oturum açma etkinliği")


Denetim günlüklerinin aşağıdakileri gösteren bir varsayılan liste görünümü vardır:

- Merhaba ilgili kullanıcı
- Merhaba uygulama hello kullanıcısı için açan
- Merhaba oturum açma durumu
- Merhaba oturum açma zamanı

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/41.png "oturum açma etkinliği")

Tıklatarak hello liste görünümü özelleştirebilirsiniz **sütunları** hello araç.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/19.png "oturum açma etkinliği")

Bu toodisplay ek alanlar etkinleştirir veya zaten görüntülenen alanları kaldırın.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/42.png "oturum açma etkinliği")

Merhaba liste görünümünde bir öğeyi tıklatarak bunu hakkında tüm kullanılabilir ayrıntıları alın.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/43.png "oturum açma etkinliği")


## <a name="filtering-sign-in-activities"></a>Oturum açma etkinliklerini filtreleme

Merhaba aşağı toonarrow veri tooa düzeyinde çalışır, alanları izleyen hello kullanarak hello gerçekleştirilen oturum açma verileri filtreleyebilirsiniz bildirdi:

- Zaman aralığı
- Kullanıcı
- Uygulama
- İstemci
- Oturum açma durumu

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/44.png "oturum açma etkinliği")


Merhaba **zaman aralığı** filtre etkinleştirir tooyou toodefine hello için bir zaman çerçevesi veri döndürdü.  
Olası değerler şunlardır:

- 1 ay
- 7 gün
- 24 saat
- Özel

Özel bir zaman çerçevesi seçerken başlangıç ve bitiş zamanını yapılandırabilirsiniz.

Merhaba **kullanıcı** filtresini etkinleştirir, size, toospecify hello adı veya hello kullanıcı asıl adı (UPN) önem verdiğiniz hello kullanıcı.

Merhaba **uygulama** filtre önem verdiğiniz hello uygulamasının toospecify hello adı sağlar.

Merhaba **istemci** filtre toospecify önem verdiğiniz hello cihaz hakkında bilgi sağlar.

Merhaba **oturum açma durumu** filtre filtre aşağıdaki Merhaba, tooselect sağlar:

- Tümü
- Başarılı
- Hata


## <a name="sign-in-activities-shortcuts"></a>Oturum açma etkinlikleri kısayolları

Ayrıca Active Directory tooAzure, hello Azure portal, iki ek giriş noktaları toosign bileşenini etkinlikleri verilerle sağlar:

- Kullanıcılar ve gruplar
- Kurumsal uygulamalar


### <a name="users-and-groups-sign-ins-activities"></a>Kullanıcı ve grupların oturum açma etkinlikleri

Oturum açma Hello kullanıcı raporu tarafından sağlanan hello bilgilerle yanıtlar tooquestions gibi bulun:

- Bir kullanıcı oturum açma hello desenini nedir?
- Bir hafta içerisinde kaç adet kullanıcı oturum açtı?
- Bu oturum açma işlemleri hello durumu nedir?



Giriş noktası toothis verilerinizi hello kullanıcı oturum açma grafiğinde hello olan **genel bakış** altında bölümünde **kullanıcılar ve gruplar**.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/45.png "oturum açma etkinliği")

oturum açma Hello kullanıcı grafik gösterir oturum haftalık toplamalarının belirli bir süre içinde tüm kullanıcılar için bileşenler. hello için Hello varsayılan süre 30 gündür.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/46.png "oturum açma etkinliği")

Oturum açma hello grafikteki bir günde tıkladığınızda, bu günlük hello oturum açma etkinliklerini ayrıntılı bir listesini alın.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/41.png "oturum açma etkinliği")

Her satırda bir seçili hello oturum açma gibi hakkında ayrıntılı bilgi hello hello oturum açma etkinlikleri listesi sağlar:

* Kim oturum açtı?
* Merhaba neydi UPN ilgili?
* Hangi uygulama hello oturum açma hello hedefi neydi?
* Başlangıç IP adresi hello oturum açma nedir?
* Merhaba oturum açma hello durumu neydi?

Merhaba **oturum açma işlemleri** seçeneği tüm kullanıcı oturum açma işlemlerine eksiksiz bir genel bakış sunar.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/51.png "oturum açma etkinliği")



## <a name="usage-of-managed-applications"></a>Yönetilen uygulamaların kullanımı

Oturum açma bilgilerinizin uygulama odaklı bir görünümüyle aşağıdakiler gibi sorular yanıtlanabilir:

* Uygulamalarımı kimler kullanıyor?
* Kuruluşunuzdaki hello üst 3 uygulamaları nelerdir?
* Kısa bir süre önce bir uygulamayı kullanıma sundum. Uygulamanın durumu nedir?

Giriş noktası toothis verilerinizi hello üst 3 uygulamalarında hello son 30 gün raporda hello kuruluşunuzda olan **genel bakış** altında bölümünde **kurumsal uygulamalar**.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/64.png "oturum açma etkinliği")

belirli bir süre içinde ilk 3 uygulamalarınız için oturum açmalar Hello uygulama kullanım grafiği haftalık toplamalarının. hello için Hello varsayılan süre 30 gündür.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/47.png "oturum açma etkinliği")

İsterseniz, belirli bir uygulama hello odak ayarlayabilirsiniz.


![Raporlama](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")

Merhaba uygulama kullanım grafiği bir günde tıkladığınızda hello oturum açma etkinliklerini ayrıntılı bir listesini alın.


![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/48.png "oturum açma etkinliği")


Merhaba **oturum açma işlemleri** seçeneği tüm oturum açma olayları tooyour uygulamaları eksiksiz bir genel bakış sunar.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/49.png "oturum açma etkinliği")



## <a name="next-steps"></a>Sonraki adımlar

Merhaba tooknow oturum açma etkinliği hata kodları hakkında daha fazla bilgi istiyorsanız bkz [oturum açma etkinliği raporu hata kodları hello Azure Active Directory portalında](active-directory-reporting-activity-sign-ins-errors.md).

