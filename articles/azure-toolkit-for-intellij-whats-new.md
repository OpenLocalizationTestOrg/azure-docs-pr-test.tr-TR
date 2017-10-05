---
title: "Intellij için Azure Araç Seti yenilikler | Microsoft Docs"
description: "Intellij için en son özelliklere Azure araç setindeki öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 23714856f0f778be04cf321e0726b53ade430f57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a>Intellij için Azure Araç Seti yenilikleri
## <a name="azure-toolkit-for-intellij-releases"></a>Intellij yayımları için Azure Araç Seti
Bu makale Intellij için çeşitli yayınları ve Azure Araç Seti en son güncelleştirmeleri hakkında bilgi içerir.

> [!NOTE]
> Bir Azure araç setini Eclipse IDE yoktur. Daha fazla bilgi için bkz: [Eclipse için Azure Araç Seti].
> 
> 

### <a name="april-14-2017"></a>14 Nisan 2017
Intellij - Nisan 2017 yayın için Azure Araç Seti aşağıdaki geliştirmeleri içerir:

* **Azure deneyimi oturum geliştirilmiş**: Intellij için Azure Araç Seti artık Azure hesabınızda oturum açılırken iki yöntemi destekler: *etkileşimli* ve *otomatik*. Daha fazla bilgi için bkz: [içinde Azure oturum yönergeler Intellij için Azure Araç Seti için].
* **Docker kapsayıcıları kullanma yayımlama**: Docker Intellij için Azure Araç Seti kullanarak kapsayıcı olarak, web uygulamalarınızı şimdi yayımlayabilirsiniz. Daha fazla bilgi için bkz: [Docker Intellij için Azure Araç Seti kullanarak bir kapsayıcı olarak bir Web uygulaması yayımlama].
* **Depolama hesap yönetimi**: Intellij için Azure Araç Seti artık destekliyor depolama hesaplarınızı Azure Explorer görünümünden yönetme. Daha fazla bilgi için bkz: [depolama Intellij için Azure Explorer'ı kullanarak hesapları yönetme].
* **Sanal Makine Yönetimi**: Intellij için Azure Araç Seti artık destekler Azure Gezgini aracı penceresinden sanal makinelerinizi yönetme. Daha fazla bilgi için bkz: [yönetme Azure Gezgini Intellij için kullanarak sanal makineleri].
* **Uzaktan hata ayıklama desteği kaldırılmasını**. Azure App Service'te Java web uygulamaları uzaktan hata ayıklama Azure araç setinin Intellij için kaldırılmıştır; Bu araç seti kullanırken müşteriler yaşıyordu bazı sorunları gidermek gerekliydi.

### <a name="august-26-2016"></a>26 Ağustos 2016
Intellij - Ağustos 2016 sürüm için Azure Araç Seti aşağıdaki geliştirmeleri içerir:

* **Özel JDK dağıtımları**. Intellij için Azure Araç Seti artık belirtme ve rasgele bir JDK sürümü, Azure WebApp kapsayıcıya dağıtma destekler:
  * Azure tarafından sağlanan JDKs yanı sıra, Azure üzerinde Azul sistemler tarafından kullanılabilir hale Zulu dili OpenJDK sürümlerinin geniş seçimden seçebilirsiniz.
  * Depolama hesabınıza bir ZIP dosyası yüklerseniz, ayrıca kendi JDK dağıtım belirtebilirsiniz.
* **Azure Explorer görünümü geliştirmeler**:
  * Azure'nın yeni Resource Manager modelini kullanarak sanal makine yönetimi desteği: listesinde, oluşturabilir ve IDE ayrılmadan resource manager tabanlı sanal makineleri silin.
  * "Klasik" depolama hesapları yönetmek için var olan işlevselliği tamamlar Azure Resource Manager kullanarak depolama hesabı blob yönetimi için destek.
* **SQL Server için Microsoft JDBC sürücüsü 6.0**. Bu güncelleştirme, Microsoft SQL olan sunucu için (v6.0), en son JDBC sürücüsü içerir, Java projenize kolayca ekleyebilirsiniz kitaplık olarak dahil artık eski sürümü böylece değiştirme.

### <a name="june-29-2016"></a>29 Haziran 2016
Intellij - Haziran 2016 sürüm için Azure Araç Seti aşağıdaki geliştirmeleri içerir:

* **Java 8 gereksinim**. Intellij için Azure Araç Seti artık Java 8, gerektirir ancak bu gereksinim yalnızca için araç seti - uygulamalarınız Java'nın Azure tarafından desteklenen tüm sürümleri kullanmaya devam edebilirsiniz.
* **En son Java JDKs desteği**. Java JDKs en son sürümlerini Intellij için artık Azure araç takımı tarafından desteklenmektedir.
* **Azure SDK'sı v2.9.1 desteği**. Azure SDK'nin en son sürümünü Intellij için Azure Araç Seti için minimum önkoşul sunulmuştur.
* **Örnekleri tümleşik**. Intellij için Azure Araç Seti artık başlama geliştiricilerin yardımcı olmak için birkaç örnek uygulama özellikleri.
* **Hdınsight aracı tümleştirme**. Azure Hdınsight araçları Intellij için artık Azure araç seti ile paketlenmiştir. Daha fazla bilgi için bkz: [Intellij için Hdınsight araçları eklentisi].
* **Uzaktan hata ayıklama Java Web uygulamaları**. Intellij için Azure Araç Seti artık Azure App Service'te Java web uygulamaları uzaktan hata ayıklama destekler.

### <a name="april-12-2016"></a>12 Nisan, 2016
Intellij - Nisan 2016 sürüm için Azure Araç Seti aşağıdaki geliştirmeleri içerir:

* **Azure SDK'sı v2.9.0 desteği**. Azure SDK'nin en son sürümünü Intellij için Azure Araç Seti için minimum önkoşul sunulmuştur.
* **Çeşitli kullanılabilirlik, yanıtlama ve performans iyileştirmeleri ilgili Azure Web uygulaması desteklemek için**. Bir dizi araç seti Azure sonucu ile nasıl iletişim kurduğu, performans iyileştirmelerini daha iyi yanıt arabiriminde.
* **Var olan bir Web uygulaması kapsayıcıyı Intellij içinde azure'da silme yeteneği**. Intellij için Azure Araç Seti artık Intellij ayrılmadan var olan bir Azure Web kapsayıcı silmenize olanak sağlar.

## <a name="see-also"></a>Ayrıca Bkz.
Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:

* [Eclipse için Azure Araç Seti]
  * [Eclipse için Azure Araç Seti Yenilikleri]
  * [Eclipse için Azure Araç Setini Yükleme]
  * [Eclipse Azure'da Hello World Web uygulaması oluşturun]
  * [Eclipse için Azure Araç Setinde Oturum Açma Yönergeleri]
* [IntelliJ için Azure Araç Seti]
  * *Intellij (Bu makalede) için Azure Araç Seti yenilikleri*
  * [IntelliJ için Azure Araç Setini Yükleme]
  * [IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]
  * [Intellij Azure'da Hello World Web uygulaması oluşturun]

Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md
[Eclipse için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[içinde Azure oturum yönergeler Intellij için Azure Araç Seti için]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Docker Intellij için Azure Araç Seti kullanarak bir kapsayıcı olarak bir Web uygulaması yayımlama]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[depolama Intellij için Azure Explorer'ı kullanarak hesapları yönetme]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[yönetme Azure Gezgini Intellij için kullanarak sanal makineleri]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Azure Java Geliştirici Merkezi]: http://go.microsoft.com/fwlink/?LinkID=699547

[Intellij için Hdınsight araçları eklentisi]: ./hdinsight/hdinsight-apache-spark-intellij-tool-plugin.md
