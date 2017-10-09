---
title: "Azure Machine Learning bir şirket içi SQL Server aaaUse | Microsoft Docs"
description: "Bir şirket içi SQL Server veritabanı tooperform Gelişmiş analitik verileri Azure Machine Learning ile kullanın."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Şirket içi SQL Server veritabanındaki verileri kullanarak Azure Machine Learning ile gelişmiş analiz gerçekleştirme

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Genellikle şirket içi verilerle çalışmak kuruluşların hello ölçek tootake avantajlarından ve bunların machine learning iş yükleri için hello bulutunun çeviklik ister. Ancak bunlar toodisrupt, geçerli iş süreçlerini ve iş akışları kendi şirket içi veri toohello bulut taşıyarak istemezsiniz. Azure Machine Learning artık bir şirket içi SQL Server veritabanından veri okumak ve ardından eğitim ve bu verileri ile bir model Puanlama destekler. Artık hello Bulut ve şirket içi sunucunuz arasında toomanually Kopyala ve eşitleme hello veri yok. Bunun yerine, hello **veri içeri aktarma** modül Azure Machine Learning Studio'da şimdi okuyabilir, doğrudan, şirket içi SQL Server veritabanından kendi eğitim ve puanlama işleri için.

Bu makalede nasıl tooingress SQL server verilerini Azure Machine Learning içi genel bir bakış sağlar. Çalışma alanları, modüller, veri kümeleri, denemeler, gibi Azure Machine Learning kavramlarını aşina varsayar *vb.*.

> [!NOTE]
> Bu özellik için ücretsiz çalışma alanı kullanılamıyor. Machine Learning fiyatlandırması ve katmanları hakkında daha fazla bilgi için bkz: [Azure Machine Learning fiyatlandırması](https://azure.microsoft.com/pricing/details/machine-learning/).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Merhaba Microsoft Veri Yönetimi ağ geçidi yükleyin
Azure Machine Learning bir şirket içi SQL Server veritabanında tooaccess, toodownload ve yükleme hello Microsoft Veri Yönetimi ağ geçidi gerekir. Machine Learning Studio'da Merhaba gateway bağlantısı yapılandırdığınızda hello ağ geçidi hello kullanarak karşıdan yükleyip hello olanağına sahip **karşıdan yükleme ve kaydetme veri ağ geçidi** aşağıda açıklanan iletişim.

İndirme ve hello hello MSI kurulum paketi çalıştırarak hello veri yönetimi ağ geçidi önceden yükleyebilirsiniz [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).
32 bit veya 64-bit, bilgisayarınız için uygun şekilde seçerek hello en son sürümünü seçin. Merhaba MSI kullanılan tooupgrade bir mevcut veri yönetimi ağ geçidi toohello en son sürümü, korunan tüm ayarlar ile de olabilir.

Merhaba ağ geçidi hello aşağıdaki önkoşullar vardır:

* Merhaba desteklenen Windows işletim sistemi sürümleri, Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 ve Windows Server 2012 R2 ' dir.
* Merhaba hello ağ geçidi makinesinin yapılandırması en az 2 GHz, 4 çekirdek, 8 GB RAM ve 80 GB disk önerilir.
* Merhaba ana makine hazırda bekleme durumunda hello ağ geçidi toodata isteklerine yanıt vermiyor. Bu nedenle, uygun güç planı hello bilgisayarda hello Gateway'i yüklemeden önce yapılandırın. Merhaba makine yapılandırılmış toohibernate ise, hello ağ geçidi yüklemesi bir ileti görüntüler.
* Kopyalama etkinliği belirli bir sıklıkta oluştuğundan hello kaynak kullanımı (CPU, bellek) hello makinede de aynı yoğun ve boşta saatlerle desen hello izler. Kaynak Kullanımı Yoğun olarak da hello taşınan veri miktarına bağlıdır. Birden çok kopyası işleri devam ederken, kaynak kullanımı yoğun zamanlarda gidebilir girdiğini. Merhaba en düşük yapılandırma yukarıda listelenen teknik olarak yeterli olsa da, veri taşıma için bağlı olarak belirli yük toohave hello en düşük yapılandırma daha fazla kaynak yapılandırmayla isteyebilirsiniz.

Ayarlama işlemleri ve veri yönetimi ağ geçidi kullanırken hello aşağıdakileri dikkate alın:

* Veri Yönetimi ağ geçidi yalnızca bir örneği tek bir bilgisayara yükleyebilirsiniz.
* Tek bir ağ geçidi birden çok şirket içi veri kaynakları için kullanabilirsiniz.
* Farklı bilgisayarlar toohello üzerinde birden çok ağ geçidi bağlanabilir aynı şirket içi veri kaynağı.
* Aynı anda yalnızca bir çalışma alanı için bir ağ geçidi yapılandırın. Şu anda, ağ geçitleri çalışma alanları arasında paylaşılamaz.
* Tek bir çalışma alanı için birden çok ağ geçidi yapılandırabilirsiniz. Örneğin, hazır toooperationalize olduğunuzda toouse geliştirme sırasında bağlı tooyour test veri kaynakları olan bir ağ geçidi ve bir üretim ağ geçidi isteyebilirsiniz.
* Merhaba ağ geçidi hello hello veri kaynağı olarak aynı makine üzerinde toobe gerekmez. Ancak daha yakından toohello kaldığını veri kaynağı hello ağ geçidi tooconnect toohello veri kaynağı hello süresini azaltır. Merhaba ağ geçidi ve veri kaynağı yok rekabet şekilde kaynaklar için bir ana bilgisayar hello şirket içi veri kaynağına hello farklı bir makinede hello ağ geçidi yüklemenizi öneririz.
* Ayrı bir ağ geçidi, Power BI veya Azure Data Factory senaryoları hizmet veren, bilgisayarınızda yüklü bir ağ geçidi zaten varsa, Azure Machine Learning için başka bir bilgisayara yükleyin.

  > [!NOTE]
  > Veri Yönetimi ağ geçidi ve Power BI Gateway hello üzerinde çalıştırılamaz aynı bilgisayar.
  >
  >
* Diğer veri için Azure ExpressRoute kullanıyor olsa bile, Azure Machine Learning için toouse hello veri yönetimi ağ geçidi gerekir. (Bir güvenlik duvarının arkasında olan) bir şirket içi veri kaynağı olarak veri kaynağınız düşünmelisiniz bile ExpressRoute kullandığınızda. Machine Learning hello veri kaynağı arasında Hello veri yönetimi ağ geçidi tooestablish bağlantısı kullanın.

Merhaba makalede yükleme önkoşulları, yükleme adımlarını ve sorun giderme ipuçları hakkında ayrıntılı bilgi bulabilirsiniz [veri yönetimi ağ geçidi](../data-factory/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>Şirket içi SQL Server veritabanınıza Azure Machine Learning giriş verileri
Bu kılavuzda, bir Azure Machine Learning çalışma alanında bir veri yönetimi ağ geçidi kurun ayarlama, yapılandırmak ve bir şirket içi SQL Server veritabanından veri okumak.

> [!TIP]
> Başlamadan önce tarayıcınızın açılır pencere engelleyicisi için devre dışı `studio.azureml.net`. Merhaba Google Chrome tarayıcısı kullanıyorsanız, karşıdan yükleyip hello birini birkaç eklentileri Google Chrome WebStore kullanılabilir [kez tıklayın uygulama uzantısı](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>1. adım: bir ağ geçidi oluşturma
Merhaba ilk adımı toocreate ve şirket içi SQL veritabanınız hello ağ geçidi tooaccess ayarlayın.

1. Çok oturum[Azure Machine Learning Studio](https://studio.azureml.net/Home/) ve toowork istediğiniz select hello çalışma alanı.
2. Hello'ı tıklatın **ayarları** hello dikey penceresinde sol ve hello ardından **veri ağ geçidi** sekmesini hello üstünde.
3. Tıklatın **yeni veri ağ geçidi** Merhaba ekranında hello sonundaki.

    ![Yeni veri ağ geçidi](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. Merhaba, **yeni veri ağ geçidi** iletişim kutusunda, hello girin **ağ geçidi adı** ve isteğe bağlı olarak ekleyin bir **açıklama**. Merhaba alt sağ köşesinde toogo toohello sonraki adıma hello yapılandırmasının Hello okuna tıklayın.

    ![Ağ geçidi ad ve açıklama girin](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. Merhaba karşıdan yükle ve veri ağ geçidi iletişim kutusunda, kopya hello ağ geçidi kayıt anahtarı toohello Pano kaydedin.

    ![Karşıdan yükle ve veri ağ geçidini kaydedin](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Henüz indirilir ve yüklenir, Microsoft Veri Yönetimi ağ geçidi hello ve ardından **indirme veri yönetimi ağ geçidi**. Toothe Microsoft İndirme Merkezi'nden hello ağ geçidi sürümü seçebileceğiniz bu alır, indirin ve yükleyin. Merhaba başına bölümlerde hello makalenin yükleme önkoşulları, yükleme adımlarını ve sorun giderme ipuçları hakkında ayrıntılı bilgi bulabilirsiniz [şirket içi kaynakları ve veri yönetimi ağ geçidiilebulutarasındaveritaşıma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Hello ağ geçidi yüklendikten sonra hello veri yönetimi ağ geçidi Yapılandırma Yöneticisi'ni açın hello ve **kayıt ağ geçidi** iletişim kutusu gösterilir. Yapıştır hello **ağ geçidi kayıt anahtarı** tıklayın ve toohello Panoya kopyalanan **kaydetmek**.
8. Yüklü bir ağ geçidi zaten varsa, hello veri yönetimi ağ geçidi yapılandırma yöneticisini çalıştırın. Tıklatın **anahtarı Değiştir**, yapıştırma **ağ geçidi kayıt anahtarı** hello önceki adımı ve tıklatın toohello Panoya kopyalanan **Tamam**.
9. Merhaba yüklemesi tamamlandıktan sonra hello **kayıt ağ geçidi** için Microsoft Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi iletişim kutusu gösterilir. Merhaba hello Panoya bir önceki adımda kopyaladığınız bir ağ geçidi kayıt ANAHTARINI yapıştırın ve tıklatın **kaydetmek**.

    ![Ağ geçidini kaydedin](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. değerleri aşağıdaki hello üzerinde hello ayarlandığında hello ağ geçidi yapılandırması tamamlandıktan **giriş** sekmesini Microsoft Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi'nde:

    * **Ağ geçidi adı** ve **örnek adı** toohello adı hello ağ geçidi olarak ayarlayın.
    * **Kayıt** çok ayarlanır**kayıtlı**.
    * **Durum** çok ayarlanır**başlatıldı**.
    * Merhaba alt görüntüler Hello durum çubuğu **tooData Yönetimi ağ geçidi bulut Hizmeti'ne bağlı** yeşil bir onay işareti yanı sıra.

      ![Veri Yönetimi Ağ Geçidi Yöneticisi](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      Azure Machine Learning Studio Hello kayıt başarılı olduğunda da güncelleştirilir.

    ![Ağ geçidi kaydı başarılı](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. Merhaba, **indirin ve veri ağ geçidini kaydetmek** iletişim kutusunda, onay işareti toocomplete hello yapısı'nı tıklatın. Merhaba **ayarları** sayfasında "Çevrimiçi" olarak ağ geçidi durumunu gösterir. Merhaba sağ taraftaki bölmede, durumunu ve diğer yararlı bilgiler bulabilirsiniz.

    ![Ağ Geçidi ayarları](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. Merhaba Microsoft Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi toohello geçiş **sertifika** bu sekmede belirtilen sekmesini hello sertifikasıdır belirttiğiniz hello şirket içi veri deposu için kullanılan tooencrypt/şifre çözme kimlik bilgileri Merhaba Portalı'nda. Bu sertifika hello varsayılan sertifika yok. Microsoft, sertifika yönetimi sisteminizi yedekleyin bu tooyour kendi sertifika değiştirme önerir. Tıklatın **değişiklik** toouse kullanarak kendi sertifikanızı yerine.

    ![Değişiklik ağ geçidi sertifikası](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (isteğe bağlı) Tooenable hello ağ geçidi ile ilgili sorunları gidermek için ayrıntılı günlük istiyorsanız hello Microsoft Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi toothe geçiş **tanılama** sekmesinde ve hello denetleyin **etkinleştir ayrıntılı sorun giderme amacıyla günlüğü** seçeneği. Merhaba günlük bilgileri hello Windows Olay Görüntüleyicisi'ni hello altında bulunabilir **uygulama ve hizmet günlükleri**  - &gt; **veri yönetimi ağ geçidi** düğümü. Merhaba de kullanabilirsiniz **tanılama** sekmesini tootest hello bağlantı tooan şirket içi veri kaynağı hello ağ geçidini kullanma.

    ![Ayrıntılı günlük kaydını etkinleştir](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Bu, Azure Machine learning'de hello ağ geçidi Kurulum işlemi tamamlar.
Şirket içi verilerinizi şimdi hazır toouse demektir.

Oluşturun ve her çalışma alanı için birden çok ağ geçidi Studio'da ayarlayın. Örneğin, tooconnect tooyour test veri kaynakları geliştirme ve farklı bir ağ geçidi sırasında üretim veri kaynaklarınız için istediğiniz bir ağ geçidi olabilir. Azure Machine Learning Şirket ortamınıza bağlı olarak birden çok ağ geçidi yukarı esneklik tooset sağlar. Şu anda çalışma alanları arasında bir ağ geçidi paylaşamaz ve yalnızca bir ağ geçidi tek bir bilgisayara yüklenebilir. Daha fazla bilgi için bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>2. adım: hello ağ geçidi tooread veri bir şirket içi veri kaynağından kullanın.
Merhaba ağ geçidi kurun ayarladıktan sonra ekleyebileceğiniz bir **veri içeri aktarma** hello şirket içi SQL Server veritabanındaki hello verileri girdi bir denemeyi modülüne.

1. Machine Learning Studio'da hello seçin **DENEMELER** sekmesini tıklatın, **+ yeni** hello sol alt köşesinde ve seçin **boş deneme** (veya birkaç örnek birini seçin denemeler kullanılabilir).
2. Bulma ve hello sürükleyin **veri içeri aktarma** modülü toohello deneme tuvaline.
3. Tıklatın **Farklı Kaydet** hello tuvale aşağıda. "Azure Machine Learning şirket içi SQL Server Öğreticisi" Merhaba deneme adı, çalışma alanını seçin ve hello tıklatın **Tamam** onay işareti.

   ![Deneme Yeni adla kaydet](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Hello tıklatın **veri içeri aktarma** modülü tooselect, sonra **özellikleri** hello bölmesini toohello hello tuvalin sağındaki seçin "Şirket içi SQL veritabanı" **veri kaynağı** aşağı açılan liste.
5. Select hello **veri ağ geçidi** yüklü ve kayıtlı. Başka bir ağ geçidi kurun "(yeni veri ağ geçidi Ekle...)"'i seçerek ayarlayabilirsiniz.

   ![Veri içeri aktarma modülü için veri ağ geçidi seçin](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Merhaba SQL girin **veritabanı sunucusu adı** ve **veritabanı adı**, hello SQL birlikte **veritabanı sorgusu** tooexecute istiyor.
7. Tıklatın **değerleri girin** altında **kullanıcı adı ve parola** ve veritabanı kimlik bilgilerinizi girin. Windows tümleşik kimlik doğrulaması veya SQL Server şirket içi SQL Server'ınızdaki nasıl yapılandırıldığına bağlı olarak kimlik doğrulaması kullanabilirsiniz.

   ![Veritabanı kimlik bilgilerini girin](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   "gerekli değerler" değişiklikleri çok "değerleri kümesi" Yeşil bir onay işareti ile Merhaba iletisi. Merhaba veritabanı bilgileri veya parola değiştirilmediği sürece yalnızca tooenter hello kimlik bilgilerini bir kez gerekir. Azure Machine Learning hello bulutta hello ağ geçidi tooencrypt hello kimlik yüklendiğinde, sağlanan hello sertifika kullanır. Azure hiçbir zaman şifreleme olmadan şirket içi kimlik bilgilerini depolar.

   ![Veri modülü özelliklerini alma](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Tıklatın **çalıştırmak** toorun hello deneme.

Merhaba deneme çalışması bittikten sonra hello hello çıkış bağlantı noktasına tıklayarak hello veritabanından alınan hello verileri görselleştirebilirsiniz **veri içeri aktarma** modülü ve seçerek **Görselleştir**.

Denemenizi geliştirme tamamladıktan sonra dağıtın ve modelinizi faaliyete. Merhaba toplu yürütme hizmeti, hello yapılandırılmış hello şirket içi SQL Server veritabanındaki verileri kullanarak **veri içeri aktar** modülü okuma ve puanlama için kullanılır. Puanlama veri şirket için hello istek yanıtı hizmeti kullanabilirsiniz, ancak Microsoft önerir kullanarak [Excel eklentisi](machine-learning-excel-add-in-for-web-services.md) yerine. Şu anda tooan yazma şirket içi SQL Server veritabanına yoluyla **verileri dışa aktar** denemelerinizi içinde ya da desteklenen veya yayımlanmış web hizmetleri değil.
