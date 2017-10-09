---
title: "aaaDelete Azure küme ve kaynaklarına | Microsoft Docs"
description: "Toocompletely delete Service Fabric küme nasıl hello küme içeren ya da silme hello kaynak grubunu veya kaynakları seçmeli silme tarafından öğrenin."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Azure ve hello kaynaklarına kullandığı Service Fabric kümesini Sil
Service Fabric kümesi diğer Azure birçok kaynakları toohello küme kaynağı kendisi ayrıca oluşur. Toocompletely silmek için Service Fabric kümesi tüm kaynakları, yapılan hello toodelete de olması gerekir.
İki seçeneğiniz vardır: küme hello ya da delete hello kaynak grubu (silen hello küme kaynağı ve hello kaynak grubundaki diğer kaynaklar) veya özellikle hello küme kaynağı siler ve ilişkili kaynakları (ancak diğer değil kaynakları hello kaynak grubunda).

> [!NOTE]
> Merhaba küme kaynağı silme **yok** tüm hello Service Fabric kümesi oluşan diğer kaynakları silin.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>Service Fabric kümesinin hello hello tüm kaynak grubu (RG) silme
Merhaba, kümeniz hello kaynak grubu dahil olmak üzere, ilişkili tüm hello kaynakları silmek en kolay yolu tooensure budur. PowerShell kullanarak hello kaynak grubunu silebilirsiniz veya hello Azure portal aracılığıyla. Ardından ilgili tooService fabric kümesi olmayan kaynakları kaynak grubunuz varsa, belirli kaynaklara silebilirsiniz.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Azure PowerShell kullanarak hello kaynak grubunu silme
Azure PowerShell cmdlet'lerini aşağıdaki hello çalıştırarak hello kaynak grubunu da silebilirsiniz. Büyük bilgisayarınızda yüklü veya Azure PowerShell 1.0 emin olun. Daha önceden yapmadıysanız özetlenen hello adımları [nasıl tooinstall ve Azure PowerShell yapılandırın.](/powershell/azure/overview)

Bir PowerShell penceresi açın ve PS cmdlet'leri aşağıdaki hello çalıştırın:

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

Hello kullanmadıysanız, bir komut istemi tooconfirm hello silme işlemi hatalarla *-Force* seçeneği. RG üzerinde onay hello ve içerdiği tüm hello kaynaklar silinir.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Hello Azure portalında bir kaynak grubunda Sil
1. Oturum açma toohello [Azure portal](https://portal.azure.com).
2. Toodelete istediğiniz toohello Service Fabric kümesi gidin.
3. Merhaba üzerinde hello küme essentials sayfasında kaynak grubu adını tıklatın.
4. Bu hello getirir **kaynak grubu Essentials** sayfası.
5. **Sil**'e tıklayın.
6. Bu sayfa toocomplete hello hello kaynak grubunun silinmesi üzerinde Hello yönergeleri izleyin.

![Kaynak Grubu Sil][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>Merhaba küme kaynağı ve hello kaynakları kullanır, ancak diğer kaynakları değil hello kaynak grubunda Sil
İlgili toohello Service Fabric kümesi olan kaynakları kaynak grubunuz varsa, toodelete istediğiniz sonra daha kolay toodelete hello tüm kaynak grubu değil. Kaynak grubunda tooselectively delete hello kaynakları tek tek istiyorsanız, aşağıdaki adımları izleyin.

Hello portal veya hello Şablon Galerisi'nden hello Service Fabric Resource Manager şablonlarından birini kullanarak kümenizi dağıtılmışsa, küme kullanan hello tüm hello kaynakları iki etiket aşağıdaki hello ile etiketlenir. Hangi kaynaklara istediğiniz toodecide kullanabilirsiniz toodelete.

***#1 etiketi:*** anahtarı clusterName, değer = 'hello küme adı' =

***#2 etiketi:*** anahtarı KaynakAdı, değer = ServiceFabric =

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Hello Azure portal'ın belirli kaynakları silin
1. Oturum açma toohello [Azure portal](https://portal.azure.com).
2. Toodelete istediğiniz toohello Service Fabric kümesi gidin.
3. Çok Git**tüm ayarları** hello essentials dikey.
4. Tıklayın **etiketleri** altında **kaynak yönetimi** hello ayarlar dikey penceresinde.
5. Merhaba birini tıklatın **etiketleri** hello etiketleri dikey tooget bu etikete sahip tüm hello kaynakların bir listesini içinde.
   
    ![Kaynak Etiketleri][ResourceTags]
6. Etiketli kaynakları hello listesine sahip olduktan sonra her hello kaynaklar'ı tıklatın ve silebilirsiniz.
   
    ![Etiketli kaynakları][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Azure PowerShell kullanarak hello kaynakları silin
Azure PowerShell cmdlet'lerini aşağıdaki hello çalıştırarak hello kaynaklarını tek tek silebilirsiniz. Büyük bilgisayarınızda yüklü veya Azure PowerShell 1.0 emin olun. Daha önceden yapmadıysanız özetlenen hello adımları [nasıl tooinstall ve Azure PowerShell yapılandırın.](/powershell/azure/overview)

Bir PowerShell penceresi açın ve PS cmdlet'leri aşağıdaki hello çalıştırın:

```powershell
Login-AzureRmAccount
```
Merhaba kaynakların her biri için toodelete istediğiniz, hello aşağıdaki komutu çalıştırın:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

Merhaba aşağıdaki komutu çalıştırarak toodelete hello küme kaynağı:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>Sonraki adımlar
Tooalso aşağıdaki okuma hello Küme yükseltme ve Hizmetleri bölümleme hakkında bilgi edinin:

* [Küme yükseltme hakkında bilgi edinin](service-fabric-cluster-upgrade.md)
* [En fazla ölçek için durum bilgisi olan hizmetler bölümleme hakkında bilgi edinin](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
