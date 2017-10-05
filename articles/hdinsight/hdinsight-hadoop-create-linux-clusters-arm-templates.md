---
title: "Şablonları - Azure Hdınsight kullanarak Hadoop kümeleri oluşturma | Microsoft Docs"
description: "Resource Manager şablonları kullanarak için Hdınsight kümeleri oluşturma hakkında bilgi edinin"
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
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="000c8-103">Resource Manager şablonları kullanarak Hdınsight'ta Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="000c8-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="000c8-104">Bu makalede, Azure Resource Manager şablonları ile Azure Hdınsight kümeleri oluşturmak için çeşitli yollar hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="000c8-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="000c8-105">Daha fazla bilgi için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="000c8-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="000c8-106">Diğer küme oluşturma araçları ve özellikleri hakkında bilgi edinmek için bu sayfanın üst kısmındaki sekme seçicisini tıklatın veya bkz [küme oluşturma yöntemleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="000c8-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="000c8-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="000c8-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="000c8-108">Bu makaledeki yönergeleri izlemek için ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="000c8-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="000c8-109">Bir [Azure aboneliği](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="000c8-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="000c8-110">Azure PowerShell ve/veya Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="000c8-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="000c8-111">Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="000c8-111">Resource Manager templates</span></span>
<span data-ttu-id="000c8-112">Resource Manager şablonu uygulamanız için aşağıdakileri tek ve eşgüdümlü bir işlemle oluşturmak kolay hale getirir:</span><span class="sxs-lookup"><span data-stu-id="000c8-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="000c8-113">Hdınsight kümeleri ile bağımlı kaynakları (örneğin, varsayılan depolama hesabı)</span><span class="sxs-lookup"><span data-stu-id="000c8-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="000c8-114">Diğer kaynaklar (örneğin, Apache Sqoop kullanmak için Azure SQL veritabanı)</span><span class="sxs-lookup"><span data-stu-id="000c8-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="000c8-115">Şablonda, uygulama için gereken kaynakları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="000c8-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="000c8-116">Ayrıca, farklı ortamlar için değer girmesini dağıtım parametrelerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="000c8-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="000c8-117">JSON ve dağıtımınız için değerleri oluşturmak için kullandığınız deyimleri şablon oluşur.</span><span class="sxs-lookup"><span data-stu-id="000c8-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="000c8-118">Hdınsight şablon örnekleri konumunda bulabilirsiniz [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="000c8-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="000c8-119">Platformlar arası kullanmak [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) ile [Resource Manager uzantısını](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) veya bir metin düzenleyicisi şablonu istasyonunuzda bir dosyaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="000c8-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="000c8-120">Farklı yöntemler kullanarak şablonu çağırma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="000c8-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="000c8-121">Resource Manager şablonları hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="000c8-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="000c8-122">Yazar Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="000c8-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="000c8-123">Bir uygulamayı Azure Resource Manager şablonları ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="000c8-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="000c8-124">Şablonları oluştur</span><span class="sxs-lookup"><span data-stu-id="000c8-124">Generate templates</span></span>

<span data-ttu-id="000c8-125">Azure Portalı'nı kullanarak, bir kümenin tüm özelliklerini yapılandırmak ve şablonunun dağıtmadan önce kaydedin.</span><span class="sxs-lookup"><span data-stu-id="000c8-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="000c8-126">Şablon daha sonra yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="000c8-126">You can then reuse the template.</span></span>

<span data-ttu-id="000c8-127">**Azure portalını kullanarak bir şablon oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="000c8-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="000c8-128">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="000c8-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="000c8-129">Tıklatın **yeni** sol menüsünde **Intelligence + analiz**ve ardından **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="000c8-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="000c8-130">Özellikler girmek için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="000c8-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="000c8-131">Kullanabilirsiniz **hızlı Oluştur** veya **özel** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="000c8-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="000c8-132">Üzerinde **Özet** sekmesini tıklatın, **karşıdan şablonu ve parametre**:</span><span class="sxs-lookup"><span data-stu-id="000c8-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![Hdınsight Hadoop kümesi Resource Manager şablonu indirme oluşturma](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="000c8-134">Şablon dosyası, Parametreler dosyası ve kod örnekleri şablonu dağıtmak için kullanılan bir listeye bakın:</span><span class="sxs-lookup"><span data-stu-id="000c8-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![Hdınsight Hadoop Resource Manager şablonu indirme seçeneklerini küme oluşturma](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="000c8-136">Buradan, şablonunu indirebilir, şablon kitaplığınızı kaydetmek veya şablonu dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="000c8-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="000c8-137">Bir şablon kitaplığınızdaki erişmek için tıklatın **daha fazla hizmet** sol menüsünden ve ardından **şablonları** (altında **diğer** kategori).</span><span class="sxs-lookup"><span data-stu-id="000c8-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="000c8-138">Şablonu ve parametre dosyanın birlikte kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="000c8-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="000c8-139">Aksi takdirde, beklenmedik sonuçlar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="000c8-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="000c8-140">Örneğin, varsayılan **clusterKind** özellik değeri olduğundan her zaman **hadoop**, şablon indirmeden önce hangi rağmen belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="000c8-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="000c8-141">PowerShell ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="000c8-141">Deploy with PowerShell</span></span>

<span data-ttu-id="000c8-142">Bu yordam, Hdınsight'ta Hadoop kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="000c8-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="000c8-143">JSON dosyasını kaydedin [ek](#appx-a-arm-template) istasyonunuzu için.</span><span class="sxs-lookup"><span data-stu-id="000c8-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="000c8-144">PowerShell komut dosyası dosya adıdır `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="000c8-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="000c8-145">Parametreler ve değişkenler gerekirse ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="000c8-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="000c8-146">Aşağıdaki PowerShell komut dosyası kullanarak şablonu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="000c8-146">Run the template by using the following PowerShell script:</span></span>

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
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="000c8-147">PowerShell komut dosyası, yalnızca küme adını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="000c8-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="000c8-148">Şablonda sabit kodlanmış depolama hesap adı değil.</span><span class="sxs-lookup"><span data-stu-id="000c8-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="000c8-149">Küme kullanıcı parolasını girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="000c8-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="000c8-150">(Varsayılan kullanıcı adı **yönetici**.) SSH kullanıcı parolasını girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="000c8-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="000c8-151">(Varsayılan SSH kullanıcı adı **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="000c8-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="000c8-152">Daha fazla bilgi için bkz: [PowerShell ile dağıtma](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="000c8-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="000c8-153">CLI ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="000c8-153">Deploy with CLI</span></span>
<span data-ttu-id="000c8-154">Aşağıdaki örnek, Azure komut satırı arabirimi (CLI) kullanır.</span><span class="sxs-lookup"><span data-stu-id="000c8-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="000c8-155">Bir küme, bağımlı depolama hesabı ve kapsayıcı Resource Manager şablonu çağırarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="000c8-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="000c8-156">Girmeniz istenir:</span><span class="sxs-lookup"><span data-stu-id="000c8-156">You are prompted to enter:</span></span>
* <span data-ttu-id="000c8-157">Küme adı.</span><span class="sxs-lookup"><span data-stu-id="000c8-157">The cluster name.</span></span>
* <span data-ttu-id="000c8-158">Küme kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="000c8-158">The cluster user password.</span></span> <span data-ttu-id="000c8-159">(Varsayılan kullanıcı adı **yönetici**.)</span><span class="sxs-lookup"><span data-stu-id="000c8-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="000c8-160">SSH kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="000c8-160">The SSH user password.</span></span> <span data-ttu-id="000c8-161">(Varsayılan SSH kullanıcı adı **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="000c8-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="000c8-162">Aşağıdaki kod, satır içi parametreleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="000c8-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="000c8-163">REST API ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="000c8-163">Deploy with the REST API</span></span>
<span data-ttu-id="000c8-164">Bkz: [REST API'si ile dağıtma](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="000c8-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="000c8-165">Visual Studio ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="000c8-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="000c8-166">Bir kaynak grubu projesi oluşturun ve kullanıcı arabirimi aracılığıyla Azure'a dağıtmak için Visual Studio'yu kullanın.</span><span class="sxs-lookup"><span data-stu-id="000c8-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="000c8-167">Projenize eklemek için kaynak türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="000c8-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="000c8-168">Bu kaynaklar, Resource Manager şablonu otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="000c8-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="000c8-169">Proje şablonu dağıtmak için bir PowerShell betiğini de sağlar.</span><span class="sxs-lookup"><span data-stu-id="000c8-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="000c8-170">Visual Studio kaynak gruplarıyla kullanmaya giriş bilgileri için bkz: [Visual Studio üzerinden Azure kaynak gruplarını oluşturma ve dağıtma](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="000c8-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="000c8-171">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="000c8-171">Troubleshoot</span></span>

<span data-ttu-id="000c8-172">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="000c8-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="000c8-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="000c8-173">Next steps</span></span>
<span data-ttu-id="000c8-174">Bu makalede, Hdınsight kümesi oluşturmanın birkaç yolu öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="000c8-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="000c8-175">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="000c8-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="000c8-176">.NET istemci kitaplığını kaynaklarına dağıtma ilişkin bir örnek için bkz: [kaynakları .NET kitaplıkları ve bir şablon kullanarak dağıtmak](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="000c8-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="000c8-177">Bir uygulama dağıtımının ayrıntılı örneği için bkz: [sağlamak ve mikro beklendiği azure'da dağıtmak](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="000c8-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="000c8-178">Çözümünüzü farklı ortamlarda dağıtmaya yönelik kılavuz için bkz. [Microsoft Azure’da geliştirme ve test ortamları](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="000c8-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="000c8-179">Azure Resource Manager şablonu bölümleri hakkında bilgi edinmek için [şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="000c8-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="000c8-180">Bir Azure Resource Manager şablonunda kullanabileceğiniz işlevleri bir listesi için bkz: [şablon işlevleri](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="000c8-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="000c8-181">Ek: Hadoop kümesi oluşturmak için Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="000c8-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="000c8-182">Aşağıdaki Azure Resource Manager şablonu ile bağımlı Azure depolama hesabı Linux tabanlı Hadoop kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="000c8-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="000c8-183">Bu örnek Hive meta depo ve Oozie meta depo için yapılandırma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="000c8-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="000c8-184">Aşağıdaki bölümü silmek veya Şablon kullanmadan önce bölüm yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="000c8-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "The location where all azure resources will be deployed."
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
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
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

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="000c8-185">Ek: Resource Manager şablonu bir Spark kümesi oluşturmak</span><span class="sxs-lookup"><span data-stu-id="000c8-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="000c8-186">Bu bölüm, bir Hdınsight Spark kümesi oluşturmak için kullanabileceğiniz bir Resource Manager şablonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="000c8-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="000c8-187">Bu şablon için yapılandırmaları içerir `spark-defaults` ve `spark-thrift-sparkconf` (Spark 1.6 kümelerinde için) ve `spark2-defaults` ve `spark2-thrift-sparkconf` (Spark 2 kümeleri için).</span><span class="sxs-lookup"><span data-stu-id="000c8-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="000c8-188">Bu, ek olarak, Hdınsight hesaplar ve yapılandırmaları gibi ayarlar `spark.executor.instances`, `spark.executor.memory`, ve `spark.executor.cores` küme boyutuna göre.</span><span class="sxs-lookup"><span data-stu-id="000c8-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="000c8-189">Herhangi bir parametre bir bölümde şablonunun parçası olarak ayarlarsanız, Hdınsight hesaplamak değil ve aynı bölüm diğer parametreleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="000c8-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="000c8-190">Örneğin, parametre `spark.executor.instances` yer `spark-defaults` yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="000c8-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="000c8-191">Başka bir parametre ayarlarsanız (örneğin, `spark.yarn.exector.memoryOverhead`) içinde `spark-defaults` yapılandırması, Hdınsight değil hesaplamak ve ayarlama `spark.executor.instances` parametresini de.</span><span class="sxs-lookup"><span data-stu-id="000c8-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
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
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
