Merhaba adımları toounregister bir işlem sunucusu hello yapılandırma sunucusu ile bağlantı durumunu bağlı olarak farklılık gösterir.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>Bağlı durumdaki işlem sunucusunun kaydını kaldırma

1. Uzaktan hello işlem sunucusuna yönetici olarak.
2. Merhaba başlatma **Denetim Masası** açarak **Programlar > program Kaldır**
3. Merhaba adıyla program Kaldır **Microsoft Azure Site kurtarma yapılandırması/işlem sunucusu**
4. Adım 3 tamamlandıktan sonra **Microsoft Azure Site Recovery Yapılandırması/İşlem Sunucusu Bağımlılıkları**’nı kaldırabilirsiniz

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>Bağlantısı kesik durumdaki işlem sunucusunun kaydını kaldırma

> [!WARNING]
> Hiçbir şekilde toorevive hello sanal makine üzerinde hangi hello işlem sunucusu yüklü ise, aşağıdaki adımları kullanın hello kullanılmalıdır.

1. Tooyour yapılandırma sunucusunda yönetici olarak oturum açın.
2. Bir yönetici komut istemi açın ve toohello dizin taraması `%ProgramData%\ASR\home\svsystems\bin`.
3. Şimdi hello komutunu çalıştırın.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Bu hello işlem sunucusu hello ayrıntılarını hello sistemden temizlenir.
