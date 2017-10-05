---
title: "Olağanüstü durum kurtarma uygulama kullanarak yedekleme ve geri yükleme Azure API Management'te | Microsoft Docs"
description: "Yedekleme ve olağanüstü durum kurtarma Azure API Management'te gerçekleştirmek için geri yükleme öğrenin."
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
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="33ee8-103">Olağanüstü durum kurtarma hizmeti Yedekleme kullanarak uygulamak ve Azure API Management'te geri yükleme</span><span class="sxs-lookup"><span data-stu-id="33ee8-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="33ee8-104">Yayımlama ve Azure API Yönetimi yoluyla, API'ları yönetmek seçerek birçok hata toleransı ve aksi durumda tasarım, uygulamak ve yönetmek için olurdu altyapı olanaklarından sürüyor.</span><span class="sxs-lookup"><span data-stu-id="33ee8-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="33ee8-105">Azure platformu olası hataları bir kısmı maliyetle en büyük bir kısmı azaltır.</span><span class="sxs-lookup"><span data-stu-id="33ee8-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="33ee8-106">Kullanılabilirlik kurtarmak için API Management hizmeti, barındırıldığı bölgeyi etkileyen sorunları hizmetiniz farklı bir bölgede herhangi bir zamanda yeniden oluşturma hazır olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="33ee8-107">Kullanılabilirlik hedefleriniz ve kurtarma süresi hedefi bağlı olarak bir yedekleme hizmeti bir veya daha fazla bölgelerde ayırabilir ve bunların yapılandırma ve içerik etkin hizmeti ile eşitlenmiş tutmak deneyin isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33ee8-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="33ee8-108">Hizmeti yedekleme ve geri yükleme özelliği, olağanüstü durum kurtarma stratejiniz uygulamak için gerekli yapı taşı sağlar.</span><span class="sxs-lookup"><span data-stu-id="33ee8-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="33ee8-109">Bu kılavuz, Azure Resource Manager istekleri kimlik doğrulaması yapmayı ve yedekleme ve geri yükleme, API Management hizmeti örnekleri nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="33ee8-110">Yedekleme ve olağanüstü durum kurtarma için bir API Management hizmet örneği geri yükleme işlemi, API Management hizmeti örnekleri hazırlama gibi senaryolar için çoğaltmak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="33ee8-111">Her yedekleme 30 gün sonra süresi dolar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="33ee8-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="33ee8-112">30 günlük süre sona erdiğinde bir yedeğini geri çalışırsanız, geri yükleme başarısız bir `Cannot restore: backup expired` ileti.</span><span class="sxs-lookup"><span data-stu-id="33ee8-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="33ee8-113">Kimlik doğrulama Azure Resource Manager istekleri</span><span class="sxs-lookup"><span data-stu-id="33ee8-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="33ee8-114">Yedekleme ve geri yükleme için REST API Azure Resource Manager kullanır ve API Management varlıklarınızı yönetmek için farklı kimlik doğrulama mekanizması REST API'leri daha vardır.</span><span class="sxs-lookup"><span data-stu-id="33ee8-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="33ee8-115">Bu bölümdeki adımlar, Azure Resource Manager isteklerinin kimlik doğrulaması açıklar.</span><span class="sxs-lookup"><span data-stu-id="33ee8-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="33ee8-116">Daha fazla bilgi için bkz: [Azure Resource Manager kimlik doğrulama istekleri](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="33ee8-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="33ee8-117">Tüm kaynakları Azure Kaynak Yöneticisi'ni kullanarak bunu görevleri Azure aşağıdaki adımları kullanarak Active Directory'e ile kimliğinin doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="33ee8-118">Azure Active Directory Kiracı için bir uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="33ee8-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="33ee8-119">Eklediğiniz uygulama izinlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="33ee8-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="33ee8-120">İstekleri için Azure Resource Manager kimlik doğrulaması için belirteç alın.</span><span class="sxs-lookup"><span data-stu-id="33ee8-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="33ee8-121">İlk adım, bir Azure Active Directory uygulaması oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="33ee8-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="33ee8-122">İçine oturum [Klasik Azure portalı](http://manage.windowsazure.com/) API Management hizmetiniz içeren aboneliğinden örneği ve gidin **uygulamaları** sekmesi, varsayılan olarak Azure Active Directory için.</span><span class="sxs-lookup"><span data-stu-id="33ee8-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="33ee8-123">Azure Active Directory varsayılan dizin hesabınıza görünür durumda değilse, hesabınız için gerekli izinleri vermek için Azure aboneliği yöneticisine başvurun.</span><span class="sxs-lookup"><span data-stu-id="33ee8-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![Azure Active Directory uygulaması oluşturma][api-management-add-aad-application]

<span data-ttu-id="33ee8-125">Tıklatın **Ekle**, **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**ve seçin **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="33ee8-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="33ee8-126">Açıklayıcı bir ad girin ve İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33ee8-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="33ee8-127">Yer tutucu URL girin `http://resources` için **yeniden yönlendirme URI'si**, gerekli bir alandır ancak değer daha sonra kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="33ee8-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="33ee8-128">Uygulamayı kaydetmek için onay kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33ee8-128">Click the check box to save the application.</span></span>

<span data-ttu-id="33ee8-129">Uygulama kaydedildikten sonra tıklatın **Yapılandır**, aşağı kaydırarak **diğer uygulamalara izinler** bölüm ve'ı tıklatın **uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="33ee8-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![İzinleri ekleme][api-management-aad-permissions-add]

<span data-ttu-id="33ee8-131">Seçin **Windows** **Azure Hizmet Yönetimi API'si** ve uygulama eklemek için onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="33ee8-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![İzinleri ekleme][api-management-aad-permissions]

<span data-ttu-id="33ee8-133">' I tıklatın **izinlere temsilci** yeni eklenen yanında **Windows** **Azure Hizmet Yönetimi API'si** uygulama için kutuyu **erişim Azure Hizmet Yönetimi (Önizleme)**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="33ee8-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![İzinleri ekleme][api-management-aad-delegated-permissions]

<span data-ttu-id="33ee8-135">Yedekleme oluşturmak ve bunu geri yüklemeyi API'lerini çağırmadan önce bir belirteç almak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="33ee8-136">Aşağıdaki örnek kullanır [Microsoft.IdentityModel.Clients.activedirectory tarafından](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) belirtecini almak için nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="33ee8-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="33ee8-137">Değiştir `{tentand id}`, `{application id}`, ve `{redirect uri}` aşağıdaki yönergeleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="33ee8-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="33ee8-138">Değiştir `{tenant id}` oluşturduğunuz Azure Active Directory Uygulama Kiracı kimliği.</span><span class="sxs-lookup"><span data-stu-id="33ee8-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="33ee8-139">Tıklatarak kimliği erişebilirsiniz **uç noktaları görüntülemek**.</span><span class="sxs-lookup"><span data-stu-id="33ee8-139">You can access the id by clicking **View endpoints**.</span></span>

![Uç Noktalar][api-management-aad-default-directory]

![Uç Noktalar][api-management-endpoint]

<span data-ttu-id="33ee8-142">Değiştir `{application id}` ve `{redirect uri}` kullanarak **istemci kimliği** ve URL'den **yeniden yönlendirme URI'ler** Azure Active Directory uygulamanızın bölümünden **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="33ee8-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Kaynaklar][api-management-aad-resources]

<span data-ttu-id="33ee8-144">Belirtilen değerler sonra kod örneği bir belirteç aşağıdaki örneğe benzer şekilde döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![Belirteç][api-management-arm-token]

<span data-ttu-id="33ee8-146">Aşağıdaki bölümlerde açıklanan yedekleme ve geri yükleme işlemleri çağırmadan önce yetkilendirme isteği başlığı REST çağrısı için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="33ee8-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="33ee8-147"><a name="step1"></a>Bir API Management hizmeti yedekleyin</span><span class="sxs-lookup"><span data-stu-id="33ee8-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="33ee8-148">Aşağıdaki HTTP isteği bir API Management hizmet sorunu yedeklemek için:</span><span class="sxs-lookup"><span data-stu-id="33ee8-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="33ee8-149">Burada:</span><span class="sxs-lookup"><span data-stu-id="33ee8-149">where:</span></span>

* <span data-ttu-id="33ee8-150">`subscriptionId`-çalıştığınız API Management hizmeti içeren abonelik kimliğini yedekleme</span><span class="sxs-lookup"><span data-stu-id="33ee8-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="33ee8-151">`resourceGroupName`-'Api - varsayılan-{hizmeti-bölge}' biçiminde bir dize nerede `service-region` burada API Management hizmeti Azure bölgelerini tanımlayan çalıştığınız yedekleme barındırılan, örn.`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="33ee8-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="33ee8-152">`serviceName`-API Management hizmet adını, oluşturma sırasında belirtilen bir yedeğini kuran</span><span class="sxs-lookup"><span data-stu-id="33ee8-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="33ee8-153">`api-version`-değiştirin`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="33ee8-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="33ee8-154">İstek gövdesinde hedef Azure depolama hesabı adı, erişim tuşu, blob kapsayıcı adı ve yedek adı belirtin:</span><span class="sxs-lookup"><span data-stu-id="33ee8-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="33ee8-155">Değerini `Content-Type` istek üstbilgisi `application/json`.</span><span class="sxs-lookup"><span data-stu-id="33ee8-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="33ee8-156">Yedekleme tamamlamak için birden çok dakika sürebilir uzun süren bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="33ee8-157">İstek başarılı oldu ve yedekleme işlemi başlatıldı, alırsınız bir `202 Accepted` yanıt durum koduyla bir `Location` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="33ee8-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="33ee8-158">'GET istekleri URL'ye' olun `Location` işlemi durumunu öğrenmek için üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="33ee8-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="33ee8-159">Yedekleme işlemi devam ederken '202 kabul edilen' durum kodunu almaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="33ee8-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="33ee8-160">Bir yanıt kodu, `200 OK` yedekleme işlemi başarılı şekilde tamamlandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="33ee8-161">Lütfen aşağıdaki kısıtlamalar yedekleme isteği yapılırken unutmayın.</span><span class="sxs-lookup"><span data-stu-id="33ee8-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="33ee8-162">**Kapsayıcı** istek gövdesinde belirtilen **bulunmalıdır**.</span><span class="sxs-lookup"><span data-stu-id="33ee8-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="33ee8-163">Yedekleme, sürerken **herhangi bir hizmet yönetim işlemini çalışmamalısınız** SKU yükseltme veya indirgeme, etki alanı adı değişikliği gibi vb..</span><span class="sxs-lookup"><span data-stu-id="33ee8-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="33ee8-164">Geri yükleme bir **yedekleme yalnızca 30 gün boyunca garanti** oluşturulduktan andan itibaren.</span><span class="sxs-lookup"><span data-stu-id="33ee8-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="33ee8-165">**Kullanım verileri** analytics raporları oluşturmak için kullanılan **eklenmedi** yedekleme.</span><span class="sxs-lookup"><span data-stu-id="33ee8-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="33ee8-166">Kullanım [Azure API Management REST API] [ Azure API Management REST API] analytics raporları güvenli olarak saklamak için düzenli aralıklarla alınamadı.</span><span class="sxs-lookup"><span data-stu-id="33ee8-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="33ee8-167">Hizmet yedeklemeler gerçekleştirmek sıklığı, kurtarma noktası hedefi etkiler.</span><span class="sxs-lookup"><span data-stu-id="33ee8-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="33ee8-168">Bu en aza indirmek için biz düzenli yedeklemeler uygulama yanı sıra API Management hizmetiniz için önemli değişiklikler yaptıktan sonra isteğe bağlı yedeklemeleri gerçekleştirmek öneriyoruz.</span><span class="sxs-lookup"><span data-stu-id="33ee8-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="33ee8-169">**Değişiklikleri** hizmet yapılandırmasını (örneğin API'leri, ilkeleri, Geliştirici Portalı Görünüm) yedekleme sırasında yapılan işlemdir işleminde **yedekleme işlemine dahil edilmeyen ve bu nedenle kaybolacak**.</span><span class="sxs-lookup"><span data-stu-id="33ee8-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="33ee8-170"><a name="step2"></a>Bir API Management hizmeti geri yükleme</span><span class="sxs-lookup"><span data-stu-id="33ee8-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="33ee8-171">Önceden oluşturulmuş bir yedek hizmetinden bir API Management geri yüklemek için aşağıdaki HTTP isteği olun:</span><span class="sxs-lookup"><span data-stu-id="33ee8-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="33ee8-172">Burada:</span><span class="sxs-lookup"><span data-stu-id="33ee8-172">where:</span></span>

* <span data-ttu-id="33ee8-173">`subscriptionId`-içine bir yedeği geri yüklediğiniz API Management hizmeti içeren abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="33ee8-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="33ee8-174">`resourceGroupName`-'Api - varsayılan-{hizmeti-bölge}' biçiminde bir dize nerede `service-region` içine bir yedeği geri yüklediğiniz API Management hizmeti barındırıldığı, Azure bölgesi örneğin tanımlar`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="33ee8-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="33ee8-175">`serviceName`-hizmet uygulamasına geri yükleniyor, oluşturma sırasında belirtilen API Management adı</span><span class="sxs-lookup"><span data-stu-id="33ee8-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="33ee8-176">`api-version`-değiştirin`2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="33ee8-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="33ee8-177">İstek gövdesinde, yani Azure depolama hesabı adı, erişim tuşu, blob kapsayıcı adı ve yedek adı yedekleme dosyasının konumunu belirtin:</span><span class="sxs-lookup"><span data-stu-id="33ee8-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="33ee8-178">Değerini `Content-Type` istek üstbilgisi `application/json`.</span><span class="sxs-lookup"><span data-stu-id="33ee8-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="33ee8-179">Geri yüklemeyi tamamlamak için en az 30 dakika sürebileceğini uzun süren bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="33ee8-180">İstek başarılı oldu ve geri yükleme işlemi başlatıldı, alırsınız bir `202 Accepted` yanıt durum koduyla bir `Location` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="33ee8-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="33ee8-181">'GET istekleri URL'ye' olun `Location` işlemi durumunu öğrenmek için üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="33ee8-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="33ee8-182">Geri yükleme işlemi devam ederken '202 kabul edilen' almaya devam edeceksiniz durum kodu.</span><span class="sxs-lookup"><span data-stu-id="33ee8-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="33ee8-183">Bir yanıt kodu, `200 OK` geri yükleme işlemi başarılı şekilde tamamlandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="33ee8-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33ee8-184">**SKU** uygulamasına geri yükleniyor hizmetinin **eşleşmelidir** SKU yedeklenen hizmet geri yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="33ee8-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="33ee8-185">**Değişiklikleri** yaptığınız geri yükleme sırasında hizmet yapılandırma (örneğin API'leri, ilkeleri, Geliştirici Portalı Görünüm) için işlem devam ediyor **üzerine yazılabilir**.</span><span class="sxs-lookup"><span data-stu-id="33ee8-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="33ee8-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33ee8-186">Next steps</span></span>
<span data-ttu-id="33ee8-187">Yedekleme/geri yükleme işleminin iki farklı izlenecek yol aşağıdaki Microsoft blogları göz atın.</span><span class="sxs-lookup"><span data-stu-id="33ee8-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="33ee8-188">Azure API Management hesapları Çoğalt</span><span class="sxs-lookup"><span data-stu-id="33ee8-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="33ee8-189">Bu makalede her katkısı için Gisela için teşekkür ederiz.</span><span class="sxs-lookup"><span data-stu-id="33ee8-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="33ee8-190">Azure API Management: Yedekleme ve yapılandırmasını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="33ee8-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="33ee8-191">Ancak çok ilginç Stuart tarafından ayrıntılı yaklaşım resmi Kılavuzu eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="33ee8-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

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
