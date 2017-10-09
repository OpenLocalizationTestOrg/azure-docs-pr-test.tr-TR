---
title: "aaaAdd veri bloğu düğümleri tooan HPC paketi küme | Microsoft Docs"
description: "Nasıl tooexpand bir HPC paketi küme Azure isteğe bağlı bir bulut hizmetinde çalışan çalışan rolü örnekleri ekleyerek öğrenin"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>İsteğe bağlı "veri bloğu" düğümleri tooan HPC paketi küme Azure'da Ekle
Ayarladığınız varsa bir [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) küme Azure içinde tooquickly ölçek hello küme kapasite yukarı veya aşağı, bir dizi korumadan işlem düğümü VM'ler önceden yapılandırılmış şekilde isteyebilirsiniz. Bu makale size gösterir nasıl tooadd isteğe bağlı "veri bloğu" düğümleri (çalışan rolü örnekleri bir bulut hizmetinde çalışan) olarak Azure işlem kaynakları tooa baş düğümü. 

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

![Düğümleri veri bloğu][burst]

Bu makaledeki adımları Hello Azure düğümleri kolayca eklemenize yardım tooa bulut tabanlı HPC paketi üstbilgi düğümü VM test veya kavram kanıtı dağıtımı için. Merhaba üst düzey adımlardır hello hello adımları çok "tooAzure veri bloğu gibi" aynı tooadd bulut işlem kapasitesi tooan şirket içi HPC Pack kümesi. Bir öğretici için bkz: [Microsoft HPC paketi ile karma işlem kümesi ayarlama](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Ayrıntılı yönergeler ve üretim dağıtımlarında değerlendirmeleri için bkz: [veri bloğu Microsoft HPC paketi ile tooAzure](https://technet.microsoft.com/library/gg481749.aspx).

## <a name="prerequisites"></a>Ön koşullar
* **Bir Azure VM dağıtılan HPC paketi üstbilgi düğümü** -tek başına bir baş düğüm VM veya daha büyük bir kümenin parçası olan bir kullanabilirsiniz. tek başına bir baş düğüm toocreate bkz [bir HPC Pack baş düğümünde Azure VM'deki dağıtmak](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Otomatik HPC paketi küme dağıtım seçenekleri için bkz: [seçenekleri toocreate ve Microsoft HPC Pack ile azure'da Windows HPC Kümesi yönetmek](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
  > [!TIP]
  > Merhaba kullanırsanız [HPC Pack Iaas dağıtım betiği](hpcpack-cluster-powershell-script.md) toocreate hello küme Azure, Azure veri bloğu düğümler otomatik dağıtımınızda içerebilir. Bu makalede Hello örneklere bakın.
  > 
  > 
* **Azure aboneliği** -tooadd Azure seçebileceğiniz düğümler, aynı abonelik kullanılan toodeploy hello baş düğüm VM veya farklı bir abonelik (veya abonelikler) hello.
* **Çekirdek kota** -özellikle çok çekirdekli boyutlarıyla birkaç Azure düğümleri toodeploy seçerseniz tooincrease hello kota çekirdek, gerekebilir. tooincrease bir kota [bir çevrimiçi müşteri destek isteği açma](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) herhangi bir ücret alınmaz.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>1. adım: Azure düğümleri bir bulut hizmeti ve hello için bir depolama hesabı oluşturma
Merhaba Klasik Azure portalı veya eşdeğer Araçlar tooconfigure hello gerekli toodeploy olan kaynaklar aşağıdaki Azure düğümleri kullanın:

* Yeni bir Azure bulut hizmeti
* Yeni bir Azure depolama hesabı

> [!NOTE]
> Aboneliğinizde var olan bir bulut hizmeti yeniden yok. 
> 
> 

**Dikkat edilmesi gerekenler**

* Toocreate planladığınız her Azure düğüm şablonu için ayrı bulut hizmeti yapılandırın. Ancak, kullanabileceğiniz hello birden çok düğüm şablonları için aynı depolama hesabı.
* Hello hello bulut hizmeti ile Merhaba depolama hesabı hello dağıtımı için bulun öneririz aynı Azure bölgesi.

## <a name="step-2-configure-an-azure-management-certificate"></a>2. adım: Azure yönetim sertifikası yapılandırma
tooadd Azure işlem kaynaklarını gibi düğümler, karşılık gelen bir sertifika toohello Azure aboneliği hello dağıtımı için kullanılan bir yönetim sertifikası hello baş düğüm ve karşıya yükleme gerekiyor.

Bu senaryo için hello seçebilirsiniz **varsayılan HPC Azure yönetim sertifikası** HPC paketi yükler ve baş düğümünde otomatik olarak yapılandırır. Bu sertifika, amaçları ve kavram kanıtı dağıtımları test etmek için kullanışlıdır. toouse Bu sertifika, dosya C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer hello baş düğümünden VM toothe abonelik karşıya yükleyin. Merhaba tooupload hello sertifikada [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **ayarları** > **yönetim sertifikaları**.

Ek seçenekler tooconfigure hello yönetim sertifikası için bkz: [senaryoları tooConfigure hello Azure veri bloğu dağıtımları için Azure yönetim sertifikası](http://technet.microsoft.com/library/gg481759.aspx).

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>3. adım: Azure düğümleri toohello küme dağıtma
Merhaba adımları tooadd ve Azure Başlat düğümleri Bu senaryoda olan genellikle hello aynı bir şirket içi baş düğüm hello adımlara olarak. Aşağıdaki bölümlerde hello daha fazla bilgi için bkz [tooDeploy Azure düğümleri Microsoft HPC Pack ile adımları](https://technet.microsoft.com/library/gg481758.aspx):

* Bir Azure düğüm şablonu oluşturma
* Azure düğümleri toohello Windows HPC Kümesi Ekle
* (Sağlayamaz) başlangıç Azure düğümleri hello

Ekleyip hello düğümleri başlatın sonra toouse toorun küme işleri hazır.

Azure düğümleri dağıtımı sırasında sorunlarla karşılaşırsanız, bkz: [sorun giderme dağıtımları, Azure düğümleri Microsoft HPC paketi ile](http://technet.microsoft.com/library/jj159097.aspx).

## <a name="next-steps"></a>Sonraki adımlar
* hello konuları Bkz toouse işlem yoğunluklu örnek boyutu hello için veri bloğu düğümleri [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Otomatik olarak büyütür veya küçültür istiyorsanız, bilgi işlem kaynakları hello küme iş yükü göre Azure Merhaba, bkz: [otomatik olarak Büyüt ve Azure işlem kaynakları bir HPC Pack kümesindeki Küçült](hpcpack-cluster-node-autogrowshrink.md).

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
