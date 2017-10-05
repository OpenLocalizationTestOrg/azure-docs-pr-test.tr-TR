---
title: "Azure Service Fabric XPlat CLI ile çalışmaya başlama"
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
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="159f7-103">Service Fabric kümeyle etkileşim kurmak için XPlat CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="159f7-103">Using the XPlat CLI to interact with a Service Fabric cluster</span></span>

<span data-ttu-id="159f7-104">Service Fabric kümesi Linux'ta XPlat CLI kullanarak Linux makinelerden etkileşim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="159f7-104">You can interact with Service Fabric cluster from Linux machines using the XPlat CLI on Linux.</span></span>

<span data-ttu-id="159f7-105">İlk adımı get git rep CLI en son sürümünü ve aşağıdaki komutları kullanarak yolunuzda ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="159f7-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="159f7-106">Her komut destekliyorsa, bu komut için Yardım almak için komut adını yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="159f7-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span>
<span data-ttu-id="159f7-107">Otomatik Tamamlama komutlar için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="159f7-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="159f7-108">Örneğin, aşağıdaki komut, Yardım için tüm uygulama komutları sağlar.</span><span class="sxs-lookup"><span data-stu-id="159f7-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="159f7-109">Aşağıdaki örnekte gösterildiği gibi belirli bir komut için Yardım daha fazla filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="159f7-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="159f7-110">CLI otomatik tamamlama etkinleştirmek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="159f7-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="159f7-111">Aşağıdaki komutlar kümeye bağlanın ve kümedeki düğümlerin göster:</span><span class="sxs-lookup"><span data-stu-id="159f7-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="159f7-112">Adlandırılmış parametreleri kullanmanız ve bunların ne olduğunu bulmak için bir komutundan sonra yazabilirsiniz--yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="159f7-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="159f7-113">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="159f7-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="159f7-114">Çoklu makine bir küme için bir makineden bağlanırken **değil parçası olan küme**, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="159f7-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="159f7-115">PublicIPorFQDN etiketi gerçek IP veya FQDN ile uygun şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="159f7-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="159f7-116">Çoklu makine bir küme için bir makineden bağlanırken **olan kümesinin parçası**, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="159f7-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="159f7-117">Azure portalı üzerinden, Linux Service Fabric kümesi ile etkileşim kurmak için CLI oluşturulan veya PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="159f7-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="159f7-118">Bu kümeleri güvenli değil, bu nedenle, bir-kutusunu küme bildiriminde genel IP adresi ekleyerek açmakta.</span><span class="sxs-lookup"><span data-stu-id="159f7-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="159f7-119">Bir Service Fabric kümeye bağlanmak için XPlat CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="159f7-119">Using the XPlat CLI to connect to a Service Fabric cluster</span></span>

<span data-ttu-id="159f7-120">Aşağıdaki Azure CLI komutları güvenli bir kümeye bağlanmak nasıl açıklar.</span><span class="sxs-lookup"><span data-stu-id="159f7-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="159f7-121">Sertifika ayrıntılarını küme düğümlerinde bir sertifika ile eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="159f7-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="159f7-122">Sertifikanızı sertifika yetkilileri (CA) varsa, aşağıdaki örnekteki gibi--ca sertifikası path parametresi eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="159f7-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="159f7-123">Birden fazla CA varsa, ayırıcı olarak virgül kullanın.</span><span class="sxs-lookup"><span data-stu-id="159f7-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="159f7-124">Sertifikadaki ortak adınızı bağlantı uç noktasının eşleşmiyorsa parametresi kullanabileceğinizi `--strict-ssl-false` aşağıdaki komutta gösterildiği gibi doğrulama atlamak için:</span><span class="sxs-lookup"><span data-stu-id="159f7-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="159f7-125">CA doğrulama atlamak istediğiniz varsa, ekleyebilirsiniz aşağıdaki komutta gösterildiği gibi Reddet yetkisiz yanlış parametre:</span><span class="sxs-lookup"><span data-stu-id="159f7-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="159f7-126">Bağlandıktan sonra kümeyle etkileşim kurmak için diğer CLI komutları çalıştırmak görebilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="159f7-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="159f7-127">Service Fabric uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="159f7-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="159f7-128">Kopyalama, kaydetme ve service fabric uygulaması başlatmak için aşağıdaki komutları yürütün:</span><span class="sxs-lookup"><span data-stu-id="159f7-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="159f7-129">Uygulamanızı yükseltme</span><span class="sxs-lookup"><span data-stu-id="159f7-129">Upgrading your application</span></span>

<span data-ttu-id="159f7-130">İşlem benzer [Windows işlem](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="159f7-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="159f7-131">Yapı, kopyalama, kaydetme ve proje kök dizininde uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="159f7-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="159f7-132">Uygulama örneği olarak adlandırılmışsa `fabric:/MySFApp`ve MySFApp türdür, komutları aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="159f7-132">If your application instance is named `fabric:/MySFApp`, and the type is MySFApp, the commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="159f7-133">Uygulamanızda değişikliği yapın ve değiştirilen hizmeti yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="159f7-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="159f7-134">Değiştirilen hizmetin bildirim dosyası (ServiceManifest.xml) hizmeti (ve kod veya yapılandırma ve verileri uygun şekilde) için güncelleştirilmiş sürümleri ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="159f7-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="159f7-135">Ayrıca uygulama bildirimi (ApplicationManifest.xml) uygulama ve değiştirilen hizmet için güncelleştirilmiş sürüm numarasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="159f7-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="159f7-136">Şimdi, kopyalamak ve aşağıdaki komutları kullanarak güncelleştirilmiş uygulamanızı kaydetme:</span><span class="sxs-lookup"><span data-stu-id="159f7-136">Now, copy and register your updated application using the following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="159f7-137">Şimdi, aşağıdaki komutla uygulama yükseltme başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="159f7-137">Now, you can start the application upgrade with the following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="159f7-138">Şimdi SFX kullanarak uygulama yükseltmesi izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="159f7-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="159f7-139">Birkaç dakika içinde uygulamanız güncelleştirilmiş olur.</span><span class="sxs-lookup"><span data-stu-id="159f7-139">In a few minutes, the application would have been updated.</span></span> <span data-ttu-id="159f7-140">Ayrıca, bir hata ile güncelleştirilmiş bir uygulamayı deneyin ve hizmet yapıda otomatik geri alma işlevselliği denetleyin.</span><span class="sxs-lookup"><span data-stu-id="159f7-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="159f7-141">PEM ve tersi yönde PFX dönüştürme</span><span class="sxs-lookup"><span data-stu-id="159f7-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="159f7-142">Farklı bir ortamda olabilir güvenli küme erişmek için yerel makinenizdeki (Windows veya Linux ile) bir sertifika yüklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="159f7-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="159f7-143">Örneğin, bir Windows makineden ve güvenli bir Linux kümesi erişirken sertifikanızı PEM ve tersi yönde PFX dönüştürmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="159f7-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="159f7-144">PEM dosyasından bir PFX dosyasına dönüştürmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="159f7-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="159f7-145">Bir PFX dosyasını PEM dosyasına dönüştürmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="159f7-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="159f7-146">Ayrıntılar için [OpenSSL belgelerine](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) bakın.</span><span class="sxs-lookup"><span data-stu-id="159f7-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="159f7-147">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="159f7-147">Troubleshooting</span></span>


### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="159f7-148">Uygulama paketi kopyalama başarılı değil</span><span class="sxs-lookup"><span data-stu-id="159f7-148">Copying of the application package does not succeed</span></span>

<span data-ttu-id="159f7-149">Olup olmadığını denetleyin `openssh` yüklenir.</span><span class="sxs-lookup"><span data-stu-id="159f7-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="159f7-150">Varsayılan olarak, Ubuntu Masaüstü yüklü sahip değil.</span><span class="sxs-lookup"><span data-stu-id="159f7-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="159f7-151">Aşağıdaki komutu kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="159f7-151">Install it using the following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="159f7-152">Sorun devam ederse, PAM için ssh değiştirerek devre dışı bırakmayı deneyin `sshd_config` aşağıdaki komutları kullanarak dosya:</span><span class="sxs-lookup"><span data-stu-id="159f7-152">If the problem persists, try disabling PAM for ssh by changing the `sshd_config` file using the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="159f7-153">Sorun devam ederse sayısını ssh oturumları aşağıdaki komutları yürüterek artırmayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="159f7-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="159f7-154">(Platform ssh paketleri kopyalamak için kullandığından) ssh kimlik doğrulaması (parola) aksine henüz desteklenmeyen için anahtarları kullanarak parola kimlik doğrulaması yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="159f7-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="159f7-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="159f7-155">Next steps</span></span>

[<span data-ttu-id="159f7-156">Geliştirme ortamını ayarlama ve Linux kümesi için Service Fabric uygulaması dağıtın.</span><span class="sxs-lookup"><span data-stu-id="159f7-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="159f7-157">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="159f7-157">Related articles</span></span>

* [<span data-ttu-id="159f7-158">Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="159f7-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
