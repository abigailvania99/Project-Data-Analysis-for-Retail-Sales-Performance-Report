# Project-Data-Analysis-for-Retail-Sales-Performance-Report
DQLab Project SQL
<hr>

### <b>Overall Performance by Year</b>
Buatlah Query dengan menggunakan SQL untuk mendapatkan total penjualan (sales) dan jumlah order (number_of_order) dari tahun 2009 sampai 2012 (years). 

Output yang harus dihasilkan adalah sebagai berikut.
<br>
<img src="https://miro.medium.com/max/438/1*24PfZ-lAsUDow1LnWVTJNg.png">


Berikut Codenya:
```
SELECT year(order_date) as years, sum(sales) as sales, COUNT(order_id) as number_of_order
FROM dqlab_sales_store
WHERE order_status='Order Finished'
GROUP BY year(order_date)
```

### <b>Overall Performance by Product Sub Category</b>
Buatlah Query dengan menggunakan SQL untuk mendapatkan total penjualan (sales) berdasarkan sub category dari produk (product_sub_category) pada tahun 2011 dan 2012 saja (years) 

Output yang harus dihasilkan adalah sebagai berikut.
<br>
<img src="https://miro.medium.com/max/536/1*FgcJnl9cXNkKhTQBrlqnig.png">


Berikut Codenya:
```
SELECT year(order_date) as years, product_sub_category, sum(sales) as sales
FROM dqlab_sales_store
WHERE order_status='order finished' AND YEAR(order_date) IN("2011","2012")
GROUP BY product_sub_category, years
ORDER BY years, sum(sales) desc

```

### <b>Promotion Effectiveness and Efficiency by Years</b>
Pada bagian ini kita akan melakukan analisa terhadap efektifitas dan efisiensi dari promosi yang sudah dilakukan selama ini

Efektifitas dan efisiensi dari promosi yang dilakukan akan dianalisa berdasarkan Burn Rate yaitu dengan membandigkan total value promosi yang dikeluarkan terhadap total sales yang diperoleh

DQLab berharap bahwa burn rate tetap berada diangka maskimum 4.5%

Formula untuk burn rate : (total discount / total sales) * 100

Buatkan Derived Tables untuk menghitung total sales (sales) dan total discount (promotion_value) berdasarkan tahun(years) dan formulasikan persentase burn rate nya (burn_rate_percentage).

Adapun output yang seharusnya dihasilkan adalah sebagai berikut.
<br>
<img src="https://miro.medium.com/max/689/1*1J1en-BE4IVJ2K2JUKVgjQ.png">


Berikut Codenya:
```
SELECT
DISTINCT YEAR(order_date) AS years,
 SUM(sales) AS sales,
 SUM(discount_value) AS promotion_value,
 ROUND(SUM(discount_value)*100/SUM(sales),2) as  burn_rate_percentage
FROM
 dqlab_sales_store
WHERE
 order_status = 'Order Finished'
GROUP BY
 YEAR(order_date)
ORDER BY
 YEAR(order_date);
```


### <b>Promotion Effectiveness and Efficiency by Product Sub Category</b>
Pada bagian ini kita akan melakukan analisa terhadap efektifitas dan efisiensi dari promosi yang sudah dilakukan selama ini seperti pada bagian sebelumnya. 

Akan tetapi, ada kolom yang harus ditambahkan, yaitu : product_sub_category dan product_category

Adapun output yang seharusnya dihasilkan adalah sebagai berikut.

<br>
<img src="https://miro.medium.com/max/875/1*cPD4Ee4_drRQE_j9jJOr0Q.png">


Berikut Codenya:
```
SELECT
 DISTINCT YEAR(order_date) AS years,
 product_sub_category,
 product_category,
 SUM(sales) AS sales,
 SUM(discount_value) AS promotion_value,
 ROUND(SUM(discount_value)*100/SUM(sales),2) as  burn_rate_percentage
FROM
 dqlab_sales_store
WHERE
 order_status = 'Order Finished' and YEAR(order_date) = 2012
GROUP BY
 YEAR(order_date),
 product_sub_category,
 product_category
ORDER BY
 YEAR(order_date),
 SUM(sales) DESC;
```

### <b>Customers Transactions per Year</b>
DQLab Store ingin mengetahui jumlah customer (number_of_customer) yang bertransaksi setiap tahun dari 2009 sampai 2012 (years).

Adapun output yang seharusnya dihasilkan adalah sebagai berikut.
<br>
<img src="https://miro.medium.com/max/414/1*kXi2VBzWEAYJiHJF-XB2HQ.png">


Berikut Codenya:
```
SELECT YEAR(order_date)as years, COUNT(DISTINCT LOWER(customer)) as number_of_customer
FROM dqlab_sales_store
WHERE order_status = 'Order Finished'
GROUP BY YEAR(order_date)
ORDER BY YEAR(order_date)
```
