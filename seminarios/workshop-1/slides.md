# Slides do Workshop 1 – Introdução à Biomecatrônica

## Slide 1 – Capa e Introdução ao Workshop

**Título principal:** Introdução à Biomecatrônica: Conceitos, Tecnologias e Reabilitação.

**Subtítulo:** Workshop Integrado no IFRN Campus Parnamirim & Centros Especializados em Reabilitação (CER).

**Objetivos:**
- Unir conceitos de engenharia e mecatrônica com a prática clínica de reabilitação motora;
- contextualizar a biomecatrônica como área interdisciplinar;
- apresentar ferramentas e tecnologias aplicadas à saúde funcional.

---

## Slide 2 – Conceito e Origem da Biomecatrônica

**Definição:** Aplicação sinérgica da engenharia mecatrônica (mecânica, eletrônica, computação e controle) à biologia humana e à medicina.

**Abrangência:** A biomecatrônica vai além da robótica convencional, focando na restauração, no auxílio e na ampliação de funções corporais afetadas por lesões, amputações ou condições neurológicas.

---

## Slide 3 – Arquitetura de um Sistema Biomecatrônico

**Estrutura fundamental:**
- sujeito humano;
- sensoriamento;
- condicionamento de sinais;
- atuadores;
- malha de feedback.

**Integração homem-máquina:** foco na harmonização contínua entre o dispositivo robótico e o usuário.

---

## Slide 4 – O Sujeito Humano e a Complexidade Fisiológica

- O corpo humano apresenta comportamento não linear, dinâmico e individualizado.
- O sistema nervoso central e periférico transmite comandos bioelétricos.
- O sistema musculoesquelético fornece suporte mecânico e locomoção.

**Conclusão:** cada paciente exige uma abordagem específica, com atenção à variabilidade fisiológica e funcional.

---

## Slide 5 – Sensores Fisiológicos e Biomecânicos

### Sensores bioelétricos e acústicos
- Eletromiografia (EMG)
- Mecanomiografia (MMG)

### Sensores inerciais e de pressão
- IMUs como MPU-9250 e LSM6DS3
- medidas de ângulo, aceleração e orientação articular
- sensores FSR para medição de força e distribuição de pressão

---

## Slide 6 – Condicionamento e Processamento de Sinais

**Tratamento de dados:**
- amplificação;
- filtragem de ruído;
- conversão analógico-digital (ADC);
- análise e interpretação do sinal.

**Importância da resolução analógica:** conversores externos como ADS1115 permitem leituras mais precisas em sensores de força e resistência.

---

## Slide 7 – Atuadores e Elementos de Acionamento

**Sistemas de propulsão:**
- motores elétricos;
- servomotores de alto torque;
- atuadores pneumáticos ou hidráulicos.

**Geração de movimento:** aplicação de torque em articulações ou por cabos de tração flexíveis.

---

## Slide 8 – Estratégias de Controle em Malha Fechada

**Abordagem “Assistance-as-Needed”:**
- o dispositivo fornece assistência proporcional ao esforço residual do paciente;
- favorece a neuroplasticidade e a reabilitação funcional.

**Sistemas biocooperativos:**
- regulação contínua do dispositivo usando feedback em tempo real;
- algoritmos como PID ou lógica fuzzy.

---

## Slide 9 – Dispositivos de Reabilitação: Próteses e Exosqueletos

- membros biónicos;
- exoesqueletos;
- apoio em reabilitação de membros superiores e inferiores;
- recuperação funcional em pacientes pós-AVC ou com lesão medular.

**Objetivo:** melhorar a capacidade funcional e a autonomia do paciente.

---

## Slide 10 – Tecnologia Assistiva de Baixo Custo e Acessibilidade

**Prototipagem rápida:**
- microcontroladores (Arduino, ESP32);
- impressão 3D;
- desenvolvimento local e acessível.

**Parcerias institucionais:** integração entre o IFRN, CER e outros atores da rede de saúde e pesquisa.

---

## Slide 11 – A Nova Prática Motivacional Hands-On

### Estrutura das bancadas práticas

**Estação 1 – Goniometria Articular Eletrônica (ROM):**
- medição de amplitude de movimento com IMU MPU-9250;
- leitura em tempo real em LCD.

**Estação 2 – Mapeamento de Pressão Plantar e Preensão:**
- leitura de cargas plantares e força via FSR e ADS1115 de 16 bits.

**Estação 3 – Órtese Ativa e Garra Assistiva em Malha Fechada:**
- controle do servo MG946R por intenção de força ou inclinação.

---

## Slide 12 – Conclusão, Discussão e Próximos Passos

**Síntese:** conexão entre teoria e execução prática nas bancadas.

**Integração interdisciplinar:** alunos de tecnologia e profissionais de saúde podem colaborar em projetos futuros.

**Próximos passos:**
- aprofundar estudos em controle e sensores;
- estreitar parcerias clínicas;
- ampliar desenvolvimento de protótipos e projetos do GEB.

---

## Resumo da apresentação

A biomecatrônica conecta engenharia, saúde e reabilitação em sistemas inteligentes que interagem diretamente com o corpo humano. A partir de sensoriamento, processamento e atuação, é possível desenvolver soluções que ampliam a funcionalidade, o cuidado e a qualidade de vida de pessoas com necessidades específicas.
