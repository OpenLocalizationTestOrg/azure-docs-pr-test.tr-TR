---
title: Azure AD SSPR'yi veri gereksinimleri | Microsoft Docs
description: "Veri gereksinimleri için Azure AD Self Servis parola sıfırlama ve bunları karşılamak nasıl"
services: active-directory
keywords: 
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
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Parola sıfırlama son kullanıcı kayıt gerektirmeden dağıtma

Self Servis parola sıfırlama (SSPR) dağıtılması için kimlik doğrulama verileri mevcut olması gerekir. Bazı kuruluşlar kendi kimlik doğrulama verileri girin, kullanıcılar sahiptir, ancak mevcut verileri Active Directory ile eşitlemek birçok kuruluş tercih. Veri şirket içi dizininizde düzgün biçimlendirilmiş ve yapılandırırsanız [hızlı ayarları kullanarak Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md), veriler Azure AD ile kullanılabilir hale gelir ve SSPR hiçbir kullanıcı etkileşimi gerekli.

Tüm telefon numaralarını olmalıdır biçimi + CountryCode PhoneNumber örnek: + 1 düzgün çalışması için 4255551234.

> [!NOTE]
> Parola sıfırlama telefon uzantıları desteklemez. Kurulmadan önce bile + 1 4255551234 X 12345 biçiminde uzantıları kaldırılır.

## <a name="fields-populated"></a>Doldurulmuş alanları

Azure AD Connect varsayılan ayarları kullanırsanız aşağıdaki eşlemelerini yapılır.

| Şirket içi AD | Azure AD | Azure AD kimlik doğrulaması kişi bilgisi |
| --- | --- | --- |
| telephoneNumber | Ofis telefonu | Diğer telefon |
| Mobil | Cep telefonu | Telefon |


## <a name="security-questions-and-answers"></a>Güvenlik sorularını ve yanıtlarını

Güvenlik sorularını ve yanıtlarını Azure AD kiracınızda güvenli bir şekilde depolanır ve yalnızca üzerinden kullanıcılara erişilebilir [SSPR kayıt portalı](https://aka.ms/ssprsetup). Yöneticiler bakın veya başka kullanıcıların sorularını ve yanıtlarını içeriğini değiştirin.

### <a name="what-happens-when-a-user-registers"></a>Kullanıcı kayıtları ne olur

Bir kullanıcı kaydettiğinde kayıt sayfası aşağıdaki alanları ayarlar:

* Kimlik doğrulama telefon
* Kimlik doğrulama e-posta
* Güvenlik sorularını ve yanıtlarını

İçin bir değer sağladıysanız **cep telefonu** veya **alternatif e-posta**, kullanıcıların hemen kullanabilir bu değerleri kendi parolalarını sıfırlamak için hizmet için kaydolmadıysanız bile. Ayrıca, kullanıcılar ilk kez kaydederken bu değerleri görmek ve istediklerinde onları değiştirebilir. İçinde başarıyla kaydettikten sonra bu değerler kalıcıdır **kimlik doğrulama telefon** ve **kimlik doğrulama e-posta** alanlar, sırasıyla.

## <a name="set-and-read-authentication-data-using-powershell"></a>Ayarlama ve PowerShell kullanarak kimlik doğrulama verileri okuma

Aşağıdaki alanları PowerShell kullanılarak ayarlanabilir.

* Alternatif e-posta
* Cep telefonu
* Ofis telefonu - yalnızca bir şirket içi diziniyle eşitlemeyi değil, ayarlanabilir

### <a name="using-powershell-v1"></a>PowerShell V1 kullanma

Başlamak için yapmanız [Azure AD PowerShell modülü yükleyip](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Yüklemediyseniz sonra her bir alan yapılandırmak için izlediği adımları izleyebilirsiniz.

#### <a name="set-authentication-data-with-powershell-v1"></a>PowerShell V1 ile kimlik doğrulaması veri kümesi

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>PowerShellPowerShell V1 ile kimlik doğrulama verilerini okuma

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a>Kimlik doğrulama telefon ve kimlik doğrulama e-posta yalnızca okunabilir Powershell V1 kullanarak gelen komutlarda kullanma

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>PowerShell V2 kullanma

Başlamak için yapmanız [Azure AD V2 PowerShell modülü yükleyip](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Yüklemediyseniz sonra her bir alan yapılandırmak için izlediği adımları izleyebilirsiniz.

Install-Module destekleyen en son sürümlerinden PowerShell hızlı bir şekilde yüklemek için (ilk satırı yalnızca zaten yüklü olup olmadığını denetler) Bu komutları çalıştırın:

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>PowerShell V2 kimlik doğrulaması veri kümesi

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>PowerShell V2 ile kimlik doğrulama verilerini okuma

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>Sonraki adımlar

Aşağıdaki bağlantılar, Azure AD kullanarak parola sıfırlama ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Kullanıma Sunma** ](active-directory-passwords-best-practices.md) - Buradaki yönergelerle SSPR’ı planlayın ve kullanıcılarınıza dağıtın
* [**Özelleştirme**](active-directory-passwords-customize.md) - SSPR deneyiminin görünümünü şirketiniz için özelleştirin.
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik Ayrıntı**](active-directory-passwords-how-it-works.md) - Nasıl çalıştığını anlamak için perde arkasına gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? - Her zaman sormak istediğiniz soruların yanıtları
* [**Sorun giderme**](active-directory-passwords-troubleshoot.md) - SSPR ile yaygın olarak karşılaştığımız sorunların çözümü hakkında bilgi alın
