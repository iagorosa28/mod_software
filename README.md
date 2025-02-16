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

![DiagramaCasosDeUso drawio](https://github.com/user-attachments/assets/9d54e305-bb7f-4529-aa2e-add22c9c3915)

### Tabela de Casos de Uso
| Identificador   | UC_01                                                          |
| :---------------| :-----------------------------------------------------------------------------|
| Função          | Verificar Cadastro                                     |
| Atores          | Cliente, Atendente |
| Prioridade      | Essencial          |     
| Pré-condição    | Cliente precisa informar o código                                                          |
| Pós-condição    |  Verificação de cadastro                                                                   |
| Fluxo Principal | - O cliente informa seu código FS001/FS002 <br> - O atendente verifica se o cliente já possui cadastro <br> - O atendente recepciona o cliente na loja <br> - O cliente escolhe a categoria do veículo <br> - O cliente realiza o pagamento do veículo por meio de um sistema de pagamento externo <br> - O cliente conclui a locação do veículo <br> - O time do pátio libera o veículo para o cliente <br> - Após a devolução do veículo, o sistema verifica a existência de infrações junto ao Detran FS004 <br> |
| Fluxo Secundário FS001| - Se o cliente não possuir cadastro, o atendente realiza o cadastro <br> |
| Fluxo Secundário FS002| - Se o cliente já possuir cadastro, o atendente verifica se há locações pendentes FS003 <br> |
| Fluxo Secundário FS003| - Se o cliente possuir locações pendentes, a locação deve ser recusada <br> |
| Fluxo Secundário FS004| - Caso existam infrações, o sistema realiza a cobrança do cliente <br> |
