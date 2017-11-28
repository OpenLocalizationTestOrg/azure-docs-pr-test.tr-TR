---
title: "Azure AD Connect eşitleme: AD Geri Dönüşüm Kutusu'nu etkinleştirme | Microsoft Docs"
description: "Bu konuda, Azure AD Connect ile AD geri dönüşüm kutusu özelliğinin hello kullan önerir."
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
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="61f14-104">Azure AD Connect eşitleme: AD Geri Dönüşüm Kutusu'nu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="61f14-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="61f14-105">Hello AD Geri Dönüşüm Kutusu özelliği, şirket içi Active eşitlenmiş tooAzure AD olan dizinleri için etkinleştirmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="61f14-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="61f14-106">Şirket içi yanlışlıkla sildiyseniz AD kullanıcı nesnesi ve geri yükleme, hello özelliğini kullanarak, Azure AD yükler hello karşılık gelen Azure AD kullanıcı nesnesi.</span><span class="sxs-lookup"><span data-stu-id="61f14-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="61f14-107">Merhaba AD Geri Dönüşüm Kutusu özelliği hakkında daha fazla bilgi için tooarticle başvurun [senaryoya genel bakış geri silinmiş Active Directory nesneleri için](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="61f14-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="61f14-108">Merhaba AD etkinleştirme avantajları geri dönüşüm kutusu</span><span class="sxs-lookup"><span data-stu-id="61f14-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="61f14-109">Bu özellik hello aşağıdakileri yaparak Azure AD kullanıcı nesneleri geri yüklemeye yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="61f14-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="61f14-110">Şirket içi yanlışlıkla sildiyseniz AD kullanıcı nesnesi, hello karşılık gelen Azure AD kullanıcı nesnesi silinecek hello sonraki eşitleme döngüsü.</span><span class="sxs-lookup"><span data-stu-id="61f14-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="61f14-111">Varsayılan olarak, Azure AD silinmiş hello Azure AD kullanıcı nesnesi 30 gün boyunca geçici olarak silinen durumda tutar.</span><span class="sxs-lookup"><span data-stu-id="61f14-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="61f14-112">Şirket içi varsa AD Geri Dönüşüm Kutusu özelliği, etkin geri yükleyebilir, silinen hello AD Kullanıcı nesnesinin kaynak bağlantısı değerini değiştirmeden şirket.</span><span class="sxs-lookup"><span data-stu-id="61f14-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="61f14-113">Ne zaman hello kurtarılan şirket içi AD kullanıcı nesnesi eşitlenir tooAzure AD, Azure AD geri geçici olarak silinen hello karşılık gelen Azure AD kullanıcı nesnesi.</span><span class="sxs-lookup"><span data-stu-id="61f14-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="61f14-114">Kaynak bağlantısı özniteliği hakkında daha fazla bilgi için tooarticle başvurun [Azure AD Connect: tasarım kavramları](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="61f14-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="61f14-115">Şirket içi yoksa AD Geri Dönüşüm Kutusu'nu özelliği etkinleştirilmiş, gerekli toocreate bir AD kullanıcı nesnesi tooreplace hello Silinmiş nesne olabilir.</span><span class="sxs-lookup"><span data-stu-id="61f14-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="61f14-116">Azure AD Connect eşitleme hizmetinin yapılandırılmış toouse sistem tarafından oluşturulan AD özniteliği (örneğin, objectGUID) hello kaynak bağlantısı özniteliği için ise, hello yeni oluşturulan AD kullanıcı nesnesi değil sahip hello aynı kaynak bağlantısı değeri hello AD kullanıcı nesnesi silindi olarak.</span><span class="sxs-lookup"><span data-stu-id="61f14-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="61f14-117">Azure AD Hello yeni oluşturulan AD kullanıcı nesnesi eşitlenmiş tooAzure AD olduğunda, yeni bir oluşturur geçici olarak silinen hello Azure AD kullanıcı nesnesi geri yerine Azure AD kullanıcı nesnesi.</span><span class="sxs-lookup"><span data-stu-id="61f14-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="61f14-118">Varsayılan olarak, Azure AD tutar geçici olarak silinen durumdaki Azure AD kullanıcı nesneler tamamen silinmeden önce 30 gün boyunca silindi.</span><span class="sxs-lookup"><span data-stu-id="61f14-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="61f14-119">Bununla birlikte, Yöneticiler bu tür nesneleri hello silinmesini hızlandırabilir.</span><span class="sxs-lookup"><span data-stu-id="61f14-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="61f14-120">Merhaba nesneler kalıcı olarak silinir sonra artık kurtarılabilir, bile içi bağlı AD Geri Dönüşüm Kutusu özelliği etkin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="61f14-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="61f14-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="61f14-121">Next steps</span></span>
<span data-ttu-id="61f14-122">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="61f14-122">**Overview topics**</span></span>

* [<span data-ttu-id="61f14-123">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="61f14-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="61f14-124">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="61f14-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
