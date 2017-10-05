---
title: "Azure içeri/dışarı aktarma Aracı'nı kullanma | Microsoft Docs"
description: "İçeri/dışarı aktarma aracı sabit sürücüler için içeri aktarma işi hazırlama, içe aktarma işi onarmak veya bir dışarı aktarma işinin onarmak için nasıl kullanılacağını öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 20a720833842f9579fd4fccaa39e964def48197e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-tool"></a><span data-ttu-id="87205-103">Azure içeri/dışarı aktarma Aracı'nı kullanma</span><span class="sxs-lookup"><span data-stu-id="87205-103">Using the Azure Import/Export Tool</span></span> 

<span data-ttu-id="87205-104">Azure içeri/dışarı aktarma Aracı'nı (WAImportExport.exe), böylece içine veya dışına Azure Blob Storage büyük miktarlarda veri aktarmak Azure içeri/dışarı aktarma hizmeti işleri oluşturmak ve yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="87205-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="87205-105">Bu belge en son Azure içeri/dışarı aktarma aracı için sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="87205-105">This documentation is for the most recent version of the Azure Import/Export Tool.</span></span> <span data-ttu-id="87205-106">Klasik dağıtım modeli kullanma hakkında daha fazla bilgi için bkz: [Azure içeri/dışarı aktarma aracı v1 kullanarak](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="87205-106">For information about using the classic deployment model, see [Using the Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="87205-107">Aşağıdaki makaleler şunları nasıl yapacağınızı için:</span><span class="sxs-lookup"><span data-stu-id="87205-107">The following articles show you how to:</span></span>  

- <span data-ttu-id="87205-108">Yükleyin ve Azure içeri/dışarı aktarma aracı ayarlamak.</span><span class="sxs-lookup"><span data-stu-id="87205-108">Install and set up the Azure Import/Export Tool.</span></span>
- <span data-ttu-id="87205-109">Burada, sürücülerden verileri Azure Blob depolama alanına içeri bir iş için sabit sürücüler hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="87205-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="87205-110">Bir işin durumu ile kopyalama günlük dosyalarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="87205-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="87205-111">İçe aktarma işi onarın.</span><span class="sxs-lookup"><span data-stu-id="87205-111">Repair an import job.</span></span> 
- <span data-ttu-id="87205-112">Bir dışarı aktarma işinin onarın.</span><span class="sxs-lookup"><span data-stu-id="87205-112">Repair an export job.</span></span> 
- <span data-ttu-id="87205-113">Azure içeri/dışarı aktarma aracı sorunlarını giderin.</span><span class="sxs-lookup"><span data-stu-id="87205-113">Troubleshoot the Azure Import/Export Tool.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="87205-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="87205-114">Next steps</span></span>

* [<span data-ttu-id="87205-115">WAImportExport Aracı'nı ayarlama</span><span class="sxs-lookup"><span data-stu-id="87205-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-setup.md)