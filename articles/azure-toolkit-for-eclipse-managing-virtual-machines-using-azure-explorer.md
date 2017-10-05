---
title: "Eclipse için Azure Gezgini'ni kullanarak sanal makineleri yönetme | Microsoft Docs"
description: "Eclipse için Azure Gezgini'ni kullanarak Azure sanal makinelerinizi yönetmeyi öğrenin."
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
ms.openlocfilehash: 9784e8af9c530078afee06f08a23403a44b0762f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a>Eclipse için Azure Gezgini'ni kullanarak sanal makineleri yönetme

Eclipse için Azure araç seti bir parçası olan Azure Gezgini, bunların Azure hesabında Eclipse tümleşik geliştirme ortamı (IDE) içindeki sanal makineleri yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Eclipse'te bir sanal makine oluşturun

Azure Gezgini'ni kullanarak bir sanal makine oluşturmak için aşağıdakileri yapın:

1. Azure hesabınızı kullanarak oturum [oturum açma yönergeleri Eclipse için Azure Araç Seti için].

2. İçinde **Azure Gezgini** görüntülemek için Genişlet **Azure** düğümünü sağ tıklatın **sanal makineler**ve ardından **VM Oluştur**.

   ![VM Oluştur komutu][CR01]  
   **Yeni sanal makine oluşturma** Sihirbazı açılır.

3. İçinde **bir abonelik seçin** penceresinde, aboneliğinizi seçin ve ardından **sonraki**.

   ![Bir abonelik penceresi seçin][CR02]

4. İçinde **bir sanal makine görüntüsü seçin** penceresinde, aşağıdaki bilgileri girin:

   * **Konum**: sanal makineniz oluşturulacağı belirtir (örneğin, *Batı ABD*).

   * **Yayımcı**: kullanmak, sanal makine oluşturmak için görüntüyü oluşturan yayımcı belirtir (örneğin, *Microsoft*).

   * **Teklif**: Seçili yayımcıdan kullanmak için sunumu sanal makine belirtir (örneğin, *JDK*).

   * **SKU**: stok tutma birimini (SKU) gelen Seçili teklifi kullanılacak belirtir (örneğin, *JDK_8*).

   * **Sürüm #**: hangi sürümünün kullanılacağını seçilen SKU belirtir.

    ![Bir sanal makine görüntüsü penceresi seçin][CR03]

5. **İleri**’ye tıklayın.

6. İçinde **sanal makine temel ayarları** penceresinde, aşağıdaki bilgileri girin:

   * **Sanal makine adı**: yeni sanal bir harfle başlamalı ve yalnızca harf, rakam ve tire içeren makinenizi adını belirtir.

   * **Boyutu**: çekirdek ve sanal makine için ayrılacak bellek sayısını belirtir.

   * **Kullanıcı adı**: sanal makineniz yönetmek için oluşturmak için yönetici hesaplarını belirtir.

   * **Parola** ve **Onayla**: yönetici hesabının parolasını belirtir.

    ![Sanal makine temel Ayarları penceresi][CR04]

7. **İleri**’ye tıklayın.

8. İçinde **yeni depolama hesabı oluştur** penceresinde, aşağıdaki bilgileri girin:

   * **Kaynak grubu**: kaynak grubu, sanal makine için belirtir. Aşağıdaki seçeneklerden birini seçin:
      * **Yeni Oluştur**: yeni bir kaynak grubu oluşturmak istediğiniz belirtir.
      * **Var olanı kullan**: Azure hesabınızla ilişkili olan bir kaynak grubunu seçmek istediğiniz belirtir.

      ![Yeni depolama hesabı oluştur iletişim kutusu][CR05]

   * **Depolama hesabı**: sanal makineniz depolamak için kullanılacak depolama hesabını belirtir. Mevcut bir depolama hesabını kullanabilir veya yeni bir hesap oluşturabilirsiniz.

   * **Sanal ağ** ve **alt**: sanal ağ ve sanal makinenin bağlanacağı alt belirtir. Bir mevcut ağ ve alt ağ kullanabilir veya yeni bir ağ ve alt ağ oluşturabilirsiniz. Seçerseniz **Yeni Oluştur**, aşağıdaki iletişim kutusu görüntülenir:

      ![Yeni sanal ağ oluştur iletişim kutusu][CR06]

9. İçinde **ilişkili kaynakları** penceresinde, aşağıdaki bilgileri girin:

   * **Genel IP adresi**: sanal makineniz için dışa dönük IP adresini belirtir. Yeni bir IP adresi oluşturmak seçebilir veya sanal makinenize genel bir IP adresi değil olacaksa, seçebileceğiniz **(hiçbiri)**.

   * **Ağ güvenlik grubu**: isteğe bağlı ağ güvenlik duvarı, sanal makine için belirtir. Var olan bir Güvenlik Duvarı'nı seçin veya sanal makinenize bir ağ Güvenlik Duvarı'nı kullanmayacaksa, seçebileceğiniz **(hiçbiri)**.

   * **Kullanılabilirlik kümesi**: isteğe bağlı bir kullanılabilirlik kümesi, sanal makinenize ait olabilir belirtir. Mevcut bir kullanılabilirlik kümesi seçin veya yeni bir kullanılabilirlik kümesi oluşturmak veya sanal makinenize bir kullanılabilirlik kümesine ait değil, seçebileceğiniz **(hiçbiri)**.

   ![İlişkilendirilmiş kaynakları penceresi][CR07]

9. **Son**'a tıklayın.  
  Yeni sanal makinenizi Azure Gezgini aracı penceresinde görüntülenir.

   ![Yeni sanal makine][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Eclipse'te bir sanal makineyi yeniden başlatın

Eclipse'te Azure Gezgini'ni kullanarak bir sanal makineyi yeniden başlatmak için aşağıdakileri yapın:

1. İçinde **Azure Gezgini** görüntülemek, sanal makineye sağ tıklayın ve ardından **yeniden**.

   ![Sanal makine yeniden başlatma komutu][RE01]

2. Onay penceresinde **Evet**.

   ![Yeniden başlatma onay penceresi][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Eclipse'te bir sanal makineyi kapatın

Eclipse'te Azure Gezgini'ni kullanarak çalışan bir sanal makineyi kapatıp için aşağıdakileri yapın:

1. İçinde **Azure Gezgini** görüntülemek, sanal makineye sağ tıklayın ve ardından **kapatma**.

   ![Sanal makine kapatma komutu][SH01]

2. Onay penceresinde **Evet**.

   ![Sanal makinenin kapatılması onay penceresi][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Eclipse'te sanal makineyi silme

Eclipse'te Azure Gezgini'ni kullanarak bir sanal makineyi silmek için aşağıdakileri yapın:

1. İçinde **Azure Gezgini** görüntülemek, sanal makineye sağ tıklayın ve ardından **silmek**.

   ![Sanal makine Delete komutu][DE01]

2. Onay penceresinde **Evet**.

   ![Sanal makine silme işlemi onay penceresi][DE02]

## <a name="next-steps"></a>Sonraki adımlar
Azure sanal makine boyutları ve fiyatlandırma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* Azure sanal makine boyutları
  * [Azure'da Windows sanal makineler için Boyutlar]
  * [Azure'daki Linux sanal makineler için Boyutlar]
* Azure sanal makinesi fiyatlandırması
  * [Windows sanal makine fiyatlandırma]
  * [Linux sanal makine fiyatlandırma]

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

[Azure'da Windows sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure'daki Linux sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows sanal makine fiyatlandırma]: /pricing/details/virtual-machines/windows/
[Linux sanal makine fiyatlandırma]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
