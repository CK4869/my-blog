tạo model từ database
Scaffold-Dbcontext "Data Source=COOL-KID\SQLEXPRESS;Initial Catalog=QLBanHang;Integrated Security=True" Microsoft.EntityFrameworkCore.SqlServer -OutputDir models

cập nhật model khi database thay đổi
Scaffold-Dbcontext "Data Source=COOL-KID\SQLEXPRESS;Initial Catalog=QLBanHang;Integrated Security=True" Microsoft.EntityFrameworkCore.SqlServer -OutputDir models -Force


số thập phân > 0: "^\d+\.0*[1-9]+\d*$"
số thực không âm (>= 0): ^\d+\.?(\d+|\d*)$
số nguyên > 0: "^\d*[1-9]{1}\d*$"


<Application x:Class="De_thi_mau_00.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:De_thi_mau_00"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <Style TargetType="TextBox">
            <Style.Triggers>
                <Trigger Property="IsMouseOver" Value="True">
                    <Setter Property="Foreground" Value="Red"></Setter>
                    <Setter Property="Background" Value="Yellow"></Setter>
                </Trigger>
            </Style.Triggers>
        </Style>
        
        <ControlTemplate x:Key="ButtonTemplate" TargetType="{x:Type Button}">
            <Grid>
                <Ellipse Fill="Cyan"></Ellipse>
                <ContentPresenter  VerticalAlignment="Center" HorizontalAlignment="Center"></ContentPresenter>
            </Grid>
        </ControlTemplate>

        <Style x:Key="WrappedColumnHeaderStyle" TargetType="{x:Type DataGridColumnHeader}">
            <Setter Property="ContentTemplate">
                <Setter.Value>
                    <DataTemplate>
                        <TextBlock TextWrapping="Wrap" Text="{Binding}" FontWeight="Bold"></TextBlock>
                    </DataTemplate>
                </Setter.Value>
            </Setter>
            <Setter Property="HorizontalContentAlignment" Value="Center"></Setter>
            <Setter Property="HorizontalAlignment" Value="Stretch"></Setter>
            <Setter Property="TextBlock.TextAlignment" Value="Center"></Setter>
        </Style>

        <Style x:Key="CellStyle" TargetType="{x:Type DataGridCell}">
            <Setter Property="Foreground" Value="DarkBlue"></Setter>
            <Setter Property="FontWeight" Value="Bold"></Setter>
            <Setter Property="TextBlock.TextAlignment" Value="Right"></Setter>
            <Setter Property="FontStyle" Value="Italic"></Setter>
        </Style>
    </Application.Resources>
</Application>




<Window x:Class="De_thi_mau_00.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:De_thi_mau_00"
        mc:Ignorable="d"
        Title="MainWindow" Height="700" Width="800"
        FontSize="16"
        WindowStartupLocation="CenterScreen"
        Loaded="Window_Loaded">
    <Grid Margin="10">
        <Label Content="SALES MANAGEMENT" HorizontalAlignment="Center" VerticalAlignment="Top" FontSize="22" FontWeight="Bold"/>
        <Label Content="Product ID" HorizontalAlignment="Left" Margin="164,48,0,0" VerticalAlignment="Top" Width="150" Height="36"/>
        <Label Content="Product Name" HorizontalAlignment="Left" Margin="164,97,0,0" VerticalAlignment="Top" Width="150" Height="36"/>
        <Label Content="Unit Price" HorizontalAlignment="Left" Margin="164,147,0,0" VerticalAlignment="Top" Width="150" Height="36"/>
        <Label Content="Quantity" HorizontalAlignment="Left" Margin="164,196,0,0" VerticalAlignment="Top" Width="150" Height="36"/>
        <Label Content="Category" HorizontalAlignment="Left" Margin="164,248,0,0" VerticalAlignment="Top" Width="150" Height="36"/>

        <TextBox x:Name="textBoxProductID" HorizontalAlignment="Left" Margin="342,48,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="300" Height="36"/>
        <TextBox x:Name="textBoxProductName" HorizontalAlignment="Left" Margin="342,97,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="300" Height="36"/>
        <TextBox x:Name="textBoxUnitPrice" HorizontalAlignment="Left" Margin="342,147,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="300" Height="36"/>
        <TextBox x:Name="textBoxQuantity" HorizontalAlignment="Left" Margin="342,196,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="300" Height="36"/>
        <ComboBox x:Name="comboBoxCategory" HorizontalAlignment="Left" Margin="342,248,0,0" VerticalAlignment="Top" Width="300" Height="36"/>

        <DataGrid x:Name="dataGrid" HorizontalAlignment="Center" Height="221" Margin="0,300,0,0" VerticalAlignment="Top" Width="760"
                  AutoGenerateColumns="False" 
                  EnableRowVirtualization="False" 
                  IsReadOnly="True"
                  SelectedCellsChanged="dataGrid_SelectedCellsChanged">
            <DataGrid.Columns>
                <DataGridTextColumn Header="Product ID" Binding="{Binding ProductID}" HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" Width=".2*"></DataGridTextColumn>
                <DataGridTextColumn Header="Product Name" Binding="{Binding ProductName}" HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" Width=".2*"></DataGridTextColumn>
                <DataGridTextColumn Header="Category ID" Binding="{Binding CategoryID}" HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" Width=".2*"></DataGridTextColumn>
                <DataGridTextColumn Header="Unit Price" Binding="{Binding UnitPrice, StringFormat={}{0:N0}}" HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" Width=".2*"></DataGridTextColumn>
                <DataGridTextColumn Header="Quantity" Binding="{Binding Quantity, StringFormat={}{0:N0}}" HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" Width=".2*"></DataGridTextColumn>
                <DataGridTextColumn Header="Amount" Binding="{Binding Amount, StringFormat=N0}"  HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" CellStyle="{StaticResource CellStyle}" Width=".2*"></DataGridTextColumn>
            </DataGrid.Columns>
        </DataGrid>

        <Button x:Name="buttonInsert" Content="Insert" Template="{StaticResource ButtonTemplate}" HorizontalAlignment="Left" Margin="164,547,0,0" VerticalAlignment="Top" Width="100" Height="36" Click="buttonInsert_Click"/>
        <Button x:Name="buttonUpdate" Content="Update" Template="{StaticResource ButtonTemplate}" HorizontalAlignment="Left" Margin="289,547,0,0" VerticalAlignment="Top" Width="100" Height="36" Click="buttonUpdate_Click"/>
        <Button x:Name="buttonDelete" Content="Delete" Template="{StaticResource ButtonTemplate}" HorizontalAlignment="Left" Margin="414,547,0,0" VerticalAlignment="Top" Width="100" Height="36" Click="buttonDelete_Click"/>
        <Button x:Name="buttonSearch" Content="Search" Template="{StaticResource ButtonTemplate}" HorizontalAlignment="Left" Margin="538,547,0,0" VerticalAlignment="Top" Width="100" Height="36" Click="buttonSearch_Click"/>

        <Label x:Name="labelErrorMsg" Foreground="Red" FontWeight="Bold" HorizontalAlignment="Center" Margin="0,603,0,0" VerticalAlignment="Top" Width="760" Height="36" HorizontalContentAlignment="Center"/>

    </Grid>
</Window>



using De_thi_mau_00.model;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Text.RegularExpressions;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace De_thi_mau_00
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        SALESMANAGEMENTContext db = new();
        List<Category> categories = new();
        public MainWindow()
        {
            InitializeComponent();
        }
        private void refreshData()
        {
            var products = from pro in db.Products
                           where pro.Quantity <= 150
                           orderby pro.ProductName ascending
                           select new
                           {
                               ProductID = pro.ProductId,
                               ProductName = pro.ProductName,
                               CategoryID = pro.CatId,
                               UnitPrice = pro.UnitPrice,
                               Quantity = pro.Quantity,
                               Amount = pro.UnitPrice * pro.Quantity,
                           };
            dataGrid.ItemsSource = products.ToList();
        }
        private void Window_Loaded(object sender, RoutedEventArgs e)
        {
            refreshData();

            categories = (from cate in db.Categories
                          select cate).ToList<Category>();
            comboBoxCategory.ItemsSource = categories;
            comboBoxCategory.DisplayMemberPath = "CatName";
            comboBoxCategory.SelectedValuePath = "CatID";

            textBoxProductID.Focus();
        }
        private void dataGrid_SelectedCellsChanged(object sender, SelectedCellsChangedEventArgs e)
        {
            dynamic selectedItem = dataGrid.SelectedItem;
            if (selectedItem != null)
            {
                textBoxProductID.Text = selectedItem.ProductID;
                textBoxProductName.Text = selectedItem.ProductName;
                textBoxQuantity.Text = selectedItem.Quantity.ToString();
                textBoxUnitPrice.Text = selectedItem.UnitPrice.ToString();
                comboBoxCategory.SelectedIndex = categories.Select(e => e.CatId).ToList().IndexOf(selectedItem.CategoryID);
            }
        }

        private void buttonInsert_Click(object sender, RoutedEventArgs e)
        {
            if (isCheckValidateInput())
            {
                var testProduct = (from pro in db.Products
                            where pro.ProductId.Equals(textBoxProductID.Text.Trim())
                            select pro).SingleOrDefault();
                if(testProduct != null)
                {
                    MessageBox.Show("Mã sản phẩm đã tồn tại", "Cảnh báo", MessageBoxButton.OK, MessageBoxImage.Warning);
                    return;
                }
                else
                {
                    Product newProduct = new();
                    newProduct.ProductId = textBoxProductID.Text.Trim();
                    newProduct.ProductName = textBoxProductName.Text.Trim();
                    newProduct.UnitPrice = Convert.ToInt32(textBoxUnitPrice.Text);
                    newProduct.Quantity = Convert.ToInt32(textBoxQuantity.Text);
                    newProduct.CatId = (comboBoxCategory.SelectedItem as Category).CatId;

                    db.Products.Add(newProduct);
                    db.SaveChanges();
                    refreshData();
                }

            }
        }

        private bool isCheckValidateInput()
        {
            labelErrorMsg.Content = "";
            string productID = textBoxProductID.Text.Trim();
            string productName = textBoxProductName.Text.Trim();
            string quantity = textBoxQuantity.Text.Trim();
            string unitPrice = textBoxUnitPrice.Text.Trim();
            var category = comboBoxCategory.SelectedItem as Category;
            if (productID == "" || productName == "" || quantity == "" || unitPrice == "" || category == null)
            {
                labelErrorMsg.Content = "Vui lòng nhập đủ các trường";
                return false;
            }
            if (!Regex.IsMatch(quantity, @"^\d*[1-9]{1}\d*$") || !Regex.IsMatch(unitPrice, @"^\d*[1-9]{1}\d*$"))
            {
                labelErrorMsg.Content = " Quantity và Unit Price phải là số nguyên dương.";
                return false;
            }
            return true;
        }

        private void buttonUpdate_Click(object sender, RoutedEventArgs e)
        {
            var product = (from pro in db.Products
                           where pro.ProductId.Equals(textBoxProductID.Text.Trim())
                           select pro).SingleOrDefault();
            if(product == null)
            {
                MessageBox.Show($"Không tìm thấy sản phẩm", "Thông báo", MessageBoxButton.OK, MessageBoxImage.Information);
            }
            else
            {
                if (isCheckValidateInput())
                {
                    product.ProductName = textBoxProductName.Text.Trim();
                    product.UnitPrice = Convert.ToInt32(textBoxUnitPrice.Text);
                    product.Quantity = Convert.ToInt32(textBoxQuantity.Text);
                    product.CatId = (comboBoxCategory.SelectedItem as Category).CatId;

                    db.SaveChanges();
                    refreshData();
                }
            }
        }

        private void buttonDelete_Click(object sender, RoutedEventArgs e)
        {
            var product = (from pro in db.Products
                           where pro.ProductId.Equals(textBoxProductID.Text.Trim())
                           select pro).SingleOrDefault();
            if (product == null)
            {
                MessageBox.Show($"Không tìm thấy sản phẩm", "Thông báo", MessageBoxButton.OK, MessageBoxImage.Information);
            }
            else
            {
                var deleteAction = MessageBox.Show("Bạn có đồng ý xoá?", "Xác nhận", MessageBoxButton.YesNo);
                if (deleteAction == MessageBoxResult.Yes)
                {
                    db.Products.Remove(product);
                    db.SaveChanges();
                    refreshData();
                }
            }
        }

        private void buttonSearch_Click(object sender, RoutedEventArgs e)
        {
            Window1 window1 = new Window1();
            window1.Show();
        }
    }
}
  
  
<Window x:Class="De_thi_mau_00.Window1"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:De_thi_mau_00"
        mc:Ignorable="d"
        Title="Window1" Height="450" Width="800"
        FontSize="16"
        WindowStartupLocation="CenterScreen"
        Loaded="Window_Loaded">
    <Grid Margin="10">
        <DataGrid x:Name="dataGrid" AutoGenerateColumns="False" IsReadOnly="True">
            <DataGrid.Columns>
                <DataGridTextColumn Header="Category ID" Binding="{Binding CategoryID}" HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" Width=".2*"></DataGridTextColumn>
                <DataGridTextColumn Header="Category Name" Binding="{Binding CategoryName}" HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" Width=".2*"></DataGridTextColumn>
                <DataGridTextColumn Header="Total Money Product" Binding="{Binding TotalMoneyProduct, StringFormat={}{0:N0}}" HeaderStyle="{StaticResource WrappedColumnHeaderStyle}" Width=".2*"></DataGridTextColumn>
            </DataGrid.Columns>
        </DataGrid>
    </Grid>
</Window>

  
  
using De_thi_mau_00.model;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Shapes;

namespace De_thi_mau_00
{
    /// <summary>
    /// Interaction logic for Window1.xaml
    /// </summary>
    public partial class Window1 : Window
    {
        SALESMANAGEMENTContext db = new();
        public Window1()
        {
            InitializeComponent();
        }

        private void Window_Loaded(object sender, RoutedEventArgs e)
        {
            var query1 = from pro in db.Products
                         group pro by pro.CatId into cateGroup
                         select new
                         {
                             CategoryID = cateGroup.Key,
                             TotalMoneyProduct = cateGroup.Sum(x => x.Quantity * x.UnitPrice),
                         };

            var query2 = from cate1 in query1
                         join cate2 in db.Categories on cate1.CategoryID equals cate2.CatId
                         select new
                         {
                             CategoryID = cate1.CategoryID,
                             CategoryName = cate2.CatName,
                             TotalMoneyProduct = cate1.TotalMoneyProduct,
                         };

            dataGrid.ItemsSource = query2.ToList();
        }
    }
}

