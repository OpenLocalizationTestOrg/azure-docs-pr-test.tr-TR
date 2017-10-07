---
title: "aaaMATLAB kümeleri sanal makinelerde | Microsoft Docs"
description: "Microsoft Azure sanal makineleri toocreate MATLAB dağıtılmış bilgi işlem sunucusu kümeleri toorun işlem yoğunluklu paralel MATLAB yüklerinizi kullanın"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Azure Vm'lerinde MATLAB dağıtılmış bilgi işlem sunucusu kümeleri oluşturma
Kullanım Microsoft Azure sanal makineleri toocreate bir veya daha fazla MATLAB dağıtılmış bilgi işlem sunucu toorun işlem yoğunluklu paralel MATLAB yüklerinizi kümeleri. Temel görüntü olarak VM toouse MATLAB dağıtılmış bilgi işlem sunucusu yazılımınızı yükleyin ve bir Azure Hızlı Başlangıç şablonu veya Azure PowerShell Betiği kullan (kullanılabilir [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy ve hello küme yönetin. Dağıtımdan sonra iş yükleri toohello küme toorun bağlanır.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>MATLAB dağıtılmış bilgi işlem sunucusu ve MATLAB hakkında
Merhaba [MATLAB](http://www.mathworks.com/products/matlab/) platform, mühendislik ve bilimsel sorunları çözmek için getirilmiştir. Büyük ölçekli benzetimleri ve veri işleme görevlerini MATLAB kullanıcılarla hesaplama kümeleri ve kılavuz Hizmetleri yararlanarak, işlem yoğunluklu iş yüklerini yedeklemek ürünleri toospeed computing MathWorks paralel kullanabilirsiniz. [Paralel bilgi işlem araç](http://www.mathworks.com/products/parallel-computing/) MATLAB kullanıcıların uygulamaları paralel hale ve çok çekirdekli işlemciler, GPU, yararlanabilir ve hesaplama kümeleri izin verir. [MATLAB dağıtılmış bilgi işlem sunucusu](http://www.mathworks.com/products/distriben/) işlem kümesindeki çok sayıda bilgisayar MATLAB kullanıcılar tooutilize sağlar.

Azure sanal makineleri kullanarak tüm MATLAB dağıtılmış bilgi işlem sunucusu kümeleri oluşturabilirsiniz hello etkileşimli işler, toplu işleri, bağımsız görevler gibi şirket içi kümeleri olarak aynı mekanizmaları kullanılabilir toosubmit paralel iş ve Görevler iletişim. Azure hello MATLAB platform ile birlikte kullanarak, birçok karşılaştırıldığında avantajları tooprovisioning sahiptir ve geleneksel kullanarak şirket içi donanım: sanal makine bir dizi boyutları, kümeleri kullanın, yalnızca hello işlem kaynaklarını ödeme için isteğe bağlı oluşturulmasını ve ölçekli Hello özelliği tootest modeller.  

## <a name="prerequisites"></a>Ön koşullar
* **İstemci bilgisayar** -dağıtımdan sonra Azure ve hello MATLAB dağıtılmış bilgi işlem sunucusu küme ile Windows tabanlı bir istemci bilgisayar toocommunicate gerekir.
* **Azure PowerShell** -bkz [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) tooinstall istemci bilgisayarınız üzerinde.
* **Azure aboneliği** -bir aboneliğiniz yoksa oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde. Daha büyük kümeleri için Kullandıkça Öde aboneliğine veya diğer satın alma seçenekleri göz önünde bulundurun.
* **Çekirdek kota** -büyük bir küme veya birden fazla MATLAB dağıtılmış bilgi işlem sunucusu küme tooincrease hello çekirdek kota toodeploy gerekebilir. tooincrease bir kota [bir çevrimiçi müşteri destek isteği açma](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) herhangi bir ücret alınmaz.
* **MATLAB, paralel bilgi işlem araç ve MATLAB dağıtılmış bilgi işlem sunucusu lisansları** -hello betikleri varsayın bu hello [MathWorks barındırılan Lisans Yöneticisi](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) için tüm lisanslar kullanılıyor.  
* **MATLAB dağıtılmış bilgi işlem sunucusu yazılım** -hello temel VM görüntüsü hello küme VM'ler için kullanılacak bir VM üzerinde yüklü.

## <a name="high-level-steps"></a>Yüksek düzey adımları
toouse Azure sanal makineleri MATLAB dağıtılmış bilgi işlem Sunucu kümeleriniz için hello aşağıdaki üst düzey adımları gereklidir. Ayrıntılı yönergeler olan üzerinde hello Hızlı Başlangıç şablonu ve betikleri eşlik hello belgelerinde [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Temel VM görüntüsü oluşturma**  

   * Bu VM MATLAB dağıtılmış bilgi işlem sunucusu yazılımları yükleyip yeniden açın.

     > [!NOTE]
     > Bu işlem birkaç saat sürebilir ancak toodo yeterlidir, MATLAB her sürümü için kullandığınız sonra.   
     >
     >
2. **Bir veya daha fazla kümeleri oluşturma**  

   * Sağlanan hello PowerShell Betiği veya hello Hızlı Başlangıç şablonu toocreate hello temel VM görüntüsü bir kümeden kullanın.   
   * Merhaba kümeleri toolist, duraklatma, sürdürme ve delete kümeleri sağlayan sağlanan hello PowerShell komut dosyasını kullanarak yönetin.

## <a name="cluster-configurations"></a>Küme yapılandırmaları
Şu anda hello küme oluşturma komut dosyasında ve şablon toocreate tek bir MATLAB dağıtılmış bilgi işlem sunucusu topolojisi etkinleştirin. İsterseniz, bir veya daha fazla ek kümeler, çalışan sanal makineleri farklı VM boyutlarını kullanarak, farklı sayıda sahip her küme oluşturun ve benzeri.

### <a name="matlab-client-and-cluster-in-azure"></a>MATLAB istemci ve küme Azure
Merhaba MATLAB istemcisi düğümü, MATLAB İş Zamanlayıcısı düğümü ve MATLAB dağıtılmış bilgi işlem sunucusu "alt düğümlerini Azure Vm'leri olarak sanal bir ağa hello aşağıda gösterildiği gibi yapılandırılır" tahmin edin.


* toouse hello küme, Uzak Masaüstü toohello istemci düğümü tarafından bağlanın. Merhaba istemci düğüm hello MATLAB istemci çalıştırır.
* Merhaba istemci düğümün tüm çalışanlar tarafından erişilebilir bir dosya paylaşımı vardır.
* MathWorks barındırılan Lisans Yöneticisi tüm MATLAB yazılım hello lisans denetimleri için kullanılır.
* Varsayılan olarak, çekirdek başına bir MATLAB dağıtılmış bilgi işlem sunucusu çalışan hello çalışan sanal makineleri üzerinde oluşturulur, ancak herhangi bir sayı belirtin.

## <a name="use-an-azure-based-cluster"></a>Azure tabanlı bir küme kullanın
Diğer tür MATLAB dağıtılmış bilgi işlem sunucusu kümeleri gibi toouse hello küme Profil Yöneticisi hello MATLAB istemcide (Merhaba istemci VM) toocreate MATLAB İş Zamanlayıcısı küme profili gerekir.

![Küme Profil Yöneticisi](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Sonraki adımlar
* Ayrıntılı yönergeler toodeploy için ve Azure MATLAB dağıtılmış bilgi işlem sunucusu kümelerinde bkz hello [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) hello şablonları ve komut dosyaları içeren havuz.
* Toohello Git [MathWorks site](http://www.mathworks.com/) ilgili ayrıntılı bilgiler MATLAB ve MATLAB dağıtılmış bilgi işlem sunucusu için.
