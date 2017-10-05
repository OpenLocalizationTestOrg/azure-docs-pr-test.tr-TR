---
title: "Microsoft Azure SUSE Linux VM'ler üzerinde SAP NetWeaver test etme | Microsoft Docs"
description: "Microsoft Azure SUSE Linux VM’lerde SAP NetWeaver’ı test etme"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 118b56376eace80788a20625497849181ad2e253
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>Microsoft Azure SUSE Linux VM’lerde SAP NetWeaver’ı çalıştırma
Bu makalede, çeşitli Microsoft Azure SUSE Linux sanal makineleri (VM'ler) SAP NetWeaver çalıştırırken göz önünde bulundurmanız gerekenler açıklanmaktadır. 19 Mayıs 2016 itibariyle SAP NetWeaver resmi olarak SUSE Linux sanal makineleri Azure üzerinde desteklenir. Linux sürümleri, SAP çekirdek sürümleri vb. ile ilgili tüm ayrıntıları SAP Not 1928533 bulunabilir "Azure SAP uygulamaları: desteklenen ürünleriyle ve Azure VM türler".
Linux VM'ler üzerinde SAP hakkında daha fazla belge şurada bulunabilir: [Linux sanal makineleri (VM'ler) üzerinde kullanarak SAP](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Aşağıdaki bilgiler, bazı olası Tuzaklar önlemenize yardımcı olmalıdır.

## <a name="suse-images-on-azure-for-running-sap"></a>SAP çalıştırmak için SUSE görüntülerinde Azure
SAP NetWeaver Azure üzerinde çalışan, yalnızca SUSE Linux Enterprise Server SLES 12 (SPx) kullanın - SAP Not 1928533 Ayrıca bkz. Azure Market ("SLES 11 SP3 SAP CAL için") içinde bir özel SUSE görüntüsü olduğundan, ancak bu genel kullanım için tasarlanmamıştır. Bu görüntü için ayrılmış olduğundan kullanmayın [SAP bulut Gereci Kitaplığı](https://cal.sap.com/) çözümü.  

Tüm yeni testleri ve Azure üzerinde yüklemeleri için Azure Kaynak Yöneticisi'ni kullanmanız gerekir. SUSE SLES görüntüler ve sürümler için Azure PowerShell veya Azure komut satırı arabirimi (CLI) kullanarak aramak için aşağıdaki komutları kullanın. Ardından çıktı, örneğin, işletim sistemi görüntüsü yeni bir SUSE Linux VM dağıtmak için JSON şablonunu tanımlamak için kullanabilirsiniz.
Azure PowerShell sürüm 1.0.1 için geçerli ve daha sonra bu PowerShell komutlarını verilmiştir.

SAP yüklemeleri için standart SLES görüntüleri kullanmak hala mümkün olmakla birlikte yeni SLES Azure görüntü Galerisi üzerinde şu anda kullanılabilir olan SAP görüntüleri kullanmak için önermiştir. Karşılık gelen üzerinde bu görüntüleri hakkında daha fazla bilgi bulunabilir [Azure Marketi sayfa]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) veya [SUSE SSS web sayfası SAP SLES hakkında]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


* SUSE dahil olmak üzere mevcut yayımcılar arayın:
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* SUSE varolan sunduğu arayın:
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* SUSE SLES teklifleri arayın:
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* SLES SKU belirli bir sürümünü arayın:
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>WALinuxAgent SUSE VM ile yükleme
WALinuxAgent adlı Aracısı Azure Marketi SLES görüntülerinde bir parçasıdır. (Örneğin bir SLES işletim sistemi sanal sabit disk (VHD) şirket içi karşıya yüklenirken el ile) yükleme hakkında daha fazla bilgi için bkz:

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Azure](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>SAP artırılmış"izleme"
SAP artırılmış"izleme" SAP Azure üzerinde çalıştırmak için zorunlu bir önkoşuldur. SAP ayrıntılarında 2191498 "SAP Linux ile Azure: Gelişmiş izleme" Not denetleyin.

## <a name="attaching-azure-data-disks-to-an-azure-linux-vm"></a>Azure veri diskleri için Azure Linux VM'de ekleme
Hiçbir zaman cihaz kimliğini kullanarak Azure Linux VM'de bağlama Azure veri diskleri gerekir Bunun yerine, evrensel benzersiz tanımlayıcı (UUID) kullanın. Bağlama Azure veri diskleri için grafik araçları örneğin kullanırken dikkatli olun. /Etc/fstab yer alan girişleri denetleyin.

Cihaz kimliği değişiklik yapmış olabilir ve Azure VM önyükleme işleminin ardından askıda bir sorundur. Sorunu azaltmak için /etc/fstab içinde nofail parametre ekleyebilirsiniz. Ancak, uygulamaları önce bağlama noktası olarak kullanabilirsiniz ve bir dış Azure veri diski önyükleme sırasında bağlı olmadığı durumda kök dosya sistemine yazma çünkü ile nofail dikkatli olun.

Bağlama UUID aracılığıyla tek özel durum aşağıdaki bölümde açıklandığı gibi sorun giderme amacıyla, işletim sistemi diski ekleniyor.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Artık erişilemiyor SUSE VM sorunlarını giderme
Burada (disklerin bağlanması için ilgili Örneğin, bir hata ile) önyükleme işleminde SUSE VM Azure üzerinde askıda durumlar olabilir. Bu sorunu Azure portalında Azure sanal makineleri v2 için önyükleme tanılaması özelliğini kullanarak doğrulayabilirsiniz. Daha fazla bilgi için bkz: [önyükleme tanılama](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).

Sorunu çözmek için bir işletim sistemi diski Azure ile ilgili başka bir SUSE VM bozuk sanal makineden iliştirmek için yoludur. Ardından sonraki bölümde açıklandığı gibi /etc/fstab düzenleme veya ağ udev kuralları, kaldırma gibi istediğiniz değişiklikleri yapın.

Dikkate alınması gereken önemli bir unsur vardır. Aynı Azure Market görüntüsünden (örneğin, SLES 11 SP4) birkaç SUSE VM'ler dağıtma her zaman aynı UUID ile takılması işletim sistemi diski neden olur. Bu nedenle, aynı Azure Market görüntüsünü kullanarak dağıtılan farklı bir VM'den bir işletim sistemi diski eklemek için UUID'si kullanılarak içinde iki özdeş UUID'ler neden olur. Bu sorunlara neden olur ve sorun giderme için amacı VM yerine özgün bir eklendi ve bozuk işletim sistemi diskinden aslında başlatılır anlamına gelebilir.

Bu durumu önlemek için iki yolu vardır:

* Sorun giderme VM (örneğin, SLES 11 SPx SLES 12 yerine) için farklı bir Azure Market görüntüsü kullanın.
* UUID--Kullan'ı kullanarak başka bir sanal makineden bozuk işletim sistemi diski VM'ye olmayan başka bir konuda.

## <a name="uploading-a-suse-vm-from-on-premises-to-azure"></a>Şirket içi bir SUSE VM Azure karşıya yükleme
Şirket içi bir SUSE VM Azure yüklemek için aşağıdaki adımları açıklaması için bkz: [SLES veya openSUSE bir sanal makine için Azure hazırlama](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bir VM sonunda deprovision adım olmadan (örneğin, Canlı var olan bir SAP yüklemesi, aynı zamanda için ana bilgisayar adı) karşıya yüklemek istiyorsanız, aşağıdaki öğeleri denetleyin:

* İşletim sistemi diski UUID ve cihaz kimliğini kullanarak bağlandığından emin olun Yalnızca /etc/fstab içinde için UUID değiştirme işletim sistemi diski için yeterli değil. Ayrıca, /boot/grub/menu.lst düzenleyerek veya YaST aracılığıyla önyükleyici uyum unutmayın.
* VHDX biçimi için SUSE işletim sistemi diski kullanıyorsanız ve Azure'a yüklemek için VHD'ye Dönüştür, ağ aygıtı için eth1 eth0 değiştirmek olasılığı yüksektir. Azure üzerinde daha sonra önyüklemesi sırasında sorunları önlemek için geri eth0 için açıklandığı gibi değiştirin [eth0 içinde düzeltme klonlanmış SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

Ne makalesinde açıklanan ek olarak, bu kaldırmanızı öneririz:

   /lib/udev/Rules.d/75-persistent-NET-Generator.Rules

Aracı birden çok NIC olmadığı sürece, olası sorunları önlemenize yardımcı olmak için Azure Linux (waagent) de yükleyebilirsiniz.

## <a name="deploying-a-suse-vm-on-azure"></a>Azure üzerinde bir SUSE VM dağıtma
Yeni Azure Resource Manager modelinde JSON şablon dosyalarını kullanarak yeni SUSE VM'ler oluşturmanız gerekir. JSON şablon dosyası oluşturulduktan sonra PowerShell alternatif olarak aşağıdaki CLI komutunu kullanarak VM dağıtabilirsiniz:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
JSON şablon dosyaları hakkında daha fazla ayrıntı için bkz: [Azure Resource Manager şablonları yazma](../../../resource-group-authoring-templates.md) ve [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).

CLI ve Azure Resource Manager hakkında daha fazla ayrıntı için [Mac, Linux ve Windows Azure Resource Manager ile Azure CLI kullanılmaya](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>SAP lisans ve donanım anahtarı
Resmi SAP Azure sertifika için yeni bir mekanizma SAP lisansını kullanılan SAP donanım anahtarı hesaplamak için sunulmuştur. SAP çekirdek yapmak için uyarlanmış olması gerekiyordu bunu kullanın. Linux için önceki SAP çekirdek sürümleri, bu kod değişikliği içermiyordu. Bu nedenle, bazı durumlarda (örneğin, Azure VM yeniden boyutlandırma), SAP donanım anahtarı değiştirildi ve SAP lisans edildi artık geçerli. Bu son SAP Linux tekrar çözülür. Ayrıntılar için lütfen SAP Not 1928533 denetleyin.

## <a name="suse-sapconf-package--tuned-adm"></a>SUSE sapconf paket / ayarlanmış adm
SUSE "SAP özgü ayarları kümesini yöneten sapconf" adlı bir paketi sağlar. Bu paket yaptığı ve nasıl yüklenmesi ve kullanılması hakkında daha fazla ayrıntı için bkz: [sapconf SAP sistemleri çalıştırmak için bir SUSE Linux Enterprise Server hazırlamak için kullanma](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) ve [sapconf nedir ya da SUSE Linux Enterprise hazırlama SAP sistemlerini çalıştıran sunucu? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

Bu sırada sapconf - ayarlanmış adm. yerini alacak yeni bir aracı yok Bir aşağıdaki iki bağlantıları aşağıdaki bu araç hakkında daha fazla ayrıntı bulabilirsiniz.

Olarak ayarlanmış adm profili sap hana ilgili SLES belgeler bulunabilir [burada](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

SAP iş yükleri ile ayarlanmış-adm - ayarlama sistemleri bulunabilir [burada](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) bölümde 6.2

## <a name="nfs-share-in-distributed-sap-installations"></a>Dağıtılmış SAP yüklemelerde NFS paylaşım
Veritabanı ve SAP uygulama sunucuları ayrı Vm'lerde--yüklemek istediğiniz bir dağıtılmış yükleme--Örneğin, varsa, ağ dosya sistemi (NFS) aracılığıyla /sapmnt dizin paylaşabilirsiniz. NFS paylaşım /sapmnt için oluşturduktan sonra yükleme adımlarını sorunları varsa, "no_root_squash" paylaşım için ayarlanmış olup olmadığını denetleyin.

## <a name="logical-volumes"></a>Mantıksal birimler
Bir büyük bir mantıksal birim (örneğin, SAP veritabanı) birden çok Azure veri disklere gerekirse geçmişte bu lvm tam henüz Azure üzerinde doğrulanmış değildi olarak mdadm kullanmanız önerilir. Azure üzerinde Linux RAID mdadm kullanarak ayarlama hakkında bilgi edinmek için bkz: [yazılım RAID Linux üzerinde yapılandırma](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Başlangıç Mayıs 2016 itibariyle bu arada da lvm tamamen Azure üzerinde desteklenir ve mdadm alternatif olarak kullanılabilir. Azure üzerinde lvm ilgili ek bilgi için bkz: [yapılandırma LVM azure'da bir Linux VM üzerinde](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Azure SUSE deposu
Standart Azure SUSE depoya erişim ile ilgili bir sorun varsa, sıfırlamak için basit bir komut kullanabilirsiniz. Bir Azure bölgesinde özel bir işletim sistemi görüntüsü oluşturup bu özel işletim sistemi yansımasını temel alan yeni sanal makineleri dağıtmak istediğiniz farklı bir bölgeye görüntüyü kopyalamak isterseniz bu durum oluşabilir. Yalnızca VM içinde aşağıdaki komutu çalıştırın:

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Gnome Masaüstü
Gnome Masaüstü'nü kullanarak bir SAP GUI dahil olmak üzere tek bir VM içinde--tam bir SAP demo sistemi yüklemek istiyorsanız, Azure SLES görüntülerinde yüklemek için bu ipucu tarayıcı ve SAP Yönetim Konsolu--kullanın:

   SLES 11 için:

   ```
   zypper in -t pattern gnome
   ```

   SLES 12 için:

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-the-cloud"></a>Oracle Linux bulutta SAP desteği
Sanallaştırılmış ortamlarda Oracle Linux üzerinde gelen destek bir kısıtlama yoktur. Bu bir Azure özgü konu olmamasına karşın, anlamak önemlidir. SAP, Oracle SUSE veya Red Hat gibi Azure genel bulutunda desteklemez. Bu konuda tartışmak için Oracle doğrudan başvurun.

