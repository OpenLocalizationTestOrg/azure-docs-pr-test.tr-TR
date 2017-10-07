---
title: aaaHow toomanage hello Azure portal'dan Azure File storage | Microsoft Docs
description: "Toouse hello Azure portal toomanage Azure File storage öğrenin."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Nasıl toouse Azure dosya depolama biriminden hello Azure portalı
Merhaba [Azure portal](https://portal.azure.com) Azure File storage yönetmek için bir kullanıcı arabirimi sağlar. Web tarayıcınızdan eylemleri aşağıdaki hello gerçekleştirebilirsiniz:

* Dosya Paylaşımı oluşturma
* Karşıya yükleme ve dosyaları tooand dosya paylaşımından indirin.
* Her dosya paylaşımına Hello gerçek kullanımını izleyin.
* Merhaba dosya paylaşım boyutu kotasını ayarlama.
* Merhaba bağlama komutları toouse toomount, dosya paylaşımı bir Windows veya Linux istemciden kopyalayın.

## <a name="create-file-share"></a>Dosya paylaşımı oluşturma
1. Toohello Azure portalında oturum açın.
2. Merhaba Gezinti menüsünde **depolama hesapları** veya **depolama hesapları (Klasik)**.
    
    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Depolama hesabınızı seçin.

    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. "Dosyalar" hizmetini seçin.

    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. "Dosya paylaşımları" seçeneğine tıklayın ve ilk dosya paylaşımı hello bağlantı toocreate izleyin.

    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Merhaba dosya paylaşımı adı ve hello dosya paylaşımı (yukarı too5120 GB) toocreate hello boyutunu ilk dosya paylaşımınızı doldurun. Merhaba dosya paylaşımı oluşturulduktan sonra SMB 2.1 veya SMB 3.0 destekleyen herhangi bir dosya sisteminden bağlayabilirsiniz. Tıklayarak **kota** hello dosya paylaşımı toochange hello boyutu hello dosyasını too5120 GB yedekleyin. Lütfen çok başvurun[Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) tooestimate hello depolama maliyeti Azure File storage kullanma.

    ![Nasıl toocreate dosya paylaşımı hello Portalı'nda gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Dosyaları yükleme ve indirme
1. Daha önce oluşturduğunuz bir dosya paylaşımını seçin.

    ![Nasıl tooupload ve yükleme dosyalarından portal hello gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Tıklatın **karşıya** hello kullanıcı arabirimi yüklenen dosyalar için açın.

    ![Tooupload hello Portalı'ndan nasıl dosyaları gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Toofile paylaşımına bağlanmak
-  Tıklatın **Bağlan** Windows ve Linux bağlama hello dosya paylaşımı için hello komut satırı alınamadı. Linux kullanıcıları için aynı zamanda çok başvurabilirsiniz[nasıl toouse Linux Azure File storage](../storage-how-to-use-files-linux.md) diğer Linux dağıtımları için daha fazla bağlama yönergeler için.

    ![Nasıl toomount hello dosya paylaşımını gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  Dosya komutları Windows veya Linux'ta paylaşma ve çalıştırın, Azure VM veya şirket içi makinede hello kopyalayabilirsiniz.

    ![Windows ve Linux için hello bağlama komutları gösteren ekran görüntüsü](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**İpucu:**  
toofind hello depolama hesabının erişim anahtarı bağlama, tıklayın **görünüm erişim için bu depolama hesabı anahtarları** hello hello altındaki sayfayı bağlayın.

## <a name="see-also"></a>Ayrıca bkz.
Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.

* [SSS](../storage-files-faq.md)
* [Windows’da sorun giderme](storage-troubleshoot-windows-file-connection-problems.md)      
* [Linux’ta sorun giderme](storage-troubleshoot-linux-file-connection-problems.md)    