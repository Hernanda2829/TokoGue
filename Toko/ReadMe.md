# Membuat aplikasi berdasarkan kasus
Membuat aplikasi sederhana toko sesuai kasus yang telah diberikan dosen.

## Fitur
- User dapat melihat daftar makanan yang ditawarkan
- User dapat memasukkan atau menghapus makanan pilihan ke dalam keranjang
- User dapat melihat subtotal makanan yang terdapat pada keranjang
- User dapat melihat daftar voucher yang ditawarkan
- User dapat menggunakan salah satu voucher
- User dapat melihat harga total termasuk potongannya
## Penjelasan
- terdapat 3 class dalam folder controller, yaitu `MenuController.cs` , `PromoController.cs`, dan `MainWindowController.cs`.
	- `MenuController.cs` ada 3 method, yaitu `addItem();` berfungsi menambahkan item pada list , `getItem();` berfungsi mengembalikan nilai dari `menuController()` item, `menuItem()` berfungsi menyimpan data yang sudah ditambahkan.
  	- `PromoController`  ada 3 method, yaitu `addPromo();` berfungsi menambahkan promo pada list, `getPromo();` berfungsi mengembalikan nilai pada list, `PromoController();` berfungsi menyimpan data sebagai list 
  	- `MainWindowController.cs` berfungsi menambahkan Item dan Promo ke view, setelah itu menghapus item dari view, dan untuk menampilkan item dan promo yang dipilih
- Model terdapat 4 Class, yaitu `Item.cs`, `KeranjangBelanja.cs`, `Payment,cs`, dan `Promo.cs`
  - pada `Item.cs` berfungsi menampung itemnya
  - pada `Promo.cs` berfungsi menampung promonya
  - pada `KeranjangBelanja.cs` Berfungsi menampung item dan promo yang dipilih dan terdapat logika perhitungan jumlah subtotal, serta logika perhitungan banyak promo yang didapat
  ``` private void calculateSubTotal()
        {
            double subTotal = 0;
            double promo = 0;
            foreach (Item item in itemkeranjangBelanja)
            {
                subTotal += item.price;

            }
   ```

```  foreach (Diskon diskon in diskonDipakai)
            {
                if (diskon.potongan == 10000)
                {
                    promo = 10000;
                }
                else if (diskon.potongan == 30000)
                {

                    promo = (subTotal * 30 / 100);

                    if (promo > 30000)
                    {
                        promo = 30000;
                    }
                    else
                    {
                        promo = (subTotal * 30 / 100);
                    }

                }
                else if (diskon.potongan == 25000)
                {
                    promo = (subTotal * 25 / 100);

                }

            }
           
            payment.updateTotal(subTotal, promo);
        }
    }


    interface onKeranjangBelanjaChangedListener
    {
        void removeItemSucceed();
        void addItemSucceed();

        void addPromoSucceed();
        
    }
}
```

- terdapat 3 class untuk mengatur logika taampilannya yaitu `Menu.xaml.cs`, `Promo.xaml.cs`, dan `MainWindow.xaml.cs` 
 - pada `Menu.xaml.cs` terdapat penambahan item untuk dijadikan list berserta harganya yaitu 
``` private void generateContentMenu()
        {
            Item Menu1 = new Item("Coffe Late", 30000);
            Item Menu2 = new Item("Black Tea", 20000);
            Item Menu3 = new Item("Pizza", 75000);
            Item Menu4 = new Item("Milk Shake", 15000);
            Item Menu5 = new Item("Fried Frice Special", 45000);
            Item Menu6 = new Item("Watermelon Juice", 25000);
            Item Menu7 = new Item("Lemon Squash", 30000);

            menuController.addItem(Menu1);
            menuController.addItem(Menu2);
            menuController.addItem(Menu3);
            menuController.addItem(Menu4);
            menuController.addItem(Menu5);
            menuController.addItem(Menu6);
            menuController.addItem(Menu7);

            listMenu.Items.Refresh();

        }
```
  - pada `Promo.xaml.cs` terdapat penambahan promo untuk dijadikan list yaitu pada
  
  ```   private void generateContentPromo()
        {
            Diskon diskon1 = new Diskon("Promo Awal tahun Diskon 25 % ", 25000);
            Diskon diskon2 = new Diskon("Promo Tebus Murah Diskon 30 % atau maksimal 30.000", 30000);
            Diskon diskon3 = new Diskon("Promo Natal Potongan 10000", 10000);

            promoController.addPromo(diskon1);
            promoController.addPromo(diskon2);
            promoController.addPromo(diskon3);

            listBoxDaftarPromo.Items.Refresh();
        }
  ```
 - pada `MainWindow.xaml.cs`terdapat logika dari event misalkan penghapusan item yang sudah dipilih terdapat pada
 ```
 private void onlistKeranjangBelanjaDoubleClicked(object sender, MouseButtonEventArgs e)
        {
            if (MessageBox.Show("Apakah kamu ingin menghapus item ini?",
                   "Konfirmasi", MessageBoxButton.YesNo) == MessageBoxResult.Yes)
            {
                ListBox listBox = sender as ListBox;
                Item item = listBox.SelectedItem as Item;
                controller.removeItem(item);
            }
        }
 ```

## ClassDiagram



### Hernanda Giri Pramudita
### 19.11.2761