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
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="80846-103">Azure Storage ile Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="80846-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="80846-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="80846-104">Overview</span></span>
<span data-ttu-id="80846-105">Azure PowerShell cmdlet'leri Azure Windows PowerShell üzerinden yönetmenizi sağlayan bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="80846-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="80846-106">Sistem yönetimi için özel olarak tasarlanan görev tabanlı bir komut satırı kabuğu ve betik dili olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="80846-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="80846-107">PowerShell ile kolayca kontrol edebilir ve Azure Hizmetleri ve uygulamaları otomatikleştirmesini.</span><span class="sxs-lookup"><span data-stu-id="80846-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="80846-108">Örneğin, aracılığıyla gerçekleştirebilirsiniz aynı görevleri gerçekleştirmek için cmdlet öğelerini kullanabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80846-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="80846-109">Bu kılavuzda, biz nasıl kullanılacağını ele alacağız [Azure depolama cmdlet'leri](/powershell/module/azurerm.storage/#storage) çeşitli Azure Storage ile geliştirme ve yönetim görevlerini gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="80846-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="80846-110">Bu kılavuz, kullanma konusunda deneyim sahibi olduğunuzu varsayar [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) ve [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="80846-111">Kılavuz bir sayıda Azure Storage ile PowerShell kullanımını göstermek için betik sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="80846-112">Her komut dosyası çalıştırılmadan önce yapılandırmanıza göre komut dosyası değişkenlerini güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="80846-113">Bu kılavuzun ilk bölümünde Azure depolama ve PowerShell hızlı bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="80846-114">Ayrıntılı bilgi ve yönergeler için başlangıç [Azure Storage ile Azure PowerShell'i kullanma önkoşulları](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="80846-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="80846-115">Azure Storage ve PowerShell 5 dakika içinde Başlarken</span><span class="sxs-lookup"><span data-stu-id="80846-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="80846-116">Bu bölümde 5 dakika içinde Azure Storage PowerShell aracılığıyla erişim gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="80846-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="80846-117">**Yeni Azure:** Microsoft Azure aboneliği ve bu abonelikle ilişkili bir Microsoft hesabı alın.</span><span class="sxs-lookup"><span data-stu-id="80846-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="80846-118">Azure satın alma seçenekleri hakkında daha fazla bilgi için bkz: [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/), [satın alma seçenekleri](https://azure.microsoft.com/pricing/purchase-options/), ve [üye teklifleri](https://azure.microsoft.com/pricing/member-offers/) (MSDN, Microsoft iş ortağı ağı ve, BizSpark üyeleri için ve diğer Microsoft programları).</span><span class="sxs-lookup"><span data-stu-id="80846-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="80846-119">Bkz: [Azure Active Directory'de (Azure AD) yönetici rolleri atama](https://msdn.microsoft.com/library/azure/hh531793.aspx) Azure abonelikleri hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="80846-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="80846-120">**Microsoft Azure aboneliği ve hesabı oluşturduktan sonra:**</span><span class="sxs-lookup"><span data-stu-id="80846-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="80846-121">En son yükleyip [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="80846-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="80846-122">Başlangıç Windows PowerShell Tümleşik komut dosyası ortamı (ISE): yerel bilgisayarınızda, Git **Başlat** menüsü.</span><span class="sxs-lookup"><span data-stu-id="80846-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="80846-123">Tür **Yönetimsel Araçlar** ve çalıştırmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="80846-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="80846-124">İçinde **Yönetimsel Araçlar** penceresinde sağ **Windows PowerShell ISE**, tıklatın **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="80846-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="80846-125">İçinde **Windows PowerShell ISE**, tıklatın **dosya** > **yeni** yeni bir komut dosyası oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="80846-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="80846-126">Şimdi, Azure depolama alanına erişmek için temel PowerShell komutları gösterir basit bir komut dosyası sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="80846-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="80846-127">Komut dosyası ilk Azure ister Azure eklemek için hesap kimlik bilgilerini yerel PowerShell ortamına hesap.</span><span class="sxs-lookup"><span data-stu-id="80846-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="80846-128">Ardından, betik varsayılan Azure aboneliği ve Azure'da yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="80846-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="80846-129">Ardından, betik yeni bir kapsayıcı bu yeni depolama hesabı oluşturun ve bu kapsayıcıya varolan bir görüntü dosyası (blob) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="80846-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="80846-130">Bu kapsayıcıdaki tüm blob'lara komut dosyasını listeler sonra yerel bilgisayarınızda yeni bir hedef dizin oluşturun ve görüntü dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="80846-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="80846-131">Aşağıdaki kod bölümünde açıklamalar arasında komut dosyasını seçin **#begin** ve **#end**.</span><span class="sxs-lookup"><span data-stu-id="80846-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="80846-132">Panoya kopyalamak için CTRL + C tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="80846-132">Press CTRL+C to copy it to the clipboard.</span></span>

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

6. <span data-ttu-id="80846-133">İçinde **Windows PowerShell ISE**, komut dosyasını kopyalamak için CTRL + V tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="80846-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="80846-134">Tıklatın **dosya** > **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="80846-134">Click **File** > **Save**.</span></span> <span data-ttu-id="80846-135">İçinde **Kaydet** iletişim penceresinde, komut dosyasının "mystoragescript." gibi bir ad yazın</span><span class="sxs-lookup"><span data-stu-id="80846-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="80846-136">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="80846-136">Click **Save**.</span></span>
7. <span data-ttu-id="80846-137">Şimdi, yapılandırma ayarlarınızı temel alan komut dosyası değişkenleri güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="80846-138">Güncelleştirmeniz gerekir **$SubscriptionName** kendi aboneliğinizle değişken.</span><span class="sxs-lookup"><span data-stu-id="80846-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="80846-139">Komut dosyasında belirtildiği gibi diğer değişkenleri tutun veya bunları istediğiniz gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="80846-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="80846-140">**$SubscriptionName:** Bu değişken, kendi abonelik adı ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="80846-141">Aboneliğinizi adını bulmak için aşağıdaki üç yoldan birini izleyin:</span><span class="sxs-lookup"><span data-stu-id="80846-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="80846-142">a.</span><span class="sxs-lookup"><span data-stu-id="80846-142">a.</span></span> <span data-ttu-id="80846-143">İçinde **Windows PowerShell ISE**, tıklatın **dosya** > **yeni** yeni bir komut dosyası oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="80846-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="80846-144">Yeni komut dosyası için aşağıdaki komutu kopyalayın ve tıklayın **hata ayıklama** > **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="80846-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="80846-145">Aşağıdaki komut dosyası ilk Azure ister Azure eklemek için hesap kimlik bilgilerini hesap yerel PowerShell ortamına ve yerel PowerShell oturumuna bağlı olan tüm abonelikler göster.</span><span class="sxs-lookup"><span data-stu-id="80846-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="80846-146">Bu öğreticiyi izleyerek sırasında kullanmak istediğiniz abonelik adını not alın:</span><span class="sxs-lookup"><span data-stu-id="80846-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="80846-147">b.</span><span class="sxs-lookup"><span data-stu-id="80846-147">b.</span></span> <span data-ttu-id="80846-148">Bulun ve abonelik adınızı kopyalamak için [Azure portal](https://portal.azure.com), sol Hub menüsünde **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="80846-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="80846-149">Bu kılavuzdaki betikleri çalıştırılırken kullanmak istediğiniz abonelik adı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="80846-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Azure portalına](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="80846-151">c.</span><span class="sxs-lookup"><span data-stu-id="80846-151">c.</span></span> <span data-ttu-id="80846-152">Bulun ve abonelik adınızı kopyalamak için [Klasik Azure portalı](https://manage.windowsazure.com/), aşağı kaydırın ve tıklayın **ayarları** portalın sol tarafındaki.</span><span class="sxs-lookup"><span data-stu-id="80846-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="80846-153">Tıklatın **abonelikleri** aboneliklerinizi listesini görmek için.</span><span class="sxs-lookup"><span data-stu-id="80846-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="80846-154">Bu kılavuzda verilen komut dosyaları çalıştırırken kullanmak istediğiniz abonelik adı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="80846-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![Klasik Azure Portalı](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="80846-156">**$StorageAccountName:** komut dosyasında verilen ad kullanın veya depolama hesabınız için yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="80846-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="80846-157">**Önemli:** depolama hesabı adının Azure'da benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="80846-158">Çok küçük olmalıdır!</span><span class="sxs-lookup"><span data-stu-id="80846-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="80846-159">**$Location:** verilen "Batı ABD" betik kullanın veya Doğu ABD, Kuzey Avrupa vb. gibi diğer Azure konumları seçin.</span><span class="sxs-lookup"><span data-stu-id="80846-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="80846-160">**$ContainerName:** komut dosyasında verilen ad kullanın veya, kapsayıcı için yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="80846-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="80846-161">**$ImageToUpload:** yerel bilgisayarınızda bir resim yolu gibi girin: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="80846-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="80846-162">**$DestinationFolder:** gibi Azure Storage'dan indirilen dosyaları depolamak için bir yerel dizinin yolunu girin: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="80846-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="80846-163">"Mystoragescript.ps1" dosyasındaki komut dosyası değişkenleri güncelleştirdikten sonra tıklatın **dosya** > **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="80846-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="80846-164">Ardından **hata ayıklama** > **çalıştırmak** veya basın **F5** komut dosyasını çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="80846-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="80846-165">Betik çalıştıktan sonra indirilen görüntü dosyasını içeren bir yerel hedef klasör olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80846-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="80846-166">Aşağıdaki ekran görüntüsünde bir örnek çıkış şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="80846-166">The following screenshot shows an example output:</span></span>

![BLOB'ları indirme](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="80846-168">"PowerShell ve Azure Storage ile 5 dakika içinde Başlarken" bölümünde Azure Storage ile Azure PowerShell'i kullanma hakkında hızlı bir giriş sağlanan.</span><span class="sxs-lookup"><span data-stu-id="80846-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="80846-169">Ayrıntılı bilgi ve yönergeler için aşağıdaki bölümleri okuyun geçirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="80846-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="80846-170">Azure Storage ile Azure PowerShell'i kullanma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="80846-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="80846-171">Bir Azure aboneliği ve yukarıda açıklandığı gibi bu kılavuzda verilen PowerShell cmdlet'lerini çalıştırmak için hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="80846-172">Azure PowerShell cmdlet'leri Azure Windows PowerShell üzerinden yönetmenizi sağlayan bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="80846-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="80846-173">Yükleme ve Azure PowerShell ayarlama hakkında daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80846-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="80846-174">İndirin ve yükleyin veya bu kılavuzu kullanmadan önce en son Azure PowerShell modülü yükseltme öneririz.</span><span class="sxs-lookup"><span data-stu-id="80846-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="80846-175">Standart Windows PowerShell konsolu veya Windows PowerShell Tümleşik komut dosyası ortamı (ISE) cmdlet'lerini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="80846-176">Örneğin, açmak için **Windows PowerShell ISE**, Başlat menüsüne gidin, Yönetimsel Araçlar yazın ve çalıştırmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="80846-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="80846-177">Yönetimsel Araçlar penceresinde, Windows PowerShell ISE sağ tıklatın, yönetici olarak çalıştır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="80846-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="80846-178">Azure depolama hesapları yönetme</span><span class="sxs-lookup"><span data-stu-id="80846-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="80846-179">Depolama hesaplarını Azure PowerShell ile yönetme bir bakalım</span><span class="sxs-lookup"><span data-stu-id="80846-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="80846-180">Varsayılan bir Azure aboneliği ayarlama</span><span class="sxs-lookup"><span data-stu-id="80846-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="80846-181">Azure PowerShell kullanarak Azure Storage yönetmek için istemci ortamınızı Azure ile Azure Active Directory kimlik doğrulaması veya sertifika tabanlı kimlik doğrulaması üzerinden kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="80846-182">Ayrıntılı bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="80846-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="80846-183">Bu kılavuz, Azure Active Directory kimlik doğrulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="80846-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="80846-184">Windows PowerShell ISE'de Azure eklemek için aşağıdaki komutu yazın hesabı yerel PowerShell ortamına:</span><span class="sxs-lookup"><span data-stu-id="80846-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="80846-185">"Oturum içinde için Microsoft Azure" penceresinde e-posta adresi ve hesabınızla ilişkili parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="80846-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="80846-186">Azure, kimlik bilgilerini doğrulayıp kaydeder ve pencereyi kapatır.</span><span class="sxs-lookup"><span data-stu-id="80846-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="80846-187">Ardından, yerel PowerShell ortamınızda Azure hesapları görüntüleyin ve hesabınızın listelendiğini doğrulamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="80846-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="80846-188">Ardından, yerel PowerShell oturumuna bağlı tüm abonelikleri görmek için aşağıdaki cmdlet'i çalıştırın ve aboneliğinizi listelenmiş olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="80846-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="80846-189">Varsayılan bir Azure aboneliği için Select-AzureSubscription cmdlet'ini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="80846-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="80846-190">Get-AzureSubscription cmdlet'ini çalıştırarak varsayılan abonelik adını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="80846-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="80846-191">Azure Storage için tüm kullanılabilir PowerShell cmdlet'leri görmek için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="80846-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="80846-192">Yeni bir Azure depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="80846-193">Azure depolama kullanan bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="80846-194">Aboneliğinize bağlanmak için bilgisayarınızı yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="80846-195">Tüm kullanılabilir veri merkezi konumlarını bulmak için Get-AzureLocation cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="80846-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="80846-196">Ardından, yeni bir depolama hesabı oluşturmak için New-AzureStorageAccount cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="80846-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="80846-197">Aşağıdaki örnekte "Batı ABD" veri merkezine yeni bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80846-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="80846-198">Depolama hesabınızın adının Azure içinde benzersiz olmalıdır ve küçük harf olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="80846-199">Adlandırma kuralları ve sınırlamaları için bkz: [Azure Storage hesapları hakkında](storage-create-storage-account.md) ve [adlandırma ve başvuran kapsayıcıları, Blobları ve meta veri](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="80846-200">Varsayılan bir Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="80846-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="80846-201">Aboneliğinizde birden çok depolama hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="80846-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="80846-202">Bunlardan birini seçin ve aynı PowerShell oturumunda tüm depolama komutlar için varsayılan depolama hesabı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="80846-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="80846-203">Bu depolama bağlamı açıkça belirtmeden Azure PowerShell depolama komutları çalıştırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="80846-204">Aboneliğiniz için bir varsayılan depolama hesabı ayarlamak için Set-AzureSubscription cmdlet'i çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="80846-205">Ardından, depolama hesabı varsayılan abonelik hesabınızla ilişkili olduğunu doğrulamak için Get-AzureSubscription cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="80846-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="80846-206">Bu komut, geçerli bir depolama hesabı dahil olmak üzere geçerli abonelikte abonelik özellikleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="80846-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="80846-207">Bir Abonelikteki tüm Azure depolama hesapları listelemek nasıl</span><span class="sxs-lookup"><span data-stu-id="80846-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="80846-208">Her Azure aboneliğinin en fazla 100 depolama hesapları olabilir.</span><span class="sxs-lookup"><span data-stu-id="80846-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="80846-209">Sınırları hakkında en güncel bilgiler için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="80846-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="80846-210">Adı ve geçerli Abonelikteki depolama hesapları durumunu öğrenmek için aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="80846-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="80846-211">Bir Azure depolama bağlamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-211">How to create an Azure storage context</span></span>
<span data-ttu-id="80846-212">Azure depolama bağlam, depolama kimlik bilgilerini kapsülleyen PowerShell'de bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="80846-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="80846-213">Bir depolama bağlamı kullanırken, bir sonraki cmdlet'ini çalıştırarak depolama hesabı ve erişim anahtarını açıkça belirtmeden isteğiniz kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="80846-214">Bir depolama bağlamı kullanarak depolama hesabı adı ve erişim anahtarı, paylaşılan erişim imzası (SAS) belirteci, bağlantı dizesi gibi birçok yolla oluşturabilirsiniz veya anonim.</span><span class="sxs-lookup"><span data-stu-id="80846-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="80846-215">Daha fazla bilgi için bkz: [yeni AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="80846-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="80846-216">Bir depolama bağlamı oluşturmak için aşağıdaki üç yoldan birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="80846-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="80846-217">Çalıştırma [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) Azure depolama hesabınız için birincil depolama erişim tuşunu bulmak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="80846-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="80846-218">Ardından, çağrı [yeni AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) depolama bağlamı oluşturmak için cmdlet'i:</span><span class="sxs-lookup"><span data-stu-id="80846-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="80846-219">Bir Azure depolama kapsayıcısı için bir paylaşılan erişim imzası belirteç oluşturmak ve bir depolama bağlamı oluşturmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="80846-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="80846-220">Daha fazla bilgi için bkz: [yeni AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) ve [kullanarak paylaşılan erişim imzaları (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="80846-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="80846-221">Bazı durumlarda, yeni bir depolama bağlamı oluşturduğunuzda, hizmet uç noktalarına belirtmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="80846-222">Depolama hesabınız için bir özel etki alanı adı Blob hizmetine kayıtlı veya bir paylaşılan erişim imzası depolama kaynaklarına erişmek için kullanmak istediğiniz durumlarda bu gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="80846-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="80846-223">Hizmet uç noktalarına bağlantı dizesi olarak ayarlayın ve aşağıda gösterildiği gibi yeni bir depolama bağlamı oluşturmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="80846-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="80846-224">Bir depolama bağlantı dizesi yapılandırma hakkında daha fazla bilgi için bkz: [bağlantı dizelerini yapılandırma](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="80846-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="80846-225">Bilgisayarınızı ayarlayın ve abonelikleri ve Azure PowerShell kullanarak depolama hesaplarını yönetecek öğrendiniz göre Azure BLOB'ları yönetmek ve anlık görüntüleri blob öğrenmek için sonraki bölüme gidin.</span><span class="sxs-lookup"><span data-stu-id="80846-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="80846-226">Nasıl alınacağını ve Azure depolama anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="80846-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="80846-227">Bir Azure Storage hesabı iki hesabı anahtarları ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="80846-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="80846-228">Anahtarlarınızı almak için aşağıdaki cmdlet'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="80846-229">Belirli bir anahtarı almak için aşağıdaki cmdlet'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="80846-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="80846-230">Birincil ve ikincil değerler geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="80846-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="80846-231">Anahtarlarınızı yeniden oluşturmak istiyorsanız, aşağıdaki cmdlet'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="80846-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="80846-232">"Birincil" ve "İkincil" - KeyType için geçerli değerler:</span><span class="sxs-lookup"><span data-stu-id="80846-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="80846-233">Azure BLOB'ları yönetme</span><span class="sxs-lookup"><span data-stu-id="80846-233">How to manage Azure blobs</span></span>
<span data-ttu-id="80846-234">Azure Blob Depolama, büyük miktarlarda herhangi bir yere HTTP veya HTTPS aracılığıyla erişilebilen metin veya ikili veriler gibi yapılandırılmamış verileri depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="80846-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="80846-235">Bu bölümde, zaten Azure Blob Depolama hizmetinin kavramlarını olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="80846-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="80846-236">Ayrıntılı bilgi için bkz: [.NET kullanarak Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="80846-237">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-237">How to create a container</span></span>
<span data-ttu-id="80846-238">Azure depolama her blob bir kapsayıcıda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80846-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="80846-239">Yeni AzureStorageContainer cmdlet'ini kullanarak özel bir kapsayıcı oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="80846-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="80846-240">Anonim okuma erişimini üç düzeyi vardır: **kapalı**, **Blob**, ve **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="80846-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="80846-241">Bloblar için anonim erişimi engellemek için izni parametre kümesini **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="80846-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="80846-242">Varsayılan olarak yeni kapsayıcı özeldir ve yalnızca hesap sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="80846-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="80846-243">Anonim izin vermek için herkese okuma erişimi blob kaynaklarına ancak kapsayıcı meta verileri için veya kapsayıcıdaki blobları listesine izin parametre kümesine **Blob**.</span><span class="sxs-lookup"><span data-stu-id="80846-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="80846-244">Kaynaklar, kapsayıcı meta verileri ve kapsayıcıdaki blobları listesi blob tam ortak okuma erişimi sağlamak üzere izin parametre kümesini **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="80846-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="80846-245">Daha fazla bilgi için bkz: [kapsayıcılar ve bloblar için anonim okuma erişimini yönetme](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="80846-245">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="80846-246">Bir kapsayıcıya bir blob karşıya yüklemek nasıl</span><span class="sxs-lookup"><span data-stu-id="80846-246">How to upload a blob into a container</span></span>
<span data-ttu-id="80846-247">Azure Blob Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="80846-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="80846-248">Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="80846-249">BLOB'ları bir kapsayıcıya karşıya yüklemek için kullanabileceğiniz [kümesi AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="80846-250">Varsayılan olarak, bu komutu bir blok blobuna yerel dosyaları karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="80846-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="80846-251">Blob türü belirtmek için - BlobType parametresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="80846-252">Aşağıdaki örnek çalıştıran [Get-Childıtem](http://technet.microsoft.com/library/hh849800.aspx) belirlenen klasördeki tüm dosyaları almak için cmdlet ve ardından bunları sonraki cmdlet'e ardışık düzen işleci kullanılarak geçirir.</span><span class="sxs-lookup"><span data-stu-id="80846-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="80846-253">[Kümesi AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet, kapsayıcıya yerel dosyaları yükler:</span><span class="sxs-lookup"><span data-stu-id="80846-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="80846-254">Kapsayıcıdan BLOB indirmek nasıl</span><span class="sxs-lookup"><span data-stu-id="80846-254">How to download blobs from a container</span></span>
<span data-ttu-id="80846-255">Aşağıdaki örnek, bir kapsayıcıdan BLOB indirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="80846-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="80846-256">Örneğin, ilk Azure depolama hesabı adı ve birincil erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="80846-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="80846-257">Ardından, örnek kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="80846-258">Ardından, örnek kullanır [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobları yerel hedef klasöre yüklemek için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

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

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="80846-259">Bir depolama kapsayıcıdan BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="80846-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="80846-260">BLOB storage hesapları ve bölgeler arasında zaman uyumsuz olarak kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="80846-261">Aşağıdaki örnekte, iki farklı depolama hesaplarındaki başka bir bir depolama kapsayıcıdan BLOB kopyalama gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="80846-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="80846-262">Örnek ilk kaynak ve hedef depolama hesapları için değişkenleri ayarlar ve ardından her hesap için bir depolama bağlam oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80846-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="80846-263">Ardından, örnek BLOB'ları kaynak kapsayıcıdan hedef kullanarak kapsayıcı kopyalar [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="80846-264">Örnek kaynak ve hedef depolama hesapları ve kapsayıcıları zaten mevcut olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="80846-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

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

<span data-ttu-id="80846-265">Bu örnekte bir zaman uyumsuz kopya gerçekleştirmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="80846-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="80846-266">Çalıştırarak her kopya durumunu izleyebilirsiniz [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="80846-267">İkincil bir konumdan BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="80846-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="80846-268">BLOB'ları, RA-GRS etkinleştirilmiş bir hesap ikincil konumdan kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="80846-269">Bir blob silme</span><span class="sxs-lookup"><span data-stu-id="80846-269">How to delete a blob</span></span>
<span data-ttu-id="80846-270">Bir blobu silmek için önce bir blob başvurusu alın ve sonra Kaldır AzureStorageBlob cmdlet'i üzerinde çağırın.</span><span class="sxs-lookup"><span data-stu-id="80846-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="80846-271">Aşağıdaki örnek, belirli bir kapsayıcıdaki tüm blob'lara siler.</span><span class="sxs-lookup"><span data-stu-id="80846-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="80846-272">Örnek ilk değişkenleri bir depolama hesabı için ayarlar ve bir depolama bağlamı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80846-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="80846-273">Ardından, örnek kullanarak bir blob başvurusu alır. [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalışan [Kaldır AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) BLOB'ları bir kapsayıcıda Azure depolama kaldırmak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="80846-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

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

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="80846-274">Azure blob anlık görüntülerini yönetme</span><span class="sxs-lookup"><span data-stu-id="80846-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="80846-275">Azure blob görüntüsünü oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="80846-276">Bir anlık görüntüsü, bir noktada geçen süre içinde bir blob, salt okunur bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="80846-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="80846-277">Bir anlık görüntü oluşturulduktan sonra okumak, kopyalanan, veya silinmiş, ancak değişiklik.</span><span class="sxs-lookup"><span data-stu-id="80846-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="80846-278">Anlık görüntüler bir anda göründüğü gibi bir blob yedeklemek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="80846-279">Daha fazla bilgi için bkz: [Blob anlık görüntüsünün oluşturulmasına](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="80846-280">Bir blob anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-280">How to create a blob snapshot</span></span>
<span data-ttu-id="80846-281">Bir BLOB snaphot oluşturmak için öncelikle bir blob başvurusu alın ve ardından çağırın `ICloudBlob.CreateSnapshot` yöntemini.</span><span class="sxs-lookup"><span data-stu-id="80846-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="80846-282">Aşağıdaki örnek ilk değişkenleri bir depolama hesabı için ayarlar ve bir depolama bağlamı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80846-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="80846-283">Ardından, örnek kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalışan [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) bir anlık görüntü oluşturmak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80846-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

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

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="80846-284">Nasıl bir blob'un anlık görüntüleri listelemek için</span><span class="sxs-lookup"><span data-stu-id="80846-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="80846-285">Bir blob için istediğiniz sayıda anlık görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="80846-286">Geçerli anlık izlemek için blob ile ilişkili anlık görüntüleri listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="80846-287">Aşağıdaki örnek, önceden tanımlanmış bir blob ve çağrıları kullanır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) bu blob anlık görüntüleri listelemek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="80846-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="80846-288">Bir anlık görüntü bir BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="80846-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="80846-289">Anlık görüntüyü geri yüklemek için bir blob görüntüsünü kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="80846-290">Ayrıntılı bilgi ve kısıtlamaları için bkz: [Blob anlık görüntüsünün oluşturulmasına](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="80846-291">Aşağıdaki örnek ilk değişkenleri bir depolama hesabı için ayarlar ve bir depolama bağlamı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80846-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="80846-292">Ardından, örnek kapsayıcı ve blob adı değişkenleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="80846-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="80846-293">Örnek kullanarak bir blob başvurusu alır [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet'i ve çalışan [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) bir anlık görüntü oluşturmak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80846-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="80846-294">Ardından, örnek çalıştırır [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet'i için kaynak blob ICloudBlob nesnesi kullanılarak bir blob görüntüsünü kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="80846-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="80846-295">Örneği çalıştırmadan önce yapılandırmanıza göre değişkenlerini güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="80846-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="80846-296">Aşağıdaki örnekte kaynak ve hedef kapsayıcılarını ve kaynak blob zaten mevcut varsaydığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="80846-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

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

<span data-ttu-id="80846-297">Azure BLOB'ları yönetmek ve Azure PowerShell ile anlık görüntülerini blob öğrendiniz, tablolar, kuyruklar ve dosyaları yönetme konusunda bilgi almak için sonraki bölüme gidin.</span><span class="sxs-lookup"><span data-stu-id="80846-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="80846-298">Azure tabloları ve tablo varlıkları yönetme</span><span class="sxs-lookup"><span data-stu-id="80846-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="80846-299">Azure tablo depolama depolamak ve yapılandırılmış ve ilişkisel olmayan verilerin büyük kümelerini sorgulamak için kullanabileceğiniz bir nosql olmayan veri hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="80846-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="80846-300">Hizmet ana bileşenlerinin tabloları, varlıkları ve özellikler mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="80846-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="80846-301">Bir tablo, varlıkları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="80846-301">A table is a collection of entities.</span></span> <span data-ttu-id="80846-302">Bir varlık özellikler kümesidir.</span><span class="sxs-lookup"><span data-stu-id="80846-302">An entity is a set of properties.</span></span> <span data-ttu-id="80846-303">Her varlığın tüm ad-değer çiftleri en çok 252 özellik olabilir.</span><span class="sxs-lookup"><span data-stu-id="80846-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="80846-304">Bu bölümde, zaten Azure tablo depolama hizmeti kavramlarını olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="80846-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="80846-305">Ayrıntılı bilgi için bkz: [tablo hizmeti veri modelini anlama](http://msdn.microsoft.com/library/azure/dd179338.aspx) ve [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="80846-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="80846-306">Aşağıdaki alt bölümlerde Azure PowerShell kullanarak Azure Table depolama hizmetini yönetmek nasıl öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="80846-307">Kapsamdaki senaryolar dahil **oluşturma**, **silme**, ve **alma** **tabloları**, yanı **ekleme**, **sorgulama**, ve **tablo varlıkları silmek**.</span><span class="sxs-lookup"><span data-stu-id="80846-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="80846-308">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-308">How to create a table</span></span>
<span data-ttu-id="80846-309">Her tablo bir Azure depolama hesabında bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80846-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="80846-310">Aşağıdaki örnek, Azure Storage'da bir tablo oluşturmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="80846-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="80846-311">Örneğin, ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="80846-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="80846-312">Ardından, kullanan [yeni AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) Azure Storage'da bir tablo oluşturmak için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="80846-313">Tablo alma</span><span class="sxs-lookup"><span data-stu-id="80846-313">How to retrieve a table</span></span>
<span data-ttu-id="80846-314">Sorgulamak ve bir depolama hesabı bir ya da tüm tablolarda alın.</span><span class="sxs-lookup"><span data-stu-id="80846-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="80846-315">Aşağıdaki örnekte verilen tablo kullanarak almayı gösterir [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="80846-316">Get-AzureStorageTable cmdlet parametre olmadan çağırırsanız, tüm depolama tablolar için bir depolama hesabı alır.</span><span class="sxs-lookup"><span data-stu-id="80846-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="80846-317">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="80846-317">How to delete a table</span></span>
<span data-ttu-id="80846-318">Kullanarak bir depolama hesabından bir tablo silebilirsiniz [Kaldır AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="80846-319">Tablo varlıkları yönetme</span><span class="sxs-lookup"><span data-stu-id="80846-319">How to manage table entities</span></span>
<span data-ttu-id="80846-320">Şu anda Azure PowerShell tablo varlıkları doğrudan yönetmek için cmdlet'leri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="80846-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="80846-321">Tablo varlıklar üzerinde işlem gerçekleştirmek için verilen sınıfları kullanabilirsiniz [.NET için Azure Storage istemci Kitaplığı](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="80846-322">Tablo varlıkları ekleme</span><span class="sxs-lookup"><span data-stu-id="80846-322">How to add table entities</span></span>
<span data-ttu-id="80846-323">Tabloya bir varlık eklemek için önce varlık özelliklerinizi tanımlayan bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="80846-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="80846-324">Bir varlık 3 sistem özelliği de dahil olmak üzere en fazla 255 özelliklere sahip olabilir: **PartitionKey**, **RowKey**, ve **zaman damgası**.</span><span class="sxs-lookup"><span data-stu-id="80846-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="80846-325">Ekleme ve değerlerini güncelleştirme sorumlu **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="80846-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="80846-326">Sunucu değeri yöneten **zaman damgası**, hangi değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="80846-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="80846-327">Birlikte **PartitionKey** ve **RowKey** tablo içindeki her varlık benzersiz şekilde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="80846-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="80846-328">**PartitionKey**: Varlık depolanan bölüm belirler.</span><span class="sxs-lookup"><span data-stu-id="80846-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="80846-329">**RowKey**: varlığın bölüm içinde benzersiz şekilde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="80846-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="80846-330">Bir varlık için en çok 252 özel özellikler tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="80846-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="80846-331">Daha fazla bilgi için bkz: [tablo hizmeti veri modelini anlama](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="80846-332">Aşağıdaki örnek, bir tabloya varlıkları eklemek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="80846-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="80846-333">Örneğin, çalışan tablosunu alın ve birkaç varlıklar içine ekleyin gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="80846-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="80846-334">İlk olarak, Azure depolama hesabı adı ve erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="80846-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="80846-335">Ardından, verilen tablo kullanarak alır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="80846-336">Tablo mevcut değilse [yeni AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet Azure Storage'da bir tablo oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="80846-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="80846-337">Ardından, örnek özel bir işlev her varlığın bölüm ve satır anahtarını belirterek tabloya varlıkları eklemek için Add-varlık tanımlar.</span><span class="sxs-lookup"><span data-stu-id="80846-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="80846-338">Add-varlık işlev çağrılarını [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet'ini [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) bir varlık nesnesini oluşturmak için sınıfı.</span><span class="sxs-lookup"><span data-stu-id="80846-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="80846-339">Daha sonra örnek çağırır [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) bir tabloya eklemek için bu varlık nesnesi üzerinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80846-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

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

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="80846-340">Tablo varlıkları sorgulama</span><span class="sxs-lookup"><span data-stu-id="80846-340">How to query table entities</span></span>
<span data-ttu-id="80846-341">Bir tabloyu sorgulamak için kullanın [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="80846-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="80846-342">Aşağıdaki örnekte nasıl verilen komut dosyası zaten çalıştırdıysanız varsayar bu kılavuzun varlıkların bölüm eklemek için.</span><span class="sxs-lookup"><span data-stu-id="80846-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="80846-343">Örneğin, ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama bağlamı kullanarak depolama bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="80846-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="80846-344">Ardından, daha önce oluşturulan "Çalışanlar" tablosunu kullanarak almaya çalışır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="80846-345">Çağırma [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet Microsoft.WindowsAzure.Storage.Table.TableQuery sınıf üzerinde yeni bir sorgu nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80846-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="80846-346">Örnek 1 dize filtresi belirtildiği gibi değeri olan 'ID' sütuna sahip varlıklar arar.</span><span class="sxs-lookup"><span data-stu-id="80846-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="80846-347">Ayrıntılı bilgi için bkz: [sorgulama tabloları ve varlıkları](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="80846-348">Bu sorgu çalıştırdığınızda, filtre ölçütüyle eşleşen tüm varlıkları döndürür.</span><span class="sxs-lookup"><span data-stu-id="80846-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

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

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="80846-349">Tablo varlıkları silme</span><span class="sxs-lookup"><span data-stu-id="80846-349">How to delete table entities</span></span>
<span data-ttu-id="80846-350">Bir varlığın bölüm ve satır anahtarını kullanarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="80846-351">Aşağıdaki örnekte nasıl verilen komut dosyası zaten çalıştırdıysanız varsayar bu kılavuzun varlıkların bölüm eklemek için.</span><span class="sxs-lookup"><span data-stu-id="80846-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="80846-352">Örneğin, ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama bağlamı kullanarak depolama bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="80846-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="80846-353">Ardından, daha önce oluşturulan "Çalışanlar" tablosunu kullanarak almaya çalışır [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="80846-354">Tablo varsa, örnek çağırır [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) bir varlık alma yöntemi temel üzerinde bölüm ve satır anahtarı değerleri.</span><span class="sxs-lookup"><span data-stu-id="80846-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="80846-355">Daha sonra varlığa geçirin [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) silmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="80846-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

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

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="80846-356">Azure kuyrukları ve iletileri kuyruğa yönetme</span><span class="sxs-lookup"><span data-stu-id="80846-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="80846-357">Azure Kuyruk depolama, HTTP veya HTTPS kullanan kimlik doğrulaması yapılmış çağrılar aracılığıyla dünyanın her yerinden erişilebilen çok sayıda iletinin depolanması için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="80846-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="80846-358">Bu bölümde, zaten Azure kuyruk depolama hizmeti kavramlarını olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="80846-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="80846-359">Ayrıntılı bilgi için bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="80846-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="80846-360">Bu bölümde Azure PowerShell kullanarak Azure kuyruk depolama hizmetini yönetmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="80846-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="80846-361">Kapsamdaki senaryolar dahil **ekleme** ve **silme** kuyruk iletileri yanı **oluşturma**, **silme**ve **sıraları alma**.</span><span class="sxs-lookup"><span data-stu-id="80846-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="80846-362">Bir sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-362">How to create a queue</span></span>
<span data-ttu-id="80846-363">Aşağıdaki örnek ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="80846-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="80846-364">Ardından, çağıran [yeni AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) 'queuename' adında bir kuyruk oluşturmak için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="80846-365">Azure kuyruk hizmeti için adlandırma kuralları hakkında bilgi için bkz: [adlandırma kuyrukları ve meta verileri](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="80846-366">Bir Sıraya alma</span><span class="sxs-lookup"><span data-stu-id="80846-366">How to retrieve a queue</span></span>
<span data-ttu-id="80846-367">Sorgulama ve belirli bir sıraya veya bir depolama hesabındaki tüm kuyrukların listesini alın.</span><span class="sxs-lookup"><span data-stu-id="80846-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="80846-368">Aşağıdaki örnek, belirtilen sırada kullanarak almak gösterilmiştir [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="80846-369">Çağırırsanız [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet parametre olmadan tüm kuyrukların listesini alır.</span><span class="sxs-lookup"><span data-stu-id="80846-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="80846-370">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="80846-370">How to delete a queue</span></span>
<span data-ttu-id="80846-371">Bir kuyruk ve içerdiği tüm iletileri silmek için Remove-AzureStorageQueue cmdlet'ini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80846-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="80846-372">Aşağıdaki örnek, Remove-AzureStorageQueue cmdlet'i kullanılarak belirtilen bir kuyruk silme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="80846-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="80846-373">Kuyruğa bir ileti ekleme</span><span class="sxs-lookup"><span data-stu-id="80846-373">How to insert a message into a queue</span></span>
<span data-ttu-id="80846-374">Varolan bir sıraya bir ileti eklemek için önce yeni bir örneğini oluşturun [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="80846-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="80846-375">Ardından [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80846-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="80846-376">Bir CloudQueueMessage bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="80846-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="80846-377">Aşağıdaki örnek, bir sıraya ileti eklemek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="80846-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="80846-378">Örneğin, ilk Azure depolama hesabı adı ve erişim anahtarını içeren depolama hesabı bağlamını kullanarak depolama bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="80846-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="80846-379">Ardından, belirtilen sırada kullanarak alır [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="80846-380">Sıranın varsa [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet'i bir örneğini oluşturmak için kullanılan [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="80846-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="80846-381">Daha sonra örnek çağırır [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) bir sıraya eklemek için bu ileti nesnede yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80846-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="80846-382">Bir sırayı alır ve 'MessageInfo' iletisi ekler kod şöyledir:</span><span class="sxs-lookup"><span data-stu-id="80846-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

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

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="80846-383">Sonraki iletiyi sıradan çıkarmak nasıl</span><span class="sxs-lookup"><span data-stu-id="80846-383">How to de-queue at the next message</span></span>
<span data-ttu-id="80846-384">Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır.</span><span class="sxs-lookup"><span data-stu-id="80846-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="80846-385">Çağırdığınızda [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) bir kuyruktaki bir sonraki iletiyi elde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80846-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="80846-386">**GetMessage**’dan dönen bir ileti bu kuyruktaki kod okuyan iletilere karşı görünmez olur.</span><span class="sxs-lookup"><span data-stu-id="80846-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="80846-387">İletiyi kuyruktan kaldırmayı tamamlamak için de çağırmanız gerekir [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80846-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="80846-388">Bir iletinin iki adımlı kaldırılma süreci, donanım veya yazılım arızasından dolayı kodunuzun bir iletiyi işleyememesi durumunda kodunuzun başka bir örneğinin aynı iletiyi alıp yeniden denemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="80846-389">Kodunuz ileti işlendikten hemen sonra **DeleteMessage**’ı çağırır.</span><span class="sxs-lookup"><span data-stu-id="80846-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

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

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="80846-390">Azure dosya paylaşımlarının ve dosyaların yönetme</span><span class="sxs-lookup"><span data-stu-id="80846-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="80846-391">Azure File storage standart SMB protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="80846-392">Microsoft Azure virtual machines ve cloud services bağlı paylaşımlar üzerinden uygulama bileşenleri arasında dosya verileri paylaşabilir ve şirket içi uygulamalar dosya depolama API'si veya Azure PowerShell üzerinden dosya verilerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="80846-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="80846-393">Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](storage-dotnet-how-to-use-files.md) ve [dosya hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="80846-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="80846-394">Nasıl ayarlanacağı ve sorgu depolama analizi</span><span class="sxs-lookup"><span data-stu-id="80846-394">How to set and query storage analytics</span></span>
<span data-ttu-id="80846-395">Kullanabileceğiniz [Azure depolama çözümlemeleri](storage-analytics.md) Azure depolama hesaplarınız için ölçümleri toplamak ve verileri depolama hesabınıza gönderilen istekleri hakkında günlüğe kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="80846-395">You can use [Azure Storage Analytics](storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="80846-396">Depolama ölçümleri, bir depolama hesabı ve tanılamak ve depolama hesabınız ile ilgili sorunları gidermek için depolama oturum durumunu izlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="80846-397">Azure Portalı'nı veya Windows PowerShell veya program aracılığıyla depolama istemci kitaplığı kullanarak izleme yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="80846-398">Depolama günlük sunucu tarafı olur ve depolama hesabınızdaki hem başarılı hem başarısız istekler için kayıt ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="80846-399">Bu günlükler, okuma, yazma ve silme işlemleri tablolarınızı, kuyruklar ve BLOB'lar yanı sıra nedeniyle başarısız istekler için karşı ayrıntılarını görmek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="80846-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="80846-400">Etkinleştirmek ve PowerShell kullanarak depolama ölçüm verilerini görüntüleme hakkında bilgi almak için bkz: [PowerShell kullanarak depolama ölçümlerini etkinleştirme](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="80846-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="80846-401">Etkinleştirmek ve PowerShell kullanarak depolama günlüğü verilerini alma hakkında bilgi almak için bkz: [PowerShell kullanarak depolama günlüğü etkinleştirme](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) ve [depolama günlüğü günlük verilerinizi bulma](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="80846-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="80846-402">Depolama sorunları gidermek için depolama ölçümleri ve depolama oturum kullanma hakkında ayrıntılı bilgi için bkz: [izleme, Diagnosing ve sorun giderme Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="80846-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="80846-403">Paylaşılan erişim imzası (SAS) ve depolanan erişim ilkesi yönetme</span><span class="sxs-lookup"><span data-stu-id="80846-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="80846-404">Paylaşılan erişim imzalar, Azure Storage kullanarak herhangi bir uygulama için güvenlik modelinin önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="80846-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="80846-405">Bunlar, depolama hesabınıza sınırlı izinlere hesap anahtarı olmamalıdır istemcilere sağlamak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="80846-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="80846-406">Varsayılan olarak, yalnızca depolama hesabı sahibi BLOB'lar, tablolar ve Kuyruklar o hesabı içinde erişebilir.</span><span class="sxs-lookup"><span data-stu-id="80846-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="80846-407">Hizmet veya uygulama bu kaynakları diğer istemciler için kullanılabilir erişim anahtarınızı paylaşmadan olması gerekiyorsa, üç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="80846-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="80846-408">Kapsayıcı ve bloblarını anonim okuma erişimine izin vermek üzere bir kapsayıcının izinlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="80846-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="80846-409">Bu tablo veya sıralara izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="80846-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="80846-410">Verir kapsayıcıları, blobları, kuyruklar ve tablolar için erişim haklarını belirli bir zaman aralığı için sınırlı bir paylaşılan erişim imzası kullanın.</span><span class="sxs-lookup"><span data-stu-id="80846-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="80846-411">Ek bir paylaşılan erişim imzaları bir kapsayıcıyı veya bloblarını için bir kuyruk için veya bir tablo üzerinde denetim düzeyini elde etmek için bir saklı erişim ilkesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="80846-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="80846-412">Bundan sonra iptal etmek için verilen veya depolanmış erişim ilkesi başlangıç saati, sona erme saati veya imza için izinleri değiştirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="80846-413">Paylaşılan erişim imzası iki forms biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="80846-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="80846-414">**Geçici SAS**: geçici bir SAS, başlangıç zamanı, bitiş zamanı, oluşturduğunuzda ve SAS izinlerini tüm belirtilen SAS URİ'si üzerinde.</span><span class="sxs-lookup"><span data-stu-id="80846-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="80846-415">Bu tür bir SAS oluşturulabilir bir kapsayıcı, blob, tablo veya kuyruğu ve iptal edilebilir olmayan.</span><span class="sxs-lookup"><span data-stu-id="80846-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="80846-416">**Saklı erişim ilkesi ile SAS**: bir saklı erişim ilkesi kaynak kapsayıcı bir blob kapsayıcısını, tablo veya kuyruğu - tanımlanmış ve bir veya daha fazla paylaşılan erişim imzaları kısıtlamalarını yönetmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="80846-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="80846-417">Bir SAS depolanmış erişim ilkesi ile ilişkilendirdiğinizde, SAS kısıtlamaları - başlangıç saati, sona erme saati ve saklı erişim ilkesi için tanımlanan izinleri - devralır.</span><span class="sxs-lookup"><span data-stu-id="80846-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="80846-418">Bu tür bir SAS iptal edilebilir.</span><span class="sxs-lookup"><span data-stu-id="80846-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="80846-419">Daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları (SAS)](storage-dotnet-shared-access-signature-part-1.md) ve [kapsayıcılar ve bloblar için anonim okuma erişimini yönetme](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="80846-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="80846-420">Sonraki bölümlerde, Azure tablolar için paylaşılan erişim imzası belirteci ve saklı erişim ilkesinin nasıl oluşturulacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="80846-421">Azure PowerShell benzer cmdlet'lerini kapsayıcıları, BLOB'ları ve kuyrukları de sağlar.</span><span class="sxs-lookup"><span data-stu-id="80846-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="80846-422">Bu bölümde komut dosyalarını çalıştırmak için karşıdan [Azure PowerShell sürüm 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="80846-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="80846-423">Bir ilke tabanlı paylaşılan erişim imzası belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="80846-424">Yeni bir saklı erişim ilkesi oluşturmak için New-AzureStorageTableStoredAccessPolicy cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="80846-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="80846-425">Ardından, çağıran [yeni AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) bir Azure Storage tablo için yeni bir ilke tabanlı paylaşılan erişim imzası belirteci oluşturmak için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80846-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="80846-426">Geçici (istenmeden olmayan) bir paylaşılan erişim imzası belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="80846-427">Kullanım [yeni AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet yeni bir geçici (istenmeden olmayan) paylaşılan erişim imzası belirteci için bir Azure depolama tablosu oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="80846-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="80846-428">Saklı erişim ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="80846-428">How to create a stored access policy</span></span>
<span data-ttu-id="80846-429">Bir Azure depolama tablosu için yeni bir saklı erişim ilkesi oluşturmak için New-AzureStorageTableStoredAccessPolicy cmdlet'i kullanın:</span><span class="sxs-lookup"><span data-stu-id="80846-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="80846-430">Bir saklı erişim ilkesi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="80846-430">How to update a stored access policy</span></span>
<span data-ttu-id="80846-431">Bir Azure depolama tablosu için varolan bir depolanmış erişim ilkesi güncelleştirmek için Set-AzureStorageTableStoredAccessPolicy cmdlet'ini kullanın:</span><span class="sxs-lookup"><span data-stu-id="80846-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="80846-432">Bir saklı erişim ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="80846-432">How to delete a stored access policy</span></span>
<span data-ttu-id="80846-433">Bir Azure Storage tablosunda depolanan erişim ilkesini silmek için Remove-AzureStorageTableStoredAccessPolicy cmdlet'ini kullanın:</span><span class="sxs-lookup"><span data-stu-id="80846-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="80846-434">ABD hükümeti ve Azure Çin için Azure Storage kullanma</span><span class="sxs-lookup"><span data-stu-id="80846-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="80846-435">Bir Azure ortamı Microsoft Azure, bağımsız bir dağıtımını olduğu gibi [US government Azure kamu](https://azure.microsoft.com/features/gov/), [genel Azure AzureCloud](https://portal.azure.com), ve [AzureChinaCloud Azure Çin'de 21Vianet tarafından işletilen](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="80846-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="80846-436">ABD hükümeti ve Azure Çin için yeni Azure ortamlarını dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="80846-437">Azure Storage ile AzureChinaCloud kullanmak için AzureChinaCloud ile ilişkili bir depolama bağlam oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="80846-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="80846-438">Başlamanıza yardımcı olmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="80846-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="80846-439">Çalıştırma [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) kullanılabilir Azure ortamları görmek için cmdlet:</span><span class="sxs-lookup"><span data-stu-id="80846-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="80846-440">Windows PowerShell için Azure Çin Hesap Ekle:</span><span class="sxs-lookup"><span data-stu-id="80846-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="80846-441">AzureChinaCloud hesabınız için bir depolama bağlam oluşturun:</span><span class="sxs-lookup"><span data-stu-id="80846-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="80846-442">Azure Storage ile kullanmak için [ABD Azure kamu](https://azure.microsoft.com/features/gov/), yeni bir ortam tanımlayın ve ardından yeni bir depolama bağlamı ile bu ortamı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="80846-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="80846-443">Çalıştırma [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) kullanılabilir Azure ortamları görmek için cmdlet:</span><span class="sxs-lookup"><span data-stu-id="80846-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="80846-444">Windows PowerShell için Azure ABD devlet kurumları Hesap Ekle:</span><span class="sxs-lookup"><span data-stu-id="80846-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="80846-445">AzureUSGovernment hesabınız için bir depolama bağlam oluşturun:</span><span class="sxs-lookup"><span data-stu-id="80846-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="80846-446">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="80846-446">For more information, see:</span></span>

* <span data-ttu-id="80846-447">[Microsoft Azure kamu Geliştirici Kılavuzu](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="80846-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="80846-448">Bir uygulama Çin hizmette oluştururken farklar genel bakış</span><span class="sxs-lookup"><span data-stu-id="80846-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="80846-449">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="80846-449">Next Steps</span></span>
<span data-ttu-id="80846-450">Bu kılavuzda, Azure Storage Azure PowerShell ile yönetme öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="80846-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="80846-451">Bazı ilgili makaleler ve bunlarla ilgili daha fazla bilgi edinmek için kaynaklar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="80846-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="80846-452">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="80846-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="80846-453">Azure Storage PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="80846-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="80846-454">Windows PowerShell başvurusu</span><span class="sxs-lookup"><span data-stu-id="80846-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

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
