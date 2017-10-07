---
title: "bir SQL Server sanal makineyi IPython dizüstü sunucusu olarak aaaSet | Microsoft Docs"
description: "Yukarı veri bilimi sahip bir sanal makine SQL Server ve IPython Server ayarlayın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Gelişmiş analiz için Azure SQL Server sanal makinesini IPython Not Defteri olarak ayarlama
Bu konuda gösterilmektedir nasıl tooprovision ve bulut tabanlı veri bilimi ortamının bir parçası kullanılan bir SQL Server sanal makine toobe yapılandırın. Hello Windows sanal makine IPython Not Defteri, Azure Storage Gezgini ve AzCopy yanı sıra veri bilimi projeleri için yararlı olan diğer yardımcı programları gibi araçları destekleme ile yapılandırılır. Azure Depolama Gezgini ve AzCopy, örneğin, sağlayan uygun şekilde tooupload veri tooAzure blob depolama nızdan yerel makine veya toodownload, blob depolama biriminden tooyour yerel makine.

Hello Azure sanal makineye Galerisi, Microsoft SQL Server içeren birkaç görüntüyü içerir. Veri ihtiyaçlarınıza uygun olan bir SQL Server VM görüntüsünü seçin. Önerilen görüntüleri şunlardır:

* SQL Server 2012 SP2 Enterprise küçük toomedium veri boyutları için
* SQL Server 2012 SP2 Enterprise en iyi duruma getirilmiş büyük toovery büyük veri boyutları için DataWarehousing iş yükleri için
  
  > [!NOTE]
  > SQL Server 2012 SP2 Enterprise görüntü **bir veri diski içermez**. Siz tooadd gerekir veya bir veya daha fazla sanal sabit diskler toostore verilerinizi ekleyin. Bir Azure sanal makine oluşturduğunuzda, hello işletim sistemi eşlenen toohello C sürücüsü için bir disk ve bir geçici disk eşlenen toohello D sürücüsü vardır. Merhaba D sürücü toostore veri kullanmayın. Merhaba adından da anlaşılacağı gibi yalnızca geçici depolama sağlar. Azure depolama alanında bulunan değil çünkü hiçbir artıklık veya yedekleme sunar.
  > 
  > 

## <a name="Provision"></a>Klasik Azure portalı toohello bağlanmak ve SQL Server sanal makine sağlama
1. İçinde toohello oturum [Klasik Azure portalında](http://manage.windowsazure.com/) hesabınızı kullanarak.
   Bir Azure hesabınız yoksa, [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)yi ziyaret edin.
2. Merhaba Klasik Azure portalında, hello hello web sayfasının sol alt tıklayın **+ yeni**, tıklatın **işlem**, tıklatın **sanal makine**ve ardından **FROM GALERİ**.
3. Merhaba üzerinde **bir sanal makine oluşturmak** sayfasında, SQL Server verileri gereksinimlerinize göre içeren bir sanal makine görüntüsü seçin ve ardından hello sayfasının sağ alt hello İleri okuna tıklayın. Azure üzerinde SQL Server görüntülerinin Hello en güncel bilgileri hello üzerinde desteklenen için bkz: [Azure Virtual Machines'de SQL Server ile çalışmaya başlama](http://go.microsoft.com/fwlink/p/?LinkId=294720) hello konudaki [Azure Virtual Machines'de SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294719) Belge ayarlayın.
   
   ![SQL Server VM seçin][1]
4. Merhaba üzerinde ilk **sanal makine yapılandırması** sayfasında, aşağıdaki bilgileri sağlayın:
   
   * Sağlayan bir **sanal makine adı**.
   * Merhaba, **yeni bir kullanıcı adı** kutusu, hello VM yerel yönetici hesabının benzersiz kullanıcı adını yazın.
   * Merhaba, **yeni parola** güçlü bir parola yazın. Daha fazla bilgi için bkz. [Güçlü Parolalar](http://msdn.microsoft.com/library/ms161962.aspx).
   * Merhaba, **PAROLAYI Onayla** kutusunda, hello parolayı yeniden yazın.
   * Select hello uygun **BOYUTU** hello listede aşağı doğru bırak.
     
     > [!NOTE]
     > Merhaba boyutunu hello sanal makine sağlama sırasında belirtilir: A2 olduğunu hello en küçük boyuta üretim iş yükleri için önerilir. Bir sanal makine için önerilen en düşük boyut A3 SQL Server Enterprise Edition kullanıldığında. A3 seçin ya da SQL Server Enterprise Edition kullanırken daha yüksek. SQL Server 2012 veya 2014 Enterprise en iyi duruma getirilmiş işlem iş yüklerinin görüntülerde kullanırken a4 seçin.
     > A7 SQL Server 2012 veya 2014 Enterprise en iyi duruma getirilmiş veri ambarı iş yüklerini görüntüler için kullanırken seçin. Seçilen hello boyutu yapılandırabileceğiniz veri diskleri sayısını sınırlar. Tooa sanal makine iliştirebilirsiniz kullanılabilir sanal makine boyutlarını ve hello veri diski sayısı en güncel bilgiler için bkz [Azure için sanal makine boyutlarını](http://msdn.microsoft.com/library/azure/dn197896.aspx). Fiyatlandırma bilgileri için bkz: [sanal Macines fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Merhaba alt sağ toocontinue Hello İleri okuna tıklayın.
   
   ![VM yapılandırması][2]
5. Merhaba üzerinde ikinci **sanal makine yapılandırması** sayfasında, ağ, depolama ve kullanılabilirlik için kaynakları yapılandırın:
   
   * Merhaba, **bulut hizmeti** kutusunda, seçin **yeni bir bulut hizmeti oluşturma**.
   * Merhaba, **bulut hizmeti DNS adı** kutusunda, böylece bir adı biçiminde tamamlandıktan hello ilk bölümü tercih ettiğiniz bir DNS adı sağlayın **TESTNAME.cloudapp.net**
   * Merhaba, **bölge/BENZEŞİM grubu/sanal ağ** kutusunda, bu sanal görüntü nerede barındırılacağı bir bölge seçin.
   * Merhaba, **depolama hesabı**, mevcut bir depolama hesabını seçin veya otomatik olarak oluşturulan bir tanesini seçin.
   * Merhaba, **kullanılabilirlik KÜMESİ** kutusunda **(hiçbiri)**.
   * Okuyun ve fiyatlandırma bilgileri hello kabul edin.
6. Merhaba, **uç noktaları** bölümünde, hello boş açılır altında tıklatın **adı**seçip **MSSQL** hello veritabanı altyapısı (örneğininbaşlangıçbağlantınoktasınumarasınıyazın**1433** hello varsayılan örnek için).
7. SQL Server VM'nize Ayrıca, bir sonraki adımda yapılandırılmış bir IPython not defteri sunucusu olarak hizmet verebilir.
   Bir yeni uç nokta toospecify hello bağlantı noktası toouse IPython dizüstü bilgisayar sunucunuz için ekleyin. Hello bir ad girin **adı** sütun, tercih ettiğiniz hello genel bağlantı noktası için bağlantı noktası numarasını seçin ve 9999 hello özel bağlantı noktası için.
   
   Merhaba alt sağ toocontinue Hello İleri okuna tıklayın.
   
   ![MSSQL ve IPython bağlantı noktalarını seçin][3]
8. Merhaba varsayılanı kabul **yükleme VM Aracısı** seçeneği denetlenir ve hello hello hello hello Sihirbazı toocomplete hello VM sağlama işlemi, sayfanın sağ alt köşesindeki onay işaretine tıklayın.
   
   `![VM son seçenekleri][4]
9. Azure sanal makineniz hazırlanırken bekleyin. Merhaba sanal makine durumu tooproceed aracılığıyla bekler:
   
   * (Kaynak sağlama) başlatılıyor
   * Durduruldu
   * (Kaynak sağlama) başlatılıyor
   * Çalıştıran (hazırlama)
   * Çalışıyor

## <a name="RemoteDesktop"></a>Uzak Masaüstü ve Kurulumu tamamlamak kullanarak Hello sanal makine açın
1. Sağlama tamamlandıktan sonra sanal makine toogo toohello PANO sayfası hello adına tıklayın. Merhaba sayfasının Hello altında tıklatın **Bağlan**.
2. Merhaba Windows Uzak Masaüstü programını kullanarak tooopen hello rpd dosyasını seçin (`%windir%\system32\mstsc.exe`).
3. Merhaba, **Windows Güvenliği** iletişim kutusunda, bir önceki adımda belirtilen yerel yönetici hesabı için hello parola sağlayın.
   (Bunu hello sanal makinenin tooverify hello kimlik bilgileri istenebilir.)
4. Merhaba ilk kez toothis sanal makinede oturum çeşitli işlemler Masaüstü, Windows güncelleştirmelerini ve hello Windows ilk yapılandırma görevleri (sysprep) tamamlanmasından Kurulumu dahil olmak üzere toocomplete gerekebilir. Windows sysprep tamamlandıktan sonra SQL Server kurulum yapılandırma görevleri tamamlar. Bunlar tamamlarken bu görevler birkaç dakikalık bir gecikme neden olabilir. `SELECT @@SERVERNAME`Merhaba doğru adı, SQL Server Kurulum tamamlandıktan ve SQL Server Management Studio hello başlangıç sayfasında visable olmayabilir kadar döndürmeyebilir.

Windows Uzak Masaüstü ile bağlı toohello sanal makine olduktan sonra hello sanal makine çok herhangi bir bilgisayar gibi çalışır. Hello toohello varsayılan (Merhaba sanal makinede çalışan) SQL Server Management Studio ile SQL Server örneğine bağlanmak normal şekilde.

## <a name="InstallIPython"></a>IPython dizüstü bilgisayar ve diğer destek araçlarını yükleme
tooconfigure bir IPython dizüstü sunucu ve yükleme ek destekleyen yeni, SQL Server VM tooserve böyle AzCopy, Azure Storage Gezgini, yararlı veri bilimi Python paketlerini ve diğer araçları, özel özelleştirme betik tooyou sağlanır. tooinstall:

1. Sağ hello **Windows Başlat** simgesi ve tıklatın **komut istemi (Yönetici)**
2. Aşağıdaki komutları hello kopyalayıp hello komut isteminde yapıştırın.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. İstendiğinde, tercih ettiğiniz bir parola Merhaba IPython dizüstü sunucusu girin.
4. Merhaba özelleştirme betik dahil birkaç yükleme sonrası yordamları otomatik hale getirir:
    * Yükleme ve Kurulum IPython not defteri sunucusu
    * Merhaba Windows Güvenlik Duvarı'nda daha önce oluşturduğunuz hello uç noktalar için TCP bağlantı noktaları açma:
    * Uzak SQL Server bağlantısı için
    * IPython dizüstü server uzak bağlantı için
    * Örnek IPython Not defterlerinin ve SQL komut dosyaları getirme
    * İndirme ve yararlı veri bilimi Python paketlerini yükleme
    * Karşıdan yükleme ve AzCopy ve Azure Storage Gezgini gibi Azure araçlarını yükleme  
    <br>
5. Erişim ve IPython dizüstü hello form URL'sini kullanarak herhangi yerel veya uzak bir tarayıcıdan çalıştırın `https://<virtual_machine_DNS_name>:<port>`, bağlantı noktası hello sanal makine sağlanırken seçtiğiniz hello IPython genel bağlantı noktası olduğu.
6. IPython not defteri sunucusu arka plan hizmetinin çalıştığından ve hello sanal makine yeniden başlatıldığında otomatik olarak yeniden başlatılacak.

## <a name="Optional"></a>Gerektiğinde veri diski Ekle
VM görüntüsü veri diski, yani, diskleri C sürücüsünde (işletim sistemi diski) ve (geçici disk), D sürücüsündeki dışında içermiyorsa verilerinizi toostore daha fazla veri diskleri veya tooadd biri gerekir. Merhaba VM görüntüsü SQL Server 2012 SP2 Enterprise en iyi duruma getirilmiş DataWarehousing iş yükleri için SQL Server veri ve günlük dosyaları için ek disklerle önceden yapılandırılmış olarak gelir.

> [!NOTE]
> Merhaba D sürücü toostore veri kullanmayın. Merhaba adından da anlaşılacağı gibi yalnızca geçici depolama sağlar. Azure depolama alanında bulunan değil çünkü hiçbir artıklık veya yedekleme sunar.
> 
> 

tooattach ek veri disklerinin açıklanan başlangıç adımları izleyin [nasıl tooAttach veri diski tooa Windows sanal makine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), hangi kılavuzluk eder aracılığıyla:

1. Önceki adımlarda sağlanan boş diskler toohello sanal makine ekleme
2. Merhaba yeni diskler hello sanal makinede başlatma

## <a name="SSMS"></a>TooSQL Server Management Studio bağlanmak ve karma mod kimlik doğrulamasını etkinleştir
Merhaba SQL Server veritabanı altyapısı etki alanı ortamında Windows kimlik doğrulamasını kullanamazsınız. başka bir bilgisayardan tooconnect toohello veritabanı altyapısının SQL Server karışık mod kimlik doğrulaması için yapılandırın. Karma mod kimlik doğrulaması hem SQL Server Kimlik Doğrulaması’na hem de Windows Kimlik Doğrulaması’na izin verir. SQL kimlik doğrulama modu, SQL Server VM veritabanlarınızı sipariş tooingest verileri doğrudan gereklidir [Azure Machine Learning Studio](https://studio.azureml.net) hello veri içeri aktarma modülü kullanma.

1. Bağlı toohello sanal Uzak Masaüstü kullanarak makineyi, Windows hello kullan **arama** bölmesinde ve türü **SQL Server Management Studio** (SMSS). Toostart hello SQL Server Management Studio (SSMS) tıklayın. Gelecekte kullanılmak üzere masaüstünüzde tooadd kısayol tooSSMS isteyebilirsiniz.
   
   ![SSMS Başlat][5]
   
   Merhaba ilk kez hello kullanıcılar Management Studio ortam oluşturmalısınız Management Studio'yu açın. Bu birkaç dakika sürebilir.
2. Açarken Management Studio hello sunar **tooServer bağlanmak** iletişim kutusu. Merhaba, **sunucu adı** kutusu, hello Nesne Gezgini ile Merhaba sanal makine tooconnect toohello veritabanı altyapısı tür hello adı.
   (Merhaba sanal makine adı yerine de kullanabilirsiniz **(yerel)** veya hello olarak tek bir nokta **sunucu adı**. Seçin **Windows kimlik doğrulaması**, bırakıp  ***,\_VM\_adı*\\,\_yerel\_yönetici**  hello içinde **kullanıcı adı** kutusu. **Bağlan**'a tıklayın.
   
   ![TooServer Bağlan][6]
   
   <br>
   
   > [!TIP]
   > Windows kayıt defteri anahtarı değişiklik veya hello SQL Server Management Studio'yu kullanarak SQL Server kimlik doğrulama modu hello değişebilir. toochange kimlik doğrulama modu Hello kayıt defteri anahtarı değişiklik, başlangıç kullanarak bir **yeni sorgu** ve komut dosyası izleyen hello yürütün:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    SQL Server management Studio kullanılarak toochange hello kimlik doğrulama modu:

1. İçinde **SQL Server Management Studio Object Explorer**, SQL Server (Merhaba sanal makine adı) hello örneğinin adını sağ tıklatın ve ardından **özellikleri**.
   
   ![Sunucu Özellikleri][7]
2. Merhaba üzerinde **güvenlik** sayfasında **sunucu kimlik doğrulaması**seçin **SQL Server ve Windows kimlik doğrulaması modu**ve ardından **Tamam** .
   
   ![Kimlik Doğrulaması Modunu Seçme][8]
3. Merhaba, **SQL Server Management Studio** iletişim kutusu, tıklatın **Tamam** hello gereksinim toorestart SQL Server onaylamak için.
4. İçinde **Object Explorer**, sunucunuzu sağ tıklatın ve ardından **yeniden**. (SQL Server Agent çalışıyorsa, onun da yeniden başlatılması gerekir.)
   
   ![Yeniden Başlatma][9]
5. Merhaba, **SQL Server Management Studio** iletişim kutusu, tıklatın **Evet** toorestart SQL Server istediğiniz kabul edin.

## <a name="Logins"></a>SQL Server kimlik doğrulama oturumları oluşturma
başka bir bilgisayardan tooconnect toohello veritabanı altyapısı, en az bir SQL Server kimlik doğrulaması oturum açma oluşturmanız gerekir.  

Yeni SQL Server oturumları program aracılığıyla oluşturabilir veya hello SQL Server Management Studio'yu kullanarak. SQL kimlik doğrulaması ile yeni bir sysadmin kullanıcı programlı olarak Başlat toocreate bir **yeni sorgu** ve komut dosyası izleyen hello yürütün. Değiştir < yeni bir kullanıcı adı\> ve < yeni parola\> seçiminizi ile *kullanıcı adı* ve *parola*. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Merhaba parola ilkesi gerektiği gibi ayarlayın (hello örnek kod ilke denetimi ve parola süre sonu devre dışı bırakır). SQL Server oturum açma kimlikleri hakkında daha fazla bilgi için bkz. [Oturum Açma Kimliği Oluşturma](http://msdn.microsoft.com/library/aa337562.aspx).  

Merhaba SQL Server Management Studio'yu kullanarak toocreate yeni SQL Server oturum açma sayısı:

1. İçinde **SQL Server Management Studio Object Explorer**, toocreate hello yeni oturum açma istediğiniz hello sunucu örneğinin hello klasörünü genişletin.
2. Sağ hello **güvenlik** klasörü, çok noktası**yeni**seçip **oturum açma...** .
   
   ![Yeni Oturum Açma Kimliği][10]
3. Merhaba, **yeni oturum açma -** iletişim kutusunda, hello **genel** sayfasında, hello hello hello yeni kullanıcı adını girin **oturum açma adı** kutusu.
4. **SQL Server kimlik doğrulaması**’nı seçin.
5. Merhaba, **parola** kutusunda, hello yeni kullanıcı için bir parola girin. Merhaba bu parolayı yeniden girin **parolayı onayla** kutusu.
6. karmaşıklık ve zorlama, tooenforce parola ilkesi seçeneklerini seçin **Şifre politikasını** (önerilen). Bu, SQL Server kimlik doğrulaması seçildiğinde bir varsayılan seçenektir.
7. tooenforce parola süre sonu ilkesi seçeneklerini seçin **parola süre sonu zorunlu** (önerilen). Şifre politikasını bu onay kutusunun seçili tooenable olması gerekir. Bu, SQL Server kimlik doğrulaması seçildiğinde bir varsayılan seçenektir.
8. Yeni bir parola Hello ilk kez sonra oturum açma kullanılır, tooforce hello kullanıcı toocreate seçin **kullanıcı bir sonraki oturum açışında parolasını değiştirmeniz** (Bu oturum açma birisi için başka toouse olup olmadığını önerilir. Merhaba oturum açma kendi kullanımınız için ise, bu seçeneği seçmeyin.) Parola geçerlilik süresi zorunlu bu onay kutusunun seçili tooenable olması gerekir. Bu, SQL Server kimlik doğrulaması seçildiğinde bir varsayılan seçenektir.
9. Merhaba gelen **varsayılan veritabanı** listesinde, hello oturum açma için varsayılan bir veritabanı seçin. **Ana** hello bu seçenek varsayılandır. Bir kullanıcı veritabanı henüz oluşturmadıysanız, bu çok ayarlamak bırakın**ana**.
10. Merhaba, **varsayılan dil** listesinde, bırakın **varsayılan** hello değeri olarak.
    
    ![Oturum Açma Özellikleri][11]
11. Oluşturmakta olduğunuz hello ilk oturum açma varsa, bu oturum açma bir SQL Server yöneticisi olarak belirtmek isteyebilirsiniz. Bunu yapmak istiyorsanız, **Sunucu Rolleri** sayfasında **sysadmin** öğesini işaretleyin.
    
    > [!IMPORTANT]
    > Merhaba sysadmin sabit sunucu rolünün üyeleri hello veritabanı altyapısı tam denetime sahiptir. Güvenlik nedeniyle, bu rol üyeliğini dikkatli bir biçimde kısıtlamalısınız.
    > 
    > 
    
    ![sysadmin][12]
12. Tamam'a tıklayın.

## <a name="DNS"></a>Merhaba DNS hello sanal makinenin adını belirleme
başka bir bilgisayardan tooconnect toohello SQL Server veritabanı altyapısı, hello etki alanı adı sistemi (DNS) bilmeniz gerekir hello sanal makine adı.

(Merhaba adı hello Internet kullanır tooidentify hello sanal makine bulunuyor. Başlangıç IP adresi kullanabilirsiniz, ancak Azure artıklık veya bakım için kaynaklar taşındığında hello IP adresi değişebilir. Bu olabilir çünkü Hello DNS adı kararlı olacaktır tooa yeni IP adresini yeniden yönlendirildi.)

1. Merhaba Klasik Azure portalı (veya hello önceki adımdaki), seçin **sanal makineleri**.
2. Merhaba üzerinde **sanal makine örnekleri** sayfasında hello **DNS adı** görünen hello sanal makine için hello DNS ad sütunu, bulma ve kopyalama öncesinde tarafından **http://**. (Merhaba kullanıcı arabirimi, adın tamamını hello görüntülemeyebilir, ancak üzerinde sağ tıklatın ve Kopyala'yı seçin.)

## <a name="cde"></a>Başka bir bilgisayardan toohello veritabanına bağlan
1. Bir bilgisayarda toohello bağlı Internet, SQL Server Management Studio'yu açın.
2. Merhaba, **tooServer bağlanmak** veya **tooDatabase altyapısı bağlanmak** iletişim kutusunda hello **sunucu adı** kutusunda, sanal makine (hello belirlenen hello DNS adını girin önceki görev) ve bir ortak uç nokta bağlantı noktası numarası hello biçiminde *DNSName, BağlantıNoktasıNumarası* gibi **tutorialtestVM.cloudapp.net,57500**.
3. Merhaba, **kimlik doğrulaması** kutusunda **SQL Server kimlik doğrulaması**.
4. Merhaba, **oturum açma** kutusu, bir önceki görevde oluşturduğunuz bir oturum açma türü hello adı.
5. Merhaba, **parola** kutusu, bir önceki görevde oluşturduğunuz hello oturum açma hello parolayı girin.
6. **Bağlan**'a tıklayın.

## <a name="amlconnect"></a>Azure Machine Learning toohello veritabanı altyapısı Bağlan
Merhaba takım veri bilimi işlemi sonraki aşamalarını hello kullanacağı [Azure Machine Learning Studio'da](https://studio.azureml.net) toobuild ve makine öğrenimi modellerini dağıtın. SQL Server VM veritabanlarınızı eğitim veya Puanlama, Azure Machine Learning doğrudan tooingest verileri hello kullan **veri içeri aktar** yeni bir modülde [Azure Machine Learning Studio](https://studio.azureml.net) deneyin. Bu konuda hello takım veri bilimi işlem kılavuzu bağlantıları üzerinden daha ayrıntılı ele alınmıştır. Giriş için bkz [Azure Machine Learning Studio nedir?](machine-learning-what-is-ml-studio.md).

1. Merhaba, **özellikleri** hello bölmesini [veri içeri aktarma modülü](https://msdn.microsoft.com/library/azure/dn905997.aspx)seçin **Azure SQL veritabanı** hello gelen **veri kaynağı** açılır liste.
2. Merhaba, **veritabanı sunucusu adı** metin kutusuna, girin`tcp:<DNS name of your virtual machine>,1433`
3. Hello Hello SQL kullanıcı adı girin **Server kullanıcı hesabı adı** metin kutusu.
4. Hello Hello sql kullanıcının parolasını girin **Server kullanıcı hesabı parolasını** metin kutusu.
   
   ![Azure Machine Learning Veri Al][13]

## <a name="shutdown"></a>Kapatma ve sanal makine kullanılmadığında serbest bırakma
Azure sanal makineler olarak fiyatlandırılır **yalnızca kullandıklarınız için ödeme**. değil yükleniyor tooensure sanal makineniz kullanmadığınızda faturalandırılır, toobe hello sahip **durduruldu (Deallocated)** durumu.

> [!NOTE]
> Merhaba sanal makinesi kapatılıyor (Windows güç seçenekleri kullanarak), içinde hello VM durduruldu ancak ayrılan kalır. tooensure değil ödeme, her zaman hello sanal makinelerden Durdur [Klasik Azure portalı](http://manage.windowsazure.com/). ShutdownRoleOperation "PostShutdownAction" eşittir ile çok çağırarak hello Powershell aracılığıyla VM durdurabilirsiniz "StoppedDeallocated".
> 
> 

tooshutdown ve hello sanal makine ayırması:

1. İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com/) hesabınızı kullanarak.  
2. Seçin **sanal makineleri** hello sol gezinti çubuğunda.
3. Sanal makineler Hello listesinde, sanal makine sonra gidin toohello hello adına tıklayın **PANO** sayfası.
4. Merhaba sayfasının Hello altında tıklatın **kapatma**.

![VM kapatma][15]

Merhaba sanal makine serbest ancak silinmez. Sanal makineniz hello Klasik Azure Portalı'ndan herhangi bir zamanda yeniden başlatılabilir.

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>Azure SQL Server VM'nize hazır toouse olduğu: sonraki nedir?
Sanal makineniz hazır toouse veri bilimi alıştırmaları içinde sunulmuştur. Hello sanal makine de hello takım veri bilimi işlem (TDSP) ve Azure Machine Learning ile Merhaba araştırması ve veri işleme için bir IPython dizüstü sunucusu ve diğer görevleri birlikte kullanım için hazırdır.

Merhaba hello veri bilimi işlemindeki sonraki adımlar hello eşlenen [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve Hdınsight'a, işlem verilerini taşımak ve Azure makineyle var. Bu örnek hello verilerden öğrenmeyi için hazırlık adımları içerebilir Öğrenme.

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

