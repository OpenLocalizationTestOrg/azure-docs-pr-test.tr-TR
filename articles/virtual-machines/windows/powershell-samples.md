---
title: "Sanal makine PowerShell örnekleri aaaAzure | Microsoft Docs"
description: "Azure sanal makinesi PowerShell örnekleri"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Azure sanal makine PowerShell örnekleri

Merhaba aşağıdaki tabloda, Windows sanal makineler oluşturun ve yönetin bağlantılar tooPowerShell komut dosyalarının örneklerini içerir.

| | |
|---|---|
|**Sanal makineler oluşturma**||
| [Tam olarak yapılandırılmış bir sanal makine oluşturun](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturur.|
| [Yüksek oranda kullanılabilir sanal makineler oluşturma](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Birkaç yüksek oranda kullanılabilir sanal makineleri ve yükü dengelenmiş yapılandırma oluşturur.|
| [Bir VM oluşturma ve yapılandırma komut dosyası çalıştırma](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir sanal makine oluşturur ve hello Azure özel betik uzantısı tooinstall IIS kullanır. |
| [Bir VM oluşturun ve DSC yapılandırması çalıştırın](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir sanal makine oluşturur ve hello Azure istenen durum yapılandırması (DSC) uzantısı tooinstall IIS kullanır. |
| [Bir VHD yüklemek ve VM'ler oluşturun](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | Uplaods yerel VHD tooAzure dosya ve VHD hello görüntü ve ardından VM bu görüntüden oluşturur. |
| [Yönetilen bir işletim sistemi disk, bir VM oluşturma](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Varolan bir yönetilen Disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturur. |
| [Bir anlık görüntüden bir VM oluşturma](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir sanal makine bir anlık görüntüden ilk yönetilen disk anlık görüntüden oluşturarak ve ardından hello yeni yönetilen işletim sistemi diski olarak diskindeki oluşturur. |
|**Depolama yönetin**||
| [Aynı veya farklı Abonelikteki bir VHD'den yönetilen disketi oluşturma](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Yönetilen bir disk, işletim sistemi diski olarak özel bir VHD veya VHD aynı veya farklı Abonelikteki veri diski olarak veri oluşturur.  |
| [Bir anlık görüntüden yönetilen bir disk oluşturma](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Yönetilen bir disk anlık görüntüden oluşturur. |
| [Yönetilen disk toosame veya farklı bir abonelik kopyalama](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Yönetilen kopya disk toosame veya farklı bir abonelik ancak içinde aynı hello hello üst bölgede yönetilen disk. 
| [Bir anlık görüntü VHD tooa depolama hesabı olarak dışarı aktarma](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Farklı bir bölgeye VHD tooa depolama hesabı olarak yönetilen bir anlık görüntüsü aktarır. |
| [Bir VHD'den bir anlık görüntü oluştur](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir VHD toocreate anlık görüntü birden çok özdeş yönetilen diskleri kısa sürede anlık görüntü oluşturur.  |
| [Anlık görüntü toosame veya farklı bir abonelik kopyalama](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Kopya anlık görüntü toosame veya aynı hello farklı abonelik ancak bölge hello üst anlık görüntü olarak. |
|**Sanal makineler güvenli**||
| [VM ve veri diskleri şifrele](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | Azure anahtar kasası, şifreleme anahtarı ve hizmet sorumlusu oluşturur ve ardından VM şifreler. |
|**Sanal makineleri izleme**||
| [Bir VM Operations Management Suite ile izleme](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir sanal makine oluşturur, hello Operations Management Suite aracısını yükler ve hello bir OMS çalışma alanında VM kaydeder.  |
| | |

