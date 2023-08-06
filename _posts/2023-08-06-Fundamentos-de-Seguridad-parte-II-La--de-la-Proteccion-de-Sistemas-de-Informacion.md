---
layout: post 
title: "Fundamentos de Seguridad Parte II: La $aga de la Protección de Sistemas de Información"
date: 2023-08-06 17:15:04 +0100
categories: "Investigacion"
---
# Fundamentos de Seguridad Parte II: La $aga de la Protección de Sistemas de Información

# Un modelo comprensivo
Dicen que no es necesario re-inventar sistemas ya existentes y además, eficientes, es por eso que hoy trabajaremos con conceptos presentados por John R. McCumber en su paper "Information Systems Security: A Comprehensive Model" . John R. McCumber es un autor y experto en seguridad de la información, conocido por su contribución al campo de la seguridad informática y por su desarrollo de un modelo comprensivo de seguridad de sistemas de información. 
Su paper "Information Systems Security: A Comprehensive Model" fue publicado en 1991 en la revista "Computers & Security". Es un paper ampliamente reconocido y citado en la comunidad de seguridad informática debido a su enfoque en proporcionar una estructura que considere en su totalidad los sistemas de información para abordar su seguridad.
# ¿Información?
Comencemos definiendo qué es o con qué se come una información. Dado que el concepto  y la percepción de la "información" puede variar dependiendo del contexto que se utilice, definir qué es la información resulta ser una tarea, cuanto menos, complicada.
Hay para quienes la información se refiere a datos procesados y organizados de manera que tengan un significado o utilidad para quien los interpreta, para otros la información es lo que se comunica de una persona a otra o de frente a un receptor para transmitir conocimiento, ideas, hechos o detalles. La información puede referirse al conocimiento adquirido a través del estudio, la experiencia o la educación. Para otras personas la información se refiere a datos procesables por computadoras, datos estructurados que pueden ser utilizados por computadoras para realizar cálculos, análisis y toma de decisiones.
Es así como vemos que el __concepto__ y la __percepción__ de información es __bastante__ amplio, sin embargo, abordemos este problema desde otra perspectiva; más allá de preocuparnos por el concepto o percepción de la información, enfoquemos nuestros esfuerzos en comprender sus __estados__.

# Estados de la información
Para abordar los principios de los que hablaremos hoy, es necesario que tengamos en mente los distintos estados en los que la información se puede encontrar. Podemos observar estos posibles estados de la información: almacenamiento, transferencia y procesamiento. Podemos definir el procesamiento como una combinación especializada del almacenamiento y la transferencia así que en realidad tenemos dos posibles estados.
Por ejemplo la criptografía puede ser utilizada para proteger información mientras es transferida a través de una red de computadoras o incluso mientras está almacenada en dispositivos físicos. La información debe estar disponible en texto plano con la finalidad de que la computadora realice la función de procesamiento. La función de procesamiento es un estado fundamental que requiere de controles de seguridad particulares.

# Características fundamentales de la información
En lo que respecta a la seguridad de sistemas de información y su mantenimiento es importante tener en cuenta tres características de la información:
- Confidencialidad.
- Integridad.
- Disponibilidad
Estos atributos de la información representan el espectro completo de los temas de seguridad en entornos automatizados. Aplican para cualquier organización sin importar su enfoque filosófico en el intercambio de información.

# Confidencialidad
La confidencialidad es el corazón de cualquier política de seguridad para un sistema de información. Una política de seguridad es un conjunto de reglas que, en base a sujetos y objetos identificados, determina si un dado sujeto puede tener acceso a determinado objeto. En el caso de accesos de control y usuarios (o grupos) selectos, formados a gusto de la organización, son controlados a que datos pueden acceder. Confidencialidad es la garantía de que los accesos de control están asegurados.
Es así que podemos decir que la confidencialidad, representa un conjunto de reglas que evita que la información sensible sea revelada a personas no autorizadas. Métodos utilizados para garantizar esta confidencialidad incluyen el __cifrado de datos__, __autenticación__ y __controles de acceso__.

# Integridad
La integridad como característica de la información, tiende a ser compleja y malinterpretada. Comúnmente se define como activos los cuales pueden ser modificados solamente por partes autorizadas. Sin embargo este tipo de definiciones encasilla el concepto en la categoría de control de acceso.
John R. McCumber propone considerar la integridad de datos como algo más amplio, nos invita a ver la integridad de los datos como una serie de ayudas comprensivas para promover la exactitud (en medida de lo necesario), la completez, la relevancia y por supuesto la seguridad. 
Es decir, la integridad como característica de la información debe velar por que no existan datos redundantes, registros innecesarios, se debe buscar que los usuarios definan sus necesidades en terminos de la información requerida para realizar ciertas funciones. Se debe asegurar que la información sea robusta y, según sea requerido, la información refleje la realidad que esta orientada a representar.
Por supuesto también debemos garantizar que la información o los procesos se encuentran respaldados contra modificaciones intencionales o accidentales. Ejemplos de esto son funciones como comprobaciones de __hash__ o __suma de comparación__.

# Disponibilidad
Disponibilidad es una característica que comparte similitudes con la integridad y la confidencialidad. Este aspecto vital de la seguridad garantiza que la información es proporcionada a usuarios autorizados cuando y donde sea solicitada o necesitada. A menudo es vista como un requerimiento menos técnico que es satisfecho con redundancias dentro del sistema de infomación, como respaldo de suministro eléctrico, varios canales para transferencia de datos, y bases de datos paralelas.
Esta percepción ignora aspectos valiosos del modelo presentado por John R. McCumber. La disponibilidad permite el balance dentro de este modelo.
En última instancia asegurar la confiabilidad y disponibilidad de un sistema funciona como una métrica para determinar el alcance de las brechas de seguridad en sistemas de información. En ultima instancia, cuando un sistema de información es comprometido acción legal es requerida contra las personas que abusan de los recursos de un sistema de información, la habilidad de probar un impacto adverso a menudo depende en en la capacidad de negar a alguien la disponibilidad de los recursos de un sistema de información,
Las violaciones de de confidencialidad de información así como de su integridad pueden ser potencialmente más desastrosas, el criterio de negación de servicio permite hacer más sencillo la cualificación y por lo tanto crear bases tangibles para tomar acciones contra intrusos.

# Conclusiones
La triada Confidencialidad-Integridad-Disponibilidad trabaja en conjunto para proporcionar una base sólida de seguridad en sistemas de información. Cuando se implementan correctamente, estos principios ayudan a mitigar riesgos y a proteger la confidencialidad, integridad y disponibilidad de los datos y sistemas. En muchas estrategias de seguridad informática, la triada Confidencialidad-Integridad-Disponibilidad se considera un punto de partida esencial para diseñar políticas y controles de seguridad efectivos.

```
...me enseñarás todo lo que sabes, aunque no pueda recordar más me seguirás enseñando...
```
