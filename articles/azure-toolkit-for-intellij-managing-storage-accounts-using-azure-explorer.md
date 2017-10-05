---
title: "Intellij için Azure Gezgini'ni kullanarak depolama hesaplarını yönetme | Microsoft Docs"
description: "Azure storage hesaplarınızı Intellij için Azure Gezgini'ni kullanarak yönetmeyi öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a>Intellij için Azure Gezgini'ni kullanarak depolama hesaplarını yönetme

Intellij için Azure araç seti bir parçası olan Azure Gezgini, kullanıcıların Azure hesabından Intellij tümleşik geliştirme ortamı (IDE) içindeki depolama hesaplarını yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Intellij içinde depolama hesabı oluşturma

Azure Gezgini'ni kullanarak bir depolama hesabı oluşturmak için aşağıdakileri yapın:

1. Azure hesabınızı kullanarak oturum [oturum açma yönergeleri Eclipse için Azure Araç Seti için]. 

2. İçinde **Azure Gezgini** görüntülemek için Genişlet **Azure** düğümünü sağ tıklatın **depolama hesapları**ve ardından **depolama hesabı oluştur**.

   ![Depolama hesabı komut oluşturma][CS01]

3. İçinde **depolama hesabı oluştur** iletişim kutusunda, aşağıdaki seçenekleri belirtin:

   ![Yeni depolama hesabı iletişim kutusu oluşturma][CS02]

   * **Ad**: yeni depolama hesabı adını belirtir.

   * **Tür hesap**: (örneğin "Blob Depolama") oluşturmak için depolama hesabı türünü belirtir. Daha fazla bilgi için bkz: [Azure storage hesapları hakkında]. 

   * **Performans**: Seçili yayımcıdan (örneğin, "Premium") kullanmak için sunumu hangi depolama hesabını belirtir. Daha fazla bilgi için bkz: [Azure storage ölçeklenebilirlik ve performans hedefleri]. 

   * **Çoğaltma**: depolama hesabı (örneğin, "bölgesel olarak yedekli") için çoğaltma belirtir. Daha fazla bilgi için bkz: [Azure storage çoğaltma]. 

   * **Abonelik**: yeni depolama hesabı için kullanmak istediğiniz Azure aboneliği belirtir.

   * **Konum**: Burada, depolama hesabı oluşturulur (örneğin, "Batı ABD") konumunu belirtir.

   * **Kaynak grubu**: kaynak grubu, sanal makine için belirtir. Aşağıdaki seçeneklerden birini seçin:
      * **Yeni Oluştur**: yeni bir kaynak grubu oluşturmak istediğiniz belirtir.
      * **Var olanı kullan**: Azure hesabınızla ilişkili kaynak gruplarının bir listeden seçer belirtir.

4. Yukarıdaki seçeneklerin tümü belirledikten sonra tıklatın **Tamam**.

## <a name="create-a-storage-container-in-intellij"></a>Intellij içinde bir depolama kapsayıcısı oluşturma

Azure Gezgini'ni kullanarak bir depolama kapsayıcısı oluşturmak için aşağıdakileri yapın:

1. Azure Gezgini görünümünde bir kapsayıcı oluşturmak ve ardından istediğiniz depolama hesabına sağ **oluşturma blob kapsayıcısı**.

   ![BLOB kapsayıcı komut oluşturma][CC01]

2. İçinde **oluşturma blob kapsayıcısı** iletişim kutusunda, kapsayıcı adını belirtin ve ardından **Tamam**. Depolama kapsayıcıları adlandırma hakkında daha fazla bilgi için bkz: [adlandırma ve kapsayıcıları, blobları ve meta verileri başvuran].

   ![Depolama kapsayıcısı iletişim kutusu oluşturma][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Intellij depolama kapsayıcısında Sil

Azure Gezgini'ni kullanarak bir depolama kapsayıcısı silmek için aşağıdakileri yapın:

1. Azure Gezgini görünümünde depolama kapsayıcıya sağ tıklayın ve ardından **silmek**.

   ![Depolama kapsayıcısı komutu silme][DC01]

2. Onay penceresinde **Evet**.

   ![Depolama kapsayıcısı onay penceresi Sil][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Intellij bir depolama hesabını silme

Azure Gezgini'ni kullanarak bir depolama hesabını silmek için aşağıdakileri yapın:

1. İçinde **Azure Gezgini** görüntülemek, depolama hesabına sağ tıklayın ve ardından **silmek**.

   ![Depolama hesabı menü silme][DS01]

2. Onay penceresinde **Evet**.

   ![Depolama hesabı onay penceresi Sil][DS02]

## <a name="next-steps"></a>Sonraki adımlar
Azure depolama hesapları hakkında daha fazla bilgi için boyutlar ve fiyatlandırma, aşağıdaki kaynaklara bakın:

* [Microsoft Azure Depolama'ya Giriş]
* [Azure storage hesapları hakkında]
* Azure depolama hesabı boyutları
  * [Windows Azure depolama hesapları için Boyutlar]
  * [Linux depolama hesaplarını Azure boyutları]
* Azure depolama hesabı fiyatlandırma
  * [Windows depolama hesabı fiyatlandırma]
  * [Linux depolama hesabı fiyatlandırma]

Java IDE Azure araç takımları hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [Eclipse için Azure Araç Seti]
  * [Eclipse için Azure Araç Seti yenilikleri]
  * [Eclipse için Azure Araç Setini Yükleme]
  * [oturum açma yönergeleri Eclipse için Azure Araç Seti için]
  * [Eclipse'te Azure Hello World web uygulaması oluşturma]
* [IntelliJ için Azure Araç Seti]
  * [Intellij için Azure Araç Seti yenilikleri]
  * [IntelliJ için Azure Araç Setini Yükleme]
  * [Oturum açma Azure Araç Seti için Intellij için yönergeler]
  * [Intellij Azure'da Hello World web uygulaması oluşturun]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md
[oturum açma yönergeleri Eclipse için Azure Araç Seti için]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Oturum açma Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

[Microsoft Azure Depolama'ya Giriş]: /azure/storage/storage-introduction
[Azure storage hesapları hakkında]: /azure/storage/storage-create-storage-account
[Azure storage çoğaltma]: /azure/storage/storage-redundancy
[Azure storage ölçeklenebilirlik ve performans hedefleri]: /azure/storage/storage-scalability-targets
[adlandırma ve kapsayıcıları, blobları ve meta verileri başvuran]: http://go.microsoft.com/fwlink/?LinkId=255555

[Windows Azure depolama hesapları için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes
[Linux depolama hesaplarını Azure boyutları]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows depolama hesabı fiyatlandırma]: /pricing/details/virtual-machines/windows/
[Linux depolama hesabı fiyatlandırma]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
