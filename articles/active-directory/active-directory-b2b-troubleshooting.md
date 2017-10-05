---
title: "Azure Active Directory B2B işbirliği sorunlarını giderme | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği ile ortak sorunları çözümler"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="891e3-103">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="891e3-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="891e3-104">Azure Active Directory (Azure AD) B2B işbirliği ile ortak sorunları için bazı çözümler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="891e3-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="891e3-105">Bir dış kullanıcı eklediğiniz, ancak bunların benim genel adres defteri veya kişi seçici görmez</span><span class="sxs-lookup"><span data-stu-id="891e3-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="891e3-106">Burada dış kullanıcılar listesinde doldurulmaz durumlarda nesne çoğaltmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="891e3-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="891e3-107">B2B Konuk kullanıcı SharePoint Online/OneDrive kişiler seçicide göstermiyor</span><span class="sxs-lookup"><span data-stu-id="891e3-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="891e3-108">SharePoint Online (SPO) Kişi Seçici varolan Konuk kullanıcılar için arama özelliğini eski davranışı eşleştirmek için varsayılan olarak kapalı'dır.</span><span class="sxs-lookup"><span data-stu-id="891e3-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="891e3-109">Bu özellik Kiracı ve site koleksiyonu düzeyinde 'ShowPeoplePickerSuggestionsForGuestUsers' ayarı kullanarak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="891e3-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="891e3-110">Tüm mevcut Konuk kullanıcılar dizinde arama üyelerin kümesini SPOTenant ve Set-SPOSite cmdlet'leri kullanarak özelliğini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="891e3-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="891e3-111">Kiracı kapsamındaki değişiklikleri zaten sağlanan SPO site etkilemez.</span><span class="sxs-lookup"><span data-stu-id="891e3-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="891e3-112">Dizin için davet devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="891e3-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="891e3-113">Kullanıcıları davet iznine sahip değil bildirilir, kullanıcı hesabınızın kullanıcı ayarları altında dış kullanıcıları davet yetkisi olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="891e3-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="891e3-114">Kısa süre önce bu ayarları değiştirilebilir veya konuk davet eden rolü atanmış bir kullanıcı, değişikliklerin etkili olması 15-60 dakikalık bir gecikmeyle olabilir.</span><span class="sxs-lookup"><span data-stu-id="891e3-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="891e3-115">I davet kullanıcı kullanım sırasında bir hata alıyor</span><span class="sxs-lookup"><span data-stu-id="891e3-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="891e3-116">Sık karşılaşılan hatalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="891e3-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="891e3-117">Davetlilerin yönetici kendi Kiracı oluşturulan EmailVerified kullanıcılar izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="891e3-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="891e3-118">Kullanıcılar, kuruluşunuzun Azure Active Directory'yi kullanarak, ancak burada belirli kullanıcının hesap yok davet olduğunda (örneğin, kullanıcının Azure AD contoso.com yok).</span><span class="sxs-lookup"><span data-stu-id="891e3-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="891e3-119">Contoso.com yönetici kullanıcılar oluşturulmasını engelleyerek yerinde bir ilke olabilir.</span><span class="sxs-lookup"><span data-stu-id="891e3-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="891e3-120">Kullanıcı dış kullanıcıların izinleri olup olmadığını belirlemek için yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="891e3-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="891e3-121">Dış kullanıcının yönetici e-posta doğrulandı kullanıcıların kendi etki alanlarındaki gerekebilir (Bu bkz [makale](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) e-posta doğrulandı kullanıcıların üzerinde).</span><span class="sxs-lookup"><span data-stu-id="891e3-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="891e3-122">Dış kullanıcı zaten bir Federasyon etki alanında mevcut değil</span><span class="sxs-lookup"><span data-stu-id="891e3-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="891e3-123">Federasyon kimlik doğrulaması kullanıyorsanız ve kullanıcının Azure Active Directory'de zaten yoksa, kullanıcı davet edilemez.</span><span class="sxs-lookup"><span data-stu-id="891e3-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="891e3-124">Bu sorunu çözmek için dış kullanıcının yönetici kullanıcının hesabı Azure Active Directory'ye eşitlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="891e3-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="891e3-125">Nasıl mu\#', olmayan normal olarak geçerli bir karakter, Azure AD ile eşitleme?</span><span class="sxs-lookup"><span data-stu-id="891e3-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="891e3-126">"\#" Azure AD B2B işbirliği veya dış kullanıcılar için ayrılmış bir karakter UPN'ler içinde olduğundan davet edilen hesap user@contoso.com user_contoso.com# haleEXT@fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="891e3-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="891e3-127">Bu nedenle, \# şirket içinden gelen UPN'ler de Azure portalında oturum açmak için izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="891e3-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="891e3-128">Bir hata Dış kullanıcılar eşitlenmiş bir gruba eklerken alır</span><span class="sxs-lookup"><span data-stu-id="891e3-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="891e3-129">Dış kullanıcılar yalnızca "atanan" veya "Güvenlik" grupları ve ana kopyalı şirket içi gruplarına eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="891e3-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="891e3-130">My dış kullanıcı kullanmak için bir e-posta almadı.</span><span class="sxs-lookup"><span data-stu-id="891e3-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="891e3-131">Davet edilene aşağıdaki adresi izin verildiğinden emin olmak için kendi ISS ya da istenmeyen posta Filtresi ile denetlemeniz gerekir:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="891e3-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="891e3-132">Özel ileti bazen davet iletileri ile birlikte almaz, ı dikkat edin</span><span class="sxs-lookup"><span data-stu-id="891e3-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="891e3-133">Gizlilik yasalarına uymak için bizim API'leri özel iletileri e-posta davetinde içermez zaman:</span><span class="sxs-lookup"><span data-stu-id="891e3-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="891e3-134">Davet eden davet Kiracı içinde bir e-posta adresi yok</span><span class="sxs-lookup"><span data-stu-id="891e3-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="891e3-135">Bir uygulama hizmeti asıl daveti gönderdiğinde</span><span class="sxs-lookup"><span data-stu-id="891e3-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="891e3-136">Bu senaryo için önemliyse bizim API davet e-posta bastırmak ve tercih ettiğiniz bir e-posta mekanizma aracılığıyla gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="891e3-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="891e3-137">Bu şekilde de gizlilik yasalarına uyumlu gönderdiğiniz herhangi bir e-emin olmak için kuruluşunuzun yasal Danışmanı başvurun.</span><span class="sxs-lookup"><span data-stu-id="891e3-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="891e3-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="891e3-138">Next steps</span></span>

<span data-ttu-id="891e3-139">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="891e3-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="891e3-140">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="891e3-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="891e3-141">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="891e3-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="891e3-142">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="891e3-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="891e3-143">B2B işbirliği davet e-posta öğeleri</span><span class="sxs-lookup"><span data-stu-id="891e3-143">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="891e3-144">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="891e3-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="891e3-145">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="891e3-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="891e3-146">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="891e3-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="891e3-147">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="891e3-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="891e3-148">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="891e3-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="891e3-149">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="891e3-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="891e3-150">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="891e3-150">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
