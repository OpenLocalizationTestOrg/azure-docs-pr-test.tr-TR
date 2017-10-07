---
title: "Windows Server ve Linux üzerinde aaaCreate Azure Service Fabric kümeleri | Microsoft Docs"
description: "Windows Server ve anlamına gelir Linux çalıştıran Service Fabric kümeleri mümkün toodeploy ve ana bilgisayar Service Fabric uygulamaları Windows Server veya Linux çalıştırabilirsiniz herhangi bir yerde olması."
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Windows Server veya Linux Service Fabric kümeleri oluşturma
Azure Service Fabric kümesi bir ağa bağlı içine, mikro dağıtılır ve yönetilen sanal veya fiziksel makineler kümesidir. Bir küme düğümü bir makine ya da bir kümenin parçasıysa VM adı verilir. Küme düğümlerinin toothousands ölçeklendirebilirsiniz. Yeni düğümler toohello kümesi eklerseniz, Service Fabric hello hizmet çoğaltmalarını ve örnekleri düğümleri artan hello sayısı arasında yeniden dengeler. Genel uygulama performansını artıran ve erişim toomemory için çekişmeyi azaltır. Merhaba kümedeki Hello düğümler verimli bir şekilde kullanılmayan, hello hello kümedeki düğüm sayısını azaltabilirsiniz. Service Fabric yeniden hello çoğaltmalarını yeniden dengeler ve her düğümde hello donanım düğümleri toomake azaltılabilir hello sayısı örneklerinde daha iyi kullanın.

Service Fabric Service Fabric kümeleri herhangi bir VM veya Windows Server veya Linux çalıştıran bilgisayarlar üzerinde hello oluşturulmasını sağlar. Bu mümkün toodeploy olduğu ve Service Fabric uygulamaları birbirine bağlı bir Windows Server veya Linux bilgisayarlar kümesi sahip olduğu herhangi bir ortamda çalıştırılabilir anlamına gelir, şirket içi, Microsoft Azure olması veya herhangi bir bulut sağlayıcısı ile.

## <a name="create-service-fabric-clusters-on-azure"></a>Azure'da Service Fabric kümeleri oluşturma
Azure üzerinde bir küme oluşturma ya da bir kaynak modeli şablonu veya hello Azure portal aracılığıyla yapılır. Okuma [Resource Manager şablonu kullanarak bir Service Fabric kümesi oluşturma](service-fabric-cluster-creation-via-arm.md) veya [hello Azure portal ' Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-portal.md) daha fazla bilgi için.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Azure üzerinde kümeleri için desteklenen işletim sistemleri
Bu işletim sistemlerini çalıştıran VM'ler mümkün toocreate kümelerinde şunlardır:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04 (önizlemede ortak) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Service Fabric tek başına içi kümeleri oluşturmak veya herhangi bir bulut sağlayıcısı ile
Service Fabric bir yükleme paketi, toocreate tek başına Service Fabric kümeleri şirket içi veya herhangi bir bulut sağlayıcısına sağlar

Windows Server'da tek başına service fabric ayarlama hakkında daha fazla bilgi kümeleri için okuma [Windows Server için Service Fabric kümesi oluşturma](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Şirket içi dağıtımları ve tüm bulut dağıtımları
Şirket içi bir Service Fabric kümesi oluşturmak için hello işlem VM'ler kümesi olan tercih ettiğiniz herhangi bir buluta bir küme oluşturma benzer toohello işlemidir. Merhaba başlangıç adımları tooprovision hello VM'ler hello bulut sağlayıcısı veya kullanmakta olduğunuz şirket içi ortamı tarafından yönetilir. VM ile birlikte bir dizi olduktan sonra bunlar arasında etkin ağ bağlantısı sonra hello Service Fabric paketi kurma adımları tooset Merhaba, hello küme ayarlarını düzenlemek ve hello küme oluşturma çalıştırmak ve yönetim komut dosyaları aynıdır. Bu bilgi ve işletim ve Service Fabric kümelerini yönetme deneyimi transfer edilebilir yeni barındırma ortamları tootarget seçtiğinizde sağlar.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Tek başına Service Fabric kümeleri oluşturma avantajları
* Ücretsiz toochoose olan herhangi bir sağlayıcı toohost kümenizi bulut.
* Service Fabric uygulamaları, bir kez yazılmış, en az toono değişikliklerle birden çok barındırma ortamlarında çalıştırabilirsiniz.
* Service Fabric uygulamaları oluşturma bilgi bir barındırma ortamı tooanother taşır.
* Çalıştıran ve Service Fabric yöneten işlemsel deneyimi taşıyan üzerinden bir ortam tooanother kümeleri.
* Geniş müşteri ulaşma ortamı kısıtlamaları barındırarak sınırsız.
* Güvenilirlik ve yaygın kesintilere karşı koruma fazladan bir katmanı, bir veri merkezi, tooanother dağıtım ortamı hello Hizmetleri taşıyabilirsiniz veya bir Kararma bulut sağlayıcısı için bulunmaktadır.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Tek başına kümeleri için desteklenen işletim sistemleri
VM'ler veya bu işletim sistemlerini çalıştıran bilgisayarlara yükleyebilirsiniz toocreate kümelerinde şunlardır:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (yakında)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Şirket içi Azure Service Fabric kümelerinde tek başına Service Fabric kümeleri üzerinden avantajları oluşturuldu
Service Fabric kümeleri Azure üzerinde çalışan hello şirket içi seçeneğini avantaj sağlar şekilde kümelerinizi çalıştırdığı için belirli gereksinimlere sahip değilseniz, ardından Azure üzerinde çalıştırmanızı öneririz. Azure üzerinde biz diğer Azure özellikleri ve işlemleri ve hello küme yönetimi daha kolay ve daha güvenilir yapar Hizmetleri ile tümleştirme sağlar.

* **Azure portal:** Azure portal kümelerini yönetmek ve kolay toocreate kolaylaştırır.
* **Azure Resource Manager:** kullanım Azure Kaynak Yöneticisi'nin bir birim olarak hello küme tarafından kullanılan tüm kaynakları kolay yönetilmesine izin verir ve maliyet izleme ve faturalama basitleştirir.
* **Service Fabric kümesi bir Azure kaynağı olarak** A Service Fabric kümesi diğer Azure ARM kaynaklarında yaptığınız gibi model bir ARM kaynak olduğundan.
* **Azure altyapısı ile tümleştirme** Service Fabric koordinatları Azure altyapı işletim sistemi, ağ ve diğer yükseltmeler tooimprove kullanılabilirliği ve güvenilirliği uygulamalarınız için temel alınan hello ile.  
* **Tanılama:** Azure üzerinde tümleştirme Azure tanılama ve günlük analizi ile sağlıyoruz.
* **Otomatik ölçeklendirme:** Azure ile ilgili daha fazla kümeler için yerleşik otomatik ölçeklendirme işlevi tooVirtual makine ölçekleme kümeleri son sağlıyoruz. Şirket içi ve diğer bulut ortamları, kendi otomatik ölçeklendirme özelliğini veya hello Service Fabric sunan API'leri kümeleri ölçekleme için kullanarak el ile ölçek toobuild sahiptir.

## <a name="next-steps"></a>Sonraki adımlar

* Vm'leri veya Windows Server çalıştıran bilgisayarlarda bir küme oluşturun: [Windows Server için Service Fabric kümesi oluşturma](service-fabric-cluster-creation-for-windows-server.md)
* Sanal makineleri veya Linux çalıştıran bilgisayarlarda bir küme oluşturun: [Linux'ta Service Fabric](service-fabric-linux-overview.md)
* [Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin

