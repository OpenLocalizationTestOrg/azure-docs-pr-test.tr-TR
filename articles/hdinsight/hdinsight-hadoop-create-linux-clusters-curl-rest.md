---
title: "aaaCreate Hadoop kümeleri Azure REST API - Azure kullanarak | Microsoft Docs"
description: "Azure Resource Manager şablonları toohello Azure REST API göndererek nasıl toocreate Hdınsight kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="80c5e-103">Hello Azure REST API'sini kullanarak Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="80c5e-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="80c5e-104">Nasıl toocreate bir Hdınsight küme bir Azure Resource Manager şablonu kullanarak ve Azure REST API hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="80c5e-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="80c5e-105">Hello Azure REST API tooperform yönetim işlemlerini hello hello oluşturulmasını Hdınsight kümeleri gibi yeni kaynaklar dahil olmak üzere Azure platformu barındırılan hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="80c5e-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80c5e-106">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="80c5e-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="80c5e-107">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="80c5e-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="80c5e-108">Merhaba adımları bu belgenin kullanımı hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) yardımcı programı toocommunicate hello Azure REST API'si ile.</span><span class="sxs-lookup"><span data-stu-id="80c5e-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="80c5e-109">Şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="80c5e-109">Create a template</span></span>

<span data-ttu-id="80c5e-110">Azure Resource Manager şablonları tanımlayan JSON belgeleri olan bir **kaynak grubu** ve ortamdaki tüm kaynaklar (örneğin, Hdınsight.) Bu şablona dayalı yaklaşım, tek bir şablonda Hdınsight için gereken toodefine hello kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="80c5e-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="80c5e-111">Merhaba aşağıdaki JSON hello birleşmesi şablonu ve parametre dosyalarını belgedir [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), Linux tabanlı oluşturur bir parola toosecure hello SSH kullanıcı hesabı kullanarak küme.</span><span class="sxs-lookup"><span data-stu-id="80c5e-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
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
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
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
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

<span data-ttu-id="80c5e-112">Bu örnek, bu belgedeki hello adımlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="80c5e-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="80c5e-113">Merhaba örneği değiştirecek *değerleri* hello içinde **parametreleri** kümeniz için hello değerlerle bölümü.</span><span class="sxs-lookup"><span data-stu-id="80c5e-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80c5e-114">Merhaba şablon hello varsayılan çalışan düğümleri (4) sayısı bir Hdınsight kümesi için kullanır.</span><span class="sxs-lookup"><span data-stu-id="80c5e-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="80c5e-115">32'den fazla çalışan düğümlerine planlıyorsanız, bir baş düğüm boyutu en az 8 çekirdek ve 14 GB ram ile seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="80c5e-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="80c5e-116">Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="80c5e-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="80c5e-117">Azure aboneliği tooyour oturum</span><span class="sxs-lookup"><span data-stu-id="80c5e-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="80c5e-118">İçinde belirtilen başlangıç adımları [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) ve tooyour abonelik hello kullanarak bağlanmak `az login` komutu.</span><span class="sxs-lookup"><span data-stu-id="80c5e-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="80c5e-119">Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="80c5e-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="80c5e-120">Bu adımları hello özetlenmiş bir sürümü olan *parolayla hizmet sorumlusu oluşturma* hello bölümünü [kullanım Azure CLI toocreate bir hizmet sorumlusu tooaccess kaynakları](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) belge.</span><span class="sxs-lookup"><span data-stu-id="80c5e-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="80c5e-121">Bu adımları kullanılan tooauthenticate toohello Azure REST API'si olan bir hizmet sorumlusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="80c5e-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="80c5e-122">Bir komut satırından komut toolist aşağıdaki hello Azure aboneliklerinize kullanın.</span><span class="sxs-lookup"><span data-stu-id="80c5e-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="80c5e-123">Merhaba listesinde toouse istediğiniz ve Not hello hello aboneliği seçin **ABONELİK_KİMLİĞİ** ve __Tenant_ID__ sütun.</span><span class="sxs-lookup"><span data-stu-id="80c5e-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="80c5e-124">Bu değerleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="80c5e-124">Save these values.</span></span>

2. <span data-ttu-id="80c5e-125">Komut toocreate bir uygulama Azure Active Directory'de aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="80c5e-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="80c5e-126">Hello için Hello değerleri `--display-name`, `--homepage`, ve `--identifier-uris` kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="80c5e-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="80c5e-127">Merhaba yeni Active Directory giriş için bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="80c5e-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="80c5e-128">Merhaba `--home-page` ve `--identifier-uris` değerleri tooreference hello üzerinde barındırılan gerçek bir web sayfasına gerekmez Internet.</span><span class="sxs-lookup"><span data-stu-id="80c5e-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="80c5e-129">Benzersiz bir URI olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80c5e-129">They must be unique URIs.</span></span>

   <span data-ttu-id="80c5e-130">Merhaba Bu komuttan döndürülen değer: Merhaba __uygulama kimliği__ hello yeni uygulama için.</span><span class="sxs-lookup"><span data-stu-id="80c5e-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="80c5e-131">Bu değer kaydedin.</span><span class="sxs-lookup"><span data-stu-id="80c5e-131">Save this value.</span></span>

3. <span data-ttu-id="80c5e-132">Kullanım hello şu komutu toocreate hello kullanarak bir hizmet sorumlusu **uygulama kimliği**.</span><span class="sxs-lookup"><span data-stu-id="80c5e-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="80c5e-133">Merhaba Bu komuttan döndürülen değer: Merhaba __nesne kimliği__.</span><span class="sxs-lookup"><span data-stu-id="80c5e-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="80c5e-134">Bu değer kaydedin.</span><span class="sxs-lookup"><span data-stu-id="80c5e-134">Save this value.</span></span>

4. <span data-ttu-id="80c5e-135">Merhaba atamak **sahibi** hello kullanarak rolü toohello hizmet sorumlusu **nesne kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="80c5e-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="80c5e-136">Kullanım hello **abonelik kimliği** daha önce aldığınız.</span><span class="sxs-lookup"><span data-stu-id="80c5e-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="80c5e-137">Kimlik Doğrulama belirtecini alma</span><span class="sxs-lookup"><span data-stu-id="80c5e-137">Get an authentication token</span></span>

<span data-ttu-id="80c5e-138">Komut tooretrieve kimlik doğrulama belirtecini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="80c5e-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="80c5e-139">Ayarlama `$TENANTID`, `$APPID`, ve `$PASSWORD` toohello değerleri elde veya önceden kullanılmış.</span><span class="sxs-lookup"><span data-stu-id="80c5e-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="80c5e-140">Bu istek başarılı olursa, 200 serisi yanıtı alır ve bir JSON belgesi hello yanıt gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="80c5e-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="80c5e-141">Merhaba bu istek tarafından döndürülen JSON belgesi adlı bir öğe içeriyorsa **access_token**.</span><span class="sxs-lookup"><span data-stu-id="80c5e-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="80c5e-142">Merhaba değerini **access_token** kullanılan tooauthentication istekleri toohello REST API değil.</span><span class="sxs-lookup"><span data-stu-id="80c5e-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="80c5e-143">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="80c5e-143">Create a resource group</span></span>

<span data-ttu-id="80c5e-144">Bir kaynak grubu toocreate aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="80c5e-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="80c5e-145">Ayarlama `$SUBSCRIPTIONID` toohello abonelik kimliği alınan hizmet asıl hello oluşturulurken.</span><span class="sxs-lookup"><span data-stu-id="80c5e-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="80c5e-146">Ayarlama `$ACCESSTOKEN` hello önceki adımda aldığınız toohello erişim belirteci.</span><span class="sxs-lookup"><span data-stu-id="80c5e-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="80c5e-147">Değiştir `DATACENTERLOCATION` ile Merhaba veri merkezi toocreate hello kaynak grubu ve kaynaklar içinde istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="80c5e-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="80c5e-148">Örneğin, 'Orta Güney ABD'.</span><span class="sxs-lookup"><span data-stu-id="80c5e-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="80c5e-149">Ayarlama `$RESOURCEGROUPNAME` toouse bu grup için istediğiniz toohello adı:</span><span class="sxs-lookup"><span data-stu-id="80c5e-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="80c5e-150">Bu istek başarılı olursa, 200 serisi yanıtını alma ve hello grubu hakkında bilgi içeren bir JSON belgesi hello yanıt gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="80c5e-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="80c5e-151">Merhaba `"provisioningState"` ögesinin değerini `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="80c5e-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="80c5e-152">Bir dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80c5e-152">Create a deployment</span></span>

<span data-ttu-id="80c5e-153">Komut toodeploy hello şablon toohello kaynak grubu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="80c5e-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="80c5e-154">Ayarlama `$DEPLOYMENTNAME` toouse bu dağıtım için istediğiniz toohello adı.</span><span class="sxs-lookup"><span data-stu-id="80c5e-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="80c5e-155">Hello şablon tooa dosyası kaydettiyseniz komut yerine aşağıdaki hello kullanabilirsiniz `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="80c5e-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="80c5e-156">Bu istek başarılı olursa, 200 serisi yanıtını alma ve hello dağıtım işlemiyle ilgili bilgi içeren bir JSON belgesi hello yanıt gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="80c5e-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80c5e-157">Merhaba dağıtım gönderildi ancak tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="80c5e-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="80c5e-158">Birkaç dakika, genellikle yaklaşık 15 ' hello dağıtım toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="80c5e-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="80c5e-159">Bir dağıtım Hello durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="80c5e-159">Check hello status of a deployment</span></span>

<span data-ttu-id="80c5e-160">Merhaba dağıtımının komutu aşağıdaki kullanım hello toocheck hello durumu:</span><span class="sxs-lookup"><span data-stu-id="80c5e-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="80c5e-161">Bu komut hello dağıtım işlemiyle ilgili bilgi içeren bir JSON belgesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="80c5e-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="80c5e-162">Merhaba `"provisioningState"` öğesi hello hello dağıtımının durumunu içerir.</span><span class="sxs-lookup"><span data-stu-id="80c5e-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="80c5e-163">Bu öğe bir değeri varsa `"Succeeded"`, hello dağıtım başarıyla tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="80c5e-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="80c5e-164">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="80c5e-164">Troubleshoot</span></span>

<span data-ttu-id="80c5e-165">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="80c5e-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80c5e-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80c5e-166">Next steps</span></span>

<span data-ttu-id="80c5e-167">Hdınsight kümesi başarıyla oluşturuldu, toolearn nasıl aşağıdaki hello kullan toowork kümenizi ile.</span><span class="sxs-lookup"><span data-stu-id="80c5e-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="80c5e-168">Hadoop kümeleri</span><span class="sxs-lookup"><span data-stu-id="80c5e-168">Hadoop clusters</span></span>

* [<span data-ttu-id="80c5e-169">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="80c5e-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="80c5e-170">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="80c5e-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="80c5e-171">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="80c5e-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="80c5e-172">HBase kümeleri</span><span class="sxs-lookup"><span data-stu-id="80c5e-172">HBase clusters</span></span>

* [<span data-ttu-id="80c5e-173">Hdınsight'ta HBase kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="80c5e-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="80c5e-174">Hdınsight'ta HBase için Java uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="80c5e-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="80c5e-175">Storm kümeleri</span><span class="sxs-lookup"><span data-stu-id="80c5e-175">Storm clusters</span></span>

* [<span data-ttu-id="80c5e-176">Hdınsight üzerinde Storm için Java topolojisi geliştirme</span><span class="sxs-lookup"><span data-stu-id="80c5e-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="80c5e-177">Hdınsight üzerinde Storm Python bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="80c5e-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="80c5e-178">Dağıtma ve hdınsight'ta Storm topolojileri izleme</span><span class="sxs-lookup"><span data-stu-id="80c5e-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
