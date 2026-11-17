# Radar DT · Matriz de Avisos (Dwell Time)

Painel de priorização de HUs (unidades de carga) paradas no piso de um centro de fulfillment.
Protótipo construído para apresentar uma proposta de melhoria operacional à liderança.

**Demo:** https://radar-dt-matriz-avisos.netlify.app
(dados 100% fictícios, gerados no navegador)

## Problema

O alerta diário de retenção mostrava tudo junto. O operador ficava no dilema entre tratar carga
antiga de outro turno ou defender a saída iminente do turno atual. Em dias de pico, a atenção ia toda
para a saída imediata e as HUs retidas ficavam invisíveis, acumulando efeito "bola de neve".

## Solução

Um filtro que cruza dois eixos e classifica cada HU em 4 níveis:

| | Retenção acima do limite (6h) | Retenção normal |
|---|---|---|
| **CPT no turno atual** | DT-CRÍTICO: busca e bipagem imediata | DT-CPT: localização e direcionamento |
| **CPT em turno futuro** | DT-6H: tratar em janela de oportunidade | DT-OK: fluxo FIFO normal |

Regras extras:
- **CPT em até 60 min** (horário de saída do caminhão) vira DT-CRÍTICO, independente do tempo parado.
- **HU grande** (300+ pacotes) recebe destaque e vem primeiro dentro do seu nível.
- Limite de retenção, janela de CPT, corte de HU grande e horário dos turnos são configuráveis.

## Funcionalidades

- "Próximo aviso": a HU que deve ser tratada agora, com motivo e ação obrigatória
- Critério de aviso escolhido pelo operador: prioridade DT, mais antigas, maiores ou CPT mais próximo
- Modos de operação: visão completa, horário de pico (só CRÍTICO e CPT) e horário de oportunidade (DT-6H primeiro)
- Filtros por HU, posição, canalização, turno, pacotes e horas na posição
- Tempo na posição pisca em vermelho acima do limite; avisos em tempo real quando uma HU muda de nível
- Contagem de pendências por turno (T1, T2, T3) para cobrança justa entre turnos
- Histórico de movimentação da HU e exportação CSV da visão filtrada

## Stack

HTML, CSS e JavaScript puro em um único arquivo. Sem build, sem dependências.
Dados gerados com PRNG de semente fixa e tempos relativos ao relógio real, para a demo estar sempre "viva".

## Como rodar

Abrir `index.html` no navegador.
