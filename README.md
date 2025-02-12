y[n] resultante de la convoluvion entre x[n] y h[n] usando sumatorias a mano
![Imagen de WhatsApp 2025-02-11 a las 22 43 20_a146d2b3](https://github.com/user-attachments/assets/45682e9a-7949-4195-a362-0a02ce55f24a)
y[n] resultante de la convoluvion entre x[n] y h[n] usando sumatorias a mano del segundo integrante 
![Imagen de WhatsApp 2025-02-12 a las 00 07 32_b0f92cb3](https://github.com/user-attachments/assets/a0962be5-a124-4098-bd4e-b61c582e4691)
x=[1,0,0,3,6,9,9,0,3,6] #se asignan valores a la señal de entrada en este caso el numero de cedula 
h=[5,6,0,0,8,0,0] #se le asignan valores al sistema en este caso el codigo estudiantil 

x2=[1,0,1,1,3,2,1,6,7,3] #se asignan valores a la señal de entrada en este caso el numero de cedula 
h2=[5,6,0,0,7,9,8]#se le asignan valores al sistema en este caso el codigo estudiantil 

longitud=len(x)+len(h)-1 #se caclcula la longitud de la señal de salida sumando la longitud del sistemas mas la longitud de entrada menos uno 
y=[0]*longitud #se inicializa una lista llena de ceros porque inicialmente no sabemos la longitud al realizar la convolucion y se hce para facilitar los calculos

longitud2=len(x2)+len(h2)-1 #se caclcula la longitud de la señal de salida sumando la longitud del sistemas mas la longitud de entrada menos uno
y2=[0]*longitud2 #se inicializa una lista llena de ceros porque inicialmente no sabemos la longitud al realizar la convolucion y se hce para facilitar los calculos

for i in range(len(x)): #se utiliza un ciclo for para que valla recorriendo cada indice de la señal x 
    for j in range (len(h)):#se crea otro ciclo dentro del anteror para que valla recorrriendo cada indice del sistema h y se haga lo siguiente:
        y[i+j] += x[i]*h[j]#Aqui se le asigna cada valor a la señal de salida haciendo la convolucion de ir multiplicando cada indice de h por x y sumando los que tengan la misma posicion para sacar la señal de salida 
        
for u in range(len(x2)): # se hace lo mismo que en el for anterior para sacar la señal de salida del segundo sistema con la segunda señal de entrada 
    for x in range (len(h2)):
        y2[u+x] += x2[u]*h2[x]
 y(n):  [5, 6, 0, 15, 56, 81, 99, 78, 63, 120, 108, 0, 24, 48, 0, 0] resultado mostrado en python del primer integrante 
 y(n):  [5, 6, 5, 11, 28, 37, 32, 52, 109, 106, 67, 67, 111, 132, 83, 24] resultado mostrado en python del segundo integrante
print ("y(n): ",y) #Da los valores de la convolucion para la señal de salida 
print ("y(n): ",y2)# Da los valores de salida para la segunda convolucion
 y(n):  [5, 6, 0, 15, 56, 81, 99, 78, 63, 120, 108, 0, 24, 48, 0, 0] resultado mostrado en python del primer integrante 
 y(n):  [5, 6, 5, 11, 28, 37, 32, 52, 109, 106, 67, 67, 111, 132, 83, 24] resultado mostrado en python del segundo integrante
 
n= range (len(y)) # Se genera una secuencia de numeros desde cero hasta la longitud de la señal de salida para graficar la señal en el eje x
n2= range (len(y))

plt.stem(n, y)# Se ponen los datos que se almacenaron en en n y en y para crear la señal discreta con la funcion
plt.xlabel('n') #Da el nombre al eje x
plt.ylabel('y[n]') #Da el nombre al eje y 
plt.title('Convolución de x[n] y h[n]') #Da el titulo a la señal 
plt.grid(True) #Muestra la cuadricula del grafico 
plt.show()#Muestra la señal de salida graficada 

plt.stem(n2, y2) #se hace lo mismo que la anterior para graficar la señal discreta de salida 
plt.xlabel('n')
plt.ylabel('y[n]')
plt.title('Convolución de x[n] y h[n]')
plt.grid(True)
plt.show()
Grafica de la señal y[n] resultante de la convolucion en python para el primer integrante 
![image](https://github.com/user-attachments/assets/8be2bb54-658c-40c6-a004-491e5b506f59)
Grafica de la señal y[n] resultante de la convolucion en python para el segundo integrante 
![image](https://github.com/user-attachments/assets/6650c969-1f7c-48b7-b9a0-53b3544ee785)

#Correlacion entre dos señales dadas en la guia y su representación grafica 
f=100 # frecuencia que dan ambas señales 
Ts= 1.25e-3 #tiempo de muestreo que representa el intervalo de tiempo entre dos muestras consecutivas en la señal discreta 
nmuestras=np.arange(0,9) #Representa que el numero de muestras este entre o y 9 sin incluir el 9 

X1=np.cos(2*np.pi*f*Ts*nmuestras) #Se escribe cada señal matematicamente como se da en la guia 
X2=np.sin(2*np.pi*f*Ts*nmuestras)

correlacion=np.correlate(X1,X2, mode="full") #Se hace la correlacion usando la funcion con la libreria numpy entre las señales de salida x1 y x2 y se calculara en todas las posibles alinaciones para las señales  
ejes=np.arange(-len(X1)+1,len(X2)) #Representa el desplazamiento en el cual se calculo la correlación generando una secuencia de valores desde menos la longiud de X1 mas 1 hasta la longitud de X2 porque la correlación toma valores negativos en el eje y 

plt.figure(figsize=(12, 5)) #crea la figura con un ancho y un alto 

plt.subplot(2, 1, 1)#Selecciona la primera grafica para que salgan ambas señales en una misma grafica selecionando dos filas y una columna 
plt.stem(nmuestras, X1, linefmt='b-', markerfmt='bo', basefmt="r-") #La funcion dibuja valores discretos con lineas donde estan nmuestras valores del eje x y X1 valores del eje y 
plt.title("Señal x1[nTs] = cos(2π100nT_s)") # Da el titulo a la grafica 
plt.xlabel("n") #Nombre del eje x
plt.ylabel("Amplitud") #Nombre del eje y
plt.grid() # Muestra la cuadricula 

plt.subplot(2, 1, 2) #Selecciona la segunda grafica con la misma cantidad de filas y columnas 
plt.stem(nmuestras, X2, linefmt='g-', markerfmt='go', basefmt="r-") #Se pone g- para pintar azul cada linea y que quede solida osea que se note, go para los puntos azules circulares y r- para la linea rojo sobre todo el eje en cero 
plt.title("Señal x2[nTs] = sin(2π100nT_s)")
plt.xlabel("n")
plt.ylabel("Amplitud")
plt.grid()
plt.tight_layout()
plt.show()
![image](https://github.com/user-attachments/assets/e261adf0-8f42-468e-b4d1-bcddc00553fc)

plt.figure(figsize=(10, 5)) #Crea la figura con una altura y un ancho
plt.stem(ejes, correlacion, linefmt='m-', markerfmt='mo', basefmt="r-") #La funcion dibuja valores dscretos los cuales tienen los datos del eje x en eje y los datos del eje y en correlacion
plt.title("Correlación entre x1[nTs] y x2[nTs]") #Da el titulo al grafico 
plt.xlabel("Desplazamiento (ejes)") #Da el nombre al eje x
plt.ylabel("Amplitud de correlación") #Da el nombre al eje y 
plt.grid() #Dibuja la cuadricula 
plt.show()# Muestra el grafico que representa la correlación 
Representacion grafica de la correlacion entre la señal 𝑥1[𝑛𝑇𝑠] = cos(2𝜋100𝑛𝑇𝑠) y la señal 𝑥2[𝑛𝑇𝑠] = sin(2𝜋100𝑛𝑇𝑠) 
![image](https://github.com/user-attachments/assets/2a8852a6-e162-47b1-8993-b714874dbadb)
print ("valores de la correlacion") #Se muestran los valores de la correlacion 
for f in range (len(correlacion)): # Se utiliza un ciclo for para que valla recorriendo cada valor de la correlación y hacer lo siguiente:
    print ("-", ejes[f], "  " ,correlacion[f]) #Se va mostrando cada valor que tome la correlacion en su posicion 
valores de la correlacion dados en python 
- -8    -2.4492935982947064e-16
- -7    -0.7071067811865479
- -6    -1.5
- -5    -1.4142135623730947
- -4    4.1718400224935397e-16
- -3    2.121320343559643
- -2    3.5
- -1    2.8284271247461903
- 0    1.9915985002059197e-16
- 1    -2.82842712474619
- 2    -3.5
- 3    -2.121320343559643
- 4    -2.83276944882399e-16
- 5    1.414213562373095
- 6    1.5
- 7    0.7071067811865476
- 8    0.0
#Caracterizacion de la señal electromiografica de Señales electromiográficas de superficie recogidas durante la marcha prolongada sobre el suelo por parte de sujetos jóvenes sanos,
#El conjunto de datos se compone de señales electromiográficas de superficie (sEMG) de larga duración (alrededor de 5 minutos) registradas entre 2011 y 2018 durante la marcha en el 
#suelo de 31 sujetos jóvenes (20 años < edad < 30 años) sin discapacidad
archivo_hea = r'C:\Users\HP RY5\Desktop\Practica_1\\S10.hea' #Direecion de el archivo .hea
archivo_dat = r'C:\Users\HP RY5\Desktop\Practica_1\\S10.dat' #Direccion del archivo .dat
recorte = wfdb.rdrecord(r'C:\Users\HP RY5\Desktop\Practica_1\\S10' ) #lee los registros de la señal 
conversion = recorte.p_signal [:,0] #selecciona las filas de los datos pero solo la primera columna
fs=recorte.fs #Devuelve la frecuencia de muestreo en Hz, indica cuantas muestras por segundo se tomaron los datos

muestras=len(conversion) #Asigna a la variable muestras el numero total de elementos
Tiempo=np.arange(muestras)/fs

Fraccion=int (10*fs) #se almacena en la variable el numero de muestras correspondientes a 10 segundos por la multiplicacion de 10 por la frecuencia de muestreo y este debe ser un numero entero 
tiempo_10=Tiempo[:Fraccion] #Se describe el tiempo desde 0 hasta los 10 segundos que es la fraccion
señal_10=conversion[:Fraccion] #Describe los datos que hay durante ese tiempo de 10 segundos 
plt.figure(figsize=(10, 5))# se crea la imagen y Da el tamaño, el alto y el ancho 
plt.plot(tiempo_10,señal_10, label='Primeros 10 segundos')#dibuja el diagrama con las muestras correspondientes a los primeros 10 segundos, en el eje x el tiempo en s y en el eje y los valores que correnponden a cada tiempo en mv 
plt.title("Señal Fisiológica") # coloca el titulo del grafico
plt.xlabel("Tiempo (s)") #da el nombre del eje x 
plt.ylabel("Amplitud (mv)")# da el nombre del eje y 
plt.legend()# muestras el label de los primeros 10 segundos 
plt.grid() #muestra la cuadricula en el grafico 
plt.show() #muestra el grafico 
Grafica de la Señal Fisiologica descargada 
![image](https://github.com/user-attachments/assets/15a87605-5ef8-4730-91b6-e84f7027520a)
media=np.mean(Tiempo) #Se calcula la media de la señal fisiologica mediante la funcion
mediana=np.median(Tiempo) #Se calcula la median de la señal mediante la funcion
varianza=np.var(Tiempo) #Se calcula la varianza de la señal mediante la funcion 
desviacion=np.std(Tiempo) #se halla la desviacion utilizando la libreria 
coeficiente_variacion=(desviacion/media)*100 # Secalcula el coeficiente de variación mediante la formula 
print("la media de la señal es: ",media) #Muestra el valor de la media calculada anteriormente 
print("la mediana de la señal es: ",mediana) #Muestra la mediana de la señal calculada anteriormente 
print("la varianza de la señal es: ",varianza) #Muestra la varianza de la señal calculada anteriormente 
print("la desviacion estandar de la señal es: ",desviacion) #Muestra la desviacion de la señal calculada anteriormente 
print("el coeficiente de variacion es: ",coeficiente_variacion) #Muestra el coeficiente de variaacion de la señal calculada anteriormente
print("la frecuencia de muestreo es: ",fs)
VALORES DADOS EN PYTHON
la media de la señal es:  125.22000000000001
la mediana de la señal es:  125.22
la varianza de la señal es:  5226.703670000002
la desviacion estandar de la señal es:  72.29594504534816
el coeficiente de variacion es:  57.735142186031105
la frecuencia de muestreo es:  2000
Histograma
plt.figure(figsize=(10, 5)) #crea un grafico y se le da unas medidas a la imagen 
plt.hist(conversion, bins=60, color='purple', alpha=0.7) #dibuja el histograma el cual contiene la variable conversion el cual contiene los valores de la señal, el numero de columnas que se quieren en el histograma, el color y ajusta la opacidad de las barras
plt.title("Histograma de la Señal Fisiológica") #Da el nombre al grafico 
plt.xlabel("Amplitud (mV)") #nombre del eje x 
plt.ylabel("Frecuencia (Hz)") #nombre del eje y
plt.grid(True) #muestra la cuadricula 
plt.show() #muestra el grafico 
Hisograma de la señal fisiologica 
![image](https://github.com/user-attachments/assets/3bb5c4cb-f53d-4181-b537-62b85891c8c9)
ordenar_datos=np.sort(conversion)#se ordenan los datos de la señal lamcenados en conversion de menor a mayor 
funcion=np.arange(1,len(ordenar_datos)+1)/len (ordenar_datos) #se genera un arreglo con numeros desde el 1 al total de datos y se divide entre el numero de datos, esto indica la fracion del total de datos que son menores o iguales a cada valor en el arreglo ordenado 
plt.figure(figsize=(10, 5)) #crea la figura y le da un ancho y un alto 
plt.plot(ordenar_datos, funcion, marker='.', linestyle='none', color='green')#dibuja el digarma el cual tiene los datos ordenados, los datos de la variable funcion, se utiliza un punto para marcar cada valor y se establece un color a la grafica  
plt.title("Función de Probabilidad de la Señal Fisiológica con la libreria") #se le asigna un titulo al grafico 
plt.xlabel("Amplitud (mV)") #se le da nombre al eje x 
plt.ylabel("Probabilidad Acumulada") #se le nombre al eje y 
plt.grid(True) #muestra la cuadricula en la grafica 
plt.show()# muestra el grafico 
Funcion de probabilidad de la señal Fisiologica 
![image](https://github.com/user-attachments/assets/3e3cc9db-91d4-4d28-bcb2-92031d98e622)
Descripcion de la señal 
-Es una señal discreta o discontinua, pues presenta saltos abruptos en su amplitud,  Específicamente, parece ser una señal periódica, pues el patrón se repite regularmente después de los 6 segundos,  Después de los 6 segundos, presenta una forma de onda rectangular o cuadrada
-Está representada en el dominio del tiempo (eje X en segundos), La amplitud está medida en milivoltios (mV) en el eje Y
Transformada de Fourier De la señal 
ejefrecuencias=np.fft.fftfreq(muestras,d=1/fs) #Se calcula la frecuencia del eje en hz para la transformada de Fourier que son negaticas y positivas 
transformada= fft(conversion) #Se usa esa funcion para calcular la transformada de fourier de la señal 
plt.figure(figsize=(10, 4))# Se crea la imagen con una altura y un ancho 
plt.semilogy(ejefrecuencias[:muestras// 2], np.abs(transformada[:len(ejefrecuencias) // 2])) #Se dibuja la magnitud de la transformada en escala logaritmica y el eje x en escala lineal, se evitan las señales negativas y se toma sola la magnitud de la transformada sin la parte imaginaria 
#y se utiliza la funcion abs que devuelve la magnitud del numero complejo 
plt.xlabel("Frecuencia (Hz)") 
plt.ylabel("Magnitud")
plt.title("Transformada de Fourier de la Señal")
plt.grid()
plt.show()
Grafica de la transformada de Fourier de la señal 
![image](https://github.com/user-attachments/assets/ac3c259d-c894-458b-9ce3-eec5b6d28495)
s, Pxx = welch(conversion, fs, nperseg=1024)  # Cálculo de densidad espectra, se utiliza el metodo welch para graficar la densidad espectral, contiene la señal, la frecuencia de muestreo, Tamaño de cada segmento en los que se divide la señal, divide la señal en bloques de 1042 muestras 
#esto permite saber cómo se distribuye la energía de la señal en el dominio de la frecuencia.
#Es útil para analizar el contenido espectral de una señal fisiológica, de audio, etc.
plt.figure(figsize=(10, 4)) 
plt.semilogy(s, Pxx) #Grafica Pxx en función de s en escala logaritmica en el eje y 
plt.xlabel("Frecuencia (Hz)")
plt.ylabel("Densidad espectral de potencia")
plt.title("Densidad espectral de la señal")
plt.grid()
plt.show()
Grafica de la densidad espectral de la señal 
![image](https://github.com/user-attachments/assets/1b0affce-dd75-4bdc-ae9e-3313535d8ba7)







