---
title: "Azure sanal makineleri - şablonu için aaaMultiple IP adreslerini | Microsoft Docs"
description: "Nasıl tooassign birden çok IP adresleri öğrenin bir Azure Resource Manager şablonu kullanarak tooa sanal makine."
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu kullanarak toovirtual makineler birden çok IP adresi atayın

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Bu makalede nasıl toocreate sanal makineye (VM) üzerinden hello Azure Resource Manager dağıtım modeli Resource Manager şablonu kullanarak açıklanmaktadır. Birden çok ortak ve özel IP adreslerini toohello atanamaz VM hello Klasik dağıtım modeli üzerinden dağıtırken aynı NIC. Merhaba okuma Azure dağıtım modelleri hakkında daha fazla toolearn [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>Şablon açıklaması

Bir şablonu dağıtmayı tooquickly sağlar ve tutarlı bir şekilde Azure kaynakları ile farklı yapılandırma değerlerini oluşturun. Okuma hello [Resource Manager şablonu Kılavuzu](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure Resource Manager şablonları ile bilmiyorsanız makalesi. Merhaba [birden çok IP adreslerine sahip bir VM'yi dağıtmak](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) şablonu bu makalede kullanılan.

<a name="resources"></a>Dağıtma hello şablon kaynakları aşağıdaki hello oluşturur:

|Kaynak|Ad|Açıklama|
|---|---|---|
|Ağ arabirimi|*myNic1*|Merhaba Hello senaryo bölümünde bu makalede açıklanan üç IP yapılandırmaları oluşturulur ve toothis NIC atanan|
|Ortak IP adresi kaynağı|2 oluşturulur: *myPublicIP* ve *myPublicIP2*|Bu kaynaklar ortak statik IP adresleri atanır ve toohello atanan *IPConfig-1* ve *IPConfig 2* hello senaryoda açıklanan IP yapılandırmaları.|
|VM|*myVM1*|Standart DS3 VM.|
|Sanal ağ|*myVNet1*|Bir sanal ağ bir alt ağ ile *mySubnet*.|
|Depolama hesabı|Benzersiz toohello dağıtımı|Bir depolama hesabı.|

<a name="parameters"></a>Merhaba şablonu dağıtırken hello şu parametreler için değerler belirtmeniz gerekir:

|Ad|Açıklama|
|---|---|
|adminUsername|Yönetici kullanıcı adı. Merhaba kullanıcı adı ile uyumlu [Azure kullanıcı adı gereksinimleri](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json).|
|Admınpassword|Yönetici parolası hello parolası ile uyumlu [Azure parola gereksinimlerini](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
|dnsLabelPrefix|PublicIPAddressName1 için DNS adı. Merhaba DNS adı toohello VM atanmış hello ortak IP adresleri tooone çözer. Merhaba adı hello Azure içinde benzersiz olmalıdır oluşturduğunuz bölge (konum) hello VM.|
|dnsLabelPrefix1|PublicIPAddressName2 için DNS adı. Merhaba DNS adı toohello VM atanmış hello ortak IP adresleri tooone çözer. Merhaba adı hello Azure içinde benzersiz olmalıdır oluşturduğunuz bölge (konum) hello VM.|
|OSVersion|Merhaba VM Hello Windows/Linux sürüm. Seçili Windows/Linux sürümü verilen hello tam olarak düzeltme eki görüntüsü Hello işletim sistemidir.|
|imagePublisher|VM Hello Windows/Linux görüntü Yayımlayıcı hello için seçilmiş.|
|imageOffer|Seçilen VM Hello Windows/Linux resim hello için.|

Merhaba şablon tarafından dağıtılan hello kaynakların her biri birkaç varsayılan ayarlarla yapılandırılır. Bu ayarları yöntemler aşağıdaki hello birini kullanarak görüntüleyebilirsiniz:

- **Github'da hello şablonu görüntüle:** şablonlarıyla aşinaysanız hello ayarları hello içinde görüntüleyebilirsiniz [şablon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json).
- **Görünüm hello ayarları dağıttıktan sonra:** şablonlarıyla bilmiyorsanız adımları aşağıdaki bölümlerde hello birini kullanarak hello şablonu dağıtmak ve ardından dağıtım sonrasında hello ayarları görüntüleyin.

Hello Azure portal, PowerShell veya hello Azure komut satırı arabirimi (CLI) toodeploy hello şablonu kullanabilirsiniz. Tüm yöntemleri hello üretmek aynı sonucu. toodeploy hello şablonu, tam hello hello aşağıdaki bölümlerde biri adımlar:

## <a name="deploy-using-hello-azure-portal"></a>Hello Azure portalını kullanarak dağıtımı

Hello Azure portalı, aşağıdaki tam hello kullanarak toodeploy hello şablonunu adımlar:

1. Merhaba şablon isterseniz değiştirin. Merhaba şablon dağıtır hello kaynakları ve ayarları hello listelenen [kaynakları](#resources) bu makalenin. toolearn şablonları hakkında daha fazla bilgi ve nasıl tooauthor bunları, okuma hello [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)makalesi.
2. Merhaba şablon yöntemler aşağıdaki hello biriyle dağıtın:
    - **Merhaba Portalı'nda SELECT hello şablonu:** tam hello adımları hello [özel şablon kaynaklardan dağıtmak](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) makalesi. Adlı hello önceden var olan şablonu seçin *vm birden çok ipconfig 101*.
    - **Doğrudan:** hello Portalı'nda doğrudan düğmesi tooopen hello şablonu aşağıdaki hello'ı tıklatın:<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Merhaba yönteminden bağımsız olarak seçtiğiniz Merhaba toosupply değerleri gerekir [parametreleri](#parameters) daha önce bu makalede listelenmektedir. Merhaba VM dağıtıldıktan sonra toohello VM bağlanmak ve hello özel IP adresleri toohello işletim sistemi dağıtılan hello tamamlayarak hello adım eklemek [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin. Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.

## <a name="deploy-using-powershell"></a>PowerShell kullanarak dağıtın

PowerShell, tam hello aşağıdaki adımları kullanarak toodeploy hello şablonu:

1. Merhaba hello adımları tamamlayarak dağıtma hello şablonu [PowerShell ile şablon dağıtma](../azure-resource-manager/resource-group-template-deploy-cli.md) makalesi. Merhaba makale bir şablonu dağıtmak için birden çok seçenekleri açıklar. Hello kullanarak toodeploy seçerseniz `-TemplateUri parameter`, bu şablon için URI hello *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Hello kullanarak toodeploy seçerseniz `-TemplateFile` parametresi, kopyalama Merhaba içeriğine hello [şablon dosyası](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) makinenizde yeni bir dosyaya github'dan. Merhaba şablon içeriği isterseniz değiştirin. Merhaba şablon dağıtır hello kaynakları ve ayarları hello listelenen [kaynakları](#resources) bu makalenin. toolearn şablonları hakkında daha fazla bilgi ve nasıl tooauthor bunları, okuma hello [Azure Resource Manager şablonları yazma ](../azure-resource-manager/resource-group-authoring-templates.md)makalesi.

    Toodeploy hello şablonla hello seçeneği bağımsız olarak, hello listelenen hello parametre değerleri için değerler girmeniz gerekir [parametreleri](#parameters) bu makalenin. Bir parametre dosyası kullanarak toosupply parametrelerini seçerseniz, hello hello içeriğini kopyalayın [parametreler dosyası](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) bilgisayarınızda yeni bir dosyaya github'dan. Merhaba dosyasında Hello değerlerini değiştirin. Oluşturduğunuz hello hello değeri olarak hello dosya kullan `-TemplateParameterFile` parametresi.

    toodetermine hello OSVersion, ImagePublisher ve imageOffer parametreleri için geçerli değerler, tam hello adımları hello [erişin ve seçin Windows VM görüntüleri makale](../virtual-machines/windows/cli-ps-findimage.md) makalesi.

    >[!TIP]
    >Bir dnslabelprefix olup emin değilseniz hello girin `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` komutu toofind çıkışı. Kullanılabilir değilse, hello komut döndürür `True`.

2. Merhaba VM dağıtıldıktan sonra toohello VM bağlanmak ve hello özel IP adresleri toohello işletim sistemi dağıtılan hello tamamlayarak hello adım eklemek [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin. Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.

## <a name="deploy-using-hello-azure-cli"></a>Hello Azure CLI kullanarak dağıtın

Hello Azure CLI 1.0, tam hello aşağıdaki adımları kullanarak toodeploy hello şablonu:

1. Merhaba hello adımları tamamlayarak dağıtma hello şablonu [hello Azure CLI ile şablon dağıtma](../azure-resource-manager/resource-group-template-deploy-cli.md) makalesi. Merhaba makale hello şablonu dağıtmak için birden çok seçenekleri açıklar. Hello kullanarak toodeploy seçerseniz `--template-uri` (-f), bu şablon için URI hello *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Hello kullanarak toodeploy seçerseniz `--template-file` (-f) parametresi, kopyalama Merhaba içeriğine hello [şablon dosyası](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) makinenizde yeni bir dosyaya github'dan. Merhaba şablon içeriği isterseniz değiştirin. Merhaba şablon dağıtır hello kaynakları ve ayarları hello listelenen [kaynakları](#resources) bu makalenin. toolearn şablonları hakkında daha fazla bilgi ve nasıl tooauthor bunları, okuma hello [Azure Resource Manager şablonları yazma ](../azure-resource-manager/resource-group-authoring-templates.md)makalesi.

    Toodeploy hello şablonla hello seçeneği bağımsız olarak, hello listelenen hello parametre değerleri için değerler girmeniz gerekir [parametreleri](#parameters) bu makalenin. Bir parametre dosyası kullanarak toosupply parametrelerini seçerseniz, hello hello içeriğini kopyalayın [parametreler dosyası](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) bilgisayarınızda yeni bir dosyaya github'dan. Merhaba dosyasında Hello değerlerini değiştirin. Oluşturduğunuz hello hello değeri olarak hello dosya kullan `--parameters-file` (-e) parametre.

    toodetermine hello OSVersion, ImagePublisher ve imageOffer parametreleri için geçerli değerler, tam hello adımları hello [erişin ve seçin Windows VM görüntüleri makale](../virtual-machines/windows/cli-ps-findimage.md) makalesi.

2. Merhaba VM dağıtıldıktan sonra toohello VM bağlanmak ve hello özel IP adresleri toohello işletim sistemi dağıtılan hello tamamlayarak hello adım eklemek [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin. Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
