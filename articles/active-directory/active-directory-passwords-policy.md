---
title: "İlke: Azure AD SSPR'yi | Microsoft Docs"
description: "Azure AD Self Servis parola sıfırlama ilkesi seçenekleri"
services: active-directory
keywords: "Active directory parola yönetimi, Azure AD parola yönetimi self servis parola sıfırlama"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Parola ilkeleri ve Azure Active Directory'de kısıtlamaları

Bu makalede hello parola ilkeleri ve Azure AD kiracınızda depolanan kullanıcı hesaplarıyla ilişkili karmaşıklık gereksinimlerini açıklar.

## <a name="administrator-password-policy-differences"></a>Yöneticinin parola ilkesi farklar

Microsoft, tüm Azure yöneticisi rolleri (Örnek: Genel Yönetici, Yardım Masası Yöneticisi, Parola Yöneticisi, vb.) için varsayılan olarak güçlü bir **iki kapılı** parola sıfırlama ilkesi uygular

Bu, yöneticilerin güvenlik soruları kullanarak devre dışı bırakır ve hello aşağıdaki uygular.

İki ilke, kimlik doğrulama verileri iki parça gerektiren kapı (e-posta adresi **ve** telefon numarası), aşağıdaki durumlarda hello uygular

* Tüm Azure yönetici rolleri
  * Yardım Masası Yöneticisi
  * Hizmet desteği Yöneticisi
  * Faturalama Yöneticisi
  * İş ortağı Tier1 desteği
  * İş ortağı Tier2 desteği
  * Exchange Hizmet Yöneticisi
  * Lync Hizmet Yöneticisi
  * Kullanıcı Hesap Yöneticisi
  * Directory yazıcılarının
  * Genel yönetici/şirket Yöneticisi
  * SharePoint Hizmet Yöneticisi
  * Uyumluluk Yöneticisi
  * Uygulama Yöneticisi
  * Güvenlik Yöneticisi
  * Ayrıcalıklı Rol Yöneticisi
  * Intune Hizmet Yöneticisi
  * Uygulama Proxy Hizmet Yöneticisi
  * CRM Hizmet Yöneticisi
  * Power BI Hizmet Yöneticisi
  
* 30 gün içinde bir deneme geçen **veya**
* Gösterim etki alanında bulunduğundan (contoso.com) **veya**
* Azure AD Connect, şirket içi dizindeki kimlikleri eşitleme

### <a name="exceptions"></a>Özel durumlar
Kimlik doğrulama verileri bir parçasının gerektiren bir ağ geçidi İlkesi (e-posta adresi **veya** telefon numarası), aşağıdaki durumlarda hello uygular

* Bir deneme ilk 30 gün **veya**
* Gösterim etki alanında mevcut değil (*. onmicrosoft.com) **ve** kimlikleri Azure AD Connect eşitleme değil


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>Tooall kullanıcı hesaplarına uygulanan UserPrincipalName ilkeleri

TooAzure AD toosign gerektiren her bir kullanıcı hesabını hesaplarıyla ilişkili benzersiz kullanıcı asıl adı (UPN) öznitelik değeri olması gerekir. tooboth uygulamak hello ilkeleri anahatları Hello tabloda toohello Bulut ve yalnızca toocloud kullanıcı hesaplarını Active Directory kullanıcı hesaplarınızı eşitlenen şirket içi.

| Özellik | UserPrincipalName gereksinimleri |
| --- | --- |
| İzin verilen karakter |<ul> <li>A-Z</li> <li>a - z</li><li>0 – 9</li> <li> . - \_ ! \# ^ \~</li></ul> |
| Karakterlere izin verilmez |<ul> <li>Bir ' @' hello kullanıcı adı hello etki alanından ayırarak olmayan karakter.</li> <li>Nokta karakteri içeremez '.' hemen önceki hello ' @' simgesi</li></ul> |
| Uzunluk kısıtlamaları |<ul> <li>Toplam uzunluğu 113 karakterden uzun olamaz</li><li>Merhaba önce 64 karakteri ' @' simgesi</li><li>48 karakterden hello sonra ' @' simgesi</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Yalnızca toocloud kullanıcı hesapları geçerli parola ilkeleri

Aşağıdaki tablonun hello oluşturulan ve Azure AD'de yönetilen uygulanan toouser hesapları olabilir hello kullanılabilir parola ilkesi ayarları açıklanır.

| Özellik | Gereksinimler |
| --- | --- |
| İzin verilen karakter |<ul><li>A-Z</li><li>a - z</li><li>0 – 9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| Karakterlere izin verilmez |<ul><li>Unicode karakterler</li><li>Alanları</li><li> **Güçlü parolalar**: bir nokta karakterini içeremez '.' hemen önceki hello ' @' simgesi</li></ul> |
| Parola kısıtlamaları |<ul><li>en az 8 karakter ve en fazla 16 karakter</li><li>**Güçlü parolalar**: hello aşağıdaki 4 dışında 3 gerektirir:<ul><li>Küçük harf karakterler</li><li>Büyük harf karakterler</li><li>Sayılar (0-9)</li><li>Simgeler (parola kısıtlamaları yukarıdaki bakın)</li></ul></li></ul> |
| Parola geçerlilik süresi |<ul><li>Varsayılan değer: **90** gün </li><li>Değer hello Azure Active Directory için Windows PowerShell Modülü'ndan hello Set-MsolPasswordPolicy cmdlet'ini kullanarak yapılandırılabilir.</li></ul> |
| Parola sona erme bildirimi |<ul><li>Varsayılan değer: **14** (parolasının süresi dolmadan)</li><li>Merhaba Set-MsolPasswordPolicy cmdlet'ini kullanarak yapılandırılabilir değerdir.</li></ul> |
| Parola süre sonu |<ul><li>Varsayılan değer: **false** gün (Bu parola süre sonu etkinleştirildiğini gösteren) </li><li>Değer hello kümesi MsolUser cmdlet'ini kullanarak bireysel kullanıcı hesapları için yapılandırılabilir. </li></ul> |
| Parola **değiştirmek** geçmişi |Son parola **olamaz** kullanılabilir yeniden ne zaman **değiştirme** bir parola. |
| Parola **sıfırlama** geçmişi | Son parola **olabilir** kullanılabilir yeniden ne zaman **sıfırlama** Unutulan parolayı. |
| Hesap kilitleme |10 başarısız oturum açma girişiminden sonra (yanlış parola), hello kullanıcı için bir dakika kilitlenir. Daha fazla yanlış oturum açma hello kullanıcı kilitlenme süreleri artırmak için çalışır. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Parola süre sonu ilkeleri Azure Active Directory'de ayarlayın.

Bir Microsoft bulut hizmeti için genel yönetici kullanıcı parolalarını değil tooexpire yedeklemek hello Microsoft Azure Active Directory için Windows PowerShell modülü tooset kullanabilirsiniz. Windows PowerShell cmdlet'leri tooremove hello-yapılandırma veya toosee hangi kullanıcı parolalarını değil tooexpire ayarlanır süresi asla de kullanabilirsiniz. Bu kılavuz, ayrıca kimlik ve Dizin Hizmetleri için Microsoft Azure Active Directory'ye bağlı Microsoft Intune ve Office 365 gibi tooother sağlayıcıları geçerlidir.

> [!NOTE]
> Yalnızca parolaları dizin eşitleme ile eşitlenmemiş kullanıcı hesapları yapılandırılabilir için toonot süresi dolacak. Dizin eşitleme hakkında daha fazla bilgi için bkz:[Bağlan Azure AD ile](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>Ayarlama veya PowerShell kullanarak parola ilkeleri denetleyin

başlatılan tooget ihtiyacınız çok[hello Azure AD PowerShell modülü yükleyip](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0). Yüklemediyseniz sonra her bir alan tooconfigure hello adımları izleyebilirsiniz.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>Nasıl bir parola için toocheck süre sonu ilkesi
1. TooWindows PowerShell şirket Yöneticisi kimlik bilgilerinizi kullanarak bağlanın.
2. Aşağıdaki komutları hello birini yürütün:

   * toosee tek bir kullanıcının parolasını toonever olup ayarlandığında sona, cmdlet hello kullanıcı asıl adı (UPN) kullanarak aşağıdaki hello çalıştırın (örneğin, aprilr@contoso.onmicrosoft.com) veya kullanıcı kimliği hello toocheck istediğiniz hello kullanıcısı:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee tüm kullanıcılar için ayarı "Parola her zaman geçerli olsun" Merhaba, hello aşağıdaki cmdlet'i çalıştırın:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>Bir parola tooexpire ayarlayın

1. TooWindows PowerShell şirket Yöneticisi kimlik bilgilerinizi kullanarak bağlanın.
2. Aşağıdaki komutları hello birini yürütün:

   * tooset hello parola bir kullanıcının hello parola süresinin dolduğu böylece hello kullanıcı asıl adı (UPN) kullanarak cmdlet'i aşağıdaki hello çalıştırmak veya hello kullanıcının kullanıcı Kimliğini hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * süreleri doluncaya böylece tooset hello parolalarını hello kuruluşunuzdaki tüm kullanıcılar hello aşağıdaki cmdlet'i kullanın:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>Bir parola toonever sona ayarlama

1. TooWindows PowerShell şirket Yöneticisi kimlik bilgilerinizi kullanarak bağlanın.
2. Aşağıdaki komutları hello birini yürütün:

   * bir kullanıcı toonever tooset hello parolasını sona hello kullanıcı asıl adı (UPN) kullanarak cmdlet'i aşağıdaki hello çalıştırmak veya hello kullanıcının kullanıcı Kimliğini hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * bir kuruluş toonever tüm hello kullanıcılar tooset hello parolalarını sona, hello aşağıdaki cmdlet'i çalıştırın:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin
