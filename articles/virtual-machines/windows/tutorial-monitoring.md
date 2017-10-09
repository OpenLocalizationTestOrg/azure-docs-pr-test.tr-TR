---
title: aaaAzure Windows sanal makineler ve izleme | Microsoft Docs
description: "Öğretici - Azure PowerShell ile Windows sanal makine İzleyicisi"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>Windows sanal makinesi Azure PowerShell ile izleme

Azure izleme aracıları toocollect önyükleme kullanır ve Azure VM'ler, performans verileri Azure depolama alanında bu verileri depolamak ve portal, hello Azure PowerShell modülü ve hello Azure CLI aracılığıyla erişilebilir. Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Bir VM üzerinde önyükleme tanılamayı etkinleştir
> * Önyükleme tanılamasını görüntüleme
> * VM konak metrikleri görüntüleyin
> * Merhaba tanılama uzantısını yükleyin
> * VM metrikleri görüntüleyin
> * Bir uyarı oluşturabilir.
> * Gelişmiş izleme işlevini ayarlama

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

Bu öğreticide toocomplete hello örnek, mevcut bir sanal makine olması gerekir. Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) sizin için bir tane oluşturabilirsiniz. Merhaba öğreticide çalışırken hello kaynak grubu, sanal makine adını ve konumunu değiştirmek gerektiğinde.

## <a name="view-boot-diagnostics"></a>Önyükleme tanılamasını görüntüleme

Windows sanal makineleri yedeklemek önyükleme gibi hello önyükleme Tanılama Aracı sorun giderme amacıyla kullanılabilir ekran çıkışına yakalar. Bu özellik varsayılan olarak etkindir. Merhaba ekran görüntüleri de varsayılan olarak oluşturulan bir Azure depolama hesabında depolanan yakalandı. 

Merhaba önyükleme Tanılama verileri hello alabilirsiniz [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) komutu. Aşağıdaki örneğine hello önyükleme tanılaması hello indirilen toohello kökü olan * c:\* sürücü. 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>Ana bilgisayar metrikleri görüntüleyin

Bir Windows VM adanmış bir konak VM ile etkileşime giren Azure sahiptir. Ölçümleri hello ana bilgisayar için otomatik olarak toplanır ve hello Azure portal görüntülenebilir.

1. Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.
2. Tıklatın **ölçümleri** üzerinde VM dikey penceresinde hello ve hello ana ölçümleri altında birini seçin **kullanılabilir ölçümler** hello konak VM gerçekleştirip nasıl toosee.

    ![Ana bilgisayar metrikleri görüntüleyin](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>Tanılama uzantısını yükleyin

Merhaba temel ana ölçümleri kullanılabilir, ancak toosee daha ayrıntılı ve VM özgü ölçümleri, size tooneed tooinstall hello Azure tanılama uzantısını hello VM. Hello Azure tanılama uzantısını ek izleme ve tanılama veri toobe VM hello alınan sağlar. Bu performans ölçümleri görüntüleyebilir ve hello VM nasıl gerçekleştireceğini temelinde uyarılar oluşturabilir. Merhaba tanılama uzantısını hello Azure portal aşağıdaki şekillerde yüklenir:

1. Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.
2. Tıklatın **tanılama ayarları**. Merhaba liste gösterir *önyükleme tanılama* hello önceki bölümden zaten etkin. Merhaba onay kutusu için *temel ölçümleri*.
3. Merhaba tıklatın **Konuk düzeyinde izlemeyi etkinleştir** düğmesi.

    ![Tanılama metrikleri görüntüleyin](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>VM metrikleri görüntüleyin

Hello hello VM ölçümleri görüntüleyebilir aynı şekilde hello konak VM ölçümleri görüntülenebilir:

1. Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.
2. Merhaba VM gerçekleştiriyor nasıl toosee tıklatın **ölçümleri** üzerinde VM dikey penceresinde hello ve hello tanılama ölçümleri altında birini seçin **kullanılabilir ölçümler**.

    ![VM metrikleri görüntüleyin](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>Uyarı oluşturma

Özel performans ölçümleri temelinde uyarılar oluşturabilirsiniz. Uyarılar, ortalama CPU kullanımını belirli bir eşiği veya kullanılabilir boş disk alanı aştığında belirli bir bir miktar düşene kullanılan toonotify örneğin olabilir. Uyarıları hello Azure portalında görüntülenen veya e-posta ile gönderilebilir. Azure Otomasyon çalışma kitabı veya Azure Logic Apps içinde oluşturulan yanıt tooalerts tetikleyebilir.

Merhaba aşağıdaki örnek ortalama CPU kullanımı için bir uyarı oluşturur.

1. Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.
2. Tıklatın **uyarı kuralları** hello VM dikey penceresinde, ardından **ölçüm uyarı Ekle** hello uyarıları dikey hello üstte.
4. Sağlayan bir **adı** , uyarının gibi *myAlertRule*
5. tootrigger CPU yüzdesi beş dakika 1.0 aştığında bir uyarı, seçili diğer Varsayılanları tüm hello bırakın.
6. İsteğe bağlı olarak, hello kutuyu için *sahipleri, Katkıda Bulunanlar ve okuyucular e-posta* toosend e-posta bildirimi. Merhaba varsayılan toopresent hello Portalı'nda bir bildirim eylemdir.
7. Merhaba tıklatın **Tamam** düğmesi.

## <a name="advanced-monitoring"></a>Gelişmiş izleme 

Kullanarak VM'yi izleme daha gelişmiş yapabileceğiniz [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Zaten yapmadıysanız, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) Operations Management Suite.

Erişim toohello OMS portalı varsa, hello çalışma alanı anahtarı ve çalışma alanı kimliği hello ayarları dikey penceresinde bulabilirsiniz. Kullanım hello [kümesi AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) dolguya tootooadd hello OMS uzantısı toohello VM. Güncelleştirme hello değişkeni örnek tooreflect aşağıda Merhaba, OMS çalışma alanı anahtarı ve çalışma alanı kimliği değerler  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

Birkaç dakika sonra görmelisiniz hello OMS çalışma alanında yeni bir VM hello. 

![OMS dikey penceresi](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide yapılandırılmış ve sanal makineleri Azure Güvenlik Merkezi ile gözden. Şunları öğrendiniz:

> [!div class="checklist"]
> * Sanal ağ oluşturma
> * Bir kaynak grubu ve VM oluşturma 
> * Önyükleme tanılaması hello VM üzerinde etkinleştir
> * Önyükleme tanılamasını görüntüleme
> * Ana bilgisayar metrikleri görüntüleyin
> * Merhaba tanılama uzantısını yükleyin
> * VM metrikleri görüntüleyin
> * Bir uyarı oluşturabilir.
> * Gelişmiş izleme işlevini ayarlama

Azure Güvenlik Merkezi hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [VM güvenliğini yönetme](./tutorial-azure-security.md)