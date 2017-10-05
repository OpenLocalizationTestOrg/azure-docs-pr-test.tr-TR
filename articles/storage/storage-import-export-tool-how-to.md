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
ms.openlocfilehash: 86073f5d15253d658fcb371e913dd3a543a2b075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-tool"></a>Azure içeri/dışarı aktarma Aracı'nı kullanma 

Azure içeri/dışarı aktarma Aracı'nı (WAImportExport.exe), böylece içine veya dışına Azure Blob Storage büyük miktarlarda veri aktarmak Azure içeri/dışarı aktarma hizmeti işleri oluşturmak ve yönetmek için kullanılır.

Bu belge en son Azure içeri/dışarı aktarma aracı için sürümüdür. V1 aracını kullanma hakkında daha fazla bilgi için lütfen bkz [Azure içeri/dışarı aktarma aracı v1 kullanarak](storage-import-export-tool-how-to-v1.md).

Bu makalelerde, aşağıdakileri yapmak için bu aracı kullanmak nasıl görürsünüz:  

- Yükleyin ve içeri/dışarı aktarma aracı ayarlamak.
- Burada, sürücülerden verileri Azure Blob depolama alanına içeri bir iş için sabit sürücüler hazırlayın.
- Bir işin durumu ile kopyalama günlük dosyalarını inceleyin. 
- İçe aktarma işi onarın. 
- Bir dışarı aktarma işinin onarın. 
- İşlemi sırasında bir sorun oluştu durumunda Azure içeri/dışarı aktarma aracı sorunlarını giderin. 

## <a name="next-steps"></a>Sonraki adımlar

* [WAImportExport Aracı'nı ayarlama](storage-import-export-tool-setup.md)