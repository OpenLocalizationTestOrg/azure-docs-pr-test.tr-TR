---
title: "Azure Active Directory B2B işbirliği aaaTroubleshooting | Microsoft Docs"
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
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="1f432-103">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="1f432-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="1f432-104">Azure Active Directory (Azure AD) B2B işbirliği ile ortak sorunları için bazı çözümler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1f432-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="1f432-105">Bir dış kullanıcı eklediğiniz, ancak bunların benim genel adres defteri veya hello Kişi Seçici görmez</span><span class="sxs-lookup"><span data-stu-id="1f432-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="1f432-106">Burada dış kullanıcılar hello listesinde doldurulmaz durumlarda, birkaç dakika tooreplicate hello nesne alabilir.</span><span class="sxs-lookup"><span data-stu-id="1f432-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="1f432-107">B2B Konuk kullanıcı SharePoint Online/OneDrive kişiler seçicide göstermiyor</span><span class="sxs-lookup"><span data-stu-id="1f432-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="1f432-108">Merhaba özelliği toosearch hello SharePoint Online (SPO) Kişi Seçici varolan Konuk kullanıcılar için varsayılan toomatch eski davranışı tarafından Kapalı'dır.</span><span class="sxs-lookup"><span data-stu-id="1f432-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="1f432-109">Bu özellik 'ShowPeoplePickerSuggestionsForGuestUsers' hello Kiracı ve site koleksiyonu düzeyinde ayarlanması hello kullanarak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f432-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="1f432-110">Üyeleri izin veren hello kümesi SPOTenant ve Set-SPOSite cmdlet'lerini kullanarak hello özelliğini ayarlayabilirsiniz toosearch hello dizinindeki tüm mevcut Konuk kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="1f432-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="1f432-111">Değişiklikler hello Kiracı kapsamda zaten sağlanan SPO site etkilemez.</span><span class="sxs-lookup"><span data-stu-id="1f432-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="1f432-112">Dizin için davet devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="1f432-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="1f432-113">İzinleri tooinvite kullanıcılar olmadığını bildirilir olursa, kullanıcı hesabınızın yetkili tooinvite dış kullanıcılar kullanıcı ayarları altında olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="1f432-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="1f432-114">Kısa süre önce bu ayarları veya değiştirdiyseniz hello Konuk davet eden rol tooa kullanıcı atanmış ise hello değişikliklerin etkili olması 15-60 dakikalık bir gecikmeyle olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f432-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="1f432-115">ı davet hello kullanıcı kullanım sırasında bir hata alıyor</span><span class="sxs-lookup"><span data-stu-id="1f432-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="1f432-116">Sık karşılaşılan hatalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1f432-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="1f432-117">Davetlilerin yönetici kendi Kiracı oluşturulan EmailVerified kullanıcılar izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="1f432-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="1f432-118">Ne zaman, kuruluşunuzun Azure Active Directory'yi kullanarak, ancak burada, özel kullanıcı hesabına hello kullanıcıları davet yok (örneğin, hello kullanıcı Azure AD contoso.com yok).</span><span class="sxs-lookup"><span data-stu-id="1f432-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="1f432-119">contoso.com Merhaba yönetici kullanıcılar oluşturulmasını engelleyerek yerinde bir ilke olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f432-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="1f432-120">Dış kullanıcılar izin veriliyorsa hello kullanıcı kendi yönetim toodetermine ile denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f432-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="1f432-121">Merhaba dış kullanıcının yönetici kendi etki alanındaki kullanıcıların e-posta doğrulandı tooallow gerekebilir (Bu bkz [makale](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) e-posta doğrulandı kullanıcıların üzerinde).</span><span class="sxs-lookup"><span data-stu-id="1f432-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="1f432-122">Dış kullanıcı zaten bir Federasyon etki alanında mevcut değil</span><span class="sxs-lookup"><span data-stu-id="1f432-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="1f432-123">Federasyon kimlik doğrulaması kullanıyorsanız ve hello kullanıcı Azure Active Directory'de zaten yoksa, hello kullanıcı davet edilemez.</span><span class="sxs-lookup"><span data-stu-id="1f432-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="1f432-124">Bu sorun, hello tooresolve dış kullanıcının yönetici hello kullanıcının hesabı tooAzure Active Directory eşitleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f432-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="1f432-125">Nasıl mu\#', olmayan normal olarak geçerli bir karakter, Azure AD ile eşitleme?</span><span class="sxs-lookup"><span data-stu-id="1f432-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="1f432-126">"\#" Merhaba hesap davet UPN'ler içinde Azure AD B2B işbirliği veya dış kullanıcılar için ayrılmış bir karakter çünkü user@contoso.com user_contoso.com# haleEXT@fabrikam.onmicrosoft.com. Bu nedenle, \# şirket içinden gelen UPN'ler içinde toosign toohello Azure portal izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="1f432-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="1f432-127">Dış kullanıcılar tooa ekleme Grup eşitlendiğinde bir hata alıyorsunuz</span><span class="sxs-lookup"><span data-stu-id="1f432-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="1f432-128">Dış kullanıcılar yalnızca çok "atanan" eklenebilir veya şirket içi "Güvenlik" gruplarını ve değil misiniz toogroups yönetilen.</span><span class="sxs-lookup"><span data-stu-id="1f432-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="1f432-129">My dış kullanıcı bir e-posta tooredeem almadı.</span><span class="sxs-lookup"><span data-stu-id="1f432-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="1f432-130">Merhaba davet edilene ISS ile denetlemelisiniz veya adres aşağıdaki hello istenmeyen posta Filtresi tooensure izin verilir:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1f432-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="1f432-131">I hello özel ileti bazen davet iletileri ile birlikte almaz dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1f432-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="1f432-132">toocomply gizlilik yasalarıyla ile bizim API'leri içermeyen özel iletileri hello e-posta davetinde zaman:</span><span class="sxs-lookup"><span data-stu-id="1f432-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="1f432-133">Merhaba davet eden Kiracı davet hello bir e-posta adresi yok</span><span class="sxs-lookup"><span data-stu-id="1f432-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="1f432-134">Bir uygulama hizmeti asıl hello davet gönderdiğinde</span><span class="sxs-lookup"><span data-stu-id="1f432-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="1f432-135">Bu senaryoda önemli tooyou ise, bizim API davet e-posta bastırmak ve tercih ettiğiniz e-posta mekanizma hello gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f432-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="1f432-136">Kuruluşunuzun yasal Danışmanı toomake bu şekilde gönderdiğiniz e-posta ayrıca gizlilik yasalarına uygun emin başvurun.</span><span class="sxs-lookup"><span data-stu-id="1f432-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f432-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1f432-137">Next steps</span></span>

<span data-ttu-id="1f432-138">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="1f432-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1f432-139">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="1f432-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1f432-140">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="1f432-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="1f432-141">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="1f432-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="1f432-142">Merhaba B2B işbirliği davet e-posta Hello öğeleri</span><span class="sxs-lookup"><span data-stu-id="1f432-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="1f432-143">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="1f432-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="1f432-144">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="1f432-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="1f432-145">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="1f432-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="1f432-146">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="1f432-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="1f432-147">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="1f432-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="1f432-148">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="1f432-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="1f432-149">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="1f432-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
