---
title: "SSL ile bir web sunucusu sertifikaları Azure'da aaaSecure | Microsoft Docs"
description: "Azure'da bir Linux VM üzerinde nasıl toosecure hello NGINX web sunucusu ile SSL sertifikaları öğrenin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="cea1c-103">Bir web sunucusu ile SSL sertifikalarını azure'da bir Linux sanal makinede güvenli</span><span class="sxs-lookup"><span data-stu-id="cea1c-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="cea1c-104">toosecure web sunucuları, bir Güvenli Yuva daha sonra (SSL) sertifikası olabilir tooencrypt web trafiği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cea1c-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="cea1c-105">Bu SSL sertifikalarını Azure anahtar kasası depolanabilir ve Azure'da sertifikaları tooLinux sanal makineleri (VM'ler) güvenli dağıtımlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="cea1c-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="cea1c-106">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cea1c-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cea1c-107">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="cea1c-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="cea1c-108">Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="cea1c-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="cea1c-109">Bir VM oluşturun ve hello NGINX web sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="cea1c-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="cea1c-110">VM hello Hello sertifika Ekle ve NGINX bir SSL bağlaması ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cea1c-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cea1c-111">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="cea1c-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cea1c-112">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="cea1c-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cea1c-113">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cea1c-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="cea1c-114">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cea1c-114">Overview</span></span>
<span data-ttu-id="cea1c-115">Azure anahtar kasası, şifreleme anahtarlarını ve gizli anahtarları, bu tür sertifikalar veya parolaları koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="cea1c-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="cea1c-116">Anahtar kasası hello sertifika yönetimi işlemini kolaylaştırmaya yardımcı olur ve bu sertifikaları erişim anahtarlarını toomaintain denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cea1c-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="cea1c-117">Anahtar kasası içinde otomatik olarak imzalanan bir sertifika oluşturun veya zaten sahip olduğunuz bir varolan, güvenilen bir sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cea1c-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="cea1c-118">Sertifikaları içeren özel bir VM görüntüsü kullanarak yerine desteklenmiş, sertifikaları çalışan VM ekleme.</span><span class="sxs-lookup"><span data-stu-id="cea1c-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="cea1c-119">Bu işlem hello en güncel sertifikaları dağıtımı sırasında bir web sunucusunda yüklü olan sağlar.</span><span class="sxs-lookup"><span data-stu-id="cea1c-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="cea1c-120">Yenileme veya bir sertifikayı değiştirin, yeni bir özel VM görüntüsü toocreate da yok.</span><span class="sxs-lookup"><span data-stu-id="cea1c-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="cea1c-121">Ek VM'ler oluşturmak gibi hello son sertifikaları otomatik olarak eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="cea1c-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="cea1c-122">Hello tüm işlem sırasında hiç hello sertifikaları hello Azure platformu bırakın veya bir komut dosyası, komut satırı geçmiş veya şablonda sunulur.</span><span class="sxs-lookup"><span data-stu-id="cea1c-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="cea1c-123">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="cea1c-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="cea1c-124">Bir anahtar kasası ve sertifikaları oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="cea1c-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="cea1c-125">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupSecureWeb* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="cea1c-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="cea1c-126">Ardından, bir anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve bir VM dağıttığınızda kullanım için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cea1c-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="cea1c-127">Her anahtar kasası benzersiz bir ad gerektirir ve tüm küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cea1c-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="cea1c-128">Değiştir  *<mykeyvault>*  kendi benzersiz bir anahtar kasası ad örnekle aşağıdaki hello içinde:</span><span class="sxs-lookup"><span data-stu-id="cea1c-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="cea1c-129">Bir sertifika oluşturmak ve anahtar kasasına depolamak</span><span class="sxs-lookup"><span data-stu-id="cea1c-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="cea1c-130">Üretim kullanımı için güvenilen bir sağlayıcı tarafından imzalanmış geçerli bir sertifika almanız gerekir [az keyvault sertifika alma](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="cea1c-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="cea1c-131">Bu öğretici için hello aşağıdaki örnek otomatik olarak imzalanan bir sertifika ile nasıl oluşturabileceğiniz gösterir [az keyvault sertifika oluştur](/cli/azure/certificate#create) hello varsayılan sertifika ilkesi kullanır:</span><span class="sxs-lookup"><span data-stu-id="cea1c-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="cea1c-132">Bir VM ile kullanılmak üzere bir sertifika hazırlama</span><span class="sxs-lookup"><span data-stu-id="cea1c-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="cea1c-133">toouse hello sertifika hello VM sırasında işlem oluşturma, sertifikanızla hello kimliği elde [az keyvault gizli listesi sürümleri](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="cea1c-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="cea1c-134">Merhaba sertifikayla Dönüştür [az vm biçimi-gizli](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="cea1c-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="cea1c-135">Aşağıdaki örnek hello hello kullanım kolaylığı için bu komutları toovariables hello çıktısını sonraki adımlar atar:</span><span class="sxs-lookup"><span data-stu-id="cea1c-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="cea1c-136">Bir bulut init config toosecure NGINX oluşturma</span><span class="sxs-lookup"><span data-stu-id="cea1c-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="cea1c-137">[Bulut init](https://cloudinit.readthedocs.io) yaygın olarak kullanılan bir yaklaşım toocustomize hello için ilk kez önyükleme bir Linux VM aynıdır.</span><span class="sxs-lookup"><span data-stu-id="cea1c-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="cea1c-138">Bulut init tooinstall paketleri ve dosyaları veya tooconfigure kullanıcılar ve güvenlik yazma kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea1c-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="cea1c-139">Bulut init hello ilk önyükleme işlemi sırasında çalışırken, hiçbir ek adımlar vardır veya aracıları tooapply yapılandırmanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="cea1c-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="cea1c-140">VM, sertifikaları oluşturduğunuzda ve anahtarlar, korumalı hello depolanır */var/lib/waagent/* dizin.</span><span class="sxs-lookup"><span data-stu-id="cea1c-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="cea1c-141">tooautomate sertifika toohello VM hello ekleyip hello web sunucusunu yapılandırma bulut init kullanın.</span><span class="sxs-lookup"><span data-stu-id="cea1c-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="cea1c-142">Bu örnekte, yükleyin ve hello NGINX web sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cea1c-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="cea1c-143">Merhaba kullanabilirsiniz aynı işlem tooinstall ve Apache yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cea1c-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="cea1c-144">Adlı bir dosya oluşturun *bulut-init-web-server.txt* Yapıştır hello izleyerek yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="cea1c-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="cea1c-145">Güvenli bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="cea1c-145">Create a secure VM</span></span>
<span data-ttu-id="cea1c-146">Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="cea1c-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="cea1c-147">Merhaba sertifika verileri ile Merhaba anahtar Kasası'nı eklenen `--secrets` parametresi.</span><span class="sxs-lookup"><span data-stu-id="cea1c-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="cea1c-148">Merhaba bulut init config hello ile geçirin `--custom-data` parametre:</span><span class="sxs-lookup"><span data-stu-id="cea1c-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="cea1c-149">Oluşturulan, hello VM toobe birkaç dakika sürer hello paketleri tooinstall ve hello uygulama toostart.</span><span class="sxs-lookup"><span data-stu-id="cea1c-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="cea1c-150">Merhaba VM oluşturduğunuzda hello not edin `publicIpAddress` hello Azure CLI tarafından görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cea1c-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="cea1c-151">Bu adres kullanılan tooaccess bir web tarayıcısında, sitedir.</span><span class="sxs-lookup"><span data-stu-id="cea1c-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="cea1c-152">açık bağlantı noktası 443 hello Internet gelen ile VM'nizi tooallow güvenli web trafiği tooreach [az vm Aç-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="cea1c-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="cea1c-153">Test hello güvenli web uygulaması</span><span class="sxs-lookup"><span data-stu-id="cea1c-153">Test hello secure web app</span></span>
<span data-ttu-id="cea1c-154">Bir web tarayıcısı açın ve girin artık *https://<publicIpAddress>*  hello adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="cea1c-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="cea1c-155">Kendi ortak sağlamak hello VM IP adresinden oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="cea1c-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="cea1c-156">Kendinden imzalı bir sertifika kullanılması durumunda hello güvenlik uyarısı kabul edin:</span><span class="sxs-lookup"><span data-stu-id="cea1c-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Web tarayıcısı güvenlik uyarısını kabul edin](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="cea1c-158">Güvenli NGINX sitenizi sonra aşağıdaki örneğine hello olduğu gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="cea1c-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Çalışan güvenli NGINX sitesini görüntüle](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="cea1c-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cea1c-160">Next steps</span></span>

<span data-ttu-id="cea1c-161">Bu öğreticide, Azure anahtar kasasında depolanan bir SSL sertifikası ile bir NGINX web sunucusu güvenli.</span><span class="sxs-lookup"><span data-stu-id="cea1c-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="cea1c-162">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="cea1c-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cea1c-163">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="cea1c-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="cea1c-164">Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="cea1c-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="cea1c-165">Bir VM oluşturun ve hello NGINX web sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="cea1c-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="cea1c-166">VM hello Hello sertifika Ekle ve NGINX bir SSL bağlaması ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cea1c-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="cea1c-167">Sanal makine kod örnekleri önceden oluşturulmuş Bu bağlantı toosee izleyin.</span><span class="sxs-lookup"><span data-stu-id="cea1c-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cea1c-168">Windows sanal makine kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="cea1c-168">Windows virtual machine script samples</span></span>](./cli-samples.md)