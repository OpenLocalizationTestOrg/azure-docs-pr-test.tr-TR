---
title: "Office 365 bağlı olan taraf güveni için değişiklik imza karma algoritmasını | Microsoft Docs"
description: "Bu sayfa, Office 365 ile bir federasyon güveni için SHA algoritma değiştirmek için yönergeler sağlar"
keywords: "SHA1, SHA256, O365, Federasyon, aadconnect, adfs, ad fs, değişiklik sha, bağlı olan taraf güveni bir federasyon güveni"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="18b99-104">Office 365 bağlı olan taraf güveni için imza karma algoritması değiştirme</span><span class="sxs-lookup"><span data-stu-id="18b99-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="18b99-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="18b99-105">Overview</span></span>
<span data-ttu-id="18b99-106">Active Directory Federasyon Hizmetleri (AD FS) Microsoft Azure Active Directory'ye bunlar ile değiştirilmemesi emin olmak için belirteçlerini imzalar.</span><span class="sxs-lookup"><span data-stu-id="18b99-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="18b99-107">Bu imza SHA1 veya SHA256 dayalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="18b99-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="18b99-108">Azure Active Directory şimdi SHA256 algoritmasını ile imzalanmış belirteçleri destekler ve belirteç imzalama algoritması yüksek düzeyde güvenlik için SHA256 ayarlanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="18b99-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="18b99-109">Bu makalede daha güvenli SHA256 belirteç imzalama algoritması düzeyi ayarlamak için gereken adımlar açıklanır.</span><span class="sxs-lookup"><span data-stu-id="18b99-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="18b99-110">Microsoft, SHA1'den daha güvenlidir, ancak desteklenen bir seçenek SHA1 kalıyor belirteç imzalama algoritması olarak SHA256 kullanımını önerir.</span><span class="sxs-lookup"><span data-stu-id="18b99-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="18b99-111">Belirteç imzalama algoritması değiştirme</span><span class="sxs-lookup"><span data-stu-id="18b99-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="18b99-112">Aşağıdaki iki işlemlerden biri ile imza algoritması ayarladıktan sonra AD FS belirteçleri Office 365 bağlı olan taraf güveni SHA256 ile imzalar.</span><span class="sxs-lookup"><span data-stu-id="18b99-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="18b99-113">Ek yapılandırma değişiklikleri yapmanıza gerek yoktur ve bu değişiklik, Office 365 veya diğer Azure AD uygulamalarına erişmek için yeteneğinizi üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="18b99-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="18b99-114">AD FS Yönetim Konsolu</span><span class="sxs-lookup"><span data-stu-id="18b99-114">AD FS management console</span></span>
1. <span data-ttu-id="18b99-115">Birincil AD FS sunucusunda AD FS Yönetimi konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="18b99-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="18b99-116">AD FS düğümünü genişletin ve tıklatın **bağlı olan taraf güvenleri**.</span><span class="sxs-lookup"><span data-stu-id="18b99-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="18b99-117">Office 365/Azure bağlı olan taraf güveniniz sağ tıklatıp **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="18b99-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="18b99-118">Seçin **Gelişmiş** sekmesinde ve güvenli karma algoritması SHA256 seçin.</span><span class="sxs-lookup"><span data-stu-id="18b99-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="18b99-119">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="18b99-119">Click **OK**.</span></span>

![SHA256 imzalama algoritmasını--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="18b99-121">AD FS PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="18b99-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="18b99-122">Herhangi bir AD FS sunucusu üzerinde PowerShell'i yönetici ayrıcalıklarıyla açın.</span><span class="sxs-lookup"><span data-stu-id="18b99-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="18b99-123">Güvenli karma algoritmasını kullanarak ayarlamak **Set-AdfsRelyingPartyTrust** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="18b99-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="18b99-124">Ayrıca okuyun</span><span class="sxs-lookup"><span data-stu-id="18b99-124">Also read</span></span>
* [<span data-ttu-id="18b99-125">Azure AD Connect ile Office 365 güven onarın</span><span class="sxs-lookup"><span data-stu-id="18b99-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

