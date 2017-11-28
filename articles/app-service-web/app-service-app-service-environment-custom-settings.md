---
title: "Uygulama hizmeti ortamları için özel ayarları"
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
ms.openlocfilehash: 687475fae0c90713c15e8abbb92b71059eae81c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="8fb01-103">Uygulama hizmeti ortamları için özel yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="8fb01-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="8fb01-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8fb01-104">Overview</span></span>
<span data-ttu-id="8fb01-105">Uygulama hizmeti ortamları tek bir müşteri için yalıtılmış olduğundan, özel olarak App Service ortamları için uygulanabilecek bazı yapılandırma ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="8fb01-105">Because App Service Environments are isolated to a single customer, there are certain configuration settings that can be applied exclusively to App Service Environments.</span></span> <span data-ttu-id="8fb01-106">Bu makale App Service ortamları için kullanılabilen çeşitli belirli özelleştirmelere içermektedir.</span><span class="sxs-lookup"><span data-stu-id="8fb01-106">This article documents the various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="8fb01-107">Bir uygulama hizmeti ortamı yoksa bkz [bir uygulama hizmeti ortamı oluşturmak nasıl](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="8fb01-107">If you do not have an App Service Environment, see [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="8fb01-108">Bir dizi yeni kullanarak uygulama hizmeti ortamı özelleştirmeleri depolayabilirsiniz **clusterSettings** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="8fb01-108">You can store App Service Environment customizations by using an array in the new **clusterSettings** attribute.</span></span> <span data-ttu-id="8fb01-109">Bu öznitelik "Özellikler" sözlükte bulunan *hostingEnvironments* Azure Resource Manager varlığı.</span><span class="sxs-lookup"><span data-stu-id="8fb01-109">This attribute is found in the "Properties" dictionary of the *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="8fb01-110">Resource Manager şablonu kod parçacığında gösterildiği aşağıdaki kısaltılmış **clusterSettings** özniteliği:</span><span class="sxs-lookup"><span data-stu-id="8fb01-110">The following abbreviated Resource Manager template snippet shows the **clusterSettings** attribute:</span></span>

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

<span data-ttu-id="8fb01-111">**ClusterSettings** özniteliği uygulama hizmeti ortamı güncelleştirmek için bir Resource Manager şablonu dahil edilebilir.</span><span class="sxs-lookup"><span data-stu-id="8fb01-111">The **clusterSettings** attribute can be included in a Resource Manager template to update the App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-to-update-an-app-service-environment"></a><span data-ttu-id="8fb01-112">Bir uygulama hizmeti ortamı güncelleştirmek için Azure kaynak Gezgini'ni kullanma</span><span class="sxs-lookup"><span data-stu-id="8fb01-112">Use Azure Resource Explorer to update an App Service Environment</span></span>
<span data-ttu-id="8fb01-113">Alternatif olarak, uygulama hizmeti ortamı kullanarak güncelleştirebileceğinizi [Azure kaynak Gezgini](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fb01-113">Alternatively, you can update the App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="8fb01-114">Kaynak Gezgini, uygulama hizmeti ortamı için düğümüne gidin (**abonelikleri** > **resourceGroups** > **sağlayıcıları** > **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="8fb01-114">In Resource Explorer, go to the node for the App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="8fb01-115">Güncelleştirmek istediğiniz belirli uygulama hizmeti ortamı'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8fb01-115">Then click the specific App Service Environment that you want to update.</span></span>
2. <span data-ttu-id="8fb01-116">Sağ bölmede **okuma/yazma** kaynak Gezgini'nde düzenleme etkileşimli izin vermek için üst araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="8fb01-116">In the right pane, click **Read/Write** in the upper toolbar to allow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="8fb01-117">Mavi tıklatın **Düzenle** Resource Manager şablonu düzenlenebilir olmasını sağlamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fb01-117">Click the blue **Edit** button to make the Resource Manager template editable.</span></span>
4. <span data-ttu-id="8fb01-118">Sağ bölmede altına gidin.</span><span class="sxs-lookup"><span data-stu-id="8fb01-118">Scroll to the bottom of the right pane.</span></span> <span data-ttu-id="8fb01-119">**ClusterSettings** buradan girin veya değerini güncelleştirme çok altındaki bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="8fb01-119">The **clusterSettings** attribute is at the very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="8fb01-120">Yazın (veya kopyalayıp yapıştırın), istediğiniz yapılandırma değerleri dizisi **clusterSettings** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="8fb01-120">Type (or copy and paste) the array of configuration values you want in the **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="8fb01-121">Yeşil tıklatın **PUT** , düğme için uygulama hizmeti ortamı değişikliği kaydetmek için sağ bölmedeki üstünde bulunan.</span><span class="sxs-lookup"><span data-stu-id="8fb01-121">Click the green **PUT** button that's located at the top of the right pane to commit the change to the App Service Environment.</span></span>

<span data-ttu-id="8fb01-122">Değişiklik Gönder ancak değişikliğin etkili olması için uygulama hizmeti ortamında ön uçlar sayısı ile çarpılır yaklaşık 30 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="8fb01-122">However you submit the change, it takes roughly 30 minutes multiplied by the number of front ends in the App Service Environment for the change to take effect.</span></span>
<span data-ttu-id="8fb01-123">Örneğin, bir uygulama hizmeti ortamı dört ön uçlar varsa, kabaca tamamlamak yapılandırma güncelleştirmesi için iki saat sürer.</span><span class="sxs-lookup"><span data-stu-id="8fb01-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for the configuration update to finish.</span></span> <span data-ttu-id="8fb01-124">Yapılandırma değişikliği alınıyor sırada başka bir ölçeklendirme işlemleri veya yapılandırma değişiklik işlemleri uygulama hizmeti ortamı yerinde alabilir.</span><span class="sxs-lookup"><span data-stu-id="8fb01-124">While the configuration change is being rolled out, no other scaling operations or configuration change operations can take place in the App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="8fb01-125">TLS 1.0 devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="8fb01-125">Disable TLS 1.0</span></span>
<span data-ttu-id="8fb01-126">Yinelenen bir soru müşterilerden özellikle PCI uyumluluğunu ile ilgilenen müşteriler denetimleri, TLS 1.0 için uygulamalarını açıkça devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="8fb01-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how to explicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="8fb01-127">TLS 1.0 devre dışı bırakılabilir aşağıdaki aracılığıyla **clusterSettings** girişi:</span><span class="sxs-lookup"><span data-stu-id="8fb01-127">TLS 1.0 can be disabled through the following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="8fb01-128">Değişiklik TLS şifre paketi sırası</span><span class="sxs-lookup"><span data-stu-id="8fb01-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="8fb01-129">Başka bir soru müşterilerden kendi sunucu tarafından anlaşılan şifre listesi değiştirebilirsiniz ve bu değiştirerek elde olan **clusterSettings** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="8fb01-129">Another question from customers is if they can modify the list of ciphers negotiated by their server and this can be achieved by modifying the **clusterSettings** as shown below.</span></span> <span data-ttu-id="8fb01-130">Şifre paketleri kullanılabilir Listesi penceresinden alınabilir [bu MSDN makalesine](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="8fb01-130">The list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="8fb01-131">SChannel anlayamıyor şifre paketi için yanlış değerleri ayarlarsanız sunucunuza tüm TLS iletişim çalışmasını durdurabilir.</span><span class="sxs-lookup"><span data-stu-id="8fb01-131">If incorrect values are set for the cipher suite that SChannel cannot understand, all TLS communication to your server might stop functioning.</span></span> <span data-ttu-id="8fb01-132">Böyle bir durumda kaldırmanız gerekecek *FrontEndSSLCipherSuiteOrder* girdisinden **clusterSettings** ve varsayılan şifre paketi ayarlarına geri dönmek için güncelleştirilmiş Resource Manager şablonu gönderin.</span><span class="sxs-lookup"><span data-stu-id="8fb01-132">In such a case, you will need to remove the *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit the updated Resource Manager template to revert back to the default cipher suite settings.</span></span>  <span data-ttu-id="8fb01-133">Lütfen bu işlevi dikkatli kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fb01-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="8fb01-134">başlarken</span><span class="sxs-lookup"><span data-stu-id="8fb01-134">Get started</span></span>
<span data-ttu-id="8fb01-135">Bir şablonu temel tanımıyla Azure hızlı başlangıç Resource Manager şablonu sitesi içeren [bir uygulama hizmeti ortamı oluşturma](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="8fb01-135">The Azure Quickstart Resource Manager template site includes a template with the base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
