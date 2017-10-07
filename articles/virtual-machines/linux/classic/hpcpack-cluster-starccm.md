---
title: "aaaRun yıldız-CCM + Linux VM'ler üzerinde HPC Pack ile | Microsoft Docs"
description: "Azure üzerinde Microsoft HPC Pack küme dağıtma ve bir yıldız çalıştırma-CCM + işi birden çok Linux işlem düğümlerini bir RDMA ağ üzerinden."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Yıldız Çalıştır-CCM + Linux RDMA üzerinde Microsoft HPC Pack ile Azure'da küme
Bu makale size nasıl toodeploy Microsoft HPC Pack küme Azure ve Çalıştır gösterir. bir [CD adapco yıldız-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) InfiniBand ile bağlandığına birden çok Linux işlem düğümlerinde iş.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Microsoft HPC Pack büyük ölçekli HPC ve paralel uygulamalar, Microsoft Azure sanal makinelerin kümelerde MPI uygulamaları da dahil olmak üzere çeşitli özellikler toorun sağlar. HPC Pack çalışan Linux HPC uygulamaları bir HPC Pack kümede dağıtılan Linux işlem düğümü vm'lerde de destekler. Bir giriş toousing Linux işlem düğümleri HPC paketi ile bakın [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).

## <a name="set-up-an-hpc-pack-cluster"></a>Bir HPC Pack kümesi
Hello Hello HPC Pack Iaas dağıtım betikleri indirin [Yükleme Merkezi'nden](https://www.microsoft.com/en-us/download/details.aspx?id=44949) ve yerel olarak ayıklayın.

Azure PowerShell önkoşuldur. PowerShell yerel makinenizde yapılandırılmamışsa, lütfen hello makaleyi okuyun [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

Bu yazma Hello anda hello Linux hello (içeren hello InfiniBand sürücüleri için Azure) Azure Marketi görüntülerden SLES 12, CentOS 6.5 ve CentOS 7.1 içindir. Bu makalede, SLES 12 hello kullanımını temel alır. tooretrieve hello adı hello Market HPC destekleyen tüm Linux görüntülerin hello aşağıdaki PowerShell komutunu çalıştırabilirsiniz:

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

Merhaba çıkış listeler bu görüntüleri kullanılabilir olduğunu ve hello görüntü adı hello konumu (**görüntü adı**) daha sonra hello dağıtım şablonda kullanılan toobe.

Merhaba küme dağıtmadan önce bir HPC paketi dağıtım şablon dosyası toobuild sahip. Küçük bir küme hedefleme olduğundan, hello baş düğüm hello etki alanı denetleyicisi olması ve yerel bir SQL veritabanı ana bilgisayar.

Merhaba aşağıdaki şablon böyle bir baş düğüm dağıtmak, adlı bir XML dosyası oluşturma **MyCluster.xml**ve hello değerlerini değiştirme **Subscriptionıd**, **StorageAccount**,  **Konum**, **VMName**, ve **ServiceName** sizin ile.

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

Merhaba baş düğüm oluşturma, yükseltilmiş bir komut istemi'nde hello PowerShell komutunu çalıştırarak başlatın:

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

20 too30 dakika sonra hello baş düğüm hazır. Merhaba tıklatarak hello Azure portal ' tooit bağlanabilirsiniz **Bağlan** hello sanal makinenin simgesi.

Sonunda toofix hello DNS ileticisi olabilir. toodo, bu nedenle, DNS Yöneticisi'ni başlatın.

1. Sağ hello sunucu adının DNS Yöneticisi ' nde seçin **özellikleri**ve ardından hello **İleticiler** sekmesi.
2. Merhaba tıklatın **Düzenle** tooremove herhangi ileticiler düğmesine tıklayın ve ardından **Tamam**.
3. Bu hello emin olun **hiçbir ileticiler mevcutsa, kök ipuçlarını kullanacak** onay kutusu seçilidir ve ardından **Tamam**.

## <a name="set-up-linux-compute-nodes"></a>Linux işlem düğümlerini ayarlayın
Hello kullanarak hello Linux işlem düğümlerini dağıtmak toocreate hello baş düğüm kullanılan aynı dağıtım şablonu.

Merhaba dosya Kopyala **MyCluster.xml** yerel makine toohello baş düğüm ve güncelleştirme hello **NodeCount** toodeploy istediğiniz düğümlerin sayısını hello etiketi (< = 20). Dikkatli toohave kullanılabilir yeterli çekirdek Azure kotanızı ile olması her A9 örneği aboneliğinizde 16 çekirdeğe tüketir. Daha fazla VM hello toouse istiyorsanız A8 örnekleri (8 çekirdek) yerine A9 kullanabilirsiniz aynı bütçeyi.

Merhaba baş düğümünde hello HPC Pack Iaas dağıtım betikleri kopyalayın.

Yükseltilmiş bir komut istemi'de Azure PowerShell komutlarını aşağıdaki hello çalıştırın:

1. Çalıştırma **Add-AzureAccount** tooconnect tooyour Azure aboneliği.
2. Birden çok aboneliğiniz varsa çalıştırmak **Get-AzureSubscription** toolist bunları.
3. Varsayılan bir abonelik hello çalıştırarak ayarlayın **Select-AzureSubscription - varlığıyla SubscriptionName xxxx-varsayılan** komutu.
4. Çalıştırma **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart Linux işlem düğümlerini dağıtma.
   
   ![Baş düğüm dağıtım eylem][hndeploy]

Merhaba HPC Pack Küme Yöneticisi aracını açın. Birkaç dakika sonra Linux işlem düğümlerini düzenli olarak küme işlem düğümleri listede görünür. Merhaba Klasik dağıtım modeliyle Iaas VM'ler sıralı olarak oluşturulur. Düğüm sayısını Hello önemliyse, böylece tüm dağıtılan alma önemli miktarda zaman alabilir.

![Linux düğümleri HPC Pack Küme Yöneticisi'nde][clustermanager]

Tüm düğüm hello kümede hazır ve çalışır olduğundan, ek Altyapı ayarlarını toomake vardır.

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>Windows ve Linux düğümleri için bir Azure dosya paylaşımı ayarlama
Hello Azure dosya hizmeti toostore komut dosyaları, uygulama paketleri ve veri dosyalarını kullanabilirsiniz. Azure dosya kalıcı deposu olarak Azure Blob Depolama CIFS işlevleri sağlar. Bu hello en ölçeklenebilir bir çözüm değildir, ancak hello basit bir olduğundan ve özel VM'ler gerektirmeyen unutmayın.

Merhaba makaledeki hello yönergeleri izleyerek bir Azure dosya paylaşımı oluşturmak [Windows Azure File storage ile çalışmaya başlama](../../../storage/files/storage-dotnet-how-to-use-files.md).

Depolama hesabınız olarak Hello adını tutmak **saname**, hello dosya paylaşımı adı olarak **sharename**ve hello depolama hesabı anahtarı olarak **sakey**.

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>Merhaba baş düğümünde Hello Azure dosya paylaşımını bağlama
Yükseltilmiş bir komut istemi açın ve komut toostore hello hello yerel makine kasa kimlik bilgilerini aşağıdaki hello çalıştırın:

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

Çalıştırma ardından toomount hello Azure dosya paylaşımı:

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Linux işlem düğümlerinde Hello Azure dosya paylaşımını bağlama
HPC paketi ile birlikte gelen bir yararlı aracı hello clusrun araçtır. İşlem düğümleri kümesi üzerinde aynı anda aynı komutu bu komut satırı aracı toorun hello kullanabilirsiniz. Bu örnekte, toomount hello Azure dosya paylaşımı kullandı ve toosurvive yeniden başlatmalar kalır.
Merhaba baş düğümünde yükseltilmiş bir komut istemi içinde hello aşağıdaki komutları çalıştırın.

toocreate hello bağlama dizini:

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

toomount hello Azure dosya paylaşımı:

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

toopersist hello bağlama paylaşımı:

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>Yıldız yükle-CCM +
Azure VM örnekleri A8 ve A9 InfiniBand destek ve RDMA yetenekleri sağlar. Bu özellikleri etkinleştirmek hello çekirdek sürücüler, Windows Server 2012 R2, SUSE 12, CentOS 6.5 ve hello Azure Marketi CentOS 7.1 görüntüleri için kullanılabilir. Microsoft MPI ve Intel MPI (5.x sürümü), bu sürücüleri Azure'da destekleyen hello iki MPI kitaplıkları var.

CD adapco yıldız-CCM + 11.x bırakın ve daha sonra Intel MPI sürümüyle birlikte Azure InfiniBand desteği dahil olacak şekilde 5.x.

Merhaba Linux64 alma yıldız-CCM + hello paketinden [CD adapco portal](https://steve.cd-adapco.com). Örneğimizde, karma duyarlık 11.02.010 sürümünde kullandık.

Merhaba baş düğümünde, hello **/hpcdata** Azure dosya paylaşımı, adlandırılmış bir kabuk betiği oluşturmak **setupstarccm.sh** içeriği aşağıdaki hello ile. Bu komut dosyasını her işlem düğümü tooset yıldız yukarı üzerinde çalıştırmak-CCM + yerel olarak.

#### <a name="sample-setupstarcmsh-script"></a>Örnek setupstarcm.sh komut dosyası
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
Şimdi, tooset yıldız yukarı-CCM + tüm Linux işlem düğümleri, yükseltilmiş bir komut istemi açın ve hello aşağıdaki komutu çalıştırın:

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Hello komutu çalışırken hello ısı Haritası Küme Yöneticisi'nin kullanarak hello CPU kullanımını izleyebilirsiniz. Birkaç dakika sonra tüm düğümleri doğru şekilde ayarlanmış olması.

## <a name="run-star-ccm-jobs"></a>Yıldız Çalıştır-CCM + işleri
HPC Pack iş Zamanlayıcı yeteneklerini sipariş toorun yıldız için kullanıldığından-CCM + işler. toodo bu nedenle, biz kullanılan toostart hello iş ve yıldız çalıştırmak birkaç komut dosyalarının destek hello-CCM +. Merhaba giriş verisi hello Azure dosya paylaşımında kolaylık olması için ilk olarak tutulur.

PowerShell Betiği aşağıdaki hello olduğu kullanılan tooqueue bir yıldız-CCM + işi. Üç bağımsız değişkeni alır:

* Merhaba model adı
* kullanılan düğümlerin toobe Hello sayısı
* Merhaba kullanılan her düğüm toobe üzerinde çekirdek sayısı

Çünkü yıldız-CCM + hello bellek bant genişliği doldurabilirsiniz, daha az çekirdek başına, genellikle daha iyi toouse işlem düğümleri ve yeni düğümler ekleyin. Merhaba tam düğümü başına çekirdek sayısı hello işlemci ailesi ve hello bağlantı hızı değişir.

Merhaba düğümleri özel olarak hello iş için ayrılmış ve diğer işlemlerle paylaşılamaz. Merhaba iş MPI iş olarak doğrudan başlatılmadı. Merhaba **runstarccm.sh** Kabuk betiği hello MPI Başlatıcısı başlayacak.

Merhaba giriş modeli ve hello **runstarccm.sh** betik hello depolanan **/hpcdata** daha önce oluşturulmuş paylaşımı.

Günlük dosyaları hello iş kimliği ile aynı ada sahiptir ve hello depolanan **/hpcdata paylaşımı**, hello yıldız birlikte-CCM + çıkış dosyaları.

#### <a name="sample-submitstarccmjobps1-script"></a>Örnek SubmitStarccmJob.ps1 komut dosyası
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
Değiştir **runner.java** , tercih edilen yıldız ile-CCM + Java modeli Başlatıcısı ve günlük kodu.

#### <a name="sample-runstarccmsh-script"></a>Örnek runstarccm.sh komut dosyası
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

Testimizde, bir isteğe bağlı güç lisans belirteci kullandık. Bu bir belirteç tooset hello sahip **$CDLMD_LICENSE_FILE** ortam değişkeni çok **1999@flex.cd-adapco.com**  ve hello hello anahtarında **- podkey** hello komut satırı seçeneği .

Bazı başlatma hello betik ayıklar--hello **$CCP_NODES_CORES** HPC Pack ayarlanan--ortam değişkenlerini hello MPI Başlatıcısı hello hostfile kullanan düğümleri toobuild listesi. Bu hostfile hello hello işi, satır başına bir ad için kullanılan işlem düğümü adlarının listesini içerir.

Merhaba biçimi **$CCP_NODES_CORES** bu deseni izler:

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

Konumlar:

* `<Number of nodes>`toothis iş ayrılan düğümler Hello sayısıdır.
* `<Name of node_n_...>`Merhaba toothis iş ayrılan her düğümün adıdır.
* `<Cores of node_n_...>`Çekirdek toothis iş ayrılan hello düğümde Hello sayısıdır.

Merhaba çekirdek sayısı (**$NBCORES**) de hesaplanan göre hello düğüm sayısı: (**$NBNODES**) ve hello düğümü başına çekirdek sayısı (parametre olarak sağlanan **$NBCORESPERNODE**).

Merhaba MPI seçenekler için hello Azure üzerinde Intel MPI ile kullanılan olanları şunlardır:

* `-mpi intel`Intel MPI toospecify.
* `-fabric UDAPL`toouse Azure InfiniBand fiilleri.
* `-cpubind bandwidth,v`YILDIZ ile MPI için toooptimize bant genişliği-CCM +.
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI iş ile Azure InfiniBand ve tooset hello düğümü başına çekirdek sayısı gereklidir.
* `-batch`toostart yıldız-CCM + toplu iş modunda kullanıcı Arabirimi ile.

Son olarak, toostart bir işin, düğümlerin ve çalışıyor olduğundan ve Küme Yöneticisi'nde çevrimiçi olduğundan emin olun. Ardından bir PowerShell komut isteminde bu çalıştırın:

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>Düğümler durdurun
Daha sonra testlerinizi ile işiniz bittiğinde sonra HPC Pack PowerShell komutları toostop aşağıdaki hello kullanın ve düğümleri başlatın:

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>Sonraki adımlar
Diğer Linux iş yükleri çalıştırmayı deneyin. Örneğin, bakın:

* [Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack NAMD çalıştırın](hpcpack-cluster-namd.md)
* [OpenFOAM, azure'da bir Linux RDMA kümede Microsoft HPC Pack ile çalıştırın.](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
