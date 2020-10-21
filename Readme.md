# The Cashier App
Fungsi dari aplikasi ini yaitu untuk menejemen barang (sejenis notes), jadi kita bisa menambahkan item/barang kedalamnya.

## Scope and Functionalities
* User dapat menginputkan huruf dan angka.
* User dapat menambahkan dan melihat barang yang sudah ditambahkan pada tabel.
* User juga dapat melihat total harga barang yang sudah ditambahkan.

## How Does it works?
Diawali pada method `MainWindow()` pada `class MainWindow.xaml.cs`, 
kita deklarasikan `InitializeComponent()` yang berfungsi untuk menganalisasi objek yang telah dibuat, serta membuat class `Calculator.cs`
```csharp
public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.getListItem();
        }
```
Data yang diinputkan oleh user akan dimasukkan pada class `Item.cs` untuk diolah datanya dan kemudian akan dimasukkan ke objek calculator.
Jadi jika button di click oleh user maka akan menambahkan title, quantity, type, dan price. 
```csharp
private void AddButton_Click(object sender, RoutedEventArgs e)
        {
            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);

            Item item = new Item(new Random().Next(), title, quantity, price, type);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = string.Format("Rp. {0}", total);
            listBox.Items.Refresh();
        }
```
Pada class `Calculator.cs` digunakan untuk menambahkan list item dan menghitung total harga. 
```csharp
public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }
```