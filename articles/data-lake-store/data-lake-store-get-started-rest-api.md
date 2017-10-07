---
title: "aaaUse hello REST API tooget Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Data Lake Store üzerinde WebHDFS REST API'lerini tooperform işlemleri kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>REST API'lerini kullanarak Azure Data Lake Store ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Bu makalede, Azure Data Lake Store dosya sistemi işlemleri yanı sıra yönetim nasıl toouse WebHDFS REST API'lerini ve Data Lake Store REST API'lerini tooperform hesap öğreneceksiniz. Azure Data Lake Store, hesap yönetimi işlemleri için kendi REST API'lerini kullanıma sunar. Ancak Data Lake Store, HDFS ve Hadoop ekosistemi ile uyumlu olması nedeniyle, dosya sistemi işlemleri için WebHDFS REST API'lerini kullanarak destek sağlar.

> [!NOTE]
> Hello Data Lake Store için REST API desteği hakkında ayrıntılı bilgi için bkz: [Azure Data Lake Store REST API Başvurusu](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Active Directory Uygulaması oluşturma**. Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Store uygulaması kullanın. Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**. Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Bu makalede, nasıl bir Data Lake Store hesabı karşı toomake REST API çağrıları cURL toodemonstrate kullanır.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak nasıl kimlik doğrulaması gerçekleştiririm?
Azure Active Directory'yi kullanarak iki yaklaşım tooauthenticate kullanabilirsiniz.

### <a name="end-user-authentication-interactive"></a>Son kullanıcı kimlik doğrulaması (etkileşimli)
Bu senaryoda, Merhaba uygulaması hello kullanıcı toolog ister ve tüm hello işlemler hello hello kullanıcı bağlamında gerçekleştirilir. Etkileşimli kimlik doğrulaması için adımlara hello gerçekleştirin.

1. Uygulamanızı kullanarak URL aşağıdaki hello kullanıcı toohello yönlendir:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<Yeniden yönlendirme URI'si > kullanılmak üzere bir URL kodlanmış toobe gerekiyor. Bu nedenle, https://localhost için `https%3A%2F%2Flocalhost` kullanılır)
   > 
   > 
   
    Bu öğretici Hello amaçla hello URL'de hello yer tutucu değerlerini değiştirin ve bir web tarayıcısının Adres çubuğuna yapıştırın. Azure oturum açma bilgilerinizi kullanarak yeniden yönlendirilen tooauthenticate olacaktır. Başarıyla oturum açtığında hello yanıt hello tarayıcının adres çubuğunda görüntülenir. Merhaba yanıt biçimi aşağıdaki hello olacaktır:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Merhaba yanıt Hello yetkilendirme kodundan yakalayın. Bu öğretici için hello web tarayıcınızın adres çubuğunda hello hello yetkilendirme kodu kopyalayın ve aşağıda gösterildiği gibi hello POST isteği toohello belirteç uç noktasında geçirin:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > Bu durumda, hello \<REDIRECT-URI > öğesinin kodlanması gerekmez.
   > 
   > 
3. Merhaba yanıt olan bir erişim belirteci içeren bir JSON nesnesi (örn., `"access_token": "<ACCESS_TOKEN>"`) ve bir yenileme belirteci (örn., `"refresh_token": "<REFRESH_TOKEN>"`). Bir erişim belirtecinin süresi dolduğunda, uygulamanızın hello erişim belirteci Azure Data Lake Store ve hello yenileme belirteci tooget erişirken başka bir erişim belirteci kullanır.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Merhaba erişim belirtecinin süresi dolduğunda, aşağıda gösterildiği gibi hello yenileme belirtecini kullanarak yeni bir erişim belirteci isteyebilirsiniz:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Etkileşimli kullanıcı kimlik doğrulaması hakkında daha fazla bilgi için bkz. [Yetki kodu izin akışı](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Hizmetten hizmete kimlik doğrulaması (etkileşimli olmayan)
Bu senaryoda, hello hello uygulama kendi kimlik bilgilerini tooperform hello işlemler sağlar. Bunun için aşağıda gösterilene hello gibi bir POST isteği yayımlamanız gerekir. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

Merhaba bu isteğin çıktısı, bir yetki belirteci içerir (belirtilmiştir `access-token` hello çıkışı aşağıdaki), REST API çağrıları ile sonradan geçecek. Bu kimlik doğrulama belirtecini bir metin dosyasına kaydedin; belirteç, bu makalenin ilerleyen bölümlerinde gerekli olacaktır.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Bu makalede hello kullanan **etkileşimli olmayan** yaklaşım. Etkileşimli olmayan (hizmet-hizmet çağrıları) hakkında daha fazla bilgi için bkz: [hizmet kimlik bilgilerini kullanarak tooservice çağrıları](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Data Lake Store hesabı oluşturma
Bu işlem üzerinde tanımlı hello REST API çağrısı tabanlı [burada](https://msdn.microsoft.com/library/mt694078.aspx).

Merhaba aşağıdaki cURL komutunu kullanın. **\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

Komut yukarıda Hello yerine \< `REDACTED` \> hello yetki belirteciyle, daha önce aldığınız. Bu komut için başlangıç istek yükü hello bulunan **input.json** hello için sağlanan dosya `-d` yukarıdaki parametresini. hello input.json dosyasının Merhaba içeriğine hello aşağıdakine benzer:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Data Lake Store hesabında klasör oluşturma
Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Merhaba aşağıdaki cURL komutunu kullanın. **\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

Komut yukarıda Hello yerine \< `REDACTED` \> hello yetki belirteciyle, daha önce aldığınız. Bu komut adlı bir dizin oluşturur **mytempdir** hello Data Lake Store hesabınızın kök klasörü altında.

Merhaba işlem başarıyla tamamlanırsa şuna benzer bir yanıt görmeniz gerekir:

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Data Lake Store hesabındaki klasörleri listeleme
Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Merhaba aşağıdaki cURL komutunu kullanın. **\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

Komut yukarıda Hello yerine \< `REDACTED` \> hello yetki belirteciyle, daha önce aldığınız.

Merhaba işlem başarıyla tamamlanırsa şuna benzer bir yanıt görmeniz gerekir:

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a>Data Lake Store hesabına veri yükleme
Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Merhaba aşağıdaki cURL komutunu kullanın. **\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

Merhaba yukarıda söz dizimi içinde **-T** parametredir karşıya hello dosyasının başlangıç konumu.

Merhaba çıkış benzer toohello aşağıda verilmiştir:
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Data Lake Store hesabından veri okuma
Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

Data Lake Store hesabından veri okuma, iki adımlı bir işlemdir.

* İlk hello uç noktası bir GET isteği gönderme `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Bu bir konum toosubmit hello sonraki GET isteğini döndürür.
* Ardından hello endpoint hello GET isteğini göndermek `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Bu hello hello dosyanın içeriğini görüntüler.

Ancak, fark olduğundan hello giriş parametreleri hello arasında önce ve hello adım ikinci, hello kullanabilirsiniz `-L` parametresi toosubmit hello ilk istek. `-L`seçeneği temelde iki isteği tek istekte birleştirir ve hello yeni konum hello isteğinde Yinele cURL hale getirir. Son olarak, tüm hello istek çağrılarının çıktısı Merhaba, olduğu gibi görüntülenir aşağıda gösterilen. **\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Data Lake Store hesabındaki bir dosyayı yeniden adlandırma
Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

Kullanım hello aşağıdaki komut toorename bir dosya cURL. **\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Data Lake Store hesabından dosya silme
Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

Kullanım hello aşağıdaki komut toodelete bir dosya cURL. **\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Data Lake Store hesabını silme
Bu işlem üzerinde tanımlı hello REST API çağrısı tabanlı [burada](https://msdn.microsoft.com/library/mt694075.aspx).

Kullanım hello aşağıdaki komut toodelete bir Data Lake Store hesabı cURL. **\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Store ile uyumlu Açık Kaynak Büyük Veri uygulamaları](data-lake-store-compatible-oss-other-applications.md)

