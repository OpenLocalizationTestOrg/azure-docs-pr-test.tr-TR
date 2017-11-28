---
<span data-ttu-id="ff8fa-101">Başlık: aaa "PowerShell: Azure Hdınsight kümesini Data Lake Store eklenti depolama ile | Microsoft Docs"Hizmetleri: data lake-deposu, hdınsight documentationcenter: '' Yazar: nitinme Yöneticisi: jhubbard Düzenleyicisi: cgronlun</span><span class="sxs-lookup"><span data-stu-id="ff8fa-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="ff8fa-102">MS.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data lake store ms.devlang: na ms.topic: ms.tgt_pltfrm makale: na ms.workload: büyük veri ms.date: 06/08/2017 ms.author: nitinme</span><span class="sxs-lookup"><span data-stu-id="ff8fa-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ff8fa-103">(Azure PowerShell toocreate Hdınsight kümesi Data Lake Store ile ek depolama alanı olarak) kullanın</span><span class="sxs-lookup"><span data-stu-id="ff8fa-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff8fa-104">Portalı kullanma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="ff8fa-105">(Varsayılan depolama için) PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="ff8fa-106">PowerShell kullanarak (için ek depolama alanı)</span><span class="sxs-lookup"><span data-stu-id="ff8fa-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="ff8fa-107">Kaynak Yöneticisi'ni kullanma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="ff8fa-108">Azure Data Lake Store ile toouse Azure PowerShell tooconfigure bir Hdınsight kümesi nasıl öğrenin **ek depolama alanı olarak**.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="ff8fa-109">Azure Data Lake Store varsayılan depolama toocreate bir Hdınsight nasıl kümesi ile ilgili yönergeler için bkz: [varsayılan depolama olarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ff8fa-110">Hdınsight kümesi için ek depolama alanı olarak toouse Azure Data Lake Store kullanacaksanız, bu makalede anlatıldığı gibi hello küme oluştururken bunu yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="ff8fa-111">Ek depolama alanı tooan Azure Data Lake Store ekleme olan bir Hdınsight kümesine bir karmaşık bir işlem yatkın tooerrors ise.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="ff8fa-112">Desteklenen küme türleri için Data Lake Store varsayılan depolama veya ek depolama alanı hesabı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="ff8fa-113">Data Lake Store ek depolama alanı olarak kullanıldığında, hello varsayılan depolama hesabı hello kümeleri için Azure Storage Blobları (WASB) çıkarılsın ve hello küme ilgili dosyalar (örneğin, günlükleri, vb.) hello veriler toohello varsayılan depolama yazılmış, bir Data Lake Store hesabında tooprocess depolanabilir istiyor.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="ff8fa-114">Data Lake Store ek depolama alanı hesabı olarak kullanarak performans veya hello özelliği tooread/yazma toohello depolama hello kümeden etkilemez.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="ff8fa-115">Hdınsight küme depolaması için Data Lake Store kullanma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="ff8fa-116">Hdınsight Data Lake Store ile kullanmak için bazı önemli noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="ff8fa-117">Seçenek toocreate Hdınsight kümeleri erişimi olan tooData Lake deposu ek depolama alanı olarak Hdınsight sürüm 3.2, 3.4, 3.5 ve 3.6 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="ff8fa-118">Hdınsight yapılandırma PowerShell kullanarak Data Lake Store ile toowork hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="ff8fa-119">Bir Azure Data Lake deposu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="ff8fa-120">Rol tabanlı kimlik doğrulaması için ayarlama tooData Lake deposuna erişim</span><span class="sxs-lookup"><span data-stu-id="ff8fa-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="ff8fa-121">Kimlik doğrulama tooData Lake Store ile Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="ff8fa-122">Test işi hello kümede çalışan</span><span class="sxs-lookup"><span data-stu-id="ff8fa-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff8fa-123">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ff8fa-123">Prerequisites</span></span>
<span data-ttu-id="ff8fa-124">Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="ff8fa-125">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-125">**An Azure subscription**.</span></span> <span data-ttu-id="ff8fa-126">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ff8fa-127">**Azure PowerShell 1.0 veya üstü**.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="ff8fa-128">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ff8fa-129">**Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-129">**Windows SDK**.</span></span> <span data-ttu-id="ff8fa-130">Şuradan yükleyebilirsiniz [burada](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="ff8fa-131">Bu toocreate bir güvenlik sertifikası kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="ff8fa-132">**Azure Active Directory hizmet asıl**.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="ff8fa-133">Bu öğreticideki adımlardan hakkında yönergeler sağlayan bir hizmet sorumlusu Azure AD'de toocreate.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="ff8fa-134">Ancak, bir Azure AD yönetici toobe mümkün toocreate bir hizmet sorumlusu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="ff8fa-135">Azure AD Yöneticiyseniz, bu önkoşulu atlayın ve hello eğitici devam edin.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="ff8fa-136">**Azure AD Yönetici değilseniz**, mümkün tooperform hello adımları gerekli toocreate bir hizmet sorumlusu olmaz.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="ff8fa-137">Data Lake Store ile Hdınsight kümesi oluşturmadan önce böyle bir durumda, Azure AD yöneticinizin önce bir hizmet sorumlusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="ff8fa-138">Ayrıca, hello hizmet sorumlusu bir sertifika kullanılarak konusunda açıklandığı gibi oluşturulmalıdır [sertifikayla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="ff8fa-139">Bir Azure Data Lake deposu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="ff8fa-140">Bu adımları toocreate bir Data Lake Store izleyin.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="ff8fa-141">Masaüstünüzde yeni bir Azure PowerShell penceresi açın ve aşağıdaki kod parçacığında hello girin.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="ff8fa-142">' De, istendiğinde toolog emin yaptığınızda, bir hello Abonelik Yöneticisi/sahibi oturum açın:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="ff8fa-143">Çok benzer bir hata alırsanız,`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` hello Data Lake Store kaynak sağlayıcısı kaydedilirken aboneliğinizi Azure Data Lake Store için Güvenilenler listesine değil mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="ff8fa-144">Bunlar izleyerek, Azure aboneliğinizin Data Lake Store genel önizlemesi için etkinleştirdiğinizden emin olun [yönergeleri](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="ff8fa-145">Azure Data Lake Store hesabı, bir Azure Kaynak Grubu ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="ff8fa-146">Azure Kaynak Grubu oluşturma işlemiyle başlayın.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="ff8fa-147">Bu gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="ff8fa-148">Bir Azure Data Lake Store hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="ff8fa-149">Merhaba hesabı, belirttiğiniz ad yalnızca küçük harf ve sayı içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="ff8fa-150">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-150">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. <span data-ttu-id="ff8fa-151">Bazı örnek veri tooAzure Data Lake karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="ff8fa-152">Bu, daha sonra hello veri bir Hdınsight kümeden erişilebilir olduğunu Bu makale tooverify kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="ff8fa-153">Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="ff8fa-154">Rol tabanlı kimlik doğrulaması için ayarlama tooData Lake deposuna erişim</span><span class="sxs-lookup"><span data-stu-id="ff8fa-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="ff8fa-155">Her Azure aboneliği bir Azure Active Directory ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="ff8fa-156">İlk kullanıcı ve hello Azure Klasik portalında veya Azure Kaynak Yöneticisi API'si kullanılarak hello aboneliğin kaynaklara services, Azure Active Directory ile kimliğini doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="ff8fa-157">Erişim tooAzure abonelikleri ve Hizmetleri Azure kaynak üzerinde hello uygun rol atama tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="ff8fa-158">Hizmetler için bir hizmet sorumlusu hello Azure Active Directory (AAD) hello hizmetinde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="ff8fa-159">Bu bölümde nasıl toogrant bir uygulama hizmeti, Azure kaynak (Merhaba daha önce oluşturduğunuz Azure Data Lake Store hesabı) erişim tooan Hdınsight gibi anlatılacaktır Merhaba uygulaması için bir hizmet sorumlusu oluşturma ve Azure aracılığıyla rolleri toothat atayarak PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="ff8fa-160">tooset Active Directory kimlik doğrulaması için Azure Data Lake yukarı hello aşağıdaki görevleri gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="ff8fa-161">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="ff8fa-162">Uygulama Azure Active Directory ve bir hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="ff8fa-163">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-163">Create a self-signed certificate</span></span>
<span data-ttu-id="ff8fa-164">Olduğundan emin olun [Windows SDK](https://dev.windows.com/en-us/downloads) hello işlemine devam etmeden bu bölümdeki adımları önce yüklü.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="ff8fa-165">Ayrıca bir dizin gibi oluşturduğunuz gerekir **C:\mycertdir**, hello sertifika oluşturulacağı.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="ff8fa-166">Merhaba PowerShell penceresinden Windows SDK'yı yüklediğiniz toohello konumuna gidin (genellikle `C:\Program Files (x86)\Windows Kits\10\bin\x86` ve hello [MakeCert] [ makecert] yardımcı programı toocreate otomatik olarak imzalanan bir sertifika ve bir özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="ff8fa-167">Merhaba aşağıdaki komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="ff8fa-168">İstendiğinde tooenter hello özel anahtar parolası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="ff8fa-169">Merhaba komutu başarıyla, görmeniz gerekir yürütüldükten sonra bir **CertFile.cer** ve **mykey.pvk** , belirtilen hello sertifika dizininde.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="ff8fa-170">Kullanım hello [Pvk2Pfx] [ pvk2pfx] yardımcı programı tooconvert hello .pvk ve .cer dosya o MakeCert oluşturulan tooa .pfx dosyası.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="ff8fa-171">Merhaba aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="ff8fa-172">İstendiğinde daha önce belirttiğiniz hello özel anahtar parolası girin.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="ff8fa-173">Merhaba hello için belirttiğiniz değere **-SAS** parametredir hello .pfx dosyasıyla ilişkili hello parola.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="ff8fa-174">Merhaba komutu başarıyla tamamlandıktan sonra belirtilen hello sertifika dizininde CertFile.pfx görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="ff8fa-175">Bir Azure Active Directory ve bir hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="ff8fa-176">Bu bölümde, bir Azure Active Directory uygulaması için başlangıç adımları toocreate bir hizmet sorumlusu gerçekleştirmek, bir rol toohello hizmet sorumlusu atayın ve bir sertifika sağlayarak hello hizmet sorumlusu kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="ff8fa-177">Aşağıdaki komutları toocreate hello Azure Active Directory'de bir uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="ff8fa-178">Cmdlet'leri hello PowerShell konsol penceresinde aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="ff8fa-179">Merhaba belirttiğiniz emin hello değeri **- DisplayName** özelliği benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="ff8fa-180">Ayrıca, değerlerini hello **- giriş sayfası** ve **- IdentiferUris** yer tutucu değerlerini olan ve olmayan doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="ff8fa-181">Merhaba uygulama kimliğini kullanarak bir hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="ff8fa-182">Merhaba hizmet asıl erişim toohello Data Lake Store klasörü ve hello Hdınsight kümeden erişecek hello dosya verin.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="ff8fa-183">Aşağıdaki Hello parçacığı Data Lake Store (Merhaba örnek veri dosyasını kopyaladığınız) hesap ve dosyasının kendisini hello hello toohello kökündeki erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ff8fa-184">Hdınsight Linux kümesi Data Lake Store ile ek depolama alanı olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="ff8fa-185">Bu bölümde, bir Hdınsight Hadoop Linux kümesi Data Lake Store ile ek depolama alanı olarak oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="ff8fa-186">Bu sürüm için hello hello Hdınsight kümesi ve hello Data Lake Store olmalıdır aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="ff8fa-187">Merhaba abonelik Kiracı kimliği alma Başlat</span><span class="sxs-lookup"><span data-stu-id="ff8fa-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="ff8fa-188">Daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="ff8fa-189">Bu sürüm için Hadoop kümesi için Data Lake Store yalnızca ek depolama alanı hello küme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="ff8fa-190">Merhaba varsayılan depolama hello Azure storage bloblarında (WASB) olmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="ff8fa-191">Bu nedenle, ilk hello depolama hesabı ve depolama kapsayıcılarına hello kümesi için gerekli oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="ff8fa-192">Merhaba Hdınsight kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="ff8fa-193">Cmdlet aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="ff8fa-194">Merhaba cmdlet'i başarıyla tamamlandıktan sonra hello küme ayrıntıları listeleyen bir çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="ff8fa-195">Merhaba Hdınsight küme toouse hello Data Lake Store üzerinde test işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="ff8fa-196">Hdınsight kümesi yapılandırdıktan sonra o hello Hdınsight test işleri hello küme tootest üzerinde çalıştırabilirsiniz küme, Data Lake Store erişebilir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="ff8fa-197">toodo bu nedenle, biz önceki tooyour Data Lake Store karşıya hello örnek verileri kullanarak bir tablo oluşturur bir örnek Hive işi çalışır.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="ff8fa-198">Bu bölümde Hdınsight Linux küme oluşturduğunuz ve hello örnek Hive sorgusu çalıştırma hello SSH olur.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="ff8fa-199">Bir Windows istemci tooSSH hello kümesine kullanıyorsanız bkz [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ff8fa-200">Merhaba kümesine Linux istemci tooSSH kullanıyorsanız, bkz: [Linux Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ff8fa-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="ff8fa-201">Bağlandıktan sonra komutu aşağıdaki hello kullanarak hello Hive CLI başlatın:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="ff8fa-202">Merhaba, CLI kullanarak girin deyimleri toocreate adlı yeni bir tablo aşağıdaki hello **taşıtlardan** hello Data Lake Store hello örnek verileri kullanarak:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="ff8fa-203">Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff8fa-203">You should see an output similar toohello following:</span></span>

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="ff8fa-204">HDFS komutları kullanarak erişim Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff8fa-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="ff8fa-205">Merhaba Hdınsight küme toouse Data Lake Store yapılandırdıktan sonra hello HDFS Kabuk komutları tooaccess hello deposu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="ff8fa-206">Bu bölümde Hdınsight Linux küme oluşturduğunuz ve hello HDFS komutları çalıştırmak hello SSH olur.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="ff8fa-207">Bir Windows istemci tooSSH hello kümesine kullanıyorsanız bkz [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ff8fa-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ff8fa-208">Merhaba kümesine Linux istemci tooSSH kullanıyorsanız, bkz: [Linux Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ff8fa-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="ff8fa-209">Bağlantı kurulduktan sonra aşağıdaki hello Data Lake Store, HDFS filesystem komutu toolist hello dosyaları hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="ff8fa-210">Bu, önceki toohello Data Lake Store karşıya hello dosya listelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="ff8fa-211">Merhaba de kullanabilirsiniz `hdfs dfs -put` tooupload bazı dosyaları toohello Data Lake Store komutunu ve ardından `hdfs dfs -ls` tooverify hello dosyaları başarıyla karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff8fa-212">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff8fa-212">See Also</span></span>
* [<span data-ttu-id="ff8fa-213">Portal: Hdınsight küme toouse Data Lake Store oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8fa-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
