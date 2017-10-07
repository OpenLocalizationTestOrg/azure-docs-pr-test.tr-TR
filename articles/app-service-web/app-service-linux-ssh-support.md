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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Linux üzerinde Azure Web uygulaması için SSH desteği

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Genel Bakış

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) Ağ Hizmetleri güvenli bir şekilde kullanmak için bir şifreleme ağ protokolüdür. Bu bir sistemine en yaygın kullanılan toolog uzaktan güvenli bir şekilde bir komut satırından ve yönetim komutları uzaktan yürütün.

Web uygulaması Linux'ta hello uygulama kapsayıcısı içeren her çalışma zamanı yığını yeni web uygulamaları, hello için kullanılan hello yerleşik Docker görüntülerinin içine SSH desteği sağlar. 

![Çalışma zamanı yığınları](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Bu konu başlığı altında açıklandığı gibi yapılandırma ve hello SSH sunucusu hello görüntüsünün bir parçası dahil olmak üzere özel Docker görüntülerinizi ile SSH kullanabilirsiniz.



## <a name="making-a-client-connection"></a>Bir istemci bağlantısını yapma

bir SSH istemci bağlantısı hello ana site toomake başlatılması gerekir. 

Web uygulamanız için Hello kaynak denetimi Yönetim (SCM) uç noktası form aşağıdaki hello kullanarak tarayıcınıza yapıştırın:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Önceden doğrulanmış değil, gerekli tooauthenticate, Azure aboneliği tooconnect ile demektir.

![SSH bağlantısı](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Özel Docker görüntülerle SSH desteği

Bir özel Docker görüntü toosupport SSH hello kapsayıcı ve istemci arasındaki iletişimin hello hello Azure portal'ın için sırayla şu adımları Docker resmi hello gerçekleştirin. 

Bu adımları olan gösterilen hello Azure uygulama hizmeti deposu bir örnek olarak [burada](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Merhaba dahil `openssh-server` yüklemesinde [ `RUN` yönerge](https://docs.docker.com/engine/reference/builder/#run) Dockerfile görüntünüzü için hello ve hello hello kök hesabının parolasını çok ayarlamak`"Docker!"`. 

    > [!NOTE] 
    > Bu yapılandırma, dış bağlantıları toohello kapsayıcı izin vermiyor. SSH yalnızca Kudu hello erişilebilir / kullanarak kimlik doğrulaması SCM Site hello yayımlama kimlik bilgileri.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Ekleme bir [ `COPY` yönerge](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy bir [sshd_config](http://man.openbsd.org/sshd_config) toohello dosya */vb./ssh/* dizin. Yapılandırma dosyanızı hello Azure App Service GitHub deposunu bizim sshd_config dosyasında dayanmalıdır [burada](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Merhaba *sshd_config* hello bağlantı başarısız veya dosya hello aşağıdaki dahil edilmelidir: 
    > * `Ciphers`Merhaba aşağıdakilerden en az birini içermelidir: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`Merhaba aşağıdakilerden en az birini içermelidir: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Bağlantı noktası 2222 hello dahil [ `EXPOSE` yönerge](https://docs.docker.com/engine/reference/builder/#expose) hello Dockerfile için. Merhaba kök parola bilinen karşın, bağlantı noktası 2222 hello erişilemez durumda Internet. Bir iç yalnızca bağlantı noktası erişilebilir yalnızca özel bir sanal ağ köprüsü ağının Merhaba kapsayıcılara tarafından değil.

    ```docker
    EXPOSE 2222 80
    ```

4. Hizmet toostart hello ssh emin olun. Merhaba örneği [burada](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) bir kabuk betiği kullanan */bin* dizin.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Merhaba Dockerfile kullanan hello [ `CMD` yönerge](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello komut dosyası.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Sonraki adımlar
Web uygulaması ile ilgili daha fazla bilgi için bağlantılar Linux üzerinde aşağıdaki hello bakın. Hakkında sorular ve sorunları nakledebilirsiniz [forumumuzda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Linux üzerinde Azure Web uygulaması için nasıl toouse özel Docker görüntü](app-service-linux-using-custom-docker-image.md)
* [Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak](app-service-linux-using-nodejs-pm2.md)
* [.NET Core Linux Azure Web uygulamasında kullanma](app-service-linux-using-dotnetcore.md)
* [Ruby Linux Azure Web uygulamasında kullanma](app-service-linux-ruby-get-started.md)
* [Azure App Service Web uygulaması Linux SSS](app-service-linux-faq.md)

