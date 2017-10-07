---
title: "aaaDeploy bir Node.js uygulaması tooLinux azure'da sanal makineler"
description: "Bilgi nasıl toodeploy bir Node.js uygulaması tooLinux sanal makineleri azure'da."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Bir Node.js uygulaması tooLinux azure'da sanal makineler dağıtma
Bu öğreticide gösterilmiştir nasıl tootake bir Node.js uygulaması ve Azure üzerinde çalışan tooLinux sanal makineler dağıtabilirsiniz. Bu öğreticide Hello yönergeler Node.js çalıştırabilen tüm işletim sisteminde izlenebilir.

Bilgi edineceksiniz nasıl yapılır:

* Çatalı ve kopya basit bir Yapılacaklar uygulamasının içeren GitHub deposunu;
* Oluşturma ve Azure toorun hello uygulamada iki Linux sanal makineleri yapılandırma;
* Merhaba uygulama güncelleştirmeleri toohello web ön uç sanal makine ileterek yineleme.

> [!NOTE]
> toocomplete Bu öğretici, GitHub hesabı ve Microsoft Azure hesabı gerekiyor ve geliştirme makineden özelliği toouse Git hello.
> 
> GitHub hesabı yoksa, kaydolabilirsiniz [burada](https://github.com/join).
> 
> Yoksa bir [Microsoft Azure](https://azure.microsoft.com/) hesabına kaydolabilirsiniz ücretsiz deneme için [burada](https://azure.microsoft.com/pricing/free-trial/). Bu ayrıca, hello kaydolma işlemini için kılavuzluk eder bir [Microsoft Account](http://account.microsoft.com) , zaten bir yoksa. Visual Studio abone varsa, dilerseniz [MSDN Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Geliştirme makinenizde git yoksa Macintosh veya Windows makine kullanıyorsanız, ardından üzerinden yükleyin [burada](http://www.git-scm.com). Linux kullanıyorsanız, sizin için en uygun hello mekanizması kullanılarak Git'i yükleyin `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>Forking ve hello TODO uygulaması kopyalama
Merhaba TODO uygulaması bu Öğreticisi tarafından kullanılan basit bir web ön uç bir Yapılacaklar listesi ve bir MongoDB örneği uygular. İçinde tooGitHub oturum sonra Git [burada](https://github.com/stepro/node-todo) toofind hello uygulama ve sağ hello üst hello bağlantısı kullanarak çatallaştırma. Bu depo adlı hesabınızı oluşturmalısınız *accountname*/node-todo.

Şimdi, geliştirme makinenizde bu depoyu kopyalayın:

    git clone https://github.com/accountname/node-todo.git

Bu yerel bir kopya hello havuzun biraz daha sonra toohello kaynak kodu değişiklik yaparken kullanacağız.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>Oluşturma ve hello Linux sanal makineleri yapılandırma
Azure Linux sanal makineleri kullanarak ham işlem için harika bir desteğe sahiptir. Bu bölümü nasıl kolayca iki Linux sanal makineleri Döndür ve dağıtma hello TODO uygulaması toothem, tek ve hello hello diğer MongoDB örneğinde çalışan hello web ön uç hello öğretici gösterir.

### <a name="creating-virtual-machines"></a>Sanal makineler oluşturma
Merhaba en kolay yolu toocreate azure'da yeni bir sanal makine toouse hello Azure Portal ' dir. Tıklatın [burada](https://portal.azure.com) içinde toosign ve başlatma hello Azure Portal, web tarayıcınızda. Hello Azure portalı yüklendikten sonra hello aşağıdaki adımları tamamlayın:

* Merhaba "+ Yeni"'i tıklatın bağlantı;
* "İşlem" Merhaba kategori seçin ve "Ubuntu Server 14.04 LTS"; seçin
* Merhaba "Resource Manager" dağıtım modelini seçin ve "Oluştur";'ı tıklatın
* Bu yönergeleri izleyerek hello temel bilgileri doldurun:
  * Daha sonra kolayca tanıyacak bir ad belirtin;
  * Bu öğretici için parola kimlik doğrulaması seçin;
  * Tanımlanabilen bir ad ile yeni bir kaynak grubu oluşturun.
* Merhaba sanal makine boyutu "A1" makul bir seçim Bu öğretici için standarttır.
* Ek ayarları için "Standard" Merhaba disk türü olduğundan emin olun ve tüm kalan Varsayılanları hello kabul edin.
* Merhaba Özet sayfasında hello oluşturma devre dışı tetiklersiniz.

Yukarıdaki Hello gerçekleştirmek iki kez toocreate iki Linux sanal makineleri, hello web ön uç için diğeri hello MongoDB örneği için işlem. Merhaba sanal makinelerin oluşturulmasını yaklaşık 5-10 dakika sürer.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Sanal makineler için bir DNS girişi atama
Varsayılan olarak yalnızca erişilebilir bir ortak IP adresi 1.2.3.4 gibi Azure üzerinde oluşturulan sanal makineler var. Merhaba makineler daha kolayca tanımlanabilen DNS girişlerini atayarak olalım.

Merhaba sanal makine oluşturulmadı Hello portal gösterir sonra hello sol gezinti çubuğu hello "Sanal makineler" bağlantısını tıklatın ve makinelerinizi bulun. Her makine için:

* Merhaba temel bilgiler sekmesinde bulun ve genel IP adresi hello üzerinde tıklatın;
* Merhaba ortak IP adresi yapılandırması, bir DNS ad etiketi atayın ve kaydedin.

Merhaba portal belirttiğiniz hello adı kullanılabilir güvence altına alır. Merhaba yapılandırma kaydedildikten sonra sanal makinelerinizi ana bilgisayar adları benzer çok olacaktır`machinename.region.cloudapp.azure.com`.

### <a name="connecting-toohello-virtual-machines"></a>Bağlantı toohello sanal makineler
Sanal makinelerinizi sağlanan, SSH üzerinden önceden yapılandırılmış tooallow uzak bağlantıları yoktu. Bu tooconfigure hello sanal makineleri kullanacağız hello mekanizmadır. Windows için geliştirme kullanıyorsanız, zaten bir yoksa tooget bir SSH istemcisi gerekir. Bir ortak burada yüklenebilir PuTTY seçimdir [burada](http://www.chiark.greenend.org.uk/~sgtatham/putty/). Macintosh ve Linux İşletim Sistemleri'ni SSH önceden yüklenmiş bir sürümü ile gelir.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Merhaba Web ön uç sanal makine yapılandırma
PuTTY, ssh komut satırı veya, diğer sık kullanılan SSH aracını kullanarak oluşturduğunuz SSH toohello web ön uç makine. Bir komut istemi tarafından izlenen bir Hoş Geldiniz iletisi görmeniz gerekir.

İlk olarak, şirketinizdeki git ve düğüm hem yüklendiğinden emin olun:

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Hello uygulamanın web ön uç yerel bazı Node.js modülleri kullandığından, biz de tooinstall hello temel kümesi derleme araçları gerekir:

    sudo apt-get install -y build-essential

Son olarak, şimdi adlı bir Node.js uygulamasını yüklemek *sonsuza kadar*, toorun Node.js sunucu uygulamaları yardımcı olur:

    sudo npm install -g forever

Bu sanal makine toobe mümkün toorun hello uygulamanın web ön uç üzerinde gerekli tüm hello bağımlılıkları bunlar, sağlandığından çalıştıran Al. toodo Bu, ilk olarak, daha önce çatallanmış kolayca güncelleştirmeleri toohello sanal makine (biz kapsayan bu güncelleştirme senaryo daha sonra) yayımlama ve hello tam kopya tooprovide kopyalama hello GitHub deposunu tam bir kopyasını hello sürümünü oluşturacağız gerçekte yürütülebilir deposu.

Merhaba giriş (~) dizininden başlayarak, aşağıdaki komutları hello çalıştırın (değiştirme *accountname* GitHub kullanıcı hesabı adı ile):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Şimdi hello düğümü Yapılacaklar dizini girin ve bu komutları çalıştırın:

    npm install
    forever start server.js

Merhaba uygulamanın web ön uç şu anda çalışıyor, ancak bir adım daha hello uygulama bir web tarayıcısından erişmeden önce. Merhaba, oluşturduğunuz sanal makine adlı bir Azure kaynağı tarafından korunan bir *ağ güvenlik grubu*, sağladığınız olduğunda hello sanal makine için oluşturulmuş. Şu anda, bu kaynak yalnızca dış istekleri tooport yönlendirilen 22 toobe toohello sanal hello makine ancak hiçbir şey bilgisayarla SSH iletişimi sağlayan makine izin verir. Bu nedenle Sipariş tooview hello bağlantı noktası 8080 üzerinde yapılandırılmış toorun olan TODO uygulaması bu bağlantı noktası açılan toobe da gerekir.

Toohello Azure portalına dönün ve hello aşağıdaki adımları tamamlayın:

* "Kaynak grubunda" Merhaba sol gezinti çubuğu; tıklayın
* Sanal makineniz içeren hello kaynak grubunu seçin;
* Merhaba elde edilen listede kaynakların hello ağ güvenlik grubu (Merhaba bir kalkan simgesi ile); seçin
* "Gelen güvenlik kuralları"; Hello özelliklerinde seçin
* Merhaba araç çubuğunda, ""; Ekle
* "Varsayılan-izin ver-todo"; gibi bir ad sağlayın
* Merhaba protokolü çok Ayarla "TCP";
* Ayarlama hello hedef bağlantı noktası aralığı çok "8080";
* Tamam'ı tıklatın ve hello güvenlik kuralı toobe oluşturulan için bekleyin.

Bu güvenlik kuralı oluşturduktan sonra hello TODO uygulaması üzerinde herkese görünür Internet hello ve örneği için bir URL gibi kullanarak tooit, göz atabilirsiniz:

    http://machinename.region.cloudapp.azure.com:8080

Biz henüz hello MongoDB sanal makine yapılandırmadınız olsa bile, hello TODO uygulaması toobe oldukça işlevsel göründüğünü fark edeceksiniz. Merhaba kaynak deposu sabit kodlanmış toouse önceden dağıtılan bir MongoDB örneği olmasıdır. Biz hello MongoDB sanal makine yapılandırdıktan sonra biz geri dönün ve bunun yerine özel bizim MongoDB örneği hello kaynak kodu tooutilize değiştirin.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Merhaba MongoDB sanal makine yapılandırma
PuTTY, ssh komut satırı veya, diğer sık kullanılan SSH aracını kullanarak oluşturduğunuz SSH toohello ikinci makine. Merhaba Hoş Geldiniz iletisi ve komut istemi gördükten sonra MongoDB yükleyin (Bu yönergeleri gelen gerçekleştirilen [burada](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

Varsayılan olarak, yalnızca de yerel olarak erişilen MongoDB yapılandırıldığından. Merhaba uygulamanın sanal makineden erişilebilmeleri adına Bu öğreticide, biz MongoDB yapılandırın. Sudo bağlamda hello /etc/mongod.conf dosyasını açın ve hello bulun `# network interfaces` bölümü. Değişiklik hello `net.bindIp` yapılandırma değeri çok`0.0.0.0`.

> [!NOTE]
> Bu yapılandırma yalnızca bu öğreticinin hello amacıyla kullanılır. Bu **değil** bir güvenlik uygulaması önerilen ve üretim ortamlarında kullanılmamalıdır.
> 
> 

Şimdi hello MongoDB hizmetinin başlatıldığından emin olun:

    sudo service mongod restart

Varsayılan olarak bağlantı noktası 27017 üzerinden MongoDB çalışır. Biz tooopen gerektiği şekilde Hello bağlantı noktası şekilde hello web ön uç sanal makineye, 8080 hello MongoDB sanal makineye tooopen bağlantı noktası 27017 ihtiyacımız.

Toohello Azure portalına dönün ve hello aşağıdaki adımları tamamlayın:

* "Kaynak grubunda" Merhaba sol gezinti çubuğu; tıklayın
* Merhaba MongoDB sanal makineyi içeren hello kaynak grubunu seçin;
* Hello elde edilen listede kaynakların hello ağ güvenlik grubu (Merhaba bir kalkan simgesi ile) ile aynı toohello MongoDB sanal makine verdiğiniz ad hello seçin;
* "Gelen güvenlik kuralları"; Hello özelliklerinde seçin
* Merhaba araç çubuğunda, ""; Ekle
* "Varsayılan-izin ver-mongo"; gibi bir ad sağlayın
* Merhaba protokolü çok Ayarla "TCP";
* Ayarlama hello hedef bağlantı noktası aralığı çok "27017";
* Tamam'ı tıklatın ve hello güvenlik kuralı toobe oluşturulan için bekleyin.

## <a name="iterating-on-hello-todo-application"></a>TODO uygulaması Hello üzerinde yineleme
Şu ana kadar biz iki Linux sanal makineleri sağlamış: MongoDB örneği çalıştıran hello uygulamanızın web ön uç ve bir çalıştıran biri. Ancak bir sorun oluştu - hello web ön uç gerçekte sağlanan hello MongoDB örneği henüz kullanmıyor. Şimdi, hello web ön uç kodu toouse güncelleştirerek bir ortam değişkeni sabit kodlanmış bir örnek yerine düzeltin.

### <a name="changing-hello-todo-application"></a>Merhaba TODO uygulaması değiştirme
İlk kopyaladığınız hello düğümü Yapılacaklar deposu, geliştirme makinenizde hello açmak `node-todo/config/database.js` dosya, en sık kullandığınız düzenleyicide ve hello sabit kodlanmış değerinden gibi hello url değeri değiştirmek `mongodb://...` çok`process.env.MONGODB`.

Değişikliklerinizi kaydetmek ve toohello GitHub ana push:

    git commit -am "Get MongoDB instance from env"
    git push origin master

Ne yazık ki, bu hello değişiklik toohello web ön uç sanal makine yayımlama değil. Birkaç daha fazla değişiklik toothat sanal makine tooenable hello Canlı ortamında hello değişikliklerine hello etkisini hızla gözleyebilirsiniz güncelleştirmeleri yayımlama için basit ancak etkili bir mekanizma olalım.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Merhaba Web ön uç sanal makine yapılandırma
Daha önce hello web ön uç sanal makinede hello düğümü Yapılacaklar deposu tam bir kopyasını biz oluşturduğunuz geri çağırma. Bu eylem uzak toowhich değişiklikleri gönderilemez yeni bir Git oluşturulan renge. Ancak, yalnızca toothis uzak Ftp'den oldukça geliştiricilerin kendi kodlarına çalışırken aradığınız hello hızlı yineleme modeli vermez.

Toobe mümkün toodo olduğundan emin olmak gibi anında toohello uzak bir depo hello sanal makinede ortaya çıktığında Merhaba çalışan TODO uygulaması otomatik olarak güncelleştirilir ne biz olacaktır. Neyse ki, git ile kolay tooachieve budur.

Git hello havuzda alınan belirli zamanlarda tooreact tooactions adresindeki adlı kancaları sayısını kullanıma sunar. Bunlar hello deponun içinde Kabuk komut dosyalarını kullanarak belirtilen `hooks` klasör. Merhaba otomatik güncelleştirme senaryo için en uygun hello kanca olduğu hello `post-update` olay.

Bir SSH oturumu toohello web ön uç sanal makinede, toohello değiştirmek `~/node-todo.git/hooks` dizin ve aşağıdaki içerik tooa dosyasına adlı hello ekleyin `post-update` (değiştirme `machinename` ve `region` MongoDB sanal makine bilgileri ile):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Merhaba aşağıdaki komutu çalıştırarak bu dosyayı yürütülebilir olduğundan emin olun:

    chmod 755 post-update

Bu komut dosyası hello geçerli sunucu uygulaması durduruldu, hello hello kopyalanan deposundaki güncelleştirilmiş toohello son kodudur, tüm güncelleştirilmiş bağımlılıkların ve hello sunucu yeniden sağlar. Ayrıca, bu hello ortam bizim ilk uygulama güncelleştirme tooget hello MongoDB örneği bir ortam değişkenini almak için hazırlık yapılandırılmış sağlar.

### <a name="configuring-your-development-machine"></a>Geliştirme makinenizde yapılandırma
Şimdi şimdi toohello web ön uç sanal Makine'yi sayfaya geliştirme makinenizde alın. Bu bir uzak hello sanal makinedeki hello tam deposu ekleme olarak gibi basit bir işlemdir. Bu komut toodo aşağıdaki hello çalıştırın (değiştirme *kullanıcı* web ön uç sanal makine oturum açma adınızın ve *machinename* ve *bölge* uygun şekilde):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

Tüm gerekli tooenable dağıtmaya ya da geçerli yayımlama, toohello web ön uç sanal makine değiştiği budur.

### <a name="publishing-updates"></a>Yayımlama güncelleştirmeleri
Şimdi kadarki yapılan ve böylece Merhaba uygulaması kendi MongoDB örneği kullanacak hello bir değişiklik yayımlayın:

    git push azure master

Çıktı benzer toothis görmeniz gerekir:

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

Bu komut tamamlandıktan sonra bir web tarayıcısında Merhaba uygulaması yenilemeyi deneyin. Burada sunulan hello Yapılacaklar listesi boş olduğunu ve artık paylaşılan bağlı toohello MongoDB örneği dağıtıldığını mümkün toosee olmalıdır.

toocomplete hello öğretici, başka bir, daha fazla görünen değişiklik olalım. Geliştirme makinenizde tercih ettiğiniz düzenleyicisi kullanarak hello node-todo/public/index.html dosyasını açın. Merhaba jumbotron üstbilgi bulun ve "Todo aholic ben" çok "Todo aholic Azure üzerinde ben!" Merhaba başlık değiştirin.

Şimdi şimdi yürüt:

    git commit -am "Azurify hello title"

Bu kez, tooback toohello GitHub deposuna göndermeden önce hello değişiklik tooAzure Şimdi Yayımla:

    git push azure master

Bu komut tamamlandığında, yenileme hello web sayfası ve hello değişiklikleri görürsünüz. İyi, görünen beri hello değişikliği geri toohello kaynak uzak itme getirin: 

    git push origin master

## <a name="next-steps"></a>Sonraki Adımlar
Bu makalede nasıl oluşturulacağını gösterir tootake bir Node.js uygulaması ve Azure üzerinde çalışan tooLinux sanal makineler dağıtabilirsiniz. Linux sanal makineleri, azure'da hakkında daha fazla toolearn bkz [Azure ile ilgili giriş tooLinux](/documentation/articles/virtual-machines-linux-introduction/).

Hakkında daha fazla bilgi için bkz: Merhaba toodevelop Node.js uygulamaları Azure üzerinde [Node.js Geliştirici Merkezi](/develop/nodejs/).

