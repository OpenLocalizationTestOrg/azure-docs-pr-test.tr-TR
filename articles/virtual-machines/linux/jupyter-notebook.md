---
title: aaaCreate Jupyter/IPython not defteri | Microsoft Docs
description: "Bir Linux sanal makinede toodeploy hello Jupyter/IPython dizüstü hello resource manager dağıtım modeline Azure ile nasıl oluşturulacağını öğrenin."
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
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Bir Azure Jupyter yükleme ve Jupyter not defteri Azure üzerinde çalışan VM oluşturma
Merhaba [Jupyter proje](http://jupyter.org), eskiden hello [IPython proje](http://ipython.org), bir koleksiyon için araçlar sağlar kod yürütmeyi hello oluşturulmasını ile birleştirin güçlü etkileşimli Kabukları kullanarak bilimsel hesaplama Canlı bir hesaplama belge. Bu not defteri dosyaları rastgele metin, matematiksel formüller, giriş kod, sonuçları, grafik, videolar ve modern bir web tarayıcısı görüntüleyebilen ortamının başka herhangi bir tür içerebilir. Olup kesinlikle yeni tooPython olduğunuz ve toolearn istiyorsanız bunu eğlenceli, etkileşimli ortam veya bazı önemli paralel/bilgi işlem teknik hello Jupyter not defteri olduğu harika bir seçim yapın.

![Ekran](./media/jupyter-notebook/ipy-notebook-spectral.png) ses kaydını kullanarak SciPy ve Matplotlib paketleri tooanalyze hello yapısı.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Jupyter iki yolu: Azure dizüstü bilgisayarlar veya özel dağıtım
Azure çok kullanabileceğiniz bir hizmet sunar[Jupyter kullanarak hızlı bir şekilde başlatmak ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  Hello Azure Not Defteri hizmeti kullanarak erişim tooJupyter'ın web üzerinden erişilebilen arabirimi kolayca kazanmadan Python tüm hello gücünü ve birçok kitaplıkları ile ölçeklenebilir hesaplama kaynaklarına.  Merhaba yükleme hello hizmeti tarafından işlenen olduğundan, kullanıcılar Yönetim ve yapılandırma hello kullanıcı tarafından hello gerek kalmadan bu kaynaklara erişebilir.

Lütfen Hello Not Defteri hizmeti senaryonuz için işe yaramazsa tooread size nasıl toodeploy hello Jupyter not defteri Microsoft Azure üzerinde Linux sanal makineleri (VM'ler) kullanarak gösterir bu makalenin devam edin.

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Oluşturma ve Azure üzerinde bir VM yapılandırma
Merhaba ilk adım bir Azure üzerinde çalıştıran sanal makine (VM) toocreate değil.
Bu VM hello bulutta eksiksiz bir işletim sistemi ve hello Jupyter not defteri çalıştırmak için kullanılır. Azure Linux ve Windows sanal makineleri çalıştırabilen ve her iki tür sanal makineler üzerinde Jupyter hello Kurulumu ele alınacaktır.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Bir Linux VM oluşturun ve Jupyter için bir bağlantı noktasını açın
Verilen hello yönergeleri [burada] [ portal-vm-linux] toocreate hello bir sanal makineye *Ubuntu* dağıtım. Bu öğretici, Ubuntu Server 14.04 LTS kullanır. Merhaba kullanıcı adı varsayıyoruz *azureuser*.

Merhaba sanal makine dağıtıldıktan sonra tooopen hello ağ güvenlik grubundaki güvenlik kuralı ihtiyacımız var.  Azure portal Hello çok Git**ağ güvenlik grupları** ve hello güvenlik grubuna karşılık gelen tooyour VM için açık hello sekmesi. Ayarları aşağıdaki hello ile tooadd gelen güvenlik kuralı gerekir: **TCP** hello protokolü için  **\***  hello kaynak (Genel) bağlantı noktası için ve **9999** için Merhaba (özel) hedef bağlantı noktası.

![ekran görüntüsü](./media/jupyter-notebook/azure-add-endpoint.png)

Ağ güvenlik grubundaki karşın, tıklayın **ağ arabirimleri** ve Not hello **genel IP adresi** hello sonraki adımda gerekli tooconnect tooyour VM olacak şekilde.

## <a name="install-required-software-on-hello-vm"></a>Merhaba VM üzerinde gerekli yazılımı yükleyin
toorun Merhaba bizim VM'de Jupyter Not Defteri, biz Jupyter ve bağımlılıklarını önce yüklemeniz gerekir. SSH kullanarak tooyour linux vm bağlanın ve vm oluştururken seçtiğiniz hello kullanıcı adı/parola çifti hello. Bu öğreticide biz PuTTY kullanın ve Windows'dan bağlanın.

### <a name="installing-jupyter-on-ubuntu"></a>Ubuntu üzerinde Jupyter yükleme
Tablodan sağlanan hello bağlantılardan birini kullanarak Anaconda, popüler veri bilimi python dağıtımı yüklemek [Continuum Analytics](https://www.continuum.io/downloads).  Bu belgenin Hello makalenin yazıldığı sırada hello aşağıdaki bağlantıları var. hello en toodate sürümleri ayarlama

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

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![ekran görüntüsü](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Jupyter yapılandırma ve SSL kullanma
Yükledikten sonra tootake şu anda toosetup hello yapılandırma dosyaları için Jupyter ihtiyacımız var. Jupyter yapılandırma ile sorunlarına karşılaşırsanız hello en yararlı toolook olabilir [Jupyter not defteri Server çalıştıran belgelerine](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Sonraki biz `cd` toohello directory toocreate bizim SSL sertifikası profili ve hello profilleri yapılandırma dosyasını düzenleyin.

Linux'ta hello aşağıdaki komutu kullanın.

    cd ~/.jupyter

Komut toocreate hello SSL sertifikası (Linux ve Windows) aşağıdaki hello kullanın.

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Toohello dizüstü bağlanırken otomatik olarak imzalanan bir SSL sertifikası oluşturuyoruz olduğundan tarayıcınız bir güvenlik uyarısı erişmenizi sağlayan olduğunu unutmayın.  Uzun vadeli üretim kullanımı için toouse kuruluşunuz ile ilişkilendirilen düzgün olarak imzalanan bir sertifika isteyeceksiniz.  Sertifika yönetimi bu demo hello kapsamı dışında olduğundan, biz tooa otomatik olarak imzalanan sertifika şu an için bağlı kalın.

Ayrıca bir sertifika toousing, de parola tooprotect defterinizde yetkisiz kullanıma karşı belirtmeniz gerekir.  Tooencrypt gerekir böylece güvenlik nedenleriyle Jupyter şifrelenmiş parola, yapılandırma dosyasında parolanızı ilk kullanır.  IPython yardımcı programı toodo bunu sağlar; bir komut isteminde hello aşağıdaki komutu çalıştırın.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Bu bir parola ve onay ister ve ardından hello parola yazdırır. Bu adım aşağıdaki Merhaba unutmayın.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

Ardından, biz hello profilinin yapılandırma dosyasını düzenlersiniz `jupyter_notebook_config.py` bulunduğunuz hello dizindeki dosyayı.  Bu dosya, olmayabilir--not yalnızca, hello durumda oluşturun.  Bu dosya alan sayısını vardır ve varsayılan olarak tüm dışı bırakılır.  Bu dosyayı, istediğiniz herhangi bir metin düzenleyicisi ile açmak ve onu sahip en az Merhaba, içerik emin olmalısınız. **Merhaba sha1 hello önceki adımdaki ile Merhaba yapılandırmada emin tooreplace hello c.NotebookApp.password olması**.

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>Merhaba Jupyter not defteri çalıştırın
Bu noktada hazır toostart hello Jupyter not defteri duyuyoruz. toodo bunu toostore not defterlerini istediğiniz ve komut aşağıdaki hello ile Merhaba Jupyter not defteri sunucu başlangıç toohello dizinine gidin.

    /anaconda3/bin/jupyter-notebook

Şimdi gerekir, Jupyter not defteri hello adresindeki mümkün tooaccess olması `https://[PUBLIC-IP-ADDRESS]:9999`.

Dizüstü bilgisayarınızı ilk eriştiğinizde hello oturum açma sayfası için parolanızı ister. Ve oturum açtığında Tim merkezi tüm dizüstü bilgisayar işlemleri için olduğu hello "Jupyter not defteri Pano" görürsünüz.  Bu sayfadan yeni not defterlerini oluşturun ve varolanları açın.

![ekran görüntüsü](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>Merhaba Jupyter Not Defteri kullanarak
Merhaba tıklatırsanız **yeni** düğmesi, giriş sayfası aşağıdaki hello görürsünüz.

![ekran görüntüsü](./media/jupyter-notebook/jupyter-untitled-notebook.png)

Merhaba alanı ile işaretlenmiş bir `In []:` istemi hello giriş alanını ve geçerli bir Python kodu buraya yazın ve, isabet olduğunda yürütecek `Shift-Enter` veya hello "Yürüt" simgesini (Merhaba sağı üçgen hello araç çubuğunda) tıklayın.

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Güçlü bir standardı: zengin medya hesaplama belgelerle Canlı
Bazı yönlerden her ikisinin bir karışımı olduğundan, Hello dizüstü kendisini Python ve bir sözcük işlemci kullanan çok doğal tooanyone eşitleyerek: Python kod bloklarını yürütebilir, ancak çok "Code" hücreden hello stilini değiştirerek notları ve diğer metin da tutabilirsiniz "Ma rkdown"Merhaba açılır menü araç çubuğundaki kullanarak.

Jupyter hesaplama ve zengin ortam (metin, grafik, video ve hemen modern bir web tarayıcısı görüntüleyebilirsiniz her şeyi) karıştırma verdiğinden sözcük işlemci çok daha fazladır. Karışımı, metin, kod, videolar ve daha fazlası!

![ekran görüntüsü](./media/jupyter-notebook/jupyter-editing-experience.png)

Ve kitaplıkların bilimsel ve teknik, ekran, aşağıdaki hello bilgi işlem için Python'un birçok mükemmel hello gücüne sahip basit bir hesaplama ile aynı tüm bir ortamda bir karmaşık ağ analizi olarak kolaylaştırır hello gerçekleştirilebilir.

Bu kip hello modern web hello gücünü Canlı hesaplama ile karıştırma, çok sayıda olasılık sunar ve hello bulut için ideal olarak uygundur; Merhaba not defteri kullanılabilir:

* Hesaplama karalama alanı toorecord keşif bir sorun üzerinde çalışır.
* arkadaşlarınızla 'Canlı' hesaplama formunda veya basılı kopya biçimleri (HTML, PDF) tooshare sonuçlanır.
* toodistribute ve hesaplama, Öğrenciler hemen hello gerçek koduyla deneyebilirsiniz şekilde gerektiren mevcut Canlı öğretme malzemeleri değiştirin ve etkileşimli olarak yeniden çalıştırın.
* "hello sonuçlarını araştırma hemen çoğaltılamaz bir biçimde sunmak yürütülebilir yazıları" tooprovide doğrulandı ve başkaları tarafından Genişletilmiş.
* Ortak bilgi işlem için bir platform olarak: birden çok kullanıcı aynı toothe içinde oturum not defteri sunucu tooshare Canlı hesaplama oturumu.

Toohello IPython kaynak kodu giderseniz [deposu][repository], indirin ve ardından kendi Azure Jupyter VM deneme dizüstü bilgisayar örnekleri ile tüm bir dizin bulacaksınız.  Yalnızca hello karşıdan `.ipynb` hello dosyalarından site ve dizüstü bilgisayarınızı Azure VM hello Pano yükleyin (veya hello doğrudan VM indirin).

## <a name="conclusion"></a>Sonuç
Merhaba Jupyter Not Defteri, azure'da hello Python ekosistemi hello gücü etkileşimli olarak erişmek için güçlü bir arabirim sağlar.  Çok çeşitli Python, veri çözümleme ve görselleştirme, benzetimi ve paralel bilgi işlem öğrenme ve basit araştırması dahil olmak üzere kullanım durumları kapsar. Merhaba elde edilen not defteri belgeler gerçekleştirilir ve diğer Jupyter kullanıcılarla paylaşılabilir hello hesaplamalar eksiksiz bir kaydı içerir.  Merhaba Jupyter not defteri yerel bir uygulama kullanılabilir, ancak azure'da bulut dağıtımları için ideal olarak uygun

Merhaba çekirdek Jupyter özelliklerini Visual Studio içinde kullanılabilir de [Visual Studio için Python Araçları] [ Python Tools for Visual Studio] (PTVS). PTVS olan ücretsiz ve açık kaynaklı Visual Studio hata ayıklama, IntelliSense, Gelişmiş bir düzenleyiciyle içeren Gelişmiş bir Python geliştirme ortamında profil oluşturma ve paralel dönüştürür Microsoft'tan eklenti computing tümleştirme.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
