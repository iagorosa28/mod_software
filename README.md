# Modelagem de um sistema para uma locadora de veículos

> Status do projeto: Em andamento

> Este projeto nos foi proposto no 6º semestre na disciplina de Modelagem de Software Orientado a Objetos

> Escrevemos esse projeto juntos durante as aulas

### Tópicos

- [Apresentação](#apresentação)
- [Casos de uso](#casos-de-uso)
- [Diagrama de classes](#diagrama-de-classes)
- [Diagrama de sequência](#diagrama-de-sequência)

### Dados temporários

Atores: cliente, atendente, time do pátio, operador, sistema do DETRAN

Classes: Veículo, funcionário, cliente, locação, "multas", 

## Apresentação 

## Casos de uso
### Diagrama de Casos de Uso

![DiagramaCasosDeUso1 drawio](https://github.com/user-attachments/assets/dd40e553-8912-4f22-a0a3-304fb378ef0e)

### Tabelas de Casos de Uso
| Identificador          | UC_01                                                                                                     |
| :----------------------| :---------------------------------------------------------------------------------------------------------|
| Função                 | Verificar Cadastro                                                                                        |
| Atores                 | Cliente, Atendente                                                                                      |
| Prioridade             | Essencial                                                                                                 |     
| Pré-condição           | Cliente precisa informar o código                                                                         |
| Pós-condição           | Aprovação ou rejeição do cliente                                                                          |
| Fluxo Principal        | - O cliente informa seu código <br> - O atendente verifica se o cliente já possui cadastro (FS001, FS002) |
| Fluxo Secundário FS001 | - Se o cliente não possuir cadastro, o atendente realiza o procedimento                                   |
| Fluxo Secundário FS002 | - Após confirmar o cadastro do cliente, o atendente verifica se há locações pendentes do cliente (FS003)  |
| Fluxo Secundário FS003 | - Caso o cliente tenha locações pendentes, o atendente deve recusar a locação                             |

| Identificador   | UC_02                                                                               |
| :---------------| :-----------------------------------------------------------------------------------|
| Função          | Alugar veículo                                                                      |
| Atores          | Cliente, Atendente, Time do pátio e Sistema de pagamento                            |
| Prioridade      | Essencial                                                                           |     
| Pré-condição    | Cadastro do cliente liberado                                                        |
| Pós-condição    | Aluguel concluído                                                                   |
| Fluxo Principal | - Recepção do cliente na loja <br> - O cliente escolhe a categoria e o veículo que melhor atendem às suas preferências <br> - O cliente realiza o pagamento da locação do veículo por meio de um sistema externo de pagamento <br> - O time do pátio libera o veículo para o cliente |

| Identificador          | UC_03                                                                                                           |
| :----------------------| :---------------------------------------------------------------------------------------------------------------|
| Função                 | Verificar multas                                                                                                |
| Atores                 | Detran                                                                                                          |
| Prioridade             | Essencial                                                                                                       |     
| Pré-condição           | Devolução do veículo pelo cliente concluída                                                                     |
| Pós-condição           | Conclusão final da locação                                                                                      |
| Fluxo Principal        | - O sistema consulta o Detran para verificar se há multas pendentes no veículo utilizado pelo cliente (FS004)   |
| Fluxo Secundário FS004 | - Caso existam multas pendentes relacionadas ao veículo do cliente, o sistema deve notificar e cobrar o cliente |

## Diagrama de Classes

```mermaid
classDiagram
  Pessoa <-- Cliente
  Pessoa <-- Funcionario
  Funcionario "1" -- "0..*" Cliente : Cadastra
  Funcionario "1" -- "0..*" Locacao : Libera
  Cliente "1" -- "1" Locacao : Realiza
  Cliente "1" -- "1" Veiculo : Aluga
  Cliente "1" -- "1" Historico : Tem
  Historico "1" -- "1" Locacao : Pertence
  Historico "1" -- "0..*" Multa : Registra
  Veiculo "1" -- "1" Locacao : Pertence
  Veiculo "1" -- "0..*" Multa : Leva

  class Pessoa{
  - cpf string
  - dataDeNascimento date
  - nome string
  }

  class Cliente{
  - codigo string
  - nivelCategoria int
  + cadastrar()
  + verificarCadastro()
  + atualizarNivelCategoria()
  + verificarNivelCategoria()
  }

  class Funcionario{
  - desempenho float
  - ocupacao boolean
  - tipoFuncionario string
  + atualizarDesempenho()
  + verificarDesempenho()
  }

  class Historico{
  - multasAtivas boolean
  - locacaoPendente boolean
  - sequenciaLocacao int
  + atualizarHistorico()
  + consultarHistorico()
  }

  class Locacao{
  - valorLocacao float
  - valorAdicional float
  - dataInicio date
  - dataEntrega date
  - reservaSeguranca
  + atualizarValores()
  + registrarDatas()
  }

  class Veiculo{
  - categoria string
  - modelo string
  - placa string
  + registrarVeiculo()
  + mostrarInformacoes()
  + removerVeiculo()
  }

  class Multa{
  - placaVeiculo string
  - tipoMulta string
  - valorMulta float
  - dataMulta date
  + registrarMulta()
  + consultarMultas()
  }
```

## Diagrama de Sequência
### UC 01 - Verificar Cadastro
![Diagrama_S1 drawio (1)](https://github.com/user-attachments/assets/7ba4604d-5a57-4f0e-b9aa-5703d7490df0)

### UC 02 - Alugar veículo
![Diagrama_S2 drawio](https://github.com/user-attachments/assets/1c56c93e-767e-4ffc-988d-d9093aa29a60)

### UC 03 - Verificar multas
![DiagramaS3 drawio](https://github.com/user-attachments/assets/bbc10ffe-4a62-483c-a3ab-d23e42d0d110)

## Diagrama de Estados
### Funcionário (Objeto):
![DE1 drawio](https://github.com/user-attachments/assets/130219d5-8a62-489f-88a8-aa6b94b634b9)

### Cliente (Objeto):
![DE2 drawio](https://github.com/user-attachments/assets/78a2d43d-76c1-4f73-a29a-0c55cf0941d9)

### Verificação Multa (Ação do Sistema):
![DE3 drawio](https://github.com/user-attachments/assets/045a5b7d-fa61-4d98-911c-7565cde66bc8)

## Diagrama de Atividades
![DA1 drawio](https://github.com/user-attachments/assets/ebb57717-a098-4c9b-91f7-062e6eb63475)


![DA2 drawio](https://github.com/user-attachments/assets/f8f5afe4-b10f-45f6-b77b-95aa1bcf40d3)

### Diagrama de Atividades da parte de Consulta de Multas
![DE3 drawio (1)](https://github.com/user-attachments/assets/f9d06ca0-9ab6-4e0e-9121-4a8d94df6e10)

### Diagrama de Atividades de Todo o Sistema
![DA3 drawio](https://github.com/user-attachments/assets/b48a346f-ea7f-4569-9609-34dd787760fb)





