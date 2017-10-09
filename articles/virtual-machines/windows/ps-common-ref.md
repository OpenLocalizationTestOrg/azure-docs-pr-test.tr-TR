---
title: "aaaCommon PowerShell komutları için Azure sanal makineleri | Microsoft Docs"
description: "Ortak PowerShell komutları tooget oluşturma ve yönetme, Windows Vm'lerini azure'da başlatıldı."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Oluşturma ve Azure sanal makineleri yönetmek için ortak PowerShell komutları

Bu makalede toocreate kullanın ve sanal makineler Azure aboneliğinizde yönetmek Azure PowerShell komutlarını hello bazıları yer almaktadır.  Daha ayrıntılı yardım belirli komut satırı anahtarları ve seçenekleri için kullanabileceğiniz **Get-Help** *komutu*.

Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooyour hesabında imzalama hakkında bilgi.

Birden fazla hello komutları bu makalede çalışıyorsa bu değişkenleri için yararlı olabilir:

- $location - hello sanal makine başlangıç konumu. Kullanabileceğiniz [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind bir [coğrafi bölge](https://azure.microsoft.com/regions/) için çalışır.
- $myResourceGroup - hello sanal makine içeren hello kaynak grubunun hello adı.
- $myVM - hello sanal makinenin hello adı.

## <a name="create-a-vm"></a>VM oluşturma

| Görev | Komut |
| ---- | ------- |
| Bir VM yapılandırması oluştur |$vm = [yeni AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) - VMName $myVM - VMSize "Standard_D1_v1"<BR></BR><BR></BR>Merhaba VM kullanılan toodefine veya güncelleştirme ayarlarını hello VM için yapılandırmadır. Merhaba yapılandırma hello VM hello adıyla başlatılır ve kendi [boyutu](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Yapılandırma ayarları ekleme |$vm = [kümesi AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) - VM $vm-Windows - ComputerName $myVM-$cred - ProvisionVMAgent kimlik bilgisi - EnableAutoUpdate<BR></BR><BR></BR>İşletim sistemi ayarları dahil olmak üzere [kimlik bilgileri](https://technet.microsoft.com/library/hh849815.aspx) daha önce oluşturduğunuz yeni AzureRmVMConfig kullanarak toohello yapılandırma nesnesi eklenir. |
| Bir ağ arabirimi ekleyin |$vm = [Ekle AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) - VM $vm-kimliği $NIC Kimliği<BR></BR><BR></BR>Bir VM'ye sahip olması gereken bir [ağ arabirimi](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate bir sanal ağ içinde. Aynı zamanda [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve var olan bir ağ arabirimi nesnesi. |
| Bir platform görüntüsü belirtin |$vm = [kümesi AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) - VM $vm - PublisherName "publisher_name"-"publisher_offer" sunar - SKU "product_sku"-"son" sürüm<BR></BR><BR></BR>[Görüntü bilgileri](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) daha önce oluşturduğunuz yeni AzureRmVMConfig kullanarak toohello yapılandırma nesnesi eklenir. bir platform görüntüsü hello işletim sistemi disk toouse ayarladığınızda, bu komuttan döndürülen hello nesnesi yalnızca kullanılır. |
| İşletim sistemi disk toouse platform görüntüsü Ayarla |$vm = [kümesi AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) - VM $vm-adı "myOSDisk" - VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" - CreateOption FromImage<BR></BR><BR></BR>Merhaba adını hello işletim sistemi diski ve konumunda [depolama](../../storage/common/storage-powershell-guide-full.md) daha önce oluşturduğunuz toohello yapılandırma nesnesi eklenir. |
| İşletim sistemi disk toouse genelleştirilmiş bir resmi ayarlama |$vm = kümesi AzureRmVMOSDisk - VM $vm-adı "myOSDisk" - SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk. {GUID} .vhd"- VhdUri"https://mystore1.blob.core.windows.net/vhds/disk_name.vhd"- CreateOption FromImage-Windows<BR></BR><BR></BR>Merhaba adını hello işletim sistemi diski, hello kaynak görüntüsünün hello konumu ve hello diskin konumda [depolama](../../storage/common/storage-powershell-guide-full.md) toohello yapılandırma nesnesi eklenir. |
| İşletim sistemi disk toouse özel bir yansıma ayarlayın |$vm = kümesi AzureRmVMOSDisk - VM $vm-adı "myOSDisk" - VhdUri "http://mystore1.blob.core.windows.net/vhds/" - CreateOption Attach - Windows |
| VM oluşturma |[Yeni-AzureRmVM]() - ResourceGroupName $myResourceGroup-konum $location - VM $vm<BR></BR><BR></BR>Tüm kaynaklar oluşturulan bir [kaynak grubu](../../azure-resource-manager/powershell-azure-resource-manager.md). Bu komutu çalıştırmadan önce yeni AzureRmVMConfig, Set-AzureRmVMOperatingSystem, Set-AzureRmVMSourceImage, Add-AzureRmVMNetworkInterface ve Set-AzureRmVMOSDisk çalıştırın. |

## <a name="get-information-about-vms"></a>Sanal makineleri hakkında bilgi edinin

| Görev | Komut |
| ---- | ------- |
| Bir abonelikte listesi VM'ler |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Bir kaynak grubunda listesi VM'ler |Get-AzureRmVM - ResourceGroupName $myResourceGroup<BR></BR><BR></BR>tooget kaynak listesini, aboneliğinizde gruplar, kullanın [Get-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| VM hakkında bilgi alma |Get-AzureRmVM - ResourceGroupName $myResourceGroup-ad $myVM |

## <a name="manage-vms"></a>VM’leri yönetme
| Görev | Komut |
| --- | --- |
| VM başlatma |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) - ResourceGroupName $myResourceGroup-ad $myVM |
| VM durdurma |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) - ResourceGroupName $myResourceGroup-ad $myVM |
| Çalışan bir VM yeniden başlatma |[Yeniden başlatma-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) - ResourceGroupName $myResourceGroup-ad $myVM |
| VM silme |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) - ResourceGroupName $myResourceGroup-ad $myVM |
| Bir VM generalize |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) - ResourceGroupName $myResourceGroup-ad $myVM-genelleştirilmiş<BR></BR><BR></BR>Kaydet-AzureRmVMImage çalıştırmadan önce bu komutu çalıştırın. |
| VM yakalama |[Kaydet-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) - ResourceGroupName $myResourceGroup - VMName $myVM - DestinationContainerName "myImageContainer" - VHDNamePrefix "myImagePrefix"-"C:\filepath\filename.json" yolu<BR></BR><BR></BR>Bir sanal makine olmalıdır [hazır, kapatmak ve genelleştirilmiş](prepare-for-upload-vhd-image.md) kullanılan toobe toocreate bir görüntü. Bu komutu çalıştırmadan önce Set-AzureRmVm çalıştırın. |
| Bir VM güncelleştir |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) - ResourceGroupName $myResourceGroup - VM $vm<BR></BR><BR></BR>Get-AzureRmVM kullanarak hello geçerli VM yapılandırmasını almak, hello VM nesnesini yapılandırma ayarlarını değiştirin ve ardından şu komutu çalıştırın. |
| Bir veri diski tooa VM ekleme |[Ekleme AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) - VM $vm-adı "myDataDisk" - VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" - LUN #-önbelleğe alma ReadWrite - DiskSizeinGB # - CreateOption boş<BR></BR><BR></BR>Get-AzureRmVM tooget hello VM nesnesini kullanın. Merhaba LUN sayısını ve hello hello diskin boyutunu belirtin. Update-AzureRmVM tooapply hello yapılandırma değişiklikleri toohello VM çalıştırın. eklediğiniz hello disk başlatılmadı. |
| Bir VM’den veri diski kaldırma |[Remove-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) - VM $vm-adı "myDataDisk"<BR></BR><BR></BR>Get-AzureRmVM tooget hello VM nesnesini kullanın. Update-AzureRmVM tooapply hello yapılandırma değişiklikleri toohello VM çalıştırın. |
| Bir uzantı tooa VM ekleme |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) - ResourceGroupName $myResourceGroup-konum $location - VMName $myVM-adı "UzantıAdı"-"publisherName" Publisher-türü "extensionType" - TypeHandlerVersion "#. #"-ayarları $Settings - ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Merhaba uygun bu komutu çalıştırmak [yapılandırma bilgilerini](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) hello uzantısı tooinstall istiyor. |
| VM uzantısı kaldırma |[Remove-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) - ResourceGroupName $myResourceGroup-adı "UzantıAdı" - VMName $myVM |

## <a name="next-steps"></a>Sonraki adımlar
* Bir sanal makine oluşturmak için temel adımlar hello bkz [Resource Manager ve PowerShell kullanarak bir Windows VM oluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

