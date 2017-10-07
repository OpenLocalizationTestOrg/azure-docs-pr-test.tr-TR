---
title: "macOS SMB üzerinden aaaMount Azure dosya paylaşımının | Microsoft Docs"
description: "Nasıl toomount bir Azure dosya paylaşımı üzerinden SMB macOS ile bilgi edinin."
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
ms.openlocfilehash: 7b4924cb42247470521c1ae8b9d03ab1756996e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>macOS’da SMB üzerinden Azure Dosya paylaşımını bağlama
[Azure File storage](storage-dotnet-how-to-use-files.md) hello Azure toocreate ve kullanım ağ dosya paylaşımları sağlayan Microsoft'un hizmetini kullanarak hello endüstri standardı. Azure Dosya paylaşımları macOS Sierra (10.12) ve El Capitan’da (10.11) bağlanabilir. Bu makalede iki farklı şekilde toomount macOS hello Terminal kullanarak ve hello Bulucu kullanıcı Arabirimi ile bir Azure dosya paylaşımı gösterir.

> [!Note]  
> SMB üzerinden Azure Dosya paylaşımını bağlamadan önce, SMB paket imzalamasını devre dışı bırakmanızı öneririz. Bunu yapmazsanız düşük performans macOS hello Azure dosya paylaşımı erişirken verim. Merhaba güvenlik bağlantınızın etkilemesini SMB bağlantınızı şifrelenir. Terminal Hello hello aşağıdaki komutları SMB paket imzalama, bu tarafından açıklandığı gibi devre dışı bırakır [SMB paket imzalama devre dışı bırakma Apple destek makalesine](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>macOS’ta Azure Dosya paylaşımını bağlama önkoşulları
* **Depolama hesabı adı**: toomount bir Azure dosya paylaşımı, hello depolama hesabının adını hello.

* **Depolama hesabı anahtarı**: toomount bir Azure dosya paylaşımı, birincil (veya ikincil) depolama anahtarı hello. SAS anahtarları şu an bağlama için desteklenmemektedir.

* **Bağlantı noktası 445’in açık olduğundan emin olun**: SMB, TCP bağlantı noktası 445 üzerinden iletişim kurar. (Merhaba Mac), istemci makinenizde toomake, güvenlik duvarının TCP bağlantı noktası 445 engellemediğinden emin olun.

## <a name="mount-an-azure-file-share-via-finder"></a>Bulucu yoluyla Azure Dosya paylaşımını bağlama
1. **Bulucu açmak**: Bulucu varsayılan macOS üzerinde açık, ancak, bunu hello şu anda seçili uygulama hello "macOS yüz simgesi"'i tıklatarak hello noktasında sağlayabilirsiniz:  
    ![Merhaba macOS yüz simgesi](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)

2. **"TooServer Bağlan" hello "Git" menü seçin**: hello hello UNC yolundan kullanarak [Önkoşullar](#preq), Dönüştür hello başına çift ters eğik çizgi (`\\`) çok`smb://` ve tüm diğer ters eğik çizgi (`\`) tooforwards eğik çizgi (`/`). Bağlantı hello aşağıdaki gibi görünmelidir: ![hello "tooServer Bağlan" iletişim](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)

3. **Bir kullanıcı adı ve parola istendiğinde hello paylaşım adı ve depolama hesabı anahtarı kullan**: "Bağlan" hello "tooServer Bağlan" iletişim kutusunda tıklattığınızda hello kullanıcı adı ve parola (Bu olacaktır, macOS ile autopopulated istenir Kullanıcı adı). MacOS Anahtarlık hello paylaşım adı/depolama hesabı anahtarı yerleştirme hello seçeneğiniz vardır.

4. **Kullanım hello Azure dosya paylaşımı istediğiniz gibi**: hello paylaşım adı ve depolama hesabı anahtar hello kullanıcı adı ve parola değiştirme sonra hello paylaşımı bağlanır. Dosyaları hello dosya paylaşım içine sürükleyip dahil olmak üzere bir yerel klasör/dosya paylaşımı, normalde kullandığınız gibi bu kullanabilir:

    ![Bağlı bir Azure Dosya paylaşımının anlık görüntüsü](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Terminal yoluyla Azure Dosya paylaşımını bağlama
1. Değiştir `<storage-account-name>` depolama hesabınızın hello ada sahip. İstendiğinde parola olarak Depolama Hesabı Anahtarı’nı girin. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Kullanım hello Azure dosya paylaşımı istediğiniz gibi**: hello Azure dosya paylaşımı takılı hello önceki komutu tarafından belirtilen hello bağlama noktasında.  

    ![Bir anlık görüntüsünü takılı hello Azure dosya paylaşımı](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Sonraki adımlar
Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.

* [Apple destek makalesi - nasıl tooconnect dosya paylaşımı Mac](https://support.apple.com/HT204445)
* [SSS](storage-files-faq.md)
* [Sorun giderme](storage-troubleshoot-file-connection-problems.md)