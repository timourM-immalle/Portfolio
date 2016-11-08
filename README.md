# Portfolio
# Csharp
## oef 5.8:
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
  
##  oef 5.10:
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

## oef 5.11:
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

## 5.12 (een uitbreiding van 5.10):
https://dotnetfiddle.net/DDHHKX

## Gewone methode vs die met return-waarde
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

## vb.-oef van H 6.8 De klasse DispatcherTimer: Raindrops
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

##Extra: ```Timer``` in Console-app
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
Deze code print om de rnd aantal seconden het woorde **"hallo"** af. ``rnd`` is een ```Random``` van max. 1,5 s (1500 ms). In een console-app is het i.p.v. ```timer.Tick```, ``` timer.Elapsed```. ```Console.Readline()``` wacht totdat u iets invoert vooraleer het het programma gaat sluiten. Hij leest als het ware de input. Als u op ``Enter`` drukt, zal het stoppen en als u een letter intypt komt dat erbij op te staan :satisfied:.

# Javascript
