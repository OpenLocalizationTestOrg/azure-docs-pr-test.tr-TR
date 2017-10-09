### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Merhaba sanal makine için bir TCP uç noktası oluşturma
Merhaba gelen sırası tooaccess SQL Server'ın Internet hello sanal makineye bir uç nokta toolisten gelen TCP iletişimi için olmalıdır. Bu Azure yapılandırma adımı erişilebilir toohello sanal makine gelen TCP bağlantı noktası trafik tooa TCP bağlantı noktasına yönlendirir.

> [!NOTE]
> İçinde hello bağlanıyorsanız aynı hizmet veya sanal ağ bulut, genel olarak erişilebilir bir uç nokta toocreate sahip değil. Bu durumda, toohello sonraki adıma devam edebilir. Daha fazla bilgi için bkz. [Bağlantı Senaryoları](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).
> 
> 

1. Hello Azure Portal, seçin **sanal makineleri (Klasik)**.
2. Ardından SQL Server sanal makinenizi seçin.
3. Seçin **uç noktaları**ve ardından hello **Ekle** hello uç noktaları dikey penceresinde hello üstündeki düğmesi.
   
    ![Uç Nokta Oluşturmak için İzlenecek Portal Adımları](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. Merhaba üzerinde **uç nokta Ekle** dikey penceresinde sağlayan bir **adı** SQLEndpoint gibi.
5. Seçin **TCP** hello için **Protokolü**.
6. **Genel bağlantı noktası** olarak **57500** gibi bir bağlantı noktası numarası belirtin.
7. İçin **özel bağlantı noktası**, çok varsayılan olan SQL Server'ın dinleme bağlantı noktası, belirtin**1433**.
8. Tıklatın **Tamam** toocreate hello uç noktası.

