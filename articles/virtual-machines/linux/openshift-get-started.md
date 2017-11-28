---
title: aaaDeploy OpenShift kaynak tooAzure | Microsoft Docs
description: "Toodeploy OpenShift kaynak tooAzure sanal makineler hakkında bilgi edinin."
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
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="fabd4-103">OpenShift kaynak tooAzure sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="fabd4-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="fabd4-104">[OpenShift kaynak](https://www.openshift.org/) üzerinde oluşturulan bir açık kaynak kapsayıcı platformdur [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="fabd4-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="fabd4-105">Dağıtma, ölçeklendirme ve çok kiracılı uygulamalara işletim hello sürecini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="fabd4-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="fabd4-106">Bu kılavuz, Azure sanal makineleri kullanma OpenShift kaynak toodeploy nasıl hello Azure CLI ve Azure Resource Manager şablonları açıklar.</span><span class="sxs-lookup"><span data-stu-id="fabd4-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="fabd4-107">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fabd4-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fabd4-108">KeyVault toomanage hello OpenShift kümesi için SSH anahtarları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="fabd4-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="fabd4-109">Azure VM'ler OpenShift kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="fabd4-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="fabd4-110">Yükleme ve yapılandırma hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello küme.</span><span class="sxs-lookup"><span data-stu-id="fabd4-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="fabd4-111">Merhaba OpenShift dağıtım özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="fabd4-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="fabd4-112">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fabd4-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="fabd4-113">Bu hızlı başlangıç hello Azure CLI Sürüm 2.0.8 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="fabd4-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="fabd4-114">çalıştırma toofind hello sürüm `az --version`.</span><span class="sxs-lookup"><span data-stu-id="fabd4-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="fabd4-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fabd4-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="fabd4-116">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="fabd4-116">Log in tooAzure</span></span> 
<span data-ttu-id="fabd4-117">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin veya **deneyin** toouse bulut Kabuk.</span><span class="sxs-lookup"><span data-stu-id="fabd4-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="fabd4-118">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fabd4-118">Create a resource group</span></span>

<span data-ttu-id="fabd4-119">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="fabd4-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="fabd4-120">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="fabd4-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="fabd4-121">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="fabd4-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="fabd4-122">Anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="fabd4-122">Create a Key Vault</span></span>
<span data-ttu-id="fabd4-123">KeyVault toostore hello ile Merhaba hello kümesi için SSH anahtarları oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="fabd4-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="fabd4-124">SSH anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fabd4-124">Create an SSH key</span></span> 
<span data-ttu-id="fabd4-125">Bir SSH anahtarı gerekli toosecure erişim toohello OpenShift kaynak kümesi olur.</span><span class="sxs-lookup"><span data-stu-id="fabd4-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="fabd4-126">Bir SSH anahtarı çifti oluşturma hello kullanarak `ssh-keygen` komutu.</span><span class="sxs-lookup"><span data-stu-id="fabd4-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="fabd4-127">Merhaba SSH anahtar çifti oluşturduğunuz bir parola olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fabd4-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="fabd4-128">Windows, SSH anahtarları hakkında daha fazla bilgi için [nasıl Windows toocreate SSH anahtarları](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="fabd4-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="fabd4-129">Anahtar kasasına SSH özel anahtar depolama</span><span class="sxs-lookup"><span data-stu-id="fabd4-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="fabd4-130">Merhaba OpenShift dağıtım toohello OpenShift ana toosecure erişim oluşturulan hello SSH anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="fabd4-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="fabd4-131">tooenable hello dağıtım toosecurely hello SSH anahtarı almak, komutu aşağıdaki hello kullanarak anahtar kasasına hello anahtarını depolamak.</span><span class="sxs-lookup"><span data-stu-id="fabd4-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="fabd4-132">Şablon dağıtımı için etkin</span><span class="sxs-lookup"><span data-stu-id="fabd4-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="fabd4-133">Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fabd4-133">Create a service principal</span></span> 
<span data-ttu-id="fabd4-134">OpenShift bir kullanıcı adı ve parola veya bir hizmet sorumlusu kullanarak Azure ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="fabd4-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="fabd4-135">Bir Azure hizmet sorumlusu uygulamaları, hizmetleri ve OpenShift gibi Otomasyon araçları ile birlikte kullanabileceğiniz bir güvenlik kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="fabd4-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="fabd4-136">Denetim ve toowhat işlemleri hello hizmet sorumlusu Azure'da gerçekleştirebilirsiniz gibi hello izinleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="fabd4-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="fabd4-137">yalnızca bir kullanıcı adı ve parola sağlayarak tooimprove güvenliği, bu örnek temel bir hizmet sorumlusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fabd4-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="fabd4-138">Bir hizmet sorumlusu ile oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) ve OpenShift gereken çıktı hello kimlik bilgileri:</span><span class="sxs-lookup"><span data-stu-id="fabd4-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="fabd4-139">Merhaba komutundan geri döndürülen hello AppID özelliği not edin.</span><span class="sxs-lookup"><span data-stu-id="fabd4-139">Take note of hello appId property returned from hello command.</span></span>
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
 > <span data-ttu-id="fabd4-140">Güvenli olmayan bir parola oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="fabd4-140">Don't create an insecure password.</span></span>  <span data-ttu-id="fabd4-141">[Azure AD parola kuralları ve kısıtlamaları](/azure/active-directory/active-directory-passwords-policy) yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="fabd4-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="fabd4-142">Hizmet sorumluları hakkında daha fazla bilgi için bkz: [bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="fabd4-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="fabd4-143">Merhaba OpenShift kaynak şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="fabd4-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="fabd4-144">Sonraki OpenShift bir Azure Resource Manager şablonu kullanarak kaynak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="fabd4-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="fabd4-145">Merhaba aşağıdaki komutu gerektirir az CLI 2.0.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="fabd4-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="fabd4-146">Doğrulayabilirsiniz az CLI hello hello sürümüyle `az --version` komutu.</span><span class="sxs-lookup"><span data-stu-id="fabd4-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="fabd4-147">tooupdate hello CLI Sürüm bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fabd4-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="fabd4-148">Kullanım hello `appId` daha önce oluşturduğunuz Merhaba hello hizmet sorumlusu değerinden `aadClientId` parametresi.</span><span class="sxs-lookup"><span data-stu-id="fabd4-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

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
<span data-ttu-id="fabd4-149">Merhaba dağıtım too20 dakika toocomplete sürebilir.</span><span class="sxs-lookup"><span data-stu-id="fabd4-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="fabd4-150">Merhaba dağıtım tamamlandığında hello hello OpenShift konsol URL'sini ve hello DNS adını yöneticisidir OpenShift toohello terminal yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="fabd4-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="fabd4-151">Toohello OpenShift kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="fabd4-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="fabd4-152">Merhaba dağıtım tamamlandığında hello kullanarak hello tarayıcı kullanarak toohello OpenShift konsol bağlantısı `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="fabd4-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="fabd4-153">Alternatif olarak, komutu aşağıdaki hello kullanarak toohello OpenShift asıl bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fabd4-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="fabd4-154">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="fabd4-154">Clean up resources</span></span>
<span data-ttu-id="fabd4-155">Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, OpenShift küme ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="fabd4-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="fabd4-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fabd4-156">Next steps</span></span>

<span data-ttu-id="fabd4-157">Bu öğretici, öğrenilmiş nasıl için:</span><span class="sxs-lookup"><span data-stu-id="fabd4-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="fabd4-158">KeyVault toomanage hello OpenShift kümesi için SSH anahtarları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="fabd4-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="fabd4-159">Azure VM'ler OpenShift kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="fabd4-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="fabd4-160">Yükleme ve yapılandırma hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello küme.</span><span class="sxs-lookup"><span data-stu-id="fabd4-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="fabd4-161">Şimdi bu OpenShift kaynak küme dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="fabd4-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="fabd4-162">OpenShift öğreticileri toolearn nasıl izleyebilirsiniz toodeploy ilk uygulama ve kullanım OpenShift araçları hello.</span><span class="sxs-lookup"><span data-stu-id="fabd4-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="fabd4-163">Bkz: [OpenShift kaynağı ile çalışmaya başlama](https://docs.openshift.org/latest/getting_started/index.html) tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="fabd4-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
