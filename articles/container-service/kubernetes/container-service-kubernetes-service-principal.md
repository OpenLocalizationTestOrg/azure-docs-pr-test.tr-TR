---
title: "Azure Kubernetes küme aaaService asıl | Microsoft Docs"
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
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="25ba5-103">Container Service’te bir Kubernetes kümesi için Azure AD hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="25ba5-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="25ba5-104">Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesi gerektiren bir [Azure Active Directory hizmet asıl](../../active-directory/develop/active-directory-application-objects.md) toointeract Azure API'leri ile.</span><span class="sxs-lookup"><span data-stu-id="25ba5-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="25ba5-105">Merhaba hizmet sorumlusu gereklidir toodynamically yönetmek kaynakları gibi [kullanıcı tanımlı yollar](../../virtual-network/virtual-networks-udr-overview.md) ve hello [katman 4 Azure yük dengeleyici](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25ba5-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="25ba5-106">Bu makale bir hizmet yukarı farklı seçenekler tooset Kubernetes kümeniz için asıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="25ba5-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="25ba5-107">Örneğin, yüklü ve hello ayarlarsanız [Azure CLI 2.0](/cli/azure/install-az-cli2), hello çalıştırabilirsiniz [ `az acs create` ](/cli/azure/acs#create) komutu toocreate hello Kubernetes küme ve hello hizmeti hello asıl aynı anda.</span><span class="sxs-lookup"><span data-stu-id="25ba5-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="25ba5-108">Merhaba hizmet sorumlusu için gereksinimler</span><span class="sxs-lookup"><span data-stu-id="25ba5-108">Requirements for hello service principal</span></span>

<span data-ttu-id="25ba5-109">Karşılıyor gereksinimlerine hello veya yeni bir tane oluşturun var olan bir Azure AD hizmet sorumlusu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25ba5-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="25ba5-110">**Kapsam**: hello abonelik hello kaynak grubunda kullanılan toodeploy hello Kubernetes küme veya hello abonelik toodeploy hello küme (daha az giderilirken) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="25ba5-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="25ba5-111">**Rol**: **Katkıda bulunan**</span><span class="sxs-lookup"><span data-stu-id="25ba5-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="25ba5-112">**Gizli anahtar**: Bir parola olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="25ba5-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="25ba5-113">Şu anda sertifika kimlik doğrulaması için ayarlanmış bir hizmet sorumlusunu kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="25ba5-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="25ba5-114">bir hizmet sorumlusu toocreate, aboneliğinizde Azure AD kiracısı ve tooassign hello uygulama tooa rolüne sahip bir uygulama izinleri tooregister olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="25ba5-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="25ba5-115">Merhaba gerekli izinlere sahip toosee [hello Portal denetleyin](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="25ba5-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="25ba5-116">1. Seçenek: Azure AD'de hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="25ba5-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="25ba5-117">Kubernetes kümenizi dağıtmadan önce bir Azure AD hizmet sorumlusu toocreate istiyorsanız, Azure çeşitli yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="25ba5-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="25ba5-118">Aşağıdaki örnek komutlar hello Göster, nasıl toodo bu hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="25ba5-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="25ba5-119">Alternatif olarak kullanarak bir hizmet asıl oluşturabilirsiniz [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), veya diğer yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="25ba5-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="25ba5-120">Çıktı (burada Redaksiyonu yapılmış gösterilen) benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="25ba5-120">Output is similar toohello following (shown here redacted):</span></span>

![Hizmet sorumlusu oluşturma](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="25ba5-122">Vurgulanan hello olan **istemci kimliği** (`appId`) ve hello **gizli** (`password`), Küme dağıtımı için hizmet asıl parametreleri olarak kullanma.</span><span class="sxs-lookup"><span data-stu-id="25ba5-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="25ba5-123">Hizmet sorumlusu hello Kubernetes küme oluştururken belirtin</span><span class="sxs-lookup"><span data-stu-id="25ba5-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="25ba5-124">Merhaba sağlamak **istemci kimliği** (hello olarak da bilinir `appId`, uygulama kimliği için) ve **gizli** (`password`) var olan bir hizmet olarak hello oluşturduğunuzda parametreler sorumlusu Kubernetes küme.</span><span class="sxs-lookup"><span data-stu-id="25ba5-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="25ba5-125">Bu makalede başlayan hello hello gereksinimlerine Hello hizmet sorumlusu karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="25ba5-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="25ba5-126">Hello kullanarak hello Kubernetes kümesini dağıtırken bu parametreleri belirtebilirsiniz [Azure komut satırı arabirimi (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), veya diğer yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="25ba5-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="25ba5-127">Merhaba belirtirken **istemci kimliği**, emin toouse hello olması `appId`, değil hello `ObjectId`, hello hizmet asıl.</span><span class="sxs-lookup"><span data-stu-id="25ba5-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="25ba5-128">Merhaba aşağıdaki örnek bir yolu toopass hello Azure CLI 2.0 hello parametrelerle gösterir.</span><span class="sxs-lookup"><span data-stu-id="25ba5-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="25ba5-129">Bu örnek hello kullanır [Kubernetes hızlı başlatma şablonunu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="25ba5-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="25ba5-130">[Karşıdan](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello şablon parametreleri dosyası `azuredeploy.parameters.json` github'dan.</span><span class="sxs-lookup"><span data-stu-id="25ba5-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="25ba5-131">toospecify hello hizmet sorumlusu için değerleri girin `servicePrincipalClientId` ve `servicePrincipalClientSecret` hello dosyasında.</span><span class="sxs-lookup"><span data-stu-id="25ba5-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="25ba5-132">(Ayrıca tooprovide için kendi değerlerinizi ihtiyacınız `dnsNamePrefix` ve `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="25ba5-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="25ba5-133">Merhaba ikinci hello SSH ortak anahtarı tooaccess hello kümedir.) Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="25ba5-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![Hizmet sorumlusu parametrelerini iletme](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="25ba5-135">Aşağıdaki komut, kullanarak çalışma hello `--parameters` tooset hello yol toohello azuredeploy.parameters.json dosyası.</span><span class="sxs-lookup"><span data-stu-id="25ba5-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="25ba5-136">Bu komut hello küme çağrılan oluşturduğunuz bir kaynak grubunda dağıtır `myResourceGroup` hello Batı ABD bölgesindeki.</span><span class="sxs-lookup"><span data-stu-id="25ba5-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="25ba5-137">Seçeneği 2: Merhaba küme oluştururken, bir hizmet sorumlusu oluşturma`az acs create`</span><span class="sxs-lookup"><span data-stu-id="25ba5-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="25ba5-138">Merhaba çalıştırırsanız [ `az acs create` ](/cli/azure/acs#create) komutu toocreate Kubernetes küme Merhaba, hello seçeneği toogenerate bir hizmet sorumlusu otomatik olarak olur.</span><span class="sxs-lookup"><span data-stu-id="25ba5-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="25ba5-139">Diğer Kubernetes kümesi oluşturma seçeneklerinde olduğu gibi, `az acs create` çalıştırırken mevcut bir hizmet sorumlusunun parametrelerini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25ba5-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="25ba5-140">Ancak, bu parametreyi de atladığınızda hello Azure CLI otomatik olarak kullanmak için bir tane kapsayıcı hizmeti ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="25ba5-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="25ba5-141">Bu saydam hello dağıtımı sırasında gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="25ba5-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="25ba5-142">Merhaba aşağıdaki komutu Kubernetes küme oluşturur ve SSH anahtarları ve hizmet asıl kimlik bilgilerini oluşturur:</span><span class="sxs-lookup"><span data-stu-id="25ba5-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="25ba5-143">Hesabınızı hello Azure AD ve abonelik izinleri toocreate yoksa ve bir hizmet sorumlusu hello komutu benzer bir hata çok oluşturur`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="25ba5-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="25ba5-144">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="25ba5-144">Additional considerations</span></span>

* <span data-ttu-id="25ba5-145">Bir hizmet asıl izinleri toocreate aboneliğinizde sahip değilseniz, tooask gerekebilecek Azure AD veya abonelik Yöneticisi tooassign hello gerekli izinleri ya da Azure kapsayıcı hizmeti ile bir hizmet asıl toouse için isteyin.</span><span class="sxs-lookup"><span data-stu-id="25ba5-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="25ba5-146">Merhaba hizmet sorumlusu Kubernetes için hello küme yapılandırmasının bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="25ba5-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="25ba5-147">Ancak, hello kimlik toodeploy hello küme kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="25ba5-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="25ba5-148">Her hizmet sorumlusunun bir Azure AD uygulamasıyla ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="25ba5-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="25ba5-149">Merhaba hizmet sorumlusu Kubernetes kümesi için geçerli tüm Azure ile ilişkilendirilebilir AD uygulama adı (örneğin: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="25ba5-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="25ba5-150">Merhaba uygulaması Hello URL'sini toobe gerçek bir uç nokta yok.</span><span class="sxs-lookup"><span data-stu-id="25ba5-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="25ba5-151">Merhaba hizmet sorumlusu belirlerken **istemci kimliği**, hello hello değerini kullanabilirsiniz `appId` (Bu makalede gösterildiği gibi) veya hello karşılık gelen hizmet sorumlusu `name` (örneğin,`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="25ba5-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="25ba5-152">Hello Yöneticisi ve hello Kubernetes kümedeki sanal makineleri aracı üzerinde hello hizmet asıl kimlik hello dosya /etc/kubernetes/azure.json depolanır.</span><span class="sxs-lookup"><span data-stu-id="25ba5-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="25ba5-153">Merhaba kullandığınızda `az acs create` toogenerate hello hizmet sorumlusu komutu otomatik olarak, hello hizmet asıl kimlik toohello dosya ~/.azure/acsServicePrincipal.json hello makinede kullanılan toorun hello komutu yazılır.</span><span class="sxs-lookup"><span data-stu-id="25ba5-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="25ba5-154">Merhaba kullandığınızda `az acs create` toogenerate hello hizmet sorumlusu komutu otomatik olarak, hello hizmet sorumlusu kimliğini de bir [Azure kapsayıcı kayıt defteri](../../container-registry/container-registry-intro.md) hello aynı oluşturulan abonelik.</span><span class="sxs-lookup"><span data-stu-id="25ba5-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="25ba5-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25ba5-155">Next steps</span></span>

* <span data-ttu-id="25ba5-156">Kapsayıcı hizmeti kümenizde [Kubernetes ile çalışmaya başlama](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="25ba5-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="25ba5-157">tootroubleshoot hello hizmet sorumlusu Kubernetes için bkz: Merhaba [ACS altyapısı belgelerine](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="25ba5-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


