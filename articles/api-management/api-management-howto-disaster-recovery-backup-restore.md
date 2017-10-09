---
title: "aaaImplement olağanüstü durum kurtarma'yı kullanarak yedekleme ve geri yükleme Azure API Management'te | Microsoft Docs"
description: "Bilgi nasıl toouse yedekleme ve geri yükleme Azure API Management'te tooperform olağanüstü durum kurtarma."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="0c8d9-103">Nasıl tooimplement olağanüstü durum kurtarma'yı kullanarak ve yedekleme hizmeti Azure API Management'te geri yükleme</span><span class="sxs-lookup"><span data-stu-id="0c8d9-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="0c8d9-104">Göre toopublish seçme ve Apı'lerinizi uygulamak ve yönetmek toodesign, aksi takdirde olması gereken çok sayıda hataya dayanıklılık ve altyapı özelliklerinden yapmakta Azure API Yönetimi yoluyla yönetin.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="0c8d9-105">Hello Azure platformu hello maliyet bir kısmı olası hatalar büyük kesir azaltır.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="0c8d9-106">API Management hizmetiniz olduğu hello bölge etkileyen kullanılabilirlik sorunlardaki toorecover barındırılan hazır tooreconstitute herhangi bir zamanda hizmetiniz farklı bir bölgede olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="0c8d9-107">Kullanılabilirlik hedefleriniz ve kurtarma süresi hedefi bağlı olarak tooreserve yedekleme hizmeti bir veya daha fazla bölgelerde istediğiniz ve kendi yapılandırma ve içerik hello etkin hizmeti ile eşitlenmiş toomaintain deneyin.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="0c8d9-108">Merhaba hizmeti yedekleme ve geri yükleme özelliği, olağanüstü durum kurtarma stratejiniz uygulamak üzere hello gerekli yapı taşı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="0c8d9-109">Bu kılavuz, Azure Resource Manager tooauthenticate istekleri nasıl ve nasıl gösterir toobackup ve API Management hizmeti örnekleri geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="0c8d9-110">Yedekleme ve olağanüstü durum kurtarma için bir API Management hizmet örneği geri yükleme için hello işlemi de API Management hizmeti örnekleri hazırlama gibi senaryolar için çoğaltmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="0c8d9-111">Her yedekleme 30 gün sonra süresi dolar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="0c8d9-112">Merhaba 30 günlük süre sona erdiğinde toorestore bir yedekleme çalışırsanız hello geri yükleme başarısız bir `Cannot restore: backup expired` ileti.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="0c8d9-113">Kimlik doğrulama Azure Resource Manager istekleri</span><span class="sxs-lookup"><span data-stu-id="0c8d9-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0c8d9-114">Merhaba yedekleme ve geri yükleme için REST API Azure Resource Manager kullanır ve API Management varlıklarınızı yönetmek için REST API'leri hello daha farklı kimlik doğrulama mekanizması vardır.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="0c8d9-115">Bu bölümdeki Hello adımları nasıl tooauthenticate Azure Resource Manager istekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="0c8d9-116">Daha fazla bilgi için bkz: [Azure Resource Manager kimlik doğrulama istekleri](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c8d9-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="0c8d9-117">Tüm kaynakları hello Azure Resource Manager kullanarak bunu hello görevleri Azure hello aşağıdaki adımları kullanarak Active Directory'e ile kimliğinin doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="0c8d9-118">Bir uygulama toohello Azure Active Directory Kiracı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="0c8d9-119">Eklediğiniz hello uygulama izinlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="0c8d9-120">Merhaba belirteç isteklerini tooAzure Resource Manager kimlik doğrulaması için alın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="0c8d9-121">Merhaba ilk adımı toocreate bir Azure Active Directory uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="0c8d9-122">Merhaba günlüğüne [Klasik Azure portalı](http://manage.windowsazure.com/) API Management hizmetiniz içeren hello aboneliğinden örneği ve toohello gidin **uygulamaları** varsayılan Azure Active Directory sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="0c8d9-123">Hello Azure Active Directory varsayılan dizin görünür tooyour hesabı değilse, hello Azure aboneliği toogrant hello kişi hello Yöneticisi izinleri tooyour hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Azure Active Directory uygulaması oluşturma][api-management-add-aad-application]

<span data-ttu-id="0c8d9-125">Tıklatın **Ekle**, **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**ve seçin **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="0c8d9-126">Açıklayıcı bir ad girin ve hello İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="0c8d9-127">Yer tutucu URL girin `http://resources` hello için **yeniden yönlendirme URI'si**, gerekli bir alandır ancak hello değer daha sonra kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="0c8d9-128">Merhaba onay kutusunu toosave hello uygulama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="0c8d9-129">Merhaba uygulama kaydedildikten sonra tıklatın **yapılandırma**, toohello aşağı kaydırın **izinleri tooother uygulamaları** bölüm ve'ı tıklatın **uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![İzinleri ekleme][api-management-aad-permissions-add]

<span data-ttu-id="0c8d9-131">Seçin **Windows** **Azure Hizmet Yönetimi API'si** ve hello onay kutusunu tooadd hello uygulama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![İzinleri ekleme][api-management-aad-permissions]

<span data-ttu-id="0c8d9-133">Tıklatın **izinlere temsilci** yeni eklenen hello yanında **Windows** **Azure Hizmet Yönetimi API'si** uygulama, hello kutuyu **erişim Azure Hizmet Yönetimi (Önizleme)**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![İzinleri ekleme][api-management-aad-delegated-permissions]

<span data-ttu-id="0c8d9-135">Önceki tooinvoking hello oluşturmak API'leri yedekleme hello ve geri yüklemek, gerekli tooget bir belirteç değildir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="0c8d9-136">Merhaba aşağıdaki örnek kullanır hello [Microsoft.IdentityModel.Clients.activedirectory tarafından](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget paketi tooretrieve hello belirteci.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="0c8d9-137">Değiştir `{tentand id}`, `{application id}`, ve `{redirect uri}` yönergeleri izleyerek hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="0c8d9-138">Değiştir `{tenant id}` hello oluşturduğunuz Azure Active Directory Uygulama hello Kiracı kimliği.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="0c8d9-139">Tıklatarak hello kimliği erişebilirsiniz **uç noktaları görüntülemek**.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-139">You can access hello id by clicking **View endpoints**.</span></span>

![Uç Noktalar][api-management-aad-default-directory]

![Uç Noktalar][api-management-endpoint]

<span data-ttu-id="0c8d9-142">Değiştir `{application id}` ve `{redirect uri}` hello kullanarak **istemci kimliği** ve hello URL hello **yeniden yönlendirme URI'ler** Azure Active Directory uygulamanızın bölümünden **Yapılandır**  sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Kaynaklar][api-management-aad-resources]

<span data-ttu-id="0c8d9-144">Hello değerleri belirlendikten sonra Merhaba kodu örneği aşağıdaki örneğine belirteci benzer bir toohello döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![Belirteç][api-management-arm-token]

<span data-ttu-id="0c8d9-146">Arama hello yedekleme ve geri yükleme işlemleri hello aşağıdaki bölümlerde açıklanan önce hello yetkilendirme istek üstbilgisi REST çağrısı için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="0c8d9-147"><a name="step1"></a>Bir API Management hizmeti yedekleyin</span><span class="sxs-lookup"><span data-stu-id="0c8d9-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="0c8d9-148">HTTP isteği izleyen bir API Management hizmet sorunu hello yukarı tooback:</span><span class="sxs-lookup"><span data-stu-id="0c8d9-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="0c8d9-149">Burada:</span><span class="sxs-lookup"><span data-stu-id="0c8d9-149">where:</span></span>

* <span data-ttu-id="0c8d9-150">`subscriptionId`-toobackup çalıştığınız hello API Management hizmeti içeren hello abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="0c8d9-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="0c8d9-151">`resourceGroupName`-'Api - varsayılan-{hizmeti-bölge}' hello biçiminde bir dize nerede `service-region` hello Azure bölgesi hello toobackup çalıştığınız API Management hizmeti barındırıldığı, örneğin tanımlar`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="0c8d9-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="0c8d9-152">`serviceName`-Merhaba, bir yedeğini Merhaba, oluşturma sırasında belirtilen API Management hizmeti hello adı</span><span class="sxs-lookup"><span data-stu-id="0c8d9-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="0c8d9-153">`api-version`-değiştirin`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="0c8d9-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="0c8d9-154">Merhaba isteği Hello gövdesinde hello hedef Azure depolama hesabı adı, erişim tuşu, blob kapsayıcı adı ve yedek adı belirtin:</span><span class="sxs-lookup"><span data-stu-id="0c8d9-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="0c8d9-155">Merhaba hello değerini ayarlamak `Content-Type` isteği üstbilgisi çok`application/json`.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="0c8d9-156">Yedekleme birden çok dakika toocomplete sürebilir uzun süren bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="0c8d9-157">Merhaba istek başarılı oldu ve hello yedekleme işlemi başlatıldı, alırsınız bir `202 Accepted` yanıt durum koduyla bir `Location` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="0c8d9-158">Oluştur 'GET' hello toohello URL'de istekleri `Location` üstbilgi toofind hello hello işlemin durumunu çıkışı.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="0c8d9-159">Merhaba yedekleme işlemi devam ederken tooreceive '202 kabul' durum kodunu devam eder.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="0c8d9-160">Bir yanıt kodu, `200 OK` hello yedekleme işlemi başarılı şekilde tamamlandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="0c8d9-161">Lütfen yedekleme isteği yapılırken kısıtlamaları aşağıdaki hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="0c8d9-162">**Kapsayıcı** hello istek gövdesinde belirtilen **bulunmalıdır**.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="0c8d9-163">Yedekleme, sürerken **herhangi bir hizmet yönetim işlemini çalışmamalısınız** SKU yükseltme veya indirgeme, etki alanı adı değişikliği gibi vb..</span><span class="sxs-lookup"><span data-stu-id="0c8d9-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="0c8d9-164">Geri yükleme bir **yedekleme yalnızca 30 gün boyunca garanti** hello anda oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="0c8d9-165">**Kullanım verileri** analytics raporları oluşturmak için kullanılan **eklenmedi** hello yedekleme.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="0c8d9-166">Kullanım [Azure API Management REST API] [ Azure API Management REST API] tooperiodically almak analytics raporları güvenli olarak saklamak için.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="0c8d9-167">Hizmet yedeklemeler gerçekleştirmek hello sıklığı, kurtarma noktası hedefi etkiler.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="0c8d9-168">Bu sizi düzenli yedeklemeler uygulama yanı sıra önemli yaptıktan sonra isteğe bağlı yedeklemeleri gerçekleştirmek bildirmek toominimize tooyour API Management hizmeti değiştirir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="0c8d9-169">**Değişiklikleri** yapılmış toohello hizmet (örneğin API'leri, ilkeleri, Geliştirici Portalı Görünüm) yedekleme işlemi sırasında yapılandırmadır işleminde **hello yedeklemeye dahil değildir ve bu nedenle kaybolacak**.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="0c8d9-170"><a name="step2"></a>Bir API Management hizmeti geri yükleme</span><span class="sxs-lookup"><span data-stu-id="0c8d9-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="0c8d9-171">toorestore önceden oluşturulmuş bir yedekten bir API Management hizmeti, HTTP isteği aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="0c8d9-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="0c8d9-172">Burada:</span><span class="sxs-lookup"><span data-stu-id="0c8d9-172">where:</span></span>

* <span data-ttu-id="0c8d9-173">`subscriptionId`-içine bir yedeği geri yüklediğiniz hello API Management hizmeti içeren hello abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="0c8d9-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="0c8d9-174">`resourceGroupName`-'Api - varsayılan-{hizmeti-bölge}' hello biçiminde bir dize nerede `service-region` hello Azure bölgesi hello içine bir yedeği geri yüklediğiniz API Management hizmeti barındırıldığı, örneğin tanımlar`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="0c8d9-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="0c8d9-175">`serviceName`-hello API uygulamasına geri yükleniyor hizmet Merhaba, oluşturma sırasında belirtilen yönetim hello adı</span><span class="sxs-lookup"><span data-stu-id="0c8d9-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="0c8d9-176">`api-version`-değiştirin`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="0c8d9-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="0c8d9-177">Merhaba isteği Hello gövdesinde hello yedekleme dosyası konumu, yani Azure depolama hesabı adı, erişim tuşu, blob kapsayıcı adı ve yedek adı belirtin:</span><span class="sxs-lookup"><span data-stu-id="0c8d9-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="0c8d9-178">Merhaba hello değerini ayarlamak `Content-Type` isteği üstbilgisi çok`application/json`.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="0c8d9-179">Geri yükleme too30 veya daha fazla dakika toocomplete sürebilir uzun süren bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="0c8d9-180">Merhaba istek başarılı oldu ve hello geri yükleme işlemi başlatıldı, alırsınız bir `202 Accepted` yanıt durum koduyla bir `Location` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="0c8d9-181">Oluştur 'GET' hello toohello URL'de istekleri `Location` üstbilgi toofind hello hello işlemin durumunu çıkışı.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="0c8d9-182">Merhaba geri yükleme işlemi devam ederken tooreceive '202 kabul edilen' durum kodunu devam eder.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="0c8d9-183">Bir yanıt kodu, `200 OK` hello geri yükleme işlemi başarılı şekilde tamamlandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c8d9-184">**Merhaba SKU** hello hizmet uygulamasına geri yükleniyor **eşleşmelidir** hello hello SKU'su yedeklenen hizmetini geri yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="0c8d9-185">**Değişiklikleri** yapılmış toohello hizmet yapılandırmasını (örneğin API'leri, ilkeleri, Geliştirici Portalı Görünüm) geri yükleme işlemi sırasında ediyor **üzerine yazılabilir**.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0c8d9-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0c8d9-186">Next steps</span></span>
<span data-ttu-id="0c8d9-187">Microsoft bloglar hello yedekleme/geri yükleme işleminin iki farklı izlenecek yollar için aşağıdaki hello göz atın.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="0c8d9-188">Azure API Management hesapları Çoğalt</span><span class="sxs-lookup"><span data-stu-id="0c8d9-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="0c8d9-189">TooGisela kendi katkı toothis makalesi için teşekkür ederiz.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="0c8d9-190">Azure API Management: Yedekleme ve yapılandırmasını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="0c8d9-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="0c8d9-191">ancak çok ilginç Stuart tarafından ayrıntılı hello yaklaşım hello resmi Kılavuzu eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="0c8d9-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
