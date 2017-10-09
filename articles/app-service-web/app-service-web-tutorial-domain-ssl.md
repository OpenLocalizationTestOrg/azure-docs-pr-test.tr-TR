---
title: "aaaAdd özel etki alanı ve SSL tooan Azure web uygulaması | Microsoft Docs"
description: "Nasıl tooprepare Azure web uygulaması toogo üretim şirket markası ekleyerek öğrenin. Merhaba özel etki alanı adı (gösterim etki alanında) tooyour web uygulaması harita ve özel bir SSL sertifikası ile güvenli."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="26d08-104">Özel etki alanı ve SSL tooan Azure web uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="26d08-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="26d08-105">Bu öğretici nasıl tooquickly bir özel etki alanı adı tooyour Azure web uygulaması harita ve özel bir SSL sertifikası ile güvenli gösterir.</span><span class="sxs-lookup"><span data-stu-id="26d08-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="26d08-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="26d08-106">Before you begin</span></span>

<span data-ttu-id="26d08-107">Bu örneği çalıştırmadan önce hello yükleyin [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="26d08-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="26d08-108">Ayrıca yönetim erişimi toohello DNS yapılandırma sayfasında ilgili etki sağlayıcınız için gerekir.</span><span class="sxs-lookup"><span data-stu-id="26d08-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="26d08-109">Örneğin, tooadd `www.contoso.com`, toobe mümkün tooconfigure DNS girişleri için gereksinim duyduğunuz `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="26d08-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="26d08-110">Son olarak, geçerli bir gerekir. PFX dosyası _ve_ tooupload istediğiniz hello SSL sertifikasının parolası ve bağlayın.</span><span class="sxs-lookup"><span data-stu-id="26d08-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="26d08-111">Bu SSL sertifikasını istediğiniz yapılandırılmış toosecure hello özel etki alanı adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="26d08-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="26d08-112">Örnek yukarıda Hello SSL sertifikanızı güvenli `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="26d08-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="26d08-113">1. adım - Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="26d08-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="26d08-114">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="26d08-114">Log in tooAzure</span></span>

<span data-ttu-id="26d08-115">Bir terminal penceresi toocreate hello kaynakları giderek toouse hello Azure CLI 2.0 toohost Node.js uygulamamıza Azure gerekli artık duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="26d08-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="26d08-116">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="26d08-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="26d08-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="26d08-117">Create a resource group</span></span>   
<span data-ttu-id="26d08-118">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="26d08-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="26d08-119">Azure kaynak grubu; web uygulamaları, veritabanları ve depolama hesapları gibi Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="26d08-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="26d08-120">toosee hangi olası değerler için kullanabilmeniz için `---location`, hello kullan `az appservice list-locations` Azure CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="26d08-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="26d08-121">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="26d08-121">Create an App Service plan</span></span>

<span data-ttu-id="26d08-122">Merhaba ile bir uygulama hizmeti planı oluştur [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="26d08-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="26d08-123">Merhaba aşağıdaki örnekte oluşturur adlı bir uygulama hizmeti planı `myAppServicePlan` hello kullanarak **temel** fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="26d08-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="26d08-124">az uygulama hizmeti planı oluşturma--ad myAppServicePlan--kaynak-grubu myResourceGroup--sku B1</span><span class="sxs-lookup"><span data-stu-id="26d08-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="26d08-125">Uygulama hizmeti planı Hello oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir.</span><span class="sxs-lookup"><span data-stu-id="26d08-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a><span data-ttu-id="26d08-126">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="26d08-126">Create a web app</span></span>

<span data-ttu-id="26d08-127">Bir uygulama hizmeti planı oluşturuldu, hello içinde bir web uygulaması oluşturma `myAppServicePlan` uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="26d08-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="26d08-128">dağıtılan uygulama, bir barındırma alanı toodeploy kodunuzu olduğunuz yanı sıra tooview hello sizin için bir URL sağlar hello web uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="26d08-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="26d08-129">Kullanım hello [az appservice web oluşturmak](/cli/azure/appservice/web#create) komutu toocreate hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="26d08-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="26d08-130">Merhaba aşağıdaki komutu, lütfen hello gördüğünüz kendi benzersiz uygulama adı yerine `<app_name>` yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="26d08-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="26d08-131">Merhaba adının toobe benzersiz azure'da tüm uygulamalarında gerekir böylece bu benzersiz bir ad hello varsayılan etki alanı adı hello web uygulaması için hello parçası olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26d08-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="26d08-132">Hiçbir özel DNS girişi toohello web uygulama daha sonra tooyour kullanıcılar kullanıma önce eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26d08-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="26d08-133">Merhaba web uygulaması oluşturduğunuzda aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir.</span><span class="sxs-lookup"><span data-stu-id="26d08-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

<span data-ttu-id="26d08-134">Merhaba JSON çıktısını gelen `defaultHostName` web uygulamanızın varsayılan etki alanı adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="26d08-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="26d08-135">Tarayıcınızda, toothis adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="26d08-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="26d08-137">2. adım - DNS eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26d08-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="26d08-138">Bu adımda, bir özel etki alanı tooyour web uygulamanızın varsayılan etki alanı adından bir eşleme Ekle `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="26d08-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="26d08-139">Genellikle, etki alanı sağlayıcınızın Web sitesinin bu adımı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="26d08-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="26d08-140">Sağlayıcınızın belgelerine bakmanız gerekir böylece her etki alanı kayıt şirketinizin Web sitesi biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="26d08-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="26d08-141">Ancak, bazı genel yönergeler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="26d08-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="26d08-142">TootooDNS yönetimi sayfasına gidin</span><span class="sxs-lookup"><span data-stu-id="26d08-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="26d08-143">İlk olarak, tooyour etki alanı kayıt şirketinizin Web sitesinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="26d08-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="26d08-144">Ardından, DNS kayıtlarını yönetme için hello sayfasını bulun.</span><span class="sxs-lookup"><span data-stu-id="26d08-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="26d08-145">Bağlantılar veya etiketli hello sitesinin alanları arayın **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="26d08-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="26d08-146">Genellikle, hesap bilgilerinizi görüntülemek ve bir bağlantı gibi arayan hello bağlantı bulabilirsiniz **My etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="26d08-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="26d08-147">Bu sayfayı bulduktan sonra Ekle veya DNS kayıtlarını düzenlemenize olanak sağlayan bir bağlantı için bakın.</span><span class="sxs-lookup"><span data-stu-id="26d08-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="26d08-148">Bu olabilir bir **bölge dosyası** veya **DNS kayıtlarını** bağlantı veya bir **Gelişmiş Yapılandırma** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="26d08-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="26d08-149">Bir CNAME kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="26d08-149">Create a CNAME record</span></span>

<span data-ttu-id="26d08-150">Hello istenen alt etki alanı adı tooyour web uygulamanızın varsayılan etki alanı adı eşleyen bir CNAME kaydı ekleyin (`<app_name>.azurewebsites.net`, burada `<app_name>` , uygulamanızın benzersiz adıdır).</span><span class="sxs-lookup"><span data-stu-id="26d08-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="26d08-151">Hello için `www.contoso.com` örnek, hello eşleyen bir CNAME oluşturun `www` ana bilgisayar adı çok`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="26d08-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="26d08-152">3. adım - web uygulamanız hello özel etki alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26d08-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="26d08-153">Etki alanı sağlayıcınızın Web sitesinin hello hostname eşleme yapılandırmayı bitirdiğinizde, web uygulamanız hazır tooconfigure hello özel etki alanı demektir.</span><span class="sxs-lookup"><span data-stu-id="26d08-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="26d08-154">Kullanım hello [az appservice web yapılandırma hostname eklemek](/cli/azure/appservice/web/config/hostname#add) tooadd bu yapılandırma komutu.</span><span class="sxs-lookup"><span data-stu-id="26d08-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="26d08-155">Merhaba aşağıdaki komutu, lütfen yerine `<app_name>` benzersiz uygulama adı ve < your_custom_domain > merhaba tam özel etki alanı adı ile (örneğin `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="26d08-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="26d08-156">Merhaba özel etki alanı artık tam olarak eşlenmiş tooyour web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="26d08-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="26d08-157">Tarayıcınızda, toohello özel etki alanı adı gidin.</span><span class="sxs-lookup"><span data-stu-id="26d08-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="26d08-158">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="26d08-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="26d08-160">4. adım - BIND özel bir SSL sertifikası tooyour web uygulaması</span><span class="sxs-lookup"><span data-stu-id="26d08-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="26d08-161">Şimdi bir Azure web uygulaması hello tarayıcının adres çubuğunda istediğiniz hello etki alanı adı ile sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="26d08-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="26d08-162">Ancak, toohello giderseniz `https://<your_custom_domain>` şimdi, bir sertifika hatası alın.</span><span class="sxs-lookup"><span data-stu-id="26d08-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="26d08-164">Web uygulamanızı henüz özel etki alanı adıyla eşleşen bir SSL sertifikası bağlaması sahip olmadığından bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="26d08-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="26d08-165">Ancak, çok giderseniz, bir hata iletisi yok`https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="26d08-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="26d08-166">Tüm Azure App Service uygulamalarının yanı sıra, uygulamanızı güvenliğinin hello için hello SSL sertifikası ile bunun nedeni `*.azurewebsites.net` joker karakter etki alanı varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="26d08-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="26d08-167">Tooaccess web uygulamanızı özel etki alanı adınızı sipariş, özel etki alanı toohello web uygulamanız için toobind hello SSL sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="26d08-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="26d08-168">Bu adımda yapar.</span><span class="sxs-lookup"><span data-stu-id="26d08-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="26d08-169">Merhaba SSL sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="26d08-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="26d08-170">Özel etki alanı tooyour web uygulamanız için SSL sertifikası Hello hello kullanarak karşıya [az appservice web yapılandırma ssl karşıya yükleme](/cli/azure/appservice/web/config/ssl#upload) komutu.</span><span class="sxs-lookup"><span data-stu-id="26d08-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="26d08-171">Merhaba aşağıdaki komutu, lütfen yerine `<app_name>` benzersiz uygulama adınız ile `<path_to_ptx_file>` hello yolu tooyour ile. PFX dosyası ve `<password>` sertifikanızın parolayla.</span><span class="sxs-lookup"><span data-stu-id="26d08-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="26d08-172">Merhaba sertifika karşıya yüklendiğinde, hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="26d08-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

<span data-ttu-id="26d08-173">Merhaba JSON çıktısını gelen `thumbprint` karşıya yüklenen sertifikanızın parmak izi gösterir.</span><span class="sxs-lookup"><span data-stu-id="26d08-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="26d08-174">Merhaba sonraki adımınız değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="26d08-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="26d08-175">Bağlama hello SSL sertifika toohello web uygulaması karşıya yüklenmedi</span><span class="sxs-lookup"><span data-stu-id="26d08-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="26d08-176">Web uygulamanız şimdi istediğiniz hello özel etki alanı adı içeriyor ve bu özel etki alanı güvenliğini sağlar bir SSL sertifikası da sahiptir.</span><span class="sxs-lookup"><span data-stu-id="26d08-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="26d08-177">Merhaba yalnızca şey sol toodo toobind hello yüklenen sertifikanın toohello web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="26d08-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="26d08-178">Hello kullanarak bunu [az appservice web yapılandırma ssl bağı](/cli/azure/appservice/web/config/ssl#bind) komutu.</span><span class="sxs-lookup"><span data-stu-id="26d08-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="26d08-179">Merhaba aşağıdaki komutu, lütfen yerine `<app_name>` benzersiz uygulama adıyla ve `<thumbprint-from-previous-output>` hello önceki komuttan alma hello sertifika parmak izine sahip.</span><span class="sxs-lookup"><span data-stu-id="26d08-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="26d08-180">az appservice web yapılandırma ssl bağı--ad < app_name >--kaynak-grubu myResourceGroup--sertifika parmak izi < parmak izi-gelen-önceki-output >--ssl türü SNI</span><span class="sxs-lookup"><span data-stu-id="26d08-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="26d08-181">Merhaba sertifika ilişkili tooyour web uygulaması olduğunda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:</span><span class="sxs-lookup"><span data-stu-id="26d08-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="26d08-182">{"availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containersize değeri yok olarak": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "< app_name >. azurewebsites.net", "enabled": true, " enabledHostNames": ["www.contoso.com"," < app_name >. azurewebsites.net "," < app_name >. scm.azurewebsites.net "],"gatewaySiteName": null,"hostNameSslStates": [{"ana":"Standart","name":" < app_name >. azurewebsites.net ","sslState":"Devre dışı","parmak izi": null,"toUpdate": null,"Virtualıp": null}, {"ana":"Repository","ad":" < app_name >. scm.azurewebsites.net ","sslState":"Devre dışı","parmak izi": null,"toUpdate": null,"Virtualıp": null}, {" ana bilgisayar türü":"Standart","name":"www.contoso.com","sslState":"SniEnabled","parmak izi":"9FD1D2D06E2293673E2A8D1CA484A092BD016D00","toUpdate": null,"Virtualıp": null}],"ana bilgisayar adları": ["www.contoso.com","< app_name >. azurewebsites.NET"],"hostNamesDisabled": false,"hostingEnvironmentProfile": null,"id":" /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < app_name > "," isDefaultContainer": null,"tür":"WebApp","lastModifiedTimeUtc":" 2017-03-29T14:36:18.803333 ","Konum":"Batı Avrupa","maxNumberOfWorkers": null,"mikro":"false","adı":"< app_name >","outboundIpAddresses":" 13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1 ","premiumAppDeployed": null,"repositorySiteName":"< app_name >","ayrılmış": false,"kaynak grubu":"contoso.com","scmSiteAlsoStopped": false,"Serverfarmıd": "/ abonelikleri/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/sağlayıcıları/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "Durum": "Çalışır", "suspendedTill": null, "etiketler": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "tür": "Microsoft.Web/sites", "usageState": "Normal"}</span><span class="sxs-lookup"><span data-stu-id="26d08-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="26d08-183">Tarayıcınızda, özel etki alanı adınızı tooHTTPS uç noktasını gidin.</span><span class="sxs-lookup"><span data-stu-id="26d08-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="26d08-184">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="26d08-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="26d08-186">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="26d08-186">More resources</span></span>

<span data-ttu-id="26d08-187">[Satın alma ve Azure App Service'te özel etki alanı adı yapılandırma](custom-dns-web-site-buydomains-web-app.md)
[satın alın ve Azure uygulama hizmetiniz için bir SSL sertifikası yapılandırma](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="26d08-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
