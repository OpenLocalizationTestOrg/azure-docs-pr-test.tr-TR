---
title: "büyük Azure sanal makine ölçek kümeleri ile aaaWorking | Microsoft Docs"
description: "Gerekenler tooknow toouse büyük Azure sanal makine ölçekleme kümeleri"
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
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>Büyük sanal makine ölçek kümeleri ile çalışma
Artık Azure oluşturabilirsiniz [sanal makine ölçek kümeleri](/azure/virtual-machine-scale-sets/) too1, 000 VM'ler yukarı kapasitesine sahip. Bu belgede, bir _büyük sanal makine ölçek kümesini_ ölçeği 100 VM'ler daha toogreater ölçeklendirme özellikli Ayarla olarak tanımlanır. Bu özellik bir ölçek kümesi özelliği ile ayarlanır (_singlePlacementGroup=False_). 

Yük Dengeleme ve hata etki alanları farklı tooa standart ölçek kümesini davranır gibi büyük ölçekli belirli özelliklerini ayarlar. Bu belge büyük ölçekli kümelerinin hello özelliklerini açıklar ve hangi tooknow toosuccessfully bunları uygulamalarınızda kullanmanız açıklar. 

Büyük ölçekli bulut altyapısını dağıtmak için ortak bir yaklaşım toocreate kümesidir _ölçek birimleri_, örneğin birden çok VM oluşturarak kümeleri birden çok sanal ağlara ve depolama hesapları arasında ölçeklendirin. Bu yaklaşım daha kolay yönetim karşılaştırıldığında toosingle VM'ler sağlar ve özellikle birden çok sanal ağlar ve uç noktaları gibi diğer yığınlanabilir bileşenleri gerektiren birçok uygulama için birden fazla ölçek birimi yararlıdır. Uygulamanızın tek bir büyük küme ancak gerektiriyorsa, tek bir ölçek too1, 000 VM'ler kümesi daha kolay toodeploy olabilir. Örnek senaryolar arasında merkezi büyük veri dağıtımları veya büyük bir çalışan düğümü havuzunun basit yönetimini gerektiren işlem kılavuzları sayılabilir. VM ölçek kümesi ile birlikte [veri diskleri ekli](virtual-machine-scale-sets-attached-disks.md), büyük ölçekli kümeleri etkinleştirmek, toodeploy binlerce çekirdek ve tek bir işlem olarak depolama petabaytlarca oluşan ölçeklenebilir bir altyapı.

## <a name="placement-groups"></a>Yerleştirme grupları 
Kılan bir _büyük_ ölçeği özel Ayarla VM hello sayısı, ancak hello sayısı değil _yerleştirme grupları_ içeriyor. Bir yapı benzer tooan Azure kullanılabilirlik kümesi, kendi hata etki alanları ve yükseltme etki alanları ile bir yerleştirme grubudur. Varsayılan olarak, bir ölçek kümesi en fazla 100 VM boyutuna sahip tek bir yerleştirme grubundan oluşur. Bir ölçek adlı özellik ayarlarsanız _singlePlacementGroup_ too_false_, ayarlanır hello ölçek kümesini birden çok yerleştirme grupları oluşturulabilir ve 0-1000 aralığındadır VM'ler. Toohello varsayılan değer olarak ayarlandığında _doğru_, Ölçek kümesini tek yerleştirme grubu oluşur ve 0-100 aralığındadır VM'ler.

## <a name="checklist-for-using-large-scale-sets"></a>Büyük ölçek kümelerini kullanmaya ilişkin denetim listesi
toodecide etkili kullanımını büyük ölçekli kümeleri, uygulamanızın yapabilirsiniz olup olmadığını hello aşağıdaki gereksinimleri göz önünde bulundurun:

- Büyük ölçek kümeleri Azure Yönetilen Diskleri gerektirir. Yönetilen Diskler ile oluşturulmayan ölçek kümeleri birden fazla depolama hesabı (her 20 VM için bir tane) gerektirir. Büyük ölçekli, özel olarak aboneliğinize çalıştıran depolama yönetim ek yükü ve tooavoid hello riskini depolama hesapları için sınırlar yönetilen diskleri tooreduce ile tasarlanmış toowork kümeleridir. Yönetilen diskleri kullanmazsanız, Ölçek sınırlı too100 VM'ler kümesidir.
- Azure Market görüntülerden oluşturulan ölçek kümeleri too1, 000 VM'ler ölçeklendirebilirsiniz.
- Özel resimler (oluşturmak ve kendiniz yüklemek VM görüntüleri) oluşturulan ölçek kümeleri şu anda too100 Vm'leri ölçeklendirebilirsiniz.
- Katman 4 Yük Dengeleme Hello Azure yük dengeleyici ile birden çok yerleştirme gruplardan oluşan ölçek kümeleri için henüz desteklenmiyor. Azure yük dengeleyici olmak emin hello Ölçeği Ayarla toouse hello gerekiyorsa yapılandırılmış toouse hello varsayılan ayar olan bir tek yerleştirme, grubudur.
- Katman 7 Yük Dengeleme Hello Azure uygulama ağ geçidi ile tüm ölçek kümeleri için desteklenir.
- Ölçek kümesini tek bir alt ağ ile tanımlanan - gereksinim duyduğunuz tüm hello VM'ler için yeterince büyük bir adres alanı alt ağınızı sahip olduğundan emin olun. Varsayılan olarak bir ölçek overprovisions kümesi (hangi sizin için sizden ücret istenmese fazladan VM'ler dağıtım zamanında veya çıkışı, ölçekleme sırasında oluşturur) tooimprove dağıtım güvenilirlik ve performans. Bir adres alanı % 20 tooscale için planlama VM'ler hello sayısından daha izin verir.
- Birçok VM toodeploy planlıyorsanız, işlem çekirdek kotası artan toobe gerekebilir.
- Hata etki alanları ve yükseltme etki alanları yalnızca bir yerleştirme grubu içinde tutarlıdır. Bu mimari hello değiştirmez genel kullanılabilirlik bir ölçek kümesi, sanal makineleri farklı fiziksel donanım üzerinde dağılımla, ancak iki VM olan farklı donanım üzerinde tooguarantee ihtiyacınız varsa, farklı hatası olduklarından emin olmak anlamına gelir mu etki alanlarında aynı yerleştirme Grup hello. Hata etki alanı ve yerleştirme Grup Kimliği hello gösterilen _örnek görünümü_ VM ölçeğini ayarlayın. VM ölçek kümesi örnek görünümünü hello hello görüntüleyebilirsiniz [Azure kaynak Gezgini](https://resources.azure.com/).


## <a name="creating-a-large-scale-set"></a>Büyük ölçek kümesi oluşturma
Ölçeği hello Azure portal Ayarla oluşturduğunuzda, onu tooscale toomultiple yerleştirme grupları ayarlama hello tarafından izin verebilirsiniz _sınırı tooa tek yerleştirme grup_ seçeneği too_False_ hello içinde _Temelleri_ dikey. Bu seçenek kümesi too_False_ belirttiğiniz bir _örnek sayısını_ değerini too1, 000 ayarlama.

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

Merhaba kullanılarak ayarlanan büyük bir VM ölçek oluşturabilirsiniz [Azure CLI](https://github.com/Azure/azure-cli) _az vmss oluşturma_ komutu. Bu komut hello bağlı alt ağ boyutu gibi akıllı varsayılan ayarlar _örnek sayısı_ bağımsız değişkeni:

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
Bu hello Not _vmss oluşturma_ bunları belirtmezseniz, komut Varsayılanları bazı yapılandırma değerleri. geçersiz kılabilirsiniz toosee hello kullanılabilir seçenekleri deneyin:
```bash
az vmss create --help
```

Bir Azure Resource Manager şablonu oluşturma tarafından ayarlanmış büyük bir ölçekte oluşturuyorsanız, yönetilen Azure disklerde dayalı bir ölçek kümesini hello şablon oluşturur emin olun. Merhaba ayarlayabilirsiniz _singlePlacementGroup_ özelliği too_false_ hello içinde _özellikleri_ hello bölümünü _Microsoft.Compute/virtualMAchineScaleSets_ kaynak. Merhaba aşağıdaki JSON parça gösterir hello 1.000 VM kapasitesi ve hello gibi bir ölçek kümesi şablonu hello başlangıcını _"singlePlacementGroup": yanlış_ ayarı:
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
Büyük ölçekli tam bir örnek için şablon ayarlama, çok bakın[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json).

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>Varolan bir ölçek dönüştürme toospan birden çok yerleştirme grupları
var olan bir VM ölçek kümesi 100 VM'ler daha toomore ölçeklendirme özellikli toomake toochange hello ihtiyacınız _singplePlacementGroup_ özelliği too_false_ hello ölçeğinde modeli ayarlayın. Bu özelliğin hello ile değiştirilmesi test [Azure kaynak Gezgini](https://resources.azure.com/). Mevcut bir ölçek kümesini, select Bul _Düzenle_ hello değiştirip _singlePlacementGroup_ özelliği. Bu özellik görmüyorsanız hello ölçeği hello Microsoft.Compute API daha eski bir sürümü Ayarla görüntüleme.

>[!NOTE] 
Birden çok yerleştirme gruplarını destekleyen bir tek yerleştirme grubu yalnızca (Merhaba, varsayılan davranıştır) tooa destekleyen ayarlamak ölçek değiştirebilirsiniz, ancak hello şekilde dönüştürülemiyor. Bu nedenle dönüştürmeden önce büyük ölçekli kümeleri hello özelliklerini anladığınızdan emin olun. Özellikle, katman 4 Yük Dengeleme hello Azure yük dengeleyici ile gerekmez emin olun.


