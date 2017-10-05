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
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="b4a21-103">Parola sıfırlama son kullanıcı kayıt gerektirmeden dağıtma</span><span class="sxs-lookup"><span data-stu-id="b4a21-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="b4a21-104">Self Servis parola sıfırlama (SSPR) dağıtılması için kimlik doğrulama verileri mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4a21-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="b4a21-105">Bazı kuruluşlar kendi kimlik doğrulama verileri girin, kullanıcılar sahiptir, ancak mevcut verileri Active Directory ile eşitlemek birçok kuruluş tercih.</span><span class="sxs-lookup"><span data-stu-id="b4a21-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="b4a21-106">Veri şirket içi dizininizde düzgün biçimlendirilmiş ve yapılandırırsanız [hızlı ayarları kullanarak Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md), veriler Azure AD ile kullanılabilir hale gelir ve SSPR hiçbir kullanıcı etkileşimi gerekli.</span><span class="sxs-lookup"><span data-stu-id="b4a21-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="b4a21-107">Tüm telefon numaralarını olmalıdır biçimi + CountryCode PhoneNumber örnek: + 1 düzgün çalışması için 4255551234.</span><span class="sxs-lookup"><span data-stu-id="b4a21-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a21-108">Parola sıfırlama telefon uzantıları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="b4a21-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="b4a21-109">Kurulmadan önce bile + 1 4255551234 X 12345 biçiminde uzantıları kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="b4a21-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="b4a21-110">Doldurulmuş alanları</span><span class="sxs-lookup"><span data-stu-id="b4a21-110">Fields populated</span></span>

<span data-ttu-id="b4a21-111">Azure AD Connect varsayılan ayarları kullanırsanız aşağıdaki eşlemelerini yapılır.</span><span class="sxs-lookup"><span data-stu-id="b4a21-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="b4a21-112">Şirket içi AD</span><span class="sxs-lookup"><span data-stu-id="b4a21-112">On-premises AD</span></span> | <span data-ttu-id="b4a21-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4a21-113">Azure AD</span></span> | <span data-ttu-id="b4a21-114">Azure AD kimlik doğrulaması kişi bilgisi</span><span class="sxs-lookup"><span data-stu-id="b4a21-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4a21-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="b4a21-115">telephoneNumber</span></span> | <span data-ttu-id="b4a21-116">Ofis telefonu</span><span class="sxs-lookup"><span data-stu-id="b4a21-116">Office phone</span></span> | <span data-ttu-id="b4a21-117">Diğer telefon</span><span class="sxs-lookup"><span data-stu-id="b4a21-117">Alternate phone</span></span> |
| <span data-ttu-id="b4a21-118">Mobil</span><span class="sxs-lookup"><span data-stu-id="b4a21-118">mobile</span></span> | <span data-ttu-id="b4a21-119">Cep telefonu</span><span class="sxs-lookup"><span data-stu-id="b4a21-119">Mobile phone</span></span> | <span data-ttu-id="b4a21-120">Telefon</span><span class="sxs-lookup"><span data-stu-id="b4a21-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="b4a21-121">Güvenlik sorularını ve yanıtlarını</span><span class="sxs-lookup"><span data-stu-id="b4a21-121">Security questions and answers</span></span>

<span data-ttu-id="b4a21-122">Güvenlik sorularını ve yanıtlarını Azure AD kiracınızda güvenli bir şekilde depolanır ve yalnızca üzerinden kullanıcılara erişilebilir [SSPR kayıt portalı](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="b4a21-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="b4a21-123">Yöneticiler bakın veya başka kullanıcıların sorularını ve yanıtlarını içeriğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4a21-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="b4a21-124">Kullanıcı kayıtları ne olur</span><span class="sxs-lookup"><span data-stu-id="b4a21-124">What happens when a user registers</span></span>

<span data-ttu-id="b4a21-125">Bir kullanıcı kaydettiğinde kayıt sayfası aşağıdaki alanları ayarlar:</span><span class="sxs-lookup"><span data-stu-id="b4a21-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="b4a21-126">Kimlik doğrulama telefon</span><span class="sxs-lookup"><span data-stu-id="b4a21-126">Authentication Phone</span></span>
* <span data-ttu-id="b4a21-127">Kimlik doğrulama e-posta</span><span class="sxs-lookup"><span data-stu-id="b4a21-127">Authentication Email</span></span>
* <span data-ttu-id="b4a21-128">Güvenlik sorularını ve yanıtlarını</span><span class="sxs-lookup"><span data-stu-id="b4a21-128">Security Questions and Answers</span></span>

<span data-ttu-id="b4a21-129">İçin bir değer sağladıysanız **cep telefonu** veya **alternatif e-posta**, kullanıcıların hemen kullanabilir bu değerleri kendi parolalarını sıfırlamak için hizmet için kaydolmadıysanız bile.</span><span class="sxs-lookup"><span data-stu-id="b4a21-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="b4a21-130">Ayrıca, kullanıcılar ilk kez kaydederken bu değerleri görmek ve istediklerinde onları değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="b4a21-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="b4a21-131">İçinde başarıyla kaydettikten sonra bu değerler kalıcıdır **kimlik doğrulama telefon** ve **kimlik doğrulama e-posta** alanlar, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="b4a21-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="b4a21-132">Ayarlama ve PowerShell kullanarak kimlik doğrulama verileri okuma</span><span class="sxs-lookup"><span data-stu-id="b4a21-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="b4a21-133">Aşağıdaki alanları PowerShell kullanılarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b4a21-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="b4a21-134">Alternatif e-posta</span><span class="sxs-lookup"><span data-stu-id="b4a21-134">Alternate Email</span></span>
* <span data-ttu-id="b4a21-135">Cep telefonu</span><span class="sxs-lookup"><span data-stu-id="b4a21-135">Mobile Phone</span></span>
* <span data-ttu-id="b4a21-136">Ofis telefonu - yalnızca bir şirket içi diziniyle eşitlemeyi değil, ayarlanabilir</span><span class="sxs-lookup"><span data-stu-id="b4a21-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="b4a21-137">PowerShell V1 kullanma</span><span class="sxs-lookup"><span data-stu-id="b4a21-137">Using PowerShell V1</span></span>

<span data-ttu-id="b4a21-138">Başlamak için yapmanız [Azure AD PowerShell modülü yükleyip](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="b4a21-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="b4a21-139">Yüklemediyseniz sonra her bir alan yapılandırmak için izlediği adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4a21-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="b4a21-140">PowerShell V1 ile kimlik doğrulaması veri kümesi</span><span class="sxs-lookup"><span data-stu-id="b4a21-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="b4a21-141">PowerShellPowerShell V1 ile kimlik doğrulama verilerini okuma</span><span class="sxs-lookup"><span data-stu-id="b4a21-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="b4a21-142">Kimlik doğrulama telefon ve kimlik doğrulama e-posta yalnızca okunabilir Powershell V1 kullanarak gelen komutlarda kullanma</span><span class="sxs-lookup"><span data-stu-id="b4a21-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="b4a21-143">PowerShell V2 kullanma</span><span class="sxs-lookup"><span data-stu-id="b4a21-143">Using PowerShell V2</span></span>

<span data-ttu-id="b4a21-144">Başlamak için yapmanız [Azure AD V2 PowerShell modülü yükleyip](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="b4a21-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="b4a21-145">Yüklemediyseniz sonra her bir alan yapılandırmak için izlediği adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4a21-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="b4a21-146">Install-Module destekleyen en son sürümlerinden PowerShell hızlı bir şekilde yüklemek için (ilk satırı yalnızca zaten yüklü olup olmadığını denetler) Bu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b4a21-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="b4a21-147">PowerShell V2 kimlik doğrulaması veri kümesi</span><span class="sxs-lookup"><span data-stu-id="b4a21-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="b4a21-148">PowerShell V2 ile kimlik doğrulama verilerini okuma</span><span class="sxs-lookup"><span data-stu-id="b4a21-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="b4a21-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4a21-149">Next steps</span></span>

<span data-ttu-id="b4a21-150">Aşağıdaki bağlantılar, Azure AD kullanarak parola sıfırlama ile ilgili ek bilgiler sağlar</span><span class="sxs-lookup"><span data-stu-id="b4a21-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="b4a21-151">[**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın</span><span class="sxs-lookup"><span data-stu-id="b4a21-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="b4a21-152">[**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b4a21-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="b4a21-153">[**Kullanıma Sunma** ](active-directory-passwords-best-practices.md) - Buradaki yönergelerle SSPR’ı planlayın ve kullanıcılarınıza dağıtın</span><span class="sxs-lookup"><span data-stu-id="b4a21-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="b4a21-154">[**Özelleştirme**](active-directory-passwords-customize.md) - SSPR deneyiminin görünümünü şirketiniz için özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b4a21-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="b4a21-155">[**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b4a21-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="b4a21-156">[**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin</span><span class="sxs-lookup"><span data-stu-id="b4a21-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="b4a21-157">[**Teknik Ayrıntı**](active-directory-passwords-how-it-works.md) - Nasıl çalıştığını anlamak için perde arkasına gidin</span><span class="sxs-lookup"><span data-stu-id="b4a21-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="b4a21-158">[**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl?</span><span class="sxs-lookup"><span data-stu-id="b4a21-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="b4a21-159">Neden?</span><span class="sxs-lookup"><span data-stu-id="b4a21-159">Why?</span></span> <span data-ttu-id="b4a21-160">Ne?</span><span class="sxs-lookup"><span data-stu-id="b4a21-160">What?</span></span> <span data-ttu-id="b4a21-161">Nerede?</span><span class="sxs-lookup"><span data-stu-id="b4a21-161">Where?</span></span> <span data-ttu-id="b4a21-162">Kim?</span><span class="sxs-lookup"><span data-stu-id="b4a21-162">Who?</span></span> <span data-ttu-id="b4a21-163">Ne zaman?</span><span class="sxs-lookup"><span data-stu-id="b4a21-163">When?</span></span> <span data-ttu-id="b4a21-164">- Her zaman sormak istediğiniz soruların yanıtları</span><span class="sxs-lookup"><span data-stu-id="b4a21-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="b4a21-165">[**Sorun giderme**](active-directory-passwords-troubleshoot.md) - SSPR ile yaygın olarak karşılaştığımız sorunların çözümü hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="b4a21-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
