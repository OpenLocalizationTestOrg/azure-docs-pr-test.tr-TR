---
title: "Azure dağıtımının aaaLink şablonları | Microsoft Docs"
description: "Toouse bir Azure Resource Manager şablonu toocreate şablonlarında modüler şablonu çözümü nasıl bağlı açıklar. Nasıl toopass parametre değerleri, bir parametre dosyası belirtin ve dinamik olarak URL'leri oluşturulan gösterir."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="c3d21-104">Azure kaynaklarını dağıtırken bağlı şablonları kullanma</span><span class="sxs-lookup"><span data-stu-id="c3d21-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="c3d21-105">Gelen bir Azure Resource Manager şablonu içinde toodecompose sağlayan tooanother şablonu dağıtımınızı hedeflenen, amaca şablonları kümesine bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="c3d21-106">Birkaç kod sınıfı bir uygulamaya gibi ayırma, ayrıştırma sınama, yeniden kullanılmasını ve okunabilirliği açısından faydaları sunar.</span><span class="sxs-lookup"><span data-stu-id="c3d21-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="c3d21-107">Bir ana şablon tooa bağlantılı şablondan parametreleri geçirebilirsiniz ve bu parametrelerin doğrudan tooparameters veya şablon çağırma hello tarafından kullanıma sunulan değişkenleri eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="c3d21-108">Merhaba bağlantılı şablonu da şablonlar arasında iki yönlü veri değişimi etkinleştirme bir çıktı değişken geri toohello kaynak şablonu geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="c3d21-109">Tooa şablon bağlama</span><span class="sxs-lookup"><span data-stu-id="c3d21-109">Linking tooa template</span></span>
<span data-ttu-id="c3d21-110">Dağıtım kaynağı hello ana şablonu içindeki noktaları toohello bağlantılı şablon ekleyerek iki şablonları arasında bir bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3d21-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="c3d21-111">Merhaba ayarladığınız **templateLink** özelliği toohello hello bağlantılı şablon URI'si.</span><span class="sxs-lookup"><span data-stu-id="c3d21-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="c3d21-112">Şablonunuzdaki doğrudan veya bir parametre dosyası hello bağlantılı şablonu için parametre değerlerini sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="c3d21-113">Merhaba aşağıdaki örnek kullanır hello **parametreleri** özelliği toospecify doğrudan bir parametre değeri.</span><span class="sxs-lookup"><span data-stu-id="c3d21-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="c3d21-114">Diğer kaynak türleri gibi hello bağlantılı şablonu ve kaynaklar arasındaki bağımlılıkları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="c3d21-115">Bu nedenle, diğer kaynakları bir çıkış değeri hello bağlantılı şablondan gerektirdiğinde hello bağlantılı şablonu daha önce dağıtılan emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="c3d21-116">Veya diğer kaynaklara hello bağlantılı şablonunu kullanır, diğer kaynakları hello bağlantılı şablonu önce dağıtılan emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="c3d21-117">Bir değer sözdizimi aşağıdaki hello ile bağlantılı bir şablondan alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3d21-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="c3d21-118">Merhaba Kaynak Yöneticisi hizmeti mümkün tooaccess hello bağlantılı şablonu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c3d21-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="c3d21-119">Yerel bir dosya veya yalnızca yerel ağınızdaki hello bağlantılı şablonu için kullanılabilir bir dosya belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="c3d21-120">İçerir ya da bir URI değeri yalnızca sağlayabilir **http** veya **https**.</span><span class="sxs-lookup"><span data-stu-id="c3d21-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="c3d21-121">Bir depolama hesabı ve kullanım bağlantılı şablonunuzda gibi aşağıdaki örneğine hello gösterilen bu öğe için URI hello tooplace bir seçenektir:</span><span class="sxs-lookup"><span data-stu-id="c3d21-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="c3d21-122">Merhaba bağlantılı şablon dışarıdan kullanılabilir olması gerekse de toobe genel olarak kullanılabilir toohello ortak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c3d21-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="c3d21-123">Erişilebilir tooonly hello depolama hesabı sahibi olan şablon tooa özel depolama hesabınız ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="c3d21-124">Ardından, bir paylaşılan erişim imzası (SAS) belirteci tooenable erişim dağıtımı sırasında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3d21-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="c3d21-125">Merhaba bağlantılı şablon için bu SAS belirteci toohello URI ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c3d21-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="c3d21-126">Bir şablonda bir depolama hesabı ayarlama ve bir SAS belirteci oluşturma adımları için bkz [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy.md) veya [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c3d21-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="c3d21-127">Aşağıdaki örneğine hello üst şablon bu bağlantılar tooanother şablonu gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="c3d21-128">Merhaba bağlantılı şablon parametre olarak geçirilen bir SAS belirteci ile erişilir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="c3d21-129">Merhaba belirteci güvenli bir dize geçirilen olsa bile, hello hello SAS belirteci dahil olmak üzere hello bağlantılı şablon URI'sini hello dağıtım işlemlerine günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="c3d21-130">toolimit Etkilenme hello belirteci için bir sona erme ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c3d21-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="c3d21-131">Resource Manager her bağlantılı bir şablon ayrı bir dağıtım işler.</span><span class="sxs-lookup"><span data-stu-id="c3d21-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="c3d21-132">Hello dağıtım geçmişini hello kaynak grubu için ayrı dağıtımları hello üst ve iç içe geçmiş şablonları için bkz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![dağıtım geçmişi](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="c3d21-134">Tooa parametre dosyası bağlama</span><span class="sxs-lookup"><span data-stu-id="c3d21-134">Linking tooa parameter file</span></span>
<span data-ttu-id="c3d21-135">Merhaba sonraki örnek kullanır hello **parametersLink** özelliği toolink tooa parametre dosyası.</span><span class="sxs-lookup"><span data-stu-id="c3d21-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="c3d21-136">Merhaba URI değeri hello bağlantılı parametre dosyası yerel bir dosya olamaz ve ya da içermelidir **http** veya **https**.</span><span class="sxs-lookup"><span data-stu-id="c3d21-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="c3d21-137">Merhaba parametre dosyası da bir SAS belirteci üzerinden sınırlı tooaccess olabilir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="c3d21-138">Değişkenleri toolink şablonlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="c3d21-138">Using variables toolink templates</span></span>
<span data-ttu-id="c3d21-139">Merhaba önceki örneklerde hello şablon bağlantılar için sabit kodlanmış URL değerleri gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="c3d21-140">Bu yaklaşım basit bir şablon için çalışabilir, ancak iyi çok sayıda modüler şablonları çalışırken çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="c3d21-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="c3d21-141">Bunun yerine, hello ana şablon için bir temel URL depolar statik bir değişkeni oluşturun ve ardından dinamik olarak URL'leri için temel bu URL'den bağlı hello şablonları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3d21-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="c3d21-142">Bu yaklaşımın avantajı Hello toochange hello statik değişkende hello ana şablon yalnızca gerektiğinden, taşıma veya çatalı hello şablonu kolayca ' dir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="c3d21-143">Merhaba ana şablon hello hello boyunca URI şablonunu ayrılmış doğru geçirir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="c3d21-144">Merhaba aşağıdaki örnekte nasıl toouse temel URL toocreate iki URL'ler için bağlantılı gösterir şablonları (**sharedTemplateUrl** ve **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="c3d21-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="c3d21-145">Aynı zamanda [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello geçerli şablon için temel URL hello ve hello diğer şablonlar için bu tooget hello URL kullanmak aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="c3d21-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="c3d21-146">Bu yaklaşım şablon konumunuza değişirse yararlı olur (belki de son tooversioning) veya tooavoid sabit hello şablon dosyası URL'lerinde kodlama istiyor.</span><span class="sxs-lookup"><span data-stu-id="c3d21-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="c3d21-147">Tam örnek</span><span class="sxs-lookup"><span data-stu-id="c3d21-147">Complete example</span></span>
<span data-ttu-id="c3d21-148">Örnek şablonları aşağıdaki hello bağlı şablonları tooillustrate Basitleştirilmiş düzenlenmesi bu makalede birkaç hello kavramları göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="c3d21-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="c3d21-149">Bu genel erişimi bir depolama hesabıyla aynı kapsayıcıda kapalı toohello hello şablonları eklenmiş varsayar.</span><span class="sxs-lookup"><span data-stu-id="c3d21-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="c3d21-150">Merhaba bağlantılı şablon geçirmeden bir değeri geri toohello ana şablon hello **çıkarır** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c3d21-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="c3d21-151">Merhaba **parent.json** dosya oluşur:</span><span class="sxs-lookup"><span data-stu-id="c3d21-151">hello **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="c3d21-152">Merhaba **helloworld.json** dosya oluşur:</span><span class="sxs-lookup"><span data-stu-id="c3d21-152">hello **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="c3d21-153">PowerShell'de, hello kapsayıcı için bir belirteç almak ve hello şablonlarıyla dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3d21-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="c3d21-154">Azure CLI 2. 0'da, hello kapsayıcı için bir belirteç almak ve başlangıç şablonları koddan hello ile dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3d21-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="c3d21-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c3d21-155">Next steps</span></span>
* <span data-ttu-id="c3d21-156">toolearn hello hello dağıtım sırası, kaynaklar için tanımlama hakkında bkz [Azure Resource Manager'da bağımlılıkları tanımlama](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="c3d21-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="c3d21-157">toolearn toodefine bir kaynak ancak oluşturmak nasıl, birçok örneklerini görmek [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="c3d21-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

