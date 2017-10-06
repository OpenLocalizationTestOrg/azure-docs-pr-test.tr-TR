---
title: "Azure Active Directory etki alanı Hizmetleri: SharePoint kullanıcı profili hizmeti için desteği etkinleştirme | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri yönetilen etki alanlarını toosupport profil eşitleme SharePoint sunucusu için yapılandırma"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="a856d-103">Yönetilen etki alanı toosupport profil eşitleme SharePoint sunucusu için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a856d-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="a856d-104">SharePoint Server kullanıcı profili eşitleme için kullanılan bir kullanıcı profili hizmeti içerir.</span><span class="sxs-lookup"><span data-stu-id="a856d-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="a856d-105">tooset hello kullanıcı profili hizmeti oluşturan bir Active Directory etki alanında verilen toobe uygun izinlerinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a856d-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="a856d-106">Daha fazla bilgi için bkz: [SharePoint Server 2013'te profil eşitleme için Active Directory etki alanı Hizmetleri izinleri](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="a856d-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="a856d-107">Bu makalede, Azure AD etki alanı Hizmetleri yönetilen etki alanlarını toodeploy hello SharePoint Server kullanıcı profili eşitleme hizmeti nasıl yapılandırabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a856d-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="a856d-108">Merhaba 'AAD DC hizmet hesapları' grubu</span><span class="sxs-lookup"><span data-stu-id="a856d-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="a856d-109">Bir güvenlik grubu olarak adlandırılan '**AAD DC hizmet hesaplarını**' hello 'Kullanıcılar' kuruluş birimi, yönetilen etki alanınızda içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a856d-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="a856d-110">Bu gruptaki hello görebilirsiniz **Active Directory Kullanıcıları ve Bilgisayarları** MMC ek bileşenini, yönetilen etki alanınızda.</span><span class="sxs-lookup"><span data-stu-id="a856d-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![AAD DC hizmet hesaplarını güvenlik grubu](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="a856d-112">Bu güvenlik grubunun üyeleri ayrıcalıkları aşağıdaki temsilci hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a856d-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="a856d-113">Merhaba 'Dizin değişiklikleri Çoğalt' ayrıcalık hello kök DSE Merhaba, etki alanı yönetilen.</span><span class="sxs-lookup"><span data-stu-id="a856d-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="a856d-114">Merhaba hello yapılandırma adlandırma bağlamında 'Dizin değişiklikleri Çoğalt' ayrıcalığı (cn = yapılandırma kapsayıcısı) Merhaba yönetilen etki alanı.</span><span class="sxs-lookup"><span data-stu-id="a856d-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="a856d-115">Bu güvenlik grubunu ayrıca hello yerleşik grubunun bir üyesi olan **Pre-Windows 2000 Compatible Access**.</span><span class="sxs-lookup"><span data-stu-id="a856d-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![AAD DC hizmet hesaplarını güvenlik grubu](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="a856d-117">Yönetilen etki alanı toosupport SharePoint Server kullanıcı profili eşitleme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a856d-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="a856d-118">SharePoint kullanıcı profili eşitleme toohello için kullanılan hello hizmet hesabı ekleyebilirsiniz **AAD DC hizmet hesaplarını** grubu.</span><span class="sxs-lookup"><span data-stu-id="a856d-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="a856d-119">Sonuç olarak, yeterli ayrıcalıkları tooreplicate değişiklikleri toohello dizin hello eşitleme hesabı alır.</span><span class="sxs-lookup"><span data-stu-id="a856d-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="a856d-120">Bu yapılandırma adımı, SharePoint Server kullanıcı profili eşitleme toowork doğru sağlar.</span><span class="sxs-lookup"><span data-stu-id="a856d-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![AAD DC hizmet hesapları - üyeleri Ekle](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC hizmet hesapları - üyeleri Ekle](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="a856d-123">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="a856d-123">Related Content</span></span>
* [<span data-ttu-id="a856d-124">Teknik başvuru - SharePoint Server 2013'te profil eşitleme izinlerini verin Active Directory etki alanı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a856d-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
