---
title: "aaaUpgrade bir Azure sanal makine ölçek kümesi | Microsoft Docs"
description: "Bir Azure sanal makine ölçek kümesini yükseltme"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Bir sanal makine ölçek kümesini yükseltme
Bu makalede nasıl herhangi kesinti olmadan ayarlanmış bir işletim sistemi güncelleştirme tooan Azure sanal makine ölçek genişletme dönebilirsiniz açıklanmaktadır. Bu bağlamda bir işletim sistemi güncelleştirme hello sürümü veya hello işletim sistemi SKU'su değiştirme veya özel bir görüntü URI'sini hello değiştirme içerir. Sanal makineleri birer birer birer veya gruplar (örneğin, bir seferde bir hata etki alanı) tüm aynı anda yerine güncelleştirme kapalı kalma süresi anlamına gelir olmadan güncelleştiriliyor. Bunu yaparak, değil yükseltilen tüm sanal makineleri çalışmaya devam.

tooavoid belirsizlik şimdi isteyebileceğiniz işletim sistemi güncelleştirme dört tür ayırt tooperform:

* Merhaba sürümü veya SKU platform görüntüsünün değiştirme. Örneğin, Ubuntu değiştirme 14.04.201506100 14.04.2-LTS sürümünden too14.04.201507060 veya hello Ubuntu 15.10/son SKU too16.04.0-LTS/latest değiştirme. Bu senaryo, bu makalede ele alınmıştır.
* Merhaba tooa yeni oluşturulan özel bir görüntü sürümü işaret URI değiştirme (**özellikleri** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **görüntü** > **URI**). Bu senaryo, bu makalede ele alınmıştır.
* Azure yönetilen diskleri kullanılarak oluşturulmuş bir ölçek kümesinin Hello resim başvurusu değiştirme.
* Bir sanal makine içinde hello OS düzeltme eki uygulama (Bu örnekleri arasında bir güvenlik düzeltme eki yükleme ve Windows Update çalıştıran). Bu senaryo desteklenir, ancak bu makalede ele alınan değil.

Bir parçası olarak dağıtılan sanal makine ölçek kümeleri bir [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) küme ele alınmamıştır burada. Bkz: [düzeltme eki Windows işletim sisteminde, Service Fabric kümesi](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) Service Fabric düzeltme eki uygulama hakkında daha fazla bilgi.

Merhaba sırasını değiştirmek için işletim sistemi sürümü/SKU'su platform görüntüsü hello veya hello özel görüntü URI'sini aşağıdaki gibi görünür temel:

1. Merhaba sanal makine ölçek kümesi modelinde alın.
2. Merhaba sürüm, SKU, görüntü başvuru ya da hello modelinde URI değeri değiştirin.
3. Merhaba modeli güncelleştirin.
4. Yapmak bir *manualUpgrade* hello hello ölçek kümesindeki sanal makinelerde çağırın. Bu adım yalnızca ilgili değilse *upgradePolicy* çok ayarlanır**el ile** , Ölçek kümesi. Çok ayarlanırsa**otomatik**, böylece kapalı kalma süresi neden olan tüm hello sanal makineleri aynı anda yükseltilir.

Aklınızda bu bilgi ile PowerShell ve hello REST API kullanarak bir ölçek hello sürümünü nasıl güncelleştirebilir görelim. Bu örnekler bir platform görüntüsü hello durumunun kapak, ancak bu makale, bu işlem tooa özel görüntü, tooadapt için yeterli bilgi sağlar.

## <a name="powershell"></a>PowerShell
Bu örnek bir Windows sanal makine ölçek kümesi (oluşturma toohello yeni sürüm 4.0.20160229. güncelleştirir Merhaba modeli güncelleştirdikten sonra bunu aynı anda bir güncelleştirme bir sanal makine örneğini yapar.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

Platform görüntü sürümü değiştiğinde yerine özel bir görüntü için URI hello güncelleştiriyorsanız hello "kümesi hello yeni sürümü" yerine güncelleştirecek bir komut satırıyla hello kaynak görüntü URI. Azure yönetilen diskleri kullanmadan Hello ölçek kümesini oluşturulduysa, örneğin, hello güncelleştirme şöyle olabilir:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Özel görüntü ölçek kümesini geliyorsa hello resim başvurusu güncelleştirilmiş sonra yönetilen Azure diskleri kullanılarak oluşturuldu. Örneğin:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Merhaba REST API'si
Burada, birkaç hello Azure REST API tooroll bir işletim sistemi sürümü güncelleştirme çıkışı kullanmak Python örnekler verilmiştir. Her ikisini de hello basit kullanmanız [azurerm](https://pypi.python.org/pypi/azurerm) Azure REST API sarmalayıcı işlevleri toodo hello ölçekte bir GET kitaplığının modeli, güncelleştirilmiş bir modelle PUT arkasından ayarlayın. Bunlar, ayrıca sanal makine örnekleri görünümlerde tooidentify hello sanal makineler güncelleştirme etki alanı tarafından arayın.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) tooroll sanal makine ölçek çalışan bir işletim sistemi yükseltme tooa çıkışı kullanılmış bir Python komut dosyası, aynı anda tek bir güncelleştirme etki alanı kümesi.

![Sanal makine ya da bir güncelleştirme etki alanı seçme Vmssupgrade komut dosyası](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Bu komut, belirli sanal makinelerin tooupdate seçin veya bir güncelleştirme etki alanı belirtirseniz olanak tanır. Platform görüntü sürümü değiştirme veya özel bir görüntü URI'sini hello değiştirme destekler.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) sanal gösterir sanal makine ölçek kümeleri heatmap Durum makinesi için bir genel amaçlı bir güncelleştirme etki alanı bir satır temsil ettiği düzenleyicisidir. Bunun yanı sıra, hello modeli ölçek kümesi için bir yeni sürümü, SKU veya özel görüntü URI'si ile güncelleştirin ve sonra hata etki alanları tooupgrade seçin. Bunu yaptığınızda, bu güncelleştirme etki alanındaki tüm hello sanal makineler yükseltilen toohello yeni modeli vardır. Alternatif olarak, tercih ettiğiniz hello toplu boyutuna göre çalışırken yükseltme yapabilirsiniz.  

Merhaba aşağıdaki ekran görüntüsü ölçeği Ubuntu 14.04-2LTS için sürüm 14.04.201507060 Ayarla modelinin gösterir. Bu ekran alındıktan sonra pek çok seçenek toothis Aracı eklenmiştir.

![Ubuntu 14.04-2LTS için ayarlanmış bir ölçek Vmsseditor modeli](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

Tıklattıktan sonra **yükseltme** ve ardından **ayrıntıları alma**, sanal makinelerinizde UD 0 tooupdate Başlat.

![Vmsseditor gösteren güncelleştirmesi devam ediyor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

