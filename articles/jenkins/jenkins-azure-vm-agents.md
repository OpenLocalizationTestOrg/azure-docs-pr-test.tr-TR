---
title: "Jenkins ile sürekli tümleştirme aaaUse Azure VM Aracısı."
description: "Jenkins alt sunucuları olarak Azure VM aracıları."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Jenkins ile sürekli tümleştirme için Azure VM aracılarını kullanın.

Bu hızlı başlangıç nasıl toouse hello Jenkins Azure VM Aracısı eklentisi toocreate isteğe bağlı Linux (Ubuntu) aracıyı Azure gösterir.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç:

* Jenkins asıl zaten yoksa, hello ile başlayabilirsiniz [çözüm şablonu](install-jenkins-solution-template.md) 
* Çok başvuran[Azure CLI 2.0 ile Azure hizmet sorumlusu oluşturma](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) bir Azure hizmet sorumlusu zaten yoksa.

## <a name="install-azure-vm-agents-plugin"></a>Azure VM Aracıları eklentisini yükleme

Hello başlatırsanız [çözüm şablonu](install-jenkins-solution-template.md), hello Azure VM Aracısı eklentisi hello Jenkins yöneticisinde yüklenir.

Aksi takdirde, hello yükleyin **Azure VM Aracısı** gelen eklentisi hello Jenkins Pano içinde.

## <a name="configure-hello-plugin"></a>Merhaba eklentisi yapılandırma

* Merhaba Jenkins Pano içinde tıklatın **Jenkins Yönet -> Sistem Yapılandırma ->**. Merhaba sayfanın toohello'e gidin ve hello açılır hello bölümle Bul **yeni bulut eklemek**. Başlangıç menüsünden seçin **Microsoft Azure VM Aracısı**
* Var olan bir hesap hello Azure kimlik bilgilerini aşağı açılır listeden seçin.  Yeni bir tooadd **Microsoft Azure hizmet sorumlusu** hello aşağıdaki değerleri girin: abonelik kimliği, istemci kimliği, gizli ve OAuth 2.0 belirteç uç noktası.

![Azure Kimlik Bilgileri](./media/jenkins-azure-vm-agents/service-principal.png)

* Tıklatın **doğrulama yapılandırma** toomake bu hello profil yapılandırmasının doğru olduğundan emin.
* Merhaba yapılandırmasını kaydetmek ve toohello sonraki adıma devam edin.

## <a name="template-configuration"></a>Şablon yapılandırması

### <a name="general-configuration"></a>Genel yapılandırma
Ardından, kullanım toodefine bir Azure VM aracısı için bir şablon yapılandırın. 

* Tıklatın **Ekle** tooadd bir şablon. 
* Şablonunuza bir ad verin. 
* "Ubuntu." Merhaba etiketini girin Bu etiket hello iş yapılandırması sırasında kullanılır.
* Merhaba açılan kutudan Hello istediğiniz bölgeyi seçin.
* Select hello VM boyutu istenen.
* Hello Azure depolama hesabı adı belirtin veya boş toouse hello varsayılan adı "jenkinsarmst." bırakın
* Merhaba bekletme süresini dakika cinsinden belirtin. Bu ayar, hello Jenkins boşta aracıyı otomatik olarak silmeden önce bekleyebilirsiniz dakika sayısını tanımlar. Otomatik olarak silinmesini boşta aracıları toobe istemiyorsanız 0 belirtin.

![Genel yapılandırma](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>Görüntü yapılandırma

toocreate Linux (Ubuntu) aracısı seçin **görüntü başvurusu** ve kullanım hello aşağıdaki örnek olarak yapılandırma. Çok başvuran[Azure Marketi](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello için görüntüleri en son Azure desteklenir.

* Görüntü Yayımcısı: Canonical
* Görüntü Teklifi: UbuntuServer
* Görüntü Sku’su: 14.04.5-LTS
* Görüntü sürümü: en son
* İşletim Sistemi Türü: Linux
* Başlatma yöntemi: SSH
* Yönetici kimlik bilgilerini sağlama
* VM başlatma betiği için şunu girin:
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Görüntü yapılandırma](./media/jenkins-azure-vm-agents/image-config.png)

* Tıklatın **doğrulayın şablonu** tooverify hello yapılandırma.
* **Kaydet** düğmesine tıklayın.

## <a name="create-a-job-in-jenkins"></a>Jenkins içinde iş oluşturma

* Merhaba Jenkins Pano içinde tıklatın **yeni öğe**. 
* Bir ad girip **Serbest tarzda proje**’yi seçin ve **Tamam**’a tıklayın.
* Merhaba, **genel** sekmesi, seçin "proje çalıştırdığı kısıtlamak" ve tür etiket ifadesi "ubuntu". Şimdi hello açılır "ubuntu" konusuna bakın.
* **Kaydet** düğmesine tıklayın.

![İşi ayarlama](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>Yeni projenizi derleme

* Toohello Jenkins panoya geri dönün.
* Oluşturduğunuz yeni hello işi, sağ tıklatın, ardından **şimdi yapı**. Derleme başlatılır. 
* Merhaba yapı tamamlandıktan sonra çok Git**konsol çıkış**. Merhaba yapı Azure üzerinde uzaktan gerçekleştirildiğini bakın.

![Konsol çıktısı](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>Başvuru

* Azure Cuma videosu: [Azure VM aracılarını kullanarak Jenkins ile Sürekli Tümleştirme](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)
* Destek bilgileri ve yapılandırma seçenekleri: [Azure VM Aracısı Jenkins Eklentisi Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 

