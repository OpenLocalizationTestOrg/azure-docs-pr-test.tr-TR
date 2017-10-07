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
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="ecc21-103">Azure Storage ile Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="ecc21-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="ecc21-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ecc21-104">Overview</span></span>
<span data-ttu-id="ecc21-105">Azure PowerShell cmdlet'leri toomanage Windows PowerShell üzerinden Azure sağlayan bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="ecc21-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="ecc21-106">Sistem yönetimi için özel olarak tasarlanan görev tabanlı bir komut satırı kabuğu ve betik dili olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="ecc21-107">PowerShell ile kolayca kontrol edebilir ve hello Azure Hizmetleri ve uygulamaları otomatikleştirmesini.</span><span class="sxs-lookup"><span data-stu-id="ecc21-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="ecc21-108">Örneğin, aynı görevleri hello gerçekleştirebilirsiniz hello cmdlet'leri tooperform hello kullanabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ecc21-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="ecc21-109">Bu kılavuzda, biz ele alacağız nasıl toouse hello [Azure depolama cmdlet'leri](/powershell/module/azurerm.storage/#storage) tooperform çeşitli Azure Storage ile geliştirme ve yönetim görevleri.</span><span class="sxs-lookup"><span data-stu-id="ecc21-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="ecc21-110">Bu kılavuz, kullanma konusunda deneyim sahibi olduğunuzu varsayar [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) ve [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="ecc21-111">Merhaba Kılavuzu bir dizi betiği toodemonstrate hello Azure Storage ile PowerShell kullanımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="ecc21-112">Her komut dosyası çalıştırılmadan önce yapılandırmanıza göre hello betik değişkenlerini güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="ecc21-113">Bu kılavuzdaki Hello ilk bölüm, PowerShell ve Azure Storage hızlı bir bakışta sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="ecc21-114">Ayrıntılı bilgi ve yönergeler için hello Başlat [Azure Storage ile Azure PowerShell'i kullanma önkoşulları](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="ecc21-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="ecc21-115">Azure Storage ve PowerShell 5 dakika içinde Başlarken</span><span class="sxs-lookup"><span data-stu-id="ecc21-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="ecc21-116">Bu bölümde, nasıl gösterilir tooaccess Azure Storage PowerShell aracılığıyla 5 dakika.</span><span class="sxs-lookup"><span data-stu-id="ecc21-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="ecc21-117">**Yeni tooAzure:** Microsoft Azure aboneliği ve bu abonelikle ilişkili bir Microsoft hesabı alın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="ecc21-118">Azure satın alma seçenekleri hakkında daha fazla bilgi için bkz: [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/), [satın alma seçenekleri](https://azure.microsoft.com/pricing/purchase-options/), ve [üye teklifleri](https://azure.microsoft.com/pricing/member-offers/) (MSDN, Microsoft iş ortağı ağı ve, BizSpark üyeleri için ve diğer Microsoft programları).</span><span class="sxs-lookup"><span data-stu-id="ecc21-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="ecc21-119">Bkz: [Azure Active Directory'de (Azure AD) yönetici rolleri atama](https://msdn.microsoft.com/library/azure/hh531793.aspx) Azure abonelikleri hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ecc21-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="ecc21-120">**Microsoft Azure aboneliği ve hesabı oluşturduktan sonra:**</span><span class="sxs-lookup"><span data-stu-id="ecc21-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="ecc21-121">Merhaba son yükleyip [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="ecc21-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="ecc21-122">Başlangıç Windows PowerShell Tümleşik komut dosyası ortamı (ISE): yerel bilgisayarınıza toohello Git **Başlat** menüsü.</span><span class="sxs-lookup"><span data-stu-id="ecc21-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="ecc21-123">Tür **Yönetimsel Araçlar** ve toorun'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="ecc21-124">Merhaba, **Yönetimsel Araçlar** penceresinde, sağ **Windows PowerShell ISE**, tıklatın **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="ecc21-125">İçinde **Windows PowerShell ISE**, tıklatın **dosya** > **yeni** toocreate yeni bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="ecc21-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="ecc21-126">Şimdi, biz temel PowerShell komutları tooaccess Azure Storage gösteren basit bir komut dosyası size.</span><span class="sxs-lookup"><span data-stu-id="ecc21-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="ecc21-127">Merhaba komut dosyası, ilk Azure hesabı toohello yerel PowerShell ortamınızın Azure hesabı kimlik bilgileri tooadd isteyecektir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="ecc21-128">Ardından, hello betik hello varsayılan Azure aboneliği ve Azure'da yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecc21-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="ecc21-129">Ardından, hello betik bu yeni depolama hesabı yeni bir kapsayıcı oluşturur ve var olan bir görüntü dosyası (blob) toothat kapsayıcıyı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ecc21-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="ecc21-130">Bu kapsayıcıdaki tüm blob'lara Hello komut dosyasını listeler sonra yerel bilgisayarınızda yeni bir hedef dizin oluşturun ve hello görüntü dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="ecc21-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="ecc21-131">Kod bölümünde aşağıdaki hello hello açıklamalar arasında hello komut dosyalarını seçin **#begin** ve **#end**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="ecc21-132">CTRL + C toocopy tuşuna basın, toohello Pano.</span><span class="sxs-lookup"><span data-stu-id="ecc21-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

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

6. <span data-ttu-id="ecc21-133">İçinde **Windows PowerShell ISE**, CTRL + V toocopy hello betik tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="ecc21-134">Tıklatın **dosya** > **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-134">Click **File** > **Save**.</span></span> <span data-ttu-id="ecc21-135">Merhaba, **Kaydet** iletişim penceresinde, "mystoragescript." gibi hello komut dosyası türü hello adı</span><span class="sxs-lookup"><span data-stu-id="ecc21-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="ecc21-136">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-136">Click **Save**.</span></span>
7. <span data-ttu-id="ecc21-137">Şimdi, yapılandırma ayarlarınızı temel alan tooupdate hello komut dosyası değişkenleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="ecc21-138">Merhaba güncelleştirmelisiniz **$SubscriptionName** kendi aboneliğinizle değişken.</span><span class="sxs-lookup"><span data-stu-id="ecc21-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="ecc21-139">Merhaba hello betik belirtildiği gibi diğer değişkenleri tutun veya bunları istediğiniz gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ecc21-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="ecc21-140">**$SubscriptionName:** Bu değişken, kendi abonelik adı ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="ecc21-141">Üç yolu toolocate hello aboneliğinizin adından hello birini izleyin:</span><span class="sxs-lookup"><span data-stu-id="ecc21-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="ecc21-142">a.</span><span class="sxs-lookup"><span data-stu-id="ecc21-142">a.</span></span> <span data-ttu-id="ecc21-143">İçinde **Windows PowerShell ISE**, tıklatın **dosya** > **yeni** toocreate yeni bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="ecc21-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="ecc21-144">Kopya hello aşağıdakiler toohello yeni komut dosyası komut dosyası ve tıklatın **hata ayıklama** > **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="ecc21-145">Merhaba aşağıdaki komut dosyası ilk Azure hesabı kimlik bilgileri tooadd Azure hesabı toohello yerel PowerShell ortamınızın isteyin ve bağlı toohello yerel PowerShell oturumu tüm hello aboneliklerin göster.</span><span class="sxs-lookup"><span data-stu-id="ecc21-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="ecc21-146">Bu öğreticiyi izleyerek sırasında toouse istediğiniz hello hello abonelik adını not alın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="ecc21-147">b.</span><span class="sxs-lookup"><span data-stu-id="ecc21-147">b.</span></span> <span data-ttu-id="ecc21-148">aboneliğinizi toolocate ve kopyalama hello ad [Azure portal](https://portal.azure.com), buna sol hello Hub menüsünde Merhaba, tıklatın **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="ecc21-149">Bu kılavuzda hello betikleri çalıştırılırken toouse istediğiniz abonelik Hello adı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Azure portalına](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="ecc21-151">c.</span><span class="sxs-lookup"><span data-stu-id="ecc21-151">c.</span></span> <span data-ttu-id="ecc21-152">aboneliğinizi toolocate ve kopyalama hello ad [Klasik Azure portalı](https://manage.windowsazure.com/), aşağı kaydırın ve tıklayın **ayarları** yan hello portalının sol hello üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ecc21-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="ecc21-153">Tıklatın **abonelikleri** toosee aboneliklerinizi listesi.</span><span class="sxs-lookup"><span data-stu-id="ecc21-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="ecc21-154">Bu kılavuzda verilen hello betikleri çalıştırılırken toouse istediğiniz abonelik Hello adı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![Klasik Azure Portalı](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="ecc21-156">**$StorageAccountName:** hello komut dosyasında adı verilen hello kullanın veya depolama hesabınız için yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="ecc21-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="ecc21-157">**Önemli:** hello depolama hesabının adını hello Azure içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="ecc21-158">Çok küçük olmalıdır!</span><span class="sxs-lookup"><span data-stu-id="ecc21-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="ecc21-159">**$Location:** "Batı ABD" verilen hello hello komut dosyasında kullanın veya Doğu ABD, Kuzey Avrupa vb. gibi diğer Azure konumları seçin.</span><span class="sxs-lookup"><span data-stu-id="ecc21-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="ecc21-160">**$ContainerName:** hello komut dosyasında adı verilen hello kullanın veya, kapsayıcı için yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="ecc21-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="ecc21-161">**$ImageToUpload:** yolu tooa resim, yerel bilgisayarınızda gibi girin: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="ecc21-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="ecc21-162">**$DestinationFolder:** bir yolu tooa yerel dizin toostore dosyaları Azure Storage'dan gibi indirilen girin: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="ecc21-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="ecc21-163">Merhaba "mystoragescript.ps1" dosyasındaki Hello komut dosyası değişkenleri güncelleştirdikten sonra tıklatın **dosya** > **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="ecc21-164">Ardından **hata ayıklama** > **çalıştırmak** veya basın **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="ecc21-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="ecc21-165">Merhaba betik çalıştıktan sonra indirilen hello görüntü dosyasını içeren bir yerel hedef klasör olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="ecc21-166">Merhaba ekran aşağıdaki örnek çıkış şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="ecc21-166">hello following screenshot shows an example output:</span></span>

![BLOB'ları indirme](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="ecc21-168">Merhaba "5 dakika içinde Azure Storage ve PowerShell Başlarken" bölümünde bir giriş nasıl sağlanan toouse Azure PowerShell'i Azure Storage ile.</span><span class="sxs-lookup"><span data-stu-id="ecc21-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="ecc21-169">Ayrıntılı bilgi ve yönergeler için aşağıdaki bölümlerde tooread hello öneririz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="ecc21-170">Azure Storage ile Azure PowerShell'i kullanma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="ecc21-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="ecc21-171">Bu kılavuzda verilen bir Azure aboneliği ve hesabı toorun hello PowerShell cmdlet'leri, yukarıda açıklandığı gibi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="ecc21-172">Azure PowerShell cmdlet'leri toomanage Windows PowerShell üzerinden Azure sağlayan bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="ecc21-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="ecc21-173">Yükleme ve Azure PowerShell ayarlama hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ecc21-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="ecc21-174">İndirin ve yükleyin veya bu kılavuzu kullanmadan önce toohello en son Azure PowerShell modülü yükseltme öneririz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="ecc21-175">Merhaba standart Windows PowerShell konsolu veya Windows PowerShell Tümleşik komut dosyası ortamı (ISE) hello hello cmdlet'lerini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="ecc21-176">Örneğin, tooopen **Windows PowerShell ISE**, toohello Başlat menüsüne gidin, Yönetimsel Araçlar yazın ve toorun'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="ecc21-177">Merhaba Yönetimsel Araçlar penceresinde, Windows PowerShell ISE sağ tıklatın, yönetici olarak çalıştır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="ecc21-178">Azure'da nasıl toomanage depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="ecc21-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="ecc21-179">Depolama hesaplarını Azure PowerShell ile yönetme bir bakalım</span><span class="sxs-lookup"><span data-stu-id="ecc21-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="ecc21-180">Nasıl tooset varsayılan bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="ecc21-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="ecc21-181">toomanage Azure PowerShell kullanarak Azure Storage istemci ortamınızı Azure ile Azure Active Directory kimlik doğrulaması veya sertifika tabanlı kimlik doğrulaması üzerinden tooauthenticate gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="ecc21-182">Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ecc21-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="ecc21-183">Bu kılavuz hello Azure Active Directory kimlik doğrulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="ecc21-184">Windows PowerShell ISE'de komutu tooadd aşağıdaki hello Azure hesabı toohello yerel PowerShell ortamınızın yazın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="ecc21-185">Merhaba "tooMicrosoft Azure oturum" penceresinde, hello e-posta adresini yazın ve hesabınızla ilişkili parola.</span><span class="sxs-lookup"><span data-stu-id="ecc21-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="ecc21-186">Azure kimliğini doğrular ve hello kimlik bilgileri kaydeder ve hello penceresini kapatır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="ecc21-187">Ardından, Azure yerel PowerShell ortamınızda hesapları ve hesabınızın listelendiğini doğrulayın komutu tooview hello aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="ecc21-188">Ardından, cmdlet tooview aşağıdaki hello bağlı toohello yerel PowerShell oturumu tüm hello aboneliklerin çalıştırın ve aboneliğinizi listelenmiş olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="ecc21-189">Varsayılan bir Azure aboneliği tooset Hello Select-AzureSubscription cmdlet'ini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="ecc21-190">Merhaba varsayılan abonelik Hello adı hello Get-AzureSubscription cmdlet'ini çalıştırarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="ecc21-191">toosee tüm hello kullanılabilir için PowerShell cmdlet'leri Azure Storage çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="ecc21-192">Nasıl toocreate yeni bir Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="ecc21-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="ecc21-193">toouse Azure depolama, depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="ecc21-194">Bilgisayar tooconnect tooyour aboneliğinizi yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="ecc21-195">Merhaba Get-AzureLocation cmdlet'i toofind tüm hello kullanılabilir veri merkezi konumlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="ecc21-196">Ardından, yeni bir depolama hesabı hello yeni AzureStorageAccount cmdlet toocreate çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="ecc21-197">Merhaba aşağıdaki örnek yeni bir depolama hesabı hello "Batı ABD" merkezinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecc21-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="ecc21-198">Depolama hesabınızın adını Hello Azure içinde benzersiz olmalıdır ve küçük harf olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="ecc21-199">Adlandırma kuralları ve sınırlamaları için bkz: [Azure Storage hesapları hakkında](../storage-create-storage-account.md) ve [adlandırma ve başvuran kapsayıcıları, Blobları ve meta veri](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="ecc21-200">Nasıl tooset varsayılan bir Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="ecc21-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="ecc21-201">Aboneliğinizde birden çok depolama hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="ecc21-202">Bunlardan birini seçin ve tüm depolama hello için hello varsayılan depolama hesabı hello aynı komutları olarak ayarlamak PowerShell oturumu.</span><span class="sxs-lookup"><span data-stu-id="ecc21-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="ecc21-203">Bu işlem, hello depolama bağlamı açıkça belirtmeden toorun hello Azure PowerShell depolama komutları sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="ecc21-204">aboneliğiniz için bir varsayılan depolama hesabı tooset hello Set-AzureSubscription cmdlet'i çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="ecc21-205">Ardından, hello depolama hesabı varsayılan abonelik hesabınızla ilişkilendirilmiş olduğunu hello Get-AzureSubscription cmdlet'i tooverify çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="ecc21-206">Bu komut, geçerli bir depolama hesabı dahil olmak üzere hello geçerli abonelikte hello abonelik özellikleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ecc21-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="ecc21-207">Nasıl toolist bir Abonelikteki tüm Azure depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="ecc21-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="ecc21-208">Her Azure aboneliği too100 depolama hesapları olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="ecc21-209">Merhaba en güncel sınırları hakkında bilgi için [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="ecc21-210">Cmdlet toofind hello adı ve hello hello geçerli Abonelikteki depolama hesapları durumunu izleyen hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="ecc21-211">Nasıl toocreate bir Azure depolama bağlamı</span><span class="sxs-lookup"><span data-stu-id="ecc21-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="ecc21-212">Azure depolama bağlam PowerShell tooencapsulate hello depolama kimlik bilgilerinde bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="ecc21-213">Herhangi bir sonraki cmdlet çalıştırırken bir depolama bağlamı kullanarak, tooauthenticate isteğiniz hello depolama hesabı ve erişim anahtarını açıkça belirtmeden sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="ecc21-214">Bir depolama bağlamı kullanarak depolama hesabı adı ve erişim anahtarı, paylaşılan erişim imzası (SAS) belirteci, bağlantı dizesi gibi birçok yolla oluşturabilirsiniz veya anonim.</span><span class="sxs-lookup"><span data-stu-id="ecc21-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="ecc21-215">Daha fazla bilgi için bkz: [yeni AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="ecc21-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="ecc21-216">Bir depolama bağlamı üç yolu toocreate aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="ecc21-217">Merhaba çalıştırmak [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind hello birincil depolama erişim tuşunu Azure depolama hesabınız için çıkışı.</span><span class="sxs-lookup"><span data-stu-id="ecc21-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="ecc21-218">Ardından, hello'ı çağırın [yeni AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate depolama bağlamı:</span><span class="sxs-lookup"><span data-stu-id="ecc21-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="ecc21-219">Bir Azure depolama kapsayıcısı için bir paylaşılan erişim imzası belirteç oluşturmak ve toocreate depolama bağlamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="ecc21-220">Daha fazla bilgi için bkz: [yeni AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) ve [kullanarak paylaşılan erişim imzaları (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="ecc21-221">Bazı durumlarda, yeni bir depolama bağlamı oluşturduğunuzda toospecify hello hizmet uç noktaları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="ecc21-222">Merhaba Blob hizmetine depolama hesabınız için bir özel etki alanı adı kayıtlı veya depolama kaynaklarına erişmek için bir paylaşılan erişim imzası toouse istediğiniz durumlarda bu gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="ecc21-223">Bağlantı dizesinde Hello hizmet uç noktaları ayarlayın ve aşağıda gösterildiği gibi toocreate yeni bir depolama bağlamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="ecc21-224">Hakkında daha fazla bilgi için tooconfigure bir depolama bağlantı dizesi bkz [bağlantı dizelerini yapılandırma](../storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="ecc21-225">Bilgisayarınızı ayarlayın ve öğrenilen göre nasıl toomanage abonelikleri ve storage hesaplarını Azure PowerShell kullanarak nasıl toomanage Azure BLOB toohello sonraki bölümde toolearn gidin ve anlık görüntülerini blob.</span><span class="sxs-lookup"><span data-stu-id="ecc21-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="ecc21-226">Nasıl tooretrieve ve yeniden Azure depolama anahtarları</span><span class="sxs-lookup"><span data-stu-id="ecc21-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="ecc21-227">Bir Azure Storage hesabı iki hesabı anahtarları ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="ecc21-228">Cmdlet tooretrieve aşağıdaki hello anahtarlarınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="ecc21-229">Aşağıdaki cmdlet'i tooretrieve belirli bir anahtarın hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="ecc21-230">Birincil ve ikincil değerler geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="ecc21-231">Tooregenerate isterseniz, anahtarlarınızı cmdlet'i aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="ecc21-232">"Birincil" ve "İkincil" - KeyType için geçerli değerler:</span><span class="sxs-lookup"><span data-stu-id="ecc21-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="ecc21-233">Nasıl toomanage Azure BLOB</span><span class="sxs-lookup"><span data-stu-id="ecc21-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="ecc21-234">Azure Blob Depolama büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış veriyi depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="ecc21-235">Bu bölümde, zaten hello Azure Blob Depolama hizmetinin kavramlarını olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="ecc21-236">Ayrıntılı bilgi için bkz: [.NET kullanarak Blob storage'ı kullanmaya başlama](../blobs/storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="ecc21-237">Nasıl toocreate bir kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="ecc21-237">How toocreate a container</span></span>
<span data-ttu-id="ecc21-238">Azure depolama her blob bir kapsayıcıda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="ecc21-239">Merhaba yeni AzureStorageContainer cmdlet'ini kullanarak özel bir kapsayıcı oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ecc21-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="ecc21-240">Anonim okuma erişimini üç düzeyi vardır: **kapalı**, **Blob**, ve **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="ecc21-241">tooprevent anonim erişim tooblobs, kümesi hello izni parametresi çok**devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="ecc21-242">Varsayılan olarak, hello yeni kapsayıcı özeldir ve yalnızca hello hesap sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="ecc21-243">tooallow anonim ortak okuma erişimine tooblob, ancak değil toocontainer meta veriler veya toohello listesi hello kapsayıcıdaki blobları, hello izni çok parametre**Blob**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="ecc21-244">tooallow tam ortak okuma tooblob kaynaklara erişmesine, kapsayıcı meta verileri ve hello kapsayıcıdaki blobları hello listesi, hello izni çok parametre**kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="ecc21-245">Daha fazla bilgi için bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-245">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="ecc21-246">Nasıl bir kapsayıcı halinde tooupload blob</span><span class="sxs-lookup"><span data-stu-id="ecc21-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="ecc21-247">Azure Blob Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="ecc21-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="ecc21-248">Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="ecc21-249">tooa kapsayıcıdaki blobları tooupload, kullanabileceğiniz hello [kümesi AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="ecc21-250">Varsayılan olarak, bu komut hello yerel dosyaları tooa blok blobu yükler.</span><span class="sxs-lookup"><span data-stu-id="ecc21-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="ecc21-251">toospecify hello türü hello blob için hello - BlobType parametresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="ecc21-252">Merhaba aşağıdaki örnekte çalışan hello [Get-Childıtem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget tüm hello hello belirtilen klasördeki dosyaları ve daha sonra bunları toohello sonraki cmdlet hello ardışık düzen işleci kullanılarak geçirir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="ecc21-253">Merhaba [kümesi AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet hello yerel dosyaları tooyour kapsayıcı yükler:</span><span class="sxs-lookup"><span data-stu-id="ecc21-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="ecc21-254">Nasıl toodownload kapsayıcıdan BLOB</span><span class="sxs-lookup"><span data-stu-id="ecc21-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="ecc21-255">Aşağıdaki örnek hello nasıl toodownload kapsayıcıdan BLOB'ların gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="ecc21-256">Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve birincil erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ecc21-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="ecc21-257">Ardından, hello örnek hello kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="ecc21-258">Ardından, hello örnek hello kullanır [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload BLOB'lar hello yerel hedef klasöre.</span><span class="sxs-lookup"><span data-stu-id="ecc21-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

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

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="ecc21-259">Bir depolama kapsayıcısı tooanother toocopy nasıl BLOB</span><span class="sxs-lookup"><span data-stu-id="ecc21-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="ecc21-260">BLOB storage hesapları ve bölgeler arasında zaman uyumsuz olarak kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="ecc21-261">Merhaba aşağıdaki örnekte nasıl bir depolama kapsayıcısı tooanother iki farklı depolama hesaplarındaki gelen toocopy BLOB gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="ecc21-262">Merhaba örneği ilk kaynak ve hedef depolama hesapları için değişkenleri ayarlar ve ardından her hesap için bir depolama bağlam oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecc21-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="ecc21-263">Ardından, hello örnek hello kullanarak hello kaynak kapsayıcı toohello hedef kapsayıcıdan BLOB kopyalar [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="ecc21-264">Merhaba örnek hello kaynak ve hedef depolama hesapları ve kapsayıcıları zaten mevcut olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

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

<span data-ttu-id="ecc21-265">Bu örnekte bir zaman uyumsuz kopya gerçekleştirmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="ecc21-266">Merhaba çalıştırarak her kopya hello durumunu izleyebilirsiniz [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="ecc21-267">İkincil bir konumdan toocopy nasıl BLOB</span><span class="sxs-lookup"><span data-stu-id="ecc21-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="ecc21-268">BLOB'ları hello ikincil RA-GRS etkinleştirilmiş bir hesap konumundan kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="ecc21-269">Nasıl toodelete blob</span><span class="sxs-lookup"><span data-stu-id="ecc21-269">How toodelete a blob</span></span>
<span data-ttu-id="ecc21-270">toodelete bir blob önce bir blob başvurusu alın ve ardından hello Kaldır AzureStorageBlob cmdlet üzerinde çağırın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="ecc21-271">Aşağıdaki örneğine hello belirli bir kapsayıcıda tüm hello BLOB'lar siler.</span><span class="sxs-lookup"><span data-stu-id="ecc21-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="ecc21-272">Hello örnek ilk değişkenleri bir depolama hesabı için ayarlar ve bir depolama bağlamı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecc21-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="ecc21-273">Ardından, hello örnek hello kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalıştırmalarını hello [Kaldır AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove bloblarından Azure depolama alanında bir kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ecc21-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

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

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="ecc21-274">Nasıl toomanage Azure blob anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="ecc21-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="ecc21-275">Azure blob görüntüsünü oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="ecc21-276">Bir anlık görüntüsü, bir noktada geçen süre içinde bir blob, salt okunur bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="ecc21-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="ecc21-277">Bir anlık görüntü oluşturulduktan sonra okumak, kopyalanan, veya silinmiş, ancak değişiklik.</span><span class="sxs-lookup"><span data-stu-id="ecc21-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="ecc21-278">Bir anda göründüğü gibi anlık bir blob yukarı şekilde tooback sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="ecc21-279">Daha fazla bilgi için bkz: [Blob anlık görüntüsünün oluşturulmasına](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="ecc21-280">Nasıl toocreate blob anlık görüntü</span><span class="sxs-lookup"><span data-stu-id="ecc21-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="ecc21-281">toocreate snaphot bir BLOB ilk bir blob başvurusu alın ve hello çağrı `ICloudBlob.CreateSnapshot` yöntemini.</span><span class="sxs-lookup"><span data-stu-id="ecc21-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="ecc21-282">Merhaba aşağıdaki örnek ilk değişkenleri bir depolama hesabı için ayarlar ve ardından depolama bağlam oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecc21-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="ecc21-283">Ardından, hello örnek hello kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalıştırmalarını hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) yöntemi toocreate bir anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="ecc21-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

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

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="ecc21-284">Nasıl toolist blob'ın anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="ecc21-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="ecc21-285">Bir blob için istediğiniz sayıda anlık görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="ecc21-286">Merhaba anlık görüntüler, blob tootrack ile ilişkili listesinde, geçerli anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ecc21-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="ecc21-287">Merhaba aşağıdaki örnek kullanan önceden tanımlanmış bir blob ve çağrıları hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) bu blob cmdlet toolist hello anlık görüntüleri.</span><span class="sxs-lookup"><span data-stu-id="ecc21-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="ecc21-288">Nasıl toocopy anlık görüntüsünü bir blob</span><span class="sxs-lookup"><span data-stu-id="ecc21-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="ecc21-289">Bir blob toorestore hello anlık görüntüsünü kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="ecc21-290">Ayrıntılı bilgi ve kısıtlamaları için bkz: [Blob anlık görüntüsünün oluşturulmasına](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="ecc21-291">Merhaba aşağıdaki örnek ilk değişkenleri bir depolama hesabı için ayarlar ve ardından depolama bağlam oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecc21-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="ecc21-292">Ardından, hello örnek hello kapsayıcı ve blob adı değişkenleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="ecc21-293">Merhaba örneği alır hello kullanarak bir blob başvurusu [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalıştırmalarını hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) yöntemi toocreate bir anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="ecc21-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="ecc21-294">Ardından, hello örnek hello çalıştırır [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello anlık görüntüsü için hello kaynak blob hello ICloudBlob nesnesi kullanılarak bir blob.</span><span class="sxs-lookup"><span data-stu-id="ecc21-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="ecc21-295">Emin tooupdate hello değişkenleri yapılandırmanızı çalışan hello örnek önce dayalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="ecc21-296">Aşağıdaki örnek, hello hello kaynak ve hedef kapsayıcılarını ve hello kaynak blob zaten mevcut varsayar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

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

<span data-ttu-id="ecc21-297">Nasıl toomanage Azure BLOB öğrendiniz ve Azure PowerShell ile anlık görüntülerini blob göre nasıl toomanage tabloları, kuyrukları ve dosyaları toohello sonraki bölümde toolearn gidin.</span><span class="sxs-lookup"><span data-stu-id="ecc21-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="ecc21-298">Nasıl toomanage Azure tabloları ve varlıkları tablo</span><span class="sxs-lookup"><span data-stu-id="ecc21-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="ecc21-299">Azure tablo depolama hizmetidir kullanabileceğiniz bir nosql olmayan veri yapılandırılmış ve ilişkisel olmayan verilerin büyük kümelerini toostore ve sorgu.</span><span class="sxs-lookup"><span data-stu-id="ecc21-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="ecc21-300">Merhaba ana hello hizmet tablo, varlıkları ve özelliklerini bileşenleridir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="ecc21-301">Bir tablo, varlıkları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="ecc21-301">A table is a collection of entities.</span></span> <span data-ttu-id="ecc21-302">Bir varlık özellikler kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-302">An entity is a set of properties.</span></span> <span data-ttu-id="ecc21-303">Her varlığın tüm ad-değer çiftleri too252 özellikleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="ecc21-304">Bu bölümde, zaten hello Azure tablo depolama hizmeti kavramlarını olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="ecc21-305">Ayrıntılı bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://msdn.microsoft.com/library/azure/dd179338.aspx) ve [.NET kullanarak Azure Table storage'ı kullanmaya başlama](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="ecc21-306">Aşağıdaki alt bölümleri hello nasıl toomanage Azure Table depolama hizmeti Azure PowerShell kullanarak bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="ecc21-307">Merhaba kapsanan senaryolar dahil **oluşturma**, **silme**, ve **alma** **tabloları**, yanı **ekleme**, **sorgulama**, ve **tablo varlıkları silmek**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="ecc21-308">Nasıl toocreate bir tablo</span><span class="sxs-lookup"><span data-stu-id="ecc21-308">How toocreate a table</span></span>
<span data-ttu-id="ecc21-309">Her tablo bir Azure depolama hesabında bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="ecc21-310">Merhaba aşağıdaki örnekte gösterilmiştir nasıl toocreate Azure storage'da bir tablo.</span><span class="sxs-lookup"><span data-stu-id="ecc21-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="ecc21-311">Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ecc21-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="ecc21-312">Ardından, hello kullanan [yeni AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate Azure storage'da bir tablo.</span><span class="sxs-lookup"><span data-stu-id="ecc21-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="ecc21-313">Nasıl tooretrieve bir tablo</span><span class="sxs-lookup"><span data-stu-id="ecc21-313">How tooretrieve a table</span></span>
<span data-ttu-id="ecc21-314">Sorgulamak ve bir depolama hesabı bir ya da tüm tablolarda alın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="ecc21-315">Merhaba aşağıdaki örnekte nasıl kullanarak verilen Tablo tooretrieve hello gösteren [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="ecc21-316">Hiçbir parametre olmadan hello Get-AzureStorageTable cmdlet'i çağırırsanız, tüm depolama tablolar için bir depolama hesabı alır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="ecc21-317">Nasıl toodelete bir tablo</span><span class="sxs-lookup"><span data-stu-id="ecc21-317">How toodelete a table</span></span>
<span data-ttu-id="ecc21-318">Hello kullanarak bir depolama hesabından bir tablo silebilirsiniz [Kaldır AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="ecc21-319">Nasıl toomanage tablo varlıkları</span><span class="sxs-lookup"><span data-stu-id="ecc21-319">How toomanage table entities</span></span>
<span data-ttu-id="ecc21-320">Şu anda Azure PowerShell cmdlet'leri toomanage tablo varlıkları doğrudan sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="ecc21-321">Tablo varlıkları tooperform işlemde hello verilen hello sınıfları kullanabilir [.NET için Azure Storage istemci Kitaplığı](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="ecc21-322">Nasıl tooadd tablo varlıkları</span><span class="sxs-lookup"><span data-stu-id="ecc21-322">How tooadd table entities</span></span>
<span data-ttu-id="ecc21-323">bir varlık tooa tablosu tooadd ilk varlık özelliklerinizi tanımlayan bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecc21-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="ecc21-324">Bir varlığın 3 sistem özelliği de dahil olmak üzere too255 özelliklerini, olabilir: **PartitionKey**, **RowKey**, ve **zaman damgası**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="ecc21-325">Ekleme ve başlangıç değerleri güncelleştirmek için sorumlu **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="ecc21-326">Merhaba sunucu yöneten hello değerini **zaman damgası**, hangi değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="ecc21-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="ecc21-327">Birlikte hello **PartitionKey** ve **RowKey** tablo içindeki her varlık benzersiz şekilde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="ecc21-328">**PartitionKey**: hello varlık depolanan hello bölüm belirler.</span><span class="sxs-lookup"><span data-stu-id="ecc21-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="ecc21-329">**RowKey**: hello varlığın hello bölüm içinde benzersiz olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="ecc21-330">Bir varlık için özel özellikleri too252 tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="ecc21-331">Daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="ecc21-332">Merhaba aşağıdaki örnekte gösterilmiştir nasıl tooadd varlıklar tooa tablo.</span><span class="sxs-lookup"><span data-stu-id="ecc21-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="ecc21-333">Merhaba örnek nasıl tooretrieve çalışan tablosu hello ve birkaç varlıkları içine ekleyin gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="ecc21-334">İlk olarak, bir bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ecc21-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="ecc21-335">Ardından, tablo hello kullanarak verilen hello alır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="ecc21-336">Merhaba tablo mevcut değilse hello [yeni AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet'tir kullanılan toocreate Azure storage'da bir tablo.</span><span class="sxs-lookup"><span data-stu-id="ecc21-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="ecc21-337">Ardından, her varlığın bölüm ve satır anahtarını belirterek özel bir işlev Ekle varlık tooadd varlıklar toohello tablo hello örnek tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="ecc21-338">Merhaba Ekle-varlık işlev çağrılarını hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) hello cmdlet'ini [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) sınıfı toocreate bir varlık nesnesine.</span><span class="sxs-lookup"><span data-stu-id="ecc21-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="ecc21-339">Daha sonra hello örnek çağırır hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) bu varlık nesnesi tooadd yöntemi, tooa tablo.</span><span class="sxs-lookup"><span data-stu-id="ecc21-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

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

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="ecc21-340">Nasıl tooquery tablo varlıkları</span><span class="sxs-lookup"><span data-stu-id="ecc21-340">How tooquery table entities</span></span>
<span data-ttu-id="ecc21-341">tooquery bir tablo kullanmak hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ecc21-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="ecc21-342">Merhaba aşağıdaki örneği hello nasıl verilen hello betik zaten çalıştırdıysanız varsayar tooadd varlıklar başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="ecc21-343">Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama bağlamını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ecc21-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="ecc21-344">Ardından, hello kullanarak tooretrieve daha önce oluşturduğunuz hello "Çalışanlar" tablosu çalışır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="ecc21-345">Arama hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello Microsoft.WindowsAzure.Storage.Table.TableQuery sınıf üzerinde yeni bir sorgu nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecc21-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="ecc21-346">Merhaba örnek 1 dize filtresi belirtildiği gibi değeri olan 'ID' sütun hello varlıklar arar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="ecc21-347">Ayrıntılı bilgi için bkz: [sorgulama tabloları ve varlıkları](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="ecc21-348">Bu sorguyu çalıştırmak hello filtre ölçütüyle eşleşen tüm varlıkları döndürür.</span><span class="sxs-lookup"><span data-stu-id="ecc21-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

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

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="ecc21-349">Nasıl toodelete tablo varlıkları</span><span class="sxs-lookup"><span data-stu-id="ecc21-349">How toodelete table entities</span></span>
<span data-ttu-id="ecc21-350">Bir varlığın bölüm ve satır anahtarını kullanarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="ecc21-351">Merhaba aşağıdaki örneği hello nasıl verilen hello betik zaten çalıştırdıysanız varsayar tooadd varlıklar başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="ecc21-352">Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama bağlamını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ecc21-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="ecc21-353">Ardından, hello kullanarak tooretrieve daha önce oluşturduğunuz hello "Çalışanlar" tablosu çalışır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="ecc21-354">Merhaba tablo varsa hello örnek hello çağırır [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) bir varlık üzerinde bölüm ve satır anahtarı değerleri temel yöntemi tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="ecc21-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="ecc21-355">Daha sonra hello varlık toohello geçirin [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) yöntemi toodelete.</span><span class="sxs-lookup"><span data-stu-id="ecc21-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

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

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="ecc21-356">Nasıl toomanage Azure kuyrukları ve iletileri kuyruğa</span><span class="sxs-lookup"><span data-stu-id="ecc21-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="ecc21-357">Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="ecc21-358">Bu bölümde, zaten hello Azure kuyruk depolama hizmeti kavramlarını olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="ecc21-359">Ayrıntılı bilgi için bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](../storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="ecc21-360">Bu bölümde toomanage Azure kuyruk depolama hizmeti Azure PowerShell kullanarak nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="ecc21-361">Merhaba kapsamdaki senaryolar da dahil **ekleme** ve **silme** kuyruk iletileri yanı **oluşturma**, **silme**ve **sıraları alma**.</span><span class="sxs-lookup"><span data-stu-id="ecc21-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="ecc21-362">Nasıl bir kuyruk toocreate</span><span class="sxs-lookup"><span data-stu-id="ecc21-362">How toocreate a queue</span></span>
<span data-ttu-id="ecc21-363">Merhaba aşağıdaki örnek ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ecc21-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="ecc21-364">Ardından, çağıran [yeni AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate 'queuename' adında bir sıra.</span><span class="sxs-lookup"><span data-stu-id="ecc21-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="ecc21-365">Azure kuyruk hizmeti için adlandırma kuralları hakkında bilgi için bkz: [adlandırma kuyrukları ve meta verileri](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="ecc21-366">Nasıl bir kuyruk tooretrieve</span><span class="sxs-lookup"><span data-stu-id="ecc21-366">How tooretrieve a queue</span></span>
<span data-ttu-id="ecc21-367">Sorgulama ve belirli bir sıraya veya bir depolama hesabındaki tüm hello kuyrukların listesini alın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="ecc21-368">Merhaba aşağıdaki örnekte nasıl kullanarak belirtilen sırayı tooretrieve hello gösterir [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="ecc21-369">Merhaba çağırırsanız [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet parametre olmadan tüm hello kuyrukların listesini alır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="ecc21-370">Nasıl bir kuyruk toodelete</span><span class="sxs-lookup"><span data-stu-id="ecc21-370">How toodelete a queue</span></span>
<span data-ttu-id="ecc21-371">toodelete bir sıra ve tüm karışılama iletileri, çağrı hello Kaldır AzureStorageQueue cmdlet içerdiği.</span><span class="sxs-lookup"><span data-stu-id="ecc21-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="ecc21-372">Aşağıdaki örneğine hello nasıl kullanarak belirtilen sırayı toodelete hello Kaldır AzureStorageQueue cmdlet'ini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="ecc21-373">Nasıl bir kuyruk iletiye tooinsert</span><span class="sxs-lookup"><span data-stu-id="ecc21-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="ecc21-374">var olan bir sırayı iletiye tooinsert ilk hello yeni bir örneğini oluşturun [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ecc21-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="ecc21-375">Ardından, hello'ı çağırın [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ecc21-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="ecc21-376">Bir CloudQueueMessage bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="ecc21-377">Aşağıdaki örneğine hello nasıl tooadd tooa kuyruk iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="ecc21-378">Merhaba örneği ilk bağlantı tooAzure depolama kurar hello depolama hesabı adı ve erişim anahtarını içeren hello depolama hesabı bağlamını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ecc21-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="ecc21-379">Ardından, hello kullanarak hello belirtilen sırayı alır [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ecc21-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="ecc21-380">Merhaba sıra hello yoksa, [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet'tir kullanılan toocreate hello örneği [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ecc21-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="ecc21-381">Daha sonra hello örnek çağırır hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) bu ileti nesne tooadd yöntemi, tooa sırası.</span><span class="sxs-lookup"><span data-stu-id="ecc21-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="ecc21-382">Bir sırayı alır ve selamlama iletisine 'MessageInfo' ekler kod şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ecc21-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

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

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="ecc21-383">Nasıl toode-hello sıraya sonraki ileti</span><span class="sxs-lookup"><span data-stu-id="ecc21-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="ecc21-384">Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="ecc21-385">Merhaba çağırdığınızda [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) kuyrukta hello sonraki iletiyi elde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ecc21-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="ecc21-386">Döndürülen bir ileti **GetMessage** iletileri bu sıradan okuma başka bir kod görünmez tooany olur.</span><span class="sxs-lookup"><span data-stu-id="ecc21-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="ecc21-387">toofinish kaldırma selamlama iletisine hello sırasından hello ayrıca çağırmalısınız [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ecc21-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="ecc21-388">Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="ecc21-389">Kod çağrılarınızı **DeleteMessage** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="ecc21-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

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

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="ecc21-390">Nasıl toomanage Azure dosya paylaşımları ve dosyaları</span><span class="sxs-lookup"><span data-stu-id="ecc21-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="ecc21-391">Azure File storage hello standart SMB protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="ecc21-392">Microsoft Azure virtual machines ve cloud services bağlı paylaşımlar üzerinden uygulama bileşenleri arasında dosya verileri paylaşabilir ve şirket içi uygulamalara hello dosya depolama API'si veya Azure PowerShell üzerinden dosya verilerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="ecc21-393">Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage-dotnet-how-to-use-files.md) ve [dosya hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc21-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="ecc21-394">Nasıl tooset ve sorgu depolama analizi</span><span class="sxs-lookup"><span data-stu-id="ecc21-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="ecc21-395">Kullanabileceğiniz [Azure depolama çözümlemeleri](../storage-analytics.md) Azure depolama hesapları ve günlük verilerini istekleriyle ilgili toocollect ölçümlerini gönderilen tooyour depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="ecc21-395">You can use [Azure Storage Analytics](../storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="ecc21-396">Depolama ölçümleri toomonitor hello sistem durumunu bir depolama hesabı ve depolama günlük toodiagnose ve depolama hesabınızı ile ilgili sorunları gidermek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="ecc21-397">Kullanarak izlemeyi yapılandırmadan Azure portalı veya Windows PowerShell'i hello veya program aracılığıyla hello depolama istemci kitaplığı kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="ecc21-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="ecc21-398">Depolama günlük sunucu tarafı olur ve depolama hesabınızdaki hem başarılı hem başarısız istekler için toorecord ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="ecc21-399">Bu günlükler, okuma, yazma ve silme işlemleri, tablolar, kuyruklar ve BLOB'lar yanı sıra hello nedeniyle başarısız istekler için karşı toosee ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="ecc21-400">PowerShell kullanarak tooenable ve görünüm Storage ölçümleri verileri nasıl bakın toolearn [nasıl tooenable Storage ölçümleri PowerShell kullanarak](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="ecc21-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="ecc21-401">PowerShell kullanarak tooenable ve alma depolama günlük verileri nasıl bakın toolearn [nasıl tooenable depolama PowerShell kullanarak oturum](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) ve [depolama günlüğü günlük verilerinizi bulma](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="ecc21-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="ecc21-402">Depolama ölçümleri ve tootroubleshoot depolama sorunları günlüğü depolama kullanma hakkında ayrıntılı bilgi için bkz: [izleme, Diagnosing ve sorun giderme Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="ecc21-403">Nasıl toomanage paylaşılan erişim imzası (SAS) ve depolanan erişim ilkesi</span><span class="sxs-lookup"><span data-stu-id="ecc21-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="ecc21-404">Paylaşılan erişim imzalar, Azure Storage kullanarak herhangi bir uygulama için hello güvenlik modelinin önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="ecc21-405">Bunlar, hello hesap anahtarı olmamalıdır sınırlı izinlere tooyour depolama hesabı tooclients sağlamak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="ecc21-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="ecc21-406">Varsayılan olarak, yalnızca hello sahibi hello depolama hesabının BLOB'lar, tablolar ve Kuyruklar o hesabı içinde erişebilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="ecc21-407">Hizmet veya uygulama toomake bu kaynaklar kullanılabilir tooother istemciler erişim anahtarınızı paylaşmadan gerekiyorsa, üç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="ecc21-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="ecc21-408">Bir kapsayıcının izinleri toopermit anonim okuma erişimini toohello kapsayıcı ve bloblarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="ecc21-409">Bu tablo veya sıralara izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="ecc21-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="ecc21-410">Kısıtlı erişim hakları toocontainers, BLOB, kuyruklar ve tablolar için belirli bir zaman aralığı veren paylaşılan erişim imzası kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="ecc21-411">Depolanmış erişim ilkesi tooobtain ek bir paylaşılan erişim imzaları üzerinde denetim düzeyi bir kapsayıcıyı veya bloblarını için bir sıraya veya bir tablo için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="ecc21-412">Merhaba depolanmış erişim ilkesi toochange hello başlangıç saati, sona erme saati veya bir imza için izinler sağlar veya toorevoke, sonra yayımlandığı.</span><span class="sxs-lookup"><span data-stu-id="ecc21-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="ecc21-413">Paylaşılan erişim imzası iki forms biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="ecc21-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="ecc21-414">**Geçici SAS**: oluştururken bir geçici SAS hello başlangıç zamanı, bitiş saati ve hello SAS izinlerini tüm belirtilen SAS URI'sini hello üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ecc21-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="ecc21-415">Bu tür bir SAS oluşturulabilir bir kapsayıcı, blob, tablo veya kuyruğu ve iptal edilebilir olmayan.</span><span class="sxs-lookup"><span data-stu-id="ecc21-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="ecc21-416">**Saklı erişim ilkesi ile SAS**: bir saklı erişim ilkesi kaynak kapsayıcı bir blob kapsayıcısını, tablo veya kuyruğu - tanımlanmış ve bir veya daha fazla paylaşılan erişim imzaları toomanage kısıtlamalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="ecc21-417">Bir SAS depolanmış erişim ilkesi ile ilişkilendirdiğinizde, hello SAS hello kısıtlamaları devralır - hello başlangıç saati, sona erme saati ve izinleri - depolanan hello erişim ilkesi için tanımlı.</span><span class="sxs-lookup"><span data-stu-id="ecc21-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="ecc21-418">Bu tür bir SAS iptal edilebilir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="ecc21-419">Daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları (SAS)](../storage-dotnet-shared-access-signature-part-1.md) ve [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="ecc21-420">Merhaba sonraki bölümlerde, öğreneceksiniz nasıl toocreate Azure tabloları için paylaşılan erişim imzası belirteci ve depolanan erişim ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ecc21-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="ecc21-421">Azure PowerShell benzer cmdlet'lerini kapsayıcıları, BLOB'ları ve kuyrukları de sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecc21-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="ecc21-422">Bu bölümdeki toorun hello komut karşıdan hello [Azure PowerShell sürüm 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ecc21-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="ecc21-423">Nasıl toocreate ilke tabanlı paylaşılan erişim imzası belirteci</span><span class="sxs-lookup"><span data-stu-id="ecc21-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="ecc21-424">Merhaba yeni AzureStorageTableStoredAccessPolicy cmdlet toocreate yeni bir saklı erişim ilkesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecc21-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="ecc21-425">Ardından, hello çağırın [yeni AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate bir Azure Storage tablo için yeni bir ilke tabanlı paylaşılan erişim imzası belirteci.</span><span class="sxs-lookup"><span data-stu-id="ecc21-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="ecc21-426">Nasıl toocreate geçici (istenmeden olmayan) bir paylaşılan erişim imzası belirteci</span><span class="sxs-lookup"><span data-stu-id="ecc21-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="ecc21-427">Kullanım hello [yeni AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate yeni bir geçici (istenmeden olmayan) paylaşılan erişim imzası belirteci için bir Azure depolama tablosu:</span><span class="sxs-lookup"><span data-stu-id="ecc21-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="ecc21-428">Nasıl toocreate depolanmış erişim ilkesi</span><span class="sxs-lookup"><span data-stu-id="ecc21-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="ecc21-429">Merhaba yeni AzureStorageTableStoredAccessPolicy cmdlet toocreate yeni bir saklı erişim ilkesi için bir Azure Storage tabloyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="ecc21-430">Nasıl tooupdate depolanmış erişim ilkesi</span><span class="sxs-lookup"><span data-stu-id="ecc21-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="ecc21-431">Merhaba kümesi AzureStorageTableStoredAccessPolicy cmdlet tooupdate varolan bir depolanmış erişim ilkesi için bir Azure Storage tabloyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="ecc21-432">Nasıl toodelete depolanmış erişim ilkesi</span><span class="sxs-lookup"><span data-stu-id="ecc21-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="ecc21-433">Hello Kaldır AzureStorageTableStoredAccessPolicy cmdlet toodelete depolanmış erişim ilkesi, bir Azure Storage tablosunda kullanın:</span><span class="sxs-lookup"><span data-stu-id="ecc21-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="ecc21-434">Nasıl toouse Azure Storage ABD hükümeti ve Azure Çin için</span><span class="sxs-lookup"><span data-stu-id="ecc21-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="ecc21-435">Bir Azure ortamı Microsoft Azure, bağımsız bir dağıtımını olduğu gibi [US government Azure kamu](https://azure.microsoft.com/features/gov/), [genel Azure AzureCloud](https://portal.azure.com), ve [AzureChinaCloud Azure Çin'de 21Vianet tarafından işletilen](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="ecc21-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="ecc21-436">ABD hükümeti ve Azure Çin için yeni Azure ortamlarını dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="ecc21-437">Azure Storage ile AzureChinaCloud toouse toocreate AzureChinaCloud ile ilişkili bir depolama bağlamı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="ecc21-438">Bu adımları tooget başlattığınız izleyin:</span><span class="sxs-lookup"><span data-stu-id="ecc21-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="ecc21-439">Merhaba çalıştırmak [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello kullanılabilir Azure ortamı:</span><span class="sxs-lookup"><span data-stu-id="ecc21-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="ecc21-440">Bir Azure Çin hesap tooWindows PowerShell ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ecc21-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="ecc21-441">AzureChinaCloud hesabınız için bir depolama bağlam oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ecc21-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="ecc21-442">toouse Azure Storage ile [ABD Azure kamu](https://azure.microsoft.com/features/gov/), yeni bir ortam tanımlayın ve ardından yeni bir depolama bağlamı ile bu ortamı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ecc21-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="ecc21-443">Merhaba çalıştırmak [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello kullanılabilir Azure ortamı:</span><span class="sxs-lookup"><span data-stu-id="ecc21-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="ecc21-444">Bir Azure ABD devlet kurumları hesap tooWindows PowerShell ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ecc21-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="ecc21-445">AzureUSGovernment hesabınız için bir depolama bağlam oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ecc21-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="ecc21-446">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="ecc21-446">For more information, see:</span></span>

* <span data-ttu-id="ecc21-447">[Microsoft Azure kamu Geliştirici Kılavuzu](../../azure-government/documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ecc21-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="ecc21-448">Bir uygulama Çin hizmette oluştururken farklar genel bakış</span><span class="sxs-lookup"><span data-stu-id="ecc21-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="ecc21-449">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ecc21-449">Next Steps</span></span>
<span data-ttu-id="ecc21-450">Bu kılavuzda, öğrendiğinize nasıl toomanage Azure PowerShell ile Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="ecc21-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="ecc21-451">Bazı ilgili makaleler ve bunlarla ilgili daha fazla bilgi edinmek için kaynaklar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ecc21-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="ecc21-452">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="ecc21-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="ecc21-453">Azure Storage PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="ecc21-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="ecc21-454">Windows PowerShell başvurusu</span><span class="sxs-lookup"><span data-stu-id="ecc21-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

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
