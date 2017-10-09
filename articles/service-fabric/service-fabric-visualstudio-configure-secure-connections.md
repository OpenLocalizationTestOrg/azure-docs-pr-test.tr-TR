---
title: "aaaConfigure güvenli Azure Service Fabric kümesi bağlantıları | Microsoft Docs"
description: "Nasıl toouse Visual Studio tooconfigure güvenli hello Azure Service Fabric kümesi tarafından desteklenen bağlantı hakkında bilgi edinin."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a><span data-ttu-id="d9c4e-103">Visual Studio'dan güvenli bağlantılar tooa Service Fabric kümesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d9c4e-103">Configure secure connections tooa Service Fabric cluster from Visual Studio</span></span>
<span data-ttu-id="d9c4e-104">Nasıl toouse Visual Studio toosecurely erişim Azure Service Fabric kümesi yapılandırılmış erişim denetimi ilkeleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-104">Learn how toouse Visual Studio toosecurely access an Azure Service Fabric cluster with access control policies configured.</span></span>

## <a name="cluster-connection-types"></a><span data-ttu-id="d9c4e-105">Küme bağlantı türleri</span><span class="sxs-lookup"><span data-stu-id="d9c4e-105">Cluster connection types</span></span>
<span data-ttu-id="d9c4e-106">İki tür bağlantı hello Azure Service Fabric kümesi tarafından desteklenir: **güvenli olmayan** bağlantıları ve **x509 sertifika tabanlı** güvenli bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-106">Two types of connections are supported by hello Azure Service Fabric cluster: **non-secure** connections and **x509 certificate-based** secure connections.</span></span> <span data-ttu-id="d9c4e-107">(Şirket içi, Service Fabric kümeleri barındırılan için **Windows** ve **dSTS** kimlik doğrulamaları de desteklenir.) Merhaba küme oluşturulduğunda tooconfigure hello küme bağlantı türüne sahip.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-107">(For Service Fabric clusters hosted on-premises, **Windows** and **dSTS** authentications are also supported.) You have tooconfigure hello cluster connection type when hello cluster is being created.</span></span> <span data-ttu-id="d9c4e-108">Merhaba bağlantı türü, bir kez oluşturulduktan sonra değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-108">Once it's created, hello connection type can’t be changed.</span></span>

<span data-ttu-id="d9c4e-109">Merhaba Visual Studio Service Fabric araçları bağlanan tooa kümesi yayımlama için tüm kimlik doğrulama türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-109">hello Visual Studio Service Fabric tools support all authentication types for connecting tooa cluster for publishing.</span></span> <span data-ttu-id="d9c4e-110">Bkz: [hello Azure portal ' bir Service Fabric kümesi ayarlama](service-fabric-cluster-creation-via-portal.md) yönelik yönergeler tooset güvenli Service Fabric kümesi.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-110">See [Setting up a Service Fabric cluster from hello Azure portal](service-fabric-cluster-creation-via-portal.md) for instructions on how tooset up a secure Service Fabric cluster.</span></span>

## <a name="configure-cluster-connections-in-publish-profiles"></a><span data-ttu-id="d9c4e-111">Küme bağlantılarını yapılandırma yayımlama profilleri</span><span class="sxs-lookup"><span data-stu-id="d9c4e-111">Configure cluster connections in publish profiles</span></span>
<span data-ttu-id="d9c4e-112">Visual Studio Service Fabric projeden yayımlama hello kullanın **Service Fabric uygulaması yayımlama** iletişim kutusu toochoose Azure Service Fabric kümesi.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-112">If you publish a Service Fabric project from Visual Studio, use hello **Publish Service Fabric Application** dialog box toochoose an Azure Service Fabric cluster.</span></span> <span data-ttu-id="d9c4e-113">Altında **bağlantı uç noktasının**, aboneliğinizdeki mevcut bir kümeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-113">Under **Connection endpoint**, select an existing cluster under your subscription.</span></span>

![Merhaba ** yayımlama Service Fabric uygulaması ** iletişim kutusudur kullanılan tooconfigure Service Fabric bağlantı.][publishdialog]

<span data-ttu-id="d9c4e-115">Merhaba **Service Fabric uygulaması yayımlama** iletişim kutusu hello küme bağlantısı otomatik olarak doğrular.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-115">hello **Publish Service Fabric Application** dialog box automatically validates hello cluster connection.</span></span> <span data-ttu-id="d9c4e-116">İstenirse, tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-116">If prompted, sign in tooyour Azure account.</span></span> <span data-ttu-id="d9c4e-117">Doğrulama başarılı olursa, sisteminizi hello sertifikaları güvenli bir şekilde tooconnect toohello küme yüklü veya güvenli olmayan kümenizi doğru olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-117">If validation passes, it means that your system has hello correct certificates installed tooconnect toohello cluster securely, or your cluster is non-secure.</span></span> <span data-ttu-id="d9c4e-118">Doğrulama hataları, ağ sorunları veya doğru şekilde yapılandırılmış sistem tooconnect tooa güvenli kümenizi olmamasından kaynaklanabilir.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-118">Validation failures can be caused by network issues or by not having your system correctly configured tooconnect tooa secure cluster.</span></span>

![Merhaba ** yayımlama Service Fabric uygulama iletişim kutusu doğrular var olan ** doğru yapılandırılmış Service Fabric kümesi bağlantısı.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a><span data-ttu-id="d9c4e-120">tooconnect tooa güvenli küme</span><span class="sxs-lookup"><span data-stu-id="d9c4e-120">tooconnect tooa secure cluster</span></span>
1. <span data-ttu-id="d9c4e-121">Bir hedef küme güvenleri hello hello istemci sertifikalarının erişebildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-121">Make sure you can access one of hello client certificates that hello destination cluster trusts.</span></span> <span data-ttu-id="d9c4e-122">Merhaba sertifika genellikle bir kişisel bilgi değişimi (.pfx) dosyası olarak paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-122">hello certificate is usually shared as a Personal Information Exchange (.pfx) file.</span></span> <span data-ttu-id="d9c4e-123">Bkz: [hello Azure portal ' bir Service Fabric kümesi ayarlama](service-fabric-cluster-creation-via-portal.md) nasıl tooconfigure hello sunucu toogrant erişim tooa istemci için.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-123">See [Setting up a Service Fabric cluster from hello Azure portal](service-fabric-cluster-creation-via-portal.md) for how tooconfigure hello server toogrant access tooa client.</span></span>
2. <span data-ttu-id="d9c4e-124">Merhaba güvenilir bir sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-124">Install hello trusted certificate.</span></span> <span data-ttu-id="d9c4e-125">toodo bunu hello .pfx dosyasını çift tıklatın veya hello PowerShell komut dosyası alma PfxCertificate tooimport hello sertifikaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-125">toodo this, double-click hello .pfx file, or use hello PowerShell script Import-PfxCertificate tooimport hello certificates.</span></span> <span data-ttu-id="d9c4e-126">Merhaba sertifikası çok yüklemek**Cert: \LocalMachine\My**.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-126">Install hello certificate too**Cert:\LocalMachine\My**.</span></span> <span data-ttu-id="d9c4e-127">Tamam tooaccept olan hello sertifika alınırken tüm varsayılan ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-127">It's OK tooaccept all default settings while importing hello certificate.</span></span>
3. <span data-ttu-id="d9c4e-128">Merhaba seçin **Yayımla...**  hello kısayol menüsünde hello proje tooopen hello komutunu **Azure uygulamasını Yayımla** iletişim kutusunu ve ardından hello hedef küme.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-128">Choose hello **Publish...** command on hello shortcut menu of hello project tooopen hello **Publish Azure Application** dialog box and then select hello target cluster.</span></span> <span data-ttu-id="d9c4e-129">Merhaba aracı otomatik olarak hello bağlantı çözümler ve hello parametrelerinde yayımlama hello güvenli bağlantı profilini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-129">hello tool automatically resolves hello connection and saves hello secure connection parameters in hello publish profile.</span></span>
4. <span data-ttu-id="d9c4e-130">İsteğe bağlı: Hello düzenleyebilirsiniz profili toospecify güvenli küme bağlantısı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-130">Optional: You can edit hello publish profile toospecify a secure cluster connection.</span></span>
   
   <span data-ttu-id="d9c4e-131">Merhaba yayımlama profili XML dosya toospecify hello sertifika bilgilerini el ile düzenlediğiniz olduğundan emin toonote hello sertifika depolama alanı adı olması, konum ve sertifika parmak izi depolamak.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-131">Since you're manually editing hello Publish Profile XML file toospecify hello certificate information, be sure toonote hello certificate store name, store location, and certificate thumbprint.</span></span> <span data-ttu-id="d9c4e-132">Bu değerler hello sertifika deposu için ad ve konum depolamak tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-132">You'll need tooprovide these values for hello certificate's store name and store location.</span></span> <span data-ttu-id="d9c4e-133">Bkz: [nasıl yapılır: bir sertifikanın parmak izini alma hello](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-133">See [How to: Retrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) for more information.</span></span>
   
   <span data-ttu-id="d9c4e-134">Merhaba kullanabilirsiniz *ClusterConnectionParameters* toohello Service Fabric kümesi bağlanırken parametreleri toospecify hello PowerShell parametreleri toouse.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-134">You can use hello *ClusterConnectionParameters* parameters toospecify hello PowerShell parameters toouse when connecting toohello Service Fabric cluster.</span></span> <span data-ttu-id="d9c4e-135">Herhangi biri hello Connect-ServiceFabricCluster cmdlet'i tarafından kabul edilen geçerli parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-135">Valid parameters are any that are accepted by hello Connect-ServiceFabricCluster cmdlet.</span></span> <span data-ttu-id="d9c4e-136">Bkz: [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) kullanılabilir parametrelerin listesi.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-136">See [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) for a list of available parameters.</span></span>
   
   <span data-ttu-id="d9c4e-137">Tooa uzaktan küme yayımlıyorsanız toospecify hello uygun parametreleri, belirli küme için gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-137">If you’re publishing tooa remote cluster, you need toospecify hello appropriate parameters for that specific cluster.</span></span> <span data-ttu-id="d9c4e-138">Merhaba, güvenli olmayan bağlantı tooa küme örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="d9c4e-138">hello following is an example of connecting tooa non-secure cluster:</span></span>
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   <span data-ttu-id="d9c4e-139">Bağlantı tooan x509 sertifika tabanlı güvenli küme için örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d9c4e-139">Here’s an example for connecting tooan x509 certificate-based secure cluster:</span></span>
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. <span data-ttu-id="d9c4e-140">Diğer gerekli tüm ayarları, yükseltme parametreler ve uygulama parametre dosyası konumu gibi düzenleyin ve ardından yayımlama hello uygulamanızdan **Service Fabric uygulaması yayımlama** Visual Studio'da iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="d9c4e-140">Edit any other necessary settings, such as upgrade parameters and Application Parameter file location, and then publish your application from hello **Publish Service Fabric Application** dialog box in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9c4e-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9c4e-141">Next steps</span></span>
<span data-ttu-id="d9c4e-142">Service Fabric kümeleri erişme hakkında daha fazla bilgi için bkz: [Service Fabric Explorer kullanarak kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d9c4e-142">For more information about accessing Service Fabric clusters, see [Visualizing your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
