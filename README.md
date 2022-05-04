import random
import msvcrt
import os
#VARIABLES GLOBALES
mazo=[]
#MAZOS PARA LOS JUGADORES
mazo1=[]
mazo2=[]
mazo3=[]
mazo4=[]
#MAZOS PARA LAS CONDICIONES
#MAZO PARA INICIO
mazo5=[]
#MAZO PARA LAS CONDICIONES
mazo6=[]
mazo7=[]
mazo8=[]
#OTRA LISTA
mazo11=[]
q="2"
r=[]

col=('ROJO','AMARILLO','AZUL','VERDE')
num3=('0','1','2','3','4','5','6','7','8','9','REVERSO','BLOQUEO','+2')
num2=('0','1','2','3','4','5','6','7','8','9')
esp=('+4 CAMBIO DE COLOR','CAMBIO DE COLOR')

#MOSTRAR MAZO DE CADA JUGADOR
def mano(lista3):
	print(" ")
	for u in lista3:
		print("\t",u)
	print(" ")

#GENERANDO MAZO REVUELTO:
def gen():
	#CARACTERISTICAS
	num=('0','1','2','3','4','5','6','7','8','9','1','2','3','4','5','6','7','8','9','REVERSO','REVERSO','BLOQUEO','BLOQUEO','+2','+2')
	for c in col:
		for k in num:
			cartas="{1} {0}".format(c,k)
			mazo.append(cartas)
	for e in range(4):
		mazo.append(esp[0])
		mazo.append(esp[1])
	for q in range(3):
		random.shuffle(mazo)
	return mazo

#GENERANDO MAZO REVUELTO2:
def gen2():
	for c1 in col:
		for k1 in num2:
			cartas2="{1} {0}".format(c1,k1)
			mazo5.append(cartas2)
	for w in range(3):
		random.shuffle(mazo5)
	return mazo5

#APOYO PARA LOS CONDICIONALES
def gen3():
	for c2 in col:
		cartas3="REVERSO {}".format(c2)
		mazo6.append(cartas3)
	return mazo6
def gen4():
	for c3 in col:
		cartas4="BLOQUEO {}".format(c3)
		mazo7.append(cartas4)
	return mazo7
def gen5():
	for c4 in col:
		cartas5="+2 {}".format(c4)
		mazo8.append(cartas5)
	return mazo8

#FUNCION PARA SUMAR CARTAS A LOS MAZOS
def gen6(lista2):
	gen()
	for f in range(2):
		lista2.append(random.choice(mazo))

#CONDICIONAL PARA CARTAS ESPECIALES	
def condi(lista,x):
	#REVERSO
	if lista[x-1] in mazo6:
		if lista==mazo1:
			oper(lista,x)
		elif lista==mazo2:
			print("\nCARTA EN MESA: ",lista[x-1])
			lista.pop(x-1)
		elif lista==mazo3:
			print("\nCARTA EN MESA: ",lista[x-1])
			lista.pop(x-1)
		elif lista==mazo4:
			print("\nCARTA EN MESA: ",lista[x-1])
			lista.pop(x-1)
		else:
			print("ERROR")
	#+2
	elif lista[x-1] in mazo8:
		if lista==mazo1:
			os.system("cls")
			print("\nCARTA EN MESA: ",lista[x-1])
			print("\nEL JUGADOR 2 HA COMIDO 2")
			lista.pop(x-1)
			gen6(mazo2)
			block()
		elif lista==mazo2:
			os.system("cls")
			print("\nCARTA EN MESA: ",lista[x-1])
			print("\nEL JUGADOR 3 HA COMIDO 2")
			lista.pop(x-1)
			gen6(mazo3)
			block1()
		elif lista==mazo3:
			os.system("cls")
			print("\nCARTA EN MESA: ",lista[x-1])
			print("\nEL JUGADOR 4 HA COMIDO 2")
			lista.pop(x-1)
			gen6(mazo4)
			block2()
		elif lista==mazo4:
			os.system("cls")
			print("\nCARTA EN MESA: ",lista[x-1])
			print("\nEL JUGADOR 1 HA COMIDO 2")
			lista.pop(x-1)
			gen6(mazo1)
			block3()
		else:
			print("ERROR")
	#BLOQUEOS
	elif lista[x-1] in mazo7:
		if lista==mazo1:
			os.system("cls")
			print("\n 	CARTA EN MESA: ",lista[x-1])
			print("\n 	EL JUGADOR 2 HA SIDO BLOQUEADO")
			lista.pop(x-1)	
			block()
		elif lista==mazo2:
			os.system("cls")
			print("\nCARTA EN MESA: ",lista[x-1])
			print("\nEL JUGADOR 3 HA SIDO BLOQUEADO")
			lista.pop(x-1)
			block1()
		elif lista==mazo3:
			print("\nCARTA EN MESA: ",lista[x-1])
			print("\nEL JUGADOR 4 HA SIDO BLOQUEADO")
			lista.pop(x-1)
			block2()
		elif lista==mazo8:
			os.system("cls")
			print("\nCARTA EN MESA: ",lista[x-1])
			print("\nEL JUGADOR 1 HA SIDO BLOQUEADO")
			lista.pop(x-1)
			block3()	
		else:
			print("ERROR")
	elif lista[x-1]=="CAMBIO DE COLOR":
		f=int(input("""\n		Ingresa el numero con el color que deseas poner: 
		1.- ROJO
		2.- AZUL
		3.- VERDE
		4.- AMARILLO 
		= """))
		os.system("cls")
		if f==1:
			print("\n COLOR EN LA MESA: ROJO")
			r.clear()
			r.append("R")
			r.append("ROJO")
		elif f==2:
			print("\n COLOR EN LA MESA: AZUL")
			r.clear()
			r.append("A")
			r.append("AZUL")
		elif f==3:
			print("\n COLOR EN LA MESA: VERDE")
			r.clear()
			r.append("V")
			r.append("VERDE")
		elif f==4:
			print("\n COLOR EN LA MESA: AMARILLO")
			r.clear()
			r.append("A")
			r.append("AMARILLO")
		else:
			print("ERROR")
	else:
		os.system("cls")
		print("\n CARTA EN MESA: ",lista[x-1])
		lista.pop(x-1)

#CONDICIONAL PARA TIRAR CARTAR 
def eva(lista4):
	h=4
	while h!=1 and h!=2:
		h=int(input("	¿Tienes cartas para tirar? 1.-Si  2.-No   "))
		if h==1:
			eva2(lista4,q)
		else:
			p=int(input("	¿Cuantas cartas deseas tomar?: "))
			gen()
			for f in range(p):
				lista4.append(random.choice(mazo))
			os.system("cls")
			print("\n CARTA EN MESA: ",q)
			mano(lista4)
			h=4

def eva2(lista5,q):
	s=q.split(" ")
	n="jiji"
	while n[0]!=s[0] and n[1]!=s[1]:
		w=int(input(" 	Ingresa la posicion de la carta que deseas tirar: "))  
		n=lista5[w-1].split(" ")
	condi(lista5,w)

##ARREGLAR ESTA PARTE PARA QUE SOLO SEA UN BUCLE
#BUCLE INICIAL
def bucle():
	x=1
	while(x==1):
		print("""
	JUGADOR 1: """)
		mano(mazo1)
		eva(mazo1)
		print("""
	JUGADOR 2: """)
		mano(mazo2)
		eva(mazo2)
		print("""
	JUGADOR 3: """)
		mano(mazo3)
		eva(mazo3)
		print("""
	JUGADOR 4: """)
		mano(mazo4)
		eva(mazo4)

#BLOQUEOS
#BLOQUEO DESDE JUGADOR1
def block():
	p=1
	while(p==1):
		print("""
	JUGADOR 3:""")
		mano(mazo3)
		eva(mazo3)
		print("""
	JUGADOR 4: """)
		mano(mazo4)
		eva(mazo4)
		print("""
	JUGADOR 1: """)
		mano(mazo1)
		eva(mazo1)
		print("""
	JUGADOR 2: """)
		mano(mazo2)
		eva(mazo2)
#BLOQUEO DESDE JUGADOR2
def block1():
	p=1
	while(p==1):
		print("""
	JUGADOR 4: """)
		mano(mazo4)
		eva(mazo4)
		print("""
	JUGADOR 1: """)
		mano(mazo1)
		eva(mazo1)
		print("""
	JUGADOR 2: """)
		mano(mazo2)
		eva(mazo2)
		print("""
	JUGADOR 3:""")
		mano(mazo3)
		eva(mazo3)
#BLOQUEO DESDE JUGADOR3
def block2():
	x=1
	while(x==1):
		print("""
	JUGADOR 1:""")
		mano(mazo1)
		eva(mazo1)
		print("""
	JUGADOR 2: """)
		mano(mazo2)
		eva(mazo2)
		print("""
	JUGADOR 3: """)
		mano(mazo3)
		eva(mazo3)
		print("""
	JUGADOR 4: """)
		mano(mazo4)
		eva(mazo4)
#BLOQUEO DESDE JUGADOR4
def block3():
	p=1
	while(p==1):
		print("""
	JUGADOR2: """)
		mano(mazo2)
		eva(mazo2)
		print("""
	JUGADOR3:""")
		mano(mazo3)
		eva(mazo3)
		print("""
	JUGADOR4: """)
		mano(mazo4)
		eva(mazo4)
		print("""
	JUGADOR: """)
		mano(mazo1)
		eva(mazo1)


#CODIGO PRINCIPAL
print("	\n   JUEGO DEL UNO")
print("""
	CANTIDAD DE JUGADORES: 4

	PRESIONA ENTER PARA INCIAR EL JUEGO...""")
msvcrt.getch()

#INICIANDO JUEGO
gen()
gen2()
gen3()
gen4()
gen5()

q=random.choice(mazo5)
print("""
CARTA EN MESA: """,q)

#REPARTIENDO CARTAS
mazo1=(random.sample(mazo,7))
mazo2=(random.sample(mazo,7))
mazo3=(random.sample(mazo,7))
mazo4=(random.sample(mazo,7))

#CODIGO PRINCIPAL
bucle()
