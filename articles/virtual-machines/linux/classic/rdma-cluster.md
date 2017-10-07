---
title: "bir Linux RDMA küme toorun MPI uygulamaları aaaSet | Microsoft Docs"
description: "Linux kümesi boyutu H16r, H16mr, A8 veya A9 Vm'lerde toouse hello Azure RDMA ağ toorun MPI uygulamaları oluşturma"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>Bir Linux RDMA küme toorun MPI uygulama ayarlama
Azure ile Linux RDMA yukarı tooset nasıl kümesi öğrenin [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun paralel ileti geçirme arabirimi (MPI) uygulamalarını. Bu makale, bir kümede Linux HPC görüntü toorun Intel MPI adımları tooprepare sağlar. Hazırlık sonra bu görüntü ve hello RDMA özellikli Azure VM boyutlarını (şu anda H16r, H16mr, A8 veya A9) birini kullanarak sanal makineleri bir küme dağıtın. Doğrudan uzak bellek erişimi (RDMA) teknolojisine dayalı düşük gecikmeli, yüksek verimlilik bir ağ üzerinden verimli bir şekilde iletişim hello küme toorun MPI uygulamaları kullanın.

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik. Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

## <a name="cluster-deployment-options"></a>Küme dağıtım seçenekleri
Aşağıdaki yöntemlerdir ile veya iş Zamanlayıcı olmadan toocreate Linux RDMA küme kullanabilirsiniz.

* **Azure CLI betikleri**: Bu makalenin sonraki bölümlerinde gösterildiği gibi hello kullanın [Azure komut satırı arabirimi](../../../cli-install-nodejs.md) (CLI) tooscript hello RDMA özellikli VM'lerin bir küme dağıtımı. çok sayıda işlem düğümleri dağıtma birkaç dakika sürebilir için hizmet yönetimi modu hello CLI hello küme düğümleri seri olarak hello Klasik dağıtım modelinde oluşturur. tooenable hello hello Klasik dağıtım modeli kullandığınızda RDMA ağ bağlantısı dağıtma hello VM'ler hello aynı bulut hizmeti.
* **Azure Resource Manager şablonları**: hello Resource Manager dağıtım modeli toodeploy toohello RDMA ağ bağlanır RDMA özellikli VM'ler oluşan bir küme de kullanabilirsiniz. Yapabilecekleriniz [kendi şablonunuzu oluşturun](../../../resource-group-authoring-templates.md), veya hello denetleyin [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/) istediğiniz Microsoft veya hello topluluk toodeploy hello çözümü tarafından katkıda bulunan şablonları için. Resource Manager şablonları hızlı ve güvenilir bir yol toodeploy Linux kümesi sağlar. tooenable hello hello Resource Manager dağıtım modeli kullandığınızda RDMA ağ bağlantısı dağıtma hello hello Vm'lerde aynı kullanılabilirlik kümesi.
* **HPC Pack**: Microsoft HPC Pack küme oluşturmayı ve desteklenen bir Linux dağıtım tooaccess hello RDMA ağ Çalıştır RDMA özellikli işlem düğümleri ekleyin. Daha fazla bilgi için bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).

## <a name="sample-deployment-steps-in-hello-classic-model"></a>Merhaba Klasik modelde örnek dağıtım adımları
Merhaba aşağıdaki adımlar nasıl toouse hello Azure CLI toodeploy hello Azure Marketi SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM'den özelleştirebilir ve özel bir VM görüntüsü oluşturma gösterir. Daha sonra hello görüntü tooscript hello RDMA özellikli sanal makineleri bir küme dağıtımını kullanabilirsiniz.

> [!TIP]
> RDMA yeteneğine sahip sanal makineleri bir küme hello Azure Marketi CentOS tabanlı HPC görüntülerinde temel benzer adımları toodeploy kullanın. Bazı adımlar belirtildiği gibi biraz daha farklı. 
>
>

### <a name="prerequisites"></a>Ön koşullar
* **İstemci bilgisayar**: Azure ile Mac, Linux veya Windows istemci bilgisayarı toocommunicate gerekir. Bu adımlarda Linux istemci kullandığınız varsayılır.
* **Azure aboneliği**: bir aboneliğiniz yoksa oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde. Daha büyük kümeleri için Kullandıkça Öde aboneliğine veya diğer satın alma seçenekleri göz önünde bulundurun.
* **VM boyutu kullanılabilirlik**: örnek boyutları aşağıdaki hello RDMA özelliğine sahip olan: H16r, H16mr, A8 ve A9. Denetleme [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/) Azure bölgelerindeki kullanılabilirlik.
* **Çekirdek kota**: çekirdek toodeploy işlem yoğunluklu VM'ler oluşan bir küme tooincrease hello kotası gerekebilir. Örneğin, bu makaledeki gösterildiği gibi toodeploy 8 A9 Vm'lerde istiyorsanız en az 128 çekirdek gerekir. Aboneliğinizi de hello hello H-serisi dahil olmak üzere belirli VM boyutu aileleri, dağıtabilirsiniz çekirdek sayısını sınırlayabilir. toorequest kota artırma, [bir çevrimiçi müşteri destek isteği açma](../../../azure-supportability/how-to-create-azure-support-request.md) herhangi bir ücret alınmaz.
* **Azure CLI**: [yükleme](../../../cli-install-nodejs.md) Azure CLI hello ve [tooyour Azure aboneliğine bağlanma](../../../xplat-cli-connect.md) hello istemci bilgisayardan.

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>SLES 12 SP1 HPC VM sağlama
TooAzure hello Azure CLI ile oturum sonra çalıştırmak `azure config list` çıktı hello tooconfirm hizmet yönetimi modu gösterir. Yoksa, şu komutu çalıştırarak hello modunu ayarlayın:

    azure config mode asm


Toolist aşağıdaki hello yetkili toouse olduğunuz tüm hello abonelikleri yazın:

    azure account list

Merhaba geçerli etkin bir aboneliğiniz ile tanımlanan `Current` çok ayarlamak`true`. Bu abonelik hello değilse, bir toouse toocreate hello küme istediğiniz, hello uygun abonelik kimliği etkin bir aboneliğiniz hello ayarlayın:

    azure account set <subscription-Id>

toosee Merhaba, kabuk ortam desteklediği varsayarak, aşağıdakileri hello gibi bir komut çalıştırmak Azure genel kullanıma açık SLES 12 SP1 HPC görüntülerinde **grep**:

    azure vm image list | grep "suse.*hpc"

SLES 12 SP1 HPC görüntüsü ile RDMA özellikli bir VM hello aşağıdaki gibi bir komutu çalıştırarak sağlayın:

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

Konumlar:

* Merhaba boyutu (Bu örnekte A9) hello RDMA özelliğine sahip VM boyutları biridir.
* Merhaba dış SSH bağlantı noktası numarası (Bu örnekte, hello SSH varsayılan olan 22) tüm geçerli bağlantı noktası numarasıdır. Merhaba iç SSH bağlantı noktası numarası too22 ayarlanır.
* Yeni bir bulut hizmeti hello hello konumu tarafından belirtilen Azure bölgesi oluşturulur. Merhaba VM boyutu seçtiğiniz kullanılabilir bir konum belirtin.
* (Bu, ek ücret doğurur) SUSE öncelik desteği için hello SLES 12 SP1 görüntü adı şu anda olabilir bu iki seçenekten birini: 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>Merhaba VM özelleştirme
Merhaba VM Sağlama tamamlandıktan sonra kullanarak SSH toohello VM VM'ın dış IP adresi (veya DNS adı) hello ve yapılandırılmış ve bu özelleştirme harici bağlantı noktası numarası hello. Bağlantı ayrıntıları için bkz: [nasıl toolog Linux çalıştıran tooa sanal makine üzerinde](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Gerekli toocomplete bir adım kök erişimi olmadığı sürece komutları hello VM üzerinde yapılandırılmış hello kullanıcı olarak gerçekleştirin.

> [!IMPORTANT]
> Microsoft Azure tooLinux VM'ler kök erişimi sağlamaz. komutları kullanarak çalışacak bir kullanıcı toohello VM olarak bağlanıldığında toogain yönetimsel erişim `sudo`.
>
>

* **Güncelleştirmeleri**: zypper kullanarak güncelleştirmeleri yükleyin. Ayrıca tooinstall NFS yardımcı programları isteyebilirsiniz.

  > [!IMPORTANT]
  > SLES 12 SP1 HPC VM ile sürücüleri hello Linux RDMA ile sorunlara neden olabilir çekirdek güncelleştirmeleri uygulanmaz öneririz.
  >
  >
* **Intel MPI**: hello aşağıdaki komutu çalıştırarak hello SLES 12 SP1 HPC VM Intel MPI hello yüklemesini tamamlayın:

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **Bellek kilitleme**: MPI kodları toolock hello bellek RDMA için ekleme veya hello /etc/security/limits.conf dosyasındaki ayarları aşağıdaki hello değiştirin. Bu dosya kök erişimi tooedit gerekir.

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > Test amacıyla, memlock toounlimited de ayarlayabilirsiniz. Örneğin: `<User or group name>    hard    memlock unlimited`. Daha fazla bilgi için bkz: [ayarı için bilinen en iyi yöntemleri kilitli bellek boyutu](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).
  >
  >
* **SLES VM'ler için SSH anahtarları**: oluşturmak SSH anahtarları tooestablish güven hello arasında kullanıcı hesabınız için işlem hello SLES küme düğümünde MPI işlerini çalıştırırken. CentOS tabanlı HPC VM dağıttıysanız, bu adımı izlemeyin. Merhaba görüntüsünü yakalamak ve hello küme dağıttıktan sonra daha sonra bu makalede tooset hello küme düğümleri arasında passwordless SSH güveni yönergeleri bakın.

    toocreate SSH anahtarları, komutu aşağıdaki hello çalıştırın. Giriş için istendiğinde seçin **Enter** toogenerate hello anahtarları bir parola ayarlama olmadan hello varsayılan konumu.

        ssh-keygen

    Bilinen ortak anahtarları için Hello ortak anahtar toohello authorized_keys dosyası ekleyin.

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    Merhaba ~/.ssh dizininde düzenleyin veya hello yapılandırma dosyası oluşturun. Başlangıç IP adresi aralığı hello özel ağ (Bu örnekte 10.32.0.0/16) azure'da toouse planlama sağlar:

        host 10.32.0.*
        StrictHostKeyChecking no

    Alternatif olarak, aşağıdaki gibi hello özel ağ IP adresi, kümedeki her bir VM listesi:

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > Yapılandırma `StrictHostKeyChecking no` belirli IP adreslerini veya aralığını belirtilmediyse, bir güvenlik riski oluşturabilir.
  >
  >
* **Uygulamaları**: hello görüntüyü yakalamadan önce diğer özelleştirmeleri gerçekleştirin veya gerektiğini tüm uygulamaları yükleyin.

### <a name="capture-hello-image"></a>Merhaba görüntü yakalama
ilk komut hello Linux VM üzerinde aşağıdaki hello çalıştırma toocapture hello resim. Bu komut hello VM deprovisions ancak kullanıcı hesapları ve ayarladığınız SSH anahtarları korur.

```
sudo waagent -deprovision
```

İstemci bilgisayarından, Azure CLI komutları toocapture hello görüntü aşağıdaki hello çalıştırın. Daha fazla bilgi için bkz: [nasıl toocapture klasik bir Linux sanal makinesini görüntü olarak](capture-image.md).  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

Bu komutları çalıştırdıktan sonra hello VM görüntüsü kullanımınız için yakalanır ve hello VM silinir. Şimdi bir küme, özel görüntü hazır toodeploy sahip.

### <a name="deploy-a-cluster-with-hello-image"></a>Hello görüntüsü olan bir kümeyi dağıtma
Ortamınız için uygun değerlerle Bash komut dosyası izleyen hello değiştirin ve istemci bilgisayardan çalıştırın. Azure hello VM'ler hello Klasik dağıtım modelinde seri olarak dağıtır çünkü toodeploy hello bu komut dosyasını önerilen sekiz A9 Vm'lerde birkaç dakika sürer.

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>CentOS HPC Kümesi için ilgili önemli noktalar
Tooset birini hello Azure Marketi SLES 12 yerine hello CentOS tabanlı HPC görüntüleri için HPC temel alarak kümesi istiyorsanız, önceki bölümde hello hello genel adımları izleyin. Farkları sağlamak ve hello VM yapılandırdığınızda aşağıdaki hello dikkat edin:

- Intel MPI CentOS tabanlı HPC görüntüden sağlanan bir VM üzerinde zaten yüklü.
- Kilit bellek ayarları hello VM'in /etc/security/limits.conf dosyasında zaten eklendi.
- Yakalama için SSH anahtarları hello sağlamanız VM üzerinde oluşturmaz. Merhaba küme dağıttıktan sonra bunun yerine, kullanıcı tabanlı kimlik doğrulaması kurma öneririz. Daha fazla bilgi için bölümden hello bakın.  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>Merhaba kümede passwordless SSH güven ayarlama
CentOS tabanlı HPC küme üzerinde hello işlem düğümleri arasında güven kurulması için iki yöntem vardır: ana bilgisayar tabanlı kimlik doğrulama ve kullanıcı tabanlı kimlik doğrulaması. Ana bilgisayar tabanlı kimlik doğrulaması bu makalenin kapsamı dışında hello ve genellikle dağıtımı sırasında bir uzantı komut dosyası yapılmalıdır. Kullanıcı tabanlı kimlik doğrulaması dağıtımdan sonra güven kurulması için uygundur ve işlem hello kümedeki düğümler hello oluşturma ve SSH anahtarları hello arasında paylaşılmasını gerektirir. Bu yöntem genellikle passwordless SSH oturumu açma olarak bilinen ve MPI işlerini çalıştırma durumlarda gereklidir.

Merhaba topluluktan katkıda bulunan bir örnek komut dosyası edinilebilir [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) CentOS tabanlı HPC küme tooenable kolay kullanıcı kimlik doğrulaması. Karşıdan yükle ve hello aşağıdaki adımları kullanarak bu betiği kullanın. Ayrıca, bu komut dosyasını değiştirin veya herhangi diğer yöntemi tooestablish passwordless SSH kimlik doğrulaması hello küme işlem düğümleri arasında kullanabilirsiniz.

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

toorun hello betik tooknow hello öneki için alt ağ IP adresi gerekir. Merhaba önek hello hello küme düğümlerinden biri üzerinde aşağıdaki komutu çalıştırarak alın. Çıktı gibi 10.1.3.5 görünmelidir ve hello önek hello 10.1.3 bölümüdür.

    ifconfig eth0 | grep -w inet | awk '{print $2}'

Artık üç parametrelerini kullanarak hello komut dosyasını çalıştırın: hello hello ortak kullanıcı adına işlem düğümlerini, hello ortak parola hello bu kullanıcıya işlem düğümlerini ve hello alt ağ önek döndürüldü hello önceki komutu.

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

Bu komut dosyası izleyen hello:

* Merhaba konak düğümde .ssh, passwordless oturum açma için gerekli olduğu adlı bir dizin oluşturur.
* Merhaba kümedeki herhangi bir düğümden passwordless oturum açma tooallow oturum açma bildirir hello .ssh dizininde bir yapılandırma dosyası oluşturur.
* Merhaba düğüm adı ve düğüm IP adresleri hello kümedeki tüm hello düğümler için içeren dosyaları oluşturur. Daha sonra başvurmak için Hello betiği çalıştırdıktan sonra bu dosyaları bırakılır.
* (Merhaba ana bilgisayar düğümü dahil) her küme düğümü için özel ve ortak anahtar çifti oluşturur ve girişleri hello authorized_keys dosyasında oluşturur.

> [!WARNING]
> Bu komut dosyasını çalıştıran bir güvenlik riski oluşturabilir. Ortak anahtar bilgileri ~/.ssh Hello değil dağıtılmış emin olun.
>
>

## <a name="configure-intel-mpi"></a>Intel MPI yapılandırın
Azure Linux RDMA toorun MPI uygulamaları, tooconfigure gereken belirli ortam değişkenleri belirli tooIntel MPI. Bir uygulama bir örnek komut dosyası tooconfigure Bash hello gerekli değişkenleri toorun aşağıdadır. Merhaba yolu toompivars.sh Intel MPI yüklemeniz için gerektiği gibi değiştirin.

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

Merhaba ana bilgisayar dosyası Hello biçimi aşağıdaki gibidir. Kümedeki her düğüm için bir satır ekleyin. Hello sanal ağdan özel IP adresleri daha önce tanımlanan DNS adlarını belirtin. Örneğin, IP adresleriyle 10.32.0.1 ve 10.32.0.2 için iki ana hello dosya hello aşağıdakileri içerir:

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>Temel iki düğümlü bir küme üzerinde MPI çalıştırın
İlk zaten yapmadıysanız, Intel MPI hello ortamını ayarlama.

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>MPI komutunu çalıştırın
Bir MPI komutu MPI düzgün bir şekilde yüklendiğini ve iletişim kurabilir hello işlem düğümleri tooshow birinde en az iki işlem düğümleri arasında çalıştırın. Merhaba aşağıdaki **mpirun** komutu çalıştırır hello **ana bilgisayar adı** iki düğüm üzerinde komutu.

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
Çıktı için giriş olarak geçirilen tüm hello düğümlerinin hello adlarını listelenmelidir `-hosts`. Örneğin, bir **mpirun** iki düğüm komutuyla hello aşağıdaki gibi bir çıktı döndürür:

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>MPI Kıyaslama çalıştırması
Intel MPI komutu aşağıdaki hello pingpong Kıyaslama tooverify hello küme yapılandırması ve bağlantı toohello RDMA ağ çalışır.

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

İki düğümle bir çalışma kümesinde hello aşağıdaki gibi bir çıktı görmeniz gerekir. Hello Azure RDMA ağ üzerinde gecikme düzeyinde veya altında 3 mikrosaniye too512 bayt ileti boyutları için bekler.

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>Sonraki adımlar
* Dağıtın ve Linux MPI uygulamaları Linux kümenizde çalıştırın.
* Merhaba bkz [Intel MPI kitaplığı belgeleri](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) Intel MPI hakkında yönergeler için.
* Deneyin bir [hızlı başlatma şablonunu](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate bir Intel Lustre küme CentOS tabanlı HPC görüntüsünü kullanarak. Ayrıntılar için bkz [dağıtma Intel bulut Edition için Microsoft Azure üzerinde Lustre](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).
