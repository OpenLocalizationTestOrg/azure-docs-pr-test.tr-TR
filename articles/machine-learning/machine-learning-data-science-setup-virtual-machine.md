---
title: "bir sanal makineyi IPython dizüstü sunucusu olarak aaaSet | Microsoft Docs"
description: "Yukarı bir Azure sanal makine için bir veri bilimi ortamında kullanılması IPython sunucusuyla gelişmiş analizler için ayarlayın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Gelişmiş analiz için Azure sanal makinesini IPython Not Defteri olarak ayarlama
Bu konuda gösterilmektedir nasıl tooprovision ve bir Azure sanal makinesi veri bilimi ortamının bir parçası kullanılabilir gelişmiş analiz için yapılandırın. Hello Windows sanal makine IPython Not Defteri, Azure Storage Gezgini, AzCopy yanı sıra gelişmiş analizler projeleri için yararlı olan diğer yardımcı programları gibi araçları destekleme ile yapılandırılır. Azure Depolama Gezgini ve AzCopy, örneğin, sağlayan uygun şekilde tooupload veri tooAzure blob depolama nızdan yerel makine veya toodownload, blob depolama biriminden tooyour yerel makine.

## <a name="create-vm"></a>1. adım: genel amaçlı bir Azure sanal makine oluşturma
Bir Azure sanal makinesi zaten varsa ve yalnızca bir IPython dizüstü sunucu üzerindeki tooset istediğiniz, bu adımı atlayın ve çok devam[2. adım: IPython not defterlerini tooan varolan sanal makine için bir uç nokta ekleme](#add-endpoint).

Azure üzerinde bir sanal makine oluşturma hello işlemini başlatmadan önce kullanıcıların proje için gerekli tooprocess hello veri hello makine toodetermine hello boyutu gerekir. Daha az bellek ve daha az CPU çekirdekleri büyük makinelerden küçük makineler var, ancak aynı zamanda daha ucuz. Merhaba makine türleri ve fiyat listesi için bkz <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">sanal makineler fiyatlandırma </a> sayfası

1. Çok oturum<a href="https://manage.windowsazure.com" target="_blank">Klasik Azure portalı</a>, tıklatıp **yeni** sol alt köşede, hello. Bir pencere açılır. Seçin **işlem** -> **sanal makine** -> **FROM GALERİ**.
   
    ![Çalışma alanı oluşturma][24]
2. Görüntüleri aşağıdaki hello birini seçin:
   
   * Windows Server 2012 R2 Datacenter
   * Windows Server Essentials deneyimi (Windows Server 2012 R2)
     
     Ardından, hello alt sağ toogo hello sonraki yapılandırma sayfanın sağ işaret eden hello oka tıklayın.
     
     ![Çalışma alanı oluşturma][25]
3. Bir ad girin toocreate, hello makine boyutunu seçme hello istediğiniz hello sanal makine için (varsayılan: A3) hello hello veri hello makine boyutuna göre giderek tooprocess hello makine toobe (bellek boyutu ve hello sayısı işlem çekirdek) ne kadar güçlü istediğiniz ise , hello makine için bir kullanıcı adı ve parola girin. Ardından, sağ toogo toohello sonraki yapılandırma sayfası işaret eden hello oka tıklayın.
   
    ![Çalışma alanı oluşturma][26]
4. Select hello **bölge/BENZEŞİM grubu/sanal ağ** hello içeren **depolama hesabı** toouse bu sanal makine için planlama ve ardından bu depolama hesabı seçin. Merhaba hello altındaki bir uç nokta ekleyin **uç noktaları** hello uç noktası ("IPython" Buraya) hello adı girerek alan. Herhangi bir dize olarak hello seçebilirsiniz **adı** hello uç noktası olan herhangi bir tamsayı 0 ile 65536 arasında ve **kullanılabilir** hello olarak **genel bağlantı noktası**. Merhaba **özel bağlantı noktası** toobe sahip **9999**. Yapmanız gerekenler **kaçının** zaten atanmış ortak bağlantı noktaları için internet hizmetlerini kullanarak. <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Internet Hizmetleri için bağlantı noktalarını</a> atandığından ve kaçınılmalıdır bağlantı noktalarının bir listesini sağlar.
   
    ![Çalışma alanı oluşturma][27]
5. Sağlama işlemi Hello onay işareti toostart hello sanal makineye tıklayın.
   
    ![Çalışma alanı oluşturma][28]

25 15 dakika toocomplete hello sanal makine sağlama işlemi devam edebilir. Merhaba sanal makine oluşturulduktan sonra bu makine hello durumunu olarak göstermelidir **çalıştıran**.

![Çalışma alanı oluşturma][29]

## <a name="add-endpoint"></a>2. adım: IPython not defterlerini tooan varolan sanal makine için bir uç nokta ekleme
Adım 1'deki hello yönergeleri izleyerek hello sanal makine oluşturduysanız, hello uç noktası IPython dizüstü bilgisayar için zaten eklenmiş ve bu adım atlanır.

Merhaba sanal makine zaten var. ve IPython aşağıdaki adım 3'te yükleyecek not defteri için tooadd bir uç nokta ihtiyacınız varsa, ilk oturum açma tooAzure Klasik portal, hello sanal makineyi seçin ve IPython dizüstü bilgisayar sunucusu için hello uç nokta ekleyin. Merhaba uç noktası IPython dizüstü bilgisayar için tooa Windows sanal makine eklendikten sonra hello aşağıdaki şekilde hello portalı ekran görüntüsü içerir.

![Çalışma alanı oluşturma][17]

## <a name="run-commands"></a>3. adım: IPython dizüstü bilgisayar ve diğer destek araçlarını yükleme
Merhaba sanal makine oluşturulduktan sonra Uzak Masaüstü Protokolü (RDP) toolog toohello Windows sanal makinede kullanın. Yönergeler için bkz: [nasıl tooLog tooa sanal makine çalıştıran Windows Server üzerinde](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Açık hello **komut istemi** (**değil hello Powershell komut penceresini**) olarak bir **yönetici** ve çalışma hello aşağıdaki komutu.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Merhaba yükleme tamamlandığında, IPython dizüstü sunucu hello otomatik olarak başlatıldığında hello *C:\\kullanıcılar\\\<kullanıcı adı\>\\belgeleri\\IPython Not defterlerini* dizin.

İstendiğinde, bir hello IPython dizüstü parolasını ve hello Makine Yöneticisi hello parolasını girin. Bu hello makinede bir hizmet olarak hello IPython dizüstü toorun sağlar.

## <a name="access"></a>4. adım: Erişim IPython dizüstü bir web tarayıcısından
tooaccess hello IPython dizüstü sunucu, açık bir web tarayıcısı ve giriş *https://&#60;virtual makine DNS adı >: &#60; genel bağlantı noktası numarası >* hello URL'si metin kutusuna. Burada, hello *&#60; genel bağlantı noktası numarası >* belirtilen zaman hello IPython dizüstü endpoint eklendi hello bağlantı noktası numarası olmalıdır.

Merhaba *&#60; sanal makine DNS adı >* Klasik Azure portalı hello bulunabilir. Toohello Klasik Portalı'nda oturum sonra tıklatın **sanal makineleri**seçin oluşturulan ve ardından hello makine **PANO**, hello DNS adı şu şekilde gösterilecek:

![Çalışma alanı oluşturma][19]

Belirten bir uyarı karşılaşır *bu Web sitesinin güvenlik sertifikasında bir sorun var.* (Internet Explorer) veya *bağlantınızı özel değil* (Merhaba aşağıda gösterildiği gibi Chrome) şekiller. Tıklatın **devam toothis Web sitesi (önerilmez)** (Internet Explorer) veya **Gelişmiş** ve ardından  **çok devam &#60;* DNS adı*> (güvenli olmayan) ** (Chrome) toocontinue. Ardından, belirtilen önceki tooaccess IPython not defterlerini hello hello parolayı girin.

**Internet Explorer:**
![çalışma alanı oluşturma][20]

**Chrome:**
![çalışma alanı oluşturma][21]

Toohello IPython dizüstü bilgisayar, bir dizin üzerinde oturum sonra *DataScienceSamples* hello tarayıcıda görüneceği. Bu dizin örnek IPython Microsoft toohelp kullanıcılar kuralları veri bilimi görevler tarafından paylaşılan not defterlerini içerir. Bu örnek IPython not defterlerini gelen kullanıma [ **GitHub deposunu** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) hello IPython dizüstü sunucu kurulum işlemi sırasında toohello sanal makineler. Microsoft tutar ve bu depo sık güncelleştirir. Kullanıcıların hello GitHub depo tooget hello en son güncelleştirilen örnek IPython not defterlerini ziyaret edebilirsiniz.
![Çalışma alanı oluşturma][18]

## <a name="upload"></a>5. adım: yerel makine toohello IPython dizüstü sunucu bir varolan IPython dizüstü bilgisayarınızı karşıya yükle
IPython dizüstü kullanıcıları tooupload kendi yerel makine toohello hello sanal makinelerde IPython dizüstü sunucu üzerinde var olan bir IPython dizüstü bilgisayar için kolay bir yol sağlar. Toohello IPython dizüstü bir web tarayıcısında oturum sonra hello tıklayın **directory** IPython Not karşıya yüklenebilir için o hello. Ardından, yerel makinede hello hello IPython not defteri .ipynb dosya tooupload seçin **dosya Gezgini**, sürükleyin ve hello web tarayıcısını toohello IPython dizüstü dizini bırakın. Merhaba tıklatın **karşıya** button, tooupload hello .ipynb dosya toohello IPython dizüstü sunucu. Diğer kullanıcıların sonra içinde web tarayıcılarından kullanmaya başlayabilirsiniz.

![Çalışma alanı oluşturma][22]

![Çalışma alanı oluşturma][23]

## <a name="shutdown"></a>Kapatmak ve sanal makine kullanılmadığında XML'deki Ayır
Azure sanal makineler olarak fiyatlandırılır **yalnızca kullandıklarınız için ödeme**. değil yükleniyor tooensure sanal makineniz kullanmadığınızda faturalandırılır, toobe hello sahip **durduruldu (Deallocated)** durum kullanılmadığı zaman.

> [!NOTE]
> Merhaba sanal makineyi kapatın, gelen VM (Windows güç seçenekleri kullanarak), hello içinde hello VM durduruldu ancak kalır ayrılmış. değil devam faturalandırılır, toobe tooensure her zaman hello sanal makinelerden Durdur [Klasik Azure portalı](http://manage.windowsazure.com/). Çağırarak hello Powershell aracılığıyla VM durdurabilirsiniz **ShutdownRoleOperation** "PostShutdownAction" ile eşit çok "StoppedDeallocated".
> 
> 

tooshut aşağı ve hello sanal makine ayırması:

1. İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com/) hesabınızı kullanarak.  
2. Seçin **sanal makineleri** hello sol gezinti çubuğunda.
3. Sanal makineler Hello listesinde, sanal makine sonra gidin toohello hello adına tıklayın **PANO** sayfası.
4. Merhaba sayfasının Hello altında tıklatın **kapatma**.

![VM kapatma][15]

Merhaba sanal makine serbest ancak silinmez. Sanal makineniz hello Klasik Azure Portalı'ndan herhangi bir zamanda yeniden başlatılabilir.

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>Azure VM'nizi hazır toouse olduğu: sonraki nedir?
Sanal makineniz hazır toouse veri bilimi alıştırmaları içinde sunulmuştur. Hello sanal makine de hello takım veri bilimi işlemi Azure Machine Learning ile Merhaba araştırması ve veri işleme için bir IPython dizüstü sunucusu ve diğer görevleri birlikte kullanım için hazırdır.

Merhaba sonraki adımlar takım veri bilimi işlemi hello eşlendi hello içinde [öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve Hdınsight'a, işlem verilerini taşımak ve Azure makineyle var. Bu örnek hello verilerden öğrenmeyi için hazırlık adımları içerebilir Öğrenme.

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
