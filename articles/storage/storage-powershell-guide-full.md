---
title: Azure PowerShell'i Azure Storage ile kullanma | Microsoft Docs
description: "Azure depolama için Azure PowerShell cmdlet'leri depolama hesaplarını oluşturmak ve yönetmek için nasıl kullanılacağını öğrenin; BLOB'lar, tablolar, kuyruklar ve dosyaları ile çalışma; Yapılandırma depolama analytics sorgu ve paylaşılan erişim imzaları oluşturma."
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
ms.openlocfilehash: 51e3e93ebedd31370857e61a00139294bcee9237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Azure Storage ile Azure PowerShell’i kullanma
## <a name="overview"></a>Genel Bakış
Azure PowerShell cmdlet'leri Azure Windows PowerShell üzerinden yönetmenizi sağlayan bir modüldür. Sistem yönetimi için özel olarak tasarlanan görev tabanlı bir komut satırı kabuğu ve betik dili olarak tanımlanır. PowerShell ile kolayca kontrol edebilir ve Azure Hizmetleri ve uygulamaları otomatikleştirmesini. Örneğin, aracılığıyla gerçekleştirebilirsiniz aynı görevleri gerçekleştirmek için cmdlet öğelerini kullanabilirsiniz [Azure portal](https://portal.azure.com).

Bu kılavuzda, biz nasıl kullanılacağını ele alacağız [Azure depolama cmdlet'leri](/powershell/module/azurerm.storage/#storage) çeşitli Azure Storage ile geliştirme ve yönetim görevlerini gerçekleştirmek için.

Bu kılavuz, kullanma konusunda deneyim sahibi olduğunuzu varsayar [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) ve [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Kılavuz bir sayıda Azure Storage ile PowerShell kullanımını göstermek için betik sağlar. Her komut dosyası çalıştırılmadan önce yapılandırmanıza göre komut dosyası değişkenlerini güncelleştirmeniz gerekir.

Bu kılavuzun ilk bölümünde Azure depolama ve PowerShell hızlı bir bakış sağlar. Ayrıntılı bilgi ve yönergeler için başlangıç [Azure Storage ile Azure PowerShell'i kullanma önkoşulları](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Azure Storage ve PowerShell 5 dakika içinde Başlarken
Bu bölümde 5 dakika içinde Azure Storage PowerShell aracılığıyla erişim gösterilmiştir.

**Yeni Azure:** Microsoft Azure aboneliği ve bu abonelikle ilişkili bir Microsoft hesabı alın. Azure satın alma seçenekleri hakkında daha fazla bilgi için bkz: [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/), [satın alma seçenekleri](https://azure.microsoft.com/pricing/purchase-options/), ve [üye teklifleri](https://azure.microsoft.com/pricing/member-offers/) (MSDN, Microsoft iş ortağı ağı ve, BizSpark üyeleri için ve diğer Microsoft programları).

Bkz: [Azure Active Directory'de (Azure AD) yönetici rolleri atama](https://msdn.microsoft.com/library/azure/hh531793.aspx) Azure abonelikleri hakkında daha fazla bilgi için.

**Microsoft Azure aboneliği ve hesabı oluşturduktan sonra:**

1. En son yükleyip [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Başlangıç Windows PowerShell Tümleşik komut dosyası ortamı (ISE): yerel bilgisayarınızda, Git **Başlat** menüsü. Tür **Yönetimsel Araçlar** ve çalıştırmak için tıklatın. İçinde **Yönetimsel Araçlar** penceresinde sağ **Windows PowerShell ISE**, tıklatın **yönetici olarak çalıştır**.
3. İçinde **Windows PowerShell ISE**, tıklatın **dosya** > **yeni** yeni bir komut dosyası oluşturmak için.
4. Şimdi, Azure depolama alanına erişmek için temel PowerShell komutları gösterir basit bir komut dosyası sunuyoruz. Komut dosyası ilk Azure ister Azure eklemek için hesap kimlik bilgilerini yerel PowerShell ortamına hesap. Ardından, betik varsayılan Azure aboneliği ve Azure'da yeni bir depolama hesabı oluşturun. Ardından, betik yeni bir kapsayıcı bu yeni depolama hesabı oluşturun ve bu kapsayıcıya varolan bir görüntü dosyası (blob) yükleyin. Bu kapsayıcıdaki tüm blob'lara komut dosyasını listeler sonra yerel bilgisayarınızda yeni bir hedef dizin oluşturun ve görüntü dosyasını indirin.
5. Aşağıdaki kod bölümünde açıklamalar arasında komut dosyasını seçin **#begin** ve **#end**. Panoya kopyalamak için CTRL + C tuşlarına basın.

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
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
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. İçinde **Windows PowerShell ISE**, komut dosyasını kopyalamak için CTRL + V tuşlarına basın. Tıklatın **dosya** > **kaydetmek**. İçinde **Kaydet** iletişim penceresinde, komut dosyasının "mystoragescript." gibi bir ad yazın **Kaydet** düğmesine tıklayın.
7. Şimdi, yapılandırma ayarlarınızı temel alan komut dosyası değişkenleri güncelleştirmeniz gerekir. Güncelleştirmeniz gerekir **$SubscriptionName** kendi aboneliğinizle değişken. Komut dosyasında belirtildiği gibi diğer değişkenleri tutun veya bunları istediğiniz gibi güncelleştirin.
   
   * **$SubscriptionName:** Bu değişken, kendi abonelik adı ile güncelleştirmeniz gerekir. Aboneliğinizi adını bulmak için aşağıdaki üç yoldan birini izleyin:
     
    a. İçinde **Windows PowerShell ISE**, tıklatın **dosya** > **yeni** yeni bir komut dosyası oluşturmak için. Yeni komut dosyası için aşağıdaki komutu kopyalayın ve tıklayın **hata ayıklama** > **çalıştırmak**. Aşağıdaki komut dosyası ilk Azure ister Azure eklemek için hesap kimlik bilgilerini hesap yerel PowerShell ortamına ve yerel PowerShell oturumuna bağlı olan tüm abonelikler göster. Bu öğreticiyi izleyerek sırasında kullanmak istediğiniz abonelik adını not alın:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. Bulun ve abonelik adınızı kopyalamak için [Azure portal](https://portal.azure.com), sol Hub menüsünde **abonelikleri**. Bu kılavuzdaki betikleri çalıştırılırken kullanmak istediğiniz abonelik adı kopyalayın.
     
     ![Azure portalına](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. Bulun ve abonelik adınızı kopyalamak için [Klasik Azure portalı](https://manage.windowsazure.com/), aşağı kaydırın ve tıklayın **ayarları** portalın sol tarafındaki. Tıklatın **abonelikleri** aboneliklerinizi listesini görmek için. Bu kılavuzda verilen komut dosyaları çalıştırırken kullanmak istediğiniz abonelik adı kopyalayın.
     
     ![Klasik Azure Portalı](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** komut dosyasında verilen ad kullanın veya depolama hesabınız için yeni bir ad girin. **Önemli:** depolama hesabı adının Azure'da benzersiz olması gerekir. Çok küçük olmalıdır!
   * **$Location:** verilen "Batı ABD" betik kullanın veya Doğu ABD, Kuzey Avrupa vb. gibi diğer Azure konumları seçin.
   * **$ContainerName:** komut dosyasında verilen ad kullanın veya, kapsayıcı için yeni bir ad girin.
   * **$ImageToUpload:** yerel bilgisayarınızda bir resim yolu gibi girin: "C:\Images\HelloWorld.png".
   * **$DestinationFolder:** gibi Azure Storage'dan indirilen dosyaları depolamak için bir yerel dizinin yolunu girin: "C:\DownloadImages".
8. "Mystoragescript.ps1" dosyasındaki komut dosyası değişkenleri güncelleştirdikten sonra tıklatın **dosya** > **kaydetmek**. Ardından **hata ayıklama** > **çalıştırmak** veya basın **F5** komut dosyasını çalıştırmak için.  

Betik çalıştıktan sonra indirilen görüntü dosyasını içeren bir yerel hedef klasör olmalıdır. Aşağıdaki ekran görüntüsünde bir örnek çıkış şunları gösterir:

![BLOB'ları indirme](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> "PowerShell ve Azure Storage ile 5 dakika içinde Başlarken" bölümünde Azure Storage ile Azure PowerShell'i kullanma hakkında hızlı bir giriş sağlanan. Ayrıntılı bilgi ve yönergeler için aşağıdaki bölümleri okuyun geçirmenizi öneririz.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Azure Storage ile Azure PowerShell'i kullanma önkoşulları
Bir Azure aboneliği ve yukarıda açıklandığı gibi bu kılavuzda verilen PowerShell cmdlet'lerini çalıştırmak için hesabı gerekir.

Azure PowerShell cmdlet'leri Azure Windows PowerShell üzerinden yönetmenizi sağlayan bir modüldür. Yükleme ve Azure PowerShell ayarlama hakkında daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview). İndirin ve yükleyin veya bu kılavuzu kullanmadan önce en son Azure PowerShell modülü yükseltme öneririz.

Standart Windows PowerShell konsolu veya Windows PowerShell Tümleşik komut dosyası ortamı (ISE) cmdlet'lerini çalıştırabilirsiniz. Örneğin, açmak için **Windows PowerShell ISE**, Başlat menüsüne gidin, Yönetimsel Araçlar yazın ve çalıştırmak için tıklatın. Yönetimsel Araçlar penceresinde, Windows PowerShell ISE sağ tıklatın, yönetici olarak çalıştır'ı tıklatın.

## <a name="how-to-manage-storage-accounts-in-azure"></a>Azure depolama hesapları yönetme

Depolama hesaplarını Azure PowerShell ile yönetme bir bakalım

### <a name="how-to-set-a-default-azure-subscription"></a>Varsayılan bir Azure aboneliği ayarlama
Azure PowerShell kullanarak Azure Storage yönetmek için istemci ortamınızı Azure ile Azure Active Directory kimlik doğrulaması veya sertifika tabanlı kimlik doğrulaması üzerinden kimlik doğrulaması gerekir. Ayrıntılı bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) Öğreticisi. Bu kılavuz, Azure Active Directory kimlik doğrulaması kullanır.

1. Windows PowerShell ISE'de Azure eklemek için aşağıdaki komutu yazın hesabı yerel PowerShell ortamına:

    ```powershell
    Add-AzureAccount
    ```

2. "Oturum içinde için Microsoft Azure" penceresinde e-posta adresi ve hesabınızla ilişkili parolayı yazın. Azure, kimlik bilgilerini doğrulayıp kaydeder ve pencereyi kapatır.

3. Ardından, yerel PowerShell ortamınızda Azure hesapları görüntüleyin ve hesabınızın listelendiğini doğrulamak için aşağıdaki komutu çalıştırın:
   
    ```powershell
    Get-AzureAccount
    ```
4. Ardından, yerel PowerShell oturumuna bağlı tüm abonelikleri görmek için aşağıdaki cmdlet'i çalıştırın ve aboneliğinizi listelenmiş olduğunu doğrulayın:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. Varsayılan bir Azure aboneliği için Select-AzureSubscription cmdlet'ini çalıştırın:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Get-AzureSubscription cmdlet'ini çalıştırarak varsayılan abonelik adını doğrulayın:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. Azure Storage için tüm kullanılabilir PowerShell cmdlet'leri görmek için çalıştırın:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a>Yeni bir Azure depolama hesabı oluşturma
Azure depolama kullanan bir depolama hesabı gerekir. Aboneliğinize bağlanmak için bilgisayarınızı yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz.

1. Tüm kullanılabilir veri merkezi konumlarını bulmak için Get-AzureLocation cmdlet'i çalıştırın:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Ardından, yeni bir depolama hesabı oluşturmak için New-AzureStorageAccount cmdlet'ini çalıştırın. Aşağıdaki örnekte "Batı ABD" veri merkezine yeni bir depolama hesabı oluşturur.
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> Depolama hesabınızın adının Azure içinde benzersiz olmalıdır ve küçük harf olması gerekir. Adlandırma kuralları ve sınırlamaları için bkz: [Azure Storage hesapları hakkında](storage-create-storage-account.md) ve [adlandırma ve başvuran kapsayıcıları, Blobları ve meta veri](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a>Varsayılan bir Azure depolama hesabı ayarlama
Aboneliğinizde birden çok depolama hesabı olabilir. Bunlardan birini seçin ve aynı PowerShell oturumunda tüm depolama komutlar için varsayılan depolama hesabı olarak ayarlayın. Bu depolama bağlamı açıkça belirtmeden Azure PowerShell depolama komutları çalıştırmanıza olanak sağlar.

1. Aboneliğiniz için bir varsayılan depolama hesabı ayarlamak için Set-AzureSubscription cmdlet'i çalıştırabilirsiniz.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Ardından, depolama hesabı varsayılan abonelik hesabınızla ilişkili olduğunu doğrulamak için Get-AzureSubscription cmdlet'ini çalıştırın. Bu komut, geçerli bir depolama hesabı dahil olmak üzere geçerli abonelikte abonelik özellikleri döndürür.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a>Bir Abonelikteki tüm Azure depolama hesapları listelemek nasıl
Her Azure aboneliğinin en fazla 100 depolama hesapları olabilir. Sınırları hakkında en güncel bilgiler için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).

Adı ve geçerli Abonelikteki depolama hesapları durumunu öğrenmek için aşağıdaki cmdlet'i çalıştırın:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a>Bir Azure depolama bağlamı oluşturma
Azure depolama bağlam, depolama kimlik bilgilerini kapsülleyen PowerShell'de bir nesnedir. Bir depolama bağlamı kullanırken, bir sonraki cmdlet'ini çalıştırarak depolama hesabı ve erişim anahtarını açıkça belirtmeden isteğiniz kimlik doğrulaması sağlar. Bir depolama bağlamı kullanarak depolama hesabı adı ve erişim anahtarı, paylaşılan erişim imzası (SAS) belirteci, bağlantı dizesi gibi birçok yolla oluşturabilirsiniz veya anonim. Daha fazla bilgi için bkz: [yeni AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Bir depolama bağlamı oluşturmak için aşağıdaki üç yoldan birini kullanın:

* Çalıştırma [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) Azure depolama hesabınız için birincil depolama erişim tuşunu bulmak için cmdlet. Ardından, çağrı [yeni AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) depolama bağlamı oluşturmak için cmdlet'i:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Bir Azure depolama kapsayıcısı için bir paylaşılan erişim imzası belirteç oluşturmak ve bir depolama bağlamı oluşturmak için kullanın:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Daha fazla bilgi için bkz: [yeni AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) ve [kullanarak paylaşılan erişim imzaları (SAS)](storage-dotnet-shared-access-signature-part-1.md).

* Bazı durumlarda, yeni bir depolama bağlamı oluşturduğunuzda, hizmet uç noktalarına belirtmek isteyebilirsiniz. Depolama hesabınız için bir özel etki alanı adı Blob hizmetine kayıtlı veya bir paylaşılan erişim imzası depolama kaynaklarına erişmek için kullanmak istediğiniz durumlarda bu gerekli olabilir. Hizmet uç noktalarına bağlantı dizesi olarak ayarlayın ve aşağıda gösterildiği gibi yeni bir depolama bağlamı oluşturmak için kullanın:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Bir depolama bağlantı dizesi yapılandırma hakkında daha fazla bilgi için bkz: [bağlantı dizelerini yapılandırma](storage-configure-connection-string.md).

Bilgisayarınızı ayarlayın ve abonelikleri ve Azure PowerShell kullanarak depolama hesaplarını yönetecek öğrendiniz göre Azure BLOB'ları yönetmek ve anlık görüntüleri blob öğrenmek için sonraki bölüme gidin.

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a>Nasıl alınacağını ve Azure depolama anahtarlarını yeniden oluştur
Bir Azure Storage hesabı iki hesabı anahtarları ile birlikte gelir. Anahtarlarınızı almak için aşağıdaki cmdlet'i kullanabilirsiniz.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Belirli bir anahtarı almak için aşağıdaki cmdlet'i kullanın. Birincil ve ikincil değerler geçerlidir.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Anahtarlarınızı yeniden oluşturmak istiyorsanız, aşağıdaki cmdlet'i kullanın. "Birincil" ve "İkincil" - KeyType için geçerli değerler:

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a>Azure BLOB'ları yönetme
Azure Blob Depolama, büyük miktarlarda herhangi bir yere HTTP veya HTTPS aracılığıyla erişilebilen metin veya ikili veriler gibi yapılandırılmamış verileri depolamak için bir hizmettir. Bu bölümde, zaten Azure Blob Depolama hizmetinin kavramlarını olduğunu varsayar. Ayrıntılı bilgi için bkz: [.NET kullanarak Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-to-create-a-container"></a>Bir kapsayıcı oluşturma
Azure depolama her blob bir kapsayıcıda olmalıdır. Yeni AzureStorageContainer cmdlet'ini kullanarak özel bir kapsayıcı oluşturabilirsiniz:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Anonim okuma erişimini üç düzeyi vardır: **kapalı**, **Blob**, ve **kapsayıcı**. Bloblar için anonim erişimi engellemek için izni parametre kümesini **devre dışı**. Varsayılan olarak yeni kapsayıcı özeldir ve yalnızca hesap sahibi tarafından erişilebilir. Anonim izin vermek için herkese okuma erişimi blob kaynaklarına ancak kapsayıcı meta verileri için veya kapsayıcıdaki blobları listesine izin parametre kümesine **Blob**. Kaynaklar, kapsayıcı meta verileri ve kapsayıcıdaki blobları listesi blob tam ortak okuma erişimi sağlamak üzere izin parametre kümesini **kapsayıcı**. Daha fazla bilgi için bkz: [kapsayıcılar ve bloblar için anonim okuma erişimini yönetme](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob karşıya yüklemek nasıl
Azure Blob Storage blok blobları ve sayfa bloblarını destekler. Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).

BLOB'ları bir kapsayıcıya karşıya yüklemek için kullanabileceğiniz [kümesi AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet'i. Varsayılan olarak, bu komutu bir blok blobuna yerel dosyaları karşıya yükleme. Blob türü belirtmek için - BlobType parametresini kullanabilirsiniz.

Aşağıdaki örnek çalıştıran [Get-Childıtem](http://technet.microsoft.com/library/hh849800.aspx) belirlenen klasördeki tüm dosyaları almak için cmdlet ve ardından bunları sonraki cmdlet'e ardışık düzen işleci kullanılarak geçirir. [Kümesi AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet, kapsayıcıya yerel dosyaları yükler:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a>Kapsayıcıdan BLOB indirmek nasıl
Aşağıdaki örnek, bir kapsayıcıdan BLOB indirmek gösterilmiştir. Örneğin, ilk Azure depolama hesabı adı ve birincil erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar. Ardından, örnek kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i. Ardından, örnek kullanır [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobları yerel hedef klasöre yüklemek için cmdlet'i.

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a>Bir depolama kapsayıcıdan BLOB kopyalama
BLOB storage hesapları ve bölgeler arasında zaman uyumsuz olarak kopyalayabilirsiniz. Aşağıdaki örnekte, iki farklı depolama hesaplarındaki başka bir bir depolama kapsayıcıdan BLOB kopyalama gösterilmiştir. Örnek ilk kaynak ve hedef depolama hesapları için değişkenleri ayarlar ve ardından her hesap için bir depolama bağlam oluşturur. Ardından, örnek BLOB'ları kaynak kapsayıcıdan hedef kullanarak kapsayıcı kopyalar [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet'i. Örnek kaynak ve hedef depolama hesapları ve kapsayıcıları zaten mevcut olduğunu varsayar.

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Bu örnekte bir zaman uyumsuz kopya gerçekleştirmediğini unutmayın. Çalıştırarak her kopya durumunu izleyebilirsiniz [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet'i.

### <a name="how-to-copy-blobs-from-a-secondary-location"></a>İkincil bir konumdan BLOB kopyalama
BLOB'ları, RA-GRS etkinleştirilmiş bir hesap ikincil konumdan kopyalayabilirsiniz.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a>Bir blob silme
Bir blobu silmek için önce bir blob başvurusu alın ve sonra Kaldır AzureStorageBlob cmdlet'i üzerinde çağırın. Aşağıdaki örnek, belirli bir kapsayıcıdaki tüm blob'lara siler. Örnek ilk değişkenleri bir depolama hesabı için ayarlar ve bir depolama bağlamı oluşturur. Ardından, örnek kullanarak bir blob başvurusu alır. [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalışan [Kaldır AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) BLOB'ları bir kapsayıcıda Azure depolama kaldırmak için cmdlet.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a>Azure blob anlık görüntülerini yönetme
Azure blob görüntüsünü oluşturmanıza olanak sağlar. Bir anlık görüntüsü, bir noktada geçen süre içinde bir blob, salt okunur bir sürümüdür. Bir anlık görüntü oluşturulduktan sonra okumak, kopyalanan, veya silinmiş, ancak değişiklik. Anlık görüntüler bir anda göründüğü gibi bir blob yedeklemek için bir yol sağlar. Daha fazla bilgi için bkz: [Blob anlık görüntüsünün oluşturulmasına](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-to-create-a-blob-snapshot"></a>Bir blob anlık görüntü oluşturma
Bir BLOB snaphot oluşturmak için öncelikle bir blob başvurusu alın ve ardından çağırın `ICloudBlob.CreateSnapshot` yöntemini. Aşağıdaki örnek ilk değişkenleri bir depolama hesabı için ayarlar ve bir depolama bağlamı oluşturur. Ardından, örnek kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalışan [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) bir anlık görüntü oluşturmak için yöntemi.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a>Nasıl bir blob'un anlık görüntüleri listelemek için
Bir blob için istediğiniz sayıda anlık görüntü oluşturabilirsiniz. Geçerli anlık izlemek için blob ile ilişkili anlık görüntüleri listeleyebilirsiniz. Aşağıdaki örnek, önceden tanımlanmış bir blob ve çağrıları kullanır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) bu blob anlık görüntüleri listelemek için cmdlet.  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a>Bir anlık görüntü bir BLOB kopyalama
Anlık görüntüyü geri yüklemek için bir blob görüntüsünü kopyalayabilirsiniz. Ayrıntılı bilgi ve kısıtlamaları için bkz: [Blob anlık görüntüsünün oluşturulmasına](http://msdn.microsoft.com/library/azure/hh488361.aspx). Aşağıdaki örnek ilk değişkenleri bir depolama hesabı için ayarlar ve bir depolama bağlamı oluşturur. Ardından, örnek kapsayıcı ve blob adı değişkenleri tanımlar. Örnek kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalışan [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) bir anlık görüntü oluşturmak için yöntemi. Ardından, örnek çalıştırır [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet'i için kaynak blob ICloudBlob nesnesi kullanılarak bir blob görüntüsünü kopyalayın. Örneği çalıştırmadan önce yapılandırmanıza göre değişkenlerini güncelleştirdiğinizden emin olun. Aşağıdaki örnekte kaynak ve hedef kapsayıcılarını ve kaynak blob zaten mevcut varsaydığını unutmayın.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Azure BLOB'ları yönetmek ve Azure PowerShell ile anlık görüntülerini blob öğrendiniz, tablolar, kuyruklar ve dosyaları yönetme konusunda bilgi almak için sonraki bölüme gidin.

## <a name="how-to-manage-azure-tables-and-table-entities"></a>Azure tabloları ve tablo varlıkları yönetme
Azure tablo depolama depolamak ve yapılandırılmış ve ilişkisel olmayan verilerin büyük kümelerini sorgulamak için kullanabileceğiniz bir nosql olmayan veri hizmetidir. Hizmet ana bileşenlerinin tabloları, varlıkları ve özellikler mevcuttur. Bir tablo, varlıkları koleksiyonudur. Bir varlık özellikler kümesidir. Her varlığın tüm ad-değer çiftleri en çok 252 özellik olabilir. Bu bölümde, zaten Azure tablo depolama hizmeti kavramlarını olduğunu varsayar. Ayrıntılı bilgi için bkz: [tablo hizmeti veri modelini anlama](http://msdn.microsoft.com/library/azure/dd179338.aspx) ve [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md).

Aşağıdaki alt bölümlerde Azure PowerShell kullanarak Azure Table depolama hizmetini yönetmek nasıl öğreneceksiniz. Kapsamdaki senaryolar dahil **oluşturma**, **silme**, ve **alma** **tabloları**, yanı **ekleme**, **sorgulama**, ve **tablo varlıkları silmek**.

### <a name="how-to-create-a-table"></a>Bir tablo oluşturma
Her tablo bir Azure depolama hesabında bulunmalıdır. Aşağıdaki örnek, Azure Storage'da bir tablo oluşturmak gösterilmiştir. Örneğin, ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar. Ardından, kullanan [yeni AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) Azure Storage'da bir tablo oluşturmak için cmdlet'i.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a>Tablo alma
Sorgulamak ve bir depolama hesabı bir ya da tüm tablolarda alın. Aşağıdaki örnekte verilen tablo kullanarak almayı gösterir [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Get-AzureStorageTable cmdlet parametre olmadan çağırırsanız, tüm depolama tablolar için bir depolama hesabı alır.

### <a name="how-to-delete-a-table"></a>Bir tablo silme
Kullanarak bir depolama hesabından bir tablo silebilirsiniz [Kaldır AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet'i.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a>Tablo varlıkları yönetme
Şu anda Azure PowerShell tablo varlıkları doğrudan yönetmek için cmdlet'leri sağlamaz. Tablo varlıklar üzerinde işlem gerçekleştirmek için verilen sınıfları kullanabilirsiniz [.NET için Azure Storage istemci Kitaplığı](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-to-add-table-entities"></a>Tablo varlıkları ekleme
Tabloya bir varlık eklemek için önce varlık özelliklerinizi tanımlayan bir nesne oluşturun. Bir varlık 3 sistem özelliği de dahil olmak üzere en fazla 255 özelliklere sahip olabilir: **PartitionKey**, **RowKey**, ve **zaman damgası**. Ekleme ve değerlerini güncelleştirme sorumlu **PartitionKey** ve **RowKey**. Sunucu değeri yöneten **zaman damgası**, hangi değiştirilemez. Birlikte **PartitionKey** ve **RowKey** tablo içindeki her varlık benzersiz şekilde tanımlar.

* **PartitionKey**: Varlık depolanan bölüm belirler.
* **RowKey**: varlığın bölüm içinde benzersiz şekilde tanımlar.

Bir varlık için en çok 252 özel özellikler tanımlayabilir. Daha fazla bilgi için bkz: [tablo hizmeti veri modelini anlama](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Aşağıdaki örnek, bir tabloya varlıkları eklemek gösterilmiştir. Örneğin, çalışan tablosunu alın ve birkaç varlıklar içine ekleyin gösterilmektedir. İlk olarak, Azure depolama hesabı adı ve erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar. Ardından, verilen tablo kullanarak alır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i. Tablo mevcut değilse [yeni AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet Azure Storage'da bir tablo oluşturmak için kullanılır. Ardından, örnek özel bir işlev her varlığın bölüm ve satır anahtarını belirterek tabloya varlıkları eklemek için Add-varlık tanımlar. Add-varlık işlev çağrılarını [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet'ini [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) bir varlık nesnesini oluşturmak için sınıfı. Daha sonra örnek çağırır [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) bir tabloya eklemek için bu varlık nesnesi üzerinde yöntemi.

```powershell
#Function Add-Entity: Adds an employee entity to a table.
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

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a>Tablo varlıkları sorgulama
Bir tabloyu sorgulamak için kullanın [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) sınıfı. Aşağıdaki örnekte nasıl verilen komut dosyası zaten çalıştırdıysanız varsayar bu kılavuzun varlıkların bölüm eklemek için. Örneğin, ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama bağlamı kullanarak depolama bağlantı kurar. Ardından, daha önce oluşturulan "Çalışanlar" tablosunu kullanarak almaya çalışır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i. Çağırma [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet Microsoft.WindowsAzure.Storage.Table.TableQuery sınıf üzerinde yeni bir sorgu nesnesi oluşturur. Örnek 1 dize filtresi belirtildiği gibi değeri olan 'ID' sütuna sahip varlıklar arar. Ayrıntılı bilgi için bkz: [sorgulama tabloları ve varlıkları](http://msdn.microsoft.com/library/azure/dd894031.aspx). Bu sorgu çalıştırdığınızda, filtre ölçütüyle eşleşen tüm varlıkları döndürür.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a>Tablo varlıkları silme
Bir varlığın bölüm ve satır anahtarını kullanarak silebilirsiniz. Aşağıdaki örnekte nasıl verilen komut dosyası zaten çalıştırdıysanız varsayar bu kılavuzun varlıkların bölüm eklemek için. Örneğin, ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama bağlamı kullanarak depolama bağlantı kurar. Ardından, daha önce oluşturulan "Çalışanlar" tablosunu kullanarak almaya çalışır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i. Tablo varsa, örnek çağırır [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) bir varlık alma yöntemi temel üzerinde bölüm ve satır anahtarı değerleri. Daha sonra varlığa geçirin [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) silmek için yöntem.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a>Azure kuyrukları ve iletileri kuyruğa yönetme
Azure Kuyruk depolama, HTTP veya HTTPS kullanan kimlik doğrulaması yapılmış çağrılar aracılığıyla dünyanın her yerinden erişilebilen çok sayıda iletinin depolanması için bir hizmettir. Bu bölümde, zaten Azure kuyruk depolama hizmeti kavramlarını olduğunu varsayar. Ayrıntılı bilgi için bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](storage-dotnet-how-to-use-queues.md).

Bu bölümde Azure PowerShell kullanarak Azure kuyruk depolama hizmetini yönetmek nasıl yapacağınızı gösterir. Kapsamdaki senaryolar dahil **ekleme** ve **silme** kuyruk iletileri yanı **oluşturma**, **silme**ve **sıraları alma**.

### <a name="how-to-create-a-queue"></a>Bir sıra oluşturma
Aşağıdaki örnek ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar. Ardından, çağıran [yeni AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) 'queuename' adında bir kuyruk oluşturmak için cmdlet'i.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Azure kuyruk hizmeti için adlandırma kuralları hakkında bilgi için bkz: [adlandırma kuyrukları ve meta verileri](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-to-retrieve-a-queue"></a>Bir Sıraya alma
Sorgulama ve belirli bir sıraya veya bir depolama hesabındaki tüm kuyrukların listesini alın. Aşağıdaki örnek, belirtilen sırada kullanarak almak gösterilmiştir [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet'i.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Çağırırsanız [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet parametre olmadan tüm kuyrukların listesini alır.

### <a name="how-to-delete-a-queue"></a>Bir kuyruk silme
Bir kuyruk ve içerdiği tüm iletileri silmek için Remove-AzureStorageQueue cmdlet'ini çağırın. Aşağıdaki örnek, Remove-AzureStorageQueue cmdlet'i kullanılarak belirtilen bir kuyruk silme gösterilmektedir.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a>Kuyruğa bir ileti ekleme
Varolan bir sıraya bir ileti eklemek için önce yeni bir örneğini oluşturun [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) sınıfı. Ardından [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) yöntemini çağırın. Bir CloudQueueMessage bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi oluşturulabilir.

Aşağıdaki örnek, bir sıraya ileti eklemek gösterilmiştir. Örneğin, ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar. Ardından, belirtilen sırada kullanarak alır [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet'i. Sıranın varsa [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet'i bir örneğini oluşturmak için kullanılan [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) sınıfı. Daha sonra örnek çağırır [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) bir sıraya eklemek için bu ileti nesnede yöntemi. Bir sırayı alır ve 'MessageInfo' iletisi ekler kod şöyledir:

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a>Sonraki iletiyi sıradan çıkarmak nasıl
Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır. Çağırdığınızda [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) bir kuyruktaki bir sonraki iletiyi elde yöntemi. **GetMessage**’dan dönen bir ileti bu kuyruktaki kod okuyan iletilere karşı görünmez olur. İletiyi kuyruktan kaldırmayı tamamlamak için de çağırmanız gerekir [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) yöntemi. Bir iletinin iki adımlı kaldırılma süreci, donanım veya yazılım arızasından dolayı kodunuzun bir iletiyi işleyememesi durumunda kodunuzun başka bir örneğinin aynı iletiyi alıp yeniden denemesini sağlar. Kodunuz ileti işlendikten hemen sonra **DeleteMessage**’ı çağırır.

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a>Azure dosya paylaşımlarının ve dosyaların yönetme
Azure File storage standart SMB protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar. Microsoft Azure virtual machines ve cloud services bağlı paylaşımlar üzerinden uygulama bileşenleri arasında dosya verileri paylaşabilir ve şirket içi uygulamalar dosya depolama API'si veya Azure PowerShell üzerinden dosya verilerine erişebilir.

Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](storage-dotnet-how-to-use-files.md) ve [dosya hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-to-set-and-query-storage-analytics"></a>Nasıl ayarlanacağı ve sorgu depolama analizi
Kullanabileceğiniz [Azure depolama çözümlemeleri](storage-analytics.md) Azure depolama hesaplarınız için ölçümleri toplamak ve verileri depolama hesabınıza gönderilen istekleri hakkında günlüğe kaydetmek için. Depolama ölçümleri, bir depolama hesabı ve tanılamak ve depolama hesabınız ile ilgili sorunları gidermek için depolama oturum durumunu izlemek için kullanabilirsiniz. Azure Portalı'nı veya Windows PowerShell veya program aracılığıyla depolama istemci kitaplığı kullanarak izleme yapılandırabilirsiniz. Depolama günlük sunucu tarafı olur ve depolama hesabınızdaki hem başarılı hem başarısız istekler için kayıt ayrıntıları sağlar. Bu günlükler, okuma, yazma ve silme işlemleri tablolarınızı, kuyruklar ve BLOB'lar yanı sıra nedeniyle başarısız istekler için karşı ayrıntılarını görmek etkinleştirin.

Etkinleştirmek ve PowerShell kullanarak depolama ölçüm verilerini görüntüleme hakkında bilgi almak için bkz: [PowerShell kullanarak depolama ölçümlerini etkinleştirme](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

Etkinleştirmek ve PowerShell kullanarak depolama günlüğü verilerini alma hakkında bilgi almak için bkz: [PowerShell kullanarak depolama günlüğü etkinleştirme](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) ve [depolama günlüğü günlük verilerinizi bulma](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Depolama sorunları gidermek için depolama ölçümleri ve depolama oturum kullanma hakkında ayrıntılı bilgi için bkz: [izleme, Diagnosing ve sorun giderme Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a>Paylaşılan erişim imzası (SAS) ve depolanan erişim ilkesi yönetme
Paylaşılan erişim imzalar, Azure Storage kullanarak herhangi bir uygulama için güvenlik modelinin önemli bir parçasıdır. Bunlar, depolama hesabınıza sınırlı izinlere hesap anahtarı olmamalıdır istemcilere sağlamak için kullanışlıdır. Varsayılan olarak, yalnızca depolama hesabı sahibi BLOB'lar, tablolar ve Kuyruklar o hesabı içinde erişebilir. Hizmet veya uygulama bu kaynakları diğer istemciler için kullanılabilir erişim anahtarınızı paylaşmadan olması gerekiyorsa, üç seçeneğiniz vardır:

* Kapsayıcı ve bloblarını anonim okuma erişimine izin vermek üzere bir kapsayıcının izinlerini ayarlayın. Bu tablo veya sıralara izin verilmez.
* Verir kapsayıcıları, blobları, kuyruklar ve tablolar için erişim haklarını belirli bir zaman aralığı için sınırlı bir paylaşılan erişim imzası kullanın.
* Ek bir paylaşılan erişim imzaları bir kapsayıcıyı veya bloblarını için bir kuyruk için veya bir tablo üzerinde denetim düzeyini elde etmek için bir saklı erişim ilkesini kullanın. Bundan sonra iptal etmek için verilen veya depolanmış erişim ilkesi başlangıç saati, sona erme saati veya imza için izinleri değiştirmek sağlar.

Paylaşılan erişim imzası iki forms biri olabilir:

* **Geçici SAS**: geçici bir SAS, başlangıç zamanı, bitiş zamanı, oluşturduğunuzda ve SAS izinlerini tüm belirtilen SAS URİ'si üzerinde. Bu tür bir SAS oluşturulabilir bir kapsayıcı, blob, tablo veya kuyruğu ve iptal edilebilir olmayan.
* **Saklı erişim ilkesi ile SAS**: bir saklı erişim ilkesi kaynak kapsayıcı bir blob kapsayıcısını, tablo veya kuyruğu - tanımlanmış ve bir veya daha fazla paylaşılan erişim imzaları kısıtlamalarını yönetmek için kullanın. Bir SAS depolanmış erişim ilkesi ile ilişkilendirdiğinizde, SAS kısıtlamaları - başlangıç saati, sona erme saati ve saklı erişim ilkesi için tanımlanan izinleri - devralır. Bu tür bir SAS iptal edilebilir.

Daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları (SAS)](storage-dotnet-shared-access-signature-part-1.md) ve [kapsayıcılar ve bloblar için anonim okuma erişimini yönetme](storage-manage-access-to-resources.md).

Sonraki bölümlerde, Azure tablolar için paylaşılan erişim imzası belirteci ve saklı erişim ilkesinin nasıl oluşturulacağını öğreneceksiniz. Azure PowerShell benzer cmdlet'lerini kapsayıcıları, BLOB'ları ve kuyrukları de sağlar. Bu bölümde komut dosyalarını çalıştırmak için karşıdan [Azure PowerShell sürüm 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) veya sonraki bir sürümü.

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a>Bir ilke tabanlı paylaşılan erişim imzası belirteci oluşturma
Yeni bir saklı erişim ilkesi oluşturmak için New-AzureStorageTableStoredAccessPolicy cmdlet'ini kullanın. Ardından, çağıran [yeni AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) bir Azure Storage tablo için yeni bir ilke tabanlı paylaşılan erişim imzası belirteci oluşturmak için cmdlet'i.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Geçici (istenmeden olmayan) bir paylaşılan erişim imzası belirteci oluşturma
Kullanım [yeni AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet yeni bir geçici (istenmeden olmayan) paylaşılan erişim imzası belirteci için bir Azure depolama tablosu oluşturmak için:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a>Saklı erişim ilkesi oluşturma
Bir Azure depolama tablosu için yeni bir saklı erişim ilkesi oluşturmak için New-AzureStorageTableStoredAccessPolicy cmdlet'i kullanın:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a>Bir saklı erişim ilkesi güncelleştirme
Bir Azure depolama tablosu için varolan bir depolanmış erişim ilkesi güncelleştirmek için Set-AzureStorageTableStoredAccessPolicy cmdlet'ini kullanın:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a>Bir saklı erişim ilkesi silme
Bir Azure Storage tablosunda depolanan erişim ilkesini silmek için Remove-AzureStorageTableStoredAccessPolicy cmdlet'ini kullanın:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a>ABD hükümeti ve Azure Çin için Azure Storage kullanma
Bir Azure ortamı Microsoft Azure, bağımsız bir dağıtımını olduğu gibi [US government Azure kamu](https://azure.microsoft.com/features/gov/), [genel Azure AzureCloud](https://portal.azure.com), ve [AzureChinaCloud Azure Çin'de 21Vianet tarafından işletilen](http://www.windowsazure.cn/). ABD hükümeti ve Azure Çin için yeni Azure ortamlarını dağıtabilirsiniz.

Azure Storage ile AzureChinaCloud kullanmak için AzureChinaCloud ile ilişkili bir depolama bağlam oluşturmanız gerekir. Başlamanıza yardımcı olmak için aşağıdaki adımları izleyin:

1. Çalıştırma [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) kullanılabilir Azure ortamları görmek için cmdlet:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Windows PowerShell için Azure Çin Hesap Ekle:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. AzureChinaCloud hesabınız için bir depolama bağlam oluşturun:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

Azure Storage ile kullanmak için [ABD Azure kamu](https://azure.microsoft.com/features/gov/), yeni bir ortam tanımlayın ve ardından yeni bir depolama bağlamı ile bu ortamı oluşturun:

1. Çalıştırma [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) kullanılabilir Azure ortamları görmek için cmdlet:

    ```powershell
    Get-AzureEnvironment
    ```

2. Windows PowerShell için Azure ABD devlet kurumları Hesap Ekle:
   
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
Bu kılavuzda, Azure Storage Azure PowerShell ile yönetme öğrendiniz. Bazı ilgili makaleler ve bunlarla ilgili daha fazla bilgi edinmek için kaynaklar aşağıda verilmiştir.

* [Azure Depolama Belgeleri](https://azure.microsoft.com/documentation/services/storage/)
* [Azure Storage PowerShell cmdlet'leri](/powershell/module/azurerm.storage/#storage)
* [Windows PowerShell başvurusu](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
