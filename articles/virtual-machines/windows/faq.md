---
title: "azure'da Windows sanal makineleri hakkında aaaFAQ | Microsoft Docs"
description: "Hello hello Resource Manager modeli kullanılarak oluşturulmuş Windows sanal makineler hakkında genel soruların yanıtları toosome sağlar."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Windows sanal makineler hakkında sık sorulan sorular
Bu makalede, Azure'da hello Resource Manager dağıtım modeli kullanarak oluşturulan Windows sanal makineler hakkında bazı sık sorulan soruları giderir. Merhaba Linux sürümü bu konu için bkz: [Linux sanal makineleri hakkında sık sorulan bir soru](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Azure sanal makinesinde ne çalıştırabilirim?
Tüm aboneler bir Azure sanal makinesinde sunucu yazılımı çalıştırabilir. Azure'da çalışan Microsoft sunucu yazılımı için hello destek ilkesi hakkında daha fazla bilgi için bkz: [Microsoft sunucu yazılımı desteği için Azure sanal makineler](https://support.microsoft.com/kb/2721672)

Belirli Windows 7, Windows 8.1 ve Windows 10 kullanılabilir tooMSDN Azure avantajı aboneleri ve geliştirme ve test görevler için MSDN Geliştirme ve Test Kullandıkça Öde aboneleri sürümleridir. Yönerge ve kısıtlamalar dahil olmak üzere ayrıntılı bilgi edinmek için bkz. [MSDN aboneleri için Windows İstemci görüntüleri](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/). 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Bir sanal makineyle birlikte ne kadar depolama alanı kullanabilirim?
Her veri diski too1 TB olabilir. Merhaba kullanabileceğiniz veri diski sayısı hello hello sanal makine boyutuna bağlıdır. Ayrıntılar için bkz. [Virtual Machines boyutları](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Azure yönetilen hello yeni ve önerilen disk depolama teklifleri kullanmak için Azure Virtual Machines ile kalıcı depolama alanı için disklerdir. Her bir Sanal Makine ile birden fazla Yönetilen Disk kullanabilirsiniz. Yönetilen Diskler iki tür dayanıklı depolama seçeneği sunar: Premium ve Standart Yönetilen Diskler. Fiyatlandırma bilgileri için bkz: [yönetilen diskleri fiyatlandırma](https://azure.microsoft.com/pricing/details/managed-disks).

Azure depolama hesapları, ayrıca hello işletim sistemi diski ve veri diskleri için depolama sağlayabilir. Her disk bir sayfa blobu olarak depolanan bir .vhd dosyasıdır. Fiyatlandırma ayrıntıları için bkz. [Depolama Fiyatlandırma Ayrıntıları](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Sanal Makinem nasıl erişebilir mi?
Bir Windows VM için Uzak Masaüstü Bağlantısı (RDP) kullanarak uzak bağlantı kurun. Yönergeler için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). En fazla iki eşzamanlı bağlantı desteklenir, Uzak Masaüstü Hizmetleri oturumu ana bilgisayarı hello sunucu yapılandırılmadığı sürece.  

Uzak Masaüstü ile sorun yaşıyorsanız, bkz: [sorun giderme Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Hyper-V ile sahibiyseniz, aracı benzer tooVMConnect için arayan. Konsol erişimi tooa sanal makine desteklenmediğinden azure benzer bir araç sağlamaz.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>Merhaba geçici disk (Merhaba D: sürücü varsayılan olarak) toostore verileri kullanabilir miyim?
Merhaba geçici disk toostore veri kullanmayın. Kurtarılamaz veri kaybetme riskini böylece yalnızca geçici depolama mümkündür. Merhaba sanal makine tooa farklı ana bilgisayar taşındığında veri kaybı oluşabilir. Bir sanal makine yeniden boyutlandırma, hello konak ya da bir donanım hatası hello ana bilgisayarda güncelleştirme bir sanal makineyi taşımak hello nedenlerden bazılarıdır.

Toouse hello D: sürücü harfi gerektiren bir uygulamanız varsa, hello geçici disk D: dışında bir şey kullanmayacağından sürücü harfi atayabilirsiniz. Yönergeler için bkz: [değişiklik hello sürücü harfi hello Windows geçici disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Merhaba geçici disk hello sürücü harfi nasıl değiştirebilir miyim?
Hello sürücü harfiyle hello sayfa dosya taşıma ve sürücü harflerini yeniden atama değiştirebilirsiniz, ancak belirli bir sırada adımları hello emin toomake gerekir. Yönergeler için bkz: [değişiklik hello sürücü harfi hello Windows geçici disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>Var olan VM tooan kullanılabilirlik kümesini ekleyebilir miyim?
Hayır. Bir kullanılabilirlik kümesi, VM toobe parçası istiyorsanız hello kümesi içinde toocreate hello VM gerekir. Şu anda hiç bir şekilde tooadd oluşturulduktan sonra ayarlanmış bir VM tooan kullanılabilirlik.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>Bir sanal makine tooAzure yükleyebilir miyim?
Evet. Yönergeler için bkz: [geçiş şirket içi sanal makineleri tooAzure](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>Merhaba işletim sistemi disk boyutunu değiştirebilir miyim?
Evet. Yönergeler için bkz: [nasıl tooexpand hello Azure kaynak grubu içindeki bir sanal makineye işletim sistemi sürücüsünde](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>I kopyalayabilir veya mevcut bir Azure VM'yi kopyalama?
Evet. Yönetilen görüntüleri kullanarak, bir sanal makine görüntüsünü oluşturmak ve ardından hello görüntü toobuild birden çok yeni VM kullanabilirsiniz. Yönergeler için bkz: [özel bir görüntü bir VM oluşturun](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Neden Kanada merkezi ve Doğu Kanada bölgeler arasında Azure Resource Manager görüyorum değil mi?

Merhaba iki yeni bölgeler Kanada merkezi ve Doğu Kanada otomatik olarak mevcut Azure abonelikleri için sanal makine oluşturmak için kayıtlı değil. Bu kayıt aracılığıyla bir sanal makine dağıtıldığında otomatik olarak yapılır Azure portal tooany Azure Kaynak Yöneticisi'ni kullanarak diğer bölge hello. Bir sanal makine sonra diğer Azure bölgesi dağıtılan tooany olan hello yeni bölgeler sonraki sanal makineler için kullanılabilir.

## <a name="does-azure-support-linux-vms"></a>Azure Linux VM'ler destekliyor mu?
Evet. tooquickly oluşturma bir Linux VM tootry çıkışı, bkz: [hello Portal kullanarak Azure'da bir Linux VM oluşturma](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>NIC toomy VM, oluşturulduktan sonra ekleyebilir miyim?
Evet, bu artık mümkündür. Merhaba VM ilk gereksinimlerini toobe deallocated durduruldu. Bir NIC ekleyip sonra (olduğu sürece son NIC hello VM üzerinde hello). 

## <a name="are-there-any-computer-name-requirements"></a>Herhangi bir bilgisayar adı gereksinimleri var mı?
Evet. Merhaba bilgisayar adı en fazla 15 karakter uzunluğunda olabilir. Bkz: [adlandırma kuralları kuralları ve sınırlamaları](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) kaynaklarınızı adlandırma geçici daha fazla bilgi için.

## <a name="are-there-any-resource-group-name-requirements"></a>Herhangi bir kaynak grubu adı gereksinimleri var mı?
Evet. Merhaba kaynak grubu adı en fazla 90 karakter uzunluğunda olabilir. Bkz: [adlandırma kuralları kuralları ve sınırlamaları](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) kaynak grupları hakkında daha fazla bilgi için.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Bir VM oluşturulurken hello kullanıcıadı gereksinimleri nelerdir?

Kullanıcı adları en fazla 20 karakter uzunluğunda olabilir ve bir noktayla bitemez ("."). 


kullanıcı adlarını aşağıdaki hello izin verilmiyor:
<table>
    <tr>
        <td style="text-align:center">Yönetici </td><td style="text-align:center"> Yönetici </td><td style="text-align:center"> Kullanıcı </td><td style="text-align:center"> Kullanıcı1</td>
    </tr>
    <tr>
        <td style="text-align:center">test etme </td><td style="text-align:center"> Kullanıcı2 </td><td style="text-align:center"> Test1 </td><td style="text-align:center"> KULLANICI3</td>
    </tr>    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> bir</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> ASPNET</td>
    </tr>
    <tr>
        <td style="text-align:center">yedekleme </td><td style="text-align:center"> Konsol </td><td style="text-align:center"> David </td><td style="text-align:center"> Konuk</td>
    </tr>
    <tr>
        <td style="text-align:center">John </td><td style="text-align:center"> Sahibi </td><td style="text-align:center"> kök </td><td style="text-align:center"> sunucu</td>
    </tr>
    <tr>
        <td style="text-align:center">SQL </td><td style="text-align:center"> Destek </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">Test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> Kullanıcı4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Bir VM oluşturulurken hello parola gereksinimleri nelerdir?
Parolalar 12-123 karakter uzunluğunda olmalıdır ve 3 4 karmaşıklık gereksinimlerini aşağıdaki hello dışında karşılaması gerekir:

* Alt karakterler
* Üst karakter
* Bir rakam olması
* (Regex eşleşen [\W_]) bir özel karakter sahip

parolaları aşağıdaki hello izin verilmiyor:

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$ $word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Parola! </td>
        <td>Parola1 </td>
        <td>Password22 </td>
        <td>ILOVEYOU veya! </td>
    </tr>
</table>
