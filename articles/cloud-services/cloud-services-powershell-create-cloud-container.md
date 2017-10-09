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
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="3bdd6-104">Bir Azure PowerShell komut toocreate boş bulut hizmeti kapsayıcısını kullanın</span><span class="sxs-lookup"><span data-stu-id="3bdd6-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="3bdd6-105">Bu makalede, Azure PowerShell cmdlet'lerini kullanarak bir bulut Hizmetleri kapsayıcı tooquickly oluşturma nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3bdd6-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3bdd6-106">Lütfen başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3bdd6-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="3bdd6-107">Hello Hello Microsoft Azure PowerShell cmdlet yükleme [Azure PowerShell indirmeleri](http://aka.ms/webpi-azps) sayfası.</span><span class="sxs-lookup"><span data-stu-id="3bdd6-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="3bdd6-108">Merhaba PowerShell komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="3bdd6-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="3bdd6-109">Kullanım hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign içinde.</span><span class="sxs-lookup"><span data-stu-id="3bdd6-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3bdd6-110">Hello Azure PowerShell cmdlet yükleme ve tooyour Azure aboneliğine bağlanma hakkında daha fazla yönerge için çok başvuran[nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3bdd6-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="3bdd6-111">Kullanım hello **New-AzureService** cmdlet toocreate boş Azure bulut hizmeti kapsayıcısını.</span><span class="sxs-lookup"><span data-stu-id="3bdd6-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="3bdd6-112">Bu örnek tooinvoke hello cmdlet izleyin:</span><span class="sxs-lookup"><span data-stu-id="3bdd6-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="3bdd6-113">Hello Azure bulut hizmeti oluşturma hakkında daha fazla bilgi için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3bdd6-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="3bdd6-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3bdd6-114">Next steps</span></span>
* <span data-ttu-id="3bdd6-115">toomanage hello bulut hizmeti dağıtımı, toohello başvuran [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), ve [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) komutları.</span><span class="sxs-lookup"><span data-stu-id="3bdd6-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="3bdd6-116">Ayrıca çok başvurabilir[nasıl tooconfigure bulut hizmetlerini](cloud-services-how-to-configure.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3bdd6-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="3bdd6-117">toopublish bulut hizmetiniz tooAzure projesi, toohello başvuran **PublishCloudService.ps1** kod örnekten [Azure'daki bulut hizmeti için kesintisiz teslim](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="3bdd6-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
