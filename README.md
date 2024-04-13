# CAPSTONE-II
**JCDSOL-013-021 NATASHA VERENA LOHANATHA**
# LATAR BELAKANG
       Supermarket melakukan program membership sebagai bentuk pengumpulan sampling untuk mengetahui demografik pelanggan dan insight untuk kegiatan marketing supermarket. Rentang waktu data adalah dari Juni 2012 - Juni 2014 (2 tahun).  
## PERNYATAAN MASALAH
        Supermarket ingin mengetahui **siapa kelas pelanggan terbesar mereka, apa kebutuhan mereka dan cara menggapai mereka**. Diketahui secara kasar rendahnya angka customer yang ikut berpartisipasi dalam aktifitas kampanye penjualan. Karena itu informasi ini akan digunakan sebagai landasan perencanaan kampanye marketing periode tahun 2014-2015, tipe "always on" maupun periodik sesuai dengan target market untuk meningkatkan partisipasi dan sebagai bentuk tolak ukur naiknya "brand awareness" diantara customer lama maupun yang akan bergabung nantinya. Kedepannya, data ini juga bisa menjadi faktor pertimbangan untuk tim purchasing dan/atau procurement (divisi produk dan pengembangan bisnis) dalam mengkurasikan barang dan menetapkan harga barang yang sesuai dengan target market Supermarket.    
## TUJUAN
        * Mengetahui demografik pelanggan Supermarket berdasarkan kelas pendapatan (Income Class) dan kegiatan berbelanja (Membership)
        * Mengetahui barang dengan jumlah purchasing tertinggi berdasarkan kelas pendapatan (Income Class) dan kegiatan berbelanja (Membership) 
        * Mengetahui channel berbelanja berdasarkan kelas pendapatan (Income Class) dan kegiatan berbelanja (Membership)
        * Memprediksi produk unggulan dan bentuk promosi yang sesuai serta menentukan set KPI untuk periode 2014-15 untuk meningkatkan jumlah dan kualitas transaksi di Supermarket 

# READ DATA
        Berikut deskripsi informasi yang terdapat di dalam dataset Supermarket Customer: 

| Kategori          | Kolom                 | Deskripsi                                                                     |
| ------------------|-----------------------|------------------------------------------------------------------------------ |
| **People**        | ID                    | Identitas unik customer                                                       |
|                   | Year_Birth            | Tahun lahir customer                                                          |
|                   | Education             | Level edukasi customer                                                        |
|                   | Marital_Status        | Status pernikahan customer                                                    |
|                   | Income                | Pendapatan per tahun customer                                                 |
|                   | Kidhome               | Jumlah anak dalam rumahtangga customer                                        |
|                   | Teenhome              | Jumlah remaja dalam rumahtangga customer                                      |
|                   | Dt_Customer           | tanggal pendaftaran customer menjadi member Supermarket                       |
|                   | Recency               | Jumlah hari sejak terakhir kali customer berbelanja                           |
|                   | Complain              | 1 jika customer pernah komplain selama 2 tahun terakhir, jika tidak 0         |    
| **Products**      | MntWines              | Jumlah (buah) pembelian produk wine dalam 2 tahun terakhir                    |
|                   | MntFruits             | Jumlah (buah) pembelian produk buah dalam 2 tahun terakhir                    |
|                   | MntMeatProducts       | Jumlah (buah) pembelian produk daging dalam 2 tahun terakhir                  |
|                   | MntFishProducts       | Jumlah (buah) pembelian produk ikan dalam 2 tahun terakhir                    |
|                   | MntSweetProducts      | Jumlah (buah) pembelian produk manis dalam 2 tahun terakhir                   |
|                   | MntGoldProds          | Jumlah (buah) pembelian produk emas dalam 2 tahun terakhir                    |
| **Promotion**     | NumDealsPurchases     | Jumlah pembelian menggunakan/melalui promosi                                  |
|                   | AcceptedCmp1          | 1 jika customer menerima tawaran kampanye 1, jika tidak 0                     |
|                   | AcceptedCmp2          | 1 jika customer menerima tawaran kampanye 2, jika tidak 0                     |
|                   | AcceptedCmp3          | 1 jika customer menerima tawaran kampanye 3, jika tidak 0                     |
|                   | AcceptedCmp4          | 1 jika customer menerima tawaran kampanye 4, jika tidak 0                     |
|                   | AcceptedCmp5          | 1 jika customer menerima tawaran kampanye 5, jika tidak 0                     |
|                   | Response              | 1 jika customer menerima tawaran kampanye terakhir, jika tidak 0              |
| **Place**         | NumWebPurchases       | Jumlah pembelian melalui website Supermarket                                  |
|                   | NumCatalogPurchases   | Jumlah pembelian melalui katalog Supermarket                                  |
|                   | NumStorePurchases     | Jumlah pembelian melalui toko Supermarket                                     |
|                   | NumWebVisitsMonth     | Jumlah pengunjungan ke website Supermarket selama sebulan terakhir            |

# DATA UNDERSTANDING
        Sebelum masuk ke analisis data, kita akan mengenal lebih lanjut dan mengolah dataset tersebut setelahnya. Di dalam tahapan *Data Understanding* kita akan mengetahui anomali-anomali apa saja yang terdapat di dalam dataset  yang nantinya akan disesuaikan dan ditangani dalam tahapan pengolahan yaitu *Data Cleaning*. Berikut adalah proses *Data Understanding*:   
## UNIQUE
       Pertama, kita akan mengidentifikasi data unik per kolom untuk mengetahui jenis insformasi/value yang terdapat dalam tiap kolom:   
* ID adalah unik per individu member 
* "year of birth" (tahun kelahiran) akan diganti menjadi value "age" (umur)
* dalam "education", value 'basic' dan '2n cycle' akan diredefinisikan
* dalam "marital status", value 'alone', 'absurd' dan 'YOLO' akan diredefinisikan
* "marital status" akan dikategorikan menjadi jumlah anggota rumahtangga 1 atau 2 orang, ditambah dengan jumlah dari "kidhome" dan "teenhome" = "household member"     
* "income" akan dikategorikan dengan cara mengkobinasi nilai dari "income" dan "household member" = "income class" 
* kolom "acceptedcmp" tidak berurutan sehingga perlu dirapihkan dengan cara diurutkan  
* "z_revenue" dan "z_costcontact" hanya memiliki 1 data unik, yang artinya kolom tersebut tidak mendiskripsikan maupun membedakan 1 member dengan yang lainnya karena itu kolom ini akan dihapus 
* "response" tidak didefinisikan secara jelas dan spesifik dan berpotensi tumpang tindih dengan data kampanye 5 (kampanye terakhir itu apakah kampanye 5 atau malah 6?) sehingga akan dihapus
## TYPE
        Kedua, kita akan melihat tipe data value di tiap kolom:
* "dt_customer" dideskripsikan sebagai tipe "object" padahal value sebenarnya adalah berupa tanggalan (date). Tipe data akan disesuaikan
## MISSING
        Ketiga, kita akan memeriksa apabila terdapat data tanpa value:
* terdapat 24 'n/a' value di dalam kolom "income". Row atau baris denga value 'n/a' akan dihapus
## NUMERICAL STATISTIC
        Keempat, kita akan melihat data numerical dan melihat distribusi, outliers dan corelation diantara data-data numerical tersebut:
* distribusi data pada kolom "year birth" dan "income" dinilai tidak normal dikarenakan adanya outliers yang perlu ditangani. Row dengan outliers ini akan dihapus
* ouliers pada produk tidak menjadi masalah karena konteks value yang berkaitan erat dengan jumlah pembelian per member , begitu pula pada data channel pembelian
* korelasi memperlihatkan beberapa poin menarik yang bisa menjadi pertimbangan dalam pengolahan data nantinya: 
    * korelasi antara "income" : "wine", "meat" : "catalogue", "store" 
    * korelasi antara "deals" : "kids", "teen" : "web"
## CATEGORICAL STATISTIC
        Kelima, kita akan melihat data kategorical dan diskripsinya: 
* data unik pada "edukasi" dan "marital status" akan disesuaikan dan disederhanakan untuk hasil pengolahan data yang lebh rapih dan terstruktur

# DATA CLEANING
Note: 2240 row x 29 kolom
* remove: 
    * "z_revenue" dan "z_costcontact" hanya memiliki 1 data unik, yang artinya kolom tersebut tidak mendiskripsikan maupun membedakan 1 member dengan yang lainnya
    * 24 'n/a' value di dalam kolom "income"
    * outliers: year birth, income
    * "response" tidak didefinisikan secara jelas dan spesifik dan berpotensi tumpang tindih dengan data kampanye lainnya
* change: 
    * "year of birth" (tahun kelahiran) akan diganti menjadi value "age" (umur) 
    * dalam "education", value 'basic' dan '2n cycle' akan diredefinisikan
            * Basic => Graduation || 2n Cycle => Master 
    * dalam "marital status", value 'alone', 'absurd' dan 'YOLO' akan diredefinisikan
            * Together => Married || Divorced, Widow, Alone, Absurd, YOLO => Single
    * "dt_customer" dideskripsikan sebagai tipe "object" padahal value sebenarnya adalah berupa tanggalan (datetime64)
    * kolom "acceptedcmp" tidak berurutan sehingga perlu dirapihkan dengan cara diurutkan
* add: 
    * "marital status" akan dikategorikan menjadi jumlah anggota rumahtangga 1 atau 2 orang, ditambah dengan jumlah dari "kidhome" dan "teenhome" = "household member"
    * "income" akan dikategorikan dengan cara mengkobinasi nilai dari "income" dan "household member" = "income class"
    * kolom yang mentotal jumlah campaign yang di terima per member = "TotAcceptedCmp" 
    * untuk RFM, dimana:
        * value Recency = "R_LastPurchase", dan dibagi menjadi 4 ranking (qcut) dimana ranking 1 tertinggi dan 4 terendah = "Rq_Ranks"
        * value Frequency diambil dari total purchasing di semua channel per member = "F_PlacePurchase", dan dibagi menjadi 4 ranking (qcut) dimana ranking 1 tertinggi dan 4 terendah = "Fq_Ranks" 
        * value Monetary diambil dari total pembelian produk per member = "M_ProductPurchase", dan dibagi menjadi 4 ranking (qcut) dimana ranking 1 tertinggi dan 4 terendah = "Mq_Ranks" 
    * total ranking RFM per member = "RFM_Score", akan manjadi acuan level membership yang dibagi menjadi 4 bagian, dimana Platinum adalah member dengan RFM Tertinggi (paling rajin dan banyak berbelanja), diikuti dengan Gold, Silver dan Bronze sebagai member dengan RFM terendah (paling jarang dan sedikit berbelanja) = "Membership"

# CLEANED DATA
Total: 2205 row x 33 kolom
| Kategori          | Kolom                 | Deskripsi                                                                     |
| ------------------|-----------------------|------------------------------------------------------------------------------ |
| **People**        | ID                    | Identitas unik customer                                                       |
|                   | Age                   | Umur customer                                                                 |
|                   | Education             | Level edukasi customer                                                        |
|                   | Household_Member      | Jumlah anggota rumahtangga customer                                           |
|                   | Income                | Pendapatan per tahun customer                                                 |
|                   | Income_Class          | Kelas ekonomi per income : household member                                   |
|                   | Dt_Customer           | Tanggal pendaftaran customer menjadi member Supermarket                       |
| **Products**      | MntWines              | Jumlah (buah) pembelian produk wine dalam 2 tahun terakhir                    |
|                   | MntFruits             | Jumlah (buah) pembelian produk buah dalam 2 tahun terakhir                    |
|                   | MntMeatProducts       | Jumlah (buah) pembelian produk daging dalam 2 tahun terakhir                  |
|                   | MntFishProducts       | Jumlah (buah) pembelian produk ikan dalam 2 tahun terakhir                    |
|                   | MntSweetProducts      | Jumlah (buah) pembelian produk manis dalam 2 tahun terakhir                   |
|                   | MntGoldProds          | Jumlah (buah) pembelian produk emas dalam 2 tahun terakhir                    |
|                   | M_ProductPurchase     | Total pembelian produk per member                                             |
|                   | Mq_Ranks              | Ranking total pembelian produk per member                                     |
|                   | R_LastPurchase        | Jumlah hari sejak terakhir kali customer berbelanja                           |
|                   | Rq_Ranks              | Ranking hari sejak terakhir kali customer berbelanja                          |
| **Place**         | NumWebVisitsMonth     | Jumlah pengunjungan ke website Supermarket selama sebulan terakhir            |
|                   | NumWebPurchases       | Jumlah pembelian melalui website Supermarket                                  |
|                   | NumCatalogPurchases   | Jumlah pembelian melalui katalog Supermarket                                  |
|                   | NumStorePurchases     | Jumlah pembelian melalui toko Supermarket                                     |
|                   | F_PlacePurchase       | Total purchasing di semua channel per member                                  |
|                   | Fq_Ranks              | Ranking total purchasing di semua channel per member                          |
| **RFM**           | RFM_Score             | Total ranking dari masing-masing kategori per member                          | 
|                   | Membership            | Label ranking berdasarkan RFM Score                                           |
| **Promotion**     | NumDealsPurchases     | Jumlah pembelian menggunakan/melalui promosi                                  |
|                   | AcceptedCmp1          | 1 jika customer menerima tawaran kampanye 1, jika tidak 0                     |
|                   | AcceptedCmp2          | 1 jika customer menerima tawaran kampanye 2, jika tidak 0                     |
|                   | AcceptedCmp3          | 1 jika customer menerima tawaran kampanye 3, jika tidak 0                     |
|                   | AcceptedCmp4          | 1 jika customer menerima tawaran kampanye 4, jika tidak 0                     |
|                   | AcceptedCmp5          | 1 jika customer menerima tawaran kampanye 5, jika tidak 0                     |
|                   | TotoAcceptedCmp       | Total penerimaan tawaran dari kampanye 1-5                                    |
|                   | Complain              | 1 jika customer pernah komplain selama 2 tahun terakhir, jika tidak 0         |   

# EXPLORATORY DATA ANALYSIS
