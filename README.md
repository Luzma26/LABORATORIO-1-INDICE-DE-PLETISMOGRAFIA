# CALCULO DEL INDICE PLETISMOGRAFICO

**Luz Marina Valderrama-5600741.**

## INTRODUCCION

La fotopletismografía (PPG) es una técnica óptica no invasiva que permite detectar variaciones en el volumen sanguíneo periférico a partir de los cambios en la cantidad de luz absorbida o reflejada por los tejidos. La señal obtenida presenta una componente pulsátil asociada con el ciclo cardíaco, por lo que permite extraer características como la amplitud de pulso y el intervalo entre pulsaciones [1]. A partir de estas características se desarrolló el índice pletismográfico quirúrgico (SPI, Surgical Pleth Index), un indicador adimensional utilizado principalmente durante anestesia general para estimar cambios relacionados con la nocicepción y la respuesta autonómica frente a estímulos quirúrgicos [2]. El SPI combina información de la amplitud de la onda pletismográfica y del intervalo entre latidos, presentando valores entre 0 y 100, donde valores mayores representan una mayor respuesta nociceptiva o de estrés [2], [3]. En esta práctica se implementó un sistema de adquisición basado en un sensor óptico de reflectancia, Arduino y procesamiento en MATLAB, con el propósito de obtener la señal pletismográfica y calcular el SPI durante una prueba de reposo, una maniobra Cold Pressor Test (CPT) y un período posterior de recuperación. El CPT constituye un estímulo fisiológico capaz de producir activación simpática y cambios cardiovasculares, por lo que puede emplearse como estímulo experimental para evaluar la respuesta del sistema [4].
### Objetivo General: 
Desarrollar un sistema de medición continua del índice pletismográfico quirúrgico (SPI) en condiciones ambulatorias.
### Objetivos Específicos
• Reconocer las características fundamentales de la onda de pulso a partir de las cuales se obtiene el SPI.

• Construir un sistema que calcule el SPI en tiempo real y bajo condiciones ambulatorias.

• Validar el funcionamiento del sistema desarrollado mediante un método que induzca una respuesta fisiológica similar a la que produce el dolor agudo.

## MARCO TEORICO
### Fotopletismografia

La fotopletismografía es una técnica óptica utilizada para registrar variaciones de volumen sanguíneo en un tejido. Su funcionamiento se basa en iluminar el tejido mediante una fuente de luz y medir, mediante un fotodetector, las variaciones en la luz recibida como consecuencia de los cambios en la absorción y reflexión producidos por el flujo sanguíneo [5].

La señal PPG contiene una componente pulsátil, denominada componente AC, relacionada principalmente con las variaciones de volumen sanguíneo producidas por cada ciclo cardíaco, y una componente de baja frecuencia o DC relacionada con las características estáticas del tejido y otros factores fisiológicos [5]. Debido a esta relación con el ciclo cardíaco, la señal permite determinar características como los máximos de cada pulso, la amplitud de la pulsación y el intervalo entre pulsaciones.

Para el desarrollo de la práctica se utilizó la configuración de reflectancia, en la cual la fuente luminosa y el detector se encuentran ubicados en el mismo lado del tejido. Esta configuración permite obtener una señal relacionada con los cambios del volumen sanguíneo periférico del dedo.

### Indice plestismografico quirúrgico

El Surgical Pleth Index (SPI), inicialmente denominado Surgical Stress Index, fue desarrollado como un indicador basado en la señal pletismográfica para estimar cambios relacionados con el estímulo nociceptivo durante anestesia general [2]. El índice utiliza dos características principales de la señal: la amplitud de la onda pletismográfica (PPGA) y el intervalo entre latidos (HBI).

La formulación utilizada en esta práctica corresponde a:

SPI = 100 - (0.7PPGA{norm} + 0.3HBI{norm})

donde (PPGA{norm}) corresponde a la amplitud de pulso normalizada y (HBI{norm}) corresponde al intervalo entre latidos normalizado [2].

La normalización permite expresar ambas variables dentro de un rango común. De esta forma, el SPI obtenido también se encuentra entre 0 y 100. Un aumento del tono simpático puede producir vasoconstricción periférica y modificaciones de la frecuencia cardíaca, reduciendo la amplitud pletismográfica y el intervalo entre pulsaciones; estos cambios pueden conducir a un incremento del SPI [3].

En estudios perioperatorios se ha utilizado frecuentemente un intervalo aproximado de 20–50 como referencia de adecuada analgesia durante anestesia general, aunque este intervalo no debe interpretarse como un límite universal ni como una medida directa de la intensidad subjetiva del dolor [3], [6].

### Cold Pressor test

El Cold Pressor Test es una prueba fisiológica utilizada para provocar una respuesta cardiovascular mediante la exposición de una extremidad al frío. La aplicación del estímulo produce activación del sistema nervioso simpático, aumento de la resistencia vascular periférica y modificaciones de variables cardiovasculares como la frecuencia cardíaca y la presión arterial [4], [7].

En estudios experimentales, la inmersión de la mano en agua fría ha demostrado generar una respuesta simpática y modificaciones cardiovasculares medibles [4]. Por esta razón, el CPT puede emplearse como estímulo controlado para comprobar si un sistema basado en PPG es capaz de detectar cambios en la respuesta autonómica.

En la presente práctica se estableció una captura de 120 s dividida en tres períodos: los primeros 40 s correspondieron al reposo inicial, los siguientes 40 s a la aplicación del CPT y los últimos 40 s al período de recuperación.

### Materiales
Para la construcción del sistema se utilizaron los elementos indicados en la guía de laboratorio:

•  Arduino UNO o Arduino Nano.

•  Protoboard.

•  Sensor óptico TCRT1000.

•  Resistencias.

•  Amplificadores operacionales.

•  Potenciómetros para ajuste de la señal.

•  Cables de conexión.

•  Computador.

•  MATLAB.

•  Recipiente con agua fría para la aplicación del Cold Pressor Test.


El sensor óptico permitió transformar las variaciones del volumen sanguíneo periférico en una señal eléctrica. La señal fue acondicionada mediante el circuito construido en protoboard y posteriormente enviada a una entrada analógica del Arduino.

## METODOLOGIA
### Circuito de adquisicion

Inicialmente se construyó sobre la protoboard el circuito indicado en la guía de laboratorio para la captura de las variaciones del volumen sanguíneo periférico. El circuito permitió acondicionar la señal producida por el sensor óptico antes de ser enviada al Arduino.

Posteriormente, el TCRT1000 fue configurado como sensor óptico de reflectancia. En esta configuración, la emisión y detección de la luz se realizan sobre la misma superficie del dedo, permitiendo detectar cambios asociados con la cantidad de sangre presente en el tejido.

El dedo del participante fue ubicado sobre el sensor procurando mantener una posición estable durante la adquisición. Los potenciómetros del circuito se ajustaron para obtener una señal con una amplitud suficiente y con la menor interferencia posible.

### Adquisición mediante Arduino

La salida del circuito fue conectada a una entrada analógica del Arduino. El microcontrolador se encargó de realizar la lectura de la señal y enviarla mediante comunicación serial al computador.

La adquisición se configuró a una frecuencia aproximada de 100 muestras por segundo, utilizando una comunicación serial de 9600 baudios. El registro completo tuvo una duración de 120 s.

La comunicación entre Arduino y MATLAB se realizó mediante el puerto serial. MATLAB permite establecer una conexión mediante serialport, configurar el terminador de las cadenas y realizar lecturas mediante readline [8], [9].

### Organización temporal de la prueba

La prueba experimental se dividió de la siguiente manera:

0–40 s: reposo inicial.

40–80 s: aplicación del Cold Pressor Test.

80–120 s: recuperación.

Durante todo el procedimiento el dedo permaneció sobre el sensor para obtener una señal continua.

La aplicación del CPT permitió generar una respuesta fisiológica asociada con la activación simpática. Esta respuesta se esperaba reflejada en cambios de la amplitud de la señal pletismográfica y del intervalo entre pulsaciones.

### Procesamiento de la señal

Una vez adquirida la señal, MATLAB realizó inicialmente una eliminación de datos no válidos. Posteriormente se aplicó un suavizado mediante una media móvil de cinco muestras:

    senalSuave = movmean(senal,5);

El objetivo del suavizado fue reducir pequeñas fluctuaciones de la señal y facilitar la identificación de las pulsaciones.

Posteriormente se realizó la búsqueda de máximos y mínimos mediante comparación entre muestras consecutivas. Para evitar que pequeñas fluctuaciones fueran interpretadas como pulsaciones independientes, se estableció una separación mínima entre detecciones.

Los máximos identificados representaron los puntos principales de cada pulsación. A partir de dos máximos consecutivos se calculó el intervalo entre latidos:

HBI=t{i} - t{i-1}

La amplitud de cada pulsación se obtuvo mediante la diferencia entre el máximo de la pulsación y el mínimo correspondiente:

PPGA = PPG{max} - PPG{min}

La extracción de estas características es consistente con el procesamiento habitual de señales PPG, en las cuales los máximos y los intervalos entre pulsaciones permiten caracterizar la señal cardíaca [5].

### Normalización y cálculo del SPI

Después de obtener los valores de HBI y PPGA para cada pulsación, ambas variables fueron normalizadas mediante:

PPGA{norm}= 100 [PPGA - min(PPGA)] / [max(PPGA) - min(PPGA)]

HBI{norm} = 100 [HBI - min(HBI)] / [max(HBI) - min(HBI)]

Posteriormente se calculó el SPI para cada latido mediante:

SPI = 100 - (0.7PPGA{norm} + 0.3HBI{norm})

El resultado fue limitado al intervalo 0–100 para evitar valores fuera del rango establecido.

Finalmente, MATLAB mostró para cada latido el tiempo de ocurrencia, HBI, PPGA y SPI. También se calcularon los promedios correspondientes a las tres etapas experimentales.

### MATLAB
El programa desarrollado se organizó en diferentes etapas.

### Configuración

En primer lugar se definieron el puerto serial, la velocidad de comunicación, la frecuencia de muestreo y la duración total:

	puerto = "COM12";
	baud = 9600;
	Fs = 100;
	tiempoTotal = 120;

Esto permitió establecer las condiciones de adquisición antes de iniciar la comunicación con el Arduino.

### Captura

La conexión se estableció mediante:

	arduino = serialport(puerto,baud);
	configureTerminator(arduino,"LF");

Posteriormente se utilizaron lecturas sucesivas mediante readline para almacenar los datos provenientes del Arduino. MATLAB documenta este procedimiento para recibir datos ASCII desde un dispositivo conectado mediante puerto serial [8].

La señal y el tiempo correspondiente se almacenaron en los vectores senal y tiempo.

### Preprocesamiento

Los datos inválidos fueron eliminados y posteriormente se aplicó un promedio móvil:

	validos = ~isnan(senal);

	senal = senal(validos);
	tiempo = tiempo(validos);

	senalSuave = movmean(senal,5);

Esto permitió trabajar con una señal más estable para la identificación de pulsaciones.

### Detección de máximos y mínimos

El algoritmo recorrió la señal suavizada y comparó cada muestra con las muestras inmediatamente anterior y posterior. Si una muestra presentaba un valor superior a ambas, se clasificaba como máximo.

De manera equivalente, si presentaba un valor inferior a las dos muestras vecinas, se clasificaba como mínimo.

Además, se estableció una distancia mínima entre detecciones para reducir la aparición de múltiples máximos correspondientes a una misma pulsación.

### Obtención de HBI y PPGA

Con los máximos detectados se calcularon los intervalos entre latidos. Posteriormente se buscó el mínimo ubicado entre dos máximos consecutivos para determinar la amplitud de cada pulsación.

El código también estableció límites fisiológicamente razonables para HBI y descartó detecciones cuya amplitud resultara negativa.

### Cálculo del SPI

Finalmente, los valores obtenidos fueron normalizados y utilizados en la ecuación del SPI:

	SPI = 100 - (0.7*PPGA_n + 0.3*HBI_n);

Este procedimiento permite obtener un valor de SPI asociado a cada pulsación.

### Código de MATLAB

	clear;
	clc;
	close all;
	
	%% CONFIGURACION
	puerto = "COM12";
	baud = 9600;
	Fs = 100;
	tiempoTotal = 120;
	
	%% CONEXION CON ARDUINO
	arduino = serialport(puerto,baud);
	configureTerminator(arduino,"LF");
	flush(arduino);
	
	pause(2);
	
	%% CAPTURA DE LA SEÑAL
	N = Fs*tiempoTotal;
	
	senal = zeros(N,1);
	tiempo = zeros(N,1);
	
	disp("Iniciando captura...");
	disp("0-40 s: reposo");
	disp("40-80 s: CPT");
	disp("80-120 s: recuperacion");
	
	tic;
	
	for i = 1:N
	
	    dato = readline(arduino);
	    senal(i) = str2double(dato);
	    tiempo(i) = toc;
	
	end
	
	clear arduino;
	
	disp("Captura terminada.");
	
	%% ELIMINAR DATOS INVALIDOS
	validos = ~isnan(senal);
	
	senal = senal(validos);
	tiempo = tiempo(validos);
	
	%% SUAVIZADO
	senalSuave = movmean(senal,5);
	
	%% DETECCION DE MAXIMOS
	maximos = [];
	
	for i = 2:length(senalSuave)-1
	
	    if senalSuave(i) > senalSuave(i-1) && ...
	       senalSuave(i) > senalSuave(i+1)
	
	        if isempty(maximos) || ...
	           i-maximos(end) > 45
	
	            maximos(end+1) = i;
	
	        end
	    end
	end
	
	%% DETECCION DE MINIMOS
	minimos = [];
	
	for i = 2:length(senalSuave)-1
	
	    if senalSuave(i) < senalSuave(i-1) && ...
	       senalSuave(i) < senalSuave(i+1)
	
	        if isempty(minimos) || ...
	           i-minimos(end) > 45
	
	            minimos(end+1) = i;
	
	        end
	    end
	end
	
	%% CALCULO DE HBI Y PPGA
	HBI = [];
	PPGA = [];
	tiempoLatido = [];
	
	for i = 2:length(maximos)
	
	    hbi = tiempo(maximos(i)) - ...
	          tiempo(maximos(i-1));
	
	    minimo = minimos(minimos > maximos(i-1) & ...
	                     minimos < maximos(i));
	
	    if ~isempty(minimo)
	
	        m = minimo(end);
	
	        ppga = senalSuave(maximos(i)) - ...
	               senalSuave(m);
	
	        if hbi > 0.45 && hbi < 2.0 && ppga > 0
	
	            HBI(end+1) = hbi;
	            PPGA(end+1) = ppga;
	            tiempoLatido(end+1) = tiempo(maximos(i));
	
	        end
	    end
	end
	
	%% NORMALIZACION
	PPGA_n = 100*(PPGA-min(PPGA)) / ...
	              (max(PPGA)-min(PPGA));
	
	HBI_n = 100*(HBI-min(HBI)) / ...
	             (max(HBI)-min(HBI));
	
	%% CALCULO DEL SPI
	SPI = 100 - (0.7*PPGA_n + 0.3*HBI_n);
	
	SPI = max(0,min(100,SPI));
	
	%% MOSTRAR RESULTADOS
	disp(" ");
	disp("==============================================");
	disp("             RESULTADOS DEL SPI");
	disp("==============================================");
	
	for i = 1:length(SPI)
	
	    fprintf("Latido %d | Tiempo = %.2f s | HBI = %.3f s | PPGA = %.3f | SPI = %.2f\n", ...
	        i,tiempoLatido(i),HBI(i),PPGA(i),SPI(i));
	
	end
	
	%% GRAFICA DE LA SEÑAL
	figure;
	
	plot(tiempo,senal);
	hold on;
	
	plot(tiempo(maximos),senalSuave(maximos),'o');
	
	xline(40,'--k','Inicio CPT');
	xline(80,'--k','Fin CPT');
	
	xlabel("Tiempo (s)");
	ylabel("Señal Arduino");
	
	title("Señal pletismográfica adquirida");
	
	legend("Señal","Máximos");
	
	grid on;
	
	%% GRAFICA DEL SPI
	figure;
	
	plot(tiempoLatido,SPI,'-o');
	
	hold on;
	
	xline(40,'--k','Inicio CPT');
	xline(80,'--k','Fin CPT');
	
	xlabel("Tiempo (s)");
	ylabel("SPI");
	
	title("Evolución del SPI durante la prueba");
	
	ylim([0 100]);
	
	grid on;
	
	%% PROMEDIOS
	SPI_reposo1 = SPI(tiempoLatido < 40);
	
	SPI_CPT = SPI(tiempoLatido >= 40 & ...
	             tiempoLatido < 80);
	
	SPI_reposo2 = SPI(tiempoLatido >= 80);
	
	disp(" ");
	disp("==============================================");
	disp("             PROMEDIOS SPI");
	disp("==============================================");
	
	fprintf("Reposo inicial : %.2f\n",mean(SPI_reposo1));
	fprintf("CPT            : %.2f\n",mean(SPI_CPT));
	fprintf("Recuperacion   : %.2f\n",mean(SPI_reposo2));

### Adquisición y resultados 

La adquisición de la señal pletismográfica se realizó durante un periodo total de 120 s. El registro se dividió en tres etapas: un periodo inicial de reposo entre 0 y 40 s, un periodo correspondiente a la aplicación del Cold Pressor Test entre 40 y 80 s y un periodo final de recuperación entre 80 y 120 s. Durante toda la adquisición se mantuvo el dedo del participante sobre el sensor óptico, permitiendo registrar las variaciones del volumen sanguíneo periférico.

La señal obtenida presentó una componente pulsátil asociada con los cambios periódicos del volumen sanguíneo producidos por cada latido cardíaco. A partir de esta señal se identificaron los máximos y mínimos correspondientes a cada pulsación. Posteriormente, estos puntos fueron utilizados para obtener el intervalo entre latidos (HBI) y la amplitud de la onda pletismográfica (PPGA), variables necesarias para calcular el SPI [1], [2].

<img width="686" height="527" alt="image" src="https://github.com/user-attachments/assets/a3c8fe2a-75ad-4278-ac12-2c663532875d" />


Fig. 2. Señal pletismográfica registrada durante 120 s. Se muestran las variaciones de amplitud de la señal durante las etapas de reposo inicial, aplicación del Cold Pressor Test (CPT) y recuperación. Las líneas verticales permiten identificar los cambios entre las diferentes etapas de la prueba.

La señal presenta una variación pulsátil continua durante todo el registro. También se observan cambios en la amplitud de las pulsaciones a lo largo del tiempo, particularmente alrededor del periodo correspondiente al CPT. Estos cambios son relevantes debido a que la amplitud de la señal pletismográfica está relacionada con las variaciones del volumen sanguíneo periférico y puede modificarse ante cambios en el tono vascular [1].

<img width="692" height="521" alt="image" src="https://github.com/user-attachments/assets/85edc3b9-c218-43ff-8ef4-5fa51fd5986e" />


Fig. 3. Señal pletismográfica con los latidos detectados mediante el algoritmo de procesamiento. Los marcadores representan los máximos identificados en cada pulsación y permiten determinar el instante de ocurrencia de los latidos y calcular posteriormente el intervalo HBI.

La detección de los máximos permitió obtener los tiempos correspondientes a las pulsaciones. A partir de dos máximos consecutivos se calculó el HBI como la diferencia entre sus respectivos tiempos. De manera complementaria, los mínimos detectados permitieron estimar la amplitud de cada pulso mediante la diferencia entre el máximo y el mínimo correspondiente.

<img width="647" height="522" alt="image" src="https://github.com/user-attachments/assets/f2eb5021-5b7e-4daa-8670-44f89b42e144" />


Fig. 4. Evolución del índice pletismográfico quirúrgico (SPI) durante los 120 s de adquisición. Los puntos representan los valores calculados para cada latido y la línea de tendencia permite observar el comportamiento general del índice durante las etapas de reposo, CPT y recuperación.

La evolución del SPI muestra un incremento durante el periodo asociado al CPT respecto al periodo inicial. Posteriormente, durante la recuperación, el índice presenta una disminución progresiva, aunque con variaciones entre latidos.

### Resultados del calculo de SPI

Durante el procesamiento se identificaron 162 latidos a lo largo del registro de 120 s. Para cada latido se obtuvo el tiempo de ocurrencia, el intervalo HBI, la amplitud PPGA y el valor correspondiente del SPI.

Algunos valores obtenidos durante el procesamiento fueron:

Latido 1   | Tiempo = 1.70 s  | HBI = 0.870 s | PPGA = 0.504 | SPI = 48.94

Latido 2   | Tiempo = 2.41 s  | HBI = 0.710 s | PPGA = 0.696 | SPI = 35.69

Latido 3   | Tiempo = 3.16 s  | HBI = 0.750 s | PPGA = 0.748 | SPI = 25.99

Latido 64  | Tiempo = 50.13 s | HBI = 0.650 s | PPGA = 0.391 | SPI = 79.75

Latido 65  | Tiempo = 50.67 s | HBI = 0.540 s | PPGA = 0.432 | SPI = 82.52

Latido 81  | Tiempo = 61.41 s | HBI = 0.600 s | PPGA = 0.303 | SPI = 94.88

Latido 162 | Tiempo = 119.02 s| HBI = 0.710 s | PPGA = 0.708 | SPI = 34.05

El comportamiento global se evaluó mediante el promedio del SPI en cada etapa de la prueba. Durante los primeros 40 s, correspondientes al reposo inicial, se obtuvo un SPI promedio de:

SPI{reposo} = 35.31

Durante el periodo correspondiente al CPT se obtuvo:

SPI{CPT} = 64.09

Finalmente, durante la etapa de recuperación se obtuvo:

SPI{recuperación} = 48.19

La frecuencia cardíaca promedio calculada a partir de los intervalos entre latidos fue de:

FC{prom} = 83.39 latidos/min

El incremento entre el reposo inicial y el periodo CPT fue:

Delta SPI = 64.09-35.31 = 28.78

Por lo tanto, el SPI aumentó aproximadamente un 81.5 % con respecto al valor promedio del periodo inicial.

## Análisis de resultados

### Comportamiento del SPI durante el Cold Pressor Test

Los resultados muestran una diferencia clara entre las tres etapas de la adquisición. Durante el reposo inicial se obtuvo un SPI promedio de 35.31. Durante el CPT, el valor aumentó hasta 64.09, mientras que durante la recuperación disminuyó nuevamente hasta 48.19.

El aumento observado durante el CPT es compatible con la respuesta autonómica esperada frente a un estímulo frío. El Cold Pressor Test produce activación del sistema nervioso simpático y puede generar modificaciones en la presión arterial, frecuencia cardíaca y respuesta vascular periférica [3]. Además, se ha reportado que la respuesta al CPT puede presentar una considerable variabilidad entre individuos [3].

Desde el punto de vista de la señal utilizada en esta práctica, la respuesta tiene sentido debido a que el SPI combina información relacionada con la amplitud de la onda pletismográfica y el intervalo entre latidos. El SPI se encuentra definido como:

SPI = 100 - (0.7PPGA{norm} + 0.3HBI{norm}) 

donde (PPGA{norm}) corresponde a la amplitud pletismográfica normalizada y (HBI{norm}) al intervalo entre latidos normalizado [2], [4].

El SPI es un índice adimensional entre 0 y 100, donde valores mayores se relacionan con una mayor respuesta de estrés autonómico/nociceptivo [2], [4].

El comportamiento observado en la Figura 3 muestra que la respuesta no es completamente uniforme. Existen fluctuaciones importantes entre latidos, incluso dentro de una misma etapa. Esto puede deberse tanto a variaciones fisiológicas reales como a factores relacionados con la adquisición de la señal pletismográfica, como movimiento del dedo, presión sobre el sensor o cambios en la perfusión periférica [1].

### Comparación con valores utilizados durante cirugía

El SPI fue desarrollado principalmente para la monitorización de la nocicepción durante procedimientos quirúrgicos bajo anestesia general. En este contexto se han utilizado valores aproximadamente entre 20 y 50 como referencia de una condición de analgesia considerada adecuada [4], [5].

El valor promedio obtenido durante el reposo inicial, de 35.31, se encuentra dentro de este intervalo. Durante el CPT, en cambio, el promedio alcanzó 64.09, superando el rango de 20–50 utilizado habitualmente durante la monitorización intraoperatoria [4], [5].

Este comportamiento concuerda con el propósito de la práctica, ya que el estímulo del CPT busca producir una respuesta fisiológica que permita evaluar si el sistema es capaz de detectar cambios en la actividad autonómica.

Sin embargo, la comparación debe hacerse con cuidado. Los valores de referencia de SPI empleados durante una cirugía corresponden principalmente a pacientes sometidos a anestesia general y bajo condiciones clínicas controladas. En este laboratorio se analiza una respuesta fisiológica en condiciones ambulatorias, por lo que un SPI de 64.09 no puede interpretarse directamente como equivalente a un determinado nivel de dolor quirúrgico.

De hecho, diferentes revisiones señalan que el SPI puede responder a estímulos nocivos, pero también puede verse afectado por factores distintos de la nocicepción, por lo que no debe considerarse una medida aislada y absoluta de dolor [4].

### Alcance y limitaciones

El sistema desarrollado permite realizar una estimación continua de cambios en la respuesta autonómica a partir de una señal pletismográfica obtenida de manera no invasiva. Una de sus principales ventajas es que permite obtener información latido a latido utilizando un sensor óptico relativamente sencillo y posteriormente procesarla mediante MATLAB.

El sistema también permite extraer características específicas de la señal, como el tiempo entre pulsaciones y la amplitud de cada pulso. Estas variables constituyen la base del cálculo del SPI y permiten transformar la señal pletismográfica en un indicador numérico de respuesta fisiológica [2].

Sin embargo, el SPI no debe considerarse una medición directa de la percepción subjetiva del dolor. La señal pletismográfica puede verse modificada por diferentes factores fisiológicos y experimentales, incluyendo temperatura, movimiento, presión ejercida sobre el sensor, perfusión periférica y actividad autonómica no relacionada directamente con un estímulo doloroso [1], [4].

Otra limitación corresponde a la variabilidad de la respuesta individual frente al CPT. Se ha demostrado que la magnitud de la respuesta cardiovascular y autonómica frente a este estímulo puede variar considerablemente entre personas [3]. Por esta razón, los resultados obtenidos deben interpretarse principalmente como una demostración del funcionamiento del sistema y de su capacidad para detectar cambios fisiológicos.

Finalmente, el algoritmo de detección de máximos y mínimos depende de la calidad de la señal adquirida. Una señal con demasiado ruido, movimiento o cambios bruscos puede producir detecciones incorrectas y afectar el cálculo del HBI, PPGA y, por consiguiente, del SPI.

## CONCLUSION

El sistema desarrollado permitió medir de forma continua la señal pletismográfica y obtener el SPI a partir de las variaciones de amplitud y del intervalo entre latidos. Durante la prueba de 120 s se obtuvo un SPI promedio de 35.31 en reposo, 64.09 durante el Cold Pressor Test y 48.19 durante la recuperación, evidenciando una respuesta del índice ante el estímulo aplicado. Estos resultados muestran que el procesamiento implementado permite extraer características de la onda de pulso y cuantificar cambios en la respuesta fisiológica de manera no invasiva. Como siguiente paso, sería necesario realizar adquisiciones en un mayor número de participantes y bajo diferentes condiciones experimentales para evaluar la reproducibilidad de la respuesta y establecer con mayor precisión el alcance del SPI como indicador de cambios asociados a estímulos nociceptivos.

## REFERENCIAS

[1] J. Allen, “Photoplethysmography and its application in clinical physiological measurement,” Physiological Measurement, vol. 28, no. 3, pp. R1–R39, 2007. [Online]. Available: PubMed Central

[2] M. Huiku et al., “Assessment of surgical stress during general anaesthesia,” British Journal of Anaesthesia, vol. 98, no. 4, pp. 447–455, 2007, doi: 10.1093/bja/aem004. [Online]. Available: PubMed

[3] J. L. Wirch, L. A. Wolfe, T. L. Weissgerber, and G. A. L. Davies, “Cold pressor test protocol to evaluate cardiac autonomic function,” Applied Physiology, Nutrition, and Metabolism, vol. 31, no. 3, pp. 235–243, 2006, doi: 10.1139/h05-018. [Online]. Available: PubMed

[4] M. Ledowski et al., “Surgical pleth index monitoring in perioperative pain management: usefulness and limitations,” Journal of Clinical Monitoring and Computing, 2023. [Online]. Available: PubMed Central

[5] M. H. S. van den Oever et al., “Objective monitoring of nociception: a review of current commercial solutions,” Current Opinion in Anaesthesiology, vol. 33, no. 4, 2020. [Online]. Available: PubMed Central

[6] M. Ledowski et al., “The quantification and monitoring of intraoperative nociception levels in thoracic surgery: a review,” Journal of Thoracic Disease, 2019. [Online]. Available: PubMed Central

[7] GE HealthCare, Adequacy of Anesthesia: Surgical Pleth Index (SPI), GE HealthCare. El documento técnico de GE indica un rango objetivo de SPI de aproximadamente 20–50 como referencia de monitorización intraoperatoria.
Documento técnico de GE HealthCare

[8] M. M. R. F. Struys et al., “Changes in a surgical stress index in response to standardized pain stimuli during propofol-remifentanil infusion,” British Journal of Anaesthesia, vol. 99, no. 3, pp. 359–367, 2007, doi: 10.1093/bja/aem173.
Artículo en PubMed
