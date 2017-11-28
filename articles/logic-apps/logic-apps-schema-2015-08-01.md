---
title: "aaaSchema güncelleştirmeleri Ağustos 1 2015 preview - Azure Logic Apps | Microsoft Docs"
description: "Şema sürüm 2015-08-01-Önizleme ile Azure Logic Apps için JSON tanımları oluşturma"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="8a7e0-103">Azure mantıksal uygulamaları - 1 Ağustos 2015 preview şema güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8a7e0-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="8a7e0-104">Bu yeni şema ve API sürümü Azure mantıksal uygulamaları için daha fazla mantıksal uygulamalar olun anahtar iyileştirmeler içerir güvenilir ve kolay toouse:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="8a7e0-105">Merhaba **APIApp** eylem türüdür yeni güncelleştirilmiş tooa [ **APIConnection** ](#api-connections) eylem türü.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="8a7e0-106">**Yineleme** çok adlandırılır[**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="8a7e0-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="8a7e0-107">Merhaba [ **HTTP dinleyicisi** API uygulaması](#http-listener) artık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="8a7e0-108">Alt iş akışlarını çağırma kullanan bir [yeni şema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="8a7e0-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="8a7e0-109">Taşıma tooAPI bağlantıları</span><span class="sxs-lookup"><span data-stu-id="8a7e0-109">Move tooAPI connections</span></span>

<span data-ttu-id="8a7e0-110">Merhaba büyük değişiklik API'lerini kullanabilmek için toodeploy API uygulamaları Azure aboneliğinizde artık sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="8a7e0-111">API'ler kullanabilirsiniz hello yollar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="8a7e0-112">Yönetilen API'ler</span><span class="sxs-lookup"><span data-stu-id="8a7e0-112">Managed APIs</span></span>
* <span data-ttu-id="8a7e0-113">Özel Web API'leri</span><span class="sxs-lookup"><span data-stu-id="8a7e0-113">Your custom Web APIs</span></span>

<span data-ttu-id="8a7e0-114">Kendi yönetim ve barındırma modellerini farklı olduğundan her şekilde biraz farklı şekilde ele alınır.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="8a7e0-115">Bu modelin avantajlarından biri artık sınırlı Azure kaynak grubunda dağıtılan tooresources.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="8a7e0-116">Yönetilen API'ler</span><span class="sxs-lookup"><span data-stu-id="8a7e0-116">Managed APIs</span></span>

<span data-ttu-id="8a7e0-117">Microsoft Office 365, Salesforce, Twitter ve FTP gibi sizin adınıza bazı API'leri yönetir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="8a7e0-118">Bazı yönetilen API'ler kullanabilirsiniz-diğer yapılandırma gerektirirken, Bing Çevir gibi ise.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="8a7e0-119">Bu yapılandırma adlı bir *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="8a7e0-120">Örneğin, Office 365 kullandığınızda, Office 365 oturum açma belirtecinizi içeren bir bağlantı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="8a7e0-121">Bu belirteç güvenli bir şekilde depolanır ve böylece mantıksal uygulamanızı her zaman hello Office 365 API çağrısı yenilenir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="8a7e0-122">Alternatif olarak, tooconnect tooyour SQL veya FTP sunucusunu istiyorsanız hello bağlantı dizesi olan bir bağlantı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="8a7e0-123">Bu tanımı'nda, bu eylemleri denir `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="8a7e0-124">Office 365 toosend bir e-posta çağıran bir bağlantı bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

<span data-ttu-id="8a7e0-125">Merhaba `host` nesnesidir benzersiz tooAPI bağlantıları ve satırındaki bölümleri içeren girişleri kısmı: `api` ve `connection`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="8a7e0-126">Merhaba `api` hello çalışma zamanı, API yönetildiği URL'sini barındırılır sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="8a7e0-127">Kullanılabilir tüm hello yönetilen API'ler çağırarak görebilirsiniz `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="8a7e0-128">Bir API kullandığınızda, hello API sahip olabilir veya herhangi bir değil *bağlantı parametrelerini* tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="8a7e0-129">Merhaba API seçili değilse, hiçbir *bağlantı* gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="8a7e0-130">Merhaba API varsa, bir bağlantı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="8a7e0-131">oluşturulan hello bağlantı seçtiğiniz hello adına sahip.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="8a7e0-132">Ardından hello hello adına başvuru `connection` nesne hello içinde `host` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="8a7e0-133">toocreate çağrısı bir kaynak grubunda bağlantı:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="8a7e0-134">Gövde aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-134">With hello following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="8a7e0-135">Yönetilen API'leri bir Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="8a7e0-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="8a7e0-136">Etkileşimli oturum açma gerekli olmadığı sürece, tüm bir uygulamayı bir Azure Resource Manager şablonu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="8a7e0-137">Oturum açma gerekiyorsa, her şeyi hello Azure Resource Manager şablonu ile ayarlayabilirsiniz ancak toovisit hello portal tooauthorize hello bağlantıları çözümlenmedi.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

<span data-ttu-id="8a7e0-138">Bu örnekte hello bağlantıların kaynak grubunuzdaki Canlı yalnızca kaynakları olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="8a7e0-139">Yönetilen hello API'leri kullanılabilir tooyou aboneliğinizde başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="8a7e0-140">Özel Web API'leri</span><span class="sxs-lookup"><span data-stu-id="8a7e0-140">Your custom Web APIs</span></span>

<span data-ttu-id="8a7e0-141">Merhaba yerleşik değil Microsoft tarafından yönetilen olanları kendi API kullanırsanız kullanın **HTTP** eylem toocall bunları.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="8a7e0-142">İdeal bir deneyim için API için Swagger uç nokta maruz bırakmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="8a7e0-143">Bu uç noktaya hello mantığı Uygulama Tasarımcısı toorender hello girişleri etkinleştirir ve API için çıkarır.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="8a7e0-144">Swagger hello Tasarımcısı sadece hello girişleri ve çıkışları donuk JSON nesneler olarak gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="8a7e0-145">Yeni bir örnek gösteren hello işte `metadata.apiDefinitionUrl` özelliği:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

<span data-ttu-id="8a7e0-146">Azure App Service'te Web API'nizi barındırıyorsanız, Web API otomatik olarak hello Tasarımcısı'nda kullanılabilir eylemleri hello listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="8a7e0-147">Değilse, toopaste hello URL'de doğrudan sahip.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="8a7e0-148">Merhaba API kendisini Swagger destekler ne olursa olsun yöntemleriyle güvenli rağmen hello Swagger uç nokta kimliği doğrulanmamış toobe hello mantığı Uygulama Tasarımcısı kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="8a7e0-149">Dağıtılan API apps 2015-08-01-Önizleme ile çağırın</span><span class="sxs-lookup"><span data-stu-id="8a7e0-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="8a7e0-150">Bir API uygulamasını daha önce dağıttıysanız hello hello uygulamayla çağırabilirsiniz **HTTP** eylem.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="8a7e0-151">Örneğin, Dropbox toolist dosyaları kullanırsanız, **2014-12-01-Önizleme** şema sürümü tanımı şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="8a7e0-152">Merhaba parametreleri hello mantıksal uygulama tanımını bölümünü değişmeden kalır ancak bu örnek gibi hello eşdeğer HTTP eylemi oluşturabileceğiniz:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="8a7e0-153">Bu özellikleri tek tek taramasını:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="8a7e0-154">Action özelliği</span><span class="sxs-lookup"><span data-stu-id="8a7e0-154">Action property</span></span> | <span data-ttu-id="8a7e0-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8a7e0-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="8a7e0-156">`Http`Onun yerine`APIapp`</span><span class="sxs-lookup"><span data-stu-id="8a7e0-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="8a7e0-157">toouse, bu eylemin hello mantığı Uygulama Tasarımcısı'ndan oluşturulan hello meta veri uç şunları içerir:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="8a7e0-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="8a7e0-158">Gelen oluşturulur:`{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="8a7e0-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="8a7e0-159">Her zaman`POST`</span><span class="sxs-lookup"><span data-stu-id="8a7e0-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="8a7e0-160">Aynı toohello API uygulaması parametreleri</span><span class="sxs-lookup"><span data-stu-id="8a7e0-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="8a7e0-161">Aynı toohello API uygulama kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8a7e0-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="8a7e0-162">Bu yaklaşım, tüm API uygulaması eylemler için çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="8a7e0-163">Ancak, bu önceki API uygulamaları artık desteklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="8a7e0-164">Bu nedenle hello tooone iki diğer önceki seçenekleri, yönetilen bir API veya özel Web API'nizi barındıran taşımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="8a7e0-165">'Repeat' too'foreach yeniden adlandırılmış '</span><span class="sxs-lookup"><span data-stu-id="8a7e0-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="8a7e0-166">Merhaba önceki şema sürümü için çok müşteri geri bildirimi aldık, **yineleyin** kafa karıştırıcı ve düzgün şekilde yakalama alamadık **yineleyin** gerçekten için-her bir döngü oluştu.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="8a7e0-167">Sonuç olarak, biz adlandırdınız `repeat` çok`foreach`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="8a7e0-168">Örneğin, daha önce aşağıdakileri yazarsınız:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-168">For example, previously you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

<span data-ttu-id="8a7e0-169">Şimdi, yazarsınız:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-169">Now you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

<span data-ttu-id="8a7e0-170">Merhaba işlevi `@repeatItem()` olan daha önce kullanılan tooreference hello geçerli öğe olan yinelendiğinde üzerinden.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="8a7e0-171">Bu işlev artık çok basitleştirilmiştir`@item()`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="8a7e0-172">'Foreach' başvuru çıkışlarından</span><span class="sxs-lookup"><span data-stu-id="8a7e0-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="8a7e0-173">Gelen hello basitleştirme için çıkarır `foreach` Eylemler adlı bir nesne değil sarılır `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="8a7e0-174">Merhaba hello önceki çıkarır sırada `repeat` örnek olan:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-174">While hello outputs from hello previous `repeat` example were:</span></span>

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

<span data-ttu-id="8a7e0-175">Bu çıktı sunulmuştur:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-175">Now these outputs are:</span></span>

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

<span data-ttu-id="8a7e0-176">Daha önce tooget toohello gövdesi bu çıktılar başvururken hello eylem:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="8a7e0-177">Bunun yerine şimdi yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-177">Now you can do instead:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="8a7e0-178">Bu değişiklikler ile Merhaba işlevleri `@repeatItem()`, `@repeatBody()`, ve `@repeatOutputs()` kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="8a7e0-179">Yerel HTTP dinleyicisi</span><span class="sxs-lookup"><span data-stu-id="8a7e0-179">Native HTTP listener</span></span>

<span data-ttu-id="8a7e0-180">Merhaba HTTP dinleyicisi özellikleri artık yerleşiktir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="8a7e0-181">Bu nedenle, artık toodeploy bir HTTP dinleyicisi API uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="8a7e0-182">Bkz: [hello ayrıntıların nasıl toomake, mantığı uygulama uç noktası aranabilir burada](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="8a7e0-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="8a7e0-183">Bu değişikliklerle biz hello kaldırılan `@accessKeys()` biz hello ile değiştirilen işlevi `@listCallbackURL()` hello endpoint gerektiğinde alma işlevi.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="8a7e0-184">Ayrıca, mantıksal uygulamanızı şimdi en az bir tetikleyici tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="8a7e0-185">Çok istiyorsanız`/run` iş akışı Merhaba, bu Tetikleyiciler birine sahip olmalıdır: `manual`, `apiConnectionWebhook`, veya `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="8a7e0-186">Alt iş akışlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="8a7e0-186">Call child workflows</span></span>

<span data-ttu-id="8a7e0-187">Daha önce alt iş akışlarını çağırma toohello iş akışı, hello erişim belirteci ve yapıştırma hello belirteci toocall istediğiniz hello mantığı uygulama tanımında alt iş akışının alma giderek gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="8a7e0-188">Merhaba tanımı tüm gizli olmayan sahip çok yapıştırdığınız şekilde hello yeni şema ile Merhaba Logic Apps altyapısı SAS için çalışma zamanında otomatik olarak oluşturur alt iş akışı hello.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="8a7e0-189">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8a7e0-189">Here is an example:</span></span>

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

<span data-ttu-id="8a7e0-190">İkinci bir geliştirme hello alt iş akışları tam erişim toohello gelen istek verirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="8a7e0-191">Hello parametreleri geçirebilirsiniz anlamına *sorguları* bölüm ve hello *üstbilgileri* nesne ve tam olarak tanımlayabileceğiniz hello tüm gövdesi.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="8a7e0-192">Son olarak, gerekli değişiklikleri toohello alt iş akışı vardır.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="8a7e0-193">Şimdi daha önce bir alt iş akışı doğrudan çağırabilirsiniz olsa da, hello iş akışında hello üst toocall için bir tetikleyici uç noktasını tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="8a7e0-194">Genellikle, sahip bir tetikleyici eklemek `manual` yazın ve ardından tetikleyicisi hello üst tanımında kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="8a7e0-195">Not hello `host` özelliği özellikle sahip bir `triggerName` tetikleyicinin her zaman belirtmeniz gerekir çünkü çağırma.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="8a7e0-196">Diğer değişiklikler</span><span class="sxs-lookup"><span data-stu-id="8a7e0-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="8a7e0-197">Yeni 'sorguları' özelliği</span><span class="sxs-lookup"><span data-stu-id="8a7e0-197">New 'queries' property</span></span>

<span data-ttu-id="8a7e0-198">Tüm eylem türleri şimdi adlı yeni bir giriş Destek `queries`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="8a7e0-199">Bu giriş, yapılandırılmış nesne yerine, el ile tooassemble hello dize sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="8a7e0-200">'Parse()' işlevi too'json() yeniden adlandırılmış '</span><span class="sxs-lookup"><span data-stu-id="8a7e0-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="8a7e0-201">Biz hello yeniden adlandırılmış şekilde daha fazla içerik türleri yakında ekliyoruz `parse()` çok işlev`json()`.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="8a7e0-202">Yakında: Kurumsal tümleştirme API'leri</span><span class="sxs-lookup"><span data-stu-id="8a7e0-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="8a7e0-203">Biz yönetilen sürümleri henüz hello AS2 gibi Kurumsal tümleştirme API'leri yok.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="8a7e0-204">Bu arada, var olan dağıtılmış BizTalk API'leri aracılığıyla hello HTTP eylemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a7e0-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="8a7e0-205">Ayrıntılar için bkz: "zaten dağıtılmış API uygulamalarınızı hello kullanarak" [tümleştirme Haritası](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="8a7e0-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
