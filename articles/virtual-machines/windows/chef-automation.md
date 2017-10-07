---
title: "aaaAzure sanal makine dağıtımı Chef ile | Microsoft Docs"
description: "Sanal makine dağıtımı ve yapılandırması Microsoft Azure üzerinde nasıl toouse Chef toodo otomatik öğrenin"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Chef ile Azure sanal makine dağıtımını otomatikleştirme
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef Otomasyon teslim etmek için harika bir araçtır ve durumu yapılandırmaları istenen.

En son bizim bulut API sürümüyle Chef Azure ile sorunsuz tümleştirme sağlar, veren özelliği tooprovision hello ve yapılandırma durumları arasında tek bir komut dağıtın.

Bu makalede, t, nasıl göstereceğiz tooset yukarı Chef ortamı tooprovision Azure sanal makineleri ve bir ilke veya "Kılavuzu" oluşturma ve ardından bu kılavuzu tooan Azure sanal makine dağıtma size yol gösterir.

Başlayalım!

## <a name="chef-basics"></a>Chef temelleri
Başlamadan önce ı hello Chef temel kavramlarını gözden öneririz. Harika malzeme yoktur <a href="http://www.chef.io/chef" target="_blank">burada</a> ve ı, bu kılavuzda denemeden önce hızlı okuma sahip öneririz. Başlamadan önce ı hello temelleri ancak olduðunu.

Aşağıdaki diyagramda hello hello üst düzey Chef mimari gösterilmektedir.

![][2]

Chef üç ana mimari bileşeni vardır: Chef sunucusu, Chef istemcisi (düğüm) ve Chef iş istasyonu.

Merhaba Chef sunucu bizim yönetim noktasıdır ve Chef sunucu Merhaba için iki seçenek vardır: barındırılan bir çözüm ya da bir şirket içi çözüm. Biz, barındırılan bir çözümü kullanarak.

Merhaba Chef (düğüm) yönettiğiniz hello sunucularda bulunur hello Aracısı istemcidir.

Merhaba Chef iş istasyonu burada biz bizim ilkeleri oluşturma ve bizim yönetimi komutları yürütme bizim yönetim iş istasyonu ' dir. Merhaba çalıştıracağımız **Bıçak** bizim altyapı Chef iş istasyonu toomanage hello komutu.

"Cookbooks" ve "Tarif" Merhaba kavramı yoktur. Bunlar etkili bir şekilde tanımlamak ve tooour sunucular geçerli hello ilkelerdir.

## <a name="preparing-hello-workstation"></a>Merhaba iş istasyonu hazırlama
İlk olarak, hazırlık hello iş istasyonu sağlar. Standart bir Windows iş istasyonu kullanıyorum. Toocreate dizin toostore bizim yapılandırma dosyaları ve cookbooks gerekir.

İlk C:\chef adlı bir dizin oluşturun.

Daha sonra c:\chef\cookbooks adlı ikinci bir dizin oluşturun.

Şimdi, Chef bizim Azure aboneliği ile iletişim kurabilmesi toodownload bizim Azure ayarları dosyası gerekir.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
Karşıdan yükle, yayımlama hello PowerShell Azure kullanarak ayarları [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) komutu. 

Yayımlama ayarları dosyası içinde C:\chef Hello.

## <a name="creating-a-managed-chef-account"></a>Yönetilen bir Chef hesap oluşturma
Barındırılan Chef hesap için kaydolabilirsiniz [burada](https://manage.chef.io/signup).

Merhaba kaydolma işlemi sırasında olacak yeni bir kuruluş toocreate istedi.

![][3]

Kuruluşunuz oluşturulduktan sonra hello starter kit indirin.

![][4]

> [!NOTE]
> Anahtarlarınızı sıfırlanacak uyarı bir uyarı alırsanız, henüz yapılandırılmış hiçbir mevcut altyapısına sahip olduğumuz Tamam tooproceed olur.
> 
> 

Bu starter kit zip dosyası kuruluş yapılandırma dosyalarını ve anahtarlarını içerir.

## <a name="configuring-hello-chef-workstation"></a>Merhaba Chef iş istasyonu yapılandırma
Merhaba chef starter.zip tooC:\chef Hello içeriğini ayıklayın.

Chef starter\chef depodaki altındaki tüm dosyaları kopyalayın\.chef tooyour c:\chef dizini.

Dizininizi hello örnek aşağıdaki gibi görünmelidir.

![][5]

Şimdi c:\chef hello kök dizininde hello Azure yayımlama dosyası dahil olmak üzere dört dosyaları olmalıdır.

Merhaba knife.rb dosya Bıçak yapılandırmanızı içerirken hello PEM dosyaları kuruluşunuz ve yönetici iletişimi için özel anahtarları içerir. Biz tooedit hello knife.rb dosyası gerekir.

Seçim düzenleyicinizde hello dosyasını açın ve hello "cookbook_path" Merhaba kaldırarak değiştirme /... / sonraki gösterildiği gibi göründüğü şekilde hello yolundan.

    cookbook_path  ["#{current_dir}/cookbooks"]

Ayrıca hello aşağıdaki Azure yansıtıcı hello adını satır ekleyin yayımlama ayarları dosyası.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

Aşağıdaki örneğine benzer toohello knife.rb dosyanızı görünmelidir.

![][6]

Bu satırlar Bıçak hello cookbooks dizini c:\chef\cookbooks altında başvuruyor ve ayrıca bizim Azure yayımlama ayarları dosyasını Azure işlemleri sırasında kullanır, güvence altına alır.

## <a name="installing-hello-chef-development-kit"></a>Yükleme hello Chef Geliştirme Seti
Sonraki [yükleyip](http://downloads.getchef.com/chef-dk/windows) ChefDK (Chef Geliştirme Seti) tooset Chef istasyonunuzu yukarı hello.

![][7]

Merhaba varsayılan konumunda c:\opscode yükleyin. Bu yükleme yaklaşık 10 dakika sürer.

PATH değişkeni C:\opscode\chefdk\bin için girdiler içeriyor doğrulayın; C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin

Bunlar yoksa, bu yollar eklediğinizden emin olun!

*Hello sipariş, hello yolu önemli olduğunu unutmayın!* Opscode yolları hello doğru sırada değilse sorunları sahip olur.

Devam etmeden önce iş istasyonunuzu yeniden başlatın.

Ardından, sisteme hello Bıçak Azure uzantısı yüklenir. Bu Bıçak "Azure eklentisi" Merhaba ile sağlar.

Merhaba aşağıdaki komutu çalıştırın.

    chef gem install knife-azure ––pre

> [!NOTE]
> Merhaba – öncesi bağımsız değişkeni, en son RC sürümünü hello erişim toohello son API kümesi sağlayan Bıçak Azure eklentisi hello alma sağlar.
> 
> 

Bağımlılık sayısı da hello sırasında yüklenecek olasıdır aynı anda.

![][8]

her şey tooensure komutu aşağıdaki çalışma hello doğru yapılandırılmış.

    knife azure image list

Her şeyin doğru şekilde yapılandırıldıysa, mevcut Azure görüntüleri kaydırın listesini görürsünüz.

Tebrikler. Merhaba iş istasyonu ayarlama!

## <a name="creating-a-cookbook"></a>Bir kılavuzu oluşturma
Bir kılavuzu Chef toodefine tarafından kullanılan yönetilen istemcide tooexecute istediğiniz komutlar kümesi. Bir kılavuzu oluşturma basit ve hello kullanırız **chef oluşturmak Kılavuzu** toogenerate bizim Kılavuzu şablon komutu. IIS otomatik olarak dağıtan bir ilke ister misiniz gibi ı Kılavuzu web sunucusunu çağırma.

C:\Chef dizini altında hello aşağıdaki komutu çalıştırın.

    chef generate cookbook webserver

Bu C:\Chef\cookbooks\webserver hello dizin altında dosya kümesi oluşturur. Şimdi toodefine hello bizim yönetilen sanal makinede bizim Chef istemci tooexecute isteriz komut kümesini ihtiyacımız var.

Merhaba komutları hello dosya default.rb içinde depolanır. Bu dosyada, ı IIS yükler, IIS başlayıp bir şablon dosyası toohello wwwroot klasörüne kopyalar komut kümesini tanımlama.

Merhaba C:\chef\cookbooks\webserver\recipes\default.rb dosyasını değiştirin ve satırlardan hello ekleyin.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

İşiniz bittiğinde hello dosyasını kaydedin.

## <a name="creating-a-template"></a>Şablon oluşturma
Daha önce belirtildiği gibi toogenerate default.html sayfamızı kullanılacak bir şablon dosyası ihtiyacımız var.

Çalışma hello aşağıdaki toogenerate hello şablon komutu.

    chef generate template webserver Default.htm

Şimdi toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb dosya gidin. Bazı basit "Hello World" HTML kod ekleyerek Hello dosyasını düzenleyin ve hello dosyasını kaydedin.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Merhaba Kılavuzu toohello Chef sunucu karşıya yükleme
Bu adımda, biz hello bizim yerel makinede oluşturduk Kılavuzu bir kopyasını almak ve toohello Chef barındırılan sunucu karşıya yükleme. Karşıya sonra hello Kılavuzu hello altında görünür **İlkesi** sekmesi.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Bir sanal makine Bıçak Azure ile dağıtma
Biz şimdi bir Azure sanal makinesi dağıtır ve hello IIS web hizmeti ve varsayılan web sayfamızı yükleyecek "Web" kılavuzu uygulayın.

Buna toodo Bu sipariş, hello kullan **Bıçak azure sunucusu oluşturmak** komutu.

Merhaba komut örneği ardından görüntülenen istiyorum.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

Merhaba parametreleri kendinden açıklamalıdır. Belirli değişkenleri değiştirin ve çalıştırın.

> [!NOTE]
> Hello hello komut satırı ı de uç nokta ağ filtre kuralları hello – tcp uç noktaları parametresini kullanarak otomatikleştirme. Bağlantı noktaları 80 ve 3389 tooprovide erişim toomy web sayfası ve RDP oturumu açmış olduğunuz.
> 
> 

Merhaba komutu çalıştırdıktan sonra toohello Azure Git portal ve tooprovision başlamak makinenizi görürsünüz.

![][13]

sonraki Hello komut istemi belirir.

![][10]

Merhaba dağıtım tamamlandıktan sonra biz hello Bıçak Azure komutu ile Merhaba sanal makine sağladığında hello bağlantı noktası açıldı biz mümkün tooconnect toohello web hizmeti bağlantı noktası 80 üzerinden olması gerekir. Bu sanal makine hello yalnızca sanal makine my bulut hizmetinde olduğu gibi ı hello bulut hizmet URL'si ile bağlanırsınız.

![][11]

Gördüğünüz gibi HTML kodumu yaratıcı aldım.

Biz de hello Azure portalı 3389 numaralı bağlantı noktası üzerinden bir RDP oturumu üzerinden bağlanabildiğini unutmayın.

Bu yardımcı olmuştur ı umuyoruz! Git ve altyapınızı Azure ile kod gezisine olarak bugün başlayın!

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
