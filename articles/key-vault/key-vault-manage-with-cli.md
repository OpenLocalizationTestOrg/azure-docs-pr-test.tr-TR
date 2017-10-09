---
title: "Azure anahtar kasası CLI kullanarak aaaManage | Microsoft Docs"
description: "Bu öğretici tooautomate ortak görevler anahtar kasasına hello CLI kullanarak"
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
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="b795b-103">Anahtar kasası CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="b795b-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="b795b-104">Azure Anahtar Kasası çoğu bölgede kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b795b-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="b795b-105">Daha fazla bilgi için bkz: Merhaba [anahtar kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="b795b-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="b795b-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="b795b-106">Introduction</span></span>

<span data-ttu-id="b795b-107">Size Bu öğretici toohelp kullanmak ile Azure anahtar kasası toocreate toostore Azure'da sağlamlaştırılmış bir kapsayıcı (bir kasa) başlatıldı ve şifreleme anahtarları ve gizli anahtarları azure'da yönetin.</span><span class="sxs-lookup"><span data-stu-id="b795b-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="b795b-108">Bu, Azure platformlar arası komut satırı arabirimi toocreate kullanarak hello sürecinde bir anahtar ya da sonra bir Azure uygulamasıyla kullanabileceğiniz parola içeren bir kasa yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b795b-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="b795b-109">Bunu daha sonra nasıl bir uygulama daha sonra bu anahtarı veya parolayı kullanabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="b795b-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="b795b-110">**Zaman toocomplete tahmini:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="b795b-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="b795b-111">Bu öğretici nasıl toowrite hello nasıl tooauthorize uygulama toouse bir anahtar veya gizli hello anahtarında kasa gösteren hello adımları içeren Azure uygulamanızı yönergeleri içermez.</span><span class="sxs-lookup"><span data-stu-id="b795b-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
> 
> <span data-ttu-id="b795b-112">Şu anda hello Azure portalında Azure anahtar kasası yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="b795b-112">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="b795b-113">Bunun yerine, bu platformlar arası komut satırı arabirimi yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b795b-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="b795b-114">Veya, Azure PowerShell yönergeleri için bkz: [bu eşdeğer öğreticiye](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b795b-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="b795b-115">Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="b795b-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b795b-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b795b-116">Prerequisites</span></span>

<span data-ttu-id="b795b-117">toocomplete Bu öğreticiyi izleyerek hello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="b795b-117">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="b795b-118">Abonelik tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b795b-118">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="b795b-119">Bir yoksa için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="b795b-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="b795b-120">Komut satırı arabirimi sürümünü 0.9.1 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b795b-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="b795b-121">tooinstall hello en son sürümünü ve tooyour Azure aboneliğine bağlanma Bkz [hello Azure platformlar arası komut satırı arabirimi yükleyip](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b795b-121">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="b795b-122">Yapılandırılmış toouse hello anahtar ya da Bu öğreticide oluşturduğunuz parola olacak bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="b795b-122">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="b795b-123">Bir örnek uygulama hello kullanılabilir [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="b795b-123">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="b795b-124">Yönergeler için Benioku dosyası ile birlikte gelen hello bakın.</span><span class="sxs-lookup"><span data-stu-id="b795b-124">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="b795b-125">Azure platformlar arası komut satırı arabirimi ile ilgili Yardım alma</span><span class="sxs-lookup"><span data-stu-id="b795b-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="b795b-126">Bu öğretici, başlangıç komut satırı arabirimi (Bash, Terminal, komut istemi) bildiğinizi varsayar</span><span class="sxs-lookup"><span data-stu-id="b795b-126">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="b795b-127">Merhaba--Yardım veya -h parametresi olabilir tooview Yardım belirli komutları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b795b-127">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="b795b-128">Alternatif olarak, aynı bilgileri hello azure Yardım [komut biçimi de kullanılan tooreturn olabilir] [Seçenekler] hello.</span><span class="sxs-lookup"><span data-stu-id="b795b-128">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="b795b-129">Örneğin, tüm dönüş hello aşağıdaki komutları hello aynı bilgileri:</span><span class="sxs-lookup"><span data-stu-id="b795b-129">For example, hello following commands all return hello same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="b795b-130">Toohelp kullanarak--zaman şüpheli bir komut tarafından gerekli hello parametreleri hakkında başvuru, -h veya azure yardıma [komut].</span><span class="sxs-lookup"><span data-stu-id="b795b-130">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or azure help [command].</span></span>

<span data-ttu-id="b795b-131">Ayrıca, Azure Resource Manager Azure platformlar arası komut satırı arabirimi ile tanıdık öğreticileri tooget aşağıdaki hello okuyabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b795b-131">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="b795b-132">Nasıl tooinstall ve Azure platformlar arası komut satırı arabirimini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b795b-132">How tooinstall and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="b795b-133">Azure Resource Manager ile Azure platformlar arası komut satırı arabirimi kullanma</span><span class="sxs-lookup"><span data-stu-id="b795b-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="b795b-134">Tooyour abonelikleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="b795b-134">Connect tooyour subscriptions</span></span>

<span data-ttu-id="b795b-135">bir kuruluş hesabı, komutu aşağıdaki kullanım hello kullanarak toolog:</span><span class="sxs-lookup"><span data-stu-id="b795b-135">toolog in using an organizational account, use hello following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="b795b-136">veya, toolog etkileşimli olarak yazarak istiyorsanız</span><span class="sxs-lookup"><span data-stu-id="b795b-136">or if you want toolog in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="b795b-137">Merhaba oturum açma yöntemi, yalnızca kuruluş hesabı ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="b795b-137">hello login method only works with organizational account.</span></span> <span data-ttu-id="b795b-138">Bir kurumsal hesap kuruluşunuz tarafından yönetilen ve kuruluşunuzun Azure Active Directory kiracısı'nda tanımlanan bir kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="b795b-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="b795b-139">Bir kurumsal hesap şu anda sahip değil ve bir Microsoft hesabı toolog tooyour Azure aboneliği kullanıyorsanız, kolayca kullanarak bir tane oluşturabilirsiniz hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b795b-139">If you do not currently have an organizational account, and are using a Microsoft account toolog in tooyour Azure subscription, you can easily create one using hello following steps.</span></span>

1. <span data-ttu-id="b795b-140">Oturum açma toohello oturum açma toohello [Azure Yönetim Portalı](https://manage.windowsazure.com/)ve üzerinde Active Directory'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b795b-140">Login toohello Login toohello [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="b795b-141">Hiçbir dizin varsa, dizin oluşturma seçip hello sağlamak bilgi istedi.</span><span class="sxs-lookup"><span data-stu-id="b795b-141">If no directory exists, select Create your directory and provide hello requested information.</span></span>
3. <span data-ttu-id="b795b-142">Dizininizi seçin ve yeni bir kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b795b-142">Select your directory and add a new user.</span></span> <span data-ttu-id="b795b-143">Bu kullanıcı bir kurumsal hesap ' dir.</span><span class="sxs-lookup"><span data-stu-id="b795b-143">This new user is an organizational account.</span></span> <span data-ttu-id="b795b-144">Merhaba kullanıcı Hello oluşturulurken hello kullanıcı için bir e-posta adresi ve geçici bir parola ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b795b-144">During hello creation of hello user, you will be supplied with both an e-mail address for hello user and a temporary password.</span></span> <span data-ttu-id="b795b-145">Başka bir adımda kullanılan olarak bu bilgileri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b795b-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="b795b-146">Merhaba portalından ayarları seçin ve yöneticileri'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="b795b-146">From hello portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="b795b-147">Ekle'yi seçin ve bir ortak yönetici hello yeni kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b795b-147">Select Add, and add hello new user as a co-administrator.</span></span> <span data-ttu-id="b795b-148">Bu, Azure aboneliğinizin hello kuruluş hesabı toomanage sağlar.</span><span class="sxs-lookup"><span data-stu-id="b795b-148">This allows hello organizational account toomanage your Azure subscription.</span></span>
5. <span data-ttu-id="b795b-149">Son olarak, dışında hello Azure portalında oturum açın ve geri hello yeni Kurumsal hesap kullanarak oturum.</span><span class="sxs-lookup"><span data-stu-id="b795b-149">Finally, log out of hello Azure portal and then log back in using hello new organizational account.</span></span> <span data-ttu-id="b795b-150">Bu hello bu hesapla önce zaman oturum ise, istendiğinde toochange hello parola olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b795b-150">If this is hello first time logging in with this account, you will be prompted toochange hello password.</span></span>

<span data-ttu-id="b795b-151">Microsoft Azure ile bir kurumsal hesap kullanma hakkında daha fazla bilgi için bkz: [Microsoft Azure'a kuruluş olarak kaydolma](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="b795b-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="b795b-152">Birden çok aboneliğiniz varsa ve Azure anahtar kasası için toospecify belirli bir toouse istediğiniz, hesabınız için toosee hello abonelikleri aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="b795b-152">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="b795b-153">Ardından, toospecify hello abonelik toouse, türü:</span><span class="sxs-lookup"><span data-stu-id="b795b-153">Then, toospecify hello subscription toouse, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="b795b-154">Azure platformlar arası komut satırı arabirimi yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooInstall ve Azure platformlar arası komut satırı arabirimi yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b795b-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How tooInstall and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-toousing-azure-resource-manager"></a><span data-ttu-id="b795b-155">Anahtar toousing Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b795b-155">Switch toousing Azure Resource Manager</span></span>
<span data-ttu-id="b795b-156">Azure Resource Manager Hello anahtar kasası gerektirir, bu nedenle tooswitch tooAzure Resource Manager moduna aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="b795b-156">hello Key Vault requires Azure Resource Manager, so type hello following tooswitch tooAzure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="b795b-157">Yeni bir kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b795b-157">Create a new resource group</span></span>
<span data-ttu-id="b795b-158">Azure Kaynak Yöneticisi'ni kullanırken, tüm ilgili kaynaklar bir kaynak grubu içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b795b-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="b795b-159">Bu öğretici için yeni bir kaynak grubu 'ContosoResourceGroup' oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="b795b-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="b795b-160">Merhaba ilk parametre kaynak grubu adı ve hello ikinci parametre başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="b795b-160">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="b795b-161">Konum için hello komutunu `azure location list` tooidentify nasıl toospecify bir alternatif konum toohello biri bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="b795b-161">For location, use hello command `azure location list` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="b795b-162">Daha fazla bilgiye ihtiyacınız varsa, yazın:`azure help location`</span><span class="sxs-lookup"><span data-stu-id="b795b-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="b795b-163">Merhaba anahtar kasası kaynak sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="b795b-163">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="b795b-164">Bu anahtar kasası kaynak sağlayıcısı aboneliğinizde kayıtlı olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="b795b-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="b795b-165">Bu, yalnızca abonelik başına bir kez yapılır toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b795b-165">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="b795b-166">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b795b-166">Create a key vault</span></span>

<span data-ttu-id="b795b-167">Kullanım hello `azure keyvault create` komutu toocreate bir anahtar kasası.</span><span class="sxs-lookup"><span data-stu-id="b795b-167">Use hello `azure keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="b795b-168">Bu komut dosyasını üç zorunlu parametreye sahiptir: bir kaynak grubu adı, anahtar kasası adı ve hello coğrafi konum.</span><span class="sxs-lookup"><span data-stu-id="b795b-168">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="b795b-169">Örneğin, ContosoKeyVault, ContosoResourceGroup hello kaynak grubu adını ve Doğu Asya konumunu hello hello kasa adını kullanırsanız yazın:</span><span class="sxs-lookup"><span data-stu-id="b795b-169">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="b795b-170">Bu komutun çıktısı Hello hello yeni oluşturduğunuz anahtar kasasının özelliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b795b-170">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="b795b-171">Merhaba iki en önemli özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b795b-171">hello two most important properties are:</span></span>

* <span data-ttu-id="b795b-172">**Ad**: hello örnekte ContosoKeyVault budur.</span><span class="sxs-lookup"><span data-stu-id="b795b-172">**Name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="b795b-173">Bu adı diğer Anahtar Kasası cmdlet'leri için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b795b-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="b795b-174">**vaultUri**: hello örnekte https://contosokeyvault.vault.azure.net budur.</span><span class="sxs-lookup"><span data-stu-id="b795b-174">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="b795b-175">REST API'si aracılığıyla kasanızı kullanan uygulamaların bu URI'yi kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b795b-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="b795b-176">Bu anahtarı üzerindeki herhangi bir işlem yetkili tooperform kasa artık Azure hesabınız bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="b795b-176">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="b795b-177">Henüz başka kimse yetkilendirilmedi.</span><span class="sxs-lookup"><span data-stu-id="b795b-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="b795b-178">Bir anahtar veya gizli toohello anahtar kasası ekleme</span><span class="sxs-lookup"><span data-stu-id="b795b-178">Add a key or secret toohello key vault</span></span>

<span data-ttu-id="b795b-179">Sizin için Azure anahtar kasası toocreate yazılımla korunan anahtardan istiyorsanız, hello kullanın `azure key create` komut ve hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="b795b-179">If you want Azure Key Vault toocreate a software-protected key for you, use hello `azure key create` command, and type hello following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="b795b-180">Ancak, yerel dosya tooupload tooAzure anahtar kasası istediğiniz softkey.pem adlı bir dosya olarak kaydedilmiş bir .pem dosyasını mevcut bir anahtarı varsa, hello tooimport hello anahtar aşağıdaki hello yazın. PEM dosyası yazılım hello anahtar kasası hizmeti ile Merhaba anahtarı korur:</span><span class="sxs-lookup"><span data-stu-id="b795b-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="b795b-181">Artık oluşturduğunuz veya tooAzure anahtar kasası URI'sini kullanarak karşıya hello anahtar başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b795b-181">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="b795b-182">Kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello geçerli sürümü almak ve kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget bu belirli sürümü.</span><span class="sxs-lookup"><span data-stu-id="b795b-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="b795b-183">tooadd SQLPassword adlı bir parola olduğu ve Pa$ $w0rd tooAzure anahtar kasası, aşağıdaki türü hello hello değerine sahip bir gizli toohello Kasası:</span><span class="sxs-lookup"><span data-stu-id="b795b-183">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="b795b-184">Artık bu parolayı URI'sini kullanarak tooAzure anahtar kasası, eklenen başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b795b-184">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="b795b-185">Kullanmak **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello geçerli sürümü almak ve kullanmak **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget bu belirli sürümü.</span><span class="sxs-lookup"><span data-stu-id="b795b-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="b795b-186">Şimdi hello anahtar veya yeni oluşturduğunuz gizli görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="b795b-186">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="b795b-187">tooview anahtar, türünüz:`azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="b795b-187">tooview your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="b795b-188">tooview, gizli, türü:`azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="b795b-188">tooview your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="b795b-189">Bir uygulamayı Azure Active Directory'ye kaydetme</span><span class="sxs-lookup"><span data-stu-id="b795b-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="b795b-190">Bu adım genellikle ayrı bir bilgisayarda bir geliştirici tarafından yapılır.</span><span class="sxs-lookup"><span data-stu-id="b795b-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="b795b-191">Belirli tooAzure anahtar kasası değildir ancak bütünlük açısından buraya eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="b795b-191">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b795b-192">toocomplete hello Öğreticisi, hesap, hello kasası ve bu adımda kaydedeceğiniz Merhaba uygulaması tüm olmalıdır hello aynı Azure dizini.</span><span class="sxs-lookup"><span data-stu-id="b795b-192">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
> 
> 

<span data-ttu-id="b795b-193">Bir anahtar kasası kullanan uygulamaların, Azure Active Directory'den bir belirteç kullanarak kimlik doğrulama yapması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b795b-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="b795b-194">toodo Bu, hello hello uygulama sahibi ilk kaydetmeniz gerekir hello uygulama Azure Active Directory'de.</span><span class="sxs-lookup"><span data-stu-id="b795b-194">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="b795b-195">Kayıt Hello sonunda, hello uygulama sahibi aşağıdaki değerleri hello alır:</span><span class="sxs-lookup"><span data-stu-id="b795b-195">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="b795b-196">Bir **uygulama kimliği** (istemci kimliği olarak da bilinir) ve **kimlik doğrulama anahtarı** (olarak da bilinen hello paylaşılan gizlilik).</span><span class="sxs-lookup"><span data-stu-id="b795b-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="b795b-197">Merhaba uygulaması bu değerleri tooAzure Active Directory, tooget bir belirteç her ikisi de sunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b795b-197">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="b795b-198">Nasıl Merhaba uygulaması, bu hello uygulamaya bağlıdır toodo yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="b795b-198">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="b795b-199">Merhaba anahtar kasası örnek uygulaması hello uygulama sahibi bu değerleri hello app.config dosyasında ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b795b-199">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="b795b-200">Azure Active Directory'de tooregister hello uygulama:</span><span class="sxs-lookup"><span data-stu-id="b795b-200">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="b795b-201">Toohello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b795b-201">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="b795b-202">Hello solda tıklatın **Active Directory**ve ardından içinde kaydettiğiniz uygulamanızı hello dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="b795b-202">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="b795b-203">Merhaba seçmelisiniz hello ile anahtar kasanızı oluşturduğunuz Azure aboneliğini içeren aynı dizini.</span><span class="sxs-lookup"><span data-stu-id="b795b-203">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="b795b-204">Hangi dizine bu bilmiyorsanız, tıklatın olduğu **ayarları**ile anahtar kasanızı oluşturduğunuz hello aboneliği tanımlayın ve hello dizinin adını not hello hello son sütununda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b795b-204">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="b795b-205">**UYGULAMALAR**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b795b-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="b795b-206">Tooyour dizin hiçbir uygulama eklenmemişse bu sayfa yalnızca hello gösterecektir **bir uygulama ekleyin** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="b795b-206">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="b795b-207">Merhaba bağlantısına tıklayın veya alternatif olarak, hello tıklatabilirsiniz **ekleme** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="b795b-207">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="b795b-208">Merhaba, **uygulama Ekle** sihirbazında, hello **neler toodo istediğiniz?** sayfasında, **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b795b-208">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="b795b-209">Merhaba üzerinde **bize uygulamanızı anlatın** sayfasında uygulamanız için bir ad belirtin ve seçin **WEB uygulaması ve/veya WEB API** (Merhaba varsayılan).</span><span class="sxs-lookup"><span data-stu-id="b795b-209">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="b795b-210">Merhaba sonraki simgeyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b795b-210">Click hello Next icon.</span></span>
6. <span data-ttu-id="b795b-211">Merhaba üzerinde **uygulama özellikleri** sayfasında, hello belirtin **oturum açma URL** ve **uygulama kimliği URI'si** web uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="b795b-211">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="b795b-212">Uygulamanız bu değerlere sahip değilse değerleri bu adım için kendiniz belirleyebilirsiniz. (örneğin, her iki kutu için http://test1.contoso.com belirtebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="b795b-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="b795b-213">Bu sitelerin var olup olmaması önemli değildir; önemli olan her uygulama için bu hello uygulama kimliği URI'SİNİN dizininizdeki her uygulama için farklı olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="b795b-213">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="b795b-214">Merhaba directory Bu dize tooidentify uygulamanızı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b795b-214">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="b795b-215">Merhaba tam simgesi toosave değişikliklerinizi hello Sihirbazı'nı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b795b-215">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="b795b-216">Merhaba hızlı başlangıç sayfasında, tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="b795b-216">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="b795b-217">Toohello kaydırma **anahtarları** bölümünde, hello süre seçin ve ardından **KAYDETMEK**.</span><span class="sxs-lookup"><span data-stu-id="b795b-217">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="b795b-218">Merhaba sayfa yenilenir ve artık bir anahtar değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b795b-218">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="b795b-219">Bu anahtar değeri ve hello ile uygulamanızı yapılandırmanız gerekir **istemci kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="b795b-219">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="b795b-220">(Bu yapılandırma için yönergeler uygulamaya özgü olur.)</span><span class="sxs-lookup"><span data-stu-id="b795b-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="b795b-221">Bu sayfadan, sonraki adım tooset izinleri hello kasanızda kullanacağınız Hello istemci kimliği değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b795b-221">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="b795b-222">Merhaba uygulama toouse hello anahtar veya gizli yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="b795b-222">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="b795b-223">tooauthorize hello uygulama tooaccess hello anahtar veya gizli hello kasadaki kullanım hello `azure keyvault set-policy` komutu.</span><span class="sxs-lookup"><span data-stu-id="b795b-223">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="b795b-224">Örneğin, kasa adınız tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed istemci Kimliğine sahip ve tooauthorize hello uygulama toodecrypt ve oturum anahtarları, kasaya istediğiniz istediğiniz ContosoKeyVault ve hello uygulama ise, ardından hello çalıştırın Aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="b795b-224">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="b795b-225">Windows komut istemi üzerinde çalıştırıyorsanız, tek tırnak işaretleri çift tırnak işareti ile değiştirin ve ayrıca hello iç çift tırnak işareti kaçış gerekir.</span><span class="sxs-lookup"><span data-stu-id="b795b-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape hello internal double quotes.</span></span> <span data-ttu-id="b795b-226">Örneğin: "[\"şifresini\",\"oturum\"]".</span><span class="sxs-lookup"><span data-stu-id="b795b-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="b795b-227">Kasa adınız, aynı uygulama tooread gizli tooauthorize istiyorsanız, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b795b-227">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="b795b-228">Bir donanım güvenlik modülü (HSM) toouse istiyorsanız</span><span class="sxs-lookup"><span data-stu-id="b795b-228">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="b795b-229">Ek güvence için alma veya donanım güvenlik modülleri (HSM'ler)'hello HSM sınırını asla bırakın anahtarları oluştur.</span><span class="sxs-lookup"><span data-stu-id="b795b-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="b795b-230">Merhaba HSM'ler, FIPS 140-2 Düzey 2 doğrulanmasına şunlardır.</span><span class="sxs-lookup"><span data-stu-id="b795b-230">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="b795b-231">Bu gereksinim tooyou geçerli değilse bu bölümü atlayın ve çok gidin[hello anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="b795b-231">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="b795b-232">toocreate bu HSM korumalı anahtarları HSM korumalı anahtarları destekleyen bir kasa aboneliğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b795b-232">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="b795b-233">Merhaba keyvault oluşturduğunuzda, hello 'sku' parametresini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b795b-233">When you create hello keyvault, add hello 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="b795b-234">HSM korumalı anahtarlar toothis kasa ve yazılım korumalı anahtarlar (daha önce gösterildiği gibi) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b795b-234">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="b795b-235">toocreate HSM korumalı bir anahtar kümesi hello hedef parametre too'HSM':</span><span class="sxs-lookup"><span data-stu-id="b795b-235">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="b795b-236">.Pem dosyasını bilgisayarınızdaki komutu tooimport bir anahtar yükseltmesinin hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b795b-236">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="b795b-237">Bu komut hello anahtar hello anahtar kasası hizmetindeki Hsm'lere aktarır:</span><span class="sxs-lookup"><span data-stu-id="b795b-237">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="b795b-238">Merhaba sonraki komutu içe aktaran bir "kendi anahtarını getir" (BYOK) paketini.</span><span class="sxs-lookup"><span data-stu-id="b795b-238">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="b795b-239">Bu, yerel HSM'NİZDE anahtarınızı oluşturur ve hello HSM sınırını terk hello anahtar olmadan hello anahtar kasası hizmetindeki tooHSMs aktarım sağlar:</span><span class="sxs-lookup"><span data-stu-id="b795b-239">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="b795b-240">Daha ayrıntılı hakkında yönergeler için toogenerate bu BYOK paketini bkz [nasıl toouse HSM-Protected anahtarları Azure anahtar kasası ile](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="b795b-240">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="b795b-241">Merhaba anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme</span><span class="sxs-lookup"><span data-stu-id="b795b-241">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="b795b-242">Merhaba anahtar kasası ve başlangıç anahtarı veya içerdiği gizli artık ihtiyacınız varsa, hello azure keyvault silme komutunu kullanarak hello anahtar kasası silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b795b-242">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="b795b-243">Ya da hello anahtar kasasını ve bu gruba dahil diğer kaynakları içeren bir tüm Azure kaynak grubu silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b795b-243">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="b795b-244">Diğer Azure platformlar arası komut satırı arabirimi komutları</span><span class="sxs-lookup"><span data-stu-id="b795b-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="b795b-245">Diğer komutlar Azure anahtar kasası yönetmek için kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b795b-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="b795b-246">Bu komut tüm anahtarların ve seçilen özelliklerin tablolu bir görüntüsünü listeler:</span><span class="sxs-lookup"><span data-stu-id="b795b-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="b795b-247">Bu komut hello belirtilen anahtar için özelliklerin tam bir liste görüntüler:</span><span class="sxs-lookup"><span data-stu-id="b795b-247">This command displays a full list of properties for hello specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="b795b-248">Bu komut tüm gizli adların ve seçilen özelliklerin tablolu bir görüntüsünü listeler:</span><span class="sxs-lookup"><span data-stu-id="b795b-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="b795b-249">Örneği nasıl tooremove belirli bir anahtarı:</span><span class="sxs-lookup"><span data-stu-id="b795b-249">Here's an example of how tooremove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="b795b-250">Örneği nasıl tooremove belirli bir gizli anahtarın:</span><span class="sxs-lookup"><span data-stu-id="b795b-250">Here's an example of how tooremove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="b795b-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b795b-251">Next steps</span></span>
<span data-ttu-id="b795b-252">Programlama başvuruları için bkz: [Azure anahtar kasası Geliştirici Kılavuzu hello](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b795b-252">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

