---
title: "PowerShell ile bir bulut hizmeti kapsayıcısını aaaCreate | Microsoft Docs"
description: "Bu makalede nasıl toocreate bir bulut hizmeti kapsayıcısını PowerShell ile açıklanmaktadır. Merhaba kapsayıcı web ve çalışan rollerini barındırır."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Bir Azure PowerShell komut toocreate boş bulut hizmeti kapsayıcısını kullanın
Bu makalede, Azure PowerShell cmdlet'lerini kullanarak bir bulut Hizmetleri kapsayıcı tooquickly oluşturma nasıl açıklanmaktadır. Lütfen başlangıç adımları izleyin:

1. Hello Hello Microsoft Azure PowerShell cmdlet yükleme [Azure PowerShell indirmeleri](http://aka.ms/webpi-azps) sayfası.
2. Merhaba PowerShell komut istemi açın.
3. Kullanım hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign içinde.

   > [!NOTE]
   > Hello Azure PowerShell cmdlet yükleme ve tooyour Azure aboneliğine bağlanma hakkında daha fazla yönerge için çok başvuran[nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
   >
   >
4. Kullanım hello **New-AzureService** cmdlet toocreate boş Azure bulut hizmeti kapsayıcısını.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Bu örnek tooinvoke hello cmdlet izleyin:

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Hello Azure bulut hizmeti oluşturma hakkında daha fazla bilgi için çalıştırın:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Sonraki adımlar
* toomanage hello bulut hizmeti dağıtımı, toohello başvuran [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), ve [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) komutları. Ayrıca çok başvurabilir[nasıl tooconfigure bulut hizmetlerini](cloud-services-how-to-configure.md) daha fazla bilgi için.
* toopublish bulut hizmetiniz tooAzure projesi, toohello başvuran **PublishCloudService.ps1** kod örnekten [Azure'daki bulut hizmeti için kesintisiz teslim](cloud-services-dotnet-continuous-delivery.md).
