---
title: "aaaCreate Azure Service Fabric kümesi bir şablondan | Microsoft Docs"
description: "Bu makalede nasıl güvenli bir Service Fabric yukarı tooset küme Azure'da Azure Resource Manager, Azure anahtar kasası ve Azure Active Directory (Azure AD) istemci kimlik doğrulaması için kullanarak açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="71907-103">Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="71907-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71907-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71907-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="71907-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="71907-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="71907-106">Bu adım adım kılavuz, Azure Kaynak Yöneticisi'ni kullanarak azure'da güvenli bir Azure Service Fabric kümesi ayarlama aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="71907-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="71907-107">Merhaba makaleyi uzun bildiremedi.</span><span class="sxs-lookup"><span data-stu-id="71907-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="71907-108">Bununla birlikte, hello içerikle baştan sona bilginiz sürece her adım dikkatle emin toofollow olması.</span><span class="sxs-lookup"><span data-stu-id="71907-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="71907-109">Merhaba kılavuz yordamları izleyerek hello kapsar:</span><span class="sxs-lookup"><span data-stu-id="71907-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="71907-110">Küme ve uygulama güvenliği için bir Azure anahtar kasası tooupload sertifikalar ayarlama</span><span class="sxs-lookup"><span data-stu-id="71907-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="71907-111">Azure Resource Manager kullanarak Azure'da güvenli küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="71907-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="71907-112">Kullanıcıların Azure Active Directory (Azure AD) kullanarak küme yönetimi için kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="71907-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="71907-113">Güvenli bir küme yetkisiz erişim toomanagement işlemleri engelleyen bir kümedir.</span><span class="sxs-lookup"><span data-stu-id="71907-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="71907-114">Bu, dağıtma, yükseltme ve silme uygulamaları, hizmetleri ve içerdikleri hello verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="71907-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="71907-115">Güvenli olmayan bir küme herkes tooat dilediğiniz zaman bağlanmak ve böylelikle yönetim işlemlerini gerçekleştirmek bir kümedir.</span><span class="sxs-lookup"><span data-stu-id="71907-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="71907-116">Olası toocreate güvenli olmayan bir küme olmasına rağmen hello outset güvenli bir küme oluşturmak önerilir.</span><span class="sxs-lookup"><span data-stu-id="71907-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="71907-117">Güvenli olmayan bir küme daha sonra korunamıyor olduğundan, yeni bir küme oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="71907-118">oluşturulurken güvenli küme Hello kavramı olan hello aynı, Linux veya Windows kümesi olup.</span><span class="sxs-lookup"><span data-stu-id="71907-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="71907-119">Güvenli Linux kümeleri oluşturmak için daha fazla bilgi ve yardımcı komut dosyası için bkz: [Linux'ta güvenli küme oluşturma](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="71907-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="71907-120">Azure hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="71907-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="71907-121">Bu kılavuzu kullanır [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="71907-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="71907-122">Yeni bir PowerShell oturumu başlattığınızda tooyour Azure hesabı oturum ve Azure komutları çalıştırmadan önce aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="71907-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="71907-123">Azure hesabı tooyour oturum:</span><span class="sxs-lookup"><span data-stu-id="71907-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="71907-124">Aboneliğinizi seçin:</span><span class="sxs-lookup"><span data-stu-id="71907-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="71907-125">Bir anahtar kasasını oluşturup</span><span class="sxs-lookup"><span data-stu-id="71907-125">Set up a key vault</span></span>
<span data-ttu-id="71907-126">Bu bölümde, Service Fabric uygulamaları ve Azure Service Fabric kümesi için bir anahtar kasası oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="71907-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="71907-127">Tam Kılavuzu tooAzure anahtar kasası, toohello başvuran [anahtar kasası kullanmaya başlama Kılavuzu][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="71907-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="71907-128">Service Fabric X.509 sertifikaları toosecure bir küme kullanır ve uygulama güvenlik özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="71907-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="71907-129">Azure Service Fabric kümeleri için anahtar kasası toomanage sertifikaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="71907-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="71907-130">Bir küme Azure'da dağıtıldığında, Service Fabric kümeleri oluşturmaktan sorumlu hello Azure kaynak sağlayıcısı sertifikaları anahtar Kasası'nı çeker ve VM'ler hello kümede yükler.</span><span class="sxs-lookup"><span data-stu-id="71907-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="71907-131">Merhaba Aşağıdaki diyagramda hello Azure anahtar kasası, Service Fabric kümesi ve küme oluşturduğunda, bir anahtar kasasında depolanan sertifika kullanan hello Azure kaynak sağlayıcısı arasındaki ilişki gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="71907-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Sertifika Yükleme diyagramı][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="71907-133">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="71907-133">Create a resource group</span></span>
<span data-ttu-id="71907-134">Merhaba ilk adımı toocreate özellikle anahtar kasanız için bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="71907-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="71907-135">Kendi kaynak grubuna hello anahtar kasası koymak öneririz.</span><span class="sxs-lookup"><span data-stu-id="71907-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="71907-136">Bu eylem, Service Fabric kümesi anahtarları ve gizli anahtarları kaybetmeden içeren hello kaynak grubunu da dahil olmak üzere hello işlem ve depolama kaynak grupları, kaldırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="71907-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="71907-137">anahtar kasanızı içeren hello kaynak grubunu _hello olmalıdır aynı bölgede_ tarafından kullanıldığı hello kümesi olarak.</span><span class="sxs-lookup"><span data-stu-id="71907-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="71907-138">Birden çok bölgeye toodeploy kümelerde planlıyorsanız, hello kaynak grubu ve ait hangi bölgede gösterir şekilde hello anahtar kasası adı öneririz.</span><span class="sxs-lookup"><span data-stu-id="71907-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="71907-139">Merhaba çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="71907-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="71907-140">Merhaba yeni kaynak grubunda bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="71907-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="71907-141">Merhaba anahtar kasası _dağıtımı için etkinleştirilmelidir_ tooallow işlem kaynak sağlayıcısı tooget sertifikaları dışarı hello ve sanal makine örnekleri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="71907-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="71907-142">Merhaba çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="71907-142">hello output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="71907-143">Var olan bir anahtar kasası kullanın</span><span class="sxs-lookup"><span data-stu-id="71907-143">Use an existing key vault</span></span>

<span data-ttu-id="71907-144">toouse var olan bir anahtar kasası, _dağıtımı için etkinleştirmeniz gerekir_ tooallow işlem kaynak sağlayıcısı tooget sertifikaları dışarı hello ve küme düğümlerine yükleyin:</span><span class="sxs-lookup"><span data-stu-id="71907-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="71907-145">Sertifikaları tooyour anahtar kasası ekleme</span><span class="sxs-lookup"><span data-stu-id="71907-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="71907-146">Sertifikaları Service Fabric tooprovide kimlik doğrulama ve şifreleme toosecure içinde kullanılan bir küme ve kendi uygulamalarına çeşitli yönlerini.</span><span class="sxs-lookup"><span data-stu-id="71907-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="71907-147">Service Fabric sertifikaların nasıl kullanıldığını daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="71907-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="71907-148">Küme ve sunucu sertifikası (gerekli)</span><span class="sxs-lookup"><span data-stu-id="71907-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="71907-149">Bu sertifika, gerekli toosecure bir kümedir ve yetkisiz erişim tooit engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71907-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="71907-150">İki yolla küme güvenlik sağlar:</span><span class="sxs-lookup"><span data-stu-id="71907-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="71907-151">Küme kimlik doğrulaması: düğümü düğümü iletişimin küme Federasyon kimlik doğrulamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="71907-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="71907-152">Yalnızca bu sertifikayla kimliğini kanıtlamak düğümleri hello kümeye katılabilir.</span><span class="sxs-lookup"><span data-stu-id="71907-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="71907-153">Sunucu kimlik doğrulaması: hello management istemcisi, toohello gerçek küme Konuşmayı bilir böylece hello küme yönetim uç noktaları tooa yönetim istemci kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="71907-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="71907-154">Bu sertifika aynı zamanda bir SSL hello HTTPS yönetim API'si ve Service Fabric Explorer için HTTPS üzerinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="71907-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="71907-155">tooserve bu amacıyla, hello sertifika hello aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="71907-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="71907-156">Merhaba sertifika özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="71907-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="71907-157">Merhaba sertifika verilebilir tooa kişisel bilgi değişimi (.pfx) dosyası olan anahtar değişimi için oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="71907-158">Merhaba sertifikanın konu adı tooaccess hello Service Fabric kümesi kullanın hello etki alanı eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="71907-159">Bu eşleştirme, gerekli tooprovide hello kümenin HTTPS yönetim uç noktaları için bir SSL ve Service Fabric Explorer değildir.</span><span class="sxs-lookup"><span data-stu-id="71907-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="71907-160">Hello için bir sertifika yetkilisinden (CA) bir SSL sertifikası alınamıyor. cloudapp.azure.com etki alanı.</span><span class="sxs-lookup"><span data-stu-id="71907-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="71907-161">Özel etki alanı adı, kümeniz için edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="71907-162">Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, kümeniz için kullandığınız hello özel etki alanı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="71907-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="71907-163">Uygulama sertifikaları (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="71907-163">Application certificates (optional)</span></span>
<span data-ttu-id="71907-164">Ek sertifikaların herhangi bir sayıda uygulama güvenlik amacıyla bir kümede yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="71907-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="71907-165">Kümenizi oluşturmadan önce hello düğümlerinde gibi yüklü bir sertifika toobe gerektiren hello güvenlik senaryolarını göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="71907-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="71907-166">Şifreleme ve şifre çözme uygulama yapılandırma değerlerini.</span><span class="sxs-lookup"><span data-stu-id="71907-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="71907-167">Çoğaltma sırasında şifreleme düğümler arasında veri.</span><span class="sxs-lookup"><span data-stu-id="71907-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="71907-168">Azure kaynak sağlayıcısı kullanmak için sertifikaları biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="71907-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="71907-169">Ekleme ve özel anahtar dosyaları (.pfx) doğrudan aracılığıyla anahtar kasanızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="71907-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="71907-170">Ancak, özel bir JavaScript nesne gösterimi (JSON) biçiminde depolanan anahtarları toobe hello Azure işlem kaynak sağlayıcısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="71907-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="71907-171">Merhaba biçiminde hello .pfx dosyası olarak bir base 64 kodlu bir dize ve hello özel anahtar parolası içerir.</span><span class="sxs-lookup"><span data-stu-id="71907-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="71907-172">Bu gereksinimler, anahtarları bir JSON dizesinde yerleştirilir ve başlangıç anahtarı "gizli" olarak depolanan hello tooaccommodate Kasa.</span><span class="sxs-lookup"><span data-stu-id="71907-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="71907-173">Bu işlem daha kolay toomake bir [PowerShell modülüdür Github'da bulunan][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="71907-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="71907-174">toouse hello Modülü aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="71907-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="71907-175">Merhaba depodaki tüm içeriğini Hello bir yerel dizine indirin.</span><span class="sxs-lookup"><span data-stu-id="71907-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="71907-176">Toohello yerel dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="71907-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="71907-177">PowerShell penceresinde Hello ServiceFabricRPHelpers modülünü içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="71907-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="71907-178">Merhaba `Invoke-AddCertToKeyVault` bu PowerShell modülünü komutu otomatik olarak bir sertifika özel anahtarı bir JSON dizeye biçimlendirir ve toohello anahtar kasası yükler.</span><span class="sxs-lookup"><span data-stu-id="71907-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="71907-179">Merhaba komutu tooadd hello küme sertifika ve tüm ek uygulama sertifikaları toohello anahtar kasası kullanın.</span><span class="sxs-lookup"><span data-stu-id="71907-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="71907-180">Kümenizdeki tooinstall istediğiniz ek sertifika için bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="71907-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="71907-181">Varolan bir sertifikayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="71907-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="71907-182">Merhaba bir burada gösterildiği gibi bir hata alırsanız, genellikle kaynak URL çakışması olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="71907-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="71907-183">tooresolve hello çakışması, değişiklik hello anahtar kasasının adı.</span><span class="sxs-lookup"><span data-stu-id="71907-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="71907-184">Merhaba çakışması çözümlendikten sonra hello çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="71907-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="71907-185">Uygulama güvenliği için kullanıyor olabilecek herhangi bir uygulama sertifika hello üç önceki dizeleri CertificateThumbprint, SourceVault ve CertificateURL, güvenli Service Fabric kümesi ve tooobtain tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="71907-186">Merhaba dizeleri kaydetmezseniz, daha sonra bunları hello anahtar sorgulamak kasa zor tooretrieve olabilir.</span><span class="sxs-lookup"><span data-stu-id="71907-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="71907-187">Otomatik olarak imzalanan sertifika oluşturma ve toohello anahtar kasası karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="71907-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="71907-188">Sertifikaları toohello anahtar kasanız zaten karşıya yüklediyseniz, bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="71907-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="71907-189">Bu adım, yeni bir otomatik olarak imzalanan sertifika oluşturma ve tooyour anahtar kasası karşıya içindir.</span><span class="sxs-lookup"><span data-stu-id="71907-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="71907-190">Komut dosyası izleyen hello hello parametreleri değiştirin ve ardından çalıştırdıktan sonra sertifika parola sorulur.</span><span class="sxs-lookup"><span data-stu-id="71907-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="71907-191">Merhaba bir burada gösterildiği gibi bir hata alırsanız, genellikle kaynak URL çakışması olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="71907-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="71907-192">tooresolve hello çakışma, değişiklik hello anahtar kasası adı, RG adı ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="71907-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="71907-193">Merhaba çakışması çözümlendikten sonra hello çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="71907-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="71907-194">Uygulama güvenliği için kullanıyor olabilecek herhangi bir uygulama sertifika hello üç önceki dizeleri CertificateThumbprint, SourceVault ve CertificateURL, güvenli Service Fabric kümesi ve tooobtain tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="71907-195">Merhaba dizeleri kaydetmezseniz, daha sonra bunları hello anahtar sorgulamak kasa zor tooretrieve olabilir.</span><span class="sxs-lookup"><span data-stu-id="71907-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="71907-196">Bu noktada, yerinde öğeleri aşağıdaki hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="71907-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="71907-197">Merhaba anahtar kasası kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="71907-197">hello key vault resource group.</span></span>
* <span data-ttu-id="71907-198">anahtar kasası ve URL'sini (PowerShell çıkış önceki hello SourceVault olarak adlandırılır) hello.</span><span class="sxs-lookup"><span data-stu-id="71907-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="71907-199">Merhaba küme sunucu kimlik doğrulama sertifikası ve URL'sini hello anahtar Kasası'nda.</span><span class="sxs-lookup"><span data-stu-id="71907-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="71907-200">Merhaba uygulama sertifikaları ve bunların URL'lerini hello anahtar Kasası'nda.</span><span class="sxs-lookup"><span data-stu-id="71907-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="71907-201">İstemci kimlik doğrulaması için Azure Active Directory'yi ayarlama ayarlayın</span><span class="sxs-lookup"><span data-stu-id="71907-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="71907-202">Azure AD kuruluş (kiracılar olarak bilinir) toomanage kullanıcı erişimi tooapplications sağlar.</span><span class="sxs-lookup"><span data-stu-id="71907-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="71907-203">Uygulamaları web tabanlı olanlar oturum açma kullanıcı Arabirimi ve yerel istemci deneyimini olanlar ayrılır.</span><span class="sxs-lookup"><span data-stu-id="71907-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="71907-204">Bu makalede, bir kiracı zaten oluşturduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="71907-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="71907-205">Yüklemediyseniz, okuyarak başlamanız [nasıl tooget bir Azure Active Directory Kiracı][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="71907-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="71907-206">Service Fabric kümesi birkaç giriş noktaları tooits hello web tabanlı dahil olmak üzere Yönetim işlevselliği sunar [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] ve [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="71907-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="71907-207">Sonuç olarak, iki Azure AD uygulamaları toocontrol erişim toohello kümesi, bir web uygulaması ve bir yerel uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71907-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="71907-208">Azure AD ile bir Service Fabric kümesi yapılandırılırken bazı hello adımlarını söz konusu toosimplify, Windows PowerShell komut kümesini oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="71907-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="71907-209">Merhaba hello küme oluşturmadan önce aşağıdaki adımları tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="71907-210">Küme adları ve uç noktaları Hello betikleri beklediğiniz çünkü hello değerler planlanması gerekir ve, önceden oluşturduğunuz değerleri değil.</span><span class="sxs-lookup"><span data-stu-id="71907-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="71907-211">[Merhaba komut dosyalarını indirme] [ sf-aad-ps-script-download] tooyour bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="71907-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="71907-212">Sağ hello zip dosyası, select **özellikleri**seçin hello **Engellemeyi Kaldır** onay kutusunu işaretleyin ve ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="71907-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="71907-213">Merhaba zip dosyasını ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="71907-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="71907-214">Çalıştırma `SetupApplications.ps1`ve hello Tenantıd, ClusterName ve WebApplicationReplyUrl parametre olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="71907-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="71907-215">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="71907-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="71907-216">Merhaba PowerShell komutunu yürüterek, Tenantıd bulabilirsiniz `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="71907-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="71907-217">Bu komutu yürütmek hello Tenantıd her abonelik için görüntüler.</span><span class="sxs-lookup"><span data-stu-id="71907-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="71907-218">ClusterName hello komut dosyası tarafından oluşturulan kullanılan tooprefix hello Azure AD uygulamaları ' dir.</span><span class="sxs-lookup"><span data-stu-id="71907-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="71907-219">Bunun toomatch hello gerçek küme adı tam olarak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="71907-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="71907-220">Hedeflenen yalnızca toomake olduğundan, bunlar ile kullanılan daha kolay toomap Azure AD yapıları toohello Service Fabric kümesi.</span><span class="sxs-lookup"><span data-stu-id="71907-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="71907-221">WebApplicationReplyUrl oturum açma işlemini tamamladıktan sonra tooyour kullanıcıları Azure AD döndüren hello varsayılan uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="71907-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="71907-222">Bu uç nokta olan varsayılan olarak, kümeniz için hello Service Fabric Explorer bitiş noktası olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="71907-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="71907-223">https://&lt;cluster_domain&gt;: 19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="71907-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="71907-224">İstendiğinde toosign tooan hesabındaki hello Azure AD kiracısı için yönetici ayrıcalıklarına sahip olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="71907-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="71907-225">Oturum açtıktan sonra hello betiği hello web ve yerel uygulamalar toorepresent Service Fabric kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="71907-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="71907-226">Merhaba hello kiracının uygulamaları gözden geçirmeniz [Klasik Azure portalı][azure-classic-portal], iki yeni giriş görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="71907-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="71907-227">*ClusterName*\_küme</span><span class="sxs-lookup"><span data-stu-id="71907-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="71907-228">*ClusterName*\_istemci</span><span class="sxs-lookup"><span data-stu-id="71907-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="71907-229">Merhaba betik bir fikir tookeep hello PowerShell penceresi olacak şekilde hello sonraki bölümde hello Küme oluşturduğunuzda hello Azure Resource Manager şablonu için gerekli JSON açmak hello yazdırır.</span><span class="sxs-lookup"><span data-stu-id="71907-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="71907-230">Service Fabric kümesi Resource Manager şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="71907-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="71907-231">Bu bölümde, hello Merhaba önceki bir Service Fabric kümesi Resource Manager şablonunda kullanılan PowerShell komutları çıkarır.</span><span class="sxs-lookup"><span data-stu-id="71907-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="71907-232">Örnek Resource Manager şablonları hello kullanılabilir [github'da Azure hızlı başlangıç Şablon Galerisi][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="71907-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="71907-233">Bu şablonlar, küme şablonunuz için bir başlangıç noktası olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="71907-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="71907-234">Merhaba Resource Manager şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="71907-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="71907-235">Bu kılavuzu hello kullanır [5-node güvenli küme] [ service-fabric-secure-cluster-5-node-1-nodetype] örnek şablonu ve şablon parametreleri.</span><span class="sxs-lookup"><span data-stu-id="71907-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="71907-236">Karşıdan `azuredeploy.json` ve `azuredeploy.parameters.json` tooyour bilgisayar ve her iki dosyalarını sık kullandığınız metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="71907-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="71907-237">Sertifikaları Ekle</span><span class="sxs-lookup"><span data-stu-id="71907-237">Add certificates</span></span>
<span data-ttu-id="71907-238">Merhaba sertifika anahtarları içeren anahtar kasası hello başvurarak sertifikaları tooa küme Resource Manager şablonu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="71907-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="71907-239">Bir Resource Manager şablonu parametreleri dosyasında hello anahtar kasası değerleri koyun öneririz.</span><span class="sxs-lookup"><span data-stu-id="71907-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="71907-240">Bunun yapılması hello Resource Manager şablon dosyası yeniden kullanılabilir ve boş değerler belirli tooa dağıtımının tutar.</span><span class="sxs-lookup"><span data-stu-id="71907-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="71907-241">OsProfile tüm sertifikaları toohello sanal makine ölçek kümesi ekleme</span><span class="sxs-lookup"><span data-stu-id="71907-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="71907-242">Merhaba kümede yüklü her sertifikanın hello osProfile bölümünde hello ölçek kümesi kaynağı (Microsoft.Compute/virtualMachineScaleSets) yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="71907-243">Bu eylemin hello kaynak sağlayıcısı tooinstall hello sertifika hello VM'ler bildirir.</span><span class="sxs-lookup"><span data-stu-id="71907-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="71907-244">Bu yükleme hello küme sertifika ve herhangi bir uygulama güvenlik sertifika toouse uygulamalarınız için planlama içerir:</span><span class="sxs-lookup"><span data-stu-id="71907-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="71907-245">Merhaba Service Fabric kümesi sertifika yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71907-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="71907-246">Merhaba küme kimlik doğrulama sertifikası her iki hello Service Fabric küme kaynağı (Microsoft.ServiceFabric/clusters) olarak yapılandırılmalıdır ve hello sanal makine ölçek için Service Fabric uzantısı hello sanal makine ölçek kümesi kaynağı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="71907-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="71907-247">Bu düzenlemenin hello Service Fabric kaynak sağlayıcısı tooconfigure sağlar, küme kimlik doğrulaması ve yönetim uç noktaları için sunucu kimlik doğrulaması için kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="71907-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="71907-248">Kaynak sanal makine ölçek kümesi:</span><span class="sxs-lookup"><span data-stu-id="71907-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="71907-249">Service Fabric kaynak:</span><span class="sxs-lookup"><span data-stu-id="71907-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="71907-250">Azure AD Yapılandırması Ekle</span><span class="sxs-lookup"><span data-stu-id="71907-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="71907-251">daha önce oluşturduğunuz hello Azure AD yapılandırma doğrudan Resource Manager şablonuna eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="71907-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="71907-252">Ancak, önce bir parametre dosyası tookeep hello Resource Manager şablonu yeniden kullanılabilir hello değerleri ayıklamak ve değerleri belirli tooa dağıtımını boş önerilir.</span><span class="sxs-lookup"><span data-stu-id="71907-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="71907-253">< bir "yapılandırma-arm" ></a>yapılandırma Resource Manager şablonu parametreleri</span><span class="sxs-lookup"><span data-stu-id="71907-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="71907-254">Son olarak, hello çıkış değerler hello anahtar kasası ve Azure AD PowerShell komutları toopopulate hello parametreler dosyası kullanın:</span><span class="sxs-lookup"><span data-stu-id="71907-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="71907-255">Bu noktada, yerinde öğeleri aşağıdaki hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="71907-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="71907-256">Anahtar kasası kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="71907-256">Key vault resource group</span></span>
  * <span data-ttu-id="71907-257">Key Vault</span><span class="sxs-lookup"><span data-stu-id="71907-257">Key vault</span></span>
  * <span data-ttu-id="71907-258">Küme sunucu kimlik doğrulama sertifikası</span><span class="sxs-lookup"><span data-stu-id="71907-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="71907-259">Veri şifreleme sertifikası</span><span class="sxs-lookup"><span data-stu-id="71907-259">Data encipherment certificate</span></span>
* <span data-ttu-id="71907-260">Azure Active Directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="71907-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="71907-261">Web tabanlı yönetim ve Service Fabric Explorer için Azure AD uygulaması</span><span class="sxs-lookup"><span data-stu-id="71907-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="71907-262">Yerel istemci yönetimi için Azure AD uygulaması</span><span class="sxs-lookup"><span data-stu-id="71907-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="71907-263">Kullanıcılar ve onların atanan roller</span><span class="sxs-lookup"><span data-stu-id="71907-263">Users and their assigned roles</span></span>
* <span data-ttu-id="71907-264">Service Fabric kümesi Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="71907-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="71907-265">Anahtar kasası ile yapılandırılan sertifikaları</span><span class="sxs-lookup"><span data-stu-id="71907-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="71907-266">Yapılandırılmış Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71907-266">Azure Active Directory configured</span></span>

<span data-ttu-id="71907-267">Aşağıdaki diyagramda hello anahtar kasası ve Azure AD yapılandırma Resource Manager şablonunuza nerelerde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="71907-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Resource Manager bağımlılık Haritası][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="71907-269">Merhaba kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="71907-269">Create hello cluster</span></span>
<span data-ttu-id="71907-270">Şimdi kullanarak hazır toocreate hello küme olan [Azure kaynak şablon dağıtımı][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="71907-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="71907-271">test</span><span class="sxs-lookup"><span data-stu-id="71907-271">Test it</span></span>
<span data-ttu-id="71907-272">PowerShell komut tootest aşağıdaki hello Resource Manager şablonu ile bir parametre dosyası kullanın:</span><span class="sxs-lookup"><span data-stu-id="71907-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="71907-273">dağıtın</span><span class="sxs-lookup"><span data-stu-id="71907-273">Deploy it</span></span>
<span data-ttu-id="71907-274">Hello Resource Manager şablonu testi başarılı olursa, aşağıdaki PowerShell komut toodeploy hello Resource Manager şablonu ile bir parametre dosyası kullanın:</span><span class="sxs-lookup"><span data-stu-id="71907-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="71907-275">Kullanıcıların tooroles atayın</span><span class="sxs-lookup"><span data-stu-id="71907-275">Assign users tooroles</span></span>
<span data-ttu-id="71907-276">Merhaba uygulamaları toorepresent kümenizi oluşturduktan sonra kullanıcılarınızın Service Fabric tarafından desteklenen toohello rolleri ata: salt okunur ve yönetici Hello kullanarak hello roller atayabilirsiniz [Klasik Azure portalı][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="71907-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="71907-277">Hello Azure portal, tooyour Kiracı gidin ve ardından **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="71907-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="71907-278">Bir ada sahip hello web uygulaması seçin gibi `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="71907-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="71907-279">Merhaba tıklatın **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="71907-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="71907-280">Bir kullanıcı tooassign seçin ve hello ardından **atamak** hello ekranın hello düğmesini.</span><span class="sxs-lookup"><span data-stu-id="71907-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Kullanıcıların tooroles düğmesi atama][assign-users-to-roles-button]
5. <span data-ttu-id="71907-282">Merhaba rol tooassign toohello kullanıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="71907-282">Select hello role tooassign toohello user.</span></span>

    !["Kullanıcılar atama" iletişim kutusu][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="71907-284">Service Fabric rolleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="71907-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="71907-285">Linux'ta güvenli küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="71907-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="71907-286">toomake hello işlemini daha kolay, biz olması koşuluyla bir [yardımcı betik](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="71907-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="71907-287">Bu yardımcı betik kullanmadan önce Azure komut satırı yüklü arabirimi (CLI) zaten var ve yolunuzda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="71907-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="71907-288">Merhaba komut dosyası çalıştırarak izinleri tooexecute olduğundan emin olun `chmod +x cert_helper.py` karşıdan sonra.</span><span class="sxs-lookup"><span data-stu-id="71907-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="71907-289">Merhaba ilk adımdır tooyour Azure hesabı toosign ile Merhaba CLI kullanarak `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="71907-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="71907-290">Tooyour Azure hesabı oturum sonra hello yardımcı komut dosyası kullan CA'nız ile komut gösterir aşağıdaki hello sertifika, oturum:</span><span class="sxs-lookup"><span data-stu-id="71907-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="71907-291">Merhaba - ifile parametresi hello sertifika türü (pfx veya pem ya da kendinden imzalı bir sertifika varsa ss) ile giriş olarak bir .pfx dosyasına ya da .pem dosyasını alabilir.</span><span class="sxs-lookup"><span data-stu-id="71907-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="71907-292">Merhaba parametre -h hello Yardım metni yazdırır.</span><span class="sxs-lookup"><span data-stu-id="71907-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="71907-293">Bu komut, üç dizeleri hello çıkış olarak aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="71907-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="71907-294">Merhaba hello kimliği SourceVaultID yeni KeyVault sizin için oluşturulan kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="71907-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="71907-295">Merhaba sertifika erişmek için CertificateUrl</span><span class="sxs-lookup"><span data-stu-id="71907-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="71907-296">Kimlik doğrulaması için kullanılan CertificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="71907-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="71907-297">Aşağıdaki örnek hello nasıl toouse hello komutu gösterir:</span><span class="sxs-lookup"><span data-stu-id="71907-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="71907-298">Üç dizeler gibi hello komut verir önceki hello yürütülüyor:</span><span class="sxs-lookup"><span data-stu-id="71907-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="71907-299">Merhaba sertifikanın konu adı tooaccess hello Service Fabric kümesi kullanın hello etki alanı eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="71907-300">Gerekli tooprovide hello kümenin HTTPS yönetim uç noktaları için bir SSL ve Service Fabric Explorer eşleşmedir.</span><span class="sxs-lookup"><span data-stu-id="71907-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="71907-301">Hello için bir CA'dan bir SSL sertifikası elde edemiyor `.cloudapp.azure.com` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="71907-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="71907-302">Özel etki alanı adı, kümeniz için edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="71907-303">Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, kümeniz için kullandığınız hello özel etki alanı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="71907-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="71907-304">Bu konu adları toocreate (olmadan Azure AD), güvenli bir Service Fabric kümesi ihtiyacınız hello konusunda açıklandığı gibi girişler [yapılandırma Resource Manager şablonu parametreleri](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="71907-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="71907-305">Merhaba yönergeleri izleyerek toohello güvenli küme bağlanabilir [istemci erişim tooa küme kimlik doğrulaması](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="71907-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="71907-306">Linux Önizleme kümeleri, Azure AD kimlik doğrulamasını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="71907-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="71907-307">Hello açıklandığı gibi yönetici ve istemci roller atayabilirsiniz [atamak rolleri toousers](#assign-roles) bölümü.</span><span class="sxs-lookup"><span data-stu-id="71907-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="71907-308">Linux Önizleme küme için yönetici ve istemci rolleri belirlemek için kimlik doğrulaması için tooprovide sertifika parmak izleri vardır.</span><span class="sxs-lookup"><span data-stu-id="71907-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="71907-309">(Hiçbir zincir doğrulama veya iptal Bu önizleme sürümünde gerçekleştirilmekte olduğundan, hello konu adı, sağlamaz.)</span><span class="sxs-lookup"><span data-stu-id="71907-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="71907-310">Test etmek için toouse otomatik olarak imzalanan bir sertifika istiyorsanız kullanabileceğiniz hello aynı komut dosyasını toogenerate biri.</span><span class="sxs-lookup"><span data-stu-id="71907-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="71907-311">Merhaba bayrağı sağlayarak hello sertifika tooyour anahtar kasası sonra yükleyebilirsiniz `ss` sağlayan hello sertifika yolu ve sertifika adı yerine.</span><span class="sxs-lookup"><span data-stu-id="71907-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="71907-312">Örneğin, oluşturma ve otomatik olarak imzalanan bir sertifika karşıya yükleme için komutu aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="71907-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="71907-313">Bu komut döndürür hello aynı üç dizeleri: SourceVault, CertificateUrl ve CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="71907-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="71907-314">Merhaba dizeleri toocreate daha sonra güvenli bir Linux kümesi ve hello otomatik olarak imzalanan sertifika yerleştirildiği konum da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71907-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="71907-315">Merhaba otomatik olarak imzalanan sertifika tooconnect toohello küme gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="71907-316">Merhaba yönergeleri izleyerek toohello güvenli küme bağlanabilir [istemci erişim tooa küme kimlik doğrulaması](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="71907-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="71907-317">Merhaba sertifikanın konu adı tooaccess hello Service Fabric kümesi kullanın hello etki alanı eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="71907-318">Gerekli tooprovide hello kümenin HTTPS yönetim uç noktaları için bir SSL ve Service Fabric Explorer eşleşmedir.</span><span class="sxs-lookup"><span data-stu-id="71907-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="71907-319">Hello için bir CA'dan bir SSL sertifikası elde edemiyor `.cloudapp.azure.com` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="71907-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="71907-320">Özel etki alanı adı, kümeniz için edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71907-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="71907-321">Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, kümeniz için kullandığınız hello özel etki alanı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="71907-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="71907-322">Hello açıklandığı gibi hello Yardımcısı hello Azure portal, kodda hello parametrelerinden doldurabilir [hello Azure portal bir küme oluşturmak](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) bölümü.</span><span class="sxs-lookup"><span data-stu-id="71907-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71907-323">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="71907-323">Next steps</span></span>
<span data-ttu-id="71907-324">Bu noktada, Azure Active Directory sağlayan yönetim kimlik doğrulama ile güvenli bir küme var.</span><span class="sxs-lookup"><span data-stu-id="71907-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="71907-325">Ardından, [tooyour kümesine bağlanın](service-fabric-connect-to-secure-cluster.md) ve nasıl çok öğrenin[uygulama parolaları yönetme](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="71907-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="71907-326">İstemci kimlik doğrulaması için Azure Active Directory ayarlayan sorun giderme</span><span class="sxs-lookup"><span data-stu-id="71907-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="71907-327">İstemci kimlik doğrulaması için Azure AD ayarlarken bir sorunu yaşayıp çalıştırırsanız, bu bölümdeki hello olası çözümleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="71907-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="71907-328">Service Fabric Explorer sertifika tooselect ister</span><span class="sxs-lookup"><span data-stu-id="71907-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="71907-329">Sorun</span><span class="sxs-lookup"><span data-stu-id="71907-329">Problem</span></span>
<span data-ttu-id="71907-330">Oturum açma başarılı bir şekilde tooAzure AD Service Fabric Explorer'da sonra hello tarayıcı toohello giriş sayfasını döndürür ancak bir sertifika tooselect isteyen bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="71907-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![SFX select sertifika iletişim kutusu][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="71907-332">Neden</span><span class="sxs-lookup"><span data-stu-id="71907-332">Reason</span></span>
<span data-ttu-id="71907-333">Merhaba kullanıcı hello Azure AD küme uygulaması bir rolü atanmamış.</span><span class="sxs-lookup"><span data-stu-id="71907-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="71907-334">Bu nedenle, Service Fabric kümesi üzerinde Azure AD kimlik doğrulaması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="71907-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="71907-335">Service Fabric Explorer toocertificate kimlik doğrulama geri döner.</span><span class="sxs-lookup"><span data-stu-id="71907-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="71907-336">Çözüm</span><span class="sxs-lookup"><span data-stu-id="71907-336">Solution</span></span>
<span data-ttu-id="71907-337">Azure AD ayarlamak için hello yönergeleri izleyin ve kullanıcı rolleri atayın.</span><span class="sxs-lookup"><span data-stu-id="71907-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="71907-338">Ayrıca, "Kullanıcı atama gerekli tooaccess uygulamayı üzerinde" Aç olarak öneririz `SetupApplications.ps1` yapar.</span><span class="sxs-lookup"><span data-stu-id="71907-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="71907-339">PowerShell ile bağlantı bir hata ile başarısız olur: "Merhaba belirtilen kimlik bilgileri geçersiz"</span><span class="sxs-lookup"><span data-stu-id="71907-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="71907-340">Sorun</span><span class="sxs-lookup"><span data-stu-id="71907-340">Problem</span></span>
<span data-ttu-id="71907-341">PowerShell tooconnect toohello küme başarıyla tooAzure AD ' oturumu sonra "AzureActiveDirectory" güvenlik modunu kullanarak kullandığınızda, hello bağlantı bir hata ile başarısız olur: "Merhaba belirtilen kimlik bilgileri geçersiz."</span><span class="sxs-lookup"><span data-stu-id="71907-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="71907-342">Çözüm</span><span class="sxs-lookup"><span data-stu-id="71907-342">Solution</span></span>
<span data-ttu-id="71907-343">Aynı şekilde bir önceki hello hello çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="71907-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="71907-344">Service Fabric Explorer oturum açarken bir hata döndürür: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="71907-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="71907-345">Sorun</span><span class="sxs-lookup"><span data-stu-id="71907-345">Problem</span></span>
<span data-ttu-id="71907-346">Service Fabric Explorer'da tooAzure AD toosign çalıştığınızda hata hello sayfasını döndürür: "AADSTS50011: Merhaba yanıt adresi &lt;url&gt; hello uygulama için yapılandırılan hello yanıt adresleri eşleşmiyor: &lt;GUID&gt;."</span><span class="sxs-lookup"><span data-stu-id="71907-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![SFX yanıt adresi eşleşmiyor][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="71907-348">Neden</span><span class="sxs-lookup"><span data-stu-id="71907-348">Reason</span></span>
<span data-ttu-id="71907-349">Azure ad tooauthenticate hello küme (web) Service Fabric Explorer temsil eden bir uygulama çalışır ve isteğe bağlı olarak hello isteğin bir parçası hello yeniden yönlendirme dönüş URL'SİYLE sağlar.</span><span class="sxs-lookup"><span data-stu-id="71907-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="71907-350">Ancak hello URL hello Azure AD uygulama listelenmemiş **yanıt URL'si** listesi.</span><span class="sxs-lookup"><span data-stu-id="71907-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="71907-351">Çözüm</span><span class="sxs-lookup"><span data-stu-id="71907-351">Solution</span></span>
<span data-ttu-id="71907-352">Merhaba üzerinde **yapılandırma** hello sekmesinde küme (web) uygulaması, hello Service Fabric Explorer URL toohello ekleme **yanıt URL'si** listelemek veya hello listesinde hello öğelerden birini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="71907-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="71907-353">İşiniz bittiğinde, değişikliğinizi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="71907-353">When you have finished, save your change.</span></span>

![Web uygulaması yanıtı URL'si][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="71907-355">PowerShell aracılığıyla Azure AD kimlik doğrulaması kullanarak Hello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="71907-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="71907-356">tooconnect hello Service Fabric kümesi, aşağıdaki PowerShell komut örneğine hello kullan:</span><span class="sxs-lookup"><span data-stu-id="71907-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="71907-357">toolearn hello Connect-ServiceFabricCluster cmdlet'i hakkında bkz [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="71907-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="71907-358">Birden çok küme hello aynı Azure AD kiracısında yeniden kullanabilir?</span><span class="sxs-lookup"><span data-stu-id="71907-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="71907-359">Evet.</span><span class="sxs-lookup"><span data-stu-id="71907-359">Yes.</span></span> <span data-ttu-id="71907-360">Ancak tooadd Merhaba Service Fabric Explorer URL tooyour küme (web) uygulaması unutmayın.</span><span class="sxs-lookup"><span data-stu-id="71907-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="71907-361">Aksi takdirde, Service Fabric Explorer işe yaramaz.</span><span class="sxs-lookup"><span data-stu-id="71907-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="71907-362">Azure AD etkinken neden hala bir sunucu sertifikası ihtiyacım var mı?</span><span class="sxs-lookup"><span data-stu-id="71907-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="71907-363">FabricClient ve FabricGateway karşılıklı kimlik doğrulaması gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="71907-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="71907-364">Azure AD kimlik doğrulaması sırasında bir istemci kimlik toohello sunucusunu Azure AD tümleştirme sağlar ve hello sunucu sertifikasıdır kullanılan tooverify hello sunucu kimliği.</span><span class="sxs-lookup"><span data-stu-id="71907-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="71907-365">Service Fabric sertifikalar hakkında daha fazla bilgi için bkz: [X.509 sertifikalarını ve Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="71907-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

