---
title: "Azure VM'ler tooan varolan kullanılabilirlik kümesi ekleme aaaSupportability | Microsoft Docs"
description: "Azure VM'ler tooan varolan kullanılabilirlik kümesi ekleme desteklenebilirlik."
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
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="ca317-103">Azure VM'ler tooan varolan kullanılabilirlik kümesi ekleme desteklenebilirlik</span><span class="sxs-lookup"><span data-stu-id="ca317-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="ca317-104">Yeni sanal makineleri (VM'ler) tooan varolan kullanılabilirlik kümesi eklediğinizde sınırlamaları bazen karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca317-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="ca317-105">Merhaba aşağıdaki ayrıntıları karıştırabilir miyim hangi VM dizisi aynı kullanılabilirlik kümesinde hello grafik.</span><span class="sxs-lookup"><span data-stu-id="ca317-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="ca317-106">Merhaba desteklenebilirlik matris toomix farklı türlerde VM'ler şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ca317-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="ca317-107">Seri & kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="ca317-107">Series & Availability Set</span></span>|<span data-ttu-id="ca317-108">İkinci VM</span><span class="sxs-lookup"><span data-stu-id="ca317-108">Second VM</span></span>|<span data-ttu-id="ca317-109">A</span><span class="sxs-lookup"><span data-stu-id="ca317-109">A</span></span>|<span data-ttu-id="ca317-110">Av2</span><span class="sxs-lookup"><span data-stu-id="ca317-110">Av2</span></span>|<span data-ttu-id="ca317-111">D</span><span class="sxs-lookup"><span data-stu-id="ca317-111">D</span></span>|<span data-ttu-id="ca317-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="ca317-112">Dv2</span></span>|<span data-ttu-id="ca317-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="ca317-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="ca317-114">İlk VM</span><span class="sxs-lookup"><span data-stu-id="ca317-114">First VM</span></span>|||||||
|<span data-ttu-id="ca317-115">A</span><span class="sxs-lookup"><span data-stu-id="ca317-115">A</span></span>||<span data-ttu-id="ca317-116">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-116">OK</span></span>|<span data-ttu-id="ca317-117">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-117">OK</span></span>|<span data-ttu-id="ca317-118">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-118">OK</span></span>|<span data-ttu-id="ca317-119">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-119">OK</span></span>|<span data-ttu-id="ca317-120">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-120">OK</span></span>|
|<span data-ttu-id="ca317-121">Av2</span><span class="sxs-lookup"><span data-stu-id="ca317-121">Av2</span></span>||<span data-ttu-id="ca317-122">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-122">OK</span></span>|<span data-ttu-id="ca317-123">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-123">OK</span></span>|<span data-ttu-id="ca317-124">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-124">OK</span></span>|<span data-ttu-id="ca317-125">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-125">OK</span></span>|<span data-ttu-id="ca317-126">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-126">OK</span></span>|
|<span data-ttu-id="ca317-127">D</span><span class="sxs-lookup"><span data-stu-id="ca317-127">D</span></span>||<span data-ttu-id="ca317-128">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-128">OK</span></span>|<span data-ttu-id="ca317-129">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-129">OK</span></span>|<span data-ttu-id="ca317-130">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-130">OK</span></span>|<span data-ttu-id="ca317-131">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-131">OK</span></span>|<span data-ttu-id="ca317-132">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-132">OK</span></span>|
|<span data-ttu-id="ca317-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="ca317-133">Dv2</span></span>||<span data-ttu-id="ca317-134">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-134">OK</span></span>|<span data-ttu-id="ca317-135">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-135">OK</span></span>|<span data-ttu-id="ca317-136">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-136">OK</span></span>|<span data-ttu-id="ca317-137">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-137">OK</span></span>|<span data-ttu-id="ca317-138">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-138">OK</span></span>|
|<span data-ttu-id="ca317-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="ca317-139">Dv3</span></span>||<span data-ttu-id="ca317-140">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-140">OK</span></span>|<span data-ttu-id="ca317-141">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-141">OK</span></span>|<span data-ttu-id="ca317-142">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-142">OK</span></span>|<span data-ttu-id="ca317-143">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-143">OK</span></span>|<span data-ttu-id="ca317-144">TAMAM</span><span class="sxs-lookup"><span data-stu-id="ca317-144">OK</span></span>|

<span data-ttu-id="ca317-145">Diğer tüm serisi hello belirli donanım gerektirdiğinden aynı kullanılabilirlik kümesi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ca317-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
