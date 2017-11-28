---
title: "aaaCreate Hadoop kümeleri şablonları - Azure Hdınsight kullanarak | Microsoft Docs"
description: "Resource Manager şablonları kullanarak toocreate Hdınsight için nasıl kümeleri öğrenin"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="d3421-103">Resource Manager şablonları kullanarak Hdınsight'ta Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3421-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="d3421-104">Bu makalede, çeşitli yollar hakkında bilgi edineceksiniz toocreate Azure Hdınsight kümeleri ile Azure Resource Manager şablonları.</span><span class="sxs-lookup"><span data-stu-id="d3421-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="d3421-105">Daha fazla bilgi için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d3421-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="d3421-106">diğer küme oluşturma araçları ve özellikleri hakkında toolearn tıklatın hello sekme seçicisini hello üstteki bu sayfa ya da bakın [küme oluşturma yöntemleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="d3421-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3421-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d3421-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="d3421-108">Bu makaledeki toofollow hello yönergeleri, ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="d3421-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="d3421-109">Bir [Azure aboneliği](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d3421-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d3421-110">Azure PowerShell ve/veya Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d3421-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="d3421-111">Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="d3421-111">Resource Manager templates</span></span>
<span data-ttu-id="d3421-112">Resource Manager şablonu tek ve eşgüdümlü bir işlemle, uygulamanız için aşağıdaki kolay toocreate hello kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="d3421-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="d3421-113">Hdınsight kümeleri ile bağımlı kaynakları (Merhaba varsayılan depolama hesabı gibi)</span><span class="sxs-lookup"><span data-stu-id="d3421-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="d3421-114">Diğer kaynaklar (örneğin, Azure SQL veritabanı toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="d3421-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="d3421-115">Merhaba şablonunda hello uygulama için gerekli olan hello kaynakları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d3421-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="d3421-116">Ayrıca, farklı ortamlar için dağıtım parametreleri tooinput değerleri de belirtin.</span><span class="sxs-lookup"><span data-stu-id="d3421-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="d3421-117">JSON ve dağıtımınız için tooconstruct değerleri kullanan ifadelerin Hello şablonu oluşur.</span><span class="sxs-lookup"><span data-stu-id="d3421-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="d3421-118">Hdınsight şablon örnekleri konumunda bulabilirsiniz [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="d3421-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="d3421-119">Platformlar arası kullanmak [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) hello ile [Resource Manager uzantısını](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) veya bir metin düzenleyicisi toosave hello şablonu istasyonunuzda bir dosyaya.</span><span class="sxs-lookup"><span data-stu-id="d3421-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="d3421-120">Nasıl toocall hello şablonu farklı yöntemler kullanarak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d3421-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="d3421-121">Resource Manager şablonları hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="d3421-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="d3421-122">Yazar Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="d3421-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="d3421-123">Bir uygulamayı Azure Resource Manager şablonları ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="d3421-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="d3421-124">Şablonları oluştur</span><span class="sxs-lookup"><span data-stu-id="d3421-124">Generate templates</span></span>

<span data-ttu-id="d3421-125">Hello Azure portal kullanarak, bir kümenin tüm hello özelliklerini yapılandırmak ve hello şablonunun dağıtmadan önce kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d3421-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="d3421-126">Merhaba şablon daha sonra yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3421-126">You can then reuse hello template.</span></span>

<span data-ttu-id="d3421-127">**toogenerate hello Azure portal kullanarak bir şablonu**</span><span class="sxs-lookup"><span data-stu-id="d3421-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="d3421-128">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3421-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d3421-129">Tıklatın **yeni** hello sol menüsünde **Intelligence + analiz**ve ardından **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="d3421-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="d3421-130">Merhaba yönergeleri tooenter özellikleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="d3421-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="d3421-131">Her iki hello kullanabilirsiniz **hızlı Oluştur** veya hello **özel** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d3421-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="d3421-132">Merhaba üzerinde **Özet** sekmesini tıklatın, **karşıdan şablonu ve parametre**:</span><span class="sxs-lookup"><span data-stu-id="d3421-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![Hdınsight Hadoop kümesi Resource Manager şablonu indirme oluşturma](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="d3421-134">Hello şablon dosyası, parametreleri dosyasını ve kod kullanılan örneklerin toodeploy hello şablon listesini bakın:</span><span class="sxs-lookup"><span data-stu-id="d3421-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![Hdınsight Hadoop Resource Manager şablonu indirme seçeneklerini küme oluşturma](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="d3421-136">Buradan, hello şablonunu indirebilir, tooyour Şablon kitaplığı Kaydet veya hello şablonunu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d3421-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="d3421-137">tooaccess kitaplığınızda, bir şablon tıklatın **daha fazla hizmet** hello sol menüsünden ve ardından **şablonları** (Merhaba altında **diğer** kategori).</span><span class="sxs-lookup"><span data-stu-id="d3421-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="d3421-138">Merhaba şablonu ve parametre dosyası birlikte kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3421-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="d3421-139">Aksi takdirde, beklenmedik sonuçlar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3421-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="d3421-140">Örneğin, varsayılan hello **clusterKind** özellik değeri olduğundan her zaman **hadoop**, hello şablon indirmeden önce hangi rağmen belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="d3421-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="d3421-141">PowerShell ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="d3421-141">Deploy with PowerShell</span></span>

<span data-ttu-id="d3421-142">Bu yordam, Hdınsight'ta Hadoop kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d3421-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="d3421-143">Hello Hello JSON dosyasını kaydedin [ek](#appx-a-arm-template) tooyour iş istasyonu.</span><span class="sxs-lookup"><span data-stu-id="d3421-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="d3421-144">Hello PowerShell Betiği, hello dosya adıdır `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="d3421-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="d3421-145">Merhaba parametreler ve değişkenler gerekirse ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d3421-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="d3421-146">PowerShell Betiği aşağıdaki hello kullanarak Hello şablon çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d3421-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="d3421-147">Merhaba PowerShell komut dosyası yalnızca hello küme adını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="d3421-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="d3421-148">Merhaba şablonu sabit kodlanmış Hello depolama hesap adı değil.</span><span class="sxs-lookup"><span data-stu-id="d3421-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="d3421-149">İstendiğinde tooenter hello küme kullanıcı parolası var.</span><span class="sxs-lookup"><span data-stu-id="d3421-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="d3421-150">(Merhaba varsayılan kullanıcı adı **yönetici**.) Ayrıca istendiğinde tooenter hello SSH kullanıcı parolası var.</span><span class="sxs-lookup"><span data-stu-id="d3421-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="d3421-151">(Merhaba varsayılan SSH kullanıcı adı **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="d3421-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="d3421-152">Daha fazla bilgi için bkz: [PowerShell ile dağıtma](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="d3421-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="d3421-153">CLI ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="d3421-153">Deploy with CLI</span></span>
<span data-ttu-id="d3421-154">Aşağıdaki örnek hello Azure komut satırı arabirimi (CLI) kullanır.</span><span class="sxs-lookup"><span data-stu-id="d3421-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="d3421-155">Bir küme, bağımlı depolama hesabı ve kapsayıcı Resource Manager şablonu çağırarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="d3421-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="d3421-156">İstendiğinde tooenter şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d3421-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="d3421-157">Merhaba küme adı.</span><span class="sxs-lookup"><span data-stu-id="d3421-157">hello cluster name.</span></span>
* <span data-ttu-id="d3421-158">Merhaba küme kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="d3421-158">hello cluster user password.</span></span> <span data-ttu-id="d3421-159">(Merhaba varsayılan kullanıcı adı **yönetici**.)</span><span class="sxs-lookup"><span data-stu-id="d3421-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="d3421-160">Merhaba SSH kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="d3421-160">hello SSH user password.</span></span> <span data-ttu-id="d3421-161">(Merhaba varsayılan SSH kullanıcı adı **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="d3421-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="d3421-162">Satır içi parametreleri koddan hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="d3421-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="d3421-163">REST API Hello ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="d3421-163">Deploy with hello REST API</span></span>
<span data-ttu-id="d3421-164">Bkz: [hello REST API ile dağıtma](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d3421-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="d3421-165">Visual Studio ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="d3421-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="d3421-166">Visual Studio toocreate bir kaynak grubu projesi kullanabilir ve tooAzure hello kullanıcı arabirimi aracılığıyla dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3421-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="d3421-167">Projenizde kaynakları tooinclude hello türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="d3421-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="d3421-168">Bu kaynakları toohello Resource Manager şablonu otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="d3421-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="d3421-169">Merhaba proje bir PowerShell komut dosyası toodeploy hello şablonu da sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3421-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="d3421-170">Bir giriş toousing için Visual Studio kaynak gruplarıyla, bkz: [Visual Studio üzerinden Azure kaynak gruplarını oluşturma ve dağıtma](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d3421-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="d3421-171">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d3421-171">Troubleshoot</span></span>

<span data-ttu-id="d3421-172">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="d3421-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3421-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3421-173">Next steps</span></span>
<span data-ttu-id="d3421-174">Bu makalede, çeşitli yolları toocreate Hdınsight kümesi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="d3421-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="d3421-175">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="d3421-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="d3421-176">Kaynaklara hello .NET istemci kitaplığı aracılığıyla dağıtmaya ilişkin bir örnek için bkz: [kaynakları .NET kitaplıkları ve bir şablon kullanarak dağıtmak](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3421-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d3421-177">Bir uygulama dağıtımının ayrıntılı örneği için bkz: [sağlamak ve mikro beklendiği azure'da dağıtmak](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="d3421-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="d3421-178">Çözüm toodifferent ortamlarınızın dağıtma ile ilgili yönergeler için bkz: [Microsoft Azure geliştirme ve test ortamlarında](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="d3421-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="d3421-179">toolearn hello Azure Resource Manager şablonu hello bölümlerini hakkında bkz [şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d3421-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d3421-180">Bir Azure Resource Manager şablonunda kullanabileceğiniz hello işlevleri bir listesi için bkz: [şablon işlevleri](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="d3421-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="d3421-181">Ek: Resource Manager şablonu toocreate Hadoop kümesi</span><span class="sxs-lookup"><span data-stu-id="d3421-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="d3421-182">Merhaba aşağıdaki Azure Resource Manager şablonu Linux tabanlı Hadoop kümesi ile Merhaba bağımlı Azure depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d3421-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="d3421-183">Bu örnek Hive meta depo ve Oozie meta depo için yapılandırma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d3421-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="d3421-184">Merhaba bölümü kaldırmak veya hello şablonunu kullanmadan önce hello bölüm yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d3421-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="d3421-185">Ek: Resource Manager şablonu toocreate bir Spark kümesi</span><span class="sxs-lookup"><span data-stu-id="d3421-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="d3421-186">Bu bölümde bir Resource Manager şablonu toocreate Hdınsight Spark kümesinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3421-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="d3421-187">Bu şablon için yapılandırmaları içerir `spark-defaults` ve `spark-thrift-sparkconf` (Spark 1.6 kümelerinde için) ve `spark2-defaults` ve `spark2-thrift-sparkconf` (Spark 2 kümeleri için).</span><span class="sxs-lookup"><span data-stu-id="d3421-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="d3421-188">Ayrıca toothis, Hdınsight hesaplar ve yapılandırmaları gibi ayarlar `spark.executor.instances`, `spark.executor.memory`, ve `spark.executor.cores` hello küme boyutuna göre.</span><span class="sxs-lookup"><span data-stu-id="d3421-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="d3421-189">Herhangi bir parametre bir bölümde hello şablona bir parçası olarak ayarlarsanız, Hdınsight değil hesaplamak ve set hello Merhaba, diğer parametreler aynı bölüm.</span><span class="sxs-lookup"><span data-stu-id="d3421-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="d3421-190">Örneğin, parametre `spark.executor.instances` hello olduğu `spark-defaults` yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="d3421-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="d3421-191">Başka bir parametre ayarlarsanız (örneğin, `spark.yarn.exector.memoryOverhead`) hello içinde `spark-defaults` yapılandırması, Hdınsight değil hesaplamak ve ayarlama hello `spark.executor.instances` parametresini de.</span><span class="sxs-lookup"><span data-stu-id="d3421-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
