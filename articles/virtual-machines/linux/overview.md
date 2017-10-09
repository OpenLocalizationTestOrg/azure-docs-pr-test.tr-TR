---
title: "Linux VM'ler için Azure'da aaaOverview | Microsoft Docs"
description: "Linux sanal makineleri ile Azure işlem, depolama ve ağ hizmetlerini açıklar."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure ve Linux
Microsoft Azure koleksiyonudur büyüyen tümleşik genel bulut, depolama, ağ, mobil analytics, sanal makineler, veritabanları dahil olmak üzere Hizmetleri ve web&mdash;çözümlerinizi barındırma için idealdir.  Microsoft Azure - tooinvest şirket içi donanıma gerek kalmadan istediğiniz zaman kullandıklarınız için tooonly ödeme sağlayan ölçeklenebilir bir bilgisayar platformu sağlar.  Azure çözümlerinizi yukarı tooscale yüklenir ve toowhatever ölçek genişletme tooservice hello istemcileriniz ihtiyaçlarını gerektirmez hazırdır.

Hakkında bilginiz varsa, Amazon'in çeşitli özelliklerini hello inceleyin AWS, Azure vs AWS hello [tanımı eşleme belge](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/).

## <a name="regions"></a>Bölgeler
Microsoft Azure kaynakları Merhaba Dünya birden çok coğrafi bölgeler arasında dağıtılır.  "Bölge" tek bir coğrafi alan birden çok veri merkezlerinde temsil eder.  Genel olarak kullanılabilir 34 bölgeler Merhaba Dünya duyurdu bir ek 4 bölgesiyle sahibiz. Tooexpand bizim genel kapsamı - sürmektedir çünkü bölgelerin güncelleştirilmiş listesini var ve yeni duyurdu korur.

* [Azure Bölgeleri](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Kullanılabilirlik
Merhaba VM tüm diskler için premium depolama ile dağıttığınız bir endüstri başında tek örnek sanal makine % 99,9 Hizmet düzeyi sözleşmesi sağlanan duyurdu.  Dağıtım tooqualify bizim standart %99,95 sırayla VM hizmet düzeyi sözleşmesi hala ihtiyacınız toodeploy İş yükünüzün bir kullanılabilirlik kümesi içinde çalışan iki veya daha fazla sanal makineler. Bu, sanal makineleri birden çok hata etki alanlarını bizim veri merkezlerinde dağıtılmış yanı sıra farklı bakım pencereleri konaklarla üzerine dağıtılan garanti eder. Merhaba tam [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) açıklayan bir bütün olarak Azure kullanılabilirliğini garanti hello.

## <a name="managed-disks"></a>Yönetilen Diskler

Yönetilen disklerde tanıtıcıları Azure depolama hesap oluşturma ve hello arka planda yönetimini ve tooworry hello hello depolama hesabı ölçeklenebilirlik sınırları hakkında sahip olmayan sağlar. Yalnızca hello disk boyutu ve hello performans Katmanı (standart veya Premium) belirtin ve Azure oluşturur ve hello disk tarafından yönetilir. Disk ekleyin veya hello VM yukarı ve aşağı doğru ölçeklendirme gibi bile, kullanılan hello depolama hakkında tooworry yok. Yeni VM oluşturuyorsanız [hello Azure CLI 2.0 kullanmak](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ya da Azure portal toocreate VM'ler yönetilen işletim sistemi ve veri diskleri hello. Yönetilmeyen disklerle VM'ler varsa [yönetilen disklerle yedeklenen, VM'ler toobe Dönüştür](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Ayrıca, kendi özel görüntülerinizi Azure bölgesi başına bir depolama hesabındaki yönetmek ve toocreate yüzlerce VM'lerin hello içinde kullanabilirsiniz aynı abonelik. Yönetilen diskler hakkında daha fazla bilgi için lütfen hello bakın [yönetilen diskleri genel bakış](../windows/managed-disks-overview.md).

## <a name="azure-virtual-machines--instances"></a>Azure sanal makineleri & örnekleri
Microsoft Azure, sağlanan ve çeşitli iş ortakları tarafından korunan popüler Linux dağıtımları sayısı çalıştırılmasını destekler.  Red Hat Enterprise, CentOS, Debian, Ubuntu, CoreOS, RancherOS, FreeBSD ve daha fazla hello Azure Marketi gibi dağıtımları bulacaksınız. Biz etkin olarak çeşitli Linux toplulukları tooadd ile daha da fazla özellikleri iş toohello [Azure destekli Linux Distro'lar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) listesi.

Tercih edilen Linux distro tercih hello Galerisi'nde mevcut değilse, "kendi Linux getirebilir" VM tarafından [oluşturma ve Azure Linux VHD'yi karşıya](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Azure sanal makineleri toodeploy çözümleri Çevik bir şekilde bilgi işlem çok çeşitli izin verin. Neredeyse tüm iş yükü ve neredeyse tüm işletim sistemi - Windows, Linux, üzerinde herhangi bir dil dağıtabilir veya özel bir tane büyüyen iş ortakları listemiz herhangi birinde oluşturdu. Hala ne aradığınız görmüyorum?  Endişelenmeyin - ayrıca şirket içi kendi görüntülerinizden kullanıma sunabilirsiniz.

## <a name="vm-sizes"></a>VM boyutları
Azure'da VM dağıttığınızda, tooselect uygun tooyour iş yükü olan bizim dizi boyutları biri içinde bir VM boyutu adımıdır. Merhaba boyutu hello işleme güç, bellek ve depolama kapasitesini hello sanal makinenin de etkiler. VM çalıştıran ve ayrılan kaynakları tüketen zaman hello hello miktarına göre faturalandırılır. Tam bir listesi [sanal makinelerin boyutları](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Burada, bir VM boyutu (A, D, DS, G ve GS) bizim serisi birini seçmek için temel bazı yönergeler bulunmaktadır.
* A-series VM'ler giriş seviyesi VM'ler hafif iş yükleri ve geliştirme ve Test senaryoları için fiyatlandırılır bizim değerlerdir. Bunlar tüm bölgelerde geniş çapta kullanılabilir ve bağlanabilir ve tüm standart kaynakları kullanılabilir toovirtual makineleri kullanın.
* A-series (A8 - A11) özel işlem yoğunluklu yapılandırmaları yüksek performanslı bilgi işlem küme uygulamalar için uygun boyutlarıdır.
* D-serisi VM'ler, daha yüksek işlem gücü ve geçici disk performans talep tasarlanmış toorun uygulamalarıdır. D-serisi VM'ler hello geçici disk için daha hızlı işlemcilerde, daha yüksek bellek çekirdek oranı ve katı hal sürücüsü (SSD) sağlayın.
* Dv2 serisi, bizim D-serisi en son sürümünü Merhaba, daha güçlü bir CPU özellikleri. Merhaba Dv2 serisi CPU yaklaşık %35 hello daha hızlı D-serisi CPU'dur. En son nesil hello üzerinde temel aldığı 2.4 GHz Intel Xeon® E5-2673 v3 (Haskell) işlemci ve hello Intel Turbo artırma teknolojisi 2.0 GHz too3.2 gidebilirsiniz. Merhaba Dv2 serisi sahip D-serisi hello gibi aynı bellek ve disk yapılandırmalarını hello.
* G-serisi VM'ler hello en fazla belleği sunar ve Intel Xeon E5 V3 ailesi işlemcilere sahip konaklarda çalıştırın.

Not: Erişim tooPremium depolama DS serisi ve GS serisi VM'ler sahip - g/ç yoğun iş yükleri için yüksek performanslı, düşük gecikme süreli depolama bizim SSD yedeklenir. Premium Depolama belirli bölgelerde kullanılabilir. Ayrıntılar için bkz.

* [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Otomasyon
tooachieve uygun bir DevOps kültür olan tüm altyapı kodu olmalıdır.  Altyapı tüm hello zaman kolayca olabilir kodda yaşamlarını yeniden (Phoenix sunucuları).  Azure Ansible, Chef, SaltStack ve Puppet gibi tooling tüm hello ana otomasyon ile çalışır.  Ayrıca Azure Otomasyon için kendi araç sahiptir:

* [Azure şablonları](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Azure desteği sunulmadan [bulut init](http://cloud-init.io/) destekleyen çoğu Linux Distro'lar arasında.  Şu anda Canonical'ın Ubuntu VM bulut init varsayılan olarak etkin olan dağıtılır.  Kırmızı şapkalar RHEL, CentOS ve bulut init destekler, ancak Azure hello Fedora görüntüleri RedHat tarafından korunan bulut init yüklü sahip değil.  toouse bulut başlatma RedHat ailesindeki işletim sistemi, bulut yüklü başlatma ile özel bir görüntü oluşturmanız gerekir.

* [Azure Linux VM'ler üzerinde bulut init kullanma](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>Kotalar
Her Azure aboneliği, çok sayıda sanal makineleri projeniz için hello dağıtımını etkileyebilir yerinde varsayılan kota sınırları vardır. Hello geçerli bir abonelik başına temelinde bölge başına 20 VM sınırıdır.  Kota sınırları hızlı bir şekilde oluşturulur ve bir sınır isteyen bir destek bileti dosyalama tarafından kolayca artırın.  Kota sınırları hakkında daha fazla ayrıntı için:

* [Azure aboneliği hizmet sınırları](../../azure-subscription-service-limits.md)

## <a name="partners"></a>İş Ortakları
Microsoft yakından tooensure hello görüntüleri güncelleştirilmiş ve Azure bir çalışma zamanı için en iyi duruma getirilmiş bizim iş ortakları ile çalışmaktadır.  Ortaklarımızın hakkında daha fazla bilgi için Market sayfaları denetleyin.

* Azure - Linux'ta [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE - [Azure Market - SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* RedHat - [Azure Market - RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Kurallı - [Azure Market - Ubuntu Server 16.04 LTS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian - [Azure Market - Debian 8 "Jessie"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD - [Azure Market - FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS - [Azure Market - CoreOS (kararlı)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS - [Azure Market - RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami - [Azure için Bitnami kitaplığı](https://azure.bitnami.com/)
* Mesosphere - [Azure Market - Mesosphere DC/OS Azure ile ilgili](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker - [Azure Market - Docker Swarm ile Azure kapsayıcı hizmeti](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins - [Azure Market - CloudBees Jenkins Platform](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Linux Azure üzerinde ile çalışmaya başlama
bir Azure hesabı, hello Azure CLI yüklenmiş ve SSH ortak ve özel anahtar çiftini gerek Azure kullanarak toobegin.

### <a name="sign-up-for-an-account"></a>Hesap için kaydolma
hello Azure bulut kullanarak hello ilk toosign bir Azure hesabı için bir adımdır.  Toohello Git [Azure hesaba kaydolmayı](https://azure.microsoft.com/pricing/free-trial/) sayfasında tooget başlatıldı.

### <a name="install-hello-cli"></a>Merhaba CLI yükleme
Yeni Azure hesabınızla, hemen hello web tabanlı yönetim paneli Azure portalını kullanmaya başlayabilirsiniz.  Merhaba komut satırı aracılığıyla toomanage hello Azure bulut, yüklediğiniz hello `azure-cli`.  Merhaba yüklemek [Azure CLI 2.0](/cli/azure/install-azure-cli) Mac veya Linux istasyonunuzda.

### <a name="create-an-ssh-key-pair"></a>SSH anahtar çifti oluşturma
Şimdi bir Azure hesabı, hello Azure web portalı ve Azure CLI hello sahiptir.  Merhaba sonraki toocreate parola kullanmadan, kullanılan tooSSH Linux içine SSH anahtar çiftini adımdır.  [Linux ve Mac'de SSH anahtarları oluşturma](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable parolasız ve daha iyi güvenlik.

### <a name="create-a-vm-using-hello-cli"></a>Merhaba CLI kullanarak bir VM oluşturma
Bir Linux VM oluşturma hello CLI hızlı şekilde toodeploy bırakma hello terminal çalıştığınız olmadan bir VM kullanmaktır.  Her şeyi hello web portalında belirtebilirsiniz, bir komut satırı bayrağı veya anahtar kullanılabilir.  

* [Merhaba CLI kullanarak bir Linux VM oluşturma](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Merhaba Portalı'nda bir VM oluşturma
Hello Azure web Portalı'nda bir Linux VM oluşturma bir yoldur tooeasily noktası ve geçişli tıklatma hello çeşitli seçenekler tooget tooa dağıtım.  Komut satırı bayrakları veya anahtarları kullanmak yerine, mümkün tooview iyi web düzeni çeşitli seçenekler ve ayarlar şunlardır.  Merhaba komut satırı arabirimi kullanılabilir her şeyi da hello Portalı'nda mevcuttur.

* [Merhaba portalı kullanarak bir Linux VM oluşturma](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>SSH olmadan parola kullanarak oturum açma
Merhaba VM artık Azure üzerinde çalışan ve içinde hazır toolog demektir.  SSH aracılığıyla parolaları toolog içinde kullanarak güvenli ve zaman alıcıdır.  SSH anahtarları kullanılarak olduğu hello en güvenli yolu ve ayrıca hello hızlı şekilde toologin.  Linux VM hello portalı veya hello CLI aracılığıyla oluşturduğunuz, iki kimlik doğrulama seçeneğiniz vardır.  SSH için bir parola seçerseniz Azure hello VM tooallow oturumu aracılığıyla parolaları yapılandırır.  Bir SSH ortak anahtarı toouse seçerseniz Azure hello VM yapılandırır tooonly izin SSH aracılığıyla oturum anahtarları ve parola oturum açmalar devre dışı bırakır. SSH ortak anahtarı seçeneği hello hello portalında veya CLI VM oluşturma sırasında hello toosecure SSH anahtar oturum açmalar, veren tarafından yalnızca, bir Linux VM kullanın.

## <a name="related-azure-components"></a>İlişkili Azure bileşenleri
## <a name="storage"></a>Depolama
* [Giriş tooMicrosoft Azure depolama](../../storage/common/storage-introduction.md)
* [Disk tooa hello azure CLI kullanarak Linux VM ekleme](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Nasıl tooattach bir veri diski hello Azure portal'ın tooa Linux VM](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Ağ
* [Sanal ağ genel bakış](../../virtual-network/virtual-networks-overview.md)
* [Azure’da IP adresleri](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Açılan bağlantı noktaları tooa Azure Linux VM'de](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tam etki alanı adı hello Azure portal oluşturma](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>Kapsayıcılar
* [Sanal makineler ve Azure kapsayıcı](containers.md)
* [Azure kapsayıcı hizmeti giriş](../../container-service/container-service-intro.md)
* [Azure Container Service kümesi dağıtma](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>Sonraki adımlar
Artık Azure üzerinde Linux genel bir bakış vardır.  Hello sonraki adımı toodive içinde ve birkaç VM'yi oluşturun!

* [Örnek komut dosyalarını ortak görevler için bizim gittikçe artan AzureCLI keşfedin](cli-samples.md)
