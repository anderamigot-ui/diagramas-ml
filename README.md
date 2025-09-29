# Diagrama de Secuencia - Proyecto ML

```mermaid
sequenceDiagram
    participant User
    participant FileSystem as Archivos .s1p
    participant Preprocesado as Funciones Preprocesado
    participant Extraccion as Extracción de picos
    participant Dataset as DataFrame Pandas
    participant Modelo as RandomForest
    participant Visualizacion as Matplotlib

    User->>FileSystem: seleccionar_archivos_por_rangos()
    FileSystem->>Preprocesado: read_s1p_custom()
    Preprocesado->>Extraccion: extract_max_with_freq()
    Extraccion->>Dataset: Guardar características (max, freq)
    Dataset->>Modelo: fit(X_train, y_train)
    User->>Modelo: predict(X_test)
    Modelo-->>User: Predicciones (0/1)
    Modelo-->>User: Probabilidades (predict_proba)
    User->>Visualizacion: Graficar resultados
