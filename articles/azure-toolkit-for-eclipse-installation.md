---
title: "Eclipse için Azure araç setini yükleme | Microsoft Docs"
description: "Eclipse için Azure Araç Seti yüklemeyi öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Eclipse için Azure araç setini yükleme
Eclipse için Azure araç seti, şablonları ve kolayca oluşturun, geliştirme, test olanak sağlar ve Eclipse geliştirme ortamı'nı kullanarak Azure uygulamalarını dağıtma işlevleri sağlar. Eclipse için Azure Araç Seti açık kaynaklı proje ' dir. Kaynak kodu MIT lisansı altında kullanılabilir <https://github.com/microsoft/azure-tools-for-java>.

Aşağıdaki adımlar, Azure araç setini Eclipse için yükleme gösterir.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Eclipse için Azure Araç Seti yüklemek için
1. Eclipse'i başlatın.
2. Tıklatın **yardımcı** menüsüne ve ardından **yeni yazılımı yükle**, aşağıdaki çizimde gösterildiği gibi.
   
    ![Eclipse için Azure araç setini yükleme][01]
3. İçinde **kullanılabilir yazılım** iletişim, içinde **çalışmak** metin kutusunda, `http://dl.microsoft.com/eclipse` arkasından **Enter** anahtarı.
4. İçinde **adı** bölmesinde, onay **Eclipse için Azure Araç Seti**ve işaretini **gerekli yazılımı bulmak için yükleme sırasında tüm güncelleştirme siteleri başvurun**. Ekranınızın aşağıdakine benzer görünmelidir:
   
    ![Eclipse için Azure araç setini yükleme][02]
5. Genişletirseniz **Eclipse için Azure Araç Seti**, aşağıdaki öğeleri görürsünüz:
   
   * **Java için uygulama Insights eklentisiyle**: Bu bileşen, uygulamaları ve sunucu örnekleri için Azure'nın telemetri günlüğe kaydetme ve Analiz Hizmetleri kullanmanıza olanak sağlar.
   * **Azure erişim denetimi Hizmetleri filtre**: Bu bileşen Azure ACS ile uygulama kullanıcıların kimlik doğrulaması, tek oturum açma senaryoları etkinleştirmek ve uygulamadan kimlik mantığını harici hale getirerek için destek sağlar.
   * **Azure ortak eklenti**: Bu bileşen, diğer araç seti bileşenleri tarafından gereken ortak işlevsellik sağlar.
   * **Eclipse için Azure Explorer**: Bu bileşen, diğer araç seti bileşenleri tarafından gereken ortak işlevsellik sağlar.
   * **Java ile Eclipse için Azure eklentisi**: Bu bileşen, derleme, test ve Eclipse ve komut satırı aracılığıyla Microsoft Azure bulut için Java uygulamaları dağıtmanıza yardımcı projeleri geliştirmek için destek sağlar.
   * **Java ile Azure Web Apps eklentisi**: Bu bileşen, Microsoft Azure Web uygulaması kapsayıcıları için Java web uygulamalarını dağıtmak için destek sağlar.
   * **SQL Server için Microsoft JDBC sürücüsü 4.2**: Bu bileşen JDBC API SQL Server ve Microsoft Azure SQL veritabanı için Java Platform Enterprise Edition 8 sağlar.
   * **Apache Qpid istemci kitaplıkları JMS için paket**: Bu bileşen, Microsoft Azure'da AMQP Mesajlaşma kullanmak için uygulamanızı etkinleştirmek için Apache Qpid projeden JMS istemci bileşeni sağlar.
   * **Java için Microsoft Azure kitaplıkları için paketi**: Bu bileşen, Microsoft Azure Hizmetleri, depolama, hizmet veri yolu, hizmet çalışma zamanı vb. gibi erişmek için API'ler sağlar.
6. **İleri**’ye tıklayın. (Araç Seti yüklerken olağan dışı gecikmeler yaşıyorsanız emin **gerekli yazılımı bulmak için yükleme sırasında tüm güncelleştirme siteleri başvurun** işaretli değildir.)
7. İçinde **Yükleme ayrıntıları** iletişim kutusunda, tıklatın **sonraki**.
   
    ![Kurulum ayrıntılarını gözden geçirin][03]
8. İçinde **gözden lisansları** iletişim kutusunda, Lisans Sözleşmesi koşullarını gözden geçirin. Lisans Sözleşmesi koşullarını kabul ediyorsanız **Lisans Sözleşmesi koşullarını kabul ediyorum** ve ardından **son**. (Kalan adımları Lisans Sözleşmesi koşullarını kabul ediyor musunuz varsayalım. Lisans Sözleşmesi koşullarını kabul etmezseniz, yükleme işlemden.)
   
    ![Lisansları gözden geçirin][04]
   
    Eclipse indirin ve gerekli paketleri yüklemek.
   
    ![Yükleme ilerleme durumu][05]
9. Yüklemeyi tamamlamak için Eclipse'i yeniden başlatmanız istenirse, tıklatın **Evet**.
   
    ![İstemi yeniden başlatın][06]

## <a name="see-also"></a>Ayrıca Bkz.
Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:

* [Eclipse için Azure Araç Seti]
  * [Eclipse için Azure Araç Seti Yenilikleri]
  * *Azure araç setini Eclipse (Bu makalede) için yükleme*
  * [Eclipse için Azure Araç Setinde Oturum Açma Yönergeleri]
  * [Eclipse Azure'da Hello World Web uygulaması oluşturun]
* [IntelliJ için Azure Araç Seti]
  * [IntelliJ için Azure Araç Seti Yenilikleri]
  * [IntelliJ için Azure Araç Setini Yükleme]
  * [IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]
  * [Intellij Azure'da Hello World Web uygulaması oluşturun]

Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md
[Eclipse için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[IntelliJ için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
