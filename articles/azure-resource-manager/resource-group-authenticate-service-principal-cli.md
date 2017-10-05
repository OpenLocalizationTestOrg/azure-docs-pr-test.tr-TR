---
title: "Azure CLI ile Azure uygulama kimliği oluşturma | Microsoft Docs"
description: "Bir Azure Active Directory uygulaması ve hizmet sorumlusu oluşturmak ve rol tabanlı erişim denetimi aracılığıyla kaynaklara erişim izni için Azure CLI kullanmayı açıklar. Uygulama ile bir parola veya sertifika kimlik doğrulaması yapmayı gösterir."
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
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="dca51-104">Kaynaklara erişmek üzere hizmet sorumlusu oluşturmak için Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="dca51-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="dca51-105">Bir uygulama ya da kaynaklara erişmek için gereken komut dosyası varsa, uygulamanın kendi kimlik bilgileriyle kimlik doğrulamasını ve uygulama için bir kimlik ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dca51-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="dca51-106">Bu kimlik, bir hizmet sorumlusu bilinir.</span><span class="sxs-lookup"><span data-stu-id="dca51-106">This identity is known as a service principal.</span></span> <span data-ttu-id="dca51-107">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="dca51-107">This approach enables you to:</span></span>

* <span data-ttu-id="dca51-108">Kendi izinlerinizi farklı uygulama kimliği için izinleri atayın.</span><span class="sxs-lookup"><span data-stu-id="dca51-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="dca51-109">Genellikle, bu izinleri tam olarak hangi uygulama yapması gereken için kısıtlanır.</span><span class="sxs-lookup"><span data-stu-id="dca51-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="dca51-110">Sertifika kimlik doğrulaması için Katılımsız betik yürütülürken kullanın.</span><span class="sxs-lookup"><span data-stu-id="dca51-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="dca51-111">Bu makalede nasıl kullanılacağı gösterilmektedir [Azure CLI 1.0](../cli-install-nodejs.md) bir uygulamanın kendi kimlik bilgilerini ve kimlik altında çalışmasına ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="dca51-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="dca51-112">En son sürümünü yüklemek [Azure CLI 1.0](../cli-install-nodejs.md) ortamınızla eşleşen bu makaledeki örneklerde emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="dca51-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="dca51-113">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="dca51-113">Required permissions</span></span>
<span data-ttu-id="dca51-114">Bu konuda tamamlamak için Azure Active Directory ve Azure aboneliğinize yeterli izniniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca51-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="dca51-115">Özellikle, Azure Active Directory'de bir uygulama oluşturun ve hizmet sorumlusu rol atama mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca51-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="dca51-116">Hesabınızın yeterli izinlere sahip olup olmadığını denetlemenin en kolay yolu portalı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="dca51-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="dca51-117">Bkz. [Portalda gerekli izinleri denetleme](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="dca51-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="dca51-118">Şimdi, bir bölüm için ya da devam [parola](#create-service-principal-with-password) veya [sertifika](#create-service-principal-with-certificate) kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="dca51-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="dca51-119">Parola ile hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca51-119">Create service principal with password</span></span>
<span data-ttu-id="dca51-120">Bu bölümde, bir parola ile AD uygulaması oluşturmak için aşağıdaki adımları gerçekleştirin ve hizmet sorumlusu okuyucu rolüne atayın.</span><span class="sxs-lookup"><span data-stu-id="dca51-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="dca51-121">Hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dca51-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="dca51-122">Bir uygulama kimliği oluşturmak için aşağıdaki komutta gösterildiği gibi uygulama ve bir parola adını sağlayın:</span><span class="sxs-lookup"><span data-stu-id="dca51-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="dca51-123">Yeni hizmet sorumlusunu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="dca51-123">The new service principal is returned.</span></span> <span data-ttu-id="dca51-124">İzin verme nesne kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dca51-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="dca51-125">Hizmet asıl adları ile listelenen GUID açarken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dca51-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="dca51-126">Uygulama kimliği ile aynı değere GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="dca51-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="dca51-127">Örnek uygulamalarda, bu değer olarak adlandırılır `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="dca51-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
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

3. <span data-ttu-id="dca51-128">Aboneliğiniz için hizmet asıl izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="dca51-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="dca51-129">Bu örnekte, hizmet sorumlusu Abonelikteki tüm kaynaklar okuma izni verir okuyucu rolüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dca51-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="dca51-130">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="dca51-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="dca51-131">ObjectID parametresi için uygulama oluştururken kullanılan nesne kimliği sağlayın.</span><span class="sxs-lookup"><span data-stu-id="dca51-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="dca51-132">Bu komutu çalıştırmadan önce süre Azure Active Directory yaymak yeni bir hizmet sorumlusu için izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="dca51-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="dca51-133">Genellikle, bu komutları el ile çalıştırdığınızda görevleri arasında yeterli bir süre geçti.</span><span class="sxs-lookup"><span data-stu-id="dca51-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="dca51-134">Bir komut dosyası komut arasında uyku moduna bir adımı eklemeniz gerekir (gibi `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="dca51-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="dca51-135">Asıl dizinde yok bildiren bir hata görürseniz, komutu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dca51-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="dca51-136">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="dca51-136">That's it!</span></span> <span data-ttu-id="dca51-137">AD uygulaması ve hizmet sorumlusu ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="dca51-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="dca51-138">Sonraki bölümde Azure CLI kimlik bilgilerinizle oturum gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="dca51-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="dca51-139">Kimlik bilgisi kodu uygulamanızda kullanmak istiyorsanız, bu konu ile devam etmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="dca51-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="dca51-140">Atlayabilirsiniz [örnek uygulamaları](#sample-applications) uygulama kimliği ve parola oturum açma örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="dca51-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="dca51-141">Azure CLI aracılığıyla kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="dca51-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="dca51-142">Şimdi, işlemleri gerçekleştirmek için uygulama olarak oturum açmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca51-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="dca51-143">Bir hizmet sorumlusu oturum olduğunda, Kiracı kimliği dizininin AD uygulamanız için sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca51-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="dca51-144">Bir kiracı, Azure Active Directory örneğidir.</span><span class="sxs-lookup"><span data-stu-id="dca51-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="dca51-145">Şu anda kimliği doğrulanmış aboneliğinizin Kiracı Kimliği almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="dca51-146">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="dca51-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="dca51-147">Başka bir abonelik Kiracı kimliğini almak gerekiyorsa, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="dca51-148">Oturum açma için kullanılacak istemci kimliğini almak gereken durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="dca51-149">Oturum açma için kullanılacak değer hizmet asıl adları listelenen GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="dca51-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
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
3. <span data-ttu-id="dca51-150">Hizmet sorumlusu oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dca51-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="dca51-151">İçin parola istenir.</span><span class="sxs-lookup"><span data-stu-id="dca51-151">You are prompted for the password.</span></span> <span data-ttu-id="dca51-152">AD uygulamasının oluştururken belirttiğiniz parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="dca51-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="dca51-153">Şimdi, oluşturduğunuz hizmet sorumlusu için hizmet sorumlusu olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="dca51-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="dca51-154">Alternatif olarak, oturum açmak için komut satırından REST işlemlerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dca51-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="dca51-155">Kimlik doğrulaması yanıtından, diğer işlemleri ile kullanmak için erişim belirtecini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dca51-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="dca51-156">REST işlemlerini çağırarak erişim belirtecini alma bir örnek için bkz: [bir erişim belirteci oluşturma](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="dca51-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="dca51-157">Sertifika ile hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca51-157">Create service principal with certificate</span></span>
<span data-ttu-id="dca51-158">Bu bölümde, adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dca51-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="dca51-159">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca51-159">create a self-signed certificate</span></span>
* <span data-ttu-id="dca51-160">AD uygulamasının sertifikası ve hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca51-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="dca51-161">Hizmet sorumlusu okuyucu rolüne atayın</span><span class="sxs-lookup"><span data-stu-id="dca51-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="dca51-162">Bu adımları tamamlamak için ihtiyacınız [OpenSSL](http://www.openssl.org/) yüklü.</span><span class="sxs-lookup"><span data-stu-id="dca51-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="dca51-163">Kendinden imzalı bir sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dca51-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="dca51-164">Önceki adımı iki dosya - privkey.pem ve cert.pem oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="dca51-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="dca51-165">Ortak ve özel anahtarlar, tek bir dosya halinde birleştirin.</span><span class="sxs-lookup"><span data-stu-id="dca51-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="dca51-166">Açık **examplecert.pem** dosya ve karakter arasında uzun dizi arayın **---başlangıç sertifika---** ve **---son SERTİFİKAYI---**.</span><span class="sxs-lookup"><span data-stu-id="dca51-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="dca51-167">Sertifika verileri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dca51-167">Copy the certificate data.</span></span> <span data-ttu-id="dca51-168">Hizmet asıl oluştururken bu verileri bir parametre olarak geçirir.</span><span class="sxs-lookup"><span data-stu-id="dca51-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="dca51-169">Hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dca51-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="dca51-170">Hizmet sorumlusu oluşturmak için aşağıdaki komutta gösterildiği gibi uygulama ve sertifika verileri adını sağlayın:</span><span class="sxs-lookup"><span data-stu-id="dca51-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="dca51-171">Yeni hizmet sorumlusunu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="dca51-171">The new service principal is returned.</span></span> <span data-ttu-id="dca51-172">İzin verme nesne kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dca51-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="dca51-173">Hizmet asıl adları ile listelenen GUID açarken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dca51-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="dca51-174">Uygulama kimliği ile aynı değere GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="dca51-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="dca51-175">Örnek uygulamalarda, bu değer için istemci kimliği olarak adlandırılır</span><span class="sxs-lookup"><span data-stu-id="dca51-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
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
6. <span data-ttu-id="dca51-176">Aboneliğiniz için hizmet asıl izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="dca51-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="dca51-177">Bu örnekte, hizmet sorumlusu Abonelikteki tüm kaynaklar okuma izni verir okuyucu rolüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dca51-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="dca51-178">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="dca51-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="dca51-179">ObjectID parametresi için uygulama oluştururken kullanılan nesne kimliği sağlayın.</span><span class="sxs-lookup"><span data-stu-id="dca51-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="dca51-180">Bu komutu çalıştırmadan önce süre Azure Active Directory yaymak yeni bir hizmet sorumlusu için izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="dca51-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="dca51-181">Genellikle, bu komutları el ile çalıştırdığınızda görevleri arasında yeterli bir süre geçti.</span><span class="sxs-lookup"><span data-stu-id="dca51-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="dca51-182">Bir komut dosyası komut arasında uyku moduna bir adımı eklemeniz gerekir (gibi `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="dca51-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="dca51-183">Asıl dizinde yok bildiren bir hata görürseniz, komutu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dca51-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="dca51-184">Otomatik Azure CLI komut dosyası aracılığıyla sertifikası sağlayın</span><span class="sxs-lookup"><span data-stu-id="dca51-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="dca51-185">Şimdi, işlemleri gerçekleştirmek için uygulama olarak oturum açmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca51-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="dca51-186">Bir hizmet sorumlusu oturum olduğunda, Kiracı kimliği dizininin AD uygulamanız için sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca51-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="dca51-187">Bir kiracı, Azure Active Directory örneğidir.</span><span class="sxs-lookup"><span data-stu-id="dca51-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="dca51-188">Şu anda kimliği doğrulanmış aboneliğinizin Kiracı Kimliği almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="dca51-189">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="dca51-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="dca51-190">Başka bir abonelik Kiracı kimliğini almak gerekiyorsa, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="dca51-191">Sertifika parmak izini almak ve gerekli olmayan karakterleri kaldırmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="dca51-192">Hangi parmak izi değeri benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="dca51-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="dca51-193">Oturum açma için kullanılacak istemci kimliğini almak gereken durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="dca51-194">Oturum açma için kullanılacak değer hizmet asıl adları listelenen GUID'dir.</span><span class="sxs-lookup"><span data-stu-id="dca51-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
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
4. <span data-ttu-id="dca51-195">Hizmet sorumlusu oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dca51-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="dca51-196">Şimdi, oluşturduğunuz Azure Active Directory uygulaması için hizmet sorumlusu olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="dca51-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="dca51-197">Kimlik bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="dca51-197">Change credentials</span></span>

<span data-ttu-id="dca51-198">Ya da güvenliğinin aşılması veya bir kimlik bilgisi sona erme nedeniyle, bir AD uygulaması için kimlik bilgilerini değiştirmek için kullanın `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="dca51-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="dca51-199">Parolayı değiştirmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="dca51-200">Bir sertifika değerini değiştirmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="dca51-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="dca51-201">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="dca51-201">Debug</span></span>

<span data-ttu-id="dca51-202">Bir hizmet sorumlusu oluşturma sırasında şu hatalarla karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dca51-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="dca51-203">**"Authentication_Unauthorized"** veya **"abonelik bağlamda bulunamadı."**</span><span class="sxs-lookup"><span data-stu-id="dca51-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="dca51-204">Hesabınızı olmadığı zaman-bu hatayı görmek [gerekli izinleri](#required-permissions) uygulama kaydetmek için Azure Active Directory üzerinde.</span><span class="sxs-lookup"><span data-stu-id="dca51-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="dca51-205">Yalnızca yönetici kullanıcıların Azure Active Directory'de uygulamaları kaydedebilirsiniz ve hesabınızın bir yönetici değil, bu hata genellikle, bakın</span><span class="sxs-lookup"><span data-stu-id="dca51-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="dca51-206">Ya da bir yönetici rolü atayın veya kullanıcıların uygulamaları kaydetmek yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="dca51-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="dca51-207">Hesabınızı **"kapsamı '/ subscriptions / {GUID}' üzerinde 'Microsoft.Authorization/roleAssignments/write' işlemini gerçekleştirme yetkisi yok."**  -Hesabınız için bir kimlik rol atamak için yeterli izinlere sahip olmadığında bu hataya bakın.</span><span class="sxs-lookup"><span data-stu-id="dca51-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="dca51-208">Kullanıcı erişimi Yöneticisi rolüne eklemek için abonelik yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="dca51-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="dca51-209">Örnek uygulamalar</span><span class="sxs-lookup"><span data-stu-id="dca51-209">Sample applications</span></span>
<span data-ttu-id="dca51-210">Farklı platformlarda üzerinden uygulama olarak oturum açma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="dca51-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="dca51-211">.NET</span><span class="sxs-lookup"><span data-stu-id="dca51-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="dca51-212">Java</span><span class="sxs-lookup"><span data-stu-id="dca51-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="dca51-213">Node.js</span><span class="sxs-lookup"><span data-stu-id="dca51-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="dca51-214">Python</span><span class="sxs-lookup"><span data-stu-id="dca51-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="dca51-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="dca51-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="dca51-216">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dca51-216">Next steps</span></span>
* <span data-ttu-id="dca51-217">Kaynakları yönetmek için Azure'da bir uygulamayı tümleştirme ayrıntılı adımlar için bkz: [Geliştirici Kılavuzu'na yetkilendirme Azure Kaynak Yöneticisi API'si ile](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dca51-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="dca51-218">Sertifikalar ve Azure CLI kullanma hakkında daha fazla bilgi edinmek için bkz: [sertifika tabanlı kimlik doğrulaması Azure hizmet asıl adı ile Linux komut satırından](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="dca51-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="dca51-219">Verilen veya kullanıcılar için reddedilen kullanılabilir eylemler listesi için bkz: [Azure Resource Manager kaynak sağlayıcısı işlemleri](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="dca51-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
