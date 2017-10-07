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
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Amazon Web Hizmetleri (AWS) tooAzure PowerShell kullanarak bir Windows VM Taşı

İş yüklerini barındırmak için Azure sanal makineleri değerlendirme, mevcut Amazon Web Hizmetleri (AWS) EC2 Windows VM örneği dışarı sonra hello sanal sabit disk (VHD) tooAzure karşıya yükleyin. Bir kez hello, VHD karşıya, yeni bir VM Azure'da hello VHD oluşturabilirsiniz. 

Bu konu, tek bir VM'ye AWS tooAzure taşıma kapsar. AWS tooAzure ölçekte toomove VM'lerin istiyorsanız, bkz: [Amazon Web Hizmetleri (AWS) tooAzure Azure Site Recovery ile sanal makineleri geçirmek](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Merhaba VM hazırlama 
 
Genelleştirilmiş ve özelleştirilmiş VHD'ler tooAzure karşıya yükleyebilirsiniz. Her tür AWS dışarı aktarmadan önce hello VM hazırlama gerektirir. 

- **VHD genelleştirilmiş** -genelleştirilmiş bir VHD tüm kişisel hesap bilgilerinizi Sysprep kullanılarak kaldırılıncaya oluşturdu. Toouse hello VHD görüntüsü toocreate olarak amaçlıyorsanız, yeni VM'lerin, aşağıdakileri yapmalısınız: 
 
    * [Bir Windows VM hazırlama](prepare-for-upload-vhd-image.md).  
    * Sysprep kullanarak Hello sanal makine genelleştirin.  

 
- **Özelleştirilmiş VHD** -özel bir VHD hello kullanıcı hesapları, uygulamaları ve diğer özgün VM Durum verilerini korur. Toouse düşünüyorsanız, VHD olarak hello-toocreate yeni bir VM olan aşağıdaki adımları hello tamamlanır emin olun.  
    * [Bir Windows VHD tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md). **Sağlamadığı** generalize Sysprep kullanarak VM hello. 
    * Konuk sanallaştırma araçları ve hello VM (yani VMware araçları) üzerinde yüklü aracıları kaldırın. 
    * Merhaba VM olun yapılandırılmış toopull kendi IP adresini ve DNS ayarlarını DHCP yoluyla değil. Bu başladığında hello sunucu hello VNet içindeki bir IP adresi alacağı sağlar.  


## <a name="export-and-download-hello-vhd"></a>Dışarı aktarma ve hello VHD indirin 

Merhaba EC2 örneği tooa bir Amazon S3 demetini VHD'yi verin. Merhaba Amazon belgelerine konusunda açıklanan başlangıç adımları [örneği bir VM kullanarak VM içeri/dışarı aktarma olarak dışarı aktarma](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) ve çalışma hello [-örnek-export-görev oluştur](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) komutu tooexport hello EC2 Örnek tooa VHD dosyası. 

Merhaba dışarı aktarılan VHD dosyasının belirttiğiniz hello Amazon S3 demetini kaydedilir. Merhaba temel sözdizimi hello VHD dışarı aktarma aşağıda için yalnızca Değiştir hello yer tutucu metin <brackets> bilgilerinizi ile.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Merhaba VHD dışarı sonra hello yönergeleri izleyin [nasıl karşıdan bir nesne S3 Demetini?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD hello S3 demetini dosya. 

> [!IMPORTANT]
> AWS hello VHD indirme veri aktarımı ücretleri giderler. Bkz: [Amazon S3 fiyatlandırma](https://aws.amazon.com/s3/pricing/) daha fazla bilgi için.


## <a name="next-steps"></a>Sonraki adımlar

Şimdi hello VHD tooAzure karşıya yükleme ve yeni bir VM oluşturun. 

- Sysprep, kaynağında çok çalıştırdıysanız**generalize** dışarı aktarmadan önce görmek [genelleştirilmiş bir VHD yüklemek ve Azure'da toocreate yeni VM'ler kullanın](upload-generalized-managed.md)
- Sysprep dışarı aktarmadan önce çalıştırmadıysanız hello VHD olarak kabul edilir **özel**, bkz: [özel bir VHD tooAzure karşıya yükleyin ve yeni bir VM oluşturun](create-vm-specialized.md)

 
