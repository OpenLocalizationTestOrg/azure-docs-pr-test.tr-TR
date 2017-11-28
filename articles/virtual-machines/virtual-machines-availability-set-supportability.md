---
title: "Azure VM'ler için mevcut bir kullanılabilirlik ekleme desteklenebilirlik ayarlama | Microsoft Docs"
description: "Azure VM'ler var olan bir kullanılabilirlik kümesine ekleme desteklenebilirlik."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a><span data-ttu-id="d3fa3-103">Azure VM'ler var olan bir kullanılabilirlik kümesine ekleme desteklenebilirlik</span><span class="sxs-lookup"><span data-stu-id="d3fa3-103">Supportability of adding Azure VMs to an existing availability set</span></span>

<span data-ttu-id="d3fa3-104">Yeni sanal makineler (VM'ler) eklediğiniz zaman sınırlamaları var olan bir kullanılabilirlik kümesine bazen karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3fa3-104">You may occasionally encounter limitations when you add new virtual machines (VMs) to an existing availability set.</span></span> <span data-ttu-id="d3fa3-105">Aşağıdaki grafikte aynı kullanılabilirlik kümesinde karıştırabilirsiniz hangi VM dizisi ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="d3fa3-105">The following chart details which VM series you can mix in the same availability set.</span></span>

<span data-ttu-id="d3fa3-106">VM'ler farklı türlerini karma olarak desteklenebilirlik matris şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d3fa3-106">Here is the supportability matrix to mix different types of VMs:</span></span>

<span data-ttu-id="d3fa3-107">Seri & kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="d3fa3-107">Series & Availability Set</span></span>|<span data-ttu-id="d3fa3-108">İkinci VM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-108">Second VM</span></span>|<span data-ttu-id="d3fa3-109">A</span><span class="sxs-lookup"><span data-stu-id="d3fa3-109">A</span></span>|<span data-ttu-id="d3fa3-110">Av2</span><span class="sxs-lookup"><span data-stu-id="d3fa3-110">Av2</span></span>|<span data-ttu-id="d3fa3-111">D</span><span class="sxs-lookup"><span data-stu-id="d3fa3-111">D</span></span>|<span data-ttu-id="d3fa3-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="d3fa3-112">Dv2</span></span>|<span data-ttu-id="d3fa3-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="d3fa3-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="d3fa3-114">İlk VM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-114">First VM</span></span>|||||||
|<span data-ttu-id="d3fa3-115">A</span><span class="sxs-lookup"><span data-stu-id="d3fa3-115">A</span></span>||<span data-ttu-id="d3fa3-116">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-116">OK</span></span>|<span data-ttu-id="d3fa3-117">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-117">OK</span></span>|<span data-ttu-id="d3fa3-118">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-118">OK</span></span>|<span data-ttu-id="d3fa3-119">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-119">OK</span></span>|<span data-ttu-id="d3fa3-120">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-120">OK</span></span>|
|<span data-ttu-id="d3fa3-121">Av2</span><span class="sxs-lookup"><span data-stu-id="d3fa3-121">Av2</span></span>||<span data-ttu-id="d3fa3-122">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-122">OK</span></span>|<span data-ttu-id="d3fa3-123">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-123">OK</span></span>|<span data-ttu-id="d3fa3-124">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-124">OK</span></span>|<span data-ttu-id="d3fa3-125">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-125">OK</span></span>|<span data-ttu-id="d3fa3-126">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-126">OK</span></span>|
|<span data-ttu-id="d3fa3-127">D</span><span class="sxs-lookup"><span data-stu-id="d3fa3-127">D</span></span>||<span data-ttu-id="d3fa3-128">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-128">OK</span></span>|<span data-ttu-id="d3fa3-129">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-129">OK</span></span>|<span data-ttu-id="d3fa3-130">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-130">OK</span></span>|<span data-ttu-id="d3fa3-131">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-131">OK</span></span>|<span data-ttu-id="d3fa3-132">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-132">OK</span></span>|
|<span data-ttu-id="d3fa3-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="d3fa3-133">Dv2</span></span>||<span data-ttu-id="d3fa3-134">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-134">OK</span></span>|<span data-ttu-id="d3fa3-135">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-135">OK</span></span>|<span data-ttu-id="d3fa3-136">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-136">OK</span></span>|<span data-ttu-id="d3fa3-137">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-137">OK</span></span>|<span data-ttu-id="d3fa3-138">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-138">OK</span></span>|
|<span data-ttu-id="d3fa3-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="d3fa3-139">Dv3</span></span>||<span data-ttu-id="d3fa3-140">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-140">OK</span></span>|<span data-ttu-id="d3fa3-141">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-141">OK</span></span>|<span data-ttu-id="d3fa3-142">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-142">OK</span></span>|<span data-ttu-id="d3fa3-143">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-143">OK</span></span>|<span data-ttu-id="d3fa3-144">TAMAM</span><span class="sxs-lookup"><span data-stu-id="d3fa3-144">OK</span></span>|

<span data-ttu-id="d3fa3-145">Diğer tüm serisi aynı kullanılabilirlik belirli donanım gerektirdiğinden kümesi içinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="d3fa3-145">All other series could not be in the same availability set because they require a specific hardware.</span></span>