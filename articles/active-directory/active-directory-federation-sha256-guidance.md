---
title: "Office 365 bağlı olan taraf güveni için aaaChange imza karma algoritmasını | Microsoft Docs"
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
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="b05b9-104">Office 365 bağlı olan taraf güveni için imza karma algoritması değiştirme</span><span class="sxs-lookup"><span data-stu-id="b05b9-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="b05b9-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b05b9-105">Overview</span></span>
<span data-ttu-id="b05b9-106">Active Directory Federasyon Hizmetleri (AD FS) ile değiştirilmemesi kendi belirteçleri tooMicrosoft Azure Active Directory tooensure imzalar.</span><span class="sxs-lookup"><span data-stu-id="b05b9-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="b05b9-107">Bu imza SHA1 veya SHA256 dayalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b05b9-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="b05b9-108">Azure Active Directory şimdi SHA256 algoritmasını ile imzalanmış belirteçleri destekler ve hello belirteç imzalama algoritması tooSHA256 hello yüksek düzeyde güvenlik için ayarlanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="b05b9-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="b05b9-109">Bu makalede, tooset hello belirteç imzalama algoritması toohello SHA256 düzeyi daha güvenli hello adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b05b9-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="b05b9-110">Microsoft, SHA1'den daha güvenlidir, ancak desteklenen bir seçenek SHA1 kalıyor gibi Belirteçleri imzalamak için hello algoritması olarak SHA256 kullanımını önerir.</span><span class="sxs-lookup"><span data-stu-id="b05b9-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="b05b9-111">Değişiklik hello belirteç imzalama algoritması</span><span class="sxs-lookup"><span data-stu-id="b05b9-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="b05b9-112">Merhaba imza algoritması hello iki işlem aşağıdaki biriyle ayarladıktan sonra AD FS bağlı olan taraf güveni SHA256 ile Office 365 için hello belirteçlerini imzalar.</span><span class="sxs-lookup"><span data-stu-id="b05b9-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="b05b9-113">Ek yapılandırma değişiklikleri toomake gerekmez ve bu değişiklik, özelliği tooaccess Office 365 veya diğer Azure AD uygulamaları herhangi bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="b05b9-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="b05b9-114">AD FS Yönetim Konsolu</span><span class="sxs-lookup"><span data-stu-id="b05b9-114">AD FS management console</span></span>
1. <span data-ttu-id="b05b9-115">Merhaba birincil AD FS sunucusunda Hello AD FS Yönetim Konsolu'nu açın.</span><span class="sxs-lookup"><span data-stu-id="b05b9-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="b05b9-116">Merhaba AD FS düğümünü genişletin ve tıklatın **bağlı olan taraf güvenleri**.</span><span class="sxs-lookup"><span data-stu-id="b05b9-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="b05b9-117">Office 365/Azure bağlı olan taraf güveniniz sağ tıklatıp **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="b05b9-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="b05b9-118">Select hello **Gelişmiş** sekmesi ve select hello güvenli karma algoritması SHA256.</span><span class="sxs-lookup"><span data-stu-id="b05b9-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="b05b9-119">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b05b9-119">Click **OK**.</span></span>

![SHA256 imzalama algoritmasını--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="b05b9-121">AD FS PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="b05b9-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="b05b9-122">Herhangi bir AD FS sunucusu üzerinde PowerShell'i yönetici ayrıcalıklarıyla açın.</span><span class="sxs-lookup"><span data-stu-id="b05b9-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="b05b9-123">Set hello güvenli karma algoritması'hello kullanarak **Set-AdfsRelyingPartyTrust** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="b05b9-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="b05b9-124">Ayrıca okuyun</span><span class="sxs-lookup"><span data-stu-id="b05b9-124">Also read</span></span>
* [<span data-ttu-id="b05b9-125">Azure AD Connect ile Office 365 güven onarın</span><span class="sxs-lookup"><span data-stu-id="b05b9-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

