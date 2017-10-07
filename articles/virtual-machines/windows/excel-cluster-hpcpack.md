---
title: "Excel ve SOA için aaaHPC paketi küme | Microsoft Docs"
description: "Büyük ölçekli Excel ve SOA iş yüklerini Azure HPC Pack kümede çalışan kullanmaya başlama"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Excel ve SOA iş yüklerini Azure HPC Pack kümede çalışan kullanmaya başlama
Bu makalede nasıl toodeploy Microsoft HPC Pack 2012 R2 küme Azure sanal makinelerde bir Azure Hızlı Başlangıç şablonu veya isteğe bağlı olarak bir Azure PowerShell dağıtım komut dosyası kullanarak gösterilmektedir. Merhaba küme Azure Market VM görüntüleri tasarlanmış toorun Microsoft Excel ya da hizmet odaklı mimari (SOA) iş yükleri ile HPC paketi kullanır. Merhaba küme toorun Excel HPC ve bir şirket içi istemci bilgisayarından SOA Hizmetleri'ni kullanabilirsiniz. Excel çalışma kitabı aktarma ve Excel kullanıcı tanımlı işlevler veya UDF'ler Hello Excel HPC hizmetleri içerir.

> [!IMPORTANT] 
> Bu makalede özellikleri, şablonları ve komut dosyaları HPC Pack 2012 R2 için temel alır. Bu senaryo HPC Pack 2016'şu anda desteklenmiyor.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Yüksek bir düzeyde hello Aşağıdaki diyagramda hello HPC paketi küme oluşturduğunuz gösterilmektedir.

![Excel iş yükleri çalıştıran düğümlerle HPC Kümesi][scenario]

## <a name="prerequisites"></a>Ön koşullar
* **İstemci bilgisayar** -bir Windows tabanlı bir istemci bilgisayar toosubmit örnek Excel ve SOA işleri toohello kümesi gerekir. (Bu dağıtım yöntemi seçerseniz) bir Windows bilgisayar toorun hello Azure PowerShell küme dağıtım betiğini de gerekir.
* **Azure aboneliği** -bir Azure aboneliğiniz yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.
* **Çekirdek kota** -özellikle çok çekirdekli VM boyutları birkaç küme düğümleri dağıtırsanız tooincrease hello kota çekirdek, gerekebilir. Hello çekirdek kota Kaynağı Yöneticisi'nde bir Azure Hızlı Başlangıç şablonu kullanıyorsanız, Azure bölgesidir. Bu durumda, belirli bir bölgedeki tooincrease hello kota gerekebilir. Bkz: [Azure aboneliği sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md). tooincrease bir kota [bir çevrimiçi müşteri destek isteği açma](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) herhangi bir ücret alınmaz.
* **Microsoft Office lisansı** - işlem düğümleri, Microsoft Excel ile bir Market HPC Pack 2012 R2 VM görüntüsü kullanarak Microsoft Excel Professional Plus 2013 30 günlük değerlendirme sürümü yüklüyse dağıtırsanız. Merhaba değerlendirme süresinden sonra tooprovide bir geçerli Microsoft Office lisansı tooactivate Excel toocontinue toorun iş yükleri gerekir. Bkz: [Excel etkinleştirme](#excel-activation) bu makalenin ilerisinde yer. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>1. Adım Azure HPC Pack kümede ayarlama
İki seçenek tooset hello HPC Pack 2012 R2 kümesi gösteriyoruz: ilk, bir Azure Hızlı Başlangıç şablonu ile hello Azure Portalı '; ve ikincisi, bir Azure PowerShell dağıtım komut dosyası kullanarak.

### <a name="option-1-use-a-quickstart-template"></a>Seçenek 1. Hızlı Başlatma şablonunu kullanma
Kullanım Azure Hızlı Başlangıç şablonu tooquickly hello Azure portal HPC Pack kümede dağıtın. Merhaba Portalı'nda hello şablonu açtığınızda hello ayarları, kümeniz için girdiğiniz basit bir kullanıcı Arabirimi alma. Merhaba adımlar şunlardır. 

> [!TIP]
> İsterseniz, kullanın bir [Azure Marketi şablonu](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) özellikle Excel iş yükleri için benzer bir küme oluşturur. Merhaba adımları hello aşağıdakiler arasından biraz farklılık gösterir.
> 
> 

1. Merhaba ziyaret [HPC küme oluşturma şablonu GitHub sayfasında](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). İsterseniz, hello şablon ve hello kaynak kodu hakkında bilgileri gözden geçirin.
2. Tıklatın **tooAzure dağıtmak** toostart hello şablon hello Azure portal ile bir dağıtımı.
   
   ![Şablon tooAzure dağıtma][github]
3. Merhaba Portalı'nda hello HPC küme şablon için bu adımları tooenter hello parametreleri izleyin.
   
   a. Merhaba üzerinde **parametreleri** sayfasında, girin veya hello şablon parametreleri için değerleri değiştirin. (Merhaba simgesi sonraki tooeach ayarı Yardım bilgileri için tıklatın.) Örnek değerler ekran aşağıdaki hello gösterilir. Bu örnek adlı bir küme oluşturur *hpc01* hello içinde *hpc.local* bir baş düğüm ve 2 oluşan etki alanı işlem düğümlerini. Merhaba işlem düğümleri, Microsoft Excel içeren bir HPC Pack VM görüntüden oluşturulur.
   
   ![Parametreleri girin][parameters-new-portal]
   
   > [!NOTE]
   > VM hello otomatik olarak oluşturulur hello baş düğüm [son Market görüntüsü](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) HPC paketi 2012 R2'in Windows Server 2012 R2. Şu anda hello görüntü HPC Pack 2012 R2 güncelleştirme 3 ' temel alır.
   > 
   > İşlem düğümü VM'ler hello son seçili hello işlem düğümü ailesi görüntüden oluşturulur. Select hello **ComputeNodeWithExcel** Microsoft Excel Professional Plus 2013'in değerlendirme sürümünü içeren hello son HPC Pack işlem düğümü görüntüsü seçeneği. toodeploy genel SOA oturumları veya Excel UDF aktarması, bir küme seçin hello **ComputeNode** (Excel yüklü olmadan) seçeneği.
   > 
   > 
   
   b. Merhaba abonelik seçin.
   
   c. Merhaba küme için bir kaynak grubu oluşturun *hpc01RG*.
   
   d. Orta ABD gibi hello kaynak grubu için bir konum seçin.
   
   e. Merhaba üzerinde **yasal koşulları** sayfasında, hello koşullarını gözden geçirin. Kabul ediyorsa **satın alma**. Merhaba şablonu için başlangıç değerlerini ayarlama işiniz bittiğinde, ardından **oluşturma**.
4. Merhaba dağıtım tamamlandığında (genellikle yaklaşık 30 dakika sürer), hello küme baş düğümünden export hello küme sertifika dosyası. Bir sonraki adımda hello istemci bilgisayar tooprovide hello sunucu tarafı kimlik doğrulaması için Güvenli HTTP bağlama üzerinde ortak bu sertifikayı içeri aktarın.
   
   a. Hello Azure portal, toohello Pano, select hello baş düğümüne gidin ve'ı tıklatın **Bağlan** Uzak Masaüstü kullanarak hello sayfa tooconnect hello üstünde.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Sertifika Yöneticisi tooexport hello baş düğümüne sertifika (Cert: \LocalMachine\My altında bulunur) standart yordamları hello özel anahtar olmadan kullanın. Bu örnekte, verme *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Merhaba sertifikasını dışarı aktarma][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Seçenek 2. Merhaba HPC Pack Iaas dağıtım betiği kullanın
Merhaba HPC Pack Iaas dağıtım komut dosyası başka bir verimli şekilde toodeploy bir HPC paketi küme sağlar. Merhaba şablonu hello Azure Resource Manager dağıtım modeli kullanır ancak hello Klasik dağıtım modelinde, bir küme oluşturur. Ayrıca, hello betik hello Azure genel veya Azure Çin hizmetinde bir abonelik ile uyumludur.

**Ek önkoşulları**

* **Azure PowerShell** - [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) (sürüm 0.8.10 veya üzeri) istemci bilgisayarınızda.
* **HPC Pack Iaas dağıtım betiği** - karşıdan yükle ve en son sürümünü hello hello betikten hello paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Merhaba betik Hello sürümünü çalıştırarak denetleme `New-HPCIaaSCluster.ps1 –Version`. Bu makalede, sürüm 4.5.0 veya daha sonra hello komut dosyasının temel alır.

**Merhaba yapılandırma dosyası oluşturma**

 Merhaba HPC Pack Iaas dağıtım betiği bir XML yapılandırma dosyasını hello HPC küme altyapısı hello açıklayan giriş olarak kullanır. bir baş düğüm ve 18 oluşan bir küme işlem düğümlerini Microsoft Excel içeren hello işlem düğümü görüntüden oluşturulan toodeploy aşağıdaki örnek yapılandırma dosyasına hello ortamınıza değerlerini değiştirin. Hello yapılandırma dosyası hakkında daha fazla bilgi için bkz: hello betik klasöründeki hello Manual.rtf dosyasını ve [hello HPC Pack Iaas dağıtım betiği ile bir HPC kümesi oluşturma](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Merhaba yapılandırma dosyası ile ilgili notlar**

* Merhaba **VMName** hello baş düğümü **gerekir** olması hello aynı hello **ServiceName**, veya SOA işleri toorun başarısız.
* Belirttiğinizden emin olun **EnableWebPortal** hello baş düğümüne sertifika oluşturulan dışarı aktarılır ve böylece.
* bir yapılandırma sonrası PowerShell komut dosyası hello baş düğüm üzerinde çalışır PostConfig.ps1 Hello dosyayı belirtir. Aşağıdaki örnek betik hello hello Azure depolama bağlantı dizesi yapılandırır, hello bilgi işlem düğümü rolü hello baş düğümünden kaldırır ve bunlar dağıtıldığında tüm düğümlerin çevrimiçi duruma getirir. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Merhaba komut dosyasını çalıştır**

1. Merhaba PowerShell konsolunu hello istemci bilgisayarda yönetici olarak açın.
2. Dizin toohello komut dosyası klasörünü Değiştir (Bu örnekte E:\IaaSClusterScript).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. komutu aşağıdaki hello çalıştırmak toodeploy hello HPC Pack kümesi. Bu örnek hello yapılandırma dosyasının E:\HPCDemoConfig.xml içinde bulunan varsayar.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

Merhaba HPC paketi dağıtım betiği süre için çalışır. Bir şey hello komut dosyasının yaptığını tooexport ve hello küme sertifikayı indirin ve hello geçerli kullanıcının Belgeler klasöründe hello istemci bilgisayara kaydedin. ileti benzer toohello aşağıdaki Hello komut dosyası oluşturur. Aşağıdaki adımda, hello sertifikasını hello uygun sertifika deposuna aktarın.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>2. Adım Excel çalışma kitaplarını boşaltması ve bir şirket içi istemciden UDF'ler çalıştırın
### <a name="excel-activation"></a>Excel etkinleştirme
Merhaba ComputeNodeWithExcel VM görüntüsü üretim iş yükleri için kullanılırken, tooprovide bir geçerli Microsoft Office lisans anahtar tooactivate Excel hello işlem düğümlerinde gerekir. Aksi takdirde Excel hello Değerlendirme sürümü 30 gün sonra süresi dolar ve Excel çalışma kitaplarını çalıştıran hello COMException (0x800AC472) ile başarısız olur. 

Excel başka bir sonraki 30 gün için değerlendirme süresi rearm: toohello baş düğüm ve clusrun oturum `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` tüm Excel işlem düğümleri aracılığıyla HPC Küme Yöneticisi. En fazla iki kez yeniden etkinleştirin. Bundan sonra geçerli bir Office lisans anahtarı sağlamanız gerekir.

Merhaba Office Professional Plus 2013 hello VM görüntüsü üzerinde yüklü bir birim bir genel toplu lisans anahtarı (GVLK) ile sürümüdür. Anahtar Yönetim Hizmeti (KMS) aracılığıyla etkinleştirebilir / etkinleştirmeyi (AD BA) veya çoklu etkinleştirme anahtarı (MAK). 

    * toouse KMS/AD-BA, var olan bir KMS sunucusu kullanın veya yeni bir Microsoft Office 2013 toplu lisans paketi hello kullanarak ayarlayın. (İstiyorsanız, hello baş düğüm hello sunucuda ayarlayın.) Ardından hello KMS ana bilgisayar anahtarı hello Internet üzerinden veya telefonla etkinleştirin. Ardından clusrun `ospp.vbs` tooset KMS sunucusunu ve bağlantı noktası hello ve tüm hello Excel işlem düğümlerinde Office etkinleştirin. 

    * MAK, ilk clusrun toouse `ospp.vbs` tooinput hello anahtarı ve tüm hello Excel işlem düğümlerini hello Internet veya telefon aracılığıyla etkinleştirin. 

> [!NOTE]
> Office Professional Plus 2013 için perakende ürün anahtarlarını bu VM görüntüsü ile kullanılamaz. Geçerli anahtarlar ve Office veya Excel sürümü bu Office Professional Plus 2013 toplu edition dışında bir yükleme medyası varsa, bunun yerine kullanabilirsiniz. Önce bu birimin sürümü kaldırın ve sahip hello sürümü yükleyin. Merhaba, özelleştirilmiş bir VM görüntüsü toouse bir dağıtımda ölçekli olarak işlem düğümü yakalanabilir Excel yeniden.
> 
> 

### <a name="offload-excel-workbooks"></a>Excel çalışma kitaplarını boşaltma
Azure'da hello HPC Pack kümesinde çalışır, bu adımları toooffload bir Excel çalışma kitabı izleyin. toodo Bu, Excel 2010 veya 2013 hello istemci bilgisayarda zaten yüklü olması gerekir.

1. İşlem düğümü görüntü 1. adım toodeploy hello Excel ile bir HPC Pack kümesi hello seçeneklerinde birini kullanın. Merhaba küme sertifika dosyasını (.cer) ve küme kullanıcı adı ve parola edinin.
2. Merhaba istemci bilgisayarda Cert: \CurrentUser\Root altında hello küme sertifikasını içeri aktarın.
3. Excel yüklü olduğundan emin olun. Merhaba içeriğine aşağıdaki hello ile Excel.exe.config dosyası oluşturmak Excel.exe aynı klasöre hello istemci bilgisayarda. Bu adım, bu hello HPC Pack 2012 R2 Excel COM eklentisi başarıyla yükleyen sağlar.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Merhaba istemci toosubmit işleri toohello HPC Pack kümesi. Bir seçenektir toodownload hello tam [HPC Pack 2012 R2 güncelleştirme 3'ü yükleme](http://www.microsoft.com/download/details.aspx?id=49922) ve hello HPC Pack istemcisini yükleyin. Alternatif olarak, karşıdan yüklenip hello [HPC Pack 2012 R2 güncelleştirme 3 istemci yardımcı programları](https://www.microsoft.com/download/details.aspx?id=49923) ve uygun Visual C++ 2010 bilgisayarınızı yeniden dağıtılabilir hello ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. Bu örnekte, ConvertiblePricing_Complete.xlsb adlandırılmış bir örnek Excel çalışma kitabı kullanırız. Karşıdan yükleyebileceğiniz [burada](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Merhaba Excel çalışma kitabı tooa çalışma klasörü D:\Excel\Run gibi kopyalayın.
7. Merhaba Excel çalışma kitabı açın. Merhaba üzerinde **geliştirme** Şerit, tıklatın **COM eklentileri** ve o hello HPC Pack Excel COM eklentisi başarıyla yüklendi onaylayın.
   
   ![HPC Pack eklentisi excel][addin]
8. Düzen hello VBA makrosu'hello değiştirerek Excel'de HPCControlMacros satırları hello betik aşağıdaki gösterildiği gibi açıklamalı. Ortamınız için uygun değerleri değiştirin.
   
   ![HPC Pack için Excel makrosu][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Merhaba Excel çalışma kitabı tooan karşıya yükleme dizini D:\Excel\Upload gibi kopyalayın. Bu dizin hello VBA makrosu hello HPC_DependsFiles sabiti belirtildi.
10. toorun hello çalışma kitabı, azure'da hello kümede tıklatın hello **küme** hello çalışma sayfası üzerinde düğmesi.

### <a name="run-excel-udfs"></a>Excel UDF'leri çalıştırın
toorun Excel UDF'leri, 1-3'ü tooset hello istemci bilgisayarı hello önceki adımları izleyin. Excel UDF'leri için işlem düğümlerinde yüklü toohave hello Excel uygulaması gerekmez. Düğümler, küme oluşturma işlem zaman seçebilir böylece normal işlem düğümü görüntü hello yerine Excel düğümü görüntüsüyle işlem.

> [!NOTE]
> Bir 34 karakter limiti hello Excel 2010 ve 2013 Küme Bağlayıcısı iletişim kutusu yok. Merhaba UDF'ler çalıştıran bu iletişim kutusunu toospecify hello kümesi kullanın. Merhaba tam küme adı uzunsa (örneğin, hpcexcelhn01.southeastasia.cloudapp.azure.com) hello iletişim kutusunda uygun değildir. Merhaba geçici çözüm tooset bir makineye gibi değişkendir *CCP_IAASHN* hello uzun küme adı hello değerine sahip. Ardından, girin *CCP_IAASHN %* hello iletişim kutusunda hello küme baş düğüm adı. 
> 
> 

Merhaba küme başarıyla dağıtıldıktan sonra aşağıdaki adımları toorun hello ile örnek yerleşik devam Excel UDF. Özelleştirilmiş Excel UDF'leri görmek [kaynakları](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild XLL'ler hello ve bunları hello Iaas kümede dağıtın.

1. Yeni bir Excel çalışma kitabı açın. Merhaba üzerinde **geliştirme** Şerit, tıklatın **eklentileri**. Merhaba iletişim kutusunda, ardından **Gözat**toohello %CCP_HOME%Bin\XLL32 klasörüne gidin ve hello örnek ClusterUDF32.xll seçin. Merhaba ClusterUDF32 hello istemci makinede yoksa, hello baş düğümünde hello %CCP_HOME%Bin\XLL32 klasöründen kopyalayın.
   
   ![Merhaba UDF seçin][udf]
2. Tıklatın **dosya** > **seçenekleri** > **Gelişmiş**. Altında **formüller**, denetleme **XLL işlevleri toorun kullanıcı tanımlı bir işlem kümesi izin**. Ardından **seçenekleri** ve hello tam küme adı girin **küme baş düğüm adı**. (Bir uzun küme adını değil sığar belirtildiği gibi daha önce bu giriş kutusu sınırlı too34 karakterden oluşabilir. "Bir makineye değişken uzun küme adı için kullanabilirsiniz.)
   
   ![Merhaba UDF yapılandırın][options]
3. toorun hello hello kümede UDF Hesaplama değeri =XllGetComputerNameC() ile Merhaba hücreyi tıklatın ve Enter tuşuna basın. Hello işlevi yalnızca hello işlem düğümü üzerinde hangi hello UDF çalıştıran hello adını alır. İlk çalıştırma Merhaba hello kullanıcı adı ve parola tooconnect toohello Iaas küme için bir kimlik bilgileri iletişim kutusu ister.
   
   ![UDF çalıştırın][run]
   
   Çok sayıda hücre toocalculate olduğunda Alt Shift Ctrl + F9 toorun hello hesaplama tüm hücreleri tuşuna basın.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>3. Adım Bir şirket içi istemciden bir SOA iş yükü çalıştırın
toorun genel SOA uygulamaları hello HPC Pack Iaas kümede ilk yöntemlerden birini kullanın hello 1. adım toodeploy hello kümede. Merhaba işlem düğümlerinde Excel gerekmediği için bir genel işlem düğümü görüntüsü bu durumda, belirtin. Ardından aşağıdaki adımları izleyin.

1. Merhaba küme sertifikası aldıktan sonra onu Cert: \CurrentUser\Root altında hello istemci bilgisayarda içeri aktarın.
2. Merhaba yüklemek [HPC Pack 2012 R2 güncelleştirme 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) ve [HPC Pack 2012 R2 güncelleştirme 3 istemci yardımcı programları](https://www.microsoft.com/download/details.aspx?id=49923). Bu araçları toodevelop etkinleştirin ve SOA istemci uygulamaları çalıştırın.
3. Merhaba HelloWorldR2 karşıdan [örnek koduna](https://www.microsoft.com/download/details.aspx?id=41633). Merhaba HelloWorldR2.sln Visual Studio 2010 veya 2012 açın. (Bu örnek, Visual Studio'nun daha yeni sürümleri ile şu anda uyumlu değildir.)
4. Merhaba EchoService projeyi önce oluşturun. Ardından, hello hizmeti toohello Iaas kümesini dağıtma hello tooan dağıttığınız şekilde küme içi. Ayrıntılı adımlar için hello HelloWordR2 Benioku.doc bakın. Değiştirebilir ve bir Azure Iaas kümede çalışan bölüm toogenerate hello SOA istemci uygulamaları aşağıdaki hello açıklandığı gibi hello HellWorldR2 ve diğer projeler derleme.

### <a name="use-http-binding-with-azure-storage-queue"></a>HTTP bağlaması ile Azure depolama kuyruğu kullanın
bir Azure depolama kuyruğu ile toouse Http bağlama toohello örnek kod birkaç değişiklik yapın.

* Merhaba küme adını güncelleştirin.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* İsteğe bağlı olarak, SessionStartInfo içinde hello varsayılan TransportScheme kullanın veya açıkça tooHttp ayarlayın.

```
    info.TransportScheme = TransportScheme.Http;
```

* Varsayılan bağlama BrokerClient hello için kullanın.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    Veya açıkça hello basicHttpBinding kullanarak ayarlayın.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* İsteğe bağlı olarak, hello UseAzureQueue bayrağı tootrue SessionStartInfo ayarlayın. Aksi durumda kümesi, bu tootrue varsayılan olarak Azure etki alanı sonekleri hello küme adına sahip ve hello TransportScheme Http olduğunda ayarlanır.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Azure depolama kuyruğu olmadan HTTP bağlaması kullanın
bir Azure depolama kuyruğu, açıkça kümesi hello UseAzureQueue bayrağı toofalse hello SessionStartInfo içinde olmadan toouse Http bağlama.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>NetTcp bağlama kullanın
toouse NetTcp bağlama, hello benzer tooconnecting tooan şirket içi küme yapılandırmadır. Merhaba baş düğüm VM üzerindeki birkaç uç noktaları tooopen gerekir. Örneğin, hello HPC Pack Iaas dağıtım komut dosyası toocreate hello küme kullandıysanız, Azure portalında şu şekilde kümesi hello uç noktalarını hello.

1. Merhaba VM durdurun.
2. Merhaba TCP bağlantı noktaları 9090, 9087, ekleme 9091, 9094 hello oturumu için Aracısı, alt ve Veri Hizmetleri, sırasıyla Aracısı
   
    ![Uç noktaları yapılandırma][endpoint-new-portal]
3. Merhaba VM başlatın.

Merhaba SOA istemci uygulaması hello baş toohello Iaas küme tam adı değiştirme dışında herhangi bir değişiklik gerektirmez.

## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [bu kaynakları](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) Excel iş yükleri HPC paketi ile çalıştırma hakkında daha fazla bilgi için.
* Bkz: [SOA Hizmetleri'nde yönetme Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) dağıtma ve SOA Hizmetleri HPC paketi ile yönetme hakkında daha fazla bilgi için.

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
