---
title: "Azure Kubernetes Helm ile aaaDeploy kapsayıcıları | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Kubernetes kümesinde Hello Helm paketleme aracı toodeploy kapsayıcıları kullanma"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>Kubernetes kümede Helm toodeploy kapsayıcılar kullanma 

[Helm](https://github.com/kubernetes/helm/) yükleyip Kubernetes uygulamaların hello yaşam döngüsünü yönetmenize yardımcı olan bir açık kaynak paketleme aracıdır. Benzer tooLinux paket yöneticileri Apt get ve Yum gibi Helm paketleri önceden yapılandırılmış Kubernetes kaynakların kullanılan toomanage Kubernetes grafikler, ' dir. Bu makalede, Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesinde toowork Helm ile nasıl dağıtılacağını gösterir.

Helm iki bileşenden oluşur: 
* Merhaba **Helm CLI** makinenizde yerel olarak veya hello bulutta çalışan bir istemci  

* **Tiller** hello Kubernetes kümede çalışan ve hello yaşam Kubernetes uygulamalarınızın yönetir. bir sunucu 
 
## <a name="prerequisites"></a>Ön koşullar

* [Kubernetes küme oluşturma](container-service-kubernetes-walkthrough.md) Azure kapsayıcı Hizmeti'nde

* [Yükleme ve yapılandırma `kubectl` ](../container-service-connect.md) yerel bir bilgisayarda

* [Helm yüklemek](https://github.com/kubernetes/helm/blob/master/docs/install.md) yerel bir bilgisayarda

## <a name="helm-basics"></a>Helm temelleri 

Merhaba Kubernetes küme hakkında Tiller yükleme ve komut aşağıdaki hello yazmak için uygulamalarınızı dağıtma olduğundan tooview bilgi:

```bash
kubectl cluster-info 
```
![kubectl küme bilgisi](./media/container-service-kubernetes-helm/clusterinfo.png)
 
Helm yükledikten sonra Tiller hello aşağıdaki komutu yazarak Kubernetes kümenizde yükleyin:

```bash
helm init --upgrade
```
Başarıyla tamamlandığında, çıkış hello aşağıdaki gibi bakın:

![Tiller yükleme](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview tüm hello Helm grafiklerde kullanılabilir hello deposu, aşağıdaki türü hello komutu:

```bash 
helm search 
```

Merhaba aşağıdaki gibi bir çıktı bakın:

![Helm arama](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate hello grafikleri tooget hello en son sürümleri, yazın:

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Bir Nginx giriş denetleyicisi grafik dağıtma 
 
toodeploy Nginx giriş denetleyicisi grafik, tek bir komut yazın:

```bash
helm install stable/nginx-ingress 
```
![Giriş denetleyicisi dağıtma](./media/container-service-kubernetes-helm/nginx-ingress.png)

Yazarsanız `kubectl get svc` tooview hello küme üzerinde çalışan tüm hizmetleri, bir IP adresi toohello giriş denetleyicisi atanır bakın. (Merhaba atama işlemi devam ederken, gördüğünüz `<pending>`. İşlem birkaç dakika toocomplete alır.) 

Başlangıç IP adresi atandıktan sonra çalışan hello dış IP adresi toosee hello Nginx arka uç toohello değerini gidin. 
 
![Giriş IP adresi](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee kümenizde türü yüklü grafikleri listesi:

```bash
helm list 
```

Merhaba komutu çok kısaltma`helm ls`.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>MariaDB grafik ve istemci dağıtma

Şimdi bir MariaDB grafik ve MariaDB istemci tooconnect toohello veritabanı dağıtın.

toodeploy hello MariaDB grafik, komutu aşağıdaki türü hello:

```bash
helm install --name v1 stable/mariadb
```

Burada `--name` olan sürümleri için kullanılan bir etiket.

> [!TIP]
> Merhaba dağıtımı başarısız olursa çalıştırmak `helm repo update` ve yeniden deneyin.
>
 
 
tooview tüm hello grafikler kümenizde türü dağıtılan:

```bash 
helm list
```
 
tooview, küme üzerinde çalışan tüm dağıtımlar yazın:

```bash
kubectl get deployments 
``` 
 
 
Son olarak, toorun pod tooaccess hello istemci yazın:

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
tooconnect toohello istemci, aşağıdaki komut, değiştirme türü hello `v1-mariadb` dağıtımınızın hello adıyla:

```bash
sudo mysql –h v1-mariadb
```
 
 
Şimdi kullanabileceğiniz standart SQL komutlarını toocreate veritabanları, tablolar vb.. Örneğin, `Create DATABASE testdb1;` boş bir veritabanı oluşturur. 
 
 
 
## <a name="next-steps"></a>Sonraki adımlar

* Merhaba Kubernetes grafikleri yönetme hakkında daha fazla bilgi için bkz: [Helm belgelerine](https://github.com/kubernetes/helm/blob/master/docs/index.md). 

