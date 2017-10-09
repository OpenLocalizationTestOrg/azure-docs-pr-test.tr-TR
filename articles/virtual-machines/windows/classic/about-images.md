---
title: "Windows sanal makineler için aaaAbout görüntüleri | Microsoft Docs"
description: "Görüntüleri azure'da Windows sanal makinelerle kullanılma hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="95a1b-103">Windows sanal makineler için görüntüler hakkında</span><span class="sxs-lookup"><span data-stu-id="95a1b-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="95a1b-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="95a1b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="95a1b-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="95a1b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="95a1b-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="95a1b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="95a1b-107">Bulma ve hello Resource Manager modelinde görüntüleri kullanma hakkında daha fazla bilgi için bkz: [burada](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95a1b-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="95a1b-108">İmajlarla çalışma</span><span class="sxs-lookup"><span data-stu-id="95a1b-108">Working with images</span></span>

<span data-ttu-id="95a1b-109">Hello Azure PowerShell modülü ve hello Azure portal toomanage hello görüntüleri kullanılabilir tooyour Azure aboneliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95a1b-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="95a1b-110">Hello Azure PowerShell modülü, tam olarak ne saptayabilirler şekilde daha fazla komut seçenekleri sağlar toosee istediğiniz ya da yapın.</span><span class="sxs-lookup"><span data-stu-id="95a1b-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="95a1b-111">Hello Azure portal GUI hello gündelik yönetim görevlerinin çoğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="95a1b-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="95a1b-112">Hello Azure PowerShell modülünü kullanan bazı örnekler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="95a1b-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="95a1b-113">**Tüm görüntüleri alma**:`Get-AzureVMImage`geçerli aboneliğinizdeki kullanılabilir tüm hello görüntüleri listesini döndürür: görüntüleri ve Azure veya iş ortakları tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="95a1b-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="95a1b-114">Merhaba sonuç listesi büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="95a1b-114">hello resulting list could be large.</span></span> <span data-ttu-id="95a1b-115">sonraki örneklerde nasıl hello tooget daha kısa bir liste.</span><span class="sxs-lookup"><span data-stu-id="95a1b-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="95a1b-116">**Görüntü aileleri alma**:`Get-AzureVMImage | select ImageFamily` dizeleri göstererek görüntü aileleri listesini alır **ImageFamily** özelliği.</span><span class="sxs-lookup"><span data-stu-id="95a1b-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="95a1b-117">**Belirli bir ailesinde tüm görüntüleri alma**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="95a1b-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="95a1b-118">**VM görüntüleri Bul**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` yalnızca tooVM görüntülerini uygular hello DataDiskConfiguration özelliği filtreleyerek Bu cmdlet'i çalışır.</span><span class="sxs-lookup"><span data-stu-id="95a1b-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="95a1b-119">Bu örnek ayrıca etiket ve resim hello çıktı tooonly hello adı filtreler.</span><span class="sxs-lookup"><span data-stu-id="95a1b-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="95a1b-120">**Genelleştirilmiş bir yansıma Kaydet**:`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="95a1b-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="95a1b-121">**Özel bir yansıma Kaydet**:`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="95a1b-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="95a1b-122">Merhaba OSState parametresi gerekli toocreate hello işletim sistemi diski içerir ve veri diskleri ekli bir VM görüntüsü ' dir.</span><span class="sxs-lookup"><span data-stu-id="95a1b-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="95a1b-123">Merhaba parametreyi kullanmazsanız hello cmdlet'i bir işletim sistemi görüntüsü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="95a1b-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="95a1b-124">Merhaba hello parametresinin değerini gösterir hello görüntü genelleştirilmiş veya özelleştirilmiş olup olmadığını dayalı hello işletim sistemi diski yeniden kullanılmak üzere hazırlanmıştır olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="95a1b-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="95a1b-125">**Bir görüntü Sil**:`Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="95a1b-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="95a1b-126">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="95a1b-126">Next Steps</span></span>
<span data-ttu-id="95a1b-127">Ayrıca [hello Azure portal kullanarak bir Windows makinesine oluşturma](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="95a1b-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
