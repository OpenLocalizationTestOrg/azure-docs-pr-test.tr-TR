---
title: "aaaTroubleshoot Azure sanal ağ geçidi ve bağlantıları - Azure CLI 2.0 | Microsoft Docs"
description: "Bu sayfayı toouse hello Azure Ağ İzleyicisi Azure CLI 2.0 nasıl sorun giderme açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a>Sanal ağ geçidi ve Azure Ağ İzleyicisi Azure CLI 2.0 kullanarak bağlantı sorunlarını giderme

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

Ağ kaynaklarınızı Azure toounderstanding ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar. Bu özelliklerin biri kaynak sorun giderme. Kaynak sorun giderme hello portal, PowerShell'i, CLI veya REST API çağrılabilir. Çağrıldığında, Ağ İzleyicisi Merhaba bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.

Bu makalede bizim nesil CLI hello kaynak yönetimi dağıtım modeli için Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.

Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Genel Bakış

Kaynak sorun giderme hello yeteneği sağlar sanal ağ geçitleri ve bağlantılarla ortaya çıkan sorunları giderme. Bir istek tooresource sorun giderme yapıldığında günlükleri yükleniyor sorgulanan ve sahip denetlenir. İnceleme tamamlandığında hello sonuçlar döndürülür. Hangi birden çok dakika tooreturn bir sonuç ele geçirebilir sorun giderme istekleri uzun süredir çalışıp kaynak ister. sorun giderme gelen hello günlükleri, belirtilen bir depolama hesabı üzerinde bir kapsayıcıda depolanır.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Sanal ağ geçidi bağlantısı alma

Bu örnekte, kaynak sorun giderme olduğu olan tükendi bağlantı üzerinde. Ayrıca bir sanal ağ geçidi geçirebilirsiniz. Merhaba aşağıdaki cmdlet'i bir kaynak grubunda hello vpn bağlantılarını listeler.

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

Hello bağlantısının hello adına sahip olduğunda, kendi kaynak kimliği bu komut tooget çalıştırabilirsiniz:

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma

Kaynak sorun giderme hello kaynak hello durumunu ilgili verileri döndürür, günlükleri tooa depolama hesabı toobe gözden de kaydeder. Bu adımda, biz depolama hesabı oluşturma, depolama hesabınız varsa bunu kullanabilirsiniz.

1. Merhaba depolama hesabı oluşturma

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. Merhaba depolama hesabı anahtarlarını alma

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. Merhaba kapsayıcı oluşturma

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Ağ İzleyicisi kaynak sorun giderme çalıştırın

Merhaba kaynaklarla ilgili sorunları giderme `az network watcher troubleshooting` cmdlet'i. Biz hello cmdlet hello kaynak grubu geçirebilir, hello hello Ağ İzleyicisi, hello hello bağlantının kimliği adını hello hello depolama hesabının kimliğini ve hello yolu toohello blob toostore hello sonuçlarında sorun giderme.

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

Merhaba cmdlet'ini çalıştırdıktan sonra Ağ İzleyicisi Merhaba kaynak tooverify hello durumu inceler. Toohello Kabuk hello sonuçlar döndürür ve belirtilen hello depolama hesabında günlüklerini hello sonuçlarını kaydeder.

## <a name="understanding-hello-results"></a>Merhaba sonuçlarını anlama

Merhaba eylem metni nasıl tooresolve hello üzerinde sorunu genel rehberlik sağlar. Bir eylemin hello sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır. Merhaba durumda hiçbir ek yönergeler olduğu hello yanıt hello url tooopen bir destek servis talebi sağlar..  Merhaba yanıt ve dahil edilen nedir hello özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)

Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için çok başvuran[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Kullanılabilir başka bir Depolama Gezgini aracıdır. Depolama Gezgini hakkında daha fazla bilgi bağlantısı aşağıdaki hello şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)

## <a name="next-steps"></a>Sonraki adımlar

Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.
