---
title: "Azure anahtar kasası CLI kullanarak yönetme | Microsoft Docs"
description: "CLI kullanarak anahtar kasası ortak görevleri otomatikleştirmek için bu öğreticiyi kullanın"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: c2565a742ce4f6ab5f7639a54c4a475f00cbc260
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="36acd-103">Anahtar kasası CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="36acd-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="36acd-104">Azure Anahtar Kasası çoğu bölgede kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36acd-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="36acd-105">Daha fazla bilgi için bkz. [Anahtar Kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="36acd-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="36acd-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="36acd-106">Introduction</span></span>

<span data-ttu-id="36acd-107">Bu öğreticiyi, Azure'da sağlamlaştırılmış bir kapsayıcı (bir kasa) oluşturmak ve Azure'da şifreleme anahtarlarını ve gizli anahtarları depolayıp yönetmek amacıyla Azure Anahtar Kasası ile çalışmaya başlamaya yardımcı olması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="36acd-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="36acd-108">Bu, bir anahtar ya da sonra bir Azure uygulamasıyla kullanabileceğiniz parola içeren bir kasa oluşturmak için Azure platformlar arası komut satırı arabirimi kullanarak işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="36acd-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="36acd-109">Bunu daha sonra nasıl bir uygulama daha sonra bu anahtarı veya parolayı kullanabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="36acd-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="36acd-110">**Tahmini tamamlanma süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="36acd-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="36acd-111">Bu öğretici, adımlardan biri, bir anahtar veya gizli anahtarı kasaya kullanmak için bir uygulamanın nasıl gösterir içerdiğini Azure uygulaması yazma yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="36acd-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="36acd-112">Şu anda Azure portalında Azure Anahtar Kasası'nı yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="36acd-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="36acd-113">Bunun yerine, bu platformlar arası komut satırı arabirimi yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="36acd-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="36acd-114">Veya, Azure PowerShell yönergeleri için bkz: [bu eşdeğer öğreticiye](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="36acd-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="36acd-115">Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="36acd-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36acd-116">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="36acd-116">Prerequisites</span></span>

<span data-ttu-id="36acd-117">Bu öğreticiyi tamamlamak için aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="36acd-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="36acd-118">Bir Microsoft Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="36acd-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="36acd-119">Bir yoksa için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="36acd-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="36acd-120">Komut satırı arabirimi sürümünü 0.9.1 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="36acd-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="36acd-121">En son sürümünü yükleyin ve Azure aboneliğinize bağlanmak için bkz: [Azure platformlar arası komut satırı arabirimi yükleyip](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="36acd-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="36acd-122">Bu öğreticide oluşturduğunuz anahtarı veya parolayı kullanmak üzere yapılandırılacak bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="36acd-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="36acd-123">[Microsoft Yükleme Merkezi](http://www.microsoft.com/download/details.aspx?id=45343)'nde örnek bir uygulama kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36acd-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="36acd-124">Yönergeler için beraberinde gelen Benioku dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="36acd-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="36acd-125">Azure platformlar arası komut satırı arabirimi ile ilgili Yardım alma</span><span class="sxs-lookup"><span data-stu-id="36acd-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="36acd-126">Bu öğretici, komut satırı arabirimi (Bash, Terminal, komut istemi) bildiğinizi varsayar</span><span class="sxs-lookup"><span data-stu-id="36acd-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="36acd-127">Yardım veya -h parametresi, belirli komutlar için Yardım görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36acd-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="36acd-128">Alternatif olarak, azure help [komut] [Seçenekler] biçimi, aynı bilgileri döndürmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36acd-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="36acd-129">Örneğin, aşağıdaki komutları tüm aynı bilgileri döndürün:</span><span class="sxs-lookup"><span data-stu-id="36acd-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="36acd-130">Kullanarak--yardımcı olmak için şüpheli bir komut tarafından gerekli parametreleri hakkında başvuru, -h veya azure yardıma [komut].</span><span class="sxs-lookup"><span data-stu-id="36acd-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="36acd-131">Ayrıca, Azure platformlar arası komut satırı arabirimi ile Azure Resource Manager hakkında bilgi edinmek için aşağıdaki öğreticileri okuyabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="36acd-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="36acd-132">Yükleme ve yapılandırma Azure platformlar arası komut satırı arabirimi</span><span class="sxs-lookup"><span data-stu-id="36acd-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="36acd-133">Azure Resource Manager ile Azure platformlar arası komut satırı arabirimi kullanma</span><span class="sxs-lookup"><span data-stu-id="36acd-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="36acd-134">Aboneliklerinize bağlanma</span><span class="sxs-lookup"><span data-stu-id="36acd-134">Connect to your subscriptions</span></span>

<span data-ttu-id="36acd-135">Bir kurumsal hesap kullanarak oturum açması aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="36acd-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="36acd-136">veya etkileşimli olarak yazarak oturum açmak istiyorsanız</span><span class="sxs-lookup"><span data-stu-id="36acd-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="36acd-137">Oturum açma yöntemi, yalnızca kuruluş hesabı ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="36acd-137">The login method only works with organizational account.</span></span> <span data-ttu-id="36acd-138">Bir kurumsal hesap kuruluşunuz tarafından yönetilen ve kuruluşunuzun Azure Active Directory kiracısı'nda tanımlanan bir kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="36acd-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="36acd-139">Şu anda bir kurumsal hesap yok ve Azure aboneliğinizde oturum açmak için bir Microsoft hesabı kullanarak, aşağıdaki adımları kullanarak kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36acd-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="36acd-140">Oturum açma için oturum açma [Azure Yönetim Portalı](https://manage.windowsazure.com/)ve üzerinde Active Directory'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="36acd-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="36acd-141">Hiçbir dizin varsa, dizin oluştur'u seçin ve istenen bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="36acd-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="36acd-142">Dizininizi seçin ve yeni bir kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="36acd-142">Select your directory and add a new user.</span></span> <span data-ttu-id="36acd-143">Bu kullanıcı bir kurumsal hesap ' dir.</span><span class="sxs-lookup"><span data-stu-id="36acd-143">This new user is an organizational account.</span></span> <span data-ttu-id="36acd-144">Kullanıcı oluşturma sırasında kullanıcı ve geçici bir parola için her iki e-posta adresi olan sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="36acd-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="36acd-145">Başka bir adımda kullanılan olarak bu bilgileri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="36acd-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="36acd-146">Portal ayarlarını seçin ve yöneticileri'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="36acd-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="36acd-147">Ekle'yi seçin ve bir ortak yönetici yeni kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="36acd-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="36acd-148">Bu, Azure aboneliğinizi yönetmek için Kurumsal hesap sağlar.</span><span class="sxs-lookup"><span data-stu-id="36acd-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="36acd-149">Son olarak dışında Azure portalında oturum açın ve sonra geri yeni Kurumsal hesap kullanarak oturum aç.</span><span class="sxs-lookup"><span data-stu-id="36acd-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="36acd-150">Bu hesap ilk zaman oturum varsa, parolayı değiştirmek için istenir.</span><span class="sxs-lookup"><span data-stu-id="36acd-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="36acd-151">Microsoft Azure ile bir kurumsal hesap kullanma hakkında daha fazla bilgi için bkz: [Microsoft Azure'a kuruluş olarak kaydolma](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="36acd-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="36acd-152">Birden çok aboneliğiniz varsa ve Azure Anahtar Kasası için kullanmak üzere belirli bir tanesini belirtmek istiyorsanız hesabınızın aboneliklerini görmek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="36acd-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="36acd-153">Ardından, kullanılacak aboneliği belirtmek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="36acd-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="36acd-154">Azure platformlar arası komut satırı arabirimi yapılandırma hakkında daha fazla bilgi için bkz: [yükleme ve yapılandırma Azure platformlar arası komut satırı arabirimi](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="36acd-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="36acd-155">Azure Resource Manager kullanarak geçiş</span><span class="sxs-lookup"><span data-stu-id="36acd-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="36acd-156">Azure Resource Manager anahtar kasası gerektirir, bu nedenle Azure Resource Manager moduna geçmek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="36acd-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="36acd-157">Yeni bir kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="36acd-157">Create a new resource group</span></span>
<span data-ttu-id="36acd-158">Azure Kaynak Yöneticisi'ni kullanırken, tüm ilgili kaynaklar bir kaynak grubu içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="36acd-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="36acd-159">Bu öğretici için yeni bir kaynak grubu 'ContosoResourceGroup' oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="36acd-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="36acd-160">İlk parametre kaynak grubu adı ve ikinci parametre konumu.</span><span class="sxs-lookup"><span data-stu-id="36acd-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="36acd-161">Konum için komutunu `azure location list` Bu örnekte bir alternatif bir konum belirtmek nasıl belirlemek üzere.</span><span class="sxs-lookup"><span data-stu-id="36acd-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="36acd-162">Daha fazla bilgiye ihtiyacınız varsa, yazın:`azure help location`</span><span class="sxs-lookup"><span data-stu-id="36acd-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="36acd-163">Anahtar kasası kaynak sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="36acd-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="36acd-164">Bu anahtar kasası kaynak sağlayıcısı aboneliğinizde kayıtlı olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="36acd-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="36acd-165">Bu yalnızca bir kez abonelik başına yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36acd-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="36acd-166">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="36acd-166">Create a key vault</span></span>

<span data-ttu-id="36acd-167">Kullanım `azure keyvault create` bir anahtar kasası oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="36acd-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="36acd-168">Bu komut dosyasını üç zorunlu parametreye sahiptir: bir kaynak grubu adı, bir anahtar kasası adı ve coğrafi konum.</span><span class="sxs-lookup"><span data-stu-id="36acd-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="36acd-169">Örneğin, ContosoKeyVault kasa adını kullanırsanız, ContosoResourceGroup kaynak grubu adını ve Doğu Asya konumunu yazın:</span><span class="sxs-lookup"><span data-stu-id="36acd-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="36acd-170">Bu komutun çıktısı, yeni oluşturduğunuz anahtar kasasının özelliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="36acd-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="36acd-171">En önemli iki özellik şunlardır:</span><span class="sxs-lookup"><span data-stu-id="36acd-171">The two most important properties are:</span></span>

* <span data-ttu-id="36acd-172">**Ad**: örnekte ContosoKeyVault budur.</span><span class="sxs-lookup"><span data-stu-id="36acd-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="36acd-173">Bu adı diğer Anahtar Kasası cmdlet'leri için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="36acd-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="36acd-174">**vaultUri**: örnekte https://contosokeyvault.vault.azure.net budur.</span><span class="sxs-lookup"><span data-stu-id="36acd-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="36acd-175">REST API'si aracılığıyla kasanızı kullanan uygulamaların bu URI'yi kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="36acd-176">Azure hesabınız artık bu anahtar kasasında herhangi bir işlemi gerçekleştirmeye yetkilidir.</span><span class="sxs-lookup"><span data-stu-id="36acd-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="36acd-177">Henüz başka kimse yetkilendirilmedi.</span><span class="sxs-lookup"><span data-stu-id="36acd-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="36acd-178">Anahtar kasasına bir anahtar veya gizli anahtar ekleme</span><span class="sxs-lookup"><span data-stu-id="36acd-178">Add a key or secret to the key vault</span></span>

<span data-ttu-id="36acd-179">Azure anahtar Kasası'nın yazılım korumalı bir anahtar oluşturmasını istiyorsanız, kullanmak `azure key create` komutunu ve aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="36acd-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="36acd-180">Ancak, yerel dosya Azure anahtar Kasası'na karşıya yüklemek istediğiniz softkey.pem adlı bir dosya olarak kaydedilmiş bir .pem dosyasını mevcut bir anahtarı varsa, anahtarı içeri aktarmak için aşağıdaki komutu yazın. Anahtar kasası hizmetinde yazılım ile anahtarı koruyan PEM dosyası:</span><span class="sxs-lookup"><span data-stu-id="36acd-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="36acd-181">Artık oluşturduğunuz veya Azure anahtar Kasası'na URI'sini kullanarak karşıya anahtar başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36acd-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="36acd-182">Kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** her zaman geçerli sürümü almak ve kullanmak için **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** bu belirli sürümü almak için.</span><span class="sxs-lookup"><span data-stu-id="36acd-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="36acd-183">Gizli SQLPassword adlı bir parola olduğu ve değer, Pa$ $w0rd Azure anahtar kasası için olan, kasaya eklemek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="36acd-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="36acd-184">Artık Azure Anahtar Kasası'na eklediğiniz bu parolaya URI'sini kullanarak başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36acd-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="36acd-185">Her zaman geçerli sürümü almak için **https://ContosoVault.vault.azure.net/secrets/SQLPassword** kullanın ve bu belirli sürümü almak için **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** kullanın.</span><span class="sxs-lookup"><span data-stu-id="36acd-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="36acd-186">Şimdi yeni anahtar veya gizli görünümü oluşturan:</span><span class="sxs-lookup"><span data-stu-id="36acd-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="36acd-187">Anahtarınızı görüntülemek için şunu yazın: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="36acd-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="36acd-188">Gizli anahtarı görüntülemek için şunu yazın: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="36acd-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="36acd-189">Bir uygulamayı Azure Active Directory'ye kaydetme</span><span class="sxs-lookup"><span data-stu-id="36acd-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="36acd-190">Bu adım genellikle ayrı bir bilgisayarda bir geliştirici tarafından yapılır.</span><span class="sxs-lookup"><span data-stu-id="36acd-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="36acd-191">Azure anahtar Kasası'na özgü değildir ancak bütünlük açısından buraya eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="36acd-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36acd-192">Öğreticiyi tamamlamak için bu adımda kaydedeceğiniz hesabınızın, kasanızın ve uygulamanızın hepsinin aynı Azure dizininde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="36acd-193">Bir anahtar kasası kullanan uygulamaların, Azure Active Directory'den bir belirteç kullanarak kimlik doğrulama yapması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="36acd-194">Bunu yapmak için uygulama sahibinin öncelikle Azure Active Directory'sinde uygulamayı kaydetmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="36acd-195">Kaydın sonunda, uygulama sahibi aşağıdaki değerleri elde eder:</span><span class="sxs-lookup"><span data-stu-id="36acd-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="36acd-196">Bir **Uygulama Kimliği** (İstemci Kimliği olarak da bilinir) ve **kimlik doğrulama anahtarı** (paylaşılan gizli anahtar olarak da bilinir).</span><span class="sxs-lookup"><span data-stu-id="36acd-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="36acd-197">Uygulama bu değerleri her ikisi de Azure bir belirteç almak için Active Directory ile sunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="36acd-198">Uygulamanın bunu yapmak için nasıl yapılandırılacağı uygulamaya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="36acd-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="36acd-199">Anahtar Kasası örnek uygulaması için uygulama sahibi bu değerleri app.config dosyasında ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36acd-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="36acd-200">Bir uygulamayı Azure Active Directory'ye kaydetmek için:</span><span class="sxs-lookup"><span data-stu-id="36acd-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="36acd-201">Azure Portal’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="36acd-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="36acd-202">Solda **Active Directory**'ye tıklayın ve ardından uygulamanızı içine kaydedeceğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="36acd-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="36acd-203">Anahtar kasanızı oluşturduğunuz Azure aboneliğini içeren aynı dizini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-203">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="36acd-204">Bu dizinin hangisi olduğunu bilmiyorsanız **Ayarlar**'a tıklayın, anahtar kasanızı oluşturduğunuz aboneliği tanımlayın ve son sütunda görüntülenen dizinin adını not edin.</span><span class="sxs-lookup"><span data-stu-id="36acd-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="36acd-205">**UYGULAMALAR**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="36acd-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="36acd-206">Dizininize hiçbir uygulama eklenmemişse bu sayfa yalnızca Göster **bir uygulama ekleyin** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="36acd-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="36acd-207">Bağlantıya tıklayın veya alternatif olarak, tıklatabilirsiniz **ekleme** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="36acd-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="36acd-208">**UYGULAMA EKLEME** sihirbazında **Ne yapmak istiyorsunuz?** sayfasında **Add an application my organization is developing (Kuruluşumun geliştirdiği bir uygulama ekle)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="36acd-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="36acd-209">Üzerinde **bize uygulamanızı anlatın** sayfasında uygulamanız için bir ad belirtin ve seçin **WEB uygulaması ve/veya WEB API** (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="36acd-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="36acd-210">Sonraki simgeyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="36acd-210">Click the Next icon.</span></span>
6. <span data-ttu-id="36acd-211">**Uygulama özellikleri** sayfasında web uygulamanız için **OTURUM AÇMA URL'Sİ** ve **UYGULAMA KİMLİĞİ URI'Sİ** belirtin.</span><span class="sxs-lookup"><span data-stu-id="36acd-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="36acd-212">Uygulamanız bu değerlere sahip değilse değerleri bu adım için kendiniz belirleyebilirsiniz. (örneğin, her iki kutu için http://test1.contoso.com belirtebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="36acd-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="36acd-213">Bu sitelerin var olup olmaması önemli değildir; önemli olan her bir uygulama için uygulama kimliği URI'sinin dizininizdeki tüm uygulamalar için farklı olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="36acd-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="36acd-214">Dizin uygulamanızı tanımlamak için bu dizeyi kullanır.</span><span class="sxs-lookup"><span data-stu-id="36acd-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="36acd-215">Sihirbazda yaptığınız değişiklikleri kaydetmek için tam simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="36acd-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="36acd-216">Hızlı Başlangıç sayfasında, tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="36acd-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="36acd-217">**Anahtarlar** bölümüne kaydırın, süre seçin ve ardından **KAYDET**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="36acd-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="36acd-218">Sayfa yenilenir ve ardından bir anahtar değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="36acd-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="36acd-219">Bu anahtar değeri ve **İSTEMCİ KİMLİĞİ** değeri ile uygulamanızı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="36acd-220">(Bu yapılandırma için yönergeler uygulamaya özgü olur.)</span><span class="sxs-lookup"><span data-stu-id="36acd-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="36acd-221">Kasanızda izinleri ayarlamak için bir sonraki adımda kullanacağınız istemci kimliği değerini bu sayfadan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="36acd-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="36acd-222">Anahtar veya gizli anahtarı kullanması için uygulamayı yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="36acd-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="36acd-223">Anahtar veya gizli kasadaki erişmek için uygulama yetkilendirmek için `azure keyvault set-policy` komutu.</span><span class="sxs-lookup"><span data-stu-id="36acd-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="36acd-224">Örneğin, kasa adınız ContosoKeyVault ve yetkilendirmek istediğiniz uygulama 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed istemci Kimliğine sahip kasanızı anahtarlarında oturum açın ve şifresini çözmek için uygulama yetkilendirmek istediğiniz ise, ardından şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="36acd-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="36acd-225">Windows komut istemi üzerinde çalıştırıyorsanız, tek tırnak işaretleri çift tırnak işareti ile değiştirin ve ayrıca iç çift tırnak işareti kaçış gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="36acd-226">Örneğin: "[\"şifresini\",\"oturum\"]".</span><span class="sxs-lookup"><span data-stu-id="36acd-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="36acd-227">Aynı uygulamayı kasanızdaki gizli anahtarları okumak için yetkilendirmek istiyorsanız şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="36acd-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="36acd-228">Bir donanım güvenlik modülü (HSM) kullanmak istiyorsanız</span><span class="sxs-lookup"><span data-stu-id="36acd-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="36acd-229">Ek güvence için HSM sınırını asla terk etmeyen donanım güvenlik modüllerinde (HSM'ler) anahtarları içeri aktarabilir veya oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36acd-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="36acd-230">HSM'ler, FIPS 140-2 Düzey 2 doğrulanmasına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="36acd-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="36acd-231">Bu gereksinim sizin için geçerli değilse bu bölümü atlayın ve [Anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme](#delete-the-key-vault-and-associated-keys-and-secrets)'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="36acd-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="36acd-232">Bu HSM korumalı anahtarları oluşturmak için HSM korumalı anahtarları destekleyen bir kasa aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36acd-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="36acd-233">Keyvault oluşturduğunuzda 'sku' parametresini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="36acd-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="36acd-234">Bu kasaya yazılım korumalı anahtarlar ve HSM korumalı anahtarlar (daha önce gösterildiği gibi) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36acd-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="36acd-235">HSM korumalı bir anahtar oluşturmak için hedef parametresini 'HSM' ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="36acd-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="36acd-236">.Pem dosyasını bilgisayarınızdaki bir anahtar almak için aşağıdaki komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36acd-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="36acd-237">Bu komut, anahtarı Anahtar Kasası hizmetindeki HSM'lere aktarır:</span><span class="sxs-lookup"><span data-stu-id="36acd-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="36acd-238">Bir sonraki komut bir "kendi anahtarınızı getirin" (BYOK) paketini içeri aktarır.</span><span class="sxs-lookup"><span data-stu-id="36acd-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="36acd-239">Böylece anahtar HSM sınırını terk etmeden yerel HSM'nizde anahtarınızı oluşturmanız ve Anahtar Kasası hizmetindeki HSM'lere bunu aktarmanız sağlanır.</span><span class="sxs-lookup"><span data-stu-id="36acd-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="36acd-240">Daha ayrıntılı bu BYOK paketini oluşturma hakkında yönergeler için bkz: [HSM-Protected anahtarları Azure anahtar kasası ile kullanmak nasıl](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="36acd-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="36acd-241">Anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme</span><span class="sxs-lookup"><span data-stu-id="36acd-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="36acd-242">Anahtar kasası ve anahtar veya içerdiği gizli artık ihtiyacınız varsa, anahtar kasası azure keyvault silme komutunu kullanarak silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="36acd-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="36acd-243">Alternatif olarak, anahtar kasasını ve bu gruba eklediğiniz herhangi diğer kaynakları içeren Azure kaynak grubunun tümünü silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36acd-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="36acd-244">Diğer Azure platformlar arası komut satırı arabirimi komutları</span><span class="sxs-lookup"><span data-stu-id="36acd-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="36acd-245">Diğer komutlar Azure anahtar kasası yönetmek için kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="36acd-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="36acd-246">Bu komut tüm anahtarların ve seçilen özelliklerin tablolu bir görüntüsünü listeler:</span><span class="sxs-lookup"><span data-stu-id="36acd-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="36acd-247">Bu komut belirtilen anahtar için özelliklerin tam listesini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="36acd-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="36acd-248">Bu komut tüm gizli adların ve seçilen özelliklerin tablolu bir görüntüsünü listeler:</span><span class="sxs-lookup"><span data-stu-id="36acd-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="36acd-249">Belirli bir anahtarın nasıl kaldırılacağına bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="36acd-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="36acd-250">Belirli bir gizli anahtarın nasıl kaldırılacağına bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="36acd-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="36acd-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36acd-251">Next steps</span></span>
<span data-ttu-id="36acd-252">Programlama başvuruları için bkz. [Azure Anahtar Kasası geliştirici kılavuzu](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="36acd-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

