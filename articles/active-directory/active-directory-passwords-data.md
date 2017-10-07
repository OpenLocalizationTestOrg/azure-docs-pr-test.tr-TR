---
title: Azure AD SSPR'yi veri gereksinimleri | Microsoft Docs
description: "Veri gereksinimleri için Azure AD Self Servis parola sıfırlama ve nasıl toosatisfy bunları"
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
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Parola sıfırlama son kullanıcı kayıt gerektirmeden dağıtma

Self Servis parola sıfırlama (SSPR) dağıtılması için kimlik doğrulama verileri toobe mevcut gerekir. Bazı kuruluşlar kendi kimlik doğrulama verileri girin, kullanıcılar sahiptir, ancak birçok kuruluş Active Directory'de mevcut verilerle toosynchronize tercih. Veri şirket içi dizininizde düzgün biçimlendirilmiş ve yapılandırırsanız [hızlı ayarları kullanarak Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md), veriler kullanılabilir tooAzure AD hale gelir ve SSPR hiçbir kullanıcı etkileşimi gerekli.

Tüm telefon numaralarını olmalıdır hello biçimi + CountryCode PhoneNumber örnek: + 1 4255551234 toowork düzgün.

> [!NOTE]
> Parola sıfırlama telefon uzantıları desteklemez. Merhaba kurulmadan önce bile hello + 1 4255551234 X 12345 biçiminde uzantıları kaldırılır.

## <a name="fields-populated"></a>Doldurulmuş alanları

Aşağıdaki Azure AD Connect hello hello varsayılan ayarları kullanırsanız eşlemeleri yapılır.

| Şirket içi AD | Azure AD | Azure AD kimlik doğrulaması kişi bilgisi |
| --- | --- | --- |
| telephoneNumber | Ofis telefonu | Diğer telefon |
| Mobil | Cep telefonu | Telefon |


## <a name="security-questions-and-answers"></a>Güvenlik sorularını ve yanıtlarını

Güvenlik sorularını ve yanıtlarını Azure AD kiracınızda güvenli bir şekilde depolanır ve yalnızca hello aracılığıyla erişilebilir toousers olan [SSPR kayıt portalı](https://aka.ms/ssprsetup). Yöneticiler bakın veya başka kullanıcıların sorularını ve yanıtlarını Merhaba içeriğine değiştirin.

### <a name="what-happens-when-a-user-registers"></a>Kullanıcı kayıtları ne olur

Bir kullanıcı kaydettiğinde hello kayıt sayfası alanları izleyen hello ayarlar:

* Kimlik doğrulama telefon
* Kimlik doğrulama e-posta
* Güvenlik sorularını ve yanıtlarını

İçin bir değer sağladıysanız **cep telefonu** veya **alternatif e-posta**, kullanıcıların hemen kullanabilir bu değerleri tooreset kullanıcıların parolalarını hello hizmeti için kaydolmadıysanız bile. Ayrıca, kullanıcıların bu değerleri hello için ilk kez kaydederken bakın ve istediklerinde bunları değiştirin. Başarıyla kaydettikten sonra bu değerler hello kalıcıdır **kimlik doğrulama telefon** ve **kimlik doğrulama e-posta** alanlar, sırasıyla.

## <a name="set-and-read-authentication-data-using-powershell"></a>Ayarlama ve PowerShell kullanarak kimlik doğrulama verileri okuma

alanları aşağıdaki hello PowerShell kullanılarak ayarlanabilir.

* Alternatif e-posta
* Cep telefonu
* Ofis telefonu - yalnızca bir şirket içi diziniyle eşitlemeyi değil, ayarlanabilir

### <a name="using-powershell-v1"></a>PowerShell V1 kullanma

başlatılan tooget ihtiyacınız çok[hello Azure AD PowerShell modülü yükleyip](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Yüklemediyseniz sonra her bir alan tooconfigure izleyin hello adımları izleyebilirsiniz.

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

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>Kimlik doğrulama telefon ve kimlik doğrulama e-posta yalnızca okunabilir Powershell V1 kullanarak hello kullanarak komutları anlatılmaktadır

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>PowerShell V2 kullanma

başlatılan tooget ihtiyacınız çok[hello Azure AD V2 PowerShell modülü yükleyip](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Yüklemediyseniz sonra her bir alan tooconfigure izleyin hello adımları izleyebilirsiniz.

Install-Module destekleyen hızla son sürümlerine PowerShell tooinstall (zaten yüklüyse hello ilk satırı yalnızca toosee denetler) Bu komutları çalıştırın:

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

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin
