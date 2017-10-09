---
title: "Azure AD Connect: Sık sorulan sorular doğrudan kimlik doğrulama - | Microsoft Docs"
description: "Azure Active Directory doğrudan kimlik doğrulaması hakkında sorular yanıtlar toofrequently."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama, Active Directory yükleyin gerekli bileşenleri Azure AD, SSO, çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Azure Active Directory doğrudan kimlik doğrulaması: Sık sorulan sorular

Bu makalede, Azure Active Directory (Azure AD) doğrudan kimlik doğrulaması hakkında sık sorulan sorular adres. Yeni içerik için geri denetleniyor tutun.

>[!IMPORTANT]
>Merhaba doğrudan kimlik doğrulama özelliği şu anda önizlemede değil.

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>Hangi yöntemlerin hello Azure AD oturum açma - geçişli kimlik doğrulaması, parola karma eşitlemesi ve Active Directory Federasyon Hizmetleri (AD FS) - seçmeliyim?

Şirket içi ortamınız ve kuruluş gereksinimlerine bağlıdır. Bu makale için gözden bir [karşılaştırması hello çeşitli Azure AD oturum açma yöntemleri](active-directory-aadconnect-user-signin.md).

## <a name="is-pass-through-authentication-a-free-feature"></a>Doğrudan kimlik doğrulama boş bir özellik mi var?

Doğrudan kimlik doğrulama boş bir özelliktir ve Azure AD toouse Ücretli tüm sürümleri olması gerekmez. Merhaba özelliği genel kullanılabilirlik ulaştığında boş kalır.

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>Doğrudan kimlik doğrulama kullanılabilir [Microsoft Cloud Almanya](http://www.microsoft.de/cloud-deutschland) ve [Microsoft Azure kamu bulut](https://azure.microsoft.com/features/gov/)?

Hayır, geçişli kimlik doğrulaması yalnızca Merhaba Dünya çapında örneğini Azure AD içinde kullanılabilir.

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>Mu [koşullu erişim](../active-directory-conditional-access.md) doğrudan kimlik doğrulama ile çalışır?

Evet, Azure multi-Factor Authentication dahil olmak üzere tüm koşullu erişim özelliklerini doğrudan kimlik doğrulaması ile çalışır.

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Doğrudan kimlik doğrulaması "Alternatif kimlik" yerine "userPrincipalName" Merhaba kullanıcı adı olarak destekliyor mu?

Evet. Doğrudan kimlik doğrulamasını destekleyen `Alternate ID` içinde Azure AD Connect gösterildiği gibi yapılandırıldığında kullanıcıadı hello gibi [burada](active-directory-aadconnect-get-started-custom.md). Tüm Office 365 uygulamaları desteklemez `Alternate ID`. Merhaba destek bildirimi toohello belirli uygulamanın belgelerine başvurun.

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>Parola karma eşitlemesi bir geri dönüş tooPass aracılığıyla kimlik doğrulaması olarak hareket mu?

Hayır, parola karması eşitlemesi bir genel geri dönüş tooPass aracılığıyla kimlik doğrulaması değil. Yalnızca bir geri dönüş için görür [doğrudan kimlik doğrulama bugün desteklemiyor senaryoları](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios). tooavoid kullanıcı oturum açma hataları, geçişli kimlik doğrulaması için yapılandırmalısınız [yüksek kullanılabilirlik](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>Yükleyebilmek için bir [Azure AD uygulama proxy'si](../active-directory-application-proxy-get-started.md) hello bağlayıcısında doğrudan kimlik doğrulama aracısı aynı sunucuya?

Evet, bu yapılandırma ile Merhaba doğrudan kimlik doğrulama Aracısı sürümleri rebranded hello desteklenir (sürümleri 1.5.193.0 veya üstü).

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>Azure AD Connect ve doğrudan kimlik doğrulama Aracısı hangi sürümlerine gerekiyor?

Sürüm 1.1.486.0 gerekir ve daha sonra Azure AD Connect ve 1.5.58.0 veya daha sonra bu özellik toowork için doğrudan kimlik doğrulama Aracısı hello için. Tüm yazılım sunucularda Windows Server 2012 R2 veya üstü yüklü olmalıdır.

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>My kullanıcının parolasının süresi dolmuş ne olur ve bunlar doğrudan kimlik doğrulama kullanarak toosign deneyin?

Yapılandırdıysanız [parola geri yazma](../active-directory-passwords-update-your-own-password.md) belirli bir kullanıcı için ve hello kullanıcı geçişli kimlik doğrulaması kullanarak oturum açar, bunlar değiştirme veya parolalarını sıfırlama. beklendiği gibi Hello parolaları tooon içi Active Directory geri yazılır.

Ancak, parola geri yazma belirli bir kullanıcı için yapılandırılmamışsa veya Merhaba, kullanıcının geçerli bir Azure AD yoksa atanan lisans hello kullanıcı parolalarını hello bulutta güncelleştiremiyor. Parolasının süresi olsa bile kullanıcılar parolalarını güncelleştirilemiyor. Merhaba kullanıcı bunun yerine bu iletiyi görür: "kuruluşunuzun tooupdate izin vermeyen parolanızı bu sitede. Lütfen kuruluşunuz tarafından önerilen toohello yöntemi göre güncelleştirebilir veya yardıma gereksiniminiz varsa yöneticinize sorun." Merhaba kullanıcı ya da Merhaba yönetici tooreset şirket içi Active Directory parolalarını içeriyor.

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>Nasıl doğrudan kimlik doğrulama yanılma parola saldırılarına karşı koruma sağlar mı?

Okuma [bu makalede](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) daha fazla bilgi için.

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>Ne doğrudan kimlik doğrulama Aracısı 80 ve 443 numaralı bağlantı noktaları üzerinden iletişim?

- tüm özellik işlemleri için bağlantı noktası 443 üzerinden HTTPS istekleri Hello kimlik doğrulama Aracısı olun.
- Merhaba kimlik doğrulama Aracısı bağlantı noktası 80 toodownload SSL sertifika iptal listeleri üzerinde HTTP isteklerini olun.

     >[!NOTE]
     >En son güncelleştirmeleri hello hello özelliği tarafından gerekli bağlantı noktalarının sayısı azalır. Azure AD Connect veya hello kimlik doğrulama Aracısı eski sürümlerini varsa, bu bağlantı noktaları da açık tutun: 5671, 8080, 9090, 9091, 9350, 9352 ve 10100 10120.

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>Merhaba doğrudan kimlik doğrulama aracıları giden web proxy sunucu iletişim kurabilir?

Evet. Şirket içi ortamınızda WPAD (Web Proxy Otomatik Bulma) etkinleştirilirse, kimlik doğrulama aracıları otomatik olarak toolocate denemek ve hello ağ üzerinde bir web proxy sunucusu kullan.

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>İki yükleyebilir veya aynı sunucu üzerinde daha fazla doğrudan kimlik doğrulama Aracısı hello?

Hayır, bir doğrudan kimlik doğrulama Aracısı yalnızca tek bir sunucuya yükleyebilirsiniz. Yüksek kullanılabilirlik için doğrudan kimlik doğrulama tooconfigure istiyorsanız, bu hello yönergeleri izleyin [makale](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) yerine.

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>I zaten Azure AD oturum açma için Active Directory Federasyon Hizmetleri (AD FS) kullanın. Nasıl onu tooPass aracılığıyla kimlik doğrulaması geçiş yapabilirim?

AD FS hello Azure AD Connect Sihirbazı'nı kullanarak, oturum açma yöntemi yapılandırdıysanız, kullanıcı oturum açma yöntemi hello değiştirmek tooPass aracılığıyla kimlik doğrulaması. Bu değişiklik hello Kiracı'geçişli kimlik doğrulamasını etkinleştirir ve dönüştürür _tüm_ , federe etki alanlarına yönetilen etki alanları. Tüm sonraki oturum açma istekleri kiracınızda doğrudan kimlik doğrulaması tarafından işlenir. Şu anda, AD FS ile doğrudan kimlik doğrulama oluşan bir bileşimdir farklı etki alanlarında Azure AD Connect toouse içinde desteklenen bir yolu yoktur.

AD FS oturum açma hello yöntemi olarak yapılandırılıp yapılandırılmadığını _dışında_ hello Azure AD Connect Sihirbazı'nın hello kullanıcı oturum açma yöntemi Değiştir tooPass aracılığıyla kimlik doğrulaması (seçeneğinden hello "yapılandırmayın"). Bu değişiklik hello Kiracı'geçişli kimlik doğrulaması sağlar. Ancak, tüm federe etki toouse AD FS oturum açma için devam edin. PowerShell toomanually dönüştürme bazılarını veya tümünü bu federe etki alanları tooManaged etki alanları kullanın. Bundan sonra yönetilen etki alanları tüm oturum açma istekleri (_yalnızca_) doğrudan kimlik doğrulaması tarafından işlenir.

>[!IMPORTANT]
>Değil, doğrudan kimlik doğrulamasını işleyecek oturum açma yalnızca bulut Azure AD kullanıcıları.

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>Doğrudan kimlik doğrulaması bir Çoklu orman AD ortamında kullanabilir miyim?

Evet. Birden çok orman ortamlarına AD ormanlar arasında orman güvenleri varsa desteklenir ve ad soneki yönlendirmesi doğru yapılandırılmışsa.

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>Doğrudan kimlik doğrulama Aracısı Yük Dengeleme özelliği sağlıyor mu?

Hayır, birden çok doğrudan kimlik doğrulama aracı yükleme sağlar [yüksek kullanılabilirlik](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability), ancak Yük Dengeleme değil. Bir veya iki hello kimlik doğrulama Aracısı hello oturum açma isteklerinin hello toplu işleme yukarı bitebilir.

Kimlik Doğrulama Aracısı gerek toohandle hello parola doğrulama isteklerini, hafif nesnelerdir. Bu nedenle en yüksek ve ortalama yük çoğu müşteri için kolayca tarafından işlenir toplamda iki veya üç kimlik doğrulama Aracısı.

Oturum açma kimlik doğrulaması aracıları Kapat tooyour etki alanı denetleyicileri tooimprove gecikme yüklemenizi öneririz.

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>Merhaba yükleyebilmek için hello Azure AD Connect çalıştıran biri başka bir sunucuda ilk doğrudan kimlik doğrulama Aracısı?

Hayır, bu senaryo olan _değil_ desteklenir.

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>Kaç tane doğrudan kimlik doğrulama Aracısı yüklediğimde?

Öneririz:

- Toplam iki veya üç kimlik doğrulama aracısını yükleyin. Bu yapılandırma, müşterilerin çoğu için yeterlidir.
- Oturum açma kimlik doğrulaması aracıları, etki alanı denetleyicilerinde (veya mümkün olduğunca yakın toothem) tooimprove gecikme yükleyin.
- (Burada kimlik doğrulama aracısı yüklü) sunucuları toohello aynı AD ormanı parolaları toobe doğrulanması gereken hello kullanıcılar olarak eklendiğinden emin olun.

>[!NOTE]
>Kiracı başına 12 kimlik doğrulaması aracıların sistem sınırı yoktur.

## <a name="how-can-i-disable-pass-through-authentication"></a>Doğrudan kimlik doğrulama nasıl devre dışı bırakabilirim?

Hello Azure AD Connect Sihirbazı yeniden çalıştırın ve doğrudan kimlik doğrulama tooanother yönteminden hello kullanıcı oturum açma yöntemi değiştirebilirsiniz. Bu değişiklik hello Kiracı'geçişli kimlik doğrulaması devre dışı bırakır ve hello kimlik doğrulama Aracısı hello sunucusundan kaldırır. Diğer sunucularından toomanually kaldırma hello kimlik doğrulama Aracısı var.

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>Doğrudan kimlik doğrulama Aracısı kaldırdığınızda ne olur?

Doğrudan kimlik doğrulama Aracısı bir sunucudan kaldırmayı oturum açma istekleri kabul toostop neden olur. Başka bir kimlik doğrulama kullanıcı oturum açma, Kiracı'çiğnemekten tooavoid bu işlemi yapmadan önce çalışan Aracısı olduğundan emin olun.

## <a name="next-steps"></a>Sonraki adımlar
- [**Geçerli sınırlamalar** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -bu özellik şu anda önizlemede değil. Hangi senaryoları desteklenir ve hangilerinin olmayan öğrenin.
- [**Hızlı Başlangıç** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - hale getirmek ve Azure AD doğrudan kimlik doğrulama çalıştıran.
- [**Teknik derinlemesine** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**Azure AD sorunsuz SSO** ](active-directory-aadconnect-sso.md) -tamamlayıcı bu özellik hakkında daha fazla bilgi edinin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
