---
title: "Azure App Service Web uygulaması Linux'ta aaaSSH desteği | Microsoft Docs"
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
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="64c24-104">Linux üzerinde Azure Web uygulaması için SSH desteği</span><span class="sxs-lookup"><span data-stu-id="64c24-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="64c24-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="64c24-105">Overview</span></span>

<span data-ttu-id="64c24-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) Ağ Hizmetleri güvenli bir şekilde kullanmak için bir şifreleme ağ protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="64c24-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="64c24-107">Bu bir sistemine en yaygın kullanılan toolog uzaktan güvenli bir şekilde bir komut satırından ve yönetim komutları uzaktan yürütün.</span><span class="sxs-lookup"><span data-stu-id="64c24-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="64c24-108">Web uygulaması Linux'ta hello uygulama kapsayıcısı içeren her çalışma zamanı yığını yeni web uygulamaları, hello için kullanılan hello yerleşik Docker görüntülerinin içine SSH desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="64c24-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Çalışma zamanı yığınları](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="64c24-110">Bu konu başlığı altında açıklandığı gibi yapılandırma ve hello SSH sunucusu hello görüntüsünün bir parçası dahil olmak üzere özel Docker görüntülerinizi ile SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64c24-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="64c24-111">Bir istemci bağlantısını yapma</span><span class="sxs-lookup"><span data-stu-id="64c24-111">Making a client connection</span></span>

<span data-ttu-id="64c24-112">bir SSH istemci bağlantısı hello ana site toomake başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="64c24-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="64c24-113">Web uygulamanız için Hello kaynak denetimi Yönetim (SCM) uç noktası form aşağıdaki hello kullanarak tarayıcınıza yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="64c24-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="64c24-114">Önceden doğrulanmış değil, gerekli tooauthenticate, Azure aboneliği tooconnect ile demektir.</span><span class="sxs-lookup"><span data-stu-id="64c24-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![SSH bağlantısı](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="64c24-116">Özel Docker görüntülerle SSH desteği</span><span class="sxs-lookup"><span data-stu-id="64c24-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="64c24-117">Bir özel Docker görüntü toosupport SSH hello kapsayıcı ve istemci arasındaki iletişimin hello hello Azure portal'ın için sırayla şu adımları Docker resmi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="64c24-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="64c24-118">Bu adımları olan gösterilen hello Azure uygulama hizmeti deposu bir örnek olarak [burada](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="64c24-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="64c24-119">Merhaba dahil `openssh-server` yüklemesinde [ `RUN` yönerge](https://docs.docker.com/engine/reference/builder/#run) Dockerfile görüntünüzü için hello ve hello hello kök hesabının parolasını çok ayarlamak`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="64c24-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="64c24-120">Bu yapılandırma, dış bağlantıları toohello kapsayıcı izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="64c24-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="64c24-121">SSH yalnızca Kudu hello erişilebilir / kullanarak kimlik doğrulaması SCM Site hello yayımlama kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="64c24-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="64c24-122">Ekleme bir [ `COPY` yönerge](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy bir [sshd_config](http://man.openbsd.org/sshd_config) toohello dosya */vb./ssh/* dizin.</span><span class="sxs-lookup"><span data-stu-id="64c24-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="64c24-123">Yapılandırma dosyanızı hello Azure App Service GitHub deposunu bizim sshd_config dosyasında dayanmalıdır [burada](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="64c24-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64c24-124">Merhaba *sshd_config* hello bağlantı başarısız veya dosya hello aşağıdaki dahil edilmelidir:</span><span class="sxs-lookup"><span data-stu-id="64c24-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="64c24-125">`Ciphers`Merhaba aşağıdakilerden en az birini içermelidir: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="64c24-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="64c24-126">`MACs`Merhaba aşağıdakilerden en az birini içermelidir: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="64c24-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="64c24-127">Bağlantı noktası 2222 hello dahil [ `EXPOSE` yönerge](https://docs.docker.com/engine/reference/builder/#expose) hello Dockerfile için.</span><span class="sxs-lookup"><span data-stu-id="64c24-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="64c24-128">Merhaba kök parola bilinen karşın, bağlantı noktası 2222 hello erişilemez durumda Internet.</span><span class="sxs-lookup"><span data-stu-id="64c24-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="64c24-129">Bir iç yalnızca bağlantı noktası erişilebilir yalnızca özel bir sanal ağ köprüsü ağının Merhaba kapsayıcılara tarafından değil.</span><span class="sxs-lookup"><span data-stu-id="64c24-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="64c24-130">Hizmet toostart hello ssh emin olun.</span><span class="sxs-lookup"><span data-stu-id="64c24-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="64c24-131">Merhaba örneği [burada](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) bir kabuk betiği kullanan */bin* dizin.</span><span class="sxs-lookup"><span data-stu-id="64c24-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="64c24-132">Merhaba Dockerfile kullanan hello [ `CMD` yönerge](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="64c24-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="64c24-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64c24-133">Next steps</span></span>
<span data-ttu-id="64c24-134">Web uygulaması ile ilgili daha fazla bilgi için bağlantılar Linux üzerinde aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="64c24-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="64c24-135">Hakkında sorular ve sorunları nakledebilirsiniz [forumumuzda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="64c24-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="64c24-136">Linux üzerinde Azure Web uygulaması için nasıl toouse özel Docker görüntü</span><span class="sxs-lookup"><span data-stu-id="64c24-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="64c24-137">Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="64c24-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="64c24-138">.NET Core Linux Azure Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="64c24-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="64c24-139">Ruby Linux Azure Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="64c24-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="64c24-140">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="64c24-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

