---
title: "Uygulama hizmeti ortamları için aaaCustom ayarları"
description: "Uygulama hizmeti ortamları için özel yapılandırma ayarları"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="0bb79-103">Uygulama hizmeti ortamları için özel yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="0bb79-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="0bb79-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0bb79-104">Overview</span></span>
<span data-ttu-id="0bb79-105">Uygulama hizmeti ortamları yalıtılmış tooa tek müşteri olduğundan var. özel olarak tooApp hizmeti ortamları olabilir yapılandırma ayarları uygulanan belirli</span><span class="sxs-lookup"><span data-stu-id="0bb79-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="0bb79-106">Bu makale belgeleri App Service ortamları için kullanılabilen çeşitli belirli özelleştirmelere hello.</span><span class="sxs-lookup"><span data-stu-id="0bb79-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="0bb79-107">Bir uygulama hizmeti ortamı yoksa bkz [nasıl tooCreate bir uygulama hizmeti ortamı](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="0bb79-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="0bb79-108">Bir dizi hello yeni kullanarak uygulama hizmeti ortamı özelleştirmeleri depolayabilir **clusterSettings** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0bb79-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="0bb79-109">Bu öznitelik hello "Özellikler" sözlüğü hello içinde bulunan *hostingEnvironments* Azure Resource Manager varlığı.</span><span class="sxs-lookup"><span data-stu-id="0bb79-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="0bb79-110">Merhaba aşağıdaki kısaltılmış Resource Manager şablonu parçacığını gösterir hello **clusterSettings** özniteliği:</span><span class="sxs-lookup"><span data-stu-id="0bb79-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="0bb79-111">Merhaba **clusterSettings** özniteliği bir Resource Manager şablonu tooupdate hello uygulama hizmeti ortamı dahil edilebilir.</span><span class="sxs-lookup"><span data-stu-id="0bb79-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="0bb79-112">Azure kaynak Gezgini tooupdate bir uygulama hizmeti ortamı kullanın</span><span class="sxs-lookup"><span data-stu-id="0bb79-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="0bb79-113">Alternatif olarak, hello uygulama hizmeti ortamı kullanarak güncelleştirebileceğinizi [Azure kaynak Gezgini](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bb79-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="0bb79-114">Kaynak Gezgini'nde hello uygulama hizmeti ortamı için toohello düğümüne gidin (**abonelikleri** > **resourceGroups** > **sağlayıcıları**  >  **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="0bb79-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="0bb79-115">Merhaba tooupdate istediğiniz belirli uygulama hizmeti ortamı'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0bb79-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="0bb79-116">Merhaba sağ bölmede **okuma/yazma** hello üst araç tooallow kaynak Gezgini'nde düzenleme etkileşimli olarak.</span><span class="sxs-lookup"><span data-stu-id="0bb79-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="0bb79-117">Merhaba mavi tıklatın **Düzenle** düğmesini toomake hello Resource Manager şablonu düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="0bb79-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="0bb79-118">Toohello bölmesinin hello sağa kaydırın.</span><span class="sxs-lookup"><span data-stu-id="0bb79-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="0bb79-119">Merhaba **clusterSettings** buradan girin veya değerini güncelleştirme hello çok altındaki bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="0bb79-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="0bb79-120">Hello istediğiniz yapılandırma değerlerini yazın (veya Kopyala ve Yapıştır) hello dizisi **clusterSettings** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0bb79-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="0bb79-121">Hello yeşil tıklatın **PUT** , düğme hello sağ bölmede toocommit hello değişiklik toohello uygulama hizmeti ortamı hello üstünde bulunan.</span><span class="sxs-lookup"><span data-stu-id="0bb79-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="0bb79-122">Merhaba değişiklik Gönder ancak hello değişikliğin tootake Merhaba uygulama hizmeti ortamı'nda ön uçlar hello sayısı ile çarpılır yaklaşık 30 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="0bb79-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="0bb79-123">Örneğin, bir uygulama hizmeti ortamı dört ön uçlar varsa, kabaca hello yapılandırmasını güncelleştirme toofinish için iki saat sürer.</span><span class="sxs-lookup"><span data-stu-id="0bb79-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="0bb79-124">Merhaba yapılandırma değişikliği alınıyor sırada başka bir ölçeklendirme işlemleri veya yapılandırma değişiklik işlemleri hello uygulama hizmeti ortamı yerinde alabilir.</span><span class="sxs-lookup"><span data-stu-id="0bb79-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="0bb79-125">TLS 1.0 devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="0bb79-125">Disable TLS 1.0</span></span>
<span data-ttu-id="0bb79-126">Yinelenen bir soru müşterilerden özellikle PCI uyumluluğunu ile ilgilenen müşteriler denetimleri, nasıl tooexplicitly devre dışı TLS 1.0 için uygulamalarını.</span><span class="sxs-lookup"><span data-stu-id="0bb79-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="0bb79-127">TLS 1.0 devre dışı bırakılabilir hello aşağıdaki aracılığıyla **clusterSettings** girişi:</span><span class="sxs-lookup"><span data-stu-id="0bb79-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="0bb79-128">Değişiklik TLS şifre paketi sırası</span><span class="sxs-lookup"><span data-stu-id="0bb79-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="0bb79-129">Başka bir soru müşterilerden kendi sunucu tarafından anlaşılan şifrelemeleri hello listesi değiştirebilirsiniz ve bu hello değiştirerek elde olan **clusterSettings** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="0bb79-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="0bb79-130">Şifre paketleri kullanılabilir Hello listesi alınabileceği [bu MSDN makalesine](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="0bb79-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="0bb79-131">SChannel anlayamıyor hello şifre paketi için yanlış değerleri ayarlarsanız, tüm TLS iletişim tooyour server çalışmasını durdurabilir.</span><span class="sxs-lookup"><span data-stu-id="0bb79-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="0bb79-132">Böyle bir durumda tooremove hello gerekir *FrontEndSSLCipherSuiteOrder* girdisinden **clusterSettings** ve hello güncelleştirilmiş Resource Manager şablonu toorevert geri toohello varsayılan şifre gönderin Suite ayarları.</span><span class="sxs-lookup"><span data-stu-id="0bb79-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="0bb79-133">Lütfen bu işlevi dikkatli kullanın.</span><span class="sxs-lookup"><span data-stu-id="0bb79-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="0bb79-134">başlarken</span><span class="sxs-lookup"><span data-stu-id="0bb79-134">Get started</span></span>
<span data-ttu-id="0bb79-135">Hello Azure hızlı başlangıç Resource Manager şablonu sitesi içeren hello temel tanımı için bir şablonla [bir uygulama hizmeti ortamı oluşturma](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="0bb79-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
