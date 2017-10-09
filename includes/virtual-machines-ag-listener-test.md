Bu adımda, hello kullanılabilirlik grubu dinleyicisi hello üzerinde çalışan bir istemci uygulaması kullanarak test aynı ağ.

İstemci bağlantısı hello gereksinimlerine sahiptir:

* İstemci bağlantıları toohello dinleyicisi konakları Always On kullanılabilirlik çoğaltmalarının hello hello biri daha farklı bulut hizmetinde bulunan makineler gelmelidir.
* İstemciler her zaman açık Hello çoğaltmaları farklı alt ağlarda olup olmadığını belirtmeniz *MultisubnetFailover = True* hello bağlantı dizesinde. Paralel bağlantısı bu koşul sonuçlarında çeşitli alt ağlar hello tooreplicas çalışır. Bu senaryo bir çapraz bölge Always On kullanılabilirlik grubu dağıtımı içerir.

Bir örnek olduğundan tooconnect toohello dinleyici hello hello VM'ler birinden aynı Azure sanal ağı (ancak bir çoğaltmasını barındıran bir değil). Kolay bir yolu toocomplete tootry tooconnect SQL Server Management Studio toohello kullanılabilirlik grubu dinleyicisinin bu denemedir. Başka bir basit toorun yöntemdir [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx)aşağıdaki gibi:

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Merhaba EndpointPort değer ise *1433*, gerekli toospecify olmayan hello çağrısı içinde. Merhaba önceki çağrı de o hello istemci makine birleştirilmiş toohello olduğunu varsayar aynı etki alanında ve o hello arayan verildiğini hello veritabanı izinleri Windows kimlik doğrulaması kullanarak.
> 
> 

Merhaba dinleyicisi test hello kullanılabilirlik grubu toomake istemciler arasında yük devretmeler toohello dinleyicisi bağlanabildiğinden emin üzerinden emin toofail olabilir.

