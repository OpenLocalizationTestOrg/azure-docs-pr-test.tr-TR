---
title: "aaaManage Hadoop kümeleri Azure CLI - Azure Hdınsight kullanma | Microsoft Docs"
description: "Azure Hdınsight'ta nasıl toouse hello Azure komut satırı arabirimi toomanage Hadoop kümeleri hakkında bilgi edinin. Hello Azure CLI, Windows, Mac ve Linux üzerinde çalışır."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Hello Azure CLI kullanarak hdınsight'ta Hadoop kümelerini yönetme
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Bilgi nasıl toouse hello [Azure komut satırı arabirimi](../cli-install-nodejs.md) Azure Hdınsight'ta toomanage Hadoop kümeleri. Hello Azure CLI, Node.js içinde uygulanmıştır. Windows, Mac ve Linux da dahil olmak üzere, Node.js'yi destekleyen herhangi bir platformda kullanılabilir.

Bu makalede, yalnızca Hdınsight ile hello Azure CLI kullanarak yer almaktadır. Nasıl genel bir kılavuz için toouse Azure CLI bkz [yükleyin ve Azure CLI yapılandırma][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure CLI** -bkz [yükleme ve yapılandırma hello Azure CLI](../cli-install-nodejs.md) yükleme ve yapılandırma bilgileri için.
* **TooAzure bağlanmak**kullanarak hello komutu:
  
        azure login
  
    Bir iş veya Okul hesabı kullanarak kimlik doğrulaması ile ilgili daha fazla bilgi için bkz: [tooan Azure aboneliği hello Azure CLI ' bağlanma](../xplat-cli-connect.md).
* **Anahtar toohello Azure Resource Manager moduna**kullanarak hello komutu:
  
        azure config mode arm

tooget Yardımını kullanma hello **-h** geçin.  Örneğin:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>CLI hello ile kümeleri oluşturma
Bkz: [kullanarak Hdınsight'ta oluşturma kümeleri hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Liste ve küme ayrıntıları göster
Aşağıdaki komutları toolist hello kullanın ve küme ayrıntıları göster:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Komut satırı görünümünü küme listesi][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Küme silme
Komut toodelete bir küme aşağıdaki hello kullan:

    azure hdinsight cluster delete <Cluster Name>

Bir küme hello küme içeren hello kaynak grubunu silerek silebilirsiniz. Lütfen unutmayın, bu hello varsayılan depolama hesabı dahil olmak üzere hello grubundaki tüm hello kaynaklarını siler.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Kümeleri ölçeklendirme
toochange hello Hadoop küme boyutu:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Bir küme için HTTP erişimi etkinleştir/devre dışı bırak
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Bir küme için RDP erişimini etkinleştir/devre dışı bırak
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, öğrendiğiniz nasıl tooperform farklı Hdınsight küme yönetim görevleri. toolearn daha makaleler hello bakın:

* [Hdınsight hello Azure Portal kullanarak yönetme][hdinsight-admin-portal]
* [Hdınsight Azure PowerShell kullanarak yönetme][hdinsight-admin-powershell]
* [Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]
* [Nasıl toouse hello Azure CLI][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Liste ve kümeleri Göster"
