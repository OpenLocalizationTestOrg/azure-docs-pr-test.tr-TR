---
title: "Azure RemoteApp koleksiyonunuzun kullanıcı ekleme | Microsoft Docs"
description: "Kullanıcıların Azure RemoteApp koleksiyonunuzun eklemeyi öğrenin"
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="3e16c-103">Azure RemoteApp koleksiyonunuzun kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="3e16c-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3e16c-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="3e16c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3e16c-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="3e16c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3e16c-106">Kullanıcılarınızın bakın ve uygulamalarınızı Azure RemoteApp kullanmaya başlamadan önce koleksiyonunuzu erişim vermek sahip.</span><span class="sxs-lookup"><span data-stu-id="3e16c-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="3e16c-107">Bu kolay bir parçasıdır: üzerinde **kullanıcı erişimini** sekmesinde, kullanıcı hesabı bilgilerini girin ve ardından onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e16c-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="3e16c-108">Hangi hesap bilgileri gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="3e16c-108">What account information do you need?</span></span> <span data-ttu-id="3e16c-109">Oluşturduğunuz (Bulut veya karma) ve Office 365 ProPlus koleksiyonda kullanıp koleksiyon türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="3e16c-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="3e16c-110">Desteklenen kullanıcı kimlikleri</span><span class="sxs-lookup"><span data-stu-id="3e16c-110">Supported user identities</span></span>
<span data-ttu-id="3e16c-111">Uygulamalara erişimi için farklı kullanıcı kimliklerini kullanarak farklı koleksiyon türleri (karma ve bulut) destekler.</span><span class="sxs-lookup"><span data-stu-id="3e16c-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="3e16c-112">RemoteApp karma koleksiyonu için şirket içi ve Azure Active Directory Kiracı dizin Tümleştirmesi ile bir Active Directory etki alanı altyapısını ayarlamak için (ve isteğe bağlı olarak çoklu oturum açmayı) gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e16c-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="3e16c-113">Ayrıca, bazı Active Directory nesnelerini şirket içi dizinini oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e16c-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="3e16c-114">RemoteApp bulut koleksiyonu için Azure Active Directory kimlikleri destek sahip herhangi bir kullanıcı RemoteApp Microsoft Accounts dahil etmek için kullanıcı erişimini verilebilir.</span><span class="sxs-lookup"><span data-stu-id="3e16c-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="3e16c-115">Aşağıdaki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="3e16c-115">See the table below.</span></span>

<span data-ttu-id="3e16c-116">Office 365, Azure Active Directory Kullanıcıları kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="3e16c-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="3e16c-117">Azure Active Directory karma varsa, dizin eşitlenen hesapları, bunlar bir RemoteApp karma dağıtımında kullanıcı erişimi verilebilir.</span><span class="sxs-lookup"><span data-stu-id="3e16c-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="3e16c-118">Bu tablo kimliği, koleksiyon ve Active Directory gereksinimleri nelerdir desteklenmektedir hızlı başvuru olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e16c-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="3e16c-119">Kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="3e16c-119">User accounts</span></span> | <span data-ttu-id="3e16c-120">Bulut</span><span class="sxs-lookup"><span data-stu-id="3e16c-120">Cloud</span></span> | <span data-ttu-id="3e16c-121">Karma</span><span class="sxs-lookup"><span data-stu-id="3e16c-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e16c-122">Microsoft Hesabı</span><span class="sxs-lookup"><span data-stu-id="3e16c-122">Microsoft Account</span></span> |<span data-ttu-id="3e16c-123">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-123">Yes</span></span> |<span data-ttu-id="3e16c-124">Hayır</span><span class="sxs-lookup"><span data-stu-id="3e16c-124">No</span></span> |
| <span data-ttu-id="3e16c-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="3e16c-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="3e16c-126">Yalnızca Azure AD bulut</span><span class="sxs-lookup"><span data-stu-id="3e16c-126">Azure AD cloud only</span></span> |<span data-ttu-id="3e16c-127">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-127">Yes</span></span> |<span data-ttu-id="3e16c-128">Hayır</span><span class="sxs-lookup"><span data-stu-id="3e16c-128">No</span></span> |
| <span data-ttu-id="3e16c-129">Parola Eşitleme ile ADsync</span><span class="sxs-lookup"><span data-stu-id="3e16c-129">ADsync with password sync</span></span> |<span data-ttu-id="3e16c-130">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-130">Yes</span></span> |<span data-ttu-id="3e16c-131">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-131">Yes</span></span> |
| <span data-ttu-id="3e16c-132">Parola Eşitleme olmadan ADsync</span><span class="sxs-lookup"><span data-stu-id="3e16c-132">ADsync without password sync</span></span> |<span data-ttu-id="3e16c-133">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-133">Yes</span></span> |<span data-ttu-id="3e16c-134">Hayır</span><span class="sxs-lookup"><span data-stu-id="3e16c-134">No</span></span> |
| <span data-ttu-id="3e16c-135">AD FS ile ADsync</span><span class="sxs-lookup"><span data-stu-id="3e16c-135">ADsync with AD FS</span></span> |<span data-ttu-id="3e16c-136">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-136">Yes</span></span> |<span data-ttu-id="3e16c-137">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-137">Yes</span></span> |
| <span data-ttu-id="3e16c-138">[3. taraf Azure desteklenen kimlik sağlayıcıları](https://msdn.microsoft.com/library/azure/jj679342.aspx) (örnek: Ping)</span><span class="sxs-lookup"><span data-stu-id="3e16c-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="3e16c-139">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-139">Yes</span></span> |<span data-ttu-id="3e16c-140">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-140">Yes</span></span> |
| <span data-ttu-id="3e16c-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3e16c-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="3e16c-142">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-142">Yes</span></span> |<span data-ttu-id="3e16c-143">Evet</span><span class="sxs-lookup"><span data-stu-id="3e16c-143">Yes</span></span> |

<span data-ttu-id="3e16c-144">Kullanıma [daha fazla bilgi](remoteapp-ad.md) RemoteApp için Active Directory yapılandırma hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="3e16c-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="3e16c-145">Azure Active Directory kullanıcıları, aboneliğinizle ilişkili kiracıya ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3e16c-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="3e16c-146">(Aboneliğinizi, portalın **Ayarlar** sekmesinde görüntüleyebilir ve değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e16c-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="3e16c-147">Daha fazla bilgi için bkz. [RemoteApp tarafından kullanılan Azure Active Directory kiracısını değiştirme](remoteapp-changetenant.md).)</span><span class="sxs-lookup"><span data-stu-id="3e16c-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="3e16c-148">Office 365 ProPlus kullanıcı hesabı bilgileri</span><span class="sxs-lookup"><span data-stu-id="3e16c-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="3e16c-149">Koleksiyonunuzda Office 365 ProPlus şablon görüntüsü kullanıyorsanız *veya* Office 365 kullanan özel bir görüntü oluşturduysanız, yalnızca aboneliğinizin varsayılan etki alanı için Office 365 aboneliğine sahip Azure Active Directory Kullanıcıları eklemek için izin verilir.</span><span class="sxs-lookup"><span data-stu-id="3e16c-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="3e16c-150">Bkz: [Azure RemoteApp ile Office 365'ı kullanarak](remoteapp-o365.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3e16c-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

