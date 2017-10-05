---
title: "Azure portalında Service Fabric kümesi oluştur | Microsoft Docs"
description: "Bu makalede, Azure anahtar kasası ve Azure portal kullanarak azure'da güvenli bir Service Fabric kümesi ayarlayın açıklar."
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
ms.openlocfilehash: 7dda9520ce3d93bf0e86bd2481ad06c268d087c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="d96fd-103">Azure portal kullanarak Azure'da bir Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="d96fd-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d96fd-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d96fd-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="d96fd-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="d96fd-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="d96fd-106">Azure portal kullanarak azure'da güvenli bir Service Fabric kümesi ayarlama adımlarını anlatan bir adım adım kılavuz budur.</span><span class="sxs-lookup"><span data-stu-id="d96fd-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="d96fd-107">Bu kılavuz aşağıdaki adımlarda size yol gösterir:</span><span class="sxs-lookup"><span data-stu-id="d96fd-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="d96fd-108">Küme güvenlik anahtarını yönetmek için anahtar kasasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d96fd-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="d96fd-109">Azure portalı üzerinden güvenli bir küme oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d96fd-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="d96fd-110">Yöneticiler sertifikaları kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="d96fd-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="d96fd-111">Azure Active Directory ile kullanıcı kimlik doğrulaması ve uygulama güvenliği için sertifikalar ayarlama gibi daha gelişmiş güvenlik seçenekleri için [Azure Kaynak Yöneticisi'ni kullanarak kümenizi oluşturduktan][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="d96fd-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="d96fd-112">Güvenli bir küme dağıtma, yükseltme ve uygulamaları, hizmetleri ve içerdikleri veriler silme içeren yönetim işlemleri için yetkisiz erişimi engelleyen bir kümedir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="d96fd-113">Güvenli olmayan bir küme herkes herhangi bir zamanda bağlanmak ve böylelikle yönetim işlemleri bir kümedir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="d96fd-114">Güvenli olmayan bir küme oluşturmak mümkün olsa da, olan **güvenli bir küme oluşturmak için tavsiye**.</span><span class="sxs-lookup"><span data-stu-id="d96fd-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="d96fd-115">Güvenli olmayan bir küme **daha sonra korunamıyor** -yeni bir küme oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="d96fd-116">Kümeleri Linux kümeleri veya Windows kümeleri olup kavramları güvenli kümeleri oluşturmak için aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="d96fd-117">Güvenli Linux kümeleri oluşturmak için daha fazla bilgi ve yardımcı komut dosyaları için lütfen bkz. [Linux'ta güvenli küme oluşturma](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="d96fd-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="d96fd-118">Sağlanan yardımcı komut dosyası tarafından alınan parametreleri doğrudan portalda bölümde açıklandığı gibi girilebilir [Azure portalında bir küme oluşturmak](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="d96fd-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="d96fd-119">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="d96fd-119">Log in to Azure</span></span>
<span data-ttu-id="d96fd-120">Bu kılavuzu kullanır [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="d96fd-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="d96fd-121">Yeni bir PowerShell oturumu başlatılırken Azure hesabınızda oturum açın ve Azure komutları çalıştırmadan önce aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="d96fd-122">Azure hesabınızda oturum açın:</span><span class="sxs-lookup"><span data-stu-id="d96fd-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d96fd-123">Aboneliğinizi seçin:</span><span class="sxs-lookup"><span data-stu-id="d96fd-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="d96fd-124">Anahtar Kasası ayarlama</span><span class="sxs-lookup"><span data-stu-id="d96fd-124">Set up Key Vault</span></span>
<span data-ttu-id="d96fd-125">Kılavuzun bu bölümü Service Fabric uygulamaları ve Azure Service Fabric kümesi için bir anahtar kasası oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="d96fd-126">Anahtar kasası üzerinde tam bir kılavuz için bkz: [anahtar kasası kullanmaya başlama Kılavuzu][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="d96fd-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="d96fd-127">Service Fabric X.509 sertifikaları bir küme güvenliğini sağlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="d96fd-128">Azure anahtar kasası, Azure Service Fabric kümeleri sertifikalarını yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="d96fd-129">Bir küme Azure'da dağıtıldığında, Azure kaynak sağlayıcısı Service Fabric kümeleri oluşturmak için sorumlu sertifikaları anahtar Kasası'nı çeker ve VM'ler kümede yükler.</span><span class="sxs-lookup"><span data-stu-id="d96fd-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="d96fd-130">Aşağıdaki diyagramda, anahtar kasası, Service Fabric kümesi ve küme oluşturduğunda, anahtar kasasında depolanan sertifika kullanan Azure kaynak sağlayıcısı arasındaki ilişki gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d96fd-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Sertifika Yükleme][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="d96fd-132">Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d96fd-132">Create a Resource Group</span></span>
<span data-ttu-id="d96fd-133">İlk adım, özellikle anahtar kasası için yeni bir kaynak grubu oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="d96fd-134">Anahtarları ve gizli anahtarları kaybetmeden işlem ve depolama kaynak grupları - gibi Service Fabric kümesi sahip olan kaynak grubunu - kaldırabilmeniz anahtar kasası, kendi kaynak grubuna koyma önerilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="d96fd-135">Anahtar kasası sahip bir kaynak grubu tarafından kullanıldığı kümesi ile aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="d96fd-136">Anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="d96fd-136">Create Key Vault</span></span>
<span data-ttu-id="d96fd-137">Bir anahtar kasası yeni kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d96fd-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="d96fd-138">Anahtar kasası **dağıtımı için etkinleştirilmelidir** sertifikaları elde ve küme düğümlerine yüklemek Service Fabric kaynak sağlayıcısı izin vermek için:</span><span class="sxs-lookup"><span data-stu-id="d96fd-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

<span data-ttu-id="d96fd-139">Var olan bir anahtar kasası varsa Azure CLI kullanarak dağıtım için etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d96fd-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="d96fd-140">Anahtar Kasası'na sertifikaları Ekle</span><span class="sxs-lookup"><span data-stu-id="d96fd-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="d96fd-141">Sertifikalar, Service Fabric’te bir küme ile uygulamalarının çeşitli yönlerini güvenli hale getirmek üzere kimlik doğrulaması ve şifreleme sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="d96fd-142">Service Fabric sertifikaların nasıl kullanıldığını daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="d96fd-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="d96fd-143">Küme ve sunucu sertifikası (gerekli)</span><span class="sxs-lookup"><span data-stu-id="d96fd-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="d96fd-144">Bu sertifika, bir küme güvenli ve yetkisiz erişimi önlemek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="d96fd-145">Birkaç yolla küme güvenlik sağlar:</span><span class="sxs-lookup"><span data-stu-id="d96fd-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="d96fd-146">**Küme kimlik doğrulaması:** düğümü düğümü iletişimin küme Federasyon kimlik doğrulamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="d96fd-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="d96fd-147">Yalnızca bu sertifikayla kimliğini kanıtlamak düğümleri kümeye katılmasını sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="d96fd-148">**Sunucu kimlik doğrulaması:** management istemcisi, gerçek kümeye Konuşmayı bilir böylece bir yönetim istemcisi küme yönetim Uç noktalara kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="d96fd-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="d96fd-149">Bu sertifika de SSL HTTPS yönetim API'si ve Service Fabric Explorer için HTTPS üzerinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="d96fd-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="d96fd-150">Bu amaca hizmet eder için sertifikanın aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="d96fd-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="d96fd-151">Sertifika bir özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="d96fd-152">Sertifikanın bir kişisel bilgi değişimi (.pfx) dosyasına dışarı aktarılabilir olarak, anahtar değişimi için oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="d96fd-153">Sertifikanın konu adı, Service Fabric kümesi erişmek için kullanılan etki alanı eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="d96fd-154">Bu, kümenin HTTPS yönetim uç noktaları ve Service Fabric Explorer için SSL sağlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="d96fd-155">İçin bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor `.cloudapp.azure.com` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="d96fd-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="d96fd-156">Kümeniz için özel etki alanı adı satın alır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="d96fd-157">CA'dan bir sertifika istediğinde sertifikanın konu adı, kümeniz için kullanılan özel etki alanı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="d96fd-158">İstemci kimlik doğrulama sertifikaları</span><span class="sxs-lookup"><span data-stu-id="d96fd-158">Client authentication certificates</span></span>
<span data-ttu-id="d96fd-159">Ek istemci sertifikalarını Yöneticiler küme yönetim görevleri için kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="d96fd-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="d96fd-160">Service Fabric sahip iki erişim düzeyleri: **yönetici** ve **salt okunur kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="d96fd-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="d96fd-161">En azından, yönetici erişimi için tek bir sertifika kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="d96fd-162">Ek kullanıcı düzeyinde erişim için ayrı bir sertifika sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="d96fd-163">Erişim rolleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="d96fd-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="d96fd-164">Anahtar kasası ile Service Fabric çalışma istemci kimlik doğrulama sertifikaları yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d96fd-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="d96fd-165">Bu sertifikalar, yalnızca yetkili kullanıcılar için küme yönetimi için sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="d96fd-166">Azure Active Directory, küme yönetimi işlemleri için istemcilerin kimliğini doğrulamak için önerilen yoldur.</span><span class="sxs-lookup"><span data-stu-id="d96fd-166">Azure Active Directory is the recommended way to authenticate clients for cluster management operations.</span></span> <span data-ttu-id="d96fd-167">Azure Active Directory'yi kullanmak için size gereken [Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturmak][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="d96fd-167">To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="d96fd-168">Uygulama sertifikaları (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="d96fd-168">Application certificates (optional)</span></span>
<span data-ttu-id="d96fd-169">Ek sertifikaların herhangi bir sayıda uygulama güvenlik amacıyla bir kümede yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="d96fd-170">Kümenizi oluşturmadan önce düğümlerine gibi yüklenmesi için bir sertifika gerektiren uygulama güvenlik senaryoları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d96fd-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="d96fd-171">Şifreleme ve şifre çözme uygulama yapılandırma değerleri</span><span class="sxs-lookup"><span data-stu-id="d96fd-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="d96fd-172">Çoğaltma sırasında düğümler arasında veri şifreleme</span><span class="sxs-lookup"><span data-stu-id="d96fd-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="d96fd-173">Uygulama sertifikaları Azure Portalı aracılığıyla bir küme oluştururken yapılandırılamaz.</span><span class="sxs-lookup"><span data-stu-id="d96fd-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="d96fd-174">Küme Kurulum sırasında uygulama sertifikaları yapılandırmak için şunları yapmalısınız [Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturmak][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="d96fd-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="d96fd-175">Oluşturulduktan sonra uygulama sertifikaları kümeye ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d96fd-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="d96fd-176">Azure kaynak sağlayıcısı kullanmak için sertifikaları biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="d96fd-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="d96fd-177">Özel anahtar dosyaları (.pfx) eklenir ve doğrudan anahtar kasası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="d96fd-178">Ancak, Azure kaynak sağlayıcısı anahtarlarının base-64 olarak .pfx içeren özel bir JSON biçiminde depolanmasını gerektirir kodlanmış dize ve özel anahtar parolası.</span><span class="sxs-lookup"><span data-stu-id="d96fd-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="d96fd-179">Bu gereksinimleri karşılamak için anahtarları bir JSON dizesinde yerleştirilir ve gerekir olarak depolanan *gizli* anahtar Kasası'nda.</span><span class="sxs-lookup"><span data-stu-id="d96fd-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="d96fd-180">Bu işlemi kolaylaştırmak için bir PowerShell modülüdür [github'da][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="d96fd-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="d96fd-181">Modülü kullanmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d96fd-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="d96fd-182">Depodaki tüm içeriğini bir yerel dizine indirin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="d96fd-183">PowerShell penceresinde modülünü içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="d96fd-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="d96fd-184">`Invoke-AddCertToKeyVault` Bu PowerShell modülünü komutu otomatik olarak bir sertifika özel anahtarı bir JSON dizeye biçimlendirir ve anahtar Kasası'na yükler.</span><span class="sxs-lookup"><span data-stu-id="d96fd-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="d96fd-185">Küme sertifikası ve herhangi bir ek uygulama sertifika anahtar Kasası'na eklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d96fd-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="d96fd-186">Kümenizdeki yüklemek istediğiniz ek sertifika için bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="d96fd-187">Bu düğümü kimlik doğrulaması, yönetim uç noktası güvenlik ve kimlik doğrulaması için sertifikaları yükler bir Service Fabric kümesi Resource Manager şablonu ve X.509 sertifikalarını kullanan ek uygulama güvenliği özellikleri yapılandırmak için tüm anahtar kasası önkoşullar bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="d96fd-188">Bu noktada, Azure'da şimdi aşağıdaki Kurulumu olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d96fd-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="d96fd-189">Anahtar kasası kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="d96fd-189">Key Vault resource group</span></span>
  * <span data-ttu-id="d96fd-190">Anahtar Kasası</span><span class="sxs-lookup"><span data-stu-id="d96fd-190">Key Vault</span></span>
    * <span data-ttu-id="d96fd-191">Küme sunucu kimlik doğrulama sertifikası</span><span class="sxs-lookup"><span data-stu-id="d96fd-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="d96fd-192">< /a "oluşturma-küme-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="d96fd-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="d96fd-193">Azure portalında küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="d96fd-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="d96fd-194">Service Fabric küme kaynağı için arama</span><span class="sxs-lookup"><span data-stu-id="d96fd-194">Search for the Service Fabric cluster resource</span></span>
![Service Fabric kümesi şablonu Azure portalında arayın.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="d96fd-196">[Azure portalında][azure-portal] oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d96fd-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="d96fd-197">Tıklatın **yeni** yeni bir kaynak şablonu eklemek için.</span><span class="sxs-lookup"><span data-stu-id="d96fd-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="d96fd-198">Service Fabric kümesi şablon için arama **Market** altında **her şeyi**.</span><span class="sxs-lookup"><span data-stu-id="d96fd-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="d96fd-199">Seçin **Service Fabric kümesi** listeden.</span><span class="sxs-lookup"><span data-stu-id="d96fd-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="d96fd-200">Gidin **Service Fabric kümesi** dikey penceresinde tıklatın **oluşturma**,</span><span class="sxs-lookup"><span data-stu-id="d96fd-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="d96fd-201">**Oluşturma Service Fabric kümesi** dikey penceresinde aşağıdaki dört adım vardır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="d96fd-202">1. Temel Bilgiler</span><span class="sxs-lookup"><span data-stu-id="d96fd-202">1. Basics</span></span>
![Yeni bir kaynak grubu oluşturma ekran görüntüsü.][CreateRG]

<span data-ttu-id="d96fd-204">Temel bilgiler dikey penceresinde, kümeniz için temel ayrıntıları sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="d96fd-205">Kümenizin adını girin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="d96fd-206">Girin bir **kullanıcı adı** ve **parola** VM'ler için Uzak Masaüstü için.</span><span class="sxs-lookup"><span data-stu-id="d96fd-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="d96fd-207">Seçtiğinizden emin olun **abonelik** özellikle birden çok aboneliğiniz varsa, dağıtılacak şekilde kümenizi istiyor.</span><span class="sxs-lookup"><span data-stu-id="d96fd-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="d96fd-208">Oluşturma bir **yeni kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="d96fd-208">Create a **new resource group**.</span></span> <span data-ttu-id="d96fd-209">Özellikle, dağıtımınız için değişiklik veya kümenizi sildiğinizden çalışırken bunları daha sonra bulma yardımcı olduğundan küme aynı adı vermek en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d96fd-210">Varolan bir kaynak grubu kullanacak şekilde karar verebilirsiniz rağmen yeni bir kaynak grubu oluşturmak için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-210">Although you can decide to use an existing resource group, it is a good practice to create a new resource group.</span></span> <span data-ttu-id="d96fd-211">Bu, ihtiyacınız olmayan kümeleri silmek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-211">This makes it easy to delete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="d96fd-212">Seçin **bölge** küme oluşturmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="d96fd-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="d96fd-213">Anahtar kasası bulunduğu aynı bölgede kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="d96fd-214">2. Küme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="d96fd-214">2. Cluster configuration</span></span>
![Düğüm türü oluşturma][CreateNodeType]

<span data-ttu-id="d96fd-216">Küme düğümlerinizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d96fd-216">Configure your cluster nodes.</span></span> <span data-ttu-id="d96fd-217">Düğüm türleri, VM boyutlarını, VM'lerin sayısını ve bunların özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d96fd-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="d96fd-218">Kümenizi birden fazla düğüm türüne sahip olabilir ancak bu düğüm tipi Service Fabric Sistem Hizmetleri yerleştirildiği olarak birincil düğüm türü (portalda tanımladığınız ilk bir) en az beş VM'ler olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="d96fd-219">Yapılandırmayın **yerleşim özellikleri** çünkü "nodetypename"adlı bir varsayılan yerleştirme özelliği otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="d96fd-220">Yaygın bir senaryo birden çok düğüm türü için bir ön uç hizmeti ve arka uç hizmeti içeren bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="d96fd-221">Ön uç hizmeti bağlantı noktalarını açık daha küçük sanal makineleri (örneğin, D2 VM boyutları) Internet'e yerleştirmek istediğiniz, ancak Internet'e yönelik bağlantı noktalarının açık olan (ile VM boyutları D4, D6, D15 vb. gibi) daha büyük VM'ler arka uç hizmetine yerleştirmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="d96fd-221">You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="d96fd-222">Düğüm türünüz (1-12 karakter yalnızca harfler ve sayılar içeren) için bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="d96fd-223">En düşük **boyutu** VM'lerin birincil düğüm türü tarafından yönetilir **dayanıklılık** katmanı küme için seçin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="d96fd-224">Bronz dayanıklılık katmanı için varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="d96fd-225">Dayanıklılık hakkında daha fazla bilgi için bkz: [Service Fabric kümesi güvenilirlik ve dayanıklılık seçme][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="d96fd-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="d96fd-226">VM boyutu ve fiyatlandırma katmanı seçin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="d96fd-227">D-serisi VM'ler SSD sürücülerine sahip ve durum bilgisi olan uygulamalar için tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="d96fd-228">Kısmi çekirdeğe sahip tüm VM SKU kullanın veya değil 7 GB kullanılabilir disk kapasiteleri daha az sahip.</span><span class="sxs-lookup"><span data-stu-id="d96fd-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="d96fd-229">En düşük **numarası** VM'lerin birincil düğüm türü tarafından yönetilir **güvenilirlik** seçtiğiniz katmanı.</span><span class="sxs-lookup"><span data-stu-id="d96fd-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="d96fd-230">Güvenilirlik katmanı için Gümüş varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="d96fd-231">Güvenilirliği hakkında daha fazla bilgi için bkz: [Service Fabric kümesi güvenilirlik ve dayanıklılık seçme][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="d96fd-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="d96fd-232">Düğüm türü için VM sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="d96fd-233">Yukarı veya aşağı düğüm türü VM'ler sayısında daha sonra ölçeklendirebilirsiniz, ancak birincil düğüm türünde en düşük seçmiş olduğunuz güvenilirlik düzeyi tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="d96fd-234">Diğer düğüm türleri, en az 1 VM olabilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="d96fd-235">Özel uç noktaları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d96fd-235">Configure custom endpoints.</span></span> <span data-ttu-id="d96fd-236">Bu alan, Azure yük dengeleyici, uygulamalarınız için genel internet üzerinden kullanıma sunmak istediğiniz bağlantı noktalarının virgülle ayrılmış bir listesi girmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d96fd-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="d96fd-237">Örneğin, bir web uygulaması kümenize dağıtmayı planlıyorsanız, "80" bağlantı noktası 80, kümesine trafiğe izin verecek şekilde olmadığını buraya girin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="d96fd-238">Uç noktalar hakkında daha fazla bilgi için bkz: [uygulamaları ile iletişim][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="d96fd-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="d96fd-239">Küme yapılandırma **tanılama**.</span><span class="sxs-lookup"><span data-stu-id="d96fd-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="d96fd-240">Varsayılan olarak, sorunları gidermenize yardımcı olacak kümenizde tanılama etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="d96fd-241">Tanılama değişiklik devre dışı bırakmak istiyorsanız **durum** geç **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="d96fd-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="d96fd-242">Tanılama kapatma olan **değil** önerilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="d96fd-243">Kümesi istediğiniz doku yükseltme modu seçin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="d96fd-244">Seçin **otomatik**, sistemin otomatik olarak en son sürümünü seçin ve kümenizi yükseltmek denemek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d96fd-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="d96fd-245">Modu ayarlamak **el ile**, desteklenen bir sürüm seçmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d96fd-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="d96fd-246">Service Fabric desteklenen sürümlerini çalıştıran kümeler destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="d96fd-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="d96fd-247">Seçerek **el ile** modu yapmakta üzerinde sorumluluk kümenizi desteklenen bir sürüme yükseltmek için.</span><span class="sxs-lookup"><span data-stu-id="d96fd-247">By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version.</span></span> <span data-ttu-id="d96fd-248">Doku hakkında daha fazla ayrıntı modu bakın yükseltmek için [service fabric Küme yükseltme belge.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="d96fd-248">For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="d96fd-249">3. Güvenlik</span><span class="sxs-lookup"><span data-stu-id="d96fd-249">3. Security</span></span>
![Azure Portal'da güvenlik yapılandırmalarını ekran görüntüsü.][SecurityConfigs]

<span data-ttu-id="d96fd-251">Son adım, bilgi daha önce oluşturduğunuz sertifika ve anahtar kasası kullanarak küme güvenliğini sağlamak için sertifika bilgilerini sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="d96fd-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="d96fd-252">Karşıya yükleme alanından elde edilen çıkış birincil sertifikası alanları doldurmak **küme sertifika** anahtar kasası kullanmaya `Invoke-AddCertToKeyVault` PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="d96fd-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="d96fd-253">Denetleme **Gelişmiş ayarları Yapılandır** için istemci sertifikaları girmek için kutusunu **yönetici istemci** ve **salt okunur istemci**.</span><span class="sxs-lookup"><span data-stu-id="d96fd-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="d96fd-254">Bu alanlarda yönetici istemci sertifikanızın parmak izi ve salt okunur kullanıcının istemci sertifikanızın parmak izi varsa girin.</span><span class="sxs-lookup"><span data-stu-id="d96fd-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="d96fd-255">Yöneticiler kümeye bağlanmaya çalıştığında, yalnızca bir sertifika parmak izi değerleri eşleşen bir parmak izi ile varsa erişim buraya girilen verilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="d96fd-256">4. Özet</span><span class="sxs-lookup"><span data-stu-id="d96fd-256">4. Summary</span></span>
![<span data-ttu-id="d96fd-257">"Dağıtma Service Fabric kümesi" görüntüleme başlangıç panosunun ekran görüntüsü</span><span class="sxs-lookup"><span data-stu-id="d96fd-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="d96fd-258">Küme oluşturma işlemini tamamlamak için tıklatın **Özet** sağladığınız yapılandırmaları bakın veya kümeniz dağıtmak için kullanılan Azure Resource Manager şablonunu indirebilir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="d96fd-259">Zorunlu ayarları girdikten sonra **Tamam** düğmesi yeşil olur ve küme oluşturma işlemi tıklatarak başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d96fd-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="d96fd-260">Oluşturma işleminin ilerleme durumunu bildirimler bölümünden görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d96fd-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="d96fd-261">(Ekranınızın sağ üst köşesindeki durum çubuğunun yanında bulunan "Zil" simgesine tıklayın.) Tıkladıysanız **başlangıç panosuna Sabitle** göreceğiniz küme oluştururken **Service Fabric kümesi dağıtma** sabitlenmiş **Başlat** Panosu.</span><span class="sxs-lookup"><span data-stu-id="d96fd-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="d96fd-262">Küme durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d96fd-262">View your cluster status</span></span>
![Küme ayrıntıları panosunda ekran görüntüsü.][ClusterDashboard]

<span data-ttu-id="d96fd-264">Kümenizi oluşturduktan sonra kümenizi portalında inceleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d96fd-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="d96fd-265">Git **Gözat** tıklatıp **Service Fabric kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="d96fd-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="d96fd-266">Kümenizi bulun ve tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d96fd-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="d96fd-267">Kümenin genel uç noktası ve bir Service Fabric Explorer bağlantısıyla birlikte kümenizin ayrıntılarını panoda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d96fd-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="d96fd-268">**Düğümü İzleyici** kümenin Pano dikey bölümde sağlıklı ve iyi VM'lerin sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="d96fd-269">Kümenin durumu hakkında daha fazla ayrıntı bulabilirsiniz [Service Fabric sistem durumu modeli giriş][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="d96fd-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="d96fd-270">Service Fabric kümeleri belirli sayıda düğümleri yukarı kullanılabilirliği sürdürmek ve "çekirdek Bakımı olarak" başvurulan durumunu - korumak için her zaman olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96fd-270">Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum".</span></span> <span data-ttu-id="d96fd-271">Therfore, değil genellikle ilk yapmadığınız sürece kümedeki tüm makineleri kapatmaya güvenli bir [tam yedekleme, durumu][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="d96fd-271">Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="d96fd-272">Bir sanal makine ölçek kümesi örneği veya bir küme düğümü için uzaktan bağlanma</span><span class="sxs-lookup"><span data-stu-id="d96fd-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="d96fd-273">Her küme sonuçlarınızın ayarı alınırken bir sanal makine ölçek kümesi içinde belirttiğiniz NodeTypes.</span><span class="sxs-lookup"><span data-stu-id="d96fd-273">Each of the NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="d96fd-274">Bkz: [uzaktan bağlanmak için bir sanal makine ölçek kümesi örnek] [ remote-connect-to-a-vm-scale-set] Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="d96fd-274">See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d96fd-275">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d96fd-275">Next steps</span></span>
<span data-ttu-id="d96fd-276">Bu noktada, yönetim kimlik doğrulaması için sertifikaları kullanarak güvenli bir küme var.</span><span class="sxs-lookup"><span data-stu-id="d96fd-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="d96fd-277">Ardından, [kümenize bağlanmak](service-fabric-connect-to-secure-cluster.md) ve öğrenin nasıl [uygulama parolaları yönetme](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="d96fd-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="d96fd-278">Ayrıca, öğrenin [Service Fabric destek seçenekleri](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="d96fd-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

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
