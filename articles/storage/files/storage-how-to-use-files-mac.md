---
title: "macOS’da SMB üzerinden Azure Dosya paylaşımını bağlama | Microsoft Docs"
description: "macOS’da SMB üzerinden Azure Dosya paylaşımını bağlamayı öğrenin."
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
ms.date: 09/19/2017
ms.author: renash
ms.openlocfilehash: 6e71a13f99160fdd310be1e9a59717c9fecbf35d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>macOS’da SMB üzerinden Azure Dosya paylaşımını bağlama
[Azure Dosyaları](storage-files-introduction.md), endüstri standardı kullanılarak Azure'da ağ dosya paylaşımları oluşturmanızı ve bunları kullanmanızı sağlayan bir Microsoft hizmetidir. Azure Dosya paylaşımları macOS Sierra (10.12) ve El Capitan’da (10.11) bağlanabilir. Bu makalede, macOS’ta Bulucu kullanıcı arabirimiyle ve Terminal kullanarak Azure Dosya paylaşımını bağlamanın iki farklı yolu gösterilir.

> [!Note]  
> SMB üzerinden Azure Dosya paylaşımını bağlamadan önce, SMB paket imzalamasını devre dışı bırakmanızı öneririz. Bunu yapmazsanız, macOS’tan Azure Dosya paylaşımına erişirken performansta düşüş olabilir. SMB bağlantınız şifrelenir, bu sayede bağlantınızın güvenliği etkilenmez. Terminalde, aşağıdaki komutlar [SMB paket imzalamasını devre dışı bırakma üzerine Apple destek makalesinde](https://support.apple.com/HT205926) anlatıldığı gibi SMB paket imzalamasını devre dışı bırakır:  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>macOS’ta Azure Dosya paylaşımını bağlama önkoşulları
* **Depolama hesabı adı**: Azure Dosya paylaşımını bağlayabilmeniz için depolama hesabınızın adı gerekir.

* **Depolama hesabı anahtarı**: Azure Dosya paylaşımını bağlayabilmeniz için birincil (veya ikincil) depolama anahtarı gerekir. SAS anahtarları şu an bağlama için desteklenmemektedir.

* **Bağlantı noktası 445’in açık olduğundan emin olun**: SMB, TCP bağlantı noktası 445 üzerinden iletişim kurar. İstemci makinenizde (Mac) güvenlik duvarının TCP bağlantı noktası 445’i engellemediğinden emin olun.

## <a name="mount-an-azure-file-share-via-finder"></a>Bulucu yoluyla Azure Dosya paylaşımını bağlama
1. **Bulucu’yu açın**: Bulucu varsayılan olarak macOS’ta açıktır, ancak bunun seçili durumdaki uygulama olduğundan emin olmak için dock’taki “macOS yüz simgesine” tıklayın:  
    ![macOS yüz simgesi](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)

2. **”Git” menüsünden “Sunucuya Bağlan”ı seçin**: [Önkoşullar](#preq)’dan UNC adını kullanarak başlangıç çift eğik çizgisini (`\\`) `smb://` ile ve diğer tüm ters eğik çizgileri (`\`) eğik çizgiyle (`/`) değiştirin. Bağlantınız şu şekilde görünmelidir: ![“Sunucuya Bağlan” iletişim kutusu](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)

3. **Kullanıcı adı ve parola istendiğinde paylaşım adını ve depolama hesabı anahtarını kullanın**: “Sunucuya Bağlan” iletişim kutusunda “Bağlan”a tıkladığınızda kullanıcı adı ve parola istenir (Bu alan otomatik olarak macOS kullanıcı adınızla doldurulur). macOS Anahtarlığınıza paylaşım adı/depolama hesabı anahtarı yerleştirebilirsiniz.

4. **Azure Dosya paylaşımını istediğiniz gibi kullanın**: Kullanıcı adı ve parola yerine paylaşım adını ve depolama hesabı anahtarını koyduktan sonra paylaşım bağlanacaktır. Bunu, yerel klasör/dosya paylaşımını normalde kullandığınız gibi kullanabilirsiniz. Örneğin, dosyaları dosya paylaşımına sürükleyip bırakabilirsiniz:

    ![Bağlı bir Azure Dosya paylaşımının anlık görüntüsü](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Terminal yoluyla Azure Dosya paylaşımını bağlama
1. `<storage-account-name>` değerini depolama hesabınızın adıyla değiştirin. İstendiğinde parola olarak Depolama Hesabı Anahtarı’nı girin. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Azure Dosya paylaşımını istediğiniz gibi kullanın**: Azure Dosya paylaşımı, önceki komutta belirtilmiş olan bağlama noktasına bağlanır.  

    ![Bağlı Azure Dosya paylaşımının anlık görüntüsü](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Sonraki adımlar
Azure Dosyaları hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.

* [Apple Destek Makalesi - Mac’inizde Dosya Paylaşımı ile bağlantı kurma](https://support.apple.com/HT204445)
* [SSS](../storage-files-faq.md)
* [Windows’da sorun giderme](storage-troubleshoot-windows-file-connection-problems.md)      
* [Linux’ta sorun giderme](storage-troubleshoot-linux-file-connection-problems.md)    