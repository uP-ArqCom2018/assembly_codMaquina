# Assembly resolución for.

Se debe resolver la siguiente iteración mediante assembly.
```
for(i=0;i<100;i++){
	x[i]=x[i]+2*i;
}
```
## Código assembly RISC-V
```
		addi X4,X0,100	--Carga de valor necesario para comparación 00 
		addi X1,X0,0	-- tiempo contador de loop for 			04	
loop:		lw X9,10(X1)    --carga el valor desde memoria			08
		slli X2,X1,1	--X2=2*X1									12
		add X9,X2,X9	--X9=X9+X2									16
		sw X9,10(X1)	--guardo X9 en memoria						20
		addi X1,X1,1	--X1=X1+1 sumo 1 a contador				24
		blt X1,X4,loop 	--salta si X1 es menor a 100				28
```
**Aclaraciones necesarias:**
* loop: debe ser igual a -20, para saltar a la instrucción que se encuentra en la posición 8.
* 20=0b000000010100 => -20=0b1111111101100 (Usamos 13 bits con los inmediatos)

## Codificación lenguaje de máquina
Se realiza el paso de assembly al código de máquina que se agrega en la memoria de programa.
```
addi	0000 0110 0100 0000 0000 0010 0001 0011 = x06400213
addi	0000 0000 0000 0000 0000 0000 1001 0011	= x00000093
lw		0000 0000 1010 0000 1010 0100 1000 0011 = x00A0A483
slli	0000 0000 0001 0000 1001 0001 0001 0011 = x00109113
add 	0000 0000 0010 0100 1000 0100 1011 0011 = x002484B3
sw 		0000 0000 1001 0000 1010 0101 0010 0011 = x0090A523
addi	0000 0000 0001 0000 1000 0000 1001 0011 = x00108093
bne 	1111 1110 0100 0000 1001 1011 1110 0011 = xFE409BE3
```

Como la memoria de programa tiene un ancho de palabra de 8 bits, el bloque a grabar en la misma debe ser el siguiente.
```
Pos | Dato
0	0000 0110 
	0100 0000 
	0000 0010 
	0001 0011
4	0000 0000 
	0000 0000 
	0000 0000 
	1001 0011	
8	0000 0000 
	1010 0000 
	1010 0100 
	1000 0011 
12	0000 0000 
	0001 0000 
	1001 0001 
	0001 0011 
16	0000 0000 
	0010 0100 
	1000 0100 
	1011 0011 
20	0000 0000 
	1001 0000 
	1010 0101 
	0010 0011 
24	0000 0000 
	0001 0000 
	1000 0000 
	1001 0011 
28	1111 1110 
 	0100 0000 
 	1001 0110 
 	1110 0011
```

 
 
Invierto la posición de los bytes para poder asignarla en la memoria de programa
 
 
```
11100011
10011010
01000000
11111110
10010011 
10000000 
00010000 
00000000
00100011
10100101
10010000
00000000
10110011
10000100
00100100
00000000
00010011
10010001
00010000
00000000
10000011
10100100
10100000
00000000
10010011
00000000
00000000
00000000
00010011
00000010
01000000 
00000110
```




