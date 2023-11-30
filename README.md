# Euler_Method: 
import numpy as np
import matplotlib.pyplot as plt

##~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
def Euler_Method(dy_dx,x0,y0,xf,h):
    n = int((xf-x0)/h)
    
    listaX = [x0]   
    listaY = [y0]
    
    for i in range(n):
        x1 = x0 + h
        y1 = y0 + h * dy_dx(x0,y0)
        
        listaX.append(x1)
        listaY.append(y1)
        
        x0 = x1
        y0 = y1        
        
    return listaX,listaY
#~ Return ~
    #~ listaX, listaY: lista de valores de x y y respectivamente 
    
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
def dy_dx(x,y):
    ec = 0.0132*y 
    return ec

x0 = 0
y0 = 6*10**9
xf = 23
h1 = 2.3
h2 = 11.5

#~ Argumentos ~
    #~ dy_dx = f(x,y)
    #~ x0: valor inicial de x 
    #~ y0: valor inicial de y
    #~ h: tamaño del paso 
    #~ n: numero de nodos o integraciones

#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
listaX1,listaY1 = Euler_Method(dy_dx, x0, y0, xf, h1)
listaX2,listaY2 = Euler_Method(dy_dx, x0, y0, xf, h2)

def y(x):
    return (6*(10**9))*np.e**(0.0132*x )

plt.title("CURVAS SOLUCION")
plt.xlabel(" Tiempo ")
plt.ylabel(" Poblacion")
plt.plot(listaX1,listaY1,color='blue',label = 'h1 = '+ str(h1))
plt.plot(listaX2,listaY2,color='red',label = 'h2 = '+ str(h2))


x = np.linspace(x0,xf,1001)
plt.plot(x,y(x),color='black',label = 'Solución Analítica')

##~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#~ Presicion de las soluciones: comparando los ultimos valores de y(xf) para tener una medida del error cometido
    #~ soluciones numericas: ultimo valor de y en las listas de puntos
y_h1 = listaY1[-1]
y_h2 = listaY2[-1]
    #~ solucion analitica: evaluando y(1)
y_ana = y(1)

print("Solución analítica: ", y_ana)
print("Solución con paso h1: ", y_h1, ", Error:", np.abs((y_ana - y_h1)/y_ana)*100, "%")
print("Solucion con paso h2: ", y_h2, ", Error:", np.abs((y_ana - y_h2)/y_ana)*100, "%")

plt.legend(loc="upper left")
plt.show()
