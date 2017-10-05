---
title: "Güvenli Azure Service Fabric kümesi bağlantılarını yapılandırma | Microsoft Docs"
description: "Azure Service Fabric kümesi tarafından desteklenen güvenli bağlantıları yapılandırmak için Visual Studio kullanmayı öğrenin."
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
ms.openlocfilehash: dc07b2f38d6fd2de941ebbe99303f6e63cbf122d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-connections-to-a-service-fabric-cluster-from-visual-studio"></a><span data-ttu-id="4999d-103">Güvenli bağlantılar Visual Studio'dan bir Service Fabric kümesi için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4999d-103">Configure secure connections to a Service Fabric cluster from Visual Studio</span></span>
<span data-ttu-id="4999d-104">Azure Service Fabric kümesi yapılandırılmış erişim denetimi ilkeleri ile güvenli bir şekilde erişmek için Visual Studio kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4999d-104">Learn how to use Visual Studio to securely access an Azure Service Fabric cluster with access control policies configured.</span></span>

## <a name="cluster-connection-types"></a><span data-ttu-id="4999d-105">Küme bağlantı türleri</span><span class="sxs-lookup"><span data-stu-id="4999d-105">Cluster connection types</span></span>
<span data-ttu-id="4999d-106">İki tür bağlantı Azure Service Fabric kümesi tarafından desteklenir: **güvenli olmayan** bağlantıları ve **x509 sertifika tabanlı** güvenli bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="4999d-106">Two types of connections are supported by the Azure Service Fabric cluster: **non-secure** connections and **x509 certificate-based** secure connections.</span></span> <span data-ttu-id="4999d-107">(Şirket içi, Service Fabric kümeleri barındırılan için **Windows** ve **dSTS** kimlik doğrulamaları de desteklenir.) Küme oluşturulduğunda küme bağlantı türünü yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4999d-107">(For Service Fabric clusters hosted on-premises, **Windows** and **dSTS** authentications are also supported.) You have to configure the cluster connection type when the cluster is being created.</span></span> <span data-ttu-id="4999d-108">Bağlantı türü, bir kez oluşturulduktan sonra değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="4999d-108">Once it's created, the connection type can’t be changed.</span></span>

<span data-ttu-id="4999d-109">Visual Studio Service Fabric araçları yayımlama bir kümeye bağlanmak için tüm kimlik doğrulama türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="4999d-109">The Visual Studio Service Fabric tools support all authentication types for connecting to a cluster for publishing.</span></span> <span data-ttu-id="4999d-110">Bkz: [Azure portalından bir Service Fabric kümesi ayarlama](service-fabric-cluster-creation-via-portal.md) güvenli Service Fabric küme ayarlama hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="4999d-110">See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for instructions on how to set up a secure Service Fabric cluster.</span></span>

## <a name="configure-cluster-connections-in-publish-profiles"></a><span data-ttu-id="4999d-111">Küme bağlantılarını yapılandırma yayımlama profilleri</span><span class="sxs-lookup"><span data-stu-id="4999d-111">Configure cluster connections in publish profiles</span></span>
<span data-ttu-id="4999d-112">Service Fabric projeyi Visual Studio'dan yayımlamak kullanırsanız **Service Fabric uygulaması yayımlama** iletişim kutusu bir Azure Service Fabric kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="4999d-112">If you publish a Service Fabric project from Visual Studio, use the **Publish Service Fabric Application** dialog box to choose an Azure Service Fabric cluster.</span></span> <span data-ttu-id="4999d-113">Altında **bağlantı uç noktasının**, aboneliğinizdeki mevcut bir kümeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="4999d-113">Under **Connection endpoint**, select an existing cluster under your subscription.</span></span>

![** Yayımlama Service Fabric uygulaması ** iletişim kutusu, Service Fabric bağlantısını yapılandırmak için kullanılır.][publishdialog]

<span data-ttu-id="4999d-115">**Service Fabric uygulaması yayımlama** iletişim kutusu otomatik olarak küme bağlantısı doğrular.</span><span class="sxs-lookup"><span data-stu-id="4999d-115">The **Publish Service Fabric Application** dialog box automatically validates the cluster connection.</span></span> <span data-ttu-id="4999d-116">İstenirse, Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4999d-116">If prompted, sign in to your Azure account.</span></span> <span data-ttu-id="4999d-117">Doğrulama başarılı olursa, sisteminizin doğru sertifikaların kümeye güvenli bir şekilde bağlanmak için yüklü olan veya güvenli olmayan kümenizi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4999d-117">If validation passes, it means that your system has the correct certificates installed to connect to the cluster securely, or your cluster is non-secure.</span></span> <span data-ttu-id="4999d-118">Doğrulama hataları, ağ sorunları veya güvenli bir kümeye bağlanmak için doğru yapılandırılmış sisteminizi olmamasından kaynaklanabilir.</span><span class="sxs-lookup"><span data-stu-id="4999d-118">Validation failures can be caused by network issues or by not having your system correctly configured to connect to a secure cluster.</span></span>

![** Yayımlama Service Fabric uygulama iletişim kutusu doğrular var olan ** doğru yapılandırılmış Service Fabric kümesi bağlantısı.][selectsfcluster]

### <a name="to-connect-to-a-secure-cluster"></a><span data-ttu-id="4999d-120">Güvenli bir kümeye bağlanmak için</span><span class="sxs-lookup"><span data-stu-id="4999d-120">To connect to a secure cluster</span></span>
1. <span data-ttu-id="4999d-121">Bir hedef küme güvenleri istemci sertifikalarının erişebildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4999d-121">Make sure you can access one of the client certificates that the destination cluster trusts.</span></span> <span data-ttu-id="4999d-122">Sertifika, genellikle bir kişisel bilgi değişimi (.pfx) dosyası olarak paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="4999d-122">The certificate is usually shared as a Personal Information Exchange (.pfx) file.</span></span> <span data-ttu-id="4999d-123">Bkz: [Azure portalından bir Service Fabric kümesi ayarlama](service-fabric-cluster-creation-via-portal.md) için bir istemci erişimi sunucusu nasıl yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="4999d-123">See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for how to configure the server to grant access to a client.</span></span>
2. <span data-ttu-id="4999d-124">Güvenilir sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4999d-124">Install the trusted certificate.</span></span> <span data-ttu-id="4999d-125">Bunu yapmak için .pfx dosyasını çift tıklatın veya sertifikaları içeri aktarmak için PowerShell betiğini alma PfxCertificate kullanın.</span><span class="sxs-lookup"><span data-stu-id="4999d-125">To do this, double-click the .pfx file, or use the PowerShell script Import-PfxCertificate to import the certificates.</span></span> <span data-ttu-id="4999d-126">Sertifikayı yükleme **Cert: \LocalMachine\My**.</span><span class="sxs-lookup"><span data-stu-id="4999d-126">Install the certificate to **Cert:\LocalMachine\My**.</span></span> <span data-ttu-id="4999d-127">Sertifika içeri aktarırken tüm varsayılan ayarları kabul etmek için bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="4999d-127">It's OK to accept all default settings while importing the certificate.</span></span>
3. <span data-ttu-id="4999d-128">Seçin **Yayımla...**  açmak için projesinin kısayol menüsünde komutu **Azure uygulamasını Yayımla** iletişim kutusu ve hedef kümeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="4999d-128">Choose the **Publish...** command on the shortcut menu of the project to open the **Publish Azure Application** dialog box and then select the target cluster.</span></span> <span data-ttu-id="4999d-129">Aracın otomatik olarak bağlantı çözümler ve güvenli bağlantı parametreleri yayımlama profilinde kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4999d-129">The tool automatically resolves the connection and saves the secure connection parameters in the publish profile.</span></span>
4. <span data-ttu-id="4999d-130">İsteğe bağlı: Güvenli küme bağlantısını belirtmek için yayımlama profili düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4999d-130">Optional: You can edit the publish profile to specify a secure cluster connection.</span></span>
   
   <span data-ttu-id="4999d-131">Sertifika bilgilerini belirtmek için sertifika deposunun adını not etmeyi unutmayın yayımlama profili XML dosyasını el ile düzenlediğiniz olduğundan, konum ve sertifika parmak izi depolar.</span><span class="sxs-lookup"><span data-stu-id="4999d-131">Since you're manually editing the Publish Profile XML file to specify the certificate information, be sure to note the certificate store name, store location, and certificate thumbprint.</span></span> <span data-ttu-id="4999d-132">Bu değerleri sertifika deposu için ad ve depolama konumu sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4999d-132">You'll need to provide these values for the certificate's store name and store location.</span></span> <span data-ttu-id="4999d-133">Bkz: [nasıl yapılır: bir sertifikanın parmak izini alma](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4999d-133">See [How to: Retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) for more information.</span></span>
   
   <span data-ttu-id="4999d-134">Kullanabileceğiniz *ClusterConnectionParameters* Service Fabric kümeye bağlanırken kullanmak üzere PowerShell parametreleri belirtmek üzere parametreler.</span><span class="sxs-lookup"><span data-stu-id="4999d-134">You can use the *ClusterConnectionParameters* parameters to specify the PowerShell parameters to use when connecting to the Service Fabric cluster.</span></span> <span data-ttu-id="4999d-135">Herhangi biri Connect-ServiceFabricCluster cmdlet tarafından kabul edilen geçerli parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="4999d-135">Valid parameters are any that are accepted by the Connect-ServiceFabricCluster cmdlet.</span></span> <span data-ttu-id="4999d-136">Bkz: [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) kullanılabilir parametrelerin listesi.</span><span class="sxs-lookup"><span data-stu-id="4999d-136">See [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) for a list of available parameters.</span></span>
   
   <span data-ttu-id="4999d-137">Uzak bir kümeye yayımlıyorsanız belirli bu küme için uygun parametreleri belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4999d-137">If you’re publishing to a remote cluster, you need to specify the appropriate parameters for that specific cluster.</span></span> <span data-ttu-id="4999d-138">Güvenli olmayan bir kümeye bağlanma bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4999d-138">The following is an example of connecting to a non-secure cluster:</span></span>
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   <span data-ttu-id="4999d-139">Örneği için bir x509 bağlamak için sertifika tabanlı güvenli küme:</span><span class="sxs-lookup"><span data-stu-id="4999d-139">Here’s an example for connecting to an x509 certificate-based secure cluster:</span></span>
   
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
5. <span data-ttu-id="4999d-140">Diğer gerekli tüm ayarları, yükseltme parametreler ve uygulama parametre dosyası konumu gibi düzenleyin ve sonra uygulamanızı yayımlamak **Service Fabric uygulaması yayımlama** Visual Studio'da iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="4999d-140">Edit any other necessary settings, such as upgrade parameters and Application Parameter file location, and then publish your application from the **Publish Service Fabric Application** dialog box in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4999d-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4999d-141">Next steps</span></span>
<span data-ttu-id="4999d-142">Service Fabric kümeleri erişme hakkında daha fazla bilgi için bkz: [Service Fabric Explorer kullanarak kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4999d-142">For more information about accessing Service Fabric clusters, see [Visualizing your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
