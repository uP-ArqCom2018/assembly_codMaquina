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
* 20=0b000000010100 => -20=0b111111101100 (Usamos 12 bits con los inmediatos)
