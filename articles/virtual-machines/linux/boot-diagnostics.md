---
title: "azure'daki Linux sanal makineleri için aaaBoot tanılama | Microsoft belge"
description: "İki hata ayıklama özelliklerini Linux sanal makineleri azure'da hello genel bakış"
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
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="72281-103">Nasıl toouse önyükleme tanılama tootroubleshoot Linux sanal makineleri Azure'da</span><span class="sxs-lookup"><span data-stu-id="72281-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="72281-104">Azure’da artık iki hata ayıklama özelliği desteklenmektedir: Azure Sanal Makineler Kaynak Yöneticisi dağıtım modelinde Konsol Çıktısı ve Ekran Görüntüsü desteği vardır.</span><span class="sxs-lookup"><span data-stu-id="72281-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="72281-105">Kendi görüntü tooAzure veya hello platform görüntüleri bile önyükleme biri getirilirken bir sanal makine önyüklenebilir olmayan bir duruma neden alır birçok nedeni olabilir.</span><span class="sxs-lookup"><span data-stu-id="72281-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="72281-106">Bu özellikler, tooeasily tanılamak ve sanal makinelerinizi önyükleme hatalarını kurtarıp etkinleştir.</span><span class="sxs-lookup"><span data-stu-id="72281-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="72281-107">Linux sanal makineleri için hello Portal, konsol günlüğünden hello çıktısını kolayca görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="72281-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure portalına](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="72281-109">Ancak, Windows ve Linux sanal makineleri için Azure ayrıca bir ekran görüntüsünü hello VM hello hiper yönetici gelen toosee sağlar:</span><span class="sxs-lookup"><span data-stu-id="72281-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Hata](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="72281-111">Bu özelliklerin her ikisi de tüm bölgelerdeki Azure sanal makineler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="72281-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="72281-112">Not, ekran görüntüleri ve çıktı too10 dakika tooappear depolama hesabınızdaki yukarı alabilir.</span><span class="sxs-lookup"><span data-stu-id="72281-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="72281-113">Sık karşılaşılan önyükleme hataları</span><span class="sxs-lookup"><span data-stu-id="72281-113">Common boot errors</span></span>

- [<span data-ttu-id="72281-114">Dosya sistemi sorunları</span><span class="sxs-lookup"><span data-stu-id="72281-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="72281-115">Çekirdek sorunları</span><span class="sxs-lookup"><span data-stu-id="72281-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="72281-116">FSTAB hataları</span><span class="sxs-lookup"><span data-stu-id="72281-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="72281-117">Yeni bir sanal makine üzerinde tanılamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="72281-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="72281-118">Önizleme portalı hello yeni bir sanal makine oluştururken, hello seçin **Azure Resource Manager** gelen hello dağıtım modeli açılır:</span><span class="sxs-lookup"><span data-stu-id="72281-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="72281-120">Bu tanılama dosyaları Hello tooplace oluşturulacağı yeri izleme seçeneği tooselect hello depolama hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="72281-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![VM oluşturma](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="72281-122">Bir Azure Resource Manager şablonu dağıtıyorsanız, tooyour sanal makine kaynağı gidin ve hello tanılama profil bölümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72281-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="72281-123">Toouse hello "2015-06-15" API sürümü üstbilgisi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="72281-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="72281-124">Merhaba tanılama profili Bu günlükler tooput istediğiniz yere tooselect hello depolama hesabını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="72281-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

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

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="72281-125">Mevcut bir sanal makineyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="72281-125">Update an existing virtual machine</span></span>

<span data-ttu-id="72281-126">tooenable önyükleme tanılaması hello Portalı aracılığıyla mevcut bir sanal makine hello Portalı aracılığıyla güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72281-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="72281-127">Select hello önyükleme tanılaması seçeneği ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72281-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="72281-128">Merhaba VM tootake etkisi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="72281-128">Restart hello VM tootake effect.</span></span>

![Mevcut VM’yi güncelleştirme](./media/boot-diagnostics/screenshot5.png)