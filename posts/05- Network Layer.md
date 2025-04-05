# Network Layer

Ağlar arasında end-to-end iletişimi sağlamak için network layer protokolleri dört temel işlemi gerçekleştirir;

### Addressing End Devices

Bulundukları ağda tanımlanabilmeleri için son kullanıcı cihazları daima benzersiz bir IP'ye sahip olmalıdır.

### Encapsulation 

Network layer, transport layer'dan aldığı PDU'yu paketin içine encapsulate eder. Bu encapsulate işlemi, source IP adresi ile destination IP adresi gibi bilgileri içeren bir IP header'i ekleme sürecidir. Encapsulation işlemleri source host tarafından gerçekleştirilir.

### Routing

Network layer, diğer bir ağdaki hedef hosta, paketlerin direkt olarak yönlendirilmesini sağlar. Bu süreçte routerlar, paketleri "best path" yaklaşımını kullanarak ve routing işlemini gerçekleştirerek iletir. Bu süreçte paket birden fazla routerdan geçebilir. Paketin geçtiği her bir routera "hop" adı verilir.

### De-encapsulation

Paket hedef hosta ulaştığında host, paketin IP header'ını kontrol eder. Eğer dest. IP kendi IP'si ile uyuşuyorsa IP header'i paketten kaldırılır (de-encapsulate edilir). De-encapsulation işlemi sonrasında ortaya çıkan Layer 4 PDU'su, transport layerdaki uygun hizmete iletilir. De-encapsulate işlemleri de hedef host tarafından gerçekleştirilir.

Her hostta çalışan işlemler arasındaki veri alışverişini yöneten transport layer'ın aksine network layer protokolleri, (IPv4, IPv6) verileri bir hosttan diğer bir hosta taşımak için kullanılan paketlerin yapısını ve onların işlenmesi için kullanılır. Paketlerdeki taşınan veriye bakılmaksızın çalışması, network layer'ın birden fazla host için birden fazla iletişim türüyle iletişim sağlamasına olanak tanır.

Verilerin katman katman encapsulate edilme süreci, farklı katmanlardaki hizmetlerin diğer katmanları etkilemeden gelişmesini ve ölçeklenmesini sağlar. Bu, taşıma katmanı segmentlerinin IPv4 veya IPv6 veya gelecekte geliştirilebilecek herhangi bir yeni protokol tarafından kolayca paketlenebileceği anlamına gelir.

IP header'ındaki adresleme bilgilerinin, genelde router tarafından gerçekleştirilen NAT işlemi dışında, kaynak hosttan hedef hosta ulaşana kadar aynı kaldığını da ayrıca belirtelim.

## Characteristics of IP

IP, "low overhead" yani düşük ek yüke sahip bir protokol olarak tasarlanmıştır. Ana amacı paketi kaynaktan hedefe, ağlar üzerinden veri aktarımı sağlamaktır. Dolayısıyla da bu protokol, paket akışını izlemek ve yönetmek için tasarlanmamıştır. Bu işlemler -eğer gerekirse- diğer katmanlara, özellikle de layer 4 TCP protokolüne bırakılmıştır. IP protokolünün temel özellikleri şu şekildedir;

### Connectionless

Bu özellik, IP protokolünün veri göndermeden önce herhangi özel bir uçtan uca bağlantı sağlamadığı anlamına gelir. Bunu, alıcıya haber vermeden mektup göndermek olarak düşünebilirsiniz.

### Best Effort

IP ayrıca, daha önceden kurulmuş bir bağlantıyı sürdürmek için header'ında ek alanlara ihtiyaç duymaz. Bu sayede IP'nin overhead'i önemli ölçüde azalır fakat önceden kurulmuş uçtan uca bağlantı olmadığında source hostlar, dest. hostların işlevsel olup olmadığını yani çalışıp çalışmadığının farkında olmazlar. Buna ek olarak, dest. hostların pakete erişip erişmediklerini ve okuyup okumadıklarını da bilmezler.

Yani kısaca IP protokolü, teslim edilen tüm paketlerin hedefe ulaştığını ya da alındığını garanti etmez. Ayrıca teslim edilmeyen paketleri tekrar yollamakla da ilgilenmez. Bu, IP protokolünün "unreliable" yani güvenilmez olduğunu ama "best effort" olduğunu yani en iyi çabayı desteklediğini gösterir. IP'nin best effort olması, ona hız, verimlilik ve basitlik kazandırır.

### Media Independent

IP, protokol yığınının alt katmanlarında verileri taşıyan medyadan bağımsız olarak çalışır. IP paketleri bakır kablo üzerinden elektronik sinyaller, fiber üzerinden optik sinyaller veya kablosuz olarak radyo sinyalleri olarak iletilebilir. Data link layer, IP paketlerini alıp herhangi bir media üzerinden iletilmek üzere hazırlamakla yükümlüdür. Bu IP protokolünün herhangi bir media ile sınırlı olmadığı anlamına gelir. Bunun haricinde network layer'ın media konusunda dikkate aldığı bir husus vardır. O da, her ortamın maksimum taşıyabileceği PDU boyutudur. Buna da "Maximum Transmission Unit (MTU)" denir. Data link layer ile network layer arasındaki kontrol iletişiminin bir parçası da paket için maksimum boyutun belirlenmesidir. Data link layer, MTU değerini network layer'a iletir. Network layer da bu değere göre paketlerin boyutunun ne kadar büyük olabileceğini belirler.

Bazı durumlarda, bir ara cihaz -genellikle router- bir IPv4 paketini bir media'dan daha küçük bir MTU'ya sahip başka bir media'ya iletirken bölmesi gerekir. Bu bölme ya da parçalama işlemine "fragmenting" veya "fragmentation" denir. Fragmentation gecikmeye (latency) neden olur. IPv6 paketleri ise router tarafından parçalanmaz.

## IPv4 Packet Header








