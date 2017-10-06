---
title: "Azure AD Connect: bağlantı sorunlarını giderme | Microsoft Docs"
description: "Azure AD Connect ile nasıl tootroubleshoot bağlantı sorunları açıklar."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Azure AD Connect ile ilgili bağlantı sorunlarını giderme
Bu makalede, Azure AD Connect ve Azure AD arasında bağlantı nasıl çalıştığını ve nasıl tootroubleshoot bağlantı sorunları açıklanmaktadır. Bu büyük olasılıkla toobe bir proxy sunucusu olan bir ortamda görülen sorunlardır.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Merhaba Yükleme Sihirbazı'nda bağlantı sorunlarını giderme
Azure AD Connect (Merhaba ADAL kitaplığını kullanarak) Modern kimlik doğrulaması için kimlik doğrulaması kullanıyor. Merhaba Yükleme Sihirbazı'nı ve hello eşitleme altyapısı uygun bu iki .NET uygulamaları olduğundan düzgün yapılandırılmış machine.config toobe gerektirir.

Bu makalede, Fabrikam tooAzure AD kendi proxy üzerinden nasıl bağlanacağını gösterir. Merhaba proxy sunucusu fabrikamproxy adlı ve bağlantı noktası 8080 kullanıyor.

İlk toomake emin ihtiyacımız [ **machine.config** ](active-directory-aadconnect-prerequisites.md#connectivity) doğru yapılandırılmış.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> Değişiklikler toomiiserver.exe.config yerine yapılmalıdır, bazı Microsoft dışı bloglar, belgelenmiştir. Ancak, bu dosyanın ilk yükleme sırasında çalışırsa, hello sistem ilk yükseltme üzerinde çalışmayı durdurur. Bu nedenle bile her yükseltmede üzerine yazılır. Bu nedenle, hello tooupdate machine.config yerine önerilir.
>
>

Merhaba proxy sunucusu de gerekli hello URL'leri açılmış olmalıdır. Merhaba resmi listesi bölümlerinde [Office 365 URL'leri ve IP adresi aralıkları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Bu URL'leri, aşağıdaki tablonun hello hello mutlak tam minimum toobe mümkün tooconnect tooAzure AD değildir. Bu liste, parola geri yazma veya Azure AD Connect Health gibi tüm isteğe bağlı özellikleri içermez. Merhaba ilk yapılandırmasını sorun giderme, belgelenmiş burada toohelp olur.

| URL | Bağlantı noktası | Açıklama |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Kullanılan toodownload CRL listeler. |
| \*. verisign.com |HTTP/80 |Kullanılan toodownload CRL listeler. |
| \*. entrust.com |HTTP/80 |Kullanılan toodownload MFA için CRL listeler. |
| \*.windows.net |HTTPS/443 |Kullanılan toosign tooAzure AD içinde. |
| Secure.aadcdn.microsoftonline p.com |HTTPS/443 |MFA için kullanılır. |
| \*.microsoftonline.com |HTTPS/443 |Azure AD dizini ve içeri/dışarı aktarma veri tooconfigure kullanılır. |

## <a name="errors-in-hello-wizard"></a>Başlangıç Sihirbazı'nda hataları
Merhaba Yükleme Sihirbazı'nı iki farklı güvenlik kapsamları kullanıyor. Merhaba sayfasında **tooAzure AD Connect**, şu anda kullanıcı olarak oturum açmış hello kullanıyor. Merhaba sayfasında **yapılandırma**, toohello değiştirme [hello eşitleme altyapısı için hello hizmetini çalıştıran hesabı](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). Bir sorun varsa, zaten hello olasılıkla göründüğü **tooAzure AD Connect** hello proxy yapılandırması genel olduğundan hello sihirbazındaki sayfası.

Aşağıdaki sorunlar hello hello Yükleme Sihirbazı'nda karşılaştığınız hello en yaygın hatalardır.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>Merhaba Yükleme Sihirbazı'nı doğru şekilde yapılandırılmadı
Merhaba Sihirbazı kendisini hello proxy ulaştığında bu hata görünür.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Bu hatayı görürseniz, hello doğrulayın [machine.config](active-directory-aadconnect-prerequisites.md#connectivity) doğru şekilde yapılandırıldı.
* Doğru görünüyorsa, hello adımları [proxy bağlanabilirliği doğrulamak](#verify-proxy-connectivity) de hello Sihirbazı dışında hello sorun varsa toosee.

### <a name="a-microsoft-account-is-used"></a>Bir Microsoft hesabı kullanılır
Kullanırsanız, bir **Microsoft hesabı** yerine **okul veya kuruluş** hesap, genel bir hata görürsünüz.  
![Bir Microsoft Account kullanılır](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>Merhaba MFA endpoint ulaşılamıyor
Bu hata hello görünür uç nokta **https://secure.aadcdn.microsoftonline-p.com** ulaşılamıyor ve MFA etkinse, genel yönetici sahip.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Bu hatayı görürseniz, bu hello uç doğrulayın **secure.aadcdn.microsoftonline p.com** toohello proxy eklendi.

### <a name="hello-password-cannot-be-verified"></a>Merhaba parola doğrulanamıyor.
Merhaba Yükleme Sihirbazı'nı tooAzure AD ancak hello parola kendisini bağlanırken başarılı olursa, bu hatayı görürsünüz doğrulanamıyor:  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* Geçici bir parola Hello parola korumalıysa ve değiştirilmesi gerekir? Bu gerçekten hello doğru parolayı mi? (Başka bir bilgisayardaki hello Azure AD Connect sunucusu daha) toohttps://login.microsoftonline.com toosign deneyin ve hello hesabı kullanılabilir olduğunu doğrulayın.

### <a name="verify-proxy-connectivity"></a>Proxy bağlanabildiğini doğrulayın
tooverify hello Azure AD Connect sunucusu hello proxy'si ve Internet ile gerçek bağlantı varsa kullanın bazı PowerShell toosee hello proxy web isteklerini veya izin veriyorsa. Bir PowerShell komut isteminde çalıştırmak `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Teknik olarak hello ilk toohttps://login.microsoftonline.com ve bu URI çalışır de, ancak hello diğer daha hızlı toorespond URI'dir çağrıdır.)

PowerShell machine.config toocontact hello proxy'sine hello yapılandırmasını kullanır. winhttp/Netsh Hello ayarları bu cmdlet'leri etkisi değil.

Merhaba proxy doğru şekilde yapılandırıldıysa, başarı durumunu almanız gerekir: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

Alırsanız **oluşturulamıyor tooconnect toohello uzak sunucu**, ardından PowerShell hello proxy kullanmadan toomake doğrudan çağrı çalışıyor veya DNS düzgün yapılandırılmamış. Merhaba emin olun **machine.config** dosyası doğru şekilde yapılandırılmış.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Merhaba proxy doğru yapılandırılmamışsa, bir hata alıyorsunuz: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Hata | Hata metni | Açıklama |
| --- | --- | --- |
| 403 |Yasak |Merhaba istenen URL için hello proxy açılmadı. Merhaba proxy yapılandırmasını tekrar ziyaret edip emin hello olun [URL'leri](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) açılmış. |
| 407 |Proxy kimlik doğrulaması gerekli |bir oturum açma Hello proxy sunucusu gereklidir ve sağlanmadı. Proxy sunucunuz kimlik doğrulaması gerektiriyorsa, bu ayar hello machine.config içinde yapılandırılmış emin toohave olun. Ayrıca hello kullanıcı hello Sihirbazı'nı çalıştıran ve hello hizmet hesabı için etki alanı hesapları kullandığınızdan emin olun. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>Azure AD Connect ve Azure AD arasındaki Hello iletişim düzeni
Bu önceki adımları izlediğinizde ve yine bağlanamıyorsanız, ağ günlüklerine arayan bu noktada başlayabilir. Bu bölümde, normal ve başarılı bağlantısı düzeni belgeleme. Ayrıca hello ağ günlükleri okunurken, göz ardı edilebilir ortak kırmızı herrings listeleme.

* Çağrıları toohttps://dc.services.visualstudio.com vardır. Bu URL hello yükleme toosucceed ve bu çağrıları için hello proxy Aç göz ardı edilebilir gerekli toohave değil.
* Dns çözümlemesi hello gerçek ana toobe hello DNS ad alanı nsatc.net ve diğer ad microsoftonline.com altında değil listeler bakın. Ancak, hello gerçek sunucu adlarına göre tüm web hizmeti isteklerinin değildir ve bu URL'leri toohello proxy tooadd sahip değil.
* Hello uç noktaları adminwebservice ve provisioningapi bulma uç noktaları ve toofind hello gerçek uç noktası toouse kullanılır. Bu uç noktalar bölgenizdeki bağlı olarak farklılık gösterir.

### <a name="reference-proxy-logs"></a>Başvuru proxy günlükleri
Bir döküm İşte bir sayfasından gerçek proxy günlük ve hello Yükleme Sihirbazı'nı nereden bunu (yinelenen girişler toohello aynı uç noktası kaldırılmış) yapılmadı. Bu bölümde, kendi proxy ve ağ günlükleri için bir başvuru olarak kullanılabilir. Merhaba gerçek uç noktaları, ortamınızda farklı olabilir (özellikle bu URL'leri *italik*).

**TooAzure AD connect**

| Zaman | URL |
| --- | --- |
| 1/11/2016 8:31 |Connect://Login.microsoftonline.com:443 |
| 1/11/2016 8:31 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |Bağlan: / /*bba800 bağlantı*. microsoftonline.com:443 |
| 1/11/2016 8:32 |Connect://Login.microsoftonline.com:443 |
| 1/11/2016 8:33 |Connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |Bağlan: / /*bwsc02 geçiş*. microsoftonline.com:443 |

**Yapılandırma**

| Zaman | URL |
| --- | --- |
| 1/11/2016 8:43 |Connect://Login.microsoftonline.com:443 |
| 1/11/2016 8:43 |Bağlan: / /*bba800 bağlantı*. microsoftonline.com:443 |
| 1/11/2016 8:43 |Connect://Login.microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |Bağlan: / /*bba900 bağlantı*. microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://Login.microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |Bağlan: / /*bba800 bağlantı*. microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://Login.microsoftonline.com:443 |
| 1/11/2016 8:46 |Connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |Bağlan: / /*bwsc02 geçiş*. microsoftonline.com:443 |

**İlk eşitleme**

| Zaman | URL |
| --- | --- |
| 1/11/2016 8:48 |Connect://Login.Windows.NET:443 |
| 1/11/2016 8:49 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |Bağlan: / /*bba900 bağlantı*. microsoftonline.com:443 |
| 1/11/2016 8:49 |Bağlan: / /*bba800 bağlantı*. microsoftonline.com:443 |

## <a name="authentication-errors"></a>Kimlik doğrulama hataları
Bu bölüm, ADAL (Azure AD Connect tarafından kullanılan kimlik doğrulama kitaplığı hello) ve PowerShell döndürülen hatalar kapsar. açıklanan hello hata, sonraki adımınız anlamanıza yardımcı olması.

### <a name="invalid-grant"></a>Geçersiz verin
Geçersiz kullanıcı adı veya parola. Daha fazla bilgi için bkz: [hello parola doğrulanamıyor](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Bilinmeyen kullanıcı türü
Azure AD dizininizi bulunamadı veya çözümlendi. Doğrulanmamış bir etki alanında bir kullanıcı adı ile toologin deneyin olabilir?

### <a name="user-realm-discovery-failed"></a>Kullanıcı bölgesi bulma başarısız oldu
Ağ veya proxy yapılandırma sorunları. Merhaba ağ erişilemiyor. Bkz: [hello Yükleme Sihirbazı'nda bağlantı sorunlarını giderme](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>Kullanıcı parolasının süresi
Kimlik bilgilerinizin süresi doldu. Parolanızı değiştirin.

### <a name="authorizationfailure"></a>AuthorizationFailure
Bilinmeyen sorun.

### <a name="authentication-cancelled"></a>Kimlik doğrulama iptal edildi
Merhaba çok faktörlü kimlik doğrulaması (MFA) sınama iptal edildi.

### <a name="connecttomsonline"></a>ConnectToMSOnline
Kimlik doğrulaması başarılı ancak bir kimlik doğrulama sorunu Azure AD PowerShell sahiptir.

### <a name="azurerolemissing"></a>AzureRoleMissing
Kimlik doğrulaması başarılı oldu. Genel yönetici değildir.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
Kimlik doğrulaması başarılı oldu. Privileged Identity management etkinleştirildi ve şu anda bir genel yönetici değildir. Daha fazla bilgi için bkz: [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
Kimlik doğrulaması başarılı oldu. Şirket bilgileri, Azure AD'den alınamadı.

### <a name="retrievedomains"></a>RetrieveDomains
Kimlik doğrulaması başarılı oldu. Azure AD etki alanı bilgileri alınamadı.

### <a name="unexpected-exception"></a>Beklenmeyen bir özel durum
Merhaba Yükleme Sihirbazı'nın beklenmeyen bir hata olarak gösterilir. Toouse çalışırsanız oluşabilir bir **Microsoft Account** yerine **okul veya kuruluş hesabı**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Önceki sürümler için sorun giderme adımları.
Yapı numarası 1.1.105.0 (Şubat 2016 yayımlandı) ile başlayan sürümleriyle hello oturum açma Yardımcısı devre dışı bırakılan. Bu bölümde ve hello yapılandırma artık gerekli olması gerekir, ancak başvuru olarak tutulur.

Merhaba çoklu oturum için Yardımcısı toowork içinde winhttp yapılandırılması gerekir. Bu yapılandırma ile yapılabilir [ **netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![Netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>Merhaba oturum açma Yardımcısı düzgün yapılandırılmamış
Merhaba oturum açma Yardımcısı hello proxy ulaşamıyor veya hello proxy hello isteği izin vermiyor bu hata görünür.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Bu hatayı görürseniz, hello proxy yapılandırmasında bakmak [netsh](active-directory-aadconnect-prerequisites.md#connectivity) ve doğru doğrulayın.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Doğru görünüyorsa, hello adımları [proxy bağlanabilirliği doğrulamak](#verify-proxy-connectivity) de hello Sihirbazı dışında hello sorun varsa toosee.

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
