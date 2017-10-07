---
title: "Sanal makine ölçek kümeleri ile aaaTroubleshoot otomatik ölçeklendirme | Microsoft Docs"
description: "Sanal makine ölçek kümeleri olan otomatik ölçeklendirme sorunlarını giderin. Karşılaşılan tipik sorunları anlamak ve nasıl tooresolve bunları."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>Sanal makine ölçek kümeleri ile sorun giderme otomatik ölçeklendirme
**Sorun** – otomatik ölçeklendirmeyi altyapı VM ölçek kümesi kullanarak Azure Resource Manager ile oluşturduğunuz – bu gibi bir şablon dağıtarak örneğin: https://github.com/Azure/azure-quickstart-templates/tree/master/201- vmss-bottle-otomatik ölçeklendirme – ölçek kurallarınızı tanımlanmış olması ve isteğe bağlı olarak hello VM'ler üzerinde put ne kadar yük olursa olsun, otomatik ölçeklendirme olmaz ancak bu harika, çalışır.

## <a name="troubleshooting-steps"></a>Sorun giderme adımları
Bazı şeyleri tooconsider şunları içerir:

* Her VM kaç çekirdeğe sahip ve her çekirdek yükleniyor? Merhaba örnek Azure Hızlı Başlangıç şablonu yukarıdaki tek bir çekirdek yükleyen bir do_work.php komut dosyası yok. Standard_A1 veya D1 sonra bu yük birden çok kez toorun gerekir gibi tek bir çekirdek VM boyutu büyük bir VM kullanıyorsanız. Kaç tane Vm'leriniz çekirdek gözden geçirerek denetleyin [boyutları için Windows azure'da sanal makineler](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Merhaba VM ölçek kümesi, kaç tane Vm'lerde, her bir iş yapmakta olduğunuz?
  
    Merhaba ortalama zaman arasında CPU olay genişletme yalnızca devre dışı gerçekleşecek **tüm** ölçek kümesindeki sanal makineleri hello hello otomatik ölçeklendirme kurallarında tanımlanan hello eşik değeri, iç hello zamanla aşıyor.
* Herhangi bir ölçek olayı eksik olabilir mi?
  
    Merhaba ölçek olayları için Azure portalı Hello denetim günlüklerini denetleyin. Belki de var. ölçek yukarı ve bir ölçekte da aşağı kaçırılan. "Ölçek" tarafından filtreleyebilirsiniz...
  
    ![Denetim Günlükleri][audit]
* Ölçek ve genişletme eşikleri yeterince farklı misiniz?
  
    Ortalama CPU % 50'den az olduğunda bir ortalama CPU 5 dakika boyunca % 50'den büyük olduğunda çıkışı kural tooscale ve tooscale ayarlayın varsayalım. CPU kullanımı ile sürekli artırma ve azaltma hello ölçeklendirme eylemi Kapat toothis eşik olduğunda bu hello kümesinin boyutu "flapping" sorunu neden olur. Bu nedenle, hello otomatik ölçeklendirme hizmeti tooprevent "dalgalanma", hangi değil ölçeklendirme olarak bildirilebilir çalışır. Bu nedenle bazı ölçeklendirme arasında boşluk yeterince farklı tooallow genişleme ve ölçek bileşenini eşikleri olduğundan emin olun.
* Kendi JSON şablonunu yazdım?
  
    Kolay toomake hatalar olduğundan, bu nedenle, yukarıdaki toowork kanıtlanmış hello gibi bir şablon ile başlayın ve küçük artımlı değişiklikleri yapın. 
* El ile içeri veya dışarı ölçekleme yapabilirsiniz?
  
    El ile yeniden dağıtırken hello VM ölçek kümesi kaynak VM'ler farklı "kapasitesi" ayarı toochange hello sayıda deneyin. Bu hazır bir örnek şablon toodo: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing – tooedit hello şablonu toomake hello olduğundan emin gerekebilir aynı makine boyutu ölçek kümesi kullanma gibi. Ardından VM'ler hello sayısı el ile başarılı bir şekilde değiştirirseniz, yalıtılmış tooautoscale hello sorun olduğunu bildiğiniz.
* Microsoft.Compute/virtualMachineScaleSet denetleyin ve hello Microsoft.ınsights kaynaklarında [Azure kaynak Gezgini](https://resources.azure.com/)
  
    Bu bir vazgeçilmez olan sorun giderme, gösteren aracı hello Azure Resource Manager kaynaklarınızı durumu. Aboneliğinizi tıklatın ve kaynak grubu sorun gidermekte olduğunuz hello arayın. Hello işlem kaynak sağlayıcısı altında hello sırasında oluşturduğunuz VM ölçek kümesi arayın ve Merhaba, gösterir örnek görünümünü kontrol hello dağıtımının durumu. Ayrıca hello örneği görünümünde VM'ler hello VM ölçek kümesi denetleyin. Ardından hello Microsoft.ınsights kaynak sağlayıcısını gidin ve hello otomatik ölçeklendirme kurallarını iyi görünen denetleyin.
* Merhaba tanılama uzantısını çalışma ve performans verilerini yayma?
  
    **Güncelleştirme:** Azure otomatik ölçeklendirme, bir ana bilgisayar tabanlı artık yüklü bir tanılama uzantısını toobe gerektiren ölçüm ardışık Gelişmiş toouse açıldı. Sonraki birkaç hello yani paragrafları artık geçerli hello yeni işlem hattı kullanarak otomatik ölçeklendirmeyi uygulama oluşturmak istiyorsanız. Dönüştürülen toouse Merhaba ana ardışık silinmiş Azure şablonları örneğidir: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale. 
  
    Otomatik ölçeklendirme için ana bilgisayar tabanlı ölçümleri kullanarak aşağıdaki nedenlerden hello için daha iyi olur:
  
  * Tanılama uzantısız olarak daha az hareketli parça yüklü toobe gerekir.
  * Daha basit şablonları. Şablon Öngörüler otomatik ölçeklendirme kurallarını tooan varolan ölçek kümesi eklemeniz yeterlidir.
  * Daha güvenilir raporlama ve yeni Vm'leri daha hızlı başlatma.
    
    Merhaba yalnızca tanılama uzantısını kullanarak tookeep isteyebilirsiniz nedeniyle Bellek Tanılama raporlama/ölçeklendirme gerekip gerekmediğini olacaktır. Ana bilgisayar tabanlı ölçümleri bellek bildirmez.
    
    Otomatik ölçeklendirmeyi için hala tanılama uzantılarını kullanıyorsanız, aklınızda yalnızca Merhaba, bu makalenin kalanında izleyin.
    
    Otomatik ölçeklendirme Azure Kaynak Yöneticisi'nde çalışabilirsiniz (ancak artık gerekir) hello tanılama uzantısını adlı VM uzantısı yoluyla. Performans veri tooa depolama hesabı hello şablonda tanımlamak yayar. Bu veriler, ardından hello Azure izleme hizmeti tarafından toplanır.
    
    Merhaba Öngörüler hizmeti VM'ler hello verileri okuyamadığında toosend beklenir, bir e-posta – örneğin hello VM'ler aşağı, bu nedenle e-posta (Merhaba hello Azure hesabı oluşturulurken belirtilen birinin) denetleyin.
    
    Ayrıca, Git ve hello veri kendiniz bakın. Cloud explorer'ı kullanarak Azure depolama hesabı Hello arayın. Örneğin hello kullanarak [Visual Studio Cloud Explorer](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), oturum açma ve hello kullanmakta olduğunuz Azure aboneliği seçin ve tanılama depolama hesabı adı hello tanılama uzantısını dağıtımınızı tanımında başvurulan hello Şablon...
    
    ![Bulut Gezgini][explorer]
    
    Burada, her bir VM hello verilerden depolandığı tabloları bir dizi görürsünüz. Linux ve hello CPU ölçüm örnek alarak, hello en son satırları arayın. Merhaba Visual Studio cloud explorer gibi bir sorgu çalıştırabilmeniz için bir sorgu dili destekler "zaman damgası gt datetime'2016-02-02T21:20:00Z'" toomake hello en son olayların (zamanı UTC olarak varsayılmıştır) edinin. Hello veri vardır, toohello karşılık gördüğünüz ayarladığınız kuralları ölçeklendirme mu? Merhaba aşağıdaki örnekte, too100% hello son 5 dakika artan hello CPU makine 20 başladı...
    
    ![Depolama tabloları][tables]
    
    Merhaba veri yoksa, sonra da hello tanılama uzantılı hello VM'ler çalıştıran hello sorunudur anlamına gelir. Merhaba veri varsa, Ölçek kurallarınızı ile veya hello Öngörüler hizmeti ile bir sorun var. anlamına gelir. Denetleme [Azure durum](https://azure.microsoft.com/status/).
    
    Otomatik ölçeklendirme sorun yaşıyorsanız bu adımları uygularken size atanmış sonra hello forumları deneyin [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), veya [yığın taşması](http://stackoverflow.com/questions/tagged/azure), veya bir destek çağrısı oturum. Hazırlanan tooshare hello şablonu ve bir görünüm hello performans verilerinin olması.

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
