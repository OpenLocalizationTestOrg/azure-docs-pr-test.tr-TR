---
title: Azure Blob depolama biriminden aaaMove veri tooand | Microsoft Docs
description: "Azure Blob depolama alanından veri tooand Taşı"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a>Azure Blob depolama alanından veri tooand Taşı
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Hangi sizin için en iyi bir yöntemdir, senaryoya bağlıdır. Merhaba [senaryoları Azure Machine Learning, gelişmiş analizler için](machine-learning-data-science-plan-sample-scenarios.md) makale ihtiyacınız analytics işlem Gelişmiş hello kullanılan veri bilimi iş akışları çeşitli hello kaynakları belirlemenize yardımcı olur.

> [!NOTE]
> Bir tam giriş tooAzure blob depolama çok başvuran[Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve çok[Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

Alternatif olarak, kullandığınız [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) için: 

* oluşturun ve veriler Azure blob depolama alanından yükler ardışık zamanlama 
* Bunu iletirsiniz tooa yayımlanan Azure Machine Learning web hizmeti 
* Merhaba Tahmine dayalı analiz sonuçlarını almak ve 
* Merhaba sonuçları toostorage karşıya yükleyin. 

Daha fazla bilgi için bkz: [Azure Data Factory ve Azure Machine Learning kullanarak Tahmine dayalı işlem hatlarını oluşturmak](../data-factory/data-factory-azure-ml-batch-execution-activity.md).

## <a name="prerequisites"></a>Ön koşullar
Bu belge, Azure aboneliği bir depolama hesabı ve o hesap için karşılık gelen depolama anahtar hello sahip olduğunuzu varsayar. Karşıya yükleme/veri yüklemeden önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.

* bir Azure aboneliği yukarı tooset bkz [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).
* Bir depolama hesabı oluşturma hakkında yönergeler ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).

