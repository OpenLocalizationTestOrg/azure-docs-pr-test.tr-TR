---
title: "Azure Active Directory B2B işbirliği API ve özelleştirme | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği, iş ortaklarının kurumsal uygulamalarınıza seçmeli olarak erişmelerini mümkün kılarak şirketler arası ilişkilerinizi destekler."
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="00521-103">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="00521-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="00521-104">Sizi davet işlemi kuruluşları için en iyi şekilde özelleştirmek istedikleri bize birçok müşteri karşılaşmışsınız.</span><span class="sxs-lookup"><span data-stu-id="00521-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="00521-105">Bizim API'si ile tam olarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00521-105">With our API, you can do just that.</span></span> [<span data-ttu-id="00521-106">https://Developer.microsoft.com/Graph/docs/api-Reference/V1.0/Resources/invitation</span><span class="sxs-lookup"><span data-stu-id="00521-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="00521-107">API davet özellikleri</span><span class="sxs-lookup"><span data-stu-id="00521-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="00521-108">API aşağıdaki özellikleri sunar:</span><span class="sxs-lookup"><span data-stu-id="00521-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="00521-109">Bir dış kullanıcı ile davet *herhangi* e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="00521-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="00521-110">Bunlar, daveti kabul ettikten sonra güden kullanıcılarınıza istediğiniz özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="00521-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="00521-111">Bize aracılığıyla standart davet posta göndermeyi seçin</span><span class="sxs-lookup"><span data-stu-id="00521-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="00521-112">içeren bir ileti özelleştirebileceğiniz alıcısına</span><span class="sxs-lookup"><span data-stu-id="00521-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="00521-113">Ve cc seçin: Bu ortak çalışanı davet hakkında Döngüdeki tutmak istediğiniz kişilerin.</span><span class="sxs-lookup"><span data-stu-id="00521-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="00521-114">Veya Azure AD aracılığıyla bildirimleri göndermek seçerek daveti ve hazırlama iş akışı tamamen özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00521-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="00521-115">Bu durumda, bir kullanım URL bir e-posta şablonu, anlık ileti veya tercih ettiğiniz başka bir dağıtım yöntem katıştırma API'sinden ulaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="00521-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="00521-116">Son olarak, bir yönetici, üye olarak kullanıcı davet seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00521-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="00521-117">Yetkilendirme modeli</span><span class="sxs-lookup"><span data-stu-id="00521-117">Authorization model</span></span>
<span data-ttu-id="00521-118">API şu yetkilendirme modlarında çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="00521-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="00521-119">Uygulama + kullanıcı modu</span><span class="sxs-lookup"><span data-stu-id="00521-119">App + User mode</span></span>
<span data-ttu-id="00521-120">Bu modda, aktaranın B2B davetleri olması oluşturma izinlerine sahip olmasını API gereksinimlerini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="00521-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="00521-121">Uygulama yalnızca modu</span><span class="sxs-lookup"><span data-stu-id="00521-121">App only mode</span></span>
<span data-ttu-id="00521-122">Uygulama yalnızca bağlamda uygulamanın başarılı olması davet için User.ReadWrite.All veya Directory.ReadWrite.All kapsamı gerekir.</span><span class="sxs-lookup"><span data-stu-id="00521-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="00521-123">Daha fazla bilgi için bkz: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="00521-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="00521-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00521-124">PowerShell</span></span>
<span data-ttu-id="00521-125">Şimdi, ekleme ve bir kuruluş için dış kullanıcılar kolayca davet etmek için PowerShell kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="00521-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="00521-126">Cmdlet'ini kullanarak bir davet oluşturun:</span><span class="sxs-lookup"><span data-stu-id="00521-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="00521-127">Aşağıdaki seçenekleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="00521-127">You can use the following options:</span></span>

* <span data-ttu-id="00521-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="00521-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="00521-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="00521-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="00521-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="00521-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="00521-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="00521-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="00521-132">Ayrıca daveti API Başvurusu'nda uğradı kontrol edebilirsiniz [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="00521-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="00521-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00521-133">Next steps</span></span>

<span data-ttu-id="00521-134">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="00521-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="00521-135">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="00521-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="00521-136">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="00521-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="00521-137">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="00521-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="00521-138">B2B işbirliği davet e-posta öğeleri</span><span class="sxs-lookup"><span data-stu-id="00521-138">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="00521-139">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="00521-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="00521-140">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="00521-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="00521-141">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="00521-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="00521-142">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="00521-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="00521-143">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="00521-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="00521-144">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="00521-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="00521-145">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="00521-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
