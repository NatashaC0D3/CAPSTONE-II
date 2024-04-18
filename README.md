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
# 1. DEMOGRAFIK PELANGGAN SUPERMARKET
## Numerical 
* dominasi umur: 35-55 tahun
* dominasi rumahtangga: 2-3 orang 
* dominasi income: $30.000 - $70.000 

perihal campaign, angka partisipasi per campaign rata-rata hanyalah 10% dari total 2205 member

## Categorical 
* dominasi edukasi: Graduasi (termasuk lulusan SMA) 
* dominasi kelas: medium class
* dominasi membership: silver

### income class
perlu diketahui bahwa standar kelas ekonomi ini menggunakan standar Pew Research tahun 2014 dimana pertimbangan bukan hanya melalui angka total annual income melainkan juga mempertimbangkan jumlah anggota rumahtangga dari si pemilik total annual income tersebut. 

perhitungan itu adalah sebagai berikut: 
| Household Member | middle income | upper income |
|------------------|---------------|--------------|
|        1         | $24,173 <     | $72,521 <    |
|        2         | $34,186 <     | $102,560 <   |
|        3         | $41,869 <     | $125,609 <   |
|        4         | $48,347 <     | $145,041 <   |
|        5         | $54,053 <     | $162,161 <   |

berdasarkan angka tersebut, dalam laporan ini kelas ekonomi (Income Class) dibafi menjadi 3: "Low" - berpendapatan lebih rendah dari middle income; "Medium" - dari middle income; dan "High" - dari upper income:

|     **TOTAL MEMBER: 2,205**     |   
|   Class   |   sum    |    %     |
|-----------|----------|----------|
|    Low    |   760    |  34.47%  |
|  Medium   |  1,324   |  60.05%  |
|   High    |   121    |  5.49%   |

### membership
untuk membership, penentuan menggunakan total ranking RFM (Recency - Frequency - Monetary) per yang dibagi menjadi 4 kelas.
* masing-masing RFM dikategorikan menjadi 4 kategori menggunakan 'qcut' function di pandas, dimana: 
    * Recency: rangking 1 mengindikasi jarak hari pembelian terpendek dan rangking 4 mengindikasi jarak hari pembelian terlama 
    * Frequency: rangking 1 mengindikasi jumlah kegiatan berbelanja di seluruh platform terbanyak dan rangking 4 mengindikasi jumlah paling sedikit
    * monetary: rangking 1 mengindikasi jumlah pembelian semua produk terbanyak dan rangking 4 mengindikasi jumlah pembelian paling sedikit

penglompokan berdasarkan total jumlah rangkin RFM adalah sebagai berikut: 

|           **TOTAL MEMBER: 2,205**         |
| Total RFM | Membership |   sum   |    %   |
|-----------|------------|---------|--------|
|   3-4     | Platinum   |   337   | 15.28% |
|   5-6     | Golden     |   528   | 23.59% |
|   7-9     | Silver     |   811   | 36.78% |
|  10-12    | Bronze     |   529   | 23.99% |

### household member
jumlah anggota rumahtangga per member diambil dari value marriage status dan jumlah anak dan remaja per member, dimana - 
* marriage status (status pernikahan) dibagi menjadi dua yaitu single (1 org) dan married (2 org) 
* ditambah dengan total jumlah anak dan remaja, maka akan terlihat seperti ini:
* Kelompok terbanyak ada pada angka 2-3 penghuni rumah tangga, dan rata-rata berada di kelompok Bronze dan Silver

### correlation
Apabila dilihat dalam bentuk korelasi akan terlihat seperti berikut: 
dapat disimpulkan terdapat 2 poin korelasi: 
1. antara "Income" dengan produk "wine" dan "Meat" serta aktivitas belanja melalui "catalogue" dan "store" 
2. antara "household member" dengan jumlah "web visit" dan jumlah "deals purchase"

### Wrap Up 1
Berdasarkan dari hasil distribusi numerical dan categorical, dapat disimpulkan bahwa customer Supermarket didominasi oleh:
Medium (Income Class) Silver (Membership), yang berpotensi merupakan anggota yang berumur kisaran 25-55 tahun berpendidikan maks S1, dan memiliki anggota rumah tangga sebanyak 2-3 orang

Namun, berdasarkan korelasi yaitu:
1. antara "Income" dengan produk "wine" dan "Meat" serta aktivitas belanja melalui "katalog" dan "store"
2. antara "household member" dengan jumlah "web visit" dan jumlah "deals purchase"

Maka terdapat kemungkinan kelompok terbesar hanyalah 1 dari target market yang sebenarnya ada untuk dikembangkan, seperti misalnya pasar market barang mewah (wine dan meat). Hal ini dikarenakan adanya potensi pembelian wine dan meat yang semakin tinggi seiring dengan tingginya pendapatan, namun disaat bersamaan adanya korelasi antara anggota keluarga dengan diskon yang di claim oleh peserta member

### Campaign
diketahui bahwa angka partisipasi kampanye dinilai kecil. mari kita lihat penjabarannya:

#### Partisipasi berdasarkan Income Class
Dari total member 2.205 orang: 
* total partisipan -
    * kampanye 1: 142 orang (6.4%)
    * kampanye 2: 30 orang (1.4%)
    * kampanye 3: 163 orang (7.4%)
    * kampanye 4: 164 orang (7.4%)
    * kampanye 5: 161 orang (7.3%)
* partisipan tertinggi berasala dari Income Class Medium dengan angka tertinggi di 141 orang pada kampanye ke 4 atau setara 6.4% dari total seluruh member atau 10.56% dari total kelas Medium
* dari kelima kampanye, partisipan tertinggi selalu dimenangkan oleh kelas Medium 
* jika dilihat dari total partisipan, maka hanya kampanye 2 yang memiliki tingkat partisipasi sangat rendah hingga dibawah 50 orang (sementara yang lainnya berada diangka 150an orang)
* hanya kampanye 3 yang memiliki angka partisipasi yang cukup signifikan dari kelas Low yaitu 65 orang atau setara 3% dari total seluruh member atau 8.6% dari total kelas Low

#### Partisipasi berdasarkan Membership
Dari total member 2,205 orang: 
* total partisipan -
    * kampanye 1: 142 orang (6.4%)
    * kampanye 2: 30 orang (1.4%)
    * kampanye 3: 163 orang (7.4%)
    * kampanye 4: 164 orang (7.4%)
    * kampanye 5: 161 orang (7.3%)
* Member Bronze dan Silver adalah partisipan teraktif dengan rata-rata 55-60 orang berpartisipasi per kampanye atau setara 2.6% dari total jumlah seluruh member atau 10.9% dari total member Bronze dan 7% dari total member Silver
*  Member Platinum hanya berpartisi pada 2 kampanye yaitu 2 dan 3

#### Total Partisipan
Dari total member 2.205 orang:
* total partisipan  per income-
    * Low = 71 (9,34%)
    * Medium = 475 (35,88%)
    * **High = 114 (94,22%)**
* total partisipan per membership-
    * **Bronze = 310 (58,6%)**
    * Silver = 271 (33,42%)
    * Gold = 44 (8,33%)
    * Platinum = 35 (10.39%)

Peserta terbesar yang ikut serta dalam kampanye total adalah berasal dari kelompok Medium Bronze, diikuti oleh Medium Silver dan High Bronze.   
Apabila dilihat dari segi kelas dan membership, kelas high income justru yang paling rajin ikut berpartisipasi saat diskon dengan angka hampir mencapai 100% , walaupun dalam segi RFM, cukup rendah yaitu pada level membership Bronze. 

Peserta terbesar yang ikut serta dalam kampanye total adalah berasal dari kelompok Medium Bronze, diikuti oleh Medium Silver dan High Bronze.   
Apabila dilihat dari segi kelas dan membership, kelas high income justru yang paling rajin ikut berpartisipasi saat diskon dengan angka hampir mencapai 100% , walaupun dalam segi RFM, cukup rendah yaitu pada level membership Bronze. 

## Wrap Up 2
Sebelumnya dinyatakan bahwa berdasarkan hitungan keseluruhan kelompok terbesar adalah  Medium (Income Class) Silver (Membership), yang berpotensi merupakan anggota yang berumur kisaran 25-55 tahun berpendidikan maks S1, dan memiliki anggota rumah tangga sebanyak 2-3 orang. 

Namun menariknya -  diluar fakta bahwa jumlah total partisipasi kegiatan kampanye marketing yang kecil (<10%) - partisipan dari kelompok High (Income Class),  Bronze (Membership) maupun Silver (Membership) secara persentase hampir 100%. Hal ini jelas menggarisbawahi bahwa kegiatan kampanye pemasaran yang selama ini dilaksanakan sedikit kurang tepat mengingat terdapat grup besar yang tidak tertarget dengan baik. 

**Namun apakah artinya kampanye pemasaran yang selama ini dapat dinilai gagal? Bagaimana dengan hubungan 2 korelasi yang telah disebutkan sebelumnya?**


