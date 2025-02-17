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
| Fluxo Principal | - O cliente informa seu código <br> - O atendente verifica se o cliente já possui cadastro (FS001, FS002) <br> |
| Fluxo Secundário FS001 | Se o cliente não possuir cadastro, o atendente realiza o procedimento <br> |
| Fluxo Secundário FS002 | Após confirmar o cadastro do cliente, o atendente verifica se há locações pendentes do cliente (FS003) <br> |
| Fluxo Secundário FS003 | Caso o cliente tenha locações pendentes, o atendente deve recusar a locação <br> |
