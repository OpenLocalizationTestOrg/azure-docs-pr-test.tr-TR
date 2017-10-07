---
title: hello Azure CLI aaaManage kaynaklarla | Microsoft Docs
description: "Hello Azure komut satırı arabirimi (CLI) toomanage Azure kullanan kaynak ve grupları"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="a15c9-103">Hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="a15c9-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a15c9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a15c9-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="a15c9-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a15c9-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="a15c9-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a15c9-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="a15c9-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a15c9-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="a15c9-108">Hello Azure komut satırı arabirimi (Azure CLI) olan bir çeşitli araçlar toodeploy kullanma ve Kaynak Yöneticisi ile kaynakları yönetme.</span><span class="sxs-lookup"><span data-stu-id="a15c9-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="a15c9-109">Bu makale ortak yolları toomanage Azure sunar kaynaklarını ve kaynak gruplarını kullanarak hello Azure CLI Kaynak Yöneticisi modunda.</span><span class="sxs-lookup"><span data-stu-id="a15c9-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="a15c9-110">Merhaba CLI toodeploy kaynakları kullanma hakkında daha fazla bilgi için bkz: [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a15c9-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="a15c9-111">Azure kaynakları ve Kaynak Yöneticisi hakkında arka plan için hello ziyaret [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a15c9-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a15c9-112">toomanage Azure kaynakları hello Azure CLI ile ihtiyacınız çok[hello Azure CLI yükleme](../cli-install-nodejs.md), ve [tooAzure içinde oturum](../xplat-cli-connect.md) hello kullanarak `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="a15c9-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="a15c9-113">CLI Kaynak Yöneticisi modunda olduğundan emin olun hello (çalıştırmak `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="a15c9-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="a15c9-114">Bunlardan yaptıysanız, hazır toogo demektir.</span><span class="sxs-lookup"><span data-stu-id="a15c9-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="a15c9-115">Kaynak grupları ve kaynakları alma</span><span class="sxs-lookup"><span data-stu-id="a15c9-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="a15c9-116">Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="a15c9-116">Resource groups</span></span>
<span data-ttu-id="a15c9-117">tooget aboneliğinizi ve konumlarına, tüm kaynak gruplarının bir listesini bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a15c9-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="a15c9-118">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a15c9-118">Resources</span></span>
 <span data-ttu-id="a15c9-119">toolist biriyle gibi bir gruptaki tüm kaynakların ad *testRG*, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="a15c9-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="a15c9-120">tooview adlı bir VM'den gibi hello grup içindeki tek bir kaynağın *MyUbuntuVM*, hello aşağıdaki gibi bir komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a15c9-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="a15c9-121">Bildirim hello **Microsoft.Compute/virtualMachines** parametresi.</span><span class="sxs-lookup"><span data-stu-id="a15c9-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="a15c9-122">Bu parametre hakkında bilgi isteyen hello kaynak hello türünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="a15c9-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="a15c9-123">Merhaba kullanırken **azure kaynak** komutları hello dışında **listesi** komutu ile Merhaba hello kaynak hello API sürümü belirtmelidir **-o** parametresi.</span><span class="sxs-lookup"><span data-stu-id="a15c9-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="a15c9-124">Hello API sürümü hakkında emin değilseniz, hello şablon dosyası başvurun ve hello kaynak için hello apiVersion alanını bulun.</span><span class="sxs-lookup"><span data-stu-id="a15c9-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="a15c9-125">Kaynak Yöneticisi'nde API sürümleri hakkında daha fazla bilgi için bkz: [kaynak sağlayıcıları ve türleri](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="a15c9-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="a15c9-126">Ayrıntıları bir kaynakta görüntülerken, yararlı toouse hello genellikle olduğu `--json` parametresi.</span><span class="sxs-lookup"><span data-stu-id="a15c9-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="a15c9-127">İç içe geçmiş yapılar veya koleksiyonlar bazı değerler olduğu için bu parametreyi hello çıktı daha okunabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="a15c9-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="a15c9-128">Merhaba aşağıdaki örnekte gösterilmiştir hello döndürmeyi hello sonuçlarını **Göster** JSON belgesi olarak komutu.</span><span class="sxs-lookup"><span data-stu-id="a15c9-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="a15c9-129">Hello JSON veri toofile'hello kullanarak kaydetmek istiyorsanız &gt; karakter toodirect hello çıktı tooa dosyası.</span><span class="sxs-lookup"><span data-stu-id="a15c9-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="a15c9-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a15c9-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="a15c9-131">Etiketler</span><span class="sxs-lookup"><span data-stu-id="a15c9-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="a15c9-132">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="a15c9-132">Manage resources</span></span>
<span data-ttu-id="a15c9-133">tooadd bir depolama hesabı tooa kaynak grubu gibi bir kaynak için benzer bir komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a15c9-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="a15c9-134">Ayrıca toospecifying hello hello kaynak API sürümü ile Merhaba **-o** parametresi, kullanım hello **-p** gerekli parametre toopass JSON biçimli dize veya ek özellikler.</span><span class="sxs-lookup"><span data-stu-id="a15c9-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="a15c9-135">bir sanal makine kaynağı gibi mevcut bir kaynağı toodelete hello aşağıdaki gibi bir komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a15c9-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="a15c9-136">toomove varolan kaynakları tooanother kaynak grubuna veya aboneliğe hello kullanın, **azure kaynak taşıma** komutu.</span><span class="sxs-lookup"><span data-stu-id="a15c9-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="a15c9-137">örnekte gösterildiği nasıl aşağıdaki hello toomove Redis önbelleği tooa yeni bir kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="a15c9-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="a15c9-138">Merhaba, **-i** parametresi hello kaynak kimliği'nin toomove virgülle ayrılmış bir listesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a15c9-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="a15c9-139">Denetim erişim tooresources</span><span class="sxs-lookup"><span data-stu-id="a15c9-139">Control access tooresources</span></span>
<span data-ttu-id="a15c9-140">Hello Azure CLI toocreate ve ilkeleri toocontrol erişim tooAzure kaynaklarını yönetmek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a15c9-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="a15c9-141">İlke tanımları ve atama ilkelerini tooresources hakkında arka plan için bkz: [İlkesi toomanage kaynakları kullanın ve erişimi denetlemenize](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a15c9-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="a15c9-142">Örneğin, ilke toodeny aşağıdaki hello konumu değil Batı ABD veya Kuzey Orta ABD olduğu tüm istekleri tanımlayın ve toohello ilke tanımı dosyası policy.json kaydedin:</span><span class="sxs-lookup"><span data-stu-id="a15c9-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="a15c9-143">Merhaba çalıştırmak **ilke tanımı oluşturun** komutu:</span><span class="sxs-lookup"><span data-stu-id="a15c9-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="a15c9-144">Bu komut çıktı benzer toohello şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="a15c9-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="a15c9-145">İlke tanımı MyPolicy veri oluşturma: PolicyName: MyPolicy veri: Policydefinitionıd: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="a15c9-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="a15c9-146">Veri: PolicyType: özel veri: DisplayName: tanımlanmamış veri: Açıklama: tanımlanmamış veri: PolicyRule: alan konumu =, içinde [westus, northcentralus], = etkisi = Reddet</span><span class="sxs-lookup"><span data-stu-id="a15c9-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="a15c9-147">bir ilke kapsamında istediğiniz hello kullan hello tooassign **Policydefinitionıd** hello önceki komuttan döndürdü.</span><span class="sxs-lookup"><span data-stu-id="a15c9-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="a15c9-148">Aşağıdaki örnek hello, bu kapsamı hello abonelik ancak tooresource grupları veya bireysel kaynakları kapsamını belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a15c9-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="a15c9-149">Azure ilke ataması oluşturma MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### /</span><span class="sxs-lookup"><span data-stu-id="a15c9-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="a15c9-150">Al, değiştirmek veya ilke tanımları hello kullanarak kaldırmak **ilke tanımı Göster**, **ilke tanım kümesini**, ve **ilke tanımı silin** komutları.</span><span class="sxs-lookup"><span data-stu-id="a15c9-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="a15c9-151">Benzer şekilde, alma, değiştirebilir veya hello kullanarak ilke atamalarını kaldırın **ilke ataması Göster**, **ilke ataması kümesi**, ve **ilke atamasını silin** komutları .</span><span class="sxs-lookup"><span data-stu-id="a15c9-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="a15c9-152">Bir kaynak grubunu şablon olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="a15c9-152">Export a resource group as a template</span></span>
<span data-ttu-id="a15c9-153">Mevcut bir kaynak grubu için hello kaynak grubu için hello Resource Manager şablonu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a15c9-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="a15c9-154">Dışarı aktarma hello şablon iki avantajları sunar:</span><span class="sxs-lookup"><span data-stu-id="a15c9-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="a15c9-155">Tüm hello altyapı hello şablonda tanımlı olduğundan hello çözümün gelecekteki dağıtımlar kolayca otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a15c9-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="a15c9-156">Çözümünüzü temsil eden JSON hello bakarak şablon söz dizimi ile tanıdık.</span><span class="sxs-lookup"><span data-stu-id="a15c9-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="a15c9-157">Hello Azure CLI kullanarak, kaynak grubunuzun hello geçerli durumunu temsil eden bir şablonu dışarı veya belirli bir dağıtım için kullanılan hello şablonunu indirebilir.</span><span class="sxs-lookup"><span data-stu-id="a15c9-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="a15c9-158">**Bir kaynak grubu için Hello şablonu dışarı aktarma** -değişiklikleri tooa kaynak grubuna yapılan ve tooretrieve geçerli durumuna JSON gösterimi hello olduğunda bu yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="a15c9-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="a15c9-159">Ancak, parametre ve değişken, yalnızca en az sayıda hello oluşturulan şablonu içerir.</span><span class="sxs-lookup"><span data-stu-id="a15c9-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="a15c9-160">Merhaba değerlerinin hello şablonu sabit kodlanmış durumdadır.</span><span class="sxs-lookup"><span data-stu-id="a15c9-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="a15c9-161">Merhaba dağıtım farklı ortamlar için özelleştirebileceğiniz şekilde oluşturulan hello şablonunun dağıtmadan önce tooconvert daha fazla hello değeri parametreleri isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="a15c9-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="a15c9-162">Merhaba çalıştırmak bir kaynak grubu tooa yerel dizin için tooexport hello şablonu `azure group export` hello aşağıdaki örnekte gösterildiği gibi komutu.</span><span class="sxs-lookup"><span data-stu-id="a15c9-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="a15c9-163">(İşletim sistemi ortamınız için uygun yerel bir dizine değiştirin.)</span><span class="sxs-lookup"><span data-stu-id="a15c9-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="a15c9-164">**Belirli bir dağıtımın Hello şablonunu indirme** --kullanılan toodeploy kaynaklar tooview hello gerçek şablon gerektiğinde bu faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="a15c9-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="a15c9-165">tüm parametreler ve değişkenler hello özgün dağıtım için tanımlanan Hello şablonu içerir.</span><span class="sxs-lookup"><span data-stu-id="a15c9-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="a15c9-166">Ancak, birisi, kuruluşunuzda değişiklikleri toohello kaynak grubu hello tanımı dışında hello şablonunda yaptıysanız, bu şablonu hello hello kaynak grubunun geçerli durumunu temsil etmez.</span><span class="sxs-lookup"><span data-stu-id="a15c9-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="a15c9-167">Merhaba çalıştırmak belirli dağıtım tooa yerel bir dizin için kullanılan toodownload hello şablonu `azure group deployment template download` komutu.</span><span class="sxs-lookup"><span data-stu-id="a15c9-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="a15c9-168">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a15c9-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="a15c9-169">Şablonu dışarı aktarma Önizleme aşamasındadır ve tüm kaynak türleri şu anda bir şablonu dışarı aktarma desteklemez.</span><span class="sxs-lookup"><span data-stu-id="a15c9-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="a15c9-170">Bir şablon tooexport çalışırken, bazı kaynaklar dışarı aktarılmadığı bildiren bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a15c9-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="a15c9-171">El ile gerekirse, bu kaynakları indirdikten sonra şablonunuzda tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="a15c9-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a15c9-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a15c9-172">Next steps</span></span>
* <span data-ttu-id="a15c9-173">Dağıtım işlemlerini tooget ayrıntılarını ve hello Azure CLI ile dağıtım hatalarını giderme bkz [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a15c9-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="a15c9-174">Bir uygulama veya komut dosyası tooaccess kaynakları toouse hello CLI tooset istiyorsanız, bkz: [kullanım Azure CLI toocreate bir hizmet sorumlusu tooaccess kaynakları](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a15c9-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="a15c9-175">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a15c9-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

