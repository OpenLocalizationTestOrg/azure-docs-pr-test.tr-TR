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
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="cdce9-103">Parola sıfırlama son kullanıcı kayıt gerektirmeden dağıtma</span><span class="sxs-lookup"><span data-stu-id="cdce9-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="cdce9-104">Self Servis parola sıfırlama (SSPR) dağıtılması için kimlik doğrulama verileri toobe mevcut gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdce9-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="cdce9-105">Bazı kuruluşlar kendi kimlik doğrulama verileri girin, kullanıcılar sahiptir, ancak birçok kuruluş Active Directory'de mevcut verilerle toosynchronize tercih.</span><span class="sxs-lookup"><span data-stu-id="cdce9-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="cdce9-106">Veri şirket içi dizininizde düzgün biçimlendirilmiş ve yapılandırırsanız [hızlı ayarları kullanarak Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md), veriler kullanılabilir tooAzure AD hale gelir ve SSPR hiçbir kullanıcı etkileşimi gerekli.</span><span class="sxs-lookup"><span data-stu-id="cdce9-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="cdce9-107">Tüm telefon numaralarını olmalıdır hello biçimi + CountryCode PhoneNumber örnek: + 1 4255551234 toowork düzgün.</span><span class="sxs-lookup"><span data-stu-id="cdce9-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="cdce9-108">Parola sıfırlama telefon uzantıları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="cdce9-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="cdce9-109">Merhaba kurulmadan önce bile hello + 1 4255551234 X 12345 biçiminde uzantıları kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="cdce9-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="cdce9-110">Doldurulmuş alanları</span><span class="sxs-lookup"><span data-stu-id="cdce9-110">Fields populated</span></span>

<span data-ttu-id="cdce9-111">Aşağıdaki Azure AD Connect hello hello varsayılan ayarları kullanırsanız eşlemeleri yapılır.</span><span class="sxs-lookup"><span data-stu-id="cdce9-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="cdce9-112">Şirket içi AD</span><span class="sxs-lookup"><span data-stu-id="cdce9-112">On-premises AD</span></span> | <span data-ttu-id="cdce9-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdce9-113">Azure AD</span></span> | <span data-ttu-id="cdce9-114">Azure AD kimlik doğrulaması kişi bilgisi</span><span class="sxs-lookup"><span data-stu-id="cdce9-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdce9-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="cdce9-115">telephoneNumber</span></span> | <span data-ttu-id="cdce9-116">Ofis telefonu</span><span class="sxs-lookup"><span data-stu-id="cdce9-116">Office phone</span></span> | <span data-ttu-id="cdce9-117">Diğer telefon</span><span class="sxs-lookup"><span data-stu-id="cdce9-117">Alternate phone</span></span> |
| <span data-ttu-id="cdce9-118">Mobil</span><span class="sxs-lookup"><span data-stu-id="cdce9-118">mobile</span></span> | <span data-ttu-id="cdce9-119">Cep telefonu</span><span class="sxs-lookup"><span data-stu-id="cdce9-119">Mobile phone</span></span> | <span data-ttu-id="cdce9-120">Telefon</span><span class="sxs-lookup"><span data-stu-id="cdce9-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="cdce9-121">Güvenlik sorularını ve yanıtlarını</span><span class="sxs-lookup"><span data-stu-id="cdce9-121">Security questions and answers</span></span>

<span data-ttu-id="cdce9-122">Güvenlik sorularını ve yanıtlarını Azure AD kiracınızda güvenli bir şekilde depolanır ve yalnızca hello aracılığıyla erişilebilir toousers olan [SSPR kayıt portalı](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="cdce9-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="cdce9-123">Yöneticiler bakın veya başka kullanıcıların sorularını ve yanıtlarını Merhaba içeriğine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cdce9-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="cdce9-124">Kullanıcı kayıtları ne olur</span><span class="sxs-lookup"><span data-stu-id="cdce9-124">What happens when a user registers</span></span>

<span data-ttu-id="cdce9-125">Bir kullanıcı kaydettiğinde hello kayıt sayfası alanları izleyen hello ayarlar:</span><span class="sxs-lookup"><span data-stu-id="cdce9-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="cdce9-126">Kimlik doğrulama telefon</span><span class="sxs-lookup"><span data-stu-id="cdce9-126">Authentication Phone</span></span>
* <span data-ttu-id="cdce9-127">Kimlik doğrulama e-posta</span><span class="sxs-lookup"><span data-stu-id="cdce9-127">Authentication Email</span></span>
* <span data-ttu-id="cdce9-128">Güvenlik sorularını ve yanıtlarını</span><span class="sxs-lookup"><span data-stu-id="cdce9-128">Security Questions and Answers</span></span>

<span data-ttu-id="cdce9-129">İçin bir değer sağladıysanız **cep telefonu** veya **alternatif e-posta**, kullanıcıların hemen kullanabilir bu değerleri tooreset kullanıcıların parolalarını hello hizmeti için kaydolmadıysanız bile.</span><span class="sxs-lookup"><span data-stu-id="cdce9-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="cdce9-130">Ayrıca, kullanıcıların bu değerleri hello için ilk kez kaydederken bakın ve istediklerinde bunları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cdce9-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="cdce9-131">Başarıyla kaydettikten sonra bu değerler hello kalıcıdır **kimlik doğrulama telefon** ve **kimlik doğrulama e-posta** alanlar, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="cdce9-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="cdce9-132">Ayarlama ve PowerShell kullanarak kimlik doğrulama verileri okuma</span><span class="sxs-lookup"><span data-stu-id="cdce9-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="cdce9-133">alanları aşağıdaki hello PowerShell kullanılarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="cdce9-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="cdce9-134">Alternatif e-posta</span><span class="sxs-lookup"><span data-stu-id="cdce9-134">Alternate Email</span></span>
* <span data-ttu-id="cdce9-135">Cep telefonu</span><span class="sxs-lookup"><span data-stu-id="cdce9-135">Mobile Phone</span></span>
* <span data-ttu-id="cdce9-136">Ofis telefonu - yalnızca bir şirket içi diziniyle eşitlemeyi değil, ayarlanabilir</span><span class="sxs-lookup"><span data-stu-id="cdce9-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="cdce9-137">PowerShell V1 kullanma</span><span class="sxs-lookup"><span data-stu-id="cdce9-137">Using PowerShell V1</span></span>

<span data-ttu-id="cdce9-138">başlatılan tooget ihtiyacınız çok[hello Azure AD PowerShell modülü yükleyip](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="cdce9-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="cdce9-139">Yüklemediyseniz sonra her bir alan tooconfigure izleyin hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdce9-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="cdce9-140">PowerShell V1 ile kimlik doğrulaması veri kümesi</span><span class="sxs-lookup"><span data-stu-id="cdce9-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="cdce9-141">PowerShellPowerShell V1 ile kimlik doğrulama verilerini okuma</span><span class="sxs-lookup"><span data-stu-id="cdce9-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="cdce9-142">Kimlik doğrulama telefon ve kimlik doğrulama e-posta yalnızca okunabilir Powershell V1 kullanarak hello kullanarak komutları anlatılmaktadır</span><span class="sxs-lookup"><span data-stu-id="cdce9-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="cdce9-143">PowerShell V2 kullanma</span><span class="sxs-lookup"><span data-stu-id="cdce9-143">Using PowerShell V2</span></span>

<span data-ttu-id="cdce9-144">başlatılan tooget ihtiyacınız çok[hello Azure AD V2 PowerShell modülü yükleyip](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="cdce9-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="cdce9-145">Yüklemediyseniz sonra her bir alan tooconfigure izleyin hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdce9-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="cdce9-146">Install-Module destekleyen hızla son sürümlerine PowerShell tooinstall (zaten yüklüyse hello ilk satırı yalnızca toosee denetler) Bu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cdce9-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="cdce9-147">PowerShell V2 kimlik doğrulaması veri kümesi</span><span class="sxs-lookup"><span data-stu-id="cdce9-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="cdce9-148">PowerShell V2 ile kimlik doğrulama verilerini okuma</span><span class="sxs-lookup"><span data-stu-id="cdce9-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="cdce9-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cdce9-149">Next steps</span></span>

<span data-ttu-id="cdce9-150">bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar</span><span class="sxs-lookup"><span data-stu-id="cdce9-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="cdce9-151">[**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın</span><span class="sxs-lookup"><span data-stu-id="cdce9-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="cdce9-152">[**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="cdce9-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="cdce9-153">[**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma</span><span class="sxs-lookup"><span data-stu-id="cdce9-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="cdce9-154">[**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdce9-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="cdce9-155">[**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın</span><span class="sxs-lookup"><span data-stu-id="cdce9-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="cdce9-156">[**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin</span><span class="sxs-lookup"><span data-stu-id="cdce9-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="cdce9-157">[**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin</span><span class="sxs-lookup"><span data-stu-id="cdce9-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="cdce9-158">[**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl?</span><span class="sxs-lookup"><span data-stu-id="cdce9-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="cdce9-159">Neden?</span><span class="sxs-lookup"><span data-stu-id="cdce9-159">Why?</span></span> <span data-ttu-id="cdce9-160">Ne?</span><span class="sxs-lookup"><span data-stu-id="cdce9-160">What?</span></span> <span data-ttu-id="cdce9-161">Nerede?</span><span class="sxs-lookup"><span data-stu-id="cdce9-161">Where?</span></span> <span data-ttu-id="cdce9-162">Kim?</span><span class="sxs-lookup"><span data-stu-id="cdce9-162">Who?</span></span> <span data-ttu-id="cdce9-163">Ne zaman?</span><span class="sxs-lookup"><span data-stu-id="cdce9-163">When?</span></span> <span data-ttu-id="cdce9-164">-Her zaman tooask istediğinizi tooquestions yanıtlar</span><span class="sxs-lookup"><span data-stu-id="cdce9-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="cdce9-165">[**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin</span><span class="sxs-lookup"><span data-stu-id="cdce9-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
