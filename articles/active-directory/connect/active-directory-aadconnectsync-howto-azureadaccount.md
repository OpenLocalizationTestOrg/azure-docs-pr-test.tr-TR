---
title: "Azure AD Connect eşitleme: Azure AD hizmet hesabı yönetme | Microsoft Docs"
description: "Bu konuda Azure AD hizmet hesabını geri yüklemek nasıl belgelenir."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, Azure AD Connect eşitleme Connector hizmet hesabı parolasını sıfırlama"
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
ms.openlocfilehash: 8e9e8192ee4fcb636b5be91d2616acbc9120c8c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="333f7-104">Azure AD Connect eşitleme: Azure AD hizmet hesabı yönetme</span><span class="sxs-lookup"><span data-stu-id="333f7-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="333f7-105">Azure AD Bağlayıcısı tarafından kullanılan hizmet hesabını hizmeti boş olması beklenir.</span><span class="sxs-lookup"><span data-stu-id="333f7-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="333f7-106">Kimlik bilgilerini sıfırlamanız gerekirse, bu konu, ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="333f7-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="333f7-107">Örneğin, bir genel yönetici yanlışlıkla varsa PowerShell kullanarak hizmet hesabı parolasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="333f7-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="333f7-108">Kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="333f7-108">Reset the credentials</span></span>
<span data-ttu-id="333f7-109">Azure AD Bağlayıcısı üzerinde tanımlı hizmet hesabı Azure AD kimlik doğrulama sorunları nedeniyle bağlantı kuramıyorsa, parolayı sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="333f7-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="333f7-110">Azure AD Connect eşitleme sunucusunda oturum açın ve PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="333f7-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="333f7-111">`Add-ADSyncAADServiceAccount` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="333f7-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="333f7-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="333f7-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="333f7-113">Azure AD genel yönetici kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="333f7-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="333f7-114">Bu cmdlet, hizmet hesabı parolasını sıfırlar ve Azure AD hem de eşitleme altyapısı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="333f7-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="333f7-115">Bu adımları çözebilir bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="333f7-115">Known issues these steps can solve</span></span>
<span data-ttu-id="333f7-116">Bu bölümde, sıfırlama Azure AD hizmeti hesabı kimlik bilgileri tarafından düzeltilen müşteriler tarafından bildirilen hataları listesidir.</span><span class="sxs-lookup"><span data-stu-id="333f7-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="333f7-117">Olay 6900</span><span class="sxs-lookup"><span data-stu-id="333f7-117">Event 6900</span></span>  
<span data-ttu-id="333f7-118">Sunucu, bir parola değişikliği bildirimi işlenirken beklenmeyen bir hatayla karşılaştı:</span><span class="sxs-lookup"><span data-stu-id="333f7-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="333f7-119">AADSTS70002: Hata doğrulama kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="333f7-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="333f7-120">AADSTS50054: Eski parola kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="333f7-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="333f7-121">Olay 659</span><span class="sxs-lookup"><span data-stu-id="333f7-121">Event 659</span></span>  
<span data-ttu-id="333f7-122">Parola İlkesi eşitleme yapılandırması alınırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="333f7-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="333f7-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="333f7-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="333f7-124">AADSTS70002: Hata doğrulama kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="333f7-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="333f7-125">AADSTS50054: Eski parola kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="333f7-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="333f7-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="333f7-126">Next steps</span></span>
<span data-ttu-id="333f7-127">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="333f7-127">**Overview topics**</span></span>

* [<span data-ttu-id="333f7-128">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="333f7-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="333f7-129">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="333f7-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

