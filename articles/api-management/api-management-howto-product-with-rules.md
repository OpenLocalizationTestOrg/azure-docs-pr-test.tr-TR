---
title: aaaProtect API'nizi Azure API Management ile | Microsoft Docs
description: "Bilgi nasıl tooprotect API'nizi kotalar ve azaltma (hız sınırlama) ilkeleri."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="5cb56-103">API’nizi, Azure API Management kullanarak hız sınırlarıyla koruma | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5cb56-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="5cb56-104">Bu kılavuz size nasıl kolay tooadd koruma arka uç API'niz için Azure API Management ile hız sınırı ve kota ilkeleri yapılandırarak olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="5cb56-105">Bu öğreticide geliştiricilerinin sağlayan "Ücretsiz deneme" API ürünü oluşturacaksınız toomake tooa maksimum 200 çağrı hello kullanarak hafta tooyour API başına yukarı too10 çağrıları dakikada kurup [abonelik başına çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) ve [ Abonelik başına kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="5cb56-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="5cb56-106">Sonra yayımlama hello API ve hello hız sınırı ilkesini test.</span><span class="sxs-lookup"><span data-stu-id="5cb56-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="5cb56-107">Daha gelişmiş azaltma senaryoları hello için [anahtar tarafından hızı sınırı](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) ve [kota anahtarı](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) ilkeleri Bkz [Gelişmiş istek azaltma Azure API Management ile](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="5cb56-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="5cb56-108"><a name="create-product"></a>toocreate bir ürün</span><span class="sxs-lookup"><span data-stu-id="5cb56-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="5cb56-109">Bu adımda, abonelik onayı gerektirmeyen bir Ücretsiz Deneme ürünü oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5cb56-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="5cb56-110">Zaten yapılandırılmış bir ürününüz varsa ve toouse istediğiniz varsa, Bu öğretici için önceden çok atlayabilirsiniz[yapılandırma çağrı hızı sınırı ve kota ilkeleri] [ Configure call rate limit and quota policies] ve ürününüzü kullanarak buradan hello öğreticisini izleyin Merhaba ücretsiz deneme ürünü yerine.</span><span class="sxs-lookup"><span data-stu-id="5cb56-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="5cb56-111">başlatıldı, tooget tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="5cb56-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="5cb56-113">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [ilk API'nizi Azure API Management'te yönetme] [ Manage your first API in Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="5cb56-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="5cb56-114">Tıklatın **ürünleri** hello içinde **API Management** hello sol toodisplay hello menüsünde **ürünleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5cb56-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Ürün ekleme][api-management-add-product]

<span data-ttu-id="5cb56-116">Tıklatın **Ekle ürün** toodisplay hello **Ekle yeni ürün** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="5cb56-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Yeni ürün ekleme][api-management-new-product-window]

<span data-ttu-id="5cb56-118">Merhaba, **başlık** kutusuna **ücretsiz deneme**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="5cb56-119">Merhaba, **açıklama** kutusu, metin aşağıdaki türü hello: **aboneleri mümkün toorun 10 çağrıları dakikada tooa en fazla 200 çağrı/hafta sonra erişim reddedildi yukarı olacaktır.**</span><span class="sxs-lookup"><span data-stu-id="5cb56-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="5cb56-120">API Management ürünleri açık ya da korumalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="5cb56-121">Korumalı ürünlerin kullanılabilmesi için abone toobefore olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="5cb56-122">Açık ürünler abonelik olmadan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="5cb56-123">Emin **abonelik iste** seçili toocreate bir abonelik gerektiren korumalı bir üründür.</span><span class="sxs-lookup"><span data-stu-id="5cb56-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="5cb56-124">Merhaba varsayılan ayar budur.</span><span class="sxs-lookup"><span data-stu-id="5cb56-124">This is hello default setting.</span></span>

<span data-ttu-id="5cb56-125">Bir yönetici tooreview istediğiniz ve kabul edin veya reddedin abonelik girişimleri toothis ürün varsa belirleyin **abonelik onayı iste**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="5cb56-126">Hello onay kutusu seçili değilse abonelik girişimleri otomatik olarak onaylanır.</span><span class="sxs-lookup"><span data-stu-id="5cb56-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="5cb56-127">Bu örnekte, abonelik otomatik olarak, hello kutuyu işaretlemeyin şekilde onaylanır.</span><span class="sxs-lookup"><span data-stu-id="5cb56-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="5cb56-128">tooallow Geliştirici hesaplarını toosubscribe birden çok kez toohello yeni ürün, select hello **birden çok aboneliğe izin** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="5cb56-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="5cb56-129">Bu öğretici aynı anda birden çok abonelik kullanmaz, bu nedenle onay kutusunu işaretlenmemiş olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="5cb56-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="5cb56-130">Tüm değerleri girdikten sonra tıklatın **kaydetmek** toocreate hello ürün.</span><span class="sxs-lookup"><span data-stu-id="5cb56-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Ürün eklendi][api-management-product-added]

<span data-ttu-id="5cb56-132">Varsayılan olarak, yeni ürünleri hello içinde görünür toousers olan **Yöneticiler** grubu.</span><span class="sxs-lookup"><span data-stu-id="5cb56-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="5cb56-133">Biz tooadd hello kalacaklarını **geliştiriciler** grubu.</span><span class="sxs-lookup"><span data-stu-id="5cb56-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="5cb56-134">' I tıklatın **ücretsiz deneme**ve ardından hello **görünürlük** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5cb56-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="5cb56-135">API Management'te, ürünlerin toodevelopers kullanılan toomanage hello görünürlüğünü gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="5cb56-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="5cb56-136">Ürünler görünürlük toogroups vermek ve geliştiricilerin görüntülemek ve, ait oldukları görünür toohello grupları toohello ürünleri abone.</span><span class="sxs-lookup"><span data-stu-id="5cb56-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="5cb56-137">Daha fazla bilgi için bkz: [nasıl toocreate ve kullanım grupları Azure API Management'te][How toocreate and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="5cb56-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Geliştiriciler grubu ekleme][api-management-add-developers-group]

<span data-ttu-id="5cb56-139">Select hello **geliştiriciler** onay kutusunu işaretleyin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="5cb56-140"><a name="add-api"></a>tooadd bir API toohello ürün</span><span class="sxs-lookup"><span data-stu-id="5cb56-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="5cb56-141">Merhaba öğreticinin bu adımında, hello Echo API'si toohello yeni ücretsiz deneme ürünü ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="5cb56-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="5cb56-142">Her API Management hizmet örneği ile kullanılan tooexperiment ve API Management hakkında bilgi edinin bir Echo API'si ile önceden yapılandırılmış olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="5cb56-143">Daha fazla bilgi için bkz. [Azure API Management'te ilk API'nizi yönetme][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="5cb56-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="5cb56-144">Tıklatın **ürünleri** hello gelen **API Management** sol hello ve ardından menüsünde **ücretsiz deneme** tooconfigure hello ürün.</span><span class="sxs-lookup"><span data-stu-id="5cb56-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Ürünü yapılandırma][api-management-configure-product]

<span data-ttu-id="5cb56-146">Tıklatın **API Ekle tooproduct**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-146">Click **Add API tooproduct**.</span></span>

![API tooproduct Ekle][api-management-add-api]

<span data-ttu-id="5cb56-148">**Echo API’si** seçeneğini belirleyin ve ardından **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cb56-148">Select **Echo API**, and then click **Save**.</span></span>

![Echo API’si ekleme][api-management-add-echo-api]

## <span data-ttu-id="5cb56-150"><a name="policies"></a>tooconfigure çağrı hızı sınırı ve kota ilkeleri</span><span class="sxs-lookup"><span data-stu-id="5cb56-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="5cb56-151">Oran sınırları ve kotalar hello İlkesi Düzenleyicisi'nde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="5cb56-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="5cb56-152">Biz ekleyerek bu öğreticide hello iki ilkelerdir hello [abonelik başına çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) ve [abonelik başına kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="5cb56-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="5cb56-153">Bu ilkeler hello ürün kapsamda uygulanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="5cb56-154">Tıklatın **ilkeleri** hello altında **API Management** hello sol menüsünde.</span><span class="sxs-lookup"><span data-stu-id="5cb56-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="5cb56-155">Merhaba, **ürün** tıklatın **ücretsiz deneme**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-155">In hello **Product** list, click **Free Trial**.</span></span>

![Ürün ilkesi][api-management-product-policy]

<span data-ttu-id="5cb56-157">Tıklatın **ilke Ekle** tooimport hello ilkesi şablonunu ve hello hız sınırı ve kota ilkeleri oluşturmaya başlamak.</span><span class="sxs-lookup"><span data-stu-id="5cb56-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![İlke ekleme][api-management-add-policy]

<span data-ttu-id="5cb56-159">Hız sınırı ve kota ilkeleri gelen hello gelen öğesindeki bunu konumu hello imleç ilkeleridir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![İlke düzenleyicisi][api-management-policy-editor-inbound]

<span data-ttu-id="5cb56-161">İlkeleri hello listesini kaydırın ve hello bulun **abonelik başına çağrı hızını sınırla** İlkesi girişi.</span><span class="sxs-lookup"><span data-stu-id="5cb56-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![İlke deyimleri][api-management-limit-policies]

<span data-ttu-id="5cb56-163">Merhaba sonra imleç hello konumlandırıldı **gelen** ilke öğesi hello yanındaki oka **abonelik başına çağrı hızını sınırla** tooinsert kendi ilke şablonunu.</span><span class="sxs-lookup"><span data-stu-id="5cb56-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="5cb56-164">Merhaba parçacığı görebileceğiniz gibi hello İlkesi sınırlarını ayarlama hello ürünün API'ler ve işlemler için sağlar.</span><span class="sxs-lookup"><span data-stu-id="5cb56-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="5cb56-165">Bu öğreticide biz değil Bu özelliği kullanın, böylece hello silme **API** ve **işlemi** hello öğelerinden **hızı sınırı** öğesi, yalnızca dış hellogibi**hızı sınırı** hello aşağıdaki örnekte gösterildiği gibi öğe kalır.</span><span class="sxs-lookup"><span data-stu-id="5cb56-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="5cb56-166">Merhaba Ücretsiz Deneme ürününde hello izin verilen maksimum çağrı hızı dakikada 10 çağrı olan, bu nedenle **10** hello hello değeri olarak **çağrıları** özniteliği ve **60** hello için**yenileme süresini** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5cb56-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="5cb56-167">tooconfigure hello **abonelik başına kullanım kotası ayarla** ilke, konum imlecinizi hello hemen altında yeni eklenen **hızı sınırı** öğesi hello içinde **gelen** öğesini ve ardından bulup hello ok toohello solundaki tıklayın **abonelik başına kullanım kotası ayarla**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="5cb56-168">Benzer şekilde toohello **abonelik başına kullanım kotası ayarla** İlkesi **abonelik başına kullanım kotası ayarla** ilke verir hello ürünün API'ler ve işlemler büyük harfler için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="5cb56-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="5cb56-169">Bu öğreticide biz değil Bu özelliği kullanın, böylece hello silme **API** ve **işlemi** hello öğelerinden **kota** hello aşağıdaki örnekte gösterildiği gibi öğesi.</span><span class="sxs-lookup"><span data-stu-id="5cb56-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="5cb56-170">Kotalar hello başına çağrı sayısı aralık, bant genişliği veya her ikisini temel alabilir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="5cb56-171">Bu öğreticide, biz bant genişliği temelinde azaltma yapmıyoruz, bu nedenle hello silme **bant genişliği** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5cb56-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="5cb56-172">Merhaba Ücretsiz Deneme ürününde hello kota haftada 200 çağrı ' dir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="5cb56-173">Belirtin **200** hello hello değeri olarak **çağrıları** özniteliği ve ardından belirtin **604800** hello hello değeri olarak **yenileme süresini** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5cb56-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="5cb56-174">İlke aralıkları saniye cinsinden belirtilir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="5cb56-175">toocalculate hello aralığı bir hafta hello hello (60)'hello bir dakikadaki (60) saniye sayısı'e kadar bir saatteki dakika sayısı (24) günde saat sayısını (7) günlere hello sayısı Çarp: 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="5cb56-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="5cb56-176">Merhaba ilke yapılandırmayı tamamladığınızda, aşağıdaki örneğine hello eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="5cb56-177">İlkeleri yapılandırılır Hello istenen sonra tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-177">After hello desired policies are configured, click **Save**.</span></span>

![İlkeyi kaydetme][api-management-policy-save]

## <span data-ttu-id="5cb56-179"><a name="publish-product"></a> toopublish hello ürün</span><span class="sxs-lookup"><span data-stu-id="5cb56-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="5cb56-180">Böylece geliştiriciler tarafından kullanılan hello hello API'ler eklenmiştir ve hello ilkelerin yapılandırıldığına göre hello ürünün yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="5cb56-181">Tıklatın **ürünleri** hello gelen **API Management** sol hello ve ardından menüsünde **ücretsiz deneme** tooconfigure hello ürün.</span><span class="sxs-lookup"><span data-stu-id="5cb56-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Ürünü yapılandırma][api-management-configure-product]

<span data-ttu-id="5cb56-183">Tıklatın **Yayımla**ve ardından **Evet, Yayımla** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="5cb56-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Ürünü yayımlama][api-management-publish-product]

## <span data-ttu-id="5cb56-185"><a name="subscribe-account"></a>toosubscribe bir geliştirici hesabı toohello ürün</span><span class="sxs-lookup"><span data-stu-id="5cb56-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="5cb56-186">Merhaba ürünün yayımlanan artık, geliştiriciler tarafından kullanılan abone kullanılabilir toobe tooand olur.</span><span class="sxs-lookup"><span data-stu-id="5cb56-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="5cb56-187">Bir API Management örneğinin yöneticileri otomatik olarak abone tooevery ürün olur.</span><span class="sxs-lookup"><span data-stu-id="5cb56-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="5cb56-188">Bu öğretici adımında, biz hello yönetici olmayan Geliştirici hesaplarını toohello ücretsiz deneme ürünü birini abone olur.</span><span class="sxs-lookup"><span data-stu-id="5cb56-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="5cb56-189">Geliştirici hesabınızda hello Yöneticiler rolünün bir parçası ise, zaten abone olmanıza rağmen bu adımın üzerinden izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cb56-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="5cb56-190">Tıklatın **kullanıcılar** hello üzerinde **API Management** hello menüsünde sol ve ardından Geliştirici hesabınızın hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cb56-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="5cb56-191">Bu örnekte, hello kullanıyoruz **Clayton Gragg** Geliştirici hesabı.</span><span class="sxs-lookup"><span data-stu-id="5cb56-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Geliştirici yapılandırma][api-management-configure-developer]

<span data-ttu-id="5cb56-193">**Abonelik Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cb56-193">Click **Add Subscription**.</span></span>

![Abonelik ekleme][api-management-add-subscription-menu]

<span data-ttu-id="5cb56-195">**Ücretsiz Deneme**’yi seçin ve ardından **Abone ol**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cb56-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Abonelik ekleme][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="5cb56-197">Bu öğreticide, birden çok aboneliğe hello ücretsiz deneme ürünü için etkin değil.</span><span class="sxs-lookup"><span data-stu-id="5cb56-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="5cb56-198">Etkin olsaydı hello aşağıdaki örnekte gösterildiği gibi istendiğinde tooname hello abonelik olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5cb56-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![Abonelik ekleme][api-management-add-subscription-multiple]

<span data-ttu-id="5cb56-200">' I tıklattıktan sonra **abone ol**, hello ürün görünür hello **abonelik** hello kullanıcıya listesi.</span><span class="sxs-lookup"><span data-stu-id="5cb56-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![Abonelik eklendi][api-management-subscription-added]

## <span data-ttu-id="5cb56-202"><a name="test-rate-limit"></a>toocall bir işlemi ve test hello hızı sınırı</span><span class="sxs-lookup"><span data-stu-id="5cb56-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="5cb56-203">Merhaba ücretsiz deneme ürünü yayımlanmış ve yapılandırılmış olduğuna göre biz bazı işlemler çağırabilir ve hello hız sınırı ilkesini test.</span><span class="sxs-lookup"><span data-stu-id="5cb56-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="5cb56-204">Anahtar toohello Geliştirici Portalı'ı tıklatarak **Geliştirici Portalı** hello sağ üst menüsünde.</span><span class="sxs-lookup"><span data-stu-id="5cb56-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![Geliştirici portalı][api-management-developer-portal-menu]

<span data-ttu-id="5cb56-206">Tıklatın **API'leri** hello üst menü ve ardından **Echo API'si**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![Geliştirici portalı][api-management-developer-portal-api-menu]

<span data-ttu-id="5cb56-208">**GET Kaynağı**’na ve ardından **Deneyin**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cb56-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Konsolu açma][api-management-open-console]

<span data-ttu-id="5cb56-210">Merhaba varsayılan parametre değerlerini koruyun ve ardından hello ücretsiz deneme ürünü için abonelik anahtarınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="5cb56-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![Abonelik anahtarı][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="5cb56-212">Birden çok aboneliğiniz varsa, emin tooselect hello anahtarı olması **ücretsiz deneme**, veya hello önceki adımlarda yapılandırılmış başka hello ilkeleri etkili olmayacak.</span><span class="sxs-lookup"><span data-stu-id="5cb56-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="5cb56-213">Tıklatın **Gönder**ve ardından hello yanıtı görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5cb56-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="5cb56-214">Not hello **yanıt durumu** , **200 Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5cb56-214">Note hello **Response status** of **200 OK**.</span></span>

![İşlem sonuçları][api-management-http-get-results]

<span data-ttu-id="5cb56-216">Tıklatın **Gönder** dakikada 10 çağrı hello hız sınır ilkesinden daha büyük bir hızda.</span><span class="sxs-lookup"><span data-stu-id="5cb56-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="5cb56-217">Merhaba hız sınırı İlkesi aşıldıktan sonra yanıt durumu **429 çok fazla istek** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5cb56-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![İşlem sonuçları][api-management-http-get-429]

<span data-ttu-id="5cb56-219">Merhaba **yanıt içeriği** hello yeniden denemeler başarılı olmadan önce kalan aralığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="5cb56-220">Dakikada 10 çağrı Hello hız sınırı ilkesi etkinken, hello 60 saniye geçinceye kadar sonraki çağrılar başarısız olur hello hız sınırı aşılmadan önce hello 10 başarılı çağrının toohello ürünün ilk.</span><span class="sxs-lookup"><span data-stu-id="5cb56-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="5cb56-221">Bu örnekte, aralık kalan hello 54 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="5cb56-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="5cb56-222"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5cb56-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="5cb56-223">Video aşağıdaki hello oran sınırlarını ve kotaları ayarlama gösterisini izleyin.</span><span class="sxs-lookup"><span data-stu-id="5cb56-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
