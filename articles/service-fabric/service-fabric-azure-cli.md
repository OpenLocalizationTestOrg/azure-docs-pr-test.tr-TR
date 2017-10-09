---
title: "Azure Service Fabric XPlat CLI ile aaaGetting başlatıldı"
description: "Azure Service Fabric XPlat CLI ile çalışmaya başlama"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="54c41-103">Service Fabric kümesi ile Merhaba XPlat CLI toointeract kullanma</span><span class="sxs-lookup"><span data-stu-id="54c41-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="54c41-104">Service Fabric kümesi Linux'ta hello XPlat CLI kullanarak Linux makinelerden etkileşim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54c41-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="54c41-105">Hello ilk adım olan Al hello CLI hello en son sürümünü hello git rep ve bunun yolu kullanarak hello komutları aşağıdaki kümesi:</span><span class="sxs-lookup"><span data-stu-id="54c41-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="54c41-106">Her komut destekliyorsa, bu komut için hello komut tooobtain hello Yardımı hello adı yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54c41-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="54c41-107">Otomatik Tamamlama hello komutları için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="54c41-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="54c41-108">Örneğin, tüm hello uygulama komutlar için Yardım komut verir aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="54c41-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="54c41-109">Aşağıdaki örnekte gösterildiği hello hello Yardım tooa belirli komut, daha fazla filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="54c41-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="54c41-110">tooenable otomatik-tamamlama hello CLI, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="54c41-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="54c41-111">Aşağıdaki komutları hello toohello küme ve hello kümedeki düğümler hello Göster Bağlan:</span><span class="sxs-lookup"><span data-stu-id="54c41-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="54c41-112">toouse adlandırılmış parametreleri ve bunların ne olduğunu bulun, yazabilirsiniz--Yardım komutundan sonra.</span><span class="sxs-lookup"><span data-stu-id="54c41-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="54c41-113">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54c41-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="54c41-114">Tooa çoklu makine küme bir makineden bağlanırken **değil parçası olan hello küme**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="54c41-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="54c41-115">Merhaba PublicIPorFQDN etiketi hello gerçek IP veya FQDN ile uygun şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="54c41-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="54c41-116">Tooa çoklu makine küme bir makineden bağlanırken **hello kümesinin parçası olan**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="54c41-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="54c41-117">Hello Azure portal CLI toointeract Linux Service Fabric kümesi ile oluşturulan veya PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54c41-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="54c41-118">Bu kümeleri güvenli değil, bu nedenle, bir-kutusunu hello küme bildiriminde hello genel IP adresi ekleyerek açmakta.</span><span class="sxs-lookup"><span data-stu-id="54c41-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="54c41-119">Merhaba XPlat CLI tooconnect tooa Service Fabric kümesi kullanma</span><span class="sxs-lookup"><span data-stu-id="54c41-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="54c41-120">Azure CLI komutları aşağıdaki hello nasıl tooconnect tooa güvenli küme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="54c41-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="54c41-121">Merhaba sertifika ayrıntıları hello küme düğümlerinde bir sertifika ile eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="54c41-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="54c41-122">Sertifikanızı sertifika yetkilileri (CA) varsa, aşağıdaki örneğine hello gibi tooadd hello--ca sertifikası path parametresi gerekir:</span><span class="sxs-lookup"><span data-stu-id="54c41-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="54c41-123">Birden fazla CA varsa, hello ayırıcı olarak virgül kullanın.</span><span class="sxs-lookup"><span data-stu-id="54c41-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="54c41-124">Merhaba sertifikadaki ortak adınızı hello bağlantı uç noktasının eşleşmiyorsa hello parametre kullanabilirsiniz `--strict-ssl-false` toobypass hello komutu aşağıdaki gösterildiği gibi doğrulama hello:</span><span class="sxs-lookup"><span data-stu-id="54c41-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="54c41-125">Tooskip hello CA doğrulama isterseniz hello--hello komutu aşağıdaki gösterildiği gibi Reddet yetkisiz yanlış parametre ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="54c41-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="54c41-126">Bağlandıktan sonra diğer CLI komutları toointeract ile mümkün toorun olmalıdır hello küme.</span><span class="sxs-lookup"><span data-stu-id="54c41-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="54c41-127">Service Fabric uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="54c41-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="54c41-128">Toocopy, kaydetme ve hello service fabric uygulaması Başlat komutlarını aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="54c41-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="54c41-129">Uygulamanızı yükseltme</span><span class="sxs-lookup"><span data-stu-id="54c41-129">Upgrading your application</span></span>

<span data-ttu-id="54c41-130">Merhaba işlemdir benzer toohello [Windows işlem](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="54c41-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="54c41-131">Yapı, kopyalama, kaydetme ve proje kök dizininde uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54c41-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="54c41-132">Uygulama örneği olarak adlandırılmışsa `fabric:/MySFApp`ve hello türdür MySFApp, hello komutları şu şekilde olacaktır:</span><span class="sxs-lookup"><span data-stu-id="54c41-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="54c41-133">Tooyour uygulama değiştirmek ve değişiklik hello hizmeti yeniden hello olun.</span><span class="sxs-lookup"><span data-stu-id="54c41-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="54c41-134">Güncelleştirme hello hizmetin bildirim dosyası (ServiceManifest.xml) güncelleştirilmiş hello sürümleriyle hello hizmeti için (ve kod veya yapılandırma ve verileri uygun olarak) değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="54c41-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="54c41-135">Ayrıca hello güncelleştirilmiş sürüm numarasıyla Merhaba uygulaması için hello uygulama bildirimi (ApplicationManifest.xml) değiştirin ve değiştirilen hizmet hello.</span><span class="sxs-lookup"><span data-stu-id="54c41-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="54c41-136">Şimdi, kopyalayabilir ve güncelleştirilmiş uygulamanızı hello aşağıdaki komutları kullanarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="54c41-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="54c41-137">Şimdi, komutu aşağıdaki hello ile Merhaba uygulama yükseltme başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="54c41-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="54c41-138">Şimdi hello uygulama yükseltme SFX kullanarak izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54c41-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="54c41-139">Birkaç dakika içinde Merhaba uygulaması güncelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="54c41-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="54c41-140">Ayrıca, bir hata ile güncelleştirilmiş bir uygulamayı deneyin ve service fabric hello otomatik geri alma işlevselliği denetleyin.</span><span class="sxs-lookup"><span data-stu-id="54c41-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="54c41-141">PFX tooPEM ve tersi yönde dönüştürme</span><span class="sxs-lookup"><span data-stu-id="54c41-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="54c41-142">Farklı bir ortamda olabilir, yerel makine (Windows veya Linux) tooaccess güvenli kümelerinde tooinstall sertifika gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="54c41-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="54c41-143">Örneğin, bir Windows makineden ve güvenli bir Linux kümesi erişirken tooconvert sertifikanızı PFX tooPEM ve bunun tersi de gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="54c41-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="54c41-144">PEM dosyası tooa PFX dosyası, komut aşağıdaki kullanım hello gelen tooconvert:</span><span class="sxs-lookup"><span data-stu-id="54c41-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="54c41-145">tooconvert dosyasından bir PFX dosyası tooa PEM, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="54c41-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="54c41-146">Çok başvuran[OpenSSL belgelerine](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="54c41-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="54c41-147">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="54c41-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="54c41-148">Merhaba uygulama paketi kopyalama başarılı değil</span><span class="sxs-lookup"><span data-stu-id="54c41-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="54c41-149">Olup olmadığını denetleyin `openssh` yüklenir.</span><span class="sxs-lookup"><span data-stu-id="54c41-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="54c41-150">Varsayılan olarak, Ubuntu Masaüstü yüklü sahip değil.</span><span class="sxs-lookup"><span data-stu-id="54c41-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="54c41-151">Komutu aşağıdaki hello kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="54c41-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="54c41-152">Merhaba sorun devam ederse, PAM için ssh hello değiştirerek devre dışı bırakmayı deneyin `sshd_config` hello aşağıdaki komutları kullanarak dosyası:</span><span class="sxs-lookup"><span data-stu-id="54c41-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="54c41-153">Merhaba sorun devam ederse, artan hello sayıda ssh oturumları hello aşağıdaki komutları yürüterek deneyin:</span><span class="sxs-lookup"><span data-stu-id="54c41-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="54c41-154">Tuşları kullanarak (Merhaba platform ssh toocopy paketleri kullandığından) ssh kimlik doğrulaması (olarak karşılıklı toopasswords) henüz desteklenmiyor, bu nedenle parola kimlik doğrulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="54c41-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54c41-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54c41-155">Next steps</span></span>

[<span data-ttu-id="54c41-156">Merhaba geliştirme ortamını ayarlama ve bir Service Fabric uygulaması tooa Linux kümesi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54c41-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="54c41-157">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="54c41-157">Related articles</span></span>

* [<span data-ttu-id="54c41-158">Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="54c41-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
