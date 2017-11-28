---
title: "aaaDeploy Visual Studio kullanarak sanal makine ölçek kümesi | Microsoft Docs"
description: "Visual Studio ve Resource Manager şablonu kullanarak sanal makine ölçek kümeleri dağıtma"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="08afe-103">Nasıl toocreate Visual Studio ile bir sanal makine ölçek kümesi</span><span class="sxs-lookup"><span data-stu-id="08afe-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="08afe-104">Bu makalede nasıl toodeploy bir Visual Studio kaynak grubu dağıtımı kullanarak bir Azure sanal makine ölçek kümesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="08afe-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="08afe-105">[Azure sanal makine ölçek kümeleri](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) bir Azure işlem kaynak toodeploy ve Otomatik ölçek benzer sanal makinelerle koleksiyonunu yönetmenize ve Yük Dengeleme.</span><span class="sxs-lookup"><span data-stu-id="08afe-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="08afe-106">Sağlama ve sanal makine ölçekleme kümeleri kullanarak dağıtın [Azure Resource Manager şablonları](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="08afe-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="08afe-107">Azure CLI, PowerShell, REST kullanarak Azure Resource Manager şablonları dağıtılabilir ve ayrıca Visual Studio'dan doğrudan.</span><span class="sxs-lookup"><span data-stu-id="08afe-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="08afe-108">Visual Studio bir Azure kaynak grubu dağıtım projesi bir parçası olarak dağıtılabilir örnek şablonları kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08afe-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="08afe-109">Azure kaynak grubu dağıtımları yolu toogroup olan ve bir dizi ilgili Azure kaynaklarını tek dağıtım işleminde yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="08afe-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="08afe-110">Bunları hakkında daha fazla burada öğrenebilirsiniz: [Visual Studio üzerinden Azure kaynak gruplarını oluşturma ve dağıtma](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="08afe-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="08afe-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="08afe-111">Pre-requisites</span></span>
<span data-ttu-id="08afe-112">Sanal makine ölçek kümeleri Visual Studio'daki dağıtımı başladı tooget hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="08afe-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="08afe-113">Visual Studio 2013 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="08afe-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="08afe-114">2.7, 2.8 veya 2.9 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="08afe-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="08afe-115">Bu yönergeler, Visual Studio ile kullandığınız varsayılmıştır [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="08afe-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="08afe-116">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="08afe-116">Creating a Project</span></span>
1. <span data-ttu-id="08afe-117">Seçerek Visual Studio'da yeni proje oluşturma **dosya | Yeni | Proje**.</span><span class="sxs-lookup"><span data-stu-id="08afe-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Yeni dosya][file_new]

2. <span data-ttu-id="08afe-119">Altında **Visual C# | Bulut**, seçin **Azure Resource Manager** toocreate bir Azure Resource Manager şablonunu dağıtmak için bir proje.</span><span class="sxs-lookup"><span data-stu-id="08afe-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Proje oluşturma][create_project]

3. <span data-ttu-id="08afe-121">Şablonları Hello listeden hello Linux veya Windows sanal makine ölçek kümesi şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="08afe-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Şablonu seçin][select_Template]

4. <span data-ttu-id="08afe-123">Projeniz oluşturulduktan sonra PowerShell dağıtım betikleri, bir Azure Resource Manager şablonu ve hello sanal makine ölçek kümesi için bir parametre dosyası bakın.</span><span class="sxs-lookup"><span data-stu-id="08afe-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Çözüm Gezgini][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="08afe-125">Projenizi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="08afe-125">Customize your project</span></span>
<span data-ttu-id="08afe-126">Merhaba şablonu toocustomize düzenleyebilirsiniz artık VM uzantısı özellikleri ekleme veya düzenleme gibi uygulamanızın ihtiyaçları için Yük Dengeleme kuralları.</span><span class="sxs-lookup"><span data-stu-id="08afe-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="08afe-127">Varsayılan olarak hello sanal makine ölçek kümesi kolay tooadd otomatik ölçeklendirme kurallarını kolaylaştırır yapılandırılmış toodeploy hello AzureDiagnostics uzantısı şablonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="08afe-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="08afe-128">Ayrıca, bir yük dengeleyici gelen NAT kuralları ile yapılandırılmış bir ortak IP adresi ile dağıtır.</span><span class="sxs-lookup"><span data-stu-id="08afe-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="08afe-129">Hello yük dengeleyici SSH (Linux) veya RDP (Windows) ile toohello VM örnekleri bağlanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="08afe-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="08afe-130">Merhaba ön uç bağlantı noktası aralığı 50000'den başlar.</span><span class="sxs-lookup"><span data-stu-id="08afe-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="08afe-131">Linux için bu olması durumunda anlamına gelir, SSH tooport 50000, yönlendirilmiş tooport 22 olan ilk VM hello ölçek kümesi ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="08afe-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="08afe-132">Tooport 50001 bağlanma olduğu yönlendirilmiş tooport 22 hello VM vb. ikinci.</span><span class="sxs-lookup"><span data-stu-id="08afe-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="08afe-133">En iyi yolu tooedit şablonlarınızı Visual Studio ile olan toouse hello JSON ana hattı tooorganize hello parametreleri, değişkenler ve kaynakları.</span><span class="sxs-lookup"><span data-stu-id="08afe-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="08afe-134">Dağıtmadan önce hello bir anlayış şablonunuzda hataları ortaya şema Visual Studio işaret edebilir.</span><span class="sxs-lookup"><span data-stu-id="08afe-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON Gezgini][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="08afe-136">Merhaba projesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="08afe-136">Deploy hello project</span></span>
1. <span data-ttu-id="08afe-137">Hello Azure Resource Manager şablonu toocreate hello kaynak sanal makine ölçek kümesi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="08afe-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="08afe-138">Merhaba proje düğümüne sağ tıklayın ve seçin **dağıtma | Yeni dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="08afe-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Şablon dağıtma][5deploy_Template]
    
2. <span data-ttu-id="08afe-140">Aboneliğinizi hello "Dağıtma tooResource grup" iletişim kutusunda seçin.</span><span class="sxs-lookup"><span data-stu-id="08afe-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![Şablon dağıtma][6deploy_Template]

3. <span data-ttu-id="08afe-142">Buradan, şablonunuza bir Azure kaynak grubu toodeploy oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08afe-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![Yeni kaynak grubu][new_resource]

4. <span data-ttu-id="08afe-144">Bundan sonra öğesini **parametreleri Düzenle** tooyour şablonu geçirilen tooenter parametreleri.</span><span class="sxs-lookup"><span data-stu-id="08afe-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="08afe-145">Merhaba gerekli toocreate hello dağıtım OS Hello kullanıcı adı ve parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="08afe-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="08afe-146">Visual Studio yüklüyse PowerShell araçları yoksa, toocheck önerilir **parolaları kaydetme** tooavoid bir gizli PowerShell komut satırı isteyebilir veya kullanmak [keyvault Destek](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="08afe-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Parametreleri Düzenle][edit_parameters]

5. <span data-ttu-id="08afe-148">Şimdi **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="08afe-148">Now click **Deploy**.</span></span> <span data-ttu-id="08afe-149">Merhaba **çıkış** penceresi hello dağıtımının ilerleme durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="08afe-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="08afe-150">Merhaba eylemin hello yürütüyor Not **dağıtma AzureResourceGroup.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="08afe-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Çıktı penceresi][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="08afe-152">Sanal makine ölçek kümesi keşfetme</span><span class="sxs-lookup"><span data-stu-id="08afe-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="08afe-153">Merhaba dağıtım işlemi tamamlandıktan sonra görüntüleyebileceğiniz yeni sanal makine ölçek kümesindeki hello Visual Studio hello **Cloud Explorer** (yenileme hello listesi).</span><span class="sxs-lookup"><span data-stu-id="08afe-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="08afe-154">Cloud Explorer uygulamaları geliştirirken Visual Studio'da Azure kaynaklarını yönetmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08afe-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="08afe-155">Ayrıca, sanal makine ölçek kümesi hello görüntüleyebilirsiniz [Azure portal](https://portal.azure.com) ve [Azure kaynak Gezgini](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="08afe-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Bulut Gezgini][cloud_explorer]

 <span data-ttu-id="08afe-157">Merhaba portal toovisually yönetmek web tarayıcısı olan Azure altyapınıza Azure kaynak Gezgini kolay bir yolu tooexplore sağlarken hello en iyi yoldur ve Azure kaynaklarını hata ayıklama, bir penceresine vermiş "örnek görüntülemek" Merhaba ve ayrıca PowerShell gösteren Baktığınız hello kaynaklar için komutları.</span><span class="sxs-lookup"><span data-stu-id="08afe-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08afe-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08afe-158">Next steps</span></span>
<span data-ttu-id="08afe-159">Visual Studio aracılığıyla sanal makine ölçek kümeleri başarıyla dağıttıktan sonra bir kez daha fazla uygulama gereksinimlerinizi proje toosuit özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08afe-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="08afe-160">Örneğin, Otomatik ölçek ekleyerek yapılandırın bir **Insights** (örneğin, tek başına VM'ler) altyapısı tooyour şablonu ekleme veya hello özel betik uzantısı kullanarak uygulamaları dağıtma kaynak.</span><span class="sxs-lookup"><span data-stu-id="08afe-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="08afe-161">İyi örnek şablonları hello bulunabilir [Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates) GitHub deposunu ("vmss" arayın).</span><span class="sxs-lookup"><span data-stu-id="08afe-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
