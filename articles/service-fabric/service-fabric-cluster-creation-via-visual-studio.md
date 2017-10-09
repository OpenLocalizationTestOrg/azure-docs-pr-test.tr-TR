---
title: "Visual Studio kullanarak Service Fabric kümesi aaaSetting | Microsoft Docs"
description: "Service Fabric yukarı tooset nasıl küme Visual Studio'da bir Azure kaynak grubu projesi tarafından oluşturulan Azure Resource Manager şablonu kullanarak açıklar"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="4d478-103">Visual Studio kullanarak bir Service Fabric kümesi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4d478-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="4d478-104">Bu makalede, Azure Service Fabric yukarı tooset nasıl küme Visual Studio ve Azure Resource Manager şablonu kullanarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d478-104">This article describes how tooset up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="4d478-105">Bir Visual Studio Azure kaynak grubu projesi toocreate hello şablonu kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="4d478-105">We will use a Visual Studio Azure resource group project toocreate hello template.</span></span> <span data-ttu-id="4d478-106">Merhaba şablonu oluşturulduktan sonra dağıtılabilir doğrudan tooAzure Visual Studio'dan.</span><span class="sxs-lookup"><span data-stu-id="4d478-106">After hello template has been created, it can be deployed directly tooAzure from Visual Studio.</span></span> <span data-ttu-id="4d478-107">Ayrıca bir komut dosyasından veya sürekli tümleştirme (CI) tesis parçası olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d478-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="4d478-108">Bir Azure kaynak grubu projesi kullanarak bir Service Fabric kümesi şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d478-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="4d478-109">tooget başlatıldı, Visual Studio'yu açın ve bir Azure kaynak grubu projesi oluşturun (hello kullanılabilir **bulut** klasörü):</span><span class="sxs-lookup"><span data-stu-id="4d478-109">tooget started, open Visual Studio and create an Azure resource group project (it is available in hello **Cloud** folder):</span></span>

![Seçili Azure kaynak grubu projesi ile yeni proje iletişim kutusu][1]

<span data-ttu-id="4d478-111">Bu proje için yeni bir Visual Studio çözümü oluşturun veya varolan bir çözümü tooan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4d478-111">You can create a new Visual Studio solution for this project or add it tooan existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="4d478-112">Hello Azure kaynak grubu projesi hello bulut düğümü altında görmüyorsanız hello Azure SDK'sı yok.</span><span class="sxs-lookup"><span data-stu-id="4d478-112">If you do not see hello Azure resource group project under hello Cloud node, you do not have hello Azure SDK installed.</span></span> <span data-ttu-id="4d478-113">Web Platformu yükleyicisi başlatın ([şimdi yüklemek](http://www.microsoft.com/web/downloads/platform.aspx) henüz yapmadıysanız) ve ".NET için Azure SDK'sı" ve Visual Studio sürümünüzle uyumlu yükleme hello sürüm için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="4d478-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install hello version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="4d478-114">Visual Studio hello Tamam düğmesine basın sonra toocreate istediğiniz tooselect hello Resource Manager şablonu ister:</span><span class="sxs-lookup"><span data-stu-id="4d478-114">After you hit hello OK button, Visual Studio will ask you tooselect hello Resource Manager template you want toocreate:</span></span>

![Azure şablonu iletişim kutusu seçili Service Fabric kümesi şablonla seçin][2]

<span data-ttu-id="4d478-116">İsabet hello Tamam düğmesi ve Hello Service Fabric kümesi şablonu yeniden seçin.</span><span class="sxs-lookup"><span data-stu-id="4d478-116">Select hello Service Fabric Cluster template and hit hello OK button again.</span></span> <span data-ttu-id="4d478-117">Merhaba proje ve hello Resource Manager şablonu şimdi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="4d478-117">hello project and hello Resource Manager template have now been created.</span></span>

## <a name="prepare-hello-template-for-deployment"></a><span data-ttu-id="4d478-118">Merhaba şablonu dağıtımı için hazırlama</span><span class="sxs-lookup"><span data-stu-id="4d478-118">Prepare hello template for deployment</span></span>
<span data-ttu-id="4d478-119">Dağıtılan toocreate hello küme Hello şablonudur önce gerekli hello şablon parametreleri için değerler sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d478-119">Before hello template is deployed toocreate hello cluster, you must provide values for hello required template parameters.</span></span> <span data-ttu-id="4d478-120">Bu parametre değerleri hello salt okunurdur `ServiceFabricCluster.parameters.json` hello dosyasını `Templates` hello kaynak grubu projesi klasörü.</span><span class="sxs-lookup"><span data-stu-id="4d478-120">These parameter values are read from hello `ServiceFabricCluster.parameters.json` file, which is in hello `Templates` folder of hello resource group project.</span></span> <span data-ttu-id="4d478-121">Merhaba dosyasını açın ve değerleri aşağıdaki hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="4d478-121">Open hello file and provide hello following values:</span></span>

| <span data-ttu-id="4d478-122">Parametre adı</span><span class="sxs-lookup"><span data-stu-id="4d478-122">Parameter name</span></span> | <span data-ttu-id="4d478-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4d478-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4d478-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="4d478-124">adminUserName</span></span> |<span data-ttu-id="4d478-125">Service Fabric makineler (düğümler) hello yönetici hesabı adı Hello.</span><span class="sxs-lookup"><span data-stu-id="4d478-125">hello name of hello administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="4d478-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="4d478-126">certificateThumbprint</span></span> |<span data-ttu-id="4d478-127">Merhaba küme korur hello sertifikanın parmak izini hello.</span><span class="sxs-lookup"><span data-stu-id="4d478-127">hello thumbprint of hello certificate that secures hello cluster.</span></span> |
| <span data-ttu-id="4d478-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="4d478-128">sourceVaultResourceId</span></span> |<span data-ttu-id="4d478-129">Merhaba *kaynak kimliği* hello anahtar kasasının hello küme korur hello sertifikanın depolandığı.</span><span class="sxs-lookup"><span data-stu-id="4d478-129">hello *resource ID* of hello key vault where hello certificate that secures hello cluster is stored.</span></span> |
| <span data-ttu-id="4d478-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="4d478-130">certificateUrlValue</span></span> |<span data-ttu-id="4d478-131">Merhaba küme güvenlik sertifikası Hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="4d478-131">hello URL of hello cluster security certificate.</span></span> |

<span data-ttu-id="4d478-132">Merhaba Visual Studio Service Fabric Resource Manager şablonu bir sertifika tarafından korunan güvenli bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4d478-132">hello Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="4d478-133">Bu sertifika hello tarafından tanımlanan üç şablon parametreleri en son (`certificateThumbprint`, `sourceVaultValue`, ve `certificateUrlValue`), ve bunu bulunmalıdır bir **Azure anahtar kasası**.</span><span class="sxs-lookup"><span data-stu-id="4d478-133">This certificate is identified by hello last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="4d478-134">Nasıl toocreate hello küme güvenlik sertifikası ile ilgili daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) makalesi.</span><span class="sxs-lookup"><span data-stu-id="4d478-134">For more information on how toocreate hello cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-hello-cluster-name"></a><span data-ttu-id="4d478-135">İsteğe bağlı: hello küme adını değiştirin</span><span class="sxs-lookup"><span data-stu-id="4d478-135">Optional: change hello cluster name</span></span>
<span data-ttu-id="4d478-136">Her Service Fabric kümesi bir adı vardır.</span><span class="sxs-lookup"><span data-stu-id="4d478-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="4d478-137">Azure'da bir Fabric kümesi oluşturduğunuzda, küme adı (hello Azure bölgesi ile birlikte) belirler hello kümesi için hello etki alanı adı sistemi (DNS) ad.</span><span class="sxs-lookup"><span data-stu-id="4d478-137">When a Fabric cluster is created in Azure, cluster name determines (together with hello Azure region) hello Domain Name System (DNS) name for hello cluster.</span></span> <span data-ttu-id="4d478-138">Örneğin, küme adı, `myBigCluster`ve hello yeni küme barındıracak hello kaynak grubu (Azure bölgesi) konumunu hello Doğu ABD, hello kümenin hello DNS adı olacaktır `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="4d478-138">For example, if you name your cluster `myBigCluster`, and hello location (Azure region) of hello resource group that will host hello new cluster is East US, hello DNS name of hello cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="4d478-139">Varsayılan olarak hello küme adı otomatik olarak oluşturulur ve bir rastgele soneki tooa "Küme" önek ekleyerek benzersiz yapılan.</span><span class="sxs-lookup"><span data-stu-id="4d478-139">By default hello cluster name is generated automatically and made unique by attaching a random suffix tooa "cluster" prefix.</span></span> <span data-ttu-id="4d478-140">Bu çok kolay toouse hello şablonunun parçası olarak kolaylaştırır bir **sürekli tümleştirme** (CI) sistem.</span><span class="sxs-lookup"><span data-stu-id="4d478-140">This makes it very easy toouse hello template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="4d478-141">Toouse istiyorsanız, küme, anlamlı tooyou olan bir için belirli bir ad hello hello değerini `clusterName` hello Resource Manager şablonu dosyasındaki değişken (`ServiceFabricCluster.json`) seçilen tooyour adı.</span><span class="sxs-lookup"><span data-stu-id="4d478-141">If you want toouse a specific name for your cluster, one that is meaningful tooyou, set hello value of hello `clusterName` variable in hello Resource Manager template file (`ServiceFabricCluster.json`) tooyour chosen name.</span></span> <span data-ttu-id="4d478-142">Bu dosyada bulunan tanımlanan hello ilk değişkenidir.</span><span class="sxs-lookup"><span data-stu-id="4d478-142">It is hello first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="4d478-143">İsteğe bağlı: genel uygulama bağlantı noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="4d478-143">Optional: add public application ports</span></span>
<span data-ttu-id="4d478-144">Dağıtmadan önce toochange hello ortak uygulama bağlantı noktaları için hello küme isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d478-144">You may also want toochange hello public application ports for hello cluster before you deploy it.</span></span> <span data-ttu-id="4d478-145">Varsayılan olarak, yalnızca iki ortak TCP bağlantı noktalarını (80 ve 8081) hello şablonu açar.</span><span class="sxs-lookup"><span data-stu-id="4d478-145">By default, hello template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="4d478-146">Daha fazla bilgi için uygulamalarınızı gerekiyorsa, hello şablonunda hello Azure yük dengeleyici tanımını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4d478-146">If you need more for your applications, modify hello Azure Load Balancer definition in hello template.</span></span> <span data-ttu-id="4d478-147">Merhaba tanımı hello ana şablon dosyasında depolanan (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="4d478-147">hello definition is stored in hello main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="4d478-148">Bu dosyayı açın ve arama `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="4d478-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="4d478-149">Her bağlantı noktası üç yapılar ile ilişkilidir:</span><span class="sxs-lookup"><span data-stu-id="4d478-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="4d478-150">Başlangıç bağlantı noktası için hello TCP bağlantı noktası değeri tanımlayan Şablon değişkeni:</span><span class="sxs-lookup"><span data-stu-id="4d478-150">A template variable that defines hello TCP port value for hello port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="4d478-151">A *araştırma* ne sıklıkta ve ne kadar süreyle hello için Azure yük dengeleyici toouse belirli bir hizmet yapı düğümü başarısız olmadan önce bir tooanother üzerinde çalışır. tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4d478-151">A *probe* that defines how frequently and for how long hello Azure load balancer attempts toouse a specific Service Fabric node before failing over tooanother one.</span></span> <span data-ttu-id="4d478-152">Merhaba araştırmalar hello yük dengeleyici kaynak bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="4d478-152">hello probes are part of hello Load Balancer resource.</span></span> <span data-ttu-id="4d478-153">Merhaba ilk varsayılan uygulama bağlantı noktası için hello araştırma tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4d478-153">Here is hello probe definition for hello first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="4d478-154">A *Yük Dengeleme kuralı* , bağlar, birlikte hello bağlantı noktası ve hangi etkinleştirir Yük Dengeleme Service Fabric küme düğümleri kümesi boyunca hello araştırma:</span><span class="sxs-lookup"><span data-stu-id="4d478-154">A *load-balancing rule* that ties together hello port and hello probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="4d478-155">Daha fazla bağlantı noktaları toodeploy toohello küme planlama hello uygulamaları ihtiyacınız varsa, bunları oluşturma ek araştırma ve Yük Dengeleme kuralı tanımlarına göre ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d478-155">If hello applications that you plan toodeploy toohello cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="4d478-156">Hakkında daha fazla bilgi için Resource Manager şablonları aracılığıyla Azure yük dengeleyici ile toowork bkz [bir şablonu kullanarak bir iç yük dengeleyici oluşturmaya başlamak](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="4d478-156">For more information on how toowork with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-hello-template-by-using-visual-studio"></a><span data-ttu-id="4d478-157">Visual Studio kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="4d478-157">Deploy hello template by using Visual Studio</span></span>
<span data-ttu-id="4d478-158">Kaydettiğiniz sonra tüm gerekli parametre değerleri hello`ServiceFabricCluster.param.dev.json` dosya, hazır toodeploy hello şablon ve çalıştığınız Service Fabric kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4d478-158">After you have saved all hello required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready toodeploy hello template and create your Service Fabric cluster.</span></span> <span data-ttu-id="4d478-159">Visual Studio Çözüm Gezgini'nde Hello kaynak grubu projesine sağ tıklayın ve seçin **dağıtma | Yeni dağıtım...** . Gerekirse, Visual Studio hello gösterir, **tooResource grubu dağıtma** tooauthenticate tooAzure soran iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="4d478-159">Right-click hello resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show hello **Deploy tooResource Group** dialog box, asking you tooauthenticate tooAzure:</span></span>

![TooResource Grup iletişim dağıtma][3]

<span data-ttu-id="4d478-161">Merhaba iletişim kutusu hello küme ve yeni bir seçenek toocreate hello verir için mevcut bir Resource Manager kaynak grubu seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d478-161">hello dialog box lets you choose an existing Resource Manager resource group for hello cluster and gives you hello option toocreate a new one.</span></span> <span data-ttu-id="4d478-162">Normal algılama toouse Service Fabric kümesi için farklı bir kaynak grubu sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d478-162">It normally makes sense toouse a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="4d478-163">Visual Studio hello Dağıt düğmesi isabet sonra tooconfirm hello şablon parametre değerlerini ister.</span><span class="sxs-lookup"><span data-stu-id="4d478-163">After you hit hello Deploy button, Visual Studio will prompt you tooconfirm hello template parameter values.</span></span> <span data-ttu-id="4d478-164">İsabet hello **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d478-164">Hit hello **Save** button.</span></span> <span data-ttu-id="4d478-165">Bir parametre kalıcı bir değere sahip değil: hello küme hello yönetici hesabı parolası.</span><span class="sxs-lookup"><span data-stu-id="4d478-165">One parameter does not have a persisted value: hello administrative account password for hello cluster.</span></span> <span data-ttu-id="4d478-166">Visual Studio için bir tane istediğinde tooprovide bir parola değeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d478-166">You need tooprovide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="4d478-167">Azure SDK 2.9 ile başlayarak, Visual Studio okuma parolalardan destekler **Azure anahtar kasası** dağıtımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="4d478-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="4d478-168">Merhaba şablon parametreleri iletişim kutusunda bu hello fark `adminPassword` parametresi metin kutusunun sağ hello küçük bir "anahtarı" simgesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="4d478-168">In hello template parameters dialog notice that hello `adminPassword` parameter text box has a little "key" icon on hello right.</span></span> <span data-ttu-id="4d478-169">Bu simge hello küme için yönetici parolasını hello olarak tooselect var olan bir anahtar kasası gizliliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d478-169">This icon allows you tooselect an existing key vault secret as hello administrative password for hello cluster.</span></span> <span data-ttu-id="4d478-170">Yalnızca anahtar kasanızı hello Gelişmiş erişim ilkelerindeki şablon dağıtımı için Azure Resource Manager erişimini etkinleştirmek emin toofirst yapın.</span><span class="sxs-lookup"><span data-stu-id="4d478-170">Just make sure toofirst enable Azure Resource Manager access for template deployment in hello Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="4d478-171">Merhaba dağıtım işlemi hello Visual Studio çıktı penceresinde hello ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d478-171">You can monitor hello progress of hello deployment process in hello Visual Studio output window.</span></span> <span data-ttu-id="4d478-172">Merhaba şablon dağıtımı tamamlandıktan sonra yeni küme hazır toouse değil!</span><span class="sxs-lookup"><span data-stu-id="4d478-172">Once hello template deployment is completed, your new cluster is ready toouse!</span></span>

> [!NOTE]
> <span data-ttu-id="4d478-173">PowerShell hiçbir zaman kullanılan tooadminister Azure şimdi kullandığınız hello makineden olduysa, küçük bir temizlik toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d478-173">If PowerShell was never used tooadminister Azure from hello machine that you are using now, you need toodo a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="4d478-174">Merhaba çalıştırarak scripting PowerShell'i etkinleştirme [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) komutu.</span><span class="sxs-lookup"><span data-stu-id="4d478-174">Enable PowerShell scripting by running hello [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="4d478-175">Geliştirme makineler için "sınırsız" ilke genellikle kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="4d478-175">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="4d478-176">Karar olup olmadığını tooallow tanılama veri koleksiyonundan Azure PowerShell komutlarını ve Çalıştır [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) veya [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) gerektiği.</span><span class="sxs-lookup"><span data-stu-id="4d478-176">Decide whether tooallow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="4d478-177">Bu gereksiz istemleri şablon dağıtımı sırasında kaçının.</span><span class="sxs-lookup"><span data-stu-id="4d478-177">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="4d478-178">Herhangi bir hata varsa, toohello Git [Azure portal](https://portal.azure.com/) ve için dağıtılan açık hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="4d478-178">If there are any errors, go toohello [Azure portal](https://portal.azure.com/) and open hello resource group that you deployed to.</span></span> <span data-ttu-id="4d478-179">Tıklatın **tüm ayarları**, ardından **dağıtımları** hello ayarları dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="4d478-179">Click **All settings**, then click **Deployments** on hello settings blade.</span></span> <span data-ttu-id="4d478-180">Başarısız bir kaynak grubu dağıtım ayrıntılı tanılama bilgisi var. bırakır.</span><span class="sxs-lookup"><span data-stu-id="4d478-180">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="4d478-181">Service Fabric kümeleri belirli sayıda düğüm toobe toomaintain kullanılabilirliği gerektirir ve durumunu - başvurulan tooas "çekirdek Bakımı" koru</span><span class="sxs-lookup"><span data-stu-id="4d478-181">Service Fabric clusters require a certain number of nodes toobe up toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="4d478-182">İlk yapmadığınız sürece bu nedenle, tüm hello makineler hello kümedeki aşağı güvenli tooshut erişilebilir bir [tam yedekleme, durumunun](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4d478-182">Therefore, it is not safe tooshut down all of hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4d478-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d478-183">Next steps</span></span>
* [<span data-ttu-id="4d478-184">Service Fabric kümesi Hello Azure portal kullanarak ayarlama hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="4d478-184">Learn about setting up Service Fabric cluster using hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="4d478-185">Bilgi nasıl toomanage ve Visual Studio kullanarak Service Fabric uygulamaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="4d478-185">Learn how toomanage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
