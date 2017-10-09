---
title: "aaaScale Service Fabric kümesi veya | Microsoft Docs"
description: "Giriş veya çıkış toomatch isteğe bağlı bir Service Fabric kümesi her düğüm türü/sanal makine ölçek kümesi için otomatik ölçeklendirme kurallarını ayarlayarak ölçeklendirin. Ekleme veya düğümleri tooa Service Fabric kümesi kaldırma"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Service Fabric kümesi veya otomatik ölçeklendirme kurallarını kullanarak uzaklaştırma ölçeklendirme
Sanal makine ölçek kümeleri toodeploy kullanın ve sanal makinelerin bir koleksiyon kümesi olarak yönetebileceğiniz bir Azure işlem kaynaktır. Service Fabric kümesi içinde tanımlanan her düğüm türü ayrı bir sanal makine ölçek kümesi ayarlanır. Her düğüm türü, genişletilebilir veya çıkışı bağımsız olarak, farklı bağlantı noktalarının açık olması ve farklı kapasite ölçümlerini olabilir. Merhaba içinde hakkında daha fazla bilgiyi [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md) belge. Hello Service Fabric düğüm türleri kümenizdeki hello arka uç, sanal makine ölçek kümelerinin yapıldıktan sonra her düğüm türü/sanal makine ölçek kümesi için otomatik ölçeklendirme kurallarını tooset gerekir.

> [!NOTE]
> Aboneliğiniz bu küme olun yeni VM'ler hello yeterli çekirdek tooadd olması gerekir. Olmadığından hiçbir model doğrulama şu anda, herhangi bir hello kota sınırları isabet durumunda bir dağıtım zaman hatası alır.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Tooscale Hello düğüm türü/sanal makine ölçek kümesi'ni seçin
Şu anda hello portal'ı kullanarak sanal makine ölçek kümeleri için mümkün toospecify hello otomatik ölçek kuralları olup olmadığı, bu nedenle Azure PowerShell (1.0 +) toolist hello düğüm türleri ve Otomatik ölçek kuralları toothem ekleyin bize.

Sanal makine ölçek kümesi tooget hello listesi hello aşağıdaki cmdlet'leri çalıştırın kümenizi, olun:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Otomatik ölçek kuralı hello düğüm türü/sanal makine ölçek kümesi için ayarlama
Birden çok düğüm türleri kümeniz varsa, bu her düğüm türleri/sanal makine Ölçek (içeri veya dışarı) tooscale istediğiniz ayarlar yineleyin. Otomatik ölçeklendirmeyi ayarlamadan önce olmalıdır hesap hello düğüm sayısını alın. Merhaba düğüm sayısı alt sınırı hello birincil düğüm türü için gereken seçmiş olduğunuz hello güvenilirlik düzeyi tarafından yönetilir. Daha fazla bilgi edinin [güvenilirlik düzeyleri](service-fabric-cluster-capacity.md).

> [!NOTE]
> Merhaba en az durum sayısı hello küme kararsız hale veya Getir daha hello birincil düğüm türü tooless ölçeklendirme. Bu, uygulamalarınız için ve hello sistem hizmetleri için veri kaybına neden olabilir.
> 
> 

Şu anda hello otomatik ölçek özelliği, uygulamalarınızın tooService doku raporlama hello yükleri tarafından yönetilir değil. Bu nedenle bu zaman hello otomatik ölçek elde tamamen her hello sanal makine ölçek kümesi örneği tarafından gösterilen hello performans sayaçları dayanmaktadır.  

Bu yönergeleri izleyin [tooset her sanal makine ölçek kümesi için Otomatik ölçek yukarı](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> Senaryo aşağı bir ölçek düğüm türünüz altın veya gümüş dayanıklılık düzeyini olmadıkça toocall hello gereksinim [Kaldır ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/azure/mt125993.aspx) hello uygun düğüm adı ile.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Sanal makineleri tooa düğüm türü/sanal makine ölçek kümesini el ile Ekle
Merhaba örnek/hello'ndaki yönergeleri izleyin [hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello her Nodetype Vm'lerde sayısı. 

> [!NOTE]
> Vm'leri ekleme hello eklemeleri toobe anlık beklemediğiniz için zaman alır. Bu nedenle de tooallow hello VM kapasitesi hello çoğaltmalar için kullanılabilir olmadan önce üzerinde 10 dakika, zaman içinde tooadd kapasite planlaması / yerleştirilen örnekleri tooget service.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Sanal makineleri hello birincil düğüm türü/sanal makine ölçek kümesinden el ile kaldırma
> [!NOTE]
> hello birincil düğüm türü kümenizdeki Hello service fabric sistem hizmetlerini çalışır. Hiçbir zaman kapatıldı veya bu düğüm türleri örneği hello sayısı ölçeğini şekilde hangi hello güvenilirlik katmanı değerinden garanti eder. Çok başvuran[hello burada güvenilirlik katmanları hakkında ayrıntılar](service-fabric-cluster-capacity.md). 
> 
> 

Tooexecute ihtiyacınız hello aşağıdaki adımlar bir VM örneği aynı anda. Merhaba Sistem Hizmetleri (ve durum bilgisi olan hizmetlerinizi) böylece toobe kapatma düzgün biçimde kaldıracağınız hello VM örneği ve diğer düğümlerde oluşturulan yeni yinelemeler.

1. Çalıştırma [devre dışı bırakma ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) hedefi 'RemoveNode' toodisable hello düğümle tooremove (Bu düğüm türü hello yüksek örneği) oluşturacağız.
2. Çalıştırma [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake emin o hello düğüm toodisabled gerçekten moda. Aksi durumda, hello düğümü devre dışı kadar bekleyin. Bu adım hurry olamaz.
3. Merhaba örnek/hello'ndaki yönergeleri izleyin [hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello VM'lerin sayısını tek bu Nodetype. Kaldırılan hello hello yüksek VM örneği örneğidir. 
4. 1 ile gerektiğinde 3 arasındaki adımları yineleyin, ancak hiçbir zaman hello birincil düğüm türleri hangi hello güvenilirlik katmanı sağlayacağını değerinden örneği hello sayısı ölçeğini. Çok başvuran[hello burada güvenilirlik katmanları hakkında ayrıntılar](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Sanal makineleri hello birincil olmayan düğüm türü/sanal makine ölçek kümesini el ile kaldırma
> [!NOTE]
> Durum bilgisi olan bir hizmet için belirli bir sayıda düğüm toobe her zaman toomaintain kullanılabilirlik ve koruma durumunu hizmetinizin gerekir. Çok düşük Hello düğümü eşit toohello hedef çoğaltma kümesi sayısı hello bölüm/hizmetinin hello sayısı gerekir. 
> 
> 

Merhaba gereken adımları bir VM örneği aynı anda aşağıdaki hello yürütün. Bu hello Sistem Hizmetleri (ve durum bilgisi olan hizmetlerinizi) toobe düzgün biçimde hello üzerinde VM örneği kaldırdığınız kapatılamadı sağlar ve başka bir konumu yeni çoğaltmaları oluşturulur.

1. Çalıştırma [devre dışı bırakma ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) hedefi 'RemoveNode' toodisable hello düğümle tooremove (Bu düğüm türü hello yüksek örneği) oluşturacağız.
2. Çalıştırma [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake emin o hello düğüm toodisabled gerçekten moda. Aksi durumda hello düğümü devre dışı kadar bekleyin. Bu adım hurry olamaz.
3. Merhaba örnek/hello'ndaki yönergeleri izleyin [hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello VM'lerin sayısını tek bu Nodetype. Bu artık hello yüksek VM örneği kaldırır. 
4. 1 ile gerektiğinde 3 arasındaki adımları yineleyin, ancak hiçbir zaman hello birincil düğüm türleri hangi hello güvenilirlik katmanı sağlayacağını değerinden örneği hello sayısı ölçeğini. Çok başvuran[hello burada güvenilirlik katmanları hakkında ayrıntılar](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Service Fabric Explorer'da davranışlarla karşılaşabilirsiniz
Bir küme hello ölçeklendirdiğinizde Service Fabric Explorer hello kümesinin parçası olan (sanal makine ölçek kümesi örneklerinin) düğüm hello sayısını yansıtır.  Ölçeklendirmek ancak, bir küme, aşağı, gerektirmediği sürece kötü durumda görüntülenen kaldırılan hello düğümü/VM örneği görürsünüz [Kaldır ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) hello uygun düğümü ada sahip.   

Bu davranış hello açıklaması aşağıda verilmiştir.

Merhaba Service Fabric Explorer'da listelenen düğümü olan bir yansıma hangi hello Service Fabric sistem hizmetlerinin (FM özellikle) vardı ve sahip düğümleri hello küme hello sayısı hakkında bilir. Sanal makine ölçek kümesi hello ölçeklendirdiğinizde hello VM silindi ancak FM sistem hizmeti hala düşündüğü (eşlenen toohello silindi VM olan) bu hello düğüme geri dönün. Bu nedenle (Merhaba sistem durumu hatası veya bilinmeyen olabilir) Service Fabric Explorer toodisplay o düğümü sürdürür.

Bir VM kaldırıldığında bir düğüm kaldırıldığından emin sipariş toomake iki seçeneğiniz vardır:

1) Altın veya gümüş dayanıklılık düzeyini seçin (kullanılabilir yakında) kümenizdeki hello düğüm türleri için size hello altyapı tümleştirme. Ölçeklendirdiğinizde, ardından otomatik olarak hello düğümleri bizim Sistem Hizmetleri (FM) durumundan kaldırır.
Çok başvuran[hello burada dayanıklılık düzeyleri hakkında ayrıntılar](service-fabric-cluster-capacity.md)

2) Merhaba VM örneği ölçeklendirilmiş sonra toocall hello gerekir [Kaldır ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Service Fabric kümeleri belirli bir sayıda düğüm toobe yukarı adresindeki tüm hello sipariş toomaintain kullanılabilirlik ve koruma durumunda - başvurulan tooas "çekirdek koruma." gerekli Dolayısıyla, ilk yapmadığınız sürece genellikle güvenli tooshut hello kümedeki tüm hello makineler aşağı taşır bir [tam yedekleme, durumunun](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Tooalso aşağıdaki okuma hello küme kapasite planlaması, Küme yükseltme ve Hizmetleri bölümleme hakkında bilgi edinin:

* [Küme kapasitenizi planlama](service-fabric-cluster-capacity.md)
* [Küme yükseltme](service-fabric-cluster-upgrade.md)
* [En fazla ölçek için bölüm durum bilgisi olan hizmetler](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
