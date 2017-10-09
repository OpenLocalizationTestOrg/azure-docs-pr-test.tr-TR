---
title: aaaMigrate VM'ler tooResource Azure CLI kullanarak Manager | Microsoft Docs
description: "Bu makalede, Azure CLI kullanarak Klasik tooAzure Resource Manager hello platform desteklenen geçiş kaynakların anlatılmaktadır"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Azure CLI kullanarak Klasik tooAzure Resource Manager Iaas kaynaklarını geçirme
Bu adımlar nasıl hello Klasik dağıtım modeli toohello Azure Resource Manager dağıtım modeli hizmet (Iaas) kaynaklardan olarak toomigrate altyapı toouse Azure komut satırı arabirimi (CLI) komutları gösterir. Merhaba makale gerektirir hello [Azure CLI](../../cli-install-nodejs.md).

> [!NOTE]
> Burada açıklanan tüm hello ıdempotent işlemleridir. Desteklenmeyen bir özellik veya bir yapılandırma hatası başka bir sorun varsa, hello yeniden deneme öneririz hazırlamak, iptal etmek veya yürütme işlemi. Merhaba platform sonra hello eylemi yeniden deneyecek.
> 
> 

<br>
Adımları bir geçiş işlemi sırasında yürütülen toobe gereken bir akış çizelgesi tooidentify hello siparişi İşte

![Merhaba geçiş adımlarını gösteren ekran görüntüsü](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>1. adım: geçiş için hazırlama
Klasik tooResource Yöneticisi geçirme Iaas kaynaklardan değerlendirirken öneririz birkaç en iyi uygulamalar şunlardır:

* Merhaba okuma [desteklenmeyen yapılandırmaları veya özellikleri listesi](../windows/migration-classic-resource-manager-overview.md). Desteklenmeyen yapılandırmaları veya özellikleri kullanan sanal makineler varsa, hello özelliği/yapılandırma desteği toobe duyurdu için beklemenizi öneririz. Alternatif olarak, bu özelliği kaldırmak veya gereksinimlerinize uygun yapılandırma tooenable geçişin dışına taşıyın.
* Bugün, altyapı ve uygulamalarınızı dağıtma komut otomatik değilse, geçiş için bu komut dosyalarını kullanarak toocreate benzer bir test Kurulum deneyin. Alternatif olarak, örnek ortamları hello Azure portal kullanarak ayarlayabilirsiniz.

> [!IMPORTANT]
> Uygulama ağ geçitleri, Klasik tooResource Yöneticisi geçiş için şu anda desteklenmemektedir. toomigrate bir uygulama ağ geçidi ile klasik sanal ağ hazırlama işlemi toomove hello ağ çalıştırmadan önce hello ağ geçidi kaldırın. Merhaba ağ geçidi Azure Kaynak Yöneticisi'nde hello geçişi tamamlandıktan sonra yeniden bağlanın. 
>
>ExpressRoute ağ geçidi başka bir Abonelikteki tooExpressRoute devreler bağlanma otomatik olarak geçirilemez. Böyle durumlarda, hello ExpressRoute ağ geçidi kaldırın, hello sanal ağını geçirin ve hello ağ geçidi oluşturun. Lütfen bakın [geçirmek ExpressRoute bağlantı hattına ve hello Klasik toohello Resource Manager dağıtım modeli sanal ağlardan ilişkili](../../expressroute/expressroute-migration-classic-resource-manager.md) daha fazla bilgi için.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>2. adım: aboneliğinizi ayarlamak ve hello sağlayıcısını Kaydet
Geçiş senaryoları için her iki Klasik için ortamınızı kurma tooset gerekir ve Resource Manager. [Azure CLI yükleme](../../cli-install-nodejs.md) ve [aboneliğinizi seçin](../../xplat-cli-connect.md).

Oturum açma tooyour hesabı.

    azure login

Komutu aşağıdaki hello kullanarak Hello Azure aboneliği seçin.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> Kayıt bir kez, ancak ihtiyaçlarını kez geçiş işlemini denemeden önce bitti toobe adımıdır. Kaydettirmeden hello aşağıdaki hata iletisini görürsünüz 
> 
> *BadRequest: Abonelik geçiş için kayıtlı değil.* 
> 
> 

Merhaba geçiş kaynak sağlayıcısı ile komutu aşağıdaki hello kullanarak kaydedin. Bazı durumlarda, bu komut zaman aşımına uğruyor olduğunu unutmayın. Ancak, hello kaydı başarılı olur.

    azure provider register Microsoft.ClassicInfrastructureMigrate

Merhaba kayıt toofinish için beş dakika bekleyin. Komutu aşağıdaki hello kullanarak hello hello onay durumunu kontrol edebilirsiniz. RegistrationState olduğundan emin olun `Registered` devam etmeden önce.

    azure provider show Microsoft.ClassicInfrastructureMigrate

Şimdi CLI toohello geçiş `asm` modu.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>3. adım: hello geçerli dağıtım veya VNET Azure bölgesi yeterli Azure Resource Manager sanal makinesi çekirdeğe sahip olduğunuzdan emin olun
Bu adımda, tooswitch çok gerekir`arm` modu. Bu komutu aşağıdaki hello ile yapın.

```
azure config mode arm
```

CLI komutu toocheck hello geçerli miktarını Azure Kaynak Yöneticisi'nde sahip Çekirdek aşağıdaki hello kullanabilirsiniz. toolearn çekirdek kotaları hakkında daha fazla bilgi görmek [sınırları ve hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

İşiniz bittiğinde bu adımı doğrulanıyor, geri çok geçebilirsiniz`asm` modu.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>4. adım: 1. seçenek - sanal makineler bir bulut hizmetinde geçirme
Komutu aşağıdaki hello kullanarak bulut Hizmetleri ve çekme hello bulut hizmeti toomigrate istediğiniz Get hello listesi. Merhaba VM'ler hello bulut hizmetindeki bir sanal ağ veya web/çalışan rolleri varsa, bir hata iletisi alırsınız unutmayın.

    azure service list

Merhaba ayrıntılı çıktı komutu tooget hello dağıtım adı hello bulut hizmeti için aşağıdaki hello çalıştırın. Çoğu durumda, hello dağıtım adı olduğu hello hello bulut hizmet adı ile aynı.

    azure service show <serviceName> -vv

Merhaba aşağıdaki komutları kullanarak hello bulut hizmeti geçirirseniz ilk olarak, doğrulama:

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

Merhaba sanal makineleri hello bulut hizmetinde geçiş için hazırlayın. Gelen iki seçenekleri toochoose sahip.

Toomigrate hello VM'ler tooa platform tarafından oluşturulan sanal ağ istiyorsanız, komutu aşağıdaki hello kullanın.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Merhaba Resource Manager dağıtım modelinde sanal ağ varolan toomigrate tooan istiyorsanız, komutu aşağıdaki hello kullanın.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Merhaba hazırladıktan sonra işlemi başarılı olur, hello ayrıntılı çıktı tooget hello geçiş durumunu hello VM'ler bakın ve hello olduklarından emin olun `Prepared` durumu.

    azure vm show <vmName> -vv

CLI veya hello Azure portal kullanarak kaynakları hazırlanmış hello için başlangıç yapılandırmasını denetleyin. Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız, komutu aşağıdaki hello kullanın.

    azure service deployment abort-migration <serviceName> <deploymentName>

Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları uygulayın.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>4. adım: 2. seçenek - bir sanal ağdaki sanal makineleri geçirme
Çekme hello sanal ağ toomigrate istiyor. Not Hello sanal ağ ile desteklenmeyen yapılandırmalar web/çalışan rolleri veya VM'ler içeriyorsa, bir doğrulama hata iletisi alırsınız.

Tüm hello sanal ağlar, komutu aşağıdaki hello kullanarak hello abonelikte alın.

    azure network vnet list

Merhaba çıktı aşağıdakine benzer görünecektir:

![Vurgulanan hello tüm sanal ağ adıyla hello komut satırının ekran görüntüsü.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

Yukarıdaki örnek Hello hello **virtualNetworkName** hello tüm adı **"Grubu classicubuntu16 classicubuntu16"**.

İlk olarak, komutu aşağıdaki hello kullanarak hello sanal ağ geçirirseniz doğrulama:

```shell
azure network vnet validate-migration <virtualNetworkName>
```

Tercih ettiğiniz Hello sanal ağ, komutu aşağıdaki hello kullanarak geçiş için hazırlayın.

    azure network vnet prepare-migration <virtualNetworkName>

CLI veya hello Azure portal kullanarak sanal makineleri hazırlanmış hello için başlangıç yapılandırmasını denetleyin. Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız, komutu aşağıdaki hello kullanın.

    azure network vnet abort-migration <virtualNetworkName>

Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları uygulayın.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>5. adım: bir depolama hesabını geçirin
Merhaba sanal makinelerin geçirilmesine bitirdiğinizde hello depolama hesabını geçirin öneririz.

Komutu aşağıdaki hello kullanarak Hello depolama hesabı geçiş için hazırlama

    azure storage account prepare-migration <storageAccountName>

Depolama hesabı CLI veya hello Azure portal kullanarak hazırlanmış hello için başlangıç yapılandırmasını denetleyin. Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız, komutu aşağıdaki hello kullanın.

    azure storage account abort-migration <storageAccountName>

Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları uygulayın.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>Sonraki adımlar

* [Klasik tooAzure Resource Manager Iaas kaynaklardan platform desteklenen geçişini genel bakış](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini planlama](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Klasik tooAzure Resource Manager PowerShell toomigrate Iaas kaynakları kullanın](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini ile Yardım için topluluk araçları](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [En sık karşılaşılan geçiş hatalarını gözden geçirme](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Gözden geçirme hello en sık Klasik tooAzure Kaynak Yöneticisi geçirme Iaas kaynaklardan hakkında sorular](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
