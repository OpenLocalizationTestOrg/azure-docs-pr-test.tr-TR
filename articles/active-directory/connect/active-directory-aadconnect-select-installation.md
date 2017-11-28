---
title: "Azure AD Connect: yükleme türünü seçin. | Microsoft Docs"
description: "Bu konu, nasıl tooselect hello yükleme yazın toouse Azure AD Connect için adım adım anlatılmaktadır"
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
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="8f596-103">Azure AD Connect için hangi yükleme türü toouse seçin</span><span class="sxs-lookup"><span data-stu-id="8f596-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="8f596-104">Azure AD Connect, yeni yükleme için iki yükleme türleri vardır: Express ve özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8f596-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="8f596-105">Bu konu, yükleme sırasında toouse seçeneği toodecide yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8f596-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="8f596-106">Express</span><span class="sxs-lookup"><span data-stu-id="8f596-106">Express</span></span>
<span data-ttu-id="8f596-107">Hızlı Başlangıç en yaygın kullanılan bir seçenektir ve yaklaşık % 90'ını tarafından tüm yeni yüklemeler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f596-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="8f596-108">Tasarlanmış tooprovide hello en yaygın müşteri senaryoları için çalışan bir yapılandırma oluştu.</span><span class="sxs-lookup"><span data-stu-id="8f596-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="8f596-109">Bunu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="8f596-109">It assumes:</span></span>

- <span data-ttu-id="8f596-110">Şirket içi orman tek bir Active Directory var.</span><span class="sxs-lookup"><span data-stu-id="8f596-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="8f596-111">Merhaba yükleme için kullanabileceğiniz bir kuruluş yöneticisi hesabına sahip.</span><span class="sxs-lookup"><span data-stu-id="8f596-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="8f596-112">Şirket içi Active Directory 100. 000'den az nesneler var.</span><span class="sxs-lookup"><span data-stu-id="8f596-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="8f596-113">Şunları alırsınız:</span><span class="sxs-lookup"><span data-stu-id="8f596-113">You get:</span></span>

- <span data-ttu-id="8f596-114">[Parola Eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md) çoklu oturum açma için şirket içi tooAzure AD alanından.</span><span class="sxs-lookup"><span data-stu-id="8f596-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="8f596-115">Eşitleyen bir yapılandırma [kullanıcılar, gruplar, kişiler ve Windows 10 bilgisayarlar](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="8f596-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="8f596-116">Tüm etki alanlarını ve tüm OU'larda tüm uygun nesneleri eşitlenmesi.</span><span class="sxs-lookup"><span data-stu-id="8f596-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="8f596-117">[Otomatik yükseltmeyi](active-directory-aadconnect-feature-automatic-upgrade.md) etkin toomake hello en son sürüme her zaman kullandığınızdan emin olan.</span><span class="sxs-lookup"><span data-stu-id="8f596-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="8f596-118">Seçenekler burada Express kullanmaya devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8f596-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="8f596-119">Tüm OU'larda toosynchronize istemiyorsanız hala Express ve kullanabilirsiniz hello son sayfasında işaretini **hello eşitleme işlemini başlat...** *.</span><span class="sxs-lookup"><span data-stu-id="8f596-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="8f596-120">Merhaba Yükleme Sihirbazı'nı yeniden çalıştırın ve hello OU'larda değiştirme [yapılandırma seçenekleri](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) ve zamanlanmış eşitleme etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8f596-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="8f596-121">Tooenable Azure AD Premium hello özelliklerden birini, parola geri yazma gibi istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="8f596-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="8f596-122">İlk tamamlandı express tooget hello ilk yükleme gidin.</span><span class="sxs-lookup"><span data-stu-id="8f596-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="8f596-123">Merhaba Yükleme Sihirbazı'nı yeniden çalıştırın ve hello değiştirme [yapılandırma seçenekleri](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="8f596-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="8f596-124">Özel</span><span class="sxs-lookup"><span data-stu-id="8f596-124">Custom</span></span>
<span data-ttu-id="8f596-125">Merhaba özelleştirilmiş yolu express daha pek çok seçenek sağlar.</span><span class="sxs-lookup"><span data-stu-id="8f596-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="8f596-126">Burada express için önceki bölümde açıklanan hello yapılandırma, kuruluşunuz için temsili olmadığı tüm durumlarda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8f596-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="8f596-127">Şu durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="8f596-127">Use when:</span></span>

- <span data-ttu-id="8f596-128">Active Directory'de erişim tooan kuruluş yöneticisi hesabı yok.</span><span class="sxs-lookup"><span data-stu-id="8f596-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="8f596-129">Birden çok orman veya hello gelecekteki birden fazla ormanda toosynchronize planlayın.</span><span class="sxs-lookup"><span data-stu-id="8f596-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="8f596-130">Merhaba Bağlan sunucudan ulaşılabilir değil, ormanınızdaki etki alanları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8f596-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="8f596-131">Toouse Federasyon veya kullanıcı oturum açma için doğrudan kimlik doğrulama planlayın.</span><span class="sxs-lookup"><span data-stu-id="8f596-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="8f596-132">100. 000'den fazla nesneleri ve toouse tam SQL Server gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f596-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="8f596-133">Grup tabanlı toouse filtreleme ve yalnızca etki alanı veya OU tabanlı filtreleme planlayın.</span><span class="sxs-lookup"><span data-stu-id="8f596-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="8f596-134">DirSync'ten yükseltme</span><span class="sxs-lookup"><span data-stu-id="8f596-134">Upgrade from DirSync</span></span>
<span data-ttu-id="8f596-135">Şu anda DirSync kullanıyorsanız, ardından hello adımları [Dirsync'ten yükseltme](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade varolan yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="8f596-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="8f596-136">İki farklı yükseltme seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8f596-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="8f596-137">Yerinde yükseltme tooinstall bağlanmak hello üzerinde aynı sunucu.</span><span class="sxs-lookup"><span data-stu-id="8f596-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="8f596-138">Merhaba mevcut DirSync sunucu hala çalışır durumdayken yeni bir sunucu üzerinde dağıtım tooinstall Bağlan paralel.</span><span class="sxs-lookup"><span data-stu-id="8f596-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="8f596-139">Azure AD eşitleme'den yükseltme</span><span class="sxs-lookup"><span data-stu-id="8f596-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="8f596-140">Azure AD eşitleme kullanmakta olduğunuz sonra hello izleyebilirsiniz [aynı adımları](active-directory-aadconnect-upgrade-previous-version.md) bir Bağlan sürüm tooa yeni yükselttiğinizde olarak.</span><span class="sxs-lookup"><span data-stu-id="8f596-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="8f596-141">İki farklı yükseltme seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8f596-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="8f596-142">Yerinde yükseltme tooinstall bağlanmak hello üzerinde aynı sunucu.</span><span class="sxs-lookup"><span data-stu-id="8f596-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="8f596-143">Merhaba var olan Azure AD eşitleme sunucusu sırasında yeni bir sunucu üzerinde esnek geçiş tooinstall Bağlan hala çalışır durumda.</span><span class="sxs-lookup"><span data-stu-id="8f596-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="8f596-144">Fım2010 veya MIM2016 geçirmek</span><span class="sxs-lookup"><span data-stu-id="8f596-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="8f596-145">Şu anda Forefront Identity Manager 2010 veya Microsoft Identity Manager 2016 hello Azure AD Bağlayıcısı ile kullanıyorsanız, tek seçeneğiniz bir geçiş değil.</span><span class="sxs-lookup"><span data-stu-id="8f596-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="8f596-146">Açıklanan başlangıç adımları [esnek geçiş](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="8f596-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="8f596-147">Merhaba adımlarda, Azure AD eşitleme herhangi Bahsetme fım2010/MIM2016 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8f596-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f596-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8f596-148">Next steps</span></span>
<span data-ttu-id="8f596-149">Toouse seçili Hello seçeneğine bağlı olarak, hello tabloyu kullanın içerik toohello sol toofind Makalenizi hello ile adımları ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="8f596-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
