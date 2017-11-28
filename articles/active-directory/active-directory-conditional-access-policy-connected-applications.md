---
title: "aaaConfigure Azure Active Directory cihaz temelli koşullu erişim ilkeleri | Microsoft Docs"
description: "Nasıl tooconfigure Azure Active Directory cihaz temelli koşullu erişim ilkeleri hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="680c6-103">Azure Active Directory cihaz temelli koşullu erişim ilkelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="680c6-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="680c6-104">İle [Azure Active Directory (Azure AD) koşullu erişim](active-directory-conditional-access-azure-portal.md), ince ayar yapabilirsiniz nasıl yetkili kullanıcılar, kaynaklara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="680c6-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="680c6-105">Örneğin, hello erişim toocertain kaynakları tootrusted aygıtları sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="680c6-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="680c6-106">Güvenilir bir aygıt gerektiren bir koşullu erişim ilkesi cihaz temelli koşullu erişim ilkesi de denir.</span><span class="sxs-lookup"><span data-stu-id="680c6-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="680c6-107">Bu konu, nasıl tooconfigure cihaz temelli koşullu erişim ilkeleri Azure AD bağlı uygulamalar için bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="680c6-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="680c6-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="680c6-108">Before you begin</span></span>

<span data-ttu-id="680c6-109">Cihaz temelli koşullu erişim TIES **Azure AD koşullu erişimi** ve **Azure AD cihaz Yönetimi birlikte**.</span><span class="sxs-lookup"><span data-stu-id="680c6-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="680c6-110">Bu alanlardan biri ile tanıdık değilse, aşağıdaki konularda, ilk hello şöyle olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="680c6-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="680c6-111">**[Azure Active Directory'de koşullu erişim](active-directory-conditional-access-azure-portal.md)**  -Bu konu, koşullu kavramsal genel bakış ile erişmek ve hello ilgili terminolojiyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="680c6-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="680c6-112">**[Giriş toodevice Yönetimi Azure Active Directory'de](device-management-introduction.md)**  -Bu konu genel bir fikir veren Merhaba Azure AD ile tooconnect aygıtları sahip çeşitli seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="680c6-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="680c6-113">Güvenilen cihazlar</span><span class="sxs-lookup"><span data-stu-id="680c6-113">Trusted devices</span></span>

<span data-ttu-id="680c6-114">Bir mobil ilk olarak, bulut ilk dünyasında, Azure Active Directory oturum açma tek toodevices, uygulama ve hizmetlere her yerden sağlar.</span><span class="sxs-lookup"><span data-stu-id="680c6-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="680c6-115">Belirli toohello doğru kullanıcılar erişim verilmesi, ortamınızdaki kaynakları iyi yeterli olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="680c6-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="680c6-116">Ayrıca toohello doğru kullanıcılar, aynı zamanda güvenilir cihaz toobe tooaccess kaynak kullanılan gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="680c6-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="680c6-117">Ortamınızda, güvenilir bir aygıt, dayanır tanımlayabilirsiniz hello bileşenleri:</span><span class="sxs-lookup"><span data-stu-id="680c6-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="680c6-118">Merhaba [cihaz platformları](active-directory-conditional-access-azure-portal.md#device-platforms) bir cihazda</span><span class="sxs-lookup"><span data-stu-id="680c6-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="680c6-119">Bir cihazın uyumlu olup</span><span class="sxs-lookup"><span data-stu-id="680c6-119">Whether a device is compliant</span></span>
- <span data-ttu-id="680c6-120">Bir cihaz etki alanına katılmış olup olmadığı</span><span class="sxs-lookup"><span data-stu-id="680c6-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="680c6-121">Merhaba [cihaz platformları](active-directory-conditional-access-azure-portal.md#device-platforms) , cihazda çalışan hello işletim sistemi tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="680c6-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="680c6-122">Cihaz temelli koşullu erişim ilkenizi erişim toocertain kaynakları toospecific cihaz platformları sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="680c6-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="680c6-123">Bir cihaz temelli koşullu erişim ilkesinde uyumlu olarak işaretlenmiş güvenilen cihazlar toobe gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="680c6-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![Bulut uygulamaları](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="680c6-125">Cihazların Merhaba dizininde tarafından uyumlu olarak işaretlenebilir:</span><span class="sxs-lookup"><span data-stu-id="680c6-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="680c6-126">Intune</span><span class="sxs-lookup"><span data-stu-id="680c6-126">Intune</span></span> 
- <span data-ttu-id="680c6-127">Azure AD ile tümleşen bir üçüncü taraf mobil cihaz yönetim sistemi</span><span class="sxs-lookup"><span data-stu-id="680c6-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="680c6-128">Bağlı tooAzure AD yalnızca cihazlar uyumlu olarak işaretlenebilir.</span><span class="sxs-lookup"><span data-stu-id="680c6-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="680c6-129">tooconnect aygıt tooAzure Active Directory, aşağıdaki seçenekleri şu hello vardır:</span><span class="sxs-lookup"><span data-stu-id="680c6-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="680c6-130">Azure AD kayıtlı</span><span class="sxs-lookup"><span data-stu-id="680c6-130">Azure AD registered</span></span>
- <span data-ttu-id="680c6-131">Azure AD alanına katılmış</span><span class="sxs-lookup"><span data-stu-id="680c6-131">Azure AD joined</span></span>
- <span data-ttu-id="680c6-132">Karma Azure AD alanına katılmış</span><span class="sxs-lookup"><span data-stu-id="680c6-132">Hybrid Azure AD joined</span></span>

    ![Bulut uygulamaları](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="680c6-134">Bir şirket içi Active Directory (AD) ayak izini varsa, bağlı tooAzure AD ancak birleştirilmiş tooyour AD toobe güvenilir olmayan cihazları düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="680c6-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![Bulut uygulamaları](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="680c6-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="680c6-136">Next steps</span></span>

<span data-ttu-id="680c6-137">Ortamınızda bir cihaz temelli koşullu erişim ilkesini yapılandırmadan önce hello bir göz atalım [Azure Active Directory'de koşullu erişim için en iyi uygulamaları](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="680c6-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

