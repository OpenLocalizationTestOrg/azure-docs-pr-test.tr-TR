---
title: "aaaAzure Active Directory B2B işbirliği API ve özelleştirme | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği Kurumsal uygulamalarınıza iş ortakları tooselectively erişim sağlayarak, şirketler arası ilişkilerinizi destekler."
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
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="95881-103">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="95881-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="95881-104">Biz toocustomize hello davet işlem kuruluşlarının en iyi şekilde çalışır şekilde istedikleri bize birçok müşteri karşılaşmışsınız.</span><span class="sxs-lookup"><span data-stu-id="95881-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="95881-105">Bizim API'si ile tam olarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95881-105">With our API, you can do just that.</span></span> [<span data-ttu-id="95881-106">https://Developer.microsoft.com/Graph/docs/api-Reference/V1.0/Resources/invitation</span><span class="sxs-lookup"><span data-stu-id="95881-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="95881-107">Merhaba davet API özellikleri</span><span class="sxs-lookup"><span data-stu-id="95881-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="95881-108">Hello API hello aşağıdaki özellikleri sunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="95881-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="95881-109">Bir dış kullanıcı ile davet *herhangi* e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="95881-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="95881-110">Bunlar, daveti kabul ettikten sonra kullanıcılar tooland istediğiniz özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="95881-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="95881-111">Bize aracılığıyla toosend hello standart davet posta seçin</span><span class="sxs-lookup"><span data-stu-id="95881-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="95881-112">özelleştirebileceğiniz bir ileti toohello alıcı</span><span class="sxs-lookup"><span data-stu-id="95881-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="95881-113">Ve toocc seçin: Merhaba tookeep istediğiniz kişilerin döngü, bu ortak çalışanı davet hakkında.</span><span class="sxs-lookup"><span data-stu-id="95881-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="95881-114">Veya Azure AD aracılığıyla değil toosend bildirimleri seçerek daveti ve hazırlama iş akışı tamamen özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95881-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="95881-115">Bu durumda, bir kullanım URL hello bir e-posta şablonu, anlık ileti veya tercih ettiğiniz başka bir dağıtım yöntem katıştırma API öğesinden ulaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="95881-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="95881-116">Son olarak, bir yönetici, üye olarak tooinvite hello kullanıcı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95881-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="95881-117">Yetkilendirme modeli</span><span class="sxs-lookup"><span data-stu-id="95881-117">Authorization model</span></span>
<span data-ttu-id="95881-118">Merhaba API yetkilendirme modları aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95881-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="95881-119">Uygulama + kullanıcı modu</span><span class="sxs-lookup"><span data-stu-id="95881-119">App + User mode</span></span>
<span data-ttu-id="95881-120">Bu modda, aktaranın kullanarak hello API gereksinimlerini toohave hello izinleri toobe B2B davetleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="95881-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="95881-121">Uygulama yalnızca modu</span><span class="sxs-lookup"><span data-stu-id="95881-121">App only mode</span></span>
<span data-ttu-id="95881-122">Uygulama yalnızca bağlamda hello uygulamanın hello davet toosucceed için hello User.ReadWrite.All veya Directory.ReadWrite.All kapsamı gerekir.</span><span class="sxs-lookup"><span data-stu-id="95881-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="95881-123">Daha fazla bilgi için bkz: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="95881-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="95881-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="95881-124">PowerShell</span></span>
<span data-ttu-id="95881-125">Şimdi olası toouse PowerShell tooadd ve davet dış kullanıcılar tooan kuruluş kolayca değil.</span><span class="sxs-lookup"><span data-stu-id="95881-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="95881-126">Merhaba cmdlet'ini kullanarak bir davet oluşturun:</span><span class="sxs-lookup"><span data-stu-id="95881-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="95881-127">Hello aşağıdaki seçenekleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95881-127">You can use hello following options:</span></span>

* <span data-ttu-id="95881-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="95881-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="95881-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="95881-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="95881-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="95881-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="95881-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="95881-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="95881-132">Merhaba davet API Başvurusu'nda uğradı kontrol edebilirsiniz [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="95881-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="95881-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95881-133">Next steps</span></span>

<span data-ttu-id="95881-134">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="95881-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="95881-135">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="95881-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="95881-136">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="95881-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="95881-137">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="95881-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="95881-138">Merhaba B2B işbirliği davet e-posta Hello öğeleri</span><span class="sxs-lookup"><span data-stu-id="95881-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="95881-139">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="95881-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="95881-140">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="95881-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="95881-141">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="95881-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="95881-142">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="95881-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="95881-143">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="95881-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="95881-144">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="95881-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="95881-145">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="95881-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
