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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Linux üzerinde Azure Web uygulaması için SSH desteği

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Genel Bakış

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) Ağ Hizmetleri güvenli bir şekilde kullanmak için bir şifreleme ağ protokolüdür. Ayrıca, bir sisteme uzaktan güvenli bir şekilde bir komut satırı ile oturum açma ve yönetimsel komutları uzaktan yürütme için en yaygın olarak kullanılır.

Web uygulaması Linux'ta uygulama kapsayıcısı içeren her yeni web uygulamaları için çalışma zamanı yığınını kullanılan yerleşik Docker görüntülerinin içine SSH desteği sağlar. 

![Çalışma zamanı yığınları](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Bu konu başlığı altında açıklandığı gibi yapılandırma ve görüntünün bir parçası olarak SSH sunucusu dahil olmak üzere özel Docker görüntülerinizi ile SSH kullanabilirsiniz.



## <a name="making-a-client-connection"></a>Bir istemci bağlantısını yapma

Bir SSH istemci bağlantısı yapmak için ana site başlatılması gerekir. 

Web uygulamanız için kaynak denetimi Yönetim (SCM) uç noktası aşağıdaki biçimi kullanarak tarayıcınıza yapıştırın:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Önceden doğrulanmış değil, Azure aboneliğinizle bağlanmak için kimlik doğrulaması için gereklidir.

![SSH bağlantısı](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Özel Docker görüntülerle SSH desteği

Azure portalında kapsayıcı ve istemci arasındaki SSH iletişimi desteklemek özel bir Docker görüntü için sırayla Docker görüntüsü için aşağıdaki adımları gerçekleştirin. 

Bu adımlar bir örnek olarak Azure App Service deposunda gösterilen [burada](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Dahil `openssh-server` yüklemesinde [ `RUN` yönerge](https://docs.docker.com/engine/reference/builder/#run) Dockerfile görüntü ve kök parolasını hesap için kümesi içinde `"Docker!"`. 

    > [!NOTE] 
    > Bu yapılandırma, kapsayıcıya dış bağlantılara izin vermiyor. SSH yalnızca Kudu erişilebilir / yayımlama kimlik bilgileri kullanılarak kimlik doğrulaması SCM Site.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Ekleme bir [ `COPY` yönerge](https://docs.docker.com/engine/reference/builder/#copy) Dockerfile kopyalamak için bir [sshd_config](http://man.openbsd.org/sshd_config) dosya */vb./ssh/* dizin. Yapılandırma dosyanızı Azure App Service GitHub deposuna bizim sshd_config dosyasında dayanmalıdır [burada](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > *Sshd_config* dosyası şunları içermelidir veya bağlantı başarısız olur: 
    > * `Ciphers`aşağıdakilerden en az birini içermelidir: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`aşağıdakilerden en az birini içermelidir: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Bağlantı noktası 2222 dahil [ `EXPOSE` yönerge](https://docs.docker.com/engine/reference/builder/#expose) Dockerfile için. Kök parolasını bilinen karşın, bağlantı noktası 2222 internet'ten erişilemez. Bir iç yalnızca bağlantı noktası erişilebilir yalnızca özel bir sanal ağ köprüsü ağının kapsayıcılara tarafından değil.

    ```docker
    EXPOSE 2222 80
    ```

4. Başlatmak emin olun ssh hizmeti. Örnek [burada](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) bir kabuk betiği kullanan */bin* dizin.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Dockerfile kullanan [ `CMD` yönerge](https://docs.docker.com/engine/reference/builder/#cmd) komut dosyasını çalıştırmak için.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Sonraki adımlar
Linux üzerinde Web uygulaması ile ilgili daha fazla bilgi için aşağıdaki bağlantılara bakın. Hakkında sorular ve sorunları nakledebilirsiniz [forumumuzda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Linux üzerinde Azure Web uygulaması için özel bir Docker görüntü kullanma](app-service-linux-using-custom-docker-image.md)
* [Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak](app-service-linux-using-nodejs-pm2.md)
* [.NET Core Linux Azure Web uygulamasında kullanma](app-service-linux-using-dotnetcore.md)
* [Ruby Linux Azure Web uygulamasında kullanma](app-service-linux-ruby-get-started.md)
* [Azure App Service Web uygulaması Linux SSS](app-service-linux-faq.md)

