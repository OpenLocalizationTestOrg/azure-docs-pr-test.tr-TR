---
title: "Azure Data Factory varlıklarını adlandırma aaaRules | Microsoft Docs"
description: "Data Factory varlıklarını için adlandırma kurallarını açıklar."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="9ff7e-103">Azure Data Factory - adlandırma kuralları</span><span class="sxs-lookup"><span data-stu-id="9ff7e-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="9ff7e-104">Aşağıdaki tablonun hello için Data Factory yapıtlarının adlandırma kuralları sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-104">hello following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="9ff7e-105">Ad</span><span class="sxs-lookup"><span data-stu-id="9ff7e-105">Name</span></span> | <span data-ttu-id="9ff7e-106">Ad benzersizliği</span><span class="sxs-lookup"><span data-stu-id="9ff7e-106">Name Uniqueness</span></span> | <span data-ttu-id="9ff7e-107">Doğrulama denetimleri</span><span class="sxs-lookup"><span data-stu-id="9ff7e-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9ff7e-108">Data Factory</span><span class="sxs-lookup"><span data-stu-id="9ff7e-108">Data Factory</span></span> |<span data-ttu-id="9ff7e-109">Microsoft Azure arasında benzersiz.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="9ff7e-110">Adları büyük küçük harf duyarsız, diğer bir deyişle, `MyDF` ve `mydf` toohello başvurmak aynı veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer toohello same data factory.</span></span> |<ul><li><span data-ttu-id="9ff7e-111">Her veri fabrikası bağlı tooexactly bir Azure aboneliği ' dir.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-111">Each data factory is tied tooexactly one Azure subscription.</span></span></li><li><span data-ttu-id="9ff7e-112">Nesne adları bir harf veya sayı ile başlamalı ve yalnızca harf, rakam ve tire (-) karakterinden hello içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-112">Object names must start with a letter or a number, and can contain only letters, numbers, and hello dash (-) character.</span></span></li><li><span data-ttu-id="9ff7e-113">Her tire (-) karakterinden hemen önünde ve bir harf veya sayı gelmelidir gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="9ff7e-114">Kapsayıcı adlarında art arda tirelere izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="9ff7e-115">Adı 3-63 karakter uzunluğunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="9ff7e-116">Bağlı hizmetler/tablolar/işlem hatları</span><span class="sxs-lookup"><span data-stu-id="9ff7e-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="9ff7e-117">Veri Fabrikası'nda ile benzersiz.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-117">Unique with in a data factory.</span></span> <span data-ttu-id="9ff7e-118">Adları büyük/küçük harfe duyarsızdır.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="9ff7e-119">Bir tablo adı karakter sayısı: 260.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="9ff7e-120">Nesne adları bir harf, sayı veya alt çizgi (_) ile başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="9ff7e-121">Şu karakterler kullanılamaz: ".", "+","?", "/", "<", ">","*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="9ff7e-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="9ff7e-122">Kaynak Grubu</span><span class="sxs-lookup"><span data-stu-id="9ff7e-122">Resource Group</span></span> |<span data-ttu-id="9ff7e-123">Microsoft Azure arasında benzersiz.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="9ff7e-124">Adları büyük/küçük harfe duyarsızdır.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="9ff7e-125">En fazla karakter sayısı: 1000.</span><span class="sxs-lookup"><span data-stu-id="9ff7e-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="9ff7e-126">Ad harf, rakam ve hello aşağıdaki karakterleri içerebilir: "-", "_",","ve"."</span><span class="sxs-lookup"><span data-stu-id="9ff7e-126">Name can contain letters, digits, and hello following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

