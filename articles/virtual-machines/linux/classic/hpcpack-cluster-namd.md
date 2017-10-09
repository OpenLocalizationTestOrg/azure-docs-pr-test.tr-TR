---
title: "Linux sanal makineleri üzerinde Microsoft HPC paketi ile aaaNAMD | Microsoft Docs"
description: "Azure Microsoft HPC Pack kümede dağıtmak ve NAMD benzetimi charmrun ile birden çok Linux işlem düğümlerinde çalışacak."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>Azure’daki Linux işlem düğümlerinde Microsoft HPC Pack ile NAMD çalıştırma
Bu makalede tek yönlü toorun Linux yüksek performanslı bilgi işlem (HPC) iş yükü Azure sanal makinelerde gösterilmektedir. Burada ayarladığınız bir [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) Azure üzerinde Linux işlem düğümü ile küme ve Çalıştır bir [NAMD](http://www.ks.uiuc.edu/Research/namd/) benzetimi toocalculate ve büyük biomolecular sistem hello yapısını görselleştirin.  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** (Nanoscale Molecular Dynamics programı) olan büyük biomolecular sistemleri yüksek performanslı benzetimi için tasarlanmış bir paralel molecular dynamics paketini içeren Atom toomillions. Bu sistemlere örnek olarak, virüsler, hücre yapıları ve büyük proteins içerir. NAMD toohundreds tipik benzetimleri ve hello en büyük benzetimleri 500.000 çekirdeği daha toomore için çekirdek ölçeklendirir.
* **Microsoft HPC Pack** özellikleri toorun sağlar büyük ölçekli HPC ve şirket içi bilgisayarları veya Azure sanal makineleri kümelerinde paralel uygulamalar. İlk olarak Windows HPC iş yükleri, HPC paketi için bir çözüm olarak geliştirilen şimdi Linux HPC uygulamaları Linux üzerinde çalışan destekleyen bir HPC Pack kümede dağıtılan düğümü VM'ler işlem. Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) giriş.

Diğer Seçenekler toorun Linux HPC için azure'da iş yüklerini bkz [toplu işlem ve yüksek performanslı bilgi işlem için teknik kaynaklar](../../../batch/batch-hpc-solutions.md).

## <a name="prerequisites"></a>Ön koşullar
* **HPC Pack küme Linux işlem düğümlerini** -ya da kullanarak Azure Linux işlem düğümlerini içeren bir HPC Pack kümeyi dağıtma bir [Azure Resource Manager şablonu](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) veya bir [Azure PowerShell Betiği](hpcpack-cluster-powershell-script.md) . Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) hello Önkoşullar ve adımlar her iki seçenek için. Merhaba PowerShell komut dosyası dağıtım seçeneği seçerseniz, bu makalenin hello sonunda hello örnek dosyalarında hello örnek yapılandırma dosyasına bakın. Bu dosya bir Windows Server 2012 R2 baş düğüm ve dört boyutu büyük CentOS 6.6 işlem düğümleri oluşan bir HPC Pack Azure tabanlı küme yapılandırır. Bu dosya, ortamınız için gerektiği gibi özelleştirin.
* **NAMD yazılım ve öğretici dosyaları** -karşıdan NAMD yazılımlardan Linux için hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (kayıt gerekli). Bu makalede sürüm 2.10 NAMD üzerinde temel alır ve kullandığı hello [Linux-x86_64 (64-bit Intel/AMD Ethernet ile)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) arşiv. Merhaba de karşıdan [NAMD öğreticileri](http://www.ks.uiuc.edu/Training/Tutorials/#namd). Merhaba yüklemeleri .tar dosyalarıdır ve bir Windows aracı tooextract hello dosyalarını hello küme baş düğümüne gerekir. tooextract hello dosyaları, bu makalenin sonraki bölümlerinde hello yönergeleri izleyin. 
* **VMD** (isteğe bağlı) - NAMD işinizin toosee hello sonuçları yükleyip hello molecular görselleştirme program [VMD](http://www.ks.uiuc.edu/Research/vmd/) tercih ettiğiniz bir bilgisayarda. Merhaba geçerli 1.9.2 sürümüdür. VMD karşıdan başlatılan site tooget hello bakın.  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>İşlem düğümleri arasında karşılıklı güven ayarlama
Bir geçici düğüm işi birden çok Linux düğümler üzerinde çalışan gerektirir hello düğümleri tootrust birbirine (tarafından **rsh** veya **ssh**). Microsoft HPC Pack Iaas dağıtım betiği hello ile Merhaba HPC Pack kümesi oluşturduğunuzda, hello betik kalıcı karşılıklı güven belirttiğiniz hello yönetici hesabı için otomatik olarak ayarlar. Bir iş toothem ayrılan hello kümenin etki alanında oluşturduğunuz yönetici olmayan kullanıcılar için tooset hello düğümler arasında geçici karşılıklı güveni vardır. Ardından, Hello işi tamamlandıktan sonra hello ilişkisi yok. toodo bu her kullanıcı için sağlayan bir RSA anahtar çifti toohello küme hangi HPC Pack tooestablish hello güven ilişkisi kullanır. Yönergeleri izleyin.

### <a name="generate-an-rsa-key-pair"></a>RSA anahtar çifti oluşturma
Kolay toogenerate bir ortak anahtar ve özel anahtarı içeren bir RSA anahtar çifti, Linux hello çalıştırarak **ssh-keygen** komutu.

1. Üzerinde tooa Linux bilgisayarda oturum açın.
2. Merhaba aşağıdaki komutu çalıştırın:
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Tuşuna **Enter** hello komut tamamlanıncaya kadar toouse hello varsayılan ayarlar. Burada bir parola girmeyin; için bir parola istendiğinde, yalnızca basın **Enter**.
   > 
   > 
   
   ![RSA anahtar çifti oluşturma][keygen]
3. Dizin toohello ~/.ssh dizini değiştirin. Merhaba özel anahtarı id_rsa.pub id_rsa ve hello ortak anahtarında depolanır.
   
   ![Özel ve genel anahtarlar][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Merhaba anahtar çifti toohello HPC paketi küme ekleme
1. [Tarafından Uzak Masaüstü Bağlantısı](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello baş düğüm VM kullanarak hello hello kümeyi (örneğin, hpc\clusteradmin) dağıttığınızda sağlanan etki alanı kimlik bilgileri. Merhaba küme hello baş düğümünden yönetin.
2. Standart Windows Server yordamları toocreate bir etki alanı kullanıcı hesabı hello kümenin Active Directory etki alanında kullanın. Örneğin, hello baş düğümünde hello Active Directory Kullanıcıları ve Bilgisayarları aracını kullanın. Bu makaledeki örneklerde Hello hpcuser hello hpclab etki alanında (hpclab\hpcuser) adlı bir etki alanı kullanıcısı oluşturun varsayalım.
3. Merhaba etki alanı kullanıcı toohello HPC paketi Küme Küme kullanıcı olarak ekleyin. Yönergeler için bkz: [ekleme veya kaldırma küme kullanıcılar](https://technet.microsoft.com/library/ff919330.aspx).
4. C:\cred.XML ve kopyalama hello RSA anahtar verilerini içine adlı bir dosya oluşturun. Bu makalenin hello sonunda örnek dosyalarını hello bir örnek bulabilirsiniz.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. Bir komut istemi açın ve tooset hello veri hello hpclab\hpcuser hesabı için kimlik bilgileri komutu aşağıdaki hello girin. Merhaba kullandığınız **extendeddata** parametresi toopass hello dosyasının adı oluşturduğunuz hello C:\cred.xml hello anahtar veriler için.
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Bu komut çıktısı başarıyla tamamlanır. Toorun işleri ihtiyacınız hello kullanıcı hesapları için hello kimlik bilgilerini ayarlama sonra hello cred.xml dosyayı güvenli bir konumda depolayın veya silin.
6. Linux düğümlerinden biri üzerinde hello RSA anahtar çifti oluşturursa, bunları kullanmayı bitirdikten sonra toodelete hello anahtarları unutmayın. Varolan bir id_rsa dosya veya id_rsa.pub dosyası bulursa, HPC Pack karşılıklı güven ayarlı değil.

> [!IMPORTANT]
> Bir yönetici tarafından gönderilen bir işin hello kök hesapta hello Linux düğümleri üzerinde çalıştığı için Linux iş paylaşılan bir kümede bir Küme Yöneticisi olarak çalışan öneririz yok. Yönetici olmayan bir kullanıcı tarafından gönderilen bir işi hello aynı hello işi kullanıcı adı ile bir yerel Linux kullanıcı hesabı altında çalışır. Bu durumda, HPC Pack bu Linux kullanıcı için karşılıklı güven toohello iş ayrılan tüm hello düğümlere ayarlar. Merhaba Linux kullanıcı hello Linux düğümlerde el ile Merhaba işi çalıştırmadan önce ayarlayabilirsiniz veya hello iş gönderildiğinde HPC Pack Merhaba kullanıcı otomatik olarak oluşturur. HPC Pack Merhaba kullanıcı oluşturursa, HPC Pack Merhaba işi tamamlandıktan sonra onu siler. tooreduce güvenlik tehdidi, hello hello düğümlerinde hello işi tamamlandıktan sonra anahtarları kaldırılır.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Linux düğümleri için bir dosya paylaşımı ayarlama
Şimdi bir SMB dosya paylaşımı ayarlama ve tüm dosyalarda Linux düğümleri tooallow hello Linux düğümleri tooaccess NAMD ortak bir yol ile Merhaba paylaşılan klasöre bağlayın. Adımları toomount hello baş düğüm üzerinde paylaşılan bir klasöre aşağıda verilmiştir. Bir paylaşım için CentOS 6.6 gibi hello Azure dosya hizmeti şu anda desteklenmiyor dağıtımları önerilir. Linux düğümleri bir Azure dosya paylaşımı desteği olup [nasıl toouse Linux Azure File storage](../../../storage/files/storage-how-to-use-files-linux.md). Ek dosya paylaşımı ile HPC Pack seçenekleri için bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).

1. Merhaba baş düğüm üzerinde bir klasör oluşturun ve okuma/yazma ayrıcalıklarına ayarlayarak tooEveryone paylaşın. Bu örnekte, \\ \\CentOS66HN\Namd CentOS66HN hello baş düğümü hello ana bilgisayar adı olduğu hello klasörünün hello adı değil.
2. Merhaba paylaşılan klasörde namd2 adlı bir alt klasör oluşturun. Namd2 içinde namdsample adlı başka bir alt klasör oluşturun.
3. Bir Windows sürümünü kullanarak hello klasördeki Hello NAMD dosyaları ayıklayın **tar** veya .tar arşivler üzerinde çalıştığı başka bir Windows yardımcı programı. 
   
   * Merhaba NAMD tar arşiv çok ayıklamak\\\\CentOS66HN\Namd\namd2.
   * Merhaba öğreticileri altında ayıklamak \\ \\CentOS66HN\Namd\namd2\namdsample.
4. Bir Windows PowerShell penceresi açın ve toomount hello hello Linux düğümleri paylaşılan klasör komutları aşağıdaki hello çalıştırın.
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /namd2 adlı bir klasör oluşturur. Merhaba ikinci komut hello paylaşılan klasör //CentOS66HN/Namd/namd2 dir_mode ve file_mode BITS kümesi too777 hello klasörüyle üzerine bağlar. Merhaba *kullanıcıadı* ve *parola* hello komutu hello baş düğüm üzerinde bir kullanıcının kimlik bilgilerini hello olması gerekir.

> [!NOTE]
> Merhaba "\`" Merhaba ikinci komut dosyasındaki simge olan PowerShell bir kaçış simgesi. "\`,"anlamına gelir hello"," (virgül karakteri) hello komutu bir parçasıdır.
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>Bir Bash betik toorun NAMD işi oluşturma
NAMD işinizi gereken bir *listesi* dosya **charmrun** toodetermine hello NAMD işlemleri başlatırken düğümleri toouse sayısı. Merhaba listesi dosyası oluşturur ve çalışan bir Bash komut dosyası kullanarak **charmrun** bu listesi dosyayla. Ardından NAMD işi HPC Kümesi bu komut dosyasını çağıran Yöneticisi'nde gönderebilirsiniz.

Tercih ettiğiniz bir metin düzenleyicisi kullanarak hello /namd2 klasöründe hello NAMD program dosyalarını içeren bir Bash komut dosyası oluşturabilir ve hpccharmrun.sh adlandırın. Hızlı bir kavram kanıtı için hello örnek hpccharmrun.sh hello bu makalenin sonunda sağlanan komut dosyasını kopyalayın ve çok Git[NAMD işi göndermek](#submit-a-namd-job).

> [!TIP]
> Satır sonlarını (yalnızca LF, CR LF) kodunuzu Linux bir metin dosyası olarak kaydedin. Bu, düzgün şekilde hello Linux düğümlerinde çalıştığını sağlar.
> 
> 

Bu bash betiğin yaptığı hakkında ayrıntılar verilmiştir. 

1. Bazı değişkenleri tanımlayın.
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. Düğüm bilgi hello ortam değişkenlerinin alın. $NODESCORES $CCP_NODES_CORES bölünmüş sözcükleri listesini depolar. $COUNT $NODESCORES hello boyutudur.
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   Merhaba $CCP_NODES_CORES değişkeni için Hello biçimi aşağıdaki gibidir:
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   Bu değişken düğümler, düğüm adı ve her düğümde toohello iş ayrılan çekirdek sayısı toplam sayısı hello listeler. Merhaba iş 10 çekirdekler toorun gerekirse, örneğin, $CCP_NODES_CORES hello değerini benzer:
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. Merhaba $CCP_NODES_CORES değişken ayarlanmamışsa, başlangıç **charmrun** doğrudan. (Bu komut dosyasını doğrudan Linux düğümlerinde çalıştırdığınızda bu yalnızca olmalıdır.)
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. Veya bir listesi dosyası oluşturma **charmrun**.
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. Çalıştırma **charmrun** hello listesi dosyayla dönüş durumunu almak ve hello listesi dosyasını hello sonunda kaldırın.
   
   ${CCP_NUMCPUS} hello HPC paketi üstbilgi düğümü tarafından ayarlanmış başka bir ortam değişkenidir. Merhaba toothis iş ayrılan toplam çekirdek sayısı depolar. Bu işlem toospecify hello sayısı charmrun için kullanırız.
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. Merhaba çıkış **charmrun** dönüş durumu.
   
   ```
   exit ${RTNSTS}
   ```

Merhaba bilgilerini hello listesi dosyasına hangi hello komut dosyası oluşturur, aşağıda verilmiştir:

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

Örneğin:

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>NAMD işi gönderin
Artık hazır toosubmit NAMD işi HPC Küme Yöneticisi'nde bulunur.

1. Tooyour küme baş düğümüne bağlanmak ve HPC Küme Yöneticisi'ni başlatın.
2. İçinde **kaynak yönetimi**, hello Linux işlem düğümlerini hello olduğundan emin olun **çevrimiçi** durumu. Değilse, bunları seçin ve tıklatın **çevrimiçine**.
3. İçinde **iş yönetimi**, tıklatın **yeni iş**.
4. İş için bir ad girin *hpccharmrun*.
   
   ![Yeni HPC iş][namd_job]
5. Hello üzerinde **iş ayrıntılarını** sayfasında **iş kaynakları**, kaynak olarak hello türünü seçin **düğümü** ve kümesi hello **Minimum** too3. , şu üç Linux düğümlerinde hello işini çalıştırın ve her düğümün dört çekirdeğe sahip.
   
   ![İş kaynakları][job_resources]
6. Tıklatın **Düzenle görevleri** hello sol gezinti bölmesinde ve ardından **Ekle** tooadd görev toohello işi.    
7. Merhaba üzerinde **görev ayrıntılarını ve g/ç yönlendirmesi** sayfasında, aşağıdaki değerleri kümesi hello:
   
   * **Komut satırı**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > Merhaba önceki komut satır sonu olmayan tek bir komut satırıdır. Birkaç satırdaki altında tooappear sarmalar **komut satırı**.
     > 
     > 
   * **Çalışma dizini** -/namd2
   * **Minimum** - 3
     
     ![Görev Ayrıntıları][task_details]
     
     > [!NOTE]
     > Çünkü hello çalışma dizini Burada ayarlanan **charmrun** toonavigate toohello çalışır her düğümde aynı çalışma dizini. HPC Pack Merhaba komut Hello çalışma dizini ayarlanmamışsa hello Linux düğümlerinden biri üzerinde oluşturduğunuz rastgele adlandırılmış bir klasördeki başlatır. Bu, diğer düğümlere hello üzerinde aşağıdaki hata hello neden olur: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid bu sorunu hello çalışma dizini olarak tüm düğümler tarafından erişilebilen bir klasör yolu belirtin.
     > 
     > 
8. Tıklatın **Tamam** ve ardından **gönderme** toorun bu işi.
   
   Varsayılan olarak, HPC Pack Merhaba iş geçerli oturum açmış kullanıcı hesabınız olarak gönderir. Tıklattıktan sonra bir iletişim kutusu tooenter hello kullanıcı adı ve parola isteyebilir **gönderme**.
   
   ![İş kimlik bilgileri][creds]
   
   Bazı koşullarda HPC Pack önce giriş ve bu iletişim kutusunu göstermez hello kullanıcı bilgilerini hatırlıyor. toomake HPC paketi yeniden göstermek, komutu bir komut isteminde aşağıdaki hello girin ve hello işi göndermek.
   
   ```command
   hpccred delcreds
   ```
9. Merhaba işi birkaç dakika toofinish alır.
10. Merhaba iş günlüğü Bul \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log ve hello çıkış dosyalarında \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. İsteğe bağlı olarak, VMD tooview iş sonuçlarınızı başlatın. Merhaba NAMD çıktı dosyaları (Bu durumda, su küre içinde ubiquitin protein molecule) görselleştirme için hello bu makalenin kapsamı dışındadır hello adımlardır. Bkz: [NAMD öğretici](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) Ayrıntılar için.
    
    ![İş sonuçları][vmd_view]

## <a name="sample-files"></a>Örnek dosyaları
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>PowerShell komut dosyası tarafından küme dağıtımı için örnek XML yapılandırma dosyası
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a>Örnek cred.xml dosyası
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```

### <a name="sample-hpccharmrunsh-script"></a>Örnek hpccharmrun.sh komut dosyası
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
