---
title: "Azure Kubernetes kümesi için hizmet sorumlusu | Microsoft Belgeleri"
description: "Azure Container Service içindeki bir Kubernetes kümesi için Azure Active Directory hizmet sorumlusu oluşturma ve yönetme"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 37171b4e69ad7d8c41ca8e7475c33ce70379f484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="37f5d-103">Container Service’te bir Kubernetes kümesi için Azure AD hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="37f5d-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="37f5d-104">Azure Container Service'te Kubernetes kümesi, Azure API'leri ile etkileşime geçmek için [Azure Active Directory hizmet sorumlusu](../../active-directory/develop/active-directory-application-objects.md) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) to interact with Azure APIs.</span></span> <span data-ttu-id="37f5d-105">Hizmet sorumlusu, [kullanıcı tanımlı yollar](../../virtual-network/virtual-networks-udr-overview.md) ve [4. Katman Azure Load Balancer](../../load-balancer/load-balancer-overview.md) gibi kaynakları dinamik olarak yönetmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="37f5d-106">Bu makalede Kubernetes kümeniz için hizmet sorumlusu ayarlamak üzere kullanabileceğiniz farklı seçenekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="37f5d-107">Örneğin, [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklemesini ve kurulumunu yaptıysanız, [`az acs create`](/cli/azure/acs#create) komutunu çalıştırarak Kubernetes kümesini ve hizmet sorumlusunu aynı anda oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f5d-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>


## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="37f5d-108">Hizmet sorumlusu için gereksinimler</span><span class="sxs-lookup"><span data-stu-id="37f5d-108">Requirements for the service principal</span></span>

<span data-ttu-id="37f5d-109">Aşağıdaki gereksinimleri karşılayan mevcut bir Azure AD hizmet sorumlusunu kullanabilir veya yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f5d-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span></span>

* <span data-ttu-id="37f5d-110">**Kapsam**: Kubernetes kümesini dağıtmak için kullanılan abonelikteki veya (daha az sınırlayıcı bir tanımla) kümeyi dağıtmak için kullanılan abonelikteki kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="37f5d-110">**Scope**: the resource group in the subscription used to deploy the Kubernetes cluster, or (less restrictively) the subscription used to deploy the cluster.</span></span>

* <span data-ttu-id="37f5d-111">**Rol**: **Katkıda bulunan**</span><span class="sxs-lookup"><span data-stu-id="37f5d-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="37f5d-112">**Gizli anahtar**: Bir parola olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37f5d-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="37f5d-113">Şu anda sertifika kimlik doğrulaması için ayarlanmış bir hizmet sorumlusunu kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="37f5d-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="37f5d-114">Bir hizmet sorumlusu oluşturmak için, Azure AD kiracınızla bir uygulamayı kaydetme ve uygulamanızı aboneliğinizdeki bir role atama izinlerinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="37f5d-115">Gerekli izinlere sahip olup olmadığınızı görmek için [Portal’dan denetleyin](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="37f5d-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="37f5d-116">1. Seçenek: Azure AD'de hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="37f5d-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="37f5d-117">Kubernetes kümenizi dağıtmadan önce bir Azure AD hizmet sorumlusu oluşturmak isterseniz, Azure birkaç yöntem sunar.</span><span class="sxs-lookup"><span data-stu-id="37f5d-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="37f5d-118">Aşağıdaki örnek komut bunu [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md) ile nasıl gerçekleştirebileceğinizi göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="37f5d-119">Veya [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md) ya da diğer yöntemleri kullanarak bir hizmet sorumlusu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f5d-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="37f5d-120">Aşağıdakine benzer bir çıktı döndürülür (burada gösterilen sonuç kısaltılmıştır):</span><span class="sxs-lookup"><span data-stu-id="37f5d-120">Output is similar to the following (shown here redacted):</span></span>

![Hizmet sorumlusu oluşturma](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="37f5d-122">Vurgulanmış olan **istemci kimliği** (`appId`) ve **gizli anahtar** (`password`), küme dağıtımı için hizmet sorumlusu parametreleri olarak kullandığınız değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a><span data-ttu-id="37f5d-123">Kubernetes kümesi oluştururken hizmet sorumlusu belirtme</span><span class="sxs-lookup"><span data-stu-id="37f5d-123">Specify service principal when creating the Kubernetes cluster</span></span>

<span data-ttu-id="37f5d-124">Kubernetes kümesini oluştururken, mevcut bir hizmet sorumlusunun **istemci kimliğini** (Uygulama kimliği anlamına gelen `appId` olarak da bilinir) ve **gizli anahtarını** (`password`) parametre olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="37f5d-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="37f5d-125">Hizmet sorumlusunun bu makalenin başında verilen gereksinimleri karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="37f5d-125">Make sure the service principal meets the requirements at the beginning this article.</span></span>

<span data-ttu-id="37f5d-126">Kubernetes kümesini dağıtırken, bu parametreleri [Azure Komut Satırı Arabirimi (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portalı](../dcos-swarm/container-service-deployment.md) veya diğer yöntemleri kullanarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f5d-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="37f5d-127">**İstemci kimliğini** belirtirken, hizmet sorumlusunun `ObjectId` değerini değil `appId` değerini kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="37f5d-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="37f5d-128">Aşağıdaki örnekte Azure CLI 2.0 ile parametreleri iletme yollarından biri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span></span> <span data-ttu-id="37f5d-129">Bu örnekte [Kubernetes hızlı başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes) kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="37f5d-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="37f5d-130">`azuredeploy.parameters.json` şablon parametre dosyasını GitHub’dan [indirin](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="37f5d-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="37f5d-131">Hizmet sorumlusunu belirtmek için dosyada `servicePrincipalClientId` ve `servicePrincipalClientSecret` değerlerini girin.</span><span class="sxs-lookup"><span data-stu-id="37f5d-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="37f5d-132">(Ayrıca `dnsNamePrefix` ve `sshRSAPublicKey` için kendi değerlerinizi de belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="37f5d-133">İkincisi, kümeye erişmek için kullanılacak SSH ortak anahtarıdır.) Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="37f5d-133">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![Hizmet sorumlusu parametrelerini iletme](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="37f5d-135">Aşağıdaki komutu `--parameters` ile çalıştırarak azuredeploy.parameters.json dosyasının yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="37f5d-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="37f5d-136">Bu komut, kümeyi Batı ABD bölgesinde `myResourceGroup` adıyla oluşturduğunuz bir kaynak grubuna dağıtır.</span><span class="sxs-lookup"><span data-stu-id="37f5d-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a><span data-ttu-id="37f5d-137">2. Seçenek: `az acs create` ile küme oluştururken hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="37f5d-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span></span>

<span data-ttu-id="37f5d-138">Kubernetes kümesini oluşturmak için [`az acs create`](/cli/azure/acs#create) komutunu çalıştırırsanız, otomatik olarak bir hizmet sorumlusu oluşturma seçeneğine sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="37f5d-138">If you run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span></span>

<span data-ttu-id="37f5d-139">Diğer Kubernetes kümesi oluşturma seçeneklerinde olduğu gibi, `az acs create` çalıştırırken mevcut bir hizmet sorumlusunun parametrelerini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f5d-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="37f5d-140">Ancak, bu parametreleri atlarsanız Azure CLI, Container Service ile kullanılacak bir hizmet sorumlusunu otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="37f5d-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="37f5d-141">Bu işlem dağıtım sırasında saydam bir şekilde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-141">This takes place transparently during the deployment.</span></span> 

<span data-ttu-id="37f5d-142">Aşağıdaki komut, bir Kubernetes kümesi oluşturmaya ek olarak hem SSH anahtarlarını hem de hizmet sorumlusu kimlik bilgilerini üretir:</span><span class="sxs-lookup"><span data-stu-id="37f5d-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="37f5d-143">Hesabınızda Azure AD ve hizmet sorumlusu oluşturmaya yönelik abonelik izinleri yoksa, komut `Insufficient privileges to complete the operation.` benzeri bir hata oluşturur</span><span class="sxs-lookup"><span data-stu-id="37f5d-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="37f5d-144">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="37f5d-144">Additional considerations</span></span>

* <span data-ttu-id="37f5d-145">Aboneliğinizde hizmet sorumlusu oluşturma izniniz yoksa, Azure AD veya abonelik yöneticinizden gerekli izinleri atamasını istemeniz veya Azure Container Service ile kullanılacak hizmet sorumlusunu sormanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span></span> 

* <span data-ttu-id="37f5d-146">Kubernetes için hizmet sorumlusu, küme yapılandırmasının bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="37f5d-146">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="37f5d-147">Ancak, kümeyi dağıtmak için kimlik kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="37f5d-147">However, don't use the identity to deploy the cluster.</span></span>

* <span data-ttu-id="37f5d-148">Her hizmet sorumlusunun bir Azure AD uygulamasıyla ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="37f5d-149">Bir Kubernetes kümesinin hizmet sorumlusu, geçerli herhangi bir Azure AD uygulama adıyla ilişkilendirilebilir (örneğin: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="37f5d-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="37f5d-150">Uygulama URL'sinin gerçek bir uç nokta olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="37f5d-150">The URL for the application doesn't have to be a real endpoint.</span></span>

* <span data-ttu-id="37f5d-151">Hizmet sorumlusu **İstemci Kimliğini** belirtirken `appId` değerini (bu makalede gösterilen şekilde) veya karşılık gelen hizmet sorumlusu `name` değerini (örneğin, `https://www.contoso.org/example`) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f5d-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="37f5d-152">Kubernetes kümesindeki ana ve aracı VM’lerde hizmet sorumlusu kimlik bilgileri, /etc/kubernetes/azure.json dosyasında saklanır.</span><span class="sxs-lookup"><span data-stu-id="37f5d-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="37f5d-153">Hizmet sorumlusunu otomatik olarak oluşturmak için `az acs create` komutunu kullandığınızda, hizmet sorumlusu kimlik bilgileri komutun çalıştırıldığı bilgisayarda ~/.azure/acsServicePrincipal.json dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="37f5d-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span></span> 

* <span data-ttu-id="37f5d-154">`az acs create` komutu ile hizmet sorumlusunu otomatik olarak oluşturduğunuzda, hizmet sorumlusu aynı abonelikte oluşturulan bir [Azure kapsayıcı kayıt defteri](../../container-registry/container-registry-intro.md) ile de kimlik doğrulaması yapabilir.</span><span class="sxs-lookup"><span data-stu-id="37f5d-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="37f5d-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37f5d-155">Next steps</span></span>

* <span data-ttu-id="37f5d-156">Kapsayıcı hizmeti kümenizde [Kubernetes ile çalışmaya başlama](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="37f5d-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="37f5d-157">Kubernetes hizmet sorumlusu sorunlarını gidermek için bkz. [ACS Altyapısı belgeleri](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="37f5d-157">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


