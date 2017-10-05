---
title: "Azure AD Connect eşitleme: AD Geri Dönüşüm Kutusu'nu etkinleştirme | Microsoft Docs"
description: "Bu konuda, Azure AD Connect ile AD geri dönüşüm kutusu özelliğinin kullanımına önerir."
services: active-directory
keywords: "AD geri dönüşüm kutusu, yanlışlıkla silinmesi, kaynak bağlantısı"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: eb455477547f3db8245cf3601576eba9c6fdc56f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="6f3f8-104">Azure AD Connect eşitleme: AD Geri Dönüşüm Kutusu'nu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6f3f8-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="6f3f8-105">Şirket içi Active hangi Azure AD ile eşitlenir dizinlerinizi için AD geri dönüşüm kutusu özelliğini etkinleştirmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span></span> 

<span data-ttu-id="6f3f8-106">Şirket içi yanlışlıkla sildiyseniz AD kullanıcı nesnesi ve bu özelliği kullanarak, Azure AD yükler karşılık gelen Azure AD kullanıcı nesnesini geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span></span>  <span data-ttu-id="6f3f8-107">AD Geri Dönüşüm Kutusu özelliği hakkında daha fazla bilgi için makalesine başvurun [senaryoya genel bakış geri silinmiş Active Directory nesneleri için](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f3f8-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-the-ad-recycle-bin"></a><span data-ttu-id="6f3f8-108">AD Geri Dönüşüm Kutusu'nu etkinleştirme avantajları</span><span class="sxs-lookup"><span data-stu-id="6f3f8-108">Benefits of enabling the AD recycle bin</span></span>
<span data-ttu-id="6f3f8-109">Bu özellik, aşağıdakileri yaparak Azure AD kullanıcı nesneleri geri yüklemeye yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="6f3f8-109">This feature helps with restoring Azure AD user objects by doing the following:</span></span>

* <span data-ttu-id="6f3f8-110">Şirket içi yanlışlıkla sildiyseniz AD kullanıcı nesnesi, ilgili Azure AD kullanıcı nesnesi sonraki eşitleme döngüsünde silinecek.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span></span> <span data-ttu-id="6f3f8-111">Varsayılan olarak, Azure AD silinen tutan Azure AD kullanıcı nesnesi 30 gün için geçici olarak silinen durumda.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="6f3f8-112">Şirket içi varsa AD Geri Dönüşüm Kutusu'nu özelliğinin etkin, silinen geri AD Kullanıcı nesnesinin kaynak bağlantısı değerini değiştirmeden şirket.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="6f3f8-113">Zaman kurtarılan şirket içi AD kullanıcı nesnesi Azure AD ile eşitlenir, Azure AD olacak geri yükleme karşılık gelen geçici olarak silinen Azure AD kullanıcı nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="6f3f8-114">Kaynak bağlantısı özniteliği hakkında daha fazla bilgi için makalesine başvurun [Azure AD Connect: tasarım kavramları](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="6f3f8-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="6f3f8-115">Şirket içi yoksa AD Geri Dönüşüm Kutusu özelliği, etkin olabilir Silinmiş nesne değiştirmek için bir AD kullanıcı nesnesi oluşturmak için gerekli.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span></span> <span data-ttu-id="6f3f8-116">Azure AD Connect eşitleme hizmeti için kaynak bağlantısı öznitelik sistem tarafından oluşturulan AD özniteliği (örneğin, objectGUID) kullanmak için yapılandırılmışsa, yeni oluşturulan AD kullanıcı nesnesi silinen AD kullanıcı nesnesi ile aynı kaynak bağlantısı değere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span></span> <span data-ttu-id="6f3f8-117">Yeni oluşturulan AD kullanıcı nesnesi için Azure AD eşitlendiğinde, Azure AD yeni bir oluşturur geçici olarak silinen geri yerine Azure AD kullanıcı nesnesi Azure AD kullanıcı nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="6f3f8-118">Varsayılan olarak, Azure AD tutar geçici olarak silinen durumdaki Azure AD kullanıcı nesneler tamamen silinmeden önce 30 gün boyunca silindi.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="6f3f8-119">Bununla birlikte, Yöneticiler bu tür nesneleri silme işlemini hızlandırabilir.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-119">However, administrators can accelerate the deletion of such objects.</span></span> <span data-ttu-id="6f3f8-120">Nesneleri kalıcı olarak silinir sonra artık kurtarılabilir, bile içi bağlı AD Geri Dönüşüm Kutusu özelliği etkin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="6f3f8-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6f3f8-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6f3f8-121">Next steps</span></span>
<span data-ttu-id="6f3f8-122">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="6f3f8-122">**Overview topics**</span></span>

* [<span data-ttu-id="6f3f8-123">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="6f3f8-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="6f3f8-124">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="6f3f8-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
