---
title: "aaaHow toouse hello Azure bağımlı Hudson sürekli tümleştirme ile eklenti | Microsoft Docs"
description: "Nasıl toouse hello Azure bağımlı Hudson sürekli tümleştirme ile eklenti açıklar."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>Nasıl toouse hello Azure bağımlı Hudson sürekli tümleştirme ile eklentisi
Dağıtılmış çalışan oluşturduğunda hello Azure bağımlı Hudson için eklenti tooprovision bağımlı düğümlerin Azure üzerinde sağlar.

## <a name="install-hello-azure-slave-plug-in"></a>Hello Azure bağımlı eklentisini yükleme
1. Hello Hudson Pano, tıklatın **yönetmek Hudson**.
2. Merhaba, **yönetmek Hudson** sayfasında, tıklatın **eklentileri yönetme**.
3. Merhaba tıklatın **kullanılabilir** sekmesi.
4. Tıklatın **arama** ve türü **Azure** toolimit hello listesi toorelevant eklentileri.
   
    Kullanılabilir eklentiler hello listesi aracılığıyla tooscroll seçerseniz, hello Azure bağımlı hello altında eklenti bulacaksınız **küme yönetimi ve dağıtılmış yapı** hello bölümünde **başkalarının** sekmesi.
5. Merhaba onay kutusunu seçip **Azure bağımlı eklentisi**.
6. **Yükle**'ye tıklayın.
7. Hudson yeniden başlatın.

Bu hello eklentisi yüklü artık hello sonraki adımlar tooconfigure hello toocreate hello VM hello ikincil düğüm için oluşturmada kullanılacak bir şablon ve Azure abonelik profiliyle eklenti olacaktır.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Abonelik profilinizle Hello Azure bağımlı eklentisi yapılandırma
Bir abonelik profili de yayımlama başvurulan tooas ayarları, güvenli kimlik bilgileri ve geliştirme ortamınızda Azure ile toowork gerekir bazı ek bilgiler içeren bir XML dosyasıdır. tooconfigure hello Azure bağımlı eklentisi, şunlar gerekir:

* Abonelik kimliği
* Aboneliğiniz için bir yönetim sertifikası

Bunlar bulunabilir, [abonelik profili]. Aşağıda, bir abonelik profili örneğidir.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Abonelik profilinizi oluşturduktan sonra bu adımları tooconfigure hello Azure bağımlı eklenti izleyin.

1. Hello Hudson Pano, tıklatın **yönetmek Hudson**.
2. Tıklatın **sistem yapılandırma**.
3. Merhaba sayfa toofind hello aşağı **bulut** bölümü.
4. Tıklatın **yeni bulut Ekle > Microsoft Azure**.
   
    ![Yeni bulut ekleme][add new cloud]
   
    Bu abonelik ayrıntılarınızı hello alanları tooenter gereken yeri gösterir.
   
    ![profili yapılandırma][configure profile]
5. Abonelik profilinizden Hello abonelik kimliği ve yönetim sertifikası kopyalayın ve bunları hello uygun alanlara yapıştırın.
   
    Merhaba abonelik kimliği ve yönetim sertifikası, kopyalarken **sağlamadığı** hello değerlerini alın hello tırnak işaretleri içine.
6. Tıklayın **doğrulama yapılandırma**.
7. Merhaba yapılandırması başarıyla doğrulandığında tıklatın **kaydetmek**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Bir sanal makine şablonu hello Azure bağımlı için eklenti ayarlayın
Bir sanal makine şablonu hello parametrelerini tanımlar hello eklenti toocreate ikincil düğüm Azure üzerinde kullanır. Aşağıdaki adımları hello şablonu için bir Ubuntu VM oluşturuluyor.

1. Hello Hudson Pano, tıklatın **yönetmek Hudson**.
2. Tıklayın **sistem yapılandırma**.
3. Merhaba sayfa toofind hello aşağı **bulut** bölümü.
4. Merhaba içinde **bulut** bölümünde, bulma **Azure sanal makine şablonu ekleme** hello tıklatıp **Ekle** düğmesi.
   
    ![VM şablonu Ekle][add vm template]
5. Bir bulut hizmet adı hello belirtmeniz **adı** alan. Belirttiğiniz hello ad bulut hizmeti varolan tooan başvuruyorsa, bu hizmeti hello VM sağlanacak. Aksi takdirde, Azure yeni bir tane oluşturun.
6. Merhaba, **açıklama** alan, hello şablonu oluşturuyorsanız açıklayan metin girin. Bu bilgiler yalnızca documentary amaçlıdır ve bir VM sağlama kullanılmaz.
7. Merhaba, **etiketleri** alanına, **linux**. Bu etiket kullanılan tooidentify hello şablonu oluşturduğunuz ve sonradan kullanılan tooreference hello şablonu Hudson işi oluştururken.
8. Merhaba VM oluşturulacağı bir bölge seçin.
9. Merhaba uygun VM boyutunu seçin.
10. Merhaba VM oluşturulacağı bir depolama hesabı belirtin. Hello olduğundan emin olun, kullanıyor hello bulut hizmeti ile aynı bölgeye. Oluşturulan yeni depolama toobe istiyorsanız bu alanı boş bırakabilirsiniz.
11. Bekletme süresini dakika boşta bir ikincil Hudson siler önce hello sayısını belirtir. Merhaba varsayılan değer 60 olarak bırakın.
12. İçinde **kullanım**, bu ikincil düğüm kullanıldığında hello uygun koşulu seçin. Şimdilik, seçin **bu düğüm mümkün olduğunca kullanma**.
    
     Bu noktada, formunuz biraz benzer toothis görünür:
    
     ![Şablon yapılandırma][template config]
13. İçinde **görüntü ailesi veya kimliği** hangi sistem görüntüsü de kendi VM'nizi yüklenecek toospecify sahip. Görüntü aileleri listesinden seçin veya özel bir görüntü belirtin.
    
     Görüntü aileleri listesinden tooselect istiyorsanız, hello ilk karakteri (büyük küçük harfe duyarlı) hello görüntü ailesi adı girin. Örneğin, yazarak **U** Ubuntu Server ailelerinin listesini getirir. Merhaba listeden seçtikten sonra Jenkins VM ayrılırken hello bu aile, sistem görüntüsünü en son sürümünü kullanır.
    
     ![İşletim sistemi ailesi listesi][OS family list]
    
     Bunun yerine toouse istediğiniz özel bir görüntü varsa, bu özel görüntü hello adını girin. Bu nedenle gerekir özel resim adları bir listede adı hello tooensure doğru girildiğini gösterilmez.    
    
     Bu öğretici için yazın **U** Ubuntu görüntüleri seçin ve bir liste toobring **Ubuntu Server 14.04 LTS**.
14. İçin **başlatma yöntemi**seçin **SSH**.
15. Aşağıda başlangıç betiği kopyalayıp hello **Init betik** alan.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Merhaba **Init betik** VM oluşturulduğunda hello sonra yürütülür. Bu örnekte, Java, git ve ant hello betik yükler.
16. Merhaba, **kullanıcıadı** ve **parola** alanları, VM üzerinde oluşturulacak hello yönetici hesabı için tercih edilen değerlerinizi girin.
17. Tıklayın **doğrulayın şablonu** belirttiğiniz başlangıç parametreleri geçerliyse toocheck.
18. **Kaydet**'e tıklayın.

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Azure üzerinde bir ikincil düğüm üzerinde çalışan bir Hudson iş oluşturma
Bu bölümde, Azure üzerinde bir ikincil düğüm üzerinde çalışacak Hudson görev oluşturma.

1. Hello Hudson Pano, tıklatın **yeni iş**.
2. Oluşturmakta olduğunuz hello işi için bir ad girin.
3. Merhaba iş türü için **serbest stili yazılım işi yapı**.
4. **Tamam** düğmesine tıklayın.
5. Merhaba iş yapılandırma sayfasında, seçin **burada bu proje çalıştırılabilir sınırla**.
6. Seçin **düğümü ve etiket menü** seçip **linux** (biz Bu etiket hello önceki bölümde hello sanal makine şablonu oluştururken, belirtilen).
7. Merhaba, **yapı** 'yi tıklatın **Ekle derleme adımı** seçip **Kabuk yürütme**.
8. Aşağıdaki komut, değiştirme hello Düzenle **{github hesap adınız}**, **{projenizin adına}**, ve **{proje dizininiz}** uygun değerleri ile Merhaba yapıştırın komut dosyası görünür hello metin alanında düzenlenebilir.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. **Kaydet**'e tıklayın.
10. Buna Hudson Pano Merhaba, yeni oluşturduğunuz hello işi bulun ve hello üzerinde tıklatın **bir yapı zamanlama** simgesi.

Hudson sonra hello önceki bölümde oluşturduğunuz hello şablonu kullanarak bir ikincil düğüm oluşturabilir ve bu görev için hello yapı adımında belirtilen hello betiğini yürütün.

## <a name="next-steps"></a>Sonraki Adımlar
Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi].

<!-- URL List -->

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[abonelik profili]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

