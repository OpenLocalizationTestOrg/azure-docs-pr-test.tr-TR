---
title: "karma bir HPC Pack yukarı aaaSet küme Azure'da | Microsoft Docs"
description: "Küçük, karma yüksek performanslı bilgi işlem (HPC) küme toouse Microsoft HPC Pack ve Azure tooset nasıl yukarı öğrenin"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Bir karma yüksek performanslı bilgi işlem (HPC) küme Microsoft HPC Pack ve isteğe bağlı Azure işlem düğümleri ile ayarlama
Microsoft HPC Pack 2012 R2 ve bilgi işlem (HPC) küme küçük, karma yüksek performans ayarlama Azure tooset kullanın. Bu makalede gösterilen hello küme bir şirket içi HPC Pack baş düğümüne oluşur ve bazı düğümler isteğe bağlı bir azure'da dağıtmak bulut hizmeti işlem. Ardından, işlem işleri hello karma kümede çalıştırabilirsiniz.

![Karma HPC Kümesi][Overview] 

Bu öğretici bir yaklaşım gösterir bazen küme "veri bloğu toohello bulut," toouse ölçeklenebilir, isteğe bağlı Azure kaynaklarını toorun yoğun uygulamalar çağrılır.

Bu öğretici hesaplama kümeleri veya HPC paketi ile konusunda deneyim varsayar. Tanıtım amacıyla hızla karma işlem kümesi dağıtma hedeflenen yalnızca toohelp olur. Konuları ve adımları toodeploy karma HPC paketi küme büyük ölçekli bir üretim ortamında ya da toouse HPC Pack 2016 hello görmek için [ayrıntılı yönergeler](http://go.microsoft.com/fwlink/p/?LinkID=200493). HPC paketi ile diğer senaryolar için Azure sanal makineleri küme dağıtımında otomatik dahil olmak üzere, bkz: [azure'da Microsoft HPC paketi ile HPC küme seçenekleri](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="prerequisites"></a>Ön koşullar
* **Azure aboneliği** -bir Azure aboneliğiniz yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
* **Windows Server 2012 R2 veya Windows Server 2012 çalıştıran bir şirket içi bilgisayar** -hello baş düğümüne hello HPC Kümesi bu bilgisayarı kullanın. Windows Server zaten çalıştırmıyor değilse, yükleme indirin ve bir [Değerlendirme sürümü](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).
  
  * Merhaba bilgisayarın Active Directory etki alanına katılmış tooan olması gerekir. Test amaçları için hello baş düğümü bilgisayarının bir etki alanı denetleyicisi olarak yapılandırabilirsiniz. tooadd Active Directory etki alanı Hizmetleri sunucu rolünü Merhaba ve hello baş düğümü bilgisayarının bir etki alanı denetleyicisi olarak Yükselt, Windows Server hello belgelerine bakın.
  * Bu dillerden birinde toosupport HPC Pack Merhaba işletim sistemi yüklenmelidir: İngilizce, Japonca veya Çince (Basitleştirilmiş).
  * Önemli ve kritik güncelleştirmelerin yüklü olduğunu doğrulayın.
* **HPC Pack 2012 R2** - [karşıdan](http://go.microsoft.com/fwlink/p/?linkid=328024) hello yükleme paketi hello en son sürümünü gider ve kopyalama hello dosyaları toohello baş düğüm bilgisayarı boş. Yükleme dosyaları hello aynı seçin dili olarak Windows Server yüklemenizin.

    >[!NOTE]
    > HPC Pack 2012 R2 yerine toouse HPC Pack 2016 istiyorsanız, ek yapılandırma gerekmez. Merhaba bkz [ayrıntılı yönergeler](http://go.microsoft.com/fwlink/p/?LinkID=200493).
    > 
* **Etki alanı hesabı** -bu hesap yerel yönetici izinleri hello baş düğüm tooinstall HPC Pack ile yapılandırılması gerekir.
* **TCP bağlantı noktası 443 üzerinden** hello baş düğüm tooAzure gelen.

## <a name="install-hpc-pack-on-hello-head-node"></a>HPC Pack Merhaba baş düğüme yükleyin
Microsoft HPC Pack ilk Windows Server çalıştıran şirket içi bilgisayarınıza yükleyin. Bu bilgisayar hello küme baş düğümüne hello haline gelir.

1. Toohello baş düğümünde yerel yönetici izinlerine sahip bir etki alanı hesabı kullanarak oturum açın.

2. Merhaba HPC Pack yükleme dosyalarından Setup.exe çalıştırarak Hello HPC Pack Yükleme Sihirbazı'nı başlatın.

3. Merhaba üzerinde **HPC Pack 2012 R2 Kurulum** ekranında **yeni yükleme veya yeni özellikler tooan mevcut yükleme ekleme**.

    ![HPC Pack 2012 Kurulumu][install_hpc1]

4. Merhaba üzerinde **Microsoft yazılım kullanıcı Sözleşmesi sayfası**, tıklatın **sonraki**.

5. Merhaba üzerinde **yükleme türünü seç** sayfasında, **bir baş düğüm oluşturarak yeni bir HPC kümesi oluşturma**ve ardından **sonraki**.

6. Merhaba Sihirbazı çeşitli ön yükleme testleri çalıştırır. Tıklatın **sonraki** hello üzerinde **yükleme kuralları** tüm testleri geçerse sayfa. Aksi takdirde, sağlanan hello bilgileri gözden geçirin ve ortamınızda gerekli değişiklikleri yapın. Daha sonra yeniden hello testler veya gerekli başlangıç Yükleme Sihirbazı'nı yeniden hello varsa çalıştırın.
7. Merhaba üzerinde **HPC DB yapılandırma** sayfasında, emin olun **baş düğüm** tüm HPC veritabanları için seçilir ve ardından **sonraki**. 

    ![DB yapılandırma][install_hpc4]

8. Merhaba sihirbazın hello kalan sayfalarındaki varsayılan seçimleri kabul edin. Merhaba üzerinde **gerekli bileşenleri yüklemek** sayfasında, **yükleme**.
   
    ![Yükleme][install_hpc6]

9. Merhaba yükleme tamamlandıktan sonra işaretini **HPC Küme Yöneticisi'ni başlatın** ve ardından **son**. (Bir sonraki adımda HPC Küme Yöneticisi'ni başlatın.)
   
    ![Son][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Hello Azure aboneliği hazırlama
Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com) Azure aboneliğinizle. Bu adımları tamamladıktan sonra Azure düğümleri hello şirket içi baş düğümünden dağıtabilirsiniz. 
  
  > [!NOTE]
  > Ayrıca, daha sonra ihtiyacınız Azure abonelik Kimliğinizi not edin. Merhaba Kimliğinde Bul **abonelikleri** hello Portalı'nda.
  > 

### <a name="upload-hello-default-management-certificate"></a>Merhaba varsayılan yönetim sertifikasını karşıya yükle
HPC Pack Merhaba baş düğüm Azure yönetim sertifikası karşıya yükleyebilir hello Microsoft HPC Azure Management varsayılan sertifika olarak adlandırılan, kendinden imzalı bir sertifika yükler. Bu sertifikayı test etmek için sağlanır ve kavram kanıtı dağıtımları toosecure hello bağlantı arasındaki hello baş düğüm ve Azure.

1. Merhaba baş düğüm bilgisayardan toohello içinde oturum [Azure portal](https://portal.azure.com).

2. Tıklatın **abonelikleri** > *your_subscription_name*.

3. Tıklatın **yönetim sertifikaları** > **karşıya**.4. Merhaba baş düğümünde hello dosyası C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer için göz atın. Ardından **karşıya**.

   
Merhaba **HPC Azure Management'ı varsayılan** sertifika hello yönetim sertifikaları listesinde görünür.

### <a name="create-an-azure-cloud-service"></a>Bir Azure bulut hizmeti oluşturma
> [!NOTE]
> En iyi performans için hello bulut hizmeti hello depolama hesabında (bir sonraki adımda) hello oluşturup aynı coğrafi bölgede.
> 
> 

1. Merhaba Portalı'nda tıklatın **bulut hizmetlerini (Klasik)** > **+ Ekle**.

2.  Merhaba hizmeti için bir DNS adı yazın, bir kaynak grubu ve bir konum seçin ve ardından **oluşturma**.


### <a name="create-an-azure-storage-account"></a>Azure Storage hesabı oluşturma
1. Merhaba Portalı'nda tıklatın **depolama hesapları (Klasik)** > **+ Ekle**.

2. Merhaba hesabı için bir ad yazın ve seçin hello **Klasik** dağıtım modeli.

3. Bir kaynak grubu ve bir konum seçin ve diğer ayarları varsayılan değerlerinde bırakın. Sonra **Oluştur**’a tıklayın.

## <a name="configure-hello-head-node"></a>Merhaba baş düğüm yapılandırın
HPC Küme Yöneticisi'ni toodeploy toouse Azure düğümleri ve toosubmit işleri önce bazı gerekli küme yapılandırma adımlarını gerçekleştirin.

1. Merhaba baş düğümünde HPC Küme Yöneticisi'ni başlatın. Merhaba, **baş düğüm Seç** iletişim kutusu görüntülenirse, tıklatın **yerel bilgisayar**. Merhaba **dağıtım Yapılacaklar listesi** görüntülenir.

2. Altında **gerekli dağıtım görevlerini**, tıklatın **ağınızı yapılandırmak**.
   
    ![Ağ yapılandırma][config_hpc2]

3. Hello Ağ Yapılandırma Sihirbazı'nı seçin **yalnızca bir kurumsal ağ üzerindeki tüm düğümleri** (topoloji 5). Bu ağ hello tanıtım amacıyla basit bir yapılandırmadır.
   
    ![Topoloji 5][config_hpc3]
   
4. Tıklatın **sonraki** hello Sihirbazı sayfaları kalan hello tooaccept varsayılan değerler. Ardından, hello **gözden geçirme** sekmesini tıklatın, **yapılandırma** toocomplete hello ağ yapılandırması.

5. Merhaba, **dağıtım Yapılacaklar listesi**, tıklatın **yükleme kimlik bilgileri sağlamak**.

6. Merhaba, **yükleme kimlik bilgileri** iletişim kutusu, tooinstall HPC Pack kullanılan hello etki alanı hesabının hello kimlik bilgilerini yazın. Daha sonra, **Tamam**'a tıklayın. 
   
    ![Yükleme kimlik bilgileri][config_hpc6]
   
7. Merhaba, **dağıtım Yapılacaklar listesi**, tıklatın **yeni düğümlerinin hello adlandırma yapılandırma**.

8. Merhaba, **düğümü adlandırma serisi belirtin** iletişim kutusunda, hello varsayılan serisi ve tıklatın adlandırma kabul **Tamam**. Hello Azure düğümleri Bu öğreticide Ekle otomatik olarak adlandırılmış olsa da bu adımı tamamlayın.
   
    ![Düğüm adlandırma][config_hpc8]
   
9. Merhaba, **dağıtım Yapılacaklar listesi**, tıklatın **düğüm şablonu oluşturma**. Daha sonra hello öğreticide hello düğüm şablonu tooadd Azure düğümleri toohello küme kullanın.

10. İçinde düğüm şablonu oluşturma Sihirbazı Merhaba, aşağıdaki hello yapın:
    
    a. Merhaba üzerinde **düğümü şablon türünü seç** sayfasında, **Windows Azure düğüm şablonu**ve ardından **sonraki**.
    
    ![Düğüm şablonu][config_hpc10]
    
    b. Tıklatın **sonraki** tooaccept hello varsayılan şablon adı.
    
    c. Merhaba üzerinde **abonelik bilgilerini gir** sayfasında, Azure abonelik Kimliğinizi (Azure hesap bilgilerinizi kullanılabilir) girin. Ardından **yönetim sertifikası**, göz **varsayılan Microsoft HPC Azure yönetimi.** Ardından **İleri**'ye tıklayın.
    
    ![Düğüm şablonu][config_hpc12]
    
    d. Merhaba üzerinde **hizmet bilgileri sağlayan** sayfası, select hello bulut hizmeti ve bir önceki adımda oluşturduğunuz hello depolama hesabı. Ardından **İleri**'ye tıklayın.
    
    ![Düğüm şablonu][config_hpc13]
    
    e. Tıklatın **sonraki** hello Sihirbazı sayfaları kalan hello tooaccept varsayılan değerler. Ardından, hello **gözden geçirme** sekmesini tıklatın, **oluşturma** toocreate hello düğüm şablonu.
    
    > [!NOTE]
    > Varsayılan olarak, hello Azure düğüm şablonu (sağlayamaz) toostart ve durdurma hello düğümleri ayarlarını el ile HPC Küme Yöneticisi'ni kullanarak içerir. İsteğe bağlı olarak bir zamanlama toostart yapılandırabilirsiniz ve Azure düğümleri otomatik olarak hello durdurun.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Azure düğümleri toohello küme ekleme
Şimdi hello düğüm şablonu tooadd Azure düğümleri toohello küme kullanın. Hello düğümleri toohello küme (sağlayamaz) başlayabilmeniz için yapılandırma bilgilerini depolayan ekleme hello bulut hizmetindeki herhangi bir zamanda bunları. Merhaba örnekleri hello bulut hizmetinde çalışan sonra aboneliğinizi yalnızca Azure düğümleri için sizden ücret.

Bu adımları tooadd iki küçük düğümler izleyin.

1. HPC Küme Yöneticisi'nde **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack geçerli sürümlerinde) > **düğüm Ekle**.
   
    ![Düğüm Ekle][add_node1]

2. İçinde Düğüm Ekleme Sihirbazı, üzerinde hello hello **dağıtım yöntemini seçin** sayfasında, **Ekle Windows Azure düğümleri**ve ardından **sonraki**.
   
    ![Azure düğüm Ekle][add_node1_1]

3. Merhaba üzerinde **belirtin yeni düğümler** sayfası, önceden oluşturduğunuz select hello Azure düğüm şablonu (varsayılan olarak adlandırılan **varsayılan AzureNode şablonu**). Ardından belirtin **2** boyutu düğümlerinin **küçük**ve ardından **sonraki**.
   
    ![Düğüm belirtin][add_node2]
   
4. Merhaba üzerinde **Düğüm Ekleme Sihirbazı Tamamlanıyor hello** sayfasında, **son**.
    
     Adlı iki Azure düğümleri **AzureCN 0001** ve **AzureCN 0002**, artık HPC Küme Yöneticisi'nde görüntülenir. Her ikisi de hello olan **değil dağıtılan** durumu.
   
    ![Eklenen düğümlerine][add_node3]

## <a name="start-hello-azure-nodes"></a>Başlangıç Azure düğümleri hello
İstediğiniz zaman toouse hello küme kaynakları Azure, kullanım HPC Küme Yöneticisi'ni toostart (sağlayamaz) Azure düğümleri hello ve çevrimiçi duruma getirin.

1. HPC Küme Yöneticisi'nde **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack geçerli sürümlerinde), ve hello Azure düğümleri seçin.

2. Tıklatın **Başlat**ve ardından **Tamam**.
   
   ![Düğümleri Başlat][add_node4]
   
    Merhaba düğümleri geçiş toohello **sağlama** durumu. Görünüm hello sağlama ilerleme durumu günlük tootrack hello sağlama.
   
    ![Sağlama düğümler][add_node6]

3. Birkaç dakika sonra hello Azure düğümleri sağlama tamamladığınızda ve hello **çevrimdışı** durumu. Bu durumda, hello rol örnekleri çalıştıran ancak henüz küme işlerini kabul edemez.

4. Rol örnekleri hello tooconfirm çalışıyorsa, hello Azure Portalı'na tıklayın **bulut Hizmetleri (Klasik)** > *your_cloud_service_name*.
   
   İki görmelisiniz **HpcWorkerRole** hello Hizmeti'nde çalışan örnekleri (düğümler). HPC Pack ayrıca otomatik olarak dağıtan iki **HpcProxy** örnekleri (boyutu Orta) toohandle iletişimi hello baş düğüm ve Azure arasında.

   ![Çalışan örnekleri][view_instances1]

5. işlerini, select hello düğümleri, sağ tıklatın ve ardından toobring hello Azure düğümleri çevrimiçi toorun küme **çevrimiçine**.
   
    ![Çevrimdışı düğümler][add_node7]
   
    HPC Küme Yöneticisi'ni gösterir hello düğümlerin hello olduğunu **çevrimiçi** durumu.

## <a name="run-a-command-across-hello-cluster"></a>Merhaba küme üzerinde bir komutu çalıştırın
toocheck hello yükleme, kullanım hello HPC Pack **clusrun** komutu toorun bir komutu veya bir veya daha fazla küme düğümlerinde uygulama. Basit bir örnek olarak kullanın **clusrun** tooget hello IP yapılandırması hello Azure düğümleri.

1. Merhaba baş düğümünde yönetici olarak bir komut istemi açın.

2. Merhaba aşağıdaki komutu yazın:
   
    `clusrun /nodes:azurecn* ipconfig`

3. İstenirse, Küme Yönetici parolanızı girin. Benzer toohello aşağıdaki komut çıktısı görmeniz gerekir.
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a>Bir test işini çalıştır
Şimdi hello karma kümede çalışan bir test işi gönderin. Bu, bir basit parametrik tarama işi (doğası gereği Paralel hesaplama türü) örneğidir. Bu örnek bir tamsayı tooitself hello kullanarak eklemek görevleri çalıştırır **/a ayarlamak** komutu. Merhaba kümedeki tüm düğümlerin hello toofinishing hello görevleri tamsayılar 1 too100 katkıda.

1. HPC Küme Yöneticisi'nde **iş yönetimi** > **yeni parametrik Sweep işi**.
   
    ![Yeni Proje][test_job1]

2. Merhaba, **yeni parametrik Sweep işi** iletişim kutusunda **komut satırı**, türü `set /a *+*` (görünür hello varsayılan komut satırı üzerine). Ayarları kalan hello için varsayılan değerleri bırakın ve ardından **gönderme** toosubmit hello işi.
   
    ![Parametrik tarama][param_sweep1]

3. Merhaba işi bittiğinde hello çift **My Sweep görev** iş.

4. Tıklatın **görünümü görevleri**ve o alt alt tooview hesaplanan hello çıktısını'ı tıklatın.
   
    ![Görev sonuçları][view_job361]

5. hangi düğümün gerçekleştirilen hello hesaplama o alt görev için toosee tıklatın **ayrılan düğümler**. (Kümeniz farklı bir düğüme adını gösterebilir.)
   
    ![Görev sonuçları][view_job362]

## <a name="stop-hello-azure-nodes"></a>Durdur Azure düğümleri hello
Merhaba küme çalıştıktan sonra hello Azure düğümleri tooavoid gereksiz ücretleri tooyour hesabı durdurun. Bu adım hello bulut hizmetini durdurur ve hello Azure rol örneklerini kaldırır.

1. HPC Küme Yöneticisi ' nde, **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack önceki sürümlerinde), hem Azure düğümleri seçin. Ardından **durdurmak**.
   
    ![Düğümler durdurun][stop_node1]

2. Merhaba, **durdurmak Windows Azure düğümleri** iletişim kutusu, tıklatın **durdurmak**. 
   
3. Merhaba düğümleri geçiş toohello **durdurma** durumu. Birkaç dakika sonra hello düğümlerinin HPC Küme Yöneticisi'ni gösterir **değil dağıtılan**.
   
    ![Dağıtılmadı düğümler][stop_node4]

4. Merhaba rol örnekleri artık Azure üzerinde çalışan tooconfirm hello Azure portal'ı tıklatın **bulut hizmetlerini (Klasik)** > *your_cloud_service_name*. Hiçbir örneği hello üretim ortamına dağıtılır. 
   
    Başlangıç Öğreticisi tamamlar.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba belgelerine keşfedin [HPC Pack](https://technet.microsoft.com/library/cc514029).
* karma bir HPC paketi Küme dağıtımı büyük ölçekte yukarı tooset bkz [Microsoft HPC paketi ile tooAzure çalışan rolü örneklerine veri bloğu](http://go.microsoft.com/fwlink/p/?LinkID=200493).
* Azure Resource Manager şablonları kullanarak diğer yolları toocreate Azure bir HPC paketi küme için de dahil olmak üzere bkz [azure'da Microsoft HPC paketi ile HPC küme seçenekleri](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
