---
title: "Azure App Service Web uygulaması Linux üzerinde SSH desteği | Microsoft Docs"
description: "Linux üzerinde Azure Web uygulaması ile SSH kullanma hakkında bilgi edinin."
keywords: "Azure uygulama hizmeti, web uygulaması, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: feee7a5c91d213a6b0bfdaf264a4da4d9e79cbe7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="db74e-104">Linux üzerinde Azure Web uygulaması için SSH desteği</span><span class="sxs-lookup"><span data-stu-id="db74e-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="db74e-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="db74e-105">Overview</span></span>

<span data-ttu-id="db74e-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) Ağ Hizmetleri güvenli bir şekilde kullanmak için bir şifreleme ağ protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="db74e-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="db74e-107">Ayrıca, bir sisteme uzaktan güvenli bir şekilde bir komut satırı ile oturum açma ve yönetimsel komutları uzaktan yürütme için en yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="db74e-107">It is most commonly used to log into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="db74e-108">Web uygulaması Linux'ta uygulama kapsayıcısı içeren her yeni web uygulamaları için çalışma zamanı yığınını kullanılan yerleşik Docker görüntülerinin içine SSH desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="db74e-108">Web App on Linux provides SSH support into the app container with each of the built-in Docker images used for the Runtime Stack of new web apps.</span></span> 

![Çalışma zamanı yığınları](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="db74e-110">Bu konu başlığı altında açıklandığı gibi yapılandırma ve görüntünün bir parçası olarak SSH sunucusu dahil olmak üzere özel Docker görüntülerinizi ile SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db74e-110">You can also use SSH with your custom Docker images by including the SSH server as part of the image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="db74e-111">Bir istemci bağlantısını yapma</span><span class="sxs-lookup"><span data-stu-id="db74e-111">Making a client connection</span></span>

<span data-ttu-id="db74e-112">Bir SSH istemci bağlantısı yapmak için ana site başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="db74e-112">To make an SSH client connection, the main site must be started.</span></span> 

<span data-ttu-id="db74e-113">Web uygulamanız için kaynak denetimi Yönetim (SCM) uç noktası aşağıdaki biçimi kullanarak tarayıcınıza yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="db74e-113">Paste the Source Control Management (SCM) endpoint for your web app into your browser using the following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="db74e-114">Önceden doğrulanmış değil, Azure aboneliğinizle bağlanmak için kimlik doğrulaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="db74e-114">If you are not already authenticated, you are required to authenticate with your Azure subscription to connect.</span></span>

![SSH bağlantısı](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="db74e-116">Özel Docker görüntülerle SSH desteği</span><span class="sxs-lookup"><span data-stu-id="db74e-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="db74e-117">Azure portalında kapsayıcı ve istemci arasındaki SSH iletişimi desteklemek özel bir Docker görüntü için sırayla Docker görüntüsü için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="db74e-117">In order for a custom Docker image to support SSH communication between the container and the client in the Azure portal, perform the following steps for your Docker image.</span></span> 

<span data-ttu-id="db74e-118">Bu adımlar bir örnek olarak Azure App Service deposunda gösterilen [burada](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="db74e-118">These steps are are shown in the Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="db74e-119">Dahil `openssh-server` yüklemesinde [ `RUN` yönerge](https://docs.docker.com/engine/reference/builder/#run) Dockerfile görüntü ve kök parolasını hesap için kümesi içinde `"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="db74e-119">Include the `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in the Dockerfile for your image and set the password for the root account to `"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="db74e-120">Bu yapılandırma, kapsayıcıya dış bağlantılara izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="db74e-120">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="db74e-121">SSH yalnızca Kudu erişilebilir / yayımlama kimlik bilgileri kullanılarak kimlik doğrulaması SCM Site.</span><span class="sxs-lookup"><span data-stu-id="db74e-121">SSH can only be accessed via the Kudu / SCM Site, which is authenticated using the publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="db74e-122">Ekleme bir [ `COPY` yönerge](https://docs.docker.com/engine/reference/builder/#copy) Dockerfile kopyalamak için bir [sshd_config](http://man.openbsd.org/sshd_config) dosya */vb./ssh/* dizin.</span><span class="sxs-lookup"><span data-stu-id="db74e-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) to the Dockerfile to copy a [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="db74e-123">Yapılandırma dosyanızı Azure App Service GitHub deposuna bizim sshd_config dosyasında dayanmalıdır [burada](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="db74e-123">Your configuration file should be based on our sshd_config file in the Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="db74e-124">*Sshd_config* dosyası şunları içermelidir veya bağlantı başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="db74e-124">The *sshd_config* file must include the following or the connection fails:</span></span> 
    > * <span data-ttu-id="db74e-125">`Ciphers`aşağıdakilerden en az birini içermelidir: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="db74e-125">`Ciphers` must include at least one of the following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="db74e-126">`MACs`aşağıdakilerden en az birini içermelidir: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="db74e-126">`MACs` must include at least one of the following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="db74e-127">Bağlantı noktası 2222 dahil [ `EXPOSE` yönerge](https://docs.docker.com/engine/reference/builder/#expose) Dockerfile için.</span><span class="sxs-lookup"><span data-stu-id="db74e-127">Include port 2222 in the [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for the Dockerfile.</span></span> <span data-ttu-id="db74e-128">Kök parolasını bilinen karşın, bağlantı noktası 2222 internet'ten erişilemez.</span><span class="sxs-lookup"><span data-stu-id="db74e-128">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="db74e-129">Bir iç yalnızca bağlantı noktası erişilebilir yalnızca özel bir sanal ağ köprüsü ağının kapsayıcılara tarafından değil.</span><span class="sxs-lookup"><span data-stu-id="db74e-129">It is an internal only port accessible only by containers within the bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="db74e-130">Başlatmak emin olun ssh hizmeti.</span><span class="sxs-lookup"><span data-stu-id="db74e-130">Make sure to start the ssh service.</span></span> <span data-ttu-id="db74e-131">Örnek [burada](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) bir kabuk betiği kullanan */bin* dizin.</span><span class="sxs-lookup"><span data-stu-id="db74e-131">The example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="db74e-132">Dockerfile kullanan [ `CMD` yönerge](https://docs.docker.com/engine/reference/builder/#cmd) komut dosyasını çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="db74e-132">The Dockerfile uses the [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) to run the script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="db74e-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db74e-133">Next steps</span></span>
<span data-ttu-id="db74e-134">Linux üzerinde Web uygulaması ile ilgili daha fazla bilgi için aşağıdaki bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="db74e-134">See the following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="db74e-135">Hakkında sorular ve sorunları nakledebilirsiniz [forumumuzda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="db74e-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="db74e-136">Linux üzerinde Azure Web uygulaması için özel bir Docker görüntü kullanma</span><span class="sxs-lookup"><span data-stu-id="db74e-136">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="db74e-137">Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="db74e-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="db74e-138">.NET Core Linux Azure Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="db74e-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="db74e-139">Ruby Linux Azure Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="db74e-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="db74e-140">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="db74e-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

