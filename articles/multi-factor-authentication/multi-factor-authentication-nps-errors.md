---
title: "hello Azure MFA NPS uzantısı için aaaTroubleshoot hata kodları | Microsoft Docs"
description: "Genel hata iletileri için özel çözümler ile Azure çok faktörlü kimlik doğrulamasını hello NPS uzantısı ile sorunlarını çözme hakkında yardım alın"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Azure çok faktörlü kimlik doğrulamasını hello NPS uzantısı hata iletilerini çözümleyin

Azure çok faktörlü kimlik doğrulamasını hello NPS uzantısı hatalarla karşılaşırsanız, bu makale tooreach bir çözüm daha hızlı kullanın. 

## <a name="troubleshooting-steps-for-common-errors"></a>Sık karşılaşılan hataları için sorun giderme adımları

| Hata kodu | Sorun giderme adımları |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [Desteğe başvurun](#contact-microsoft-support)ve hello günlüklerinin toplanması için adımlar listesi Bahsediyor. Kiracı kimliği ve kullanıcı asıl adı (UPN) dahil olmak üzere hello hata önce ne hakkında mümkün olduğu kadar bilgi sağlayın. |
| **CLIENT_CERT_INSTALL_ERROR** | Merhaba istemci sertifikası yüklü veya Kiracı ile ilişkilendirilen nasıl bir sorun olabilir. Merhaba yönergeleri izleyin [sorun giderme hello MFA NPS uzantısı](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate istemci sertifika sorunları. |
| **ESTS_TOKEN_ERROR** | Merhaba yönergeleri izleyin [sorun giderme hello MFA NPS uzantısı](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate istemci sertifikası ve ADAL belirteci sorunları. |
| **HTTPS_COMMUNICATION_ERROR** | Azure MFA oluşturulamıyor tooreceive yanıtlarının Hello NPS sunucusudur. Güvenlik duvarlarında https://adnotifications.windowsazure.com gelen trafiği tooand için açık çift yönlü olduğunu doğrulayın |
| **HTTP_CONNECT_ERROR** | Merhaba NPS uzantısı çalışır hello sunucusunda https://adnotifications.windowsazure.com ve https://login.microsoftonline.com/ ulaşabilir doğrulayın. Bu siteleri yükleme, bu sunucu üzerinde bağlantı sorunlarını giderme. |
| **REGISTRY_CONFIG_ERROR** | Merhaba kayıt defteri olabilir Merhaba uygulaması için bir anahtarı eksik hello [PowerShell Betiği](multi-factor-authentication-nps-extension.md#install-the-nps-extension) yüklendikten sonra Çalıştır değildi. Merhaba hata iletisi hello eksik anahtar içermelidir. Başlangıç anahtarı HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa altında olduğundan emin olun. |
| **REQUEST_FORMAT_ERROR** <br> RADIUS isteği zorunlu RADIUS userName\Identifier özniteliği eksik. NPS RADIUS isteklerini aldığını doğrulayın | Bu hata genellikle bir yükleme sorunu yansıtır. RADIUS istekleri alabilen NPS sunucuları Hello NPS uzantısı'nın yüklü olması gerekir. RDG ve RRAS gibi hizmetler için bağımlılık yüklü NPS sunucularını RADIUS isteklerini alacak yok. NPS uzantısı hello kimlik doğrulama isteğini hello ayrıntıları okuyamıyor beri böyle yüklemeleri ve hataları üzerinden yüklendiğinde çalışmaz. |
| **REQUEST_MISSING_CODE** | Merhaba parola şifreleme protokolünü hello NPS ve NAS sunucular arasında kullanmakta olduğunuz hello ikincil kimlik doğrulama yöntemini desteklediğinden emin olun. **PAP** hello bulutta Azure mfa tüm hello kimlik doğrulama yöntemlerini destekler: telefon araması, tek yönlü SMS mesajı, mobil uygulama bildirimi ve mobil uygulama doğrulama kodu. **CHAPV2** ve **EAP** telefon araması ve mobil uygulama bildirimi destekler. |
| **USERNAME_CANONICALIZATION_ERROR** | Merhaba, şirket içi Active Directory örneğinde mevcut kullanıcıdır ve o hello NPS hizmetinin izinleri tooaccess hello dizin sahip olduğunu doğrulayın. Ormanlar arası güven kullanıyorsanız [desteğine başvurun](#contact-microsoft-support) daha fazla yardım için. |


   

### <a name="alternate-login-id-errors"></a>Alternatif oturum açma kimliği hataları

| Hata kodu | Hata iletisi | Sorun giderme adımları |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | Hata: userObjectSid arama başarısız oldu | Şirket içi Active Directory örneğinizi hello kullanıcı var olduğunu doğrulayın. Ormanlar arası güven kullanıyorsanız [desteğine başvurun](#contact-microsoft-support) daha fazla yardım için. |
| **ALTERNATE_LOGIN_ID_ERROR** | Hata: Alternatif LoginId arama başarısız oldu | LDAP_ALTERNATE_LOGINID_ATTRIBUTE tooa ayarlandığını doğrulayıp [geçerli bir active directory öznitelik](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx). <br><br> LDAP_FORCE_GLOBAL_CATALOG tooTrue ayarlanır veya LDAP_LOOKUP_FORESTS bir boş değer ile yapılandırılmışsa, bir genel katalog yapılandırdıysanız ve bu hello AlternateLoginId öznitelik tooit eklenir doğrulayın. <br><br> LDAP_LOOKUP_FORESTS bir boş değer ile yapılandırılmışsa, hello değerinin doğru olduğunu doğrulayın. Birden çok orman adı varsa, hello adları noktalı virgülle, boşluk ile ayrılmış olması gerekir. <br><br> Bu adımları hello sorun gidermeyi yok ediyorsanız [desteğine başvurun](#contact-microsoft-support) daha fazla yardım için. |
| **ALTERNATE_LOGIN_ID_ERROR** | Hata: Alternatif LoginId değeri boş. | Bu hello AlternateLoginId öznitelik hello kullanıcı için yapılandırıldığını doğrulayın. |


## <a name="errors-your-users-may-encounter"></a>Kullanıcılarınızın hatalarla karşılaşabilirsiniz

| Hata kodu | Hata iletisi | Sorun giderme adımları |
| ---------- | ------------- | --------------------- |
| **Erişim engellendi** | Arayan Kiracı hello kullanıcı için erişim izinleri toodo kimlik doğrulaması yok | Merhaba Kiracı etki alanı ve hello etki alanını hello kullanıcı asıl adı (UPN) olan hello olup olmadığını aynı denetleyin. Örneğin, olduğundan emin olun user@contoso.com tooauthenticate toohello Contoso Kiracı çalışıyor. Merhaba UPN azure'da hello Kiracı için geçerli bir kullanıcı temsil eder. |
| **AuthenticationMethodNotConfigured** | kimlik doğrulama yöntemini hello kullanıcı için yapılandırılmadığı Hello belirtilen | Ekleme veya toohello yönergelerinde göre kendi doğrulama yöntemlerini doğrulama hello kullanıcı sahip [iki aşamalı doğrulama için ayarlarınızı yönetme](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **AuthenticationMethodNotSupported** | Belirtilen kimlik doğrulama yöntemi desteklenmiyor. | Bu hataya dahil etmek, günlükleri toplamak ve [desteğine başvurun](#contact-microsoft-support). Desteğe başvurduğunuzda hello kullanıcı adını ve hello hata tetiklenen hello ikincil doğrulama yöntemi sağlar. |
| **BecAccessDenied** | MSODS Bec çağrısı erişim reddedildi döndürdü, büyük olasılıkla hello kullanıcıadı hello Kiracı içinde tanımlı değil | Merhaba kullanıcı Active Directory şirket içi var, ancak Azure AD tarafından AD Connect eşitlenmedi. Veya hello kullanıcı hello Kiracı için eksik. Merhaba kullanıcı tooAzure AD ekleyin ve bunları toohello yönergelerinde göre kendi doğrulama yöntemlerini ekleyin [iki aşamalı doğrulama için ayarlarınızı yönetme](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **InvalidFormat** veya **StrongAuthenticationServiceInvalidParameter** | Merhaba telefon numarasıdır tanınmayan bir biçimde | Doğrulama telefon numaralarına düzeltmek hello kullanıcı sahip. |
| **InvalidSession** | Hello belirtilen oturum geçersiz veya süresi sona ermiş olabilir | Merhaba oturum birden çok üç dakika toocomplete duruma getirdi. Merhaba kullanıcı hello doğrulama kodunu girerek veya üç hello kimlik doğrulama isteğini başlatarak dakika içinde toohello uygulama bildirimine yanıt doğrulayın. Merhaba sorunu gidermezse, istemci, NAS sunucusu, NPS sunucusu ve hello Azure MFA uç arasında hiçbir ağ gecikmeleri olup olmadığını denetleyin.  |
| **NoDefaultAuthenticationMethodIsConfigured** | Varsayılan kimlik doğrulama yöntemi hello kullanıcı için yapılandırılmış | Ekleme veya toohello yönergelerinde göre kendi doğrulama yöntemlerini doğrulama hello kullanıcı sahip [iki aşamalı doğrulama için ayarlarınızı yönetme](./end-user/multi-factor-authentication-end-user-manage-settings.md). Merhaba kullanıcının bir varsayılan kimlik doğrulama yöntemini seçmiş ve bu yöntem, hesap için yapılandırılan doğrulayın. |
| **OathCodePinIncorrect** | Yanlış kod ve PIN girildi. | Bu hata hello NPS uzantısı beklenmiyor. Bu, kullanıcı karşılaşırsa [desteğine başvurun](#contact-microsoft-support) sorun giderme Yardımı. |
| **ProofDataNotFound** | Sağlama verileri belirtilen hello için yapılandırılmamış kimlik doğrulama yöntemi. | Farklı bir doğrulama yöntemi deneyin veya toohello yönergelerinde göre yeni bir doğrulama yöntemlerini ekleyin hello kullanıcı sahip [iki aşamalı doğrulama için ayarlarınızı yönetme](./end-user/multi-factor-authentication-end-user-manage-settings.md). Merhaba kullanıcı toosee çalıştırdıktan sonra bu hatayı teyit kendi doğrulama yöntemini doğru şekilde kurulduğundan emin olmaya devam ederse [desteğine başvurun](#contact-microsoft-support). |
| **SMSAuthFailedWrongCodePinEntered** | Yanlış kod ve PIN girildi. (OneWaySMS) | Bu hata hello NPS uzantısı beklenmiyor. Bu, kullanıcı karşılaşırsa [desteğine başvurun](#contact-microsoft-support) sorun giderme Yardımı. |
| **TenantIsBlocked** | Kiracı engellendi | [Desteğe başvurun](#contact-microsoft-support) hello Azure Portalı'nda hello Azure AD özellikler sayfasından dizin kimliği. |
| **UserNotFound** | Merhaba belirtilen kullanıcı bulunamadı. | Merhaba Kiracı artık Azure AD'de etkin olarak görünür olur. Birinci taraf uygulamalar, aboneliğinizin etkin olduğunu ve hello sahip denetimi gereklidir. Ayrıca hello sertifika konusu hello Kiracı beklendiği gibi değil ve hello sertifika hala geçerli ve başlangıç hizmet sorumlusu altında kayıtlı olduğundan emin olun. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>Hata iletileri, kullanıcılarınızın, karşılaşabileceğiniz değil

Bazı durumlarda, kendi kimlik doğrulama isteği başarısız olduğundan, kullanıcılarınızın çok faktörlü kimlik doğrulamasını iletileri alabilirsiniz. Bunlar yapılandırmasının hello üründe hatalar değil, ancak neden bir kimlik doğrulama isteği reddedildi kasıtlı uyarıları açıklayan.

| Hata kodu | Hata iletisi | Önerilen adımlar | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | Yanlış kod entered\OATH kodu yanlış | Bir hata kullanıcı yanlış kod girmiştir. | Merhaba kullanıcı hello yanlış kod girildi. Yeni bir kod isteme veya tekrar oturum açmayı tekrar denemelerini sağlayın. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | İzin verilen en fazla kod yeniden deneme üst sınırına | Merhaba kullanıcısı, birden çok kez hello doğrulama sınaması başarısız oldu. Ayarlarınıza bağlı olarak, bunlar bir yönetici tarafından şimdi engellemesini toobe gerekebilir.  |
| **SMSAuthFailedWrongCodeEntered** | Yanlış kod girildi/metin iletisi OTP yanlış | Merhaba kullanıcı hello yanlış kod girildi. Yeni bir kod isteme veya tekrar oturum açmayı tekrar denemelerini sağlayın. |

## <a name="errors-that-require-support"></a>Desteği gerektiren hataları

Bu hatalardan biri karşılaşırsanız öneririz, [desteğine başvurun](#contact-microsoft-support) tanılama Yardım. Bu hataları gidermek adımları standard ayarlanmış yok. Desteğe başvurduğunuzda mümkün olduğu kadar bilgi tooan hata neden hello adımlar hakkında ve Kiracı bilgilerinizi olarak emin tooinclude olabilir.

| Hata kodu | Hata iletisi |
| ---------- | ------------- |
| **InvalidParameter** | İstek null olmamalıdır |
| **InvalidParameter** | Null veya boş ReplicationScope için objectID olmamalıdır: {0} |
| **InvalidParameter** | Merhaba ŞirketAdı uzunluğu \{0} \ hello izin verilen maksimum {1} uzun |
| **InvalidParameter** | UserPrincipalName null veya boş olmamalıdır |
| **InvalidParameter** | Tenantıd doğru biçimde değil Hello sağlanan |
| **InvalidParameter** | SessionID null veya boş olmamalıdır |
| **InvalidParameter** | İstek herhangi ProofData veya Msods çözümlenemedi. Merhaba ProofData bilinmiyor |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>Sonraki adımlar

### <a name="troubleshoot-user-accounts"></a>Kullanıcı hesaplarıyla ilgili sorunları giderme

Kullanıcılarınız varsa [iki aşamalı doğrulamayı sorununuz](./end-user/multi-factor-authentication-end-user-troubleshoot.md), bunları otomatik olarak tanılamak sorunları yardımcı olur. 

### <a name="contact-microsoft-support"></a>Microsoft Destek'e başvurun

Ek Yardım gerekirse, aracılığıyla destek uzmanına başvurun [Azure çok faktörlü kimlik doğrulama sunucusu desteği](https://support.microsoft.com/oas/default.aspx?prid=14947). Sorununuzu mümkün olduğunca hakkında kadar bilgi dahil ederseniz bize kurulurken yardımcı olur. Sağladığınız bilgileri nerede hello hata, özel hata kodu, hello belirli bir oturum kimliği, hello hello kullanıcının Kimliğini hello gördüğünüzü hello sayfa hello hata gördünüz ve hata ayıklama günlüklerini içerir.

Destek Tanılama için toocollect hata ayıklama günlüklerini hello aşağıdaki adımları kullanın: 

1. Bir yönetici komut istemi açın ve şu komutları çalıştırın:

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Merhaba sorunu yeniden oluşturun

3. Bu komutlar Hello İzlemeyi Durdur:

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. Merhaba hello C:\NPS klasörünün içeriğini zip ve daraltılmış hello dosya toohello destek talebi ekleyin.


