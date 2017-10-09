---
title: "aaaMount bir Azure dosya paylaşımı ve erişim hello paylaşmak Windows | Microsoft Docs"
description: "Bir Azure dosya paylaşımı ve Windows hello paylaşımına erişim bağlayın."
services: storage
documentationcenter: na
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
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Bir Azure dosya paylaşımı ve Windows hello paylaşımına erişim bağlama
[Azure File storage](storage-dotnet-how-to-use-files.md) Microsoft'un kolay toouse bulut dosya sistemidir. Azure Dosya paylaşımları, Windows ve Windows Server’a bağlanabilir. Bu makalede üç farklı şekilde toomount bir Azure dosya paylaşımı Windows gösterilmektedir: hello dosya Gezgini kullanıcı Arabirimi, PowerShell aracılığıyla ve hello komut istemi aracılığıyla ile. 

Bir Azure dosya paylaşımı dışında hello içinde şirket içi gibi veya farklı bir Azure bölgesindeki barındırıldığı Azure bölgesi sipariş toomount içinde SMB 3.0 hello OS desteklemesi gerekir. 

Azure Dosya paylaşımı, işletim sistemi sürümüne bağlı olarak şirket içindeki Windows makinesine veya Azure sanal makinesine bağlanabilir. Aşağıdaki tablo hello gösterir 

| Windows Sürümü        | SMB Sürümü |Azure VM'ye Bağlanabilir|Şirket İçine Bağlanabilir|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Evet                 | Hayır                  |
| Windows Server 2008 R2 | SMB 2.1     | Evet                 | Hayır                  |
| Windows 8              | SMB 3.0     | Evet                 | Evet                 |
| Windows Server 2012    | SMB 3.0     | Evet                 | Evet                 |
| Windows Server 2012 R2 | SMB 3.0     | Evet                 | Evet                 |
| Windows 10             | SMB 3.0     | Evet                 | Evet                 |

> [!Note]  
> Her zaman alma öneririz Windows sürümünüz için en son KB hello.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Windows ile Azure Dosya Paylaşımını bağlama önkoşulları 
* **Depolama hesabı adı**: toomount bir Azure dosya paylaşımı, hello depolama hesabının adını hello.

* **Depolama hesabı anahtarı**: toomount bir Azure dosya paylaşımı, birincil (veya ikincil) depolama anahtarı hello. SAS anahtarları şu an bağlama için desteklenmemektedir.

* **Bağlantı noktası 445’in açık olduğundan emin olun**: Azure Dosya depolama SMB protokolünü kullanır. Güvenlik duvarınızın istemci makineden 445 numaralı TCP bağlantı noktaları engellemediğinden SMB 445 - TCP bağlantı noktası üzerinden iletişim kurar toosee kontrol edin.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Dosya Gezgini ile Hello Azure dosya paylaşımını bağlama
> [!Note]  
> Yönergeleri izleyerek hello Not üzerinde Windows 10 gösterilir ve eski sürümleri üzerinde biraz farklı olabilir. 

1. **Dosya Gezgini'ni açın**: Bu hello Başlat menüsü açmasının tarafından ya da Win + E kısayol tuşuna basarak yapılabilir.

2. **Merhaba penceresinin hello sol taraftaki toohello "Bu bilgisayar" öğesini gidin. Bu hello menüleri hello Şeritte kullanılabilir değiştirir. "Ağ sürücüsüne" Merhaba bilgisayar menüsünün altında tıklatın**.
    
    ![Merhaba "Harita ağ sürücüsü" açılan menüden bir ekran görüntüsü](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Merhaba "Bağlan" Merhaba Azure portal bölmesinde Kopyala hello UNC yolundan**: toofind bu bilgileri nasıl bulunabilir ayrıntılı bir açıklama [burada](storage-file-how-to-use-files-portal.md#connect-to-file-share).

    ![Merhaba UNC yolundan hello Azure dosya depolama Bağlan bölmesi](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. **Merhaba sürücü harfi seçin ve hello UNC yolunu girin.** 
    
    !["Ağ sürücüsüne" Merhaba iletişim kutusunun ekran görüntüsü](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Kullanım hello depolama hesabı adı ile $a `Azure\` hello kullanıcı adı ve bir depolama hesabı anahtarı hello parola olarak olarak.**
    
    ![Merhaba ağ kimlik bilgisi iletişim kutusunun ekran görüntüsü](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Azure Dosya paylaşımını istediğiniz gibi kullanın**.
    
    ![Azure Dosya paylaşımı artık bağlanmıştır](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Hazır toodismount olan (veya kesin olduğunda) hello Azure dosya paylaşımı, hello girişinde hello "ağ konumlarını" dosya Gezgini'nde altında hello paylaşımı için sağ tıklayarak ve "Bağlantıyı Kes"'yi seçerek bunu yapabilirsiniz**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>PowerShell ile Hello Azure dosya paylaşımını bağlama
1. **Kullanım hello şu komutu toomount hello Azure dosya paylaşımı**: tooreplace unutmayın `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello uygun bilgilerle.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Kullanım hello Azure dosya paylaşımı istediğiniz gibi**.

3. **İşiniz bittiğinde, komutu aşağıdaki hello kullanarak hello Azure dosya paylaşımı kaldırma**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> Merhaba kullanabilir `-Persist` parametresini `New-PSDrive` toomake hello Azure dosya paylaşımı görünür toohello hello takılı sırasında işletim sistemi geri kalanı.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Komut İstemi ile Hello Azure dosya paylaşımını bağlama
1. **Kullanım hello şu komutu toomount hello Azure dosya paylaşımı**: tooreplace unutmayın `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello uygun bilgilerle.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Kullanım hello Azure dosya paylaşımı istediğiniz gibi**.

3. **İşiniz bittiğinde, komutu aşağıdaki hello kullanarak hello Azure dosya paylaşımı kaldırma**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> Kalıcı hello kimlik bilgileri Windows tarafından yeniden başlatmada hello Azure dosya paylaşımı tooautomatically yeniden yapılandırabilirsiniz. komutu aşağıdaki hello hello kimlik kalıcı:
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Sonraki adımlar
Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.

* [SSS](storage-files-faq.md)
* [Sorun giderme](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Kavramsal makaleler ve videolar
* [Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Nasıl toouse Linux Azure File storage](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Azure Dosya depolama için araç desteği
* [Azure Depolama ile Azure PowerShell’i kullanma](storage-powershell-guide-full.md)
* [Nasıl toouse Microsoft Azure Storage ile AzCopy](storage-use-azcopy.md)
* [Azure Storage ile Hello Azure CLI kullanma](storage-azure-cli.md#create-and-manage-file-shares)
* [Azure Dosya depolama sorunlarını giderme](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a>Blog yazıları
* [Azure Dosya Depolama genel kullanıma sunulmuştur](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure Dosya depolama incelemesi](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure Dosya Hizmeti’ne Giriş](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Geçirme verilerini tooAzure dosyası](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Başvuru
* [.NET başvurusu için Depolama İstemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dosya Hizmeti REST API başvurusu](http://msdn.microsoft.com/library/azure/dn167006.aspx)
