# Modelagem de um sistema para uma locadora de veículos

> Status do projeto: Em andamento

> Este projeto nos foi proposto no 6º semestre na disciplina de Modelagem de Software Orientado a Objetos

> Escrevemos esse projeto juntos durante as aulas

### Tópicos

- [Apresentação](#apresentação)
- [Casos de uso](#casos-de-uso)
- [Diagrama de classes](#diagrama-de-classes)

### Dados temporários

Atores: cliente, atendente, time do pátio, operador, sistema do DETRAN

## Apresentação 

## Casos de uso
### Diagrama de Casos de Uso

Identificação UC_01
Função Retirar Dinheiro do caixa eletrônico
Atores Cliente, Caixa eletrônico
Prioridade Essencial
Pré-condição Cliente precisa ter em mãos o cartão do
banco
Pós-condição Dinheiro sacado com sucesso
Fluxo
Principal

### Tabela de Casos de Uso
| Identificador   | UC_01                                                          |
| :---------------| :-----------------------------------------------------------------------------|
| Função          | Verificar Cadastro                                     |
| Atores          | Cliente, Atendente |
| Prioridade      | Essencial          |     
| Pré-condição    | Cliente precisa informar o código                                                          |
| Pós-condição    |  Verificação de cadastro                                                                   |
| Fluxo Principal | - Cliente deve informar seu código <br> - Atendente verifica se cliente já possui cadastro <br> - Se cliente não possuir cadastro, atendente cria um cadastro <br> - Se possuir cadastro, o atendente verifica se possui locações pendentes <br> - Se não possuir cadastro ou possuir locações pendentes a locação deve ser recusada |
