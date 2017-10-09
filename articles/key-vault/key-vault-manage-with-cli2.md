---
title: "Azure anahtar kasası CLI kullanarak aaaManage | Microsoft Docs"
description: "Bu öğretici tooautomate ortak görevler anahtar kasasına hello CLI 2.0 kullanarak"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="a7387-103">Anahtar kasası CLI 2.0 kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="a7387-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="a7387-104">Azure Anahtar Kasası çoğu bölgede kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7387-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="a7387-105">Daha fazla bilgi için bkz: Merhaba [anahtar kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="a7387-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="a7387-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="a7387-106">Introduction</span></span>
<span data-ttu-id="a7387-107">Size Bu öğretici toohelp kullanmak ile Azure anahtar kasası toocreate toostore Azure'da sağlamlaştırılmış bir kapsayıcı (bir kasa) başlatıldı ve şifreleme anahtarları ve gizli anahtarları azure'da yönetin.</span><span class="sxs-lookup"><span data-stu-id="a7387-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="a7387-108">Bu, Azure platformlar arası komut satırı arabirimi toocreate kullanarak hello sürecinde bir anahtar ya da sonra bir Azure uygulamasıyla kullanabileceğiniz parola içeren bir kasa yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a7387-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="a7387-109">Bunu daha sonra nasıl bir uygulama daha sonra bu anahtarı veya parolayı kullanabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="a7387-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="a7387-110">**Zaman toocomplete tahmini:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="a7387-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="a7387-111">Bu öğretici nasıl toowrite hello nasıl tooauthorize uygulama toouse bir anahtar veya gizli hello anahtarında kasa gösteren hello adımları içeren Azure uygulamanızı yönergeleri içermez.</span><span class="sxs-lookup"><span data-stu-id="a7387-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="a7387-112">Bu öğretici kullanır, en son Azure CLI 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="a7387-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="a7387-113">Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a7387-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7387-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a7387-114">Prerequisites</span></span>
<span data-ttu-id="a7387-115">toocomplete Bu öğreticiyi izleyerek hello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="a7387-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="a7387-116">Abonelik tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a7387-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="a7387-117">Bir yoksa için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="a7387-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="a7387-118">Komut satırı arabirimi sürüm 2.0 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="a7387-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="a7387-119">tooinstall hello en son sürümünü ve tooyour Azure aboneliğine bağlanma Bkz [hello Azure platformlar arası komut satırı arabirimi 2.0 yükleyip](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a7387-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="a7387-120">Yapılandırılmış toouse hello anahtar ya da Bu öğreticide oluşturduğunuz parola olacak bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="a7387-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="a7387-121">Bir örnek uygulama hello kullanılabilir [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="a7387-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="a7387-122">Yönergeler için Benioku dosyası ile birlikte gelen hello bakın.</span><span class="sxs-lookup"><span data-stu-id="a7387-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="a7387-123">Azure platformlar arası komut satırı arabirimi ile ilgili Yardım alma</span><span class="sxs-lookup"><span data-stu-id="a7387-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="a7387-124">Bu öğretici, başlangıç komut satırı arabirimi (Bash, Terminal, komut istemi) bildiğinizi varsayar</span><span class="sxs-lookup"><span data-stu-id="a7387-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="a7387-125">Merhaba--Yardım veya -h parametresi olabilir tooview Yardım belirli komutları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a7387-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="a7387-126">Alternatif olarak, aynı bilgileri hello azure Yardım [komut biçimi de kullanılan tooreturn olabilir] [Seçenekler] hello.</span><span class="sxs-lookup"><span data-stu-id="a7387-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="a7387-127">Örneğin, tüm dönüş hello aşağıdaki komutları hello aynı bilgileri:</span><span class="sxs-lookup"><span data-stu-id="a7387-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="a7387-128">Toohelp kullanarak--zaman şüpheli bir komut tarafından gerekli hello parametreleri hakkında başvuru Yardım, -h veya [komut] Yardım az.</span><span class="sxs-lookup"><span data-stu-id="a7387-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="a7387-129">Ayrıca, Azure Resource Manager Azure platformlar arası komut satırı arabirimi ile tanıdık öğreticileri tooget aşağıdaki hello okuyabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a7387-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="a7387-130">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="a7387-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="a7387-131">Azure CLI 2.0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a7387-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="a7387-132">Tooyour abonelikleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="a7387-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="a7387-133">bir kuruluş hesabı, komutu aşağıdaki kullanım hello kullanarak toolog:</span><span class="sxs-lookup"><span data-stu-id="a7387-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="a7387-134">veya, toolog etkileşimli olarak yazarak istiyorsanız</span><span class="sxs-lookup"><span data-stu-id="a7387-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="a7387-135">Birden çok aboneliğiniz varsa ve Azure anahtar kasası için toospecify belirli bir toouse istediğiniz, hesabınız için toosee hello abonelikleri aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="a7387-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="a7387-136">Ardından, toospecify hello abonelik toouse, türü:</span><span class="sxs-lookup"><span data-stu-id="a7387-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="a7387-137">Azure platformlar arası komut satırı arabirimi yapılandırma hakkında daha fazla bilgi için bkz: [Azure CLI yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a7387-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="a7387-138">Yeni bir kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7387-138">Create a new resource group</span></span>
<span data-ttu-id="a7387-139">Azure Kaynak Yöneticisi'ni kullanırken, tüm ilgili kaynaklar bir kaynak grubu içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a7387-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="a7387-140">Bu öğretici için yeni bir kaynak grubu 'ContosoResourceGroup' oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="a7387-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="a7387-141">Merhaba ilk parametre kaynak grubu adı ve hello ikinci parametre başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="a7387-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="a7387-142">Konum için hello komutunu `az account list-locations` tooidentify nasıl toospecify bir alternatif konum toohello biri bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="a7387-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="a7387-143">Daha fazla bilgiye ihtiyacınız varsa, yazın: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="a7387-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="a7387-144">Merhaba anahtar kasası kaynak sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="a7387-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="a7387-145">Bu anahtar kasası kaynak sağlayıcısı aboneliğinizde kayıtlı olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="a7387-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="a7387-146">Bu, yalnızca abonelik başına bir kez yapılır toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7387-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="a7387-147">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7387-147">Create a key vault</span></span>
<span data-ttu-id="a7387-148">Kullanım hello `az keyvault create` komutu toocreate bir anahtar kasası.</span><span class="sxs-lookup"><span data-stu-id="a7387-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="a7387-149">Bu komut dosyasını üç zorunlu parametreye sahiptir: bir kaynak grubu adı, anahtar kasası adı ve hello coğrafi konum.</span><span class="sxs-lookup"><span data-stu-id="a7387-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="a7387-150">Örneğin, ContosoKeyVault, ContosoResourceGroup hello kaynak grubu adını ve Doğu Asya konumunu hello hello kasa adını kullanırsanız yazın:</span><span class="sxs-lookup"><span data-stu-id="a7387-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="a7387-151">Bu komutun çıktısı Hello hello yeni oluşturduğunuz anahtar kasasının özelliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a7387-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="a7387-152">Merhaba iki en önemli özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a7387-152">hello two most important properties are:</span></span>

* <span data-ttu-id="a7387-153">**ad**: hello örnekte ContosoKeyVault budur.</span><span class="sxs-lookup"><span data-stu-id="a7387-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="a7387-154">Bu adı diğer anahtar kasası komutları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a7387-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="a7387-155">**vaultUri**: hello örnekte https://contosokeyvault.vault.azure.net budur.</span><span class="sxs-lookup"><span data-stu-id="a7387-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="a7387-156">REST API'si aracılığıyla kasanızı kullanan uygulamaların bu URI'yi kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7387-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="a7387-157">Bu anahtarı üzerindeki herhangi bir işlem yetkili tooperform kasa artık Azure hesabınız bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="a7387-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="a7387-158">Henüz başka kimse yetkilendirilmedi.</span><span class="sxs-lookup"><span data-stu-id="a7387-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="a7387-159">Bir anahtar veya gizli toohello anahtar kasası ekleme</span><span class="sxs-lookup"><span data-stu-id="a7387-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="a7387-160">Sizin için Azure anahtar kasası toocreate yazılımla korunan anahtardan istiyorsanız, hello kullanın `az key create` komut ve hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="a7387-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="a7387-161">Ancak, yerel dosya tooupload tooAzure anahtar kasası istediğiniz softkey.pem adlı bir dosya olarak kaydedilmiş bir .pem dosyasını mevcut bir anahtarı varsa, hello tooimport hello anahtar aşağıdaki hello yazın. PEM dosyası yazılım hello anahtar kasası hizmeti ile Merhaba anahtarı korur:</span><span class="sxs-lookup"><span data-stu-id="a7387-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="a7387-162">Artık oluşturduğunuz veya tooAzure anahtar kasası URI'sini kullanarak karşıya hello anahtar başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7387-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="a7387-163">Kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello geçerli sürümü almak ve kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget bu belirli sürümü.</span><span class="sxs-lookup"><span data-stu-id="a7387-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="a7387-164">tooadd SQLPassword adlı bir parola olduğu ve Pa$ $w0rd tooAzure anahtar kasası, aşağıdaki türü hello hello değerine sahip bir gizli toohello Kasası:</span><span class="sxs-lookup"><span data-stu-id="a7387-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="a7387-165">Artık bu parolayı URI'sini kullanarak tooAzure anahtar kasası, eklenen başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7387-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="a7387-166">Kullanmak **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello geçerli sürümü almak ve kullanmak **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget bu belirli sürümü.</span><span class="sxs-lookup"><span data-stu-id="a7387-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="a7387-167">Şimdi hello anahtar veya yeni oluşturduğunuz gizli görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="a7387-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="a7387-168">tooview anahtar, türünüz:`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="a7387-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="a7387-169">tooview, gizli, türü:`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="a7387-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="a7387-170">Bir uygulamayı Azure Active Directory'ye kaydetme</span><span class="sxs-lookup"><span data-stu-id="a7387-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="a7387-171">Bu adım genellikle ayrı bir bilgisayarda bir geliştirici tarafından yapılır.</span><span class="sxs-lookup"><span data-stu-id="a7387-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="a7387-172">Belirli tooAzure anahtar kasası değildir ancak bütünlük açısından buraya eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="a7387-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7387-173">toocomplete hello Öğreticisi, hesap, hello kasası ve bu adımda kaydedeceğiniz Merhaba uygulaması tüm olmalıdır hello aynı Azure dizini.</span><span class="sxs-lookup"><span data-stu-id="a7387-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="a7387-174">Bir anahtar kasası kullanan uygulamaların, Azure Active Directory'den bir belirteç kullanarak kimlik doğrulama yapması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7387-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="a7387-175">toodo Bu, hello hello uygulama sahibi ilk kaydetmeniz gerekir hello uygulama Azure Active Directory'de.</span><span class="sxs-lookup"><span data-stu-id="a7387-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="a7387-176">Kayıt Hello sonunda, hello uygulama sahibi aşağıdaki değerleri hello alır:</span><span class="sxs-lookup"><span data-stu-id="a7387-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="a7387-177">Bir **uygulama kimliği** (istemci kimliği olarak da bilinir) ve **kimlik doğrulama anahtarı** (olarak da bilinen hello paylaşılan gizlilik).</span><span class="sxs-lookup"><span data-stu-id="a7387-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="a7387-178">Merhaba uygulaması bu değerleri tooAzure Active Directory, tooget bir belirteç her ikisi de sunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7387-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="a7387-179">Nasıl Merhaba uygulaması, bu hello uygulamaya bağlıdır toodo yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a7387-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="a7387-180">Merhaba anahtar kasası örnek uygulaması hello uygulama sahibi bu değerleri hello app.config dosyasında ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a7387-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="a7387-181">Azure Active Directory'de tooregister hello uygulama:</span><span class="sxs-lookup"><span data-stu-id="a7387-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="a7387-182">Toohello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a7387-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="a7387-183">Hello solda tıklatın **Azure Active Directory**ve ardından içinde kaydettiğiniz uygulamanızı hello dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="a7387-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="a7387-184">Merhaba seçmelisiniz hello ile anahtar kasanızı oluşturduğunuz Azure aboneliğini içeren aynı dizini.</span><span class="sxs-lookup"><span data-stu-id="a7387-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="a7387-185">Hangi dizine bu bilmiyorsanız, tıklatın olduğu **ayarları**ile anahtar kasanızı oluşturduğunuz hello aboneliği tanımlayın ve hello dizinin adını not hello hello son sütununda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a7387-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="a7387-186">**UYGULAMALAR**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a7387-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="a7387-187">Tooyour dizin hiçbir uygulama eklenmemişse bu sayfa yalnızca hello gösterecektir **bir uygulama ekleyin** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="a7387-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="a7387-188">Merhaba bağlantısına tıklayın veya alternatif olarak, hello tıklatabilirsiniz **ekleme** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="a7387-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="a7387-189">Merhaba, **uygulama Ekle** sihirbazında, hello **neler toodo istediğiniz?** sayfasında, **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a7387-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="a7387-190">Merhaba üzerinde **bize uygulamanızı anlatın** sayfasında uygulamanız için bir ad belirtin ve seçin **WEB uygulaması ve/veya WEB API** (Merhaba varsayılan).</span><span class="sxs-lookup"><span data-stu-id="a7387-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="a7387-191">Merhaba sonraki simgeyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a7387-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="a7387-192">Merhaba üzerinde **uygulama özellikleri** sayfasında, hello belirtin **oturum açma URL** ve **uygulama kimliği URI'si** web uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="a7387-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="a7387-193">Uygulamanız bu değerlere sahip değilse değerleri bu adım için kendiniz belirleyebilirsiniz. (örneğin, her iki kutu için http://test1.contoso.com belirtebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="a7387-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="a7387-194">Bu sitelerin var olup olmaması önemli değildir; önemli olan her uygulama için bu hello uygulama kimliği URI'SİNİN dizininizdeki her uygulama için farklı olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a7387-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="a7387-195">Merhaba directory Bu dize tooidentify uygulamanızı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a7387-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="a7387-196">Merhaba tam simgesi toosave değişikliklerinizi hello Sihirbazı'nı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a7387-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="a7387-197">Merhaba hızlı başlangıç sayfasında, tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="a7387-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="a7387-198">Toohello kaydırma **anahtarları** bölümünde, hello süre seçin ve ardından **KAYDETMEK**.</span><span class="sxs-lookup"><span data-stu-id="a7387-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="a7387-199">Merhaba sayfa yenilenir ve artık bir anahtar değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a7387-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="a7387-200">Bu anahtar değeri ve hello ile uygulamanızı yapılandırmanız gerekir **istemci kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="a7387-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="a7387-201">(Bu yapılandırma için yönergeler uygulamaya özgü olur.)</span><span class="sxs-lookup"><span data-stu-id="a7387-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="a7387-202">Bu sayfadan, sonraki adım tooset izinleri hello kasanızda kullanacağınız Hello istemci kimliği değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a7387-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="a7387-203">Merhaba uygulama toouse hello anahtar veya gizli yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="a7387-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="a7387-204">tooauthorize hello uygulama tooaccess hello anahtar veya gizli hello kasadaki kullanım hello `az keyvault set-policy` komutu.</span><span class="sxs-lookup"><span data-stu-id="a7387-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="a7387-205">Örneğin, kasa adınız tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed istemci Kimliğine sahip ve tooauthorize hello uygulama toodecrypt ve oturum anahtarları, kasaya istediğiniz istediğiniz ContosoKeyVault ve hello uygulama ise, ardından hello çalıştırın Aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="a7387-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="a7387-206">Kasa adınız, aynı uygulama tooread gizli tooauthorize istiyorsanız, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a7387-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="a7387-207">Bir donanım güvenlik modülü (HSM) toouse istiyorsanız</span><span class="sxs-lookup"><span data-stu-id="a7387-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="a7387-208">Ek güvence için alma veya donanım güvenlik modülleri (HSM'ler)'hello HSM sınırını asla bırakın anahtarları oluştur.</span><span class="sxs-lookup"><span data-stu-id="a7387-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="a7387-209">Merhaba HSM'ler, FIPS 140-2 Düzey 2 doğrulanmasına şunlardır.</span><span class="sxs-lookup"><span data-stu-id="a7387-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="a7387-210">Bu gereksinim tooyou geçerli değilse bu bölümü atlayın ve çok gidin[hello anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="a7387-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="a7387-211">toocreate bu HSM korumalı anahtarları HSM korumalı anahtarları destekleyen bir kasa aboneliğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7387-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="a7387-212">Merhaba keyvault oluşturduğunuzda, hello 'sku' parametresini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a7387-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="a7387-213">HSM korumalı anahtarlar toothis kasa ve yazılım korumalı anahtarlar (daha önce gösterildiği gibi) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7387-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="a7387-214">toocreate HSM korumalı bir anahtar kümesi hello hedef parametre too'HSM':</span><span class="sxs-lookup"><span data-stu-id="a7387-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="a7387-215">.Pem dosyasını bilgisayarınızdaki komutu tooimport bir anahtar yükseltmesinin hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7387-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="a7387-216">Bu komut hello anahtar hello anahtar kasası hizmetindeki Hsm'lere aktarır:</span><span class="sxs-lookup"><span data-stu-id="a7387-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="a7387-217">Merhaba sonraki komutu içe aktaran bir "kendi anahtarını getir" (BYOK) paketini.</span><span class="sxs-lookup"><span data-stu-id="a7387-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="a7387-218">Bu, yerel HSM'NİZDE anahtarınızı oluşturur ve hello HSM sınırını terk hello anahtar olmadan hello anahtar kasası hizmetindeki tooHSMs aktarım sağlar:</span><span class="sxs-lookup"><span data-stu-id="a7387-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="a7387-219">Daha ayrıntılı hakkında yönergeler için toogenerate bu BYOK paketini bkz [nasıl toouse HSM-Protected anahtarları Azure anahtar kasası ile](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="a7387-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="a7387-220">Merhaba anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme</span><span class="sxs-lookup"><span data-stu-id="a7387-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="a7387-221">Merhaba anahtar kasası ve başlangıç anahtarı veya içerdiği gizli artık ihtiyacınız varsa, hello kullanarak hello anahtar kasası silebilirsiniz `az keyvault delete` komutu:</span><span class="sxs-lookup"><span data-stu-id="a7387-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="a7387-222">Ya da hello anahtar kasasını ve bu gruba dahil diğer kaynakları içeren bir tüm Azure kaynak grubu silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a7387-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="a7387-223">Diğer Azure platformlar arası komut satırı arabirimi komutları</span><span class="sxs-lookup"><span data-stu-id="a7387-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="a7387-224">Diğer komutlar Azure anahtar kasası yönetmek için kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a7387-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="a7387-225">Bu komut tüm anahtarların ve seçilen özelliklerin tablolu bir görüntüsünü listeler:</span><span class="sxs-lookup"><span data-stu-id="a7387-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="a7387-226">az keyvault anahtar listesi--kasa adı 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="a7387-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="a7387-227">Bu komut hello belirtilen anahtar için özelliklerin tam bir liste görüntüler:</span><span class="sxs-lookup"><span data-stu-id="a7387-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="a7387-228">az keyvault anahtar Göster--kasa adı 'ContosoKeyVault'--ad 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="a7387-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="a7387-229">Bu komut tüm gizli adların ve seçilen özelliklerin tablolu bir görüntüsünü listeler:</span><span class="sxs-lookup"><span data-stu-id="a7387-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="a7387-230">az keyvault gizli listesi--kasa adı 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="a7387-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="a7387-231">Örneği nasıl tooremove belirli bir anahtarı:</span><span class="sxs-lookup"><span data-stu-id="a7387-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="a7387-232">az keyvault anahtarını silmek--kasa adı 'ContosoKeyVault'--ad 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="a7387-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="a7387-233">Örneği nasıl tooremove belirli bir gizli anahtarın:</span><span class="sxs-lookup"><span data-stu-id="a7387-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="a7387-234">az keyvault gizli anahtarı silme--kasa adı 'ContosoKeyVault'--ad 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="a7387-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="a7387-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7387-235">Next steps</span></span>
<span data-ttu-id="a7387-236">Anahtar kasası komutları için tam Azure CLI başvuru için bkz: [anahtar kasası CLI başvurusu](/cli/azure/keyvault)</span><span class="sxs-lookup"><span data-stu-id="a7387-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="a7387-237">Programlama başvuruları için bkz: [Azure anahtar kasası Geliştirici Kılavuzu hello](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="a7387-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
