---
title: Azure Storage ile Azure PowerShell aaaUsing | Microsoft Docs
description: "Nasıl toouse Azure Storage toocreate için Azure PowerShell cmdlet'leri hello ve depolama hesaplarını yönetme öğrenin; BLOB'lar, tablolar, kuyruklar ve dosyaları ile çalışma; Yapılandırma depolama analytics sorgu ve paylaşılan erişim imzaları oluşturma."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Azure Storage ile Azure PowerShell’i kullanma
## <a name="overview"></a>Genel Bakış
Azure PowerShell cmdlet'leri toomanage Windows PowerShell üzerinden Azure sağlayan bir modüldür. Sistem yönetimi için özel olarak tasarlanan görev tabanlı bir komut satırı kabuğu ve betik dili olarak tanımlanır. PowerShell ile kolayca kontrol edebilir ve hello Azure Hizmetleri ve uygulamaları otomatikleştirmesini. Örneğin, aynı görevleri hello gerçekleştirebilirsiniz hello cmdlet'leri tooperform hello kullanabilirsiniz [Azure portal](https://portal.azure.com).

Bu kılavuzda, biz ele alacağız nasıl toouse hello [Azure depolama cmdlet'leri](/powershell/module/azurerm.storage/#storage) tooperform çeşitli Azure Storage ile geliştirme ve yönetim görevleri.

Bu kılavuz, kullanma konusunda deneyim sahibi olduğunuzu varsayar [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) ve [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Merhaba Kılavuzu bir dizi betiği toodemonstrate hello Azure Storage ile PowerShell kullanımını sağlar. Her komut dosyası çalıştırılmadan önce yapılandırmanıza göre hello betik değişkenlerini güncelleştirmeniz gerekir.

Bu kılavuzdaki Hello ilk bölüm, PowerShell ve Azure Storage hızlı bir bakışta sağlar. Ayrıntılı bilgi ve yönergeler için hello Başlat [Azure Storage ile Azure PowerShell'i kullanma önkoşulları](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Azure Storage ve PowerShell 5 dakika içinde Başlarken
Bu bölümde, nasıl gösterilir tooaccess Azure Storage PowerShell aracılığıyla 5 dakika.

**Yeni tooAzure:** Microsoft Azure aboneliği ve bu abonelikle ilişkili bir Microsoft hesabı alın. Azure satın alma seçenekleri hakkında daha fazla bilgi için bkz: [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/), [satın alma seçenekleri](https://azure.microsoft.com/pricing/purchase-options/), ve [üye teklifleri](https://azure.microsoft.com/pricing/member-offers/) (MSDN, Microsoft iş ortağı ağı ve, BizSpark üyeleri için ve diğer Microsoft programları).

Bkz: [Azure Active Directory'de (Azure AD) yönetici rolleri atama](https://msdn.microsoft.com/library/azure/hh531793.aspx) Azure abonelikleri hakkında daha fazla bilgi için.

**Microsoft Azure aboneliği ve hesabı oluşturduktan sonra:**

1. Merhaba son yükleyip [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Başlangıç Windows PowerShell Tümleşik komut dosyası ortamı (ISE): yerel bilgisayarınıza toohello Git **Başlat** menüsü. Tür **Yönetimsel Araçlar** ve toorun'ı tıklatın. Merhaba, **Yönetimsel Araçlar** penceresinde, sağ **Windows PowerShell ISE**, tıklatın **yönetici olarak çalıştır**.
3. İçinde **Windows PowerShell ISE**, tıklatın **dosya** > **yeni** toocreate yeni bir komut dosyası.
4. Şimdi, biz temel PowerShell komutları tooaccess Azure Storage gösteren basit bir komut dosyası size. Merhaba komut dosyası, ilk Azure hesabı toohello yerel PowerShell ortamınızın Azure hesabı kimlik bilgileri tooadd isteyecektir. Ardından, hello betik hello varsayılan Azure aboneliği ve Azure'da yeni bir depolama hesabı oluşturun. Ardından, hello betik bu yeni depolama hesabı yeni bir kapsayıcı oluşturur ve var olan bir görüntü dosyası (blob) toothat kapsayıcıyı karşıya yükleyin. Bu kapsayıcıdaki tüm blob'lara Hello komut dosyasını listeler sonra yerel bilgisayarınızda yeni bir hedef dizin oluşturun ve hello görüntü dosyasını indirin.
5. Kod bölümünde aşağıdaki hello hello açıklamalar arasında hello komut dosyalarını seçin **#begin** ve **#end**. CTRL + C toocopy tuşuna basın, toohello Pano.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. İçinde **Windows PowerShell ISE**, CTRL + V toocopy hello betik tuşuna basın. Tıklatın **dosya** > **kaydetmek**. Merhaba, **Kaydet** iletişim penceresinde, "mystoragescript." gibi hello komut dosyası türü hello adı **Kaydet** düğmesine tıklayın.
7. Şimdi, yapılandırma ayarlarınızı temel alan tooupdate hello komut dosyası değişkenleri gerekir. Merhaba güncelleştirmelisiniz **$SubscriptionName** kendi aboneliğinizle değişken. Merhaba hello betik belirtildiği gibi diğer değişkenleri tutun veya bunları istediğiniz gibi güncelleştirin.
   
   * **$SubscriptionName:** Bu değişken, kendi abonelik adı ile güncelleştirmeniz gerekir. Üç yolu toolocate hello aboneliğinizin adından hello birini izleyin:
     
    a. İçinde **Windows PowerShell ISE**, tıklatın **dosya** > **yeni** toocreate yeni bir komut dosyası. Kopya hello aşağıdakiler toohello yeni komut dosyası komut dosyası ve tıklatın **hata ayıklama** > **çalıştırmak**. Merhaba aşağıdaki komut dosyası ilk Azure hesabı kimlik bilgileri tooadd Azure hesabı toohello yerel PowerShell ortamınızın isteyin ve bağlı toohello yerel PowerShell oturumu tüm hello aboneliklerin göster. Bu öğreticiyi izleyerek sırasında toouse istediğiniz hello hello abonelik adını not alın:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. aboneliğinizi toolocate ve kopyalama hello ad [Azure portal](https://portal.azure.com), buna sol hello Hub menüsünde Merhaba, tıklatın **abonelikleri**. Bu kılavuzda hello betikleri çalıştırılırken toouse istediğiniz abonelik Hello adı kopyalayın.
     
     ![Azure portalına](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. aboneliğinizi toolocate ve kopyalama hello ad [Klasik Azure portalı](https://manage.windowsazure.com/), aşağı kaydırın ve tıklayın **ayarları** yan hello portalının sol hello üzerinde. Tıklatın **abonelikleri** toosee aboneliklerinizi listesi. Bu kılavuzda verilen hello betikleri çalıştırılırken toouse istediğiniz abonelik Hello adı kopyalayın.
     
     ![Klasik Azure Portalı](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** hello komut dosyasında adı verilen hello kullanın veya depolama hesabınız için yeni bir ad girin. **Önemli:** hello depolama hesabının adını hello Azure içinde benzersiz olmalıdır. Çok küçük olmalıdır!
   * **$Location:** "Batı ABD" verilen hello hello komut dosyasında kullanın veya Doğu ABD, Kuzey Avrupa vb. gibi diğer Azure konumları seçin.
   * **$ContainerName:** hello komut dosyasında adı verilen hello kullanın veya, kapsayıcı için yeni bir ad girin.
   * **$ImageToUpload:** yolu tooa resim, yerel bilgisayarınızda gibi girin: "C:\Images\HelloWorld.png".
   * **$DestinationFolder:** bir yolu tooa yerel dizin toostore dosyaları Azure Storage'dan gibi indirilen girin: "C:\DownloadImages".
8. Merhaba "mystoragescript.ps1" dosyasındaki Hello komut dosyası değişkenleri güncelleştirdikten sonra tıklatın **dosya** > **kaydetmek**. Ardından **hata ayıklama** > **çalıştırmak** veya basın **F5** toorun hello komut dosyası.  

Merhaba betik çalıştıktan sonra indirilen hello görüntü dosyasını içeren bir yerel hedef klasör olmalıdır. Merhaba ekran aşağıdaki örnek çıkış şunları gösterir:

![BLOB'ları indirme](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Merhaba "5 dakika içinde Azure Storage ve PowerShell Başlarken" bölümünde bir giriş nasıl sağlanan toouse Azure PowerShell'i Azure Storage ile. Ayrıntılı bilgi ve yönergeler için aşağıdaki bölümlerde tooread hello öneririz.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Azure Storage ile Azure PowerShell'i kullanma önkoşulları
Bu kılavuzda verilen bir Azure aboneliği ve hesabı toorun hello PowerShell cmdlet'leri, yukarıda açıklandığı gibi gerekir.

Azure PowerShell cmdlet'leri toomanage Windows PowerShell üzerinden Azure sağlayan bir modüldür. Yükleme ve Azure PowerShell ayarlama hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). İndirin ve yükleyin veya bu kılavuzu kullanmadan önce toohello en son Azure PowerShell modülü yükseltme öneririz.

Merhaba standart Windows PowerShell konsolu veya Windows PowerShell Tümleşik komut dosyası ortamı (ISE) hello hello cmdlet'lerini çalıştırabilirsiniz. Örneğin, tooopen **Windows PowerShell ISE**, toohello Başlat menüsüne gidin, Yönetimsel Araçlar yazın ve toorun'ı tıklatın. Merhaba Yönetimsel Araçlar penceresinde, Windows PowerShell ISE sağ tıklatın, yönetici olarak çalıştır'ı tıklatın.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Azure'da nasıl toomanage depolama hesapları

Depolama hesaplarını Azure PowerShell ile yönetme bir bakalım

### <a name="how-tooset-a-default-azure-subscription"></a>Nasıl tooset varsayılan bir Azure aboneliği
toomanage Azure PowerShell kullanarak Azure Storage istemci ortamınızı Azure ile Azure Active Directory kimlik doğrulaması veya sertifika tabanlı kimlik doğrulaması üzerinden tooauthenticate gerekir. Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) Öğreticisi. Bu kılavuz hello Azure Active Directory kimlik doğrulaması kullanır.

1. Windows PowerShell ISE'de komutu tooadd aşağıdaki hello Azure hesabı toohello yerel PowerShell ortamınızın yazın:

    ```powershell
    Add-AzureAccount
    ```

2. Merhaba "tooMicrosoft Azure oturum" penceresinde, hello e-posta adresini yazın ve hesabınızla ilişkili parola. Azure kimliğini doğrular ve hello kimlik bilgileri kaydeder ve hello penceresini kapatır.

3. Ardından, Azure yerel PowerShell ortamınızda hesapları ve hesabınızın listelendiğini doğrulayın komutu tooview hello aşağıdaki hello çalıştırın:
   
    ```powershell
    Get-AzureAccount
    ```
4. Ardından, cmdlet tooview aşağıdaki hello bağlı toohello yerel PowerShell oturumu tüm hello aboneliklerin çalıştırın ve aboneliğinizi listelenmiş olduğunu doğrulayın:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. Varsayılan bir Azure aboneliği tooset Hello Select-AzureSubscription cmdlet'ini çalıştırın:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Merhaba varsayılan abonelik Hello adı hello Get-AzureSubscription cmdlet'ini çalıştırarak doğrulayın:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee tüm hello kullanılabilir için PowerShell cmdlet'leri Azure Storage çalıştırın:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>Nasıl toocreate yeni bir Azure depolama hesabı
toouse Azure depolama, depolama hesabı gerekir. Bilgisayar tooconnect tooyour aboneliğinizi yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz.

1. Merhaba Get-AzureLocation cmdlet'i toofind tüm hello kullanılabilir veri merkezi konumlarını çalıştırın:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Ardından, yeni bir depolama hesabı hello yeni AzureStorageAccount cmdlet toocreate çalıştırın. Merhaba aşağıdaki örnek yeni bir depolama hesabı hello "Batı ABD" merkezinde oluşturur.
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> Depolama hesabınızın adını Hello Azure içinde benzersiz olmalıdır ve küçük harf olmalıdır. Adlandırma kuralları ve sınırlamaları için bkz: [Azure Storage hesapları hakkında](storage-create-storage-account.md) ve [adlandırma ve başvuran kapsayıcıları, Blobları ve meta veri](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>Nasıl tooset varsayılan bir Azure depolama hesabı
Aboneliğinizde birden çok depolama hesabı olabilir. Bunlardan birini seçin ve tüm depolama hello için hello varsayılan depolama hesabı hello aynı komutları olarak ayarlamak PowerShell oturumu. Bu işlem, hello depolama bağlamı açıkça belirtmeden toorun hello Azure PowerShell depolama komutları sağlar.

1. aboneliğiniz için bir varsayılan depolama hesabı tooset hello Set-AzureSubscription cmdlet'i çalıştırabilirsiniz.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Ardından, hello depolama hesabı varsayılan abonelik hesabınızla ilişkilendirilmiş olduğunu hello Get-AzureSubscription cmdlet'i tooverify çalıştırın. Bu komut, geçerli bir depolama hesabı dahil olmak üzere hello geçerli abonelikte hello abonelik özellikleri döndürür.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Nasıl toolist bir Abonelikteki tüm Azure depolama hesapları
Her Azure aboneliği too100 depolama hesapları olabilir. Merhaba en güncel sınırları hakkında bilgi için [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).

Cmdlet toofind hello adı ve hello hello geçerli Abonelikteki depolama hesapları durumunu izleyen hello çalıştırın:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>Nasıl toocreate bir Azure depolama bağlamı
Azure depolama bağlam PowerShell tooencapsulate hello depolama kimlik bilgilerinde bir nesnedir. Herhangi bir sonraki cmdlet çalıştırırken bir depolama bağlamı kullanarak, tooauthenticate isteğiniz hello depolama hesabı ve erişim anahtarını açıkça belirtmeden sağlar. Bir depolama bağlamı kullanarak depolama hesabı adı ve erişim anahtarı, paylaşılan erişim imzası (SAS) belirteci, bağlantı dizesi gibi birçok yolla oluşturabilirsiniz veya anonim. Daha fazla bilgi için bkz: [yeni AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Bir depolama bağlamı üç yolu toocreate aşağıdaki hello birini kullanın:

* Merhaba çalıştırmak [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind hello birincil depolama erişim tuşunu Azure depolama hesabınız için çıkışı. Ardından, hello'ı çağırın [yeni AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate depolama bağlamı:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Bir Azure depolama kapsayıcısı için bir paylaşılan erişim imzası belirteç oluşturmak ve toocreate depolama bağlamı kullanın:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Daha fazla bilgi için bkz: [yeni AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) ve [kullanarak paylaşılan erişim imzaları (SAS)](storage-dotnet-shared-access-signature-part-1.md).

* Bazı durumlarda, yeni bir depolama bağlamı oluşturduğunuzda toospecify hello hizmet uç noktaları isteyebilirsiniz. Merhaba Blob hizmetine depolama hesabınız için bir özel etki alanı adı kayıtlı veya depolama kaynaklarına erişmek için bir paylaşılan erişim imzası toouse istediğiniz durumlarda bu gerekli olabilir. Bağlantı dizesinde Hello hizmet uç noktaları ayarlayın ve aşağıda gösterildiği gibi toocreate yeni bir depolama bağlamı kullanın:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Hakkında daha fazla bilgi için tooconfigure bir depolama bağlantı dizesi bkz [bağlantı dizelerini yapılandırma](storage-configure-connection-string.md).

Bilgisayarınızı ayarlayın ve öğrenilen göre nasıl toomanage abonelikleri ve storage hesaplarını Azure PowerShell kullanarak nasıl toomanage Azure BLOB toohello sonraki bölümde toolearn gidin ve anlık görüntülerini blob.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>Nasıl tooretrieve ve yeniden Azure depolama anahtarları
Bir Azure Storage hesabı iki hesabı anahtarları ile birlikte gelir. Cmdlet tooretrieve aşağıdaki hello anahtarlarınızı kullanabilirsiniz.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Aşağıdaki cmdlet'i tooretrieve belirli bir anahtarın hello kullanın. Birincil ve ikincil değerler geçerlidir.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Tooregenerate isterseniz, anahtarlarınızı cmdlet'i aşağıdaki hello kullanın. "Birincil" ve "İkincil" - KeyType için geçerli değerler:

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Nasıl toomanage Azure BLOB
Azure Blob Depolama büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış veriyi depolamak için bir hizmettir. Bu bölümde, zaten hello Azure Blob Depolama hizmetinin kavramlarını olduğunu varsayar. Ayrıntılı bilgi için bkz: [.NET kullanarak Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-toocreate-a-container"></a>Nasıl toocreate bir kapsayıcı
Azure depolama her blob bir kapsayıcıda olmalıdır. Merhaba yeni AzureStorageContainer cmdlet'ini kullanarak özel bir kapsayıcı oluşturabilirsiniz:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Anonim okuma erişimini üç düzeyi vardır: **kapalı**, **Blob**, ve **kapsayıcı**. tooprevent anonim erişim tooblobs, kümesi hello izni parametresi çok**devre dışı**. Varsayılan olarak, hello yeni kapsayıcı özeldir ve yalnızca hello hesap sahibi tarafından erişilebilir. tooallow anonim ortak okuma erişimine tooblob, ancak değil toocontainer meta veriler veya toohello listesi hello kapsayıcıdaki blobları, hello izni çok parametre**Blob**. tooallow tam ortak okuma tooblob kaynaklara erişmesine, kapsayıcı meta verileri ve hello kapsayıcıdaki blobları hello listesi, hello izni çok parametre**kapsayıcı**. Daha fazla bilgi için bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>Nasıl bir kapsayıcı halinde tooupload blob
Azure Blob Storage blok blobları ve sayfa bloblarını destekler. Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooa kapsayıcıdaki blobları tooupload, kullanabileceğiniz hello [kümesi AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet'i. Varsayılan olarak, bu komut hello yerel dosyaları tooa blok blobu yükler. toospecify hello türü hello blob için hello - BlobType parametresini kullanabilirsiniz.

Merhaba aşağıdaki örnekte çalışan hello [Get-Childıtem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget tüm hello hello belirtilen klasördeki dosyaları ve daha sonra bunları toohello sonraki cmdlet hello ardışık düzen işleci kullanılarak geçirir. Merhaba [kümesi AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet hello yerel dosyaları tooyour kapsayıcı yükler:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Nasıl toodownload kapsayıcıdan BLOB
Aşağıdaki örnek hello nasıl toodownload kapsayıcıdan BLOB'ların gösterir. Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve birincil erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak. Ardından, hello örnek hello kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i. Ardından, hello örnek hello kullanır [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload BLOB'lar hello yerel hedef klasöre.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Bir depolama kapsayıcısı tooanother toocopy nasıl BLOB
BLOB storage hesapları ve bölgeler arasında zaman uyumsuz olarak kopyalayabilirsiniz. Merhaba aşağıdaki örnekte nasıl bir depolama kapsayıcısı tooanother iki farklı depolama hesaplarındaki gelen toocopy BLOB gösterir. Merhaba örneği ilk kaynak ve hedef depolama hesapları için değişkenleri ayarlar ve ardından her hesap için bir depolama bağlam oluşturur. Ardından, hello örnek hello kullanarak hello kaynak kapsayıcı toohello hedef kapsayıcıdan BLOB kopyalar [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet'i. Merhaba örnek hello kaynak ve hedef depolama hesapları ve kapsayıcıları zaten mevcut olduğunu varsayar.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Bu örnekte bir zaman uyumsuz kopya gerçekleştirmediğini unutmayın. Merhaba çalıştırarak her kopya hello durumunu izleyebilirsiniz [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet'i.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>İkincil bir konumdan toocopy nasıl BLOB
BLOB'ları hello ikincil RA-GRS etkinleştirilmiş bir hesap konumundan kopyalayabilirsiniz.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>Nasıl toodelete blob
toodelete bir blob önce bir blob başvurusu alın ve ardından hello Kaldır AzureStorageBlob cmdlet üzerinde çağırın. Aşağıdaki örneğine hello belirli bir kapsayıcıda tüm hello BLOB'lar siler. Hello örnek ilk değişkenleri bir depolama hesabı için ayarlar ve bir depolama bağlamı oluşturur. Ardından, hello örnek hello kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalıştırmalarını hello [Kaldır AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove bloblarından Azure depolama alanında bir kapsayıcı.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Nasıl toomanage Azure blob anlık görüntüler
Azure blob görüntüsünü oluşturmanıza olanak sağlar. Bir anlık görüntüsü, bir noktada geçen süre içinde bir blob, salt okunur bir sürümüdür. Bir anlık görüntü oluşturulduktan sonra okumak, kopyalanan, veya silinmiş, ancak değişiklik. Bir anda göründüğü gibi anlık bir blob yukarı şekilde tooback sağlar. Daha fazla bilgi için bkz: [Blob anlık görüntüsünün oluşturulmasına](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>Nasıl toocreate blob anlık görüntü
toocreate snaphot bir BLOB ilk bir blob başvurusu alın ve hello çağrı `ICloudBlob.CreateSnapshot` yöntemini. Merhaba aşağıdaki örnek ilk değişkenleri bir depolama hesabı için ayarlar ve ardından depolama bağlam oluşturur. Ardından, hello örnek hello kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalıştırmalarını hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) yöntemi toocreate bir anlık görüntü.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>Nasıl toolist blob'ın anlık görüntüler
Bir blob için istediğiniz sayıda anlık görüntü oluşturabilirsiniz. Merhaba anlık görüntüler, blob tootrack ile ilişkili listesinde, geçerli anlık görüntüler. Merhaba aşağıdaki örnek kullanan önceden tanımlanmış bir blob ve çağrıları hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) bu blob cmdlet toolist hello anlık görüntüleri.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>Nasıl toocopy anlık görüntüsünü bir blob
Bir blob toorestore hello anlık görüntüsünü kopyalayabilirsiniz. Ayrıntılı bilgi ve kısıtlamaları için bkz: [Blob anlık görüntüsünün oluşturulmasına](http://msdn.microsoft.com/library/azure/hh488361.aspx). Merhaba aşağıdaki örnek ilk değişkenleri bir depolama hesabı için ayarlar ve ardından depolama bağlam oluşturur. Ardından, hello örnek hello kapsayıcı ve blob adı değişkenleri tanımlar. Merhaba örneği alır hello kullanarak bir blob başvurusu [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalıştırmalarını hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) yöntemi toocreate bir anlık görüntü. Ardından, hello örnek hello çalıştırır [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello anlık görüntüsü için hello kaynak blob hello ICloudBlob nesnesi kullanılarak bir blob. Emin tooupdate hello değişkenleri yapılandırmanızı çalışan hello örnek önce dayalı olabilir. Aşağıdaki örnek, hello hello kaynak ve hedef kapsayıcılarını ve hello kaynak blob zaten mevcut varsayar unutmayın.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Nasıl toomanage Azure BLOB öğrendiniz ve Azure PowerShell ile anlık görüntülerini blob göre nasıl toomanage tabloları, kuyrukları ve dosyaları toohello sonraki bölümde toolearn gidin.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Nasıl toomanage Azure tabloları ve varlıkları tablo
Azure tablo depolama hizmetidir kullanabileceğiniz bir nosql olmayan veri yapılandırılmış ve ilişkisel olmayan verilerin büyük kümelerini toostore ve sorgu. Merhaba ana hello hizmet tablo, varlıkları ve özelliklerini bileşenleridir. Bir tablo, varlıkları koleksiyonudur. Bir varlık özellikler kümesidir. Her varlığın tüm ad-değer çiftleri too252 özellikleri olabilir. Bu bölümde, zaten hello Azure tablo depolama hizmeti kavramlarını olduğunu varsayar. Ayrıntılı bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://msdn.microsoft.com/library/azure/dd179338.aspx) ve [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md).

Aşağıdaki alt bölümleri hello nasıl toomanage Azure Table depolama hizmeti Azure PowerShell kullanarak bilgi edineceksiniz. Merhaba kapsanan senaryolar dahil **oluşturma**, **silme**, ve **alma** **tabloları**, yanı **ekleme**, **sorgulama**, ve **tablo varlıkları silmek**.

### <a name="how-toocreate-a-table"></a>Nasıl toocreate bir tablo
Her tablo bir Azure depolama hesabında bulunmalıdır. Merhaba aşağıdaki örnekte gösterilmiştir nasıl toocreate Azure storage'da bir tablo. Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak. Ardından, hello kullanan [yeni AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate Azure storage'da bir tablo.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>Nasıl tooretrieve bir tablo
Sorgulamak ve bir depolama hesabı bir ya da tüm tablolarda alın. Merhaba aşağıdaki örnekte nasıl kullanarak verilen Tablo tooretrieve hello gösteren [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Hiçbir parametre olmadan hello Get-AzureStorageTable cmdlet'i çağırırsanız, tüm depolama tablolar için bir depolama hesabı alır.

### <a name="how-toodelete-a-table"></a>Nasıl toodelete bir tablo
Hello kullanarak bir depolama hesabından bir tablo silebilirsiniz [Kaldır AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet'i.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Nasıl toomanage tablo varlıkları
Şu anda Azure PowerShell cmdlet'leri toomanage tablo varlıkları doğrudan sağlamaz. Tablo varlıkları tooperform işlemde hello verilen hello sınıfları kullanabilir [.NET için Azure Storage istemci Kitaplığı](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Nasıl tooadd tablo varlıkları
bir varlık tooa tablosu tooadd ilk varlık özelliklerinizi tanımlayan bir nesne oluşturun. Bir varlığın 3 sistem özelliği de dahil olmak üzere too255 özelliklerini, olabilir: **PartitionKey**, **RowKey**, ve **zaman damgası**. Ekleme ve başlangıç değerleri güncelleştirmek için sorumlu **PartitionKey** ve **RowKey**. Merhaba sunucu yöneten hello değerini **zaman damgası**, hangi değiştirilemez. Birlikte hello **PartitionKey** ve **RowKey** tablo içindeki her varlık benzersiz şekilde tanımlar.

* **PartitionKey**: hello varlık depolanan hello bölüm belirler.
* **RowKey**: hello varlığın hello bölüm içinde benzersiz olarak tanımlar.

Bir varlık için özel özellikleri too252 tanımlayabilir. Daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Merhaba aşağıdaki örnekte gösterilmiştir nasıl tooadd varlıklar tooa tablo. Merhaba örnek nasıl tooretrieve çalışan tablosu hello ve birkaç varlıkları içine ekleyin gösterir. İlk olarak, bir bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak. Ardından, tablo hello kullanarak verilen hello alır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i. Merhaba tablo mevcut değilse hello [yeni AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet'tir kullanılan toocreate Azure storage'da bir tablo. Ardından, her varlığın bölüm ve satır anahtarını belirterek özel bir işlev Ekle varlık tooadd varlıklar toohello tablo hello örnek tanımlar. Merhaba Ekle-varlık işlev çağrılarını hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) hello cmdlet'ini [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) sınıfı toocreate bir varlık nesnesine. Daha sonra hello örnek çağırır hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) bu varlık nesnesi tooadd yöntemi, tooa tablo.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Nasıl tooquery tablo varlıkları
tooquery bir tablo kullanmak hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) sınıfı. Merhaba aşağıdaki örneği hello nasıl verilen hello betik zaten çalıştırdıysanız varsayar tooadd varlıklar başlığına bakın. Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama bağlamını kullanarak. Ardından, hello kullanarak tooretrieve daha önce oluşturduğunuz hello "Çalışanlar" tablosu çalışır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i. Arama hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello Microsoft.WindowsAzure.Storage.Table.TableQuery sınıf üzerinde yeni bir sorgu nesnesi oluşturur. Merhaba örnek 1 dize filtresi belirtildiği gibi değeri olan 'ID' sütun hello varlıklar arar. Ayrıntılı bilgi için bkz: [sorgulama tabloları ve varlıkları](http://msdn.microsoft.com/library/azure/dd894031.aspx). Bu sorguyu çalıştırmak hello filtre ölçütüyle eşleşen tüm varlıkları döndürür.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Nasıl toodelete tablo varlıkları
Bir varlığın bölüm ve satır anahtarını kullanarak silebilirsiniz. Merhaba aşağıdaki örneği hello nasıl verilen hello betik zaten çalıştırdıysanız varsayar tooadd varlıklar başlığına bakın. Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama bağlamını kullanarak. Ardından, hello kullanarak tooretrieve daha önce oluşturduğunuz hello "Çalışanlar" tablosu çalışır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i. Merhaba tablo varsa hello örnek hello çağırır [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) bir varlık üzerinde bölüm ve satır anahtarı değerleri temel yöntemi tooretrieve. Daha sonra hello varlık toohello geçirin [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) yöntemi toodelete.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Nasıl toomanage Azure kuyrukları ve iletileri kuyruğa
Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir. Bu bölümde, zaten hello Azure kuyruk depolama hizmeti kavramlarını olduğunu varsayar. Ayrıntılı bilgi için bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](storage-dotnet-how-to-use-queues.md).

Bu bölümde toomanage Azure kuyruk depolama hizmeti Azure PowerShell kullanarak nasıl yapacağınızı gösterir. Merhaba kapsamdaki senaryolar da dahil **ekleme** ve **silme** kuyruk iletileri yanı **oluşturma**, **silme**ve **sıraları alma**.

### <a name="how-toocreate-a-queue"></a>Nasıl bir kuyruk toocreate
Merhaba aşağıdaki örnek ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak. Ardından, çağıran [yeni AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate 'queuename' adında bir sıra.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Azure kuyruk hizmeti için adlandırma kuralları hakkında bilgi için bkz: [adlandırma kuyrukları ve meta verileri](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>Nasıl bir kuyruk tooretrieve
Sorgulama ve belirli bir sıraya veya bir depolama hesabındaki tüm hello kuyrukların listesini alın. Merhaba aşağıdaki örnekte nasıl kullanarak belirtilen sırayı tooretrieve hello gösterir [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet'i.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Merhaba çağırırsanız [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet parametre olmadan tüm hello kuyrukların listesini alır.

### <a name="how-toodelete-a-queue"></a>Nasıl bir kuyruk toodelete
toodelete bir sıra ve tüm karışılama iletileri, çağrı hello Kaldır AzureStorageQueue cmdlet içerdiği. Aşağıdaki örneğine hello nasıl kullanarak belirtilen sırayı toodelete hello Kaldır AzureStorageQueue cmdlet'ini gösterir.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>Nasıl bir kuyruk iletiye tooinsert
var olan bir sırayı iletiye tooinsert ilk hello yeni bir örneğini oluşturun [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) sınıfı. Ardından, hello'ı çağırın [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) yöntemi. Bir CloudQueueMessage bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi oluşturulabilir.

Aşağıdaki örneğine hello nasıl tooadd tooa kuyruk iletisi gösterir. Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak. Ardından, hello kullanarak hello belirtilen sırayı alır [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet'i. Merhaba sıra hello yoksa, [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet'tir kullanılan toocreate hello örneği [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) sınıfı. Daha sonra hello örnek çağırır hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) bu ileti nesne tooadd yöntemi, tooa sırası. Bir sırayı alır ve selamlama iletisine 'MessageInfo' ekler kod şöyledir:

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Nasıl toode-hello sıraya sonraki ileti
Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır. Merhaba çağırdığınızda [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) kuyrukta hello sonraki iletiyi elde yöntemi. Döndürülen bir ileti **GetMessage** iletileri bu sıradan okuma başka bir kod görünmez tooany olur. toofinish kaldırma selamlama iletisine hello sırasından hello ayrıca çağırmalısınız [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) yöntemi. Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar. Kod çağrılarınızı **DeleteMessage** hello ileti işlendikten sonra sağ.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>Nasıl toomanage Azure dosya paylaşımları ve dosyaları
Azure File storage hello standart SMB protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar. Microsoft Azure virtual machines ve cloud services bağlı paylaşımlar üzerinden uygulama bileşenleri arasında dosya verileri paylaşabilir ve şirket içi uygulamalara hello dosya depolama API'si veya Azure PowerShell üzerinden dosya verilerine erişebilir.

Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](storage-dotnet-how-to-use-files.md) ve [dosya hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-tooset-and-query-storage-analytics"></a>Nasıl tooset ve sorgu depolama analizi
Kullanabileceğiniz [Azure depolama çözümlemeleri](storage-analytics.md) Azure depolama hesapları ve günlük verilerini istekleriyle ilgili toocollect ölçümlerini gönderilen tooyour depolama hesabı. Depolama ölçümleri toomonitor hello sistem durumunu bir depolama hesabı ve depolama günlük toodiagnose ve depolama hesabınızı ile ilgili sorunları gidermek kullanabilirsiniz. Kullanarak izlemeyi yapılandırmadan Azure portalı veya Windows PowerShell'i hello veya program aracılığıyla hello depolama istemci kitaplığı kullanılarak. Depolama günlük sunucu tarafı olur ve depolama hesabınızdaki hem başarılı hem başarısız istekler için toorecord ayrıntıları sağlar. Bu günlükler, okuma, yazma ve silme işlemleri, tablolar, kuyruklar ve BLOB'lar yanı sıra hello nedeniyle başarısız istekler için karşı toosee ayrıntıları sağlar.

PowerShell kullanarak tooenable ve görünüm Storage ölçümleri verileri nasıl bakın toolearn [nasıl tooenable Storage ölçümleri PowerShell kullanarak](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

PowerShell kullanarak tooenable ve alma depolama günlük verileri nasıl bakın toolearn [nasıl tooenable depolama PowerShell kullanarak oturum](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) ve [depolama günlüğü günlük verilerinizi bulma](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Depolama ölçümleri ve tootroubleshoot depolama sorunları günlüğü depolama kullanma hakkında ayrıntılı bilgi için bkz: [izleme, Diagnosing ve sorun giderme Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Nasıl toomanage paylaşılan erişim imzası (SAS) ve depolanan erişim ilkesi
Paylaşılan erişim imzalar, Azure Storage kullanarak herhangi bir uygulama için hello güvenlik modelinin önemli bir parçasıdır. Bunlar, hello hesap anahtarı olmamalıdır sınırlı izinlere tooyour depolama hesabı tooclients sağlamak için kullanışlıdır. Varsayılan olarak, yalnızca hello sahibi hello depolama hesabının BLOB'lar, tablolar ve Kuyruklar o hesabı içinde erişebilir. Hizmet veya uygulama toomake bu kaynaklar kullanılabilir tooother istemciler erişim anahtarınızı paylaşmadan gerekiyorsa, üç seçeneğiniz vardır:

* Bir kapsayıcının izinleri toopermit anonim okuma erişimini toohello kapsayıcı ve bloblarını ayarlayın. Bu tablo veya sıralara izin verilmez.
* Kısıtlı erişim hakları toocontainers, BLOB, kuyruklar ve tablolar için belirli bir zaman aralığı veren paylaşılan erişim imzası kullanın.
* Depolanmış erişim ilkesi tooobtain ek bir paylaşılan erişim imzaları üzerinde denetim düzeyi bir kapsayıcıyı veya bloblarını için bir sıraya veya bir tablo için kullanın. Merhaba depolanmış erişim ilkesi toochange hello başlangıç saati, sona erme saati veya bir imza için izinler sağlar veya toorevoke, sonra yayımlandığı.

Paylaşılan erişim imzası iki forms biri olabilir:

* **Geçici SAS**: oluştururken bir geçici SAS hello başlangıç zamanı, bitiş saati ve hello SAS izinlerini tüm belirtilen SAS URI'sini hello üzerinde. Bu tür bir SAS oluşturulabilir bir kapsayıcı, blob, tablo veya kuyruğu ve iptal edilebilir olmayan.
* **Saklı erişim ilkesi ile SAS**: bir saklı erişim ilkesi kaynak kapsayıcı bir blob kapsayıcısını, tablo veya kuyruğu - tanımlanmış ve bir veya daha fazla paylaşılan erişim imzaları toomanage kısıtlamalarını kullanabilirsiniz. Bir SAS depolanmış erişim ilkesi ile ilişkilendirdiğinizde, hello SAS hello kısıtlamaları devralır - hello başlangıç saati, sona erme saati ve izinleri - depolanan hello erişim ilkesi için tanımlı. Bu tür bir SAS iptal edilebilir.

Daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları (SAS)](storage-dotnet-shared-access-signature-part-1.md) ve [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](storage-manage-access-to-resources.md).

Merhaba sonraki bölümlerde, öğreneceksiniz nasıl toocreate Azure tabloları için paylaşılan erişim imzası belirteci ve depolanan erişim ilkesi. Azure PowerShell benzer cmdlet'lerini kapsayıcıları, BLOB'ları ve kuyrukları de sağlar. Bu bölümdeki toorun hello komut karşıdan hello [Azure PowerShell sürüm 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) veya sonraki bir sürümü.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>Nasıl toocreate ilke tabanlı paylaşılan erişim imzası belirteci
Merhaba yeni AzureStorageTableStoredAccessPolicy cmdlet toocreate yeni bir saklı erişim ilkesi kullanın. Ardından, hello çağırın [yeni AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate bir Azure Storage tablo için yeni bir ilke tabanlı paylaşılan erişim imzası belirteci.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Nasıl toocreate geçici (istenmeden olmayan) bir paylaşılan erişim imzası belirteci
Kullanım hello [yeni AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate yeni bir geçici (istenmeden olmayan) paylaşılan erişim imzası belirteci için bir Azure depolama tablosu:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>Nasıl toocreate depolanmış erişim ilkesi
Merhaba yeni AzureStorageTableStoredAccessPolicy cmdlet toocreate yeni bir saklı erişim ilkesi için bir Azure Storage tabloyu kullanın:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>Nasıl tooupdate depolanmış erişim ilkesi
Merhaba kümesi AzureStorageTableStoredAccessPolicy cmdlet tooupdate varolan bir depolanmış erişim ilkesi için bir Azure Storage tabloyu kullanın:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>Nasıl toodelete depolanmış erişim ilkesi
Hello Kaldır AzureStorageTableStoredAccessPolicy cmdlet toodelete depolanmış erişim ilkesi, bir Azure Storage tablosunda kullanın:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Nasıl toouse Azure Storage ABD hükümeti ve Azure Çin için
Bir Azure ortamı Microsoft Azure, bağımsız bir dağıtımını olduğu gibi [US government Azure kamu](https://azure.microsoft.com/features/gov/), [genel Azure AzureCloud](https://portal.azure.com), ve [AzureChinaCloud Azure Çin'de 21Vianet tarafından işletilen](http://www.windowsazure.cn/). ABD hükümeti ve Azure Çin için yeni Azure ortamlarını dağıtabilirsiniz.

Azure Storage ile AzureChinaCloud toouse toocreate AzureChinaCloud ile ilişkili bir depolama bağlamı gerekir. Bu adımları tooget başlattığınız izleyin:

1. Merhaba çalıştırmak [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello kullanılabilir Azure ortamı:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Bir Azure Çin hesap tooWindows PowerShell ekleyin:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. AzureChinaCloud hesabınız için bir depolama bağlam oluşturun:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse Azure Storage ile [ABD Azure kamu](https://azure.microsoft.com/features/gov/), yeni bir ortam tanımlayın ve ardından yeni bir depolama bağlamı ile bu ortamı oluşturun:

1. Merhaba çalıştırmak [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello kullanılabilir Azure ortamı:

    ```powershell
    Get-AzureEnvironment
    ```

2. Bir Azure ABD devlet kurumları hesap tooWindows PowerShell ekleyin:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. AzureUSGovernment hesabınız için bir depolama bağlam oluşturun:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Daha fazla bilgi için bkz.

* [Microsoft Azure kamu Geliştirici Kılavuzu](../azure-government-developer-guide.md).
* [Bir uygulama Çin hizmette oluştururken farklar genel bakış](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Sonraki Adımlar
Bu kılavuzda, öğrendiğinize nasıl toomanage Azure PowerShell ile Azure depolama. Bazı ilgili makaleler ve bunlarla ilgili daha fazla bilgi edinmek için kaynaklar aşağıda verilmiştir.

* [Azure Depolama Belgeleri](https://azure.microsoft.com/documentation/services/storage/)
* [Azure Storage PowerShell cmdlet'leri](/powershell/module/azurerm.storage/#storage)
* [Windows PowerShell başvurusu](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
