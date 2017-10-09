---
title: "bir VM üzerinde aaaCompute yoğunluklu Java uygulaması | Microsoft Docs"
description: "Toocreate bir işlem yoğunluklu Java uygulaması çalıştıran bir Azure sanal makinesi başka bir Java uygulaması tarafından nasıl izlenebilir öğrenin."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>Nasıl toorun işlem yoğunluklu görev Java sanal bir makinede
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Azure ile bir sanal makine toohandle işlem yoğunluklu görevleri kullanabilirsiniz. Örneğin, bir sanal makine görevleri ve sonuçları tooclient makine ya da mobil uygulamalara teslim etmek. Bu makaleyi okuduktan sonra toocreate bir işlem yoğunluklu Java uygulaması çalıştıran bir sanal makineyi başka bir Java uygulaması tarafından nasıl izlenebilir, anlaşılması gerekir.

Bu öğretici nasıl toocreate Java konsol uygulamaları kitaplıkları tooyour Java uygulaması içe aktarabilir ve Java arşiv (JAR) oluşturabilir bildiğiniz varsayar. Microsoft Azure olanağıyla varsayılır.

Şunları öğreneceksiniz:

* Nasıl bir sanal makine bir Java Geliştirme Seti (JDK) ile toocreate zaten yüklü.
* Nasıl tooremotely tooyour sanal makinede oturum.
* Nasıl toocreate bir hizmet veri yolu ad alanı.
* Nasıl toocreate bir işlem yoğunluklu görevi gerçekleştiren bir Java uygulaması.
* Nasıl toocreate izler bir Java uygulaması hello işlem yoğunluklu görev ilerlemesini hello.
* Nasıl toorun Java uygulamalarını hello.
* Nasıl toostop Java uygulamalarını hello.

Bu öğretici hello gezici satış temsilcisi hello işlem yoğunluklu görev için kullanır. Merhaba, hello Java uygulama çalışan hello işlem yoğunluklu görev örneği verilmiştir.

![Gezici satış temsilcisi Çözücü][solver_output]

Merhaba, hello Java uygulama izleme hello işlem yoğunluklu görevi örneği verilmiştir.

![Gezici satış temsilcisi istemci][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate bir sanal makine
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Tıklatın **yeni**, tıklatın **işlem**, tıklatın **sanal makine**ve ardından **Galeri'den**.
3. Merhaba, **sanal makine görüntüsü seçin** iletişim kutusunda **JDK 7 Windows Server 2012**.
   Unutmayın **JDK 6 Windows Server 2012** henüz hazır toorun JDK 7 bulunmayan eski uygulamaları olduğunda kullanılabilir.
4. **İleri**’ye tıklayın.
5. Merhaba, **sanal makine yapılandırması** iletişim kutusunda:
   1. Merhaba sanal makine için bir ad belirtin.
   2. Merhaba sanal makine için başlangıç boyutu toouse belirtin.
   3. Hello Merhaba yönetici adı **kullanıcı adı** alan. Sonraki girer bu adı ve hello parolayı unutmayın, uzaktan toohello sanal makinede oturum zaman kullanır.
   4. Hello bir parola girmenizi **yeni parola** alan ve yeniden hello girin **Onayla** alan. Hello Yöneticisi hesabının parolasını belirtir.
   5. **İleri**’ye tıklayın.
6. Merhaba, sonraki **sanal makine yapılandırması** iletişim kutusunda:
   1. İçin **bulut hizmeti**, hello varsayılan kullanmak **yeni bir bulut hizmeti oluşturma**.
   2. Merhaba değeri **bulut hizmeti DNS adı** cloudapp.net arasında benzersiz olması gerekir. Bu Azure benzersiz olduğunu gösterir şekilde gerekirse, bu değeri değiştirin.
   3. Bir bölgeyi, benzeşim grubunu veya sanal ağ belirtin. Bu öğreticinin amaçları doğrultusunda, bir bölge gibi belirtin **Batı ABD**.
   4. İçin **depolama hesabı**seçin **otomatik olarak oluşturulan depolama hesabı kullan**.
   5. İçin **kullanılabilirlik kümesi**seçin **(hiçbiri)**.
   6. **İleri**’ye tıklayın.
7. Merhaba son içinde **sanal makine yapılandırması** iletişim kutusunda:
   1. Merhaba varsayılan uç noktası girişleri kabul eder.
   2. **Tamamla**’ya tıklayın.

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>tooyour sanal makine tooremotely günlüğünde
1. Toohello üzerinde oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Tıklatın **sanal makineleri**.
3. Merhaba, toolog istediğiniz içinde hello sanal makine adını tıklatın.
4. **Bağlan**'a tıklayın.
5. Yanıt toohello gerekli tooconnect toohello sanal makine olarak ister. Hello Yöneticisi adı ve parola istendiğinde, hello sanal makineyi oluşturduğunuzda belirttiğiniz hello değerlerini kullanın.

Bu hello Azure hizmet veri yolu işlevselliğini gerektirir JRE'ın bir parçası olarak yüklenen hello Baltimore CyberTrust kök sertifika toobe Not **cacerts** depolar. Bu sertifika otomatik olarak hello Java Çalışma zamanı ortamı (JRE) bu Öğreticisi tarafından kullanılan dahil edilir. Bu sertifika, JRE sahip değilseniz **cacerts** depolamak için bkz: [sertifika toohello Java CA sertifika deposuna ekleme] [ add_ca_cert] onu ekleme hakkında bilgi için (yanı Merhaba sertifikalarını cacerts deponuzda görüntüleme hakkında bilgi).

## <a name="how-toocreate-a-service-bus-namespace"></a>Nasıl toocreate bir service bus ad alanı
Azure'da Service Bus kullanarak toobegin kuyruklar, öncelikle bir hizmet ad alanı oluşturmanız gerekir. Hizmet ad alanı, uygulamanızın Service Bus kaynaklarını adreslemek için kapsam bir kapsayıcı sağlar.

toocreate hizmet ad alanı:

1. Toohello üzerinde oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba sol gezinti bölmesinde hello Klasik Azure portalı, tıklatın **Service Bus, erişim denetimi ve önbelleğe alma**.
3. Hello sol üst hello Klasik Azure portalı, hello bölmesinde **Service Bus** düğümü ve ardından hello **yeni** düğmesi.  
   ![Hizmet veri yolu düğümü ekran görüntüsü][svc_bus_node]
4. Merhaba, **yeni bir hizmet Namespace oluşturma** iletişim kutusuna bir **Namespace**, ve ardından toomake benzersiz olduğundan emin **Kullanılabilirliği Denetle** düğmesi.  
   ![Yeni Namespace ekran oluşturma][create_namespace]
5. Emin olduktan sonra hello ad alanı adı kullanılabilir olduğu, ülke veya bölge, ad alanınızın barındırılması ve hello ardından seçin **oluşturma Namespace** düğmesi.  
   
   oluşturduğunuz hello ad hello Klasik Azure portalı daha sonra görünür ve şu anda tooactivate alır. Merhaba durum olana kadar bekleyin **etkin** hello sonraki adıma geçmeden önce.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Merhaba varsayılan yönetim kimlik hello ad alanı için elde
Sipariş tooperform yönetim işlemlerinin'hello yeni ad, bir kuyruk oluşturma gibi ad alanı için tooobtain hello yönetim kimlik bilgileri gerekir.

1. Merhaba Sol Gezinti Bölmesi'nde hello tıklatın **Service Bus** hello kullanılabilir ad alanlarının listesini görüntülemek için düğümü.
   ![Kullanılabilir ad alanlarının ekran görüntüsü][avail_namespaces]
2. Gösterilen hello listeden yeni oluşturduğunuz hello ad alanını seçin.
   ![Namespace listesi ekran görüntüsü][namespace_list]
3. sağ taraftaki Hello **özellikleri** bölmesi, yeni ad alanı için hello özellikleri listeler.
   ![Özellikler bölmesinde ekran görüntüsü][properties_pane]
4. Merhaba **varsayılan anahtar** gizlenir. Merhaba tıklatın **Görünüm** düğmesini toodisplay hello güvenlik kimlik bilgileri.
   ![Varsayılan anahtar ekran görüntüsü][default_key]
5. Merhaba Not **varsayılan veren** ve hello **varsayılan anahtar** bu bilgileri tooperform işlemleri altına ad alanıyla kullanacağınız.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>Nasıl toocreate bir işlem yoğunluklu görevi gerçekleştiren bir Java uygulaması
1. (Olmayan oluşturduğunuz toobe hello sanal makine) geliştirme makinenizdeki, indirme hello [Java için Azure SDK](https://azure.microsoft.com/develop/java/).
2. Merhaba bu bölümün sonunda Hello örnek kod kullanarak bir Java konsol uygulaması oluşturun. Bu öğreticide, kullanacağız **TSPSolver.java** hello Java dosya adı olarak. Merhaba değiştirme **,\_hizmet\_veri yolu\_ad alanı**, **,\_hizmet\_veri yolu\_sahibi**ve **,\_hizmet\_veri yolu\_anahtar** yer tutucuları toouse, hizmet veri yolu **ad alanı**, **varsayılan veren** ve  **Varsayılan anahtar** değerler, sırasıyla.
3. Kodlama sonra verme hello uygulama tooa runnable Java arşiv (JAR) ve paket hello hello kitaplıklara JAR oluşturulan gereklidir. Bu öğreticide, kullanacağız **TSPSolver.jar** oluşturulan hello JAR adı.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>Nasıl toocreate izler bir Java uygulaması hello hello işlem yoğunluklu görev ilerleme durumu
1. Geliştirme makinenizde hello bu bölümün sonunda hello örnek kod kullanarak bir Java konsol uygulaması oluşturun. Bu öğreticide, kullanacağız **TSPClient.java** hello Java dosya adı olarak. Daha önce gösterildiği gibi hello değiştirme **,\_hizmet\_veri yolu\_ad alanı**, **,\_hizmet\_veri yolu\_sahibi**, ve **,\_hizmet\_veri yolu\_anahtar** yer tutucuları toouse, hizmet veri yolu **ad alanı**, **varsayılan veren**ve **varsayılan anahtar** değerler, sırasıyla.
2. Merhaba uygulama tooa verme runnable JAR ve paket hello gerekli hello kitaplıklara JAR oluşturulur. Bu öğreticide, kullanacağız **TSPClient.jar** oluşturulan hello JAR adı.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>Nasıl toorun hello Java uygulamaları
Merhaba işlem yoğunluklu uygulamayı çalıştırın, ilk toocreate hello sırayı sonra toosolve seyahat Saleseman hello geçerli en iyi yolu toohello hizmet veri yolu kuyruğu ekleyeceksiniz sorunun, hello. Merhaba sırasında işlem yoğunluklu çalışmıyor (veya daha sonra), çalışma hello istemci toodisplay sonuçları hello service bus kuyruğundan uygulamasıdır.

### <a name="toorun-hello-compute-intensive-application"></a>toorun Merhaba işlem yoğunluklu uygulaması
1. Tooyour sanal makinede oturum açın.
2. Uygulamanızın çalıştırdığı bir klasör oluşturun. Örneğin, **c:\TSP**.
3. Kopya **TSPSolver.jar** çok**c:\TSP**,
4. Adlı bir dosya oluşturun **c:\TSP\cities.txt** içeriği aşağıdaki hello ile.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. Bir komut isteminde dizinleri tooc:\TSP değiştirin.
6. Merhaba JRE'ın bin klasörü hello PATH ortam değişkeni olduğundan emin olun.
7. Merhaba TSP Çözücü permütasyon çalıştırmadan önce toocreate hello hizmet veri yolu kuyruğu gerekir. Çalışma hello aşağıdaki toocreate hello hizmet veri yolu kuyruğu komutu.
   
        java -jar TSPSolver.jar createqueue
8. Merhaba sırası oluşturulduğunda, hello TSP Çözücü permütasyon çalıştırabilirsiniz. Örneğin, komut toorun hello Çözücü 8 şehir için aşağıdaki hello çalıştırın.
   
        java -jar TSPSolver.jar 8
   
   Bir sayı belirtmezseniz, bu için 10 Şehir çalışır. Merhaba Çözücü geçerli kısa yollar buldukça, bunları toohello sıra ekleyeceksiniz.

> [!NOTE]
> Merhaba büyük Merhaba, belirttiğiniz, hello uzun hello Çözücü çalışacak sayı. Örneğin, 14 Şehir birkaç dakika sürebilir ve çalıştırmak için 15 Şehir birkaç saat sürebilir çalışıyor. Too16 veya daha fazla şehir artırma çalışma zamanı (sonunda hafta, ay ve yıl) gün içinde neden olabilir. Merhaba Şehir artar hello sayıda hello Çözücü tarafından değerlendirilen permütasyon sayısını toohello hızla artması son budur.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>Nasıl toorun hello izleme istemci uygulaması
1. Merhaba istemci uygulaması çalıştırdığı tooyour makinede oturum açın. Bu ihtiyaç duymadığı toobe hello hello çalıştıran aynı makine **TSPSolver** olabilir ancak uygulama.
2. Uygulamanızın çalıştırdığı bir klasör oluşturun. Örneğin, **c:\TSP**.
3. Kopya **TSPClient.jar** çok**c:\TSP**,
4. Merhaba JRE'ın bin klasörü hello PATH ortam değişkeni olduğundan emin olun.
5. Bir komut isteminde dizinleri tooc:\TSP değiştirin.
6. Merhaba aşağıdaki komutu çalıştırın.
   
        java -jar TSPClient.jar
   
    İsteğe bağlı olarak, bir komut satırı bağımsız değişkeni geçirerek hello sıra denetimi Between dakika toosleep hello sayısını belirtin. Merhaba hello sıra denetleme varsayılan uyku süresi 3 dakika hiçbir komut satırı bağımsız değişkeni çok aktarılırsa, kullanılır**TSPClient**. Örneğin, hello uyku aralığı için toouse farklı bir değer istiyorsanız, bir dakika hello aşağıdaki komutu çalıştırın.
   
        java -jar TSPClient.jar 1
   
    "Tam" bir kuyruk iletisi görür kadar hello istemci çalıştırın. Merhaba istemci çalıştırmadan hello Çözücü birden çok tekrarı çalıştırırsanız toorun hello istemci birden çok kez toocompletely boş hello sıra gerekebileceğini unutmayın. Alternatif olarak, hello sıra silin ve yeniden oluşturun. Merhaba aşağıdaki komutu çalıştırarak toodelete hello sıra **TSPSolver** (değil **TSPClient**) komutu.
   
        java -jar TSPSolver.jar deletequeue
   
    tüm yollar inceleniyor sonlanana kadar hello Çözücü çalıştırın.

## <a name="how-toostop-hello-java-applications"></a>Nasıl toostop hello Java uygulamaları
Merhaba Çözücü ve istemci uygulamaları için basabilirsiniz **Ctrl + C** tooend önceki toonormal tamamlama istiyorsanız tooexit.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
