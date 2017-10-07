---
title: aaaHow toouse PowerShell toomanage Azure File storage | Microsoft Docs
description: "Toouse PowerShell toomanage Azure File storage öğrenin."
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>Nasıl toouse PowerShell toomanage Azure dosya depolama
Azure PowerShell toocreate ve dosya paylaşımlarını yönetmek kullanabilirsiniz.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Azure Storage için Hello PowerShell cmdlet'lerini yükleyin
tooprepare toouse PowerShell, indirin ve hello Azure PowerShell cmdlet'lerini yükleyin. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs) noktası ve yükleme yönergeleri için hello yükleyin.

> [!NOTE]
> Bu, indirin ve yükleyin veya toohello en son Azure PowerShell modülü yükseltme önerilir.
> 
> 

**Başlat**’a tıklayıp **Windows PowerShell** yazarak Azure PowerShell penceresini açın. Merhaba PowerShell penceresinde hello Azure Powershell modülü sizin yerinize yükler.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Depolama hesabınız ve anahtarı için bir bağlam oluşturma
Merhaba depolama hesabı bağlamını oluşturun. Merhaba bağlam Merhaba, depolama hesabı adı ve hesap anahtarını kapsar. Hesap anahtarınızı hello kopyalama yönergeleri için [Azure portal](https://portal.azure.com), bkz: [depolama erişim tuşlarını görüntüleme ve kopyalama](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

Değiştir `storage-account-name` ve `storage-account-key` depolama hesabı adı ve örnek aşağıdaki hello anahtarında ile.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Yeni dosya paylaşımı oluşturma
Adlı hello yeni paylaşım oluşturun `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

Artık, File Storage’da bir dosya paylaşımınız bulunur. Şimdi, bir dizin ve dosya ekleyeceğiz.

> [!IMPORTANT]
> Merhaba, dosya paylaşımının adını tamamen küçük harfli olması gerekir. Dosya paylaşımlarının ve dosyaların adlandırılması hakkında tüm ayrıntılara ulaşmak için bkz. [Paylaşımları, Dizinleri, Dosyaları ve Meta Verileri Adlandırma ve Bunlara Başvuruda Bulunma](https://msdn.microsoft.com/library/azure/dn167011.aspx)
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Merhaba dosya paylaşımında bir dizin oluşturun
Merhaba paylaşımda bir dizin oluşturun. Aşağıdaki örneğine hello hello dizin adlı `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Bir yerel dosya toohello dizin karşıya yükle
Şimdi bir yerel dosya toohello dizin karşıya yükleyin. Merhaba aşağıdaki örnek dosya karşıya yükleme `C:\temp\Log1.txt`. Hello dosya yolu geçerli bir dosya tooa yerel makinenizde işaret şekilde düzenleyin.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Merhaba dizininde hello dosyaları listeleme
toosee hello dosya hello dizinindeki tüm hello dizin dosyalarını listeleyebilirsiniz. (Varsa) Bu komut hello CustomLogs dizinindeki hello dosyaları ve alt dizinleri döndürür.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile, hangi dizin nesnesi geçiriliyorsa, onun için dosyaların ve dizinlerin bir listesini döndürür. "Get-AzureStorageFile-Share $s" Merhaba kök dizinindeki dosyaları ve dizinleri listesini döndürür. tooget alt dizindeki dosyaların listesi, toopass hello alt tooGet-AzureStorageFile sahip. Bu yaptığı olan--hello toohello kanal hello komutu ilk parçası CustomLogs hello alt dizininin dizin örneğini döndürür. Daha sonra customlogs alt dizinindeki hello dosyaları ve dizinleri döndüren Get-AzureStorageFile içine geçirilir.

## <a name="copy-files"></a>Dosyaları kopyalama
Azure PowerShell'in 0.9.7 sürümünden başlayarak, tooanother dosyası, dosya tooa blob veya bir blobu tooa dosyayı kopyalayabilirsiniz. Aşağıda nasıl tooperform bu kopyalama göstermek PowerShell cmdlet'lerini kullanarak işlemleri.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Sonraki adımlar
Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.

* [SSS](../storage-files-faq.md)
* [Windows’da sorun giderme](storage-troubleshoot-windows-file-connection-problems.md)      
* [Linux’ta sorun giderme](storage-troubleshoot-linux-file-connection-problems.md)    