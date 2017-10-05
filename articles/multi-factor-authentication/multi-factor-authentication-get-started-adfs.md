---
title: "İki aşamalı doğrulama ve AD FS - Azure MFA | Microsoft Docs"
description: "Bu, nasıl Azure MFA ve AD FS kullanmaya başlayacağınızı açıklayan Azure Multi-Factor Authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 28aede545c738137ff04257214e4a3f42792d85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="9c05f-103">Azure Multi-Factor Authentication ve Active Directory Federasyon Hizmetlerini kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9c05f-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="9c05f-104"><center>![Bulut](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="9c05f-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="9c05f-105">Kuruluşunuz şirket için Active Directory’nizi AD FS kullanan Azure Active Directory ile birleştirdiyse Azure Multi-Factor Authentication’ın kullanılması için iki seçenek mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="9c05f-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="9c05f-106">Azure Multi-Factor Authentication veya Active Directory Federasyon Hizmetleri’ni kullanarak bulut kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="9c05f-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="9c05f-107">Azure Multi-Factor Authentication Sunucusu kullanarak bulut ve şirket içi kaynakları güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="9c05f-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="9c05f-108">Aşağıdaki tabloda, kaynakların Azure Multi-Factor Authentication ve AD FS ile güvenliğini sağlama arasındaki doğrulama deneyimi özetlenmiştir</span><span class="sxs-lookup"><span data-stu-id="9c05f-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="9c05f-109">Doğrulama Deneyimi - Tarayıcı Tabanlı Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="9c05f-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="9c05f-110">Doğrulama Deneyimi - Tarayıcı Tabanlı Olmayan Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="9c05f-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9c05f-111">Azure AD’yi Azure Multi-Factor Authentication kullanarak güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="9c05f-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="9c05f-112">İlk doğrulama adımı, AD FS kullanılarak şirket içinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9c05f-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="9c05f-113">İkinci adım, bulut kimlik doğrulaması kullanılarak yapılan telefon tabanlı yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="9c05f-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="9c05f-114">Active Directory Federasyon Hizmetleri’ni kullanarak Azure AD kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="9c05f-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="9c05f-115">İlk doğrulama adımı, AD FS kullanılarak şirket içinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9c05f-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="9c05f-116">İkinci adım, talebin onaylanmasıyla şirket içinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9c05f-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="9c05f-117">Federasyon kullanıcıları için uygulama parolaları ile ilgili uyarılar:</span><span class="sxs-lookup"><span data-stu-id="9c05f-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="9c05f-118">Uygulama parolaları, bulut kimlik doğrulaması kullanılarak doğrulanır ve bu nedenle federasyonu atlar.</span><span class="sxs-lookup"><span data-stu-id="9c05f-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="9c05f-119">Federasyon, yalnızca uygulama parolası ayarlanırken etkin şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9c05f-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="9c05f-120">Şirket içi İstemci Erişim Denetimi ayarları, uygulama parolaları tarafından onaylanmaz.</span><span class="sxs-lookup"><span data-stu-id="9c05f-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="9c05f-121">Uygulama parolaları için şirket içi kimlik doğrulaması günlüğe kaydetme özelliğini kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="9c05f-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="9c05f-122">Hesabı devre dışı bırakma/silme işlemi, bulut kimliğinde dizin eşitlemesi ve uygulama parolalarının devre dışı bırakılması/silinmesi nedeniyle üç saate kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9c05f-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c05f-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c05f-123">Next steps</span></span>
<span data-ttu-id="9c05f-124">Azure Multi-Factor Authentication ya da AD FS ile Azure Multi-Factor Authentication Sunucusu kurulumu hakkında bilgi edinmek için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="9c05f-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="9c05f-125">Azure Multi-Factor Authentication ve AD FS kullanarak bulut kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="9c05f-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="9c05f-126">Windows Server 2012 R2 AD FS ile Azure Multi-Factor Authentication Sunucusu kullanarak bulut ve şirket içi kaynakları güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="9c05f-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="9c05f-127">AD FS 2.0 ile Azure Multi-Factor Authentication Sunucusu kullanarak bulut ve şirket içi kaynakları güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="9c05f-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
