---
title: "MySQL için Azure veritabanında aaaLimitations | Microsoft Docs"
description: "MySQL için Azure veritabanındaki Önizleme sınırlamaları açıklar."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="1c18c-103">MySQL (Önizleme) Azure veritabanındaki sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="1c18c-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="1c18c-104">MySQL hizmeti için Hello Azure veritabanı genel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="1c18c-104">hello Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="1c18c-105">Merhaba aşağıdaki bölümlerde kapasite ve hello veritabanı hizmeti işlevsel sınırları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1c18c-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="1c18c-106">Hizmet katmanı üst sınırlar</span><span class="sxs-lookup"><span data-stu-id="1c18c-106">Service Tier Maximums</span></span>
<span data-ttu-id="1c18c-107">Azure veritabanı MySQL için bir sunucu oluştururken seçebileceğiniz birden çok hizmet katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="1c18c-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="1c18c-108">Daha fazla bilgi için bkz: [her hizmet katmanında nelerin kullanılabildiğini anlama](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="1c18c-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="1c18c-109">Olduğundan maksimum sayısını bağlantıları, işlem birimleri ve depolama her hizmet katmanında hello hizmet Önizleme sırasında şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="1c18c-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="1c18c-110">**En fazla bağlantı**</span><span class="sxs-lookup"><span data-stu-id="1c18c-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="1c18c-111">Temel 50 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="1c18c-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="1c18c-112">50 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="1c18c-112">50 connections</span></span>    |
| <span data-ttu-id="1c18c-113">Temel 100 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="1c18c-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="1c18c-114">100 bağlantılar</span><span class="sxs-lookup"><span data-stu-id="1c18c-114">100 connections</span></span>   |
| <span data-ttu-id="1c18c-115">Standart 100 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="1c18c-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="1c18c-116">200 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="1c18c-116">200 connections</span></span>   |
| <span data-ttu-id="1c18c-117">Standart 200 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="1c18c-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="1c18c-118">300 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="1c18c-118">300 connections</span></span>   |
| <span data-ttu-id="1c18c-119">Standart 400 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="1c18c-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="1c18c-120">400 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="1c18c-120">400 connections</span></span>   |
| <span data-ttu-id="1c18c-121">Standart 800 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="1c18c-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="1c18c-122">500 bağlantılar</span><span class="sxs-lookup"><span data-stu-id="1c18c-122">500 connections</span></span>   |
| <span data-ttu-id="1c18c-123">**En fazla işlem birimleri**</span><span class="sxs-lookup"><span data-stu-id="1c18c-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="1c18c-124">Temel hizmet katmanı</span><span class="sxs-lookup"><span data-stu-id="1c18c-124">Basic service tier</span></span>         | <span data-ttu-id="1c18c-125">100 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="1c18c-125">100 Compute Units</span></span> |
| <span data-ttu-id="1c18c-126">Standart hizmet katmanı</span><span class="sxs-lookup"><span data-stu-id="1c18c-126">Standard service tier</span></span>      | <span data-ttu-id="1c18c-127">800 işlem birimleri</span><span class="sxs-lookup"><span data-stu-id="1c18c-127">800 Compute Units</span></span> |
| <span data-ttu-id="1c18c-128">**En fazla depolama**</span><span class="sxs-lookup"><span data-stu-id="1c18c-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="1c18c-129">Temel hizmet katmanı</span><span class="sxs-lookup"><span data-stu-id="1c18c-129">Basic service tier</span></span>         | <span data-ttu-id="1c18c-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="1c18c-130">1 TB</span></span>              |
| <span data-ttu-id="1c18c-131">Standart hizmet katmanı</span><span class="sxs-lookup"><span data-stu-id="1c18c-131">Standard service tier</span></span>      | <span data-ttu-id="1c18c-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="1c18c-132">1 TB</span></span>              |

<span data-ttu-id="1c18c-133">Çok fazla bağlantı erişildiğinde, aşağıdaki hata hello alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1c18c-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="1c18c-134">1040 (08004). hata: Çok fazla bağlantı</span><span class="sxs-lookup"><span data-stu-id="1c18c-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="1c18c-135">Önizleme işlevsel sınırlamaları:</span><span class="sxs-lookup"><span data-stu-id="1c18c-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="1c18c-136">Ölçek işlemleri:</span><span class="sxs-lookup"><span data-stu-id="1c18c-136">Scale operations:</span></span>
1.  <span data-ttu-id="1c18c-137">Dinamik sunucularının hizmet katmanları arasında ölçeklendirme şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1c18c-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="1c18c-138">Diğer bir deyişle, temel ve standart hizmet katmanları arasında geçiş yapma.</span><span class="sxs-lookup"><span data-stu-id="1c18c-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="1c18c-139">Önceden oluşturulmuş sunucusundaki depolama dinamik talep üzerine çıktığını şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1c18c-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="1c18c-140">Sunucu depolama boyutunu azaltmak desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1c18c-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="1c18c-141">Sunucu sürüm yükseltme:</span><span class="sxs-lookup"><span data-stu-id="1c18c-141">Server version upgrades:</span></span>
- <span data-ttu-id="1c18c-142">Ana veritabanı altyapısı sürümleri arasında otomatik geçiş şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1c18c-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="1c18c-143">Abonelik Yönetimi:</span><span class="sxs-lookup"><span data-stu-id="1c18c-143">Subscription management:</span></span>
- <span data-ttu-id="1c18c-144">Önceden oluşturulmuş sunucuları abonelik ve kaynak grubu arasında dinamik olarak taşıma şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1c18c-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="1c18c-145">Noktası-içinde--geri yükleme:</span><span class="sxs-lookup"><span data-stu-id="1c18c-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="1c18c-146">Toodifferent hizmet katmanı ve/veya işlem birimleri ve depolama boyutu geri izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="1c18c-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="1c18c-147">Bırakılan bir sunucuya geri yüklenmesi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1c18c-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c18c-148">Sonraki Adımlar:</span><span class="sxs-lookup"><span data-stu-id="1c18c-148">Next Steps:</span></span>
<span data-ttu-id="1c18c-149">[Her hizmet katmanında nelerin kullanılabildiğini](concepts-service-tiers.md)
[MySQL veritabanı sürümleri desteklenir](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="1c18c-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
