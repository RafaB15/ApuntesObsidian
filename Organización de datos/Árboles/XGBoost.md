- Boosting de árboles de decisión.
- Tiene una función objetivo
    
    $$
    Obj(\theta) = L(\theta) + \Omega(\theta)
    $$
    
    $\theta:$ parámetro a aprender
    
    $L:$ error del modelo
    
    $\Omega:$ factor de regularización
    

$$
L(\theta) = \sum_{i=1}^nl(y_i, \hat y_i)
$$

$l:$ es el error en la predicción de Y.

Para regresión puede ser → $l = (y_i - \hat y _i )^2$

Para clasificación binaria → $l = y_i \ln(1+ e^{- \hat y_i})+(1-y_i)\ln(i+e^{\hat y_i})$

- La predicción es la sumatoria de la predicción de varios árboles

$$
\hat y_i = \sum_{j=1}^k f_j(x_i)
$$

![[Organización de datos/Árboles/XGBoost/Untitled.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 1.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 2.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 3.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 4.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 5.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 6.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 7.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 8.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 9.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 10.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 11.png|Untitled]]

![[Organización de datos/Árboles/XGBoost/Untitled 12.png|Untitled]]

# Conclusión:

XGBoosting hace varios árboles, uno predice bien algunas cosas, entonces hace una predicción y cuando le da bien lo dejamos ahí, pero cuando le da mal se lo pasa a otro árbol para ver si ese predice bien. Algo así 😛