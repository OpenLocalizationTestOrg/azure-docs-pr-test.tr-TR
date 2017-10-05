---
title: "Azure şablonu arasındaki karmaşık değerleri geçirmek | Microsoft Docs"
description: "Gösterir karmaşık nesne durumu verileri Azure Resource Manager şablonları ve bağlı şablonları ile paylaşmak için kullanmayı yaklaşımları önerilir."
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
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="183eb-103">Azure Resource Manager şablonları gelen ve giden paylaşım durumu</span><span class="sxs-lookup"><span data-stu-id="183eb-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="183eb-104">Bu konu, yönetme ve şablonlar içindeki durumu paylaşımı için en iyi uygulamaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="183eb-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="183eb-105">Bu konuda gösterilen değişkenleri ve parametreleri tanımlayabilirsiniz nesnelerin türü örnekleridir rahat Dağıtım gereksinimlerinizi düzenlemek için.</span><span class="sxs-lookup"><span data-stu-id="183eb-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="183eb-106">Bu örnekler, ortamınız için anlamlı özellik değerlerini kendi nesneleriyle uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="183eb-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="183eb-107">Bu konuda daha büyük bir Teknik İnceleme bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="183eb-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="183eb-108">Tam kağıt okumak için karşıdan [World sınıfı Resource Manager şablonları konuları ve kanıtlanmış yöntemler](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="183eb-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="183eb-109">Standart yapılandırma ayarlarını belirtin</span><span class="sxs-lookup"><span data-stu-id="183eb-109">Provide standard configuration settings</span></span>
<span data-ttu-id="183eb-110">Toplam esneklik ve sayısız Çeşitlemeler sağlayan bir şablon sunmak yerine, genel bir desen bilinen yapılandırmaları seçimi sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="183eb-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="183eb-111">Etkin kullanıcılar korumalı alan, küçük, Orta ve büyük gibi standart ısı boyutları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="183eb-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="183eb-112">Diğer ısı boyutları community edition veya enterprise edition gibi ürün teklifleri gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="183eb-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="183eb-113">Diğer durumlarda, harita azaltmak gibi iş yüküne özgü yapılandırmaları bir teknolojisi – olabilir veya hiç sql.</span><span class="sxs-lookup"><span data-stu-id="183eb-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="183eb-114">Karmaşık nesneleriyle bazen "özellik paketleri" bilinen veri topluluklarını değişkenleri oluşturmak ve bu verileri kaynak bildirimi şablonunuzda sürücü için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="183eb-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="183eb-115">Bu yaklaşım, müşteri için yapılandırılmış farklı boyutlarda iyi, bilinen yapılandırmaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="183eb-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="183eb-116">Bilinen yapılandırmaları, şablonun kullanıcıları gerekir, kendi boyutlandırma küme belirlemek, platform kaynak kısıtlamaları faktörü ve sonuçta elde edilen bölümleme depolama hesapları ve diğer kaynakları (nedeniyle, küme boyutu ve kaynak tanımlamak için matematik yapın kısıtlamaları).</span><span class="sxs-lookup"><span data-stu-id="183eb-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="183eb-117">Daha iyi bir deneyim müşteri için yapmanın yanı sıra birkaç bilinen yapılandırmaları daha kolay desteklemek ve yoğunluğu daha yüksek düzeyde sunmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="183eb-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="183eb-118">Aşağıdaki örnek veri koleksiyonları için karmaşık nesneler içeren değişkenleri tanımlayın gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="183eb-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="183eb-119">Koleksiyonları, sanal makine boyutu, ağ ayarları, işletim sistemi ayarlarını ve kullanılabilirlik ayarları için kullanılan değerleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="183eb-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="183eb-120">Dikkat **tshirtSize** değişkeni, bir parametre aracılığıyla sağlanan ısı boyutu art arda ekler (**küçük**, **orta**, **büyük** ) metne **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="183eb-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="183eb-121">Bu ısı boyut ilişkili karmaşık nesne değişkeni almak için bu değişkeni kullanın.</span><span class="sxs-lookup"><span data-stu-id="183eb-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="183eb-122">Ardından şablonunda daha sonra bu değişkenleri başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="183eb-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="183eb-123">Adlandırılmış değişkenleri ve bunların özelliklerini başvuru olanağı şablon söz dizimi basitleştirir ve bağlamı anlamak daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="183eb-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="183eb-124">Aşağıdaki örnek değerleri ayarlamak için daha önce gösterilen nesneleri kullanarak dağıtmak için bir kaynak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="183eb-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="183eb-125">Örneğin, VM boyutu değeri alarak ayarlanır `variables('tshirtSize').vmSize` disk boyutunu alınır için değer while `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="183eb-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="183eb-126">Ek olarak, bağlantılı bir şablon için URI değeri ile ayarlanır `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="183eb-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-to-a-template"></a><span data-ttu-id="183eb-127">Bir şablon durumuna geçişi</span><span class="sxs-lookup"><span data-stu-id="183eb-127">Pass state to a template</span></span>
<span data-ttu-id="183eb-128">Bir şablonu doğrudan dağıtım sırasında sağladığınız parametreler aracılığıyla içine durumu paylaşır.</span><span class="sxs-lookup"><span data-stu-id="183eb-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="183eb-129">Aşağıdaki tabloda şablonlarındaki yaygın olarak kullanılan parametreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="183eb-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="183eb-130">Ad</span><span class="sxs-lookup"><span data-stu-id="183eb-130">Name</span></span> | <span data-ttu-id="183eb-131">Değer</span><span class="sxs-lookup"><span data-stu-id="183eb-131">Value</span></span> | <span data-ttu-id="183eb-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="183eb-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="183eb-133">location</span><span class="sxs-lookup"><span data-stu-id="183eb-133">location</span></span> |<span data-ttu-id="183eb-134">Azure bölgeleri kısıtlanmış listesinden dize</span><span class="sxs-lookup"><span data-stu-id="183eb-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="183eb-135">Kaynakları dağıtıldığı konumu.</span><span class="sxs-lookup"><span data-stu-id="183eb-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="183eb-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="183eb-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="183eb-137">Dize</span><span class="sxs-lookup"><span data-stu-id="183eb-137">String</span></span> |<span data-ttu-id="183eb-138">VM'in disklerini yerleştirildiği depolama hesabı için benzersiz DNS adı</span><span class="sxs-lookup"><span data-stu-id="183eb-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="183eb-139">domainName</span><span class="sxs-lookup"><span data-stu-id="183eb-139">domainName</span></span> |<span data-ttu-id="183eb-140">Dize</span><span class="sxs-lookup"><span data-stu-id="183eb-140">String</span></span> |<span data-ttu-id="183eb-141">Etki alanı adı biçiminde VM genel olarak erişilebilir jumpbox: **{domainName}. { konum}.cloudapp.com** örneğin: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="183eb-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="183eb-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="183eb-142">adminUsername</span></span> |<span data-ttu-id="183eb-143">Dize</span><span class="sxs-lookup"><span data-stu-id="183eb-143">String</span></span> |<span data-ttu-id="183eb-144">Sanal makineleri için kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="183eb-144">Username for the VMs</span></span> |
| <span data-ttu-id="183eb-145">Admınpassword</span><span class="sxs-lookup"><span data-stu-id="183eb-145">adminPassword</span></span> |<span data-ttu-id="183eb-146">Dize</span><span class="sxs-lookup"><span data-stu-id="183eb-146">String</span></span> |<span data-ttu-id="183eb-147">VM'ler için parola</span><span class="sxs-lookup"><span data-stu-id="183eb-147">Password for the VMs</span></span> |
| <span data-ttu-id="183eb-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="183eb-148">tshirtSize</span></span> |<span data-ttu-id="183eb-149">Sunulan ısı boyutları kısıtlanmış listesinden dize</span><span class="sxs-lookup"><span data-stu-id="183eb-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="183eb-150">Adlandırılmış ölçek birimi boyutu sağlama.</span><span class="sxs-lookup"><span data-stu-id="183eb-150">The named scale unit size to provision.</span></span> <span data-ttu-id="183eb-151">Örneğin, "Küçük", "Medium", "Büyük"</span><span class="sxs-lookup"><span data-stu-id="183eb-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="183eb-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="183eb-152">virtualNetworkName</span></span> |<span data-ttu-id="183eb-153">Dize</span><span class="sxs-lookup"><span data-stu-id="183eb-153">String</span></span> |<span data-ttu-id="183eb-154">Tüketici kullanmak isterse sanal ağ adı.</span><span class="sxs-lookup"><span data-stu-id="183eb-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="183eb-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="183eb-155">enableJumpbox</span></span> |<span data-ttu-id="183eb-156">(Etkin/devre dışı) kısıtlanmış listeden dize</span><span class="sxs-lookup"><span data-stu-id="183eb-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="183eb-157">Jumpbox ortamı için etkinleştirilip etkinleştirilmeyeceğini tanımlayan bir parametre.</span><span class="sxs-lookup"><span data-stu-id="183eb-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="183eb-158">Değerler: "etkin", "disabled"</span><span class="sxs-lookup"><span data-stu-id="183eb-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="183eb-159">**TshirtSize** önceki bölümünde kullanılan parametre olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="183eb-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

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
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="183eb-160">Durum bağlı şablonları geçirin</span><span class="sxs-lookup"><span data-stu-id="183eb-160">Pass state to linked templates</span></span>
<span data-ttu-id="183eb-161">Bağlı şablonları bağlanırken genellikle statik bir karışımını kullanın ve değişkenleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="183eb-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="183eb-162">Statik değişkenler</span><span class="sxs-lookup"><span data-stu-id="183eb-162">Static variables</span></span>
<span data-ttu-id="183eb-163">Statik değişkenler genellikle bir şablon kullanılan URL'leri gibi temel değerlerini sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="183eb-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="183eb-164">Aşağıdaki şablonu alıntı içinde `templateBaseUrl` Github'da şablonu için kök konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="183eb-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="183eb-165">Sonraki satıra yeni bir değişken oluşturur `sharedTemplateUrl` temel URL paylaşılan kaynakları şablonu bilinen adı ile birleştirir.</span><span class="sxs-lookup"><span data-stu-id="183eb-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="183eb-166">Bu satır, bir karmaşık nesne değişkeni burada temel URL bilinen yapılandırma şablonu konumuna birleştirilmiş ve depolanan bir ısı boyutu depolamak için kullanılan `vmTemplate` özelliği.</span><span class="sxs-lookup"><span data-stu-id="183eb-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="183eb-167">Bu yaklaşımın avantajı, şablon konumu değişirse, yalnızca tüm bağlı şablonlarda geçirir tek bir yerde statik değişkeni değiştirmeniz gerektiğini ' dir.</span><span class="sxs-lookup"><span data-stu-id="183eb-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="183eb-168">Oluşturulan değişkenleri</span><span class="sxs-lookup"><span data-stu-id="183eb-168">Generated variables</span></span>
<span data-ttu-id="183eb-169">Statik değişkenler yanı sıra çeşitli değişkenler dinamik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="183eb-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="183eb-170">Bu bölümde bazı oluşturulan değişkenlerin ortak türlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="183eb-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="183eb-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="183eb-171">tshirtSize</span></span>
<span data-ttu-id="183eb-172">Yukarıdaki örneklerde ile oluşturulan bu değişken hakkında bilgi sahibi.</span><span class="sxs-lookup"><span data-stu-id="183eb-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="183eb-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="183eb-173">networkSettings</span></span>
<span data-ttu-id="183eb-174">Bir Kapasite yetenek veya uçtan uca kapsamlı çözüm şablonu, bağlı şablonları bir ağdaki genellikle mevcut kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="183eb-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="183eb-175">Bir kolay yaklaşım ağ ayarlarını depolamak ve bunlara bağlı şablonları geçirmek için karmaşık bir nesne kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="183eb-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="183eb-176">Ağ Ayarları iletişim kurulurken bir örnek aşağıda görülebilir.</span><span class="sxs-lookup"><span data-stu-id="183eb-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="183eb-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="183eb-177">availabilitySettings</span></span>
<span data-ttu-id="183eb-178">Bağlantılı şablonlarında oluşturulan kaynakları, genellikle bir kullanılabilirlik kümesine yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="183eb-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="183eb-179">Aşağıdaki örnekte, kullanılabilirlik kümesi adı belirtildi ve ayrıca kullanmak için hata etki alanı ve güncelleştirme etki alanı sayısı.</span><span class="sxs-lookup"><span data-stu-id="183eb-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="183eb-180">Önek olarak bir ad kullanabilirsiniz birden çok kullanılabilirlik kümesine (örneğin, bir ana düğüm için) ve veri düğümlerini için başka bir gereksinim duyarsanız, birden çok kullanılabilirlik kümesine belirtin veya belirli bir ısı boyutu için bir değişken oluşturmak için daha önce gösterilen modelini izler.</span><span class="sxs-lookup"><span data-stu-id="183eb-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="183eb-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="183eb-181">storageSettings</span></span>
<span data-ttu-id="183eb-182">Depolama ayrıntıları genellikle bağlı şablonları ile paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="183eb-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="183eb-183">Aşağıdaki örnekte bir *storageSettings* nesnesi, depolama hesabı ve kapsayıcı adları hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="183eb-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="183eb-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="183eb-184">osSettings</span></span>
<span data-ttu-id="183eb-185">Bağlantılı şablonları ile işletim sistemi ayarlarını çeşitli düğüm türleri için farklı bilinen yapılandırma türleri arasında geçmesi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="183eb-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="183eb-186">Karmaşık bir nesne depolamak ve işletim sistemi bilgilerini paylaşmak için kolay bir yoludur ve dağıtımı için birden çok işletim sistemi seçenekleri desteklemeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="183eb-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="183eb-187">Aşağıdaki örnek, bir nesne için gösterir *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="183eb-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="183eb-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="183eb-188">machineSettings</span></span>
<span data-ttu-id="183eb-189">Oluşturulan bir değişken *machineSettings* bir VM oluşturmak için çekirdek değişkenleri bir karışımını içeren karmaşık bir nesne.</span><span class="sxs-lookup"><span data-stu-id="183eb-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="183eb-190">Değişkenleri, yönetici kullanıcı adı ve parola, VM adları ve bir işletim sistemi görüntüsü başvurusu için bir önek içerir.</span><span class="sxs-lookup"><span data-stu-id="183eb-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="183eb-191">Unutmayın *osImageReference* değerleri alır *osSettings* ana şablonda tanımlanan değişken.</span><span class="sxs-lookup"><span data-stu-id="183eb-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="183eb-192">Anlamı kolayca değiştirebilirsiniz işletim sistemi için bir VM — tamamen veya bir şablon tüketici tercihine göre.</span><span class="sxs-lookup"><span data-stu-id="183eb-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="183eb-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="183eb-193">vmScripts</span></span>
<span data-ttu-id="183eb-194">*VmScripts* nesne indirmek ve dış ve iç başvuruları dahil olmak üzere bir VM örneğinde yürütmek için komut dosyaları hakkında ayrıntılar içerir.</span><span class="sxs-lookup"><span data-stu-id="183eb-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="183eb-195">Dışında altyapı başvurular içerir.</span><span class="sxs-lookup"><span data-stu-id="183eb-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="183eb-196">İç başvurular yüklü yazılımı yüklüyse ve yapılandırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="183eb-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="183eb-197">Kullandığınız *scriptsToDownload* VM'ye karşıdan yüklemek için komut dosyaları listelemek için özellik.</span><span class="sxs-lookup"><span data-stu-id="183eb-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="183eb-198">Bu nesne, aynı zamanda farklı türde eylemler için komut satırı bağımsız değişkenleri başvurular içeriyor.</span><span class="sxs-lookup"><span data-stu-id="183eb-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="183eb-199">Bu Eylemler, tek tek her düğüm için varsayılan yükleme, tüm düğümler dağıtıldıktan sonra çalıştırılan bir yükleme ve verilen bir şablon için belirli herhangi bir ek betiği yürütülürken içerir.</span><span class="sxs-lookup"><span data-stu-id="183eb-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="183eb-200">Bu, yüksek kullanılabilirlik sağlamak bir arbiter gerektirir MongoDB dağıtmak için kullanılan bir şablondan örneğidir.</span><span class="sxs-lookup"><span data-stu-id="183eb-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="183eb-201">*ArbiterNodeInstallCommand* eklendi *vmScripts* arbiter yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="183eb-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="183eb-202">Uygun değerlerle betik yürütmek için belirli bir metni tanımlamak değişkenleri nerede değişkenleri bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="183eb-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="183eb-203">Bir şablondan dönüş durumu</span><span class="sxs-lookup"><span data-stu-id="183eb-203">Return state from a template</span></span>
<span data-ttu-id="183eb-204">Yalnızca veri geçirebilirsiniz bir şablona geri çağırma şablon verileri de paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="183eb-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="183eb-205">İçinde **çıkarır** bölüm bağlantılı şablonu, kaynak şablonu tarafından kullanılabilecek anahtar/değer çiftleri sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="183eb-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="183eb-206">Aşağıdaki örnek, bağlantılı bir şablonda oluşturulan özel IP adresi geçirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="183eb-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="183eb-207">Ana Şablon içerisinde, aşağıdaki sözdizimi ile bu verileri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="183eb-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="183eb-208">Bu ifadede çıkışları bölüm veya ana şablon kaynakları bölümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="183eb-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="183eb-209">Çalışma zamanı durumunu kullandığından deyim değişkenler bölümünde kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="183eb-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="183eb-210">Bu değer ana şablondan döndürmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="183eb-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="183eb-211">Bir sanal makine veri diski döndürmek için bağlantılı bir şablon çıktıları bölümünü kullanarak bir örnek için bkz: [bir sanal makine için birden fazla veri diski oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="183eb-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="183eb-212">Sanal makine için kimlik doğrulama ayarlarını tanımlayın</span><span class="sxs-lookup"><span data-stu-id="183eb-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="183eb-213">Bir sanal makine için kimlik doğrulama ayarlarını belirtmek için yapılandırma ayarları daha önce gösterilen aynı yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="183eb-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="183eb-214">Parametre geçirme için kimlik doğrulama türünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="183eb-214">You create a parameter for passing in the type of authentication.</span></span>

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

<span data-ttu-id="183eb-215">Farklı kimlik doğrulama türleri için değişkenleri ekleyin ve hangi tür depolamak için bir değişken parametre değeri temel alınarak bu dağıtım için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="183eb-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

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

<span data-ttu-id="183eb-216">Sanal makine tanımlarken, ayarladığınız **osProfile** oluşturduğunuz değişkene.</span><span class="sxs-lookup"><span data-stu-id="183eb-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="183eb-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="183eb-217">Next steps</span></span>
* <span data-ttu-id="183eb-218">Şablon bölümleri hakkında bilgi edinmek için [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="183eb-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="183eb-219">Bir şablonu içinde kullanılabilen işlevlerin görmek için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="183eb-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
