---
title: "aaaAdd kullanıcı tooyour Azure RemoteApp koleksiyonu | Microsoft Docs"
description: "Bilgi nasıl tooadd kullanıcılar tooyour Azure RemoteApp koleksiyonu"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="15456-103">Nasıl tooadd kullanıcı tooyour Azure RemoteApp koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="15456-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="15456-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="15456-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="15456-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="15456-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="15456-106">Kullanıcılarınızın bakın ve uygulamalarınızı Azure RemoteApp kullanmaya başlamadan önce tooyour koleksiyonuna erişmek toogrant sahip.</span><span class="sxs-lookup"><span data-stu-id="15456-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="15456-107">Bu hello kolay bir parçasıdır: hello üzerinde **kullanıcı erişimini** sekmesinde, hello hello kullanıcısı için hesap bilgilerini girin ve ardından hello onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="15456-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="15456-108">Hangi hesap bilgileri gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="15456-108">What account information do you need?</span></span> <span data-ttu-id="15456-109">Oluşturduğunuz (Bulut veya karma) ve Office 365 ProPlus koleksiyonda kullanıp hello koleksiyon türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="15456-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="15456-110">Desteklenen kullanıcı kimlikleri</span><span class="sxs-lookup"><span data-stu-id="15456-110">Supported user identities</span></span>
<span data-ttu-id="15456-111">Merhaba farklı koleksiyon türleri (karma ve bulut) kullanarak farklı bir kullanıcı kimlikleri için erişim tooapplications destekler.</span><span class="sxs-lookup"><span data-stu-id="15456-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="15456-112">RemoteApp karma koleksiyonu, şirket içi ve Azure Active Directory Kiracı dizin Tümleştirmesi ile Active Directory etki alanı altyapısı yukarı tooset gerekir (ve isteğe bağlı olarak çoklu oturum açmayı).</span><span class="sxs-lookup"><span data-stu-id="15456-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="15456-113">Ayrıca, bazı Active Directory nesneleri hello şirket içi dizin toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="15456-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="15456-114">RemoteApp bulut koleksiyonu için Azure Active Directory kimlikleri destek sahip herhangi bir kullanıcı, kullanıcı erişim tooRemoteApp tooinclude Microsoft Accounts verilebilir.</span><span class="sxs-lookup"><span data-stu-id="15456-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="15456-115">Merhaba tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="15456-115">See hello table below.</span></span>

<span data-ttu-id="15456-116">Office 365, Azure Active Directory Kullanıcıları kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="15456-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="15456-117">Azure Active Directory karma varsa, dizin eşitlenen hesapları, bunlar bir RemoteApp karma dağıtımında kullanıcı erişimi verilebilir.</span><span class="sxs-lookup"><span data-stu-id="15456-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="15456-118">Bu tablo kimliği, koleksiyon ve hello Active Directory gereksinimleri nelerdir desteklenmektedir hızlı başvuru olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15456-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="15456-119">Kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="15456-119">User accounts</span></span> | <span data-ttu-id="15456-120">Bulut</span><span class="sxs-lookup"><span data-stu-id="15456-120">Cloud</span></span> | <span data-ttu-id="15456-121">Karma</span><span class="sxs-lookup"><span data-stu-id="15456-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15456-122">Microsoft Hesabı</span><span class="sxs-lookup"><span data-stu-id="15456-122">Microsoft Account</span></span> |<span data-ttu-id="15456-123">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-123">Yes</span></span> |<span data-ttu-id="15456-124">Hayır</span><span class="sxs-lookup"><span data-stu-id="15456-124">No</span></span> |
| <span data-ttu-id="15456-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="15456-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="15456-126">Yalnızca Azure AD bulut</span><span class="sxs-lookup"><span data-stu-id="15456-126">Azure AD cloud only</span></span> |<span data-ttu-id="15456-127">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-127">Yes</span></span> |<span data-ttu-id="15456-128">Hayır</span><span class="sxs-lookup"><span data-stu-id="15456-128">No</span></span> |
| <span data-ttu-id="15456-129">Parola Eşitleme ile ADsync</span><span class="sxs-lookup"><span data-stu-id="15456-129">ADsync with password sync</span></span> |<span data-ttu-id="15456-130">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-130">Yes</span></span> |<span data-ttu-id="15456-131">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-131">Yes</span></span> |
| <span data-ttu-id="15456-132">Parola Eşitleme olmadan ADsync</span><span class="sxs-lookup"><span data-stu-id="15456-132">ADsync without password sync</span></span> |<span data-ttu-id="15456-133">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-133">Yes</span></span> |<span data-ttu-id="15456-134">Hayır</span><span class="sxs-lookup"><span data-stu-id="15456-134">No</span></span> |
| <span data-ttu-id="15456-135">AD FS ile ADsync</span><span class="sxs-lookup"><span data-stu-id="15456-135">ADsync with AD FS</span></span> |<span data-ttu-id="15456-136">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-136">Yes</span></span> |<span data-ttu-id="15456-137">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-137">Yes</span></span> |
| <span data-ttu-id="15456-138">[3. taraf Azure desteklenen kimlik sağlayıcıları](https://msdn.microsoft.com/library/azure/jj679342.aspx) (örnek: Ping)</span><span class="sxs-lookup"><span data-stu-id="15456-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="15456-139">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-139">Yes</span></span> |<span data-ttu-id="15456-140">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-140">Yes</span></span> |
| <span data-ttu-id="15456-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="15456-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="15456-142">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-142">Yes</span></span> |<span data-ttu-id="15456-143">Evet</span><span class="sxs-lookup"><span data-stu-id="15456-143">Yes</span></span> |

<span data-ttu-id="15456-144">Kullanıma [daha fazla bilgi](remoteapp-ad.md) RemoteApp için Active Directory yapılandırma hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="15456-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="15456-145">Hello Azure Active Directory Kullanıcıları, aboneliğinizle ilişkili hello Kiracı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="15456-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="15456-146">(Görüntülemek ve aboneliğinizi hello değiştirmek **ayarları** hello portal sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="15456-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="15456-147">Bkz: [RemoteApp tarafından kullanılan değişiklik hello Azure Active Directory Kiracı](remoteapp-changetenant.md) daha fazla bilgi için.)</span><span class="sxs-lookup"><span data-stu-id="15456-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="15456-148">Office 365 ProPlus kullanıcı hesabı bilgileri</span><span class="sxs-lookup"><span data-stu-id="15456-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="15456-149">Koleksiyonunuzda hello Office 365 ProPlus şablon görüntüsü kullanıyorsanız *veya* Office 365 kullanan özel bir görüntü oluşturduysanız, hello için Office 365 aboneliğine sahip tooadd Azure Active Directory Kullanıcıları yalnızca izin verilir aboneliğiniz için varsayılan etki alanı.</span><span class="sxs-lookup"><span data-stu-id="15456-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="15456-150">Bkz: [Azure RemoteApp ile Office 365'ı kullanarak](remoteapp-o365.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="15456-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

