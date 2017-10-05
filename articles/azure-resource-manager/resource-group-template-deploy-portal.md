---
title: "Azure kaynaklarınızı dağıtmak için Azure portalını kullanma | Microsoft Docs"
description: "Azure portalı ve Azure Resource Manager kaynaklarınızı dağıtmak için kullanın."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="44805-103">Kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="44805-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44805-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="44805-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="44805-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="44805-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="44805-106">Portal</span><span class="sxs-lookup"><span data-stu-id="44805-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="44805-107">REST API</span><span class="sxs-lookup"><span data-stu-id="44805-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="44805-108">Bu konuda nasıl kullanılacağını gösterir [Azure portal](https://portal.azure.com) ile [Azure Resource Manager](resource-group-overview.md) Azure kaynaklarınızı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="44805-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="44805-109">Kaynaklarınızın yönetilmesi hakkında bilgi edinmek için [yönetmek Azure kaynakları portal üzerinden](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="44805-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="44805-110">Şu anda, her hizmeti Portalı'nı veya Kaynak Yöneticisi'ni destekler.</span><span class="sxs-lookup"><span data-stu-id="44805-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="44805-111">Bu hizmetler için kullanmanız gerekir. [Klasik portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="44805-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="44805-112">Her hizmet durumunu görmek [Azure portal kullanılabilirlik grafik](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="44805-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="44805-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="44805-113">Create resource group</span></span>
1. <span data-ttu-id="44805-114">Boş bir kaynak grubu oluşturmak için seçin **yeni** > **Yönetim** > **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="44805-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![boş bir kaynak grubu oluştur](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="44805-116">Bir ad ve konum girin ve gerekiyorsa, bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="44805-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="44805-117">Kaynak grubu kaynaklarla ilgili meta verileri depoladığından kaynak grubu için bir konum sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="44805-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="44805-118">Uyumluluk nedenleriyle meta verilerin nerede depolanacağını belirtmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="44805-119">Genel olarak, çoğu kaynaklarınızın bulunacağı bir konum belirtin öneririz.</span><span class="sxs-lookup"><span data-stu-id="44805-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="44805-120">Aynı konuma kullanarak şablonunuzu basitleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-120">Using the same location can simplify your template.</span></span>
   
    ![kümesi Grup değerleri](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="44805-122">Market kaynaklardan dağıtma</span><span class="sxs-lookup"><span data-stu-id="44805-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="44805-123">Bir kaynak grubu oluşturduktan sonra kendisine marketten kaynakları dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="44805-124">Market yaygın senaryoları için önceden tanımlanmış çözümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="44805-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="44805-125">Bir dağıtımı başlatmak için **yeni** ve dağıtmak istiyor kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="44805-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="44805-126">Ardından, dağıtmak istediğiniz kaynak belirli sürümü için bakın.</span><span class="sxs-lookup"><span data-stu-id="44805-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![Kaynak dağıtma](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="44805-128">Dağıtmak istediğiniz belirli çözüm görmüyorsanız, Market arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![Arama Market](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="44805-130">Seçilen kaynak türüne bağlı olarak, dağıtım öncesinde ayarlamak için ilgili özellikleri koleksiyonu vardır.</span><span class="sxs-lookup"><span data-stu-id="44805-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="44805-131">Kaynak türü göre farklılık bu seçenekler Burada, bunlar gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="44805-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="44805-132">Tüm türleri için bir hedef kaynak grubu seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="44805-133">Aşağıdaki resimde, bir web uygulaması oluşturmak ve oluşturduğunuz kaynak grubuna dağıtmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="44805-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![kaynak grubu oluştur](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="44805-135">Alternatif olarak, kaynaklarınızın dağıtırken bir kaynak grubu oluşturmak için karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="44805-136">Seçin **Yeni Oluştur** ve kaynak grubu bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="44805-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![Yeni kaynak grubu oluştur](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="44805-138">Dağıtımınızı başlar.</span><span class="sxs-lookup"><span data-stu-id="44805-138">Your deployment begins.</span></span> <span data-ttu-id="44805-139">Dağıtımın birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="44805-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="44805-140">Dağıtım tamamlandığında, bir bildirim görür.</span><span class="sxs-lookup"><span data-stu-id="44805-140">When the deployment has finished, you see a notification.</span></span>
   
    ![Görünüm bildirim](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="44805-142">Kaynaklarınızı dağıttıktan sonra daha fazla kaynak kaynak grubuna kullanarak ekleyebileceğiniz **Ekle** kaynak grubu dikey komutu.</span><span class="sxs-lookup"><span data-stu-id="44805-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![kaynak ekle](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="44805-144">Özel şablon kaynaklardan dağıtma</span><span class="sxs-lookup"><span data-stu-id="44805-144">Deploy resources from custom template</span></span>
<span data-ttu-id="44805-145">Bir dağıtım yürütme ancak şablonlardan herhangi birini markette kullanmamak istiyorsanız, çözümünüz için altyapıyı tanımlayan özelleştirilmiş bir şablon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="44805-146">Şablonları oluşturma hakkında bilgi edinmek için [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="44805-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="44805-147">Özelleştirilmiş bir şablon portal üzerinden dağıtmak için seçin **yeni**ve Arama Başlat **şablon dağıtımı** kadar seçenekler arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![Arama şablon dağıtımı](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="44805-149">Seçin **şablon dağıtımı** kullanılabilir kaynaklardan.</span><span class="sxs-lookup"><span data-stu-id="44805-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![Şablon dağıtımı seçin](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="44805-151">Şablon dağıtımı başlatılıyor sonra özelleştirmek için kullanılabilir boş şablonu açın.</span><span class="sxs-lookup"><span data-stu-id="44805-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![Şablonu oluşturma](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="44805-153">Düzenleyicisi'nde dağıtmak istediğiniz kaynakları tanımlayan JSON söz dizimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44805-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="44805-154">Seçin **kaydetmek** bittiğinde.</span><span class="sxs-lookup"><span data-stu-id="44805-154">Select **Save** when done.</span></span> <span data-ttu-id="44805-155">JSON söz dizimi yazma ile ilgili yönergeler için bkz: [Resource Manager şablonu Kılavuzu](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="44805-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![şablonu düzenleme](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="44805-157">Veya önceden varolan bir şablondan seçebilirsiniz [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="44805-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="44805-158">Bu şablonlar, topluluk tarafından katkısı.</span><span class="sxs-lookup"><span data-stu-id="44805-158">These templates are contributed by the community.</span></span> <span data-ttu-id="44805-159">Birçok ortak senaryolarını kapsamak ve birisi ne dağıtmaya çalıştığınız benzer bir şablon eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="44805-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="44805-160">Şablonları senaryonuzla eşleşen bir şey bulmak için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![Hızlı Başlatma şablonunu seçin](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="44805-162">Seçili şablonu Düzenleyicisi'nde görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44805-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="44805-163">Diğer tüm değerleri girdikten sonra seçin **oluşturma** şablonu dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="44805-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![şablonu dağıtma](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="44805-165">Hesabınız için kaydedilen bir şablon kaynaklardan dağıtma</span><span class="sxs-lookup"><span data-stu-id="44805-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="44805-166">Portal, Azure hesabınızda bir şablonu kaydetmek ve daha sonra yeniden dağıtmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="44805-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="44805-167">Bu şablonlar, kaydedilen çalışma hakkında daha fazla bilgi için [Azure Portal'da özel şablonları kullanmaya başlama](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="44805-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="44805-168">Kaydedilen şablonlarınızı bulmak için seçin **Gözat** > **şablonları**.</span><span class="sxs-lookup"><span data-stu-id="44805-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![Şablonları Gözat](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="44805-170">Hesabınıza kaydedilebilir şablonları listesinden, üzerinde çalışmak istediğiniz birini seçin.</span><span class="sxs-lookup"><span data-stu-id="44805-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![kaydedilen şablonları](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="44805-172">Seçin **dağıtma** kaydedilmiş bu şablonu yeniden dağıtılamadı.</span><span class="sxs-lookup"><span data-stu-id="44805-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![Kaydedilmiş şablonu dağıtma](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="44805-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44805-174">Next steps</span></span>
* <span data-ttu-id="44805-175">Denetim günlüklerini görüntülemek için bkz: [denetim işlemleri Resource Manager ile](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="44805-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="44805-176">Dağıtım hataları gidermek için bkz: [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="44805-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="44805-177">Bir dağıtım veya kaynak grubunu şablon almak için bkz: [Azure Resource Manager şablonunu dışarı mevcut kaynaklardan](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="44805-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="44805-178">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="44805-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

