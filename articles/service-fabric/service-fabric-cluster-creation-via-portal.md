---
title: "aaaCreate Service Fabric kümesi hello Azure portalı | Microsoft Docs"
description: "Bu makalede, Azure kullanarak güvenli bir Service Fabric kümesi tooset nasıl hello Azure portalı ve Azure anahtar kasası açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="be81c-103">Azure'da hello Azure portal kullanarak bir Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="be81c-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be81c-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be81c-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="be81c-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="be81c-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="be81c-106">Hello Azure portal kullanarak azure'da güvenli bir Service Fabric kümesi ayarlama hello adımlarını anlatan bir adım adım kılavuz budur.</span><span class="sxs-lookup"><span data-stu-id="be81c-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="be81c-107">Bu kılavuz, aşağıdaki adımları hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="be81c-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="be81c-108">Anahtar kasası toomanage anahtarlarını küme güvenlik ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="be81c-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="be81c-109">Güvenli bir küme Azure'da hello Azure portal oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be81c-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="be81c-110">Yöneticiler sertifikaları kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="be81c-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="be81c-111">Azure Active Directory ile kullanıcı kimlik doğrulaması ve uygulama güvenliği için sertifikalar ayarlama gibi daha gelişmiş güvenlik seçenekleri için [Azure Kaynak Yöneticisi'ni kullanarak kümenizi oluşturduktan][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="be81c-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="be81c-112">Güvenli bir küme dağıtma, yükseltme ve uygulamaları, hizmetleri ve içerdikleri hello veri silme içeren yetkisiz erişim toomanagement işlemleri engelleyen bir kümedir.</span><span class="sxs-lookup"><span data-stu-id="be81c-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="be81c-113">Güvenli olmayan bir küme herkes tooat dilediğiniz zaman bağlanmak ve böylelikle yönetim işlemlerini gerçekleştirmek bir kümedir.</span><span class="sxs-lookup"><span data-stu-id="be81c-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="be81c-114">Olası toocreate güvenli olmayan bir küme olmasına rağmen olan **güvenli küme toocreate tavsiye**.</span><span class="sxs-lookup"><span data-stu-id="be81c-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="be81c-115">Güvenli olmayan bir küme **daha sonra korunamıyor** -yeni bir küme oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be81c-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="be81c-116">Merhaba kavramları olan hello güvenli küme hello kümeleri Linux kümeleri veya Windows kümeleri oluşturmak için aynı.</span><span class="sxs-lookup"><span data-stu-id="be81c-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="be81c-117">Güvenli Linux kümeleri oluşturmak için daha fazla bilgi ve yardımcı komut dosyaları için lütfen bkz. [Linux'ta güvenli küme oluşturma](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="be81c-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="be81c-118">Merhaba hello Yardımcısı betiği tarafından sağlanan elde parametreleri hello Portalı'na doğrudan hello bölümde açıklandığı gibi girilebilir [hello Azure portal bir küme oluşturmak](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="be81c-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="be81c-119">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="be81c-119">Log in tooAzure</span></span>
<span data-ttu-id="be81c-120">Bu kılavuzu kullanır [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="be81c-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="be81c-121">Yeni bir PowerShell oturumu başlatılırken tooyour içinde Azure hesabınızı ve oturum Azure komutları çalıştırmadan önce aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="be81c-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="be81c-122">Tooyour azure hesabında oturum:</span><span class="sxs-lookup"><span data-stu-id="be81c-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="be81c-123">Aboneliğinizi seçin:</span><span class="sxs-lookup"><span data-stu-id="be81c-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="be81c-124">Anahtar Kasası ayarlama</span><span class="sxs-lookup"><span data-stu-id="be81c-124">Set up Key Vault</span></span>
<span data-ttu-id="be81c-125">Başlangıç Kılavuzu'nun bu bölümü Service Fabric uygulamaları ve Azure Service Fabric kümesi için bir anahtar kasası oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="be81c-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="be81c-126">Anahtar kasası üzerinde tam bir kılavuz için bkz: Merhaba [anahtar kasası kullanmaya başlama Kılavuzu][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="be81c-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="be81c-127">Service Fabric X.509 sertifikaları toosecure bir küme kullanır.</span><span class="sxs-lookup"><span data-stu-id="be81c-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="be81c-128">Azure anahtar kasası Azure Service Fabric kümeleri için kullanılan toomanage sertifikaları olur.</span><span class="sxs-lookup"><span data-stu-id="be81c-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="be81c-129">Bir küme Azure'da dağıtıldığında hello Azure kaynak sağlayıcısı Service Fabric kümeleri oluşturmak için sorumlu sertifikaları anahtar Kasası'nı çeker ve VM'ler hello kümede yükler.</span><span class="sxs-lookup"><span data-stu-id="be81c-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="be81c-130">Merhaba Aşağıdaki diyagramda hello anahtar kasası, Service Fabric kümesi ve küme oluşturduğunda, anahtar kasasında depolanan sertifika kullanan hello Azure kaynak sağlayıcısı arasındaki ilişki gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="be81c-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Sertifika Yükleme][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="be81c-132">Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="be81c-132">Create a Resource Group</span></span>
<span data-ttu-id="be81c-133">Merhaba ilk adımı toocreate özellikle anahtar kasası için yeni bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be81c-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="be81c-134">İşlem ve depolama kaynak grupları - gibi Service Fabric kümesi olan hello kaynak grubuna - kaldırabilmeniz anahtar kasası, kendi kaynak grubuna koyma anahtarları ve gizli anahtarları kaybetmeden önerilir.</span><span class="sxs-lookup"><span data-stu-id="be81c-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="be81c-135">Anahtar kasası olan hello kaynak grubuna hello olmalıdır tarafından kullanıldığı hello küme aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="be81c-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="be81c-136">Anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="be81c-136">Create Key Vault</span></span>
<span data-ttu-id="be81c-137">Bir anahtar kasası hello yeni kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be81c-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="be81c-138">Merhaba anahtar kasası **dağıtımı için etkinleştirilmelidir** tooallow Service Fabric kaynak sağlayıcısı tooget sertifikaları dışarı hello ve küme düğümlerine yükleyin:</span><span class="sxs-lookup"><span data-stu-id="be81c-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
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

<span data-ttu-id="be81c-139">Var olan bir anahtar kasası varsa Azure CLI kullanarak dağıtım için etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be81c-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="be81c-140">Sertifikaları tooKey kasası ekleme</span><span class="sxs-lookup"><span data-stu-id="be81c-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="be81c-141">Sertifikaları Service Fabric tooprovide kimlik doğrulama ve şifreleme toosecure içinde kullanılan bir küme ve kendi uygulamalarına çeşitli yönlerini.</span><span class="sxs-lookup"><span data-stu-id="be81c-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="be81c-142">Service Fabric sertifikaların nasıl kullanıldığını daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="be81c-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="be81c-143">Küme ve sunucu sertifikası (gerekli)</span><span class="sxs-lookup"><span data-stu-id="be81c-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="be81c-144">Bu sertifika, gerekli toosecure bir kümedir ve yetkisiz erişim tooit engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be81c-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="be81c-145">Birkaç yolla küme güvenlik sağlar:</span><span class="sxs-lookup"><span data-stu-id="be81c-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="be81c-146">**Küme kimlik doğrulaması:** düğümü düğümü iletişimin küme Federasyon kimlik doğrulamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="be81c-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="be81c-147">Yalnızca bu sertifikayla kimliğini kanıtlamak düğümleri hello kümeye katılabilir.</span><span class="sxs-lookup"><span data-stu-id="be81c-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="be81c-148">**Sunucu kimlik doğrulaması:** hello management istemcisi, toohello gerçek küme Konuşmayı bilir böylece hello küme yönetim uç noktaları tooa yönetim istemci kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="be81c-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="be81c-149">Bu sertifika de SSL hello HTTPS yönetim API'si ve Service Fabric Explorer için HTTPS üzerinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="be81c-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="be81c-150">tooserve bu amacıyla, hello sertifika hello aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="be81c-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="be81c-151">Merhaba sertifika özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="be81c-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="be81c-152">anahtar değişimi için dışarı aktarılabilir tooa kişisel bilgi değişimi (.pfx) dosyasını Hello sertifika oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be81c-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="be81c-153">Merhaba sertifikanın konu adı hello kullanılan etki alanı tooaccess hello Service Fabric kümesi eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="be81c-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="be81c-154">Merhaba kümenin HTTPS yönetim uç noktaları ve Service Fabric Explorer için gerekli tooprovide SSL budur.</span><span class="sxs-lookup"><span data-stu-id="be81c-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="be81c-155">Hello için bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor `.cloudapp.azure.com` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="be81c-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="be81c-156">Kümeniz için özel etki alanı adı satın alır.</span><span class="sxs-lookup"><span data-stu-id="be81c-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="be81c-157">İstediğinde bir CA hello sertifikanın konu adındaki bir sertifika, kümeniz için kullanılan hello özel etki alanı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="be81c-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="be81c-158">İstemci kimlik doğrulama sertifikaları</span><span class="sxs-lookup"><span data-stu-id="be81c-158">Client authentication certificates</span></span>
<span data-ttu-id="be81c-159">Ek istemci sertifikalarını Yöneticiler küme yönetim görevleri için kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="be81c-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="be81c-160">Service Fabric sahip iki erişim düzeyleri: **yönetici** ve **salt okunur kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="be81c-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="be81c-161">En azından, yönetici erişimi için tek bir sertifika kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be81c-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="be81c-162">Ek kullanıcı düzeyinde erişim için ayrı bir sertifika sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be81c-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="be81c-163">Erişim rolleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="be81c-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="be81c-164">Service Fabric ile tooupload istemci kimlik doğrulama sertifikaları tooKey kasa toowork gerekmez.</span><span class="sxs-lookup"><span data-stu-id="be81c-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="be81c-165">Bu sertifikalar yalnızca yetkili toousers küme yönetimi için sağlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="be81c-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="be81c-166">Azure Active Directory hello yolu tooauthenticate istemciler için küme yönetimi işlemleri önerilen ' dir.</span><span class="sxs-lookup"><span data-stu-id="be81c-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="be81c-167">Azure Active Directory toouse, şunları yapmalısınız [Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturmak][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="be81c-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="be81c-168">Uygulama sertifikaları (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="be81c-168">Application certificates (optional)</span></span>
<span data-ttu-id="be81c-169">Ek sertifikaların herhangi bir sayıda uygulama güvenlik amacıyla bir kümede yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="be81c-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="be81c-170">Kümenizi oluşturmadan önce hello düğümlerinde gibi yüklü bir sertifika toobe gerektiren hello güvenlik senaryolarını göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="be81c-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="be81c-171">Şifreleme ve şifre çözme uygulama yapılandırma değerleri</span><span class="sxs-lookup"><span data-stu-id="be81c-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="be81c-172">Çoğaltma sırasında düğümler arasında veri şifreleme</span><span class="sxs-lookup"><span data-stu-id="be81c-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="be81c-173">Uygulama sertifikaları hello Azure portal aracılığıyla bir küme oluştururken yapılandırılamaz.</span><span class="sxs-lookup"><span data-stu-id="be81c-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="be81c-174">Küme kurulumu zaman tooconfigure uygulama sertifikalar, şunları yapmalısınız [Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturmak][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="be81c-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="be81c-175">Oluşturulduktan sonra uygulama sertifikaları toohello küme de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be81c-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="be81c-176">Azure kaynak sağlayıcısı kullanmak için sertifikaları biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="be81c-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="be81c-177">Özel anahtar dosyaları (.pfx) eklenir ve doğrudan anahtar kasası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="be81c-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="be81c-178">Ancak, bir base-64 kodlanmış dize ve hello özel anahtar parolası olarak hello .pfx içeren özel bir JSON biçiminde depolanan anahtarları toobe hello Azure kaynak sağlayıcısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="be81c-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="be81c-179">Bu gereksinimler, anahtarları bir JSON dizesinde yerleştirilir ve olarak depolanan tooaccommodate *gizli* anahtar Kasası'nda.</span><span class="sxs-lookup"><span data-stu-id="be81c-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="be81c-180">Bu işlem daha kolay toomake PowerShell modülüdür [github'da][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="be81c-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="be81c-181">Bu adımları toouse hello modülü izleyin:</span><span class="sxs-lookup"><span data-stu-id="be81c-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="be81c-182">Merhaba depodaki tüm içeriğini Hello bir yerel dizine indirin.</span><span class="sxs-lookup"><span data-stu-id="be81c-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="be81c-183">PowerShell penceresinde Hello modülünü içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="be81c-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="be81c-184">Merhaba `Invoke-AddCertToKeyVault` bu PowerShell modülünü komutu otomatik olarak bir sertifika özel anahtarı bir JSON dizeye biçimlendirir ve tooKey kasası yükler.</span><span class="sxs-lookup"><span data-stu-id="be81c-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="be81c-185">Tooadd hello küme sertifika ve tüm ek uygulama sertifikaları tooKey kasası kullanın.</span><span class="sxs-lookup"><span data-stu-id="be81c-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="be81c-186">Kümenizdeki tooinstall istediğiniz ek sertifika için bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="be81c-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="be81c-187">Bunlar düğümü kimlik doğrulaması, yönetim uç noktası güvenlik ve kimlik doğrulama ve tüm ek uygulama güvenliği için sertifikaları yükler bir Service Fabric kümesi Resource Manager şablonu yapılandırmak için tüm hello anahtar kasası önkoşulları X.509 sertifikaları kullanan özellikler.</span><span class="sxs-lookup"><span data-stu-id="be81c-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="be81c-188">Bu noktada, Azure kurulumunda aşağıdaki hello şimdi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="be81c-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="be81c-189">Anahtar kasası kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="be81c-189">Key Vault resource group</span></span>
  * <span data-ttu-id="be81c-190">Anahtar Kasası</span><span class="sxs-lookup"><span data-stu-id="be81c-190">Key Vault</span></span>
    * <span data-ttu-id="be81c-191">Küme sunucu kimlik doğrulama sertifikası</span><span class="sxs-lookup"><span data-stu-id="be81c-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="be81c-192">< /a "oluşturma-küme-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="be81c-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="be81c-193">Hello Azure portal kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="be81c-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="be81c-194">Service Fabric küme kaynağı Hello için arama</span><span class="sxs-lookup"><span data-stu-id="be81c-194">Search for hello Service Fabric cluster resource</span></span>
![Service Fabric kümesi hello Azure portal şablona arayın.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="be81c-196">İçinde toohello oturum [Azure portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="be81c-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="be81c-197">Tıklatın **yeni** tooadd yeni bir kaynak şablonu.</span><span class="sxs-lookup"><span data-stu-id="be81c-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="be81c-198">Arama hello hello Service Fabric kümesi şablonunun **Market** altında **her şeyi**.</span><span class="sxs-lookup"><span data-stu-id="be81c-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="be81c-199">Seçin **Service Fabric kümesi** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="be81c-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="be81c-200">Toohello gidin **Service Fabric kümesi** dikey penceresinde tıklatın **oluşturma**,</span><span class="sxs-lookup"><span data-stu-id="be81c-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="be81c-201">Merhaba **oluşturma Service Fabric kümesi** dikey penceresinde hello aşağıdaki dört adımları vardır.</span><span class="sxs-lookup"><span data-stu-id="be81c-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="be81c-202">1. Temel Bilgiler</span><span class="sxs-lookup"><span data-stu-id="be81c-202">1. Basics</span></span>
![Yeni bir kaynak grubu oluşturma ekran görüntüsü.][CreateRG]

<span data-ttu-id="be81c-204">Merhaba temel bilgileri dikey penceresinde, kümeniz için tooprovide hello temel ayrıntıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="be81c-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="be81c-205">Merhaba, kümenin adını girin.</span><span class="sxs-lookup"><span data-stu-id="be81c-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="be81c-206">Girin bir **kullanıcı adı** ve **parola** hello VM'ler için Uzak Masaüstü.</span><span class="sxs-lookup"><span data-stu-id="be81c-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="be81c-207">Tooselect hello emin olun **abonelik** özellikle birden çok aboneliğiniz varsa, dağıtılmış, küme toobe istiyor.</span><span class="sxs-lookup"><span data-stu-id="be81c-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="be81c-208">Oluşturma bir **yeni kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="be81c-208">Create a **new resource group**.</span></span> <span data-ttu-id="be81c-209">Bunu hello hello küme adıyla aynı özellikle toomake değişiklikleri tooyour dağıtım çalıştığınız veya kümenizi sildiğinizden bunları daha sonra bulma yardımcı olan bu yana en iyi toogive olur.</span><span class="sxs-lookup"><span data-stu-id="be81c-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="be81c-210">Varolan bir kaynak grubu toouse karar verebilirsiniz rağmen iyi bir uygulama toocreate yeni bir kaynak grubu var.</span><span class="sxs-lookup"><span data-stu-id="be81c-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="be81c-211">Bu işlem, ihtiyacınız olmayan kolay toodelete kümeleri kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="be81c-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="be81c-212">Select hello **bölge** toocreate hello küme istiyor.</span><span class="sxs-lookup"><span data-stu-id="be81c-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="be81c-213">Anahtarınızı kasa aynı bölgede yer hello kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be81c-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="be81c-214">2. Küme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="be81c-214">2. Cluster configuration</span></span>
![Düğüm türü oluşturma][CreateNodeType]

<span data-ttu-id="be81c-216">Küme düğümlerinizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="be81c-216">Configure your cluster nodes.</span></span> <span data-ttu-id="be81c-217">Düğüm türleri hello VM boyutları, VM'ler hello sayısını ve bunların özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be81c-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="be81c-218">Kümenizi birden fazla olabilir düğüm türü, ancak hello birincil düğüm türü (Merhaba hello portalında tanımlayan birinci) olması gerekir en az beş VM'ler, bu Service Fabric Sistem Hizmetleri yerleştirildiği hello düğüm türü olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="be81c-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="be81c-219">Yapılandırmayın **yerleşim özellikleri** çünkü "nodetypename"adlı bir varsayılan yerleştirme özelliği otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="be81c-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="be81c-220">Yaygın bir senaryo birden çok düğüm türü için bir ön uç hizmeti ve arka uç hizmeti içeren bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="be81c-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="be81c-221">Tooput hello ön uç hizmeti bağlantı noktalarını açık toohello Internet küçük sanal makineleri (örneğin, D2 VM boyutları) üzerinde istediğiniz, ancak isterseniz tooput hello arka uç hizmetine (ile VM boyutları D4, D6, D15 vb. gibi) daha büyük sanal makineleri üzerinde hiçbir İnternete bağlantı açık.</span><span class="sxs-lookup"><span data-stu-id="be81c-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="be81c-222">Düğüm türünüz (1 too12 karakterler yalnızca harfler ve sayılar içeren) için bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="be81c-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="be81c-223">Hello minimum **boyutu** VM'lerin hello birincil düğüm türü hello tarafından yönetilir **dayanıklılık** katmanı hello küme için seçin.</span><span class="sxs-lookup"><span data-stu-id="be81c-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="be81c-224">Merhaba hello dayanıklılık katmanı için Bronz varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="be81c-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="be81c-225">Dayanıklılık hakkında daha fazla bilgi için bkz: [nasıl toochoose hello Service Fabric kümesi güvenilirlik ve dayanıklılık][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="be81c-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="be81c-226">Merhaba VM boyutu ve fiyatlandırma katmanı seçin.</span><span class="sxs-lookup"><span data-stu-id="be81c-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="be81c-227">D-serisi VM'ler SSD sürücülerine sahip ve durum bilgisi olan uygulamalar için tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="be81c-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="be81c-228">Kısmi çekirdeğe sahip tüm VM SKU kullanın veya değil 7 GB kullanılabilir disk kapasiteleri daha az sahip.</span><span class="sxs-lookup"><span data-stu-id="be81c-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="be81c-229">Merhaba minimum **numarası** VM'lerin hello birincil düğüm türü hello tarafından yönetilir **güvenilirlik** seçtiğiniz katmanı.</span><span class="sxs-lookup"><span data-stu-id="be81c-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="be81c-230">Merhaba hello güvenilirlik katmanı için Gümüş varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="be81c-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="be81c-231">Güvenilirliği hakkında daha fazla bilgi için bkz: [nasıl toochoose hello Service Fabric kümesi güvenilirlik ve dayanıklılık][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="be81c-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="be81c-232">Merhaba hello düğüm türü için VM sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="be81c-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="be81c-233">Yukarı veya aşağı hello sayısında VM'ler düğüm türü daha sonra ölçeklendirebilirsiniz ancak hello birincil düğüm türüne hello minimum seçmiş olduğunuz hello güvenilirlik düzeyi tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="be81c-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="be81c-234">Diğer düğüm türleri, en az 1 VM olabilir.</span><span class="sxs-lookup"><span data-stu-id="be81c-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="be81c-235">Özel uç noktaları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="be81c-235">Configure custom endpoints.</span></span> <span data-ttu-id="be81c-236">Bu alan tooenter tooexpose hello Azure yük dengeleyici toohello aracılığıyla istediğiniz bağlantı noktalarının virgülle ayrılmış bir liste sağlar, uygulamalarınız için genel Internet.</span><span class="sxs-lookup"><span data-stu-id="be81c-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="be81c-237">Bir web uygulaması tooyour küme toodeploy düşünüyorsanız, örneğin, "80" Buraya girdiğiniz bağlantı noktası 80, kümesine tooallow trafiğine.</span><span class="sxs-lookup"><span data-stu-id="be81c-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="be81c-238">Uç noktalar hakkında daha fazla bilgi için bkz: [uygulamaları ile iletişim][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="be81c-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="be81c-239">Küme yapılandırma **tanılama**.</span><span class="sxs-lookup"><span data-stu-id="be81c-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="be81c-240">Varsayılan olarak, tanılama sorunlarını giderme ile küme tooassist üzerinde etkindir.</span><span class="sxs-lookup"><span data-stu-id="be81c-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="be81c-241">Toodisable tanılama hello değiştirmek istiyorsanız **durum** çok geçiş**devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="be81c-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="be81c-242">Tanılama kapatma olan **değil** önerilir.</span><span class="sxs-lookup"><span data-stu-id="be81c-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="be81c-243">Hello doku yükseltme kümesi istediğiniz modu seçin.</span><span class="sxs-lookup"><span data-stu-id="be81c-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="be81c-244">Seçin **otomatik**, hello sistem tooautomatically çekme hello en son sürüme yedeklemek istiyorsanız ve küme tooit tooupgrade deneyin.</span><span class="sxs-lookup"><span data-stu-id="be81c-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="be81c-245">Başlangıç modu çok ayarlamak**el ile**toochoose desteklenen bir sürüm istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="be81c-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="be81c-246">Service Fabric desteklenen sürümlerini çalıştıran kümeler destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="be81c-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="be81c-247">Merhaba seçerek **el ile** modu yapmakta hello sorumluluk tooupgrade üzerinde Küme desteklenen tooa sürümü.</span><span class="sxs-lookup"><span data-stu-id="be81c-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="be81c-248">Merhaba hello doku yükseltme modu hakkında daha fazla ayrıntı görmek için [service fabric Küme yükseltme belge.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="be81c-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="be81c-249">3. Güvenlik</span><span class="sxs-lookup"><span data-stu-id="be81c-249">3. Security</span></span>
![Azure Portal'da güvenlik yapılandırmalarını ekran görüntüsü.][SecurityConfigs]

<span data-ttu-id="be81c-251">Merhaba son adım hello anahtar kasası ve bilgileri daha önce oluşturduğunuz sertifika kullanarak tooprovide sertifika bilgileri toosecure hello kümedir.</span><span class="sxs-lookup"><span data-stu-id="be81c-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="be81c-252">Merhaba karşıya elde hello çıktıyla Hello birincil sertifikası alanları doldurmak **küme sertifika** tooKey kasası kullanılarak hello `Invoke-AddCertToKeyVault` PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="be81c-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="be81c-253">Merhaba denetleyin **Gelişmiş ayarları Yapılandır** tooenter istemci sertifikalarını kutusunda **yönetici istemci** ve **salt okunur istemci**.</span><span class="sxs-lookup"><span data-stu-id="be81c-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="be81c-254">Bu alanlarda yönetici istemci sertifikanızın parmak izi hello ve salt okunur kullanıcının istemci sertifikanızın hello parmak izi varsa girin.</span><span class="sxs-lookup"><span data-stu-id="be81c-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="be81c-255">Yöneticiler tooconnect toohello küme denediğinizde, yalnızca hello parmak izi değerleri eşleşen bir parmak izine sahip bir sertifika varsa erişim buraya girilen verilir.</span><span class="sxs-lookup"><span data-stu-id="be81c-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="be81c-256">4. Özet</span><span class="sxs-lookup"><span data-stu-id="be81c-256">4. Summary</span></span>
![<span data-ttu-id="be81c-257">"Dağıtma Service Fabric kümesi" görüntüleme hello başlangıç panosunun ekran görüntüsü</span><span class="sxs-lookup"><span data-stu-id="be81c-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="be81c-258">toocomplete hello küme oluşturma, tıklatın **Özet** sağlamış ya da indirme toosee hello yapılandırmaları Merhaba, kümenizi toodeploy kullanılan Azure Resource Manager şablonu.</span><span class="sxs-lookup"><span data-stu-id="be81c-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="be81c-259">Merhaba zorunlu ayarları girdikten sonra hello **Tamam** düğmesi yeşil olur ve tıklayarak hello küme oluşturma işlemi başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be81c-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="be81c-260">Merhaba oluşturma ilerlemesi hello Bildirimlerde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be81c-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="be81c-261">(Hello durum çubuğu, ekranınızın sağ üst hello en yakın hello "zil" simgesine tıklayın.) Tıkladıysanız **PIN tooStartboard** göreceğiniz hello küme oluştururken **Service Fabric kümesi dağıtma** toohello sabitlenmiş **Başlat** Panosu.</span><span class="sxs-lookup"><span data-stu-id="be81c-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="be81c-262">Küme durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="be81c-262">View your cluster status</span></span>
![Küme ayrıntıları hello panosunda ekran görüntüsü.][ClusterDashboard]

<span data-ttu-id="be81c-264">Kümenizi oluşturduktan sonra kümenizi hello portalında inceleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be81c-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="be81c-265">Çok Git**Gözat** tıklatıp **Service Fabric kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="be81c-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="be81c-266">Kümenizi bulun ve tıklatın.</span><span class="sxs-lookup"><span data-stu-id="be81c-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="be81c-267">Şimdi kümenizi hello kümenin ortak uç noktası ve bağlantı tooService Fabric Explorer dahil olmak üzere hello panosundaki hello ayrıntılarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be81c-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="be81c-268">Merhaba **düğümü İzleyici** hello kümenin Pano dikey bölümde sağlıklı ve iyi olan VM'ler hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be81c-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="be81c-269">Hello kümenin durumu hakkında daha fazla ayrıntı bulabilirsiniz [Service Fabric sistem durumu modeli giriş][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="be81c-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="be81c-270">Service Fabric kümeleri durumunu - "çekirdek Bakımı" başvurulan tooas korumak ve belirli bir sayıda düğüm toobe her zaman toomaintain kullanılabilirliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="be81c-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="be81c-271">Therfore, değil genellikle hello kümedeki tüm makineler aşağı güvenli tooshut ilk yapmadığınız sürece bir [tam yedekleme, durumu][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="be81c-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="be81c-272">Uzaktan bağlantı tooa sanal makine ölçek kümesi örneği veya bir küme düğümü</span><span class="sxs-lookup"><span data-stu-id="be81c-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="be81c-273">Her hello NodeTypes, küme sonuçlarınızda ayarı alınırken bir sanal makine ölçek kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="be81c-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="be81c-274">Bkz: [uzaktan bağlanma tooa sanal makine ölçek kümesi örnek] [ remote-connect-to-a-vm-scale-set] Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="be81c-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be81c-275">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be81c-275">Next steps</span></span>
<span data-ttu-id="be81c-276">Bu noktada, yönetim kimlik doğrulaması için sertifikaları kullanarak güvenli bir küme var.</span><span class="sxs-lookup"><span data-stu-id="be81c-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="be81c-277">Ardından, [tooyour kümesine bağlanın](service-fabric-connect-to-secure-cluster.md) ve nasıl çok öğrenin[uygulama parolaları yönetme](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="be81c-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="be81c-278">Ayrıca, öğrenin [Service Fabric destek seçenekleri](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="be81c-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
