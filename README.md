# Diagrama de Secuencia - Proyecto ML (versión detallada)

```mermaid
sequenceDiagram
    participant Usuario
    participant Sistema as Script Python
    participant FS as Archivos .s1p
    participant Preproc as Preprocesado S11
    participant Picos as Extracción de Picos
    participant Dataset as Dataset (Pandas)
    participant Modelo as RandomForest
    participant Visualizacion as Matplotlib

    Usuario->>Sistema: Ejecutar script
    Sistema->>FS: seleccionar_archivos_por_rangos()
    loop Archivos sin grieta
        Sistema->>Preproc: read_s1p_custom()
        Preproc->>Picos: extract_max_with_freq(S11, S11_ref)
        Picos-->>Sistema: Características [max_i, freq_i]
        Sistema->>Dataset: Guardar fila (label=0)
    end
    loop Archivos con grieta
        Sistema->>Preproc: read_s1p_custom()
        Preproc->>Picos: extract_max_with_freq(S11, S11_ref)
        Picos-->>Sistema: Características [max_i, freq_i]
        Sistema->>Dataset: Guardar fila (label=1)
    end

    Sistema->>Modelo: fit(X_train, y_train)
    Usuario->>Modelo: predict(X_test)
    Modelo-->>Usuario: Predicciones (0/1)
    Modelo-->>Usuario: Probabilidades (predict_proba)

    Usuario->>Visualizacion: Graficar resultados
