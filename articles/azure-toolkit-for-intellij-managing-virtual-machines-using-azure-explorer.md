---
title: "kullanılarak aaaManage sanal makine için Intellij Azure Gezgini hello | Microsoft Docs"
description: "Nasıl toomanage kullanarak Azure, sanal makineleriniz için Azure Explorer hello öğrenin Intellij."
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a>Intellij için hello Azure Gezgini kullanarak sanal makineleri yönetme

Hello hello Intellij için Azure araç seti bir parçası olan Azure Gezgini, kullanıcıların Azure hesabından sanal makineleri yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar hello Intellij tümleşik geliştirme ortamı (IDE) içinde.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Intellij içinde bir sanal makine oluşturun

toocreate hello Azure Gezgini kullanarak bir sanal makine hello aşağıdaki: 

1. Hello hello adımları kullanarak tooyour Azure hesabı oturum [oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij] makalesi.

2. Merhaba, **Azure Gezgini** görüntülemek için hello genişletin **Azure** düğümü, sağ **sanal makineler**ve ardından **VM Oluştur**. 

   ![Merhaba VM Oluştur komutu][CR01]  
    Merhaba **yeni sanal makine oluşturma** Sihirbazı açılır.

3. Merhaba, **bir abonelik seçin** penceresinde, aboneliğinizi seçin ve ardından **sonraki**. 

   ![Merhaba Seç bir abonelik penceresi][CR02]

4. Merhaba, **bir sanal makine görüntüsü seçin** penceresinde, aşağıdaki bilgilerle hello girin:

   * **Konum**: sanal makineniz oluşturulacağı belirtir (örneğin, *Batı ABD*). 

   * **Görüntü önerilen**: kısaltılmış bir sık kullanılan görüntüleri listesinden görüntü seçeceğinizi belirtir.

   * **Özel görüntü**: özel bir görüntü bilgisinden hello sağlayarak seçecektir belirtir:

      * **Yayımcı**: sanal makine için kullanacağınız hello görüntüyü oluşturan hello yayımcı belirtir (örneğin, *Microsoft*).

      * **Teklif**: hello sanal makine toouse hello seçili yayımcıdan sunumu belirtir (örneğin, *JDK*).

      * **SKU**: hello stok tutma birimini (SKU) toouse hello Seçili teklifi gelen belirtir (örneğin, *JDK_8*).

      * **Sürüm #**: Seçili hello hangi sürümünü belirtir SKU toouse.

   ![Merhaba, bir sanal makine görüntüsü penceresi seçin][CR03]

5. **İleri**’ye tıklayın. 

6. Merhaba, **sanal makine temel ayarları** penceresinde, aşağıdaki bilgilerle hello girin:

   * **Sanal makine adı**: Merhaba, yeni sanal makine için ad, bir harf ile başlamalı ve yalnızca harf, rakam ve tire içerebilir, belirtir.

   * **Boyutu**: çekirdek ve bellek tooallocate sanal makineniz için hello sayısını belirtir.

   * **Kullanıcı adı**: sanal makineniz yönetmek için hello yönetici hesabı toocreate belirtir.

   * **Parola** ve **Onayla**: Merhaba, yönetici hesabının parolasını belirtir.

   ![Merhaba sanal makine temel Ayarları penceresi][CR04]

7. **İleri**’ye tıklayın. 

8. Merhaba, **ilişkili kaynakları** penceresinde, aşağıdaki bilgilerle hello girin:

   * **Kaynak grubu**: hello kaynak grubu, sanal makine için belirtir. Seçenekler aşağıdaki hello birini seçin:
      * **Yeni Oluştur**: toocreate yeni bir kaynak grubu istediğinizi belirtir.
      * **Var olanı kullan**: Azure hesabınızla ilişkili kaynak grupları listesinden tooselect istediğinizi belirtir.

       ![Merhaba ilişkili kaynakları penceresi][CR07]

   * **Depolama hesabı**: sanal makineniz depolamak için depolama hesabı toouse hello belirtir. Mevcut bir depolama hesabını seçin veya yeni bir hesap oluşturun. Seçerseniz **Yeni Oluştur**, iletişim kutusu aşağıdaki hello görüntülenir:

      ![Merhaba depolama hesabı oluştur iletişim kutusu][CR05]

   * **Sanal ağ** ve **alt**: hello sanal ağ ve sanal makinenin bağlanacağı alt belirtir. Bir mevcut ağ ve alt ağ kullanabilir veya yeni bir ağ ve alt ağ oluşturabilirsiniz. Seçerseniz **Yeni Oluştur**, iletişim kutusu aşağıdaki hello görüntülenir:

      ![Merhaba sanal ağ oluştur iletişim kutusu][CR06]

   * **Genel IP adresi**: sanal makineniz için dışa dönük IP adresini belirtir. Yeni bir IP adresi toocreate seçebilir veya sanal makinenize genel bir IP adresi değil olacaksa, seçebileceğiniz **(hiçbiri)**. 

   * **Ağ güvenlik grubu**: isteğe bağlı ağ güvenlik duvarı, sanal makine için belirtir. Var olan bir Güvenlik Duvarı'nı seçin veya sanal makinenize bir ağ Güvenlik Duvarı'nı kullanmayacaksa, seçebileceğiniz **(hiçbiri)**. 

   * **Kullanılabilirlik kümesi**: isteğe bağlı bir kullanılabilirlik kümesi, sanal makinenize ait olabilir belirtir. Mevcut bir kullanılabilirlik kümesi seçin, yeni bir kullanılabilirlik kümesi oluşturabilir veya, sanal makinenize tooan kullanılabilirlik kümesine ait değil, seçin **(hiçbiri)**.

9. **Son**'a tıklayın.  
    Yeni bir sanal makine hello Azure Gezgini aracı penceresinde görüntülenir. 

   ![Yeni sanal makine hello Azure Gezgin Görünümü][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Intellij içinde bir sanal makineyi yeniden başlatın

toorestart Intellij içinde hello Azure Gezgini kullanarak bir sanal makine hello aşağıdaki:

1. Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **yeniden**.

   ![Merhaba sanal makine yeniden başlatma komutu][RE01]

2. Merhaba onay penceresinde **Evet**. 

   ![Merhaba yeniden sanal makine onay penceresi][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Intellij içinde bir sanal makineyi kapatın

Intellij içinde hello Azure Gezgini kullanarak çalışan bir sanal makineyi aşağı tooshut hello aşağıdaki:

1. Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **kapatma**.

   ![Merhaba sanal makine kapatma komutu][SH01]

2. Merhaba onay penceresinde **Evet**. 

   ![sanal makine onay penceresi Hello Kapat][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Bir sanal makinede Intellij Sil

toodelete Intellij içinde hello Azure Gezgini kullanarak bir sanal makine hello aşağıdaki:

1. Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **silmek**.

   ![Merhaba sanal makinesi Delete komutu][DE01]

2. Merhaba onay penceresinde **Evet**. 

   ![sanal makine onay penceresi Hello Sil][DE02]

## <a name="next-steps"></a>Sonraki adımlar
Azure sanal makine boyutları ve fiyatlandırma hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* Azure sanal makine boyutları
  * [Azure'da Windows sanal makineler için Boyutlar]
  * [Azure'daki Linux sanal makineler için Boyutlar]
* Azure sanal makinesi fiyatlandırması
  * [Windows sanal makine fiyatlandırma]
  * [Linux sanal makine fiyatlandırma]

Java IDE hello Azure araç takımları hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Eclipse için Azure Araç Seti]
  * [Merhaba Eclipse için Azure Araç Seti yenilikleri]
  * [Yükleme hello Eclipse için Azure Araç Seti]
  * [Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]
  * [Eclipse'te Azure Hello World web uygulaması oluşturma]
* [IntelliJ için Azure Araç Seti]
  * [Merhaba Intellij için Azure Araç Seti yenilikleri]
  * [Yükleme hello Intellij için Azure Araç Seti]
  * [oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij]
  * [Intellij Azure'da Hello World web uygulaması oluşturun]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij-installation.md
[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Merhaba Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Merhaba Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

[Azure'da Windows sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure'daki Linux sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows sanal makine fiyatlandırma]: /pricing/details/virtual-machines/windows/
[Linux sanal makine fiyatlandırma]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
