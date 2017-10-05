---
title: "SQL Server sanal makine bir IPython dizüstü sunucusu olarak ayarlama | Microsoft Docs"
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
ms.openlocfilehash: 8a151a6a15d4d000a774e3ec4e38bfa0e58ca33b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Gelişmiş analiz için Azure SQL Server sanal makinesini IPython Not Defteri olarak ayarlama
Bu konu, sağlamak ve bir bulut tabanlı veri bilimi ortamının bir parçası kullanılacak bir SQL Server sanal makine yapılandırma gösterilmektedir. Windows sanal makine IPython Not Defteri, Azure Storage Gezgini ve AzCopy yanı sıra veri bilimi projeleri için yararlı olan diğer yardımcı programları gibi araçları destekleme ile yapılandırılır. Örneğin, Azure Depolama Gezgini ve AzCopy, verileri Azure blob depolama alanına yerel makinenizden karşıya yüklemek veya bir blob depolama alanından yerel makinenize indirmek için uygun şekilde girin.

Azure sanal makineye Galerisi, Microsoft SQL Server içeren birkaç görüntüyü içerir. Veri ihtiyaçlarınıza uygun olan bir SQL Server VM görüntüsünü seçin. Önerilen görüntüleri şunlardır:

* SQL Server 2012 SP2 Enterprise küçük ve orta veri boyutları için
* SQL Server 2012 SP2 Enterprise en iyi duruma getirilmiş DataWarehousing iş yükleri için çok büyük veri boyutları için
  
  > [!NOTE]
  > SQL Server 2012 SP2 Enterprise görüntü **bir veri diski içermez**. Ekleme ve/veya bir veya daha fazla sanal sabit verilerinizi depolamak için disk ekleme gerekecektir. Bir Azure sanal makine oluşturduğunuzda, C sürücüsünün eşlenen işletim sistemi için bir disk ve D sürücüsüne eşlenen geçici bir disk vardır. D sürücüsündeki verileri depolamak için kullanmayın. Adından da anlaşılacağı gibi yalnızca geçici depolama sağlar. Azure depolama alanında bulunan değil çünkü hiçbir artıklık veya yedekleme sunar.
  > 
  > 

## <a name="Provision"></a>Azure Klasik Portalı'na bağlanmak ve SQL Server sanal makine sağlama
1. Oturum [Klasik Azure portalında](http://manage.windowsazure.com/) hesabınızı kullanarak.
   Bir Azure hesabınız yoksa, [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)yi ziyaret edin.
2. Klasik Azure portalında web sayfasının sol alt tıklayın **+ yeni**, tıklatın **işlem**, tıklatın **sanal makine**ve ardından **FROM Galerisi** .
3. Üzerinde **bir sanal makine oluşturmak** sayfasında, verileri gereksinimlerinize göre SQL Server içeren bir sanal makine görüntüsü seçin ve ardından sayfanın sağ alt İleri okuna tıklayın. Desteklenen SQL Server görüntülerinde Azure ile ilgili en güncel bilgiler için bkz: [Azure Virtual Machines'de SQL Server ile çalışmaya başlama](http://go.microsoft.com/fwlink/p/?LinkId=294720) konuda [Azure Virtual Machines'de SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294719) Belge ayarlayın.
   
   ![SQL Server VM seçin][1]
4. İlk **sanal makine yapılandırması** sayfasında, aşağıdaki bilgileri sağlayın:
   
   * Sağlayan bir **sanal makine adı**.
   * İçinde **yeni bir kullanıcı adı** kutusu, VM yerel yönetici hesabının benzersiz kullanıcı adını yazın.
   * İçinde **yeni parola** güçlü bir parola yazın. Daha fazla bilgi için bkz. [Güçlü Parolalar](http://msdn.microsoft.com/library/ms161962.aspx).
   * İçinde **PAROLAYI Onayla** kutusunda, parolayı yeniden yazın.
   * Uygun seçin **BOYUTU** açılır listeden.
     
     > [!NOTE]
     > Sağlama işlemi sırasında belirtilen sanal makine boyutu: A2 üretim iş yükleri için önerilen en küçük boyutudur. Bir sanal makine için önerilen en düşük boyut A3 SQL Server Enterprise Edition kullanıldığında. A3 seçin ya da SQL Server Enterprise Edition kullanırken daha yüksek. SQL Server 2012 veya 2014 Enterprise en iyi duruma getirilmiş işlem iş yüklerinin görüntülerde kullanırken a4 seçin.
     > A7 SQL Server 2012 veya 2014 Enterprise en iyi duruma getirilmiş veri ambarı iş yüklerini görüntüler için kullanırken seçin. Seçilen boyutuna yapılandırabileceğiniz veri diskleri sayısını sınırlar. Kullanılabilir sanal makine boyutlarını ve bir sanal makineye İliştir veri diski sayısı en güncel bilgiler için bkz: [Azure için sanal makine boyutlarını](http://msdn.microsoft.com/library/azure/dn197896.aspx). Fiyatlandırma bilgileri için bkz: [sanal Macines fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Devam etmek için alt köşedeki İleri okuna tıklayın.
   
   ![VM yapılandırması][2]
5. İkinci **sanal makine yapılandırması** sayfasında, ağ, depolama ve kullanılabilirlik için kaynakları yapılandırın:
   
   * İçinde **bulut hizmeti** kutusunda, seçin **yeni bir bulut hizmeti oluşturma**.
   * İçinde **bulut hizmeti DNS adı** kutusunda, böylece bir adı biçiminde tamamlandıktan tercih ettiğiniz bir DNS adı'nın ilk kısmı sağlayın **TESTNAME.cloudapp.net**
   * İçinde **bölge/BENZEŞİM grubu/sanal ağ** kutusunda, bu sanal görüntü nerede barındırılacağı bir bölge seçin.
   * İçinde **depolama hesabı**, mevcut bir depolama hesabını seçin veya otomatik olarak oluşturulan bir tanesini seçin.
   * İçinde **kullanılabilirlik KÜMESİ** kutusunda **(hiçbiri)**.
   * Okuyun ve fiyatlandırma bilgileri kabul edin.
6. İçinde **uç noktaları** bölümünde, boş açılır altında tıklatın **adı**seçip **MSSQL** veritabanı altyapısı örneği bağlantı noktası numarasını yazın (**1433** varsayılan örnek için).
7. SQL Server VM'nize Ayrıca, bir sonraki adımda yapılandırılmış bir IPython not defteri sunucusu olarak hizmet verebilir.
   IPython dizüstü bilgisayar sunucunuz için kullanılacak bağlantı noktasını belirtmek için yeni bir uç noktası ekleyin. Bir ad girin **adı** sütun, genel bağlantı noktası için tercih ettiğiniz bir bağlantı noktası numarasını seçin ve özel bağlantı noktası için 9999.
   
   Devam etmek için alt köşedeki İleri okuna tıklayın.
   
   ![MSSQL ve IPython bağlantı noktalarını seçin][3]
8. Varsayılanı kabul **yükleme VM Aracısı** işaretli seçeneğini ve tıklayın VM sağlama işlemini tamamlamak için sihirbazın sağ alt köşesindeki onay işaretine.
   
   `![VM son seçenekleri][4]
9. Azure sanal makineniz hazırlanırken bekleyin. İle devam etmek için sanal makine durumu bekler:
   
   * (Kaynak sağlama) başlatılıyor
   * Durduruldu
   * (Kaynak sağlama) başlatılıyor
   * Çalıştıran (hazırlama)
   * Çalışıyor

## <a name="RemoteDesktop"></a>Uzak Masaüstü ve Kurulumu tamamlamak kullanarak sanal makineyi açın
1. Sağlama tamamlandıktan sonra PANO sayfasına gitmek için sanal makine adına tıklayın. Sayfanın alt kısmındaki tıklatın **Bağlan**.
2. Windows Uzak Masaüstü programını kullanarak rpd dosyayı açmaya seçin (`%windir%\system32\mstsc.exe`).
3. Konumundaki **Windows Güvenliği** iletişim kutusunda, bir önceki adımda belirtilen yerel yönetici hesabı için parola sağlayın.
   (, Sanal makinenin kimlik bilgilerini doğrulamak için istenebilir.)
4. Bu sanal makinede oturum açıp ilk kez çeşitli işlemler tamamlanması, masaüstü, Windows güncelleştirmelerinin ve Windows ilk yapılandırma görevleri (sysprep) tamamlanmasından Kurulum dahil olmak üzere gerekebilir. Windows sysprep tamamlandıktan sonra SQL Server kurulum yapılandırma görevleri tamamlar. Bunlar tamamlarken bu görevler birkaç dakikalık bir gecikme neden olabilir. `SELECT @@SERVERNAME`doğru adı, SQL Server Kurulum tamamlandıktan ve SQL Server Management Studio Başlangıç sayfasında visable olmayabilir kadar döndürmeyebilir.

Windows Uzak Masaüstü kullanarak sanal makineye bağlandıktan sonra sanal makine herhangi bir bilgisayara benzer çalışır. (Sanal makinede çalışan) SQL Server Management Studio ile SQL Server'ın varsayılan örnek normal şekilde bağlanın.

## <a name="InstallIPython"></a>IPython dizüstü bilgisayar ve diğer destek araçlarını yükleme
IPython not defteri sunucusu olarak hizmet ve böyle AzCopy, Azure Storage Gezgini, yararlı veri bilimi Python paketlerini ve diğer ek destek araçlarını yüklemek için yeni SQL Server VM yapılandırmak için bir özel özelleştirme betik olanak sağlanır. Yüklemek için:

1. Sağ **Windows Başlat** simgesi ve tıklatın **komut istemi (Yönetici)**
2. Aşağıdaki komutları kopyalayın ve komut isteminde yapıştırın.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. İstendiğinde, IPython dizüstü bilgisayar sunucusu için tercih ettiğiniz bir parola girin.
4. Özelleştirme betik dahil birkaç yükleme sonrası yordamları otomatik hale getirir:
    * Yükleme ve Kurulum IPython not defteri sunucusu
    * Daha önce oluşturduğunuz uç noktaları için Windows Güvenlik Duvarı'nda TCP bağlantı noktaları açma:
    * Uzak SQL Server bağlantısı için
    * IPython dizüstü server uzak bağlantı için
    * Örnek IPython Not defterlerinin ve SQL komut dosyaları getirme
    * İndirme ve yararlı veri bilimi Python paketlerini yükleme
    * Karşıdan yükleme ve AzCopy ve Azure Storage Gezgini gibi Azure araçlarını yükleme  
    <br>
5. Erişim ve bir URL biçiminde kullanarak herhangi yerel veya uzak bir tarayıcıdan IPython dizüstü çalıştırın `https://<virtual_machine_DNS_name>:<port>`, bağlantı noktası sanal makine sağlanırken seçtiğiniz IPython genel bağlantı noktası olduğu.
6. IPython not defteri sunucusu arka plan hizmetinin çalıştığından ve sanal makine yeniden başlatıldığında otomatik olarak yeniden başlatılacak.

## <a name="Optional"></a>Gerektiğinde veri diski Ekle
VM görüntüsü veri diski, yani, diskleri C sürücüsünde (işletim sistemi diski) ve (geçici disk), D sürücüsündeki dışında içermiyorsa verilerinizi depolamak için bir veya daha fazla veri diski eklemeniz gerekir. SQL Server 2012 SP2 Enterprise en iyi duruma getirilmiş DataWarehousing iş yükleri için VM görüntüsü için SQL Server veri ve günlük dosyaları ek disklerle önceden yapılandırılmış olarak gelir.

> [!NOTE]
> D sürücüsündeki verileri depolamak için kullanmayın. Adından da anlaşılacağı gibi yalnızca geçici depolama sağlar. Azure depolama alanında bulunan değil çünkü hiçbir artıklık veya yedekleme sunar.
> 
> 

Ek veri disklerinin eklemek için açıklanan adımları izleyin [bir Windows sanal makineye bir veri diski Ekle nasıl](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), hangi kılavuzluk eder aracılığıyla:

1. Önceki adımlarda sağlanan sanal makine için boş disklerin bağlanmasını
2. Sanal makinede yeni diskler başlatma

## <a name="SSMS"></a>SQL Server Management Studio'ya bağlanın ve karma mod kimlik doğrulamasını etkinleştir
SQL Server Veritabanı Altyapısı, etki alanı ortamı olmadan Windows Kimlik Doğrulaması’nı kullanamaz. Başka bir bilgisayardan Veritabanı Altyapısı’na bağlanmak için, SQL Server’ı karma mod kimlik doğrulamasıyla yapılandırın. Karma mod kimlik doğrulaması hem SQL Server Kimlik Doğrulaması’na hem de Windows Kimlik Doğrulaması’na izin verir. SQL kimlik doğrulama modu, SQL Server VM veritabanlarınızı doğrudan veri alma için gereklidir [Azure Machine Learning Studio](https://studio.azureml.net) veri içeri aktarma modülü kullanma.

1. Sanal makineye Uzak Masaüstü'nü kullanarak bağlıyken, Windows kullanma **arama** bölmesinde ve türü **SQL Server Management Studio** (SMSS). SQL Server Management Studio (SSMS) başlatmak için tıklatın. SSMS gelecekte kullanım için Masaüstünde kısayol eklemek isteyebilirsiniz.
   
   ![SSMS Başlat][5]
   
   İlk kez açtığınızda Management Studio’nun, kullanıcıların Management Studio ortamını oluşturması gerekir. Bu birkaç dakika sürebilir.
2. Management Studio açarken gösterir **sunucuya Bağlan** iletişim kutusu. İçinde **sunucu adı** Nesne Gezgini sahip veritabanı motoru bağlanmak için sanal makinenin adını yazın.
   (Sanal makine adı yerine de kullanabilirsiniz **(yerel)** veya tek bir nokta olarak **sunucu adı**. Seçin **Windows kimlik doğrulaması**, bırakıp  ***,\_VM\_adı*\\,\_yerel\_yönetici**  içinde **kullanıcı adı** kutusu. **Bağlan**'a tıklayın.
   
   ![Sunucuya bağlanma][6]
   
   <br>
   
   > [!TIP]
   > Windows kayıt defteri anahtarı değişiklik veya SQL Server Management Studio'yu kullanarak SQL Server kimlik doğrulama modu değişebilir. Kayıt defteri anahtarı değişiklik kullanarak kimlik doğrulaması modunu değiştirmek için başlangıç bir **yeni sorgu** ve aşağıdaki komut dosyasını çalıştırın:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    SQL Server management Studio kullanarak kimlik doğrulaması modunu değiştirmek için:

1. İçinde **SQL Server Management Studio Object Explorer**(sanal makine adı) SQL Server örneğinin adını sağ tıklatın ve ardından **özellikleri**.
   
   ![Sunucu Özellikleri][7]
2. **Güvenlik** sayfasındaki **Sunucu kimlik doğrulaması** bölümünde **SQL Server ve Windows Kimlik Doğrulaması modu**’nu seçin ve **Tamam**’a tıklayın.
   
   ![Kimlik Doğrulaması Modunu Seçme][8]
3. İçinde **SQL Server Management Studio** iletişim kutusu, tıklatın **Tamam** SQL Server'ı yeniden başlatmak için gereksinim bildiremedi.
4. İçinde **Object Explorer**, sunucunuzu sağ tıklatın ve ardından **yeniden**. (SQL Server Agent çalışıyorsa, onun da yeniden başlatılması gerekir.)
   
   ![Yeniden Başlatma][9]
5. İçinde **SQL Server Management Studio** iletişim kutusu, tıklatın **Evet** SQL Server'ı yeniden başlatmak istediğiniz kabul edin.

## <a name="Logins"></a>SQL Server kimlik doğrulama oturumları oluşturma
Başka bir bilgisayardan Veritabanı Altyapısı’na bağlanmak için, en az bir SQL Server kimlik doğrulaması oturum açma kimliği oluşturmalısınız.  

Yeni SQL Server oturumları program aracılığıyla oluşturabilir veya SQL Server Management Studio'yu kullanarak. SQL kimlik doğrulaması ile program aracılığıyla yeni bir sysadmin kullanıcı oluşturmak için başlangıç bir **yeni sorgu** ve aşağıdaki komut dosyasını çalıştırın. Değiştir < yeni bir kullanıcı adı\> ve < yeni parola\> seçiminizi ile *kullanıcı adı* ve *parola*. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Parola İlkesi (örnek kodu kapatır ilke denetimi ve parola süre sonu) gerektiği gibi ayarlayın. SQL Server oturum açma kimlikleri hakkında daha fazla bilgi için bkz. [Oturum Açma Kimliği Oluşturma](http://msdn.microsoft.com/library/aa337562.aspx).  

SQL Server Management Studio'yu kullanarak yeni SQL Server oturumları oluşturmak için:

1. İçinde **SQL Server Management Studio Object Explorer**, yeni oturum açma oluşturmak istediğiniz sunucu örneğinin klasörünü genişletin.
2. Sağ **güvenlik** klasörünü **yeni**seçip **oturum açma...** .
   
   ![Yeni Oturum Açma Kimliği][10]
3. **Oturum Açma - Yeni** iletişim kutusunun **Genel** sayfasında, **Oturum açma adı** kutusuna yeni kullanıcının adını girin.
4. **SQL Server kimlik doğrulaması**’nı seçin.
5. **Parola** kutusuna, yeni kullanıcı için bir parola girin. **Parolayı Onayla** kutusuna parolayı yeniden girin.
6. Parola İlkesi seçenekleri karmaşıklık ve zorlama için zorunlu kılmak için seçin **Şifre politikasını** (önerilen). Bu, SQL Server kimlik doğrulaması seçildiğinde bir varsayılan seçenektir.
7. Süre sonu için parola ilkesi seçenekleri zorunlu kılmak için seçin **parola süre sonu zorunlu** (önerilen). Zorunlu parola ilkesi, bu onay kutusunu etkinleştirmek için seçilmelidir. Bu, SQL Server kimlik doğrulaması seçildiğinde bir varsayılan seçenektir.
8. Kullanıcı ilk defa oturum açma kullanıldığında sonra yeni bir parola oluşturmak için zorlamayı seçin **kullanıcı bir sonraki oturum açışında parolasını değiştirmeniz** (Bu oturum açma kullanmak için başka birisi olup olmadığını önerilir. Oturum açma kendi kullanımınız için ise, bu seçeneği seçmeyin.) Zorunlu parola geçerlilik süresi, bu onay kutusunu etkinleştirmek için seçilmelidir. Bu, SQL Server kimlik doğrulaması seçildiğinde bir varsayılan seçenektir.
9. **Varsayılan veritabanı** listesinde, oturum açma kimliği için varsayılan veritabanını seçin. Bu seçeneği varsayılan değeri **asıl** veritabanıdır. Henüz bir kullanıcı veritabanı oluşturmadıysanız, bu ayarı **asıl** olarak bırakın.
10. İçinde **varsayılan dil** listesinde, bırakın **varsayılan** değeri olarak.
    
    ![Oturum Açma Özellikleri][11]
11. Bu oluşturduğunuz ilk oturum açma kimliğiyse, bu kimliği SQL Server yöneticisi olarak belirlemeniz yararlı olabilir. Bunu yapmak istiyorsanız, **Sunucu Rolleri** sayfasında **sysadmin** öğesini işaretleyin.
    
    > [!IMPORTANT]
    > Sysadmin sabit sunucu rolünün üyeleri, Veritabanı Altyapısı üzerinde tam denetime sahip olur. Güvenlik nedeniyle, bu rol üyeliğini dikkatli bir biçimde kısıtlamalısınız.
    > 
    > 
    
    ![sysadmin][12]
12. Tamam'a tıklayın.

## <a name="DNS"></a>Sanal makinenin DNS adını belirleme
Başka bir bilgisayardan SQL Server Veritabanı Altyapısı’na bağlanmak için, sanal makinenin Etki Alanı Adı Sistemi (DNS) adını biliyor olmalısınız.

(İnternet, sanal makineyi tanımlamak için bu adı kullanır. IP adresini kullanabilirsiniz, ancak Azure yedeklilik veya bakım nedeniyle kaynakları taşıdığında IP adresi değişebilir. DNS adı yeni IP adresine yeniden yönlendirilebileceği için değişmez.)

1. Azure Klasik Portalı'ndaki (ya da önceki adımdan) seçin **sanal makineleri**.
2. Üzerinde **sanal makine örnekleri** sayfasında **DNS adı** sütun, bulma ve görünen sanal makine için DNS ad öncesinde tarafından kopya **http://**. (Kullanıcı arabirimi, adın tamamını göstermeyebilir, ancak üzerinde sağ tıklatın ve Kopyala'yı seçin.)

## <a name="cde"></a>Başka bir bilgisayardan veritabanı altyapısına bağlanma
1. İnternet'e bağlı bir bilgisayarda SQL Server Management Studio’yu açın.
2. İçinde **sunucuya Bağlan** veya **veritabanı motoruna Bağlan** iletişim kutusunda **sunucu adı** kutusuna, (önceki görevde saptanmıştır) sanal makinenin DNS adını girin ve bir ortak uç nokta bağlantı noktası numarası biçiminde *DNSName, BağlantıNoktasıNumarası* gibi **tutorialtestVM.cloudapp.net,57500**.
3. **Kimlik Doğrulaması** kutusunda **SQL Server Kimlik Doğrulaması**’nı seçin.
4. **Oturum Açma** kutusuna, önceki görevlerden birinde oluşturduğunuz oturum açma kimliğinin adını yazın.
5. **Parola** kutusuna, önceki görevlerden birinde oluşturduğunuz oturum açma kimliğinin parolasını yazın.
6. **Bağlan**'a tıklayın.

## <a name="amlconnect"></a>Azure Machine Learning gelen veritabanı motoruna Bağlan
Takım veri bilimi işlemi sonraki aşamalarını kullanacağınız [Azure Machine Learning Studio'da](https://studio.azureml.net) oluşturmak ve makine öğrenimi modellerini dağıtmak için. Azure Machine Learning eğitim veya Puanlama için doğrudan, SQL Server VM veritabanlarından veri alma için kullanın **veri içeri aktar** yeni bir modülde [Azure Machine Learning Studio](https://studio.azureml.net) deneyin. Bu konu, takım veri bilimi işlem kılavuzu bağlantılar yoluyla daha ayrıntılı ele alınmıştır. Giriş için bkz [Azure Machine Learning Studio nedir?](machine-learning-what-is-ml-studio.md).

1. İçinde **özellikleri** bölmesinde [veri içeri aktarma modülü](https://msdn.microsoft.com/library/azure/dn905997.aspx)seçin **Azure SQL veritabanı** gelen **veri kaynağı** açılır liste.
2. İçinde **veritabanı sunucusu adı** metin kutusuna, girin`tcp:<DNS name of your virtual machine>,1433`
3. SQL kullanıcı adı girin **Server kullanıcı hesabı adı** metin kutusu.
4. Sql kullanıcının parolasını girin **Server kullanıcı hesabı parolasını** metin kutusu.
   
   ![Azure Machine Learning Veri Al][13]

## <a name="shutdown"></a>Kapatma ve sanal makine kullanılmadığında serbest bırakma
Azure sanal makineler olarak fiyatlandırılır **yalnızca kullandıklarınız için ödeme**. Sanal makinenize kullanmadığınızda ücretlendirilen değil emin olmak için onu olduğu sahip **durduruldu (Deallocated)** durumu.

> [!NOTE]
> Sanal makinesi kapatılıyor (Windows güç seçenekleri kullanarak içinde), VM durduruldu ancak ayrılan kalır. Değil faturalandırılır emin olmak için her zaman sanal makinelerden Durdur [Klasik Azure portalı](http://manage.windowsazure.com/). Sanal makineyi ayrıca PowerShell üzerinden "PostShutdownAction" eşittir "StoppedDeallocated" ile ShutdownRoleOperation'a çağrı yaparak da durdurabilirsiniz.
> 
> 

Kapatmak için ve sanal makine ayırması:

1. Oturum [Klasik Azure portalı](http://manage.windowsazure.com/) hesabınızı kullanarak.  
2. Seçin **sanal makineleri** sol gezinti çubuğunda.
3. Sanal makineler listesi, sanal makine adına tıklayın ardından Git **PANO** sayfası.
4. Sayfanın alt kısmındaki tıklatın **kapatma**.

![VM kapatma][15]

Sanal makine serbest ancak silinmez. Azure Klasik Portalı'ndan herhangi bir zamanda, sanal makine yeniden başlatılabilir.

## <a name="your-azure-sql-server-vm-is-ready-to-use-whats-next"></a>Azure SQL Server VM'nize kullanıma hazırdır: sonraki nedir?
Sanal makine artık veri bilimi alıştırmalarda kullanmak hazırdır. Sanal makine de Azure Machine Learning ve takım veri bilimi işlem (TDSP) ile araştırması ve veri ve diğer görevleri birlikte işlenmesini IPython dizüstü sunucusu olarak kullanıma hazırdır.

İçinde veri bilimi işlemi sonraki adımlarda eşlenen [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve Hdınsight'a, işlem verilerini taşımak ve bunu var. Azure Machine Learning ile verileri öğrenme hazırlığı örnek adımlarda içerebilir .

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

