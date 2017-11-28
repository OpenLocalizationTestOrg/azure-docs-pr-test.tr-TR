---
title: "aaaAzure AD Connect Health sürüm geçmişi"
description: "Bu belgede, Azure AD Connect Health ve bu sürümlerde dahil hello sürümleri açıklanmaktadır."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: a583263e412f5da9af75947f3431de2494042388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-version-release-history"></a><span data-ttu-id="df878-103">Azure AD Connect Health: Sürüm Yayınlama Geçmişi</span><span class="sxs-lookup"><span data-stu-id="df878-103">Azure AD Connect Health: Version Release History</span></span>
<span data-ttu-id="df878-104">Hello Azure Active Directory ekibi, yeni özellikler ve işlevsellik ile Azure AD Connect Health düzenli olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="df878-104">hello Azure Active Directory team regularly updates Azure AD Connect Health with new features and functionality.</span></span> <span data-ttu-id="df878-105">Bu makalede hello sürümleri ve çıkarılan özellikleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="df878-105">This article lists hello versions and features that have been released.</span></span>

## <a name="october-2016"></a><span data-ttu-id="df878-106">Ekim 2016</span><span class="sxs-lookup"><span data-stu-id="df878-106">October 2016</span></span>
<span data-ttu-id="df878-107">**Aracı güncelleştirmesi:**</span><span class="sxs-lookup"><span data-stu-id="df878-107">**Agent Update:**</span></span>

* <span data-ttu-id="df878-108">AD FS için Azure AD Connect Health Aracısı \(sürüm 2.6.408.0\)</span><span class="sxs-lookup"><span data-stu-id="df878-108">Azure AD Connect Health agent for AD FS \(version 2.6.408.0\)</span></span>
  1. <span data-ttu-id="df878-109">İstemci IP adresleri kimlik doğrulama isteklerinin seviyelerinden geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="df878-109">Improvements in detecting client IP addresses in authentication requests</span></span>
  2. <span data-ttu-id="df878-110">Hata düzeltmeleri tooAlerts ilgili</span><span class="sxs-lookup"><span data-stu-id="df878-110">Bug Fixes related tooAlerts</span></span>
* <span data-ttu-id="df878-111">AD DS (sürüm 2.6.408.0) için Azure AD Connect Health Aracısı</span><span class="sxs-lookup"><span data-stu-id="df878-111">Azure AD Connect Health agent for AD DS (version 2.6.408.0)</span></span>
  1. <span data-ttu-id="df878-112">Hata düzeltmeleri tooAlerts ilgili.</span><span class="sxs-lookup"><span data-stu-id="df878-112">Bug fixes related tooAlerts.</span></span>
* <span data-ttu-id="df878-113">Azure AD Connect ile sürüm 1.1.281.0 yayımlanan eşitleme (sürüm 2.6.353.0) için Azure AD Connect Health Aracısı</span><span class="sxs-lookup"><span data-stu-id="df878-113">Azure AD Connect Health agent for Sync (version 2.6.353.0) released with Azure AD Connect version 1.1.281.0</span></span>
  1. <span data-ttu-id="df878-114">Eşitleme hata raporlarını hello için gerekli hello verileri sağlar</span><span class="sxs-lookup"><span data-stu-id="df878-114">Provide hello required data for hello Synchronization Error Reports</span></span>
  2. <span data-ttu-id="df878-115">Hata düzeltmeleri tooAlerts ilgili</span><span class="sxs-lookup"><span data-stu-id="df878-115">Bug fixes related tooAlerts</span></span>

<span data-ttu-id="df878-116">**Yeni Önizleme özellikleri:**</span><span class="sxs-lookup"><span data-stu-id="df878-116">**New preview features:**</span></span>

* <span data-ttu-id="df878-117">Azure ad eşitleme hata raporlarını Bağlan</span><span class="sxs-lookup"><span data-stu-id="df878-117">Synchronization Error Reports for Azure AD Connect</span></span>

<span data-ttu-id="df878-118">**Yeni Özellikler:**</span><span class="sxs-lookup"><span data-stu-id="df878-118">**New features:**</span></span>

* <span data-ttu-id="df878-119">Azure AD Connect Health AD FS için-IP adres alanını hatalı kullanıcı adı/parola ile ilk 50 kullanıcıya ilişkin hello rapordaki kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="df878-119">Azure AD Connect Health for AD FS - IP address field is available in hello report about top 50 users with bad username/password.</span></span>

## <a name="july-2016"></a><span data-ttu-id="df878-120">Temmuz 2016</span><span class="sxs-lookup"><span data-stu-id="df878-120">July 2016</span></span>
<span data-ttu-id="df878-121">**Yeni Önizleme özellikleri:**</span><span class="sxs-lookup"><span data-stu-id="df878-121">**New preview features:**</span></span>

* <span data-ttu-id="df878-122">[Azure AD Connect Health için AD DS](active-directory-aadconnect-health-adds.md).</span><span class="sxs-lookup"><span data-stu-id="df878-122">[Azure AD Connect Health for AD DS](active-directory-aadconnect-health-adds.md).</span></span>

## <a name="january-2016"></a><span data-ttu-id="df878-123">2016 Ocak</span><span class="sxs-lookup"><span data-stu-id="df878-123">January 2016</span></span>
<span data-ttu-id="df878-124">**Aracı güncelleştirmesi:**</span><span class="sxs-lookup"><span data-stu-id="df878-124">**Agent Update:**</span></span>

* <span data-ttu-id="df878-125">AD FS (sürüm 2.6.91.1512) için Azure AD Connect Health Aracısı</span><span class="sxs-lookup"><span data-stu-id="df878-125">Azure AD Connect Health agent for AD FS (version 2.6.91.1512)</span></span>

<span data-ttu-id="df878-126">**Yeni Özellikler:**</span><span class="sxs-lookup"><span data-stu-id="df878-126">**New features:**</span></span>

* [<span data-ttu-id="df878-127">Test Bağlantısı aracı için Azure AD Connect Health aracıları</span><span class="sxs-lookup"><span data-stu-id="df878-127">Test Connectivity Tool for Azure AD Connect Health Agents</span></span>](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a><span data-ttu-id="df878-128">2015 Kasım</span><span class="sxs-lookup"><span data-stu-id="df878-128">November 2015</span></span>
<span data-ttu-id="df878-129">**Yeni Özellikler:**</span><span class="sxs-lookup"><span data-stu-id="df878-129">**New features:**</span></span>

* <span data-ttu-id="df878-130">Desteği [rol tabanlı erişim denetimi](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)</span><span class="sxs-lookup"><span data-stu-id="df878-130">Support for [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)</span></span>

<span data-ttu-id="df878-131">**Yeni Önizleme özellikleri:**</span><span class="sxs-lookup"><span data-stu-id="df878-131">**New preview features:**</span></span>

* <span data-ttu-id="df878-132">[Azure AD Connect Health eşitleme](active-directory-aadconnect-health-sync.md).</span><span class="sxs-lookup"><span data-stu-id="df878-132">[Azure AD Connect Health for sync](active-directory-aadconnect-health-sync.md).</span></span>

<span data-ttu-id="df878-133">**Giderilen sorunlar:**</span><span class="sxs-lookup"><span data-stu-id="df878-133">**Fixed issues:**</span></span>

* <span data-ttu-id="df878-134">Aracı kaydı sırasında görülen hataları için hata düzeltmeleri.</span><span class="sxs-lookup"><span data-stu-id="df878-134">Bug fixes for errors seen during agent registrations.</span></span>

## <a name="september-2015"></a><span data-ttu-id="df878-135">Eylül 2015</span><span class="sxs-lookup"><span data-stu-id="df878-135">September 2015</span></span>
<span data-ttu-id="df878-136">**Yeni Özellikler:**</span><span class="sxs-lookup"><span data-stu-id="df878-136">**New features:**</span></span>

* <span data-ttu-id="df878-137">AD FS için kullanıcı adı parola rapor yanlış</span><span class="sxs-lookup"><span data-stu-id="df878-137">Wrong Username password report for AD FS</span></span>
* <span data-ttu-id="df878-138">Destek tooconfigure kimliği doğrulanmamış HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="df878-138">Support tooconfigure Unauthenticated HTTP Proxy</span></span>
* <span data-ttu-id="df878-139">Sunucu Çekirdeği yüklemesinde tooconfigure Aracısı desteği</span><span class="sxs-lookup"><span data-stu-id="df878-139">Support tooconfigure agent on Server core</span></span>
* <span data-ttu-id="df878-140">AD FS için geliştirmeler tooAlerts</span><span class="sxs-lookup"><span data-stu-id="df878-140">Improvements tooAlerts for AD FS</span></span>
* <span data-ttu-id="df878-141">Bağlantı ve veriler için AD FS için Azure AD Connect Health Aracısı geliştirmeler karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="df878-141">Improvements in Azure AD Connect Health Agent for AD FS for connectivity and data upload.</span></span>

<span data-ttu-id="df878-142">**Giderilen sorunlar:**</span><span class="sxs-lookup"><span data-stu-id="df878-142">**Fixed issues:**</span></span>

* <span data-ttu-id="df878-143">AD FS hata türleri için kullanım incelemesi hata düzeltmeleri.</span><span class="sxs-lookup"><span data-stu-id="df878-143">Bug fixes in Usage Insights for AD FS Error types.</span></span>

## <a name="june-2015"></a><span data-ttu-id="df878-144">Haziran 2015</span><span class="sxs-lookup"><span data-stu-id="df878-144">June 2015</span></span>
<span data-ttu-id="df878-145">**Azure AD Connect Health ilk sürüm için AD FS ve AD FS Proxy.**</span><span class="sxs-lookup"><span data-stu-id="df878-145">**Initial release of Azure AD Connect Health for AD FS and AD FS Proxy.**</span></span>

<span data-ttu-id="df878-146">**Yeni Özellikler:**</span><span class="sxs-lookup"><span data-stu-id="df878-146">**New features:**</span></span>

* <span data-ttu-id="df878-147">AD FS ve AD FS Proxy sunucularının e-posta bildirimleri ile izleme için Uyarılar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="df878-147">Alerts for monitoring AD FS and AD FS Proxy servers with email notifications.</span></span>
* <span data-ttu-id="df878-148">Kolay erişim tooAD FS topolojisi ve AD FS performans sayaçları düzenleri.</span><span class="sxs-lookup"><span data-stu-id="df878-148">Easy access tooAD FS topology and patterns in AD FS Performance Counters.</span></span>
* <span data-ttu-id="df878-149">Uygulamalar, kimlik doğrulama yöntemleri, ağ konumu vb. isteği göre gruplandırılmış AD FS sunucularında başarılı belirteç isteklerini eğilimi.</span><span class="sxs-lookup"><span data-stu-id="df878-149">Trend in successful token requests on AD FS servers grouped by Applications, Authentication Methods, Request Network Location etc.</span></span>
* <span data-ttu-id="df878-150">Hata türleri vb. uygulamalar tarafından gruplandırılmış AD FS sunucularındaki başarısız istek eğilimler.</span><span class="sxs-lookup"><span data-stu-id="df878-150">Trends in failed request on AD FS servers grouped by Applications, Error Types etc.</span></span>
* <span data-ttu-id="df878-151">Azure AD genel yönetici kimlik bilgilerini kullanarak basit aracı dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="df878-151">Simpler Agent Deployment using Azure AD Global Admin credentials.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="df878-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="df878-152">Next steps</span></span>
<span data-ttu-id="df878-153">Daha fazla bilgi edinmek [hello bulutta, şirket içi kimlik altyapınızı ve Eşitleme hizmetlerini izlemek](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="df878-153">Learn more about [Monitor your on-premises identity infrastructure and synchronization services in hello cloud](active-directory-aadconnect-health.md).</span></span>

