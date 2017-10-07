---
title: aaaMove Windows AWS VM'ler tooAzure | Microsoft Docs
description: "Amazon Web Hizmetleri (AWS) EC2 Windows örneği tooAzure Azure PowerShell kullanarak sanal makineleri taşıyın."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="29cf1-103">Amazon Web Hizmetleri (AWS) tooAzure PowerShell kullanarak bir Windows VM Taşı</span><span class="sxs-lookup"><span data-stu-id="29cf1-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="29cf1-104">İş yüklerini barındırmak için Azure sanal makineleri değerlendirme, mevcut Amazon Web Hizmetleri (AWS) EC2 Windows VM örneği dışarı sonra hello sanal sabit disk (VHD) tooAzure karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="29cf1-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="29cf1-105">Bir kez hello, VHD karşıya, yeni bir VM Azure'da hello VHD oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29cf1-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="29cf1-106">Bu konu, tek bir VM'ye AWS tooAzure taşıma kapsar.</span><span class="sxs-lookup"><span data-stu-id="29cf1-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="29cf1-107">AWS tooAzure ölçekte toomove VM'lerin istiyorsanız, bkz: [Amazon Web Hizmetleri (AWS) tooAzure Azure Site Recovery ile sanal makineleri geçirmek](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="29cf1-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="29cf1-108">Merhaba VM hazırlama</span><span class="sxs-lookup"><span data-stu-id="29cf1-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="29cf1-109">Genelleştirilmiş ve özelleştirilmiş VHD'ler tooAzure karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29cf1-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="29cf1-110">Her tür AWS dışarı aktarmadan önce hello VM hazırlama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="29cf1-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="29cf1-111">**VHD genelleştirilmiş** -genelleştirilmiş bir VHD tüm kişisel hesap bilgilerinizi Sysprep kullanılarak kaldırılıncaya oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="29cf1-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="29cf1-112">Toouse hello VHD görüntüsü toocreate olarak amaçlıyorsanız, yeni VM'lerin, aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="29cf1-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="29cf1-113">[Bir Windows VM hazırlama](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="29cf1-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="29cf1-114">Sysprep kullanarak Hello sanal makine genelleştirin.</span><span class="sxs-lookup"><span data-stu-id="29cf1-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="29cf1-115">**Özelleştirilmiş VHD** -özel bir VHD hello kullanıcı hesapları, uygulamaları ve diğer özgün VM Durum verilerini korur.</span><span class="sxs-lookup"><span data-stu-id="29cf1-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="29cf1-116">Toouse düşünüyorsanız, VHD olarak hello-toocreate yeni bir VM olan aşağıdaki adımları hello tamamlanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="29cf1-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="29cf1-117">[Bir Windows VHD tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="29cf1-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="29cf1-118">**Sağlamadığı** generalize Sysprep kullanarak VM hello.</span><span class="sxs-lookup"><span data-stu-id="29cf1-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="29cf1-119">Konuk sanallaştırma araçları ve hello VM (yani VMware araçları) üzerinde yüklü aracıları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="29cf1-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="29cf1-120">Merhaba VM olun yapılandırılmış toopull kendi IP adresini ve DNS ayarlarını DHCP yoluyla değil.</span><span class="sxs-lookup"><span data-stu-id="29cf1-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="29cf1-121">Bu başladığında hello sunucu hello VNet içindeki bir IP adresi alacağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="29cf1-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="29cf1-122">Dışarı aktarma ve hello VHD indirin</span><span class="sxs-lookup"><span data-stu-id="29cf1-122">Export and download hello VHD</span></span> 

<span data-ttu-id="29cf1-123">Merhaba EC2 örneği tooa bir Amazon S3 demetini VHD'yi verin.</span><span class="sxs-lookup"><span data-stu-id="29cf1-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="29cf1-124">Merhaba Amazon belgelerine konusunda açıklanan başlangıç adımları [örneği bir VM kullanarak VM içeri/dışarı aktarma olarak dışarı aktarma](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) ve çalışma hello [-örnek-export-görev oluştur](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) komutu tooexport hello EC2 Örnek tooa VHD dosyası.</span><span class="sxs-lookup"><span data-stu-id="29cf1-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="29cf1-125">Merhaba dışarı aktarılan VHD dosyasının belirttiğiniz hello Amazon S3 demetini kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="29cf1-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="29cf1-126">Merhaba temel sözdizimi hello VHD dışarı aktarma aşağıda için yalnızca Değiştir hello yer tutucu metin <brackets> bilgilerinizi ile.</span><span class="sxs-lookup"><span data-stu-id="29cf1-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="29cf1-127">Merhaba VHD dışarı sonra hello yönergeleri izleyin [nasıl karşıdan bir nesne S3 Demetini?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD hello S3 demetini dosya.</span><span class="sxs-lookup"><span data-stu-id="29cf1-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="29cf1-128">AWS hello VHD indirme veri aktarımı ücretleri giderler.</span><span class="sxs-lookup"><span data-stu-id="29cf1-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="29cf1-129">Bkz: [Amazon S3 fiyatlandırma](https://aws.amazon.com/s3/pricing/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="29cf1-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="29cf1-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="29cf1-130">Next steps</span></span>

<span data-ttu-id="29cf1-131">Şimdi hello VHD tooAzure karşıya yükleme ve yeni bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="29cf1-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="29cf1-132">Sysprep, kaynağında çok çalıştırdıysanız**generalize** dışarı aktarmadan önce görmek [genelleştirilmiş bir VHD yüklemek ve Azure'da toocreate yeni VM'ler kullanın](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="29cf1-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="29cf1-133">Sysprep dışarı aktarmadan önce çalıştırmadıysanız hello VHD olarak kabul edilir **özel**, bkz: [özel bir VHD tooAzure karşıya yükleyin ve yeni bir VM oluşturun](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="29cf1-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
