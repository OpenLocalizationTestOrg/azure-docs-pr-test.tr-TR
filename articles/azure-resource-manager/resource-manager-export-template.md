---
title: "aaaExport Azure Resource Manager şablonu | Microsoft Docs"
description: "Azure Resource Manager tooexport var olan bir kaynak grubundan bir şablon kullanın."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="50c85-103">Mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="50c85-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="50c85-104">Bu makalede, bilgi nasıl tooexport, aboneliğinizdeki mevcut kaynaklardan bir Resource Manager şablonu.</span><span class="sxs-lookup"><span data-stu-id="50c85-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="50c85-105">Bu oluşturulan şablonu toogain şablon söz dizimi daha iyi anlamasına kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="50c85-106">Bir şablon iki yolu tooexport vardır:</span><span class="sxs-lookup"><span data-stu-id="50c85-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="50c85-107">Merhaba verebilirsiniz **dağıtımı için kullanılan gerçek şablonu**.</span><span class="sxs-lookup"><span data-stu-id="50c85-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="50c85-108">Merhaba özgün şablonda tam olarak göründüğü gibi hello dışarı aktarılan şablonu tüm hello parametreler ve değişkenler içerir.</span><span class="sxs-lookup"><span data-stu-id="50c85-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="50c85-109">Bu yaklaşım hello portalı üzerinden kaynaklarına dağıtıldığında yardımcı olur ve bu kaynakları toosee hello şablonu toocreate istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="50c85-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="50c85-110">Bu şablon kullanıma hazırdır.</span><span class="sxs-lookup"><span data-stu-id="50c85-110">This template is readily usable.</span></span> 
* <span data-ttu-id="50c85-111">Dışa aktarabilirsiniz bir **hello hello kaynak grubunun geçerli durumunu temsil eden şablon oluşturdu**.</span><span class="sxs-lookup"><span data-stu-id="50c85-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="50c85-112">Merhaba dışarı aktarılan şablon dağıtımı için kullanılan herhangi bir şablonu dayanmıyor.</span><span class="sxs-lookup"><span data-stu-id="50c85-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="50c85-113">Bunun yerine, hello kaynak grubunun bir anlık görüntüdür bir şablon oluşturur.</span><span class="sxs-lookup"><span data-stu-id="50c85-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="50c85-114">Merhaba dışarı aktarılan şablon birçok sabit kodlu değer ve normalde tanımlayacağınız kadar fazla büyük olasılıkla parametre vardır.</span><span class="sxs-lookup"><span data-stu-id="50c85-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="50c85-115">Bu yaklaşım, dağıtımdan sonra hello kaynak grubu değiştirdiniz. yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="50c85-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="50c85-116">Genellikle bu şablonun kullanılabilir olması için önce değişiklikler yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50c85-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="50c85-117">Bu konu, her iki yaklaşımın hello portal üzerinden gösterir.</span><span class="sxs-lookup"><span data-stu-id="50c85-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="50c85-118">Kaynakları dağıtma</span><span class="sxs-lookup"><span data-stu-id="50c85-118">Deploy resources</span></span>
<span data-ttu-id="50c85-119">Bir şablon olarak dışarı aktarmak için kullanabileceğiniz kaynakları tooAzure dağıtarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="50c85-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="50c85-120">Aboneliğinizi tooexport tooa şablonu istediğiniz bir kaynak grubu zaten varsa, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="50c85-121">Bu makalenin sonraki bölümlerinde Hello hello web uygulaması ve SQL veritabanı çözümü bu bölümde gösterilen dağıttığınız varsayar.</span><span class="sxs-lookup"><span data-stu-id="50c85-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="50c85-122">Farklı bir çözüme kullanırsanız, deneyiminizi biraz farklı olabilir, ancak aynı tooexport şablon olan hello adımları hello.</span><span class="sxs-lookup"><span data-stu-id="50c85-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="50c85-123">Merhaba, [Azure portal](https://portal.azure.com)seçin **yeni**.</span><span class="sxs-lookup"><span data-stu-id="50c85-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![yeni’yi seçin](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="50c85-125">Arama **web uygulaması + SQL** ve hello kullanılabilir seçeneklerden birini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="50c85-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![web uygulaması ve SQL’i arayın](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="50c85-127">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="50c85-127">Select **Create**.</span></span>

      ![oluştur’u seçin](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="50c85-129">Merhaba web uygulaması ve SQL veritabanı için hello gerekli değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="50c85-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="50c85-130">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="50c85-130">Select **Create**.</span></span>

      ![web ve SQL değerini sağlayın](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="50c85-132">Merhaba dağıtım bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="50c85-132">hello deployment may take a minute.</span></span> <span data-ttu-id="50c85-133">Merhaba dağıtım tamamlandıktan sonra aboneliğiniz hello çözüm içerir.</span><span class="sxs-lookup"><span data-stu-id="50c85-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="50c85-134">Dağıtım geçmişinden şablonu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="50c85-134">View template from deployment history</span></span>
1. <span data-ttu-id="50c85-135">Yeni kaynak grubunuz için toohello kaynak grubu dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="50c85-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="50c85-136">Bu hello dikey penceresinde hello son dağıtım hello sonucunu gösterir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="50c85-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="50c85-137">Bu bağlantıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="50c85-137">Select this link.</span></span>
   
      ![kaynak grubu dikey penceresi](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="50c85-139">Merhaba grubu için dağıtım geçmişini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="50c85-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="50c85-140">Sizin durumunuzda hello dikey büyük olasılıkla yalnızca bir dağıtım listeler.</span><span class="sxs-lookup"><span data-stu-id="50c85-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="50c85-141">Bu dağıtımı seçin.</span><span class="sxs-lookup"><span data-stu-id="50c85-141">Select this deployment.</span></span>
   
     ![son dağıtım](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="50c85-143">Merhaba dikey penceresinde hello dağıtım özetini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="50c85-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="50c85-144">Merhaba Özet hello hello dağıtımının durumunu ve işlemlerini ve parametreleri için sağlanan hello değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="50c85-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="50c85-145">Merhaba dağıtımda, select kullanılan toosee hello şablonu **şablonu görüntüleme**.</span><span class="sxs-lookup"><span data-stu-id="50c85-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![dağıtım özetini görüntüleme](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="50c85-147">Kaynak Yöneticisi, sizin için aşağıdaki yedi dosyaları hello alır:</span><span class="sxs-lookup"><span data-stu-id="50c85-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="50c85-148">**Şablon** -Merhaba, çözümünüz için altyapıyı tanımlayan hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="50c85-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="50c85-149">Merhaba hello portal üzerinden depolama hesabı oluşturduğunuzda, Resource Manager şablonu toodeploy kullanılan onu ve bu şablonu gelecekte başvurmak üzere kaydetti.</span><span class="sxs-lookup"><span data-stu-id="50c85-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="50c85-150">**Parametreleri** -bir parametre dosyası toopass dağıtım sırasında değerleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="50c85-151">Merhaba ilk dağıtım sırasında sağlanan Başlangıç değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="50c85-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="50c85-152">Merhaba şablonu yeniden dağıtırken bu değerleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="50c85-153">**CLI** -bir Azure komut satırı arabirimi (CLI) betik dosyası toodeploy hello şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="50c85-154">**CLI 2.0** -bir Azure komut satırı arabirimi (CLI) betik dosyası toodeploy hello şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="50c85-155">**PowerShell** -bir Azure PowerShell komut dosyası toodeploy hello şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="50c85-156">**.NET** -toodeploy hello şablon kullanabileceğiniz bir .NET sınıfı.</span><span class="sxs-lookup"><span data-stu-id="50c85-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="50c85-157">**Ruby** -A Ruby sınıfı toodeploy hello şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="50c85-158">Merhaba dosyaları hello dikey pencerelerdeki bağlantılar aracılığıyla ulaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="50c85-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="50c85-159">Varsayılan olarak, hello dikey penceresinde hello şablonunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="50c85-159">By default, hello blade displays hello template.</span></span>
      
       ![şablonu görüntüleme](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="50c85-161">Bu şablon hello gerçek şablonu toocreate web uygulaması ve SQL database kullanılır.</span><span class="sxs-lookup"><span data-stu-id="50c85-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="50c85-162">Dağıtım sırasında tooprovide farklı değerleri etkinleştir parametreleri içeren dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="50c85-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="50c85-163">bir şablonun hello yapısı hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="50c85-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="50c85-164">Merhaba şablonu kaynak grubundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="50c85-164">Export hello template from resource group</span></span>
<span data-ttu-id="50c85-165">El ile kaynaklarınızı değiştirmiş veya birden çok dağıtımlarda kaynakları eklenen, bir şablon hello dağıtım geçmişini alma hello hello kaynak grubunun geçerli durumunu yansıtmaz.</span><span class="sxs-lookup"><span data-stu-id="50c85-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="50c85-166">Bu bölümde, nasıl tooexport yansıtan bir şablon hello hello kaynak grubunun geçerli durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="50c85-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="50c85-167">200’den fazla kaynağı olan bir kaynak grubu için bir şablonu dışarı aktaramazsınız.</span><span class="sxs-lookup"><span data-stu-id="50c85-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="50c85-168">tooview hello şablonu seçin, kaynak grubu için **Otomasyon betiğini**.</span><span class="sxs-lookup"><span data-stu-id="50c85-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![kaynak grubunu dışarı aktarma](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="50c85-170">Resource Manager hello kaynak grubunda hello kaynakları değerlendirir ve bu kaynakları için bir şablon oluşturur.</span><span class="sxs-lookup"><span data-stu-id="50c85-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="50c85-171">Merhaba şablonu dışarı aktarma işlevini tüm kaynak türleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="50c85-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="50c85-172">Merhaba dışarı aktarma ile ilgili bir sorun olduğunu bildiren bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="50c85-173">Toohandle olanlar nasıl sorunları içinde bilgi hello [dışarı aktarma sorunlarını düzeltme](#fix-export-issues) bölümü.</span><span class="sxs-lookup"><span data-stu-id="50c85-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="50c85-174">Yeniden tooredeploy hello çözüm kullanabilir hello altı dosyalarına bakın.</span><span class="sxs-lookup"><span data-stu-id="50c85-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="50c85-175">Ancak, bu zaman hello şablon biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="50c85-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="50c85-176">Oluşturulan şablon hello bildirimi önceki bölümdeki hello şablon sayısından daha az parametre içeriyor.</span><span class="sxs-lookup"><span data-stu-id="50c85-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="50c85-177">Ayrıca, bu şablon yerine bir parametre değeri kabul sabit kodlanmış birçok hello değerleri (örneğin, konum ve SKU değerleri).</span><span class="sxs-lookup"><span data-stu-id="50c85-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="50c85-178">Bu şablonu yeniden kullanmadan önce tooedit hello şablonu toomake daha iyi kullanılmasını parametrelerini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="50c85-179">Bir birkaç toowork bu şablonla devam etmek seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="50c85-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="50c85-180">Merhaba şablonunu indirebilir ve üzerinde yerel olarak bir JSON Düzenleyicisi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="50c85-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="50c85-181">Veya hello şablon tooyour kitaplığı kaydedin ve hello Portalı aracılığıyla üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="50c85-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="50c85-182">Gibi bir JSON düzenleyicisi kullanarak kullanabiliyorsanız [VS Code](https://code.visualstudio.com/) veya [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), yerel olarak hello şablonu indirme ve o düzenleyicisini kullanarak tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="50c85-183">toowork yerel olarak select **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="50c85-183">toowork locally, select **Download**.</span></span>
   
      ![şablonu indirme](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="50c85-185">Bir JSON düzenleyicisiyle ayarlanmayan, hello şablon hello portal üzerinden düzenlemeyi tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="50c85-186">Bu konuda Hello kalanı hello Portalı'nda hello şablon tooyour kitaplığı kaydettiğiniz varsayar.</span><span class="sxs-lookup"><span data-stu-id="50c85-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="50c85-187">Ancak, aynı hello yaptığınız sözdizimi değişip toohello şablonu hello portal aracılığıyla veya JSON Düzenleyicisi ile yerel olarak çalışma.</span><span class="sxs-lookup"><span data-stu-id="50c85-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="50c85-188">Merhaba portal üzerinden toowork seçin **toolibrary eklemek**.</span><span class="sxs-lookup"><span data-stu-id="50c85-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![toolibrary Ekle](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="50c85-190">Bir şablon toohello kitaplığı eklerken hello şablonuna bir ad ve açıklama verin.</span><span class="sxs-lookup"><span data-stu-id="50c85-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="50c85-191">Ardından **Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="50c85-191">Then, select **Save**.</span></span>
   
     ![şablon değerlerini ayarlama](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="50c85-193">tooview kitaplığınızda, kaydedilen bir şablon seçin **daha fazla hizmet**, türü **şablonları** toofilter sonuçları, select **şablonları**.</span><span class="sxs-lookup"><span data-stu-id="50c85-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![şablonları bulma](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="50c85-195">Kaydettiğiniz hello adla Hello şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="50c85-195">Select hello template with hello name you saved.</span></span>
   
      ![şablon seçme](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="50c85-197">Merhaba şablonunu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="50c85-197">Customize hello template</span></span>
<span data-ttu-id="50c85-198">toocreate hello istiyorsanız, uygulama ve SQL veritabanı her dağıtım için aynı web ince dışarı hello şablon çalışır.</span><span class="sxs-lookup"><span data-stu-id="50c85-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="50c85-199">Bununla birlikte Resource Manager, şablonları çok daha fazla esneklikle dağıtabileceğiniz seçenekler sunar.</span><span class="sxs-lookup"><span data-stu-id="50c85-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="50c85-200">Bu makale size nasıl veritabanı yönetici adı ve parola hello tooadd parametrelerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="50c85-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="50c85-201">Merhaba şablonundaki diğer değerler için daha fazla esneklik aynı bu yaklaşım tooadd kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="50c85-202">toocustomize hello şablonu, select **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="50c85-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![şablonu gösterme](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="50c85-204">Merhaba şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="50c85-204">Select hello template.</span></span>
   
     ![şablonu düzenleme](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="50c85-206">toobe mümkün toopass hello değerleri dağıtımı sırasında toospecify isteyebilirsiniz ekleyin iki parametreleri toohello aşağıdaki hello **parametreleri** hello şablonu bölümünde:</span><span class="sxs-lookup"><span data-stu-id="50c85-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="50c85-207">toouse hello yeni parametreleri değiştirin hello SQL server hello tanımında **kaynakları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="50c85-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="50c85-208">Şimdi **administratorLogin** ve **administratorLoginPassword** için parametre değerlerinin kullanıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="50c85-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="50c85-209">Seçin **Tamam** düzenleme hello şablon bittiğinde.</span><span class="sxs-lookup"><span data-stu-id="50c85-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="50c85-210">Seçin **kaydetmek** toosave hello değişiklikleri toohello şablonu.</span><span class="sxs-lookup"><span data-stu-id="50c85-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![şablonu kaydetme](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="50c85-212">tooredeploy güncelleştirilmiş hello şablonu, select **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="50c85-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![şablonu dağıtma](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="50c85-214">Parametre değerlerini sağlayın ve bir kaynak grubu toodeploy hello kaynakları seçin.</span><span class="sxs-lookup"><span data-stu-id="50c85-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="50c85-215">Dışarı aktarma sorunlarını düzeltme</span><span class="sxs-lookup"><span data-stu-id="50c85-215">Fix export issues</span></span>
<span data-ttu-id="50c85-216">Merhaba şablonu dışarı aktarma işlevini tüm kaynak türleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="50c85-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="50c85-217">el ile bu sorunu tooresolve hello eksik kaynakları şablonunuza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="50c85-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="50c85-218">Merhaba hata iletisi verilemez hello kaynak türleri içerir.</span><span class="sxs-lookup"><span data-stu-id="50c85-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="50c85-219">Bu kaynak türünü [Şablon başvurusunda](/azure/templates/) bulun.</span><span class="sxs-lookup"><span data-stu-id="50c85-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="50c85-220">Örneğin, toomanually bir sanal ağ geçidi eklemek için bkz: [Microsoft.Network/virtualNetworkGateways şablon başvurusu](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="50c85-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="50c85-221">Yalnızca, dağıtım geçmişiniz yerine bir kaynak grubundan dışarı aktarma yaparken dışarı aktarma sorunlarıyla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="50c85-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="50c85-222">Son dağıtımınız hello hello kaynak grubunun geçerli durumunu doğru şekilde temsil ediyorsa hello şablon hello dağıtım geçmişi engellemeniz hello kaynak grubu vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="50c85-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="50c85-223">Yalnızca tek bir şablonda tanımlı değil toohello kaynak grubu değişiklikler yaptığınızda kaynak grubundan dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="50c85-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="50c85-224">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="50c85-224">Next steps</span></span>
<span data-ttu-id="50c85-225">Öğrendiğiniz nasıl tooexport hello portalda oluşturduğunuz kaynaklardan bir şablonu.</span><span class="sxs-lookup"><span data-stu-id="50c85-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="50c85-226">Bir şablonu [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md) veya [REST API](resource-group-template-deploy-rest.md) aracılığıyla dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c85-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="50c85-227">tooexport bir şablonu PowerShell aracılığıyla nasıl görürüm toosee [Azure PowerShell kullanarak Azure Resource Manager ile](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="50c85-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="50c85-228">tooexport bir şablonu Azure CLI aracılığıyla nasıl görürüm toosee [kullanım hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="50c85-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

