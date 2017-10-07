---
title: "Azure veritabanı PostgreSQL için aaaLimitations | Microsoft Docs"
description: "PostgreSQL Azure veritabanındaki sınırlamalar açıklanır."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="77bf2-103">PostgreSQL Azure veritabanındaki sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="77bf2-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="77bf2-104">Hello Azure veritabanı PostgreSQL hizmeti için genel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="77bf2-104">hello Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="77bf2-105">Merhaba aşağıdaki bölümlerde kapasite ve hello veritabanı hizmeti işlevsel sınırları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="77bf2-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="77bf2-106">Hizmet katmanı üst sınırlar</span><span class="sxs-lookup"><span data-stu-id="77bf2-106">Service Tier Maximums</span></span>
<span data-ttu-id="77bf2-107">Azure veritabanı PostgreSQL için bir sunucu oluştururken seçebileceğiniz birden çok hizmet katmanı içerir.</span><span class="sxs-lookup"><span data-stu-id="77bf2-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="77bf2-108">Daha fazla bilgi için bkz: [her hizmet katmanında nelerin kullanılabildiğini anlama](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="77bf2-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="77bf2-109">Olduğundan maksimum sayısını bağlantıları, işlem birimleri ve depolama her hizmet katmanında hello hizmet Önizleme sırasında şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="77bf2-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="77bf2-110">**En fazla bağlantı**</span><span class="sxs-lookup"><span data-stu-id="77bf2-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="77bf2-111">Temel 50 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="77bf2-112">50 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="77bf2-112">50 connections</span></span>    |
| <span data-ttu-id="77bf2-113">Temel 100 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="77bf2-114">100 bağlantılar</span><span class="sxs-lookup"><span data-stu-id="77bf2-114">100 connections</span></span>   |
| <span data-ttu-id="77bf2-115">Standart 100 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="77bf2-116">200 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="77bf2-116">200 connections</span></span>   |
| <span data-ttu-id="77bf2-117">Standart 200 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="77bf2-118">300 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="77bf2-118">300 connections</span></span>   |
| <span data-ttu-id="77bf2-119">Standart 400 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="77bf2-120">400 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="77bf2-120">400 connections</span></span>   |
| <span data-ttu-id="77bf2-121">Standart 800 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="77bf2-122">500 bağlantılar</span><span class="sxs-lookup"><span data-stu-id="77bf2-122">500 connections</span></span>   |
| <span data-ttu-id="77bf2-123">**En fazla işlem birimleri**</span><span class="sxs-lookup"><span data-stu-id="77bf2-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="77bf2-124">Temel hizmet katmanı</span><span class="sxs-lookup"><span data-stu-id="77bf2-124">Basic service tier</span></span>         | <span data-ttu-id="77bf2-125">100 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-125">100 Compute Units</span></span> |
| <span data-ttu-id="77bf2-126">Standart hizmet katmanı</span><span class="sxs-lookup"><span data-stu-id="77bf2-126">Standard service tier</span></span>      | <span data-ttu-id="77bf2-127">800 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-127">800 Compute Units</span></span> |
| <span data-ttu-id="77bf2-128">**En fazla depolama**</span><span class="sxs-lookup"><span data-stu-id="77bf2-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="77bf2-129">Temel hizmet katmanı</span><span class="sxs-lookup"><span data-stu-id="77bf2-129">Basic service tier</span></span>         | <span data-ttu-id="77bf2-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="77bf2-130">1 TB</span></span>              |
| <span data-ttu-id="77bf2-131">Standart hizmet katmanı</span><span class="sxs-lookup"><span data-stu-id="77bf2-131">Standard service tier</span></span>      | <span data-ttu-id="77bf2-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="77bf2-132">1 TB</span></span>              |

<span data-ttu-id="77bf2-133">Çok fazla bağlantı erişildiğinde, aşağıdaki hata hello alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="77bf2-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="77bf2-134">Önemli: ne yazık ki zaten çok fazla sayıda istemci</span><span class="sxs-lookup"><span data-stu-id="77bf2-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="77bf2-135">Önizleme işlevsel sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="77bf2-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="77bf2-136">Ölçek işlemleri</span><span class="sxs-lookup"><span data-stu-id="77bf2-136">Scale operations</span></span>
1.  <span data-ttu-id="77bf2-137">Dinamik sunucularının hizmet katmanları arasında ölçeklendirme şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="77bf2-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="77bf2-138">Diğer bir deyişle, temel ve standart hizmet katmanları arasında geçiş yapma.</span><span class="sxs-lookup"><span data-stu-id="77bf2-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="77bf2-139">Önceden oluşturulmuş sunucusundaki depolama dinamik talep üzerine çıktığını şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="77bf2-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="77bf2-140">Sunucu depolama boyutunu azaltmak desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="77bf2-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="77bf2-141">Sunucu sürüm yükseltme</span><span class="sxs-lookup"><span data-stu-id="77bf2-141">Server version upgrades</span></span>
- <span data-ttu-id="77bf2-142">Ana veritabanı altyapısı sürümleri arasında otomatik geçiş şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="77bf2-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="77bf2-143">Abonelik Yönetimi</span><span class="sxs-lookup"><span data-stu-id="77bf2-143">Subscription management</span></span>
- <span data-ttu-id="77bf2-144">Önceden oluşturulmuş sunucuları abonelik ve kaynak grubu arasında dinamik olarak taşıma şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="77bf2-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="77bf2-145">belirli bir noktaya geri yükleme</span><span class="sxs-lookup"><span data-stu-id="77bf2-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="77bf2-146">Toodifferent hizmet katmanı ve/veya işlem birimleri ve depolama boyutu geri izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="77bf2-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="77bf2-147">Bırakılan bir sunucuya geri yüklenmesi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="77bf2-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77bf2-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="77bf2-148">Next steps</span></span>
- <span data-ttu-id="77bf2-149">Anlamak [her fiyatlandırma katmanının kullanılabilir](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="77bf2-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="77bf2-150">Anlamak [PostgreSQL veritabanı sürümleri desteklenir](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="77bf2-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="77bf2-151">Gözden geçirme [nasıl tooBack yedeklemek ve geri yükleme PostgreSQL kullanmak için bir sunucu Azure veritabanındaki Azure portal hello](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="77bf2-151">Review [How tooBack up and Restore a server in Azure Database for PostgreSQL using hello Azure portal](howto-restore-server-portal.md)</span></span>
