---
title: "aaaHow toodelete Hdınsight kümesi - Azure | Microsoft Docs"
description: "Merhaba Hdınsight kümesi silebilmek için çeşitli yollar hakkında bilgiler."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>Tarayıcı, PowerShell veya hello Azure CLI kullanarak bir Hdınsight kümesi Sil

Hdınsight küme faturalandırma bir küme oluşturulur ve hello küme silindiğinde durdurur sonra başlar. Artık kullanımda olmadığında, küme her zaman silmelisiniz Faturalaması dakika başına Faturalaması olduğundan. Bu belgede, kullanarak bir küme toodelete nasıl hello Azure portalı, Azure PowerShell ve Azure CLI 1.0 hello öğrenin.

> [!IMPORTANT]
> Bir Hdınsight kümesi siliniyor hello Azure depolama hesapları silmez veya Data Lake Store hello kümesi ile ilişkili. Bu hizmetlerin gelecekteki hello içinde depolanan verileri yeniden kullanabilirsiniz.

## <a name="azure-portal"></a>Azure portalına

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) ve Hdınsight kümenize seçin. Hdınsight kümenize sabitlenmiş toohello Pano değilse, bunun için hello arama alanı kullanarak ada göre arama yapabilirsiniz.
   
    ![Portal arama](./media/hdinsight-delete-cluster/navbar.png)

2. Merhaba küme için Hello dikey pencere açılır sonra hello seçeneğini **silmek** simgesi. İstendiğinde, seçin **Evet** toodelete hello küme.
   
    ![Sil simgesi](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

Bir PowerShell isteminden komutu toodelete hello küme aşağıdaki hello kullan:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Değiştir **CLUSTERNAME** Hdınsight kümenize hello adı.

## <a name="azure-cli-10"></a>Azure CLI 1.0

Bir isteminden toodelete hello küme aşağıdaki hello kullan:

    azure hdinsight cluster delete CLUSTERNAME

Değiştir **CLUSTERNAME** Hdınsight kümenize hello adı.

> [!NOTE]
> Azure CLI 2.0 silme Hdınsight kümeleri şu anda (31 Temmuz 2017) desteklemez.