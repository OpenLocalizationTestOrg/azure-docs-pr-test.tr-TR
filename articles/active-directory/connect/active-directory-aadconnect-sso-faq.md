---
title: "Azure AD Connect: Sorunsuz çoklu oturum açma sık sorulan sorular özelliğini - | Microsoft Docs"
description: "Azure Active Directory sorunsuz çoklu oturum açma hakkında sorular yanıtlar toofrequently."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Azure Active Directory sorunsuz çoklu oturum açma: sık sorulan sorular

Bu makalede, ilgili Azure Active Directory sorunsuz çoklu oturum açma (sorunsuz SSO) sık sorulan sorular adres. Yeni içerik için geri denetleniyor tutun.

>[!IMPORTANT]
>Merhaba sorunsuz SSO özelliği şu anda önizlemede değil.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Oturum açma yöntemleri ile sorunsuz SSO çalışıyor mu?

Sorunsuz SSO ya da hello ile birleştirilebilir [parola karması eşitlemesi](active-directory-aadconnectsync-implement-password-synchronization.md) veya [doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md) oturum açma yöntemleri. Ancak bu özellik Active Directory Federasyon Hizmetleri (ADFS) ile kullanılamaz.

## <a name="is-seamless-sso-a-free-feature"></a>Sorunsuz SSO boş bir özellik mi var?

Sorunsuz SSO boş bir özelliktir ve Azure AD toouse Ücretli tüm sürümleri olması gerekmez. Merhaba özelliği genel kullanılabilirlik ulaştığında boş kalır.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Hangi uygulamaların yararlanmak `domain_hint` veya `login_hint` sorunsuz SSO parametre yeteneğini?

Bu parametreler ve hello içermeyen olanları göndermek uygulamaların listesini hello derleme hello işlemi içinde duyuyoruz. İlginizi çekiyor mu uygulamalarınız varsa, hello Açıklamalar bölümüne bize bildirin.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Sorunsuz SSO desteklemiyor `Alternate ID` yerine kullanıcı adı, hello gibi `userPrincipalName`?

Evet. Sorunsuz SSO destekleyen `Alternate ID` içinde Azure AD Connect gösterildiği gibi yapılandırıldığında kullanıcıadı hello gibi [burada](active-directory-aadconnect-get-started-custom.md). Tüm Office 365 uygulamaları desteklemez `Alternate ID`. Merhaba destek bildirimi toohello belirli uygulamanın belgelerine başvurun.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>AD FS kullanmadan tooregister Windows 10 cihazları Azure AD ile istiyorum. Sorunsuz SSO yerine kullanabilir miyim?

Evet, bu senaryo sürüm 2.1 veya hello sonraki gerek duyduğu [çalışma alanına katılma istemcisi](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Nasıl miyim alma hello Kerberos şifre çözme anahtarı hello `AZUREADSSOACCT` bilgisayar hesabı?

Toofrequently alma hello Kerberos şifre çözme anahtarı hello önemlidir `AZUREADSSOACCT` şirket içinde oluşturulan (Azure AD temsil eder) bilgisayar hesabını AD orman.

>[!IMPORTANT]
>En az 30 günde hello Kerberos şifre çözme anahtarı alma öneririz.

Azure AD Connect çalıştırdığınız hello şirket içi sunucusunda aşağıdaki adımları izleyin:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>1. Adım AD ormanına sorunsuz SSO etkinleştirdiğiniz listesini al

1. İlk olarak, indirme ve yükleme hello [Microsoft Online Services oturum açma Yardımcısı](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Ardından yükleyip hello [64-bit Windows PowerShell için Azure Active Directory Modülü](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Toohello gidin `%programfiles%\Microsoft Azure Active Directory Connect` klasör.
4. Bu komutu kullanarak içeri aktarma hello sorunsuz SSO PowerShell Modülü: `Import-Module .\AzureADSSO.psd1`.
5. PowerShell'i yönetici olarak çalıştırın. PowerShell'de, çağrı `New-AzureADSSOAuthenticationContext`. Bu komut açılan tooenter vermeniz gerekir, kiracının genel yönetici kimlik bilgileri.
6. Çağrı `Get-AzureADSSOStatus`. Bu komut, bu özellik etkinleştirildiği üzerinde AD ormanına (Merhaba "etki alanları" listesi bakın) listesi hello sağlar.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>2. Adım Bunu üzerinde oluşturulduğuna her bir AD ormanda Hello Kerberos şifre çözme anahtarını güncelleştir

1. Çağrı `$creds = Get-Credential`. İstendiğinde, AD ormanındaki Hello hedeflenen hello etki alanı yönetici kimlik bilgilerini girin.
2. Çağrı `Update-AzureADSSOForest -OnPremCredentials $creds`. Güncelleştirmeleri hello Kerberos şifre çözme anahtarı hello için bu komutu `AZUREADSSOACCT` bu belirli AD ormanında bilgisayar hesabını ve Azure AD içinde güncelleştirir.
3. Merhaba özelliği ayarladığınız her bir AD orman için adımları önceki hello yineleyin.

>[!IMPORTANT]
>Sağlamak sizin _yok_ hello çalıştırmak `Update-AzureADSSOForest` birden çok kez komutu. Aksi takdirde hello özelliği, kullanıcılarınızın Kerberos biletleri süresinin dolmasını ve şirket içi Active Directory tarafından yeniden hello zamana kadar çalışmayı durdurur.

## <a name="how-can-i-disable-seamless-sso"></a>Sorunsuz SSO nasıl devre dışı bırakabilirim?

Azure AD Connect'i kullanarak sorunsuz SSO devre dışı bırakılabilir.

Azure AD Connect çalıştırın, "Değiştirme kullanıcı oturum açma sayfası" seçin ve "İleri" yi tıklatın. Ardından hello "Etkinleştirme çoklu oturum açma" seçeneğinin işaretini kaldırın. Merhaba sihirbaza devam edin. Merhaba Sihirbazı tamamlandıktan sonra Kiracı'sorunsuz SSO devre dışı bırakılır.

Ancak, aşağıdaki gibi okur ekranda bir ileti görür:

"Çoklu oturum açma artık devre dışıdır, ancak sıra toocomplete temizleyin ek adımları el ile tooperform vardır. Daha fazla bilgi edinin"

toocomplete Merhaba işlemi, Azure AD Connect çalıştırdığınız hello şirket içi sunucuda el ile şu adımları izleyin:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>1. Adım AD ormanına sorunsuz SSO etkinleştirdiğiniz listesini al

1. İlk olarak, indirme ve yükleme hello [Microsoft Online Services oturum açma Yardımcısı](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Ardından yükleyip hello [64-bit Windows PowerShell için Azure Active Directory Modülü](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Toohello gidin `%programfiles%\Microsoft Azure Active Directory Connect` klasör.
4. Bu komutu kullanarak içeri aktarma hello sorunsuz SSO PowerShell Modülü: `Import-Module .\AzureADSSO.psd1`.
5. PowerShell'i yönetici olarak çalıştırın. PowerShell'de, çağrı `New-AzureADSSOAuthenticationContext`. Bu komut açılan tooenter vermeniz gerekir, kiracının genel yönetici kimlik bilgileri.
6. Çağrı `Get-AzureADSSOStatus`. Bu komut, bu özellik etkinleştirildiği üzerinde AD ormanına (Merhaba "etki alanları" listesi bakın) listesi hello sağlar.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>2. Adım Merhaba el ile silmeniz `AZUREADSSOACCT` listelenen gördüğünüz her AD ormanındaki bilgisayar hesabı.

## <a name="next-steps"></a>Sonraki adımlar

- [**Hızlı Başlangıç** ](active-directory-aadconnect-sso-quick-start.md) - hale getirmek ve Azure AD sorunsuz SSO çalışıyor.
- [**Teknik derinlemesine** ](active-directory-aadconnect-sso-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
