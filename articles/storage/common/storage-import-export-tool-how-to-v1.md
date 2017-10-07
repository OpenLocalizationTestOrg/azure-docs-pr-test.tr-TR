---
title: "aaaUsing hello Azure içeri/dışarı aktarma aracı - v1 | Microsoft Docs"
description: "Nasıl toouse hello içeri/dışarı aktarma aracı tooprepare sabit sürücüler içeri aktarma işi için bir alma işi onarmak veya bir dışarı aktarma işinin onarın öğrenin."
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
ms.openlocfilehash: 030dbad403cae76799c9ddf3cb8d2ced7cd41911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-tool-classic-deployment-model"></a><span data-ttu-id="9c802-103">Hello Azure içeri/dışarı aktarma Aracı (Klasik dağıtım modeli) kullanma</span><span class="sxs-lookup"><span data-stu-id="9c802-103">Using hello Azure Import/Export Tool (classic deployment model)</span></span>

<span data-ttu-id="9c802-104">Hello Azure içeri/dışarı aktarma Aracı (WAImportExport.exe) kullanılan toocreate olan ve içine veya dışına Azure Blob Storage tootransfer büyük miktarlarda verinin etkinleştirme hello Azure içeri/dışarı aktarma hizmeti işleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="9c802-104">hello Azure Import/Export Tool (WAImportExport.exe) is used toocreate and manage jobs for hello Azure Import/Export service, enabling you tootransfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="9c802-105">Bu belge için hello Azure içeri/dışarı aktarma aracı hello Klasik dağıtım modelini ' dir.</span><span class="sxs-lookup"><span data-stu-id="9c802-105">This documentation is for hello classic deployment model of hello Azure Import/Export Tool.</span></span> <span data-ttu-id="9c802-106">Merhaba aracının en son sürümünü hello kullanma hakkında daha fazla bilgi için bkz: [kullanma hello Azure içeri/dışarı aktarma aracı](../storage-import-export-tool-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="9c802-106">For information about using hello most recent version of hello tool, see [Using hello Azure Import/Export Tool](../storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="9c802-107">Merhaba aşağıdaki makalelere şunları nasıl yapacağınızı için:</span><span class="sxs-lookup"><span data-stu-id="9c802-107">hello following articles show you how to:</span></span>

- <span data-ttu-id="9c802-108">Yükleme ve içeri/dışarı aktarma aracı hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9c802-108">Install and set up hello Import/Export Tool.</span></span>
- <span data-ttu-id="9c802-109">Sabit sürücüler, veri sürücüleri tooAzure Blob Depolama burada aldığınız bir iş için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="9c802-109">Prepare your hard drives for a job where you import data from your drives tooAzure Blob Storage.</span></span>
- <span data-ttu-id="9c802-110">Bir işin Hello durumu ile kopyalama günlük dosyalarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="9c802-110">Review hello status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="9c802-111">İçe aktarma işi onarın.</span><span class="sxs-lookup"><span data-stu-id="9c802-111">Repair an import job.</span></span> 
- <span data-ttu-id="9c802-112">Bir dışarı aktarma işinin onarın.</span><span class="sxs-lookup"><span data-stu-id="9c802-112">Repair an export job.</span></span> 
- <span data-ttu-id="9c802-113">İşlemi sırasında bir sorun oluştu durumda hello Azure içeri/dışarı aktarma aracı sorunlarını giderin.</span><span class="sxs-lookup"><span data-stu-id="9c802-113">Troubleshoot hello Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9c802-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c802-114">Next steps</span></span>

* [<span data-ttu-id="9c802-115">Merhaba WAImportExport aracı ayarlama</span><span class="sxs-lookup"><span data-stu-id="9c802-115">Setting up hello WAImportExport tool</span></span>](../storage-import-export-tool-how-to.md)
