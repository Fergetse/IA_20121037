# Secuencia de percepción y medida de rendimiento

## Problema 1
Se describe la situación en la que un grupo de sujetos se numeran desde el 1 a n

## Problema 2
Se describe la situación en la que 100 prisioneros son tomados de uno en uno y se les pide encontrar su número en una matriz de 100 posibilidades, esto con el propósito de que encuentren el número que estos con **(1 -100)**, en la matriz estos números se acomodan de forma aleatoria, por lo que encontrar el número de un prisionero tiene una probabilidad de *1/100* , es importante destacar que cada prisionero tiene 50 oportunidades para encontrar su número, así mismo, la cantidad de posibilidades de elección que tiene un prisionero, tomando en cuanta las 100 posiciones y las 50 oportunidades de es aproximadamente *(100!/50!)*

Es posible reducir esta cantidad de elecciones si se sigue una estrategia que les permita seguir una línea dada. Por ejemplo.

* Si un prisionero es el número 5 que este vaya a la casilla número 5
* Una vez destapado el número se dirija a la casilla con el número que haya salido
	* Por ejemplo, si en la casilla 5 salió 9, que se dirija a la casilla 9 y así sucesivamente

Si bien esto mantiene una relación estadística más caótica, de 1/100, se mantiene como la original, pero desde otra perspectiva, la cantidad de posibilidades de selección mejora ya que habrá un sólo camino que seguir.

Si se toman estos factores en cuenta podemos calcular un valor promedio aproximado

En el segundo caso es un sólo camino de elección, por lo que directamente la probabilidad es de 1/100

Sin embargo en el primero además de la probabilidad de 1/100 se tiene el factor de elección al azar de 100!/50! que hace más caótico el proceso de elección

**CON BASE A LO DESCRITO, se establece que la secuencia de percepción es que cada individuo siga la estrategia descrita anteriormente y la medida de rendimiento es que cada prisionero encuentre su número en el rango de esas 50 oportunidades**



# CV2 for color vision

```python


import cv2 as cv

cap = cv.VideoCapture(0)
while(True):
    ret, img = cap.read()

    img2 = cv.cvtColor(img, cv.COLOR_BGR2HSV)
 
    if ret == True:
        cv.imshow('video2', img2)
        cv.imshow('video', img)

        ubb=(40,60,60)
        uba=(60, 255,255)

        #ubb1=(170,60,60)
        #uba1=(180,255,255)

        mask1 = cv.inRange(img2, ubb, uba)

        #mask2 = cv.inRange(img2, ubb1, uba1)

        mask3 = mask1 #+ mask2
        img3 = cv.bitwise_and(img,img, mask=mask3)

        cv.imshow('mask3', mask3)
        cv.imshow('img', img)
        cv.imshow('img3', img3)

        k =cv.waitKey(20) & 0xFF
        if k == 27 :
            break
    else:
        break
cap.release()
cv.destroyAllWindows()


```