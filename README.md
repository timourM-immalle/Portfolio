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

### De basis van mijn eerste RM in WPF
Ik heb tot nu toe een rekenmachine gemaakt die de som van 2 getallen kan berekenen. Dit is nog maar een begin; uitbreiding is noodzakelijk en is voor de toekomst (wellicht). Ik heb het volgende aangemaakt:
XAML:
```XAML
<Window x:Class="RM.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:RM"
        mc:Ignorable="d"
        Title="Calculator" Height="400" Width="236.834">
    <Grid>
        <TextBlock x:Name="schermBlock" HorizontalAlignment="Right" Height="33" Margin="0,10,10,0" TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="203"/>
        <Button x:Name="btn1" Content="1" HorizontalAlignment="Left" Height="35" Margin="16,48,0,0" VerticalAlignment="Top" Width="47" Click="btn1_Click"/>
        <Button x:Name="btn2" Content="2" HorizontalAlignment="Left" Height="35" Margin="68,48,0,0" VerticalAlignment="Top" Width="47" Click="btn2_Click"/>
        <Button x:Name="Btn3" Content="3" HorizontalAlignment="Left" Height="35" Margin="120,48,0,0" VerticalAlignment="Top" Width="47" Click="Btn3_Click"/>
        <Button x:Name="optelButton" Content="+" HorizontalAlignment="Left" Height="35" Margin="172,48,0,0" VerticalAlignment="Top" Width="47" Click="optelButton_Click"/>
        <Button x:Name="btn4" Content="4" HorizontalAlignment="Left" Height="35" Margin="16,88,0,0" VerticalAlignment="Top" Width="47" Click="btn4_Click"/>
        <Button x:Name="btn5" Content="5" HorizontalAlignment="Left" Height="35" Margin="68,88,0,0" VerticalAlignment="Top" Width="47" Click="btn5_Click"/>
        <Button x:Name="btn6" Content="6" HorizontalAlignment="Left" Height="35" Margin="120,88,0,0" VerticalAlignment="Top" Width="47" Click="btn6_Click"/>
        <Button x:Name="aftrekButton" Content="-" HorizontalAlignment="Left" Height="35" Margin="172,88,0,0" VerticalAlignment="Top" Width="47" Click="aftrekButton_Click"/>
        <Button x:Name="btn7" Content="7" HorizontalAlignment="Left" Height="35" Margin="16,128,0,0" VerticalAlignment="Top" Width="47" Click="btn7_Click"/>
        <Button x:Name="btn8" Content="8" HorizontalAlignment="Left" Height="35" Margin="68,128,0,0" VerticalAlignment="Top" Width="47" Click="btn8_Click"/>
        <Button x:Name="btn9" Content="9" HorizontalAlignment="Left" Height="35" Margin="120,128,0,0" VerticalAlignment="Top" Width="47" Click="btn9_Click"/>
        <Button x:Name="uitkomstButton" Content="=" HorizontalAlignment="Left" Height="35" Margin="172,128,0,0" VerticalAlignment="Top" Width="47" Click="uitkomstButton_Click"/>
        <Button x:Name="btn0" Content="0" HorizontalAlignment="Left" Height="35" Margin="16,168,0,0" VerticalAlignment="Top" Width="47" Click="btn0_Click"/>
        <Button x:Name="clearButton" Content="CLEAR" HorizontalAlignment="Left" Height="35" Margin="120,168,0,0" VerticalAlignment="Top" Width="99" Click="clearButton_Click"/>
        <TextBlock x:Name="cacheBlock" HorizontalAlignment="Left" Height="24" Margin="44,264,0,0" TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="142"/>
    </Grid>
</Window>
```
code:
```C#
public partial class MainWindow : Window
    {
        private string huidigGetal = "";
        private int som = 0;
        private int cacheGetal = 0;
        private int verschil = 0;

        public MainWindow()
        {
            InitializeComponent();
        }

	private void OpOperatorknopGeklikt()
        {
            cacheBlock.Text = schermBlock.Text;
            cacheGetal = Convert.ToInt32(cacheBlock.Text);
            schermBlock.Text = null;
            huidigGetal = "";
        }
	
        private void btn1_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(1);
            huidigGetal += "1";
        }

        private void btn2_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(2);
            huidigGetal += "2";
        }

        private void Btn3_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(3);
            huidigGetal += "3";
        }

        private void btn4_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(4);
            huidigGetal += "4";
        }

        private void btn5_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(5);
            huidigGetal += "5";
        }

        private void btn6_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(6);
            huidigGetal += "6";
        }

        private void btn7_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(7);
            huidigGetal += "7";
        }

        private void btn8_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(8);
            huidigGetal += "8";
        }

        private void btn9_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(9);
            huidigGetal += "9";
        }

        private void btn0_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text += Convert.ToString(0);
            huidigGetal += "0";
        }

        private void clearButton_Click(object sender, RoutedEventArgs e)
        {
            schermBlock.Text = null;
            huidigGetal = "";
            cacheBlock.Text = null;
            som = 0;
            verschil = 0;
            cacheGetal = 0;
        }

        private void optelButton_Click(object sender, RoutedEventArgs e)
        {
            OpOperatorknopGeklikt();
        }
	
	private void aftrekButton_Click(object sender, RoutedEventArgs e)
        {
            OpOperatorknopGeklikt();
        }

        private void uitkomstButton_Click(object sender, RoutedEventArgs e)
        {
            som = Convert.ToInt32(huidigGetal) + cacheGetal;
	    verschil = cacheGetal - Convert.ToInt32(huidigGetal);
            schermBlock.Text = null;
            cacheBlock.Text = null;
            schermBlock.Text = Convert.ToString(som);
        }
    }
}
```
##H10: in dit programma kunnen we erg veel ballonnen toevoegen, maar op den duur wordt het erg onhandig:
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
    class Ballon
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

## Javascript
