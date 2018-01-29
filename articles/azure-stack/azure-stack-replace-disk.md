---
title: "Fiziksel disk Azure yığınında değiştirme | Microsoft Docs"
description: "Bir fiziksel disk Azure yığınında değiştirme işlemini açıklar."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 449ae53e-b951-401a-b2c9-17fee2f491f1
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: mabrigg
ms.openlocfilehash: a95617a8dd2a8f296164c672e2b4b2628574ce5a
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="replace-a-physical-disk-in-azure-stack"></a>Azure yığınında fiziksel disk değiştirme

*Uygulandığı öğe: Azure yığın tümleşik sistemleri ve Azure yığın Geliştirme Seti*

Bu makalede Azure yığınında fiziksel diski değiştirmek için genel işlem açıklanır. Bir fiziksel disk başarısız olursa, mümkün olan en kısa sürede değiştirmelisiniz.

Tümleşik sistemleri ve hot Swap disklere sahip Geliştirme Seti dağıtımları için bu yordamı kullanabilirsiniz.

Gerçek disk değiştirme adımları farklılık gösterir, özgün donanım üreticisi (OEM) donanım satıcınıza temel. Sisteme özgü ayrıntılı adımlar için satıcınızın alan değiştirilebilen biriminin (FRU) belgelerine bakın. 

## <a name="review-disk-alert-information"></a>Disk uyarı bilgileri gözden geçirin
Bir disk başarısız olduğunda, bir fiziksel disk bağlantısı kaybedildi bildiren bir uyarı alırsınız. 

 ![Fiziksel disk uyarı gösterme bağlantısı kesildi.](media/azure-stack-replace-disk/DiskAlert.png)

Uyarı açarsanız, uyarı açıklaması ölçek birimi düğümü ve değiştirmeniz gereken disk tam fiziksel yuva konumunu içerir. Daha fazla Azure yığın başarısız disk LED göstergesi yeteneklerini kullanarak belirlemenize yardımcı olabilir.

 ## <a name="replace-the-disk"></a>Disk değiştirme

Gerçek disk değiştirme OEM donanım satıcısının FRU yönergeleri izleyin.

Tümleşik bir sistemde desteklenmeyen bir diske kullanılmasını önlemek için sistem satıcınız tarafından desteklenmeyen diskleri engeller. Desteklenmeyen bir diske kullanmayı denerseniz, yeni bir uyarı, bir disk desteklenmeyen modeli veya bellenim nedeniyle karantinaya alınan olduğunu bildirir.

Disk değiştirdikten sonra Azure yığın otomatik olarak yeni disk bulur ve sanal disk onarım işlemi başlatır.  
 
 ## <a name="check-the-status-of-virtual-disk-repair"></a>Sanal disk onarım durumunu denetleme
 
 Disk değiştirdikten sonra sanal disk sistem durumu izleme ve ayrıcalıklı uç nokta kullanarak iş ilerleme durumunu onarın. Ayrıcalıklı uç ağ bağlantısına sahip herhangi bir bilgisayardan aşağıdaki adımları izleyin.

1. Bir Windows PowerShell oturumu açın ve ayrıcalıklı uç noktasına bağlanın.
    ````PowerShell
        $cred = Get-Credential
        Enter-PSSession -ComputerName <IP_address_of_ERCS>`
          -ConfigurationName PrivilegedEndpoint -Credential $cred
    ```` 
  
2. Sanal disk durumunu görüntülemek için aşağıdaki komutu çalıştırın:
    ````PowerShell
        Get-VirtualDisk -CimSession s-cluster
    ````
   ![PowerShell Get-VirtualDisk komutunun çıktısı](media/azure-stack-replace-disk/GetVirtualDiskOutput.png)

3. Geçerli depolama iş durumunu görüntülemek için aşağıdaki komutu çalıştırın:
    ```PowerShell
        Get-VirtualDisk -CimSession s-cluster | Get-StorageJob
    ````
      ![PowerShell Get-StorageJob komutunun çıktısı](media/azure-stack-replace-disk/GetStorageJobOutput.png)

## <a name="troubleshoot-virtual-disk-repair"></a>Sanal disk onarım sorun giderme

Sanal disk onarım durumunda iş takılan, olarak görünür ve işi yeniden başlatmak için aşağıdaki komutu çalıştırın:
  ````PowerShell
        Get-VirtualDisk -CimSession s-cluster | Repair-VirtualDisk
  ```` 
