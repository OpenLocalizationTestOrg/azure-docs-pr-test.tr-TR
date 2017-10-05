---
title: "Linux sanal makineleri için tanılama Azure'da önyükleme | Microsoft belge"
description: "Azure'daki Linux sanal makineleri için iki hata ayıklama özelliklerine genel bakış"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: 70254d39b5c6326166f7e29fdfc99533835502f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-boot-diagnostics-to-troubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="ee71d-103">Linux sanal makineleri azure'da gidermek için önyükleme tanılaması kullanma</span><span class="sxs-lookup"><span data-stu-id="ee71d-103">How to use boot diagnostics to troubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="ee71d-104">Azure’da artık iki hata ayıklama özelliği desteklenmektedir: Azure Sanal Makineler Kaynak Yöneticisi dağıtım modelinde Konsol Çıktısı ve Ekran Görüntüsü desteği vardır.</span><span class="sxs-lookup"><span data-stu-id="ee71d-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="ee71d-105">Azure’a kendi görüntünüzü ekleme ve hatta bir platform görüntüsünden önyükleme yapma sırasında bir Sanal Makineni önyüklenebilir olmayan bir duruma gelmesinin birçok nedeni olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee71d-105">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="ee71d-106">Bu özellikler sanal makinelerinizin önyükleme hatalarını kolayca tanılamanızı ve düzeltmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee71d-106">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="ee71d-107">Linux sanal makineleri için Portal'dan konsol oturum çıktısını kolayca görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ee71d-107">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure portalına](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="ee71d-109">Ancak, hem Windows hem de Linux sanal makineleri için Azure, hiper yöneticiden VM'nin ekran görüntüsünü görmenizi de sağlar:</span><span class="sxs-lookup"><span data-stu-id="ee71d-109">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Hata](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="ee71d-111">Bu özelliklerin her ikisi de tüm bölgelerdeki Azure sanal makineler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ee71d-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="ee71d-112">Not, ekran görüntüleri ve çıktının depolama hesabınızda görünmesi 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ee71d-112">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="ee71d-113">Sık karşılaşılan önyükleme hataları</span><span class="sxs-lookup"><span data-stu-id="ee71d-113">Common boot errors</span></span>

- [<span data-ttu-id="ee71d-114">Dosya sistemi sorunları</span><span class="sxs-lookup"><span data-stu-id="ee71d-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="ee71d-115">Çekirdek sorunları</span><span class="sxs-lookup"><span data-stu-id="ee71d-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="ee71d-116">FSTAB hataları</span><span class="sxs-lookup"><span data-stu-id="ee71d-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="ee71d-117">Yeni bir sanal makine üzerinde tanılamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ee71d-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="ee71d-118">Önizleme Portalı'ndan yeni bir sanal makine oluştururken dağıtım modeli açılır menüsünde **Azure Resource Manager**’ı seçin:</span><span class="sxs-lookup"><span data-stu-id="ee71d-118">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="ee71d-120">Burada bu tanılama dosyalarını yerleştirmek istediğiniz depolama hesabını seçmek için izleme seçeneğini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ee71d-120">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![VM oluşturma](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="ee71d-122">Bir Azure Resource Manager şablonu dağıtıyorsanız, sanal makine kaynağınıza gidin ve tanılama profili bölümünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ee71d-122">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="ee71d-123">"2015-06-15" API sürümü üst bilgisini kullanmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ee71d-123">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="ee71d-124">Tanılama profili, bu günlükleri yerleştirmek istediğiniz depolama hesabını seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee71d-124">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="ee71d-125">Mevcut bir sanal makineyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ee71d-125">Update an existing virtual machine</span></span>

<span data-ttu-id="ee71d-126">Önyükleme tanılaması portalı üzerinden etkinleştirmek için mevcut bir sanal makine Portalı aracılığıyla da güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee71d-126">To enable boot diagnostics through the portal, you can also update an existing virtual machine through the portal.</span></span> <span data-ttu-id="ee71d-127">Önyükleme Tanılaması seçeneğini ve Kaydet’i seçin.</span><span class="sxs-lookup"><span data-stu-id="ee71d-127">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="ee71d-128">Etkili olması için VM'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="ee71d-128">Restart the VM to take effect.</span></span>

![Mevcut VM’yi güncelleştirme](./media/boot-diagnostics/screenshot5.png)