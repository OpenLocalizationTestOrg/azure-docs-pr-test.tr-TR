---
title: "Sanal makine bir IPython dizüstü sunucusu olarak ayarlama | Microsoft Docs"
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
ms.openlocfilehash: 66fd9e5573390ac6faeb82ad5b0f7ddb18d50a77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Gelişmiş analiz için Azure sanal makinesini IPython Not Defteri olarak ayarlama
Bu konu, sağlamak ve veri bilimi ortamının bir parçası kullanılabilir gelişmiş analizler için bir Azure sanal makine yapılandırma gösterilmektedir. Windows sanal makine IPython Not Defteri, Azure Storage Gezgini, AzCopy yanı sıra gelişmiş analizler projeleri için yararlı olan diğer yardımcı programları gibi araçları destekleme ile yapılandırılır. Örneğin, Azure Depolama Gezgini ve AzCopy, verileri Azure blob depolama alanına yerel makinenizden karşıya yüklemek veya bir blob depolama alanından yerel makinenize indirmek için uygun şekilde girin.

## <a name="create-vm"></a>1. adım: genel amaçlı bir Azure sanal makine oluşturma
Bir Azure sanal makinesi zaten varsa ve bir IPython dizüstü bilgisayar sunucusunda, ayarlamak istediğiniz, bu adımı atlayın ve devam [2. adım: IPython dizüstü bilgisayarlar için varolan bir sanal makineye bir uç nokta ekleyin](#add-endpoint).

Azure üzerinde bir sanal makine oluşturma işlemi başlamadan önce kullanıcıların proje için verileri işlemek için gerekli makine boyutunu belirlemeniz gerekir. Daha az bellek ve daha az CPU çekirdekleri büyük makinelerden küçük makineler var, ancak aynı zamanda daha ucuz. Makine türlerini ve fiyat listesi için bkz: <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">sanal makineler fiyatlandırma </a> sayfası

1. Oturum <a href="https://manage.windowsazure.com" target="_blank">Klasik Azure portalı</a>, tıklatıp **yeni** sol alt köşedeki içinde. Bir pencere açılır. Seçin **işlem** -> **sanal makine** -> **FROM GALERİ**.
   
    ![Çalışma alanı oluşturma][24]
2. Aşağıdaki görüntülerden birini seçin:
   
   * Windows Server 2012 R2 Datacenter
   * Windows Server Essentials deneyimi (Windows Server 2012 R2)
     
     Ardından, sonraki yapılandırma sayfasına gitmek için alt sağ taraftaki sağ oku tıklatın.
     
     ![Çalışma alanı oluşturma][25]
3. İstediğiniz makine boyutunu seçin oluşturmak için sanal makine için bir ad girin (varsayılan: A3) makine işlemine geçmeden veri boyutu ve ne kadar güçlü göre (bellek boyutu ve işlem çekirdek sayısı) makinenin istiyor , makine için bir kullanıcı adı ve parola girin. Ardından, sonraki yapılandırma sayfasına doğrudan gitmek için oku tıklatın.
   
    ![Çalışma alanı oluşturma][26]
4. Seçin **bölge/BENZEŞİM grubu/sanal ağ** içeren **depolama hesabı** bu sanal makine için kullanın ve ardından bu depolama hesabı seçin dağıtmayı planlıyorsanız. En altta bir uç nokta ekleyin **uç noktaları** ("IPython" Buraya) uç noktanın adı girerek alan. Herhangi bir dize olarak seçebileceğiniz **adı** uç noktası olan herhangi bir tamsayı 0 ile 65536 arasında ve **kullanılabilir** olarak **genel bağlantı noktası**. **Özel bağlantı noktası** olmalıdır **9999**. Yapmanız gerekenler **kaçının** zaten atanmış ortak bağlantı noktaları için internet hizmetlerini kullanarak. <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Internet Hizmetleri için bağlantı noktalarını</a> atandığından ve kaçınılmalıdır bağlantı noktalarının bir listesini sağlar.
   
    ![Çalışma alanı oluşturma][27]
5. Sanal makine sağlama işlemini başlatmak için onay işaretine tıklayın.
   
    ![Çalışma alanı oluşturma][28]

Sanal makine sağlama işlemini tamamlamak için 25 15 dakika sürebilir. Sanal makine oluşturulduktan sonra bu makine durumunu olarak göstermelidir **çalıştıran**.

![Çalışma alanı oluşturma][29]

## <a name="add-endpoint"></a>2. adım: IPython dizüstü bilgisayarlar için bir uç nokta, varolan bir sanal makineye ekleyin.
Adım 1'ndaki yönergeleri izleyerek sanal makine oluşturduysanız, uç nokta IPython dizüstü bilgisayar için zaten eklenmiş ve bu adım atlanır.

Sanal makine zaten varsa ve IPython Aşağıda, Klasik Azure portalında ilk oturum açışınızda adım 3'te yükleyecek dizüstü bilgisayar için bir uç nokta eklemeniz gerekir, sanal makineyi seçin ve IPython dizüstü bilgisayar sunucusu için uç nokta ekleyin. Uç nokta IPython dizüstü bilgisayar için bir Windows sanal makineye eklendikten sonra aşağıdaki şekilde portalı ekran görüntüsü içerir.

![Çalışma alanı oluşturma][17]

## <a name="run-commands"></a>3. adım: IPython dizüstü bilgisayar ve diğer destek araçlarını yükleme
Sanal makine oluşturulduktan sonra Windows sanal makinede oturum açmak için Uzak Masaüstü Protokolü (RDP) kullanın. Yönergeler için bkz: [nasıl bir sanal makine çalıştıran Windows Server oturum](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Açık **komut istemi** (**Powershell komut penceresini**) olarak bir **yönetici** ve aşağıdaki komutu çalıştırın.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Yükleme tamamlandığında, IPython dizüstü sunucunun otomatik olarak başlatılır *C:\\kullanıcılar\\\<kullanıcı adı\>\\belgeleri\\IPython dizüstü bilgisayarlar*  dizin.

İstendiğinde, bir parola IPython not defteri ve makine yönetici parolasını girin. Bu makinede bir hizmet olarak çalıştırmak IPython dizüstü sağlar.

## <a name="access"></a>4. adım: Erişim IPython dizüstü bir web tarayıcısından
IPython dizüstü sunucusuna erişmek için bir web açmak tarayıcı ve giriş *https://&#60;virtual makine DNS adı >: &#60; genel bağlantı noktası numarası >* URL'si metin kutusuna. Burada, *&#60; genel bağlantı noktası numarası >* belirtilen IPython dizüstü endpoint zaman eklendi bağlantı noktası numarası olmalıdır.

*&#60; sanal makine DNS adı >* Azure Klasik portalında bulunabilir. Klasik portalda oturum açtıktan sonra tıklatın **sanal makineleri**, oluşturulan ve ardından makine seçin **PANO**, DNS adı şu şekilde gösterilir:

![Çalışma alanı oluşturma][19]

Belirten bir uyarı karşılaşır *bu Web sitesinin güvenlik sertifikasında bir sorun var.* (Internet Explorer) veya *bağlantınızı özel değil* (Chrome), aşağıda gösterildiği gibi şekiller . Tıklatın **(önerilmez) bu Web sitesine devam et** (Internet Explorer) veya **Gelişmiş** ve ardından  **İlerle olarak &#60;* DNS adı*> (güvenli olmayan) ** (Chrome devam etmek için). Ardından IPython not defterlerini erişmek için daha önce belirttiğiniz parolayı girin.

**Internet Explorer:**
![çalışma alanı oluşturma][20]

**Chrome:**
![çalışma alanı oluşturma][21]

Bir dizin IPython dizüstü bilgisayar oturumunu sonra *DataScienceSamples* tarayıcıda görüneceği. Bu dizin örnek IPython veri bilimi görevleri gerçekleştir kullanıcılara yardımcı olmak için Microsoft tarafından paylaşılan not defterlerini içerir. Bu örnek IPython not defterlerini gelen kullanıma [ **GitHub deposunu** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) IPython dizüstü sunucu kurulum işlemi sırasında sanal makinelere. Microsoft tutar ve bu depo sık güncelleştirir. Kullanıcılar en son güncelleştirilen örnek IPython not defterlerini almak için GitHub deposuna ziyaret edebilirsiniz.
![Çalışma alanı oluşturma][18]

## <a name="upload"></a>5. adım: Varolan IPython not defterini yerel makineden IPython dizüstü sunucuya karşıya yükle
IPython not defterlerini IPython dizüstü sunucunun sanal makinelerde varolan IPython not defterini kendi yerel makinede yüklemek kullanıcılar için kolay bir yol sağlar. Bir web tarayıcısında IPython dizüstü oturum açtıktan sonra tıklayın **dizin** , IPython not defteri yüklenecek. Ardından, yerel makinede karşıya yüklemek için bir IPython dizüstü .ipynb dosyasını seçin **dosya Gezgini**, sürükleyin ve web tarayıcısı IPython dizüstü dizinine bırakın. Tıklatın **karşıya** IPython dizüstü sunucuya .ipynb dosyayı karşıya yüklemeyi düğmesi. Diğer kullanıcıların sonra içinde web tarayıcılarından kullanmaya başlayabilirsiniz.

![Çalışma alanı oluşturma][22]

![Çalışma alanı oluşturma][23]

## <a name="shutdown"></a>Kapatmak ve sanal makine kullanılmadığında XML'deki Ayır
Azure sanal makineler olarak fiyatlandırılır **yalnızca kullandıklarınız için ödeme**. Sanal makinenize kullanmadığınızda ücretlendirilen değil emin olmak için onu olduğu sahip **durduruldu (Deallocated)** durum kullanılmadığı zaman.

> [!NOTE]
> VM içindeki sanal makineden kapatın (Windows güç seçenekleri kullanarak), VM durduruldu ancak ayrılmış kalır. Değil faturalandırılmaya devam edecek emin olmak için her zaman sanal makinelerden Durdur [Klasik Azure portalı](http://manage.windowsazure.com/). Çağırarak Powershell aracılığıyla VM durdurabilirsiniz **ShutdownRoleOperation** "PostShutdownAction" ile "StoppedDeallocated" değerine eşit.
> 
> 

Kapatmak ve sanal makine ayırması için:

1. Oturum [Klasik Azure portalı](http://manage.windowsazure.com/) hesabınızı kullanarak.  
2. Seçin **sanal makineleri** sol gezinti çubuğunda.
3. Sanal makineler listesi, sanal makine adına tıklayın ardından Git **PANO** sayfası.
4. Sayfanın alt kısmındaki tıklatın **kapatma**.

![VM kapatma][15]

Sanal makine serbest ancak silinmez. Azure Klasik Portalı'ndan herhangi bir zamanda, sanal makine yeniden başlatılabilir.

## <a name="your-azure-vm-is-ready-to-use-whats-next"></a>Azure VM kullanılmaya hazırdır: sonraki nedir?
Sanal makine artık veri bilimi alıştırmalarda kullanmak hazırdır. Sanal makine de Azure Machine Learning ve takım veri bilimi işlemi ile araştırması ve veri ve diğer görevleri birlikte işlenmesini IPython dizüstü sunucusu olarak kullanıma hazırdır.

Takım veri bilimi işlemindeki sonraki adımlar, eşlenmiş [öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve Hdınsight'a, işlem verilerini taşımak ve bunu var. Azure Machine Learning ile verileri öğrenme hazırlığı örnek adımlarda içerebilir.

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
