# CLAP: **R**efuerzo impulsado por la curiosidad **A**prendizaje **A**utomático **A**gente de pruebas de intrusión

![](https://files.catbox.moe/784yxg.jpg)


`CLAP` es un [agente PPO](https://arxiv.org/abs/1707.06347) de aprendizaje por refuerzo que realiza [**Pruebas de penetración**](https://en.wikipedia.org/wiki/Penetration_test) en un entorno de red informática simulado (utilizamos el [Simulador de Ataques a Redes (NASim)](https://github.com/Jjschwartz/NetworkAttackSimulator)). El agente está entrenado para buscar vulnerabilidades en la red y explotarlas para obtener acceso a varios recursos de la red. 



## Entorno de Red Simulado: [Simulador de Ataque a Redes (NASim)](https://github.com/Jjschwartz/NetworkAttackSimulator)
Network Attack Simulator (NASim) es una red de ordenadores simulada completa con vulnerabilidades, escaneos y exploits diseñada para ser utilizada como entorno de pruebas para agentes de IA y técnicas de planificación aplicadas a pruebas de penetración de redes.

Sin embargo, en comparación con el documento original, este repositorio ha introducido los siguientes cambios

- Desarrollado en base a [CleanRL](https://github.com/vwxyzjn/cleanrl) 
- Añadir LSTM para escenarios POMDP
  - Como [Recurrent Model-Free RL Can Be a Strong Baseline for Many POMDPs](https://proceedings.mlr.press/v162/ni22a.html)
- Para apoyar NASim [espacio de observación 2D](https://networkattacksimulator.readthedocs.io/en/latest/reference/envs/environment.html), `Transformer` fue implementado como precepciones 
  - Sin embargo, son extremadamente inestables para entrenar
  - Para aprender más sobre el transformador enocder: [Ver Nota de Yekun](https://ychai.uk/notes/2019/07/21/RL/DRL/Decipher-AlphaStar-on-StarCraft-II/#Encoders)


`CLAP` aborda el problema de automatizar las pruebas de penetración en redes de seguridad utilizando el aprendizaje por refuerzo profundo (Deep Reinforcement Learning, RL). El objetivo es reducir el esfuerzo humano y mejorar la confiabilidad al emular a adversarios reales.

![](https://lh3.googleusercontent.com/fife/APg5EObWDg8doTIdhrWyUyIyB4zJ6qK4if0shGvuKFG4wxn-eui-LRYnPaBRMbcPTiy12RzuoPRkWnnFnn0R5vpzw4OA_vGq9XtM-7h53qplbEYhrMe18Vg8bVdNRcvGMKAYvLnQ1P70M_303deRgCfBGmyUGo2MUNi87SKQVym1NaPr7L0L75UMEmNRIaXFi0ll_O8FA7DAuAQTgs-Kl6xjHJcDDeUQSKbzom58ZknbTPuIDJ74NFDbyxDK3W2bmrKhXA9eBhKpEjVbBCFsoa03U-1dUu6I9MNM_Me0UvFv2d5jUzhZQ--VHQOrJBqHzzYhVC2Up6kacF9e8iyScXhaaM0CVee68JRIxdeMEjqcip0h5_Fyuf6489jraM4OcXFPnvp7aqSyMt1F0ktF5b7eCGpzbLZxL91YckRfRDeCoIBm_f_cGna9wBDonkyUcVG-d5wovWAsXXEiQ34LVbN7go2gM4BDiBdLQE6F89vwLRm_UWHN1WayhSTSA6ecc_-A1nD-yWzhiFGA8WluJDfC533RurN0TxBomR6er8b3XmIPVQXf2p_VERVa4AKFV3lu0EXwgybHapl5KHVwDEeQwtN4yZu_4CbISIEjJZBM6uJZEh1nq3GAxyWbddc4DQQO6lGzyasV1p6IpwUWD3ZHDoZbczDyD9L9W6k2a2tVTWtpqvElCGIxTb1Xo8RaS-V1TQ-iKCjWAu_6DeRDBA-MWqEvwdkedWdlzyxXxcVPD1vJYgQae8ZKsxC0y20p6NJU4BBpADXd5zkr_53xZKIitqS2TFE4JcQ4RKhKqhpTbVKQKuSu5oLS85P14hGjF4snPTOkvdMg_2jCwdcHy6Idn1rJih-R2sW-3WLsNnCvI7W83VWVFnOK0ETYHxv_qFemOY17LY3GrYrcfhE3zBCyvTu-nGP1fVkgyF-RPISxRBBPsnc855JKFrEmAAP7CAUYz31L78UjF4TKna_wKkM0s-ivdM_leKyZUo-baSUxQnKp-GuE-KhjoKsrChH4tu6SPWwSnCHWLJg2jNIq7xPUgbD17Lsg3vDLU-Sja47TdJczjUPnE4o-CAwwmEnar633M_k88GfOB3AICD80dIrrU1SEmqRTI7g4agpc23KTfbj5PcgRbv0RDpW4CYnOQGF4Dze-imTr9gd36abhh-57_5LWpL1Ht9BbH9wN7s_MhBzQpMJe7bMuwWqor6gNXt_v-o-Al_0IBpJGVxDMsdCJy_07oXABeMnadi_oMW7xR_7v5w7bmXsbqkAzlZjgv3GUDIj2bh5JkDSmT8Z4YRLubVHMkB2buBRLOxo8dT8-ZjNIKU0KNVbm_vU_MRmHVql1k2KTln0O_UFcX2xP7Kno5k67WFETHw6RaGq8HjGPeB0nVK-ko1oMGLyzjTe62wbM8T_ToMcCKTi2SHJihgPI0tGH-MeZrxF5B0C1x2lMx-Cow1pXfy_NCy4MGZvlMo-wR7qT5ovXh_oi3aRov2YJpo3kiQ=w1920-h975)
- Arquitectura de nuestro método propuesto. Las observaciones del agente atacante se alimentan a través de extractores MLP separados a la Red Actor-Crítico
y RND respectivamente. La distribución de cobertura se fusiona con la salida logits de la red de actores
<br>
- Aprendizaje profundo
  - Red neuronales profundas 
    - Actor
      - para generar la política de salida del agente
        - MLP Extractor   
        - Linear layers + ReLU
    -  Crítico
         - para calcular los valores intrínsecos y extrínsecos
           - MLP Extractor   
           - Linear layers + ReLU
   - Random Network Distillation (Destilación de redes aleatorias)
     - RND se utiliza como un componente clave para incentivar la exploración del agente de ataque en entornos con recompensas escasas. RND funciona generando dos redes neuronales aleatorias, una red predictor y una red objetivo
   
   - MLP Extractor: Multilayer Perceptron, que es un tipo de red neuronal artificial que se utiliza para el aprendizaje supervisado. MLP se utiliza como un componente del extractor, que es responsable de extraer características relevantes de los datos de entrada
   - Capas ReLU (Rectified Linear Unit), que son funciones de activación no lineales comúnmente utilizadas en redes neuronales profundas. 
   - La política de salida del agente:  es una estrategia que utiliza el agente para seleccionar acciones en función de su estado actual, y se entrena utilizando un marco DRL para maximizar una recompensa acumulativa a largo plazo.
   - Los valores intrínsecos son recompensas internas que se otorgan al agente por realizar acciones que lo acercan a una meta o logro intermedio dentro del entorno simulado. Estas recompensas son independientes de la tarea principal y se utilizan para fomentar la exploración y el aprendizaje en el agente.
   - Por otro lado, los valores extrínsecos son recompensas externas que se otorgan al agente por completar con éxito la tarea principal, es decir, realizar un ataque exitoso en el entorno simulado. Estas recompensas están directamente relacionadas con la tarea principal y se utilizan para guiar al agente hacia un comportamiento deseado.
     - En resumen, los valores intrínsecos y extrínsecos son dos tipos de recompensas utilizadas en el marco DRL de CLAP, donde los valores intrínsecos fomentan la exploración y el aprendizaje del agente, mientras que los valores extrínsecos están directamente relacionados con la tarea principal. La red neuronal "crítico" se utiliza para calcular ambos tipos de recompensas.
   - agente PPO se refiere a un agente de aprendizaje por refuerzo que utiliza el algoritmo de optimización de política proximal (PPO) para aprender a realizar tareas en un entorno simulado.
   - El algoritmo PPO es un método de aprendizaje por refuerzo que se utiliza para entrenar agentes en entornos complejos y dinámicos. Este algoritmo es "on-policy", lo que significa que utiliza la política actual del agente para recopilar datos y actualizar la política. 
   - La capa de fusión es una parte importante de una red neuronal que se utiliza para combinar información de diferentes fuentes y generar una salida única. En el contexto del marco CLAP (Control from Learning Action Policies), esta capa se utiliza para combinar la información generada por dos tipos diferentes de redes neuronales: una que determina acciones discretas y otra que determina acciones continuas.
