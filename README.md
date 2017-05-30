# Portfolio
## Csharp
### oef 5.8:
https://dotnetfiddle.net/RKK9fm

oef 5.9 (Voluma van kubus berekenen):
https://dotnetfiddle.net/zuhvul
```C#
public static double KubusVolume(double zijde)
	{
		double voluma = Math.Pow(zijde, 3);
		return voluma;
	}
	
	public static void Main()
	{
		double vol = KubusVolume(1.2);
		Console.WriteLine(vol);
	}
  ```
  
###  oef 5.10:
  https://dotnetfiddle.net/sRYs4Y
  ```C#
  public static double OppCirkel(double straal)
	{
		double oppervlakte = Math.Pow(straal, 2) * Math.PI;
		return oppervlakte;
	}
	
	public static void Main()
	{
		double a = OppCirkel(1.25);
		Console.WriteLine(a);
	}
```

### oef 5.11:
https://dotnetfiddle.net/csaxjl
```C#
public static int TijdInSec(int h, int min, int s)
	{
		int urenNaarSeconden = h * 3600;
		int minutenNaarSeconden = min * 60;
		
		int seconden = urenNaarSeconden + minutenNaarSeconden + s;
		return seconden;
	}
	
	public static void Main()
	{
		int seconden = TijdInSec(1, 1, 2);
		Console.WriteLine(seconden);
	}
```

### 5.12 (een uitbreiding van 5.10):
https://dotnetfiddle.net/DDHHKX

### Gewone methode vs die met return-waarde
* Als u een gewone methode aanroept, **doet** het programma er iets mee als u dat later (of eerder) opvraagt, zoals het tekenen van een ellipse:
```C#
private void Ellipse(int straal)
{
Ellipse ell = new Ellipse();
ell.Width = straal;
ell.Height = straal;
ell.Margin = new Thickness(10, 10, 0, 0);
ell.Fill = new SolidColorBrush(Colors.Black);
canvas.children.Add(ell);
}
```
dit moet altijd "void" zijn.

* Als u een methode met een `return`-statement aanroept, kan u er effectief mee verder **werken/rekenen**, bv. als in oef **5.11**. U kan met `TijdInSec()` effectief mee verder werken het als een variable declareren en zelfs op berekenen als u dat wil. Dit heeft altijd een type, bv. een int. als de uiteindelijke waarde(n) een geheel getal (integer) moet zijn.

### vb.-oef van H 6.8 De klasse DispatcherTimer: Raindrops
Voeg eerst bij de ```using```-namespaces ```using System.Windows.Threading;``` toe!
```C#
namespace Raindrups
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        private Random random = new Random();
        private double x, y, grootte;
        private SolidColorBrush brush;
        private DispatcherTimer timer = new DispatcherTimer();

        public MainWindow()
        {
            InitializeComponent();

            sliderLabel.Content = Convert.ToString(slider.Value);
            brush = new SolidColorBrush(Colors.Blue);
            timer.Interval = TimeSpan.FromMilliseconds(slider.Value);
            timer.Tick += timer_Tick;
        }

        private void timer_Tick(object sender, EventArgs e)
        {
            x = random.Next(0, Convert.ToInt32(canvas.Width));
            y = random.Next(0, Convert.ToInt32(canvas.Height));
            grootte = random.Next(1, 40);

            Ellipse ell = new Ellipse();
            ell.Width = grootte;
            ell.Height = ell.Width;
            ell.Stroke = brush;
            ell.Fill = brush;
            ell.Margin = new Thickness(x, y, 0, 0);
            canvas.Children.Add(ell);

            //nieuw interval voor timer
            timer.Stop();
            int ms = random.Next(Convert.ToInt32(slider.Value));
            timer.Interval = TimeSpan.FromMilliseconds(ms);
            timer.Start();
        }

        private void slider_ValueChanged(object sender, RoutedPropertyChangedEventArgs<double> e)
        {
            int timeGap = Convert.ToInt32(slider.Value);
            sliderLabel.Content = Convert.ToString(timeGap);
        }

        private void startButton_Click(object sender, RoutedEventArgs e)
        {
            timer.Start();
        }

        private void closeButton_Click(object sender, RoutedEventArgs e)
        {
            timer.Stop();
        }

        private void leegButton_Click(object sender, RoutedEventArgs e)
        {
            canvas.Children.Clear();
        }
    }
}
```
Voeg een label, 3 knoppen, een slider en een canvas toe. De canvas moet in de XAML-code ``height``- en ``width``-properties hebben!
iets als dit:
```XAML
<Canvas x:Name="canvas" Width="420" Height="299" Background="LightGray" Margin="97,10,0,10"/>
```
PS: ik was te lui om in de naam van de namespace de veranderen (er staat "Raindrups" i.p.v. "Raindrops")

### Extra: ```Timer``` in Console-app
```C#
namespace ConsoleTimer
{
    class Program
    {
        private static Random rnd = new Random();
        private static Timer timer = new Timer();

        static void Main(string[] args)
        {
            int interval = rnd.Next(1500);
            timer.Interval = Convert.ToDouble(interval);
            timer.Elapsed += Timer_Elapsed;

            timer.Start();
            Console.ReadLine();
        }

        private static void Timer_Elapsed(object sender, ElapsedEventArgs e)
        {
            Console.WriteLine("hallo");
        }
    }
}
```
Deze code print om de rnd aantal seconden het woorde **"hallo"** af. ``rnd`` is een ```Random``` van max. 1,5 s (1500 ms). In een console-app is het i.p.v. ```timer.Tick```, ``` timer.Elapsed```. ```Console.Readline()``` wacht totdat u iets invoert vooraleer het het programma gaat sluiten. Hij leest als het ware de input. Als u op ``Enter`` drukt, zal het stoppen en als u een letter intypt, komt dat erbij op te staan :satisfied:.
PS: Voeg bij de namspace ook nog het volgende toe: ```using System.Timers;```

### Mijn Fizz Buzz Test
In de Fizz Buzz Test was het de bedoeling dat er de getallen van 1 tot en met 100 wordt afgeprint op de console. Als het getal een veelvoud is van (deelbaar is door) 3, komt er "Fizz" in de plaats te staan. Als het getal een veelvoud is van 5, wordt er "Buzz" afgeprint en als het getal deelbaar is door beide getallen, komt er "FizzBuzz" in de plaats te staan. Dit is mijn code:
```C#
static void Main(string[] args)
        {
            for (int i = 1; i <= 100; i++)
            {
                if (i % 3 == 0 && i % 5 == 0)
                {
                    Console.WriteLine("FizzBuzz");
                }
                else if (i % 5 == 0)
                {
                    Console.WriteLine("Buzz");
                }
                else if (i % 3 == 0)
                {
                    Console.WriteLine("Fizz");
                }
                else
                {
                    Console.WriteLine(i);
                }
            }
        }
```
PS: bij de enkelvoudige iteratie, **moet** u als tweede vergelijkingsoperator "```i <= 100```" invullen, i.p.v. "```i == 100```", omdat ```i``` in het begint gelijk is aan 1 en niet aan 100, maar wel kleiner is dan of gelijk aan 100!

### oef 1 en 2 over de enkelvoudige en tweevoudige selectie
```C#
 private static double BerekenWeekLoon(double uurloon = 14, int aantalUurGewerkt = 38)
        {
            double weekloon = 0;
            double standaardWeekloon = uurloon * aantalUurGewerkt;

            if (aantalUurGewerkt <= 38)
            {
                weekloon = standaardWeekloon;
            }
            else
            {
                int overuren = aantalUurGewerkt - 38;
                weekloon = (uurloon * 38) + (uurloon * 1.35 * overuren);
            }

            return weekloon;
        }

        private static double BerekenVP(double ap)
        {
            double vp = 2 * ap;

            if (vp > 80)
            {
                vp -= vp * 0.3;
            }
            else if (vp > 40)
            {
                vp -= vp * 0.2;
            }

            return vp;
        }

        static void Main(string[] args)
        {
            //Weekloon
            Console.WriteLine("Weekloon");
            Console.WriteLine(BerekenWeekLoon(14, 45));
            Console.WriteLine(BerekenWeekLoon(14, 25));
            Console.WriteLine();

            //VP
            Console.WriteLine("Verkoopprijs");
            Console.WriteLine(BerekenVP(36));
            Console.WriteLine(BerekenVP(48));
            Console.WriteLine(BerekenVP(85));
            Console.WriteLine();
        }
```

### oef 8.11 Kinderliedje: 7 kleine Visjes
Ik heb in dotnetfiddle een code geschreven die de tekst van "7 kleine visjes" print. Die 7 worden er telkens minder ... Dit was een beetje het allereerste 'horrorverhaaltje'.
```C#
using System;
					
public class Program
{
	public static void Main()
	{
		for (int aantalVissen = 7; aantalVissen > 0; aantalVissen--)
		{
			if (aantalVissen == 1)
			{
				Console.WriteLine(aantalVissen + " klein Visje zwom naar de zee.");
				Console.WriteLine("``Dat is goed``, zei de moeder, ``maar ik ga niet mee.``");
				Console.WriteLine("``Ik blijf liever in die vieze, ouwe sloot,");
				Console.WriteLine("want in de zee daar zwemmen Haaien en die bijten je dan ... dood!``");
				Console.WriteLine();
			}
			else
			{
				Console.WriteLine(aantalVissen + " kleine Visjes, die zwommen naar de zee");
				Console.WriteLine("``Dat is goed``, zei de moeder, ``maar ik ga niet mee.``");
				Console.WriteLine("``Ik blijf liever in die vieze, ouwe sloot,");
				Console.WriteLine("want in de zee daar zwemmen Haaien en die bijten jullie dan ... dood!");
				Console.WriteLine();
			}
		}
	}
}
```
https://dotnetfiddle.net/LddqqX

### H10: in dit programma kunnen we erg veel ballonnen toevoegen, maar op den duur wordt het erg onhandig:
```C#
public partial class MainWindow : Window
    {

        private Ellipse ballon = new Ellipse();
        private int bovenVerplaatsen = 100;

        private Ellipse ballon2 = new Ellipse();

        public MainWindow()
        {
            InitializeComponent();

            ballon.Width = 50;
            ballon.Height = ballon.Width;
            ballon.Stroke = new SolidColorBrush(Colors.Red);
            ballon.Margin = new Thickness(200, bovenVerplaatsen, 0, 0);
            canvas.Children.Add(ballon);

            ballon2.Width = 50;
            ballon2.Height = ballon2.Width;
            ballon2.Stroke = new SolidColorBrush(Colors.Blue);
            ballon2.Margin = new Thickness(250, bovenVerplaatsen, 0, 0);
            canvas.Children.Add(ballon2);
        }

        private void btnBewegen_Click(object sender, RoutedEventArgs e)
        {
            bovenVerplaatsen += 3;
            ballon.Margin = new Thickness(200, bovenVerplaatsen, 0, 0);
            ballon2.Margin = new Thickness(250, bovenVerplaatsen, 0, 0);
        }

        private void btnGroeien_Click(object sender, RoutedEventArgs e)
        {
            ballon.Width += 5;
            ballon2.Width += 5;

            ballon.Height = ballon.Width;
            ballon2.Height = ballon2.Width;
        }
    }
    ```
We kunnen beter een aparte klasse maken die de ballonnen doet bewegen en groeien. Het maakt i.d.g. niet uit of de **klasse** ```public``` of ```private``` maken; ```public``` zorgt ervoor dat die klassen ook buiten de namespace ```WpfBallon``` (hier niet zichtbaar, maar is deze namespace), terwijl dat bij private alleen maar binnen deze namespace kunnen gebruiken.
De klasse zetten we in een aparte file (Hoe?: RM op ```Project```-menu, ```Add```, ```Class```):
```C#
namespace WpfBallon
{
    public class Ballon
    {
            public Ellipse ballonnen;
            public int bovenVerplaatsen = 100;
            public int d = 20;
            public int x = 50;
            public int y = 50;

            public Ballon()
            {
                MaakBallon();
                VeranderBallon();
            }

            private void MaakBallon()
            {
                ballonnen = new Ellipse();
                ballonnen.Stroke = new SolidColorBrush(Colors.Red);
                ballonnen.StrokeThickness = 2;
            }

            private void VeranderBallon()
            {
                ballonnen.Width = d;
                ballonnen.Height = ballonnen.Width;
                ballonnen.Margin = new Thickness(x, y, 0, 0);
            }

            public void BeweegRechts(int xStap)
            {
                x += xStap;
                VeranderBallon();
            }

            public void VeranderStraal(int r)
            {
                d += r;
                VeranderBallon();
            }

            public void Tekenen(Canvas tekenCanvas)
            {
                tekenCanvas.Children.Add(ballonnen);
            }
        }
    }
```
Voeg ook hier de nodige namespaces toe! U kan deze klasse als volgt aanroepen:
```C#
    namespace WpfBallon
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        Ballon ballon = new Ballon();
        Ballon ballon2 = new Ballon();

        public MainWindow()
        {
            InitializeComponent();

            ballon.Tekenen(canvas);
            ballon2.Tekenen(canvas);
        }

        private void btnBewegen_Click(object sender, RoutedEventArgs e)
        {
            ballon.BeweegRechts(20);
            ballon2.BeweegRechts(50);
        }

        private void btnGroeien_Click(object sender, RoutedEventArgs e)
        {
            ballon.VeranderStraal(20);
            ballon2.VeranderStraal(5);
        }
    }
}
```
### 10.5 Dobbelstenen
in de klasse ```Dobbelstenen``` Let op: het maken van een contructor waarin u een methode aanroept:
```C#
public class Dobbelsteen
    {
        private static Random rnd = new Random();
        private int waarde;

        public Dobbelsteen()
        {
            Werp();
        }

        public void Werp()
        {
            waarde = rnd.Next(1, 7);
        }

        public int Waarde
        {
           get { return waarde; }
        }
    }
```
De constructor kan u herkennen aan (dezelfde naam als de klasse en) aan het feit dat het ``` public```, maar geen ```void``` of zo is ... Wel roept ie methods aan. ```rnd``` moet ```static``` zijn, omdat ie binnen deze klasse blijft + om te vermijden dat ie verschillende ```Random```-objecten aanmaakt! Gebruik NOOIT haakjes bij properties, noch bij het maken, noch bij de aanroep! Maak het object eerst aan en daarna kan u de property gebruiken:
```C#
Dobbelsteen dobbel = new Dobbelsteen();
lblDobbelsteen.Content = Convert.ToString(dobbel.Waarde);
```
PS: bij een ```Random```-klasse is de minValue altijd incl., maar de maxValue excl.!!!
PS: Geef uw klasse niet/nooit dezelfde naam als uw project!

### H13: Boodschappenlijst
Een 'grote' oef in het begin was er een oef van een boodschappenlijst. Mijn XAML ziet er als volgt uit:
```XAML
<Window x:Class="H13Boodschappen.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:H13Boodschappen"
        mc:Ignorable="d"
        Title="MainWindow" Height="350" Width="525">
    <Grid>
        <ListBox x:Name="boodschappenlijst" HorizontalAlignment="Left" Height="299" Margin="353,10,0,0" VerticalAlignment="Top" Width="154" SelectionChanged="boodschappenlijst_SelectionChanged">
            <ListBoxItem>brood</ListBoxItem>
            <ListBoxItem>melk</ListBoxItem>
            <ListBoxItem>koffie</ListBoxItem>
        </ListBox>
        <TextBox x:Name="txtToevoegen" HorizontalAlignment="Left" Height="25" Margin="10,91,0,0" TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="212"/>
        <Button x:Name="btnToevoegen" Content="toevoegen ~>" HorizontalAlignment="Left" Height="25" Margin="227,91,0,0" VerticalAlignment="Top" Width="121" Click="btnToevoegen_Click"/>
        <Label x:Name="lblAantalItems" Content="0" HorizontalAlignment="Left" Height="25" Margin="233,135,0,0" VerticalAlignment="Top" Width="116"/>
        <Label x:Name="label_Copy" Content="aantal items:" HorizontalAlignment="Left" Height="25" Margin="109,135,0,0" VerticalAlignment="Top" Width="116"/>
        <Label x:Name="lblIndex" Content="/" HorizontalAlignment="Left" Height="25" Margin="232,165,0,0" VerticalAlignment="Top" Width="116"/>
        <Label x:Name="label_Copy2" Content="geselecteerde index:" HorizontalAlignment="Left" Height="30" Margin="96,160,0,0" VerticalAlignment="Top" Width="126"/>
        <Label x:Name="lblItem" Content="/" HorizontalAlignment="Left" Height="25" Margin="232,195,0,0" VerticalAlignment="Top" Width="116"/>
        <Label x:Name="label_Copy4" Content="geselecteerde item:" HorizontalAlignment="Left" Height="34" Margin="111,195,0,0" VerticalAlignment="Top" Width="116"/>
        <Button x:Name="btnVerwijderen" Content="verwijderen" HorizontalAlignment="Left" Height="25" Margin="227,61,0,0" VerticalAlignment="Top" Width="121" Click="btnVerwijderen_Click"/>
        <TextBox x:Name="txtToevoegenIn" HorizontalAlignment="Left" Height="25" Margin="10,37,0,0" TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="212"/>
        <Button x:Name="btnToevoegenIn" Content="voeg toe in:" HorizontalAlignment="Left" Height="24" Margin="227,37,0,0" VerticalAlignment="Top" Width="71" Click="btnToevoegenIn_Click"/>
        <TextBox x:Name="txtInvoegindex" HorizontalAlignment="Left" Height="24" Margin="309,37,0,0" TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="39"/>
    </Grid>
</Window>
```
en mijn code:
```C#
public partial class MainWindow : Window
{
        private int aantalItems;

        private void TelItems()
        {
            aantalItems = boodschappenlijst.Items.Count;
        }

        public MainWindow()
        {
            InitializeComponent();
            txtToevoegen.Focus();

            TelItems();

            lblAantalItems.Content = aantalItems;
        }

        private void btnToevoegen_Click(object sender, RoutedEventArgs e)
        {
            if (txtToevoegen.Text != "")
            {
                ListBoxItem item = new ListBoxItem();
                item.Content = txtToevoegen.Text;
                boodschappenlijst.Items.Add(item);

                TelItems();
                lblAantalItems.Content = aantalItems;
            }
            else
            {
                txtToevoegen.Focus();
            }
        }

        private void boodschappenlijst_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            int index = boodschappenlijst.SelectedIndex;

            if (boodschappenlijst.SelectedValue != null)
            {
                lblIndex.Content = index;

                //ListBoxItem item = (ListBoxItem)boodschappenlijst.Items[index];
                //lblItem.Content = item.Content;
                ////op 1 regel:
                //lblItem.Content = ((ListBoxItem)boodschappenlijst.Items[index]).Content;
                ////is hetzelfde als:
                lblItem.Content = ((ListBoxItem)boodschappenlijst.SelectedValue).Content;
            }
            else
            {
                TelItems();
                lblAantalItems.Content = aantalItems;
                lblIndex.Content = "/";
                lblItem.Content = "/";
            }
        }

        private void btnVerwijderen_Click(object sender, RoutedEventArgs e)
        {
            boodschappenlijst.Items.RemoveAt(boodschappenlijst.SelectedIndex);
        }

        private void btnToevoegenIn_Click(object sender, RoutedEventArgs e)
        {
            if(txtInvoegindex.Text != "" && Convert.ToInt32(txtInvoegindex.Text) >= 0 && Convert.ToInt32(txtInvoegindex.Text) < aantalItems)
            {
                boodschappenlijst.Items.Insert(Convert.ToInt32(txtInvoegindex.Text), txtToevoegenIn.Text);
            }
        }
}
```

### Nullpadd--
#### gewoon Appje
```XAML
<Window x:Class="Nullpad__.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Nullpad__"
        mc:Ignorable="d"
        Title="Nullpad--" Height="350" Width="525">
    <DockPanel>
        <Menu x:Name="menu" DockPanel.Dock="Top">
            <MenuItem Header="_Bestand">
                <MenuItem x:Name="itemOpenen" Header="_Open" Click="itemOpenen_Click"/>
                <MenuItem x:Name="itemOpslaan" Header="_Opslaan" Click="itemOpslaan_Click"/>
                <Separator/>
		<MenuItem x:Name="itemOpslaanAls" Header="_Opslaan als" Click="itemOpslaanAls_Click"/>
                <MenuItem x:Name="itemSluiten" Header="_Sluiten" Click="itemSluiten_Click"/>
            </MenuItem>
            <MenuItem Header="_Help">
                <MenuItem Header="_Over"/>
            </MenuItem>
        </Menu>
        <Grid DockPanel.Dock="Bottom">
            <TextBox x:Name="txtHoofdtekst" Margin="50,21,49,31"/>
            <!--inhoud-->
        </Grid>
    </DockPanel>
</Window>
```
code tot de 1e 2 event-handlers:
```C#
namespace Nullpad__
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        private string huidigeFile = "";
        private string basisDir;

        public MainWindow()
        {
            InitializeComponent();

            basisDir = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
        }

        private void itemOpenen_Click(object sender, RoutedEventArgs e)
        {
            //OpenFileDialog verkennerOpenen = new OpenFileDialog();
            //verkennerOpenen.InitialDirectory = basisDir;

            //if (verkennerOpenen.ShowDialog().Value /*hetzelfde als verkennerOpenen.ShowDialog() == true, aangezien het van type bool? is*/)
            //{
            //    MessageBox.Show(verkennerOpenen.FileName);
            //}

            ////StreamReader inputStream;
            OpenFileDialog verkenner = new OpenFileDialog();

            verkenner.InitialDirectory = basisDir;

            if (verkenner.ShowDialog().Value)
            {
                huidigeFile = verkenner.FileName;
                ////inputStream = File.OpenText(huidigeFile);
                ////txtHoofdtekst.Text = inputStream.ReadToEnd();
                ////inputStream.Close();
                txtHoofdtekst.Text = File.ReadAllText(huidigeFile);
            }
        }

        private void itemOpslaan_Click(object sender, RoutedEventArgs e)
        {
            if (huidigeFile == "")
            {
                SaveFileDialog opTeSlaan = new SaveFileDialog();

                opTeSlaan.InitialDirectory = basisDir;

                if (opTeSlaan.ShowDialog().Value)
                {
                    huidigeFile = opTeSlaan.FileName;
                }
            }

            //StreamWriter outputStream = File.CreateText(huidigeFile);
            //outputStream.Write(txtHoofdtekst.Text);
            //outputStream.Close();
            File.WriteAllText(huidigeFile, txtHoofdtekst.Text);
        }
	
	private void itemOpslaanAls_Click(object sender, RoutedEventArgs e)
        {
	    //Dit moet sowieso geopend worden; huidigeFile bestaat nu sowieso nog niet, dus geen selectie (i.t.t. vorige methode):
            SaveFileDialog opslaanDir = new SaveFileDialog();

            opslaanDir.InitialDirectory = basisDir;

            if (opslaanDir.ShowDialog().Value)
            {
                huidigeFile = opslaanDir.FileName;

                File.WriteAllText(huidigeFile, txtInhoud.Text);
            }
        }

        private void sluitItem_Click(object sender, RoutedEventArgs e)
        {
            Environment.Exit(0); //0 is de exitcode om gewoonweg te sluiten (risico: niet opgeslagen)
        }
    }
}
```

#### tweede kolom
```XAML
<Window x:Class="Nullpad__.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Nullpad__"
        mc:Ignorable="d"
        Title="Nullpad--" Height="350" Width="525">
    <DockPanel>
        <Menu x:Name="menu" DockPanel.Dock="Top">
            ...
        </Menu>
        <StatusBar DockPanel.Dock="Bottom"> <!--boven Grid, anders wordt Grid eerder onderaan geplaatst-->
            <TextBlock>Status</TextBlock>
        </StatusBar>
        <Grid DockPanel.Dock="Bottom">
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition Width="7*"/>
                <ColumnDefinition Width="Auto"/>
                <ColumnDefinition Width="8*"/>
            </Grid.ColumnDefinitions>
            <TextBox x:Name="txtFileContents" Grid.Column="0" Grid.ColumnSpan="2" AcceptsReturn="True"/>
            <GridSplitter Grid.Column="2" Width="5" HorizontalAlignment="Right" VerticalAlignment="Stretch" ResizeBehavior="PreviousAndNext" Background="LightGray"/>
            <DataGrid x:Name="parsedDataGrid" Grid.Column="3"/>
        </Grid>
    </DockPanel>
</Window>
```
```C#
 public partial class MainWindow : Window
{
        private string huidigeFile = "";
        private string basisDir;
        private DateTime geboorteDatum = new DateTime(1990, 1, 2);

        public MainWindow()
        {
            InitializeComponent();

            basisDir = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

            List<Personen> personen = new List<Personen>();

            personen.Add(new Personen { Voornaam = "Willy", Achternaam = "Janssens", Geboortedatum = new DateTime(1990, 1, 2) });
            personen.Add(new Personen { Voornaam = "Ed", Achternaam = "Sheeran", Geboortedatum = new DateTime(2000, 12, 26) });
            personen.Add(new Personen { Voornaam = "Hans", Achternaam = "Van Broeckhoven", Geboortedatum = new DateTime(1981, 10, 12) });

            parsedDataGrid.ItemsSource = personen;
}
...
public class Personen
{
        public string Voornaam { get; set; }
        public string Achternaam { get; set; }
        public DateTime Geboortedatum { get; set; }

        //zonder DataGrid, maar met ListView:
        //public override string ToString()
        //{
        //    return Voornaam + " " + Achternaam + " (" + Geboortedatum.ToShortDateString() + ")";
        //}
}
```
Exceptions moeten nog verbeterd en aangevuld worden:
```C#
private void Parse_Click(object sender, RoutedEventArgs e)
{
            List<Persoon> parsedPersonen = new List<Persoon>();

            string[] filedata = fileContents.Text.Split('\n');
            try {
                foreach (var row in filedata)
                {
                    // MessageBox.Show(String.Format("[{0}]", row.Trim()));

                    // is row valid?
                    string[] fields = row.Trim().Split(';');

                    if (fields.Length != 3)
                    {
                        MessageBox.Show(
                            String.Format("Couldn't parse [{0}]. Number of fields: {1}.", 
                                row.Trim(),
                                fields.Length)
                        );
                    }
                    else if(row.Trim() == "")
                    {
                        // ignore empty rows
                    }
                    else
                    {
                        var p = new Persoon();
                        p.Voornaam = fields[0];
                        p.Achternaam = fields[1];
                        p.GeboorteDatum = DateTime.Parse(fields[2]);
                        parsedPersonen.Add(p);
                    }
                }
            } catch(Exception exc)
            {
                MessageBox.Show(exc.ToString());
            }

            parsedDataGrid.ItemsSource = parsedPersonen;
}
```
PS: louter de belangrijke dingen (voor dit) zijn aangevuld ...

### ConsoleGTA
ik heb het niet echt verder uitgebreid/kunnen uitbreiden ...
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleGTA
{

public class Console2
    {
        public static void Write(string str, ConsoleColor kleur)
        {
            Console.ForegroundColor = kleur;
            Console.Write(str);
            Console.ResetColor();
        }

        public static void WriteLine(string str, ConsoleColor kleur)
        {
            Console2.Write(str, kleur);
            Console.WriteLine();
        }

        enum LexerState
        {
            BEFORE,
            ACCENTED,
            AFTER,
            FIRST_OPENING_BRACE,
            SECOND_OPENING_BRACE,
            FIRST_CLOSING_BRACE,
            SECOND_CLOSING_BRACE
        }

        //Parset een Mustacheachtige (= met "{}") template-string (met max. 1 parameter) en print deze op de console met de parameter 		//in "de" geaccentueerdeKleur.
        public static void Write(string str, ConsoleColor basiskleur, ConsoleColor geaccentueerdeKleur)
        {
            string voor = "";
            string geaccentueerd = "";
            string na = "";
            LexerState ps = LexerState.BEFORE;

            foreach (char c in str)
            {
                switch (ps)
                {
                    case LexerState.BEFORE:
                        if (c != '{')
                        {
                            voor += c;
                        }
                        else
                        {
                            ps = LexerState.FIRST_OPENING_BRACE;
                        }
                        break;
                    case LexerState.FIRST_OPENING_BRACE:
                        if (c == '{')
                        {
                            ps = LexerState.SECOND_OPENING_BRACE;
                        }
                        else
                        {
                            ps = LexerState.BEFORE;
                            voor += '{';
                            voor += c;
                        }
                        break;
                    case LexerState.SECOND_OPENING_BRACE:
                        if (c == '}')
                        {
                            ps = LexerState.FIRST_CLOSING_BRACE;
                        }
                        else
                        {
                            ps = LexerState.ACCENTED;
                            geaccentueerd += c;
                        }
                        break;
                    case LexerState.ACCENTED:
                        if (c == '}')
                        {
                            ps = LexerState.FIRST_CLOSING_BRACE;
                        }
                        else
                        {
                            geaccentueerd += c;
                        }
                        break;
                    case LexerState.FIRST_CLOSING_BRACE:
                        if (c == '}')
                        {
                            ps = LexerState.SECOND_CLOSING_BRACE;
                        }
                        else
                        {
                            geaccentueerd += '}';
                            geaccentueerd += c;
                        }
                        break;
                    case LexerState.SECOND_CLOSING_BRACE:
                        ps = LexerState.AFTER;
                        na += c;
                        break;
                    case LexerState.AFTER:
                        na += c;
                        break;
                }
            }

            Console2.Write(voor, basiskleur);
            Console2.Write(geaccentueerd, geaccentueerdeKleur);
            Console2.Write(na, basiskleur);
        }

        public static void WriteLine(string str, ConsoleColor basiskleur, ConsoleColor geaccentueerdeKleur)
        {
            Console2.Write(str, basiskleur, geaccentueerdeKleur);
	    Console2.WriteLine(str, basiskleur, geaccentueerdeKleur);
        }
    }
    
    class Voertuig
    {
        private ConsoleColor kleur;

        public Voertuig(ConsoleColor kleur)
        {
            this.kleur = kleur;
        }

        public virtual void Rij()
        {
            Console2.WriteLine("Het {{voertuig}} rijdt...", ConsoleColor.White, kleur);
        }

        public virtual void Stuur(int graden)
        {
            Console.WriteLine("Ik stuur " + graden + "graden");
        }
    }
    
    class Auto : Voertuig
    {
        public Auto() : base(ConsoleColor.DarkYellow)
        {
        }

        public override void Rij()
        {
            Console2.WriteLine("De auto rijdt...", ConsoleColor.Red);
        }
    }
    
    class Vrachtwagen : Voertuig
    {
        public Vrachtwagen() : base(ConsoleColor.Green)
        {
        }

        public override void Rij()
        {
            Console2.WriteLine("De vrachtwagen rijdt...", ConsoleColor.Red);
        }

        public override void Stuur(int graden)
        {
            Console.WriteLine("De vrachtwagenchauffeur kijkt in zijn dodehoekspiegel");
            base.Stuur(graden);
        }

        public void LaadLeeg()
        {
        }
    }
    
    class Brommer : Voertuig
    {
        public Brommer() : base(ConsoleColor.DarkRed)
        {
        }

        public override void Rij()
        {
            Console2.WriteLine("De brommer rijdt...", ConsoleColor.Cyan);
        }

        public override void Stuur(int graden)
        {
            base.Stuur(graden);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Voertuig v = new Voertuig(ConsoleColor.Magenta);
            Voertuig camion = new Vrachtwagen();
            Voertuig brommerke = new Brommer();

            v.Rij();
            camion.Rij();
            Console.WriteLine();

            brommerke.Rij();
            brommerke.Stuur(45);

            Console2.Write("lol", ConsoleColor.Green, ConsoleColor.DarkRed);
        }
    }
}
```
- ``abstract`` wil zeggen dat de klasse overgeërfd **moet** worden. U maakt een abstracte klasse, als u min. 1 abstracte methode o.d. gebruikt.
- ``virtual`` wil zeggen dat u het mogelijk zal aanpassen (liefst in min. 1) subklasse.
- u maakt het aan met deze woorden, maar roept beiden aan met ``override``
- polymorfie: ...

## C# Interactive
Dit valt een beetje te vergelijken met de JavaScript-console.
Met bv. de volgende code:
```C#
string fileNamenText = File.ReadAllText("\\\\imma-fs-0003\\timour.meeusen$\\documents\\namen.csv");
```
kan u makkelijk de tekst in een bestaande file lezen. De volgende code kan u helpen het pad de vinden:
```C#
Directory.GetFiles(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments))
```
### ?
``bool?`` is hetzelfde als ```Nullable<bool>```. dit wil betekent dat de ```bool``` ook de waarde ```null``` kan hebben. Hieruit volgt automatisch dat er bv. in een selectie (of in het midden van de ```for```-regel ofzo) de bool als iets dergelijk zou moeten invullen:
```C#
OpenFileDialog verkenneropenen = new OpenFileDialog();
if (verkennerOpenen.ShowDialog() == true) /*== true verplicht*/
{ ... }
//OF als:
if (verkennerOpenen.ShowDialog().Value) /*hierbij moet de bool? een waarde hebben, dus is ie sowieso true of false*/
{ ... }
```
### value vs referentietypes
zie H 5....-5....
- value type: int; bv. ...
- referentietypes: ...; bv. klasse, ...
heap vs stack (geheugen)

## Javascript
valt nog te verbeteren:
```HTML
<!DOCTYPE html>
<html>
	<title>JavaScript06</title>
	<style>
		#klik
		{
			border: 1px solid red;
			width: 20em;
		}
		
		#vierkant
		{
			width: 100px;
			height: width;
		}
	</style>
	<body>
		<button id="klik">Klik!</button>
		<div id="vierkant" style="color:#FF0000">"Hi!"</div>
		<button id="timer">Time!</button>
		<button id="stopTimer" onclick="setInterval(SecondenTimen, 1000)">Stop timen!</button>
		<p id="timeparagraaf" visibility="hidden"/>
		<script>
			var knop = document.getElementById("klik");
			var figuur = document.getElementById("vierkant");
			var btnTimer = document.getElementById("timer");
			var btnStopTimer = document.getElementById("stopTimer");
			var tijdsinterval;
			
			function VeranderAchtergrond()
			{
				console.log("U kan klikken, hoera!!!");
				knop.style.backgroundColor="green";
			}
			
			function HoverFiguur()
			{
				console.log("Ga weg!!!");
				figuur.style.backgroundColor="green";
			}
			
			function Kleur()
			{
				btnStopTimer.style.backgroundColor = "red";
			}
			
			function SecondenTimen()
			{
				var i = 0;
				
				timeparagraaf.style.visibility = "visible";
				timeparagraaf.innerHTML = i;
				i++;
			}
			
			knop.addEventListener("click", VeranderAchtergrond);
			figuur.addEventListener("mouseover", HoverFiguur);
			figuur.addEventListener("mouseout", function (){
				console.log("Dank u!");
				figuur.style.backgroundColor="red";
			});
			btnTimer.addEventListener("click", setTimeout(SecondenTimen, 1000));
			btnStopTimer.addEventListener("click", Kleur);
		</script>
	</body>
</html>
```
