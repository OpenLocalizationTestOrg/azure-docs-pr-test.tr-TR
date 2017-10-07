---
title: "bir Linux VM üzerinde rayları Web sitesinde bir Ruby aaaHost | Microsoft Docs"
description: "Ayarlama ve Ruby kullanarak bir Linux sanal makine azure'da rayları tabanlı Web sitesinde ana bilgisayar."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Azure VM’de Ruby on Rails Web uygulaması
Bu öğreticide gösterilmiştir nasıl toohost Ruby kullanarak bir Linux sanal makine azure'da rayları Web sitesinde.  

Bu öğretici, Ubuntu Server 14.04 LTS kullanılarak doğrulandı. Başka bir Linux dağıtım kullanırsanız, toomodify gerekebilecek hello tooinstall rayları adımları.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.
>
>

## <a name="create-an-azure-vm"></a>Bir Azure VM oluşturma
Bir Linux görüntüsüyle bir Azure VM oluşturarak başlayın.

toocreate VM Merhaba, hello Azure portalında veya Azure komut satırı arabirimi (CLI) hello kullanabilirsiniz.

### <a name="azure-portal"></a>Azure portalına
1. Merhaba içine oturum [Azure portalı](https://portal.azure.com)
2. Tıklatın **yeni**, ardından "Ubuntu Server 14.04" Merhaba arama kutusuna yazın. Merhaba araması tarafından döndürülen hello girdiyi tıklatın. Merhaba dağıtım modelini seçin **Klasik**, "Oluştur" seçeneğine tıklayın.
3. Merhaba temel bilgileri dikey penceresinde hello gerekli alanlar için değerleri girin: (için hello VM) adı, kullanıcı adı, kimlik doğrulama türü ve hello ilgili kimlik bilgileri, Azure abonelik, kaynak grubunu ve konumu.

   ![Yeni bir Ubuntu görüntüsü oluşturma](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Merhaba VM sağlandıktan sonra hello VM adına tıklayın ve'ı tıklatın **uç noktaları** hello içinde **ayarları** kategorisi. Altında listelenen hello SSH uç noktasını Bul **tek başına**.

   ![Varsayılan uç noktası](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>Azure CLI
Merhaba adımları [çalıştıran bir sanal makine Linux oluşturma][vm-instructions].

Merhaba VM sağlandıktan sonra komutu aşağıdaki hello çalıştırarak hello SSH uç noktası alabilirsiniz:

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>Ruby rayları üzerinde yükle
1. SSH tooconnect toohello VM kullanın.
2. Merhaba SSH oturumundan komutları tooinstall Ruby hello VM üzerinde aşağıdaki hello kullan:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    Merhaba yükleme birkaç dakika sürebilir. Tamamlandığında, Ruby yüklendiğini komutu tooverify aşağıdaki hello kullan:

        ruby -v

3. Kullanım hello aşağıdaki tooinstall rayları komutu:

        sudo gem install rails --no-rdoc --no-ri -V

    Merhaba--yok rdoc ve--hızlıdır hello belge yükleme Hayır RI bayrakları tooskip kullanın.
    Bu komut, büyük olasılıkla ekleme hello şekilde -V tooexecute hello yükleme ilerleme durumu hakkında bilgi görüntüler uzun bir zaman alır.

## <a name="create-and-run-an-app"></a>Oluşturma ve bir uygulamayı çalıştırma
SSH yoluyla hala oturum açmış olsa da, hello aşağıdaki komutları çalıştırın:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Merhaba [yeni](http://guides.rubyonrails.org/command_line.html#rails-new) komut yeni bir rayları uygulaması oluşturur. Merhaba [server](http://guides.rubyonrails.org/command_line.html#rails-server) başlatır hello rayları ile birlikte gelen WEBrick web sunucusu komutu. (Üretim kullanımı için büyük olasılıkla toouse Unicorn veya yolcu gibi farklı bir sunucuya istersiniz.)

Çıktı benzer toohello aşağıdaki görmeniz gerekir.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Bir uç nokta ekleme
1. Git toohello [Azure portalı] [https://portal.azure.com] ve VM'yi seçin.

2. Seçin **uç noktaları** hello içinde **ayarları** hello sol kenarı hello sayfa boyunca.

3. Tıklatın **ekleme** hello sayfanın üst kısmındaki hello.

4. Merhaba, **uç nokta ekleme** iletişim sayfasında, aşağıdaki bilgilerle hello girin:

   * **Ad**: HTTP
   * **Protokol**: TCP
   * **Genel bağlantı noktası**: 80
   * **Özel bağlantı noktası**: 3000
   * **PI adresi kayan**: devre dışı
   * **Erişim denetimi listesi - sipariş**: Bu erişim kuralı hello önceliğini ayarlar 1001 ya da başka bir değer.
   * **Erişim denetimi listesi - adı**: allowHTTP
   * **Erişim denetimi listesi - eylem**: izin ver
   * **Erişim denetimi listesi - uzak alt**: 1.0.0.0/16

     Bu uç noktaya burada hello rayları sunucu dinliyor trafiğini toohello özel bağlantı noktası 3000, yönlendirecek 80 genel bir bağlantı noktası var. Merhaba erişim denetimi listesi kuralı bağlantı noktası 80 üzerinde ortak trafiğine izin verir.

     ![Yeni uç noktası](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Tamam toosave hello uç noktasına tıklayın.

6. Bildiren bir ileti görüntülenmelidir **sanal makine uç noktası kaydediliyor**. Bu ileti kaybolur sonra hello endpoint etkindir. Şimdi, sanal makinenin DNS adı toohello giderek uygulamanızı test. Merhaba Web sitesi toohello aşağıdaki benzer görünmelidir:

    ![Varsayılan rayları sayfası][default-rails-cloud]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, çoğu hello adımları el ile yaptınız. Bir üretim ortamında, uygulama geliştirme makinenizde yazmak ve toohello Azure VM dağıtabilirsiniz. Ayrıca, çoğu üretim ortamlarında Apache veya yürüten hello rayları uygulama ve statik kaynakları hizmet veren yönlendirme toomultiple örnekleri isteği NginX gibi başka bir sunucu işlemi ile birlikte Merhaba rayları uygulaması barındırır. Daha fazla bilgi için http://rubyonrails.org/deploy/ bakın.

Ruby rayları üzerinde hakkında daha fazla toolearn ziyaret hello [rayları kılavuzları üzerinde Söyleniş][rails-guides].

toouse Söyleniş uygulamanızdan Azure Hizmetleri, bakın:

* [BLOB'ları kullanarak yapılandırılmamış veri depolayın][blobs]
* [Mağaza anahtar/değer çiftlerinin tabloları kullanma][tables]
* [İçerik teslim ağı hello ile yüksek bant genişliği içerik sunmak][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
