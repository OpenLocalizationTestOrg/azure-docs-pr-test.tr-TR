---
title: "aaaAzure sanal makine ölçek ayarlar genel bakış | Microsoft Docs"
description: "Azure sanal makine ölçek kümeleri hakkında daha fazla bilgi edinin"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>Azure’daki sanal makine ölçek kümeleri nedir?
Sanal makine ölçek kümeleri toodeploy kullanmak ve aynı VM'ler kümesini yönetmek bir Azure işlem kaynaktır. Yapılandırılan tüm sanal makineleri ile aynı Merhaba, Ölçek kümeleridir tasarlanmış toosupport true otomatik ölçeklendirme ve hiçbir Vm'leri önceden sağlama gereklidir. Dolayısıyla hedef big compute, büyük veri ve kapsayıcılı iş yüklerini daha kolay toobuild büyük ölçekli hizmetler taşır.

Tooscale işlem kaynakları oturumunuzu kapatıp, Ölçek gereken uygulamalar için işlemleri örtük olarak arıza ve güncelleştirme etki alanları arasında dengeli. Başka bir giriş tooscale ayarlar için toohello başvuran [Azure blogu duyuru](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/).

Ölçek kümeleri hakkında daha fazla bilgi için şu videoları izleyin:

* [Mark Russinovich, Azure ölçek kümeleri hakkında konuşuyor](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)  
* [Guy Bowerman ile Sanal Makine Ölçek Kümeleri](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>Ölçek kümeleri oluşturma ve yönetme
Ölçeği hello Ayarla oluşturabilirsiniz [Azure portal](https://portal.azure.com) seçerek **yeni** yazarak **ölçek** hello arama çubuğunda. **Sanal makine ölçek kümesi** hello sonuçlarında listelenir. Buradan, gerekli hello alanları toocustomize doldurun ve ölçek kümesini dağıtın. Seçenekler tooset hello portalında CPU kullanımına bağlı olarak temel otomatik ölçeklendirme kurallarını da vardır.

Tıpkı tek Azure Resource Manager VM’lerinde olduğu gibi JSON şablonları ve [REST API’leri](https://msdn.microsoft.com/library/mt589023.aspx) kullanarak da ölçek kümeleri tanımlayıp dağıtabilirsiniz. Bu nedenle, tüm standart Azure Resource Manager dağıtım yöntemlerini kullanabilirsiniz. Şablonlar hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

Örnek şablonları için sanal makine ölçek kümesi ayarlar hello bulabilirsiniz [Azure hızlı başlangıç şablonlarını GitHub deposunu](https://github.com/Azure/azure-quickstart-templates). (Şablonları ile arayın **vmss** hello başlığında.)

Merhaba Hızlı Başlangıç şablonu örnekleri için hello Benioku her şablon için bir "Dağıtma tooAzure" düğmesini toohello portal dağıtımı özelliği bağlar. toodeploy hello ölçeği ayarlamak, hello düğmesini tıklatın ve ardından hello Portalı'nda gerekli herhangi bir parametre doldurun. 

## <a name="scaling-a-scale-set-out-and-in"></a>Ölçek kümesinin ölçeğini artırma veya azaltma
Bir ölçeği hello tıklayarak hello Azure portal Ayarla hello kapasitesini değiştirebileceğiniz **ölçeklendirme** altında bölümünde **ayarları**. 

toochange ölçek kümesi kapasitesi hello komut satırında, hello kullan **ölçek** komutunu [Azure CLI](https://github.com/Azure/azure-cli). Örneğin, bu komutu tooset 10 VM ölçek kümesi tooa kapasitesini kullanın:

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

tooset hello sayısı VM'ler içinde bir ölçek PowerShell kullanarak ayarlayabilir, hello kullanabilir **güncelleştirme AzureRmVmss** komutu:

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

sanal makine bir ölçek azaltın veya tooincrease hello sayısı bir Azure Resource Manager şablonu kullanılarak ayarla, hello Değiştir **kapasite** hello şablon özelliği ve yeniden dağıtın. Bu Basitlik kolay toointegrate ölçek kümeleriyle Azure otomatik ölçeklendirme ya da kendi özel ölçeklendirme katman toodefine özel ölçek olayları, Azure otomatik ölçeklendirme gerekiyorsa desteklemediği toowrite kolaylaştırır. 

Bir Azure Resource Manager şablonu toochange hello kapasite dağıtarak, yalnızca hello içeren kadar küçük şablon tanımlayabilirsiniz **SKU** hello özellik paketi kapasite güncelleştirildi. [Bir örneği aşağıda verilmiştir](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing).

## <a name="autoscale"></a>Otomatik Ölçeklendirme

Hello Azure portal oluşturulduğunda ölçek kümesi isteğe bağlı olarak otomatik ölçeklendirme ayarlarıyla yapılandırılabilir. VM Hello sayısı artırılabilir veya ortalama CPU kullanımı tabanlı azaltılabilir. 

Merhaba çoğunu kümesi şablonları hello ölçeklendirme [Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates) otomatik ölçeklendirme ayarlarını tanımlar. Otomatik ölçeklendirme ayarlarını tooan ölçek kümesi varolan de ekleyebilirsiniz. Örneğin, bu Azure PowerShell Betiği CPU tabanlı otomatik ölçeklendirme tooa ölçek kümesini ekler:

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

Geçerli ölçümleri tooscale listesi üzerinde bulabilirsiniz [desteklenen Azure İzleyicisi ile ölçümleri](../monitoring-and-diagnostics/monitoring-supported-metrics.md) hello "Microsoft.Compute/virtualMachineScaleSets." başlık altında Daha gelişmiş otomatik ölçeklendirme seçenekleri de uyarı sistemleriyle Web kancalarını toointegrate kullanarak ve zamanlama tabanlı otomatik ölçeklendirme dahil olmak üzere, kullanılabilir.

## <a name="monitoring-your-scale-set"></a>Ölçek kümenizi izleme
Merhaba [Azure portal](https://portal.azure.com) listeleri ölçek ayarlar ve bunların özelliklerini gösterir. Merhaba portal ayrıca yönetim işlemlerini destekler. Yönetim işlemlerini hem ölçek kümeleri hem de bir ölçek kümesindeki tek VM’ler üzerinde gerçekleştirebilirsiniz. Merhaba portal özelleştirilebilir kaynak kullanım grafiği de sağlar. 

Toosee gerekir veya bir Azure kaynağı JSON tanımını temel hello Düzenle de kullanabilirsiniz [Azure kaynak Gezgini](https://resources.azure.com). Ölçek kümeleri hello Microsoft.Compute Azure kaynak sağlayıcısı altında bir kaynaktır. Bu siteden, bunları bağlantılar aşağıdaki hello genişleterek görebilirsiniz:

**Abonelikler** > **aboneliğiniz** > **resourceGroups** > **sağlayıcılar** > **Microsoft.Compute** > **virtualMachineScaleSets** > **ölçek kümeniz** > vb.

## <a name="scale-set-scenarios"></a>Ölçek kümesi senaryoları
Bu bölümde tipik ölçek kümesi senaryolarından bazıları listelenmektedir. Daha yüksek düzeydeki bazı Azure hizmetleri (Batch, Service Fabric ve Container Service gibi) bu senaryoları kullanır.

* **RDP kullanın veya SSH tooconnect tooscale ayarlayın örnekleri**: ölçek kümesi bir sanal ağ içinde oluşturulur ve tek tek sanal makineleri hello ölçek kümesinde değil olarak varsayılan olarak genel IP adresleri ayrılır. Bu ilke hello gider önler ve işlem Kılavuzunuzun tooall hello düğümler ayrı genel IP ayırma yönetim ek yükü giderir. Dış bağlantıları tooscale VM'ler ayarlamak doğrudan gerekiyorsa, bir ölçek kümesi tooautomatically Ata ortak IP adresleri toonew VM'ler yapılandırabilirsiniz. Alternatif olarak, genel IP adresleri, örneğin, ayrılabilen sanal ağınızda yük dengeleyicileri ve tek başına sanal makineler diğer kaynaklardan tooVMs bağlanabilirsiniz. 
* **NAT kurallarını kullanarak tooVMs bağlanmak**: genel bir IP adresi oluşturun, tooa yük dengeleyici atamak ve bir gelen NAT havuzu tanımlayın. Bu eylemler hello IP adresi tooa hello ölçek kümesindeki VM numaralı bağlantı noktalarını eşleyin. Örneğin:
  
  | Kaynak | Kaynak bağlantı noktası | Hedef | Hedef bağlantı noktası |
  | --- | --- | --- | --- |
  |  Genel IP |Bağlantı Noktası 50000 |vmss\_0 |Bağlantı noktası 22 |
  |  Genel IP |Bağlantı noktası 50001 |vmss\_1 |Bağlantı noktası 22 |
  |  Genel IP |Bağlantı noktası 50002 |vmss\_2 |Bağlantı noktası 22 |
  
   İçinde [Bu örnek](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat), NAT kuralları, tanımlanan tooenable ölçek kümesindeki bir SSH bağlantısı tooevery VM, kullanarak tek bir ortak IP adresi.
  
   [Bu örnek](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat) aynı RDP ve Windows hello.
* **"Jumpbox" kullanarak tooVMs bağlanmak**: aynı sanal ağ, hello hello ölçek kümesini ve tek başına VM oluşturursanız, VM, başka kullanarak kendi iç IP adresleri, tooone bağlanabilir, hello sanal tarafından tanımlanan tek başına VM ve hello ölçek kümesi ağ veya alt ağ. Bir ortak IP adresi oluşturup toohello tek başına VM atamak isterseniz, RDP veya SSH tooconnect toohello tek başına VM kullanabilirsiniz. Ardından gelen makine tooyour ölçek örnekleri kümesi bağlayabilirsiniz. Bu noktada, basit ölçek kümesinin, varsayılan yapılandırmasında genel IP adresine sahip basit bir tek başına VM’den doğal olarak daha güvenli olduğunu fark edebilirsiniz.
  
   Örneğin, [bu şablon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox) bir tek başına VM ile basit bir ölçek kümesini dağıtır. 
* **Yük Dengeleme tooscale kümesi örneklerinin**: hepsini bir yaklaşım kullanarak toodeliver iş tooa işlem kümesi VM'lerin istiyorsanız, Azure yük dengeleyici katman 4 Yük Dengeleme kuralları ile uygun şekilde yapılandırabilirsiniz. Araştırmalar tanımlayabilirsiniz ping atılarak uygulamanızı çalıştıran tooverify bağlantı noktaları belirtilen protokolü, aralık ve istek yolu. [Azure Application Gateway](https://azure.microsoft.com/services/application-gateway/) ayrıca katman 7 ve daha karmaşık yük dengeleme senaryolarıyla birlikte ölçek kümelerini destekler.
  
   [Bu örnek](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl) çalıştığında Apache web sunucuları ve onu kullanan her VM'nin aldığı bir yük dengeleyici toobalance hello yük ölçek kümesi oluşturur. (Merhaba Microsoft.Network/loadBalancers kaynak türü ve networkProfile ve virtualMachineScaleSet extensionProfile bakın.)

   [Bu Linux örneği](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway) ile [bu Windows örneği](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway), Application Gateway kullanır.  

* **Bir ölçek kümesini PaaS küme yöneticisi içinde işlem kümesi olarak dağıtma**: Ölçek kümeleri bazı durumlarda yeni nesil çalışan rolü olarak tanımlanır. Geçerli bir açıklama olsa da, bunu kafa karıştırıcı ölçek hello riskini kümesi özellikleri Azure Cloud Services özelliklerle çalıştırın. Bir anlamda, ölçek kümeleri gerçek bir çalışan rolü veya çalışan kaynağı sağlar. Bunlar platform/çalışma zamanından bağımsız, özelleştirilebilir ve Azure Resource Manager IaaS ile tümleşen genelleştirilmiş işlem kaynaklarıdır.
  
   Bir Cloud Services çalışan rolü, platform/çalışma zamanı desteği bakımından sınırlıdır (yalnızca Windows platform görüntüleri). Ancak, aynı zamanda VIP değiştirme, yapılandırılabilir yükseltme ayarları ve çalışma zamanı/uygulama dağıtımına özel ayarlar gibi hizmetleri içerir. Bu hizmetler ölçek kümelerinde *henüz* kullanılamamaktadır veya Azure Service Fabric gibi diğer üst düzey PaaS hizmetleri tarafından sunulmaktadır. Ölçek kümelerini PaaS desteğine sahip bir altyapı olarak düşünebilirsiniz. [Service Fabric](https://azure.microsoft.com/services/service-fabric/) gibi PaaS çözümleri bu altyapıyı kullanır.
  
   Bu yaklaşımın [bu örneğinde](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos) [Azure Container Service](https://azure.microsoft.com/services/container-service/), bir kapsayıcı düzenleyicisi ile ölçek kümelerini temel alan bir küme dağıtır.

## <a name="scale-set-performance-and-scale-guidance"></a>Ölçek kümesi performansı ve ölçek kılavuzu
* Destekleyen bir ölçek kümesi too1, 000 VM'ler ayarlama. Oluşturursanız ve kendi özel VM görüntülerini hello sınırı 100'dür. Büyük ölçek kümeleri kullanma hakkında konular için bkz. [Büyük sanal makine ölçek kümeleri ile çalışma](virtual-machine-scale-sets-placement-groups.md).
* Toopre yok-Azure depolama hesapları toouse ölçek kümeleri oluşturun. Ölçek kümeleri destek Azure depolama hesabı başına disk hello sayısı performans endişeniz negate diskleri yönetilen. Daha fazla bilgi için bkz. [Azure sanal makine ölçek kümeleri ve yönetilen diskler](virtual-machine-scale-sets-managed-disks.md).
* Daha hızlı, daha öngörülebilir VM sağlama zamanları ve gelişmiş G/Ç performansı için Azure Depolama yerine Azure Premium Depolama kullanmayı düşünün.
* Merhaba çekirdek kotası, dağıttığınız hello bölgede oluşturabileceğiniz VM'ler hello sayısını sınırlar. Azure bulut Hizmetleri ile kullanmak için çekirdek yüksek sınırı bugün olsa bile, işlem kota sınırı toocontact müşteri desteği tooincrease gerekebilir. tooquery bu Azure CLI komutu çalıştırmak, kota: `azure vm list-usage`. Veya bu PowerShell komutunu çalıştırın: `Get-AzureRmVMUsage`.

## <a name="frequently-asked-questions-for-scale-sets"></a>Ölçek kümeleri için sık sorulan sorular
**S.** Bir ölçek kümesinde kaç tane sanal makinem olabilir?

**C.** Özel görüntülerinde 0 too100 VM'ler tabanlı veya 000 VM'ler platform görüntülerinde tabanlı veya ölçek kümesini 0 too1 olabilir. 

**S.** Ölçek kümelerinde veri diskleri destekleniyor mu?

**C.** Evet. Ölçek kümesini tooall VM'ler hello kümesindeki geçerli bir bağlı veri diskleri yapılandırmasını tanımlayabilirsiniz. Daha fazla bilgi için bkz. [Azure ölçek kümeleri ve bağlı veri diskleri](virtual-machine-scale-sets-attached-disks.md). Veri depolamayla ilgili diğer seçenekler şunlardır:

* Azure dosyaları (paylaşılan SMB sürücüleri)
* İşletim sistemi sürücüsü
* Geçici sürücü (yerel, Azure Depolama tarafından yedeklenmez)
* Azure veri hizmeti (örneğin Azure tabloları, Azure blobları)
* Dış veri hizmeti (örneğin, uzak veritabanı)

**S.** Hangi Azure bölgeleri ölçek kümelerini destekler?

**C.** Tüm bölgeler ölçek kümelerini destekler.

**S.** Özel bir görüntü kullanarak nasıl ölçek kümesi oluşturabilirim?

**C.** Özel görüntü VHD’nizi temel alan bir yönetilen disk oluşturun ve ölçek kümesi şablonunuzda başvurun. [Bir örneği aşağıda verilmiştir](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os).

**S.** I azaltılırsa my ölçek VM'ler kaldırılır 20 too15 kümesi kapasitesi?

**C.** Sanal makineler hello ölçeği güncelleştirme etki alanları ve hata etki alanları toomaximize kullanılabilirlik arasında eşit olarak ayarla çıkarılır. VM'ler ile Merhaba yüksek kimlikleri ilk kaldırılır.

**S.** Ne 15 too18 hello kapasiteden sonra artırmak?

**C.** Kapasite too18 artırırsanız, 3 yeni VM'ler oluşturulur. Her zaman hello VM örneği kimliği hello önceki en yüksek değerinden (örneğin, 20, 21, 22) artırılır. VM’ler hata etki alanlarında ve güncelleştirme etki alanlarında dengelenir.

**S.** Bir ölçek kümesinde birden fazla uzantı kullanırken bir yürütme sırası uygulamayı zorunlu kılabilir miyim?

**C.** Doğrudan ancak hello customScript uzantısını için komut dosyanızı için başka bir uzantı toofinish bekleyebilirsiniz. Ek yönergeler hello blog gönderisi uzantısı sıralaması alabilirsiniz [uzantısı sıralaması Azure VM ölçek kümesi](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).

**S.** Ölçek kümeleri Azure kullanılabilirlik kümeleri ile birlikte çalışır mı?

**C.** Evet. Bir ölçek kümesi, 5 hata etki alanı ve 5 güncelleştirme etki alanına sahip örtülü bir kullanılabilirlik kümesidir. Ölçek 100'den fazla VMs kümesi yayılan birden çok *yerleştirme grupları*, eşdeğer toomultiple kullanılabilirlik kümeleri olduğu. Yerleştirme grupları hakkında daha fazla bilgi için bkz. [Büyük sanal makine ölçek kümeleri ile çalışma](virtual-machine-scale-sets-placement-groups.md). Sanal makineleri bir kullanılabilirlik kümesi aynı hello mevcut VM ölçek kümesi olarak sanal ağ. Bir ortak bir kullanılabilirlik tooput denetim düğümü (gerektiren genellikle benzersiz yapılandırma) VM'ler ayarlamak ve veri düğümlerini hello ölçek kümesinde put yapılandırmadır.

Ölçek hakkında daha fazla yanıtlar tooquestions ayarlar hello bulabilirsiniz [Azure sanal makine ölçek ayarlar SSS](virtual-machine-scale-sets-faq.md).
