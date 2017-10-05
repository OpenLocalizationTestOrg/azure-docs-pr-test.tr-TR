---
title: "Jupyter/IPython not defteri oluşturma | Microsoft Docs"
description: "Azure resource manager dağıtım modelinde oluşturulan Linux sanal makinede Jupyter/IPython dizüstü dağıtmayı öğrenin."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Bir Azure Jupyter yükleme ve Jupyter not defteri Azure üzerinde çalışan VM oluşturma
[Jupyter proje](http://jupyter.org), eskiden [IPython proje](http://ipython.org), bir koleksiyon için araçlar sağlar kod yürütmeyi canlı bir oluşturulmasını ile birleştirin güçlü etkileşimli Kabukları kullanarak bilimsel hesaplama Hesaplama belgesi. Bu not defteri dosyaları rastgele metin, matematiksel formüller, giriş kod, sonuçları, grafik, videolar ve modern bir web tarayıcısı görüntüleyebilen ortamının başka herhangi bir tür içerebilir. Python için kesinlikle yeni ve eğlenceli, etkileşimli bir ortamda öğrenin veya paralel/teknik ciddi bazı bilgi işlem yapmak istediğiniz olup olmadığını Jupyter not defteri harika bir seçenektir.

![Ekran](./media/jupyter-notebook/ipy-notebook-spectral.png) ses kaydını yapısını çözümlemek için kullanarak SciPy ve Matplotlib paketleri.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Jupyter iki yolu: Azure dizüstü bilgisayarlar veya özel dağıtım
Azure için kullanabileceğiniz bir hizmet sunar [Jupyter kullanarak hızlı bir şekilde başlatmak ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  Azure Not Defteri hizmetini kullanarak, kolayca Jupyter'ın web üzerinden erişilebilen arabirimi Python tüm gücünü ile ölçeklenebilir hesaplama kaynaklarına ve onun birçok kitaplıklarına erişebilirsiniz.  Yükleme hizmeti tarafından işlenen olduğundan, kullanıcılar Yönetim ve yapılandırma kullanıcı tarafından gerek kalmadan bu kaynaklara erişebilir.

Senaryonuz için Not Defteri hizmeti çalışmıyorsa Lütfen size Microsoft Azure üzerinde Jupyter not defteri dağıtma Linux sanal makineleri (VM'ler) kullanarak gösterir bu makalenin okumaya devam eder.

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Oluşturma ve Azure üzerinde bir VM yapılandırma
Azure üzerinde çalışan sanal makine (VM) oluşturmak için ilk adımdır bakın.
Bu VM bulutta eksiksiz bir işletim sistemi ve Jupyter not defteri çalıştırmak için kullanılır. Azure Linux ve Windows sanal makineleri çalıştırabilen ve her iki tür sanal makineler üzerinde Jupyter Kurulum ele alınacaktır.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Bir Linux VM oluşturun ve Jupyter için bir bağlantı noktasını açın
Verilen yönergeleri izleyin [burada] [ portal-vm-linux] , bir sanal makine oluşturmak için *Ubuntu* dağıtım. Bu öğretici, Ubuntu Server 14.04 LTS kullanır. Kullanıcı adı varsayıyoruz *azureuser*.

Sanal makine dağıtıldıktan sonra bir ağ güvenlik grubu güvenlik kuralı açmak gerekir.  Azure Portal'dan Git **ağ güvenlik grupları** ve VM'nize karşılık gelen güvenlik grubu için sekmesini açın. Aşağıdaki ayarlarla bir gelen güvenlik kuralı eklemeniz gerekir: **TCP** protokolü için  **\***  kaynak (Genel) bağlantı noktası için ve **9999** için (özel) hedef bağlantı noktası.

![ekran görüntüsü](./media/jupyter-notebook/azure-add-endpoint.png)

Ağ güvenlik grubundaki karşın, tıklayın **ağ arabirimleri** ve not edin **genel IP adresi** sonraki adımda VM'nize bağlanmak için gerekli şekilde.

## <a name="install-required-software-on-the-vm"></a>Gerekli yazılımı'nı VM'e yükleyin
Jupyter not defteri bizim VM üzerinde çalıştırmak için biz öncelikle Jupyter ve bağımlılıklarını yüklemeniz gerekir. Linux vm ssh kullanarak bağlanma ve kullanıcı adı/parola eşleştirin vm oluştururken seçtiniz. Bu öğreticide biz PuTTY kullanın ve Windows'dan bağlanın.

### <a name="installing-jupyter-on-ubuntu"></a>Ubuntu üzerinde Jupyter yükleme
Tablodan sağlanan bağlantılardan birini kullanarak Anaconda, popüler veri bilimi python dağıtımı yüklemek [Continuum Analytics](https://www.continuum.io/downloads).  İtibariyle, bu belgenin bağlantılardır en tarih sürümleri kadar.

#### <a name="anaconda-installs-for-linux"></a>Linux için anaconda yükler
<table>
  <th>Python 3.4</th>
  <th>Python 2.7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Anaconda3 yükleme 2.3.0 Ubuntu üzerinde 64-bit
Örnek olarak, bu, Ubuntu üzerinde Anaconda nasıl yükleyebileceğinizi değil.

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![ekran görüntüsü](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Jupyter yapılandırma ve SSL kullanma
Yükledikten sonra bir kez Jupyter için kurulum yapılandırma dosyaları için bir dakikanızı ayırın gerekiyor. Jupyter yapılandırma ile sorunlarına karşılaşırsanız bakmak yararlı olabilir [Jupyter not defteri Server çalıştıran belgelerine](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Sonraki biz `cd` profili dizine bizim SSL sertifikası oluşturun ve profilleri yapılandırma dosyasını düzenleyin.

Linux üzerinde aşağıdaki komutu kullanın.

    cd ~/.jupyter

SSL sertifikası (Linux ve Windows) oluşturmak için aşağıdaki komutu kullanın.

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Dizüstü tarayıcınız bağlamak için bir güvenlik uyarısı verecektir olduğunda otomatik olarak imzalanan bir SSL sertifikası oluşturmakta olduğunuz bu yana unutmayın.  Uzun vadeli üretim kullanımı için kuruluşunuz ile ilişkilendirilen düzgün olarak imzalanan bir sertifika kullanmak istersiniz.  Sertifika yönetiminin bu demo kapsamında olduğundan, biz kendinden imzalı bir sertifika için şu an için bağlı kalın.

Bir sertifika kullanarak ek olarak, dizüstü bilgisayarınızı yetkisiz kullanıma karşı korumak için bir parola sağlamalısınız.  Parolanızı ilk şifrelemek gerekir böylece güvenlik nedenleriyle, yapılandırma dosyasında şifrelenmiş parolalar Jupyter kullanır.  Bunu yapmak için bir yardımcı program IPython sağlar; bir komut isteminde aşağıdaki komutu çalıştırın.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Bu bir parola ve onay ister ve ardından parolayı yazdırır. İçin aşağıdaki adımı unutmayın.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

Ardından, biz profilinin yapılandırma dosyasını düzenlersiniz `jupyter_notebook_config.py` bulunduğunuz dizindeki dosyayı.  Bu dosya, olmayabilir--Not Böyle değilse yalnızca oluşturun.  Bu dosya alan sayısını vardır ve varsayılan olarak tüm dışı bırakılır.  Bu dosyayı, istediğiniz herhangi bir metin düzenleyicisi ile açmak ve onu en az aşağıdaki içeriğe sahip olmanız gerekir. **Önceki adımdan sha1 yapılandırmada c.NotebookApp.password değiştirdiğinizden emin olun**.

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a>Jupyter not defteri çalıştırın
Bu noktada biz Jupyter not defteri başlatmaya hazırsınız. Bunu yapmak için not defterlerinde depolamak ve Jupyter not defteri sunucusu aşağıdaki komutla başlatmak istediğiniz dizine gidin.

    /anaconda3/bin/jupyter-notebook

Şimdi, Jupyter not defteri adresinde erişebilir olmalıdır `https://[PUBLIC-IP-ADDRESS]:9999`.

Dizüstü bilgisayarınızı ilk eriştiğinizde, oturum açma sayfasına parolanızı ister. Ve oturum açtığında Tim merkezi tüm dizüstü bilgisayar işlemleri için olan "Jupyter not defteri panoyu" görürsünüz.  Bu sayfadan yeni not defterlerini oluşturun ve varolanları açın.

![ekran görüntüsü](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a>Jupyter Not Defteri kullanarak
Tıklatırsanız **yeni** düğme, aşağıdaki açma sayfasını görürsünüz.

![ekran görüntüsü](./media/jupyter-notebook/jupyter-untitled-notebook.png)

Alan işaretlenmiş bir `In []:` istemi giriş alanını ve geçerli bir Python kodu buraya yazın ve, isabet olduğunda yürütecek `Shift-Enter` veya (sağı gösteren üçgen araç çubuğunda) "Çalıştır" simgesine tıklayın.

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Güçlü bir standardı: zengin medya hesaplama belgelerle Canlı
Bazı yönlerden her ikisinin bir karışımı olduğundan dizüstü Python ve bir sözcük işlemci kullandı herkes çok doğal geliyor olmalıdır: Python kod bloklarını yürütebilir, ancak bir "Markdo"Code"hücreden stilini değiştirerek notları ve diğer metin da tutabilirsiniz aşağı"araç çubuğundaki aşağı açılan menüyü kullanarak.

Jupyter hesaplama ve zengin ortam (metin, grafik, video ve hemen modern bir web tarayıcısı görüntüleyebilirsiniz her şeyi) karıştırma verdiğinden sözcük işlemci çok daha fazladır. Karışımı, metin, kod, videolar ve daha fazlası!

![ekran görüntüsü](./media/jupyter-notebook/jupyter-editing-experience.png)

Ve bilimsel ve teknik için birçok mükemmel kitaplıkları Python'un gücü, aşağıdaki ekran görüntüsünde, basit bir hesaplama bir karmaşık ağ analizi, tüm bir ortamda olarak aynı kolaylığı ile gerçekleştirilebilir.

Modern web gücünü Canlı hesaplama ile karıştırma, bu kip pek çok sayıda olasılık sunar ve bulut için ideal uygundur; Not Defteri kullanılabilir:

* Keşif kaydetmek için hesaplama bir karalama alanı bir sorun üzerinde çalışır.
* 'Canlı' hesaplama form veya basılı kopya biçimleri (HTML, PDF) iş arkadaşlarınızı sonuçları paylaşmak için.
* Dağıtma ve dinamik öğretme sunmak için hesaplama, Öğrenciler hemen gerçek koduyla deneyebilirsiniz şekilde gerektiren malzemeleri değiştirin ve etkileşimli olarak yeniden çalıştırın.
* "Araştırma sonuçlarını hemen çoğaltılamaz, doğrulandı ve başkaları tarafından genişletilmiş bir şekilde sunmak yürütülebilir yazıları" sağlamak için.
* Ortak bilgi işlem için bir platform olarak: birden çok kullanıcı Canlı hesaplama oturumu paylaşmak için aynı not defteri sunucuya oturum açabilirsiniz.

IPython kaynak koduna giderseniz [deposu][repository], indirin ve ardından kendi Azure Jupyter VM deneme dizüstü bilgisayar örnekleri ile tüm bir dizin bulacaksınız.  Yalnızca karşıdan `.ipynb` sitesinden dosyaları ve dizüstü bilgisayarınızı Azure VM Pano yükleyin (veya doğrudan VM'de oturum indirin).

## <a name="conclusion"></a>Sonuç
Jupyter Not Defteri, etkileşimli olarak Azure üzerinde Python ekosistemi gücünü erişmek için güçlü bir arabirim sağlar.  Çok çeşitli Python, veri çözümleme ve görselleştirme, benzetimi ve paralel bilgi işlem öğrenme ve basit araştırması dahil olmak üzere kullanım durumları kapsar. Sonuçta elde edilen not defteri belgeler gerçekleştirilir ve diğer Jupyter kullanıcılarla paylaşılabilir hesaplamayı eksiksiz bir kaydı içerir.  Jupyter not defteri yerel bir uygulama kullanılabilir, ancak azure'da bulut dağıtımları için ideal olarak uygun

Jupyter çekirdek özelliklerini de Visual Studio içinde kullanılabilir [Visual Studio için Python Araçları] [ Python Tools for Visual Studio] (PTVS). PTVS olan ücretsiz ve açık kaynaklı Visual Studio hata ayıklama, IntelliSense, Gelişmiş bir düzenleyiciyle içeren Gelişmiş bir Python geliştirme ortamında profil oluşturma ve paralel dönüştürür Microsoft'tan eklenti computing tümleştirme.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz. [Python Geliştirici Merkezi](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
