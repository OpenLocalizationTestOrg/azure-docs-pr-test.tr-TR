---
title: "Microsoft Azure SUSE Linux sanal makineleri üzerinde SAP NetWeaver aaaTesting | Microsoft Docs"
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
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>Microsoft Azure SUSE Linux VM’lerde SAP NetWeaver’ı çalıştırma
Bu makalede, Microsoft Azure SUSE Linux sanal makineleri (VM'ler) SAP NetWeaver çalıştırırken çeşitli şeyler tooconsider açıklanmaktadır. 19 Mayıs 2016 itibariyle SAP NetWeaver resmi olarak SUSE Linux sanal makineleri Azure üzerinde desteklenir. Linux sürümleri, SAP çekirdek sürümleri vb. ile ilgili tüm ayrıntıları SAP Not 1928533 bulunabilir "Azure SAP uygulamaları: desteklenen ürünleriyle ve Azure VM türler".
Linux VM'ler üzerinde SAP hakkında daha fazla belge şurada bulunabilir: [Linux sanal makineleri (VM'ler) üzerinde kullanarak SAP](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Aşağıdaki bilgilerle hello bazı olası Tuzaklar önlemenize yardımcı olmalıdır.

## <a name="suse-images-on-azure-for-running-sap"></a>SAP çalıştırmak için SUSE görüntülerinde Azure
SAP NetWeaver Azure üzerinde çalışan, yalnızca SUSE Linux Enterprise Server SLES 12 (SPx) kullanın - SAP Not 1928533 Ayrıca bkz. Hello Azure Marketi ("SLES 11 SP3 SAP CAL için") içinde bir özel SUSE görüntüsü olduğundan, ancak bu genel kullanım için tasarlanmamıştır. Hello için ayrılmış olduğundan bu görüntüyü kullanmayın [SAP bulut Gereci Kitaplığı](https://cal.sap.com/) çözümü.  

Tüm yeni testleri ve Azure üzerinde yüklemeleri için Azure Kaynak Yöneticisi'ni kullanmanız gerekir. toolook SUSE SLES görüntüler ve Azure PowerShell veya hello Azure komut satırı arabirimi (CLI), aşağıdaki komutları kullanın hello kullanarak sürümleri için. Daha sonra hello çıktı, örneğin, toodefine hello işletim sistemi görüntüsüne yeni bir SUSE Linux VM dağıtmak için bir JSON şablonu kullanabilirsiniz.
Azure PowerShell sürüm 1.0.1 için geçerli ve daha sonra bu PowerShell komutlarını verilmiştir.

Hala olası toouse hello SAP yüklemeleri için standart SLES görüntüleri ederken önerilen toomake kullanımını hello yeni SLES kullanılabilir olan SAP görüntüleri galeri şimdi hello Azure üzerinde görüntü için. Merhaba karşılık gelen üzerinde bu görüntüleri hakkında daha fazla bilgi bulunabilir [Azure Marketi sayfa]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) veya hello [SUSE SSS web sayfası SAP SLES hakkında]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


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
Merhaba Aracısı WALinuxAgent adlı hello Azure Marketi hello SLES görüntüleri bir parçasıdır. (Örneğin bir SLES işletim sistemi sanal sabit disk (VHD) şirket içi karşıya yüklenirken el ile) yükleme hakkında daha fazla bilgi için bkz:

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Azure](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>SAP artırılmış"izleme"
SAP artırılmış"izleme" zorunlu bir önkoşul toorun Azure üzerinde SAP olur. SAP ayrıntılarında 2191498 "SAP Linux ile Azure: Gelişmiş izleme" Not denetleyin.

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>Azure veri diskleri tooan Azure Linux VM ekleme
Azure veri diskleri tooan Azure Linux VM hello cihaz kimliğini kullanarak hiçbir zaman bağlamanız Bunun yerine, hello evrensel benzersiz tanımlayıcı (UUID) kullanın. Grafik araçları toomount Azure veri diski, örneğin kullanırken dikkatli olun. /Etc/fstab Hello girişlerini denetleyin.

Merhaba hello cihaz kimliği değişiklik yapmış olabilir ve hello Azure VM hello önyükleme işleminde telefonu bir sorundur. toomitigate hello sorunu /etc/fstab içinde hello nofail parametre ekleyebilirsiniz. Ancak, uygulamaları önce hello bağlama noktası olarak kullanabilirsiniz ve bir dış Azure veri diski hello önyükleme sırasında bağlı olmadığı durumda hello kök dosya sistemine yazma çünkü ile nofail dikkatli olun.

Merhaba tek özel durum toomounting UUID aracılığıyla bölümden hello açıklandığı gibi sorun giderme amacıyla, işletim sistemi diski ekleniyor.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Artık erişilemiyor SUSE VM sorunlarını giderme
Burada SUSE VM azure'da hello önyükleme işleminde (disklerin bağlanması için ilgili Örneğin, bir hata ile) askıda kalır durumlar olabilir. Bu sorunu Azure sanal makineleri v2'hello Azure portal'hello önyükleme Tanılama özelliğini kullanarak doğrulayabilirsiniz. Daha fazla bilgi için bkz: [önyükleme tanılama](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).

Tek yönlü toosolve hello tooattach hello OS hello diskten VM tooanother Azure SUSE VM zarar görmüş bir sorundur. Ardından hello sonraki bölümde açıklandığı gibi /etc/fstab düzenleme veya ağ udev kuralları, kaldırma gibi istediğiniz değişiklikleri yapın.

Bir önemli şey tooconsider yoktur. Merhaba aynı Azure Market görüntüsü (örneğin, SLES 11 SP4) neden olan birkaç SUSE Vm'lerden dağıtma hello işletim sistemi disk tooalways hello tarafından oluşturulmuş aynı UUID'si. Bu nedenle, hello UUID tooattach aynı Azure Market görüntüsü içinde iki özdeş UUID'ler sonuçlanır hello kullanılarak dağıtılan farklı bir VM OS diskten kullanma. Bu sorunlara neden olur ve hello sorun giderme için amacı VM aslında bağlı hello önyükleme yapmaz ve yerine bozuk işletim sistemi diski hello özgün anlamına gelebilir.

Vardır iki yolu tooavoid bu:

* VM (örneğin, SLES 11 SPx SLES 12 yerine) sorunlarını giderme hello için farklı bir Azure Market görüntüsü kullanın.
* UUID--Kullan'ı kullanarak başka bir sanal makineden bozuk hello işletim sistemi diski VM'ye yok başka bir konuda.

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>Şirket içi tooAzure SUSE VM'den karşıya yükleme
Merhaba adımları tooupload şirket içi tooAzure SUSE VM'den açıklaması için bkz: [SLES veya openSUSE bir sanal makine için Azure hazırlama](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

VM hello deprovision olmadan (örneğin, var olan bir SAP yüklemesi tookeep yanı sıra hello ana bilgisayar adı) hello sonunda adım tooupload istiyorsanız, aşağıdaki öğelerindeki hello denetleyin:

* Bu hello işletim sistemi diski UUID ve değil hello cihaz kimliğini kullanarak bağlandığından emin olun Yalnızca /etc/fstab içinde tooUUID değiştirme hello işletim sistemi diski için yeterli değil. Ayrıca, tooadapt hello önyükleme yükleyicisi /boot/grub/menu.lst düzenleyerek veya YaST aracılığıyla unutmayın.
* Merhaba SUSE işletim sistemi diski için hello VHDX biçimi kullanıyorsanız ve tooAzure yüklemeyle tooVHD dönüştürmek, o hello ağ aygıtı eth0 tooeth1 değiştirecek olasılığı yüksektir. Azure üzerinde daha sonra önyükleme yaparken tooavoid sorunları açıklandığı gibi geri tooeth0 değiştirme [eth0 içinde düzeltme klonlanmış SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

Ayrıca toowhat'ın hello makalesinde açıklanan, bu kaldırmanızı öneririz:

   /lib/udev/Rules.d/75-persistent-NET-Generator.Rules

Birden çok NIC olmadığı sürece hello Azure Linux Aracısı'nı (waagent) toohelp olası sorunları önlemek de yükleyebilirsiniz.

## <a name="deploying-a-suse-vm-on-azure"></a>Azure üzerinde bir SUSE VM dağıtma
JSON şablon dosyaları hello yeni Azure Resource Manager modelini kullanarak yeni SUSE VM'ler oluşturmanız gerekir. Merhaba JSON şablon dosyası oluşturulduktan sonra CLI komut bir alternatif tooPowerShell olarak aşağıdaki hello kullanarak hello VM dağıtabilirsiniz:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
JSON şablon dosyaları hakkında daha fazla ayrıntı için bkz: [Azure Resource Manager şablonları yazma](../../../resource-group-authoring-templates.md) ve [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).

CLI ve Azure Resource Manager hakkında daha fazla ayrıntı için [kullanım hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>SAP lisans ve donanım anahtarı
Merhaba resmi SAP Azure sertifika için yeni bir mekanizma hello SAP lisansını kullanılan sunulan toocalculate hello SAP donanım anahtarı oluştu. Merhaba SAP çekirdek uyarlanan toobe toomake kullanımını bu vardı. Linux için önceki SAP çekirdek sürümleri, bu kod değişikliği içermiyordu. Bu nedenle, bazı durumlarda (örneğin, Azure VM yeniden boyutlandırma), hello SAP donanım anahtarı değiştirildi ve hello SAP lisans edildi artık geçerli. Bu hello son SAP Linux tekrar çözülür. Ayrıntılar için lütfen SAP Not 1928533 denetleyin.

## <a name="suse-sapconf-package--tuned-adm"></a>SUSE sapconf paket / ayarlanmış adm
SUSE "SAP özgü ayarları kümesini yöneten sapconf" adlı bir paketi sağlar. Hangi bu paketle ilgili daha fazla ayrıntı için ve nasıl tooinstall ve kullanmak için bkz: [sapconf tooprepare SUSE Linux Enterprise Server toorun SAP sistemleri kullanarak](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) ve [sapconf nedir veya nasıl tooprepare SUSE Linux Enterprise SAP sistemlerini çalıştıran sunucu? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

Hello sırada olduğundan sapconf - ayarlanmış adm. yerini alacak yeni bir aracı Bir hello aşağıdaki iki bağlantıları aşağıdaki bu araç hakkında daha fazla ayrıntı bulabilirsiniz.

Olarak ayarlanmış adm profili sap hana ilgili SLES belgeler bulunabilir [burada](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

SAP iş yükleri ile ayarlanmış-adm - ayarlama sistemleri bulunabilir [burada](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) bölümde 6.2

## <a name="nfs-share-in-distributed-sap-installations"></a>Dağıtılmış SAP yüklemelerde NFS paylaşım
Dağıtılmış bir yüklemede--varsa, örneğin, burada istediğiniz tooinstall hello veritabanını ve SAP uygulama sunucuları ayrı VM'ler--hello hello /sapmnt directory ağ dosya sistemi (NFS) aracılığıyla paylaşabilirsiniz. NFS paylaşım için /sapmnt hello oluşturduktan sonra hello yükleme adımlarını sorunlar yaşıyorsanız, "no_root_squash" Merhaba paylaşımı için ayarlandıysa toosee denetleyin.

## <a name="logical-volumes"></a>Mantıksal birimler
Bir büyük bir mantıksal birim (örneğin, hello SAP veritabanı), birden çok Azure veri disklere gerekirse lvm tam henüz Azure üzerinde doğrulanmış değildi olarak hello geçmiş onu toouse mdadm önerilir. mdadm, kullanarak Linux RAID Azure üzerinde yukarı tooset nasıl görürüm toolearn [yazılım RAID Linux üzerinde yapılandırma](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Merhaba başına Mayıs 2016 itibariyle bu arada da lvm tamamen Azure üzerinde desteklenir ve bir alternatif toomdadm kullanılabilir. Azure üzerinde lvm ilgili ek bilgi için bkz: [yapılandırma LVM azure'da bir Linux VM üzerinde](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Azure SUSE deposu
Erişim toohello standart Azure SUSE deposu ile ilgili bir sorun varsa, bir basit komutu tooreset kullanabilirsiniz. Bir Azure bölgesi sonra toodeploy istediğiniz kopyalama hello görüntü tooa farklı bir bölgeye özel bir işletim sistemi görüntüsünü oluşturursanız, bu durum oluşabilir bu özel işletim sistemi yansımasını temel alan yeni VM'ler. Yalnızca hello VM içinde komutu aşağıdaki hello çalıştırın:

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Gnome Masaüstü
Tarayıcı ve SAP Yönetim Konsolu--toouse hello Gnome Masaüstü tooinstall SAP GUI dahil olmak üzere tek bir VM içinde--tam bir SAP demo sistem istiyorsanız, bu ipucu tooinstall kullanın hello Azure SLES görüntüleri üzerinde:

   SLES 11 için:

   ```
   zypper in -t pattern gnome
   ```

   SLES 12 için:

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>Oracle Linux hello bulutta SAP desteği
Sanallaştırılmış ortamlarda Oracle Linux üzerinde gelen destek bir kısıtlama yoktur. Bu bir Azure özgü konu olmamasına karşın, önemli toounderstand var. SAP, Oracle SUSE veya Red Hat gibi Azure genel bulutunda desteklemez. toodiscuss Bu konu, Oracle doğrudan başvurun.

