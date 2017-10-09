---
title: "kimlik doğrulaması ve Azure MFA sunucusu aaaIIS | Microsoft Docs"
description: "Bu, IIS kimlik doğrulaması ve Azure multi-Factor Authentication Sunucusu'nu dağıtmada yardımcı olacak hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>IIS web uygulamaları için Azure Multi-Factor Authentication Sunucusu

Microsoft IIS web uygulamaları ile tümleştirme için IIS kimlik doğrulamasını yapılandırma ve hello Azure çok faktörlü kimlik doğrulama (MFA) sunucusu tooenable Hello IIS kimlik doğrulaması bölümü kullanın. Hello Azure MFA sunucusu toohello IIS web sunucusu tooadd Azure çok faktörlü kimlik doğrulaması yapılan istekleri filtreleyebilirsiniz bir eklenti yükler. Merhaba IIS eklentisi Form tabanlı kimlik doğrulaması ve tümleşik Windows HTTP kimlik doğrulaması için destek sağlar. Güvenilen IP'leri yapılandırılmış tooexempt iç IP adreslerinden iki öğeli kimlik doğrulama da olabilir.

![IIS Kimlik Doğrulaması](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication Sunucusu ile Form Tabanlı IIS Kimlik Doğrulaması kullanma
bir IIS web form tabanlı kimlik doğrulaması kullanan uygulaması, hello IIS web sunucusunda hello Azure multi-Factor Authentication sunucusu yükleme ve yapılandırma toosecure sunucu aşağıdaki yordamı hello hello:

1. Hello Azure multi-Factor Authentication sunucusu, hello hello soldaki menüde IIS kimlik doğrulaması simgesine tıklayın.
2. Merhaba tıklatın **Form tabanlı** sekmesi.
3. **Ekle**'ye tıklayın.
4. toodetect kullanıcı adı, parola ve etki alanı değişkenlerini otomatik olarak hello form tabanlı Web sitesi iletişim kutusunda hello oturum açma URL'si (örneğin, https://localhost/contoso/auth/login.aspx) girin ve tıklayın **Tamam**.
5. Merhaba denetleyin **multi-Factor Authentication iste kullanıcı eşleşme** tüm kullanıcılar Sunucu'ya aktarılmışsa ya da hello sunucu ve konu toomulti faktörlü kimlik doğrulaması olarak içeri aktarılacak varsa kutusu. Çok sayıda kullanıcı sunucu hello henüz içeri aktarılmadı ve/veya multi-Factor authentication'da muaf tutulacaksa hello kutunun işaretini kaldırın.
6. Merhaba sayfa değişkenleri otomatik olarak algılanamaz ise tıklatın **el ile belirt** hello form tabanlı Web sitesi iletişim kutusunda.
7. Hello form tabanlı Web sitesi iletişim kutusunda, hello URL toohello oturum açma sayfasına hello URL Gönder alanına ve (isteğe bağlı) bir uygulama adı girin. Merhaba uygulama adı Azure multi-Factor Authentication raporlarında görünür ve SMS veya mobil uygulama kimlik doğrulama iletilerinde görüntülenebilir.
8. Merhaba doğru istek biçimini seçin. Bu çok ayarlanır**POST veya GET** çoğu web uygulamaları için.
9. Merhaba kullanıcı adı değişkenini, parola değişkenini ve etki alanı değişkenini (Merhaba oturum açma sayfasında görünürse) girin. Merhaba toofind hello adlarını giriş kutuları, bir web tarayıcısında toohello oturum açma sayfasına gidin, hello sayfada sağ tıklamanız ve seçin **kaynağı görüntüle**.
10. Merhaba denetleyin **Azure multi-Factor Authentication iste kullanıcı eşleşme** tüm kullanıcılar Sunucu'ya aktarılmışsa ya da hello sunucu ve konu toomulti faktörlü kimlik doğrulaması olarak içeri aktarılacak varsa kutusu. Çok sayıda kullanıcı sunucu hello henüz içeri aktarılmadı ve/veya multi-Factor authentication'da muaf tutulacaksa hello kutunun işaretini kaldırın.
11. Tıklatın **Gelişmiş** tooreview dahil olmak üzere, Gelişmiş ayarları:

  - Özel bir reddetme sayfa dosyası seçme
  - Tanımlama bilgilerini kullanarak bir süre için önbellek başarılı kimlik doğrulamalarını toohello Web sitesi
  - Bir Windows etki alanına göre LDAP dizini tooauthenticate hello birincil kimlik bilgileri olup olmadığını seçin. RADIUS sunucusuna göre mi doğrulanacağını belirtin.

12. Tıklatın **Tamam** tooreturn toohello form tabanlı Web sitesi iletişim kutusu.
13. **Tamam** düğmesine tıklayın.
14. Bir kez URL Merhaba ve sayfa değişkenleri algılandığında veya girildiğinde, hello Web sitesi verileri Form tabanlı panel hello görüntüler.

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication Sunucusu ile Tümleşik Windows Kimlik Doğrulaması kullanma
bir IIS tümleşik Windows HTTP kimlik doğrulaması kullanan uygulamayı web, hello Azure MFA sunucusu hello IIS web sunucusuna yükleyin ve ardından yapılandırma toosecure, aşağıdaki adımları hello ile sunucu hello:

1. Hello Azure multi-Factor Authentication sunucusu, hello hello soldaki menüde IIS kimlik doğrulaması simgesine tıklayın.
2. Merhaba tıklatın **HTTP** sekmesi.
3. **Ekle**'ye tıklayın.
4. Merhaba taban URL'si Ekle iletişim kutusu, hello Web sitesi HTTP kimlik doğrulaması (http://localhost/owa gibi) gerçekleştirildiği için hello URL'sini girin ve bir uygulama adı (isteğe bağlı) sağlayın. Merhaba uygulama adı Azure multi-Factor Authentication raporlarında görünür ve SMS veya mobil uygulama kimlik doğrulama iletilerinde görüntülenebilir.
5. Merhaba varsayılan yeterli değilse hello boşta kalma zaman aşımı ve maksimum oturum sürelerini ayarlayın.
6. Merhaba denetleyin **multi-Factor Authentication iste kullanıcı eşleşme** tüm kullanıcılar Sunucu'ya aktarılmışsa ya da hello sunucu ve konu toomulti faktörlü kimlik doğrulaması olarak içeri aktarılacak varsa kutusu. Çok sayıda kullanıcı sunucu hello henüz içeri aktarılmadı ve/veya multi-Factor authentication'da muaf tutulacaksa hello kutunun işaretini kaldırın.
7. Merhaba denetleyin **tanımlama bilgisi önbellek** isterseniz kutusu.
8. **Tamam** düğmesine tıklayın.

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication Sunucusu için IIS Eklentilerini Etkinleştirme
Yapılandırdıktan sonra hello Form tabanlı veya HTTP kimlik doğrulaması URL'lerini ve ayarlarını, select hello burada hello Azure çok faktörlü kimlik doğrulaması IIS eklentilerini yüklenmesi ve IIS'de etkinleştirilmesi konumları. Merhaba aşağıdaki yordamı kullanın:

1. IIS 6'da çalıştırılıyorsa hello tıklatın **ISAPI** sekmesi. Web uygulaması hello select hello Web sitesi (örneğin varsayılan Web sitesi altında) çalıştıran tooenable hello Azure multi-Factor Authentication ISAPI filtresi eklentisini bu site için.
2. IIS 7 veya üzeri çalıştıran hello tıklatın **yerel modül** sekmesi. Merhaba sunucusu, Web siteleri veya uygulamaları tooenable hello hello istenen düzeylerde IIS eklentisini seçin.
3. Merhaba tıklatın **etkinleştirmek IIS kimlik doğrulaması** Merhaba ekranında hello üstündeki kutusu. Azure çok faktörlü kimlik doğrulaması artık hello seçilen IIS uygulamasını güvenli hale getirir. Kullanıcıların sunucu hello aktarıldığından emin olun.

## <a name="trusted-ips"></a>Güvenilen IP'ler
Merhaba güvenilen IP'leri belirli IP adresleri veya alt ağlardan kaynaklanan Web sitesi istekleri için kullanıcıların toobypass Azure çok faktörlü kimlik doğrulaması sağlar. Örneğin, Azure multi-Factor Authentication tooexempt kullanıcılardan hello ofisten oturum açarken sırasında isteyebilirsiniz. Bunun için güvenilen IP'ler girişi olarak hello ofis alt belirtirsiniz. tooconfigure güvenilen IP'leri hello aşağıdaki yordamı kullanın:

1. Hello IIS kimlik doğrulaması bölümü, hello tıklatın **güvenilen IP'leri** sekmesi.
2. **Ekle**'ye tıklayın.
3. Merhaba güvenilen IP'leri Ekle iletişim kutusu göründüğünde, hello seçin **tek bir IP**, **IP aralığı**, veya **alt** radyo düğmesi.
4. Başlangıç IP adresi, IP adresi aralığı veya güvenilir listesinde olması gereken alt ağ girin. Bir alt ağ, select hello girme ve uygun ağ maskesini tıklatırsanız **Tamam**. Merhaba beyaz listesi şimdi eklendi.
