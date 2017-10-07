---
title: AD FS 2.0 ile Azure MFA sunucusu aaaUse | Microsoft Docs
description: "Bu tooget Azure MFA ve AD FS 2.0 ile çalışmaya nasıl açıklayan hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>AD FS 2.0 ile Azure multi-Factor Authentication sunucusu toowork yapılandırın
Bu makalede, Azure Active Directory ile Federasyon ve şirket içi toosecure kaynakları istediğiniz kuruluşlarda veya hello bulut bulunur. Hello Azure multi-Factor Authentication sunucusu kullanarak ve böylece yüksek değerli uç noktalar için iki aşamalı doğrulamayı tetiklenir AD FS ile toowork yapılandırma kaynaklarınızı koruyun.

Bu belge, AD FS 2.0 ile hello Azure multi-Factor Authentication sunucusu kullanmayı ele alır. AD FS hakkında bilgi için bkz. [Windows Server 2012 R2 AD FS ile Azure Multi-Factor Authentication Sunucusu kullanarak bulut ve şirket içi kaynakları güvenli hale getirme](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>AD FS 2.0’ı bir ara sunucu ile güvenli hale getirme
AD FS 2.0 proxy ile toosecure hello AD FS proxy sunucusuna hello Azure multi-Factor Authentication sunucusu yükleyin.

### <a name="configure-iis-authentication"></a>IIS kimlik doğrulamasını yapılandırma
1. Hello Azure multi-Factor Authentication sunucusu, hello tıklatın **IIS kimlik doğrulaması** hello soldaki menüde simgesi.
2. Merhaba tıklatın **Form tabanlı** sekmesi.
3. **Ekle**'ye tıklayın.

   <center>![Kurulum](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. toodetect kullanıcı adı, parola ve etki alanı değişkenlerini otomatik olarak hello form tabanlı Web sitesi iletişim kutusu içinde (örneğin, https://sso.contoso.com/adfs/ls) hello oturum açma URL'sini girin ve tıklayın **Tamam**.
5. Merhaba denetleyin **Azure multi-Factor Authentication iste kullanıcı eşleşme** tüm kullanıcılar Sunucu'ya aktarılmışsa ya da hello sunucu ve konu tootwo adım doğrulama aktarılır, kutu. Kullanıcıların önemli sayıda sunucu hello henüz içeri aktarılmadı ve/veya iki aşamalı doğrulamayı muaf tutulacaksa hello kutunun işaretini kaldırın.
6. Merhaba sayfa değişkenleri otomatik olarak algılanamaz ise hello tıklatın **el ile belirt...** Merhaba form tabanlı Web sitesi iletişim kutusunda düğme.
7. Merhaba form tabanlı Web sitesi iletişim kutusunda hello URL toohello AD FS oturum açma sayfasına hello gönderme URL'si alanına (örneğin, https://sso.contoso.com/adfs/ls) girin ve (isteğe bağlı) bir uygulama adı girin. Merhaba uygulama adı Azure multi-Factor Authentication raporlarında görünür ve SMS veya mobil uygulama kimlik doğrulama iletilerinde görüntülenebilir.
8. Merhaba istek biçimi çok ayarlamak**POST veya GET**.
9. Merhaba kullanıcı adı değişkeni (ctl00$ ContentPlaceHolder1$ UsernameTextBox) ve parola değişkenini (ctl00$ ContentPlaceHolder1$ PasswordTextBox) girin. Form tabanlı oturum açma sayfanız bir etki alanı metin kutusu görüntülerse, hello etki alanı değişkenini de girin. hello giriş kutularının hello oturum açma sayfasında, bir web tarayıcısında oturum açma sayfasına gidin toohello toofind hello adlarını sağ hello sayfası ve seçin **kaynağı görüntüle**.
10. Merhaba denetleyin **Azure multi-Factor Authentication iste kullanıcı eşleşme** tüm kullanıcılar Sunucu'ya aktarılmışsa ya da hello sunucu ve konu tootwo adım doğrulama aktarılır, kutu. Kullanıcıların önemli sayıda sunucu hello henüz içeri aktarılmadı ve/veya iki aşamalı doğrulamayı muaf tutulacaksa hello kutunun işaretini kaldırın.
    <center>![Kurulum](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. **Gelişmiş...** öğesine tıklayarak Gelişmiş ayarlar tooreview. Yapılandırabileceğiniz ayarlar şunlardır:

    - Özel bir reddetme sayfa dosyası seçme
    - Önbellek başarılı kimlik doğrulamalarını toohello tanımlama bilgilerini kullanarak Web sitesi
    - Nasıl tooauthenticate hello birincil kimlik bilgilerini seçin

12. Merhaba AD FS proxy sunucusu olası olmadığından toobe toohello etki alanına katılmış, kullanıcı içeri aktarma ve ön kimlik doğrulaması için LDAP tooconnect tooyour etki alanı denetleyicisini kullanabilirsiniz. Merhaba Hello Gelişmiş form tabanlı Web sitesi iletişim kutusunda tıklatın **birincil kimlik doğrulaması** sekmesinde ve seçin **LDAP bağı** hello ön kimlik doğrulama türü için.
13. Tamamlandığında, tıklayın **Tamam** tooreturn toohello form tabanlı Web sitesi iletişim kutusu.
14. Tıklatın **Tamam** tooclose hello iletişim kutusu.
15. Bir kez URL Merhaba ve sayfa değişkenleri algılandığında veya girildiğinde, hello Web sitesi verileri Form tabanlı panel hello görüntüler.
16. Merhaba tıklatın **yerel modül** sekmesinde ve hello sunucusunu, başlangıç AD FS proxy (gibi "Default Web Site altında"), çalışan hello Web sitesi seçin veya AD FS proxy (örneğin, "ls" altında "adfs") uygulama tooenable hello IIS hello eklenti hello İstenen düzeyi.
17. Merhaba tıklatın **etkinleştirmek IIS kimlik doğrulaması** Merhaba ekranında hello üstündeki kutusu.

Merhaba IIS kimlik doğrulaması şimdi etkinleştirildi.

### <a name="configure-directory-integration"></a>Dizin tümleştirmesini yapılandırma
IIS kimlik doğrulaması etkin, ancak tooperform hello ön kimlik doğrulama tooyour Active Directory (AD) yapılandırmanız gerekir LDAP aracılığıyla hello LDAP bağlantısı toohello etki alanı denetleyicisi.

1. Merhaba tıklatın **dizin tümleştirme** simgesi.
2. Merhaba Ayarlar sekmesinde hello seçin **belirli LDAP yapılandırması kullan** radyo düğmesi.

   <center>![Kurulum](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. **Düzenle**’ye tıklayın.
4. Merhaba LDAP yapılandırmasını Düzenle iletişim kutusunda hello bilgi gerekli tooconnect toohello AD etki alanı denetleyicisiyle hello alanları doldurun. Merhaba alanların açıklamaları hello Azure multi-Factor Authentication sunucusu Yardım dosyasına dahil edilir.
5. Merhaba tıklayarak hello LDAP bağlantısı testi **Test** düğmesi.

   <center>![Kurulum](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Merhaba LDAP bağlantısı testi başarılı olursa tıklatın **Tamam**.

### <a name="configure-company-settings"></a>Şirket ayarlarını yapılandırma
1. Bundan sonra hello öğesini **şirket ayarları** simgesi ve select hello **kullanıcı adı çözümlemesi** sekmesi.
2. Select hello **kullanıcı adlarını eşleştirmek için LDAP benzersiz tanımlayıcı özniteliği kullanın** radyo düğmesi.
3. Kullanıcılar kullanıcı adlarını "etki alanı\kullanıcı adı" biçiminde girin, hello LDAP sorgusu oluşturduğunda hello sunucu hello kullanıcıadı Kapat toobe mümkün toostrip hello etki alanı gerekir. Bu, bir kayıt defteri ayarı aracılığıyla yapılabilir.
4. Hello Kayıt Defteri Düzenleyicisi'ni açın ve tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive gidin ağları/PhoneFactor bir 64-bit sunucuda. 32 bit ise, sunucusunda hello "Wow6432Node" Merhaba yolu dışında alın. Oluşturma bir DWORD kayıt defteri anahtarı "UsernameCxz_stripPrefixDomain" adlı ve hello değeri too1 ayarlayın. Azure multi-Factor Authentication artık hello AD FS proxy güvenli hale getirir.

Kullanıcıları Active Directory'den sunucu hello aktarıldığından emin olun. Merhaba bkz [güvenilen IP'ler bölümüne](#trusted-ips) toowhitelist iç IP adreslerini iki aşamalı doğrulama bu konumlardan toohello Web sitesinde oturum açarken gerekli olmasını isteyip istemediğinizi.

<center>![Kurulum](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>Ara sunucu olmadan AD FS 2.0 Direct
Merhaba AD FS Ara sunucusu kullanılmadığında AD FS güvenliğini sağlayabilirsiniz. Merhaba AD FS sunucusuna Hello Azure multi-Factor Authentication sunucusu yükleyin ve aşağıdaki hello Sunucu'yu adımları hello yapılandırın:

1. Hello Hello Azure çok faktörlü kimlik doğrulama sunucusu içinde tıklatın **IIS kimlik doğrulaması** hello soldaki menüde simgesi.
2. Merhaba tıklatın **HTTP** sekmesi.
3. **Ekle**'ye tıklayın.
4. Merhaba taban URL'si Ekle iletişim kutusunda hello hello taban URL'si alanına HTTP kimlik doğrulaması (https://sso.domain.com/adfs/ls/auth/integrated gibi) gerçekleştirildiği AD FS Web sitesi hello URL'sini girin. Ardından bir uygulama adı (isteğe bağlı) girin. Merhaba uygulama adı Azure multi-Factor Authentication raporlarında görünür ve SMS veya mobil uygulama kimlik doğrulama iletilerinde görüntülenebilir.
5. İsterseniz, ayarlama hello boşta kalma zaman aşımı ve maksimum oturum sürelerini.
6. Merhaba denetleyin **Azure multi-Factor Authentication iste kullanıcı eşleşme** tüm kullanıcılar Sunucu'ya aktarılmışsa ya da hello sunucu ve konu tootwo adım doğrulama aktarılır, kutu. Kullanıcıların önemli sayıda sunucu hello henüz içeri aktarılmadı ve/veya iki aşamalı doğrulamayı muaf tutulacaksa hello kutunun işaretini kaldırın.
7. İsterseniz Hello tanımlama bilgisi önbellek kutusunu işaretleyin.

   <center>![Kurulum](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. **Tamam** düğmesine tıklayın.
9. Merhaba tıklatın **yerel modül** sekmesi ve select hello sunucu, hello Web sitesi (gibi "Default Web Site") veya hello AD FS uygulama (örneğin, "ls" altında "adfs") tooenable hello IIS hello eklenti istenen düzeyi.
10. Merhaba tıklatın **etkinleştirmek IIS kimlik doğrulaması** Merhaba ekranında hello üstündeki kutusu.

Azure Multi-Factor Authentication artık AD FS’yi güvenli hale getirir.

Kullanıcıları Active Directory'den sunucu hello aktarıldığından emin olun. Bkz: Merhaba toowhitelist iç IP isterseniz güvenilen IP'ler bölümüne adresleri iki aşamalı doğrulama bu konumlardan toohello Web sitesinde oturum açarken gerekli değildir.

## <a name="trusted-ips"></a>Güvenilen IP'ler
Güvenilen IP'leri belirli IP adresleri veya alt ağlardan kaynaklanan Web sitesi istekleri için kullanıcıların toobypass Azure çok faktörlü kimlik doğrulaması sağlar. Örneğin, bunlar hello ofisten oturum açtığında, iki aşamalı doğrulamayı tooexempt kullanıcılardan isteyebilirsiniz. Bunun için güvenilen IP'ler girişi olarak hello ofis alt belirtirsiniz.

### <a name="tooconfigure-trusted-ips"></a>tooconfigure güvenilen IP'leri
1. Hello IIS kimlik doğrulaması bölümü, hello tıklatın **güvenilen IP'leri** sekmesi.
2. Merhaba tıklatın **Ekle...** tıklayın.
3. Merhaba güvenilen IP'leri Ekle iletişim kutusu göründüğünde, hello birini seçin **tek bir IP**, **IP aralığı**, veya **alt** radyo düğmeleri.
4. Başlangıç IP adresi, IP adresleri aralığını ya da güvenilir listesinde olması gereken alt ağ girin. Bir alt ağ giriyorsanız, uygun ağ maskesi ve tıklatın hello seçin hello **Tamam** düğmesi. Merhaba, IP şimdi eklendi güvenilir.

<center>![Kurulum](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
