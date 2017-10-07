---
title: "aaaUnderstand paylaşılan Azure DevTest Labs IP adresleri | Microsoft Docs"
description: "Azure DevTest Labs paylaşılan IP adreslerini toominimize hello ortak IP adresleri gerekli tooaccess laboratuvarınız sanal makineleri nasıl kullandığını öğrenin."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Azure DevTest Labs paylaşılan IP adresleri anlama

Azure DevTest Labs sağlar Laboratuvar VM'ler paylaşımı tek tek laboratuvarınız sanal makineleri aynı ortak IP adresi toominimize hello sayıda ortak IP adresleri gerekli tooaccess hello.  Bu makalede, paylaşılan IP'leri iş ve bunların ilgili yapılandırma seçenekleri açıklanmaktadır.

## <a name="shared-ip-setting"></a>IP ayarı paylaşılan

Bir laboratuvar oluşturduğunuzda, bir sanal ağ alt ağında yer alıyor.  Varsayılan olarak, bu alt ağ ile oluşturulan **etkinleştir paylaşılan ortak IP** çok ayarlamak*Evet*.  Bu yapılandırma hello tüm alt ağ için bir genel IP adresi oluşturur.  Sanal ağlar ve alt ağları yapılandırma hakkında daha fazla bilgi için bkz: [Azure DevTest Labs'de sanal ağ yapılandırma](devtest-lab-configure-vnet.md).

![Yeni Laboratuvar alt ağ](media/devtest-lab-shared-ip/lab-subnet.png)

Var olan Laboratuarları için bu seçeneği seçerek etkinleştirebilirsiniz **yapılandırma ve ilkeleri > sanal ağlar**. Ardından, bir sanal ağ hello listeden seçip seçin **etkinleştirmek genel IP paylaşılan** seçilen alt ağ için. Laboratuvar VM'ler arasında bir ortak IP adresi tooshare istemiyorsanız, bu seçenek, tüm laboratuvarında devre dışı bırakabilirsiniz.

Bu Laboratuvar varsayılan toousing paylaşılan IP oluşturulan herhangi bir VM.  Merhaba VM oluştururken, bu ayar hello gösterilebilir **Gelişmiş ayarları** altında dikey **IP adresi yapılandırması**.

![Yeni VM](media/devtest-lab-shared-ip/new-vm.png)

- **Paylaşılan:** olarak oluşturulan tüm sanal makineleri **paylaşılan** (RG) bir kaynak grubuna yerleştirilir. Tek bir IP adresi için RG ve hello RG tüm Vm'lerde bu IP adresini kullanacak atanır.
- **Genel:** oluşturduğunuz her VM kendi IP adresi vardır ve kendi kaynak grubunda oluşturulur.
- **Özel:** oluşturduğunuz her VM özel IP adresini kullanır. Merhaba doğrudan mümkün tooconnect toothis VM olmaz Internet Uzak Masaüstü ile.

Paylaşılan IP etkin'yle bir VM'yi toohello alt eklendiğinde DevTest Labs otomatik olarak hello VM tooa yük dengeleyici ekler ve toohello hello VM üzerinde RDP noktasına iletme hello genel IP adresi üzerinde bir TCP bağlantı noktası numarası atar.  

## <a name="using-hello-shared-ip"></a>IP paylaşılan Hello kullanma

- **Linux kullanıcıları:** hello IP adresini veya tam etki alanı adı, izleyen iki nokta ile kullanarak SSH toohello VM hello bağlantı noktası tarafından izlenen. Örneğin, aşağıdaki hello görüntü içinde hello RDP adres VM tooconnect toohello `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![VM örneği](media/devtest-lab-shared-ip/vm-info.png)

- **Windows kullanıcıları:** Select hello **Bağlan** hello Azure portal toodownload üzerinde önceden yapılandırılmış bir RDP dosyası düğmesini ve hello VM erişebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

* [Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md)
* [Azure DevTest Labs'de sanal ağ yapılandırma](devtest-lab-configure-vnet.md)





