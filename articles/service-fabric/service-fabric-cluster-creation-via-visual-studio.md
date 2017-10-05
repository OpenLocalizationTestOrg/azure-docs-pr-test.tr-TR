---
title: "Visual Studio kullanarak bir Service Fabric kümesi ayarlama | Microsoft Docs"
description: "Visual Studio'da bir Azure kaynak grubu projesi tarafından oluşturulan Azure Resource Manager şablonu kullanarak bir Service Fabric kümesini ayarlamak açıklar"
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
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="eaa3a-103">Visual Studio kullanarak bir Service Fabric kümesi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="eaa3a-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="eaa3a-104">Bu makalede, Visual Studio ve Azure Resource Manager şablonu kullanarak bir Azure Service Fabric kümesini ayarlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="eaa3a-105">Şablonu oluşturmak için Visual Studio Azure kaynak grubu projesi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="eaa3a-106">Şablonu oluşturduktan sonra Visual Studio'dan doğrudan Azure dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="eaa3a-107">Ayrıca bir komut dosyasından veya sürekli tümleştirme (CI) tesis parçası olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="eaa3a-108">Bir Azure kaynak grubu projesi kullanarak bir Service Fabric kümesi şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="eaa3a-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="eaa3a-109">Başlamak için Visual Studio'yu açın ve bir Azure kaynak grubu projesi oluşturun (içinde kullanılabilir **bulut** klasörü):</span><span class="sxs-lookup"><span data-stu-id="eaa3a-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![Seçili Azure kaynak grubu projesi ile yeni proje iletişim kutusu][1]

<span data-ttu-id="eaa3a-111">Bu proje için yeni bir Visual Studio çözümü oluşturun veya varolan bir çözümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="eaa3a-112">Azure kaynak grubu projesi bulut düğümü altında görmüyorsanız Azure yüklü SDK'sı yok.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="eaa3a-113">Web Platformu yükleyicisi başlatın ([Şimdi Yükle](http://www.microsoft.com/web/downloads/platform.aspx) henüz yapmadıysanız), "Azure SDK'sı için .NET için" araması yapın ve Visual Studio sürümünüzle uyumlu sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="eaa3a-114">Tamam düğmesine basın sonra Visual Studio oluşturmak istediğiniz Resource Manager şablonu seçmenizi ister:</span><span class="sxs-lookup"><span data-stu-id="eaa3a-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![Azure şablonu iletişim kutusu seçili Service Fabric kümesi şablonla seçin][2]

<span data-ttu-id="eaa3a-116">Service Fabric kümesi şablonunu seçin ve Tamam düğmesine tekrar basın.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="eaa3a-117">Proje ve Resource Manager şablonu şimdi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="eaa3a-118">Şablon dağıtımı için hazırlama</span><span class="sxs-lookup"><span data-stu-id="eaa3a-118">Prepare the template for deployment</span></span>
<span data-ttu-id="eaa3a-119">Kümeyi oluşturmak için şablon dağıtılmadan önce gerekli şablon parametreleri için değerler sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="eaa3a-120">Bu parametre değerlerini okuma `ServiceFabricCluster.parameters.json` dosyasını, `Templates` kaynak grubu projesi klasörü.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="eaa3a-121">Dosyasını açın ve aşağıdaki değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="eaa3a-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="eaa3a-122">Parametre adı</span><span class="sxs-lookup"><span data-stu-id="eaa3a-122">Parameter name</span></span> | <span data-ttu-id="eaa3a-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eaa3a-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eaa3a-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="eaa3a-124">adminUserName</span></span> |<span data-ttu-id="eaa3a-125">Yönetici hesabı adı için Service Fabric makineler (düğümler).</span><span class="sxs-lookup"><span data-stu-id="eaa3a-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="eaa3a-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="eaa3a-126">certificateThumbprint</span></span> |<span data-ttu-id="eaa3a-127">Sertifikanın parmak izi, küme güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="eaa3a-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="eaa3a-128">sourceVaultResourceId</span></span> |<span data-ttu-id="eaa3a-129">*Kaynak kimliği* küme korur sertifikanın depolandığı anahtar kasasının.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="eaa3a-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="eaa3a-130">certificateUrlValue</span></span> |<span data-ttu-id="eaa3a-131">Küme güvenlik sertifikası URL'si.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="eaa3a-132">Visual Studio Service Fabric Resource Manager şablonu bir sertifika tarafından korunan güvenli bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="eaa3a-133">Bu sertifika son üç şablon parametreleri ile tanımlanan (`certificateThumbprint`, `sourceVaultValue`, ve `certificateUrlValue`), ve bunu bulunmalıdır bir **Azure anahtar kasası**.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="eaa3a-134">Küme güvenlik sertifikasının nasıl oluşturulacağı hakkında daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) makalesi.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="eaa3a-135">İsteğe bağlı: küme adını değiştirin</span><span class="sxs-lookup"><span data-stu-id="eaa3a-135">Optional: change the cluster name</span></span>
<span data-ttu-id="eaa3a-136">Her Service Fabric kümesi bir adı vardır.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="eaa3a-137">Azure'da bir Fabric kümesi oluşturduğunuzda, küme adı (Azure bölgesi ile birlikte) küme için etki alanı adı sistemi (DNS) ad belirler.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="eaa3a-138">Örneğin, küme adı, `myBigCluster`ve yeni küme barındıracak kaynak grubu konumu (Azure bölgesi) Doğu ABD, DNS adı kümenin `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="eaa3a-139">Varsayılan olarak küme adını otomatik olarak oluşturulur ve "Küme" öneki rastgele bir sonek ekleyerek benzersiz yapılan.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="eaa3a-140">Bu, çok şablon parçası olarak kullanmak üzere kolaylaştırır bir **sürekli tümleştirme** (CI) sistem.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="eaa3a-141">Sizin için anlamlı bir kümeniz için belirli bir ad kullanmak istiyorsanız, değeri ayarlayın `clusterName` Resource Manager şablonu dosyasındaki değişken (`ServiceFabricCluster.json`) için seçtiğiniz ad.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="eaa3a-142">Bu, o dosyasında tanımlanan ilk değişkenidir.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="eaa3a-143">İsteğe bağlı: genel uygulama bağlantı noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="eaa3a-143">Optional: add public application ports</span></span>
<span data-ttu-id="eaa3a-144">Dağıtmadan önce küme için genel uygulama bağlantı noktalarını değiştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="eaa3a-145">Varsayılan olarak, şablon yalnızca iki ortak TCP bağlantı noktalarını (80 ve 8081) açar.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="eaa3a-146">Daha fazla bilgi için uygulamalarınızı gerekiyorsa, Azure yük dengeleyici tanımını şablondaki değiştirin.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="eaa3a-147">Tanımı ana şablon dosyasında depolanır (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="eaa3a-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="eaa3a-148">Bu dosyayı açın ve arama `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="eaa3a-149">Her bağlantı noktası üç yapılar ile ilişkilidir:</span><span class="sxs-lookup"><span data-stu-id="eaa3a-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="eaa3a-150">Bağlantı noktası TCP bağlantı noktası değerini tanımlayan Şablon değişkeni:</span><span class="sxs-lookup"><span data-stu-id="eaa3a-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="eaa3a-151">A *araştırma* tanımlayan ne sıklıkta ve ne kadar Azure yük dengeleyici üzerinden başka bir başarısız olmadan önce belirli bir Service Fabric düğüm kullanmayı dener.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="eaa3a-152">Araştırmalar yük dengeleyici kaynak bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="eaa3a-153">İlk varsayılan uygulama bağlantı noktası için araştırma tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="eaa3a-153">Here is the probe definition for the first default application port:</span></span>
   
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
3. <span data-ttu-id="eaa3a-154">A *Yük Dengeleme kuralı* , bağlar, birlikte bağlantı noktası ve hangi etkinleştirir Yük Dengeleme Service Fabric küme düğümleri kümesi boyunca araştırma:</span><span class="sxs-lookup"><span data-stu-id="eaa3a-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
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
   <span data-ttu-id="eaa3a-155">Kümeye dağıtmayı planladığınız uygulamalar daha fazla bağlantı noktası gerekiyorsa, bunları oluşturma ek araştırma ve Yük Dengeleme kuralı tanımlarına göre ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="eaa3a-156">Azure yük dengeleyici ile Resource Manager şablonları ile çalışma konusunda daha fazla bilgi için bkz: [bir şablonu kullanarak bir iç yük dengeleyici oluşturmaya başlamak](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="eaa3a-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="eaa3a-157">Visual Studio kullanarak şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="eaa3a-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="eaa3a-158">Tüm gerekli parametre değerleri kaydettikten sonra`ServiceFabricCluster.param.dev.json` dosyası, şablonu dağıtmak ve Service Fabric kümesi oluşturmak hazır.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="eaa3a-159">Visual Studio Çözüm Gezgini kaynak grubu projesindeki sağ tıklatın ve seçin **dağıtma | Yeni dağıtım...** .</span><span class="sxs-lookup"><span data-stu-id="eaa3a-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**.</span></span> <span data-ttu-id="eaa3a-160">Gerekirse, Visual Studio gösterir, **kaynak grubuna Dağıt** iletişim kutusu, Azure için kimlik doğrulaması isteyen:</span><span class="sxs-lookup"><span data-stu-id="eaa3a-160">If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![Kaynak grubu iletişim için dağıtma][3]

<span data-ttu-id="eaa3a-162">İletişim kutusu, küme için var olan bir Resource Manager kaynak grubu seçmenize olanak sağlar ve yeni bir tane oluşturmak için seçeneği sunar.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-162">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="eaa3a-163">Normalde bir Service Fabric kümesi için farklı bir kaynak grubu kullanacak şekilde mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-163">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="eaa3a-164">Dağıt düğmesi isabet sonra Visual Studio şablon parametre değerlerini onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-164">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="eaa3a-165">İsabet **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-165">Hit the **Save** button.</span></span> <span data-ttu-id="eaa3a-166">Bir parametre kalıcı bir değere sahip değil: küme yönetici hesabı parolası.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-166">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="eaa3a-167">Visual Studio için bir tane istediğinde bir parola değeri sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-167">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="eaa3a-168">Azure SDK 2.9 ile başlayarak, Visual Studio okuma parolalardan destekler **Azure anahtar kasası** dağıtımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-168">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="eaa3a-169">Şablon parametreleri iletişim kutusunda dikkat `adminPassword` parametresi metin kutusu sağda little "anahtar" simgesi vardır.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-169">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="eaa3a-170">Bu simge, küme yönetici parolası olarak var olan bir anahtar kasası gizli seçmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-170">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="eaa3a-171">Yalnızca ilk etkinleştirme, anahtar kasanızı Gelişmiş erişim ilkelerindeki şablon dağıtımı için Azure Resource Manager erişim için emin olun.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-171">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="eaa3a-172">Visual Studio çıktı penceresinde dağıtım işleminin ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-172">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="eaa3a-173">Şablon dağıtımı tamamlandıktan sonra yeni küme kullanıma hazır!</span><span class="sxs-lookup"><span data-stu-id="eaa3a-173">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="eaa3a-174">PowerShell hiçbir zaman Azure şimdi kullanmakta olduğunuz makineden yönetmek için kullanıldıysa, küçük bir temizlik yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-174">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="eaa3a-175">PowerShell komut dosyasını çalıştırarak etkinleştirme [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) komutu.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-175">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="eaa3a-176">Geliştirme makineler için "sınırsız" ilke genellikle kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-176">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="eaa3a-177">Tanılama veri koleksiyonunu Azure PowerShell komutlarındaki izin verir ve çalıştırmak karar [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) veya [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) gerektiği.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-177">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="eaa3a-178">Bu gereksiz istemleri şablon dağıtımı sırasında kaçının.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-178">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="eaa3a-179">Herhangi bir hata varsa, Git [Azure portal](https://portal.azure.com/) ve için dağıttığınız kaynak grubunu açın.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-179">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="eaa3a-180">Tıklatın **tüm ayarları**, ardından **dağıtımları** ayarlar dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-180">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="eaa3a-181">Başarısız bir kaynak grubu dağıtım ayrıntılı tanılama bilgisi var. bırakır.</span><span class="sxs-lookup"><span data-stu-id="eaa3a-181">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="eaa3a-182">Service Fabric kümeleri belirli sayıda düğümleri kullanılabilirliği sürdürmek ve "çekirdek koruma olarak." başvurulan durumunu - korumak için yukarı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="eaa3a-182">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="eaa3a-183">Bu nedenle, ilk yapmadığınız sürece tüm kümesindeki makineleri kapatmaya güvenli değil bir [tam yedekleme, durumunun](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="eaa3a-183">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="eaa3a-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eaa3a-184">Next steps</span></span>
* [<span data-ttu-id="eaa3a-185">Azure portalını kullanarak Service Fabric kümesi ayarlama hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="eaa3a-185">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="eaa3a-186">Visual Studio kullanarak Service Fabric uygulamaları yönetmeyi ve dağıtmayı öğrenin</span><span class="sxs-lookup"><span data-stu-id="eaa3a-186">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
