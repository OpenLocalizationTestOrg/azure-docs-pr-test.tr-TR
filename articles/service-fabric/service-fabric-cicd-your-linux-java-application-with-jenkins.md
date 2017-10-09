---
title: "aaaContinuous derleme ve Jenkins kullanarak Azure Service Fabric Linux Java uygulamanız için tümleştirme | Microsoft Docs"
description: "Azure Service Fabric Linux Java uygulamanızda Jenkins aracılığıyla sürekli derleme ve tümleştirme"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Jenkins toobuild kullanmak ve Linux Java uygulamanızı dağıtın
Jenkins, uygulamanızın sürekli tümleştirme ve dağıtımı için yaygın olarak kullanılan bir araçtır. İşte nasıl toobuild Jenkins kullanarak Azure Service Fabric uygulamanızı dağıtabilirsiniz.

## <a name="general-prerequisites"></a>Genel önkoşullar
- Git’i yerel olarak yükleyin. Merhaba uygun Git sürümünden yükleyebilir [hello Git indirmeler sayfası](https://git-scm.com/downloads), işletim sistemine göre. Yeni tooGit varsa, hello hakkında daha fazla bilgi [Git belgelerine](https://git-scm.com/docs).
- Merhaba Service Fabric Jenkins eklenti sahip elinizin altında. Eklentiyi [Service Fabric indirmeleri](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi) sayfasından indirebilirsiniz.

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Jenkins’i bir Service Fabric kümesi içinde ayarlama

Jenkins’i bir Service Fabric kümesinin içinde veya dışında ayarlayabilirsiniz. Merhaba aşağıdaki bölümler Göster nasıl tooset bunun bir Azure depolama kullanırken bir küme içindeki hesap hello kapsayıcı örneğinin toosave hello durumu.

### <a name="prerequisites"></a>Ön koşullar
1. Bir Service Fabric Linux kümesini hazır bulundurun. Azure portal Hello önceden oluşturulmuş bir Service Fabric kümesi yüklü Docker sahiptir. Merhaba küme yerel olarak çalıştırıyorsanız, Docker hello komutunu kullanarak yüklü olup olmadığını denetle ``docker info``. Yüklenmemişse, uygun şekilde kullanarak yüklemek hello komutlar:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Merhaba aşağıdaki adımları kullanarak Hello kümede dağıtılan hello Service Fabric kapsayıcı uygulama vardır:

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. Merhaba gereksinim toopersist hello hello Jenkins kapsayıcı örneğinin durumunu istediğiniz hello Azure depolama dosya paylaşımı, seçeneği ayrıntılarını bağlanın. Merhaba hello Microsoft Azure portalını kullanıyorsanız, aynı, lütfen hello adımları - bir Azure depolama hesabı deyin oluşturma ``sfjenkinsstorage1``. Oluşturma bir **dosya paylaşımı** bu depolama hesabı altında söyleyin ``sfjenkins``. Tıklayın **Bağlan** isteğe bağlı olarak hello dosya paylaşımı ve Not hello görüntüler altındaki değerler için **Linux bağlanma**, deyin bu gibi aşağıdaki gibi - görünür
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Merhaba Hello yer tutucu değerlerini güncelleştirmek ```setupentrypoint.sh``` karşılık gelen azure depolama ayrıntılarla komut dosyası.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
Değiştir ``[REMOTE_FILE_SHARE_LOCATION]`` hello değerle ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` noktası Yukarıdaki 3 hello hello çıktısından bağlanın.
Değiştir ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` hello değerle ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` noktasından Yukarıdaki 3.

5. Toohello kümesine bağlanın ve hello kapsayıcısı uygulamasına yükleyin.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
Bu hello kümede Jenkins kapsayıcı yükler ve hello Service Fabric Explorer kullanarak izlenebilir.

### <a name="steps"></a>Adımlar
1. Tarayıcınızdan çok Git``http://PublicIPorFQDN:8081``. Merhaba ilk yönetici parolası gerekli toosign hello yolunu sağlar. Bir yönetici kullanıcı olarak toouse Jenkins devam edebilirsiniz. Veya oluşturup hello ilk yönetici hesabıyla oturum sonra hello kullanıcı değiştirin.

   > [!NOTE]
   > Merhaba küme oluştururken hello 8081 bağlantı noktası hello uygulama bitiş bağlantı noktası olarak belirtildiğinden emin olun.
   >

2. Merhaba kapsayıcı örnek kimliği kullanarak alma ``docker ps -a``.
3. Güvenli Kabuk (SSH) oturum açma toohello kapsayıcı ve hello Jenkins portalında gösterilen hello yolu yapıştırın. Örneğin, isteğe bağlı olarak hello Portalı'nda hello yolunu gösterir `PATH_TO_INITIAL_ADMIN_PASSWORD`, hello aşağıdaki komutu çalıştırın:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Belirtilen hello adımları kullanarak GitHub toowork Jenkins ile ayarlamak [yeni bir SSH anahtarı oluşturma ve toohello SSH aracı ekleyerek](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * GitHub toogenerate hello SSH anahtarı ve tooadd hello SSH anahtar toohello deponuz barındıran GitHub hesabı tarafından sağlanan hello yönergeleri kullanın.
    * Merhaba hello Jenkins Docker Kabuğu (ve ana bilgisayarınız üzerinde değil) bağlantı önceki bölümünde belirtildiği hello komutları çalıştırın.
    * toosign toohello ana bilgisayar, komutu aşağıdaki kullanım hello Jenkins kabuğundan içinde:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Jenkins’i Service Fabric kümesi dışında ayarlama

Jenkins’i bir Service Fabric kümesinin içinde veya dışında ayarlayabilirsiniz. bölümler Göster nasıl aşağıdaki hello tooset bunun bir küme dışında.

### <a name="prerequisites"></a>Ön koşullar
Toohave yüklü Docker gerekir. Aşağıdaki komutları hello hello terminal gelen kullanılan tooinstall Docker olabilir:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Şimdi çalıştırdığınızda ``docker info`` hello terminal, o Merhaba hizmeti çalışırken Docker hello çıktı görmeniz gerekir.

### <a name="steps"></a>Adımlar
  1. Merhaba Service Fabric Jenkins kapsayıcı görüntü çekme:``docker pull raunakpandya/jenkins:v1``
  2. Merhaba kapsayıcı görüntüsü çalıştırın:``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Merhaba kapsayıcı görüntü örneğinin Hello kimliği alın. Tüm hello Docker kapsayıcıları hello komutuyla listesi``docker ps –a``
  4. İçinde toohello hello aşağıdaki adımları kullanarak Jenkins portalında oturum:

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Kapsayıcı kimliği 2d24a73b5964 ise, 2d24 kullanın.
    * Bu parola toohello Jenkins panosunda olduğu Portalı'ndan imzalamak için gereklidir``http://<HOST-IP>:8080``
    * Merhaba ilk kez oturum açtıktan sonra kendi kullanıcı hesabı oluşturun ve gelecekteki amaçları için kullanmak veya toouse hello yönetici hesabı devam edebilirsiniz. Bir kullanıcı oluşturduktan sonra ile toocontinue gerekir.
  5. Belirtilen hello adımları kullanarak GitHub toowork Jenkins ile ayarlamak [yeni bir SSH anahtarı oluşturma ve toohello SSH aracı ekleyerek](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * GitHub toogenerate hello SSH anahtarı ve tooadd hello SSH anahtar toohello hello deposu barındıran GitHub hesabı tarafından sağlanan hello yönergeleri kullanın.
        * Merhaba hello Jenkins Docker Kabuğu (ve ana bilgisayarınız üzerinde değil) bağlantı önceki bölümünde belirtildiği hello komutları çalıştırın.
      * toosign toohello ana bilgisayarınız, aşağıdaki komutları kullanın hello Jenkins kabuğundan içinde:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Bu hello küme veya Jenkins kapsayıcı görüntü barındırılan hello genel kullanıma yönelik IP sahip olduğu makine emin olun. Merhaba Jenkins örneği tooreceive bildirimleri github'dan sağlar.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>Merhaba portalından Hello Service Fabric Jenkins eklentisini yükleme

1. Çok gidin``http://PublicIPorFQDN:8081``
2. Merhaba Jenkins panodan seçin **yönetmek Jenkins** > **eklentileri yönetme** > **Gelişmiş**.
Burada, bir eklentiyi karşıya yükleyebilirsiniz. Seçin **dosya**ve ardından hello **serviceFabric.hpi** altında Önkoşullar indirilen dosya. Seçtiğinizde, **karşıya**, Jenkins hello eklenti otomatik olarak yükler. Yeniden başlatma isteniyorsa izin verin.

## <a name="create-and-configure-a-jenkins-job"></a>Bir Jenkins işi oluşturma ve yapılandırma

1. Panodan **yeni öğe** oluşturun.
2. Bir öğe adını girin (örneğin, **MyJob**). **Serbest stil proje**’yi seçip **Tamam**’a tıklayın.
3. Merhaba iş sayfasına gidin ve'ı tıklatın **yapılandırma**.

   a. Merhaba genel bölümdeki altında **GitHub proje**, GitHub proje URL'sini belirtin. Sürekli dağıtım (CI/CD) toointegrate hello Jenkins sürekli tümleştirme ile istediğiniz bu URL konakları hello hizmet doku Java uygulaması akış (örneğin, ``https://github.com/sayantancs/SFJenkins``).

   b. Merhaba altında **kaynak kodu Yönetimi** bölümünde, select **Git**. Merhaba Jenkins CI/CD akış ile toointegrate istediğiniz hello Service Fabric Java uygulamasını barındıran hello depo URL'si belirtin (örneğin, ``https://github.com/sayantancs/SFJenkins.git``). Ayrıca, burada hangi şube toobuild belirtebilirsiniz (örneğin, **/ana**).
4. Yapılandırma, *GitHub* (hangi barındırma hello depo) mümkün tootalk tooJenkins olmasını sağlayın. Merhaba aşağıdaki adımları kullanın:

   a. Tooyour GitHub depo sayfasına gidin. Çok Git**ayarları** > **tümleştirmeler ve Hizmetleri**.

   b. Seçin **Hizmet Ekle**, türü **Jenkins**ve select hello **Jenkins GitHub eklentisi**.

   c. Jenkins web kancası URL'nizi girin (varsayılan olarak, ``http://<PublicIPorFQDN>:8081/github-webhook/`` olmalıdır). **Hizmet ekle/güncelleştir** öğesine tıklayın.

   d. Bir test olayı tooyour Jenkins örneği gönderilir. Github'da hello Web kancası tarafından yeşil bir onay işareti görürsünüz ve projenizi oluşturacaksınız.

   e. Merhaba altında **yapı tetikleyicileri** bölümünde, hangi oluşturmak istediğiniz seçeneği seçin. Bu örnekte, bazı itme toohello depo olur her tootrigger bir yapı istediğiniz. Bu nedenle **GITScm yoklaması için GitHub kanca tetikleyicisi**’ni seçin. (Bu seçenek daha önce çağrıldı **bir değişiklik tooGitHub gönderildiğinde yapı**.)

   f. Merhaba altında **yapı bölüm**, hello açılan gelen **Ekle derleme adımı**, hello seçeneğini belirleyin **çağırma Gradle betik**. Gelen hello pencere öğesinde hello yolu çok belirtin**kök yapı betik** uygulamanız için. Belirtilen hello yolundan build.gradle seçer ve uygun şekilde çalışır. Adlı bir proje oluşturduğunuzda ``MyActor`` (Merhaba Eclipse eklenti veya Yeoman oluşturucusunu kullanarak), hello kök derleme betiğindeki içermelidir ``${WORKSPACE}/MyActor``. Bunun nasıl göründüğünü bir örnek için ekran görüntüsü aşağıdaki hello bakın:

    ![Service Fabric Jenkins Derleme eylemi][build-step]

   g. Merhaba gelen **oluşturma sonrası eylemleri** açılan listesinde, select **dağıtmak Service Fabric proje**. Burada, burada hello Jenkins Service Fabric uygulaması derlenmiş ayrıntıları dağıtılabilecek tooprovide küme gerekir. Ek uygulama ayrıntıları toodeploy hello uygulama kullanılan de sağlayabilirsiniz. Bunun nasıl göründüğünü bir örnek için ekran görüntüsü aşağıdaki hello bakın:

    ![Service Fabric Jenkins Derleme eylemi][post-build-step]

   > [!NOTE]
   > Service Fabric toodeploy hello Jenkins kapsayıcı görüntü kullandığınız durumda burada hello küme hello bir barındırma hello Jenkins kapsayıcı uygulaması aynı olabilir.
   >

## <a name="next-steps"></a>Sonraki adımlar
GitHub ve Jenkins yapılandırılmıştır. Bazı örnek değişiklik yapmayı düşünün, ``MyActor`` hello deposu örnek projesinde https://github.com/sayantancs/SFJenkins. Değişiklikleri tooa uzak anında ``master`` şube (veya toowork ile yapılandırılmış herhangi bir dal). Bu hello Jenkins iş tetikler ``MyJob``, yapılandırdığınız. Github'dan hello değişiklikleri getirir, bunları oluşturur ve oluşturma sonrası eylemleri belirtilen hello uygulama toohello küme uç noktası dağıtır.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
