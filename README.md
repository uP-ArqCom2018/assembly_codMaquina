# Assembly resolución for.

Se debe resolver la siguiente iteración mediante assembly.
```
for(i=0;i<100;i++){
	x[i]=x[i]+2*i;
}
```
## Código assembly RISC-V
```
		addi X4,X0,100	--Carga de valor necesario para comparación
		addi X1,X0,0		-- tiempo contador de loop for 
loop:		lw X9,10(X1)    --carga el valor desde memoria
		slli X2,X1,1	--X2=2*X1
		add X9,X2,X9	--X9=X9+X2
		sw X9,10(X1)	--guardo X9 en memoria
		addi X1,X1,1		--X1=X1+1 sumo 1 a contador
		blt X1,X4,loop 	--salta si X1 es menor a 100
```