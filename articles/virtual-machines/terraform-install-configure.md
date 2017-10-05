---
title: "VM'ler ve diğer Azure altyapısında sağlayacak Terraform yükleyip | Microsoft Docs"
description: "Yükleyin ve Azure kaynaklarını oluşturmak için Terraform yapılandırma hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 1f26bccf279ebb61fbf77767186d0435e4f4ba40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-configure-terraform-to-provision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="eeaa0-103">Yükleme ve Azure'da VM'ler ve diğer altyapıya sağlamak için Terraform yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eeaa0-103">Install and configure Terraform to provision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="eeaa0-104">Bu makalede yüklemek ve Azure'da sanal makineleri gibi sağlama kaynaklarına Terraform yapılandırmak için gerekli adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-104">This article describes the necessary steps to install and configure Terraform to provision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="eeaa0-105">Oluşturma ve bulut kaynaklarına güvenli bir şekilde sağlamak Terraform etkinleştirmek için Azure kimlik bilgilerini kullanan öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-105">You will learn how to create and use Azure credentials to enable Terraform to provision cloud resources in a secure manner.</span></span>

<span data-ttu-id="eeaa0-106">HashiCorp Terraform tanımlamak ve bulut altyapısı HashiCorp yapılandırma dili (HCL) adlı bir özel şablon dili kullanarak dağıtmak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-106">HashiCorp Terraform provides an easy way to define and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="eeaa0-107">Bu özel dil [yazmak kolay ve kolay anlaşılır](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-107">This custom language is [easy to write and easy to understand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="eeaa0-108">Kullanarak Ayrıca, `terraform plan` komutu, görselleştirmek değişiklikleri altyapınız için bunları kullanmadan önce.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-108">Additionally, by using the `terraform plan` command, you can visualize the changes to your infrastructure before you commit them.</span></span> <span data-ttu-id="eeaa0-109">Azure ile Terraform kullanmaya başlamak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-109">Follow these steps to start using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="eeaa0-110">Terraform yükleyin</span><span class="sxs-lookup"><span data-stu-id="eeaa0-110">Install Terraform</span></span>
<span data-ttu-id="eeaa0-111">Terraform, yüklemek için [karşıdan](https://www.terraform.io/downloads.html) bir ayrı bir işletim sistemi için uygun paket yükleme dizini.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-111">To install Terraform, [download](https://www.terraform.io/downloads.html) the package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="eeaa0-112">Yükleme için genel bir yol da tanımlamanız gerekir bir tek bir yürütülebilir dosya içerir.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-112">The download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="eeaa0-113">Linux ve Mac'de yolunu ayarlama hakkında daha fazla yönerge için Git [bu Web sayfası](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-113">For instructions on how to set the path on Linux and Mac, go to [this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="eeaa0-114">Windows üzerinde yolunu ayarlama hakkında daha fazla yönerge için Git [bu Web sayfası](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-114">For instructions on how to set the path on Windows, go to [this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="eeaa0-115">Kurulumunuzu doğrulamak için çalıştırın `terraform` komutu.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-115">To verify your installation, run the `terraform` command.</span></span> <span data-ttu-id="eeaa0-116">Çıkış olarak kullanılabilir Terraform seçeneklerin bir listesini görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="eeaa0-117">Ardından, altyapı sağlamak için Azure aboneliğinizin Terraform erişmesine izin vermek gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-117">Next, you need to allow Terraform access to your Azure subscription to perform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-to-azure"></a><span data-ttu-id="eeaa0-118">Azure Terraform erişimi ayarlama</span><span class="sxs-lookup"><span data-stu-id="eeaa0-118">Set up Terraform access to Azure</span></span>
<span data-ttu-id="eeaa0-119">Terraform sağlama kaynaklara Azure'da etkinleştirmek için Azure Active Directory (Azure AD) iki varlık oluşturmanız gerekir: Azure AD uygulaması ve bir Azure AD hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-119">To enable Terraform to provision resources into Azure, you need to create two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="eeaa0-120">Ardından, Terraform komut dosyalarınızı bu varlıkları tanımlayıcılar kullanın.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="eeaa0-121">Bir hizmet sorumlusu genel Azure yerel örneğidir AD uygulaması.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="eeaa0-122">Bir hizmet sorumlusu Genel kaynaklar için ayrıntılı yerel erişim denetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-122">A service principal allows granular local access control to global resources.</span></span>

<span data-ttu-id="eeaa0-123">Azure AD uygulaması ve bir Azure AD hizmet sorumlusu oluşturmak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-123">There are several ways to create an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="eeaa0-124">Kolay ve hızlı şekilde bugün Azure CLI 2.0 kullanmaktır hangi [indirin ve Windows, Linux veya Mac yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-124">The easiest and fastest way today is to use Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="eeaa0-125">Gerekli güvenlik altyapısı oluşturmak için PowerShell veya Azure CLI 1.0 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-125">You also can use PowerShell or Azure CLI 1.0 to create the necessary security infrastructure.</span></span> <span data-ttu-id="eeaa0-126">Aşağıdaki yönergelerde Terraform Azure için tüm bu yaklaşım kullanarak yapılandırmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-126">The instructions that follow show you how to configure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="eeaa0-127">Azure CLI 2.0 (Windows, Linux veya Mac kullanıcıları için) kullanın</span><span class="sxs-lookup"><span data-stu-id="eeaa0-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="eeaa0-128">Karşıdan yükleyip sonra [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), aşağıdaki komutu gönderdikten Azure aboneliğinizi yönetmek oturum açın:</span><span class="sxs-lookup"><span data-stu-id="eeaa0-128">After you download and install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in to administer your Azure subscription by issuing the following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="eeaa0-129">Çin, Azure Almanya veya Azure kamu Bulutlar kullanıyorsanız, önce bu bulut ile çalışmak için Azure CLI yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-129">If you use the China, Azure Germany, or Azure Government clouds, you need to first configure the Azure CLI to work with that cloud.</span></span> <span data-ttu-id="eeaa0-130">Aşağıdaki komutu çalıştırarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eeaa0-130">You can do this by running the following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="eeaa0-131">Birden çok Azure aboneliğiniz varsa, bunların ayrıntıları tarafından döndürülen `az login` komutu.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-131">If you have multiple Azure subscriptions, their details are returned by the `az login` command.</span></span> <span data-ttu-id="eeaa0-132">Ayarlama `SUBSCRIPTION_ID` döndürülen değeri tutmak için ortam değişkeni `id` kullanmak istediğiniz abonelikten alan.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-132">Set the `SUBSCRIPTION_ID` environment variable to hold the value of the returned `id` field from the subscription you want to use.</span></span> 

<span data-ttu-id="eeaa0-133">Bu oturum için kullanmak istediğiniz aboneliği ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-133">Set the subscription that you want to use for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="eeaa0-134">Abonelik kimliği ve Kiracı kimliği değerleri almak için hesap sorgu.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-134">Query the account to get the subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="eeaa0-135">Ardından, farklı kimlik bilgileri için Terraform oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="eeaa0-136">AppID, parola, sp_name ve Kiracı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="eeaa0-137">Uygulama kimliği ve parola not edin.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-137">Make a note of the appId and password.</span></span>

<span data-ttu-id="eeaa0-138">Kimlik bilgilerinizi (hizmet sorumlusu) onaylamak için yeni bir Kabuğu'nu açın ve aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-138">To confirm your credentials (service principal), open a new shell and run the following commands.</span></span> <span data-ttu-id="eeaa0-139">Sp_name, şifresi ve Kiracı için döndürülen değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="eeaa0-139">Substitute the returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="eeaa0-140">(Windows kullanıcıları için) PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="eeaa0-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="eeaa0-141">Yazma ve yürütme Terraform komut dosyalarınızı ve yapılandırma görevleri için PowerShell kullanmak için bir Windows makinesine kullanmak için makinenizde sağ PowerShell araçları ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-141">To use a Windows machine to write and execute your Terraform scripts and to use PowerShell for configuration tasks, configure your machine with the right PowerShell tools.</span></span> 

1. <span data-ttu-id="eeaa0-142">İçindeki adımları izleyerek PowerShell araçlarını yükleme [yükleyin ve Azure PowerShell yapılandırma](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-142">Install PowerShell tools by following the steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="eeaa0-143">İndir ve Yürüt [azure setup.ps1 betik](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) PowerShell konsolundan.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-143">Download and execute the [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from the PowerShell console.</span></span>

3. <span data-ttu-id="eeaa0-144">Azure setup.ps1 komut dosyasını çalıştırmak için onu indir ve Yürüt `./azure-setup.ps1 setup` PowerShell konsolundan komutu.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-144">To run the azure-setup.ps1 script, download it and execute the `./azure-setup.ps1 setup` command from the PowerShell console.</span></span> <span data-ttu-id="eeaa0-145">Ardından Azure aboneliğinize yönetici ayrıcalıklarıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-145">Then sign in to your Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="eeaa0-146">Bir uygulama adı (isteğe bağlı dize gerekli) sağlamanız istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="eeaa0-147">İsteğe bağlı olarak, istendiğinde güçlü bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="eeaa0-148">Bir parola sağlamazsanız, güçlü bir parola sizin için .NET güvenlik kitaplıklarını kullanarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="eeaa0-149">Azure CLI 1.0 (Linux veya Mac kullanıcıları için) kullanın</span><span class="sxs-lookup"><span data-stu-id="eeaa0-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="eeaa0-150">Linux makineler veya Azure CLI 1.0 ile Mac'ler Terraform ile çalışmaya başlamak için uygun kitaplıkları makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-150">To get started with Terraform on Linux machines or Macs with Azure CLI 1.0, install the proper libraries on your machine.</span></span>  

1. <span data-ttu-id="eeaa0-151">İçindeki adımları izleyerek Azure xPlat CLI araçlarını yükleme [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-151">Install Azure xPlat CLI tools by following the steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="eeaa0-152">Karşıdan yükleyip JSON işlemci yönergeleri takip ederek [karşıdan jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-152">Download and install a JSON processor by following the instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="eeaa0-153">İndir ve Yürüt [azure setup.sh betik](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) komut konsolundan bash.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-153">Download and execute the [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from the console.</span></span>

4. <span data-ttu-id="eeaa0-154">Azure setup.sh komut dosyasını çalıştırmak için onu indir ve Yürüt `./azure-setup setup` konsolundan komutu.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-154">To run the azure-setup.sh script, download it and execute the `./azure-setup setup` command from the console.</span></span> <span data-ttu-id="eeaa0-155">Ardından Azure aboneliğinize yönetici ayrıcalıklarıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-155">Then sign in to your Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="eeaa0-156">Bir uygulama adı (isteğe bağlı dize gerekli) sağlamanız istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="eeaa0-157">İsteğe bağlı olarak, istendiğinde güçlü bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="eeaa0-158">Bir parola sağlamazsanız, güçlü bir parola sizin için .NET güvenlik kitaplıklarını kullanarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="eeaa0-159">Önceki tüm betikler, bir Azure AD uygulaması ve hizmet sorumlusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-159">All the previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="eeaa0-160">Hizmet sorumlusu abonelikte katılımcı veya sahibi düzeyinde erişim alır.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-160">The service principal gets a contributor or owner-level access on the subscription.</span></span> <span data-ttu-id="eeaa0-161">Yüksek verilen erişim düzeyi nedeniyle, bu komut dosyaları tarafından üretilen güvenlik bilgileri her zaman korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-161">Because of the high level of access granted, you should always protect the security information generated by those scripts.</span></span> <span data-ttu-id="eeaa0-162">Bu komut dosyaları tarafından sağlanan güvenlik bilgileri tüm dört adet Not: AppID, parola, ABONELİK_KİMLİĞİ ve tenant_id.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="eeaa0-163">Ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="eeaa0-163">Set environment variables</span></span>
<span data-ttu-id="eeaa0-164">Oluşturma ve Azure AD hizmet sorumlusu yapılandırdıktan sonra Kiracı kimliği, abonelik kimliği, istemci kimliği ve istemci parolası kullanmak için bilmeniz Terraform izin gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-164">After you create and configure an Azure AD service principal, you need to let Terraform know the tenant ID, subscription ID, client ID, and client secret to use.</span></span> <span data-ttu-id="eeaa0-165">Bu değerleri Terraform komut dosyalarınızı gömerek açıklandığı gibi bunu yapabilirsiniz [Terraform kullanarak temel altyapı oluşturma](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="eeaa0-166">Alternatif olarak, aşağıdaki ortam değişkenleri ayarlayabilir (ve dolayısıyla yanlışlıkla etme veya kimlik bilgilerinizi paylaşımı kaçının):</span><span class="sxs-lookup"><span data-stu-id="eeaa0-166">Alternately, you can set the following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="eeaa0-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="eeaa0-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="eeaa0-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="eeaa0-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="eeaa0-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="eeaa0-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="eeaa0-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="eeaa0-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="eeaa0-171">Bu değişkenleri ayarlamak için bu örnek Kabuk betiği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eeaa0-171">You can use this sample shell script to set those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="eeaa0-172">Ayrıca, Azure Çin veya ya da Azure kamu içinde veya Azure Almanya ile Terraform kullanıyorsanız, ortam değişkenine uygun şekilde ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need to set the environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eeaa0-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eeaa0-173">Next steps</span></span>
<span data-ttu-id="eeaa0-174">Şimdi Terraform yükledikten ve Azure aboneliğinize altyapısı dağıtma başlayabilmeniz için Azure kimlik yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="eeaa0-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="eeaa0-175">Ardından, bilgi nasıl [Terraform ile altyapı oluşturma](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="eeaa0-175">Next, learn how to [create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
