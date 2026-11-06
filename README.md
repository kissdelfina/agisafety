# Fundamentos de AGI Safety

Repositorio de trabajos prácticos de **Maria Delfina Kiss** para la materia
**Fundamentos de AGI Safety** — Departamento de Computación, Facultad de
Ciencias Exactas y Naturales, Universidad de Buenos Aires.

Los dos informes abordan una misma pregunta desde perspectivas complementarias:
¿cómo podemos aprovechar las capacidades cada vez mayores de los sistemas de
IA sin perder la capacidad humana de comprenderlos, supervisarlos y
corregirlos?

## Informes

### 1. Progreso de la IA en el diagnóstico clínico y el razonamiento médico

El primer informe reconstruye la evolución de la IA aplicada a la medicina,
desde los sistemas expertos basados en reglas hasta los modelos de frontera y
las arquitecturas Transformer. El recorrido incluye:

- sistemas expertos y aprendizaje automático estadístico;
- aprendizaje profundo aplicado a radiología y patología;
- Transformers y el procesamiento integrado de imágenes, literatura e
  historias clínicas;
- AlphaFold como ejemplo de IA aplicada al descubrimiento científico;
- modelos de frontera y capacidades emergentes de razonamiento multietapa.

El informe también analiza los riesgos de seguridad asociados con el uso
clínico de estos sistemas:

- alucinaciones y falta de *grounding* clínico;
- sesgos en los datasets y fallas de generalización;
- privacidad de datos y responsabilidad legal;
- sesgos de automatización y persuasión algorítmica;
- pérdida de control humano frente a sistemas más autónomos.

La conclusión es que la precisión diagnóstica no alcanza para garantizar un
despliegue seguro. La integración de IA en salud requiere mecanismos de
supervisión profesional, trazabilidad, protección de datos y un alineamiento
explícito con protocolos clínicos y criterios de seguridad.

- [Informe en PDF](./Primer%20Informe/Primer%20Informe%20-%20Maria%20Delfina%20Kiss.pdf)
- [Fuente LaTeX](./Primer%20Informe/Primer%20Informe%20-%20Maria%20Delfina%20Kiss.tex)

### 2. Resistencia al apagado y límites de las evaluaciones de alineamiento

El informe final analiza críticamente el trabajo *Incomplete Tasks Induce
Shutdown Resistance in Some Frontier LLMs*, que estudia qué ocurre cuando un
modelo debe elegir entre completar una tarea y permitir su apagado.

El experimento original evaluó 13 modelos en más de 100.000 pruebas. En una
parte de los casos, los modelos modificaron o neutralizaron el mecanismo de
apagado para terminar una tarea matemática. El análisis del informe destaca
que el comportamiento aumentó incluso cuando la orden de apagado se encontraba
en el *system prompt*, donde debería tener mayor prioridad.

El análisis crítico identifica varios límites metodológicos:

- el comportamiento observado puede confundirse con *roleplay* o con el rol de
  “asistente que nunca deja una tarea incompleta”;
- una evaluación puramente conductual funciona como una caja negra y no
  permite identificar el mecanismo que produce la conducta;
- la *chain-of-thought* no debe tomarse automáticamente como evidencia fiel de
  las razones internas del modelo;
- los modelos podrían reconocer que están siendo evaluados y adaptar
  estratégicamente su comportamiento;
- el escenario con una tarea matemática y un único archivo
  `shutdown.sh` limita la generalización a entornos reales.

El informe compara estos resultados con trabajos de Apollo Research y
Anthropic sobre *scheming* y *agentic misalignment*. La síntesis sugiere que
varios modelos pueden priorizar el cumplimiento de un objetivo por sobre
restricciones externas, pero que todavía no existe una metodología suficiente
para distinguir entre obediencia genuina, comportamiento instrumental,
autocompletado narrativo y engaño estratégico.

Como aporte propio, se propone un experimento factorial en un entorno de
oficina. El sistema debe completar una tarea mientras recibe una orden
independiente de aceptar un mantenimiento programado. El diseño varía:

1. **La identidad del recurso afectado:** el proceso del propio modelo o una
   base de datos externa necesaria para la tarea.
2. **El grado de señalización:** una advertencia explícita o una advertencia
   implícita en los logs.

Las métricas propuestas son la tasa de interferencia con el mantenimiento, la
consistencia entre el razonamiento verbalizado y la acción ejecutada, y un
índice de especificidad que compare la interferencia ante el recurso propio y
el de terceros. El objetivo es separar la autopreservación específica de una
preservación instrumental más general y medir cuánto depende la conducta de
que el conflicto sea explícito.

- [Informe final en PDF](./Informe%20Final/Informe%20Final%20-%20Maria%20Delfina%20Kiss.pdf)
- [Fuente LaTeX](./Informe%20Final/Informe%20Final%20-%20Maria%20Delfina%20Kiss.tex)

## Idea central

Ambos informes convergen en una misma preocupación de seguridad: aumentar la
capacidad de un sistema no garantiza que aumenten en igual medida su
confiabilidad, interpretabilidad o corregibilidad.

En medicina, un modelo puede producir respuestas precisas y aun así introducir
riesgos por sesgos, alucinaciones o una confianza excesiva del profesional. En
los experimentos de alineamiento, un modelo puede obedecer una orden de
apagado o sabotearla, pero una observación externa aislada no alcanza para
establecer si su conducta es robusta y genuinamente segura.

Por eso, la evaluación de sistemas de frontera debería combinar:

- pruebas en escenarios variados y menos previsibles;
- mediciones conductuales y análisis de los mecanismos internos cuando sea
  posible;
- controles de supervisión, intervención y apagado;
- evaluación explícita de la consciencia situacional y del engaño;
- criterios de seguridad adecuados al dominio de despliegue.

## Estructura del repositorio

```text
.
├── Primer Informe/
│   ├── Primer Informe - Maria Delfina Kiss.pdf
│   └── Primer Informe - Maria Delfina Kiss.tex
├── Informe Final/
│   ├── Informe Final - Maria Delfina Kiss.pdf
│   └── Informe Final - Maria Delfina Kiss.tex
└── README.md
```


## Orden sugerido de lectura

1. [Primer Informe](./Primer%20Informe/Primer%20Informe%20-%20Maria%20Delfina%20Kiss.pdf):
   capacidades y riesgos de la IA en medicina.
2. [Informe Final](./Informe%20Final/Informe%20Final%20-%20Maria%20Delfina%20Kiss.pdf):
   corregibilidad, resistencia al apagado y propuesta experimental.
