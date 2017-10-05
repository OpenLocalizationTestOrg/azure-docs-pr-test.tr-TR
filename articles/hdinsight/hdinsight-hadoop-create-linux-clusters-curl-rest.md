---
title: "Azure REST API - Azure kullanarak Hadoop kümeleri oluşturma | Microsoft Docs"
description: "Azure Resource Manager şablonları Azure REST API göndererek Hdınsight kümeleri oluşturmayı öğrenin."
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
ms.openlocfilehash: a36a41c231472ceeeb46d02ddb65549b1c79728a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="48fe1-103">Azure REST API'sini kullanarak Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="48fe1-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="48fe1-104">Bir Azure Resource Manager şablonu ve Azure REST API'sini kullanarak bir Hdınsight kümesi oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="48fe1-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="48fe1-105">Azure REST API'sini Hdınsight kümeleri gibi yeni kaynaklar oluşturma dahil olmak üzere Azure platformu barındırılan Hizmetleri yönetim işlemlerini gerçekleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="48fe1-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48fe1-106">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="48fe1-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="48fe1-107">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="48fe1-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="48fe1-108">Bu adımlarda belge kullanımı [curl (https://curl.haxx.se/)](https://curl.haxx.se/) Azure REST API'si ile iletişim kurmak için yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="48fe1-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="48fe1-109">Şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="48fe1-109">Create a template</span></span>

<span data-ttu-id="48fe1-110">Azure Resource Manager şablonları tanımlayan JSON belgeleri olan bir **kaynak grubu** ve ortamdaki tüm kaynaklar (örneğin, Hdınsight.) Bu şablona dayalı yaklaşım, tek bir şablonda Hdınsight için gereken kaynaklar tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="48fe1-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="48fe1-111">Bir birleşme şablonu ve parametre dosyalarının aşağıdaki JSON belgedir [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), Linux tabanlı bir küme oluşturur SSH kullanıcı hesabını güvenli hale getirmek için bir parola kullanma.</span><span class="sxs-lookup"><span data-stu-id="48fe1-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

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
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
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
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
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

<span data-ttu-id="48fe1-112">Bu örnekte, bu belgede yer alan adımlar, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="48fe1-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="48fe1-113">Örneği değiştirecek *değerleri* içinde **parametreleri** kümeniz için değerlerle bölümü.</span><span class="sxs-lookup"><span data-stu-id="48fe1-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48fe1-114">Şablonu çalışan düğümleri (4) varsayılan sayısı bir Hdınsight kümesi için kullanır.</span><span class="sxs-lookup"><span data-stu-id="48fe1-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="48fe1-115">32'den fazla çalışan düğümlerine planlıyorsanız, bir baş düğüm boyutu en az 8 çekirdek ve 14 GB ram ile seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="48fe1-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="48fe1-116">Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="48fe1-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="48fe1-117">Azure aboneliğinizde oturum açın</span><span class="sxs-lookup"><span data-stu-id="48fe1-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="48fe1-118">Konusunda belgelenen adımları izleyin [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) ve kullanarak aboneliğinze bağlanın `az login` komutu.</span><span class="sxs-lookup"><span data-stu-id="48fe1-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="48fe1-119">Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="48fe1-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="48fe1-120">Bu adımları özetlenmiş bir sürümü olan *parolayla hizmet sorumlusu oluşturma* bölümünü [kaynaklara erişmek için bir hizmet sorumlusu oluşturmak için kullanım Azure CLI](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) belge.</span><span class="sxs-lookup"><span data-stu-id="48fe1-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="48fe1-121">Bu adımlar Azure REST API'sine kimliğini doğrulamak için kullanılan bir hizmet sorumlusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48fe1-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="48fe1-122">Bir komut satırından, Azure aboneliklerinize listelemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="48fe1-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="48fe1-123">Listede, kullanıp not etmek istediğiniz aboneliği seçin **ABONELİK_KİMLİĞİ** ve __Tenant_ID__ sütun.</span><span class="sxs-lookup"><span data-stu-id="48fe1-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="48fe1-124">Bu değerleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="48fe1-124">Save these values.</span></span>

2. <span data-ttu-id="48fe1-125">Azure Active Directory'de bir uygulama oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="48fe1-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="48fe1-126">İçin değerleri `--display-name`, `--homepage`, ve `--identifier-uris` kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="48fe1-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="48fe1-127">Yeni Active Directory giriş için bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="48fe1-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="48fe1-128">`--home-page` Ve `--identifier-uris` değerleri internet'te barındırılan gerçek bir web sayfasına başvuru gerekmez.</span><span class="sxs-lookup"><span data-stu-id="48fe1-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="48fe1-129">Benzersiz bir URI olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="48fe1-129">They must be unique URIs.</span></span>

   <span data-ttu-id="48fe1-130">Bu komuttan döndürülen değer __uygulama kimliği__ yeni uygulama için.</span><span class="sxs-lookup"><span data-stu-id="48fe1-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="48fe1-131">Bu değer kaydedin.</span><span class="sxs-lookup"><span data-stu-id="48fe1-131">Save this value.</span></span>

3. <span data-ttu-id="48fe1-132">Kullanarak bir hizmet sorumlusu oluşturmak için aşağıdaki komutu kullanın **uygulama kimliği**.</span><span class="sxs-lookup"><span data-stu-id="48fe1-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="48fe1-133">Bu komuttan döndürülen değer __nesne kimliği__.</span><span class="sxs-lookup"><span data-stu-id="48fe1-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="48fe1-134">Bu değer kaydedin.</span><span class="sxs-lookup"><span data-stu-id="48fe1-134">Save this value.</span></span>

4. <span data-ttu-id="48fe1-135">Ata **sahibi** hizmet asıl kullanarak rolü **nesne kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="48fe1-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="48fe1-136">Kullanım **abonelik kimliği** daha önce aldığınız.</span><span class="sxs-lookup"><span data-stu-id="48fe1-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="48fe1-137">Kimlik Doğrulama belirtecini alma</span><span class="sxs-lookup"><span data-stu-id="48fe1-137">Get an authentication token</span></span>

<span data-ttu-id="48fe1-138">Kimlik Doğrulama belirtecini almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="48fe1-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="48fe1-139">Ayarlama `$TENANTID`, `$APPID`, ve `$PASSWORD` elde ya da daha önce kullanılan değerler.</span><span class="sxs-lookup"><span data-stu-id="48fe1-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="48fe1-140">Bu istek başarılı olursa, 200 serisi yanıtı alır ve bir JSON belgesi yanıt gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="48fe1-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="48fe1-141">Bu istek tarafından döndürülen JSON belgesi adlı bir öğe içeriyorsa **access_token**.</span><span class="sxs-lookup"><span data-stu-id="48fe1-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="48fe1-142">Değeri **access_token** REST API için kimlik doğrulama istekleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="48fe1-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="48fe1-143">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="48fe1-143">Create a resource group</span></span>

<span data-ttu-id="48fe1-144">Bir kaynak grubu oluşturmak için aşağıdakileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="48fe1-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="48fe1-145">Ayarlama `$SUBSCRIPTIONID` abonelik kimliği alınan hizmet asıl oluşturulurken.</span><span class="sxs-lookup"><span data-stu-id="48fe1-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="48fe1-146">Ayarlama `$ACCESSTOKEN` önceki adımda aldığınız erişim belirtecini için.</span><span class="sxs-lookup"><span data-stu-id="48fe1-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="48fe1-147">Değiştir `DATACENTERLOCATION` kaynak grubu ve kaynakları, oluşturmak istediğiniz veri merkezi ile.</span><span class="sxs-lookup"><span data-stu-id="48fe1-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="48fe1-148">Örneğin, 'Orta Güney ABD'.</span><span class="sxs-lookup"><span data-stu-id="48fe1-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="48fe1-149">Ayarlama `$RESOURCEGROUPNAME` bu grup için kullanmak istediğiniz adı:</span><span class="sxs-lookup"><span data-stu-id="48fe1-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="48fe1-150">Bu istek başarılı olursa, 200 serisi yanıtını alma ve grubu ile ilgili bilgileri içeren bir JSON belgesi yanıt gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="48fe1-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="48fe1-151">`"provisioningState"` Ögesinin değerini `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="48fe1-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="48fe1-152">Bir dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="48fe1-152">Create a deployment</span></span>

<span data-ttu-id="48fe1-153">Şablonu kaynak grubuna dağıtmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="48fe1-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="48fe1-154">Ayarlama `$DEPLOYMENTNAME` bu dağıtım için kullanmak istediğiniz adı.</span><span class="sxs-lookup"><span data-stu-id="48fe1-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="48fe1-155">Bir dosyaya şablon kaydettiyseniz yerine aşağıdaki komutu kullanabilirsiniz `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="48fe1-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="48fe1-156">Bu istek başarılı olursa, 200 serisi yanıtını alma ve dağıtım işlemiyle ilgili bilgi içeren bir JSON belgesi yanıt gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="48fe1-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48fe1-157">Dağıtım gönderildi ancak tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="48fe1-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="48fe1-158">Tamamlamak için dağıtım için genellikle yaklaşık 15, birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="48fe1-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="48fe1-159">Bir dağıtım durumunu denetleyin</span><span class="sxs-lookup"><span data-stu-id="48fe1-159">Check the status of a deployment</span></span>

<span data-ttu-id="48fe1-160">Dağıtım durumunu denetlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="48fe1-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="48fe1-161">Bu komut, dağıtım işlemi hakkında bilgi içeren bir JSON belgesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="48fe1-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="48fe1-162">`"provisioningState"` Öğesi dağıtım durumunu içerir.</span><span class="sxs-lookup"><span data-stu-id="48fe1-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="48fe1-163">Bu öğe bir değeri varsa `"Succeeded"`, dağıtım başarıyla tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="48fe1-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="48fe1-164">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="48fe1-164">Troubleshoot</span></span>

<span data-ttu-id="48fe1-165">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="48fe1-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48fe1-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48fe1-166">Next steps</span></span>

<span data-ttu-id="48fe1-167">Hdınsight kümesi başarıyla oluşturuldu, kümenizi ile çalışmayı öğrenmek için aşağıdakileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="48fe1-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="48fe1-168">Hadoop kümeleri</span><span class="sxs-lookup"><span data-stu-id="48fe1-168">Hadoop clusters</span></span>

* [<span data-ttu-id="48fe1-169">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="48fe1-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="48fe1-170">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="48fe1-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="48fe1-171">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="48fe1-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="48fe1-172">HBase kümeleri</span><span class="sxs-lookup"><span data-stu-id="48fe1-172">HBase clusters</span></span>

* [<span data-ttu-id="48fe1-173">Hdınsight'ta HBase kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="48fe1-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="48fe1-174">Hdınsight'ta HBase için Java uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="48fe1-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="48fe1-175">Storm kümeleri</span><span class="sxs-lookup"><span data-stu-id="48fe1-175">Storm clusters</span></span>

* [<span data-ttu-id="48fe1-176">Hdınsight üzerinde Storm için Java topolojisi geliştirme</span><span class="sxs-lookup"><span data-stu-id="48fe1-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="48fe1-177">Hdınsight üzerinde Storm Python bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="48fe1-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="48fe1-178">Dağıtma ve hdınsight'ta Storm topolojileri izleme</span><span class="sxs-lookup"><span data-stu-id="48fe1-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
