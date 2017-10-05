---
title: "OpenShift kaynak Azure'a dağıtma | Microsoft Docs"
description: "Azure sanal makinelerine OpenShift kaynak dağıtmayı öğrenin."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: e03da05625e440eab29ccc28a2343d3433fc7607
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-openshift-origin-to-azure-virtual-machines"></a><span data-ttu-id="adbc9-103">Azure sanal makinelerine OpenShift kaynak dağıtma</span><span class="sxs-lookup"><span data-stu-id="adbc9-103">Deploy OpenShift Origin to Azure Virtual Machines</span></span> 

<span data-ttu-id="adbc9-104">[OpenShift kaynak](https://www.openshift.org/) üzerinde oluşturulan bir açık kaynak kapsayıcı platformdur [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="adbc9-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="adbc9-105">Dağıtma, ölçeklendirme ve çok kiracılı uygulamalara çalışan işlemini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="adbc9-105">It simplifies the process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="adbc9-106">Bu kılavuz, OpenShift kaynak üzerinde Azure Azure CLI ve Azure Resource Manager şablonları kullanarak sanal makineleri dağıtmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="adbc9-106">This guide describes how to deploy OpenShift Origin on Azure Virtual Machines using the Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="adbc9-107">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="adbc9-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="adbc9-108">OpenShift küme için SSH anahtarları yönetmek için bir KeyVault oluşturun.</span><span class="sxs-lookup"><span data-stu-id="adbc9-108">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="adbc9-109">Azure VM'ler OpenShift kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="adbc9-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="adbc9-110">Yükleme ve yapılandırma [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) kümeyi yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="adbc9-110">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>
> * <span data-ttu-id="adbc9-111">OpenShift dağıtım özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="adbc9-111">Customize the OpenShift deployment.</span></span>

<span data-ttu-id="adbc9-112">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="adbc9-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="adbc9-113">Bu hızlı başlangıç Azure CLI Sürüm 2.0.8 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="adbc9-113">This quick start requires the Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="adbc9-114">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="adbc9-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="adbc9-115">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="adbc9-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="adbc9-116">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="adbc9-116">Log in to Azure</span></span> 
<span data-ttu-id="adbc9-117">Oturum açtığınızda, Azure aboneliğinizle [az oturum açma](/cli/azure/#login) komut ve izleyin ekrandaki yönergeleri veya tıklatın **deneyin** bulut Kabuğu'nu kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="adbc9-117">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions or click **Try it** to use Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="adbc9-118">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="adbc9-118">Create a resource group</span></span>

<span data-ttu-id="adbc9-119">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="adbc9-119">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="adbc9-120">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="adbc9-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="adbc9-121">Aşağıdaki örnek *eastus* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="adbc9-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="adbc9-122">Anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="adbc9-122">Create a Key Vault</span></span>
<span data-ttu-id="adbc9-123">Küme için SSH anahtarları depolamak için bir KeyVault oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="adbc9-123">Create a KeyVault to store the SSH keys for the cluster with the [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="adbc9-124">SSH anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="adbc9-124">Create an SSH key</span></span> 
<span data-ttu-id="adbc9-125">Bir SSH anahtarı OpenShift kaynak kümesine erişimi güvenli hale getirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="adbc9-125">An SSH key is needed to secure access to the OpenShift Origin cluster.</span></span> <span data-ttu-id="adbc9-126">Kullanarak bir SSH anahtar çifti oluşturma `ssh-keygen` komutu.</span><span class="sxs-lookup"><span data-stu-id="adbc9-126">Create an SSH key-pair using the `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="adbc9-127">Oluşturduğunuz SSH anahtar çiftiniz bir parola olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="adbc9-127">The SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="adbc9-128">Windows, SSH anahtarları hakkında daha fazla bilgi için [SSH oluşturma Windows anahtarları](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="adbc9-128">For more information on SSH keys on Windows, [How to create SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="adbc9-129">Anahtar kasasına SSH özel anahtar depolama</span><span class="sxs-lookup"><span data-stu-id="adbc9-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="adbc9-130">OpenShift dağıtım OpenShift asıl güvenli erişim için oluşturulan SSH anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="adbc9-130">The OpenShift deployment uses the SSH key you created to secure access to the OpenShift master.</span></span> <span data-ttu-id="adbc9-131">SSH anahtarı güvenli bir şekilde almasını dağıtımını etkinleştirmek için aşağıdaki komutu kullanarak anahtar kasasına anahtarı depolar.</span><span class="sxs-lookup"><span data-stu-id="adbc9-131">To enable the deployment to securely retrieve the SSH key, store the key in Key Vault using the following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="adbc9-132">Şablon dağıtımı için etkin</span><span class="sxs-lookup"><span data-stu-id="adbc9-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="adbc9-133">Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="adbc9-133">Create a service principal</span></span> 
<span data-ttu-id="adbc9-134">OpenShift bir kullanıcı adı ve parola veya bir hizmet sorumlusu kullanarak Azure ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="adbc9-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="adbc9-135">Bir Azure hizmet sorumlusu uygulamaları, hizmetleri ve OpenShift gibi Otomasyon araçları ile birlikte kullanabileceğiniz bir güvenlik kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="adbc9-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="adbc9-136">Denetim ve hizmet sorumlusu Azure'da gerçekleştirebilirsiniz ne gibi işlemler için izinler tanımlar.</span><span class="sxs-lookup"><span data-stu-id="adbc9-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="adbc9-137">Yalnızca bir kullanıcı adı ve parola sağlayarak üzerinden güvenliğini artırmak için bu örnek temel bir hizmet sorumlusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="adbc9-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="adbc9-138">Bir hizmet sorumlusu ile oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) ve OpenShift gereken kimlik bilgilerini çıktı:</span><span class="sxs-lookup"><span data-stu-id="adbc9-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="adbc9-139">Komuttan döndürülen AppID özelliği not edin.</span><span class="sxs-lookup"><span data-stu-id="adbc9-139">Take note of the appId property returned from the command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="adbc9-140">Güvenli olmayan bir parola oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="adbc9-140">Don't create an insecure password.</span></span>  <span data-ttu-id="adbc9-141">[Azure AD parola kuralları ve kısıtlamaları](/azure/active-directory/active-directory-passwords-policy) yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="adbc9-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="adbc9-142">Hizmet sorumluları hakkında daha fazla bilgi için bkz: [bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="adbc9-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-the-openshift-origin-template"></a><span data-ttu-id="adbc9-143">OpenShift kaynak şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="adbc9-143">Deploy the OpenShift Origin template</span></span>
<span data-ttu-id="adbc9-144">Sonraki OpenShift bir Azure Resource Manager şablonu kullanarak kaynak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="adbc9-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="adbc9-145">Aşağıdaki komutu az CLI 2.0.8 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="adbc9-145">The following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="adbc9-146">CLI az doğrulayabilirsiniz sürümüyle `az --version` komutu.</span><span class="sxs-lookup"><span data-stu-id="adbc9-146">You can verify the az CLI version with the `az --version` command.</span></span> <span data-ttu-id="adbc9-147">CLI Sürüm güncelleştirmek için bkz: [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="adbc9-147">To update the CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="adbc9-148">Kullanım `appId` daha önce oluşturduğunuz için hizmet sorumlusu değerinden `aadClientId` parametresi.</span><span class="sxs-lookup"><span data-stu-id="adbc9-148">Use the `appId` value from the service principal you created earlier for the `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="adbc9-149">Dağıtımın tamamlanması 20 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="adbc9-149">The deployment may take up to 20 minutes to complete.</span></span> <span data-ttu-id="adbc9-150">Dağıtım tamamlandığında OpenShift asıl DNS adını ve OpenShift konsol URL'sini terminale yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="adbc9-150">The URL of the OpenShift console and DNS name of the OpenShift master is printed to the terminal when the deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-to-the-openshift-cluster"></a><span data-ttu-id="adbc9-151">OpenShift kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="adbc9-151">Connect to the OpenShift cluster</span></span>
<span data-ttu-id="adbc9-152">Dağıtım tamamlandığında, tarayıcı kullanarak OpenShift Konsolu'na bağlanmak `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="adbc9-152">When the deployment completes, connect to the OpenShift console using the browser using the `OpenShift Console Uri`.</span></span> <span data-ttu-id="adbc9-153">Alternatif olarak, aşağıdaki komutu kullanarak OpenShift ana bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="adbc9-153">Alternatively, you can connect to the OpenShift master using the following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="adbc9-154">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="adbc9-154">Clean up resources</span></span>
<span data-ttu-id="adbc9-155">Artık gerekli olduğunda, kullanabileceğiniz [az grubu Sil](/cli/azure/group#delete) OpenShift küme, kaynak grubu kaldırmak için komut ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="adbc9-155">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="adbc9-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="adbc9-156">Next steps</span></span>

<span data-ttu-id="adbc9-157">Bu öğretici, öğrenilmiş nasıl için:</span><span class="sxs-lookup"><span data-stu-id="adbc9-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="adbc9-158">OpenShift küme için SSH anahtarları yönetmek için bir KeyVault oluşturun.</span><span class="sxs-lookup"><span data-stu-id="adbc9-158">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="adbc9-159">Azure VM'ler OpenShift kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="adbc9-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="adbc9-160">Yükleme ve yapılandırma [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) kümeyi yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="adbc9-160">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>

<span data-ttu-id="adbc9-161">Şimdi bu OpenShift kaynak küme dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="adbc9-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="adbc9-162">İlk Uygulamanızı dağıtmak ve OpenShift araçlarını kullanma hakkında bilgi almak için OpenShift öğreticileri izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adbc9-162">You can follow OpenShift tutorials to learn how to deploy your first application and use the OpenShift tools.</span></span> <span data-ttu-id="adbc9-163">Bkz: [OpenShift kaynağı ile çalışmaya başlama](https://docs.openshift.org/latest/getting_started/index.html) başlamak için.</span><span class="sxs-lookup"><span data-stu-id="adbc9-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) to get started.</span></span> 
