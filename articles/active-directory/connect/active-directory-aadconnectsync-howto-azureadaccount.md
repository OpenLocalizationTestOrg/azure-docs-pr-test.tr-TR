---
title: "Azure AD Connect eşitleme: nasıl toomanage hello Azure AD hizmet hesabı | Microsoft Docs"
description: "Bu konuda nasıl toorestore hello Azure AD hizmet hesabı belgeler."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, tooreset hello nasıl parolasını hello Azure AD Connect eşitleme Bağlayıcısı hizmeti hesabı"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="ce1f6-104">Azure AD Connect eşitleme: nasıl toomanage hello Azure AD hizmet hesabı</span><span class="sxs-lookup"><span data-stu-id="ce1f6-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="ce1f6-105">Azure AD Bağlayıcısı Hello tarafından kullanılan hello hizmet hesabı toobe hizmet boş varsayılır.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="ce1f6-106">Kimlik bilgilerini tooreset gerekiyorsa, bu konu, ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="ce1f6-107">Örneğin, bir genel yönetici tarafından hata hello hizmet hesabının PowerShell kullanarak hello parola sıfırlama varsa.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="ce1f6-108">Merhaba kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="ce1f6-108">Reset hello credentials</span></span>
<span data-ttu-id="ce1f6-109">Hello Azure AD Bağlayıcısı üzerinde tanımlı hello hizmet hesabı Azure AD tooauthentication sorunlar nedeniyle iletişim kuramazsa, hello parolanızı sıfırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="ce1f6-110">Toohello Azure AD Connect eşitleme sunucusunda oturum açın ve PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="ce1f6-111">`Add-ADSyncAADServiceAccount` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="ce1f6-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="ce1f6-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="ce1f6-113">Azure AD genel yönetici kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="ce1f6-114">Bu cmdlet hello hello hizmeti hesabının parolasını sıfırlar ve Azure AD hem de hello eşitleme altyapısı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="ce1f6-115">Bu adımları çözebilir bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="ce1f6-115">Known issues these steps can solve</span></span>
<span data-ttu-id="ce1f6-116">Bu bölümde, Azure AD hizmet hesabı hello üzerinde sıfırlama kimlik bilgileri tarafından düzeltilen müşteriler tarafından bildirilen hataları listesidir.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="ce1f6-117">Olay 6900</span><span class="sxs-lookup"><span data-stu-id="ce1f6-117">Event 6900</span></span>  
<span data-ttu-id="ce1f6-118">Merhaba sunucu, bir parola değişikliği bildirimi işlenirken beklenmeyen bir hatayla karşılaştı:</span><span class="sxs-lookup"><span data-stu-id="ce1f6-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="ce1f6-119">AADSTS70002: Hata doğrulama kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="ce1f6-120">AADSTS50054: Eski parola kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="ce1f6-121">Olay 659</span><span class="sxs-lookup"><span data-stu-id="ce1f6-121">Event 659</span></span>  
<span data-ttu-id="ce1f6-122">Parola İlkesi eşitleme yapılandırması alınırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="ce1f6-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="ce1f6-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="ce1f6-124">AADSTS70002: Hata doğrulama kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="ce1f6-125">AADSTS50054: Eski parola kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ce1f6-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce1f6-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ce1f6-126">Next steps</span></span>
<span data-ttu-id="ce1f6-127">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="ce1f6-127">**Overview topics**</span></span>

* [<span data-ttu-id="ce1f6-128">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="ce1f6-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="ce1f6-129">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="ce1f6-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

