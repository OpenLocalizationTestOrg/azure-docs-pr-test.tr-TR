---
title: "aaaTwo adım doğrulama ve AD FS - Azure MFA | Microsoft Docs"
description: "Bu tooget Azure MFA ve AD FS ile çalışmaya nasıl açıklayan hello Azure multi-Factor authentication sayfasıdır."
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
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="d4c73-103">Azure Multi-Factor Authentication ve Active Directory Federasyon Hizmetlerini kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d4c73-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="d4c73-104"><center>![Bulut](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="d4c73-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="d4c73-105">Kuruluşunuz şirket için Active Directory’nizi AD FS kullanan Azure Active Directory ile birleştirdiyse Azure Multi-Factor Authentication’ın kullanılması için iki seçenek mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="d4c73-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="d4c73-106">Azure Multi-Factor Authentication veya Active Directory Federasyon Hizmetleri’ni kullanarak bulut kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="d4c73-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="d4c73-107">Azure Multi-Factor Authentication Sunucusu kullanarak bulut ve şirket içi kaynakları güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="d4c73-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="d4c73-108">Aşağıdaki tablonun hello kaynaklarını Azure multi-Factor Authentication ve AD FS ile güvenli hale getirme arasında hello doğrulama deneyimi özetlenmiştir</span><span class="sxs-lookup"><span data-stu-id="d4c73-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="d4c73-109">Doğrulama Deneyimi - Tarayıcı Tabanlı Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d4c73-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="d4c73-110">Doğrulama Deneyimi - Tarayıcı Tabanlı Olmayan Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d4c73-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4c73-111">Azure AD’yi Azure Multi-Factor Authentication kullanarak güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="d4c73-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="d4c73-112">Merhaba ilk doğrulama adımı gerçekleştirilir şirket içi AD FS kullanma.</span><span class="sxs-lookup"><span data-stu-id="d4c73-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="d4c73-113">Merhaba ikinci adım bulut kimlik doğrulaması kullanarak yapılan bir telefon tabanlı yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="d4c73-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="d4c73-114">Active Directory Federasyon Hizmetleri’ni kullanarak Azure AD kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="d4c73-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="d4c73-115">Merhaba ilk doğrulama adımı gerçekleştirilir şirket içi AD FS kullanma.</span><span class="sxs-lookup"><span data-stu-id="d4c73-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="d4c73-116">Merhaba ikinci adım, hello talebi onaylanmasıyla şirket içi gerçekleştirilir bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d4c73-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="d4c73-117">Federasyon kullanıcıları için uygulama parolaları ile ilgili uyarılar:</span><span class="sxs-lookup"><span data-stu-id="d4c73-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="d4c73-118">Uygulama parolaları, bulut kimlik doğrulaması kullanılarak doğrulanır ve bu nedenle federasyonu atlar.</span><span class="sxs-lookup"><span data-stu-id="d4c73-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="d4c73-119">Federasyon, yalnızca uygulama parolası ayarlanırken etkin şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4c73-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="d4c73-120">Şirket içi İstemci Erişim Denetimi ayarları, uygulama parolaları tarafından onaylanmaz.</span><span class="sxs-lookup"><span data-stu-id="d4c73-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="d4c73-121">Uygulama parolaları için şirket içi kimlik doğrulaması günlüğe kaydetme özelliğini kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="d4c73-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="d4c73-122">Hesap devre dışı bırakma/silme, devre dışı bırakma/silme, uygulama parolaları hello bulut kimliği olarak geciktirme dizin eşitleme için toothree saatlerini sürebilir.</span><span class="sxs-lookup"><span data-stu-id="d4c73-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4c73-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d4c73-123">Next steps</span></span>
<span data-ttu-id="d4c73-124">Azure çok faktörlü kimlik doğrulaması veya hello AD FS ile Azure multi-Factor Authentication sunucusu kurma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="d4c73-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="d4c73-125">Azure Multi-Factor Authentication ve AD FS kullanarak bulut kaynaklarını güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="d4c73-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="d4c73-126">Windows Server 2012 R2 AD FS ile Azure Multi-Factor Authentication Sunucusu kullanarak bulut ve şirket içi kaynakları güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="d4c73-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="d4c73-127">AD FS 2.0 ile Azure Multi-Factor Authentication Sunucusu kullanarak bulut ve şirket içi kaynakları güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="d4c73-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
