---
title: "aaaCreate Hdınsight kümeleri Data Lake Store ile varsayılan depolama alanı olarak PowerShell kullanarak | Microsoft Docs"
description: "Azure PowerShell toocreate kullanın ve Hdınsight kümeleri Azure Data Lake Store ile kullanma"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="612ae-103">Varsayılan depolama alanı olarak Data Lake Store ile PowerShell kullanarak Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="612ae-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="612ae-104">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="612ae-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="612ae-105">(Varsayılan depolama için) PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="612ae-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="612ae-106">PowerShell (için ek depolama alanı) kullanın</span><span class="sxs-lookup"><span data-stu-id="612ae-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="612ae-107">Kaynak Yöneticisi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="612ae-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="612ae-108">Varsayılan depolama alanı olarak Azure Data Lake Store ile nasıl toouse Azure PowerShell tooconfigure Azure Hdınsight kümeleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="612ae-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="612ae-109">Ek depolama alanı olarak Data Lake Store ile bir Hdınsight kümesi oluşturma ile ilgili yönergeler için bkz: [ek depolama alanı olarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="612ae-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="612ae-110">Hdınsight Data Lake Store ile kullanmak için bazı önemli noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="612ae-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="612ae-111">Merhaba seçeneği toocreate Hdınsight kümeleri erişimi olan Hdınsight sürüm 3.5 ve 3.6 tooData Lake deposu varsayılan depolama olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="612ae-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="612ae-112">Hdınsight kümeleri ile Merhaba seçeneği toocreate erişim tooData Lake deposu varsayılan depolama olarak *kullanılamaz* Hdınsight Premium kümeleri için.</span><span class="sxs-lookup"><span data-stu-id="612ae-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="612ae-113">PowerShell kullanarak Data Lake Store ile tooconfigure Hdınsight toowork hello sonraki beş bölümlerdeki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="612ae-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="612ae-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="612ae-114">Prerequisites</span></span>
<span data-ttu-id="612ae-115">Bu öğreticiye başlamadan önce hello aşağıdaki gereksinimleri karşıladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="612ae-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="612ae-116">**Bir Azure aboneliği**: çok Git[alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="612ae-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="612ae-117">**Azure PowerShell 1.0 veya büyük**: bkz [nasıl tooinstall ve PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="612ae-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="612ae-118">**Windows Yazılım Geliştirme Seti (SDK)**: tooinstall Windows SDK'sı Git çok[indirir ve Windows 10 için Araçlar](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="612ae-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="612ae-119">Merhaba SDK kullanılan toocreate bir güvenlik sertifikası ' dir.</span><span class="sxs-lookup"><span data-stu-id="612ae-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="612ae-120">**Azure Active Directory hizmet asıl**: Bu öğreticide açıklar nasıl toocreate Azure Active Directory'de (Azure AD) bir hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="612ae-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="612ae-121">Ancak, bir hizmet sorumlusu toocreate olmalıdır Azure AD yönetici.</span><span class="sxs-lookup"><span data-stu-id="612ae-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="612ae-122">Bir yöneticiyseniz, bu önkoşulu atlayın ve hello eğitici devam edin.</span><span class="sxs-lookup"><span data-stu-id="612ae-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="612ae-123">Yalnızca, Azure AD yöneticisiyseniz, bir hizmet asıl oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="612ae-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="612ae-124">Azure AD yöneticinizin Data Lake Store ile Hdınsight kümesi oluşturmadan önce bir hizmet asıl oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="612ae-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="612ae-125">Merhaba hizmet sorumlusu bir sertifikayla açıklandığı şekilde oluşturulmalıdır [sertifikayla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="612ae-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="612ae-126">Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="612ae-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="612ae-127">bir Data Lake Store hesabı toocreate hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="612ae-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="612ae-128">Masaüstünüzde bir PowerShell penceresi açın ve aşağıdaki hello kod parçacıkları girin.</span><span class="sxs-lookup"><span data-stu-id="612ae-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="612ae-129">İçinde oturum açma hello abonelik yöneticileri veya sahipleri biri olarak istendiğinde toosign olduğunda.</span><span class="sxs-lookup"><span data-stu-id="612ae-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="612ae-130">Merhaba Data Lake Store kaynak sağlayıcısı kaydetme ve çok benzer bir hata alırsanız`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, aboneliğinizin Data Lake Store için Güvenilenler listesine olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="612ae-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="612ae-131">tooenable hello Data Lake Store genel önizlemesi, Azure aboneliğinizin hello yönergeleri izleyin [hello Azure portal kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="612ae-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="612ae-132">Bir Azure kaynak grubu ile ilişkili bir Data Lake Store hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="612ae-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="612ae-133">Bir kaynak grubu oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="612ae-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="612ae-134">Bu gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="612ae-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="612ae-135">Bir Data Lake Store hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="612ae-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="612ae-136">Merhaba hesabı, belirttiğiniz ad yalnızca küçük harf ve sayı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="612ae-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="612ae-137">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="612ae-137">You should see an output like hello following:</span></span>

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

4. <span data-ttu-id="612ae-138">Data Lake Store varsayılan depolama alanı olarak kullanarak küme oluşturma sırasında bir kök yolu toowhich hello kümeye özgü dosyalar kopyalanır toospecify gerektirir.</span><span class="sxs-lookup"><span data-stu-id="612ae-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="612ae-139">toocreate olan bir kök yolu **/kümeleri/hdiadlcluster** hello parçacığında, hello aşağıdaki cmdlet'leri kullanın:</span><span class="sxs-lookup"><span data-stu-id="612ae-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="612ae-140">Rol tabanlı kimlik doğrulaması için ayarlama tooData Lake deposuna erişim</span><span class="sxs-lookup"><span data-stu-id="612ae-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="612ae-141">Her Azure aboneliği bir Azure AD varlıkla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="612ae-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="612ae-142">İlk kullanıcılar ve kullanarak abonelik kaynaklarına erişim Azure portalı hello veya Azure Kaynak Yöneticisi API'si hello hizmetler Azure AD ile kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="612ae-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="612ae-143">Erişim tooAzure abonelikleri ve Hizmetleri Azure kaynak üzerinde hello uygun rol atama tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="612ae-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="612ae-144">Hizmetler için bir hizmet sorumlusu Azure AD'de hello hizmeti tanımlar.</span><span class="sxs-lookup"><span data-stu-id="612ae-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="612ae-145">Bu bölümde, nasıl toogrant bir uygulama hizmeti, Hdınsight gibi erişim tooan Azure kaynak (Merhaba daha önce oluşturduğunuz Data Lake Store hesabı) gösterir.</span><span class="sxs-lookup"><span data-stu-id="612ae-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="612ae-146">Bir hizmet asıl hello uygulaması oluşturma ve PowerShell aracılığıyla rolleri tooit atayarak bunu.</span><span class="sxs-lookup"><span data-stu-id="612ae-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="612ae-147">Active Directory kimlik doğrulaması için Azure Data Lake yukarı tooset iki bölüm şu hello hello görevleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="612ae-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="612ae-148">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="612ae-148">Create a self-signed certificate</span></span>
<span data-ttu-id="612ae-149">Olduğundan emin olun [Windows SDK](https://dev.windows.com/en-us/downloads) hello işlemine devam etmeden bu bölümdeki adımları önce yüklü.</span><span class="sxs-lookup"><span data-stu-id="612ae-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="612ae-150">Ayrıca bir dizin gibi oluşturduğunuz gerekir *C:\mycertdir*burada hello sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="612ae-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="612ae-151">Merhaba PowerShell penceresinden Windows SDK'yı yüklediğiniz toohello konumuna gidin (genellikle *C:\Program Files (x86) \Windows Kits\10\bin\x86*) ve hello [MakeCert] [ makecert] yardımcı programı toocreate otomatik olarak imzalanan bir sertifika ve özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="612ae-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="612ae-152">Merhaba aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="612ae-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="612ae-153">İstendiğinde tooenter hello özel anahtar parolası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="612ae-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="612ae-154">Merhaba komutu başarıyla yürütüldükten sonra görmelisiniz **CertFile.cer** ve **mykey.pvk** belirttiğiniz hello sertifika dizininde.</span><span class="sxs-lookup"><span data-stu-id="612ae-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="612ae-155">Kullanım hello [Pvk2Pfx] [ pvk2pfx] yardımcı programı tooconvert hello .pvk ve .cer dosya o MakeCert oluşturulan tooa .pfx dosyası.</span><span class="sxs-lookup"><span data-stu-id="612ae-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="612ae-156">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="612ae-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="612ae-157">İstendiğinde, daha önce belirttiğiniz hello özel anahtar parolası girin.</span><span class="sxs-lookup"><span data-stu-id="612ae-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="612ae-158">Merhaba hello için belirttiğiniz değere **-SAS** parametredir hello .pfx dosyasıyla ilişkili hello parola.</span><span class="sxs-lookup"><span data-stu-id="612ae-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="612ae-159">Merhaba komutu başarıyla tamamlandıktan sonra da görmeniz gerekir bir **CertFile.pfx** belirttiğiniz hello sertifika dizininde.</span><span class="sxs-lookup"><span data-stu-id="612ae-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="612ae-160">Azure AD oluşturmak ve bir hizmet sorumlusu</span><span class="sxs-lookup"><span data-stu-id="612ae-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="612ae-161">Bu bölümde, Azure AD uygulaması için bir hizmet sorumlusu oluşturmak, bir rol toohello hizmet sorumlusu atamak ve bir sertifika sağlayarak hello hizmet sorumlusu kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="612ae-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="612ae-162">toocreate uygulamanın Azure AD'de hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="612ae-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="612ae-163">Cmdlet'leri hello PowerShell konsol penceresinde aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="612ae-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="612ae-164">Merhaba belirttiğiniz hello değeri emin olun **- DisplayName** özelliği benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="612ae-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="612ae-165">Merhaba değerlerini **- giriş sayfası** ve **- IdentiferUris** yer tutucu değerlerini olan ve olmayan doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="612ae-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="612ae-166">Merhaba uygulama kimliğini kullanarak bir hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="612ae-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="612ae-167">Merhaba hizmet asıl erişim toohello Data Lake Store kök ve daha önce belirtilen hello kök yolu tüm hello klasörlerde verin.</span><span class="sxs-lookup"><span data-stu-id="612ae-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="612ae-168">Hello aşağıdaki cmdlet'leri kullanın:</span><span class="sxs-lookup"><span data-stu-id="612ae-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="612ae-169">Hdınsight Linux kümesi Data Lake Store ile Merhaba varsayılan depolama alanı olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="612ae-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="612ae-170">Bu bölümde, bir Hdınsight Hadoop Linux kümesi hello varsayılan depolama alanı olarak Data Lake Store ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="612ae-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="612ae-171">Bu sürüm için Hdınsight kümesi hello ve Data Lake Store hello olmalıdır aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="612ae-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="612ae-172">Merhaba abonelik Kiracı Kimliği almak ve daha sonra toouse saklayın.</span><span class="sxs-lookup"><span data-stu-id="612ae-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="612ae-173">Merhaba Hdınsight kümesi cmdlet'leri aşağıdaki hello kullanarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="612ae-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="612ae-174">Merhaba cmdlet'i başarıyla tamamlandıktan sonra hello küme ayrıntılarını listeler bir çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="612ae-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="612ae-175">Merhaba Hdınsight küme toouse Data Lake Store üzerinde test işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="612ae-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="612ae-176">Hdınsight kümesi yapılandırdıktan sonra Data Lake Store erişebildiğinizi tooensure üzerinde test işleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="612ae-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="612ae-177">toodo Data Lake Store'da kullanılabilir zaten hello örnek verileri kullanan bir tablo, bir örnek Hive işi toocreate çalıştırmak  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="612ae-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="612ae-178">Bu bölümdeki hello oluşturduğunuz Hdınsight Linux kümesi içine güvenli Kabuk (SSH) bağlantısı ve sonra bir örnek Hive sorgusunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="612ae-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="612ae-179">Bir Windows istemci toomake hello kümesine bir SSH bağlantısı kullanıyorsanız, bkz: [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="612ae-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="612ae-180">Linux istemci toomake hello kümesine bir SSH bağlantısı kullanıyorsanız, bkz: [Linux Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="612ae-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="612ae-181">Merhaba bağlantı yaptıktan sonra komutu aşağıdaki hello kullanarak hello Hive komut satırı arabirimi (CLI) başlatın:</span><span class="sxs-lookup"><span data-stu-id="612ae-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="612ae-182">Kullanım hello CLI tooenter hello deyimleri toocreate adlı yeni bir tablo aşağıdaki **taşıtlardan** Data Lake Store'da hello örnek verileri kullanarak:</span><span class="sxs-lookup"><span data-stu-id="612ae-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="612ae-183">Merhaba SSH konsolda hello sorgu çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="612ae-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="612ae-184">Merhaba yolu toohello örnek CREATE TABLE komutu önceki hello verisinde `adl:///example/data/`, burada `adl:///` hello küme köküdür.</span><span class="sxs-lookup"><span data-stu-id="612ae-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="612ae-185">Bu öğreticide belirtilen hello küme kök Hello örneği hello komuttur `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="612ae-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="612ae-186">Merhaba kısa alternatif kullanın veya hello tam yolunu toohello küme kök sağlayın.</span><span class="sxs-lookup"><span data-stu-id="612ae-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="612ae-187">HDFS komutlarını kullanarak Data Lake Store'a erişme</span><span class="sxs-lookup"><span data-stu-id="612ae-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="612ae-188">Merhaba Hdınsight küme toouse Data Lake Store yapılandırdıktan sonra Hadoop dağıtılmış dosya sistemi (HDFS) Kabuk komutları tooaccess hello deposu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="612ae-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="612ae-189">Bu bölümdeki hello oluşturduğunuz Hdınsight Linux kümesi içine bir SSH bağlantısı ve ardından hello HDFS komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="612ae-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="612ae-190">Bir Windows istemci toomake hello kümesine bir SSH bağlantısı kullanıyorsanız, bkz: [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="612ae-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="612ae-191">Linux istemci toomake hello kümesine bir SSH bağlantısı kullanıyorsanız, bkz: [Linux Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="612ae-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="612ae-192">Merhaba bağlantı yaptıktan sonra HDFS dosya sistemi komutu aşağıdaki hello kullanarak Data Lake Store hello dosyalarında listeleyin.</span><span class="sxs-lookup"><span data-stu-id="612ae-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="612ae-193">Merhaba de kullanabilirsiniz `hdfs dfs -put` tooupload bazı dosyaları tooData Lake Store komutunu ve ardından `hdfs dfs -ls` tooverify hello dosyaları başarıyla karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="612ae-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="612ae-194">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="612ae-194">See also</span></span>
* [<span data-ttu-id="612ae-195">Azure portal: Hdınsight küme toouse Data Lake Store oluşturma</span><span class="sxs-lookup"><span data-stu-id="612ae-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
