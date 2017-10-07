---
title: "Azure AD Connect: Sorunsuz çoklu oturum açma - hızlı başlangıç | Microsoft Docs"
description: "Bu makalede, Azure Active Directory sorunsuz çoklu oturum açma ile tooget nasıl başlatılacağını açıklar."
services: active-directory
keywords: "Azure AD, SSO, gerekli bileşenleri yükleme Active Directory, Azure AD Connect nedir çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Azure Active Directory sorunsuz çoklu oturum açma: Hızlı Başlangıç

## <a name="how-toodeploy-seamless-sso"></a>Nasıl toodeploy sorunsuz SSO

Azure Active Directory sorunsuz çoklu oturum açma (Azure AD sorunsuz SSO) otomatik olarak imzalar kurumsal masaüstü bağlı tooyour Kurumsal ağlarında olduklarında kullanıcıların. Şirket içinde ek bileşenleri gerek kalmadan tooyour bulut tabanlı uygulamalar, kullanıcıların kolay erişim sağlar.

>[!IMPORTANT]
>Merhaba sorunsuz SSO özelliği şu anda önizlemede değil.

toodeploy sorunsuz SSO, toofollow gereken adımları:

## <a name="step-1-check-prerequisites"></a>1. adım: Önkoşul denetimi

Önkoşullar aşağıdaki o hello yerinde olduğundan emin olun:

1. Azure AD Connect sunucusunu ayarlama: kullanırsanız [doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md) , oturum açma yöntemi başka bir eylem gerekli değildir. Kullanırsanız [parola karması eşitlemesi](active-directory-aadconnectsync-implement-password-synchronization.md) , oturum açma yöntemi olarak ve Azure AD Connect ve Azure AD arasında bir güvenlik duvarı varsa, emin olun:
- Sürümleri 1.1.484.0 kullanıyorsanız veya Azure AD Connect sonraki.
- Azure AD Connect ile iletişim kurabilir `*.msappproxy.net` URL'leri ve üstünde bağlantı noktası 443'tür. Yalnızca asıl kullanıcı oturum açma işlemleri için hello özelliğini etkinleştirdiğinizde bu geçerli bir önkoşuldur.
- Azure AD Connect, doğrudan IP bağlantıları toohello yapabilir [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653). Yeniden yalnızca hello özelliğini etkinleştirdiğinizde bu önkoşulu geçerlidir.
2. TooAzure AD eşitleme her bir AD orman için etki alanı yönetici kimlik bilgilerine ihtiyacınız (Azure AD Connect'i kullanarak) ve olan kullanıcılar için sorunsuz SSO tooenable istiyor.

## <a name="step-2-enable-hello-feature"></a>2. adım: hello özelliğini etkinleştir

Sorunsuz SSO kullanarak etkinleştirilebilir [Azure AD Connect](active-directory-aadconnect.md).

Azure AD Connect yeni yüklemesini yapıyorsanız, hello seçin [özel yükleme yolu](active-directory-aadconnect-get-started-custom.md). Merhaba "Kullanıcı oturum açma" sayfanın hello "Etkinleştirme çoklu oturum açma" seçeneği işaretleyin.

![Azure AD Connect - kullanıcı oturum açma](./media/active-directory-aadconnect-sso/sso8.png)

Azure AD Connect yüklemesi zaten varsa, "Değişiklik kullanıcı oturum açma sayfasında" Azure AD Connect seçin ve "İleri" yi tıklatın. Ardından hello "Etkinleştirme çoklu oturum açma" seçeneği işaretleyin.

![Azure AD Connect - değişiklik kullanıcı oturum açma](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Toohello "Etkinleştirme çoklu oturum açma" sayfasına ulaşana kadar hello sihirbaza devam edin. TooAzure AD eşitlemek için her bir AD orman etki alanı yönetici kimlik bilgilerini girin (Azure AD Connect'i kullanarak) ve olan kullanıcılar için sorunsuz SSO tooenable istiyor. 

Merhaba Sihirbazı tamamlandıktan sonra Kiracı'sorunsuz SSO etkin.

>[!NOTE]
> Merhaba etki alanı yönetici kimlik bilgileri Azure AD Connect veya Azure AD depolanmaz, ancak yalnızca kullanılan tooenable hello özelliğidir.

Bu yönergeler tooverify sorunsuz SSO doğru etkinleştirdiyseniz izleyin:

1. İçinde toohello oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello kiracınız için genel yönetici kimlik bilgileriyle.
2. Seçin **Azure Active Directory** hello sol gezinti çubuğunda.
3. Seçin **Azure AD Connect**.
4. Bu hello doğrulayın **sorunsuz çoklu oturum açma** özelliği gösterildiğinden **etkin**.

![Azure portal - Azure AD Connect dikey penceresi](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>3. adım: hello özelliği alma

tooroll hello özelliği tooyour kullanıcılar çıkışı tooadd iki Azure AD URL'leri (https://autologon.microsoftazuread-sso.com ve https://aadg.windows.net.nsatc.net) toousers'Intranet bölgesi ayarlarını Active Directory'de Grup İlkesi aracılığıyla gerekir.

>[!NOTE]
> (Bu güvenilen site URL'leri kümesini Internet Explorer ile paylaşıyorsa) Windows Internet Explorer ve Google Chrome için yalnızca çalışma yönergeleri aşağıdaki hello. Mozilla Firefox ve Mac üzerinde Google Chrome yönergeleri tooset için sonraki bölüme Hello okuma

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>Neden toomodify kullanıcıların Intranet bölgesi ayarlarını gerekiyor mu?

Varsayılan olarak, hello tarayıcı bir URL'den hello sağ bölgesi (Internet veya Intranet) otomatik olarak hesaplar. Örneğin, (Merhaba URL'si nokta içerdiğinden) http://intranet.contoso.com/ eşlenen toohello Internet bölgesi iken http://contoso/ eşlenen toohello Intranet bölgesi, ' dir. URL'sini açıkça toohello tarayıcısının Intranet eklenmediği sürece tarayıcılar - gibi hello iki Azure AD URL'leri - Kerberos biletleri tooa bulut uç noktası göndermeyin.

### <a name="detailed-steps"></a>Ayrıntılı adımlar

1. Merhaba Grup İlkesi yönetim aracını açın.
2. Merhaba uygulanan toosome ya da tüm kullanıcıları Grup İlkesi düzenleyin. Bu örnekte, kullandığımız hello **varsayılan etki alanı ilkesi**.
3. Çok gidin**Kullanıcı Yapılandırması\Yönetim Şablonları\Windows Bileşenleri\Internet Explorer\Internet Denetim Panel\Security sayfası** seçip **tooZone ataması listesi Site**.
![Çoklu oturum açma](./media/active-directory-aadconnect-sso/sso6.png)  
4. Merhaba ilkesini etkinleştirmek ve değerleri (Azure AD URL'ler Kerberos biletleri yere iletilmez) aşağıdaki hello ve veri girin (*1* Intranet bölgesine gösterir) hello iletişim kutusunda.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Bu kullanıcılar paylaşılan bilgi noktaları üzerinde - imzalama, bazı kullanıcıların sorunsuz SSO - Örneğin, kullanarak toodisallow istiyorsanız değerleri çok önceki hello ayarlayın*4*. Bu eylemin hello Azure AD URL'leri toohello Yasak Bölge ekler ve sorunsuz SSO hello zaman başarısız olur.

5. Tıklatın **Tamam** ve **Tamam** yeniden.

![Çoklu oturum açma](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Tarayıcı konuları

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox otomatik olarak Kerberos kimlik doğrulamasını yapmaz. Her kullanıcının hello aşağıdaki adımları kullanarak hello Azure AD URL'leri tootheir Firefox ayarlarını eklemek toomanually vardır:
1. Firefox çalıştırın ve girin `about:config` hello adres çubuğundaki. Gördüğünüz herhangi bir bildirim yok sayın.
2. Merhaba Ara **network.negotiate auth.trusted URI'ler** tercih. Bu tercih Kerberos kimlik doğrulaması için Firefox'in Güvenilen siteler listelenir.
3. Sağ tıklayın ve "Değiştir"'i seçin.
4. Girin "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" Merhaba alanında.
5. "Tamam" düğmesini tıklatın ve hello tarayıcı yeniden açın.

#### <a name="safari-on-mac-os"></a>Mac OS Safari

Mac OS çalıştıran bu hello makine birleştirilmiş tooAD olduğundan emin olun. Yönergeler Bkz toodo, [burada](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Mac OS Google Chrome

Mac OS ve diğer Windows olmayan platformlarda Google Chrome için çok başvuran[bu makalede](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) nasıl toowhitelist hello tümleşik kimlik doğrulaması için Azure AD URL'ler hakkında bilgi için.

Üçüncü taraf Active Directory Grup İlkesi'ni kullanarak bu makalenin kapsamı dışında Mac Kullanıcıları hello Azure AD URL'leri tooFirefox ve Google Chrome uzantıları tooroll değildir.

#### <a name="known-limitations"></a>Bilinen sınırlamaları

Sorunsuz SSO Firefox ve kenar tarayıcılarda özel gözatma modunda çalışmıyor. Merhaba tarayıcı geliştirilmiş koruma modunda çalışıyorsa, ayrıca Internet Explorer, işe yaramaz.

>[!IMPORTANT]
>Biz son kenar tooinvestigate desteği müşteri bildirilen sorunlar geri.

## <a name="step-4-test-hello-feature"></a>4. adım: Test hello özelliği

tootest hello özellik belirli bir kullanıcı için olmak _tüm_ koşullar aşağıdaki hello olan yerinde:
  - Merhaba kullanıcı kurumsal bir cihazda oturum açma.
  - Merhaba aygıt daha önceden birleştirilmiş tooyour Active Directory (AD) etki alanı olmuştur.
  - Merhaba, doğrudan bağlantı tooyour etki alanı denetleyicisi (DC), hello şirket ağındaki kablolu veya kablosuz veya VPN bağlantısı gibi bir uzaktan erişim bağlantısı aracılığıyla aygıtın.
  - Sahip olduğunuz [hello özelliği alındı](##step-3-roll-out-the-feature) toothis kullanıcı Grup İlkesi kullanarak.

Burada hello kullanıcı adı, ancak değil hello parola hello kullanıcının girdiği tootest hello senaryo:
- Oturum *https://myapps.microsoft.com/* yeni bir özel tarayıcı oturumunda.

tootest hello senaryo hello kullanıcı tooenter hello kullanıcı adı veya hello parola burada sahip değil: 
- Oturum *https://myapps.microsoft.com/contoso.onmicrosoft.com* yeni bir özel tarayıcı oturumunda. Değiştir "*contoso*", kiracının ada sahip.
- Veya oturum *https://myapps.microsoft.com/contoso.com* yeni bir özel tarayıcı oturumunda. Değiştir "*contoso.com*" kiracınızda doğrulanmış bir etki alanıyla (bir Federasyon etki alanı değil).

## <a name="step-5-roll-over-keys"></a>5. adım: anahtarlar üzerinden alma

2. adımda, Azure AD Connect (Azure AD temsil eder) bilgisayar hesapları sorunsuz SSO etkin tüm hello AD ormanlardaki oluşturur. İçinde daha ayrıntılı bilgi [burada](active-directory-aadconnect-sso-how-it-works.md). Gelişmiş güvenlik için bu bilgisayar hesaplarının hello Kerberos şifre çözme anahtarlarını sık alma önerilir.

>[!IMPORTANT]
>Bu adım toodo gerekmeyen _hemen_ hello özelliği etkinleştirdikten sonra. Merhaba Kerberos şifre çözme anahtarları üzerinde en az 30 günde alma.

## <a name="next-steps"></a>Sonraki adımlar

- [**Teknik derinlemesine** ](active-directory-aadconnect-sso-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.
- [**Sık sorulan sorular** ](active-directory-aadconnect-sso-faq.md) -toofrequently sorular yanıtlanmaktadır.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
