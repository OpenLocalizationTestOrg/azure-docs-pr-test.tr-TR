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
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="3ce5e-103">Azure ve hello kaynaklarına kullandığı Service Fabric kümesini Sil</span><span class="sxs-lookup"><span data-stu-id="3ce5e-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="3ce5e-104">Service Fabric kümesi diğer Azure birçok kaynakları toohello küme kaynağı kendisi ayrıca oluşur.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="3ce5e-105">Toocompletely silmek için Service Fabric kümesi tüm kaynakları, yapılan hello toodelete de olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="3ce5e-106">İki seçeneğiniz vardır: küme hello ya da delete hello kaynak grubu (silen hello küme kaynağı ve hello kaynak grubundaki diğer kaynaklar) veya özellikle hello küme kaynağı siler ve ilişkili kaynakları (ancak diğer değil kaynakları hello kaynak grubunda).</span><span class="sxs-lookup"><span data-stu-id="3ce5e-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="3ce5e-107">Merhaba küme kaynağı silme **yok** tüm hello Service Fabric kümesi oluşan diğer kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="3ce5e-108">Service Fabric kümesinin hello hello tüm kaynak grubu (RG) silme</span><span class="sxs-lookup"><span data-stu-id="3ce5e-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="3ce5e-109">Merhaba, kümeniz hello kaynak grubu dahil olmak üzere, ilişkili tüm hello kaynakları silmek en kolay yolu tooensure budur.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="3ce5e-110">PowerShell kullanarak hello kaynak grubunu silebilirsiniz veya hello Azure portal aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="3ce5e-111">Ardından ilgili tooService fabric kümesi olmayan kaynakları kaynak grubunuz varsa, belirli kaynaklara silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="3ce5e-112">Azure PowerShell kullanarak hello kaynak grubunu silme</span><span class="sxs-lookup"><span data-stu-id="3ce5e-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="3ce5e-113">Azure PowerShell cmdlet'lerini aşağıdaki hello çalıştırarak hello kaynak grubunu da silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3ce5e-114">Büyük bilgisayarınızda yüklü veya Azure PowerShell 1.0 emin olun.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="3ce5e-115">Daha önceden yapmadıysanız özetlenen hello adımları [nasıl tooinstall ve Azure PowerShell yapılandırın.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="3ce5e-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="3ce5e-116">Bir PowerShell penceresi açın ve PS cmdlet'leri aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3ce5e-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="3ce5e-117">Hello kullanmadıysanız, bir komut istemi tooconfirm hello silme işlemi hatalarla *-Force* seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="3ce5e-118">RG üzerinde onay hello ve içerdiği tüm hello kaynaklar silinir.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="3ce5e-119">Hello Azure portalında bir kaynak grubunda Sil</span><span class="sxs-lookup"><span data-stu-id="3ce5e-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="3ce5e-120">Oturum açma toohello [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ce5e-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3ce5e-121">Toodelete istediğiniz toohello Service Fabric kümesi gidin.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="3ce5e-122">Merhaba üzerinde hello küme essentials sayfasında kaynak grubu adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="3ce5e-123">Bu hello getirir **kaynak grubu Essentials** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="3ce5e-124">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-124">Click **Delete**.</span></span>
6. <span data-ttu-id="3ce5e-125">Bu sayfa toocomplete hello hello kaynak grubunun silinmesi üzerinde Hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![Kaynak Grubu Sil][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="3ce5e-127">Merhaba küme kaynağı ve hello kaynakları kullanır, ancak diğer kaynakları değil hello kaynak grubunda Sil</span><span class="sxs-lookup"><span data-stu-id="3ce5e-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="3ce5e-128">İlgili toohello Service Fabric kümesi olan kaynakları kaynak grubunuz varsa, toodelete istediğiniz sonra daha kolay toodelete hello tüm kaynak grubu değil.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="3ce5e-129">Kaynak grubunda tooselectively delete hello kaynakları tek tek istiyorsanız, aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="3ce5e-130">Hello portal veya hello Şablon Galerisi'nden hello Service Fabric Resource Manager şablonlarından birini kullanarak kümenizi dağıtılmışsa, küme kullanan hello tüm hello kaynakları iki etiket aşağıdaki hello ile etiketlenir.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="3ce5e-131">Hangi kaynaklara istediğiniz toodecide kullanabilirsiniz toodelete.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="3ce5e-132">***#1 etiketi:*** anahtarı clusterName, değer = 'hello küme adı' =</span><span class="sxs-lookup"><span data-stu-id="3ce5e-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="3ce5e-133">***#2 etiketi:*** anahtarı KaynakAdı, değer = ServiceFabric =</span><span class="sxs-lookup"><span data-stu-id="3ce5e-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="3ce5e-134">Hello Azure portal'ın belirli kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="3ce5e-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="3ce5e-135">Oturum açma toohello [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ce5e-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3ce5e-136">Toodelete istediğiniz toohello Service Fabric kümesi gidin.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="3ce5e-137">Çok Git**tüm ayarları** hello essentials dikey.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="3ce5e-138">Tıklayın **etiketleri** altında **kaynak yönetimi** hello ayarlar dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="3ce5e-139">Merhaba birini tıklatın **etiketleri** hello etiketleri dikey tooget bu etikete sahip tüm hello kaynakların bir listesini içinde.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![Kaynak Etiketleri][ResourceTags]
6. <span data-ttu-id="3ce5e-141">Etiketli kaynakları hello listesine sahip olduktan sonra her hello kaynaklar'ı tıklatın ve silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![Etiketli kaynakları][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="3ce5e-143">Azure PowerShell kullanarak hello kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="3ce5e-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="3ce5e-144">Azure PowerShell cmdlet'lerini aşağıdaki hello çalıştırarak hello kaynaklarını tek tek silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3ce5e-145">Büyük bilgisayarınızda yüklü veya Azure PowerShell 1.0 emin olun.</span><span class="sxs-lookup"><span data-stu-id="3ce5e-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="3ce5e-146">Daha önceden yapmadıysanız özetlenen hello adımları [nasıl tooinstall ve Azure PowerShell yapılandırın.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="3ce5e-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="3ce5e-147">Bir PowerShell penceresi açın ve PS cmdlet'leri aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3ce5e-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="3ce5e-148">Merhaba kaynakların her biri için toodelete istediğiniz, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3ce5e-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="3ce5e-149">Merhaba aşağıdaki komutu çalıştırarak toodelete hello küme kaynağı:</span><span class="sxs-lookup"><span data-stu-id="3ce5e-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="3ce5e-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ce5e-150">Next steps</span></span>
<span data-ttu-id="3ce5e-151">Tooalso aşağıdaki okuma hello Küme yükseltme ve Hizmetleri bölümleme hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="3ce5e-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="3ce5e-152">Küme yükseltme hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="3ce5e-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="3ce5e-153">En fazla ölçek için durum bilgisi olan hizmetler bölümleme hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="3ce5e-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
