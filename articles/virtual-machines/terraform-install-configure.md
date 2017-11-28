---
title: "aaaInstall ve Azure'da Terraform tooprovision VM'ler ve diğer altyapıya yapılandırma | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Terraform toocreate Azure yapılandırma kaynakları"
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
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="30d6b-103">Yükleme ve Azure'da Terraform tooprovision VM'ler ve diğer altyapı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="30d6b-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="30d6b-104">Bu makalede hello gerekli adımları tooinstall ve Azure'da sanal makineleri gibi Terraform tooprovision kaynaklarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="30d6b-105">Nasıl toocreate ve kullanım Azure kimlik bilgilerini tooenable Terraform tooprovision bulut kaynaklarını güvenli bir şekilde öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="30d6b-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="30d6b-106">HashiCorp Terraform kolay bir yolu toodefine sağlar ve bulut altyapısı HashiCorp yapılandırma dili (HCL) adlı bir özel şablon dili kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="30d6b-107">Bu özel dil [kolay toowrite ve kolay toounderstand](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="30d6b-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="30d6b-108">Hello kullanarak ek olarak, `terraform plan` komutu, bunları yürütme önce hello değişiklikleri tooyour altyapı görsel öğe.</span><span class="sxs-lookup"><span data-stu-id="30d6b-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="30d6b-109">Azure ile Terraform kullanarak bu adımları toostart izleyin.</span><span class="sxs-lookup"><span data-stu-id="30d6b-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="30d6b-110">Terraform yükleyin</span><span class="sxs-lookup"><span data-stu-id="30d6b-110">Install Terraform</span></span>
<span data-ttu-id="30d6b-111">tooinstall Terraform, [karşıdan](https://www.terraform.io/downloads.html) hello paket işletim sisteminize ayrı yükleme dizini için uygun.</span><span class="sxs-lookup"><span data-stu-id="30d6b-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="30d6b-112">Merhaba indirme için genel bir yol da tanımlamanız gerekir bir tek bir yürütülebilir dosya içerir.</span><span class="sxs-lookup"><span data-stu-id="30d6b-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="30d6b-113">Nasıl tooset hello Linux ve Mac yolda hakkında yönergeler için gidin çok[bu Web sayfası](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="30d6b-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="30d6b-114">Nasıl tooset hello Windows yolda hakkında yönergeler için gidin çok[bu Web sayfası](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="30d6b-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="30d6b-115">tooverify hello çalıştırmak yüklemenizi `terraform` komutu.</span><span class="sxs-lookup"><span data-stu-id="30d6b-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="30d6b-116">Çıkış olarak kullanılabilir Terraform seçeneklerin bir listesini görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="30d6b-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="30d6b-117">Ardından, tooallow Terraform erişim tooyour Azure aboneliği tooperform altyapı sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="30d6b-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="30d6b-118">Terraform erişim tooAzure ayarlayın</span><span class="sxs-lookup"><span data-stu-id="30d6b-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="30d6b-119">tooenable Terraform tooprovision kaynakları Azure, Azure Active Directory'de (Azure AD) toocreate iki varlık gerekir: Azure AD uygulaması ve bir Azure AD hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="30d6b-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="30d6b-120">Ardından, Terraform komut dosyalarınızı bu varlıkları tanımlayıcılar kullanın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="30d6b-121">Bir hizmet sorumlusu genel Azure yerel örneğidir AD uygulaması.</span><span class="sxs-lookup"><span data-stu-id="30d6b-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="30d6b-122">Bir hizmet sorumlusu ayrıntılı yerel erişim denetimi tooglobal kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="30d6b-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="30d6b-123">Azure AD uygulaması ve bir Azure AD hizmet sorumlusu birkaç yolu toocreate vardır.</span><span class="sxs-lookup"><span data-stu-id="30d6b-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="30d6b-124">Merhaba kolay ve hızlı şekilde bugün toouse Azure CLI 2.0 olan hangi [indirin ve Windows, Linux veya Mac yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="30d6b-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="30d6b-125">Ayrıca, PowerShell veya Azure CLI 1.0 toocreate hello gerekli güvenlik altyapısını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="30d6b-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="30d6b-126">izleyen hello yönergeleri göstermek, nasıl tüm bu yaklaşım kullanarak Azure Terraform tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="30d6b-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="30d6b-127">Azure CLI 2.0 (Windows, Linux veya Mac kullanıcıları için) kullanın</span><span class="sxs-lookup"><span data-stu-id="30d6b-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="30d6b-128">Merhaba yükleyip sonra [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), komutu aşağıdaki hello vererek tooadminister içinde Azure aboneliğinizde oturum:</span><span class="sxs-lookup"><span data-stu-id="30d6b-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="30d6b-129">Merhaba Çin'de, Azure Almanya veya Azure kamu Bulutlar kullanırsanız, toofirst gerekir, bulut ile hello Azure CLI toowork yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="30d6b-130">Merhaba aşağıdakini çalıştırarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="30d6b-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="30d6b-131">Birden çok Azure aboneliğiniz varsa, kendi ayrıntıları hello tarafından döndürülen `az login` komutu.</span><span class="sxs-lookup"><span data-stu-id="30d6b-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="30d6b-132">Set hello `SUBSCRIPTION_ID` ortam değişkeni toohold hello hello değerini döndürdü `id` hello abonelikten alan toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="30d6b-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="30d6b-133">Bu oturum için toouse istediğiniz hello abonelik ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="30d6b-134">Merhaba hesap tooget hello abonelik kimliği sorgular ve Kiracı kimliği değerleri.</span><span class="sxs-lookup"><span data-stu-id="30d6b-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="30d6b-135">Ardından, farklı kimlik bilgileri için Terraform oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30d6b-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="30d6b-136">AppID, parola, sp_name ve Kiracı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="30d6b-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="30d6b-137">Merhaba AppID ve parolayı not edin.</span><span class="sxs-lookup"><span data-stu-id="30d6b-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="30d6b-138">tooconfirm kimlik bilgilerinizi (hizmet sorumlusu) yeni bir Kabuğu'nu açın ve hello aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="30d6b-139">Yedek hello sp_name, şifresi ve Kiracı için döndürülen:</span><span class="sxs-lookup"><span data-stu-id="30d6b-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="30d6b-140">(Windows kullanıcıları için) PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="30d6b-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="30d6b-141">toouse bir Windows makinesine toowrite ve, Terraform yürütme komut dosyaları ve yapılandırma görevleri için PowerShell toouse hello sağ PowerShell araçları ile makinenizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="30d6b-142">Merhaba adımları izleyerek PowerShell araçlarını yükleme [yükleyin ve Azure PowerShell yapılandırma](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="30d6b-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="30d6b-143">İndir ve Yürüt hello [azure setup.ps1 betik](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) hello PowerShell konsolundan.</span><span class="sxs-lookup"><span data-stu-id="30d6b-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="30d6b-144">toorun hello azure setup.ps1 komut dosyasını indirin ve hello yürütme `./azure-setup.ps1 setup` hello PowerShell konsolundan komutu.</span><span class="sxs-lookup"><span data-stu-id="30d6b-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="30d6b-145">Daha sonra oturum açma tooyour yönetici ayrıcalıklarına sahip Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="30d6b-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="30d6b-146">Bir uygulama adı (isteğe bağlı dize gerekli) sağlamanız istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="30d6b-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="30d6b-147">İsteğe bağlı olarak, istendiğinde güçlü bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="30d6b-148">Bir parola sağlamazsanız, güçlü bir parola sizin için .NET güvenlik kitaplıklarını kullanarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="30d6b-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="30d6b-149">Azure CLI 1.0 (Linux veya Mac kullanıcıları için) kullanın</span><span class="sxs-lookup"><span data-stu-id="30d6b-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="30d6b-150">tooget Terraform ile Linux makineler veya Mac bilgisayarları yükleme hello uygun kitaplıkları makinenizde Azure CLI 1.0 ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="30d6b-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="30d6b-151">Hello adımları izleyerek Azure xPlat CLI araçlarını yükleme [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="30d6b-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="30d6b-152">Karşıdan yükleyip JSON işlemci hello yönergeleri takip ederek [karşıdan jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="30d6b-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="30d6b-153">İndir ve Yürüt hello [azure setup.sh betik](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) hello konsol betikten bash.</span><span class="sxs-lookup"><span data-stu-id="30d6b-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="30d6b-154">toorun hello azure setup.sh komut dosyasını indirin ve hello yürütme `./azure-setup setup` hello konsolundan komutu.</span><span class="sxs-lookup"><span data-stu-id="30d6b-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="30d6b-155">Daha sonra oturum açma tooyour yönetici ayrıcalıklarına sahip Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="30d6b-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="30d6b-156">Bir uygulama adı (isteğe bağlı dize gerekli) sağlamanız istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="30d6b-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="30d6b-157">İsteğe bağlı olarak, istendiğinde güçlü bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="30d6b-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="30d6b-158">Bir parola sağlamazsanız, güçlü bir parola sizin için .NET güvenlik kitaplıklarını kullanarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="30d6b-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="30d6b-159">Tüm hello önceki betikler, bir Azure AD uygulaması ve hizmet sorumlusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30d6b-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="30d6b-160">Merhaba hizmet sorumlusu hello abonelikte katılımcı veya sahibi düzeyinde erişim alır.</span><span class="sxs-lookup"><span data-stu-id="30d6b-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="30d6b-161">Merhaba yüksek sağladığı erişim düzeyi nedeniyle, bu komut dosyaları tarafından oluşturulan hello güvenlik bilgileri her zaman korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="30d6b-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="30d6b-162">Bu komut dosyaları tarafından sağlanan güvenlik bilgileri tüm dört adet Not: AppID, parola, ABONELİK_KİMLİĞİ ve tenant_id.</span><span class="sxs-lookup"><span data-stu-id="30d6b-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="30d6b-163">Ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="30d6b-163">Set environment variables</span></span>
<span data-ttu-id="30d6b-164">Oluşturma ve Azure AD hizmet sorumlusu yapılandırdıktan sonra toolet gerek Terraform bilmeniz hello Kiracı kimliği, abonelik kimliği, istemci kimliği ve istemci gizli toouse.</span><span class="sxs-lookup"><span data-stu-id="30d6b-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="30d6b-165">Bu değerleri Terraform komut dosyalarınızı gömerek açıklandığı gibi bunu yapabilirsiniz [Terraform kullanarak temel altyapı oluşturma](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="30d6b-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="30d6b-166">Alternatif olarak, ortam değişkenleri aşağıdaki hello ayarlayabilir (ve dolayısıyla yanlışlıkla etme veya kimlik bilgilerinizi paylaşımı kaçının):</span><span class="sxs-lookup"><span data-stu-id="30d6b-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="30d6b-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="30d6b-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="30d6b-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="30d6b-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="30d6b-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="30d6b-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="30d6b-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="30d6b-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="30d6b-171">Bu örnek Kabuk komut dosyası tooset bu değişkenleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="30d6b-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="30d6b-172">Azure Çin veya ya da Azure kamu içinde veya Azure Almanya ile Terraform kullanıyorsanız, ayrıca, tooset hello ortam değişkeni uygun şekilde gerekir.</span><span class="sxs-lookup"><span data-stu-id="30d6b-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30d6b-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30d6b-173">Next steps</span></span>
<span data-ttu-id="30d6b-174">Şimdi Terraform yükledikten ve Azure aboneliğinize altyapısı dağıtma başlayabilmeniz için Azure kimlik yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="30d6b-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="30d6b-175">Ardından, nasıl çok öğrenin[Terraform ile altyapı oluşturma](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="30d6b-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
