---
title: "Azure AD Connect: yükleme türünü seçin. | Microsoft Docs"
description: "Bu konuda, Azure AD Connect için kullanılacak yükleme türü seçme açıklanmaktadır"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="2bb8c-103">Azure AD Connect için kullanmak üzere hangi yükleme türünü seçin</span><span class="sxs-lookup"><span data-stu-id="2bb8c-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="2bb8c-104">Azure AD Connect, yeni yükleme için iki yükleme türleri vardır: Express ve özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="2bb8c-105">Bu konuda, yükleme sırasında kullanmak için hangi seçeneği karar vermenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="2bb8c-106">Express</span><span class="sxs-lookup"><span data-stu-id="2bb8c-106">Express</span></span>
<span data-ttu-id="2bb8c-107">Express en yaygın kullanılan bir seçenektir ve yaklaşık % 90'ını tarafından tüm yeni yüklemeler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="2bb8c-108">En yaygın müşteri senaryoları için çalışan bir yapılandırma sağlamak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="2bb8c-109">Bunu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="2bb8c-109">It assumes:</span></span>

- <span data-ttu-id="2bb8c-110">Şirket içi orman tek bir Active Directory var.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="2bb8c-111">Yükleme için kullanabileceğiniz bir kuruluş yöneticisi hesabına sahip.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="2bb8c-112">Şirket içi Active Directory 100. 000'den az nesneler var.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="2bb8c-113">Şunları alırsınız:</span><span class="sxs-lookup"><span data-stu-id="2bb8c-113">You get:</span></span>

- <span data-ttu-id="2bb8c-114">[Parola Eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md) şirket içi Azure ad çoklu oturum açma için.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="2bb8c-115">Eşitleyen bir yapılandırma [kullanıcılar, gruplar, kişiler ve Windows 10 bilgisayarlar](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="2bb8c-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="2bb8c-116">Tüm etki alanlarını ve tüm OU'larda tüm uygun nesneleri eşitlenmesi.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="2bb8c-117">[Otomatik yükseltmeyi](active-directory-aadconnect-feature-automatic-upgrade.md) en son sürüme her zaman kullandığınızdan emin olmak için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="2bb8c-118">Seçenekler burada Express kullanmaya devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2bb8c-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="2bb8c-119">Tüm OU'larda eşitlemek istemediğiniz yaparsanız hala Express kullanın ve son sayfasında seçimini kaldırın **eşitleme işlemini başlat...** *.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...***.</span></span> <span data-ttu-id="2bb8c-120">Yükleme Sihirbazı'nı yeniden çalıştırın ve OU'larda değiştirme [yapılandırma seçenekleri](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) ve zamanlanmış eşitleme etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="2bb8c-121">Azure AD Premium, parola geri yazma gibi özelliklerden birini, etkinleştirmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="2bb8c-122">İlk ilk yükleme almak için express gidin.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="2bb8c-123">Yükleme Sihirbazı'nı yeniden çalıştırın ve değiştirme [yapılandırma seçenekleri](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="2bb8c-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="2bb8c-124">Özel</span><span class="sxs-lookup"><span data-stu-id="2bb8c-124">Custom</span></span>
<span data-ttu-id="2bb8c-125">Özelleştirilmiş yolu express daha pek çok seçenek sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="2bb8c-126">Burada express için önceki bölümde açıklanan yapılandırma, kuruluşunuz için temsili olmadığı tüm durumlarda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="2bb8c-127">Şu durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="2bb8c-127">Use when:</span></span>

- <span data-ttu-id="2bb8c-128">Active Directory içinde bir kuruluş yöneticisi hesabı için erişim sahip değil.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="2bb8c-129">Birden çok orman veya birden çok orman gelecekte eşitlemek planlama.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="2bb8c-130">Connect sunucudan ulaşılabilir değil, ormanınızdaki etki alanları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="2bb8c-131">Kullanıcı oturum açma için Federasyon veya doğrudan kimlik doğrulama kullanmayı planlayın.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="2bb8c-132">100. 000'den fazla nesneleri ve tam bir SQL Server kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="2bb8c-133">Grup tabanlı filtreleme ve yalnızca etki alanı veya OU tabanlı filtreleme kullanmayı planlayın.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="2bb8c-134">DirSync'ten yükseltme</span><span class="sxs-lookup"><span data-stu-id="2bb8c-134">Upgrade from DirSync</span></span>
<span data-ttu-id="2bb8c-135">Şu anda DirSync kullanıyorsanız, ardından adımları [Dirsync'ten yükseltme](active-directory-aadconnect-dirsync-upgrade-get-started.md) varolan yapılandırmanızı yükseltmek için.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="2bb8c-136">İki farklı yükseltme seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2bb8c-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="2bb8c-137">Connect aynı sunucuya yüklemek için yerinde yükseltme.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="2bb8c-138">Mevcut DirSync sunucu hala durumdayken Bağlan yeni bir sunucuya yüklemek için paralel dağıtım.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="2bb8c-139">Azure AD eşitleme'den yükseltme</span><span class="sxs-lookup"><span data-stu-id="2bb8c-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="2bb8c-140">Azure AD eşitleme kullanmakta olduğunuz sonra izleyebilirsiniz [aynı adımları](active-directory-aadconnect-upgrade-previous-version.md) bir Connect sürümünden yeni bir yükseltme yaptığınızda olarak.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="2bb8c-141">İki farklı yükseltme seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2bb8c-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="2bb8c-142">Connect aynı sunucuya yüklemek için yerinde yükseltme.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="2bb8c-143">Esnek geçiş Bağlan varolan sırasında yeni bir sunucuya yüklemek için Azure AD eşitleme sunucusunun hala çalışır durumda.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="2bb8c-144">Fım2010 veya MIM2016 geçirmek</span><span class="sxs-lookup"><span data-stu-id="2bb8c-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="2bb8c-145">Şu anda Forefront Identity Manager 2010 veya Microsoft Identity Manager 2016 Azure AD Bağlayıcısı ile kullanıyorsanız, tek seçeneğiniz bir geçiş değil.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="2bb8c-146">Bölümünde açıklanan adımları [esnek geçiş](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="2bb8c-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="2bb8c-147">Aşağıdaki adımlarda, Azure AD eşitleme herhangi Bahsetme fım2010/MIM2016 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bb8c-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2bb8c-148">Next steps</span></span>
<span data-ttu-id="2bb8c-149">Kullanmak için seçtiğiniz seçeneğine bağlı olarak, içerik sol tablo Makalenizi ayrıntılı adımları bulmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="2bb8c-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
