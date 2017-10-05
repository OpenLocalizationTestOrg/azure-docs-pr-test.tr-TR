---
title: "Azure içeri/dışarı aktarma aracı - v1 kullanarak | Microsoft Docs"
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
ms.date: 1/15/2017
ms.author: muralikk
ms.openlocfilehash: 67bdfa8c2cd0f8314c82e2b334a3fa3a5c520c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-tool-v1"></a><span data-ttu-id="b08a2-103">Azure içeri/dışarı aktarma Aracı'nı (v1) kullanma</span><span class="sxs-lookup"><span data-stu-id="b08a2-103">Using the Azure Import/Export Tool (v1)</span></span>

<span data-ttu-id="b08a2-104">Azure içeri/dışarı aktarma Aracı'nı (WAImportExport.exe), böylece içine veya dışına Azure Blob Storage büyük miktarlarda veri aktarmak Azure içeri/dışarı aktarma hizmeti işleri oluşturmak ve yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b08a2-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="b08a2-105">Azure içeri/dışarı aktarma aracı v1 için belgesidir.</span><span class="sxs-lookup"><span data-stu-id="b08a2-105">This documentation is for v1 of the Azure Import/Export Tool.</span></span> <span data-ttu-id="b08a2-106">Aracın en son sürümünü kullanma hakkında daha fazla bilgi için lütfen bkz [Azure içeri/dışarı aktarma aracını kullanarak](storage-import-export-tool-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="b08a2-106">For information about using the most recent version of the tool, please see [Using the Azure Import/Export Tool](storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="b08a2-107">Bu makalelerde, aşağıdakileri yapmak için bu aracı kullanmak nasıl görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="b08a2-107">In these articles, you will see how to use the tool to do the following:</span></span>

- <span data-ttu-id="b08a2-108">Yükleyin ve içeri/dışarı aktarma aracı ayarlamak.</span><span class="sxs-lookup"><span data-stu-id="b08a2-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="b08a2-109">Burada, sürücülerden verileri Azure Blob depolama alanına içeri bir iş için sabit sürücüler hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="b08a2-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="b08a2-110">Bir işin durumu ile kopyalama günlük dosyalarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="b08a2-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="b08a2-111">İçe aktarma işi onarın.</span><span class="sxs-lookup"><span data-stu-id="b08a2-111">Repair an import job.</span></span> 
- <span data-ttu-id="b08a2-112">Bir dışarı aktarma işinin onarın.</span><span class="sxs-lookup"><span data-stu-id="b08a2-112">Repair an export job.</span></span> 
- <span data-ttu-id="b08a2-113">İşlemi sırasında bir sorun oluştu durumunda Azure içeri/dışarı aktarma aracı sorunlarını giderin.</span><span class="sxs-lookup"><span data-stu-id="b08a2-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b08a2-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b08a2-114">Next steps</span></span>

* [<span data-ttu-id="b08a2-115">WAImportExport Aracı'nı ayarlama</span><span class="sxs-lookup"><span data-stu-id="b08a2-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-how-to.md)