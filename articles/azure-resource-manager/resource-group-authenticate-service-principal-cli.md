---
title: "Azure CLI ile Azure uygulaması için aaaCreate kimlik | Microsoft Docs"
description: "Toouse Azure CLI toocreate bir Azure Active Directory uygulaması ve hizmet sorumlusu ve rol tabanlı erişim, erişim tooresources nasıl kontrol açıklar. Bunu gösterir nasıl tooauthenticate uygulamayla bir parola veya sertifika."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="803c8-104">Bir hizmet asıl tooaccess kaynakları Azure CLI toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="803c8-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="803c8-105">Bir uygulama ya da tooaccess kaynakları gereken komut dosyası varsa, kendi kimlik bilgileriyle hello uygulamanın kimlik doğrulamasını ve hello uygulama için bir kimlik ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="803c8-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="803c8-106">Bu kimlik, bir hizmet sorumlusu bilinir.</span><span class="sxs-lookup"><span data-stu-id="803c8-106">This identity is known as a service principal.</span></span> <span data-ttu-id="803c8-107">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="803c8-107">This approach enables you to:</span></span>

* <span data-ttu-id="803c8-108">İzinleri kendi izinlerinizi farklı toohello uygulama kimliği atayın.</span><span class="sxs-lookup"><span data-stu-id="803c8-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="803c8-109">Genellikle, bu kısıtlı tooexactly hangi hello uygulamanın toodo ihtiyacı izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="803c8-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="803c8-110">Sertifika kimlik doğrulaması için Katılımsız betik yürütülürken kullanın.</span><span class="sxs-lookup"><span data-stu-id="803c8-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="803c8-111">Bu makale size nasıl gösterir toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset kendi kimlik bilgilerini ve kimlik altında bir uygulama toorun ayarlama.</span><span class="sxs-lookup"><span data-stu-id="803c8-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="803c8-112">Merhaba en son sürümünü yüklemek [Azure CLI 1.0](../cli-install-nodejs.md) toomake ortamınızı bu makaledeki örneklerde hello eşleştiğinden emin.</span><span class="sxs-lookup"><span data-stu-id="803c8-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="803c8-113">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="803c8-113">Required permissions</span></span>
<span data-ttu-id="803c8-114">toocomplete bu konuda, Azure Active Directory ve Azure aboneliğinize yeterli izniniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="803c8-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="803c8-115">Özellikle, mümkün toocreate hello Azure Active Directory içinde bir uygulama olabilir. ve hello hizmet asıl tooa rolünü atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="803c8-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="803c8-116">hesabınızın yeterli izinlere sahip olup olmadığı hello portalıdır hello en kolay yolu toocheck.</span><span class="sxs-lookup"><span data-stu-id="803c8-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="803c8-117">Bkz. [Portalda gerekli izinleri denetleme](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="803c8-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="803c8-118">Şimdi, tooa bölüm için ya da devam [parola](#create-service-principal-with-password) veya [sertifika](#create-service-principal-with-certificate) kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="803c8-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="803c8-119">Parola ile hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="803c8-119">Create service principal with password</span></span>
<span data-ttu-id="803c8-120">Bu bölümdeki hello adımları toocreate hello AD uygulaması bir parola ile gerçekleştirmek ve hello okuyucu rolü toohello hizmet sorumlusu atayın.</span><span class="sxs-lookup"><span data-stu-id="803c8-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="803c8-121">Tooyour hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="803c8-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="803c8-122">toocreate bir uygulama kimliği sağlayın hello uygulamasının hello adı ve parola hello komutu aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="803c8-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="803c8-123">Merhaba yeni hizmet sorumlusu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="803c8-123">hello new service principal is returned.</span></span> <span data-ttu-id="803c8-124">izin verme Hello nesne kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="803c8-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="803c8-125">Hizmet asıl adları Merhaba ile listelenmiş hello GUID açarken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="803c8-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="803c8-126">Merhaba bu GUID'dir hello uygulama kimliği ile aynı değeri. Merhaba örnek uygulamalarda, bu değer başvurulan tooas hello: `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="803c8-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="803c8-127">Merhaba, aboneliğinizin hizmet asıl izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="803c8-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="803c8-128">Bu örnekte, izni tooread hello Abonelikteki tüm kaynaklar veren hello hizmet asıl toohello okuyucu rolü, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="803c8-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="803c8-129">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="803c8-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="803c8-130">Merhaba objectID parametresi için hello Merhaba uygulaması oluşturulurken kullanılan nesne kimliği sağlayın.</span><span class="sxs-lookup"><span data-stu-id="803c8-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="803c8-131">Bu komutu çalıştırmadan önce biraz zaman hello yeni hizmet asıl toopropagate Azure Active Directory boyunca izin vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="803c8-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="803c8-132">Genellikle, bu komutları el ile çalıştırdığınızda görevleri arasında yeterli bir süre geçti.</span><span class="sxs-lookup"><span data-stu-id="803c8-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="803c8-133">Bir komut dosyasında bir adım toosleep hello komutları arasında eklemeniz gerekir (gibi `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="803c8-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="803c8-134">Belirten bir hata hello asıl hello dizininde yok görürseniz, hello komutu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="803c8-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="803c8-135">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="803c8-135">That's it!</span></span> <span data-ttu-id="803c8-136">AD uygulaması ve hizmet sorumlusu ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="803c8-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="803c8-137">Merhaba sonraki bölümde hello oturum toolog Azure CLI aracılığıyla nasıl kimlik bilgisi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="803c8-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="803c8-138">Kod uygulamanızda toouse hello kimlik bilgisi istiyorsanız, bu konu ile toocontinue gerekmez.</span><span class="sxs-lookup"><span data-stu-id="803c8-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="803c8-139">Toohello atlayabilirsiniz [örnek uygulamaları](#sample-applications) uygulama kimliği ve parola oturum açma örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="803c8-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="803c8-140">Azure CLI aracılığıyla kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="803c8-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="803c8-141">Şimdi, hello uygulaması tooperform işlemleri toolog de gerekir.</span><span class="sxs-lookup"><span data-stu-id="803c8-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="803c8-142">Bir hizmet sorumlusu oturum olduğunda, AD uygulamanız için hello dizininin tooprovide hello Kiracı kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="803c8-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="803c8-143">Bir kiracı, Azure Active Directory örneğidir.</span><span class="sxs-lookup"><span data-stu-id="803c8-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="803c8-144">şu anda kimliği doğrulanmış aboneliğiniz, kullanım için tooretrieve hello Kiracı kimliği:</span><span class="sxs-lookup"><span data-stu-id="803c8-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="803c8-145">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="803c8-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="803c8-146">Başka bir abonelik tooget hello Kiracı kimliği gerekiyorsa, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="803c8-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="803c8-147">Oturum açma için tooretrieve hello istemci kimliği toouse gerekiyorsa kullanın:</span><span class="sxs-lookup"><span data-stu-id="803c8-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="803c8-148">oturum açma için hello değeri toouse hello hizmet asıl adları listelenen hello GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="803c8-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="803c8-149">Asıl Hello hizmet olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="803c8-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="803c8-150">Merhaba parolayı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="803c8-150">You are prompted for hello password.</span></span> <span data-ttu-id="803c8-151">Merhaba AD uygulaması oluştururken, belirtilen hello parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="803c8-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="803c8-152">Şimdi, oluşturduğunuz hello hizmet sorumlusu için hello hizmet sorumlusu olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="803c8-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="803c8-153">Alternatif olarak, REST işlemlerini hello komut satırı toolog çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="803c8-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="803c8-154">Merhaba kimlik doğrulaması yanıttan hello erişim belirteci diğer işlemleri ile kullanılmak üzere alabilir.</span><span class="sxs-lookup"><span data-stu-id="803c8-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="803c8-155">REST işlemlerini çağırarak hello erişim belirteci alma bir örnek için bkz: [bir erişim belirteci oluşturma](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="803c8-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="803c8-156">Sertifika ile hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="803c8-156">Create service principal with certificate</span></span>
<span data-ttu-id="803c8-157">Bu bölümde, hello adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="803c8-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="803c8-158">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="803c8-158">create a self-signed certificate</span></span>
* <span data-ttu-id="803c8-159">hello sertifika ve hello hizmet sorumlusu Hello AD uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="803c8-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="803c8-160">Merhaba okuyucu rolü toohello hizmet sorumlusu atayın</span><span class="sxs-lookup"><span data-stu-id="803c8-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="803c8-161">Aşağıdaki adımları toocomplete olmalıdır [OpenSSL](http://www.openssl.org/) yüklü.</span><span class="sxs-lookup"><span data-stu-id="803c8-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="803c8-162">Kendinden imzalı bir sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="803c8-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="803c8-163">Önceki adımda oluşturulan iki dosya - privkey.pem ve cert.pem hello.</span><span class="sxs-lookup"><span data-stu-id="803c8-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="803c8-164">Merhaba ortak ve özel anahtarlar, tek bir dosya halinde birleştirin.</span><span class="sxs-lookup"><span data-stu-id="803c8-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="803c8-165">Açık hello **examplecert.pem** dosya ve hello karakter arasında uzun bir sıra arayın **---başlangıç sertifika---** ve **---son SERTİFİKAYI---**.</span><span class="sxs-lookup"><span data-stu-id="803c8-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="803c8-166">Merhaba sertifika verileri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="803c8-166">Copy hello certificate data.</span></span> <span data-ttu-id="803c8-167">Hizmet sorumlusu hello oluştururken, bu verileri bir parametre olarak geçirir.</span><span class="sxs-lookup"><span data-stu-id="803c8-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="803c8-168">Tooyour hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="803c8-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="803c8-169">toocreate hello hizmet sorumlusu hello komutu aşağıdaki gösterildiği gibi hello uygulamanın ve hello sertifika verileri hello adı girin:</span><span class="sxs-lookup"><span data-stu-id="803c8-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="803c8-170">Merhaba yeni hizmet sorumlusu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="803c8-170">hello new service principal is returned.</span></span> <span data-ttu-id="803c8-171">izin verme Hello nesne kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="803c8-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="803c8-172">Hizmet asıl adları Merhaba ile listelenmiş hello GUID açarken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="803c8-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="803c8-173">Merhaba bu GUID'dir hello uygulama kimliği ile aynı değeri. Merhaba örnek uygulamalarda, bu değer başvurulan tooas hello istemci kimliği:</span><span class="sxs-lookup"><span data-stu-id="803c8-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="803c8-174">Merhaba, aboneliğinizin hizmet asıl izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="803c8-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="803c8-175">Bu örnekte, izni tooread hello Abonelikteki tüm kaynaklar veren hello hizmet asıl toohello okuyucu rolü, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="803c8-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="803c8-176">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="803c8-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="803c8-177">Merhaba objectID parametresi için hello Merhaba uygulaması oluşturulurken kullanılan nesne kimliği sağlayın.</span><span class="sxs-lookup"><span data-stu-id="803c8-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="803c8-178">Bu komutu çalıştırmadan önce biraz zaman hello yeni hizmet asıl toopropagate Azure Active Directory boyunca izin vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="803c8-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="803c8-179">Genellikle, bu komutları el ile çalıştırdığınızda görevleri arasında yeterli bir süre geçti.</span><span class="sxs-lookup"><span data-stu-id="803c8-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="803c8-180">Bir komut dosyasında bir adım toosleep hello komutları arasında eklemeniz gerekir (gibi `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="803c8-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="803c8-181">Belirten bir hata hello asıl hello dizininde yok görürseniz, hello komutu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="803c8-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="803c8-182">Otomatik Azure CLI komut dosyası aracılığıyla sertifikası sağlayın</span><span class="sxs-lookup"><span data-stu-id="803c8-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="803c8-183">Şimdi, hello uygulaması tooperform işlemleri toolog de gerekir.</span><span class="sxs-lookup"><span data-stu-id="803c8-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="803c8-184">Bir hizmet sorumlusu oturum olduğunda, AD uygulamanız için hello dizininin tooprovide hello Kiracı kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="803c8-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="803c8-185">Bir kiracı, Azure Active Directory örneğidir.</span><span class="sxs-lookup"><span data-stu-id="803c8-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="803c8-186">şu anda kimliği doğrulanmış aboneliğiniz, kullanım için tooretrieve hello Kiracı kimliği:</span><span class="sxs-lookup"><span data-stu-id="803c8-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="803c8-187">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="803c8-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="803c8-188">Başka bir abonelik tooget hello Kiracı kimliği gerekiyorsa, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="803c8-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="803c8-189">tooretrieve sertifika parmak izi hello ve gereksiz karakterleri kaldırmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="803c8-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="803c8-190">Hangi parmak izi değeri benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="803c8-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="803c8-191">Oturum açma için tooretrieve hello istemci kimliği toouse gerekiyorsa kullanın:</span><span class="sxs-lookup"><span data-stu-id="803c8-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="803c8-192">oturum açma için hello değeri toouse hello hizmet asıl adları listelenen hello GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="803c8-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="803c8-193">Asıl Hello hizmet olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="803c8-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="803c8-194">Şimdi hello hizmet sorumlusu hello oluşturulan Azure Active Directory uygulaması için olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="803c8-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="803c8-195">Kimlik bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="803c8-195">Change credentials</span></span>

<span data-ttu-id="803c8-196">kimlik bilgileri güvenliğinin aşılması veya bir kimlik bilgisi sona erme nedeniyle, bir AD uygulaması toochange hello kullanın `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="803c8-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="803c8-197">toochange bir parola kullanın:</span><span class="sxs-lookup"><span data-stu-id="803c8-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="803c8-198">toochange sertifika değerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="803c8-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="803c8-199">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="803c8-199">Debug</span></span>

<span data-ttu-id="803c8-200">Bir hizmet sorumlusu oluşturma sırasında aşağıdaki hatalar hello karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="803c8-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="803c8-201">**"Authentication_Unauthorized"** veya **"abonelik hello bağlamda bulunamadı."**</span><span class="sxs-lookup"><span data-stu-id="803c8-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="803c8-202">-Hesabınızı hello olmadığında bu hatayı gördüğünüz [gerekli izinleri](#required-permissions) hello Azure Active Directory tooregister bir uygulama üzerinde.</span><span class="sxs-lookup"><span data-stu-id="803c8-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="803c8-203">Yalnızca yönetici kullanıcıların Azure Active Directory'de uygulamaları kaydedebilirsiniz ve hesabınızın bir yönetici değil, bu hata genellikle, bakın Yönetici tooeither atamak, tooan Yönetici rolü ya da tooenable kullanıcılar tooregister uygulamaları isteyin.</span><span class="sxs-lookup"><span data-stu-id="803c8-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="803c8-204">Hesabınızı **"yetkilendirme tooperform eylemi 'Microsoft.Authorization/roleAssignments/write' kapsamı üzerinde '/ subscriptions / {GUID}' yok."**  -Hesabınızı rol tooan kimlik yeterli izinleri tooassign olmadığında bu hatayı bakın.</span><span class="sxs-lookup"><span data-stu-id="803c8-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="803c8-205">Abonelik Yöneticisi tooadd isteyin, tooUser erişim Yönetici rolü.</span><span class="sxs-lookup"><span data-stu-id="803c8-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="803c8-206">Örnek uygulamalar</span><span class="sxs-lookup"><span data-stu-id="803c8-206">Sample applications</span></span>
<span data-ttu-id="803c8-207">Farklı platformlarda üzerinden hello uygulama olarak oturum açma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="803c8-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="803c8-208">.NET</span><span class="sxs-lookup"><span data-stu-id="803c8-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="803c8-209">Java</span><span class="sxs-lookup"><span data-stu-id="803c8-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="803c8-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="803c8-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="803c8-211">Python</span><span class="sxs-lookup"><span data-stu-id="803c8-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="803c8-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="803c8-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="803c8-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="803c8-213">Next steps</span></span>
* <span data-ttu-id="803c8-214">Kaynakları yönetmek için Azure'da bir uygulamayı tümleştirme ayrıntılı adımlar için bkz: [Geliştirici Kılavuzu tooauthorization hello Azure Kaynak Yöneticisi API'si ile](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="803c8-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="803c8-215">Sertifikalar ve Azure CLI kullanma hakkında daha fazla bilgi tooget bkz [sertifika tabanlı kimlik doğrulaması Azure hizmet asıl adı ile Linux komut satırından](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="803c8-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="803c8-216">Verilen veya toousers reddedilen kullanılabilir eylemler listesi için bkz: [Azure Resource Manager kaynak sağlayıcısı işlemleri](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="803c8-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
