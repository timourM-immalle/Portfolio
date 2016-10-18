# Portfolio
# Csharp
oef 5.8:
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
  
  oef 5.10:
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

oef 5.11:
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
# Javascript
