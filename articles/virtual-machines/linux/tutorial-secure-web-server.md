---
title: "Bir web sunucusu ile Azure SSL sertifikalarının güvenli | Microsoft Docs"
description: "Azure'da bir Linux VM üzerinde SSL sertifikalarını NGINX web sunucusuyla güvenli öğrenin"
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
ms.openlocfilehash: 181be35aeb61020db3abaeba22aa882848923c31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="e2d88-103">Bir web sunucusu ile SSL sertifikalarını azure'da bir Linux sanal makinede güvenli</span><span class="sxs-lookup"><span data-stu-id="e2d88-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="e2d88-104">Web sunucularının güvenliğini sağlamak için bir Güvenli Yuva daha sonra (SSL) sertifikası web trafiğini şifrelemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e2d88-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="e2d88-105">Bu SSL sertifikalarını Azure anahtar kasası depolanabilir ve Azure'da, Linux sanal makineleri (VM'ler) sertifikalarının güvenli dağıtımlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2d88-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Linux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="e2d88-106">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e2d88-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2d88-107">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2d88-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="e2d88-108">Oluşturmak veya bir sertifika anahtar Kasası'na Karşıya Yükle</span><span class="sxs-lookup"><span data-stu-id="e2d88-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="e2d88-109">Bir VM oluşturun ve NGINX web sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="e2d88-109">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="e2d88-110">Sertifika VM ekleme ve NGINX SSL bağlaması ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e2d88-110">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e2d88-111">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e2d88-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e2d88-112">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e2d88-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="e2d88-113">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e2d88-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="e2d88-114">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e2d88-114">Overview</span></span>
<span data-ttu-id="e2d88-115">Azure anahtar kasası, şifreleme anahtarlarını ve gizli anahtarları, bu tür sertifikalar veya parolaları koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2d88-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="e2d88-116">Anahtar kasası, sertifika yönetimi işlemini kolaylaştırmaya yardımcı olur ve bu sertifikaları erişim anahtarlarını denetim kurmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2d88-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="e2d88-117">Anahtar kasası içinde otomatik olarak imzalanan bir sertifika oluşturun veya zaten sahip olduğunuz bir varolan, güvenilen bir sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e2d88-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="e2d88-118">Sertifikaları içeren özel bir VM görüntüsü kullanarak yerine desteklenmiş, sertifikaları çalışan VM ekleme.</span><span class="sxs-lookup"><span data-stu-id="e2d88-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="e2d88-119">Bu işlem en güncel sertifikaları dağıtımı sırasında bir web sunucusunda yüklü olan sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2d88-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="e2d88-120">Yenileme veya bir sertifikayı değiştirin, yeni bir özel VM görüntüsü oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e2d88-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="e2d88-121">Ek sanal makineleri oluştururken en son sertifikaları otomatik olarak eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="e2d88-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="e2d88-122">Tüm işlem sırasında sertifikalar hiçbir zaman Azure platformu bırakın veya bir komut dosyası, komut satırı geçmiş veya şablonda sunulur.</span><span class="sxs-lookup"><span data-stu-id="e2d88-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="e2d88-123">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2d88-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="e2d88-124">Bir anahtar kasası ve sertifikaları oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e2d88-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e2d88-125">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroupSecureWeb* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="e2d88-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="e2d88-126">Ardından, bir anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve bir VM dağıttığınızda kullanım için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e2d88-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="e2d88-127">Her anahtar kasası benzersiz bir ad gerektirir ve tüm küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e2d88-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="e2d88-128">Değiştir  *<mykeyvault>*  aşağıdaki örnekte kendi benzersiz bir anahtar kasası ad ile:</span><span class="sxs-lookup"><span data-stu-id="e2d88-128">Replace *<mykeyvault>* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="e2d88-129">Bir sertifika oluşturmak ve anahtar kasasına depolamak</span><span class="sxs-lookup"><span data-stu-id="e2d88-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="e2d88-130">Üretim kullanımı için güvenilen bir sağlayıcı tarafından imzalanmış geçerli bir sertifika almanız gerekir [az keyvault sertifika alma](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="e2d88-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="e2d88-131">Bu öğretici için aşağıdaki örnek, otomatik olarak imzalanan bir sertifika ile nasıl oluşturabileceğiniz gösterir [az keyvault sertifika oluştur](/cli/azure/certificate#create) varsayılan sertifika ilkesi kullanır:</span><span class="sxs-lookup"><span data-stu-id="e2d88-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="e2d88-132">Bir VM ile kullanılmak üzere bir sertifika hazırlama</span><span class="sxs-lookup"><span data-stu-id="e2d88-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="e2d88-133">VM sırasında sertifikayı kullanmak üzere işlem oluşturma, sertifikanızla kimliği elde [az keyvault gizli listesi sürümleri](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="e2d88-133">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="e2d88-134">Sertifikayla Dönüştür [az vm biçimi-gizli](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="e2d88-134">Convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="e2d88-135">Aşağıdaki örnek sonraki adımlarda kullanım kolaylığı için değişkenleri bu komutların çıktısı atar:</span><span class="sxs-lookup"><span data-stu-id="e2d88-135">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="e2d88-136">NGINX güvenli hale getirmek için bir bulut init yapılandırması oluştur</span><span class="sxs-lookup"><span data-stu-id="e2d88-136">Create a cloud-init config to secure NGINX</span></span>
<span data-ttu-id="e2d88-137">[Bulut init](https://cloudinit.readthedocs.io) ilk kez önyükleme gibi bir Linux VM özelleştirmek için yaygın olarak kullanılan bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="e2d88-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="e2d88-138">Bulut init paketleri yüklemek ve dosyaları yazma veya kullanıcılar ve güvenlik yapılandırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2d88-138">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="e2d88-139">Bulut init ilk önyükleme işlemi sırasında çalışırken, ek adımlar veya yapılandırmanızı uygulamak için gerekli aracıların yok.</span><span class="sxs-lookup"><span data-stu-id="e2d88-139">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="e2d88-140">VM, sertifikaları oluşturduğunuzda ve anahtarlar depolanır korumalı içinde */var/lib/waagent/* dizin.</span><span class="sxs-lookup"><span data-stu-id="e2d88-140">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="e2d88-141">Sertifika VM ekleme ve web sunucusu yapılandırma otomatikleştirmek için bulut init kullanın.</span><span class="sxs-lookup"><span data-stu-id="e2d88-141">To automate adding the certificate to the VM and configuring the web server, use cloud-init.</span></span> <span data-ttu-id="e2d88-142">Bu örnekte, yükleyin ve NGINX web sunucusu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e2d88-142">In this example, we install and configure the NGINX web server.</span></span> <span data-ttu-id="e2d88-143">Aynı işlem yüklemek ve Apache yapılandırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2d88-143">You can use the same process to install and configure Apache.</span></span> 

<span data-ttu-id="e2d88-144">Adlı bir dosya oluşturun *bulut-init-web-server.txt* ve aşağıdaki yapılandırma yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2d88-144">Create a file named *cloud-init-web-server.txt* and paste the following configuration:</span></span>

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

### <a name="create-a-secure-vm"></a><span data-ttu-id="e2d88-145">Güvenli bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2d88-145">Create a secure VM</span></span>
<span data-ttu-id="e2d88-146">Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e2d88-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e2d88-147">Sertifika verileri ile anahtar Kasası'ndan eklenen `--secrets` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e2d88-147">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="e2d88-148">Bulut init config ile geçirdiğiniz `--custom-data` parametre:</span><span class="sxs-lookup"><span data-stu-id="e2d88-148">You pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="e2d88-149">Oluşturulacak VM, yüklemek için paketleri ve uygulamayı başlatmak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="e2d88-149">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="e2d88-150">VM oluşturduğunuzda not edin `publicIpAddress` Azure CLI tarafından görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e2d88-150">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="e2d88-151">Bu adresi bir web tarayıcısında, siteye erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e2d88-151">This address is used to access your site in a web browser.</span></span>

<span data-ttu-id="e2d88-152">VM ulaşmak güvenli web trafiği izin vermek için 443 numaralı bağlantı noktasını Internet'ten gelen ile açmayı [az vm Aç-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="e2d88-152">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="e2d88-153">Güvenli web uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="e2d88-153">Test the secure web app</span></span>
<span data-ttu-id="e2d88-154">Bir web tarayıcısı açın ve girin artık *https://<publicIpAddress>*  adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="e2d88-154">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="e2d88-155">Kendi ortak sağlamak VM IP adresinden oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="e2d88-155">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="e2d88-156">Kendinden imzalı bir sertifika kullanılması durumunda güvenlik uyarısı kabul edin:</span><span class="sxs-lookup"><span data-stu-id="e2d88-156">Accept the security warning if you used a self-signed certificate:</span></span>

![Web tarayıcısı güvenlik uyarısını kabul edin](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="e2d88-158">Güvenli NGINX sitenizi sonra aşağıdaki örnekte olduğu gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="e2d88-158">Your secured NGINX site is then displayed as in the following example:</span></span>

![Çalışan güvenli NGINX sitesini görüntüle](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="e2d88-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e2d88-160">Next steps</span></span>

<span data-ttu-id="e2d88-161">Bu öğreticide, Azure anahtar kasasında depolanan bir SSL sertifikası ile bir NGINX web sunucusu güvenli.</span><span class="sxs-lookup"><span data-stu-id="e2d88-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="e2d88-162">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="e2d88-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2d88-163">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2d88-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="e2d88-164">Oluşturmak veya bir sertifika anahtar Kasası'na Karşıya Yükle</span><span class="sxs-lookup"><span data-stu-id="e2d88-164">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="e2d88-165">Bir VM oluşturun ve NGINX web sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="e2d88-165">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="e2d88-166">Sertifika VM ekleme ve NGINX SSL bağlaması ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e2d88-166">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="e2d88-167">Önceden derlenmiş sanal makine kod örnekleri görmek için bu bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="e2d88-167">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e2d88-168">Windows sanal makine kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="e2d88-168">Windows virtual machine script samples</span></span>](./cli-samples.md)