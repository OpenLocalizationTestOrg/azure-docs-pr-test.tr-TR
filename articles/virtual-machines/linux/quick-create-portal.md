---
title: "Azure Hızlı Başlangıç - VM Portalı oluşturma | Microsoft Docs"
description: "Azure Hızlı Başlangıç - VM Portalı oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d009020e86fdfed6a45b5b63b9664c623bcb1843
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-portal"></a>Azure portal ile Linux sanal makinesi oluşturma

Azure sanal makineleri, Azure portalı üzerinden oluşturulabilir. Bu yöntem, sanal makineleri ve tüm ilgili kaynakları oluşturup yapılandırmaya yönelik tarayıcı tabanlı bir kullanıcı arabirimi sağlar. Sanal makine oluşturma ve VM’ye web sunucusu yüklemeye yönelik Hızlı Başlangıç adımları.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

## <a name="create-ssh-key-pair"></a>SSH anahtar çifti oluşturma

Bu hızlı başlangıcı tamamlamak için bir SSH anahtar çifti gerekir. Bir SSH anahtar çiftiniz varsa bu adımı atlayabilirsiniz.

Bir Bash kabuğundan bu komutu çalıştırın ve ekrandaki yönergeleri izleyin. Komut çıktısı genel anahtar dosyasının dosya adını içerir. Ortak anahtar dosyasının içeriğini panoya kopyalayın.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-to-azure"></a>Azure'da oturum açma 

http://portal.azure.com sayfasından Azure portalda oturum açın.

## <a name="create-virtual-machine"></a>Sanal makine oluşturma

1. Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.

2. **İşlem**'i ve ardından **Ubuntu Server 16.04 LTS**'yi seçin. 

3. Sanal makine bilgilerini girin. **Kimlik doğrulama türü** için **SSH ortak anahtarı**’nı seçin. SSH ortak anahtarınıza yapıştırırken, önce veya sonra gelen tüm boşlukları kaldırmaya dikkat edin. İşlem tamamlandığında **Tamam**’a tıklayın.

    ![Portal dikey penceresinde VM’niz ile ilgili temel bilgileri girin](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. VM için bir boyut seçin. Daha fazla boyut görmek için **Tümünü görüntüle**’yi seçin veya **Desteklenen disk türü** filtresini değiştirin. 

    ![VM boyutlarını gösteren ekran görüntüsü](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. Ayarlar dikey penceresinde varsayılan değerleri koruyun ve **Tamam**'a tıklayın.

6. Özet sayfasında **Tamam**’a tıklayarak sanal makine dağıtımını başlatın.

7. VM, Azure portalı panosuna sabitlenir. Dağıtım tamamlandıktan sonra VM özeti dikey penceresi otomatik olarak açılır.


## <a name="connect-to-virtual-machine"></a>Sanal makineye bağlanma

Sanal makine ile bir SSH bağlantısı oluşturun.

1. Sanal makine dikey penceresindeki **Bağlan** düğmesine tıklayın. Bağlan düğmesi, sanal makineye bağlanmak için kullanılabilen bir SSH bağlantı dizesi gösterir.

    ![Portal 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. Bir SSH oturumu oluşturmak için aşağıdaki komutu çalıştırın. Bağlantı dizesini Azure portaldan kopyaladığınız dizeyle değiştirin.

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a>NGINX yükleme

Paket kaynaklarını güncelleştirmek ve en son NGINX paketini yüklemek için aşağıdaki bash betiğini kullanın. 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

İşiniz bittiğinde, SSH oturumundan çıkıp Azure portalında VM özelliklerine geri dönün.


## <a name="open-port-80-for-web-traffic"></a>Web trafiği için 80 numaralı bağlantı noktasını açın 

Ağ güvenlik grubu (NSG), gelen ve giden trafiğin güvenliğini sağlar. Azure portalından bir VM oluşturulduğunda, SSH bağlantıları için 22 numaralı bağlantı noktasında bir gelen kuralı oluşturulur. Bu VM bir web sunucusunu barındırdığından, 80 numaralı bağlantı noktası için bir NSG kuralının oluşturulması gerekir.

1. Sanal makinede **Kaynak grubunun** adına tıklayın.
2. **Ağ güvenlik grubu**’nu seçin. NSG, **Tür** sütunu kullanılarak tanımlanabilir. 
3. Sol menüdeki ayarlar altında **Gelen güvenlik kuralları**’na tıklayın.
4. **Ekle**'ye tıklayın.
5. **Ad** alanına **http** yazın. **Bağlantı noktası aralığı** değerinin 80, **Eylem** ayarının **İzin Ver** olarak belirlendiğinden emin olun. 
6. **Tamam** düğmesine tıklayın.


## <a name="view-the-nginx-welcome-page"></a>NGINX karşılama sayfasını görüntüleme

NGINX yüklüyken ve 80 numaralı bağlantı noktası sanal makineniz için açıkken, web sunucusuna İnternet üzerinden erişilebilir. Bir web tarayıcısı açın ve VM’nin ortak IP adresini girin. Genel IP adresi, Azure portalındaki VM dikey penceresinde bulunabilir.

![Varsayılan NGINX sitesi](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Kaynakları temizleme

Artık gerekli olmadığında kaynak grubunu, sanal makineyi ve tüm ilişkili kaynakları silin. Bunu yapmak için sanal makine dikey penceresinden kaynak grubunu seçip **Sil**’e tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz. Azure sanal makineleri hakkında daha fazla bilgi için Linux VM’lerine yönelik öğreticiye geçin.

> [!div class="nextstepaction"]
> [Azure Linux sanal makine öğreticileri](./tutorial-manage-vm.md)
