---
title: "Azure şablonları arasındaki aaaPass karmaşık değerleri | Microsoft Docs"
description: "Gösterir karmaşık nesneler tooshare durumu verilerinin Azure Resource Manager şablonları ile bağlı şablonları kullanma yaklaşım önerilir."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="fcd6e-103">Paylaşım durumu tooand Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="fcd6e-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="fcd6e-104">Bu konu, yönetme ve şablonlar içindeki durumu paylaşımı için en iyi uygulamaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="fcd6e-105">Hello parametreler ve değişkenler bu konuda gösterilen örnekler tanımlayabilirsiniz nesnelerin hello türü tooconveniently Dağıtım gereksinimlerinizi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="fcd6e-106">Bu örnekler, ortamınız için anlamlı özellik değerlerini kendi nesneleriyle uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="fcd6e-107">Bu konuda daha büyük bir Teknik İnceleme bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="fcd6e-108">tam kağıt tooread hello karşıdan [World sınıfı Resource Manager şablonları konuları ve kanıtlanmış yöntemler](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="fcd6e-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="fcd6e-109">Standart yapılandırma ayarlarını belirtin</span><span class="sxs-lookup"><span data-stu-id="fcd6e-109">Provide standard configuration settings</span></span>
<span data-ttu-id="fcd6e-110">Toplam esneklik ve sayısız Çeşitlemeler sağlayan bir şablon sunmak yerine, genel bir desen tooprovide bilinen yapılandırmaları Seçimi ' dir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="fcd6e-111">Etkin kullanıcılar korumalı alan, küçük, Orta ve büyük gibi standart ısı boyutları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="fcd6e-112">Diğer ısı boyutları community edition veya enterprise edition gibi ürün teklifleri gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="fcd6e-113">Diğer durumlarda, harita azaltmak gibi iş yüküne özgü yapılandırmaları bir teknolojisi – olabilir veya hiç sql.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="fcd6e-114">Karmaşık nesneler ile bazen "özellik paketleri" bilinen veri topluluklarını değişkenleri oluşturun ve o veri toodrive hello kaynak bildirimi şablonunuzda kullanın.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="fcd6e-115">Bu yaklaşım, müşteri için yapılandırılmış farklı boyutlarda iyi, bilinen yapılandırmaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="fcd6e-116">Bilinen yapılandırmaları hello şablon kullanıcılarının gerekir küme boyutlandırma platform kaynak kısıtlamaları kendi faktörünü üzerinde belirlemek ve depolama hesapları ve diğer kaynakların bölümleme matematik tooidentify hello kaynaklanan yapın (toocluster boyutu nedeniyle ve Kaynak sınırlamaları).</span><span class="sxs-lookup"><span data-stu-id="fcd6e-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="fcd6e-117">Ayrıca toomaking hello müşteri için daha iyi bir deneyim, birkaç bilinen yapılandırmaları daha kolay toosupport olan ve yoğunluğu daha yüksek düzeyde sunmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="fcd6e-118">örnekte gösterildiği nasıl aşağıdaki hello veri koleksiyonları için karmaşık nesneler içeren toodefine değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="fcd6e-119">Merhaba koleksiyonları, sanal makine boyutu, ağ ayarları, işletim sistemi ayarlarını ve kullanılabilirlik ayarları için kullanılan değerleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="fcd6e-120">Bu hello fark **tshirtSize** değişkeni, bir parametre aracılığıyla sağlanan hello ısı boyutu art arda ekler (**küçük**, **orta**, **büyük**) toohello metin **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="fcd6e-121">Bu değişken tooretrieve hello ilişkili karmaşık nesne değişkeni bu ısı boyut için kullanın.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="fcd6e-122">Ardından hello şablondaki daha sonra bu değişkenleri başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="fcd6e-123">Merhaba özelliği tooreference adlı-değişkenleri ve bunların özelliklerini hello şablon söz dizimi basitleştirir ve kolay toounderstand bağlamı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="fcd6e-124">Aşağıdaki örneğine hello tooset değerleri daha önce gösterilen hello nesneleri kullanılarak bir kaynak toodeploy tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="fcd6e-125">Örneğin, hello VM boyutu hello değeri alınırken tarafından ayarlanır `variables('tshirtSize').vmSize` hello disk boyutu alınır için hello değeri while `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="fcd6e-126">Ayrıca, bağlantılı bir şablon için hello değerle ayarlamak için URI hello `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a><span data-ttu-id="fcd6e-127">Geçişi durumu tooa şablonu</span><span class="sxs-lookup"><span data-stu-id="fcd6e-127">Pass state tooa template</span></span>
<span data-ttu-id="fcd6e-128">Bir şablonu doğrudan dağıtım sırasında sağladığınız parametreler aracılığıyla içine durumu paylaşır.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="fcd6e-129">şu Tablo listeleri yaygın olarak kullanılan parametreler şablonlarındaki hello.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="fcd6e-130">Ad</span><span class="sxs-lookup"><span data-stu-id="fcd6e-130">Name</span></span> | <span data-ttu-id="fcd6e-131">Değer</span><span class="sxs-lookup"><span data-stu-id="fcd6e-131">Value</span></span> | <span data-ttu-id="fcd6e-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcd6e-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fcd6e-133">location</span><span class="sxs-lookup"><span data-stu-id="fcd6e-133">location</span></span> |<span data-ttu-id="fcd6e-134">Azure bölgeleri kısıtlanmış listesinden dize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="fcd6e-135">Merhaba kaynakları dağıtıldığı hello konumu.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="fcd6e-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="fcd6e-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="fcd6e-137">Dize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-137">String</span></span> |<span data-ttu-id="fcd6e-138">Merhaba hello VM'in disklerini yerleştirildiği depolama hesabı için benzersiz DNS adı</span><span class="sxs-lookup"><span data-stu-id="fcd6e-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="fcd6e-139">domainName</span><span class="sxs-lookup"><span data-stu-id="fcd6e-139">domainName</span></span> |<span data-ttu-id="fcd6e-140">Dize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-140">String</span></span> |<span data-ttu-id="fcd6e-141">Merhaba biçiminde hello genel olarak erişilebilir jumpbox VM etki alanı adı: **{domainName}. { konum}.cloudapp.com** örneğin: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="fcd6e-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="fcd6e-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="fcd6e-142">adminUsername</span></span> |<span data-ttu-id="fcd6e-143">Dize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-143">String</span></span> |<span data-ttu-id="fcd6e-144">Merhaba VM'ler için kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="fcd6e-144">Username for hello VMs</span></span> |
| <span data-ttu-id="fcd6e-145">Admınpassword</span><span class="sxs-lookup"><span data-stu-id="fcd6e-145">adminPassword</span></span> |<span data-ttu-id="fcd6e-146">Dize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-146">String</span></span> |<span data-ttu-id="fcd6e-147">Merhaba VM'ler için parola</span><span class="sxs-lookup"><span data-stu-id="fcd6e-147">Password for hello VMs</span></span> |
| <span data-ttu-id="fcd6e-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-148">tshirtSize</span></span> |<span data-ttu-id="fcd6e-149">Sunulan ısı boyutları kısıtlanmış listesinden dize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="fcd6e-150">Ölçek birimi boyutu tooprovision adlı hello.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="fcd6e-151">Örneğin, "Küçük", "Medium", "Büyük"</span><span class="sxs-lookup"><span data-stu-id="fcd6e-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="fcd6e-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="fcd6e-152">virtualNetworkName</span></span> |<span data-ttu-id="fcd6e-153">Dize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-153">String</span></span> |<span data-ttu-id="fcd6e-154">Tüketici hello hello sanal ağın adını toouse istemektedir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="fcd6e-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="fcd6e-155">enableJumpbox</span></span> |<span data-ttu-id="fcd6e-156">(Etkin/devre dışı) kısıtlanmış listeden dize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="fcd6e-157">Tanımlayan parametresi olup olmadığını tooenable jumpbox hello ortamı için.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="fcd6e-158">Değerler: "etkin", "disabled"</span><span class="sxs-lookup"><span data-stu-id="fcd6e-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="fcd6e-159">Merhaba **tshirtSize** hello önceki bölümünde kullanılan parametre olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="fcd6e-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="fcd6e-160">Durum toolinked şablonları geçirin</span><span class="sxs-lookup"><span data-stu-id="fcd6e-160">Pass state toolinked templates</span></span>
<span data-ttu-id="fcd6e-161">Toolinked şablonları bağlanırken genellikle statik bir karışımını kullanın ve değişkenleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="fcd6e-162">Statik değişkenler</span><span class="sxs-lookup"><span data-stu-id="fcd6e-162">Static variables</span></span>
<span data-ttu-id="fcd6e-163">Statik değişkenler genellikle kullanılan tooprovide temel gibi bir şablon kullanılan URL'leri değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="fcd6e-164">Şablon alıntı aşağıdaki hello içinde `templateBaseUrl` Github'da hello şablon hello kök konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="fcd6e-165">Merhaba sonraki satıra yeni bir değişken oluşturur `sharedTemplateUrl` hello temel URL hello bilinen hello paylaşılan kaynakları şablonunun adını ile birleştirir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="fcd6e-166">Bu satır, bir karmaşık nesne değişkeni kullanılan toostore ısı boyutu hello temel URL birleştirilmiş toohello olduğu bilinen yapılandırma şablon konumu ve hello depolanan `vmTemplate` özelliği.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="fcd6e-167">Bu yaklaşımın avantajı Hello hello şablon konumu değişirse, yalnızca tüm bağlı hello şablonlarda geçirir tek bir yerde toochange hello statik değişken olmanızdır.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="fcd6e-168">Oluşturulan değişkenleri</span><span class="sxs-lookup"><span data-stu-id="fcd6e-168">Generated variables</span></span>
<span data-ttu-id="fcd6e-169">Toplama toostatic değişkenlerde çeşitli değişkenler dinamik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="fcd6e-170">Bu bölümde bazı oluşturulan değişkenlerin hello ortak türlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="fcd6e-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="fcd6e-171">tshirtSize</span></span>
<span data-ttu-id="fcd6e-172">Örnekler hello yukarıdaki ile oluşturulan bu değişken hakkında bilgi sahibi.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="fcd6e-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="fcd6e-173">networkSettings</span></span>
<span data-ttu-id="fcd6e-174">Bir kapasite, özelliği veya uçtan uca kapsamlı çözüm şablonu hello bağlı şablonları mevcut kaynaklar genellikle bir ağda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="fcd6e-175">Bir kolay yaklaşım karmaşık nesne toostore ağ ayarlarını toouse olduğu ve bunları toolinked şablonları geçirin.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="fcd6e-176">Ağ Ayarları iletişim kurulurken bir örnek aşağıda görülebilir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="fcd6e-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="fcd6e-177">availabilitySettings</span></span>
<span data-ttu-id="fcd6e-178">Bağlantılı şablonlarında oluşturulan kaynakları, genellikle bir kullanılabilirlik kümesine yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="fcd6e-179">Merhaba, aşağıdaki örneğine içinde hello kullanılabilirlik kümesi adı belirtilen ve hata etki alanı da hello ve etki alanı sayısı toouse güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="fcd6e-180">Önek olarak bir ad kullanabilirsiniz birden çok kullanılabilirlik kümesine (örneğin, bir ana düğüm için) ve veri düğümlerini için başka bir gereksinim duyarsanız, birden çok kullanılabilirlik kümesine belirtin veya belirli bir ısı boyutu için bir değişken oluşturmak için daha önce gösterilen hello modeli izleyin.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="fcd6e-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="fcd6e-181">storageSettings</span></span>
<span data-ttu-id="fcd6e-182">Depolama ayrıntıları genellikle bağlı şablonları ile paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="fcd6e-183">Aşağıda, hello örnekte bir *storageSettings* nesnesi, depolama hesabı ve kapsayıcı adları hello hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="fcd6e-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="fcd6e-184">osSettings</span></span>
<span data-ttu-id="fcd6e-185">Bağlantılı şablonlarıyla bilinen farklı yapılandırma türlerine toopass işletim sistemi ayarlarını toovarious düğümleri türlerini gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="fcd6e-186">Karmaşık bir nesne bir kolay bir yolu toostore ve paylaşımı işletim sistemi bilgileri ve ayrıca daha kolay toosupport kılar dağıtımı için birden çok işletim sistemi seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="fcd6e-187">Merhaba aşağıdaki örnek gösteren bir nesne için *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="fcd6e-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="fcd6e-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="fcd6e-188">machineSettings</span></span>
<span data-ttu-id="fcd6e-189">Oluşturulan bir değişken *machineSettings* bir VM oluşturmak için çekirdek değişkenleri bir karışımını içeren karmaşık bir nesne.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="fcd6e-190">Merhaba değişkenleri yönetici kullanıcı adı ve parola, hello VM adları için bir önek ve bir işletim sistemi görüntüsü başvurusu içerir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="fcd6e-191">Unutmayın *osImageReference* alır hello hello değerlerinden *osSettings* hello ana şablonda tanımlanan değişken.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="fcd6e-192">Anlamı kolayca değiştirebilirsiniz hello işletim sistemi için bir VM — tamamen veya bir şablon tüketici hello tercihine göre.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="fcd6e-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="fcd6e-193">vmScripts</span></span>
<span data-ttu-id="fcd6e-194">Merhaba *vmScripts* hello betikleri toodownload hakkında ayrıntılar içeren nesne ve dış ve iç başvuruları dahil olmak üzere bir VM örneğinde yürütün.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="fcd6e-195">Dışında hello altyapı başvurular içerir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="fcd6e-196">Merhaba yüklü yazılımı yüklü ve yapılandırma iç başvurular içerir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="fcd6e-197">Merhaba kullandığınız *scriptsToDownload* özelliği toolist hello toodownload toohello VM komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="fcd6e-198">Bu nesne farklı türde eylemler için başvurular toocommand satırı değişkenlerini de içerir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="fcd6e-199">Bu eylemler hello Varsayılan yüklemede tek tek her düğüm, tüm düğümler dağıtıldıktan sonra çalıştırılan bir yükleme ve şablon verilen belirli tooa olabilecek ek betik yürütme içerir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="fcd6e-200">Bu, bir şablon toodeploy arbiter toodeliver yüksek kullanılabilirlik gerektiren MongoDB örneğidir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="fcd6e-201">Merhaba *arbiterNodeInstallCommand* çok eklenen*vmScripts* tooinstall hello arbiter.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="fcd6e-202">Merhaba değişkenleri hello belirli metin tooexecute hello komut hello uygun değerlerle tanımlamak hello değişkenleri nerede bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="fcd6e-203">Bir şablondan dönüş durumu</span><span class="sxs-lookup"><span data-stu-id="fcd6e-203">Return state from a template</span></span>
<span data-ttu-id="fcd6e-204">Yalnızca, bir şablona veri geçişi, paylaşım veri geri toohello arama şablonu de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="fcd6e-205">Merhaba, **çıkarır** bölüm bağlantılı şablonu, hello kaynak şablonu tarafından kullanılabilecek anahtar/değer çiftleri sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="fcd6e-206">Merhaba aşağıdaki örnekte nasıl toopass bağlantılı bir şablonda oluşturulan özel IP adresi hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="fcd6e-207">Merhaba ana şablonda sözdizimi aşağıdaki hello ile bu verileri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fcd6e-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="fcd6e-208">Bu ifadede hello çıkışları bölüm veya hello kaynakları hello ana şablon bölümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="fcd6e-209">Merhaba ifade hello değişkenler bölümünde kullanamazsınız, çünkü hello çalışma zamanı durumuna dayanır.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="fcd6e-210">tooreturn bu değer şablondan hello ana kullanın:</span><span class="sxs-lookup"><span data-stu-id="fcd6e-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="fcd6e-211">Bağlantılı şablonu tooreturn veri diski bir sanal makine için bölüm hello kullanma örneği çıkarır için bkz: [bir sanal makine için birden fazla veri diski oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fcd6e-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="fcd6e-212">Sanal makine için kimlik doğrulama ayarlarını tanımlayın</span><span class="sxs-lookup"><span data-stu-id="fcd6e-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="fcd6e-213">Merhaba kullanabileceğiniz yapılandırma ayarları toospecify hello kimlik doğrulama ayarları bir sanal makine için daha önce gösterilen aynı düzeni.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="fcd6e-214">Parametre geçirme için kimlik doğrulama hello türünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-214">You create a parameter for passing in hello type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="fcd6e-215">Merhaba farklı kimlik doğrulama türleri ve hangi tür hello parametresinin hello değere göre bu dağıtım için kullanılan bir değişken toostore değişkenleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="fcd6e-216">Merhaba sanal makine tanımlarken hello ayarlamak **osProfile** oluşturduğunuz toohello değişkeni.</span><span class="sxs-lookup"><span data-stu-id="fcd6e-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="fcd6e-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fcd6e-217">Next steps</span></span>
* <span data-ttu-id="fcd6e-218">toolearn hello şablon hello bölümlerini hakkında bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="fcd6e-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="fcd6e-219">bir şablonu içinde kullanılabilir toosee hello işlevleri bkz [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="fcd6e-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
