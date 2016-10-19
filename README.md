# Portfolio
# Csharp
## oef 5.8:
https://dotnetfiddle.net/RKK9fm

oef 5.9 (Voluma van kubus berekenen):
https://dotnetfiddle.net/zuhvul
```
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
  ```
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
```
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
* Als u een gewone methode aanroept, **doet** het programma er iets mee zoals het tekenen van een ellipse:
```
private void Ellipse(int straal)
{
Ellipse ell = new Ellipse;
ell.Width = straal;
ell.Height = straal;
ell.Margin = new Thickness(10, 10, 0, 0);
ell.Fill = new SolidColorBrush(Colors.Black);
canvas.children.Add(ell);
```
dit moet altijd "void" zijn.

* Als u een methode met een `return`-statement aanroept, kan u er effectief mee verder **werken/rekenen**, bv. als in oef **5.11**. U kan met `TijdInSec()` effectief mee verder werken het als een variable declareren en zelfs op berekenen als u dat wil. Dit heeft altijd een type, bv. een int. als de uiteindelijke waarde(n) een geheel getal (integer) moet zijn.

# Javascript
