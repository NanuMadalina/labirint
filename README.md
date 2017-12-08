# labirint
Arduino game

----------------------------Labirint--------------------------------------

-pionul sau jucatorul ->setat in punctul cu coordonatele (6,6);
-jocul incepe la apasarea butonului;
-numar vieti = 3 -> intotdeauna;
-greseli <=> numberLives -1;
-la 3 greseli repetate => numberLives=0 => "Gamve Over";
-in momentul in care pionul atinge yPos=0, xPos=6=> "You Won";


----Librarii folosite:
LiquidCrystal
LedControl

----Functii create:
setup()
readJoystick()
firstStep()
secondStep()
loop()

Le-am folosit dupa cum urmeaza:
-readJoystick() -> functie care determina daca butonul a fost apasat sau nu
-firstStep() -> functie folosita in prima faza, adica atunci cand butonul nu a fost apasat
-secondStep()  -> functie principala ce contine tot behavior jocului
-loop()  ->functie bucla careia i-am transmis un parametru global isTrue
	 ->isTrue este initial false
	 ->isTrue isi schimba valoarea in readJoystick() cand e apasat butonul =>trece in true
	 ->cand e True intra pe ramura 2 =>secondStep()
	 ->cand isTrue=false 
			apelam functia firstStep (suntem in primul caz)
			apelam readJoystick() pt starea butonului
		else
			apelam functia secondStep (suntem in cazul 2)

----Variabile globale:
matrice[8][8] prin care trasam drumul;
xPos,yPos ->pozitiile initiale pion;
bool isTrue ->folosit in loop();
numberLives=3 ->nr vieti;


----Behavior
-in matrice[8][8] aprind doar ledurile necesare pt a delimita labirintul
-prin urmare, populez matrice cu valoarea 1 pt ledurile aprinse
-daca pionul se loveste de led aprins=> numberLives -1
-fiind un om matur, cel care se loveste, trebuie si sa iasa din gardul viu,
-daca ramane prea mult in gardul viu => "Game over" :(
	*( Coliziunea putea fi imbunatatita si o sa continui sa lucrez la asta )*
- de asemenea, am marcat in matrice iesirea cu o valoare diferita de 1, in exemplul meu  = 2
-pt a castiga se verifica daca pionul intalneste valoarea 2 
-pentru deplasarea pionului am mapat 0->1023 in 1->300
-si am verificat pe cazuri in ce directie se deplaseaza
-cand se pierd cele 3 vieti este afisat pe LCD mesajul "Game Over"
-daca pionul este norocos, si reuseste sa iasa pe LCD afisez "You Won"
-jocul cicleaza la infinit, deci dupa ce castigi poti continua sa te joci, din punctul in care ai ramas
-evident vietile se reseteaza fiind global initializate deci, in afara loop-ului ()
( 
Am ales sa las pionul in acelasi punct in cazul in care la iesire,
jucatorul realizeaza ca s-a bazat doar pe noroc si vrea sa se asigure ca a fost si stiinta,
decide la iesire, sa se intoarca si sa fie mai dur cu el de data aceasta,
reincercand sa rezolve labirintul :D
)





