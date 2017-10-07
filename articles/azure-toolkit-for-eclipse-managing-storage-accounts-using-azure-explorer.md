---
title: "Eclipse için Azure Explorer kullanarak aaaManage depolama hesapları hello | Microsoft Docs"
description: "Nasıl toomanage Eclipse için hello Azure Explorer kullanarak, Azure depolama hesapları hakkında bilgi edinin."
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
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a>Eclipse için hello Azure Gezgini kullanarak depolama hesaplarını yönetme

Merhaba hello Eclipse için Azure araç seti bir parçası olan Azure Gezgini, kullanıcıların Azure hesabından depolama hesaplarını yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar hello Eclipse tümleşik geliştirme ortamı (IDE) içinde.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a>Eclipse'te depolama hesabı oluşturma

toocreate hello Azure Gezgini kullanarak bir depolama hesabı hello aşağıdaki:

1. Tooyour Azure hesabı hello kullanarak oturum [oturum açma yönergeleri hello Eclipse için Azure Araç Seti için].

2. Hello içinde **Azure Gezgini** görüntülemek için hello genişletin **Azure** düğümünü sağ tıklatın **depolama hesapları**ve ardından **depolama hesabı oluştur**.

   ![Depolama hesabı komut oluşturma][CS01]

3. Merhaba, **depolama hesabı oluştur** iletişim kutusunda, aşağıdaki seçenekleri şu hello belirtin:

   ![Yeni depolama hesabı iletişim kutusu oluşturma][CS02]

   * **Ad**: hello yeni depolama hesabı hello adını belirtir.

   * **Abonelik**: Merhaba toouse hello yeni depolama hesabı için istediğiniz Azure aboneliği belirtir.

   * **Kaynak grubu**: hello kaynak grubu, sanal makine için belirtir. Seçenekler aşağıdaki hello birini seçin:
      * **Yeni Oluştur**: toocreate yeni bir kaynak grubu istediğinizi belirtir.
      * **Varolan kullanmak**: Azure hesabınızla ilişkili kaynak gruplarının bir listeden seçer belirtir.

   * **Bölge**: Burada, depolama hesabı oluşturulur (örneğin, "Batı ABD") hello konumunu belirtir.

   * **Tür hesap**: depolama hesabı toocreate (örneğin, "Blob Depolama") hello türünü belirtir. Daha fazla bilgi için bkz: [Azure storage hesapları hakkında].

   * **Performans**: (örneğin, "Premium") hello seçili yayımcıdan toouse sunumu hangi depolama hesabını belirtir. Daha fazla bilgi için bkz: [Azure storage ölçeklenebilirlik ve performans hedefleri].

   * **Çoğaltma**: hello çoğaltma hello depolama hesabı (örneğin, "bölgesel olarak yedekli") için belirtir. Daha fazla bilgi için bkz: [Azure storage çoğaltma].

4. Tüm seçenekleri önceki hello belirledikten sonra tıklatın **oluşturma**.

## <a name="create-a-storage-container-in-eclipse"></a>Eclipse'te bir depolama kapsayıcısı oluşturma

toocreate hello Azure Gezgini kullanarak bir depolama kapsayıcısı hello aşağıdaki:

1. Merhaba, **Azure Gezgini** görüntülemek için burada, toocreate bir kapsayıcı istediğiniz ve ardından hello depolama hesabına sağ **oluşturma blob kapsayıcısı**.

   ![BLOB kapsayıcı komut oluşturma][CC01]

2. Merhaba, **oluşturma blob kapsayıcısı** iletişim kutusu, Merhaba, kapsayıcı için bir ad belirtin ve ardından **Tamam**. Depolama kapsayıcıları adlandırma hakkında daha fazla bilgi için bkz: [adlandırma ve kapsayıcıları, blobları ve meta verileri başvuran].

   ![BLOB kapsayıcısı iletişim kutusu oluşturma][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a>Depolama kapsayıcısı eclipse'te Sil

toodelete hello Azure Gezgini kullanarak bir depolama kapsayıcısı hello aşağıdaki:

1. Merhaba, **Azure Gezgini** görüntülemek, hello depolama kapsayıcısına sağ tıklayın ve ardından **silmek**.

   ![Depolama kapsayıcısı komutu silme][DC01]

2. Merhaba onay penceresinde **Tamam**.

   ![Depolama kapsayıcısı onay penceresi Sil][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a>Eclipse'te bir depolama hesabını silme

toodelete hello Azure Gezgini kullanarak bir depolama hesabı hello aşağıdaki:

1. Merhaba, **Azure Gezgini** görüntülemek, hello depolama hesabına sağ tıklayın ve ardından **silmek**.

   ![Depolama hesabı komutu silme][DS01]

2. Merhaba onay penceresinde **Tamam**.

   ![Depolama hesabı onay penceresi Sil][DS02]

## <a name="next-steps"></a>Sonraki adımlar
Azure depolama hesapları, boyutlar ve fiyatlandırma hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Giriş tooMicrosoft Azure depolama]
* [Azure storage hesapları hakkında]
* Azure depolama hesabı boyutları
  * [Windows Azure depolama hesapları için Boyutlar]
  * [Linux depolama hesaplarını Azure boyutları]
* Azure depolama hesabı fiyatlandırma
  * [Windows depolama hesabı fiyatlandırma]
  * [Linux depolama hesabı fiyatlandırma]

Java IDE için Azure araç takımları hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Eclipse için Azure Araç Seti]
  * [Merhaba Eclipse için Azure Araç Seti yenilikleri]
  * [Yükleme hello Eclipse için Azure Araç Seti]
  * [oturum açma yönergeleri hello Eclipse için Azure Araç Seti için]
  * [Eclipse'te Azure Hello World web uygulaması oluşturma]
* [IntelliJ için Azure Araç Seti]
  * [Merhaba Intellij için Azure Araç Seti yenilikleri]
  * [Yükleme hello Intellij için Azure Araç Seti]
  * [Oturum açma hello Azure Araç Seti için Intellij için yönergeler]
  * [Intellij Azure'da Hello World web uygulaması oluşturun]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij-installation.md
[oturum açma yönergeleri hello Eclipse için Azure Araç Seti için]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Oturum açma hello Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Merhaba Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Merhaba Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

[Giriş tooMicrosoft Azure depolama]: /azure/storage/storage-introduction
[Azure storage hesapları hakkında]: /azure/storage/storage-create-storage-account
[Azure storage çoğaltma]: /azure/storage/storage-redundancy
[Azure storage ölçeklenebilirlik ve performans hedefleri]: /azure/storage/storage-scalability-targets
[adlandırma ve kapsayıcıları, blobları ve meta verileri başvuran]: http://go.microsoft.com/fwlink/?LinkId=255555

[Windows Azure depolama hesapları için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes
[Linux depolama hesaplarını Azure boyutları]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows depolama hesabı fiyatlandırma]: /pricing/details/virtual-machines/windows/
[Linux depolama hesabı fiyatlandırma]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
